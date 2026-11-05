# FFmpeg sources for Performance Onerom v3.0.14, Windows x64

Download the [third-party source kit](https://github.com/RapidFire-001/onerom-v3/releases/download/v3.0.14/FFmpeg-Electron-44.9.0-third-party-sources.zip). Relative filenames in this document refer to that kit.

These are upstream third-party library sources and build records. They contain no private Performance Onerom application source, firmware unlock keys, user ROMs or private development history.

## Exact binary and source provenance

The distributed ffmpeg.dll has SHA-256 `96094bc6b5082e6372a9aa21970fcecfc069abd68caf4b48673b84dc3e8cf99b`. It is byte-identical to ffmpeg.dll in the official `electron-v44.9.0-win32-x64.zip`, whose SHA-256 is `88e08039d0ef359bab9f674e8051fa103bd8628ea7c5a5e1daaa610a8a0c6931`. That ZIP was verified against Electron's published SHASUMS256.txt. The separately published Electron ffmpeg ZIP is a different build and is not asserted to be this binary.

Electron v44.9.0 pins Chromium 152.0.7977.167. That Chromium DEPS pins its FFmpeg fork to `2b68d2babae73714846961fb0ee47e3b3d2e39a9`. The included FFmpeg source archive is the complete tree at that revision, including Chromium modifications, generated Windows x64 configuration, build files, notices and licences. README.chromium identifies upstream merge `a5e6c0175a7245fc1a9f4639da2810156128aa8b` (15 July 2026); this is a fork revision, not an assertion that an unmodified numbered FFmpeg release produced the DLL.

Electron's complete source archive at v44.9.0 is included. Its `patches/config.json` applies `patches/ffmpeg/link_with_loader_path.patch`, also copied separately here. This changes macOS loader-path handling; retain it when recreating Electron's source tree even though this application is for Windows. No Rapid Fire changes were made to FFmpeg.

The Chromium Chrome/win/x64 config declares `FFMPEG_LICENSE "LGPL version 2.1 or later"`, `CONFIG_GPL 0`, `CONFIG_NONFREE 0` and `CONFIG_VERSION3 0`. It includes AAC/H.264 and libopus options. Electron release arguments set `is_component_ffmpeg=true`, `ffmpeg_branding="Chrome"`, `proprietary_codecs=true` and `is_component_build=false`. Codec names do not change the stated LGPL licence or grant patent rights.

The exact Chromium `third_party/opus` source tree is included separately because the FFmpeg build depends on it. Its original BSD notices remain within the archive. SHA256SUMS records hashes of the supplied upstream materials.

## Build and modify the library

Use Electron's included `docs/development/build-instructions-gn.md` and Windows prerequisites; a copy of the main build guide is also at this archive's root. These instructions require a Windows C++ toolchain and substantial source/dependency downloads and disk space. A byte-for-byte reproducible rebuild has not been claimed or performed.

1. Set up depot_tools and Electron's source checkout as the included guide describes. Check out Electron tag `v44.9.0` in `src/electron` before `gclient sync --with_branch_heads --with_tags`. Electron-DEPS and Chromium-DEPS supplied here record the exact revisions; do not substitute current main branches. Gclient retrieves the Chromium build framework, compiler tooling and other dependencies and applies Electron's pinned patches. The included complete Electron source archive also supplies its dependency-fetch and patch/build scripts.
2. The resulting `src/third_party/ffmpeg` must use the pinned fork revision above plus Electron's patch. The complete source archive provided here can be used to inspect, modify or restore that source. Generated configuration is under `chromium/config/Chrome/win/x64`; the full configure line is recorded in its config.h. The included Opus archive corresponds to `src/third_party/opus` at the pinned Chromium tag.
3. From `src`, generate an x64 release configuration importing `//electron/build/args/release.gn`, with `target_cpu="x64"`, then build the `ffmpeg` target using the build tool described in the Electron guide (for example `ninja -C out/Release ffmpeg` in a configured checkout). The DLL is built as a shared library. Keep its exported interface compatible with the original. Changes to ABI, architecture or required exports can prevent startup.
4. Install the rebuilt ffmpeg.dll in a writable extracted copy of the application's runtime, replacing its original ffmpeg.dll, and run `Performance Onerom v3.exe` from that runtime. Do not modify the packaged application ASAR. The instructions below allow use of a replacement without changing or signing the application executable.

## Extracting a writable runtime for library replacement

The normal one-file launcher extracts a temporary runtime and removes it after exit. For library modification, create a persistent local runtime from your downloaded EXE. This PowerShell example reads its appended ZIP payload into a separate folder. It does not connect to hardware or need private application source. Set `$download` to your downloaded file and `$destination` to a new writable folder that does not already exist.

```powershell
$download = 'C:\Downloads\Performance-Onerom-v3-Rapid-Fire-3.0.14.exe'
$destination = 'C:\Downloads\OneROM-library-test'
if (Test-Path -LiteralPath $destination) { throw 'Choose a new destination folder.' }
$allBytes = [IO.File]::ReadAllBytes($download)
$count = [BitConverter]::ToInt64($allBytes, $allBytes.Length - 16)
if ([Text.Encoding]::ASCII.GetString($allBytes, $allBytes.Length - 8, 8) -ne 'ONEROM13' -or $count -le 0 -or $count -ge ($allBytes.Length - 16)) { throw 'Unsupported or damaged executable.' }
$zipFile = Join-Path ([IO.Path]::GetTempPath()) ([guid]::NewGuid().ToString('N') + '.zip')
try {
    $zipBytes = New-Object byte[] $count
    [Array]::Copy($allBytes, $allBytes.Length - 16 - $count, $zipBytes, 0, $count)
    [IO.File]::WriteAllBytes($zipFile, $zipBytes)
    Expand-Archive -LiteralPath $zipFile -DestinationPath $destination
} finally {
    if (Test-Path -LiteralPath $zipFile) { Remove-Item -LiteralPath $zipFile }
}
```

Close all instances of the test runtime before replacing its DLL. Retain a copy of the original library. Start the inner executable directly; running the one-file outer EXE again creates a fresh runtime containing the original library. You may modify the library for your own use and reverse engineer the combined work for debugging those modifications as permitted by LGPL 2.1 section 6. No application distribution term overrides these rights. A different official interface-compatible Electron FFmpeg DLL was substituted locally and the app opened successfully; this is a startup check, not proof that every possible custom library will work.

## Upstream locations

- Electron release and checksums: https://github.com/electron/electron/releases/tag/v44.9.0
- Electron source: https://github.com/electron/electron/tree/v44.9.0
- Chromium dependency manifest: https://chromium.googlesource.com/chromium/src/+/refs/tags/152.0.7977.167/DEPS
- Complete FFmpeg fork source: https://chromium.googlesource.com/chromium/third_party/ffmpeg/+/2b68d2babae73714846961fb0ee47e3b3d2e39a9/
- Complete FFmpeg source archive: https://chromium.googlesource.com/chromium/third_party/ffmpeg/+archive/2b68d2babae73714846961fb0ee47e3b3d2e39a9.tar.gz
- Source licence: COPYING.LGPLv2.1 and the other original notices in the source tree; see also https://ffmpeg.org/legal.html

This source download is optional for running the application. The application remains a single EXE download. It supplies library source access rather than a future written source-supply offer. Other third-party notices are available in the app's offline About & licenses reader.
