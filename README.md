# Configuring-System-Monitoring

# 🖥️ Assisted Lab: Configuring System Monitoring

## 📌 Overview

This lab demonstrates how to configure **centralized log management** using **Windows Event Forwarding (WEF)**. A Windows Server 2019 domain controller (DC10) is configured as an **Event Collector**, while a Windows Server 2016 system (MS10) acts as the **Event Source**.

By creating an Event Viewer subscription, security administrators can collect logs from multiple systems into a single location, simplifying monitoring, investigations, and incident response.

---

## 🎯 Objectives

This lab aligns with the following **CompTIA Security+ (SY0-701)** objectives:

- **4.1** – Apply common security techniques to computing resources
- **4.4** – Explain security alerting and monitoring concepts and tools
- **4.9** – Use data sources to support an investigation

---

# 🖥️ Lab Environment

| System | Purpose |
|---------|----------|
| **DC10** | Windows Server 2019 Event Collector |
| **MS10** | Windows Server 2016 Event Source |

---

# 🛠️ Technologies Used

- Windows Event Forwarding (WEF)
- Windows Event Collector (WEC)
- Windows Event Viewer
- Windows PowerShell
- WinRM
- Windows Defender Firewall
- Group Policy (GPO)
- Event Viewer Subscriptions
- Windows Security Logs
- Centralized Logging

---

# 📚 Skills Learned

- Configure Windows Event Forwarding (WEF)
- Configure Windows Event Collector (WEC)
- Modify Group Policy using PowerShell
- Configure WinRM
- Configure Windows Firewall for remote logging
- Configure Event Viewer subscriptions
- Collect logs from remote systems
- Verify event forwarding
- Implement centralized logging
- Monitor remote Windows systems

---

# 📖 Scenario

Structureality Inc. wants to centralize Windows event logs to improve security monitoring and simplify incident investigations.

Instead of reviewing logs individually on each server, all important Windows events will be forwarded to a central server for easier monitoring and analysis.

---

# 🔧 Part 1 – Configure the Event Collector

The Domain Controller (**DC10**) was configured as the **Windows Event Collector**.

Tasks completed:

- Modified Group Policy
- Configured WinRM listener
- Enabled Windows Event Collector service
- Verified collector configuration

PowerShell was used to:

- Import Group Policy module
- Configure WinRM IPv4 listener
- Update Group Policy
- Refresh policies

The Windows Event Collector service was initialized using:

```powershell
wecutil qc
```

---

# 🌐 Part 2 – Configure the Event Source

The source server (**MS10**) was prepared for remote event forwarding.

Configuration included:

- Restarting the system
- Enabling WinRM
- Enabling Remote Event Log Management
- Enabling Remote Event Monitor firewall rules

PowerShell commands enabled:

- Remote Event Log Management
- Remote Event Monitor

WinRM was verified using:

```powershell
winrm quickconfig
```

---

# 👥 Part 3 – Configure Event Log Readers

To allow DC10 to retrieve logs from MS10:

- Added **DC10** computer account
- Granted membership in **Event Log Readers**
- Restarted MS10 to apply changes

This allows the collector to remotely read Windows Event Logs.

---

# 📡 Part 4 – Configure Event Viewer Subscription

An Event Viewer Subscription was created on **DC10**.

Configuration included:

- Subscription Name
- Collector-Initiated Subscription
- Remote Computer Selection
- Event Query Filter
- Windows Logs Selection

The subscription was configured to collect:

- Application
- Security
- Setup
- System
- Forwarded Events

from **MS10**.

---

# 🔄 Collector-Initiated Forwarding

This lab used a **Collector-Initiated** subscription.

In this configuration:

- Collector contacts source computers.
- Collector periodically retrieves logs.
- Centralized storage occurs on the collector.

Windows also supports:

- **Source Computer Initiated**

where client computers push events to the collector.

---

# 📥 Forwarded Events

After the subscription became active:

- DC10 began polling MS10.
- Remote events appeared inside:

```
Event Viewer
└── Forwarded Events
```

This log serves as the centralized repository for collected Windows events.

---

# 🔐 Security Benefits

Centralized logging provides several advantages:

- Simplified monitoring
- Faster investigations
- Easier incident response
- Centralized log retention
- Improved forensic analysis
- Reduced administrative effort
- Better compliance reporting
- Improved visibility across systems

---

# 📊 Centralized Logging Workflow

```text
MS10 (Event Source)
        │
        │ WinRM
        ▼
Windows Event Forwarding
        │
        ▼
DC10 (Event Collector)
        │
        ▼
Forwarded Events
        │
        ▼
Security Monitoring
Incident Response
Threat Hunting
```

---

# 📖 Key Takeaways

This lab demonstrated how to deploy **Windows Event Forwarding (WEF)** for centralized log collection.

Using **WinRM**, **Windows Event Collector**, **PowerShell**, **Group Policy**, and **Event Viewer Subscriptions**, logs from remote Windows systems can be automatically collected into a single location for monitoring and security analysis.

Centralized logging improves visibility, supports incident response, and forms a critical component of modern Security Operations Centers (SOCs).

---

# 🏷️ Tags

`CompTIA Security+` `Windows Event Forwarding` `WEF` `Windows Event Collector` `WEC` `Windows Server` `Event Viewer` `PowerShell` `WinRM` `Group Policy` `Centralized Logging` `Windows Security` `SOC Analyst` `Incident Response` `Security Monitoring` `Blue Team` `Cybersecurity Lab`
