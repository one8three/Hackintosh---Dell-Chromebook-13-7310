# Dell Chromebook 13 7310 Hackintosh
### Now using OpenCore 0.5.9! 

This is not meant to be a guide or walkthrough but merely a dump of files and notes to get MacOS working on a Dell Chromebook 13. I will try to keep this updated as I update my Chromebook to future MacOS releases.

Confirmed working on MacOS Catalina 10.15.5
#

### Requirements
  - Core i3 or Core i5 Processor 
    - Will not work with the Celeron model
  - Minimum of a 32GB SSD
    - Minimum 64GB recommended
  - A compatible WiFi card
    - The Dell DW1560 works in MacOS, Windows & Ubuntu
  - MacOS installer flash drive 
    - There are plenty of guides on how to make this so that won't be covered here

### Notes
  - This is all made for [OpenCore 0.5.9](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.5.9)
    - Be sure to use the same version
  - You will need to generate your own SMBIOS for the attached config.plist - Use the MacBook Air 7,2 profile
    - Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to do this
  - The DSDT/SSDTs are made from version 4.11.2 of MrChromebox's firmware (other versions may work but YMMV)
  - Keyboard backlight is controlled with left ctrl + alt + brightness keys (F6/F7). There are 7 stages, including off

### What's Working: 
  - Just about everything!
  
### What's Not Working:
  - Touchscreen - highly unlikely that this will ever work - fairly uncommon to have one on this device anyway
  - Occasionally the trackpad will get stuck in a click
    - I've been able to clear it by "rubbing" the trackpad with my palm
    - Possibly fixed with latest [VoodooI2C.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/VoodooI2C-CB13.zip)

### To Do:  
  - Nothing!

#

