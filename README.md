# Performance Onerom v3

Created by **Rapid Fire**. Windows desktop application distributed through **RapidFire-001**.

This repository is for downloads and documentation. It does not contain the application's private development repository or build history.

## Download and use

Download the single Windows x64 `.exe` attached to the [latest application release](https://github.com/RapidFire-001/onerom-v3/releases/tag/v3.0.10). Run it to use the application; no separately downloaded firmware, plugin pack or companion application folder is required. The app works offline. It unpacks its bundled runtime locally while running and attempts cleanup after normal exit.

The app supports One ROM Fire 28A, 28B, 28C, 32A and 32B with the supplied v0.8.0 firmware. Supplied system plugins cover Fire 28A/C and Fire 32A/B; no Fire 28B system plugin was supplied. Select firmware and a ROM appropriate to the connected board. Programming replaces the selected flash contents.

The app can build firmware, save encrypted `.orfw` files, reopen compatible saved files, inspect a USB-connected board, program it and verify flash readback. A ROM/calibration file is not bundled for use in an ECU.

## Credits and notices

This independent desktop utility incorporates upstream One ROM software and firmware by Piers Finlayson and other third-party components. It is not official One ROM Studio and does not imply upstream endorsement. Rapidfire's creator credit does not claim exclusive authorship of upstream firmware or libraries.

Open **About & licenses** for the bundled offline licence reader. One ROM MIT notices and the complete supplied Electron/Chromium and plugin notices are retained. See [NOTICES.md](NOTICES.md) for source and licensing references.

## Saved files and local protection

Encrypted saves use automatic unlocking in compatible app versions. They are portable rather than tied to one computer. Offline encryption is a copying deterrent; it is not a guarantee against a determined reverse engineer. Do not treat the application as a secret-key vault.

## Release scope

The published download is a single executable. GitHub may label automatically generated documentation-only repository archives as “Source code”; those archives do not contain private application source or build history.

This software uses libraries from the FFmpeg project under LGPL 2.1 or later. Its [matching third-party source materials](https://github.com/RapidFire-001/onerom-v3/releases/tag/third-party-electron-44.9.0) are available separately, with [build and library replacement instructions](THIRD-PARTY-SOURCE.md). No application source licence is granted by the upstream library licences.
