# Driver Updater v3.1

This README documents only functionality present in `DriveUpdateV3.1.ps1`.

## Requirements

- Windows 10/11
- PowerShell 5.1 or newer
- UAC permission to elevate when prompted

## Start

```powershell
powershell -ExecutionPolicy Bypass -File .\DriveUpdateV3.1.ps1
```

If started without admin rights, the script now triggers a UAC prompt and relaunches itself as Administrator with the same startup parameters.

## Script Parameters

- `-Silent` (switch): run without GUI and execute one task
- `-Task` (string): silent task name
- `-Language` (string): `en`, `es`, `fr`, `de`, `pt`, `it`
- `-ProxyAddress` (string): proxy URL
- `-FilterClass` (string): driver class filter
- `-FilterManufacturer` (string): manufacturer filter

## Startup Elevation Behavior

- Checks for Administrator rights at startup.
- If not elevated, relaunches itself with `powershell.exe -Verb RunAs`.
- Preserves provided startup arguments (for example: `-Silent`, `-Task`, `-Language`, `-ProxyAddress`, `-FilterClass`, `-FilterManufacturer`).
- Original non-admin process exits after handing off to elevated process.
- If UAC is canceled, startup is aborted.

## Implemented GUI Functionality

- Multi-language UI (`en`, `es`, `fr`, `de`, `pt`, `it`)
- Dark/Light theme toggle
- Check driver updates
- Install available driver updates
- Scan installed drivers and export CSV
- Backup installed drivers (`dism /export-driver`)
- Install drivers from folder (`pnputil` with `.inf`)
- Update Wizard with selectable steps:
  - check updates
  - backup drivers
  - download updates
  - install updates
- Cancel running task
- Open log folder
- Create system restore point
- Configure proxy settings
- Configure class/manufacturer filters
- View update history
- Schedule automatic silent install task (Daily/Weekly/Monthly)

## Silent Mode (Implemented Tasks)

```powershell
.\DriveUpdateV3.1.ps1 -Silent -Task "<TaskName>"
```

Valid task names:

- `WindowsUpdate`
- `CheckDriverUpdates`
- `InstallDriverUpdates`
- `ScanDrivers`

Examples:

```powershell
.\DriveUpdateV3.1.ps1 -Silent -Task "CheckDriverUpdates"
.\DriveUpdateV3.1.ps1 -Silent -Task "InstallDriverUpdates"
.\DriveUpdateV3.1.ps1 -Silent -Task "ScanDrivers"
```

Silent mode can be combined with:

```powershell
.\DriveUpdateV3.1.ps1 -Silent -Task "InstallDriverUpdates" -FilterManufacturer "Intel" -FilterClass "Display" -ProxyAddress "http://proxy:8080"
```

## Data and Logs

The script stores files in:

- `%USERPROFILE%\Documents\The CHARITH_DriverUpdater`

Files used by the script:

- `Settings.json`
- `UpdateHistory.json`
- task log files (`*.log`)
- scan export files (`InstalledDrivers_*.csv`)
- temporary task folder under `Temp\` (created/cleaned during tasks)

## License

MIT (`LICENSE`)

---

Made with 💜 by TheCHARITH
Organization: Simplest Circuits
