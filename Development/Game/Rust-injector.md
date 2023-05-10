---
title: Rust Injector
description: 
published: true
date: 2023-05-10T07:03:33.444Z
tags: security, injector, dll, dll-injection
editor: markdown
dateCreated: 2023-05-10T07:03:33.444Z
---

# Injection Code
```rust
use std::{io::{stdin, }, ffi::c_void};

use argh::FromArgs;
use color_eyre::{Report, eyre::eyre};
use u16cstr::{u16cstr, };

use widestring::U16String;
use windows::{
    core:: {PCWSTR, PCSTR, PWSTR},
    Win32::{
        //Foundation::{HANDLE},
        System::Threading::{
            OpenProcess, 
            PROCESS_QUERY_INFORMATION, 
            PROCESS_CREATE_THREAD, PROCESS_VM_OPERATION, PROCESS_VM_READ, PROCESS_VM_WRITE, CreateRemoteThread,
        },
        System::{Memory::{
            VirtualAllocEx, MEM_COMMIT, PAGE_EXECUTE_READWRITE, MEM_RESERVE
        }, LibraryLoader::GetProcAddress, Diagnostics::Debug::{FormatMessageW, FORMAT_MESSAGE_FROM_SYSTEM, FORMAT_MESSAGE_IGNORE_INSERTS}},
        System::{Diagnostics::Debug::{
            WriteProcessMemory,
        }, Memory::{MEMORY_BASIC_INFORMATION, VirtualQueryEx, MEM_FREE,}},
        System::LibraryLoader::{
            GetModuleHandleW,
        }, Foundation::GetLastError
    },
};

#[link(name = "kernel32")]
extern "C" {
    fn TerminateProcess();
}

#[derive(FromArgs, Debug)]
/// Reach new heights.
struct Args {
    /// whether or not to jump
    #[argh(positional)]
    pid: u32,
}


fn main() -> Result<(), Report>{
    color_eyre::install()?;
    let args: Args = argh::from_env();
    unsafe { do_crimes(args) }
}

/*
unsafe extern "system" fn entry(_param: *mut c_void) -> u32 {
    println!("entry point");
    0
}
 */

unsafe fn do_crimes(args: Args) -> Result<(), Report>{
    let kernel32 = GetModuleHandleW(PCWSTR(u16cstr!("kernel32.dll").as_ptr())).ok()?;
    let tproc = GetProcAddress(
        kernel32, 
        PCSTR("TerminateProcess\0".as_ptr())
    ).ok_or(eyre!("TerminateProcess not found!"))? as *const ();

    println!("TerminateProcess address: {tproc:p}");

    let pid = args.pid;

    let access = PROCESS_CREATE_THREAD 
                        | PROCESS_QUERY_INFORMATION 
                        | PROCESS_VM_OPERATION 
                        | PROCESS_VM_READ 
                        | PROCESS_VM_WRITE;
    let proc = OpenProcess(access, false, pid).ok()?;
    println!("Opened process {proc:?}");

    let mut mem_info: MEMORY_BASIC_INFORMATION = std::mem::zeroed();
    {
        let mut probe_addr = tproc as *const c_void;

        loop {
            println!("Is {probe_addr:p} in an already-allocated region?");

            //let mut mem_info: MEMORY_BASIC_INFORMATION = std::mem::zeroed();
            let ret = VirtualQueryEx(
                proc,
                probe_addr, 
                &mut mem_info, 
                std::mem::size_of_val(&mem_info)
            );
            if ret == 0 {
                break;
            }

            probe_addr = mem_info.BaseAddress.add(mem_info.RegionSize as _);
        }
    }

    //let mut wanted_addr = tproc as *const c_void;
    println!("Last memory region: {mem_info:#?}");
    assert_eq!(mem_info.State, MEM_FREE);
    let wanted_addr = mem_info.BaseAddress.add(0x1_0000);
    println!("Allocating at addr {wanted_addr:p}");

    let ret = VirtualQueryEx(proc, wanted_addr, &mut mem_info, std::mem::size_of_val(&mem_info));
    assert!(ret != 0);
    println!("That's in this region : {mem_info:#?}");

    let target_addr = VirtualAllocEx(proc, wanted_addr, 
        1024, MEM_RESERVE | MEM_COMMIT, PAGE_EXECUTE_READWRITE,);

    //assert!(!target_addr.is_null());
    if target_addr.is_null() {
        return Err(get_last_error());
    }

    let mut src: Vec<u8> = vec![
        //0xb8, 0x2c, 0x00, 0x00, 0x00,
        //0x49, 0xc7, 0xc2, 0xff, 0xff, 0xff, 0xff,
        //0x48, 0xc7, 0xc2, 0x4d, 0x00, 0x00, 0x00,
        //0x45, 0x05,
        //0xf4,
        0x48, 0x83, 0xec, 0x28, // sub rsp, 0x28
        0x48, 0xc7, 0xc1, 0xff, 0xff, 0xff, 0xff, // mov rcx, -1
        0x48, 0xc7, 0xc2, 0x70, 0x00, 0x00, 0x00, // mov rdx, 112
        0xe8,
        //0xe8, 0x00, 0x00, 0x00, 0x00, // call TerminateProcess
        //0xf4, // hlt
        ];

    let next_instruction_rip = target_addr.add(src.len() as usize + 4);
    println!("{target_addr:p} code starts");
    println!("{next_instruction_rip:p} next instruction");
    println!("{tproc:p} kernel32 TP");
    let displacement = (tproc as *const u8).offset_from(next_instruction_rip as _ ) as i32; 
    println!("{displacement} relative displacement");
    src.extend(displacement.to_le_bytes());
    src.push(0xf4);

    println!("F {src:02x?}");

    let mut written = 0;
    WriteProcessMemory(
        proc,
        target_addr,
        src.as_ptr() as _,
        src.len(),
        &mut written,
    ).ok()?;
    assert_eq!(written, src.len() as _);

    println!("Address of TerminateProcess: {:p}", TerminateProcess as *const());
    println!("Wrote program to {target_addr:p}, press enter to wreak havoc...");
    stdin().read_line(&mut String::new())?;

    let mut tid: u32 = 0;
    let thread = CreateRemoteThread(
        proc, 
        std::ptr::null(), 
        0, 
        Some(std::mem::transmute(target_addr)), 
        std::ptr::null(), 
        0, 
        &mut tid
    ).ok()?;

    println!("Created thread {thread:?}, tid = {tid:?}");

    //let full_name = query_full_process_image_name(process, PROCESS_NAME_WIN32)?;
    //println!("process {pid} has image name {full_name}");

    Ok(())
}

unsafe fn get_last_error() -> Report {
    let error_code = GetLastError().0;

    let mut buf = vec![0u16, 16384];
    let len = FormatMessageW(
        FORMAT_MESSAGE_FROM_SYSTEM |FORMAT_MESSAGE_IGNORE_INSERTS, 
        std::ptr::null(), 
        error_code, 
        0, PWSTR(buf.as_mut_ptr()), buf.len() as _,
        std::ptr::null_mut(),
    ) as usize;
    buf.truncate(len);
    let message = U16String::from_vec(buf).to_string_lossy();
    eyre!("Win32 Error 0x{error_code:x} ({error_code}): {message}")
}
```

# Execute
```powershell
$proc = Start-Process -Passthru {$process_name}; Sleep 1; cargo run -- $proc.Id ; Wait-Process -Id $proc.Id; $proc.ExitCode
```

# Reference
## This docs
[I'm in ur address space](https://www.youtube.com/watch?v=xN5WjaeeklA) - fasterthanlime
## Watch Later...
[Getting good at SNES games through DLL injection](https://www.youtube.com/watch?v=Yr9qy9reLCc&t=1028s) - fasterthanlime