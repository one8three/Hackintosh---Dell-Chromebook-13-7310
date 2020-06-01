# Dell Chromebook 13 7310 Hackintosh
### Now using OpenCore! 

This is not meant to be a guide or walkthrough but merely a dump of files and notes to get MacOS working on a Dell Chromebook 13. I will try to keep this updated as I update my Chromebook to future MacOS releases.

Confirmed working on MacOS Catalina 10.15.5
#
### Basic steps:
 - Install MrChromebox custom [UEFI firmware](https://mrchromebox.tech/#fwscript)
 - Create MacOS installer flashdrive with [OpenCore](https://github.com/acidanthera/OpenCorePkg/releases) bootloader
 - Download SSDTs, kexts, and config.plist from this repo
 - Generate SMBIOS and add it to the config.plist
 - Place the SSDTs, kexts, and config.plist in appropriate locations in your EFI partition
 - Install MacOS
 - Install OpenCore to internal SSD
 - Disable force click in trackpad settings
 - Install [Karabiner](https://karabiner-elements.pqrs.org) to map top row keyboard shortcuts
   - Here is a premapped configuration for Chromebook keys - [Top row mapped to Chromebook keys](https://genesy.github.io/karabiner-complex-rules-generator/#eyJ0aXRsZSI6IkNocm9tZWJvb2sgVG9wIFJvdyIsInJ1bGVzIjpbeyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmMSJ9LCJ0byI6W3sia2V5X2NvZGUiOiJvcGVuX2JyYWNrZXQiLCJyZXBlYXQiOmZhbHNlLCJtb2RpZmllcnMiOlsibGVmdF9ndWkiXX1dfV0sImRlc2NyaXB0aW9uIjoiRjEgdG8gQmFjayJ9LHsibWFuaXB1bGF0b3JzIjpbeyJ0eXBlIjoiYmFzaWMiLCJmcm9tIjp7ImtleV9jb2RlIjoiZjIifSwidG8iOlt7ImtleV9jb2RlIjoiY2xvc2VfYnJhY2tldCIsIm1vZGlmaWVycyI6WyJsZWZ0X2d1aSJdLCJyZXBlYXQiOmZhbHNlfV19XSwiZGVzY3JpcHRpb24iOiJGMiB0byBGb3J3YXJkIn0seyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmMyJ9LCJ0byI6W3sia2V5X2NvZGUiOiJyIiwicmVwZWF0IjpmYWxzZSwibW9kaWZpZXJzIjpbImxlZnRfZ3VpIl19XX1dLCJkZXNjcmlwdGlvbiI6IkYzIHRvIFJlZnJlc2gifSx7Im1hbmlwdWxhdG9ycyI6W3sidHlwZSI6ImJhc2ljIiwiZnJvbSI6eyJrZXlfY29kZSI6ImY0In0sInRvIjpbeyJrZXlfY29kZSI6ImYiLCJtb2RpZmllcnMiOlsibGVmdF9ndWkiLCJsZWZ0X2NvbnRyb2wiXSwicmVwZWF0IjpmYWxzZX1dfV0sImRlc2NyaXB0aW9uIjoiRjQgdG8gRnVsbHNjcmVlbiJ9LHsibWFuaXB1bGF0b3JzIjpbeyJ0eXBlIjoiYmFzaWMiLCJmcm9tIjp7ImtleV9jb2RlIjoiZjUifSwidG8iOlt7ImtleV9jb2RlIjoibWlzc2lvbl9jb250cm9sIiwicmVwZWF0IjpmYWxzZX1dfV0sImRlc2NyaXB0aW9uIjoiRjUgdG8gTWlzc2lvbiBDb250cm9sIn0seyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmNiJ9LCJ0byI6W3sicmVwZWF0Ijp0cnVlLCJrZXlfY29kZSI6ImRpc3BsYXlfYnJpZ2h0bmVzc19kZWNyZW1lbnQifV19XSwiZGVzY3JpcHRpb24iOiJGNiB0byBCcmlnaHRuZXNzIERvd24ifSx7Im1hbmlwdWxhdG9ycyI6W3sidHlwZSI6ImJhc2ljIiwiZnJvbSI6eyJrZXlfY29kZSI6ImY3In0sInRvIjpbeyJyZXBlYXQiOnRydWUsImtleV9jb2RlIjoiZGlzcGxheV9icmlnaHRuZXNzX2luY3JlbWVudCJ9XX1dLCJkZXNjcmlwdGlvbiI6IkY3IHRvIEJyaWdodG5lc3MgdXAifSx7Im1hbmlwdWxhdG9ycyI6W3sidHlwZSI6ImJhc2ljIiwiZnJvbSI6eyJrZXlfY29kZSI6ImY4In0sInRvIjpbeyJrZXlfY29kZSI6Im11dGUiLCJyZXBlYXQiOmZhbHNlfV19XSwiZGVzY3JpcHRpb24iOiJGOCB0byBNdXRlIn0seyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmOSJ9LCJ0byI6W3sicmVwZWF0Ijp0cnVlLCJrZXlfY29kZSI6InZvbHVtZV9kZWNyZW1lbnQifV19XSwiZGVzY3JpcHRpb24iOiJGOSB0byBWb2x1bWUgRG93biJ9LHsibWFuaXB1bGF0b3JzIjpbeyJ0eXBlIjoiYmFzaWMiLCJmcm9tIjp7ImtleV9jb2RlIjoiZjEwIn0sInRvIjpbeyJyZXBlYXQiOnRydWUsImtleV9jb2RlIjoidm9sdW1lX2luY3JlbWVudCJ9XX1dLCJkZXNjcmlwdGlvbiI6IkYxMCB0byBWb2x1bWUgVXAifV19)
 - Disable hibernate with "sudo pmset -a hibernatemode 0"
 - Install LogoutHook.command according to directions in Utilities folder of the OpenCore download

If you want a full guide, use this: https://dortania.github.io/vanilla-laptop-guide/
All of the SSDTs and the config file were created through this guide.


# Requirements
  - Core i3 or Core i5 Processor 
    - Will NOT work with the Celeron model
  - Minimum of a 32GB SSD
    - Minimum 64GB recommended
  - A compatible WiFi card
    - The Dell DW1560 works in MacOS, Windows & Ubuntu
  - MacOS installer flash drive 
    - There are plenty of guides on how to make this so that won't be covered here

## Notes
  - This is all made for [OpenCore](https://github.com/acidanthera/OpenCorePkg/releases) 0.5.8
    - Clover is no longer used here but old Clover data can be found in the Clover branch.
  - You will need to generate your own SMBIOS for the attached config.plist - Use the MacBook Air 7,2 profile 
    - Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to do this
  - The SSDTs are made from version 4.11.2 MrChromebox's firmware (other versions may work but YMMV)

## What's Working: 
  - Just about everything!
  
## What's Not Working:
  - Touchscreen - unlikely to be fixed
  - Keyboard backlight control - also turns off after closing the lid
  - Occasional trackpad click stick after waking from sleep
    - Possibly fixed with latest custom [VoodooI2C.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/VoodooI2C-CB13.zip)

## To Do:  
  - Keyboard backlight control
    - From my research this will likely need a custom kext or modifications to VoodooPS2Controller.kext and a SSDT. From what I can tell, it wouldn't be difficult for somebody who knows what they're doing but unfortunately, it's well above my skill level. If anyone sees this with the knowledge to get this done, please reach out! I have the location of the backlight control in the DSDT and it's pretty straightforward on what it does but I don't know how to implement it.

## OpenCore Config
Place this in EFI/EFI/OC/
  - [config.plist](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/config.plist)
    - You will need to generate your own SMBIOS section with [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) - use a Macbook Air 7,2 profile.

## SSDT files
Place these in EFI/EFI/OC/ACPI
- [SSDT-EC.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT-EC.aml)
  - Exposes the embedded controller to MacOS
- [SSDT-PLNF.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/OpenCore/SSDT-PNLF.aml)
  - Enables LCD backlight control
- [SSDT-PLUG](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/SSDT-PLUG.aml?raw=true)
  - Enables proper CPU power management
- [SSDT-USB.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/OpenCore/SSDT-USB.aml)
  - Properly maps USB ports, Micro SD card reader, webcam, and bluetooth
- [SSDT-SBUS-MCHC.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/OpenCore/SSDT-SBUS-MCHC.aml)
- [SSDT-HPET.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/OpenCore/SSDT-HPET.aml)

  
## Required Kexts
Placed these in EFI/EFI/OC/Kexts
- [AppleALC.kext](https://github.com/acidanthera/applealc/releases)
- [Lilu.kext](https://github.com/acidanthera/lilu/releases)
- [WhateverGreen.kext](https://github.com/acidanthera/whatevergreen/releases)
- [VirtualSMC.kext](https://github.com/acidanthera/virtualsmc/releases)
  - SMCBatteryManager.kext
  - SMCProcessor.kext
  - SMCSuperIO.kext
- [VoodooI2C.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/VoodooI2C-CB13.zip) 
  - VoodooI2CSynaptics.kext
  - This is a modified VoodooI2C.kext for appropriate Trackpad sensitivity
- [VoodooPS2Controller.kext](https://github.com/acidanthera/VoodooPS2/releases)
- [CPUFriend.kext](https://github.com/acidanthera/CPUFriend/releases)
- [CPUFriendDataProvider.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/CPUFriendDataProvider.kext.zip)

## Kexts for Dell DW1560 wifi
Placed in EFI/EFI/OC/Kexts 
 - [AirportBrcmFixup.kext](https://github.com/acidanthera/airportbrcmfixup/releases)
 - [BrcmPatchRAM3.kext](https://github.com/acidanthera/BrcmPatchRAM/releases)  
   - BrcmBluetoothInjector.kext
   - BrcmFirmwareData.kext
 

### Post-Install
- Setup LogoutHook.command following the directions found in the Utilities folder of the OpenCore download
- Disable force click in trackpad settings
- Install [Karabiner](https://karabiner-elements.pqrs.org) to map top row keyboard shortcuts
  - Here is a premapped configuration for Chromebook keys - [Top row mapped to Chromebook keys](https://genesy.github.io/karabiner-complex-rules-generator/#eyJ0aXRsZSI6IkNocm9tZWJvb2sgVG9wIFJvdyIsInJ1bGVzIjpbeyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmMSJ9LCJ0byI6W3sia2V5X2NvZGUiOiJvcGVuX2JyYWNrZXQiLCJyZXBlYXQiOmZhbHNlLCJtb2RpZmllcnMiOlsibGVmdF9ndWkiXX1dfV0sImRlc2NyaXB0aW9uIjoiRjEgdG8gQmFjayJ9LHsibWFuaXB1bGF0b3JzIjpbeyJ0eXBlIjoiYmFzaWMiLCJmcm9tIjp7ImtleV9jb2RlIjoiZjIifSwidG8iOlt7ImtleV9jb2RlIjoiY2xvc2VfYnJhY2tldCIsIm1vZGlmaWVycyI6WyJsZWZ0X2d1aSJdLCJyZXBlYXQiOmZhbHNlfV19XSwiZGVzY3JpcHRpb24iOiJGMiB0byBGb3J3YXJkIn0seyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmMyJ9LCJ0byI6W3sia2V5X2NvZGUiOiJyIiwicmVwZWF0IjpmYWxzZSwibW9kaWZpZXJzIjpbImxlZnRfZ3VpIl19XX1dLCJkZXNjcmlwdGlvbiI6IkYzIHRvIFJlZnJlc2gifSx7Im1hbmlwdWxhdG9ycyI6W3sidHlwZSI6ImJhc2ljIiwiZnJvbSI6eyJrZXlfY29kZSI6ImY0In0sInRvIjpbeyJrZXlfY29kZSI6ImYiLCJtb2RpZmllcnMiOlsibGVmdF9ndWkiLCJsZWZ0X2NvbnRyb2wiXSwicmVwZWF0IjpmYWxzZX1dfV0sImRlc2NyaXB0aW9uIjoiRjQgdG8gRnVsbHNjcmVlbiJ9LHsibWFuaXB1bGF0b3JzIjpbeyJ0eXBlIjoiYmFzaWMiLCJmcm9tIjp7ImtleV9jb2RlIjoiZjUifSwidG8iOlt7ImtleV9jb2RlIjoibWlzc2lvbl9jb250cm9sIiwicmVwZWF0IjpmYWxzZX1dfV0sImRlc2NyaXB0aW9uIjoiRjUgdG8gTWlzc2lvbiBDb250cm9sIn0seyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmNiJ9LCJ0byI6W3sicmVwZWF0Ijp0cnVlLCJrZXlfY29kZSI6ImRpc3BsYXlfYnJpZ2h0bmVzc19kZWNyZW1lbnQifV19XSwiZGVzY3JpcHRpb24iOiJGNiB0byBCcmlnaHRuZXNzIERvd24ifSx7Im1hbmlwdWxhdG9ycyI6W3sidHlwZSI6ImJhc2ljIiwiZnJvbSI6eyJrZXlfY29kZSI6ImY3In0sInRvIjpbeyJyZXBlYXQiOnRydWUsImtleV9jb2RlIjoiZGlzcGxheV9icmlnaHRuZXNzX2luY3JlbWVudCJ9XX1dLCJkZXNjcmlwdGlvbiI6IkY3IHRvIEJyaWdodG5lc3MgdXAifSx7Im1hbmlwdWxhdG9ycyI6W3sidHlwZSI6ImJhc2ljIiwiZnJvbSI6eyJrZXlfY29kZSI6ImY4In0sInRvIjpbeyJrZXlfY29kZSI6Im11dGUiLCJyZXBlYXQiOmZhbHNlfV19XSwiZGVzY3JpcHRpb24iOiJGOCB0byBNdXRlIn0seyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmOSJ9LCJ0byI6W3sicmVwZWF0Ijp0cnVlLCJrZXlfY29kZSI6InZvbHVtZV9kZWNyZW1lbnQifV19XSwiZGVzY3JpcHRpb24iOiJGOSB0byBWb2x1bWUgRG93biJ9LHsibWFuaXB1bGF0b3JzIjpbeyJ0eXBlIjoiYmFzaWMiLCJmcm9tIjp7ImtleV9jb2RlIjoiZjEwIn0sInRvIjpbeyJyZXBlYXQiOnRydWUsImtleV9jb2RlIjoidm9sdW1lX2luY3JlbWVudCJ9XX1dLCJkZXNjcmlwdGlvbiI6IkYxMCB0byBWb2x1bWUgVXAifV19)
- Disable hibernate with "sudo pmset -a hibernatemode 0"


#


## Credits & Sources (in no particular order and maybe missing some)
- Apple
- https://github.com/acidanthera/
- https://github.com/alexandred/
- https://github.com/MrChromebox/
- https://github.com/RehabMan
- https://www.insanelymac.com/
- https://www.tonymacx86.com/
- https://reddit.com/r/hackintosh
- https://github.com/corpnewt/CPUFriendFriend
- https://github.com/TheRandMan/VoodooI2C
- https://dortania.github.io/vanilla-laptop-guide/
