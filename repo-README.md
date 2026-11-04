# Surface Pro 6 — macOS 15 Sequoia (OpenCore)

An OpenCore 1.0.8 EFI and USB installer package that runs **macOS 15 Sequoia** on the **Microsoft Surface Pro 6** (Core i5-8350U / Intel UHD 620 / 16 GB). The machine is presented to macOS as a MacBookPro15,2, a model Sequoia fully supports. The config validates clean with `ocvalidate`.

> No macOS files are included. The recovery image is downloaded directly from Apple by the included `FETCH-RECOVERY.bat` (OpenCore's macrecovery tool).

## What works / what doesn't

| Works | Doesn't work |
| --- | --- |
| UHD 620 graphics, full acceleration (spoofed + framebuffer patches) | **Built-in Wi-Fi / Bluetooth** — the Marvell AVASTAR chip has no macOS driver, ever |
| Internal NVMe SSD | Both cameras |
| Type Cover keyboard / trackpad | AirDrop / Handoff (needs native Apple wireless) |
| USB ports (device-specific port map included) | Sleep can be rough |
| Speakers / headphone jack (AppleALC, layout 3) | |
| Battery, power/volume buttons, touchscreen — via BigSurface | |
| Optional: Realtek USB Wi-Fi dongles (drivers included, see below) | |

## What you need

- A Surface Pro 6 (built and tested for i5-8350U / UHD 620; other SP6 configs are untested)
- A USB stick, 8 GB or larger (it will be erased)
- **A network connection macOS can use during setup** — the built-in Wi-Fi is dead in macOS, and the installer downloads macOS from Apple while it runs. Use one of:
  - An iPhone (or Android phone) on a USB cable with USB tethering / Personal Hotspot on, or
  - A USB Ethernet adapter with an **ASIX AX88179** chip (built-in macOS driver). Realtek-chip adapters (e.g. RTL8153) do **not** work in macOS.
- The install erases the internal drive. Back up first.

## Quick start

1. Download the package zip from the [latest release](../../releases/latest) and unzip it.
2. Run `FETCH-RECOVERY.bat` on Windows (needs Python, free from python.org). It downloads Apple's Sequoia recovery image (~1.2 GB) into `com.apple.recovery.boot`.
3. **Generate your own SMBIOS values** (the shipped ones are placeholders): run [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) for **MacBookPro15,2** and put the serial, MLB, UUID and ROM into `EFI/OC/config.plist` under `PlatformInfo > Generic`. Never use anyone else's serial, and do not sign a real Apple ID into a machine running someone else's generated identity.
4. Format the USB stick as FAT32 and copy `EFI` and `com.apple.recovery.boot` to its root.
5. On the Surface: UEFI (hold Volume Up at power-on) → Secure Boot **None**. Then boot the stick (hold Volume Down at power-on) and pick the recovery entry in the OpenCore menu.
6. Full step-by-step instructions, the internal-drive boot setup, and troubleshooting are in the bundled `README.txt`.

## Everyday Wi-Fi (optional)

The EFI already contains the Realtek USB Wi-Fi drivers (RtWlanU). With a dongle based on **RTL8811AU / RTL8821AU / RTL8812AU** (e.g. EDUP AC600, TP-Link Archer T2U Plus / T2U Nano) and chris1111's free Wireless USB Adapter app, you get working Wi-Fi after setup — through that app, not the macOS Wi-Fi menu, and WPA2 only. Chips ending in BU/CU are not supported. A dongle can't join a network during the install itself, so the tether/Ethernet from step 0 is still needed for setup.

## Credits

- [OpenCore](https://github.com/acidanthera/OpenCorePkg) and the Acidanthera kexts (Lilu, WhateverGreen, VirtualSMC, AppleALC, NVMeFix)
- [BigSurface](https://github.com/Xiashangning/big-surface) by Xiashangning — Surface battery, buttons and touch
- Device data (SSDT-SURFACE, USB port map, framebuffer values) cross-checked against a known-working Surface Pro 6 EFI by murdrd00
- [Dortania's OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/) — the Kaby Lake laptop values this config follows

## Disclaimer

A personal, unofficial project, provided as-is with no warranty. Running macOS on non-Apple hardware is outside Apple's license terms — proceed at your own risk. All trademarks belong to their owners; this project is not affiliated with Apple or Microsoft. Every component remains under its own license.

Copyright (c) 2026 c12n Apps
