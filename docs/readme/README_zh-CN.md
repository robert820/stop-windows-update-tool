<div align="center">

<a href="https://blog.dei3c.com" target="_blank" rel="noopener noreferrer">
  <img src="https://github.com/user-attachments/assets/2830eb70-512c-4ddb-87ec-5213a6e465b1" alt="得翼科技 | Windows 停止更新工具" height="70" />
</a>

<br /><br />

[繁體中文](../../README.md) · **简体中文** · [English](README_en.md)

# Windows 停止更新工具 (Stop Windows Update Tool)

### 彻底阻断微软自动更新 · 还给电脑纯净安定的工作环境
专为日常使用、电竞游戏、专业工作站与 WinPE 电脑维修环境打造

[![Platform](https://img.shields.io/badge/Platform-Windows%207%20%7C%208%20%7C%2010%20%7C%2011%20%7C%20WinPE-blue?style=flat-square&logo=windows)](https://github.com/robert820/stop-windows-update-tool)
[![License](https://img.shields.io/badge/License-Freeware-informational?style=flat-square)](../../LICENSE)
[![Type](https://img.shields.io/badge/Type-Freeware%20%7C%20Portable-success?style=flat-square)](#-下载与使用说明)
[![Download](https://img.shields.io/badge/Download-GitHub%20Releases-blue?style=flat-square&logo=github)](https://github.com/robert820/stop-windows-update-tool/releases)

**告别强制重启、带宽占用与更新蓝屏。五重防御深度关闭 Windows Update，随时一键无损还原！**

[软件简介](#-软件简介) · [功能介绍](#-功能介绍) · [软件操作画面](#-软件操作画面) · [下载与使用说明](#-下载与使用说明) · [系统需求](#-系统兼容性与需求) · [常见问题](#-常见问题-faq) · [问题反馈](#-问题反馈与支持)

</div>

---

## 📖 软件简介

在进行重要的商业工作、电竞对战、线上直播或大型 3D 渲染时，微软 Windows 的强制自动更新常带来严重的困扰：
- 突如其来的自动重新启动，导致未保存的文档与项目毁于一旦。
- 后台 Delivery Optimization (传递优化) 与 BITS 疯狂占用网络带宽与硬盘读写，造成系统延迟卡顿。
- 恼人的系统更新造成硬件驱动冲突、周边打印机失效，甚至开机蓝屏 (BSOD)。
- 系统反复“死灰复燃”，即使手动在“服务”中关闭，微软的医疗保健服务 (WaaSMedic) 又会在开机时自动强行重启。
- 关机菜单中顽固出现的“更新并关机”、“更新并重新启动”幻影按钮，让人避无可避。

**“Windows 停止更新工具”** 是一款专为 Windows 10 / 11 / 8 / 7 用户与电脑维修技术人员打造的原生绿色免安装实用工具。结合**系统底层服务冻结**、**全量微软更新 CDN 域名屏蔽**、**更新暂存快取深度清理**、**关机菜单幻影更新按钮消除**与 **DISM 撤销排程** 等五重防御技术，彻底杜绝 Windows Update 自动重启与强制更新，并提供 1 分钟守护防御与一键完整还原机制，让您随心所欲掌控电脑系统！

---

## ✨ 功能介绍

### 1. ⚡ 系统核心服务底层冻结 (Multi-Service Deep Freeze)
- 全面接管并冻结 Windows 更新核心 5 大系统服务：
  - `wuauserv`：Windows Update 更新主服务
  - `dosvc`：Delivery Optimization (传递优化 / P2P 后台上传)
  - `bits`：Background Intelligent Transfer Service (后台智能传送服务)
  - `WaaSMedicSvc`：Windows Update 医疗保健修复服务（彻底瓦解微软自动修复与自愈复活机制）
  - `UsoSvc`：Update Orchestrator Service (更新排程主控)
- 通过 Win32 底层 API 直接将注册表启动类型锁定为“已禁用 (Disabled)”，防止系统任务计划程序在后台自动唤醒。

### 2. 🛡️ 全量微软更新 CDN 域名屏蔽 (Hosts Domain Shield)
- 内置 19 组微软更新与遥测分发域名黑名单（涵盖 `windowsupdate.microsoft.com`、`download.windowsupdate.com`、`delivery.mp.microsoft.com` 等），通过系统 Hosts 文件直接导向本机回环地址 (`127.0.0.1`)。
- 双重路径兼容处理（自动识别 `Sysnative` 与 `System32`），确保 32 位与 64 位环境皆能完美阻断。

### 3. 🧹 更新暂存快取深度清理 (SoftwareDistribution Cache Cleanup)
- 服务停用后，自动安全清空 `C:\Windows\SoftwareDistribution\Download` 与 `DataStore` 暂存目录。
- 释放数 GB 被未完成或损坏更新占用的磁盘空间，彻底斩断系统“重启又重新下载”的无限卡死循环。

### 4. 🚫 开始菜单“更新并关机”幻影按钮彻底扫除 (Ghost Button Elimination)
- 写入组策略 (GPO) 与家庭版专用配置 (`NoAUShutdownOption`、`NoAUAsDefaultShutdownOption`、`ShutdownFlyoutOptions`、`EnhancedShutdownEnabled`)。
- 深入扫除 5 大系统残留重启标记（包含 `RebootRequired`、`RebootPending`、`RebootInProgress` 等），重启后恢复干净利落的“正常关机 / 重新启动”。

### 5. ↩️ DISM 撤销已就绪更新操作 (Revert Pending Actions)
- 调用系统原生 DISM 引擎执行 `/online /cleanup-image /RevertPendingActions`，撤回所有已经处于 Staged 状态准备开机安装的更新封包，避免重启时卡在“正在处理更新...”进度条。

### 6. ⏱️ 后台 1 分钟守护防御与状态监控 (Active Defense Thread)
- 执行停止操作后，自动启动后台 60 秒持续守护监控（每 2 秒轮询防御一次），一旦侦测到微软后台企图还原 Hosts 或重新拉起服务，即时记录警报。
- 智能侦测 `TrustedInstaller` (Windows Modules Installer) 状态，提供专业维护诊断提示。

### 7. 🔄 一键无损还原官方更新 (One-Click Safe Restore)
- 想安装最新系统补丁或功能升级时，只需点击“恢复更新”，即可自动清除 Hosts 屏蔽、还原服务默认启动状态（手动/自动）、解除关机菜单限制，重启后无缝恢复微软官方更新管道。

### 8. 🪶 原生高效、极致轻量、免安装绿色单文件 (Native Rust & Software Renderer)
- 采用 Rust 打造，无任何臃肿垃圾依赖，占用极低内存与 CPU。
- 强制配置软件渲染 (`SLINT_BACKEND=software`)，即便在没有 GPU 硬件加速的老旧电脑或 WinPE 维护环境中亦能稳定运作，绝不崩溃。

---

## 📸 软件操作画面

<div align="center">
  <img src="../../images/應用程式執行畫面.png" alt="Windows 停止更新工具操作界面" width="720" />
</div>

---

## 📦 下载与使用说明

### 📥 下载方式
1. 前往本项目的 [Releases 页面](https://github.com/robert820/stop-windows-update-tool/releases) 下载最新版可执行文件。
2. 本程序为**单文件免安装绿色版**，无需安装任何额外运行库，下载即可直接放入维修 U 盘随身携带。

### 🚀 使用指南
1. 下载后以 **“管理员身份运行”** 本工具（因涉及修改 Windows 系统服务与 Hosts 文件，需管理员权限）。
2. 界面会实时显示当前“Windows Update”、“传递优化”、“后台智能传输”、“更新排程主控”之运行状态与 Hosts 阻断状态。
3. **彻底停止更新**：
   - 点击“**停止更新**”，程序将自动依次阻断域名、停用服务、清空暂存、清除关机按钮标记并撤销已挂起更新。
   - 完成后请**重新启动电脑**，即可享受完全无更新干扰的系统！
4. **恢复官方更新**：
   - 点击“**恢复更新**”，程序将自动解除域名屏蔽并将各项系统服务还原为官方默认值。
   - 完成后请**重新启动电脑**，即可正常前往 Windows Update 检查并安装更新。

---

## 🖥️ 系统兼容性与需求

- **操作系统**：Windows 11 / 10 / 8.1 / 8 / 7 (SP1) 及各类 WinPE 维护环境
- **架构支持**：64 位 (x64) 与 32 位 (x86)
- **运行权限**：需要“管理员权限 (Run as Administrator)”
- **运行环境**：单一绿色原生程序，无需额外安装 .NET Framework 或 VC++ 可再发行组件包

---

## ❓ 常见问题 (FAQ)

<details>
<summary><b>Q1: 这款软件完全免费吗？电脑维修同行可以使用吗？</b></summary>
A: 是的！本软件免费提供个人、企业与电脑维修工作室使用，亦可自由放置于维修随身盘中帮客户维护修复电脑。但严禁单独贩售、出租或捆绑收费营利。
</details>

<details>
<summary><b>Q2: 为什么杀毒软件偶尔会提示或误报？</b></summary>
A: 本程序为纯净绿色工具，绝无后门或木马。由于本程序直接调用 Windows 底层 API 修改系统服务启动类型与 Hosts 文件，部分杀毒引擎启发式可能较严格判定，请安心加入信任名单。
</details>

<details>
<summary><b>Q3: 点击“停止更新”后，为什么开始菜单仍显示“更新并关机”？</b></summary>
A: 若在运行本工具前系统已在后台下载好更新文件并标记了“准备重启”，本工具会自动清除该标记并调用 DISM 撤销操作。请务必在点击停止后“重新启动电脑”一次，重启后系统便会清除挂起状态，开始菜单中的更新按钮即会彻底消失。
</details>

<details>
<summary><b>Q4: 停用更新后，日后微软推出重大安全性更新我想安装该怎么办？</b></summary>
A: 随时开启本工具，点击“恢复更新”按钮并重新启动电脑，即可百分之百无损还原至微软官方默认状态，正常使用 Windows Update 下载补丁。
</details>

<details>
<summary><b>Q5: 本工具需要常驻在后台运行吗？</b></summary>
A: 完全不需要！本工具为“一次性修改工具”，在完成停止或恢复操作并重启电脑后，所有设置已永久写入系统底层与注册表。日常使用时无需常驻后台，完全不占用任何 CPU 与内存资源。
</details>

---

## 💬 问题反馈与支持

- 🐛 **错误回报与功能建议**：欢迎至本项目的 [Issues 页面](https://github.com/robert820/stop-windows-update-tool/issues) 提出。
- 🌐 **得翼科技官方网站**：[https://blog.dei3c.com](https://blog.dei3c.com)
- 📧 **技术支持与商务洽询**：请通过官方网站联系我们。

---

## 📄 授权条款 (License)

本软件采用专有免费软件授权（Proprietary Freeware），完整授权规范、使用条款与免责声明请参阅 [LICENSE](../../LICENSE) 文件。
