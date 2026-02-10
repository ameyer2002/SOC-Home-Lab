# Setting up Wazuh

First thing's first, I setup Wazuh using the Wazuh OVA (Open Virtual Appliance) directly from the [installation documentation](https://documentation.wazuh.com/current/deployment-options/virtual-machine/virtual-machine.html). Once this was downloaded and powered on, the VM was getting stuck on the logo page and not properly booting to where I could be prompted with entering credentials. I checked the network adapter, the display of the machine, only to realize the OVA I had downloaed was specifically for Workstation 6.5-7.x which is a much older version of the VMware Workstation I am currently using, Workstation 25H2. I switched this and the machine booted properly where I could login using **wazuh-user** as the username and **wazuh** as the password. I then ran ip a to check the address of the machine which was **192.168.146.133**.
<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/8c46e263-c220-41e9-abed-1dab819f849c" />

My next task was to open a browser and enter the IP address in a tab where I could enter **admin** as both the username and password. Just like that, I had the machine up and running successfully.

<img width="1897" height="945" alt="image" src="https://github.com/user-attachments/assets/be8a9edc-99fb-4f5b-870b-3a06b8c7c675" />

Now it's time to setup the Wazuh agent on my Kali Linux machine. An agent is installed on different endpoints to see what's occurring locally and collect logs and forward them to a central system. Again, following the [Wazuh agent installation documentation](https://documentation.wazuh.com/current/installation-guide/wazuh-agent/wazuh-agent-package-linux.html), I ran the following commands in my Kali:

* curl -sO https://packages.wazuh.com/4.14/wazuh-install.sh
* apt-get install gnupg apt-transport-https
* curl -s https://packages.wazuh.com/key/GPG-KEY-WAZUH | gpg --no-default-keyring --keyring gnupg-ring:/usr/share/keyrings/wazuh.gpg --import && chmod 644 /usr/share/keyrings/wazuh.gpg
* echo "deb [signed-by=/usr/share/keyrings/wazuh.gpg] https://packages.wazuh.com/4.x/apt/ stable main" | tee -a /etc/apt/sources.list.d/wazuh.list
* apt-get update
* WAZUH_MANAGER="192.168.146.133" apt-get install wazuh-agent
* systemctl daemon-reload
* To verify the agent was running: **sudo systemctl status wazuh-agent**.

<img width="1280" height="800" alt="image" src="https://github.com/user-attachments/assets/ea14299b-9763-4131-aeed-432ab40a35c0" />
