# 🔢 Key Sysmon Event IDs

Sysmon assigns a unique **Event ID** to each type of activity it monitors. These are the most important ones every beginner should know.

---

## Quick Reference Table

| Event ID | Name | Why It Matters |
|---|---|---|
| 1 | Process Creation | Most important — shows every process launched |
| 2 | File Creation Time Changed | Timestomping detection |
| 3 | Network Connection | Outbound/inbound connections by process |
| 5 | Process Terminated | When a process ends |
| 6 | Driver Loaded | Kernel driver loads (rootkit detection) |
| 7 | Image Loaded | DLL loads into a process |
| 8 | CreateRemoteThread | Thread injection (malware technique) |
| 10 | ProcessAccess | A process accessing another (credential theft) |
| 11 | FileCreate | New file written to disk |
| 12/13 | Registry Events | Registry key create/modify |
| 15 | FileCreateStreamHash | Alternate Data Streams (ADS) |
| 22 | DNS Query | Domain lookups made by a process |
| 23 | File Delete | File deletion events |

---

## Deep Dive — Most Critical Event IDs

### 🔴 Event ID 1 — Process Creation
The most powerful event. Captures:
- Process name & full path
- Command-line arguments
- Parent process (who spawned it)
- User account
- File hash (MD5/SHA256)

**Example use:** Detect `cmd.exe` spawned by `word.exe` → likely macro malware.

---

### 🔴 Event ID 3 — Network Connection
Logs outbound TCP/UDP connections. Captures:
- Source & destination IP
- Port numbers
- Process that made the connection

**Example use:** Detect `powershell.exe` connecting to an unknown IP on port 4444 → possible reverse shell.

---

### 🔴 Event ID 8 — CreateRemoteThread
Logs when a process creates a thread in another process. This is a classic technique used by:
- Process injection malware
- Ransomware
- RATs (Remote Access Trojans)

---

### 🔴 Event ID 10 — ProcessAccess
Logs when one process opens/reads another process's memory. Commonly used in:
- **LSASS credential dumping** (e.g., Mimikatz)
- `sekurlsa::logonpasswords` access patterns

---

### 🔴 Event ID 22 — DNS Query
Logs every DNS lookup. Useful for detecting:
- **C2 communication** (beaconing to strange domains)
- **DNS tunneling**
- Malware phoning home

---

## 💡 Beginner Tip

Start by focusing on:
> **Event IDs 1, 3, 8, 10, and 22** — these cover the most common attack techniques.

---

➡️ Next: [Configuration Guide](../04-configuration/sysmon-config.md)
