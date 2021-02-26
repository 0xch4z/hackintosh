# hackintosh

My Hackintosh EFI partition booting [macOS Big Sur 11.2](https://developer.apple.com/documentation/macos-release-notes/macos-big-sur-11_2-release-notes) via [OpenCore Bootloader v0.6.6](https://github.com/acidanthera/OpenCorePkg/releases/tag/0.6.6).

**Note: Backup your EFI partition and [regenerate the SMBIOS](https://github.com/corpnewt/GenSMBIOS)!** The serial number in `config.plist` is inactive.

![About Screenshot](/assets/about.png)

## Hardware Configuration

This configuration has full support for macOS.

Component | Name | Caveats
--- | --- | -- |
CPU | [Intel Core i7-8700K](https://ark.intel.com/content/www/us/en/ark/products/126684/intel-core-i7-8700k-processor-12m-cache-up-to-4-70-ghz.html)
GPU | [GIGABYTE Radeon VII](https://www.gigabyte.com/us/Graphics-Card/GV-RVEGA20-16GD-B#kf)
Motherboard | [GIGABYTE Z370n WIFI](https://www.gigabyte.com/us/Motherboard/Z370N-WIFI-rev-10#kf) | on-board WIFI/BT not supported
Airport Card | [Broadcom BCM94360CS2](https://www.amazon.com/Broadcom-Bcm94360cs2-Bcm94360cs2ax-Bluetooth-Wireless/dp/B00PDNDQ0K) | no native windows support

## ACPI Configuration

SSDT | Required | Details |
--- | --- | --- |
SSDT-PLUG | Yes | Native CPU power management support for Haswell+
SSDT-EC-USBX | Yes | Fixes embedded controller and USB power for Z370
SSDT-AWAC | Yes | Fakes a legacy RTC clock as macOS cannot communicate with AWAC clocks used in Z370

## Device Properties

### `PciRoot(0x0)/Pci(0x2,0x0)` entries

`APPL,ig-platform-id` Data value | When to use
--- | --- |
`07009B3E` | iGPU drives display
`0300913E` | iGPU does not drive display

#### Other keys

Key | Type | Value
--- | --- | --- |
`framebuffer-patch-enable` | Data | `01000000`
`framebuffer-stolenmem` | Data | `00003001`

## SMBIOS

As this is a Coffee Lake processor with the Z370 chipset, the Product name is "iMac (Retina 5K, 27-inch, 2019)" (`iMac19,1`).

## Reference

See [Coffee Lake OpenCore configuration](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#starting-point).
