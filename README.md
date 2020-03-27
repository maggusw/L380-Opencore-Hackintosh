# Lenovo L380 (20M6) Opencore 0.5.6 EFI for Catalina 10.15.4

## ACPI

* `DSDT.dsl` - patched for use with VoodooI2C
* `SSDT-EC-USBX.dsl`
* `SSDT-PLUG.dsl` 
* `SSDT-PNLF.dsl` - ability to change display brightness
* `SSDT-SMBUS.dsl` - needed for ELAN Touchpad

## Drivers 

* minimal collection taken from Opencore Tutorial


## Kexts

* `AppleALC` - audio fix
* `ELANSMBus` - taken from (https://github.com/gokula/ELANSMBus) to support ELAN Touchpad as VoodooI2C is not supported
* `IntelMausi` - Ethernet
* `Lilu` and `NoTouchId`
* `NVMeFix` for NVMe SSD
* `SMCBatteryManager` for battery status
* `USBInjectAll` for USB Ports
* `VirtualSMC`
* `VoodooInput` and `VoodooPS2Controller` for keyboard 
* `WhateverGreen` for iGPU


## config.plist

### ACPI

* Add the `DSDT` and the `SSDT`
* Change `H_EC` to `EC` according to guide

### Device Properties

* `PciRoot(0x0)/Pci(0x1b,0x0)` where `AAPL, ig-platform-id` is set to `00001659` and `device-id` to `16590000`


### Kernel 

#### Add

* Contains all kext 
* `VoodooPS2Mouse` must be `Enabled` set to `FALSE`

#### Block

* `com.apple.driver.AppleSMBusController`, `com.apple.driver.AppleSMBusPCI`, `com.apple.driver.AppleIntelLpssI2C` and `com.apple.driver.AppleIntelLpssI2CController` must be `ENABLED` here for the Touchpad to work. Do note that prior to an macOS update these must be unblocked for the update to go through as we are block Apple kexts here


### NVRAM

* `boot-args` for the SSD would be `alcid=11` for the audio to work and `keepsyms=1` 


### PlatformInfo

#### Generic

* Use MacBookPro14,1 here



The rest should be done according to Opencore guides. 
