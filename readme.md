# Dell Chromebook 13 7310 Hackintosh

This is NOT meant to be a guide or walkthrough but merely a dump of files and notes to get MacOS working on a Dell Chromebook 13. I will try to keep this updated as I update my Chromebook to future MacOS releases.

Working on MacOS 10.15.4


# Requirements
  - Core i3 or Core i5 Processor 
    - Will NOT work with the Celeron model
  - Minimum of a 32GB SSD
    - Minimum 64GB recommended
  - A compatible WiFi card
    - If you're planning on booting an additional OS I recommend a Dell DW1560 - for other compatible cards, do your own research
  - MacOS installer flash drive 
    - There are plenty of guides on how to make this so that won't be covered here
  - USB mouse (the built in touchpad will not work in the installer)

## Notes
  - You will need to generate your own SMBIOS in the attached config.plist - Use the MacBook Air 7,2 profile 
    - Use [Clover Configurator](https://github.com/CloverHackyColor/CloverBootloader/releases) to do this
  - The DSDT is for MrChromebox's firmware version 4.11.2 (other versions may work but YMMV)

## What's Working: 
  - Just about everything!
  
## What's Not Working:
  - Touchscreen - unlikely to be fixed 
  - Keyboard Backlight Control - turns off after closing the lid
  - Clicking and dragging with 1 finger doesn't release until your finger is removed from the trackpad
    - Temporary fix here: [https://github.com/VoodooI2C/VoodooI2C/issues/290](https://github.com/VoodooI2C/VoodooI2C/issues/290)


## To Do:  
  - Get better trackpad speed (Currently 100% usable but just not 100% perfect)
    - I'm using [SmoothCursor](https://smoothcursor.com) set to 0.05 to get a speed/acceleration that feels right to me
  - Get off-center Apple logo at boot to be centered
    - Setting Clover resolution to 1080p and booting centers the Apple logo but causes major graphical glitches at the login screen
  - Mapping of the top row keys requires an app. I'd like to do this natively by modifying VoodooPS2.kext
     - [https://github.com/RehabMan/OS-X-Voodoo-PS2-Controller/wiki/How-to-Use-Custom-Keyboard-Mapping](https://github.com/RehabMan/OS-X-Voodoo-PS2-Controller/wiki/How-to-Use-Custom-Keyboard-Mapping)
  
## Clover Installation Options
![image](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/Clover_Setup.jpg)

## Clover Config
  - [config.plist](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/config.plist)
    - You will need to generate your own SMBIOS section - use the Macbook Air 7,2 profile

## Full list of DSDT / SSDT files
- [DSDT.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/DSDT.aml)
- SSDT-PLNF.aml
  - https://bitbucket.org/RehabMan/applebacklightfixup/downloads/
- [SSDT-UIAC.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT-UIAC.aml)
  - For properly mapped USB ports (internal and external) - Not perfect but I don't think it'll cause issues

## List of Required Kexts
### Installed from Clover Configurator
- AirportBrcmFixup.kext
- AppleALC.kext
- Lilu.kext
- USBInjectAll.kext
- WhateverGreen.kext
- VirtualSMC.kext
  - SMCBatteryManager.kext
  - SMCProcessor.kext
  - SMCSuperIO.kext
  
### Installed from elsewhere:
- BrcmBluetoothInjector.kext
- BrcmFirmwareData.kext
- BrcmPatchRAM3.kext
  - https://github.com/acidanthera/BrcmPatchRAM/releases
- VoodooI2C.kext
  - VoodooI2CSynaptics.kext
    - https://github.com/alexandred/VoodooI2C/releases
- VoodooPS2Controller.kext
  - https://github.com/acidanthera/VoodooPS2/releases
#
#
# 
#
# What does what?
## Keyboard
- Voodoops2Controller.kext
  - https://github.com/acidanthera/VoodooPS2/releases
- Keyboard shortcuts with Karabiner-Elements
  - https://karabiner-elements.pqrs.org

## Touchpad
- VoodooI2C.kext
- VoodooI2CSynaptics.kext 
  - https://github.com/alexandred/VoodooI2C/releases
- The required "Windows" edits are applied to the dsdt.aml in this repo

## Sound
- AppleALC.kext
  - https://github.com/acidanthera/applealc/releases
- Audio layout 3

## LCD Backlight Control
- SSDT-PNLF.aml
  - https://bitbucket.org/RehabMan/applebacklightfixup/downloads/

## WiFi
You need swap in a compatible WiFi card - I'll be using a Dell DW1560 so the following kexts are required
- AirportBrcmFixup.kext
- BrcmBluetoothInjector.kext
- BrcmFirmwareData.kext
- BrcmPatchRAM3.kext
  - https://github.com/acidanthera/BrcmPatchRAM/releases
  - https://github.com/acidanthera/AirportBrcmFixup/releases
#
#
#
#
## Credits & Sources (in no particular order and maybe missing some)
- https://github.com/acidanthera/
- https://github.com/alexandred/
- https://github.com/MrChromebox/
- https://github.com/RehabMan
- https://www.insanelymac.com/
- https://reddit.com/r/hackintosh
- https://tonymacx86.com/
- https://www.tonymacx86.com/threads/guide-intel-broadwell-nuc5-using-clover-uefi-nuc5i5mhye-nuc5i3myhe-etc.261712/
