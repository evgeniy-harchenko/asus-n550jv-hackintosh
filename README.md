<div align="center">
<img src="https://github.com/alirezatheh/asus-n550jk-hackintosh/blob/readme-header-data/images/header-image.svg">
<h1>Asus N550JV Hackintosh</h1>

[![Bootloader](https://badgen.net/badge/Bootloader/OpenCore/cyan?icon=terminal)](https://github.com/acidanthera/OpenCorePkg)
[![macOS](https://badgen.net/badge/macOS/Ventura/orange?icon=apple)](https://www.apple.com/macos/ventura/)

</div>

A collection of all resources needed to run macOS on an Asus N550JV


## Specifications
- **Processor**: Intel i7 4700HQ (Haswell)
- **Integrated Graphics**: Intel® HD Graphics 4600
- **Dedicated Graphics**: NVIDIA GeForce GTX 750M
- **Ethernet**: Realtek 8111G
- **Audio**: Realtek ALC668
- **Memory**: 16 GB
- **Wi-Fi and Bluetooth**: Intel(R) Dual Band Wireless N 7260
- **Touchpad**: Elan


## Overview
This is more of a compilation of information and configs from various
repositories and forums than a place where real development happens. This
repository should contain everything needed to get macOS up and running on your
specific Asus N550JV configuration.


## Current Status
- [x] Intel® HD Graphics 4600
- [x] Internal Speakers
- [x] Internal Microphone
- [x] Combo Jack Headphones
- [x] Combo Jack Microphone
- [x] Sleep and Wake also with lid
- [x] Touchpad with gestures
- [x] Keyboard with backlight
- [x] F1 Sleep key
- [x] F3 and F4 Backlight keys
- [x] F5 and F6 Brightness keys
- [x] F9 Touchpad key
- [x] F10, F11 and F12 Audio keys
- [x] Wi-Fi and Bluetooth
- [x] Ethernet
- [x] Webcam
- [x] Touchscreen
- [x] All Sensors
- [x] Battery
- [x] NVRAM
- [x] macOS Recovery
- [ ] Card Reader
- [ ] HDMI Output
- [ ] Mini Display Port Output (Not tested)
- [ ] HDMI Audio Output
- [ ] Mini DisplayPort Audio Output (Not tested)
- [ ] NVIDIA GeForce GTX 750M (Disabled)


## Installation
Follow this guide if you have never set up a Hackintosh before.

### USB Creation
To start you need a USB flash drive with at least 16 GB of available storage.
Then you can follow
[this section](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)
from [dortania](https://github.com/dortania)'s guide to create your bootable
USB.

### Configuring EFI
Download
[latest release EFI](https://github.com/evgeniy-harchenko/asus-n550jv-hackintosh/releases/latest)
to get the base EFI folder as well as all additional kexts and patches. If your
hardware differs with mine you should modify EFI folder for your exact hardware
configuration. If you don't know how to do that you should probably learn more
about hackintoshing. you can read
[Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/)
for start. Once everything is configured properly, copy the folder into the EFI
partition you have mounted in the previous step.

### Before Installation
#### BIOS Setting
- Advanced:
	- Wake On Lid Open **[ENABLED]**
	- Intel Virtualization Technology **[ENABLED]**
	- Intel AES-NI **[ENABLED]**
	- VT-d **[DISABLED]**
	- SATA Configuration:
		- SATA mode selection **[AHCI]**
	- Graphics configuration:
		- DMVT Pre-Allocated **[64M]**
	- USB Configuration:
		- Legacy USB Support **[ENABLED]**
		- XHCI Pre-Boot Mode **[ENABLED]**
- Boot:
	- Launch PXE OpROM policy **[DISABLED]**

#### OpenCore Setting
1. Rename
   [`config.plist`](https://github.com/evgeniy-harchenko/asus-n550jv-hackintosh/blob/main/EFI/OC/config.plist)
   to `config-backup.plist`.
2. Rename
   [`install-config.plist`](https://github.com/evgeniy-harchenko/asus-n550jv-hackintosh/blob/main/EFI/OC/install-config.plist)
   to `config.plist`.

### Installation Process
After having created the installer USB flash drive, you are ready to install
macOS on your laptop. Then you can follow
[this section](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html)
from [dortania](https://github.com/dortania)'s guide to install your macOS.

### After Installation
Congratulations! You have successfully booted and installed macOS. At this
point, you just need to follow next final steps to complete your installation.

#### BIOS Setting
For fixing CFG lock follow
[this section](https://dortania.github.io/OpenCore-Post-Install/misc/msr-lock.html)
from [dortania](https://github.com/dortania)'s guide.

#### Root Patching
Open
[OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher]),
then from main menu select `Post-Install Root Patch` > `Start Root Patching`.

#### OpenCore Setting
1. Rename `config-backup.plist` to `config.plist`.
2. Rename `config.plist` to `install-config.plist`.

### Updating masOS
- Before every macOS update, switch the config files like the
  `OpenCore Setting` step before installation.
- After every masOS update apply the [`Root Patching`](#root-patching) again
  and switch the config files like `OpenCore Setting` step after installation.


## Issues
### Audio
Combo Jack is buggy. External microphone is detected, but by default it isn't
active and also not auto switchable. So you need to select it manually in
**System Preferences** and replug it to make it work! I've tried `3`, `20`,
`27`, `28` for `layout-id` but `29` was the best. Then I thought that there is
something wrong with AppleHDA patching and tried to use
[this guide](https://osxlatitude.com/forums/topic/1946-complete-applehda-patching-guide/)
and add a custom codec to [AppleALC](https://github.com/acidanthera/AppleALC),
but that made no difference. I also tried to modify
[ALCPlugFix](https://github.com/Sniki/ALCPlugFix),
[ComboJack](https://github.com/lvs1974/ComboJack) and
[CodecCommander](https://github.com/RehabMan/EAPD-Codec-Commander) for ALC668
but none of them seems to be worked.

### Card Reader
Card Reader is not detected. I've tried
[Sinetek-rtsx](https://github.com/cholonam/Sinetek-rtsx), but no luck. Maybe try
[this](https://www.noobsplanet.com/index.php?threads/fix-internal-external-card-reader-hackintosh-guide.32/)
later.

### Dedicated Graphics
Will never work because of Nvidia Optimus and Apple completely dropped Nvidia
support beginning with Mojave. Thus it's completely disabled to save power.


## Acknowledgements
- [Apple](https://www.apple.com) for macOS and Xcode
- [Acidanthera](https://github.com/acidanthera) for
  [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg),
  [Lilu](https://github.com/acidanthera/Lilu),
  [AppleALC](https://github.com/acidanthera/AppleALC),
  [VirtualSMC](https://github.com/acidanthera/VirtualSMC),
  [VoodooPS2](https://github.com/acidanthera/VoodooPS2),
  [WhateverGreen](https://github.com/acidanthera/WhateverGreen),
  [CPUFriend](https://github.com/acidanthera/CPUFriend),
  [BlueToolFixup](https://github.com/acidanthera/BrcmPatchRAM),
  [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock),
  [NVMeFix](https://github.com/acidanthera/NVMeFix),
  [AMFIPass](https://github.com/dortania/OpenCore-Legacy-Patcher/tree/main/payloads/Kexts/Acidanthera) and
  [MaciASL](https://github.com/acidanthera/MaciASL)
- [Pike R. Alpha](https://github.com/Piker-Alpha),
  [onemanOSX](https://github.com/onemanosx) and
  [Acidanthera](https://github.com/acidanthera) for
  [CPUFriendDataProvider](https://www.olarila.com/topic/5693-guide-ssdt-with-pikes-pm-script-and-use-with-cpufriend/)
- [VoodooI2C Team](https://github.com/VoodooI2C/VoodooI2C/graphs/contributors) for
  [VoodooI2C](https://github.com/VoodooI2C/VoodooI2C)
- [dortania](https://github.com/dortania) for
  [OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) and
  [OpenCore Legacy Patcher](https://github.com/dortania/OpenCore-Legacy-Patcher)
- [OpenIntelWireless](https://github.com/OpenIntelWireless) for
  [AthBluetoothFirmware](https://github.com/OpenIntelWireless/IntelBluetoothFirmware),
  [itlwm](https://github.com/OpenIntelWireless/itlwm) and
  [HeliPort](https://github.com/OpenIntelWireless/HeliPort)
- [Hiep Bao Le](https://github.com/hieplpvip) for
  [AsusSMC](https://github.com/hieplpvip/AsusSMC)
- [Laura Müller](https://github.com/Mieze) for
  [RealtekRTL8111](https://github.com/Mieze/RTL8111_driver_for_OS_X)
- [ami](https://www.ami.com) for
  [AMI Firmware Update (AMU)](https://www.ami.com/resources/support-other/)
- [LongSoft](https://github.com/LongSoft) for
  [UEFITool](https://github.com/LongSoft/UEFITool)
- [CorpNewt](https://github.com/corpnewt) for
  [ProperTree](https://github.com/corpnewt/ProperTree)
- [headzake](https://github.com/headkaze) for
  [Hackintool](https://github.com/headkaze/Hackintool)
- [fatcatsoftware](https://www.fatcatsoftware.com) for
  [Plist Edit Pro](https://www.fatcatsoftware.com/plisteditpro/)
- [mackie100projects](https://mackie100projects.altervista.org) for
  [OpenCore Configurator](https://mackie100projects.altervista.org/opencore-configurator/)
- [superrnovae](https://github.com/superrnovae) for
  [asusn550jv-hackintosh](https://github.com/superrnovae/asusn550jv-hackintosh/)
- [rubinda](https://github.com/rubinda) for
  [hackintosh-n550](https://github.com/rubinda/hackintosh-n550/)
