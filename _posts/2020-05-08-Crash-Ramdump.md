---
layout: post
title: Crash & Ramdump
tags: linux kernel crash ramdump panic
categories: debug
---
For linux panic, dmesg could show some bactrace & stack mem info.
And we could do some analysis, get some cause and give the solution.
But for many cases, we need to do ramdump and use cross crash tool
to analyse the scene.
Eg.
1. stack corruption
2. system hung
3. ...

So below topics are mainly about crash and ramdump related.
### How to do ramdump
some method as below:
1. kdump
    Linux official ramdump method. It needs to open some options with menuconfig,
    such as kexec and kdump. Kexec contains mainly contains 2 parts, syscall kexec_load,
    userspace kexec-tools. Anyway, kexec could launch a new kernel from the old kernel.
    Therefore, kdump's logic is just like below:
    kernel panic -> panic handler -> run backup kernel (which is configed in kernel cmd args)
    -> dump the whole memory to target. (disk/net/...)
    Obviously, the backup kernel will be configured and positioned in the reserved memory, which
    won't have conflict with the front kernel.

2. uboot
    Just warm-reboot to uboot, and use uboot to dump all the memory. The key is bootrom, spl, and uboot
    shouldn't corrupt kernel's memory, and dram won't lose the data with warm reset.

    Then uboot can use many methods to do ramdump... such as tftp, udsik, emmc, fastboot and so on.

3. let other alive chip do ramdump
    Previous project, when AP panic/hung happen, we will use the other processor, a stm32 core to do whole 
    memory dump. What needs to be guanranteed is if stm32's ramdump opartion won't corrupt the kernel mem
    region.

### How to analyse the ramdump
Just use crash tool, which is based on gdb.
Some command as below:
1. crash vmlinux ramdump@0
2. crash vmlinux ramdump@0 --no_panic
    # --no-panic option will don't search the panic task, but just set on PID 0 as default.
3. bt
    -a
    -t
    -f
4. log
5. dmesg
6. ps
7. rd <address>     # read memory

### What's more?
to be continued...
