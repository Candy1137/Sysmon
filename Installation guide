# ⚙️ Installing Sysmon

## Step 1 — Download Sysmon

1. Go to the official page: https://learn.microsoft.com/en-us/sysinternals/downloads/sysmon
2. Download **Sysmon.zip** and extract it

You'll get:
- `Sysmon.exe` (32-bit)
- `Sysmon64.exe` (64-bit) ← use this on modern systems
- `Eula.txt`

---

## Step 2 — Install with Default Config

Open **Command Prompt as Administrator** and run:

```cmd
Sysmon64.exe -accepteula -i
```

This installs Sysmon with **minimal default logging**.

---

## Step 3 — Install with a Config File (Recommended)

A config file controls **what Sysmon logs and what it ignores**. Without one, you'll get too much noise.

Using the popular SwiftOnSecurity config:

```cmd
Sysmon64.exe -accepteula -i sysmonconfig.xml
```

Download the config from:
👉 https://github.com/SwiftOnSecurity/sysmon-config

---

## Useful Commands

| Command | Description |
|---|---|
| `Sysmon64.exe -i config.xml` | Install with config |
| `Sysmon64.exe -c config.xml` | Update/reload config |
| `Sysmon64.exe -u` | Uninstall Sysmon |
| `Sysmon64.exe -s` | Print current schema |

---

## Step 4 — Verify It's Running

Check if Sysmon service is active:

```cmd
sc query sysmon64
```

Or check in **Services** (`services.msc`) — look for `Sysmon64`.

---

## Step 5 — View Logs

Open **Event Viewer**:
```
Event Viewer → Applications and Services Logs → Microsoft → Windows → Sysmon → Operational
```

---

## ⚠️ Notes

- Always run as **Administrator**
- Sysmon works silently in the background — no GUI
- It survives reboots once installed

---

➡️ Next: [Key Event IDs](../03-event-ids/key-event-ids.md)
