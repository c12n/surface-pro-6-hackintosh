## Surface Pro 6 — macOS 15 Sequoia installer package

First release. Everything you need to build the USB installer:

- **OpenCore 1.0.8 EFI** for the Surface Pro 6 (i5-8350U / UHD 620), presented as MacBookPro15,2 — config validates clean with ocvalidate
- Graphics spoof + framebuffer patches, BigSurface (battery/buttons/touch), the Pro 6's own USB port map, fresh Acidanthera kexts, and Realtek USB Wi-Fi drivers (RtWlanU) included
- `FETCH-RECOVERY.bat` — downloads Apple's Sequoia recovery image (~1.2 GB) straight from Apple (no macOS files are redistributed here)
- Full step-by-step `README.txt`: USB creation, Surface UEFI settings, install, moving OpenCore to the internal drive, troubleshooting

**Before you use it:**
- The SMBIOS values in the config are **placeholders** — generate your own for MacBookPro15,2 with GenSMBIOS (see the repo README)
- The install needs a network connection macOS can use: the Surface's built-in Wi-Fi has no macOS driver. USB tethering from a phone or an AX88179-chip USB Ethernet adapter works
- The install erases the internal drive — back up first

Built and packaged by c12n Apps. Components remain under their own licenses.
