# DELL-XPS-9560-Ventura
Working EFI for MacOS Monterey (up to Ventura). Lower OS versions were not tested but may work. Higher as well.
Based on [OpenCorePkg](https://github.com/acidanthera/OpenCorePkg) and old fork from [NOTNlCE-OpenCore](https://github.com/NOTNlCE/XPS-9560-OpenCore).

<img width="1680" alt="res" src="https://github.com/user-attachments/assets/c5460956-bcfc-440f-8963-abec6af55353">

## Core features:
- Fixed the issue when wrong BusID was chosen into SSDT-PNLF.aml. 
    Replace with the one in /Optional directory to check which one works best for you.
- Fixed EverythingGreen most common issues with Kaby Lake iGPU's.
- Updated all kernel extensions to latest versions.
- Updated Opencore to 1.0.0.

## What does work:
Everything except
- <b>GTX 1050</b>. no metal support.
- Headphones volume control buttons. 

### How to begin:
- Install Opencore on your pendrive [(How to)](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer).
- Remove EFI folder and replace it with one from this build (do not merge!).
- Choose  config.plist (4k, 1080). Rename it to config.plist.
- Disable Secure Boot, Sata Operation > Select AHCI. Keep virtualisation and Intel ME.
- Setup in BIOS: 
    "Boot Options" > 
    Delete every option > 
    Add new > 
    Choose your pendrive (usually FB0) > 
    EFI/OC/Opencore.efi. Save & exit.
- Plug in your installation drive for MacOS. You can find tutorial how to make it [here](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer)
- Boot, select your installer and format your drive to APFS. At least 60gb is required. If you plan to add Windows later, create ExFat volume.

## Extra features and knowledge to make debugging easier:
- If you have another Mac machine, you can use [OCLP](https://dortania.github.io/OpenCore-Legacy-Patcher/INSTALLER.html#creating-the-installer) to create base EFI partitions fast on pendrives.
- FAT type also works as EFI boot option, but you dont have to mount the EFI partition each time to make some changes.
- Use (PlistEdit Pro)[https://www.fatcatsoftware.com/plisteditpro/] for editing .plist files, [MaciASL](https://github.com/acidanthera/MaciASL/releases/tag/1.6.4) for ACPI, and [Hackintool](https://github.com/benbaker76/Hackintool/releases) for general debuging and updates.
- For SMBIOS SN, Board ID generation [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) is quite good. You need it to make iMessages work.
- SystemProductName value actually matters. Check everymac.com to find model that match your machine the best. For 9560 is usually MacbookPro14,3.
- Don't be afraid to break anything, if it's already broken.



Also check the [NOTNlCE-OpenCore](https://github.com/NOTNlCE/XPS-9560-OpenCore) thread: https://www.tonymacx86.com/threads/guide-dell-xps-9560-ventura-opencore.324866/
