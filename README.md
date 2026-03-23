My name is Samuel Cesar, and I have been studying Cyber Security for over a year. I use GitHub to publish my studies, providing a clear and structured way to share my learning process. My goal is to explain each stage of cybersecurity in a straightforward manner, including practical tips and insights.

Certifications and Achievements:

IEFP – Cybersecurity Specialist Technician (Level 5)

Blue Team Level 1 (BTL1) – Gold Coin

Splunk Core Certified Power User

Microsoft SC-900 (Security, Compliance, and Identity Fundamentals)

Microsoft AZ-900 (Azure Fundamentals)

Fortinet Network Security Expert (FCA)

CCNA (expired)

Blue Team Labs Online: #https://blueteamlabs.online/public/user/6255328b393299c2c9a387

Linkedln: #www.linkedin.com/in/samuel-cesar-9100261a5

Microsoft SC-200 In Progress

In this walkthrough, I will explore Microsoft Defender XDR and Microsoft Sentinel to demonstrate how to create a subscription, perform onboarding, configure integrations, and implement detection rules. I will also perform test attacks to tune alerts using my techniques to simplify troubleshooting and optimize the lab environment for learning purposes.

I will use a VirtualBox virtual machine. Below, I provide its configuration and guidance on how to optimize the VM for testing and ensuring smooth integrations.


**Before starting, I use “Free-VirtualBox”, which is my preferred choice as it minimizes conflicts and is simple to operate.**

Windows VM Setup Recommendation
------------------------------

This section outlines my recommended setup for building a clean, stable, and realistic Windows Virtual Machine environment for malware analysis and hands-on lab practices.

The goal is to ensure optimal performance while minimizing system lag, crashes, and unwanted conflicts that could interfere with analysis activities.

I will document the exact configuration I use, including system resources, VM settings, and optimization techniques to maintain a reliable and efficient lab environment.

Hypervisor Choice:
- I use Oracle VirtualBox as my primary virtualization platform.
- It provides a lightweight, stable, and easy-to-manage environment.
- Reduces compatibility issues and allows quick deployment of analysis VMs.

Key Objectives:
- Maintain a clean and controlled analysis environment
- Avoid performance bottlenecks during dynamic analysis
- Ensure system stability during malware execution
- Support repeatable and safe testing procedures

Additional Notes:
- All lab activities are performed in an isolated Windows VM
- Snapshots are used to restore clean states after each test
- The environment is configured to simulate realistic user behavior when needed

This setup is designed to support practical cyber exercise while maintaining safety, stability, and efficiency.


Windows ISO Download – Initial Setup
-----------------------------------

The first step is to download the Windows operating system directly from the official Microsoft website.

Procedure:
1. Access the official Microsoft download page.
2. Select the desired Windows version.
3. Choose the system language.

Recommendation:
- Use **English (United States)** as the system language.
- This helps reduce potential compatibility issues during installation and when using security tools, scripts, and documentation (most are standardized in English).

Download Process:
- Select the option to download the installation file in **ISO format**.
- The ISO file provides a complete image of the operating system and is the most reliable method for creating a virtual machine.

Notes:
- ISO format allows easier integration with virtualization platforms like VirtualBox.
- Ensures a clean and controlled installation environment.

Initial VM Configuration – Best Practices
----------------------------------------

The key to a clean and error-free Windows installation is to first create a base virtual machine with minimal and optimized settings. This base VM can later be cloned and reused for multiple analysis scenarios.

Basic Configuration:

Name:
- Assign a generic and reusable name.
- This VM will serve as a “clean baseline” image for cloning and future lab use.

Memory (RAM):
- Recommended: Minimum 8 GB
- Windows 10/11 requires significant memory due to background services and system processes.
- Using less than 8 GB may cause:
  - Installation failures or freezes
  - System instability
  - Poor performance during analysis
- Critical note: Insufficient RAM can impact real-time memory analysis (volatile memory), leading to inaccurate results or system crashes.

Storage (Disk):
- Recommended:
  - 50 GB+ for reusable (baseline) VM
  - 80 GB+ for long-term projects and multiple tools
- Ensures enough space for:
  - Analysis tools
  - Malware samples
  - System logs and memory dumps

