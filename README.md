# 🛡️ Samuel Cesar – Microsoft Sentinel & Defender XDR Walkthrough

My name is **Samuel Cesar**, and I have been studying Cybersecurity for over a year. I use GitHub to publish my studies, providing a structured and clear way to share my learning process. My goal is to explain each stage of cybersecurity in a practical, straightforward manner, including tips and insights from hands-on experience.

---

## 🎓 Certifications & Achievements

- **IEFP – Cybersecurity Specialist Technician (Level 5)**  
- **Blue Team Level 1 (BTL1) – Gold Coin**  
- **Splunk Core Certified Power User**  
- **Microsoft SC-900 (Security, Compliance, and Identity Fundamentals)**  
- **Microsoft AZ-900 (Azure Fundamentals)**  
- **Fortinet Network Security Expert (FCA)**  
- **CCNA (expired)**  
- **Blue Team Labs Online:** [Profile](https://blueteamlabs.online/public/user/6255328b393299c2c9a387)  
- **LinkedIn:** [Profile](https://www.linkedin.com/in/samuel-cesar-9100261a5)  
- **Microsoft SC-200:** In Progress  

---

## 🖥️ Lab Overview

⚠️ Important Note – Role-Based Access Control (RBAC)

When working with Log Analytics Workspace, Microsoft Defender, and Microsoft Sentinel, certain actions require specific permissions.

If you are not using a Global Administrator account, you must have the appropriate role assigned to perform tasks such as creating workspaces, configuring Sentinel, or managing integrations.
Microsoft solutions are based on RBAC (Role-Based Access Control), so always verify that your account has the necessary roles and permissions before starting the lab.

💡 Tip:
Use the least privileged role needed for each task. This helps you practice real-world security best practices while avoiding permission issues.

In this walkthrough, I will explore **Microsoft Defender XDR** and **Microsoft Sentinel** to demonstrate:

- Creating a Microsoft subscription and performing onboarding  
- Configuring integrations between Sentinel and Defender Portal  
- Implementing detection rules  
- Performing test attacks to tune alerts  

> **Note:** Microsoft solutions are based on **RBAC (Role-Based Access Control)**.

---

## 🧪 Lab Environment Setup

For this lab, I will use:

- **Microsoft 365 Defender E5 Trial**  
- **Azure Free Trial**  

> To isolate the environment from personal accounts, it is recommended to create a new email specifically for this trial. A payment method is required (e.g., virtual credit card). The 30-day trial is sufficient for hands-on practice.

### 🖥️ Windows 11 VM Setup

- One Windows 11 VM will be connected via **Microsoft Defender for Endpoint (MDE)**.  
- Onboarding MDE allows better understanding of how **endpoint telemetry** is collected and ingested into Microsoft Sentinel.

**Important Network and VM Configuration:**

- Set the VM’s network adapter to **Bridged mode**.  
  - Ensures the endpoint sensor communicates directly with Microsoft Defender cloud services via **HTTPS endpoints**.  
  - On Windows, the agent uses **WinHTTP** (Windows HTTP Services) to make HTTPS calls.
- Ensure internet access and connectivity to all required MDE URLs; otherwise, telemetry collection will fail.  
- Proper configuration is essential for logs to successfully enrich Sentinel.

---

### ⚡ Lab Simulation Notes

Before simulating attacks:

- PowerShell execution policies should **allow script execution**.  
- Microsoft Defender Antivirus should be **disabled or adjusted**.  
- Other protection features such as **ASR rules** or security policies should be **turned off or configured** to avoid interfering with simulations.  

> These settings ensure test activities are not blocked and telemetry is generated correctly for analysis.
