## Welcome to Domain Name System (DNS)
DNS servers are responsible for resolving domain names into IP addresses. When setting up a DNS server, you typically use software like BIND (Berkeley Internet Name Domain), Unbound, or others. On Red Hat-based systems (like RHEL or CentOS), BIND is commonly used for installation and configuration. 

![DNS Architecture](/img/dns-architecture.png)

We will discuss 
- DNS Server Installation
- Primary DNS Server 
- Secondary DNS Server 
- Caching Only DNS Server 
- Forwarding to Another DNS Server 
- Recursive & Non Recursive Query 
- DNS Caching 
- Zone: Forward & Reverse
- DNS Record Types: A, PTR, NS, MX, SOA, TXT etc.
- DNS Testing Utilities: nslookup, Host, Dig etc. 
- DNS ACL 
- DNS Logging
- DNS Remote Control with Rndc (Remote Name Daemon Control)

### DNS Server Installation
```bash 
hostname
hostname -f
sudo dnf update
sudo dnf install bind bind-utils
sudo systemctl start named
sudo systemctl enable named
cat /etc/named.conf
sudo systemctl restart named
netstat -antp # Shows all active connections and listening ports
```
### Primary DNS Server 
The Primary DNS Server (also known as the Master DNS Server) holds the main records for a domain. It is where DNS zone files are stored and maintained. Key functions:
- Stores zone files for domains.
- Responds to DNS queries from clients.
- Provides authoritative information for a specific zone. Example of a zone file (`/etc/named.conf`):
```bash
zone "example.com" IN {
    type master;
    file "example.com.zone";
};
```
### Secondary DNS Server
The Secondary DNS Server (also known as Slave DNS Server) is a backup server that holds a read-only copy of the zone files. It helps distribute the DNS load and provides redundancy. Key functions:
- Retrieves zone files from the primary DNS server through zone transfers.
- Responds to queries in the same way as the primary server but without the ability to modify the zone records. Configuration in `/etc/named.conf`:
```bash
zone "example.com" IN {
    type slave;
    file "example.com.zone";
    masters { 192.168.1.10; };  # IP of primary DNS server
};
```
### Caching Only DNS Server 
A Caching Only DNS Server does not store authoritative records for domains. Instead, it caches the results from other DNS servers to reduce query times and traffic. This server only responds to DNS queries and stores the results temporarily.
- **Configuration:**
  - Typically configured without a zone file.
  - Responds only to recursive queries.
### Forwarding to Another DNS Server
Forwarding is a method where a DNS server forwards DNS queries to another DNS server (usually a more authoritative or external one) when it cannot resolve the query locally.
- **Forwarder Configuration:**
```bash
options {
    forwarders {
        8.8.8.8;  # Google's DNS
        8.8.4.4;
    };
};
```
### Recursive & Non Recursive Query 
- **Recursive Query:** The DNS server takes full responsibility for resolving the domain, querying other servers if necessary, until the final answer is found.
- **Non-Recursive Query:** The DNS server does not perform the full resolution and will only answer with cached data or refer the client to another DNS server.
### DNS Caching 
DNS servers store results of DNS queries for a period of time (called the Time to Live or TTL). This helps reduce the load on DNS servers and speeds up domain resolution.
- **TTL setting in a zone file:**
```bash
@   IN  SOA ns1.example.com. admin.example.com. (
        2023050101 ; Serial
        3600       ; Refresh
        1800       ; Retry
        1209600    ; Expire
        86400 )    ; TTL
```
### Zone: Forward & Reverse
- **Forward Zone:** This is the most common zone where a domain name is mapped to an IP address (A or AAAA records). Example for `forward zone` (`example.com.zone`):
```bash
@ IN A 192.168.1.1
```
- **Reverse Zone:** Used to resolve an IP address back to a domain name (PTR records). It's the reverse of the forward zone. Example for `reverse zone` (`1.168.192.in-addr.arpa.zone`):
```bash
@ IN PTR example.com.
```
### DNS Record Types: A, PTR, NS, MX, SOA, TXT etc.
There are many DNS record types, but here are some of the key ones:
| Record Type | Purpose                                                     |
| ----------- | ----------------------------------------------------------- |
| A           | Maps a domain to an IPv4 address.                           |
| AAAA        | Maps a domain to an IPv6 address.                           |
| CNAME       | Maps a domain to another domain (used for aliasing).        |
| MX          | Specifies mail servers for email delivery.                  |
| TXT         | Holds arbitrary text (e.g., SPF, domain verification).      |
| NS          | Lists authoritative name servers for the domain.            |
| SOA         | Start of Authority – provides info about the domain/zone.   |
| SRV         | Specifies location of services (e.g., SIP, XMPP).           |
| Alias       | AWS-specific alias to AWS resources (e.g., S3, CloudFront). |
### DNS Testing Utilities: nslookup, Host, Dig etc. 
These tools help you query DNS servers and troubleshoot DNS issues.
- **nslookup:** Simple command-line tool to query DNS records.
```bash
nslookup example.com
```
- **dig:** A more advanced tool for querying DNS.
```bash
dig example.com
```
- **host:** Another tool to perform DNS lookups.
```bash
host example.com
```
### DNS ACL 
DNS servers can use ACLs to control which clients are allowed to query the server, transfer zones, or update records. ACLs are useful for securing DNS servers and restricting access. Example in `/etc/named.conf`:
```bash
acl trusted {
    192.168.1.0/24;
};
options {
    allow-query { trusted; };
};
```
### DNS Logging
DNS logs can help troubleshoot DNS issues, monitor performance, and detect unusual activity. BIND can log queries and other events. 
- BIND Logging Configuration:
```bash
logging {
    channel default_file {
        file "/var/log/named.log" versions 3 size 5m;
        severity info;
    };
    category queries { default_file; };
};
```
### DNS Remote Control with Rndc (Remote Name Daemon Control)
`rndc` is a tool for managing BIND DNS servers remotely. It can be used to restart the server, reload zone files, or perform other administrative tasks.
- Basic usage:
```bash
rndc reload      # Reloads the configuration
rndc status      # Shows the current status of the DNS server
rndc stop        # Stops the DNS server
```
- For security, you usually set up rndc with a key for authentication. Example `/etc/rndc.key`:
```bash
key "rndc-key" {
    algorithm hmac-md5;
    secret "your-secret-key";
};
```
- In `/etc/named.conf`, configure the rndc key:
```bash
controls {
    inet 127.0.0.1 port 953 allow { 127.0.0.1; } keys { rndc-key; };
};
```
