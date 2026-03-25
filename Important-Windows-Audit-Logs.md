# Windows SOC Audit Logs

This repository contains guidance, scripts, and examples for enabling **SOC-ready Windows auditing**. The purpose is to ensure that critical security events are logged, monitored, and ingested into SIEM solutions like Microsoft Sentinel for **Advanced Hunting** and alerting.

---

## Overview

Windows provides a comprehensive auditing system to track user activity, process execution, privilege use, and changes to accounts or security policies.  
Proper auditing is essential for:

- Threat detection
- Incident investigation
- Compliance (e.g., NIST CSF, ISO 27001)
- Security monitoring in enterprise environments

This repository focuses on **core audit categories** that are most relevant for SOC operations.

---

## Core Audit Categories

| Category              | Subcategories                                         | Purpose / Use Case |
|-----------------------|------------------------------------------------------|------------------|
| **Logon/Logoff**      | Logon, Logoff, Account Lockout, Special Logon       | Track user activity, failed logins, and suspicious authentication |
| **Detailed Tracking** | Process Creation, Process Termination               | Detect execution of scripts, malware, and lateral movement |
| **Privilege Use**     | Sensitive Privilege Use                              | Monitor privilege escalation attempts and admin actions |
| **Object Access**     | File System, Registry                                | Track modifications to sensitive files and system configuration |
| **Policy Change**     | Audit Policy Change, Authorization Policy Change    | Detect changes to security configurations |
| **Account Management**| User, Computer, Group Management                     | Detect creation, deletion, or modification of accounts |

> These categories are recommended for endpoints that are part of SOC monitoring.

---

## SOC-Ready Audit Script

The following PowerShell script enables auditing for the most important subcategories:

```powershell
# File: Windows-Audit-SOC-Prod.ps1
$Subcategories = @(
    "Logon",
    "Logoff",
    "Account Lockout",
    "Special Logon",
    "Process Creation",
    "Process Termination",
    "Sensitive Privilege Use",
    "File System",
    "Registry"
)

foreach ($sub in $Subcategories) {
    Write-Host "Enabling auditing for $sub..."
    auditpol /set /subcategory:"$sub" /success:enable /failure:enable
}

Write-Host "SOC-ready audit configuration completed successfully."
```
Verify Audit Settings

Check if auditing is enabled for a specific subcategory:

```
auditpol /get /subcategory:"Process Creation"
```
List all available audit subcategories:

```
auditpol /list /subcategory:*
````
This repository is provided as-is for educational and SOC deployment purposes.
Feel free to adapt scripts and queries to your organization’s environment.
