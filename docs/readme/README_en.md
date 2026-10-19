<div align="center">

<a href="https://blog.dei3c.com" target="_blank" rel="noopener noreferrer">
  <img src="https://github.com/user-attachments/assets/2830eb70-512c-4ddb-87ec-5213a6e465b1" alt="DEI Tech | Stop Windows Update Tool" height="70" />
</a>

<br /><br />

[繁體中文](../../README.md) · [简体中文](README_zh-CN.md) · **English**

# Stop Windows Update Tool (Windows 停止更新工具)

### Completely Block Windows Automatic Updates · Regain a Clean, Stable PC Environment
Designed for daily use, esports gaming, workstation rendering, and WinPE computer maintenance environments.

[![Platform](https://img.shields.io/badge/Platform-Windows%207%20%7C%208%20%7C%2010%20%7C%2011%20%7C%20WinPE-blue?style=flat-square&logo=windows)](https://github.com/robert820/stop-windows-update-tool)
[![License](https://img.shields.io/badge/License-Freeware-informational?style=flat-square)](../../LICENSE)
[![Type](https://img.shields.io/badge/Type-Freeware%20%7C%20Portable-success?style=flat-square)](#-download--usage)
[![Download](https://img.shields.io/badge/Download-GitHub%20Releases-blue?style=flat-square&logo=github)](https://github.com/robert820/stop-windows-update-tool/releases)

**Say goodbye to forced restarts, bandwidth hogging, and update BSODs. Multi-layered defense to completely disable Windows Update, with instant one-click lossless restoration!**

[Overview](#-overview) · [Key Features](#-key-features) · [Screenshots](#-screenshots) · [Download & Usage](#-download--usage) · [System Requirements](#-system-compatibility--requirements) · [FAQ](#-frequently-asked-questions-faq) · [Feedback](#-support--feedback)

</div>

---

## 📖 Overview

During mission-critical work, competitive gaming, live streaming, or 3D rendering sessions, forced Windows updates often cause serious interruptions:
- Sudden automatic restarts causing unsaved documents and projects to be lost.
- Background Delivery Optimization (`DoSvc`) and BITS consuming massive network bandwidth and disk I/O, leading to severe latency and stuttering.
- Faulty updates causing peripheral driver conflicts, printer failures, or boot Blue Screens (BSOD).
- Persistent "resurrection" by Microsoft's repair services (such as `WaaSMedicSvc`), which automatically re-enable update services upon system boot even after manual disabling.
- Stubborn "Update and shut down" or "Update and restart" phantom buttons appearing in the power menu.

**Stop Windows Update Tool** is a lightweight, portable, and native utility developed in Rust for Windows 11 / 10 / 8 / 7 users and IT maintenance technicians. Combining **low-level service freezing**, **full Microsoft update CDN hosts shielding**, **update cache purging**, **power menu phantom button elimination**, and **DISM pending action rollback**, it fundamentally puts an end to forced updates while offering 60-second active defense and one-click full restoration.

---

## ✨ Key Features

### 1. ⚡ Multi-Service Low-Level Deep Freeze
- Directly manages and freezes the 5 core Windows Update services:
  - `wuauserv`: Windows Update Core Service
  - `dosvc`: Delivery Optimization (P2P background upload & download)
  - `bits`: Background Intelligent Transfer Service
  - `WaaSMedicSvc`: Windows Update Medic Service (breaks Microsoft's self-healing resurrection mechanism)
  - `UsoSvc`: Update Orchestrator Service
- Modifies service startup types to `Disabled` (4) via low-level Win32 Registry APIs, preventing the Windows Task Scheduler from automatically reviving them.

### 2. 🛡️ Microsoft Update CDN Hosts Shield
- Built-in blocklist of 19 Microsoft update and telemetry distribution domains (including `windowsupdate.microsoft.com`, `download.windowsupdate.com`, `delivery.mp.microsoft.com`, etc.), rerouting them to localhost (`127.0.0.1`).
- Dual 32-bit and 64-bit architecture compatibility handling (`Sysnative` and `System32`).

### 3. 🧹 Update Cache Deep Purging (SoftwareDistribution)
- Automatically purges `C:\Windows\SoftwareDistribution\Download` and `DataStore` directories once services are stopped.
- Reclaims gigabytes of disk space wasted by corrupt or pending update packages and breaks the endless cycle of download-and-fail loops.

### 4. 🚫 Ghost Shutdown Button Elimination
- Enforces GPO and Windows Home edition policies (`NoAUShutdownOption`, `ShutdownFlyoutOptions`, `EnhancedShutdownEnabled`).
- Thoroughly wipes 5 major system reboot pending markers (`RebootRequired`, `RebootPending`, `RebootInProgress`), restoring clean, normal shutdown options.

### 5. ↩️ DISM Revert Pending Actions
- Invokes Windows DISM engine via `/online /cleanup-image /RevertPendingActions` to revoke staged update packages scheduled for next boot, avoiding the dreaded "Working on updates..." boot delay or boot loop.

### 6. ⏱️ 60-Second Active Defense & Monitoring Thread
- Automatically runs a background 60-second watchdog thread (polling every 2 seconds) post-operation to detect and alert against background system attempts to restore hosts or services.
- Monitors `TrustedInstaller` (Windows Modules Installer) status and provides intelligent diagnostic advice.

### 7. 🔄 One-Click Safe Restore
- Whenever you need official security patches or feature updates, simply click **"恢復更新 (Restore Update)"** to remove Hosts blocking, restore default service startup types (Manual/Automatic), and unhide power menu options.

### 8. 🪶 Ultra-Lightweight Native Rust Executable
- Built with Rust: zero bloated runtimes, minimal RAM and CPU footprint.
- Software rendering mode forced (`SLINT_BACKEND=software`) for maximum stability on older hardware or WinPE environments without GPU drivers.

---

## 📸 Screenshots

<div align="center">
  <img src="../../images/應用程式執行畫面.png" alt="Stop Windows Update Tool UI" width="720" />
</div>

---

## 📦 Download & Usage

### 📥 Download
1. Head over to the [Releases Page](https://github.com/robert820/stop-windows-update-tool/releases) to download the latest binary.
2. The application is a **single portable standalone executable** with zero external dependencies.

### 🚀 Usage Guide
1. Run the application as **Administrator** (required for Windows Services and Hosts file modification).
2. The dashboard displays the real-time status of Windows Update, Delivery Optimization, BITS, Update Orchestrator, and Hosts blocking.
3. **To Disable Updates**:
   - Click **「停止更新 (Stop Update)」**. The tool will block domains, disable services, purge caches, remove shutdown tags, and revert pending staged actions.
   - **Restart your computer** when finished to enjoy a completely quiet and uninterrupted system.
4. **To Restore Updates**:
   - Click **「恢復更新 (Restore Update)」**. The tool will clear hosts rules and restore default service configurations.
   - **Restart your computer** to resume official updates through Windows Update settings.

---

## 🖥️ System Compatibility & Requirements

- **Operating System**: Windows 11 / 10 / 8.1 / 8 / 7 (SP1) and Windows PE maintenance environments
- **Architecture**: 64-bit (x64) and 32-bit (x86)
- **Permissions**: Requires Administrator Privileges
- **Runtimes**: Standalone executable; no .NET Framework or VC++ Redistributable required.

---

## ❓ Frequently Asked Questions (FAQ)

<details>
<summary><b>Q1: Is this tool completely free? Can computer repair shops use it?</b></summary>
A: Yes! It is 100% free for personal, corporate, and professional computer repair use. Technicians are welcome to include it on maintenance USB drives. However, selling, leasing, or bundling it with paid products for profit is strictly prohibited.
</details>

<details>
<summary><b>Q2: Why do some antivirus engines trigger a false positive?</b></summary>
A: This tool directly modifies system service startup configurations and the hosts file via native Windows APIs. Some heuristic engines may flag this behavior. It contains zero adware, spyware, or malicious code.
</details>

<details>
<summary><b>Q3: Why does the power menu still show "Update and shut down" after disabling?</b></summary>
A: If Windows had already staged an update prior to using this tool, the system requires one reboot to process the DISM reversion and wipe the reboot markers. Reboot once, and the phantom buttons will disappear.
</details>

<details>
<summary><b>Q4: Does this tool need to stay running in the background?</b></summary>
A: No! It is a one-time configuration utility. Once applied and rebooted, all changes persist directly in the Windows registry and system files. No background daemon is required.
</details>

---

## 💬 Support & Feedback

- 🐛 **Bug Reports & Feature Requests**: Please submit via [GitHub Issues](https://github.com/robert820/stop-windows-update-tool/issues).
- 🌐 **Official Website**: [https://blog.dei3c.com](https://blog.dei3c.com)
- 📧 **Technical Inquiries**: Reach out through our official website.

---

## 📄 License

This software is released under the **Proprietary Freeware EULA**. For complete terms, conditions, and disclaimers, please refer to the [LICENSE](../../LICENSE) file.
