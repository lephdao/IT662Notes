Chapter 9: Linux Forensics
==============================================

## History of Linux
* From Bell Labs (now Nokia Bell Labs). In 1960s, Bell Labs made Multics, Bell Labs pulled out. Bell Labs made UNIX in 1972 as side project, then after C was created, UNIX was written in C completely. Before, it was written in Assembly.
* 1983: Richard Stallman created GNU (GNU’s Not Unix) aka open source version of UNIX
* 1987: Andrew S. Tanenbaum created Minix, it was written in C.
* Linus Torvalds created Linux

## Introduction

### Types of shell
* Bourne shell (sh): default, 1977
* Bourne-again shell (Bash): most common, 1989. Ubuntu uses this one as default.
* C shell (csh): syntax looks like C, 1978
* Korn shell (ksh): developed David Korn in 1980s

### Graphical User Interface
GNOME // GNU Network Object Model Environment
* Most popular GUI
* Ubuntu ships only with GNOME

KDE/Plasma
* Was founded in 1996 by Matthias Ettrich
* KDE was word play of Common Desktop Environment (CDE) for UNIX
* Built for Qt framework, Qt is a multiplatform GUI framework written in C++

Others: CDE, Enlightenment (for graphic devs)

## Linux Boot Process
1. The system loads the bootstrap environment (bootstrap env is a program that is stored in a special section of flash memory). Booting begins the BIOS at 0xFFFF0
2. After BIOS loaded and power-on self test completed, BIOS locates the master boot record and passes control to it
* First sector = boot sector, boot sector contains executable codes, hex value 0xaa55 in final 2 bytes
3. MBR loads boot loader program including LILO (Linux Loader), or GRUB (Grand Unified Bootloader). When bootable device is found, first stage boot loader is loaded into RAM and execute
* 2 boot loaders in Linux. First one is 512 bytes (446 bytes are primary boot loader, next 64 bytes are partition table). Second one will load the kernel.
4. A splash screen is displayed, which means Linux image is loaded into RAM. The second stage boot loader passes control to kernel image. The kernel is then decompressed and initialized.
5. Boot loader checks the system hardwares and peripherals. Then the boot loader mount the root device and load necessary kernel modules.
6. Kernel stage: 2nd state boot loader loads the kernel image.
* Kernel must initialize all devices system has
7. The system switches the CPU from real mode to protected mode, and it loads compressed kernel and call decompress_kernel().
* “Uncompressing Linux…” means start_kernel was called, and the kernel displays messages.
8. Now kernel is initialized, and the first user program starts.
* init() is called, kernel_thread() is called next
* Kernel goes into an idle loop and becomes an idle thread with process ID 0
9. Boot process inspects /etc/inittab file to determine run level.
* Based on run level, init process executes start-up script located in /etc/rc.d

## Logical Volume Manager
* LVM is an abstraction layer that provides volume management for the Linux kernel
* Role: allowing the resizing of partitions and creating backups by taking snapshots of logical volumes.
* First megabyte of physical drive/volume/PV has LVM

## Linux File System
