---
title: SharpMonoInjector
description: 
published: true
date: 2023-05-10T05:40:23.017Z
tags: security, unity, mono, injector
editor: markdown
dateCreated: 2023-05-10T05:40:23.017Z
---

# SharpMonoInjector.Console
## Main
- CMD 에서 인자 Parsing
- Injector 클래스 : IDisposable 
   - 프로세스명(또는 PID)으로 대상 타겟 확인
   - kernel32.dll을 import하여 OpenProcess 호출
      - 프로세스 ptr에 저장 
   - mono.dll을 찾아서, lpBase 를 ptr에 저장
- Inject Func 호출

## Inject
- 주입 대상 assembly 파일 전체 Read
   - 파일의 namespace 확인
   - class name 확인
   - method name 확인
- Injector.Inject 호출
   - 프로세스내 mono.dll 에서 Function Export (`ObtainMonoExports()`)
      - { mono_get_root_domain, IntPtr.Zero }
      - { mono_thread_attach, IntPtr.Zero }
      - { mono_image_open_from_data, IntPtr.Zero }
      - { mono_assembly_load_from_full, IntPtr.Zero }
      - { mono_assembly_get_image, IntPtr.Zero }
      - { mono_class_from_name, IntPtr.Zero }
      - { mono_class_get_method_from_name, IntPtr.Zero }
      - { mono_runtime_invoke, IntPtr.Zero }
      - { mono_assembly_close, IntPtr.Zero }
      - { mono_image_strerror, IntPtr.Zero }
      - { mono_object_get_class, IntPtr.Zero }
      - { mono_class_get_name, IntPtr.Zero }
   - kernel32.dll 을 import하여 CreateRemoteThread 호출
   - 재조합
   ```cs 
        public IntPtr Inject(byte[] rawAssembly, string @namespace, string className, string methodName)
        {
            if (rawAssembly == null)
                throw new ArgumentNullException(nameof(rawAssembly));

            if (rawAssembly.Length == 0)
                throw new ArgumentException($"{nameof(rawAssembly)} cannot be empty", nameof(rawAssembly));

            if (className == null)
                throw new ArgumentNullException(nameof(className));

            if (methodName == null)
                throw new ArgumentNullException(nameof(methodName));

            IntPtr rawImage, assembly, image, @class, method;

            ObtainMonoExports();
            _rootDomain = GetRootDomain();
            rawImage = OpenImageFromData(rawAssembly);
            _attach = true;
            assembly = OpenAssemblyFromImage(rawImage);
            image = GetImageFromAssembly(assembly);
            @class = GetClassFromName(image, @namespace, className);
            method = GetMethodFromName(@class, methodName);
            RuntimeInvoke(method);
            return assembly;
        }
   ```
   - 주입 대상 assembly를 원본 mono.dll 과 바인딩
   ```cs
        private IntPtr Execute(IntPtr address, params IntPtr[] args)
        {
            IntPtr retValPtr = Is64Bit
                ? _memory.AllocateAndWrite((long)0)
                : _memory.AllocateAndWrite(0);

            byte[] code = Assemble(address, retValPtr, args);
            IntPtr alloc = _memory.AllocateAndWrite(code);

            IntPtr thread = Native.CreateRemoteThread(
                _handle, IntPtr.Zero, 0, alloc, IntPtr.Zero, 0, out _);

            if (thread == IntPtr.Zero)
                throw new InjectorException("Failed to create a remote thread", new Win32Exception(Marshal.GetLastWin32Error()));

            WaitResult result = Native.WaitForSingleObject(thread, -1);

            if (result == WaitResult.WAIT_FAILED)
                throw new InjectorException("Failed to wait for a remote thread", new Win32Exception(Marshal.GetLastWin32Error()));

            IntPtr ret = Is64Bit
                ? (IntPtr)_memory.ReadLong(retValPtr)
                : (IntPtr)_memory.ReadInt(retValPtr);

            if ((long)ret == 0x00000000C0000005)
                throw new InjectorException($"An access violation occurred while executing {Exports.First(e => e.Value == address).Key}()");

            return ret;
        }
   ```
   
# Sample dll 주입
## Loader.cs
- 실행하는 게임의 유니티 오브젝트를 가져옴
- 아래 Cheat.cs 의 컴포넌트를 호출하여 gameObject에 Attach
```cs
namespace ExampleAssembly
{
    public class Loader
    {
        static UnityEngine.GameObject gameObject;

        public static void Load()
        {
            gameObject = new UnityEngine.GameObject();
            gameObject.AddComponent<Cheat>();
            UnityEngine.Object.DontDestroyOnLoad(gameObject);
        }

        public static void Unload()
        {
            UnityEngine.Object.Destroy(gameObject);
        }
    }
}

```

## Cheat.cs
```cs
namespace ExampleAssembly
{
    public class Cheat : UnityEngine.MonoBehaviour
    {
        private void OnGUI()
        {
            UnityEngine.GUI.Label(new UnityEngine.Rect(10, 10, 200, 40), "This is a very useful cheat");
        }
    }
}
```

