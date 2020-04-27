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
- 
