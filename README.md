# Windows Driver Updater v3.1
[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![PowerShell](https://img.shields.io/badge/PowerShell-%235391FE.svg?style=flat&logo=powershell&logoColor=white)](https://github.com/PowerShell/PowerShell)
[![Windows](https://img.shields.io/badge/Windows-0078D6?style=flat&logo=windows&logoColor=white)](https://www.microsoft.com/windows)

A PowerShell GUI tool to check, download, and install Windows driver updates with logging, filtering, scheduling, and silent automation support.

![Driver Updater Screenshot](https://raw.githubusercontent.com/CHXRITH/DriverUpdate/main/screenshot.png)

## Features

- Modern WinForms UI with dark/light theme
- Multi-language interface (`en`, `es`, `fr`, `de`, `pt`, `it`)
- **New in v3.1:** guided **Update Wizard** (step-by-step flow)
- **New in v3.1:** dedicated **Install Updates** action for driver updates
- Driver update check with manufacturer/class filters
- Driver backup and install-from-folder (`.inf`) support
- Update history and per-task log files
- Proxy settings and persistent app settings
- Scheduled **auto-install** task support
- Cooperative cancel with temporary file cleanup

## Requirements

- Windows 10 or Windows 11
- PowerShell 5.1+
- Administrator privileges
- Internet connection for update checks/downloads

## Run

Run one of the scripts as Administrator:

```powershell
powershell -ExecutionPolicy Bypass -File .\DriveUpdateV3.1.ps1
```

Legacy script still available:

```powershell
powershell -ExecutionPolicy Bypass -File .\DriveUpdateV3.ps1
```

## v3.1 Workflow

1. Open the app as Administrator
2. Run **Update Wizard** (`F5`) for guided update flow
3. Or use:
   - **Check Driver Updates** (`F6`)
   - **Install Updates** (`F8`)
   - **Scan Installed Drivers** (`F7`)
4. Use **Tools** for restore point, filters, schedule, and history
5. Check logs in `Documents\The CHARITH_DriverUpdater`

## Silent Mode

General format:

```powershell
.\DriveUpdateV3.1.ps1 -Silent -Task "<TaskName>"
```

Available tasks:

- `WindowsUpdate`
- `CheckDriverUpdates`
- `InstallDriverUpdates` (new in v3.1)
- `ScanDrivers`

Examples:

```powershell
.\DriveUpdateV3.1.ps1 -Silent -Task "CheckDriverUpdates"
.\DriveUpdateV3.1.ps1 -Silent -Task "InstallDriverUpdates"
.\DriveUpdateV3.1.ps1 -Silent -Task "ScanDrivers"
```

Optional filter/proxy parameters:

```powershell
.\DriveUpdateV3.1.ps1 -Silent -Task "InstallDriverUpdates" -FilterManufacturer "Intel" -FilterClass "Display" -ProxyAddress "http://proxy:8080"
```

## Scheduled Auto-Install

The schedule feature now creates an automatic driver install task (silent mode with `InstallDriverUpdates`) at the selected frequency and time.

## Version History

- **v3.1**
  - Added Update Wizard flow
  - Added Install Updates action (GUI + silent mode)
  - Added cache reuse for recent update checks before install
  - Improved cancellation with cancel token and temp cleanup
  - Updated schedule behavior to auto-install driver updates
- **v3.0**
  - Added multi-language support
  - Added settings, filters, history, and proxy support
  - Added backup/install-from-folder and restore point actions

## License

This project is licensed under the MIT License. See `LICENSE` for details.
