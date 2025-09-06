# OBS Studio for Jetson AGX Orin

![OBS Studio](https://img.shields.io/badge/OBS%20Studio-32.0.0-blue) ![FFmpeg](https://img.shields.io/badge/FFmpeg-7.1-green) ![Platform](https://img.shields.io/badge/Platform-Jetson%20AGX%20Orin-orange) ![JetPack](https://img.shields.io/badge/JetPack-6.2.1-red)

**一键安装 OBS Studio + NVMPI 硬件编码，专为 Jetson AGX Orin 优化**

## ✨ 核心特性

🎯 **完整GUI界面** + **NVMPI硬件编码** + **内置FFmpeg 7.1**  
🚀 **一键安装** | **开箱即用** | **专业直播录制**

## 💻 系统要求

- **硬件**: NVIDIA Jetson AGX Orin
- **系统**: JetPack 6.2.1 (Ubuntu 22.04 ARM64)  
- **内存**: 8GB+ | **存储**: 500MB+

## ⚡ 快速安装

```bash
# 下载安装包 (96MB)
wget https://github.com/2WalterW/OBS4Jetson/releases/download/v32.0.0/obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz

# 解压安装
tar -xzf obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz
cd obs-studio-jetson-package
sudo ./install.sh

# 立即使用
obs
```

## 🎯 包含内容

- **OBS Studio 32.0.0** + 完整GUI界面
- **FFmpeg 7.1** + NVMPI硬件编码器 (`h264_nvmpi`, `hevc_nvmpi`)
- **40+ 插件** + 智能安装脚本
- **推荐设置**: 1080p60直播 | 4K30录制

## 📚 详细文档

- [安装指南](INSTALL_INSTRUCTIONS_COMPLETE.txt) | [技术说明](RELEASE_INFO_COMPLETE.md)

## ❓ 问题排除

**安装失败**: 确保root权限 + JetPack 6.2.1  
**编码器不可用**: 运行 `/usr/local/bin/ffmpeg -encoders | grep nvmpi`  
**启动失败**: 查看 `~/.config/obs-studio/logs/`

## 🙏 致谢

基于 [OBS Studio](https://obsproject.com/) + [jetson-ffmpeg](https://github.com/Seeed-Studio/jetson-ffmpeg)

---

⭐ **如果有帮助，请给个Star支持！**