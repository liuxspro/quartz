---
title: Rust 安装及换源
date: 2025-03-29T21:49
tags:
  - Rust
  - Mirrors
---

使用 `https://rsproxy.cn/` 的镜像源

## 设置 Rustup 镜像

windows powershell 命令:

```pwsh
[System.Environment]::SetEnvironmentVariable("RUSTUP_DIST_SERVER", "https://rsproxy.cn", "User")

[System.Environment]::SetEnvironmentVariable("RUSTUP_UPDATE_ROOT", "https://rsproxy.cn/rustup", "User")
```

Linux shell 命令:

```
export RUSTUP_DIST_SERVER="https://rsproxy.cn"
export RUSTUP_UPDATE_ROOT="https://rsproxy.cn/rustup"
```

## 安装 Rust

```
curl --proto '=https' --tlsv1.2 -sSf https://rsproxy.cn/rustup-init.sh | sh
```

## 设置 crates.io 镜像

> 修改配置 ~/.cargo/config，已支持 git 协议和 sparse 协议，>=1.68 版本建议使用 sparse-index，速度更快

```toml
[source.crates-io]
replace-with = 'rsproxy-sparse'
[source.rsproxy]
registry = "https://rsproxy.cn/crates.io-index"
[source.rsproxy-sparse]
registry = "sparse+https://rsproxy.cn/index/"
[registries.rsproxy]
index = "https://rsproxy.cn/crates.io-index"
[net]
git-fetch-with-cli = true
```
