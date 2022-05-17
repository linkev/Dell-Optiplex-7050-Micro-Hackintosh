# Dell Optiplex 7050 Micro OpenCore 0.8.0

![Optiplex Showoff](images/main.jpeg)

This repository contains my personal EFI configuration for the fantastic Dell Optiplex 7050 Micro.

The current version installed is Monterey 12.4 (21F79) with OpenCore 0.8.0. Catalina was installed prior to Big Sur and it worked perfectly. I aim to have as clean of configuration as possible and so far everything has been working great.

I use iMac18,1 as my SMBIOS. Macmini8,1 is also a good alternative, depends what you want it to show up as (have used both SMBIOS with no issues).

This was setup using the latest Dell BIOS at the time: [1.14.0](https://www.dell.com/support/home/en-tc/drivers/driversdetails?driverid=80chv&oscode=wt64a&productcode=optiplex-7050-desktop). I have successfully updated to [1.15.1](https://www.dell.com/support/home/en-uk/drivers/driversdetails?driverid=jkt52&oscode=wt64a&productcode=optiplex-7050-desktop) and then [1.15.2](https://www.dell.com/support/home/en-uk/drivers/driversdetails?driverid=2xjd2&oscode=wt64a&productcode=optiplex-7050-desktop) after the fact with no issues (via Windows or the built in BIOS Update Utility). If you are starting from scratch, I recommend updating to the latest BIOS before anything else.

This has mostly been created with the help of the [Vanilla Hackintosh Guide by Dortania](https://dortania.github.io/OpenCore-Install-Guide/) and my own personal experience.

**MAKE SURE YOU ADD YOUR SYSTEM SERIAL NUMBER, SYSTEM UUID, MLB AND ROM IN PLATFORMINFO BEFORE BOOTING!**

You may also need to remove the AirportBrcmFixup.kext, BlueToolFixup.kext, BrcmBluetoothInjector.kext, BrcmFirmwareData.kext and BrcmPatchRAM3.kext if you are not using a Dell WiFi card or any WiFi at all.

Don't forget to check the NVRAM values as well:
- Remove `-v` after you're fully done installing macOS, to turn off Verbose.
- You need to remove `brcmfx-country=#a` if you are not using a DW1560/DW1820A, but an [Intel WiFi chip instead](https://github.com/OpenIntelWireless/itlwm), or no WiFi at all (just Ethernet).
- Modify `alcid=11` in case your audio chip is different, although I think all of the 7050's I've seen use the same Realtek ALC3234 controller.
- Remove `igfxonln=1` if you have a monitor plugged in all the time (not a dummy dongle, not sure if this flag helps anything really).

Double/triple check everything to make sure, its a relatively light setup, but better safe than sorry!

## Hardware Configuration

![About This Mac](images/aboutmac.png)

- Intel i7-7700 CPU (Not the T version, the full desktop 65W version) (I don't think the CPU matters, they're all relatively the same)
- 32GB RAM DDR4 SK Hynix 3200 MHz, but running at 2400 MHz, because Intel limits the speed
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
- [x] Built in Displayport 1.2 and HDMI 1.4
- [x] TRIM working on Sabrent NVMe
- [x] TRIM enabled for SATA SSD with `sudo trimforce enable`
- [x] Sidecar
- [x] Various sharing functions like Content Caching (very useful if you have lots of Apple devices)
- [x] Time Machine
- [x] Seamless software updates
- [x] Monterey's AirPlay to Mac with [FeatureUnlock](https://github.com/acidanthera/FeatureUnlock)

### Not Working

- [ ] Sleep/Wake (I haven't tested, but I don't think it does).
- [ ] Booting up without a monitor (or dummy Displayport dongle). This takes a much longer time to boot and the system is very laggy if there is no monitor plugged in. Seems like the iGPU is not activated, which makes everything lag. Disabling WiFi improves things, but that's not ideal as I am running this in headless mode (I connect via [VNC](https://www.realvnc.com/en/connect/download/vnc/)/[TeamViewer](https://www.teamviewer.com/en/download/mac-os/) from time to time).
I had to buy a dummy Displayport which activates the iGPU and performs normally with it. Let me know if there is a way to do it without the dummy plug or maybe the actual Macmini can't run headless either.
I recently started using [Parsec](https://parsec.app/) to remote in and its been working fantastic so far.

## Using the EFI

Only things you need to set manually is the **System Serial Number**, **System UUID**, **MLB** and **ROM**. I have set them as **{CHANGE ME}** and OpenCore will complain if you do not set them correctly. You can get the first three created with [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS). The ROM part can be your Ethernet or WiFi MAC Address such as E4 85 G6 M8 H9 2Q, for example. Refer to the [Vanilla Hackintosh Guide by Dortania](https://dortania.github.io/OpenCore-Install-Guide/) if you need more help.

## Preparation

- Update to the latest BIOS if you can.
- Once on the latest BIOS, reset it to defaults (maybe even go as far as taking the CMOS battery out for a few minutes to hard reset).
- Make sure CFG Lock is **Disabled**. Alternatively, enable AppleCpuPmCfgLock and AppleXcpmCfgLock in Kernel, however, its better for performance to disable CFG Lock with the UEFI Variables below. You can also use the CFG Lock tool included to find the bit and flip it between Enabled and Disabled. [More info here](https://dortania.github.io/OpenCore-Install-Guide/config.plist/kaby-lake.html#kernel).
- Avoid Samsung PM drives as they did not let me go past the installer, it would always crash (may be fixed with NVMEFix.kext, I just bought a Sabrent SSD instead).
- To add to the above point, just use a Sabrent SSD to make your life easy. I never got Samsung/Toshiba drives to work with the installer (they come as default with XPS/Optiplex computers).
- For Big Sur, if you're using Dell Wireless 1560/1820A or something similar, make sure to modify your config [according to the "Please pay attention" section](https://github.com/acidanthera/AirportBrcmFixup#please-pay-attention), otherwise it will take forever to boot into the installer.

## BIOS Settings

[The entire BIOS settings can be found here](BIOS.md)

## UEFI Variables

| Variable name          | Offset | Default value  | Required value  | Description                                                         |
|------------------------|--------|----------------|-----------------|---------------------------------------------------------------------|
| CFG Lock               | 0x4ED  | 0x01 (Enabled) | 0x00 (Disabled) | Disables CFG Lock, otherwise you won't be able to boot              |
| DVMT Pre-Allocated     | 0x795  | 0x01 (32M)     | 0x02 (64M)      | Increases DVMT pre-allocated size to 64M which is required          |
| DVMT Total Gfx Mem     | 0x796  | 0x01 (128M)    | 0x03 (MAX)      | Increases total gfx memory limit to maximum                         |
| Bi-directional PROCHOT | 0x527  | 0x01 (Enabled) | 0x00 (Disabled) | Disables PROCHOT, which limits your CPU to 0.79GHz. More info below |

### Automated way
You can use the tools included to find your hidden CFG Lock value and disable it. These are **CFGUnlock** and **ControlMsrE2**. As of OpenCore 0.6.8, ControlMsrE2 is included and may be used to unlock CFG Lock for systems which have no easy way of doing so. This is a more automated and user-friendly way.

Here is an example of the **CFGUnlock** tool. Boot into OpenCore, choose **CFGUnlock** and follow the instructions:

![CFGUnlock](images/CFGUnlock.jpg)

You will still need to use the manual way below to change the DVMT variables.

### Manual way
The manual way is to boot into OpenCore, choose UEFIModify, type in `setup_var`, the offset and the required value. An example screenshot is below:

![UEFIModify](images/UEFIModify.jpg)

The above image is for the CFG Lock value. For DVMT, you would type:

**setup_var 0x795 0x02**

**setup_var 0x796 0x03**

Make sure to restart after any changes, they should apply. You used to be able to check the CFG Lock status with VerifyMsrE2, but since it was replaced by ControlMsrE2, you can use that instead. You'll know if it worked or not, by whether you can boot your installer:

![VerifyMsrE2](images/VerifyMsrE2.jpg)

## Miscellaneous thoughts

I have swapped from DW1820A to the DW1560 recently to see if Airdrop/Continuity/Handoff would work better, but I'm just not sure on both of these cards anymore. It seems [itlwm](https://github.com/OpenIntelWireless/itlwm) is making very good progress and you're better off with an Intel card these days. Still, I'll keep it in there since I am connected via Ethernet anyway.

I am using [exelban's Stats](https://github.com/exelban/stats) to monitor CPU, GPU, Memory, Disk, Temperatures, Fan Speed and Network.

This has been a great Plex Server throughout its use, very good Minecraft server too and have Wireguard VPN Server setup with [this guide](https://barrowclift.me/post/wireguard-server-on-macos).

As for the Bi-directional PROCHOT (BDPROCHOT), I've encountered this several times at work with our Dell machines and finally figured out how to stop it or at least suppress it. What happens is either a sensor dies, misinforms the BIOS or just the power supply is crappy and sends signals all over the place which in turn locks your CPU to a low power state.
Sometimes its 0.79GHz, sometimes a little bit higher or lower, but the result is an EXTREMELY slow system.
The computer thinks its essentially on fire and limits everything it can to save itself. However, in reality, the cooling is more than enough and no overheating is ocurring. I've had to replace a few motherboards under warranty to fix this issue before, but I found out that you don't need to do any of that, you just set the variables hidden in the BIOS as shown above. Of course, this remove the temperature checks/protections and could result in your computer overheating, so exercise caution with this option. I'm sure other CPU overheating protections would kick in regardless, but this probably voids your warranty, unless you reset the BIOS completely before sending your computer in.
Rambling aside, I will be making a tutorial on how to find the variable and turn it off and get your CPU speed back up to normal in the future.