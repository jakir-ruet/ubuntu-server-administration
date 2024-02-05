#### File Management:
File management is so important on a computer that users always want a simple and easy way to use it. Performing simple tasks such as searching, copying, moving, creating and deleting files, and complex operations such as remote access of files and SSH connections is vital.

##### Renaming the file & folder:
```bash
sudo mv presentNameOfFile.format NewNameOfFile.format
sudo mv presentNameOfFolder NewNameOfFolder
```

##### Deleting/removing the file:
removing/deleting files/directories
```bash
sudo rm -f fileName.format
sudo rm -R dirName # if there is something in the directory
sudo rm -r dirname1 dirname2 dirname3
sudo rm -r filename1 filename2 filename3
```
copying the file & folder:
```bash
sudo cp fileName.format destinationFolder
```
Same as with files you can also use a wildcard (*) and regular expansions to match multiple directories.

File, folder & its permission management:
Permission Notation
|  SL   | Command     | Notation              |
| :---: | :---------- | :-------------------- |
|   1   | `-`         | File                  |
|   2   | `d`         | Directory             |
|   3   | `r`         | Read (4)              |
|   4   | `w`         | Write (2)             |
|   5   | `x`         | Execute (1)           |
|   6   | `o`         | Other                 |
|   7   | `a`         | All                   |
|   8   | `b`         | Block File            |
|   9   | `c`         | Character Device File |
|  10   | `p`         | Pipe File             |
|  11   | `s`         | Socket File           |
|  12   | `Pipe Sign` | Symbolic Links        |
|  13   | `-`         | No Permission         |
|  14   | `.`         | Extended Attributes   |

Segment Layout
|  SL   | file/directory   | rwx (7)   |  r-x (5)  |  r-x (5)  | root  |    root    |
| :---: | :--------------- | :-------- | :-------: | :-------: | :---: | :--------: |
|   1   | `File/Directory` | Owner (o) | Group (g) | Users (u) | User  | User Group |

We can give permission to others in two ways: one is alphabetic & another is numeric.

|  SL   | Numeric                           | Alphabetic                                |
| :---: | :-------------------------------- | :---------------------------------------- |
|   1   | `sudo chmod 777 file/folder name` | `sudo chmod u/g/o+r/w/x file/folder name` |
|   2   | `sudo chmod 777 file/folder name` | `sudo chmod ugo+rwx file/folder name`     |
|   3   | `sudo chmod 000 file/folder name` | `sudo chmod u/g/o-r/w/x file/folder name` |
|   4   | `sudo chmod 777 file/folder name` | `sudo chmod ugo-rwx file/folder name`     |
|   5   | `sudo chmod 777 file/folder name` | `sudo chmod a=rwx file/folder name`       |

The following are the usual options used with chmod:
- -f, --silent, --quiet: Suppresses most error messages.
- -v, --verbose: Outputs a diagnostic for every file processed.
- -c, --changes: Like verbose but reports only when a change is made.
- -R, --recursive: Changes files and directories recursively. 
  To modify the permissions of each and every file and folder in a provided directory at once, use sudo chmod with -R
- --help: Displays help and exits.
- --version: Outputs version information and exits.

The table below gives numbers for all permissions types.
|  SL   | Decimal Value | Permission Type (rwx)    | Symbol (rwx) | Binary Value |
| :---: | :-----------: | :----------------------- | :----------: | :----------: |
|   1   |      `0`      | `No Permission`          |    `---`     |    `000`     |
|   2   |      `1`      | `Execute`                |    `--x`     |    `001`     |
|   3   |      `2`      | `Write`                  |    `-w-`     |    `010`     |
|   4   |      `3`      | `Read + Execute`         |    `-wx`     |    `011`     |
|   5   |      `4`      | `Read`                   |    `r--`     |    `100`     |
|   6   |      `5`      | `Read + Execute`         |    `r-w`     |    `101`     |
|   7   |      `6`      | `Read + Write`           |    `rw-`     |    `110`     |
|   8   |      `7`      | `Read + Write + Execute` |    `rwx`     |    `111`     |

Symbolic Mode
|  SL   | Operator | Description                                                      |
| :---: | :------: | :--------------------------------------------------------------- |
|   1   |   `+`    | `Adds permission to a file or directory`                         |
|   2   |   `-`    | `Removes the permission`                                         |
|   3   |   `=`    | `Sets the permission and overrides the permissions set earlier.` |

Change Permission Recursively
It is common to use the basic chmod command to change the permission of a single file. However, you may need to modify the permissions recursively for all files within a directory. 
```bash
sudo chmod -R 755 Example
```
