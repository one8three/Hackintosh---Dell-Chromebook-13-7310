# Dell Chromebook 13 7310 Hackintosh

### Confirmed working on:
- MacOS: **Catalina 10.15.5**
- MrChromebox coreboot: **4.12**

#
This is not meant to be a thorough guide or walkthrough. It is merely a dump of files and notes to get MacOS working on a Dell Chromebook 13 7310. I will try to keep this updated as I update my Chromebook to future MacOS releases.


#
If updating from coreboot 4.11.2 to 4.12:
  - Grab the new [DSDT.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/DSDT.aml), [SSDT-PLUG.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT-PLUG.aml), [config.plist](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/config.plist), and [USBMap.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/USBMap.kext.zip)
  - Copy your SMBIOS into the new config.plist
  - Remove SSDT-USB.aml from /EFI/OC/ACPI
  - Remove the NVRAM logouthook:
    - Run this command in terminal "sudo defaults delete com.apple.loginwindow LogoutHook"
    - Delete /Users/yourusername/LogoutHook

#

### Requirements:
  - Core i3 or i5 Processor
  - [MrChromebox's coreboot firmware 4.12](https://mrchromebox.tech/#fwscript)
  - [OpenCore 0.5.9](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.5.9) 
  - Minimum of a 32GB SSD
    - Minimum 64GB recommended
  - A compatible WiFi card
    - The Dell DW1560 works in MacOS, Windows & Ubuntu
  - MacOS installer flash drive 
    - See the guide linked in [Basic Installation Steps](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310#basic-installation-steps) below

### Notes:
  - You will need to generate your own SMBIOS for the attached config.plist - Use the MacBookAir7,2 profile
     - Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to do this
  - Keyboard backlight is controlled with left ctrl + alt + brightness keys (F6/F7). There are 7 stages, including off
  - OpenCore is set to boot at 1280x1024 - booting at 1920x1080 causes the login screen to load up with extreme graphical glitches so don't bother changing it
  - Most DRM doesn't work. If you need streaming services like Netflix, Hulu, Amazon Prime, etc., then this probably isn't for you. Or dual boot!
  
### What's Working: 
  - Just about everything!
  
### What's Not Working: 
  - Touchscreen - unlikely that this will ever work - fairly uncommon to have one on this device anyway
  - Occasionally the trackpad will get stuck in a drag/highlight mode
    - Sometimes it can be cleared by clicking/dragging randomly. Mostly succesful with clicking the lower portion of the trackpad. Sometimes a restart is required.
    - This might actually be fixed with the current version of VoodooI2C. I haven't experienced this issue in several days.
  - Most DRM does not work. This means no Apple TV shows, Hulu, Netflix (in Safari), Amazon Prime streaming, etc.
      - DRM simply does not work on an iGPU only Hackintosh 
  
### To Do:  
  - Nothing!

#

## Before Getting Started
- I strongly suggest becoming familiar with Hackintoshing before jumping into this. Know the downsides, shortcomings, and difficulties. Read through the [dortania guide](https://dortania.github.io/vanilla-laptop-guide/), poke around on [r/hackintosh](https://reddit.com/r/hackintosh), have a look around [InsanelyMac](https://www.insanelymac.com) and [TonyMacX86](https://www.tonymacx86.com) (even though their tools aren't used here, they have a lot of useful information), and do some general web searches. Even if a lot of it doesn't make sense, just reading through it and becoming familiar with terms will be helpful!
- Know that MacOS updates and firmware updates may break your installation! Before updating MacOS or firmware, check back here to see what the status is! I will likely be keeping my device up to date so check back here before doing any MacOS or firmware updates! The latest compatible MacOS and firmware versions will always be at the top of the this page.
- Don't let this section scare you off! Once MacOS is up and running on your system, it is very stable!


## Basic Installation Steps
- Install/update [MrChromebox coreboot firmware](https://mrchromebox.tech/#fwscript) if you haven't already
 - Create a MacOS installer flash drive by following [this guide](https://dortania.github.io/vanilla-laptop-guide/preparations/online-installer.html)
 - Download [OpenCore 0.5.9](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.5.9) and copy only the files shown in [this screenshot](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/Required%20Files%20From%20OC.png) to your flash drive, keeping the folder structure as seen in the image
 - Download all of the [required files](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310#required-files)
 - Move the required files to their appropriate locations on your installer flash drive
    - Your EFI folder should look like [this](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/EFI.png) - make sure all of the files are there
 - Get the MAC address of your WiFi card - it should be printed on the WiFi card or you can get it from your current OS - you'll need it for the next step
 - Follow the PlatformInfo portion of the [this guide](https://dortania.github.io/vanilla-laptop-guide/OpenCore/config-laptop.plist/broadwell.html#platforminfo) to edit the config.plist from this repo
    - You'll need [ProperTree](https://github.com/corpnewt/ProperTree) to edit the plist file and [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to generate the SMBIOS info
    - Use a MacBookAir7,2 profile
    - In the config.plist, you need to enter values for: SystemProductName, SystemSerialNumber, MLB, SystemUUID, and ROM 
      - Use your MAC address without the colons for the ROM field (You did get your MAC address, right?)
 - Install your new WiFi card if you haven't already
    - I had an odd issue of the Chromebook not booting after initially installing the new WiFi card. If this happens, disconnect the battery and WiFi card and try again.
 - Boot to your installer and install MacOS
 - Boot into MacOS using your installer flash drive and copy the EFI folder from you installer flashdrive to the EFI partition of your internal SSD - you can mount the EFI partition with [MountEFI](https://github.com/corpnewt/MountEFI)
    - More info can be found [here](https://dortania.github.io/OpenCore-Desktop-Guide/post-install/oc2hdd.html#moving-opencore-from-usb-to-macos-drive) 
 - Follow the [post install](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310#post-install) steps below
 
If you want a full guide, I suggest this one: https://dortania.github.io/vanilla-laptop-guide/ -
most of the files in this repo were created using this guide so you won't need to generate them yourself. Simply pull them from here as you go through the guide.
#
## Required Files

### OpenCore Config
Place this in /EFI/OC/
  - [config.plist](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/config.plist)
    - You will need to generate your own SMBIOS section using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) - use a MacBookAir7,2 profile.
    
### OpenCore Drivers
These are included with the OpenCore download unless noted otherwise.
Place these in /EFI/OC/Drivers
- AudioDxe.efi
- [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)
- OpenCanopy.efi
- OpenRuntime.efi
- Ps2KeyboardDxe.efi

### DSDT/SSDT files
Place these in /EFI/OC/ACPI
- [DSDT.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/DSDT.aml)
  - Adds control for keyboard backlight
- [SSDT-EC.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT-EC.aml)
  - Creates a phony EC controller - required to boot Catalina
- [SSDT-PLNF.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/OpenCore/SSDT-PNLF.aml)
  - Enables LCD backlight control
- [SSDT-PLUG.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/SSDT-PLUG.aml)
  - Enables proper CPU power management 
- [SSDT-HPET.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/OpenCore/SSDT-HPET.aml)
  - Fixes IRQ conflicts with MacOS
- [SSDT-SBUS-MCHC.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/OpenCore/SSDT-SBUS-MCHC.aml)
  - This one might not actually be necessary but it doesn't seem to have any negative side-effects

### Required Kexts
Place these in /EFI/OC/Kexts
- [AppleALC.kext](https://github.com/acidanthera/applealc/releases)
- [Lilu.kext](https://github.com/acidanthera/lilu/releases)
- [WhateverGreen.kext](https://github.com/acidanthera/whatevergreen/releases)
- [VirtualSMC.kext](https://github.com/acidanthera/virtualsmc/releases)
  - SMCBatteryManager.kext
  - SMCProcessor.kext
  - SMCSuperIO.kext
- [USBMap.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/USBMap.kext.zip)
- [VoodooI2C.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/VoodooI2C-CB13.zip) 
  - VoodooI2CSynaptics.kext
  - This is a modified VoodooI2C.kext for proper trackpad sensitivity
- [VoodooPS2Controller.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/VoodooPS2Controller-CB13.zip)
  - This is a modified VoodooPS2Controller.kext that changes the keyboard brightness control keys to ones that actually exist on most laptops. In this case, left ctrl + alt + F6/F7 (CB13 brightness keys)
- [CPUFriend.kext](https://github.com/acidanthera/CPUFriend/releases)
- [CPUFriendDataProvider.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/CPUFriendDataProvider.kext.zip)

### Kexts for Dell DW1560 wifi
Place these in /EFI/OC/Kexts 
 - [AirportBrcmFixup.kext](https://github.com/acidanthera/airportbrcmfixup/releases)
 - [BrcmPatchRAM3.kext](https://github.com/acidanthera/BrcmPatchRAM/releases)  
   - BrcmBluetoothInjector.kext
   - BrcmFirmwareData.kext
#
## Post-Install
- Disable force click in trackpad settings
- Disable hibernate with "sudo pmset -a hibernatemode 0"
- Install [Karabiner](https://karabiner-elements.pqrs.org) to map top row keyboard shortcuts
  - Use the "Function keys" tab to map mission control, volume, and brightness keys (F5-F10)
  - Here are preconfigured "Complex modifications" for the first 4 keys (F1-F4) - [First 4 top row Chromebook keys](https://genesy.github.io/karabiner-complex-rules-generator/#eyJ0aXRsZSI6IkNocm9tZWJvb2sgVG9wIFJvdyIsInJ1bGVzIjpbeyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmMSJ9LCJ0byI6W3sia2V5X2NvZGUiOiJvcGVuX2JyYWNrZXQiLCJyZXBlYXQiOmZhbHNlLCJtb2RpZmllcnMiOlsibGVmdF9ndWkiXX1dfV0sImRlc2NyaXB0aW9uIjoiRjEgdG8gQmFjayJ9LHsibWFuaXB1bGF0b3JzIjpbeyJ0eXBlIjoiYmFzaWMiLCJmcm9tIjp7ImtleV9jb2RlIjoiZjIifSwidG8iOlt7ImtleV9jb2RlIjoiY2xvc2VfYnJhY2tldCIsIm1vZGlmaWVycyI6WyJsZWZ0X2d1aSJdLCJyZXBlYXQiOmZhbHNlfV19XSwiZGVzY3JpcHRpb24iOiJGMiB0byBGb3J3YXJkIn0seyJtYW5pcHVsYXRvcnMiOlt7InR5cGUiOiJiYXNpYyIsImZyb20iOnsia2V5X2NvZGUiOiJmMyJ9LCJ0byI6W3sia2V5X2NvZGUiOiJyIiwicmVwZWF0IjpmYWxzZSwibW9kaWZpZXJzIjpbImxlZnRfZ3VpIl19XX1dLCJkZXNjcmlwdGlvbiI6IkYzIHRvIFJlZnJlc2gifSx7Im1hbmlwdWxhdG9ycyI6W3sidHlwZSI6ImJhc2ljIiwiZnJvbSI6eyJrZXlfY29kZSI6ImY0In0sInRvIjpbeyJrZXlfY29kZSI6ImYiLCJtb2RpZmllcnMiOlsibGVmdF9ndWkiLCJsZWZ0X2NvbnRyb2wiXSwicmVwZWF0IjpmYWxzZX1dfV0sImRlc2NyaXB0aW9uIjoiRjQgdG8gRnVsbHNjcmVlbiJ9XX0=)
- Optional: Give OpenCore a [GUI menu](https://dortania.github.io/OpenCore-Desktop-Guide/extras/gui.html)


#


### Credits & Sources (in no particular order and maybe missing some)
- [Apple](https://www.apple.com)
- https://github.com/MrChromebox
- https://github.com/acidanthera
- https://github.com/alexandred
- https://github.com/RehabMan
- https://github.com/corpnewt
- https://www.insanelymac.com/
- https://www.tonymacx86.com/
- https://reddit.com/r/hackintosh
- https://reddit.com/r/chrultrabook
- https://github.com/TheRandMan/VoodooI2C-CB13/
- https://github.com/TheRandMan/VoodooPS2-CB13/
- https://dortania.github.io/vanilla-laptop-guide/
