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
- Windows CE was the first Windows mobile OS, was released as the Pocket PC 2000 based on Windows CE ver 3. 
- Windows Phone ws released 2008
- Windows Phone 7 was released in 2010

### BlackBerry
- OS: BlackBerry 10 based on QRNX OS
- No more BlackBerry

## Evidence Gathering From Cellphone
- Call history: cyberstalking cases, patterns  
- Emails, texts, messages
- Photos, videos: direct evidences of crime 
- Phone information: model #, serial number SIM card, OS. >> first thing that you document in the investigation. 
- Global positioning system information (GPS): cheated boyfriend. Some GPS isn't correct because instead of using GPS satellies, some phones use triangular of signal strength with various cell towers. 
- The use of Wi-fi with GPS improves accuravy of GPS.
- Network information

### Phone states
- NIST - National Institute of Standards and Technology lists 4 different states a mobile device can be when data is extracted:
1. **Nascent state**: No user data, fresh
2. **Active state**: Powered on, performing tasks, have file systems populated with data 
3. **Quiescent state**: look to be inactive but actually performing functions 
4. **Semi-active state**: between active and quiescent, waiting for a set time to perform a function 

## Seizing Evidence from Mobile Device 
- Rules: (1) Make sure when plugging phone to computer the phone does not sync. iPhone sometimes auto-sync. (2) Make sure touching device as little as possible and document everything. (3) Don't write data to mobile device 
- *How to prevent writing into mobile phone?* if working on a Windows machine, use the Windows Registry to prevent writing by find HKEY_LOCAL_MACHINE\System\CurrentControlSet\StorageDevicePolicies >> set vaue to 0x00000001 >> restart. 
- Use tools like Forensic Toolkit and EnCase can image the phone.
- Oxygen Forensics: user friendly tool for imaging and exmining iphones and android phones
- Cellebrite: used by federal law enforcement but very expensive. 
- MobileEdit: easy to use interface 
- Data Doctor: recovers all Inbox and Outbox data and other contact data
- Sim card data retrieval utility: retrieves inbox and send message data + contact data, runs on Windows 
- Device Seizure: by Paraben SW
- Forensic SIM Cloner: clones SIM card to do forensics analysis on the SIM. 
- The NIST sponsors the Computer Forensics Tool Testing Project (CFTT), which decides which tools you should use for your forensic project. 
- The NIST also provides guildlines for how to write a report. 
- Good report includes: Descriptive list of items + Identify and signature of the examiner + Equipment and setup + Brief description of the steps + Supporting materials + Details of findings + Report conclusions 

### Seizing Evidence on iPhone 
- Use XRY to break passcode 
- Use iTunes to export data >> iOS version number, phone number, serial number 
- Deleted Files: look for files in .Trashes\501 >> new data can be retrieved 
- Tools: Pwnage, Recover My iPod 

### Blackberry phone
- Install Blackberry Desktop Manager 

## JTAG 
- What for? bypass locked login screen
- Joint Test Action Group, IEEE standard for testing chips. Test Access Points (TAP) are used to directly access the chip and extract data. 
- Android phone has TAP order publishes 
- Extract raw binary dumps: takes the back off of the phone --> connects wires to the TAPs of memory chip --> use software to extract data from JTAG --> get binary data, use sw to analyze raw data. 
- *chip-off* remove the chip completely and extract data from it, but chip off will destroy the phone. 
- If the chip is encrypted then JTAG and chip off won't work

