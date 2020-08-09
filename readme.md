# Dell Chromebook 13 7310 Hackintosh

### Confirmed working on:
- MacOS: **Catalina 10.15.6**
- MacOS beta: **Big Sur 11.0 (Public Beta)**
- MrChromebox coreboot: **4.12**
- OpenCore: **0.6.0**

#
This is not meant to be a thorough guide or walkthrough. It is merely a dump of files and notes to get MacOS working on a Dell Chromebook 13 7310. I will try to keep this updated as I update my Chromebook to future MacOS releases. It may or may not work on your specific device. If it doesn't, you likely need to make some sort of changes to the supplied config.plist.


#
### Update 08/07/2020
- Confirmed working on MacOS 11.0 Big Sur Public Beta
  - Configs updated
  - VoodooPS2Controller big update
    - Most top row keys are now mapped through the kext
    - Keyboard backlight now controlled with left ctrl + alt + "comma" and "period" keys
  - Karabiner no longer required!

### Update 08/05/2020
- Switched to SSDT-KBBL.aml for keyboard backlight control
  - DSDT.aml no longer required

### Update 08/04/2020
- Updated configs for OpenCore 0.6.0
- Switched to [VoodooRMI](https://github.com/VoodooSMBus/VoodooRMI/releases) as the trackpad kext
  - More on this in the Required Kexts section below
  - No longer using a modified VoodooI2CSynaptics.kext
- In an attempt to make this easier to maintain, this will be the last time multiple configs are supplied
   
### Update 07/29/2020
- Confirmed working on 10.15.6. I updated successfully through System Preferences.

#

### Requirements:
  - Core i3 or Core i5 processor
  - [MrChromebox's coreboot firmware 4.12](https://mrchromebox.tech/#fwscript)
  - [OpenCore 0.6.0](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.6.0) 
  - Minimum of a 32GB SSD
    - Minimum 64GB recommended
  - A [compatible m.2 WiFi card](https://dortania.github.io/Wireless-Buyers-Guide/types-of-wireless-card/m2.html#supported-cards)
    - I can confirm the Dell DW1560 works in MacOS (with additional kexts), Windows, & Ubuntu
    - Other users have reported success with the BCM94360NG (has native MacOS support so no additional kexts required!)
  - MacOS installer flash drive 
    - See the guides linked in [Basic Installation Steps](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310#basic-installation-steps) below

### Notes:
  - You will need to generate your own SMBIOS for the attached config.plist - Use the MacBookAir7,2 profile
     - Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to do this
  - Keyboard backlight is controlled with left ctrl + alt + "comma" and "period" keys. There are 7 stages, including off
  - Most top row keys are mapped with the custom VoodooPS2Controll.kext
    - Back arrow = Previous track
    - Forward arrow = Next track
    - Refresh key = Play/Pause
    - Brightness down = Brightness down
    - Brightness up = Brightness up
    - Mute key = Mute
    - Volume down = Volume down
    - Volume up = Volume up
  - OpenCore is set to boot at 1280x1024 - booting at 1920x1080 causes the login screen to load up with extreme graphical glitches so don't bother changing it
  - Most DRM doesn't work. If you need streaming services like Netflix, Hulu, Amazon Prime, etc., then this might not be for you. Or dual boot!

### What's Working: 
  - Just about everything!
  
### What's Not Working: 
  - Touchscreen - unlikely that this will ever work - fairly uncommon to have one on this device anyway
  - Most DRM does not work. This means no Apple TV shows, Hulu, Netflix (in Safari), Amazon Prime streaming, etc.
      - This isn't specific to the Dell CB13. DRM simply does not work on an iGPU only Hackintosh 
  
### To Do:  
  - Enjoy a very low price HackBook!

#

## Before Getting Started
- I strongly suggest becoming familiar with Hackintoshing before jumping into this. Know the downsides, shortcomings, and difficulties. Read through the [dortania guide](https://dortania.github.io/OpenCore-Install-Guide/), poke around on [r/hackintosh](https://reddit.com/r/hackintosh), have a look around [InsanelyMac](https://www.insanelymac.com) and [TonyMacX86](https://www.tonymacx86.com) (even though their tools aren't used here, they still have a lot of useful information), and do some general web searches. Even if a lot of it doesn't make sense, just reading through it and becoming familiar with terms will be helpful!
- Updates to MacOS, OpenCore, or firmware may break your installation! I will likely be keeping my device up to date so check back here before doing any MacOS, OpenCore, or firmware updates! The latest compatible MacOS, OpenCore, and firmware versions will always be at the top of the this page.
- Don't let this section scare you off! Once MacOS is up and running on your system, it is very stable!


## Basic Installation Steps
- Install/update [MrChromebox coreboot firmware](https://mrchromebox.tech/#fwscript) if you haven't already
- Create a MacOS installer flash drive
  - A guide can be found [here](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#creating-the-usb)
- Download [OpenCore 0.6.0](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.6.0) and copy only the files shown in [this screenshot](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/Images/Required%20Files%20From%20OC.png) to your flash drive, keeping the folder structure as seen in the image
- Download all of the [required files](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310#required-files)
- Move the required files to their appropriate locations on your installer flash drive
   - Your EFI folder should look like [this](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/Images/EFI.png) - make sure all of the files are there (leave out the 4 highlighted WiFi/Bluetooth kexts if you're using a BCM94360NG)
- Get the MAC address of your WiFi card - it should be printed on the WiFi card or you can get it from your current OS - you'll need it for the next step
- Follow the PlatformInfo portion of the [this guide](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/broadwell.html#platforminfo) to edit the config.plist from this repo
   - You can use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to generate the SMBIOS info and [ProperTree](https://github.com/corpnewt/ProperTree) to confirm GenSMBIOS worked properly or paste the SMBIOS info into the proper locations in your plist file
   - Use a MacBookAir7,2 profile
   - In the config.plist, you need to fill in values for: SystemProductName, SystemSerialNumber, MLB, SystemUUID, and ROM 
     - Use your MAC address without the colons for the ROM field (You did get your MAC address, right?)
- Install your new WiFi card if you haven't already
   - I had an odd issue of the Chromebook not booting after initially installing the new WiFi card. If this happens, disconnect the battery and WiFi card and try again.
- Boot to your installer and install MacOS
- Boot into MacOS using your installer flash drive and copy the EFI folder from you installer flashdrive to the EFI partition of your internal SSD - you can mount the EFI partition with [MountEFI](https://github.com/corpnewt/MountEFI)
    - More info can be found [here](https://dortania.github.io/OpenCore-Post-Install/universal/oc2hdd.html) 
- Follow the [post install](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310#post-install) steps below
 
## Post-Install
- Disable force click in trackpad settings
- Disable hibernate with "sudo pmset -a hibernatemode 0"
- Map Full Screen and Mission Control keys
  - Map Full Screen button (F4) to full screen in [System Preferences > Keyboard > Shortcuts > App Shortcuts](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/Images/Full_Screen.png)
  - Map Mission Control key (F5) Mission Controlin System Preferences > Keyboard > Shortcuts > [Mission Control](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/Images/Mission_Control.png) 
- Optional: Give OpenCore a [GUI menu and boot chime](https://dortania.github.io/OpenCore-Desktop-Guide/extras/gui.html)
  - Use the this [OCEFIAudio_VoiceOver_Boot.wav](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/OCEFIAudio_VoiceOver_Boot.wav) as it is resampled to work with the CB13

If you want a full Hackintosh guide (not Chromebook specific), I suggest this one: https://dortania.github.io/OpenCore-Install-Guide/ -
most of the files in this repo were created using this guide so you won't need to generate them yourself. Simply pull them from here as you go through the guide.

#
## Required Files

### OpenCore Config
Place a config.plist in /EFI/OC/
  - Download an OpenCore config file from here [config.plist](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/tree/master/configs)
    - Some i3 models require the iGPU to be faked to HD 6000. If you have trouble booting MacOS use the i3Alt config. Fix found by @mankot14
    - Be sure to rename your config file to config.plist
    - You will need to generate your own PlatformInfo section using [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) - use a MacBookAir7,2 profile.
    
### OpenCore Drivers
These are included with the OpenCore download unless noted otherwise.
Place these in /EFI/OC/Drivers
- AudioDxe.efi
- [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)
- OpenCanopy.efi
- OpenRuntime.efi

### SSDT files
Place these in /EFI/OC/ACPI
- [SSDT-EC.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT_Files/SSDT-EC.aml)
  - Creates a phony EC controller - required to boot Catalina
- [SSDT-PLNF.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT_Files/SSDT-PNLF.aml)
  - Enables LCD backlight control
- [SSDT-PLUG.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT_Files/SSDT-PLUG.aml)
  - Enables proper CPU power management 
- [SSDT-HPET.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT_Files/SSDT-HPET.aml)
  - Fixes IRQ conflicts with MacOS
- [SSDT-KBBL.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT_Files/SSDT-KBBL.aml)
  - Required for keyboard backlight control
- [SSDT-SBUS-MCHC.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT_Files/SSDT-SBUS-MCHC.aml)
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
- [USBMap.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/USBMap.zip)
- [VoodooI2C.kext](https://github.com/VoodooI2C/VoodooI2C/releases)
- [VoodooRMI.kext](https://github.com/VoodooSMBus/VoodooRMI/releases)
  -  For version 1.0.1, you will need to add SYNA0000 to the info.plist file found in VoodooRMI.kext/Contents/PlugIns/RMII2C.kext/Contents
    - Simply open the info.plist file and replace the one instance of SYNA2B33 with SYNA0000
    - This shouldn't be necessary for future versions
- [VoodooPS2Controller.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/VoodooPS2Controller-CB13.zip)
  - This is a modified VoodooPS2Controller.kext that changes the keyboard brightness control keys to ones that actually exist on most laptops. In this case, left ctrl + alt + "comma" / "period" keys
- [CPUFriend.kext](https://github.com/acidanthera/CPUFriend/releases)
- [CPUFriendDataProvider.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/CPUFriendDataProvider.zip)

### Kexts for Dell DW1560 wifi
Place these in /EFI/OC/Kexts 
 - [AirportBrcmFixup.kext](https://github.com/acidanthera/airportbrcmfixup/releases)
 - [BrcmPatchRAM3.kext](https://github.com/acidanthera/BrcmPatchRAM/releases)  
   - BrcmBluetoothInjector.kext
   - BrcmFirmwareData.kext

#
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
- https://github.com/TheRandMan/VoodooPS2-CB13/
- https://dortania.github.io/vanilla-laptop-guide/
