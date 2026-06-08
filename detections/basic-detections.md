# Basic Detection Searches

This document contains foundational Splunk searches used within the Home SOC Lab to identify and investigate common security events.

---

# Process Creation Monitoring

## Description

Monitor process creation activity using Sysmon Event ID 1.

## Search

```spl
index=* EventCode=1
| table _time host Image CommandLine ParentImage User
```

## Use Cases

- Process execution monitoring
- Parent-child process analysis
- Suspicious process identification
- Threat hunting

---

# PowerShell Execution Detection

## Description

Identify PowerShell activity across monitored hosts.

## Search

```spl
index=* EventCode=1 Image="*powershell.exe"
| table _time host User CommandLine ParentImage
```

## Use Cases

- PowerShell monitoring
- Script execution analysis
- Living-off-the-land detection

---

# Command Prompt Execution Detection

## Description

Identify Command Prompt activity.

## Search

```spl
index=* EventCode=1 Image="*cmd.exe"
| table _time host User CommandLine ParentImage
```

## Use Cases

- Interactive shell monitoring
- Suspicious command execution
- User activity analysis

---

# Failed Logon Detection

## Description

Identify failed authentication attempts.

## Event ID

4625

## Search

```spl
index=* EventCode=4625
| table _time host Account_Name Source_Network_Address Logon_Type
```

## Use Cases

- Brute force detection
- Unauthorized access attempts
- Password spraying investigations

---

# Successful Logon Detection

## Description

Monitor successful authentication activity.

## Event ID

4624

## Search

```spl
index=* EventCode=4624
| table _time host Account_Name Logon_Type Workstation_Name
```

## Use Cases

- User activity monitoring
- Authentication investigations
- Account tracking

---

# New Service Installation Detection

## Description

Detect newly installed services.

## Event ID

7045

## Search

```spl
index=* EventCode=7045
| table _time host Service_Name Service_File_Name Account_Name
```

## Use Cases

- Persistence detection
- Malware investigations
- Unauthorized software installations

---

# Account Creation Detection

## Description

Identify newly created user accounts.

## Event ID

4720

## Search

```spl
index=* EventCode=4720
| table _time host Target_Account_Name Subject_Account_Name
```

## Use Cases

- Privilege escalation investigations
- Unauthorized account creation
- Insider threat monitoring

---

# Account Deletion Detection

## Description

Identify deleted user accounts.

## Event ID

4726

## Search

```spl
index=* EventCode=4726
| table _time host Target_Account_Name Subject_Account_Name
```

## Use Cases

- Account lifecycle monitoring
- Insider threat investigations
- Administrative auditing

---

# DNS Activity Monitoring

## Description

Monitor DNS activity from the domain controller.

## Search

```spl
index=* host=DC01 source="WinEventLog:DNS Server"
```

## Use Cases

- DNS investigations
- Domain monitoring
- Threat hunting

---

# Top Executed Processes

## Description

Identify the most commonly executed processes.

## Search

```spl
index=* EventCode=1
| top Image
```

## Use Cases

- Baseline development
- Process monitoring
- Threat hunting

---

# Event Volume by Host

## Description

Monitor event volume across hosts.

## Search

```spl
index=* (host=WIN10-1 OR host=DC01)
| timechart count by host
```

## Use Cases

- Host activity monitoring
- Event spike identification
- SIEM health validation

---

# Future Detection Opportunities

The following detections are planned for future implementation:

- Nmap Scan Detection
- PowerShell Encoded Command Detection
- Suspicious Parent-Child Process Detection
- Brute Force Alerting
- Kerberoasting Detection
- Pass-the-Hash Detection
- MITRE ATT&CK Mapping
- Scheduled Alerting
- Custom Splunk Dashboards
