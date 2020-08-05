### 08/04/2020
- Updated config.plist for OpenCore 0.6.0

### 07/29/2020
- Confirmed working on MacOS 10.15.6
  - Updated through System Preferences - no changes necessary

### 07/04/2020
- Fixed poor headphone audio
  - Changed boot-args entry from **alcid=3** to **alcid=15**


### 07/02/2020

- Fixed the weird click/highlight stick after sleep
  - New modified VoodooI2CSynaptics.kext included in VoodooI2C-CB13.zip
- Fixed lid wake
  - Added **darkwake=1** to boot-args
