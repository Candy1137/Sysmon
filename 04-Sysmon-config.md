# 🛠️ Sysmon Configuration

## Why Config Files Matter

Without a config file, Sysmon either:
- Logs **too much** (noise overload), or
- Logs **too little** (misses threats)

A good config tells Sysmon **what to capture and what to ignore**.

---

## Config File Structure

Sysmon configs are written in **XML**. Basic structure:

```xml
<Sysmon schemaversion="4.90">
  <HashAlgorithms>md5,sha256</HashAlgorithms>
  <EventFiltering>

    <!-- Log all process creations -->
    <ProcessCreate onmatch="exclude">
    </ProcessCreate>

    <!-- Log network connections, excluding common noise -->
    <NetworkConnect onmatch="exclude">
      <Image condition="is">C:\Windows\System32\svchost.exe</Image>
    </NetworkConnect>

  </EventFiltering>
</Sysmon>
```

---

## Key Concepts

### `onmatch="include"` vs `onmatch="exclude"`

| Mode | Behavior |
|---|---|
| `include` | Only log events that **match** the rules |
| `exclude` | Log **everything except** what matches the rules |

**Tip:** `exclude` is generally safer for beginners — you won't miss things accidentally.

---

### Filter Conditions

| Condition | Meaning |
|---|---|
| `is` | Exact match |
| `contains` | String is anywhere in value |
| `begin with` | Value starts with string |
| `end with` | Value ends with string |
| `image` | Matches the process image path |

---

## Recommended Community Configs

Don't start from scratch — use battle-tested configs:

| Config | Link | Best For |
|---|---|---|
| SwiftOnSecurity | https://github.com/SwiftOnSecurity/sysmon-config | General use, beginners |
| Olaf Hartong (modular) | https://github.com/olafhartong/sysmon-modular | Advanced, customizable |
| Neo23x0 | https://github.com/Neo23x0/sysmon-config | Threat hunting focus |

---

## Loading / Updating a Config

```cmd
# Install with config
Sysmon64.exe -i config.xml

# Update running config (no restart needed)
Sysmon64.exe -c config.xml

# Check current config
Sysmon64.exe -s
```

---

## 💡 Beginner Tips

- Always test configs in a **lab/VM** before production
- Start with SwiftOnSecurity's config — it's well-maintained
- Add exclusions gradually to reduce noise
- Comment your rules using `<!-- your comment here -->`

---

➡️ Next: [Use Cases & Detection Scenarios](../05-use-cases/detection-scenarios.md)
