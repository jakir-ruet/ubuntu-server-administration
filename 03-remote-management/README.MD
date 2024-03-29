#### Remote Server Management (SSH Server Configuration)
Install SSH
```bash
sudo apt update
sudo apt install openssh-server
sudo systemctl status ssh
```
Checking the Uncomplicated FireWall (UFW)
Uncomplicated Firewall (UFW) is a program for managing a net-filter firewall designed to be easy to use.
```bash
sudo ufw status verbose # by default inactive
sudo ufw app list
sudo ufw app info 'OpenSSH'
```
Change SSH default port (22) in `/etc/ssh/sshd_config`
```bash
sudo nano /etc/ssh/sshd_config
control + x # save & exit
sudo ufw allow 2020/tcp
sudo ufw delete allow 22/tcp
sudo systemctl status ssh
sudo systemctl restart ssh
ufw enable
sudo ufw reload
sudo apt update
sudo ufw status verbose
ss -an | grep 2020 # To verify that SSH daemon is listening on the new port 2020, type:
sudo systemctl disable --now ssh # if we need to disable SSH service
sudo systemctl enable --now ssh
```

Access to this server from remote computer via SSH
```bash
ssh -p 2020 server_username@host_name/ip_address
ssh -p 2020 ubuntuserver@172.16.102.134
```

If you faced ‘Host key verification failed’
```bash
ssh-keygen -R 172.16.102.134
exit
```
#### Virtual Network Computing (VNC)
It is a graphical desktop-sharing system that uses the Remote Frame Buffer protocol (RFB) to remotely control another computer. It transmits the keyboard and mouse input from one computer to another, relaying the graphical-screen updates, over a network.
```bash
lsb_release -a # os version check
cat /etc/os-release
```
```bash
sudo apt update 
sudo apt install lightdm 
sudo reboot 
sudo apt install x11vnc 

sudo nano /lib/systemd/system/x11vnc.service

!Copy and paste these commands - change the password
[Unit] 
Description=x11vnc service 
After=display—manager.service network.target syslog.target 

[Service] 
Type=simple 
ExecStart=/usr/bin/x11vnc —forever —display :0 —auth guess -passwd 
ExecStop=/usr/bin/killall x11vnc 
Restart=on—failure 

[Install] 
WantedBy=multi—user.target 

systemctl daemon—reload 
systemctl enable x11vnc.service 
systemctl start x11vnc.service
systemctl status x11vnc.service
```