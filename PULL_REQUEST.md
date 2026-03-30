# Pull Request: Driver Updater v3.1 (Update from v3.0)

## Summary
This PR contains only the delta from `DriveUpdateV3.ps1` (v3.0) to `DriveUpdateV3.1.ps1` (v3.1), including the new update/install workflow and related documentation/assets updates.

## Changes from v3.0 to v3.1

### 1) New update workflow in GUI
- Added **Update Wizard** action (`F5`) with step-by-step flow:
  - Check updates
  - Optional backup
  - Optional download
  - Optional install
- Added dedicated **Install Updates** menu action (`F8`) for direct driver update installation.
- Toolbar was simplified to focus on the main v3.1 workflow buttons.

### 2) New silent-mode task
- Added silent task: `InstallDriverUpdates`
- Silent mode now supports:
  - `WindowsUpdate`
  - `CheckDriverUpdates`
  - `InstallDriverUpdates` (new)
  - `ScanDrivers`

### 3) Scheduling behavior updated
- Scheduled task changed from silent **check-only** to silent **auto-install**:
  - old: `-Task CheckDriverUpdates`
  - new: `-Task InstallDriverUpdates`
- Schedule/history messages updated accordingly (auto-install wording).

### 4) Check/Install coordination improvements
- Added caching of last check results (`LastDriverCheckCache.json`) to reuse recent check data before install.
- Added filter-aware handling (`FilterClass`, `FilterManufacturer`) in install flow as well.

### 5) Cancellation and cleanup improvements
- Added cancel token mechanism for cooperative cancellation during long-running wizard/update operations.
- Added per-task temp path creation and cleanup.
- Improved cleanup on cancel, task completion, and form closing.

### 6) Progress and status improvements
- Added/updated progress heuristics for:
  - Update wizard phases (`[1/5] ... [5/5]`)
  - Download/install phases
- Updated status text to match the new v3.1 update terminology.

### 7) Localization updates
- Added/updated language strings for new actions:
  - `BtnWizard`
  - `BtnInstallUpdates`
- Updated wording for update/schedule labels in existing language packs.

### 8) Version/UI markers
- Version label updated from `v3.0` to `v3.1`.
- Minor theme/toolbar visual consistency adjustments.

### 9) Admin startup behavior (UAC auto-elevation)
- Added startup auto-elevation flow when script is launched without admin rights.
- Script now requests UAC (`RunAs`) and relaunches itself as Administrator.
- Startup parameters are preserved during relaunch (`-Silent`, `-Task`, `-Language`, `-ProxyAddress`, `-FilterClass`, `-FilterManufacturer`).
- Non-admin instance exits after successful handoff; startup aborts if UAC is declined.

## Files in this PR
- `DriveUpdateV3.1.ps1` (new)
- `README.md` (updated for v3.1 usage and features)
- `screenshot_v3.1.png` (new screenshot asset)

## Testing Focus (v3.1 delta)
- Run Update Wizard and verify step toggles and completion path.
- Verify `Install Updates` action installs available driver updates.
- Verify silent mode:
  - `.\DriveUpdateV3.1.ps1 -Silent -Task "InstallDriverUpdates"`
- Verify schedule creates an auto-install task (not check-only).
- Verify cancel behavior removes temp artifacts and stops running job safely.
- Start script without admin rights and verify UAC relaunch behavior.

