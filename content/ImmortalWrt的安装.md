---
title: ImmortalWrt 的安装
date: 2024-11-13T22:57:00
tags:
  - Openwrt
---

## 原版固件安装

首先进入固件选择网站: https://firmware-selector.immortalwrt.org/ ，选择适合自己设备的固件
我是一台 X86 小主机，选择`Generic x86/64`。

`img.gz`文件，解压后得到 img 文件`immortalwrt-23.05.4-0814427250ba-x86-64-generic-ext4-combined-efi.img`
使用`DiskImage`工具进行写盘（在 PE 系统操作）

> 这个工具的官网是: https://roadkil.net/program.php?ProgramID=12

选择安装`COMBINED-EFI (EXT4)`版本

> [!todo]+ Todo:
> 映像格式有什么区别

### 自定义预安装软件包

ImmortalWrt 提供了**自定义预安装软件包**和**首次启动脚本**的功能
比如我想安装 `argon` 主题，将 `luci-theme-argon` 添加到预安装软件包列表中即可
下载的固件就会预装好对应的软件包

常用的软件包:

- `luci-theme-argon` argon 主题
- `luci-app-argon-config` `luci-i18n-argon-config-zh-cn` argon 主题设置及中文包
- `openssh-sftp-server` sftp server, 用于 winscp 传文件
- `luci-app-ttyd` `luci-i18n-ttyd-zh-cn` 网页终端及其中文语言包

```bash
luci-theme-argon luci-app-argon-config luci-i18n-argon-config-zh-cn luci-app-ttyd luci-i18n-ttyd-zh-cn
```

## 使用 armbian-installer 进行安装

得益于悟空大佬的开源项目，OpenWrt 的安装变得非常简单

自动编译 ImmortalWrt: https://github.com/wukongdaily/AutoBuildImmortalWrt

IMG 安装器: https://github.com/wukongdaily/armbian-installer

### 安装 ImmortalWrt

下载`immortalwrt-installer-x86_64.iso`，丢进`ventoy`启动盘中，选择该镜像进行安装。
进入系统后使用`ddd`命令进入安装向导。

### OpenWRT 配置

> 参考 https://wkdaily.cpolar.top/archives/13

#### 安装 iStoreOS 商店

```bash
wget -qO imm.sh https://cafe.cpolar.top/wkdaily/zero3/raw/branch/main/zero3/imm.sh && chmod +x imm.sh && ./imm.sh
```

#### 安装网络向导和首页

```bash
is-opkg install luci-i18n-quickstart-zh-cn
```

#### 配置网络

进入`网络向导`，我这里选择“连接现有路由器”，也可配置为旁路由模式。
设置 IP 为`192.168.1.2`（光猫的网段），将 OpenWrt 连接到光猫上，然后主路由器连接到 OpenWRT 上。

> 重新刷机时，将主路由连光猫正常进行上网，openwrt 连入主路由进后台配置，配置好后重新连回光猫。

#### 安装 Nikki

添加软件源:

```bash
curl -s -L https://github.com/nikkinikki-org/OpenWrt-nikki/raw/refs/heads/main/feed.sh | ash
```

安装:

```bash
opkg install nikki
opkg install luci-app-nikki
opkg install luci-i18n-nikki-zh-cn
```
