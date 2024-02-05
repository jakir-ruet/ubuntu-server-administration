#### File transfer
File transferring among Ubuntu, Window & MacOS can be done few way. Here we are going to discuss some popular methods. As per our need we will discussed `scp` & `ssh`
1. Via Secure Copy (scp)
   ```bash
   scp -p DestinationPcSSHPort FileInHost(hello.txt) DestinationPcUser@DestinationPcIP:/home/DestinationPcUser
   scp -p 22 hello.txt nodetwo@172.16.102.133:/home/nodetwo
   scp -p 22 nodetwo@172.16.102.133:/home/nodetwo/hello.txt /home/ubuntuserver
   ```
2. Via FTP using SSH
   - FileZilla, 
   - WinSCP
3. Via Samba Server
4. Via Shared Network Folders
   