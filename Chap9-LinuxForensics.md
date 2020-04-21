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

### Ext
* Extended File System, current version of ext4. Ext4 can support volumes with sizes up to 1 exabyte and single file with sizes up to 16Tb.
* On Linux, run >>df -T to find out what file system it's using
* Ext3 and Ext4 support journaling, journaling = logging.
* Ext4 level: journal --> ordered --> writeback

### Reiser File System
* ReiserSF supports journaling, is part of kernel ver 2.4.1

### Bekerley Fast File system
* = UNIX File System, uses a bitmap to track free clusters to see which are free and what not.

## Logs

### var/log/faillog Log
* Contains failed user logins --> tracking attempts cracking into the system.
* Take notes of: number of failed login attempts, timestamps

### var/log/kern.log Log
* Shows systemwide problem
* Contains messages from the OS

### /var/log/lpr.log Log
Contains printer records

### /var/log/mail.* Log
Contains mail server log

### /var/log/mysql.* Log
* Contains records related to MySQL database server
* Can be used to track SQL injection attacks

### /var/log/apache2/* Log
Contains logs related to Apache server

### /var/log/lighttpd/* Log
Contains logs related to Lighttpd web server and other activities.

### /var/log/apport.log Log
Contains records of application crashes. Can be either bugs or malware present.

### What is Snort?
Open source Intrusion detection system (IDS). There are passive and active system. Passive only log suspicious activities and maybe notify network admin, Active shuts down the suspected attack. Active IDS can be inconvenient to false positives.

## Directories

* **/root**: home directory for root user
* **/bin**: binaries, compiled files, some malwares might be here
* **/sbin**: binaries that are not for regular users
* **/etc**: configuration files like web servers, boot loaders
* /etc/inittab file: bootup process is set here. initab has: label (unique identification label up to 4 chars), run_level (init level at which entry is executed), action:a (some keywork telling what init gonna take on), process (process that init executes after entering some run level), boot (start process, move on to next entry), bootwait (start process once, waits for it to terminate before starting next initab entry), initdefault (which run level to enter initially?), sysinit (start process first time init reads the table).
* /dev: interfaces to devices and drives
* /mnt: floppy and CD-ROM drives are mounted here
* /boot: files that are critical to booting like boot loader
* /usr: subdirectories for individual users
* /var: contains data that is changed during system operation
* /var/spool: contains the print queue
* /proc: is not stored on hard disk, it is created in memory and keeps infos about running processes

## Shell commands for Forensics

* **dmesg > file.txt** displays all messages during boot process
* **fsck** file system check
* **grep** searches for wide range of parameters
* **history** allows user to see previously entered commands
* **mount** mounts a new file system
* **ps** shows currently running processes for current user, display includes: pid (process id), terminal associated with process (tty), cumulated CPU time in dd-hh:mm:ss, executable name.
* **pstree** shows all processes in tree structure
* **top** lists the processes in order of how much CPU time that process is using
* **kill pid** to kill a process
* **file** which type of file?
* **su** puts you in super user mode
* **who** info about current user
* **finger** gets back information regarding specific user. combo: finger + who
* **dd** makes a copy of a drive, example: *dd if=/dev/mem of=/evidence/image.memory1*, it takes /dev/mem and sends it to evidence partition and creates an image of it.
* **ls** lists contents

## Recovering deleted files?

*inode* is a data structure in the file system that stores information about a file except name and the data. So inode = link to the file

### Manually

A file is deleted when its inode link count reaches 0.
1. System --> single-user mode, use **init**
2. grep -b 'search-text' /dev/partition > file.txt or grep -a -B[size before] -A[size after] 'text' /dev/[partition] > file.txt
3. cat file.txt