## Basic Installation steps:
 - Install [MrChromebox UEFI firmware](https://mrchromebox.tech/#fwscript)
 - Create MacOS installer flashdrive with [OpenCore 0.5.9](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.5.9) bootloader
 - Download the [required files](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310#required-files)
 - Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)to generate a unique SMBIOS and add it to the config.plist
 - Place the required files in their appropriate locations on your EFI partition
 - Install MacOS
 - Install OpenCore to the internal SSD
 - Disable force click in trackpad system preferences
 - Install [Karabiner](https://karabiner-elements.pqrs.org) to map top row keyboard shortcuts
   - Use the "Function keys" tab to map mission control, volume, and brightness keys (F5-F10)
   - Here are preconfigured "Complex modifications" tab for the first 4 keys (F1-F4) - [First 4 top row Chromebook keys](https://genesy.github.io/karabiner-complex-rules-generator/#eyJ0aXRsZSI6IkNocm9tZWJvb2sgVG9wIFJvdyIsInJ1bGVzIjpbeyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmMSJ9LCJ0byI6W3sia2V5X2NvZGUiOiJvcGVuX2JyYWNrZXQiLCJyZXBlYXQiOmZhbHNlLCJtb2RpZmllcnMiOlsibGVmdF9ndWkiXX1dfV0sImRlc2NyaXB0aW9uIjoiRjEgdG8gQmFjayJ9LHsibWFuaXB1bGF0b3JzIjpbeyJ0eXBlIjoiYmFzaWMiLCJmcm9tIjp7ImtleV9jb2RlIjoiZjIifSwidG8iOlt7ImtleV9jb2RlIjoiY2xvc2VfYnJhY2tldCIsIm1vZGlmaWVycyI6WyJsZWZ0X2d1aSJdLCJyZXBlYXQiOmZhbHNlfV19XSwiZGVzY3JpcHRpb24iOiJGMiB0byBGb3J3YXJkIn0seyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmMyJ9LCJ0byI6W3sia2V5X2NvZGUiOiJyIiwicmVwZWF0IjpmYWxzZSwibW9kaWZpZXJzIjpbImxlZnRfZ3VpIl19XX1dLCJkZXNjcmlwdGlvbiI6IkYzIHRvIFJlZnJlc2gifSx7Im1hbmlwdWxhdG9ycyI6W3sidHlwZSI6ImJhc2ljIiwiZnJvbSI6eyJrZXlfY29kZSI6ImY0In0sInRvIjpbeyJrZXlfY29kZSI6ImYiLCJtb2RpZmllcnMiOlsibGVmdF9ndWkiLCJsZWZ0X2NvbnRyb2wiXSwicmVwZWF0IjpmYWxzZX1dfV0sImRlc2NyaXB0aW9uIjoiRjQgdG8gRnVsbHNjcmVlbiJ9XX0=)
 - Disable hibernate with "sudo pmset -a hibernatemode 0"
 - Install LogoutHook.command according to directions in Utilities folder of the OpenCore download

If you want a full guide, use this: https://dortania.github.io/vanilla-laptop-guide/ -
most of the files in this repo were created using this guide
#
## Required Files

### OpenCore Config
Place this in EFI/EFI/OC/
  - [config.plist](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/config.plist)
    - You will need to generate your own SMBIOS section using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) - use a Macbook Air 7,2 profile.
    
### OpenCore Drivers
These are included with the OpenCore download unless noted otherwise.
You'll find them in EFI/EFI/OC/Drivers
- AudioDxe.efi
- OpenCanopy.efi
- Ps2KeyboardDxe.efi
- [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)
- OpenRuntime.efi

### DSDT/SSDT files
Place these in EFI/EFI/OC/ACPI
- [DSDT.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/DSDT.aml)
  - Adds control for keyboard backlight
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

### Required Kexts
Place these in EFI/EFI/OC/Kexts
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
- [VoodooPS2Controller.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/VoodooPS2Controller-CB13.zip)
  - This is a modified VoodooPS2Controller.kext that changes the keyboard brightness control keys to ones that actually exist on most laptops. In this case, left ctrl + alt + brightness keys (F6/F7)
- [CPUFriend.kext](https://github.com/acidanthera/CPUFriend/releases)
- [CPUFriendDataProvider.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/CPUFriendDataProvider.kext.zip)

### Kexts for Dell DW1560 wifi
Place these in EFI/EFI/OC/Kexts 
 - [AirportBrcmFixup.kext](https://github.com/acidanthera/airportbrcmfixup/releases)
 - [BrcmPatchRAM3.kext](https://github.com/acidanthera/BrcmPatchRAM/releases)  
   - BrcmBluetoothInjector.kext
   - BrcmFirmwareData.kext
 
## Post-Install
- Setup LogoutHook.command following the directions found in the Utilities folder of the OpenCore download
- Disable force click in trackpad settings
- Install [Karabiner](https://karabiner-elements.pqrs.org) to map top row keyboard shortcuts
  - Here are preconfigured "Complex modifications" for the first 4 keys - [First 4 top row Chromebook keys](https://genesy.github.io/karabiner-complex-rules-generator/#eyJ0aXRsZSI6IkNocm9tZWJvb2sgVG9wIFJvdyIsInJ1bGVzIjpbeyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmMSJ9LCJ0byI6W3sia2V5X2NvZGUiOiJvcGVuX2JyYWNrZXQiLCJyZXBlYXQiOmZhbHNlLCJtb2RpZmllcnMiOlsibGVmdF9ndWkiXX1dfV0sImRlc2NyaXB0aW9uIjoiRjEgdG8gQmFjayJ9LHsibWFuaXB1bGF0b3JzIjpbeyJ0eXBlIjoiYmFzaWMiLCJmcm9tIjp7ImtleV9jb2RlIjoiZjIifSwidG8iOlt7ImtleV9jb2RlIjoiY2xvc2VfYnJhY2tldCIsIm1vZGlmaWVycyI6WyJsZWZ0X2d1aSJdLCJyZXBlYXQiOmZhbHNlfV19XSwiZGVzY3JpcHRpb24iOiJGMiB0byBGb3J3YXJkIn0seyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmMyJ9LCJ0byI6W3sia2V5X2NvZGUiOiJyIiwicmVwZWF0IjpmYWxzZSwibW9kaWZpZXJzIjpbImxlZnRfZ3VpIl19XX1dLCJkZXNjcmlwdGlvbiI6IkYzIHRvIFJlZnJlc2gifSx7Im1hbmlwdWxhdG9ycyI6W3sidHlwZSI6ImJhc2ljIiwiZnJvbSI6eyJrZXlfY29kZSI6ImY0In0sInRvIjpbeyJrZXlfY29kZSI6ImYiLCJtb2RpZmllcnMiOlsibGVmdF9ndWkiLCJsZWZ0X2NvbnRyb2wiXSwicmVwZWF0IjpmYWxzZX1dfV0sImRlc2NyaXB0aW9uIjoiRjQgdG8gRnVsbHNjcmVlbiJ9XX0=)
- Disable hibernate with "sudo pmset -a hibernatemode 0"


#


### Credits & Sources (in no particular order and maybe missing some)
- [Apple](https://www.apple.com)
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
