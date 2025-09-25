# OBS + FFmpeg (nvmpi) Debian Packages

This guide explains how **any** Jetson user running JetPack 6.2 (L4T 36.4.3) can install the nvmpi-enabled FFmpeg and OBS Studio builds produced in this project. Follow the steps below on the target device with sudo access on a 64‑bit Jetson platform.

## 1. Obtain the packages

Two `.deb` files are required: `ffmpeg-nvmpi_0.0+git20250115-1.deb` (≈56 MB) and `obs-jetson-nvmpi_32.0.0-nvmpi1.deb` (≈44 MB). Copy them to the Jetson with any transfer method (e.g., `scp`, USB drive) and place them in a working directory such as `/tmp`.

> Both packages install under `/usr/local` so they coexist with the system `/usr`. Post-install scripts refresh `ldconfig` and desktop caches automatically.

## 2. Prepare the Jetson

1. Update APT metadata and ensure the expected runtime libraries are present:
   ```bash
   sudo apt-get update
   sudo apt-get install -y \
     libqt6core6 libqt6gui6 libqt6widgets6 libqt6svg6 libqt6network6 libqt6dbus6 libqt6xml6 \
     libpulse0 libasound2 libcurl4 libdrm2 libva2 libva-drm2 libva-x11-2 libpci3 \
     libx11-6 libxcb1 libxcomposite1 libxfixes3 libxrandr2 libxi6 libxkbcommon0 libwayland-client0 \
     libfontconfig1 libfreetype6 libharfbuzz0b libpng16-16 libexpat1 libjansson4 \
     libzstd1 libssl3 libcrypto3 libv4l-0
   ```
   JetPack 6.2 already bundles most of these, but installing them explicitly prevents runtime surprises on minimal or custom images.

2. Remove conflicting OBS/FFmpeg builds (apt or manual):
   ```bash
   sudo apt-get remove --purge -y obs-studio ffmpeg
   sudo apt-get autoremove --purge -y
   ```

   If older hand-installed builds remain in custom locations, remove them or ensure they are not on your `PATH`/`LD_LIBRARY_PATH`.

## 3. Install nvmpi-enabled FFmpeg and OBS

1. Install FFmpeg first (replace `/tmp` with the directory you used):
   ```bash
   cd /tmp
   sudo dpkg -i ffmpeg-nvmpi_0.0+git20250115-1.deb
   ```
   This drops the toolchain under `/usr/local/ffmpeg-nvmpi` and adds wrappers (`ffmpeg-nvmpi`, `ffprobe-nvmpi`) that set the correct `LD_LIBRARY_PATH`.

2. Install the matching OBS Studio build:
   ```bash
   sudo dpkg -i obs-jetson-nvmpi_32.0.0-nvmpi1.deb
   ```
   OBS installs to `/usr/local/obs-jetson` and ships a desktop entry named **OBS Studio (Jetson NVENC)**. Both packages declare `Conflicts` against the stock `obs-studio` to avoid ABI mismatches.

If `dpkg` reports missing dependencies, rerun `sudo apt-get install -f` to let APT resolve them.

## 4. Verify the installation

```bash
ffmpeg-nvmpi -hide_banner -encoders | grep nvmpi
obs --version
```

Launch OBS from the desktop or via `QT_FATAL_WARNINGS=1 obs --verbose`. Under **Settings ➝ Output ➝ Recording**, confirm that *H.264 (Jetson NVENC)* (and optionally *H.265 (Jetson NVENC)*) appear. Start a short recording and check `~/.config/obs-studio/logs/latest.log` for lines mentioning `nvmpi: global headers not supported, SPS/PPS will be sent inline`; their presence indicates the nvmpi encoder loaded successfully.

For GPU utilization, open `jtop` ➝ **HW engines** while recording. `NVENC` and `VIC` should activate; `NVDEC` lights up only when decoding with the nvmpi decoder (playback, preview, or ffmpeg tests).

## 5. Known issues and mitigations

- **Pixel-format mismatch (Invalid argument)** – The nvmpi encoder only accepts `yuv420p`. Leave the OBS *Video ➝ Color Format* at “NV12 (default)” or add a filter that converts to 8‑bit 4:2:0. Forcing I444/P010 triggers the “Invalid argument” dialog.
- **Green strip along the bottom of camera feeds** – Many USB capture cards expose 1080×1088 surfaces. Crop 8 px off the bottom (`Filters ➝ Crop/Pad`) or enforce a clean crop at the driver level: `v4l2-ctl --device=/dev/videoX --set-selection=target=crop,height=1080`.
- **NVDEC hangs after crashes** – If OBS/FFmpeg wedges NVDEC and logs `InitNVDEC: Host1x channel open failed`, perform a cold reboot before retrying hardware decoding.
- **DeckLink / VAAPI warnings** – `libDeckLinkAPI.so` and VAAPI probes fail by default on Jetson; they are harmless unless you need SDI capture or Intel iGPU acceleration.
- **Legacy installs cause segfaults** – Leftover trees in `/opt/obs-jetson` or custom library paths can load mismatched Qt/FFmpeg symbols and crash OBS. Ensure only the packaged `/usr/local/obs-jetson` remains.

## 6. Optional tuning & tests

- Run `sudo jetson_clocks` or choose an appropriate `nvpmodel` profile to keep GPU clocks high for 1080p60 workloads.
- Command-line smoke test (replace `/path/to/sample.h264` with media on disk):
  ```bash
  LD_LIBRARY_PATH=/usr/local/ffmpeg-nvmpi/lib:/usr/local/lib \
    /usr/local/ffmpeg-nvmpi/bin/ffmpeg -hide_banner \
    -c:v h264_nvmpi -i /path/to/sample.h264 -f null -
  ```
- Inspect camera formats with:
  ```bash
  v4l2-ctl --device=/dev/video2 --list-formats-ext
  ```
  Use this to pick MJPEG if you want to avoid padded NV12 frames.

## 7. Backups & redistribution

- Keep a copy of both `.deb` files in a safe location (NAS, artifact store, removable media). They are self-contained; no extra firmware is required beyond JetPack 6.2.
- When sharing with another Jetson, transfer both packages together and follow the same install order (FFmpeg first, OBS second) so the nvmpi plugin resolves correctly.
