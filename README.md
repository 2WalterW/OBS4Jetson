# OBS4Jetson Bundle

Prebuilt OBS Studio and FFmpeg (nvmpi-enabled) packages for Jetson devices running JetPack 6.2 (L4T 36.4.3).

## Contents
- `docs/obs_ffmpeg_nvmpi_deb_guide.md` — installation and troubleshooting guide for Jetson users.
- `pkg/ffmpeg-nvmpi_0.0+git20250115-1.deb` — FFmpeg build with nvmpi encoder/decoder support.
- `pkg/obs-jetson-nvmpi_32.0.0-nvmpi1.deb` — OBS Studio build linked against the nvmpi-enabled FFmpeg toolchain.

Follow the guide in `docs/` for dependency preparation, installation order, and validation steps.
