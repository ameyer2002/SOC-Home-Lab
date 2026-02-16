# Setting up pfSense

While setting up my pfSense firewall, I ran into several bumps in the road that made the process more challenging than I thought. At first, I assigned IP addresses to the LAN and WAN interfaces without fully checking how they aligned with VMware’s virtual networks. The WAN interface was connected to the NAT network, but its IP didn’t fall within the NAT subnet, so pfSense couldn’t properly reach the internet. Also, the LAN interface was tied to the host-only network, but the initial IP I assigned wasn’t compatible with the host-only subnet which made the web GUI inaccessible from my host machine. I was also not sure whether I should let the LAN interface get an IP via DHCP or to assign it a static IP, but ultimately I chose to statically assign the LAN interface to 192.168.240.1.

The biggest issue turned out to be the host-only adapter itself. It was using the .0 network address (192.168.240.0), which isn’t a valid host IP, so my host couldn’t communicate with the pfSense LAN at 192.168.240.1. Once I correctly assigned a proper IP to the host adapter (192.168.240.100) within the same subnet and ensured the pfSense LAN was on the static address 192.168.240.1, the network finally became reachable. I received ICMP messages when pinging the IP which told me it should be up and running. 

<img width="720" height="400" alt="pfSense-2026-02-15-10-30-35" src="https://github.com/user-attachments/assets/1d2b9d73-7929-4f01-9055-0c93a605b52a" />


<img width="1920" height="927" alt="Screenshot (3)" src="https://github.com/user-attachments/assets/85595c47-bc74-48a5-8d24-8deb482d6079" />

From  here, I am going to run the Setup Wizard.

<img width="1920" height="943" alt="Screenshot (4)" src="https://github.com/user-attachments/assets/baabc1cb-c748-41d3-bc55-5c19b0c3cce4" />
