---
title: Diskpart
description: 
published: true
date: 2023-03-15T07:49:56.900Z
tags: system, configuration, windows
editor: markdown
dateCreated: 2023-03-15T03:22:08.694Z
---

# Diskpart

태그: Disk, Partition

# Format

```bash
list disk
select disk #
clean
create partition primary
active
format fs=ntfs {quick}
assign letter=x
```