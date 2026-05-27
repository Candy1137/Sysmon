# 🎯 Use Cases & Detection Scenarios

Sysmon becomes powerful when you know **what to look for**. Here are common attack techniques and how Sysmon helps detect them.

---

## 1. 🐚 Suspicious PowerShell Execution

**Attack:** Attacker runs encoded PowerShell command to download malware.

**What Sysmon Captures:** Event ID 1 (Process Creation)

**Look for:**
```
Image: C:\Windows\System32\WindowsPowerShell\v1.0\powershell.exe
CommandLine: powershell -enc <base64string>
ParentImage: cmd.exe or explorer.exe
```

**Red Flag:** PowerShell with `-enc`, `-nop`, `-w hidden` flags.

---

## 2. 🔑 LSASS Credential Dumping (Mimikatz)

**Attack:** Attacker reads LSASS memory to steal credentials.

**What Sysmon Captures:** Event ID 10 (ProcessAccess)

**Look for:**
```
TargetImage: C:\Windows\System32\lsass.exe
GrantedAccess: 0x1010 or 0x1410
```

**Red Flag:** Any process other than Windows system processes accessing LSASS.

---

## 3. 🌐 Reverse Shell / C2 Beaconing

**Attack:** Malware connects back to attacker's server (Command & Control).

**What Sysmon Captures:** Event ID 3 (Network Connection)

**Look for:**
```
Image: powershell.exe or cmd.exe
DestinationPort: 4444, 1337, 8080, 443 (unusual process)
DestinationIp: unknown/external IP
```

**Red Flag:** `cmd.exe` or `powershell.exe` initiating outbound connections.

---

## 4. 💉 Process Injection

**Attack:** Malware injects code into a legitimate process (e.g., explorer.exe) to hide.

**What Sysmon Captures:** Event ID 8 (CreateRemoteThread)

**Look for:**
```
SourceImage: malware.exe
TargetImage: explorer.exe or svchost.exe
```

**Red Flag:** Unknown process creating threads in trusted Windows processes.

---

## 5. 📄 Malicious Office Macro

**Attack:** Word/Excel file with a macro that spawns a shell.

**What Sysmon Captures:** Event ID 1 (Process Creation)

**Look for:**
```
ParentImage: WINWORD.EXE or EXCEL.EXE
Image: cmd.exe or powershell.exe or wscript.exe
```

**Red Flag:** Office apps should **never** spawn command shells.

---

## 6. 🔍 DNS Tunneling / C2 via DNS

**Attack:** Malware uses DNS queries to communicate with C2 server.

**What Sysmon Captures:** Event ID 22 (DNS Query)

**Look for:**
```
QueryName: verylongrandombsubdomain.suspicious-domain.com
Image: any unexpected process making DNS queries
```

**Red Flag:** Unusually long/random subdomains, high-frequency DNS queries.

---

## 💡 Detection Mindset

> Always ask: **"Is this normal behavior for this process?"**

- `explorer.exe` making network connections? Suspicious.
- `word.exe` spawning `powershell.exe`? Big red flag.
- `svchost.exe` connecting to a foreign IP on port 4444? Investigate immediately.

---

## Helpful Resources for Practice

- [Blue Team Labs Online](https://blueteamlabs.online/) — Free Sysmon-based challenges
- [CyberDefenders](https://cyberdefenders.org/) — DFIR labs with Sysmon logs
- [EVTX Attack Samples](https://github.com/sbousseaden/EVTX-ATTACK-SAMPLES) — Real attack log samples

---

➡️ Next: [Resources & References](../resources/references.md)
