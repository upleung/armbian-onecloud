<div align="center">

# 🚀 Armbian for 玩客云 (OneCloud)

**专为玩客云 (Amlogic S805 / ARMv7) 打造的最新 Armbian 自动化构建系统**

[![GitHub Workflow Status](https://img.shields.io/github/actions/workflow/status/upleung/armbian-onecloud/ci.yml?branch=main&style=for-the-badge&logo=github-actions&logoColor=white&color=blue)](https://github.com/upleung/armbian-onecloud/actions)
[![Latest Release](https://img.shields.io/github/v/release/upleung/armbian-onecloud?style=for-the-badge&logo=github&color=success)](https://github.com/upleung/armbian-onecloud/releases/latest)
[![Architecture](https://img.shields.io/badge/Arch-ARMv7%20%2F%20armhf-orange?style=for-the-badge&logo=arm)](https://github.com/upleung/armbian-onecloud)
[![SoC](https://img.shields.io/badge/SoC-Amlogic%20S805-deepskyblue?style=for-the-badge)](https://github.com/upleung/armbian-onecloud)

[📥 下载最新固件](https://github.com/upleung/armbian-onecloud/releases) • [🛠️ 刷机指南](#-刷机说明) • [💡 镜像说明](#-镜像变体说明)

</div>

---

## 🌟 项目亮点

* 📺 **HDMI 输出完美修复**：内置专为 Amlogic S805 整合的 HDMI 驱动与时钟补丁，无论是**命令行 TTY 终端**还是 **XFCE 4 桌面环境**均可完美点亮显示器！
* ⚡ **多版本支持**：原生适配 **Debian 12 (Bookworm)** 与 **Ubuntu 22.04 LTS (Jammy)**。
* 📦 **全形态覆盖**：包含 **Minimal (极简)**、**CLI (标准命令行)**、**XFCE Desktop (轻量桌面)** 三种镜像变体。
* 🔥 **开箱即用线刷包**：自动调用 `AmlImg` 打包生成 `.burn.img` 镜像，支持直接使用晶晨 USB 烧录工具（USB Burning Tool）一键刷入 eMMC。
* 🤖 **GitHub Actions 云端全自动构建**：保持最新 Armbian 构建体系，构建产物一键打包直达 Releases。

---

## 📋 规格参数与环境

| 项目 | 参数规格 / 版本 |
| :--- | :--- |
| **适配设备** | 玩客云 OneCloud (网心云 1代) |
| **CPU 架构** | Amlogic S805 (4 核 Cortex-A5 @ 1.5GHz / ARMv7-A `armhf`) |
| **Armbian 基线** | `26.08.0` |
| **Linux 内核** | `6.12.x LTS` (Armbian `current` 分支) |
| **基础发行版** | Debian 12 (Bookworm) / Ubuntu 22.04 LTS (Jammy) |
| **产物格式** | Standard `.img.xz`（标准镜像） / Amlogic `.burn.img.xz`（线刷包） |

---

## 📦 镜像变体说明

编译任务会自动生成以下两类格式镜像（均使用 `xz` 高比例压缩）：

| 文件后缀 | 适用于场景 | 说明 |
| :--- | :--- | :--- |
| **`*.burn.img.xz`** | **线刷（强烈推荐）** | 解压出 `.burn.img` 后，使用 **Amlogic USB Burning Tool** 工具配合双公头 USB 线直接烧录至玩客云内置 eMMC。（实测USB-C数据线连接带C口的笔记本也能刷）） |
| **`*.img.xz`** | **卡刷 / 传统 DD 刷机** | 解压出 `.img` 后，可使用 **BalenaEtcher** 或 **Rufus** 写入 SD 卡、U 盘，或在已有 Linux 下通过 `dd` 命令写入。 |

### 发行版及版本规格表：

* 🟢 **bookworm-minimal**：体积最小、资源占用极低，适合跑 Docker、青龙、NAS 挂载等纯服务端场景。
* 🔵 **bookworm-cli**：标准命令行版本，内置常用系统工具，适合大多数 Linux 玩家。
* 🟣 **bookworm-xfce_desktop**：自带 XFCE 4 桌面，配合 HDMI 显示器可作为轻量终端 display/仪表盘显示屏使用。
* 🟠 **jammy-***：Ubuntu 22.04 LTS 环境下的对应变体版本。

---

## 🛠️ 刷机说明（以线刷为例）

1. **获取固件**：
   前往本仓库的 [Releases 页面](https://github.com/upleung/armbian-onecloud/releases)，下载适合您需求的 `*.burn.img.xz` 压缩包并解压。
2. **准备工具**：
   * 双公头 USB 数据线 一条（或用USB-C数据线连接笔记本也能刷）
   * 安装 **Amlogic USB Burning Tool** (推荐 v2.2.0 及以上版本)
3. **开始烧录**：
   * 打开烧录工具，导入解压出来的 `.burn.img` 镜像文件。
   * 勾选“擦除烧录”选项（建议勾选擦除所有）。
   * 玩客云板子短接进入烧录模式（USB线插在靠网口侧的 USB 口），点击“开始”。
   * 进度条走满至 100% 提示烧录成功后，断电重新拔插电源即可正常启动。
4. **显示器连接**：
   * 使用 HDMI 线连接玩客云与显示器/电视，上电启动即可看到开机日志输出（TTY 命令行或桌面界面）。

---

## 🤖 自动化构建 (GitHub Actions)

本项目基于 GitHub Actions 实现全自动构建。如果您希望自行编译：

1. **Fork 本仓库** 到您的个人账号下。
2. 进入仓库的 **Actions** 选项卡。
3. 在左侧选择 **Build Armbian for OneCloud** 工作流。
4. 点击右侧 **Run workflow** 手动触发构建。
5. 构建完成后，新镜像会自动上传并发布到您个人仓库的 **Releases** 页面中。

---

## 🙏 致谢与参考

* 官方 Armbian 构建框架：[armbian/build](https://github.com/armbian/build)
* 玩客云构建参考仓库：[hzyitc/armbian-onecloud](https://github.com/hzyitc/armbian-onecloud)
* HDMI 补丁与内核支持：[xdarklight/linux (meson-mx-integration)](https://github.com/xdarklight/linux/tree/meson-mx-integration-5.18-20220417)
* Amlogic S805 Datasheet & Odroid 官方文档

---

## 📄 开源许可证

本项目基于 [GPL-3.0 许可证](LICENSE) 开源。
