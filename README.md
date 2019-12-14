# About the installation

## Hardware Configuration

- AMD Ryzen 5 1600
- Gigabyte AB 350 Gaming 3
- Zotac GTX 1080 8GB DDR5X Mini
- GSkill F4-3200C16D-16GTRZ DDR4 8GBx2

## Software Configuration

Currently, we are limited to High Sierra because of lack of Nvidia WebDrivers for more recent macOS releases.

- High Sierra 10.13.6 (17G66)

# Installation

The installation is a chimera of guides like https://vanilla.amd-osx.com and https://github.com/AMD-OSX/AMD_Vanilla.

## Resources needed

1. Download the High Sierra installer using https://github.com/corpnewt/gibMacOS.
    1. First run `gibMacOS.command` to download the required pieces.
    2. Then run `BuildmacOSInstallApp.command`.
    
2. Prepare the bootable USB:
   
    ```
    sudo /Applications/Install\ macOS\ High\ Sierra.app/Contents/Resources/createinstallmedia --volume /Volumes/MyVolumeName
    ```
    
3. Download [Clover Configurator](https://mackie100projects.altervista.org/download-clover-configurator/) and mount the EFI partition of the USB installer.

4. Install [Clover bootloader](https://github.com/CloverHackyColor/CloverBootloader/releases) in the EFI partition.

5. Copy the file https://github.com/AMD-OSX/AMD_Vanilla/blob/master/17h/config.plist overwriting `EFI/EFI/CLOVER/config.plist`.

6. Make sure you have following in the `/Volumes/EFI/EFI/CLOVER/drivers/UEFI`:

    ```
    ApfsDriverLoader.efi	AptioMemoryFix.efi	DataHubDxe.efi		Fat.efi			SMCHelper.efi
    AptioInputFix.efi	AudioDxe.efi		FSInject.efi		HFSPlus.efi		VBoxHfs.efi
    ```
 
7. Install the following kexts in `/Volumes/EFI/EFI/CLOVER/kexts/Other`:

    ```
    AppleALC.kext			NullCPUPowerManagement.kext	RtWlanU.kext			USBInjectAll.kext		WhateverGreen.kext
    Lilu.kext			RealtekRTL8111.kext		RtWlanU1827.kext		VirtualSMC.kext			XHCI-unsupported.kext
    ```
 
8. Now you can reboot into the USB to perform the installation. **Please use APFS with SSDs** or installation won't proceed.
