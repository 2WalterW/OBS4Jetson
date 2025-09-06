# OBS Studio v32.0.0 for Jetson AGX Orin

## 🎉 首次发布 - Complete Package

**发布日期**: 2025-09-06  
**版本**: OBS Studio 32.0.0-beta2 + FFmpeg 7.1  
**平台**: NVIDIA Jetson AGX Orin (JetPack 6.2.1)

## ✨ 核心特性

🎯 **完整GUI界面** - 基于Qt6的专业直播软件  
🚀 **NVMPI硬件编码** - H.264/HEVC硬件加速编码  
📦 **内置FFmpeg 7.1** - 无需单独安装依赖  
⚡ **一键安装** - 智能安装脚本，96MB开箱即用  

## 📦 下载文件

### 主安装包
- **obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz** (96MB)
  - 完整的OBS Studio + FFmpeg 7.1安装包
  - 包含NVMPI硬件编码器支持
  - 40+插件模块 + 智能安装脚本

### 校验文件
- **obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz.sha256**
  - SHA256校验和，确保下载完整性

## ⚡ 安装方法

```bash
# 1. 下载主安装包
wget https://github.com/2WalterW/OBS4Jetson/releases/download/v32.0.0/obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz

# 2. 解压安装
tar -xzf obs-studio-jetson-agx-orin-v32.0.0-complete-20250906.tar.gz
cd obs-studio-jetson-package
sudo ./install.sh

# 3. 启动使用
obs
```

## 🔧 技术规格

| 组件 | 版本 | 说明 |
|------|------|------|
| OBS Studio | 32.0.0-beta2 | Jetson优化版本 |
| FFmpeg | 7.1 (1b48158) | 包含jetson-ffmpeg支持 |
| Qt Framework | 6.2.4 | GUI界面框架 |
| 编译器 | GCC 11.4.0 | ARM64优化编译 |
| 硬件编码器 | NVMPI | h264_nvmpi + hevc_nvmpi |
| 插件数量 | 40+ | 完整功能支持 |

## 🎯 推荐设置

### 直播设置 (1080p60)
- 分辨率: 1920x1080 @ 60 FPS
- 编码器: FFmpeg NVMPI H.264
- 比特率: 6000 kbps

### 录制设置 (4K30)
- 分辨率: 3840x2160 @ 30 FPS  
- 编码器: FFmpeg NVMPI HEVC
- 比特率: 20000 kbps

## 🆚 优势对比

| 特性 | OBS4Jetson | 手动编译 | 官方版本 |
|------|------------|----------|----------|
| 安装难度 | ⭐ 一键安装 | ⭐⭐⭐⭐⭐ 复杂 | ⭐⭐ 简单但受限 |
| NVMPI支持 | ✅ 完整支持 | ⭐ 需要配置 | ❌ 不支持 |
| FFmpeg集成 | ✅ 内置7.1 | ⭐ 需单独编译 | ❌ 系统版本 |
| 即用性 | ✅ 开箱即用 | ❌ 需要专业知识 | ❌ 功能受限 |

## 💻 系统要求

- **硬件**: NVIDIA Jetson AGX Orin
- **操作系统**: JetPack 6.2.1 (Ubuntu 22.04.3 LTS ARM64)
- **内存**: 8GB+ 推荐
- **存储空间**: 500MB+ 可用空间
- **权限**: 安装时需要root权限

## ❗ 重要说明

- 本包包含完整的FFmpeg 7.1，安装到 `/usr/local/` 不会影响系统FFmpeg
- 支持所有主流直播平台 (YouTube, Twitch, Bilibili等)
- 包含中英文界面支持
- 自动配置硬件编码器，无需手动设置

## 🛠️ 故障排除

### 安装失败
```bash
# 确保有root权限
sudo ./install.sh

# 检查系统版本
cat /etc/nv_tegra_release
```

### 硬件编码器不可用
```bash
# 验证NVMPI编码器
/usr/local/bin/ffmpeg -encoders | grep nvmpi

# 检查库链接
ldd /usr/lib/aarch64-linux-gnu/obs-plugins/obs-ffmpeg.so
```

### 启动问题
```bash
# 查看日志
ls ~/.config/obs-studio/logs/

# 检查依赖
ldd /usr/bin/obs
```

## 🗑️ 卸载方法

```bash
cd obs-studio-jetson-package
sudo ./uninstall.sh
```

## 📝 更新日志

### v32.0.0 (2025-09-06)
- ✅ 首次发布完整版本
- ✅ 集成FFmpeg 7.1 + NVMPI支持
- ✅ 优化Qt6兼容性 (6.2.4)
- ✅ 修复所有编译错误
- ✅ 添加智能安装脚本
- ✅ 包含40+插件模块
- ✅ 完整中英文文档

## 📄 许可证

基于GPL v2+许可证，遵循OBS Studio开源协议。

## 🙏 致谢

- **OBS Studio团队** - 提供优秀的开源直播软件
- **jetson-ffmpeg项目** - 提供Jetson硬件加速支持  
- **NVIDIA Jetson社区** - 提供技术支持和反馈

---

**🎉 为Jetson AGX Orin用户提供专业级直播录制解决方案！**

如有问题，请提交Issue或查看仓库文档。