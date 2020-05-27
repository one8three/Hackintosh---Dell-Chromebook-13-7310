# Dell Chromebook 13 7310 Hackintosh
#
# Updated for OpenCore!

This is NOT meant to be a guide or walkthrough but merely a dump of files and notes to get MacOS working on a Dell Chromebook 13. I will try to keep this updated as I update my Chromebook to future MacOS releases.

Working on MacOS 10.15.4


# Requirements
  - Core i3 or Core i5 Processor 
    - Will NOT work with the Celeron model
  - Minimum of a 32GB SSD
    - Minimum 64GB recommended
  - A compatible WiFi card
    - The Dell DW1560 works in MacOS, Windows & Ubuntu
  - MacOS installer flash drive 
    - There are plenty of guides on how to make this so that won't be covered here
  - USB mouse (the built in touchpad will not work in the installer)

## Notes
  - I'm now using OpenCore to boot! For Clover see the Clover branch
  - You will need to generate your own SMBIOS in the attached config.plist - Use the MacBook Air 7,2 profile 
    - Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to do this
  - The SSDTs are made from version 4.11.2 MrChromebox's firmware (other versions may work but YMMV)

## What's Working: 
  - Just about everything!
  
## What's Not Working:
  - Touchscreen - unlikely to be fixed
  - Keyboard Backlight Control - turns off after closing the lid
  - Occasional trackpad click stick after waking from sleep
    - Likely caused by this temporary fix to VoodooInput here: [https://github.com/VoodooI2C/VoodooI2C/issues/290](https://github.com/VoodooI2C/VoodooI2C/issues/290)


## To Do:  
  - Keyboard backlight control   

## Clover Config
  - [config.plist](Coming soon....)
    - You will need to generate your own SMBIOS section - use a Macbook Air 7,2 profile - 

## Full list of DSDT / SSDT files
- [SSDT-PLNF.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/OpenCore/SSDT-PNLF.aml)
- [SSDT-UIAC.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/SSDT-UIAC.aml)
  - For properly mapped USB ports (internal and external) - Not perfect but I don't think it'll cause issues
- [SSDT-PLUG](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/blob/master/SSDT-PLUG.aml?raw=true)
  - For proper CPU power management
- [SSDT-USB.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/OpenCore/SSDT-USB.aml)
  - For proper USB mapping
- [SSDT-SBUS-MCHC.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/OpenCore/SSDT-SBUS-MCHC.aml)
- [SSDT-HPET.aml](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/OpenCore/SSDT-HPET.aml)

  
## List of Required Kexts
### Installed from Clover Configurator
- AirportBrcmFixup.kext
- AppleALC.kext
- Lilu.kext
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
  - Use my modified versions of these kexts [here](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/VoodooI2C.zip) for appropriate sensitivity
    - https://github.com/alexandred/VoodooI2C/releases
- VoodooPS2Controller.kext
  - https://github.com/acidanthera/VoodooPS2/releases
- CPUFriend.kext 
  - https://github.com/acidanthera/CPUFriend/releases
- [CPUFriendDataProvider.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/CPUFriendDataProvider.kext.zip)
#
#
# 
#
# What does what?
## Keyboard
- Voodoops2Controller.kext
  - https://github.com/acidanthera/VoodooPS2/releases
- Top row keyboard shortcuts with Karabiner-Elements
  - https://karabiner-elements.pqrs.org

## Touchpad
- [VoodooI2C.kext](https://github.com/TheRandMan/Hackintosh---Dell-Chromebook-13-7310/raw/master/VoodooI2C.zip)
  - VoodooI2CSynaptics.kext 
  - This is my modified one for appropriate sensitivity

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
- https://github.com/corpnewt/CPUFriendFriend
- https://dortania.github.io/Getting-Started-With-ACPI/