## Compile Option
- 최신 버젼의 dotnet 사용으로, 일부 컴파일 옵션을 변경해야한다.
```xml
<!--?xml version="1.0" encoding="utf-8"?>
<Project ToolsVersion="14.0" DefaultTargets="Build" xmlns="http://schemas.microsoft.com/developer/msbuild/2003">
  <Import Project="$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props" Condition="Exists('$(MSBuildExtensionsPath)\$(MSBuildToolsVersion)\Microsoft.Common.props')" /-->
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <Configuration Condition=" '$(Configuration)' == '' ">Debug</Configuration>
    <Platform Condition=" '$(Platform)' == '' ">AnyCPU</Platform>
    <ProjectGuid>{251A7FF8-4D39-4F8B-9838-61124BF62F99}</ProjectGuid>
    <OutputType>Library</OutputType>
    <AppDesignerFolder>Properties</AppDesignerFolder>
    <RootNamespace>ExampleAssembly</RootNamespace>
    <AssemblyName>ExampleAssembly</AssemblyName>
    <TargetFramework>net6.0</TargetFramework>
    <FileAlignment>512</FileAlignment>
    <EnableDefaultCompileItems>false</EnableDefaultCompileItems>
    <GenerateAssemblyInfo>false</GenerateAssemblyInfo>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Debug|AnyCPU' ">
    <DebugSymbols>true</DebugSymbols>
    <DebugType>full</DebugType>
    <Optimize>false</Optimize>
    <OutputPath>..\..\build\debug\</OutputPath>
    <DefineConstants>DEBUG;TRACE</DefineConstants>
    <ErrorReport>prompt</ErrorReport>
    <WarningLevel>4</WarningLevel>
    <PlatformTarget>AnyCPU</PlatformTarget>
  </PropertyGroup>
  <PropertyGroup Condition=" '$(Configuration)|$(Platform)' == 'Release|AnyCPU' ">
    <DebugType>pdbonly</DebugType>
    <Optimize>true</Optimize>
    <OutputPath>..\..\build\release\</OutputPath>
    <DefineConstants>TRACE</DefineConstants>
    <ErrorReport>prompt</ErrorReport>
    <WarningLevel>4</WarningLevel>
    <PlatformTarget>AnyCPU</PlatformTarget>
  </PropertyGroup>
  <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Debug|x64'">
    <DebugSymbols>true</DebugSymbols>
    <OutputPath>bin\x64\Debug\</OutputPath>
    <DefineConstants>DEBUG;TRACE</DefineConstants>
    <DebugType>full</DebugType>
    <PlatformTarget>x64</PlatformTarget>
    <ErrorReport>prompt</ErrorReport>
    <CodeAnalysisRuleSet>MinimumRecommendedRules.ruleset</CodeAnalysisRuleSet>
  </PropertyGroup>
  <PropertyGroup Condition="'$(Configuration)|$(Platform)' == 'Release|x64'">
    <OutputPath>bin\x64\Release\</OutputPath>
    <DefineConstants>TRACE</DefineConstants>
    <Optimize>true</Optimize>
    <DebugType>pdbonly</DebugType>
    <PlatformTarget>x64</PlatformTarget>
    <ErrorReport>prompt</ErrorReport>
    <CodeAnalysisRuleSet>MinimumRecommendedRules.ruleset</CodeAnalysisRuleSet>
  </PropertyGroup>
  <ItemGroup>
    <Reference Include="System" />
    <Reference Include="System.Core" />
    <Reference Include="UnityEngine">
      <HintPath>/Applications/Unity/Hub/Editor/2021.3.24f1/Unity.app/Contents/Managed/UnityEngine.dll</HintPath>
      <Private>False</Private>
    </Reference>
  </ItemGroup>
  <ItemGroup>
    <Compile Include="Cheat.cs" />
    <Compile Include="Loader.cs" />
    <Compile Include="Properties\AssemblyInfo.cs" />
  </ItemGroup>
  <Import Project="$(MSBuildToolsPath)\Microsoft.CSharp.targets" />
  <!-- To modify your build process, add your task inside one of the targets below and uncomment it. 
       Other similar extension points exist, see Microsoft.Common.targets.
  <Target Name="BeforeBuild">
  </Target>
  <Target Name="AfterBuild">
  </Target>
  -->
</Project>
```

# Execute Game & Inject dll
```bat
smi.exe -p "{$GAME_NAME}" inject -a ExampleAssembly.dll -n ExampleAssembly -c Loader -m Load
```

- 일반적인 dll injection 처럼 프로세스에 붙는 형태가 아님
- Process Explore로 확인하면, ExampleAssembly.dll 은 게임 프로세스에 붙어있지 않음
- 즉, mono.dll 에 binary 형태로 Attach 되어 실행되었음을 의미함
- 게임 실행시, 왼쪽 상단에 `This is a very useful cheat` 라는 문구가 지속적으로 노출됨