# Dell Optiplex 7050 Micro OpenCore 0.6.3

![Optiplex Showoff](images/main.jpeg)

This repository contains my personal EFI configuration for the fantastic Dell Optiplex 7050 Micro.

The current version installed is Catalina 10.15.7 (19H2) with OpenCore 0.6.3.

I use Macmini8,1 as my SMBIOS.

This was setup using the latest BIOS: `1.14.0`

This has mostly been created with the help of the [Vanilla Hackintosh Guide by Dortania](https://dortania.github.io/OpenCore-Install-Guide/) and my own personal experience.

## Hardware Configuration

![About This Mac](images/aboutmac.png)

- Intel i7-7700 CPU (Not the T version, the full desktop 65W version)
- 16GB RAM DDR4 Samsung 2666 MHz, but running at 2400 MHz, because Intel limits the speed
- Intel HD Graphics 630 1536 MB
- Sabrent Rocket 512GB in the NVMe slot
- Samsung 860 QVO 1TB in the SATA slot
- Dell DW1560 802.11ac WiFi + Bluetooth 4.0 LE
- Intel I219-LM Gigabit Ethernet
- Integrated speaker at the front, works perfectly with `alcid=11`
- 1 Displayport 1.2
- 1 HDMI 1.4
- 1 addon Displayport port, works in Windows, doesn't work in macOS, came with the specific Optiplex I bought
- 1 USB-C Port and 1 USB-A port at the front
- 1 headphone jack and 1 microphone port at the front
- 4 USB-A ports at the back
- 130 watt Dell power supply

## What works and what doesn't

### Working

- [x] APFS
- [x] CPU power management
- [x] GPU acceleration
- [x] Video encoder/decoder hardware
- [x] All USB ports at their max speed (manually mapped)
- [x] Gigabit Ethernet
- [x] Secure Boot
- [x] WiFi and Bluetooth (I use DW1560, but the included Intel chips may work with [OpenIntelWireless](https://github.com/OpenIntelWireless/itlwm))
- [x] Location Services
- [x] Onboard Audio + Integrated Speaker at the front
- [x] iMessage (set your Serial Number, UUID and MLB correctly)
- [x] All iCloud Services
- [x] App Store
- [x] FaceTime
- [x] Handoff
- [x] Unlock with Apple Watch
- [x] AirDrop
- [x] AirPlay
- [x] Continuity
- [x] DRM:
  - iTunes Movies (FairPlay 1)
  - Netflix (FairPlay 2/3)
  - Amazon Prime (FairPlay 2/3)
  - Apple TV+ (FairPlay 4)
- [x] NVRAM
- [x] FileVault
- [x] Dell Sensors (Fans/Temperature)
- [x] Built in Displayport 1.4 and HDMI 1.2
- [x] TRIM working on Sabrent NVMe
- [x] TRIM enabled for SATA SSD with `sudo trimforce enable`
- [x] Sidecar
- [x] Various sharing functions like Content Caching (very useful if you have lots of Apple devices)
- [x] Time Machine
- [x] Seamless software updates

### Not Working

- [ ] Sleep/Wake (haven't tested, but I don't think it does)
- [ ] Booting up without a monitor (or dummy Displayport). This takes a much longer time to boot and the system is very laggy if there is no monitor plugged in. Seems like the iGPU is not activated, which makes everything lag. Disabling WiFi improves things, but that's not ideal as I am running this in headless mode (VNC in from time to time). I had to buy a dummy Displayport which activates the iGPU and performs normally with it. Let me know if there is a way to do it without the dummy plug or maybe the actual Macmini can't run headless either.

## Using the EFI

Only things you need to set manually is the System Serial Number, System UUID, MLB and ROM. I have set them as {CHANGE ME} and OpenCore will complain if you do not set them correctly. You can get the first three created with [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). The ROM part can be your Ethernet or WiFi MAC Address such as E4 85 G6 M8 H9 2Q, for example. Refer to the [Vanilla Hackintosh Guide by Dortania](https://dortania.github.io/OpenCore-Install-Guide/) if you need more help.

## Preparation

- Update to the latest BIOS if you can
- Once on the latest BIOS, reset it defaults (maybe even go as far as taking the battery out a few minutes to hard reset)
- Avoid Samsung PM drives as they did not let me go past the installer, it would always crash (may be fixed with NVMEFix.kext, I just bought Sabrent instead)

## UEFI Variables

## Miscellaneous

To be completed...
