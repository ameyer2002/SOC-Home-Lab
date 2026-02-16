# Windows 10 VM

Creating the Windows 10 ISO image was a bit more complicated then I expected it to be. Looking over the official [Download Windows 10](https://www.microsoft.com/en-us/software-download/windows10?msockid=106e5622b34763fd1a1640dfb29e623d) documentation, I downloaded the installation media which eventually prompted me with selecting a USB flash drive, DVD, or ISO file. I chose the ISO file and saved it to my desktop. This took around 5 minutes to download but once it finished, I opened the file in my VMware and began setting up the machine to my liking. Once the machine became usable, I immediately opened up PowerShell as an admin and ran **ipconfig** to check the IP address. 

<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/59613698-f5ae-4dd7-b74b-039285230530" />

After finding the IP address, I began setting up the Wazuh agent on this endpoint. On my Kali machine, I setup the agent directly from the terminal but this time I wanted to setup the agent directly from Wazuh. However, I did still have to run some commands in PowerShell to download and install the agent. I ran the following commands:

* Invoke-WebRequest -Uri https://packages.wazuh.com/4.x/windows/wazuh-agent-4.14.2-1.msi -OutFile $env:TEMP\wazuh-agent.msi 
* msiexec.exe /i $env:TEMP\wazuh-agent.msi WAZUH_MANAGER="192.168.00.198"**.

Now I just had to start the agent. I ran **GET-SERVICE wazuh** to check that the agent exists which it did so I then ran **NET START wazuh** which activated the agent to start running. 

<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/f33598af-e746-4072-b8a8-8d70084e1e65" />

The Windows endpoint is now appearing in Wazuh.

<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/28b333aa-8d0e-47e6-9dd4-d6e0ebf473cc" />

Now that mostly everything is in place and my Kali machine, Windows machine, and Wazuh machine are all on the same LAN behind the firewall, I wanted to ping the Windows machine from Kali. I first attempted to do this and didn't get any ICMP messages sent back to me. I found out that by default, Windows 10 machines blocks all inbound ICMP messages so I ran this command to disable the Windows firewall which is also important for this lab so I can attack it from Kali. **netsh advfirewall set allprofiles state off**

<img width="1024" height="768" alt="image" src="https://github.com/user-attachments/assets/b5772e77-9c52-4d0e-b4e2-f806121643a3" />

What's really cool about Wazuh is that once I installed the agent on my Windows machine, a security report card is generated which is called CIS Microsoft Windows 10 Enterprise Benchmark v4.0.0. Within this are benchmarks that help with system hardening. Wazuh uses its SCA (Security Configuration Assessment) module to scan my VMs which in this case is the Windows 10 machine and checks how many of these "best practice" rules I am actually following.

<img width="1920" height="948" alt="Screenshot (6)" src="https://github.com/user-attachments/assets/a5927ff1-43ae-4e04-9b18-a90f14333625" />

The **passed** logs mean my Windows settings match the secure recommendation and the **failed** logs mean the current state of the machine is considered a security risk.
