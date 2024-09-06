#### Server Securing
Securing an Ubuntu Server involves implementing various measures to protect it from unauthorized access, malicious attacks, and vulnerabilities.

***Step-01*** We should do regularly update your server's software packages, including the operating system and installed applications, to patch security vulnerabilities and ensure that you have the latest security fixes.
```bash
sudo apt update
sudo apt upgrade
```
***Step-02*** Allow only necessary ports and services and deny all others
```bash
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

***Step-03*** [Secure SSH access](https://github.com/jakir-ruet/ubuntu-server-administration/blob/master/03-remote-management/README.MD)
- Disable root login `PermitRootLogin no` and use SSH key authentication.
- Change the default SSH port `Port 22` (optional but can reduce exposure to automated attacks).
- Install and configure `fail2ban` to block IP addresses that have too many failed login attempts.

***Step-04*** Disable unused services
```bash
sudo systemctl disable httpd
```

***Step-05*** Monitor system logs
Regularly monitor system logs (`/var/log/syslog`, `/var/log/auth.log`, etc.) for any suspicious activities or signs of security breaches.

***Step-06*** Implement SSL/TLS Encryption
Secure communications between clients and your server by installing SSL/TLS certificates for services such as web servers, email servers, and FTP servers.

***Step-07*** Regular security audits
Conduct regular security audits and vulnerability assessments to identify and address potential security weaknesses and risks.

***Step-08*** Use strong passwords
For example `LionsEat3Cake$AtDawn!`

***Step-09*** Taking regular backups
Regularly back up your server's data to prevent data loss in case of hardware failure, accidental deletion, or security breaches.

***Step-10*** Enable automatic security updates:
Configure the unattended-upgrades package to automatically install security updates.

```bash
sudo apt install unattended-upgrades
sudo dpkg-reconfigure -plow unattended-upgrades
```

***Step-11*** Use security tools
Install and configure security tools such as intrusion detection systems (IDS), intrusion prevention systems (IPS), and antivirus software to further enhance your server's security posture.

***Step-12:*** Harden the Kernel
Consider implementing kernel hardening techniques such as restricting kernel modules, enabling ASLR (Address Space Layout Randomization), and configuring kernel security parameters.

NB:
After configuring these we should take creative initiative to properly configure the local network devices such as routers (MikroTik Router, CCNA Router), physical firewall, and so on.

#### IP Table
iptables is a command-line utility for configuring the Linux kernel firewall rules and network traffic, included in most Linux distributions. It allows users to set up, maintain, and inspect the tables of IP packet filter rules.

##### Architecture & Components
![Architecture](/img/iptables%20architecture.png)
1. **Tables**: A table is a collection of chains. The most common tables are:
   - `Filter`: Default table used for filtering packets. It has **three** built-in chains: `Input`, `Output`, and `Forward`.
   - `Network Address Translation (NAT)`: Altering packets to route traffic to the correct destination. It has chains like `Prerouting`, `Output`, and `Postrouting`.
   - `Mangle`: Used for `specialized` packet alteration such as `QoS`.
   - `Raw`: Used to configure exemptions from connection tracking.
2. **Chains**: A chain is a set of rules that match packets against specific criteria. Each table has its `five` chains:
   - `Prerouting`: Handles packets before any routing decisions are made by the system. 
   - `Input`: Handles packets destined for the local machine.
   - `Forward`: Handles packets being routed through the machine, but not destined for it.
   - `Output`: Handles packets originating from the local machine.
   - `Postrouting`: Handles packets after routing decisions have been made but before they leave the network interface.
3. **Rules**: Rules are added to chains to specify criteria for matching packets. Each rule consists of a set of conditions and a target action such as 
   - `Accept`, 
   - `Drop`, 
   - `Reject`, or 
   - `Log`
4. Targets: The target is what should happen to the packet if it matches the rule. Common targets include:
   - `Accept`: Allow the packet.
   - `Drop`: Drop the packet silently.
   - `Reject`: Drop the packet and send an error response.
   - `LOGog Log the packet details.