# Security Onion

Setting up the Security Onion should be fairly simple. I did some research and found this [Github repo](https://github.com/Security-Onion-Solutions/securityonion/blob/2.4/main/DOWNLOAD_AND_VERIFY_ISO.md) that had the ISO image to download. On Security Onion's documentation, I saw I could download an AMI for Security Onion to be deployed in AWS which is really intriguing and something I may pursue down the line when I want to switch up the architecture of this SOC. But to start, I will have to configure two interfaces for this. One for management and one for sniffing. The management interface will be assigned an IP of **192.168.240.50**. Since my LAN VMs are between the range of 192.168.240.100–192.168.240.200, I want the management interface to be outside that DHCP/static range to avoid IP conflicts.

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/969c0421-60c3-4a35-b558-3c28e5b93484" />

I then setup the gateway IP to be **192.168.240.1** and the DNS server to **8.8.8.8**. Following this, I basically configured an allowlist in a way since I had to select an IP address or range to allow access to Security Onion. For this, I used my subnet IP which is **192.168.240.0/24**.


What I did from here was boot my pfsense machine which contains the LAN of all my machines. From the security onion terminal, I tried pinging the kali and windows machine but didn't get any ICMP messages sent back to me. I then went into each of those machines as ran a **ip a** on the kali machine and **ipconfig** on the windows machine to confirm the IP addresses were those from the IP range from the LAN. I saw they weren't but then realized my pfsense machine would have to be the first machine started in this lab in order for every other machine to have the correct IP in the LAN. I then pinged those machines and they were now running from the LAN.

<img width="800" height="600" alt="image" src="https://github.com/user-attachments/assets/fff6c885-5683-4405-ba0d-55a9212b0ebb" />
