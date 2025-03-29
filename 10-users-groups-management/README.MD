### User & Group Access Management
Add user - `adduser/useradd(Debian)`
```bash
adduser jasim # add a user
id jasim # check user
```

Set password - `passwd`
```bash
passwd jasim # add a user
id jasim # check user
```

Delete user - `userdel/deluser(Debian)`
```bash
deluser jasim
userdel -r jasim # delete from home directory
```

The user **account was deleted**, but the home directory `/home/UserName` was not removed.

Check if Any Files Still Belong to the Deleted User
```bash
ls -ld /home/jasim
ls -l /home/jasim
```
Check for Stale Entries in `/etc/group` and `/etc/shadow`
```bash
grep jasim /etc/group
grep jasim /etc/shadow
```
If you find stale entries, you can remove them manually using `Be careful when editing these system files`
```bash
sudo vi /etc/group # remove, save & exit
sudo vi /etc/shadow # remove, but cannot save, force save `:wq!`
rm -rf jasim # remove user manually
```
Remove the Home Directory `If Safe` - If you are sure the user `jasim` is no longer needed:
```bash
sudo rm -rf /home/jasim
```
`For Group:` Good to know `jasim:x:1002:` its get using `sudo vi /etc/group`
```bash
group_name(jasim):password(x):group_ID(1002):user_list(empty)
```

`For Shadow:` Good to know `jasim:!!:19547:0:99999:7:::` its get using `sudo vi /etc/shadow`
```bash
username(jasim):password(!!):last_change(19547):min_days(0):max_days(99999):warn(7):inactive(empty):expire(empty)
```

The error message `adduser: user 'jasim' already exists` indicates that there might still be remnants of the user `jasim` in the system, even after removing the `/etc/group` and `/etc/shadow` entries.

Check `/etc/passwd` for Residual Entries
```bash
cat /etc/passwd | grep jasim
jasim:x:1002:1002::/home/jasim:/bin/bash # output
```
Then remove the line from `/etc/passwd`
```bash
sudo vi /etc/passwd
ls /home/
```

The message `Creating mailbox file: File exists` suggests that there is an existing `mailbox file` for the user `jasim`, which is typically `created for users` with a mail system like `Sendmail` / `Postfix` configured.
Check and Remove the Mailbox File from `/var/mail`
```bash
rm -f /var/mail/jasim
```
Check `/var/spool/mail/` Directory: If the file is located in `/var/spool/mail/`, remove it as well:
```bash
rm -f /var/spool/mail/jasim
```

Additionally, The `lsof` `List Open Files` command is a powerful tool in Linux used to list all the files that are currently open by processes.
```bash
lsof +D /home/jasim # +D: Recursively lists all files opened under the specified directory, including files in subdirectories.
```

Finally, create the user named `jasim`. It will work properly
```bash
sudo adduser jasim
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