Network Configuration:
- Mode: Bridged Adapter
  - Provides a more realistic network environment
  - Allows the VM to behave like a real host on the network

- Promiscuous Mode: Allow VMs
  - Useful for network traffic analysis and packet capture

Security Warning:
- If using the VM for malware analysis or sandboxing:
  - Always isolate the environment when required
  - Avoid exposing infected VMs to production networks
  - Consider using Host-Only or Internal Network for safer testing scenarios

Notes:
- This base VM should remain clean (no malware execution)
- Use snapshots and cloning for each new analysis session
- Ensures repeatability, safety, and consistency across tests

Important Installation Tips
--------------------------

To ensure a clean and error-free Windows installation in a virtual machine, follow these best practices:

1. Avoid Direct ISO Attachment During VM Creation
- Do NOT attach the Windows ISO during the initial VM creation step.
- First, create the VM with only hardware settings (Name, RAM, Disk, CPU).
- After the VM is created, configure the ISO manually:

  Path:
  Settings → Storage → Optical Drive → Select Windows ISO

- This approach helps prevent boot issues and ensures a cleaner and more controlled installation process.

2. Disable Network Adapter Before Installation
- Go to:
  Settings → Network → Disable Network Adapter

- This prevents Windows Setup from forcing:
  - Mandatory updates
  - Microsoft account login
  - Unnecessary online dependencies

- This is especially useful for:
  - Malware analysis labs
  - C2 testing scenarios
  - Offline environments
  - Faster installation process

3. Bypass Network Requirement (Windows 10/11)
- In some cases, Windows Setup will still require an internet connection.

- To bypass this requirement:
  - Press: Shift + F10
  - This will open the Command Prompt (CMD)

- Then execute the following command:

  OOBE\BYPASSNRO

- The system will restart, and after reboot:
  - You will be able to continue installation without internet
  - Option to create a local account will be available

Notes:
- This method is commonly used in lab environments and testing scenarios
- Avoid unnecessary updates when working with controlled malware analysis setups
- Always keep a clean snapshot before executing any samples

Post-Installation Essentials & Optimization
------------------------------------------

1. Install Guest Additions (Critical Step)
- Always install Guest Additions to ensure full compatibility and performance of the VM.
- It improves:
  - Graphics performance
  - Mouse integration
  - Clipboard sharing
  - File transfer between host and VM

Installation Steps (VirtualBox):
1. Start the VM
2. In the top menu: Devices → Insert Guest Additions CD Image
3. Open "This PC" inside the VM
4. Run: VBoxWindowsAdditions.exe
5. Follow the installation wizard
6. Reboot the VM after installation

Benefits:
- Enables copy & paste between host and VM
- Allows drag-and-drop file transfer
- Improves usability for lab environments
- Speeds up analysis workflow

2. Enable Clipboard & File Transfer
- Go to:
  Settings → General → Advanced

- Configure:
  - Shared Clipboard: Bidirectional
  - Drag’n’Drop: Bidirectional

Note:
- This feature is useful for:
  - Copying commands/scripts
  - Transferring tools and samples
  - Improving productivity during analysis

⚠ Security Note:
- Be cautious when transferring malware samples.
- Prefer using isolated folders or controlled environments.

3. PowerShell Script Execution Policy
- By default, PowerShell restricts script execution.

- To allow script execution, run PowerShell as Administrator:

  Command:
  Set-ExecutionPolicy Bypass -Scope Process

- This allows scripts to run temporarily for the current session.

Alternative (less secure):
  Set-ExecutionPolicy Unrestricted

Note:
- Use "Bypass" for lab scenarios to avoid permanent changes.

4. Re-enable Network After Setup
- After completing installation and configuration:
  - Go to: Settings → Network → Enable Network Adapter

- This allows:
  - Tool downloads
  - Updates (if needed)
  - External communication for testing

5. Final Recommendation
- Take a snapshot of the clean VM before using it
- Use this baseline for cloning and repeated malware analysis
- Ensures:
  - Consistency
  - Safety
  - Easy recovery after infection

Summary:
- Install Guest Additions for full VM functionality
- Enable clipboard and file sharing for efficiency
- Allow PowerShell scripts for automation
- Re-enable network only when needed
- Always maintain a clean snapshot baseline
