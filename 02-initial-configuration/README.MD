#### Initial Configuration
```bash
sudo apt upgrade
sudo apt install net-tools
sudo apt update
```
#### Setup static IP Address
```bash
ip a
ip addr
ifconfig
ifconfig -a
```
Go to `/etc/netplan/`
```bash
cp 00-installer-config.yaml 00-installer-config.yaml_bak # take backup
nano 00-installer-config.yaml
```
Initialize IP Address on `00-installer-config.yaml`
```YAML
# This is the network config written by 'subiquity'
network:
  ethernets:
    ens160:
      dhcp4: false
      addresses: [192.168.3.128/24]
      gateway4: 192.168.3.1
      nameservers:
        addresses: [192.18.145.1, 8.8.8.8]
  version: 2
```
Or
```YAML
# This is the network config written by 'subiquity'
network:
  version: 2
  renderer: networkd
  ethernets:
    ens160:
      dhcp4: false
      addresses:
        - 192.168.13.129/32
      routes:
        - to: default
          via: 192.168.13.1
      nameservers:
        addresses: [192.18.145.1,8.8.8.8]
```
```bash
control + x # save & exit
```
```bash
netplan try
netplan apply
netplan –debug  apply
ifconfig
```