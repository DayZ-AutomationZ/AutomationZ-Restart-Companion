# AutomationZ Restart Delay Companion v0.2.7

## Fix
Auto-start crash fixed by making **all UI updates thread-safe** (monitor thread never touches tkinter).

## If you are stuck in a crash loop
Open `app/config.json` and set:
`"auto_start": false`
(or delete `app/config.json` and the tool will recreate it)

## Run
- Windows: double click `windows_run.bat`
- Linux/macOS: `bash linux_mac_run.sh`
