# Roach Modbus Tool

**Poll devices. Simulate slaves. Script the whole test.**

A desktop toolkit for engineers working with **Modbus TCP** and **Modbus RTU**. Poll a device as the master, simulate slaves before the hardware arrives, and turn repeated read/write checks into automated PASS/FAIL runs — in one app.

[![Latest release](https://img.shields.io/github/v/release/EricRoach9402/Public_Roach_Modbus_tool)](https://github.com/EricRoach9402/Public_Roach_Modbus_tool/releases/latest)
[![Download for Windows or Linux](https://img.shields.io/badge/download-Windows%20%7C%20Linux-0f766e)](https://mrroach.com/modbus/download)
[![Docs](https://img.shields.io/badge/docs-mrroach.com-334155)](https://mrroach.com/modbus/docs/)

[Official site](https://mrroach.com/modbus/) · [Download the 30-day trial](https://mrroach.com/modbus/download) · [Documentation](https://mrroach.com/modbus/docs/) · [Buy a license — US$79, one-time](https://buy.polar.sh/polar_cl_qHWQnKGI7f9rHowIymwAyNfayRNJO08c4vZ0r36hOAa) · [繁體中文說明](#繁體中文)

![Roach Modbus Tool in Poll mode](https://mrroach.com/modbus/assets/screenshots/poll.png)

<p align="center">
  <img src="https://mrroach.com/modbus/assets/screenshots/slave.png" alt="Slave mode — simulated Modbus device" width="48%">
  &nbsp;
  <img src="https://mrroach.com/modbus/assets/screenshots/script.png" alt="Script mode — automated test run" width="48%">
</p>

This repository hosts the **official Windows and Linux builds** (see [Releases](https://github.com/EricRoach9402/Public_Roach_Modbus_tool/releases)). It is not the application source tree.

## Features

**Poll, Slave, and Script live in the same app.** Switch mode as the job changes. One window cannot run Poll and Slave at the same time; open a second window if you need both (for example, Slave simulating a device while Poll or Script talks to it).

### Poll — read registers as values you understand

Connect as a **Modbus master** over TCP or RTU. Name each point, choose a format and a scale or value map, and the Engineering column can show `24.6 °C` instead of `246`, with the raw value beside it.

- Coils, discrete inputs, holding registers, and input registers (function codes 01, 02, 03, 04, 05, 06, 15, 16)
- Signed / unsigned, hex, binary, 32-bit long and float, 64-bit double, with selectable byte order
- Auto poll on an interval, plus manual read (F5) and write (F6)
- Several devices and several Slave IDs in one project (for example a TCP gateway with devices behind it)
- Live communication log with raw TX/RX frames in hex
- Projects saved as `.mbproj`

### Slave — test the master before the hardware arrives

Run a **local Modbus slave** with your own register map. Point a PLC, HMI, gateway, or another copy of this tool at it.

- TCP listen address under your control (`127.0.0.1` on this PC only, a specific adapter, or all interfaces) or RTU on a serial port
- Several simulated devices and Slave IDs at once, including a gateway-style layout (one listener, different unit IDs)
- Watch which addresses the master reads and writes (last access and count)
- Save the setup as a `.mbslave` project and reopen it for the next test

### Script — turn a checklist into a test run

Build steps that read, write, wait, compare, and branch. Rerun the same cases after a firmware change and export the result.

- PASS / FAIL (and related) verdicts against expected values or ranges
- Flow control: If / Else, While, Repeat, subroutines, End Case / End Round
- Two channels, A and B, for gateway tests (write on one side, read back on the other)
- Scripts saved as JSON you can share
- Excel or CSV reports
- Unattended / CI runs: `--run-script`, optional `--report`, `--loops`, `--case`, and `--log`, with an exit code (0 = PASS)

Sample scripts ship in the `scripts` folder of the Windows zip. Guides, a full command reference, worked examples, and a one-day training course are in the [documentation](https://mrroach.com/modbus/docs/).

## Download

The latest official build is on the [latest GitHub release](https://github.com/EricRoach9402/Public_Roach_Modbus_tool/releases/latest) and on the [download page](https://mrroach.com/modbus/download).

As of this draft (26 November 2026, Asia/Taipei), the current release is **[v1.3.4](https://github.com/EricRoach9402/Public_Roach_Modbus_tool/releases/tag/v1.3.4)**. Prefer the `latest` links below so they stay current.

| Platform | File | Link |
|---|---|---|
| Windows 10 / 11 (x64) | Portable zip (includes sample scripts) | [RoachModbusTool-windows-x64.zip](https://github.com/EricRoach9402/Public_Roach_Modbus_tool/releases/latest/download/RoachModbusTool-windows-x64.zip) |
| Windows 10 / 11 (x64) | Single `.exe` (same build) | [RoachModbusTool.exe](https://github.com/EricRoach9402/Public_Roach_Modbus_tool/releases/latest/download/RoachModbusTool.exe) |
| Linux (x86_64) | AppImage | [RoachModbusTool-x86_64.AppImage](https://github.com/EricRoach9402/Public_Roach_Modbus_tool/releases/latest/download/RoachModbusTool-x86_64.AppImage) |

SHA-256 checksums for each file are listed on the [release page](https://github.com/EricRoach9402/Public_Roach_Modbus_tool/releases/latest). Compare them before you run a new build:

```powershell
Get-FileHash .\RoachModbusTool.exe
Get-FileHash .\RoachModbusTool-windows-x64.zip
```

```bash
sha256sum RoachModbusTool-x86_64.AppImage
```

**Windows SmartScreen:** current builds are not code-signed yet. Your browser may ask you to keep the file anyway, and Windows may say “Windows protected your PC”. Choose *More info*, then *Run anyway*. Download only from [mrroach.com/modbus](https://mrroach.com/modbus/) or from this repository’s releases.

## Quick start

### Windows

1. Download `RoachModbusTool-windows-x64.zip` and unzip it to any folder (for example `D:\Tools\RoachModbusTool`).
2. Run `RoachModbusTool.exe`. There is nothing else to install.
3. The 30-day full trial starts on first launch. No account and no credit card.

### Linux (x86_64)

```bash
chmod +x RoachModbusTool-x86_64.AppImage
./RoachModbusTool-x86_64.AppImage
```

To use an RTU serial port, add your account to the `dialout` group, then log out and back in:

```bash
sudo usermod -aG dialout $USER
```

If the AppImage reports that FUSE is missing (common on Ubuntu 22.04+), install `libfuse2` (Ubuntu 22.04) or `libfuse2t64` (Ubuntu 24.04), or run `./RoachModbusTool-x86_64.AppImage --appimage-extract-and-run`. See [Troubleshooting](https://mrroach.com/modbus/docs/troubleshooting).

### First exchange (no hardware)

You can practise with two windows of the same app:

1. In the first window, click **Slave**, then **Listen**. It waits on `127.0.0.1:502` and serves a small holding-register table.
2. In the second window (it opens in **Poll**), click **Connect**. Auto poll starts, quality should show Good, and the log shows the raw frames.

Then follow [Getting started](https://mrroach.com/modbus/docs/getting-started) and the [Poll](https://mrroach.com/modbus/docs/poll/), [Slave](https://mrroach.com/modbus/docs/slave/), and [Script](https://mrroach.com/modbus/docs/script/tutorial) guides. Sample projects used on the website can also be opened from the [download page](https://mrroach.com/modbus/download).

## Trial and license

- **30-day full trial** — Poll, Slave, and Script are all unlocked. No account and no credit card.
- When the trial ends, features lock until you enter a license key.
- **US$79 once**, no subscription and no feature tiers. Pay through [Polar](https://buy.polar.sh/polar_cl_qHWQnKGI7f9rHowIymwAyNfayRNJO08c4vZ0r36hOAa), or choose **Help → License → Buy License…** in the app, then **Enter License…** to activate.
- **Single-user license.** The licensed person may activate it on up to **3 of their own computers**. It is not to be shared with other people. To move to a new computer, deactivate an old one (**Help → License → Remove License…**), or contact [mr.roach.company@gmail.com](mailto:mr.roach.company@gmail.com) to reset activations.
- The license does not expire by calendar date. After a successful online check, the app can work offline for 14 days. License scope, updates, and commercial use are set out in the [Terms of Use](https://mrroach.com/modbus/terms).

## System requirements

| | |
|---|---|
| Windows | Windows 10 or 11, 64-bit (x64). Portable `.exe`, no installer. |
| Linux | x86_64 AppImage, tested on Ubuntu and Debian. A graphical desktop is needed for the windowed app; `--run-script` does not need one. |
| Protocols | Modbus TCP and Modbus RTU (serial). |

macOS and ARM builds are not offered. Minimum RAM, CPU, and disk size are not specified in the public docs.

Each window supports up to 32 connections (32 Poll devices or 32 Slave listeners).

## Documentation

- [Documentation home](https://mrroach.com/modbus/docs/)
- [Getting started](https://mrroach.com/modbus/docs/getting-started) — install, license, first connection
- [Poll guide](https://mrroach.com/modbus/docs/poll/)
- [Slave guide](https://mrroach.com/modbus/docs/slave/)
- [Script tutorial](https://mrroach.com/modbus/docs/script/tutorial) · [Concepts](https://mrroach.com/modbus/docs/script/concepts) · [Command reference](https://mrroach.com/modbus/docs/script/reference/) · [Examples](https://mrroach.com/modbus/docs/script/examples/)
- [Command-line runs](https://mrroach.com/modbus/docs/script/command-line)
- [Troubleshooting](https://mrroach.com/modbus/docs/troubleshooting)
- [Training course](https://mrroach.com/modbus/docs/training/)
- [繁體中文文件](https://mrroach.com/modbus/docs/zh/)

## Support

- [Feedback](https://mrroach.com/modbus/feedback) — bug reports, feature requests, and licensing questions. Please include the app version (in the window title), your OS, and steps to reproduce.
- Email: [mr.roach.company@gmail.com](mailto:mr.roach.company@gmail.com)

## License

Roach Modbus Tool is commercial software by Mr.Roach, not an open-source project. Downloading or using the software means you agree to the [Terms of Use](https://mrroach.com/modbus/terms), [Privacy Policy](https://mrroach.com/modbus/privacy), and [Disclaimers](https://mrroach.com/modbus/disclaimer).

The trial is for evaluation. A paid license is a personal, single-user license for internal business or personal use, with the limits described in the Terms.

---

## 繁體中文

**Roach Modbus Tool** 是給 Modbus TCP／RTU 工程師的桌面工具：用 **Poll** 當主站讀寫設備，並把暫存器顯示成 °C、Hz 這類工程值；用 **Slave** 在本機模擬從站，硬體還沒到也能先測 PLC／HMI／閘道；用 **Script** 把手動檢查編成可重跑的自動測試，結果可匯出 Excel，也可在治具或 CI 用命令列執行。

- 官網：https://mrroach.com/modbus/
- 繁體中文文件：https://mrroach.com/modbus/docs/zh/
- 下載（30 天完整功能試用，不需帳號或信用卡）：https://mrroach.com/modbus/download
- 購買授權（US$79 一次買斷，無訂閱；單人授權最多 3 台自己的電腦）：https://buy.polar.sh/polar_cl_qHWQnKGI7f9rHowIymwAyNfayRNJO08c4vZ0r36hOAa
- 支援信箱：mr.roach.company@gmail.com

本倉庫只提供官方 Windows／Linux 建置檔與發行頁，**不含原始碼**。目前建置尚未程式碼簽章，Windows 可能出現「不明的發行者」或 SmartScreen 提示，請只從官網或本倉庫的 Releases 下載。系統需求與授權範圍以[英文說明](#system-requirements)與[使用條款](https://mrroach.com/modbus/terms)為準。
