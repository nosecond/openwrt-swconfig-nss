# HONOR XD27 (IPQ5018) OpenWrt NSS 固件

> ⚠️ **项目状态：测试阶段 (Beta)**

## 📖 项目简介

本项目基于 [mufeng05/openwrt-cmcc-pz-l8-nss](https://github.com/mufeng05/openwrt-cmcc-pz-l8-nss) 修改而来。
核心 OpenWrt 源码基线更新至 **`v25.12.6`**，主要针对 **HONOR XD27** 路由器进行适配。

本项目在保留上游 NSS 加速特性的基础上，对系统进行了更改：
1. **回归纯净**：剥离了原项目中定制的配置，将系统状态还原为 OpenWrt 默认风格。
2. **新增实用组件**：集成轻量级代理服务 `msd_lite`。
3. **独立硬件监控**：将定制化的硬件状态展示页面独立封装为 `luci-app-hardware`。

## ✨ 核心特性

- **NSS 硬件加速**：完整集成 `kmod-qca-nss-drv`、`kmod-qca-nss-ecm` 等驱动，支持无线与有线硬件 NAT 卸载。
- **原生体验**：还原 OpenWrt 默认的主题、网络配置及系统参数，更贴近官方原生体验。
- **msd_lite**：预装轻量级单播代理服务及 LuCI 管理界面，满足家庭组播转单播需求。

## 📦 刷机指南

请在项目的 **Releases** 页面下载对应版本的固件压缩包，并在刷机前务必核对 `sha256sums`。

| 文件名后缀 | 适用场景与说明 |
| :--- | :--- |
| `*-squashfs-sysupgrade.bin` | **系统升级包**。适用于目前已经运行 OpenWrt 的设备，在 LuCI 后台或终端执行 `sysupgrade -n`。 |
| `*-squashfs-factory.ubi` | **原厂/底包直刷包**。适用于从原厂固件或 U-Boot 环境过渡，通过底层工具写入。 |
| `*-initramfs-uImage.itb` | **内存恢复包**。不写入闪存，仅在内存中运行，适用于救砖或临时调试。 |

## 🛠️ 构建与编译

本项目已配置 GitHub Actions 自动化编译流程，每次构建时，将自动执行：
1. 拉取 OpenWrt `v25.12.6` 源码。
2. 应用适配补丁并注入自定义 Feed（包含 `luci-app-hardware`）。
3. 编译并发布至 GitHub Releases。

## 🙏 致谢

- 感谢 [mufeng05](https://github.com/mufeng05) 提供的 NSS 基础项目。
- 感谢 OpenWrt 社区及所有上游开源贡献者。

---

