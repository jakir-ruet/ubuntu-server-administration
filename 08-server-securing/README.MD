#### Server Securing
Securing an Ubuntu Server involves implementing various measures to protect it from unauthorized access, malicious attacks, and vulnerabilities.

**Step-01** We should do regularly update your server's software packages, including the operating system and installed applications, to patch security vulnerabilities and ensure that you have the latest security fixes.
```bash
sudo apt update
sudo apt upgrade
```
**Step-02** Allow only necessary ports and services and deny all others
```bash
sudo ufw enable
sudo ufw default deny incoming
sudo ufw default allow outgoing
```

**Step-03** [Secure SSH access](https://github.com/jakir-ruet/ubuntu-server-administration/blob/master/03-remote-management/README.MD)
- Disable root login `PermitRootLogin no` and use SSH key authentication.
- Change the default SSH port `Port 22` (optional but can reduce exposure to automated attacks).
- Install and configure `fail2ban` to block IP addresses that have too many failed login attempts.

**Step-04** Disable unused services
```bash
sudo systemctl disable httpd
```

**Step-05** Monitor system logs
Regularly monitor system logs (`/var/log/syslog`, `/var/log/auth.log`, etc.) for any suspicious activities or signs of security breaches.

**Step-06** Implement SSL/TLS Encryption (Cryptographic Protocol)
Secure communications between clients and your server by installing SSL/TLS certificates for services such as web servers, email servers, and FTP servers. Types of cryptographic protocol;
- [`Secure Sockets Layer - SSL`](https://www.digicert.com/faq/public-trust-and-certificates/what-is-ssl)
  An old encryption protocol used to secure communication over the internet. It ensures data privacy and integrity between two systems (e.g., browser and server). Obsolete — SSL 2.0 and 3.0 are insecure and deprecated.
- [`Transport Layer Security - TLS`](https://www.digicert.com/tls-ssl/tls-ssl-certificates)
  The modern and secure replacement for SSL.Current version: TLS 1.3 (latest) and TLS 1.2 (widely used). Used for: Encrypting data in transit (`web`, `email`, `FTP`, `VPN`, etc.)
- [`Hyper Text Protocol Secure - HTTPS`](https://www.digicert.com/faq/vulnerability-management/what-is-https-everywhere)
  Uses: HTTP + TLS, Port: 443 (vs. 80 for HTTP). Benefit: Encrypts all web traffic between the client (browser) and server, preventing: `Eavesdropping`, `Man-in-the-middle (MITM) attacks` & `Data tampering`

**SSL/TSL Certificate Types with Description & Ideal Use**
| **Type**                        | **Description**                     | **Ideal For**                                           |
| ------------------------------- | ----------------------------------- | ------------------------------------------------------- |
| **DV (Domain Validated)**       | Validates only domain ownership     | Personal websites, blogs, internal tools                |
| **OV (Organization Validated)** | Validates org + domain              | Business websites, company portals                      |
| **EV (Extended Validated)**     | Strictest identity verification     | Banks, eCommerce, finance, legal, healthcare sectors    |
| **Wildcard**                    | Covers all subdomains of one domain | Enterprises with many subdomains (e.g., `*.domain.com`) |
| **SAN (Multi-domain)**          | Covers multiple different domains   | SaaS providers, multi-brand websites, O365 deployments  |
| **Self-signed**                 | Only for internal/test environments | Development, internal servers, lab setups               |

**Step-07** Regular security audits
Conduct regular security audits and vulnerability assessments to identify and address potential security weaknesses and risks.

**Step-08** Use strong passwords
For example `LionsEat3Cake$AtDawn!`

**Step-09** Taking regular backups
Regularly back up your server's data to prevent data loss in case of hardware failure, accidental deletion, or security breaches.

**Step-10** Enable automatic security updates:
Configure the unattended-upgrades package to automatically install security updates.

```bash
sudo apt install unattended-upgrades
sudo dpkg-reconfigure -plow unattended-upgrades
```

**Step-11** Use security tools
Install and configure security tools such as intrusion detection systems (IDS), intrusion prevention systems (IPS), and antivirus software to further enhance your server's security posture.

**Step-12:** Harden the Kernel
Consider implementing kernel hardening techniques such as restricting kernel modules, enabling ASLR (Address Space Layout Randomization), and configuring kernel security parameters.

NB:
After configuring these we should take creative initiative to properly configure the local network devices such as routers (MikroTik Router, CCNA Router), physical firewall, and so on.

#### IP Table
iptables is a command-line utility for configuring the Linux kernel firewall rules and network traffic, included in most Linux distributions. It allows users to set up, maintain, and inspect the tables of IP packet filter rules.

##### Prerequisite
- On Ubuntu
```bash
sudo apt update
sudo apt install iptables
```
- On Rocky/CentOS/RedHat
```text
Installed by Default
```

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

##### Basic Commands
```bash
iptables -L # List all rules
iptables -A INPUT -p tcp --dport 22 -j ACCEPT # Add a rule
iptables -D INPUT 1 # Delete a rule
sudo iptables-save > /etc/iptables/rules.v4 # Save rules to make them persistent across reboots
```

**Explanation:**
- -A INPUT > Append the rule to the INPUT chain.
- -p tcp > Specify the protocol (TCP in this case).
- -s Source > Define the source.
- -d Destination > Define the destination.
- --dport 80 > Match packets destined for port 80.
- -j ACCEPT > The target action (ACCEPT the packet).
- -m > match extension
- -i > Insert the rule

If you want to block all incoming traffic except SSH (port 22), you could use:
```bash
iptables -P INPUT DROP # Set the default policy of INPUT chain to DROP
iptables -A INPUT -p tcp --dport 22 -j ACCEPT # Allow incoming SSH traffic
iptables -A INPUT -m state --state ESTABLISHED,RELATED -j ACCEPT # Allow established/related traffic
```
##### Common Use Cases
- Firewall configuration: To allow or block specific traffic.
- Network Address Translation (NAT): For forwarding traffic from one IP to another.
- Port forwarding: Redirect traffic from one port to another.

##### Advanced iptables uses
1. **Port Forwarding with NAT:** Port forwarding can be used to redirect traffic from one port on your server to another port or machine.
```bash
iptables -t nat -A PREROUTING -p tcp --dport 80 -j DNAT --to-destination 192.168.1.2:8080
iptables -t nat -A POSTROUTING -j MASQUERADE
```
This example forwards incoming HTTP traffic (port 80) to a different server (`192.168.1.2`) on port `8080`.

2. **Logging Dropped Packets:** You might want to log packets that are being dropped by your firewall rules.
```bash
iptables -A INPUT -p tcp --dport 23 -j LOG --log-prefix "Dropped Telnet Packet: "
iptables -A INPUT -p tcp --dport 23 -j DROP
```
This rule logs any attempt to connect via Telnet (port 23) and then drops the packet.

3. **Restricting SSH Access to a Specific IP:** To allow SSH access only from a particular IP address.
```bash
iptables -A INPUT -p tcp --dport 22 -s 203.0.113.10 -j ACCEPT
iptables -A INPUT -p tcp --dport 22 -j DROP
```
Only the IP address `203.0.113.10` can connect via SSH; all other SSH traffic is dropped.

4. **Rate Limiting Connections:** To limit incoming connections to prevent brute-force attacks.
```bash
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --set
iptables -A INPUT -p tcp --dport 22 -m state --state NEW -m recent --update --seconds 60 --hitcount 4 -j DROP
```
This example allows a maximum of 3 new SSH connections per minute.

5. **Making Rules Persistent:** On most Linux distributions, iptables rules are not persistent across reboots. To make them persistent:
- Save the current iptables configuration:
```bash
sudo iptables-save > /etc/iptables/rules.v4
```
- Restore rules on reboot: Use a service like `iptables-persistent` (Debian/Ubuntu) or configure them in the appropriate system file (`/etc/sysconfig/iptables` on CentOS/RedHat).

### Encryption
It's a fundamental technique in computer security used to protect data confidentiality by transforming `plaintext` into unreadable `ciphertext` using algorithms and cryptographic keys. It ensures that only authorized parties can read the original data, even if intercepted.

#### Basic Concepts of Encryption
| **Type**                 | **Description**                                                                             |
| ------------------------ | ------------------------------------------------------------------------------------------- |
| **PlainTex**             | The original readable data that needs to be encrypted, like "Hello, world!"                 |
| **Ciphertext**           | The encrypted, unreadable data after applying encryption, line "7d0a2b1e6a1c"               |
| **Key**                  | A secret string of data used by encryption algorithms to perform the encryption/decryption. |
| **Encryption Algorithm** | The original readable data that needs to be encrypted.                                      |
| **Decryption**           | The reverse process of encryption to convert ciphertext back into plaintext.                |

#### Types of Encryption
There are `two` types of encryption algorithms: `symmetric` (also called shared key algorithm) and `asymmetric` (also known as public key algorithm). **Hash functions** are not technically encryption, but they are often used alongside encryption for integrity checks, digital signatures, and password hashing.

1. **Symmetric Key Encryption (Private Key Encryption)**
   It's uses the same key for `encryption` and `decryption`. Because it uses the `same key`, symmetric encryption can be more cost effective for the security it provides. That said, it is important to invest more in securely storing data when using symmetric encryption.

![Symmetric Key Encryption (Private Key Encryption)](/img/symmetric-key-encryption.png)

2. **Asymmetric Key Encryption (Public Key Encryption)**
   It's uses `two` separate keys: a `public key` and a `private key`. Often a public key is used to encrypt the data while a private key is required to decrypt the data. The private key is only given to users with authorized access. As a result, asymmetric encryption can be more effective, but it is also more costly.

![Asymmetric Key Encryption (Public Key Encryption)](/img/asymmetric-encryption.png)

#### Types of data encryption
Here are some examples of common types of encryption used today.
1. **AES - Advanced Encryption Standard**
   It's is a **symmetric encryption** algorithm standardized by NIST. It uses the same key for both encryption and decryption, operating on `128`-bit data blocks with key sizes of `128`, `192`, or `256` bits. Known for its speed and strong security, AES is widely used in government, finance, and technology to protect sensitive data across software and hardware systems.
2. **Triple DES (3DES) - Triple Data Encryption Standard**
   It's, often written `3DES`, is a version of the original DES encryption algorithm that encrypts data `three` times. The Triple DES uses three `64`-bit keys, so the key length is `192` bits. Triple DES is a **symmetric encryption**, and the key is private. Because it encrypts data in `64`-bit segments, Triple DES is considered a block cipher. Cipher Block Chaining (CBC), however, is an encryption mode that struggles at high data rates.
3. **Blowfish**
   It's Similar to Triple DES, Blowfish is a **symmetric block cipher**. Unlike Triple DES, Blowfish does variable-length key encryption. Rather than set `64`-bit segments, Blowfish encrypts segments ranging from `32 to 448` bits. Blowfish is an unpatented and unlicensed encryption technique. For this reason, it is free and available for public use.
4. **RSA - Ron `R`ivest, Adi `S`hamir, and Leonard `A`delman**
   It's the standard encryption technique for important data security. RSA is asymmetric cryptography, so there is one public key and one private key. The RSA algorithm uses prime factorization. Simply put, this key requires the factorization of a product involving two large prime numbers. While it seems easy, figuring out these two numbers can be difficult. Even for large computers, it can be expensive and exhaustive to decrypt. While RSA can be very useful, it becomes increasingly inefficient at higher security levels.
5. **AES - Advanced Encryption Standard**
   Because of an increase in brute-force attacks on the original DES, It was put into place in 2002. AES is a symmetric block cipher that was originally named Rijndael. This block cipher uses three separate keys: `AES-128`, `AES-192`, and `AES-256`. These three keys are used to encrypt and decrypt information of 128 bits. Since its adoption, AES has been used to protect classified government information and sensitive data.
6. **ECC - Elliptic Curve Cryptography**
   It's a very advanced approach. Often based on a common public key algorithm, ECC combines elliptic curves and number theory to encrypt data. These elliptic curves are within finite fields and are symmetrical over the x-axis of a graph. Given these properties, cryptographers can provide robust security with much smaller and efficient keys. For example, an RSA key of 15,360 bits would be equivalent to an ECC key of just 512 bits.

  #### Hash functions
  A hash function is a mathematical algorithm that transforms input data of any size into a fixed-size output, known as a hash, digest, or checksum. Types of hash functions
  - Secure Hash Algorithm (SHA)
  - Message Digest Algorithm 5 (MD5)

**Secure Hash Algorithm (SHA)**
  The Secure Hash Algorithm (SHA) is a family of cryptographic hash functions developed by the National Security Agency (NSA) and published by NIST. SHA functions are widely used to ensure `data integrity`, `authenticate messages`, and `secure digital signatures`, and `password hashing`. Common Variants:
- `SHA-1:` Produces a `160`-bit hash (now considered insecure).
- `SHA-2:` Includes `SHA-224`, `SHA-256`, `SHA-384`, and `SHA-512` (stronger and widely used).
- `SHA-3:` A newer standard with a different internal design (based on the Keccak algorithm).

**Message Digest Algorithm 5 (MD5)**
It's stands for `Message Digest Algorithm 5`. It's a widely used cryptographic hash function that produces a `128`-bit (16-byte) hash value, typically rendered as a `32`-digit hexadecimal number.
