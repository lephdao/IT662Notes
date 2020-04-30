Chapter 11 - Mobile Forensics
======================================================

## Terms

### Mobile Switching Center (MSC)
- MSC is a switching system for the cellular network, responsible for routing calls between base stations and the public switched telephone network. 
- MSCs are used in 1G, 2G, 3G and GSM (Global system for mobile) communcation networks. 

### Base Transceiver Station (BTS)
- reponsible for communcations between the mobile network and the network switching system. 
- BTS + BSC (base station controller) = BSS (base station system)

### Home Location Register (HLR)
- HLR is a database used by MSC that contains subscriber data and service information

### Subscriber Identity Modile (SIM)
- SIM card is a memory chip that stores the International Mobile Subscriber Identity. It is unique to each phone.
- Removable SIM
- SIM card contains: ICCID, IMSI (serial number), security authentication, ciphering information, network information, services that user has access to, 2 passwords (PIN aka personal identification number and PUK aka personal unlocking code).
- SIM cloning is illegal

### Electronic Serial Number (ESN)
- ESNs are unique identifiction numbers developed by US Federal Communications Commission (FCC) to idetify cell phones, now only used in CDMA phones (code division multiple access). 
- Later phones use GSM and IMEI (international mobile equipment identity number)
- ESN combination: 8 bits (manufacturer code) + 24 bits (phone code). 
- IMEI is used with GSM and LTE

### Personal Unlocking Code
- To reset forgotten PIN
- If entered incorrectly 10 times in a row >> device is blocked permanently

### Integrated Circuit Card Identifier 
- Each SIM is identified by its ICCID, it was engraved on the card. 
- Combination: 7 digits (issuer identification number) + some digits (individual account identification number) + check digit.

### Networks types
- **Global System for Mobile communcations**: 2G network
- **Enhanced Data Rates for GSM Evolution**: 2G+
- **Universal Mobile Telecommuncations System**: 3G
- **Long Term Evolution**: LTE and 4G
- **Wireless Fidelity**: phones can connect to Wifi networks too 

## Operating Systems

### iOS
- Current version is iOS 13.4.1
- Originally released in 2007 for iPod Touch and iPhone. 
- Supports "gestures": swipe, drag, pinch, tap and so on. 
- Has 4 layers: (1) Core OS layer is heart of the OS, (2) Core Services layer is how applications interact with OS (3) Media layer, which is responsible for music, video, etc., (4) Cocoa Touch layer, responds to the touch motions.
- In the past, iOS uses HFS+ file system, but it could use FAT32 when communicating with a PC. 
- Data partition elements: Calendar entries, contacts, note, iPod_control, iTunes config, iTunes music. 
- **iPod_control\devices\sysinfo** contains Model number and Serial number. 

### Android
- Current Android version is Android 10.0 with no dessert name :disappointed:
- Linux-based OS and open source
- Differences between versions are new features, not really OS changes
- Each vendor would modify their own version of Android, partition layout can vary. But in general, these are most common partitions: boot loader, recovery partition (boot the phone in recovery mode), user data partition (user data), cache partition (frequently accessed data and recovery logs), system partition (not very important to forensics).

#### Diretories that might return forensic evidences
- acct: mount point for the control group
- cache: cache data
- data: data for each app
- mnt: shows internal and external storage like SD cards

#### Extracting data
- Must be in developer mode 
- User adb (Android Debugging Bridge) shell by connecting thru a USB cable and then use the shell to extract the data. 

### Windows 
