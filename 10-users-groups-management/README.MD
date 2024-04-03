### User & Group Management
```bash
adduser/useradd: # To add a user
deluser/userdel: # To delete a user
grep jakir /etc/passwd # check password
sudo deluser userName groupName # remove a user from the group
sudo usermod -l newName oldName # change user name
sudo usermod -l jasim jakir # change user name
sudo passwd jasim # change user password
id -u jasim # show user ID of a user
sudo usermod -u 4567 jasim # change the user ID of a user
```

```bash
addgroup/groupadd: # To add a group
delgroup/groupdel: # To delete a group
sudo grep finance /etc/group
sudo usermod -g devops jasim # change group of jasim (g for primary group)
sudo usermod -G ops jasim # change group of jasim (G for secondary group)
sudo groupadd -g 650 finance # add a new group with specific GID
sudo userdel -r jasim # delete a home directory of a user (/home)
```
```bash
passwd: # To change the user’s password
```
```bash
su - jakir # login
```
```bash
cat /etc/passwd # understanding password
```

Add a user to sudoers group
```bash
sudo usermod -aG sudo jasim # -a is add a user to the group without removing the current group.
ALL=(ALL:ALL) ALL # first one is the users allowed,  second one is the hosts, third one is the user as you are running the command & last one is the commands allowed
```