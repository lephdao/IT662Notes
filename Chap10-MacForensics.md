Chapter 10: Mac Forensics
========================================

## Mac History
* First prototype of Apple computer: 1975
* Formation of Apple Computer: April 1976 with Jobs, Wozniak and Ronald Wayne.
* First computer was Apple I by Wozniak
* **Apple II**: came in plastic case with keyboard built-in, first pc with color graphics. OS for Apple II: Apple DOS (1978), Apple Pascal (run on p-code Pascal), Apple SOS (all programs use Sophisticated Operating System loaded into memory), ProDOS (support Assembly and BASIC), Lisa OS (had full GUI with file browser with mouse and stuff).

After Apple II, there were:
* The Macintosh (1984), OS was System 1
* Systems 7: allowed text dragging between applications
* Mac OS for PowerPC: ran on System 7.1.2 OS
* AIX for PowerPC (1996): discontinued in 1997

**Mac OS X**
* What change? OS was based on FreeBSD, which is a UNIX clone.
* Code names: Cheetah --> Puma --> Jaguar --> Panther --> Tiger --> Leopard --> Snow Leopard --> Lion --> Moutain Lion --> Yosemite --> Sierra --> High Sierra --> Mojave --> Catalina (current October 2019)

## Mac File System

Apple File System (APFS) is the default file system for Mac computers using macOS 10.13 or later, features strong encryption, space sharing, snapshots, fast directory sizing, and improved file system fundamentals. 
[link to offical page!](https://support.apple.com/guide/disk-utility/file-system-formats-available-in-disk-utility-dsku19ed921c/mac)

### MFS - Macintosh File System
- Was probably replaced with HFS and HFS+

### Hierarchical File System (HFS)
- Was used on Macintosh Plus to replace MFS 

### HFS+
- aka HFS Standard comparing to HFS Standard 
- Supports journaling and disk quotas (limiting users disk usage)
- Has 2 types of links: hard link and soft link 
- Differences between HFS and HFS+: HFS+ uses 32 bits allocation blocks, supports long filenames (up to 255 chars), uses Unicode rather than ASCII. 
- **Aliases**: symbolic pinks, allows user to have multiple references to a single file or directory. 
- Otimization: defragmentation on a per-file basis, before the file is defragmented, it needs to qualify some conditions. This is an advantage over NTFS and FAT.
- **Allocation file**: keeps track of which allocation blocks are free and which are not. 0 >> block is free, 1 >> block is in use. Uses B-tree structure to hold the data. Each record in catalog file is 8KB in size. 
- Bash shell. Uses B tree structure to hold the data. 

### ISO9660
- Used by compact discs (CDs)

### Microsoft Disk Operating System
- Mac OS X includes support for MS-DOS file system FAT12, FAT16 and FAT32 >> Macintosh machine can read floppy disk (FAT12) and files created with DOS/Windows 3.1

### New Technology File System
- Is the file system that used by DVD-ROM discs, not guarantee that Mac OS X can read the files.

### UNIX File System
- The file system used by FreeBSD >> MacOS X can read UFS volumes. 

## Partition Types 

**What?** refers to Apple documents as partition schemes. Apple supports 3 partition schemes: GUID Partition Table, Apple Partition Map, master boot record. 

### GUID Partition Table
- Globally Unique Identifier is used in computers that have Intel processor, requires OS X v 10.4 or later. 

### Apple Partition Map
- APM is used with any PowerPC based Mac, basically you can mount and use a drive formatted with APM, can be used as start-up device.

### Master Boot Record
- Contained in the boot section, is used when DOS or Windows based computer. 

## Mac Logs

### /var/log
- General repository for lots of information
- Contains many logs: /var/log/daily.log contains data on all mounted >> why? can see what devices was attacked and get data from them because it stores data about removable media + serial numbers.

### /var/spool/cups (Folder)
Contains information about printed documents like name of document printed and user who printed it. 

### /Library/Receipts (Folder)
Contains information about system and software updates

### /Users/<username>/.bash_history 
Because Mac uses Bash shell, this log shows variety of commands (rm, dd).

### /var/vm (Folder)
/var/vm/app contains lists of recently opened applications and temporary data used by applications. 

### /Users/
Contains users' files 

### /Users/<username>/Library/Preferences 
Contains user preferences + preferences of programs that have been deleted. 

## Directories

### /Volumes 
Contains information about mounted devices >> data about hard disks, eternal disks, CDs, DVDs, virtual machines. 

### /Users
Contains all user accounts and associated files 

### /Applications 
Stores the applications 

### /Network
Contains information about servers, network libraries, network properties 


### /etc 
Contains configuration files 

### /Library/Preferences/SystemConfiguration
Contains the network config data for each network card

## Mac Forensic Techniques 

### Target Disk Mode
- Create bit-level copy of suspect drive. Use dd with netcat to make a forensic copy. Manually do it in Mac: place computer into Target Disk Mode - it cannot be written to anymore - then connect to the computer with USB or FireWire.
- What good about it? allows computers to be inspected on-site, before disconnecting and transported into a lab. 

### Searching Virtual Memory
- Look for swap file in /var/vm/ by typing ls -al + grep which gives you listing of all files in virtual memory

## Shell Commands

### date
Returns the current date and time zone >> good for documenting time of examination, to convert to UTC use date -u command.

### ls /dev/disk? 
Lists all current device files that are in use

### /hdiutil partition /dev/disk0
Lists the partition table for the boot drive

### system_profiler SPHardwareDataType 
Returns the hardware information for the host system, all the attached Serial Advanced Technology Attachment (SATA) devices

### system_profiler SPSoftwareDataType 
Returns all information about the OS

## Examine a Mac
Ideally: create a copy of the forensic image --> mount it as a read-only virtual machine (either using Forensic Explorer and OSForensics)

## Undelete in Mac
- Depends on how soon after the deletion you attempt to recover the data 
- How? Trash folder --> go to Trash directory --> copy/move file to original location or using tools.



