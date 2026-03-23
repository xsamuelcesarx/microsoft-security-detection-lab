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

Note: Microsoft solutions are based on RBAC (Role-Based Access Control).

For this walkthrough, I will use Microsoft 365 Defender E5 Trial and an Azure Trial for learning and practice purposes.
To keep the environment isolated from personal accounts, I recommend creating a new email specifically for this trial. You will also need a credit card or, in my case, I used a virtual card to register the trial license. The 30-day trial is sufficient for hands-on practice and learning.
I will use one Windows 11 VM to connect and ingest logs for testing purposes, which will help enrich my Sentinel environment.
This VM will be connected via Microsoft Defender for Endpoint (MDE). I will perform MDE onboarding on the VM, which will allow me to better understand how endpoint telemetry is collected and ingested into Microsoft Sentinel.
Important Note:
When using a VM to integrate with MDE for log ingestion into Sentinel:

    • Set the VM’s network adapter to Bridged mode. This ensures the endpoint sensor can communicate directly with Microsoft Defender cloud services via secure HTTPS endpoints. On Windows, the agent uses WinHTTP (Windows HTTP Services) to make these HTTPS calls.
    • Ensure the VM has internet access and can reach all required MDE URLs; otherwise, onboarding and telemetry collection will fail.
    • Proper network configuration is essential for the sensor to successfully send logs and enrich Sentinel.
    
This setup provides a safe, isolated lab environment for testing, learning, and understanding how MDE and Sentinel interact.
Before simulating attacks on the VM, ensure that PowerShell script execution policies are properly configured (execution policy is not restricted). 
Microsoft Defender Antivirus should be disabled or adjusted, and additional protection features such as ASR rules and security policies (e.g., AV policies) should be turned off or configured accordingly to prevent interference with the simulation.

This ensures that test activities are not blocked and that telemetry can be properly generated for analysis.

Create an Azure account and select the Azure Free Trial:

Sign in using the email created specifically for this lab environment.

Currently, Microsoft requires MFA (Multi-Factor Authentication) registration during account setup.

A payment method is required for registration. In my case, I used a virtual card instead of a physical credit card.

The registration process is straightforward and easy to complete. After finishing the setup, you will have access to the Azure Free Trial and can begin your lab.

Don’t forget that Azure is Microsoft’s cloud platform, which includes services such as:

- Entra ID (formerly Azure AD)  
- Microsoft Sentinel  
- Azure Monitor  
- Azure Arc  
- And many other functionalities  

Azure is a great place to explore and practice each service to understand what it does. 

Be proactive and take the time to learn—this hands-on experience will set you apart and become a valuable professional differentiator.
