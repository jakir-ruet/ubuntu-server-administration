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