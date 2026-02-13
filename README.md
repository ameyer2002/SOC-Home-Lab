# SOC-Home-Lab

SOC Architecture
1. On-Premises Network (My Home)

Edge: pfSense Firewall (Acts as the VPN Endpoint).

Security Stack: * Wazuh Manager: Central SIEM/HIDS collector.

Security Onion: Network sensor and traffic analyzer.

Endpoints:

Kali Linux: Attacker machine (Wazuh Agent installed).

Windows 10: Local victim (Wazuh Agent + Sysmon installed).

2. The Tunnel (The Bridge)

Site-to-Site VPN: IPsec tunnel connecting pfSense (Home) to AWS Virtual Private Gateway.

3. AWS Cloud Environment (Cloud Extension)

Infrastructure: VPC (e.g., 10.0.0.0/16).

Cloud Victim: EC2 Instance (Linux or Windows) with Wazuh Agent installed.

Cloud Logging: CloudTrail & VPC Flow Logs (forwarded to Wazuh/Security Onion).

