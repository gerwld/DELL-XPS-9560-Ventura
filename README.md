# DELL-XPS-9560-Ventura

> Working XPS15-9560 Hackintosh OpenCore Config for macOS Monterey (up to Ventura). Lower OS versions have not been tested but may work. Higher versions might also be compatible.
Based on [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg) and an old fork from [NOTNlCE-OpenCore](https://github.com/NOTNlCE/XPS-9560-OpenCore).

<img width="1680" alt="res" src="https://github.com/user-attachments/assets/c5460956-bcfc-440f-8963-abec6af55353">

## Core features:
- Fixed the issue where the wrong BusID was chosen in SSDT-PNLF.aml. 
  Replace it with the one in the `./Optional` directory to see which one works best for you.
- Fixed common issues with EverythingGreen for Kaby Lake iGPUs.
- Updated all kernel extensions to the latest versions.
- Updated OpenCore to `1.0.0`.

## What works:
Everything works, except:
- <b>GTX 1050</b> (No support for either [Metal API](https://en.wikipedia.org/wiki/Metal_(API)) or [Optimus technology](https://en.wikipedia.org/wiki/Nvidia_Optimus)).
- Headphone volume control buttons.
- Stock Wi-Fi Card Killer Wireless 1535 __(DW1560 / DW1830 is a good m.2 alternative)__.

## Installation:
- Install OpenCore on your pendrive [(How to)](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer).
- Remove the EFI folder and replace it with the one from this build (do not merge!).
- Choose the config.plist (4k, 1080). Rename it to config.plist.
- Disable Secure Boot, set SATA Operation to AHCI. Keep virtualization and Intel ME enabled.
- Setup in BIOS: 
    "Boot Options" > 
    Delete every option > 
    Add new > 
    Choose your pendrive (usually FB0) > 
    EFI/OC/OpenCore.efi. Save & exit.
- Plug in your macOS installation drive. You can find a tutorial on how to create it [here](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer).
- Boot, select your installer, and format your drive to APFS. At least 60GB is required. If you plan to add Windows later, create an ExFat volume.
- Disable Verbose `-v` arg after successful installation in `config.plist` (optional).
- Generate <B>SMBIOS</B>:<br>
    `SystemSerialNumber`, `Board Serial`, `Apple ROM`, and `SystemUUID` and set them in `config.plist` (without these, iCloud and AppStore won't work).

## Warning:

1. Do not turn on `FileVault Encryption`.
2. Before using OpenCore, ensure that you have disabled `CFGlock`! If you don't disable `CFGLock`, you need to change the values of `AppleXcpmCfgLock` and `IgnoreInvalidFlexRatio` to `True` or you will experience boot failures.

## Pros of this build:
- Everything is up-to-date (Kexts, Drivers, OpenCore).
- ACPI > Kexts support.
- SD Card / HDMI work properly.
  
## Extra features and tips to make debugging easier:
- If you have another Mac machine, you can use [OCLP](https://dortania.github.io/OpenCore-Legacy-Patcher/INSTALLER.html#creating-the-installer) to quickly create base EFI partitions on pendrives.
- FAT type also works as an EFI boot option, so you don't have to mount the EFI partition each time to make changes. Use `sudo diskutil eraseVolume FAT32 EFI /dev/diskXsY`.
- Use [PlistEdit Pro](https://www.fatcatsoftware.com/plisteditpro/) for editing .plist files, [MaciASL](https://github.com/acidanthera/MaciASL/releases/tag/1.6.4) for ACPI, and [Hackintool](https://github.com/benbaker76/Hackintool/releases) for general debugging and updates.
- For SMBIOS SN and Board ID generation, [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) is quite good. You'll need it to make iMessages work.
- The value of SystemProductName actually matters. Check everymac.com to find the model that best matches your machine, usually MacbookPro14,3 for the 9560.
- Don't be afraid to break anything if it's already broken.

Also, check the [NOTNlCE-OpenCore](https://github.com/NOTNlCE/XPS-9560-OpenCore) thread: https://www.tonymacx86.com/threads/guide-dell-xps-9560-ventura-opencore.324866/

<br>
<hr>

### Troubleshooting (Post install):
- If you lost your original Windows EFI, the easiest way to restore it is to create a `209mb FAT partition` with Disk Utility under Mac.
  Then simply follow this guide: https://www.youtube.com/watch?v=LILSaEGzhOg
- You may disable the default BIOS recovery to prevent it from breaking something - both `"Disable Pre-boot Help"` and `"Auto Recovery after 3 Failed Boots"`.
- Uncheck other boot options, but don't delete them. Otherwise, the system will reinitialize them shortly after and set one of them as the main boot option.
- Click on the space bar in OpenCore, and you will find `GRUBShell.efi` added to it. It can help you undervolt your CPU without downgrading (do this only at your own risk).
