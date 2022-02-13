# Dell Optiplex 7050 Micro BIOS Settings

This was written with my Optiplex 7050 Micro being on BIOS 1.14.0, newer BIOSes might change stuff, you never know (even if Intel 7th gen's were ages ago).

**Update:** It seems BIOS updates don't change anything, in terms of what you can turn off or on these days, just security updates, so don't worry about them too much!


I'll just lay out the way my BIOS is shown and whatever is ticked/selected so you can copy it on yours, and hopefully make it work. Make sure your BIOS is updated to at least what mine is and its always best to Reset to Factory Defaults before starting to flick switches (from personal experience, resetting BIOS does sometimes flip hidden switches, in case anybody tried to screw around with it before).

# Settings
## General
- **System Information** - Not much to change here, its just information about your Optiplex
- **Boot Sequence** - Make sure its set to UEFI and the only boot option is your drive with the EFI (depends how many drives you have and if you dualboot)
- **Advanced Boot Options** - Untick "Enable Legacy Option ROMs" and "Enable Attempt Legacy Boot" should be greyed out
- **UEFI Booth Path Security** - Left as default at "Always, Except Internal HDD". I don't  think it changes anything
- **Date/Time** - Left as default, its just time settings

## System Configuration
- **Integrated NIC** - Untick "Enable UEFI Network Stack" and select Enabled (or not, if you don't want Ethernet)
- **SATA Operation** - Select "AHCI" and make sure its enabled before installing anything, RAID On is only a driver for Windows 7 which didn't support RAID at the time, you want the AHCI option here
- **Drives** - Leave all ticked, may be different for you. I had SATA-0, SATA-4 and M.2 PCIe SSD-0.
- **SMART Reporting** - "Enable SMART Reporting" is enabled/ticked. Probably doesn't matter, but I like to have it on
- **USB Configuration** - Everything is ticked, "Enable USB Boot Support", "Enable Front USB Ports" and "Enable Rear USB Ports". Self explanatory
- **Front USB Configuration** - All options enabled/ticked
- **Rear USB Configuration** - All options enabled/ticked
- **USB PowerShare** - "Enable USB PowerShare" is disabled/unticked. It may cause problems with graphics later if enabled, leave it off
- **Audio** - Everything is enabled/ticked here too
- **Dust Filter Maintenance** - I left it at disabled, there isn't even any dust filter in the Micro version, must be an oversight ¯\\\_(ツ)\_/¯

## Video
- **Primary Display** - Set it as "Intel HD Graphics" instead of Auto, just to reinforce it to use the iGPU (unless you have a bigger Optiplex with a dedicated AMD GPU or an [old NVIDIA GPU](https://dortania.github.io/GPU-Buyers-Guide/modern-gpus/nvidia-gpu.html) that is still supported)

## Security
- **Admin Password** - Left as default
- **System Password** - Left as default
- **Internal HDD-0 Password** - Left as default
- **Strong Password** - "Enable Strong Password" is unticked
- **Password Configuration** - Left as default
- **Password Bypass** - Left as default
- **Password Change** - Left as default, "Allow Non-Admin Password Changes" is ticked
- **UEFI Capsule Firmware Updates** - "Enable UEFI Capsule Firmware Updates" is disabled/unticked, I personally disable this on everything, because Windows Update doing BIOS updates is a recipe for disaster, especially when supporting people who might unplug/force shutdown the computer in the middle of it
- **TPM 1.2 Security** - "TPM On" is disabled/unticked. ~~I personally hate Dell TPM's, the amount of issues it has caused me at work is too many with literally 0 benefit.~~ Nevermind, the TPM's malfunctioning was just my work colleagues having stupidly old Group Policies. macOS also doesn't care about TPM, so disable it here
- **Computrace(R)** - Deactivate this, never used it and macOS doesn't need it
- **Chassis Intrusion** - Left as default, you can change to your preference
- **CPU XD Support** - **MAKE SURE TO ENABLE CPU XD SUPPORT!!!** If disabled, computer immediately restarts after trying to boot and you cannot progress. I even had to DM a couple Reddit users who had the same computer as me to ask for help, only to realise I disabled it
- **OROM Keyboard Access** - Left as default
- **Admin Setup Lockout** - Left as default
- **Master Password Lockout** - Left as default
- **SMM Security Mitigation** - Left as default

## Secure Boot
- **Secure Boot Enable** - Obviously disabled, absolutely useless
- **Expert Key Management** - Left as default

## Intel R Software Guard Extensions TM
- **Intel R SGX TM Enable** - Disabled
- **Enclave Memory Size** - This is greyed out since its disabled

## Performance
- **Multi Core Support** - Enable all cores
- **Intel R SpeedStep TM** - Enabled
- **C-States Control** - "C states" is enabled
- **Limit CPUID Value** - This is unticked
- **Intel R TurboBoost TM** - Enabled
- **HyperThread control** - Enabled

## Power Management
- **AC Recovery** - I keep this enabled, so the computer starts again in case of power loss, totally up to you
- **Auto On Time** - Left as default
- **Deep Sleep Control** - Disabled
- **USB Wake Support** - This is unticked
- **Wake on LAN/WLAN** - Disabled
- **Block Sleep** - "Block Sleep (S3 State)" is unticked
- **Intel Ready Mode** - Disabled

## POST Behaviour
- **Adapter Warnings** - Disabled, to prevent the boot process from being halted
- **Numlock LED** - Enabled, up to you though
- **Keyboard Errors** - Disabled
- **Fastboot** - I set it to Thorough, up to you as well, I prefer everything to be initialized at the start
- **Extend BIOS POST Time** - 0 seconds
- **Full Screen Logo** - Disabled
- **Warning and Errors** - Continue on Warnings and Errors

## Manageability
- **USB Provision** - Disabled
- **MEBx Hotkey** - Enabled, doesn't matter

## Virtualization Support
- **Virtualization** - Enabled
- **VT for Direct I/O** - Enabled, double check if DisableIOMapper is set to YES. [More info here.](https://dortania.github.io/OpenCore-Install-Guide/config.plist/kaby-lake.html#kernel)
- **Trusted Execution** - Disabled, it will probably be greyed out

## Wireless
- **Wireless Device Enable** - Enabled, self explanatory

## Maintenance
- **Service Tag** - This is just information
- **Asset Tag** - This is just information
- **SERR Messages** - Enabled
- **BIOS Downgrade** - Enabled, doesn't matter
- **Data Wipe** - Disabled forever, unless you want the computer to erase everything on the next boot
- **BIOS Recovery** - BIOS Recovery from Hard Drive is enabled, BIOS Auto-Recovery is disabled, I don't think this matters though

## System Logs
- **BIOS Events** - View only, self explanatory

## Advanced configurations
- **ASPM** - Disabled
