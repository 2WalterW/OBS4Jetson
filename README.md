# OBS Studio for Jetson AGX Orin

![OBS Studio](https://img.shields.io/badge/OBS%20Studio-32.0.0-blue) ![FFmpeg](https://img.shields.io/badge/FFmpeg-7.1-green) ![Platform](https://img.shields.io/badge/Platform-Jetson%20AGX%20Orin-orange) ![JetPack](https://img.shields.io/badge/JetPack-6.2.1-red)

**专为NVIDIA Jetson AGX Orin优化的OBS Studio完整安装包**

## 🚀 特性亮点

- ✅ **完整GUI界面** - 基于Qt6的专业直播软件
- ✅ **硬件加速编码** - NVMPI H.264/HEVC硬件编码支持  
- ✅ **内置FFmpeg 7.1** - 无需单独安装，开箱即用
- ✅ **一键安装** - 智能安装脚本，自动配置所有依赖
- ✅ **专业功能** - 直播推流、本地录制、场景管理
- ✅ **Jetson优化** - 专门针对ARM64架构和Tegra GPU优化

## 📦 安装包信息

| 文件 | 大小 | 描述 |
|------|------|------|
| `obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz` | 96MB | 主安装包 |
| `obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz.sha256` | - | 校验和文件 |
| `INSTALL_INSTRUCTIONS_COMPLETE.txt` | - | 快速安装指南 |
| `RELEASE_INFO_COMPLETE.md` | - | 详细发布说明 |

## 💻 系统要求

- **硬件**: NVIDIA Jetson AGX Orin
- **系统**: JetPack 6.2.1 (Ubuntu 22.04.3 LTS ARM64)
- **内存**: 8GB+ 推荐
- **存储**: 500MB+ 可用空间

## ⚡ 快速安装

### 方法1: 下载Release版本 (推荐)

```bash
# 1. 下载安装包
wget https://github.com/2WalterW/OBS4Jetson/releases/download/v32.0.0/obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz

# 2. 验证完整性
wget https://github.com/2WalterW/OBS4Jetson/releases/download/v32.0.0/obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz.sha256
sha256sum -c obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz.sha256

# 3. 解压安装
tar -xzf obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz
cd obs-studio-jetson-package
sudo ./install.sh

# 4. 启动使用
obs
```

### 方法2: 克隆仓库

```bash
# 克隆完整项目 (包含安装包)
git clone https://github.com/2WalterW/OBS4Jetson.git
cd OBS4Jetson
tar -xzf obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz
cd obs-studio-jetson-package
sudo ./install.sh
```

## 🎯 核心功能

### 硬件编码器
- `h264_nvmpi` - NVMPI H.264 硬件编码
- `hevc_nvmpi` - NVMPI HEVC 硬件编码

### 推荐设置

**直播设置 (1080p60)**:
```
分辨率: 1920x1080
帧率: 60 FPS
编码器: FFmpeg NVMPI H.264
比特率: 6000 kbps
```

**录制设置 (4K30)**:
```
分辨率: 3840x2160  
帧率: 30 FPS
编码器: FFmpeg NVMPI HEVC
比特率: 20000 kbps
```

## 📚 文档

- [快速安装指南](INSTALL_INSTRUCTIONS_COMPLETE.txt) - 简单安装步骤
- [详细发布说明](RELEASE_INFO_COMPLETE.md) - 完整技术规格和使用说明

## 🔧 技术规格

- **OBS Studio**: 32.0.0-beta2-modified
- **FFmpeg**: 7.1 (Git hash: 1b48158) 
- **Qt Framework**: 6.2.4
- **编译器**: GCC 11.4.0
- **架构**: ARM64 (aarch64)
- **插件数量**: 40+

## 🆚 优势对比

| 特性 | OBS4Jetson | 手动编译 | 官方版本 |
|------|------------|----------|----------|
| 安装难度 | ⭐ 一键安装 | ⭐⭐⭐⭐⭐ 复杂 | ⭐⭐ 简单但受限 |
| NVMPI支持 | ✅ 完整支持 | ✅ 需要配置 | ❌ 不支持 |
| FFmpeg集成 | ✅ 内置7.1 | ⭐ 需单独编译 | ❌ 系统版本 |
| 硬件优化 | ✅ Jetson优化 | ⭐ 手动优化 | ❌ 通用版本 |

## ❓ 故障排除

### 常见问题

1. **安装失败**
   - 确保有root权限: `sudo ./install.sh`
   - 检查系统版本: JetPack 6.2.1

2. **硬件编码不可用**
   - 验证编码器: `/usr/local/bin/ffmpeg -encoders | grep nvmpi`
   - 检查依赖: `ldd /usr/lib/aarch64-linux-gnu/obs-plugins/obs-ffmpeg.so`

3. **启动失败**
   - 查看日志: `~/.config/obs-studio/logs/`

## 🗑️ 卸载

```bash
cd obs-studio-jetson-package
sudo ./uninstall.sh
```

## 📄 许可证

本项目基于OBS Studio开源项目，遵循GPL v2+许可证。

## 🙏 致谢

- [OBS Studio](https://obsproject.com/) - 开源直播录制软件
- [jetson-ffmpeg](https://github.com/Seeed-Studio/jetson-ffmpeg) - Jetson硬件加速支持
- NVIDIA Jetson 社区

---

**🎉 为Jetson AGX Orin用户提供专业级直播录制解决方案！**

> 如果这个项目对您有帮助，请给个⭐Star支持一下！