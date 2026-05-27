# 📖 What is Sysmon?

## Overview

**Sysmon** (System Monitor) is a free Windows system service and device driver from **Microsoft Sysinternals**. Once installed, it logs detailed system activity to the **Windows Event Log**, giving security teams deep visibility into what's happening on an endpoint.

---

## Why Sysmon?

Default Windows logging is **limited**. It doesn't capture:
- Which process spawned another process
- Exact command-line arguments used
- Network connections made by a process
- File creation timestamps

Sysmon fills these gaps.

---

## What Does Sysmon Monitor?

| Activity | Description |
|---|---|
| Process Creation | Every new process started, including parent process & command line |
| Network Connections | Outbound/inbound TCP/UDP connections |
| File Creation | New files written to disk |
| Registry Changes | Modifications to registry keys |
| Driver/DLL Loads | Modules loaded into processes |
| Raw Disk Access | Low-level disk reads (used by rootkits) |

---

## Where Does Sysmon Log?

Sysmon writes events to:
```
Applications and Services Logs > Microsoft > Windows > Sysmon > Operational
```
You can view them in **Windows Event Viewer**.

---

## Sysmon vs Default Windows Logging

| Feature | Windows Default | Sysmon |
|---|---|---|
| Process Creation | ✅ Basic | ✅ Detailed (PID, PPID, CLI args, hashes) |
| Network Connections | ❌ | ✅ |
| File Creation Time | ❌ | ✅ |
| DNS Queries | ❌ | ✅ |
| Config Filtering | ❌ | ✅ |

---

## Key Takeaway

> Sysmon doesn't replace Windows Event Logs — it **enhances** them.

---

➡️ Next: [Installation Guide](../02-installation/installation-guide.md)
