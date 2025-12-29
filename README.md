# AutomationZ Restart Delay Companion
[![Automation_Z_Restart_Companion.png](https://i.postimg.cc/yxnvGV6q/Automation_Z_Restart_Companion.png)](https://postimg.cc/5QYBYWFp)
AutomationZ Restart Delay Companion is a lightweight monitoring and restart-control tool designed to **work alongside AutomationZ Mod Update Auto-Deploy**.  
Its primary goal is to **eliminate PBO mismatches, version desyncs, and forced restarts at the wrong time** by introducing a **safe, delayed restart workflow** after mod updates.

This tool was built for DayZ (and similar servers), but the concept is generic and file-based, making it usable for other games and services as well.

---

## Why this tool exists (the problem it fixes)

Server admins commonly face these issues:

- ❌ Mods update on Steam while the server is running
- ❌ Players get kicked with **PBO mismatch / version mismatch**
- ❌ Admins manually babysit restarts after every update

**AutomationZ Restart Delay Companion fixes this by separating concerns:**

- **Mod Update Auto-Deploy** handles *detecting and deploying mods*
- **Restart Delay Companion** handles *when* a restart should happen

No guessing. No racing Steam. No broken servers.

---

## Core concept (simple & reliable)

The Restart Companion **does not touch mods** and **does not deploy files**.

Instead, it:

1. **Monitors a simple marker file, by default automationz_last_deploy.txt (send to the server by Steam-Workshop-Mod-Update-Auto-Deploy after a update or updates are done)**
2. **By reading the file every 30 second the Restart Companion Detects when an update is finished**
3. **The Restart companion Starts a restart with a configurable delay (default in config is 1 minute) i personally set it to 5**
4. **It Executes a restart action when the timer ends, OR if another update is detected resets the timer to what you have set it to, so it wont restart during a update**

This ensures the restart happens **only after everything is fully deployed and stable**.

---

## How it works together with Mod Update Auto-Deploy

### Recommended setup (best practice)

1. **AutomationZ Mod Update Auto-Deploy**
   - Deploys all updated mods
   - After the *entire deploy batch finishes*, it uploads or writes a **marker file**
     - Example:
       ```
       /dayzstandalone/automationz_last_deploy.txt
       ```

2. **AutomationZ Restart Companion**
   - Watches that marker file every 30 seconds (configurable)
   - When the marker timestamp changes:
     - A restart timer starts (for example: 5–10 minutes)
     - If another update happens, the timer resets
   - When the timer expires:
     - Server restart is executed safely (WORKS LOCAL AND WITH FTP)

This turns multiple mod updates into **one clean restart**.

---

## Supported detection modes

The Restart Companion supports:

### 🔍 Detection
- **Local folder monitoring**
- **FTP / FTPS monitoring**
- Detection by:
  - Newest file modification time
  - Dedicated marker file

### ⏱ Restart delay
- Delay is configurable per target
- Timer resets automatically if new updates arrive

---

## Supported restart actions

When the delay expires, the tool can:

- ✅ Execute a **local command**
- ✅ Send a **BattlEye RCON shutdown**
- ⚠️ Fallback to **notify-only mode** if restart fails

If RCON fails, the tool:
- Logs the failure
- Sends a Discord message (optional)
- Falls back to:
RESTART NEEDED now. (Use host panel/app)


---
[![Automation_Z_Restart_Companion_Discord.png](https://i.postimg.cc/1XMJd9mL/Automation_Z_Restart_Companion_Discord.png)](https://postimg.cc/QK9Q9ZWb)
## Discord integration (optional)

Both tools support Discord webhooks.

Restart Companion can send messages for:
- Restart triggered
- Restart succeeded
- Restart failed / fallback used

This gives admins full visibility without babysitting the server.

---

## What this tool deliberately does NOT do

- ❌ It does NOT deploy mods
- ❌ It does NOT modify server files
- ❌ It does NOT force restarts instantly
- ❌ It does NOT assume your server layout

This separation is intentional and is what makes the system safe.

---

## Typical real-world workflow

1. Steam updates one or more mods
2. Mod Update Auto-Deploy detects changes
3. Mods are uploaded or copied
4. Marker file is overwritten after deploy finishes
5. Restart Delay Companion detects marker change
6. Restart delay timer starts
7. Timer expires → server restarts cleanly
8. Players reconnect with matching mods

No PBO errors. No manual restarts. No downtime chaos. (YES REALLY! this years old PAIN fixed) :)

---

## Who this is for

- DayZ server owners
- Modded game server admins
- VPS / dedicated server operators
- Anyone running automated deployments who needs **safe restart timing**

---

## Design philosophy

- File-based logic (host-agnostic)
- No hardcoded paths
- No assumptions about hosting providers
- Simple UI, predictable behavior
- Tools that do **one job well**

---

## Part of the AutomationZ ecosystem

This tool is designed to be used together with:

- **AutomationZ Mod Update Auto-Deploy**
- Other AutomationZ admin tools

Each tool is independent, but stronger together.

---

## Author

Created by **Danny van den Brande**  
Open-source, admin-driven, built from real server experience.

Support development:
- ☕ https://ko-fi.com/dannyvandenbrande
- 🧠 https://github.com/DayZ-AutomationZ
