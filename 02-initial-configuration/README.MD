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
#### In details of Nano Editor
Operation & Navigation
|  SL   | Hit Key                  | Explanation                         |
| :---: | :----------------------- | :---------------------------------- |
|   1   | CTRL + Z                 | Suspend                             |
|   2   | CTRL + X                 | Exit Nano permanently               |
|   3   | CTRL + P                 | Move the cursor up one line         |
|   4   | CTRL + N                 | Move the cursor down one line       |
|   5   | CTRL + B                 | Move the cursor left one character  |
|   6   | CTRL + F                 | Move the cursor right one character |
|   7   | ALT + F or CTRL + →      | Move forward by one word            |
|   8   | CTRL + V                 | Scroll page down                    |
|   9   | CTRL + Y                 | Scroll half a page up               |
|  10   | CTRL + W                 | Scroll a full page up               |
|  11   | CTRL + A                 | Go to beginning of the line         |
|  12   | CTRL + E                 | Go to end of the line               |
|  13   | ALT + <                  | Go to beginning of the file         |
|  14   | ALT + >                  | Go to end of the file               |
|  15   | CTRL + _                 | Go to a specific line               |
|  16   | ALT + ,                  | Jump to a specific line or column   |
|  17   | CTRL + ↑                 | To previous block                   |
|  18   | CTRL + ↓                 | To next block                       |
|  19   | ALT + \|To top of buffer |
|  20   | ALT + /                  | To bottom of buffer                 |

Case Conversion
|  SL   | Hit Key | Explanation                                      |
| :---: | :------ | :----------------------------------------------- |
|   1   | ALT + L | Convert the selected text to lowercase           |
|   2   | ALT + U | Convert the selected text to uppercase           |
|   3   | ALT + C | Capitalize the selected text or the current word |

File Handling
|  SL   | Hit Key  | Explanation                                             |
| :---: | :------- | :------------------------------------------------------ |
|   1   | CTRL + S | Save current file                                       |
|   2   | CTRL + O | Offer to write file (“Save as”)                         |
|   3   | CTRL + R | Insert a file into current one                          |
|   4   | CTRL + A | Append the contents of another file to the current file |
|   5   | CTRL + W | Write the current file to a different filename          |
|   6   | CTRL + T | Invoke the spell checker on the current file            |

Editing Shortcuts 
|  SL   | Hit Key      | Explanation                        |
| :---: | :----------- | :--------------------------------- |
|   1   | CTRL + K     | Cut current line into cutbuffer    |
|   2   | ALT + 6      | Copy current line into cutbuffer   |
|   3   | CTRL + U     | Paste contents of cutbuffer        |
|   4   | ALT + T      | Cut until end of buffer            |
|   5   | CTRL + SPACE | Set a mark at the current position |
|   6   | CTRL + ]     | Indent the current line            |
|   7   | ALT + ]      | Unindent the current line          |
|   8   | ALT + 3      | Comment/uncomment line/region      |
|   9   | ALT + U      | Undo last action                   |
|  10   | ALT + E      | Redo last undone action            |

Search Shortcuts 
|  SL   | Hit Key             | Explanation                                                           |
| :---: | :------------------ | :-------------------------------------------------------------------- |
|   1   | CTRL + W            | Start forward search                                                  |
|   2   | CTRL + Q            | Start backward search                                                 |
|   3   | ALT + W             | Repeat the last forward search                                        |
|   4   | ALT + Q             | Find next occurrence backward                                         |
|   5   | ALT + R             | Repeat the last backward search                                       |
|   6   | ALT + W + CTRL + W  | Toggle case sensitivity during search                                 |
|   7   | ALT + W + ALT + W   | Toggle whole word search during search                                |
|   8   | ALT + W + ALT + R   | Toggle regular expression search during search                        |
|   9   | CTRL + W + CTRL + W | Move to the next occurrence of the search pattern                     |
|  10   | CTRL + W + CTRL + V | Move to the previous occurrence of search pattern                     |
|  11   | ALT + W + ALT + V   | Move to the next occurrence of the search pattern (ignoring case)     |
|  12   | ALT + W + ALT + B   | Move to the previous occurrence of the search pattern (ignoring case) |
|  13   | CTRL + W + CTRL + L | Toggle the “Search backwards” option during search                    |
|  14   | CTRL + W + CTRL + O | Toggle the “Wrap around” option during search                         |
|  15   | CTRL + W + CTRL + C | Count the number of occurrences of the search pattern                 |
|  16   | CTRL + W + CTRL + G | Cancel the search and return to editing                               |

Replace Shortcuts 
|  SL   | Hit Key             | Explanation                                                 |
| :---: | :------------------ | :---------------------------------------------------------- |
|   1   | CTRL + W + CTRL + T | Replace the current occurrence of the search pattern        |
|   2   | CTRL + W + CTRL + + | Replace all occurrences of the search pattern               |
|   3   | CTRL + W + CTRL + A | Replace all occurrences of the search pattern interactively |
|   4   | CTRL + W + CTRL + I | Interactive replace with confirmation for each occurrence   |

Deleting Shortcuts 
|  SL   | Hit Key    | Explanation                    |
| :---: | :--------- | :----------------------------- |
|   1   | CTRL + H   | Delete character before cursor |
|   2   | CTRL + D   | Delete character under cursor  |
|   3   | ALT + BSP  | Delete word to the left        |
|   4   | CTRL + DEL | Delete word to the right       |
|   5   | ALT + DEL  | Delete current line            |