# OBS Studio for Jetson AGX Orin - Complete Release Package

## 发布信息 (完整版 - 包含FFmpeg)

**版本**: OBS Studio 32.0.0-beta2 (Jetson优化版) + FFmpeg 7.1  
**发布日期**: 2025-09-06  
**包大小**: 96MB (压缩后)  
**解压后大小**: 234MB  
**文件数量**: 1,451 个文件

## ⭐ 重要更新

**现在包含完整的FFmpeg 7.1！** 用户无需单独安装FFmpeg，即可直接获得NVMPI硬件编码支持。

## 包内容

### 🎯 OBS Studio 组件
- OBS Studio 主程序 (107MB)
- 40+ 插件模块
- Qt6 GUI 界面
- 多语言支持文件
- 图标和主题资源

### 🚀 FFmpeg 7.1 (包含)
- **FFmpeg 可执行文件** (`/usr/local/bin/ffmpeg`, `/usr/local/bin/ffprobe`)
- **完整库文件** (`libavcodec.so.61`, `libavformat.so.61`, `libavutil.so.59`, `libavfilter.so.10`, `libavdevice.so.61`)
- **NVMPI编码器** (h264_nvmpi, hevc_nvmpi)
- **jetson-ffmpeg集成** (专为Jetson AGX Orin优化)

### 📋 安装工具
- 智能安装脚本 (`install.sh`)
- 安全卸载脚本 (`uninstall.sh`)
- 完整文档 (`README.md`)
- 版本信息 (`VERSION`)

## 核心优势

✅ **一键安装** - 无需复杂的依赖配置  
✅ **完整集成** - FFmpeg + OBS Studio 完美结合  
✅ **硬件加速** - NVMPI H.264/HEVC 硬件编码  
✅ **专业功能** - 直播推流 + 本地录制  
✅ **即装即用** - 解压即可获得完整功能  

## 安装方法

### 快速安装

```bash
# 1. 下载完整安装包 (96MB)
wget obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz

# 2. 验证完整性
sha256sum -c obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz.sha256

# 3. 解压并安装
tar -xzf obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz
cd obs-studio-jetson-package
sudo ./install.sh

# 4. 立即使用
obs
```

### 安装过程说明

安装脚本会自动：
1. 检查系统兼容性
2. 安装必要的系统依赖包
3. 部署 OBS Studio 到系统目录
4. 安装 FFmpeg 7.1 到 `/usr/local/`
5. 配置动态链接库
6. 验证硬件编码器可用性
7. 创建桌面快捷方式

## 系统要求

- **硬件**: NVIDIA Jetson AGX Orin
- **系统**: JetPack 6.2.1 (Ubuntu 22.04.3 LTS ARM64)
- **内存**: 8GB+ 推荐
- **存储**: 500MB+ 可用空间
- **权限**: 需要 root 权限进行系统安装

## 技术规格

### OBS Studio 特性
- 版本: 32.0.0-beta2-modified
- GUI框架: Qt 6.2.4
- 编译器: GCC 11.4.0
- 架构: ARM64 优化
- 插件: 40+ 模块

### FFmpeg 规格  
- 版本: 7.1 (Git hash: 1b48158)
- 编译配置: `--enable-nvmpi --enable-shared --enable-gpl --enable-nonfree`
- 安装位置: `/usr/local/bin/`, `/usr/local/lib/`
- NVMPI支持: H.264 + HEVC 硬件编码

### 硬件编码器
- `h264_nvmpi` - NVMPI H.264 encoder wrapper
- `hevc_nvmpi` - NVMPI HEVC encoder wrapper  
- GPU加速: ✅
- 低延迟: ✅
- 高质量: ✅

## 性能基准

### 推荐直播设置
- **分辨率**: 1920x1080
- **帧率**: 60 FPS  
- **编码器**: FFmpeg NVMPI H.264
- **比特率**: 6000 kbps
- **预设**: 低延迟

### 推荐录制设置  
- **分辨率**: 3840x2160 (4K)
- **帧率**: 30 FPS
- **编码器**: FFmpeg NVMPI HEVC  
- **比特率**: 20000 kbps
- **质量**: 高质量

## 与系统FFmpeg的关系

本包安装的FFmpeg 7.1会安装到 `/usr/local/`，不会覆盖系统自带的FFmpeg。两者可以和谐共存：

- **系统FFmpeg**: `/usr/bin/ffmpeg` (Ubuntu默认)
- **Jetson FFmpeg**: `/usr/local/bin/ffmpeg` (本包提供)
- **OBS使用**: 自动使用Jetson FFmpeg获得NVMPI支持

## 故障排除

### 常见问题

1. **安装失败**
   - 确保有root权限: `sudo ./install.sh`
   - 检查系统兼容性: Jetson AGX Orin + JetPack 6.2.1

2. **硬件编码不可用**  
   - 验证编码器: `/usr/local/bin/ffmpeg -encoders | grep nvmpi`
   - 检查库链接: `ldd /usr/lib/aarch64-linux-gnu/obs-plugins/obs-ffmpeg.so`

3. **OBS启动失败**
   - 检查依赖: `ldd /usr/bin/obs`
   - 查看日志: `~/.config/obs-studio/logs/`

## 包文件清单

```
obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz      (96MB - 完整安装包)
obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz.sha256  (校验和文件)
RELEASE_INFO_COMPLETE.md                                         (本发布说明)
```

## 优势对比

| 特性 | 本包 | 手动编译 | 官方版本 |
|------|------|----------|----------|
| 安装难度 | ⭐ 一键安装 | ⭐⭐⭐⭐⭐ 复杂 | ⭐⭐ 简单但功能受限 |
| NVMPI支持 | ✅ 完整支持 | ✅ 需要配置 | ❌ 不支持 |
| FFmpeg集成 | ✅ 内置7.1 | ⭐ 需单独编译 | ❌ 系统版本 |
| 硬件优化 | ✅ Jetson优化 | ⭐ 手动优化 | ❌ 通用版本 |
| 技术支持 | ✅ 文档完整 | ❌ 自行解决 | ⭐ 官方支持 |

## 卸载方法

```bash
cd obs-studio-jetson-package
sudo ./uninstall.sh
```

卸载脚本提供选项：
- 卸载OBS Studio (必选)
- 卸载FFmpeg 7.1 (可选，避免影响其他程序)

---

**总结**: 这是目前最完整的Jetson AGX Orin OBS Studio解决方案，集成了所有必要组件，为用户提供开箱即用的专业级直播和录制体验。

**构建者**: Claude Code Assistant  
**基于**: OBS Studio + FFmpeg 开源项目  
**专为**: NVIDIA Jetson AGX Orin 用户设计