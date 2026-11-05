# Credits and third-party notices

Created by Rapid Fire. Copyright (c) 2026 Rapidfire for application-specific additions. The distribution account is RapidFire-001.

Upstream and third-party components retain their own copyrights, licences and recipient rights. This document does not relicense the entire app as MIT and does not impose restrictions on third-party rights.

The executable embeds a complete offline notice reader under **About & licenses**. It contains One ROM's licence, the One ROM website-derived and WASM notices, supplied custom USB plugin notices, pico-sdkless, picobootx, TinyUSB, Electron, and the runtime's complete Chromium component collection.

- One ROM software/firmware v0.8.0: MIT, copyright 2026 Piers Finlayson. [Licence](https://github.com/piersfinlayson/one-rom/blob/v0.8.0/LICENSE.md), [upstream source](https://github.com/piersfinlayson/one-rom/tree/v0.8.0).
- Supplied custom plugin ownership marker: Copyright 2026 TXRX. That marker is retained rather than replaced by the application credit; the source headers examined identify MIT licensing.
- TinyUSB: MIT; copyright 2018 hathach, with descriptor code notices including Ha Thach retained.
- pico-sdkless and picobootx: MIT; Piers Finlayson notices retained.
- Electron v44.9.0: [MIT licence and copyright notices](https://github.com/electron/electron/blob/v44.9.0/LICENSE), [source/dependencies](https://github.com/electron/electron/tree/v44.9.0).
- Chromium and its bundled dependencies: complete component notices embedded in the executable. [Electron's pinned dependencies](https://github.com/electron/electron/blob/v44.9.0/DEPS).
- FFmpeg: the runtime uses FFmpeg library code with applicable [LGPL provisions](https://ffmpeg.org/legal.html), available in the offline Chromium collection. The complete pinned FFmpeg fork source, Electron source/patches and Windows build records are supplied through the [third-party source download](https://github.com/RapidFire-001/onerom-v3/releases/download/v3.0.14/FFmpeg-Electron-44.9.0-third-party-sources.zip). See [THIRD-PARTY-SOURCE.md](THIRD-PARTY-SOURCE.md) for binary hashes, source revisions and library replacement instructions. This optional source download is not needed to run the app.

One ROM hardware design files have a separate CERN-OHL-W-2.0 licence and are not distributed with this desktop application. This project makes no claim to be the originator of upstream One ROM v0.8.0.

Recipients may modify the LGPL library for their own use and reverse engineer the combined work for debugging those modifications as permitted by LGPL 2.1 section 6. No application term restricts those rights. The application uses the library as a separate DLL; the optional third-party source materials include instructions for running a writable runtime with an interface-compatible replacement.
