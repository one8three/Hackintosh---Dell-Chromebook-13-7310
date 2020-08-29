# Dell Chromebook 13 7310 Hackintosh

### Confirmed working on:
- MacOS: **Catalina 10.15.6**
- MacOS beta: **Big Sur 11.0 (Public Beta)**
- MrChromebox coreboot: **4.12**
- OpenCore: **0.6.0**

#
**Disclaimer:** This is not meant to be a thorough guide or walkthrough. It is merely a dump of files and notes to get MacOS working on a Dell Chromebook 13 7310. I will try to keep this updated as I update my Chromebook to future MacOS releases. It's not guaranteed to work on your specific device. If it doesn't, you likely need to make some sort of changes to the supplied config.plist. I do not know what those changes may be. I am not responsible for any damage done or data lost by attempting this.


#
### Update 08/28/2020
- Spoofed iGPU to HD 6000 as default
  - Required for some devices but has no negative effects on devices that do not require it
- Mentioned Intel wifi kext in readme
  - Won't be supported here but is worth a mention and should work fine.

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
    - **Note:** There is now an Intel wifi kext and the stock wireless card is listed as compatible. I don't have experience with using this so it won't be covered here.
      - https://github.com/OpenIntelWireless/itlwm
  - MacOS installer flash drive 
    - See the guides linked in [Basic Installation Steps](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310#basic-installation-steps) below

### Notes:
  - Keyboard backlight is controlled with left ctrl + alt + "comma" and "period" keys. There are 7 stages, including off
  - Most top row keys are mapped with the custom VoodooPS2Controller.kext
    - Back arrow key = Previous track
    - Forward arrow key = Next track
    - Refresh key = Play/Pause
    - Brightness down key = Brightness down
    - Brightness up key = Brightness up
    - Mute key = Mute
    - Volume down key = Volume down
    - Volume up key = Volume up
  - OpenCore is set to boot at 1280x1024 - booting at 1920x1080 causes the login screen to load up with extreme graphical glitches so don't bother changing it
  
### What's Working: 
  - Just about everything!
  
### What's Not Working: 
  - Touchscreen - unlikely that this will ever work as there is no kext for it - fairly uncommon to have one on this device anyway
  - Most DRM does not work. This means no Apple TV shows, Hulu, Netflix (in Safari), Amazon Prime streaming, etc.
      - This isn't specific to the Dell CB13. DRM simply does not work on an iGPU only Hackintosh 
  
### To Do:  
  - Enjoy MacOS!

#

## Before Getting Started
- I strongly suggest becoming familiar with Hackintoshing before jumping into this. Know the downsides, shortcomings, and difficulties. Read through the [dortania guide](https://dortania.github.io/OpenCore-Install-Guide/), poke around on [r/hackintosh](https://reddit.com/r/hackintosh), have a look around [InsanelyMac](https://www.insanelymac.com) and [TonyMacX86](https://www.tonymacx86.com) (even though their tools aren't used here, they still have a lot of useful information), and do some general web searches. Even if a lot of it doesn't make sense, just reading through it and becoming familiar with terms will be helpful!
- Updates to MacOS, OpenCore, or firmware may break your installation! I will likely be keeping my device up to date so check back here before doing any MacOS, OpenCore, or firmware updates! The latest confirmed working versions will always be at the top of the this page.
- Don't let this section scare you off! Once MacOS is up and running on your system, it is very stable!


## Basic Installation Steps
- Install/update [MrChromebox coreboot firmware](https://mrchromebox.tech/#fwscript) if you haven't already
- Get the MAC address of your WiFi card - it should be printed on the WiFi card or you can get it from your current OS - you'll need this later
- Create a MacOS installer flash drive
  - A guide can be found [here](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#creating-the-usb)
- Download [OpenCore 0.6.0](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.6.0) and copy only the files shown in [this screenshot](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/Images/Required%20Files%20From%20OC.png) to your flash drive, keeping the folder structure as seen in the image
- Download all of the [required files](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310#required-files)
  - Be sure to make any edits mentioned - particularly to config.plist and VoodooI2CSynaptics.kext
- Move the required files to their appropriate locations on your installer flash drive
   - Your EFI folder should look like [this](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/Images/EFI.png) - make sure all of the files are there (leave out the 4 highlighted WiFi/Bluetooth kexts if you're using a BCM94360NG)
- Install your new WiFi card if you haven't already
   - I had an odd issue of the Chromebook not booting after initially installing the new WiFi card. If this happens, disconnect the battery and WiFi card and try again.
- Boot to your installer and install MacOS
- Boot into MacOS using your installer flash drive and copy the EFI folder from you installer flash drive to the EFI partition of your internal SSD - you can mount the EFI partition with [MountEFI](https://github.com/corpnewt/MountEFI)
    - More info can be found [here](https://dortania.github.io/OpenCore-Post-Install/universal/oc2hdd.html) 
- Follow the [post install](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310#post-install) steps below
 
## Post-Install
- Disable force click in trackpad settings
- Disable hibernate with "sudo pmset -a hibernatemode 0"
- Map Full Screen and Mission Control keys
  - Map Full Screen button (F4) to full screen in: **System Preferences > Keyboard > Shortcuts > App Shortcuts**
    - [Example screenshot](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/Images/Full_Screen.png)
  - Map Mission Control key (F5) Mission Control in: **System Preferences > Keyboard > Shortcuts > Mission Control**
    - [Example screenshot](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/Images/Mission_Control.png) 
- Optional: Give OpenCore a [GUI menu and boot chime](https://dortania.github.io/OpenCore-Desktop-Guide/extras/gui.html)
  - Use this [OCEFIAudio_VoiceOver_Boot.wav](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/Misc%20FIles/OCEFIAudio_VoiceOver_Boot.wav) as it is resampled to work with the CB13

If you want a full Hackintosh guide (not Chromebook specific), I suggest this one: https://dortania.github.io/OpenCore-Install-Guide/ -
most of the files in this repo were created using this guide so you won't need to generate them yourself. Simply pull them from here as you go through the guide.

#
## Required Files

### OpenCore Config
Place config.plist in /EFI/OC/
  - [config-base.plist](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/tree/master/config-base.plist)
    - Use [ProperTree](https://github.com/corpnewt/ProperTree) to make the following edits to the config-base.plist file
    - If you are using a BCM94360NG for wifi:
      - Delete the following kext entries from the config:
        - AirportBrcmFixup.kext
        - AirPortBrcm4360_Injector.kext
        - BrcmBluetoothInjector.kext
        - BrcmFirmwareData.kext
        - BrcmPatchRAM3.kext
      - Remove "brcmfx-driver=2 -brcmfxbeta" from the boot-args field
    - Follow the PlatformInfo portion of [this guide](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/broadwell.html#platforminfo) to edit the config.plist
      - You can use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to generate the SMBIOS info
       - Use a MacBookAir7,2 profile
       - In the config.plist, you need to fill in values for: SystemProductName, SystemSerialNumber, MLB, SystemUUID, and ROM 
       - Use your MAC address without the colons for the ROM field (You did get your MAC address, right?)
     - Be sure to rename the config file to config.plist
    
    
### OpenCore Drivers
These are included with the OpenCore download unless noted otherwise.
Place these in /EFI/OC/Drivers
- AudioDxe.efi
- [HfsPlus.efi](https://github.com/acidanthera/OcBinaryData/blob/master/Drivers/HfsPlus.efi)
- OpenCanopy.efi
- OpenRuntime.efi

### SSDT files
Place these in /EFI/OC/ACPI
- [SSDT-EC.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT%20Files/SSDT-EC.aml)
  - Creates a phony EC controller - required to boot Catalina
- [SSDT-PLNF.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT%20Files/SSDT-PNLF.aml)
  - Enables LCD backlight control
- [SSDT-PLUG.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT%20Files/SSDT-PLUG.aml)
  - Enables proper CPU power management 
- [SSDT-HPET.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT%20Files/SSDT-HPET.aml)
  - Fixes IRQ conflicts with MacOS
- [SSDT-KBBL.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT%20Files/SSDT-KBBL.aml)
  - Required for keyboard backlight control
- [SSDT-SBUS-MCHC.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT%20Files/SSDT-SBUS-MCHC.aml)
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
- [USBMap.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/CB13%20specific%20%20kexts/USBMap.zip)
- [VoodooI2C.kext](https://github.com/VoodooI2C/VoodooI2C/files/5061517/Archive.zip)
  - VoodooI2CSynaptics.kext
    -  You will need to add SYNA0000 to the info.plist file found in VoodooI2CSynaptic.kext/Contents/
      - Simply open the info.plist file and replace the one instance of SYNA2B33 with SYNA0000
- [VoodooPS2Controller.kext](https://github.com/TheRandMan/VoodooPS2-Chromebook/releases)
  - Custom for Chromebooks
- [CPUFriend.kext](https://github.com/acidanthera/CPUFriend/releases)
- [CPUFriendDataProvider.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/CB13%20specific%20%20kexts/CPUFriendDataProvider.zip)

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
