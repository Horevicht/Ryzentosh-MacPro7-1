Last update: 13/09/2021

# AMD SETUP
* **Bootloader:** OpenCore 0.7.3
* **Systems:** macOS BigSur 11.6 + Windows 10 Pro
* **Motherboard/Mobo:** [Gigabyte B450m Gaming V1](https://www.gigabyte.com/br/Motherboard/B450M-GAMING-rev-1x/sp#sp)
* **CPU:** [3,2 GHz AMD Ryzen 5 1600 Six-Core Processor](https://www.amd.com/pt/products/cpu/amd-ryzen-5-1600)
* **GPU:** [XFX Radeon RX 570 8 GB XXX Edition](https://www.xfxforce.com/gpus/amd-radeon-tm-rx-570-rs-8gb-xxx-edition-2)
* **Wifi + BT:** Fenvi T919 - AliExpress
* **Memory:** 2x [XPG Gammix D10 8 GB DDR4-3000](https://www.xpg.com/pt/xpg/486)
* **Storage (macOS):** Aigo P2000 120GB M.2 NVMe SSD - AliExpress, LVCARDS
* **Storage (Windows):** Kunup 120GB SSD - AliExpress
* **Power Supply:** C3TECH 650W
* **Case:** Caseintosh Power Mac G5


# Previous info
* **USB mapping:** your hardware will need a different mapping (even if it's the exact model) - at [installation process](#installation-process), you will need `xhciportlimit = true` to functional USB ports » then, at [post-install](#post-install), you gotta do your own mapping process, please refer to [Dortania's USB Mapping guide](https://dortania.github.io/OpenCore-Post-Install/usb/)
* **Kexts and Drivers:** https://dortania.github.io/OpenCore-Install-Guide/ktext.html#firmware-drivers

# Files
*almost all of them comes in [Builds|Dortania](https://dortania.github.io/builds/?viewall=true)*
* **Masters**
1. [Opencore Pkg](https://github.com/acidanthera/OpenCorePkg/releases/) - *bootloader*
2. [ProperTree](https://github.com/corpnewt/ProperTree) - *plist editor*
3. [SSDTTime](https://github.com/corpnewt/SSDTTime) - *extractor of DSDT and editor to SSDT compilation for properly ACPI changes, extrictly important on how macOS "talks" to our Mobo*
5. [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) - *to make our SMBIOS (in this case, MacPro7,1)*
6. [AMD Kernel Patches](https://github.com/AMD-OSX/AMD_Vanilla/tree/master) - *please, refer to their github, the patches need to be changed according to your CPU*
7. [OCBinaryData](https://github.com/acidanthera/OcBinaryData) - *Canopy GUI (Resources) and Drivers*

* **Kexts** = you'll need the `.kext` file
1. [Lilu](https://github.com/acidanthera/Lilu/releases/) - *needed to boot*
2. [WhateverGreen](https://github.com/acidanthera/WhateverGreen/releases/) - *needed to boot (GPU)*
3. [VirtualSMC](https://github.com/acidanthera/VirtualSMC/releases/) - *needed to boot (to AMD, we just need the `VirtualSMC.kext` without the plugins)*
4. [AppleALC](https://github.com/acidanthera/AppleALC/releases/) - *audio (generally `alcid=1` as `boot-arg`)*
5. [RestrictEvents](https://github.com/acidanthera/RestrictEvents/releases/) - *amd cpu name in `"about macOS"`, fix memory errors of MacPro7,1 SMBIOS*
6. [NVMeFix](https://github.com/acidanthera/NVMeFix/releases/) - *optimizes SSD M.2 NVMe power management and such*
7. [Realtek8111](https://github.com/Mieze/RTL8111_driver_for_OS_X/releases/) - *ethernet*
8. [AppleMCEReporterDisabler](https://github.com/AMD-OSX/AMD_Vanilla/blob/master/Extra/AppleMCEReporterDisabler.kext.zip) - *when using `MacPro6,1`, `MacPro7,1`, or `iMacPro1,1`, as SMBIOS, `AppleIntelMCEReporter.kext` macOS might panic, so to prevent this you need to either use a different SMBIOS or use that disabler kext*
9. [SMCAMDProcessor + AMDRyzenCPUPowerManagement](https://github.com/trulyspinach/SMCAMDProcessor/releases/) - *properly powermanagement and SMC readings (e.g. FAN spins)... besides, it comes with `AMD Power Gadget`, totally optional, but the other 2 (kexts) are mandatory*
* **Drivers and Canopy (GUI)** = you'll need `.efi`files
1. HfsPlus - *it comes with `OCBinaryData` in `Drivers`*
2. OpenCanopy - *it comes with `OpenCore Pkg` in `Drivers`*
3. OpenRuntime - *needed to boot*
4. OpenLinuxBoot - *recent, experimental, need careful*
* **ACPI / SSDTs** = `.aml` files
1. SSDT-EC - *`SSDTTime` and needed to boot*
2. [SSDT-USBX](https://github.com/dortania/OpenCore-Post-Install/blob/master/extra-files/SSDT-USBX.aml) - *properly USB power management*
3. SSDT-HPET - *`SSDTTime` with patches on `plist`*
4. [SSDT-SBUS-MCHC](https://dortania.github.io/Getting-Started-With-ACPI/Universal/smbus.html) - *properly SMBUS support (post-install)*
* **Tools**
1. [Mount EFI Automator](https://github.com/corpnewt/MountEFI/blob/update/Mount%20EFI%20Automator%20Quick%20Action.zip) - *it becomes a "macOS service", you just gotta select the drive you want in Finder and voilá*
2. [MountyApp](https://mounty.app/) - *properly NTFS support*
3. [MaciASL](https://github.com/acidanthera/MaciASL/releases/) - *compiling/decompiling DSDT at macOS*
4. [GFX utility](https://github.com/acidanthera/gfxutil/releases/) - *listing PCI devices*
5. [Hackintool](https://github.com/headkaze/Hackintool/releases/) - *almost the same as `gfxutil`*
