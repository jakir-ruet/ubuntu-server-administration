### User & Group Access Management
Add user - `adduser/useradd(Debian)`
```bash
adduser jasim # add a user
id jasim # check user
```

Set password - `passwd`
```bash
passwd jasim # add a user
id jasim # check user's id
usermod -u 5000 jasim # 5000 is new id
```
To check how many groups in system & how many groups a user is a part 
```bash
cat /etc/group
groups jasim
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
grep jasim /etc/group # check group
grep jasim /etc/shadow # check password
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
`For Group:` 

Good to know `jasim:x:1002:` its get using `sudo vi /etc/group`
```bash
group_name(jasim):password(x):group_ID(1002):user_list(empty)
```

`For Shadow:` 

Good to know `jasim:!!:19547:0:99999:7:::` its get using `sudo vi /etc/shadow`
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

User is involved how many groups
```bash
groups jasim
```

Create a New Group
```bash
groupadd developer
groupadd designer
```

Replace a user to new group `-g`
```bash
usermod -g mango jasim # replace old/mother group
```
Append/add/assign a user to new group `-aG`
```bash
usermod -aG mango jasim # add extra group, old remain unchanged
usermod -aG mango,developer,designer jasim # add multiple - use `no spaces`
```

Remove group from a user
```bash
gpasswd -d jasim developer
```

The sudoers group is a system group. Its `sudoers` group in Linux is a special user group that is typically used to grant `sudo` privileges to users, allowing them to execute commands as the `root`/`superuser` or other users with administrative privileges.

Add a user to the sudoers group in `Debian`
```bash
usermod -aG sudo jasim # here, `sudo` group
```

Add a user to the sudoers group in `RPM`
```bash
sudo usermod -aG wheel jasim # here, `wheel` group
```

`sudoers` Configuration - Privilege
```bash
root  ALL=(ALL)   ALL
jasim ALL=(ALL)   ALL # allow privilege as root
```
Granting `wheel` Privileges to Groups:
```bash
%wheel   ALL=(ALL)   ALL   # Allow members of the 'sudo' group to run any command
```
If jasim is not in the wheel group, you can add him to the group using the following command:
```bash
sudo usermod -aG wheel jasim
```

Verifying Group Membership
```bash
groups jasim
```
Verify Privileges Using `sudo -l`
```bash
sudo -l -U jasim
```
If everything is set up correctly, you should see
```bash
User jasim may run the following commands on this host:
    (ALL) ALL
```
Test with a Command
```bash
su - jasim
su
ls /root # you should see root directory
```

Understanding Password Aging Parameters
```bash
sudo chage -l jasim
```
Check global defaults
```bash
cat /etc/login.defs
```