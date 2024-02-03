[![LinkedIn][linkedin-shield-lapissoft]][linkedin-url-lapissoft]
[![Facebook-Page][facebook-shield-lapissoft]][facebook-url-lapissoft]
[![Youtube][youtube-shield-lapissoft]][youtube-url-lapissoft]

## Visit Us [Lapis Soft](http://www.lapissoft.com)

### Terminal Multiplexer (tmux)

tmux is an open-source terminal multiplexer for Unix-like operating systems. It allows multiple terminal sessions to be accessed simultaneously in a single window. It is useful for running more than one command-line program at the same time. It can also be used to detach processes from their controlling terminals, allowing remote sessions to remain active without being visible.

### Install
#### Ubuntu Linux
```bash
sudo apt-get update
sudo apt-get install tmux
```
#### MacOS
```bash
brew update
brew install tmux
```
##### Tmux Plugin Manager Install

https://github.com/tmux-plugins/tpm

#### Version Check
```bash
tmux -V
```
#### Terminal use as tmux
```bash
tmux
```
#### Check location
```bash
command -v tmux
```
### tmux consist three sections
- Session (t target, a > attach, i > index no, d > detach ):   
  It is collection of windows (terminal). each session has a active window. Sessions are useful for completely separating work environments.
  |  SL   | Command                                                                                  | Explanation                                             |
  | :---: | :--------------------------------------------------------------------------------------- | :------------------------------------------------------ |
  |   1   | `tmux \ tmux new \ tmux new-session`                                                     | start new as tmux                                       |
  |   2   | `tmux a \ tmux at \ tmux attach \  tmux attach-session`                                  | attach to last sessions                                 |
  |   3   | `tmux a -t session_name`                                                                 | creates a new tmux session by session-name              |
  |   4   | `tmux ls \ tmux list-sessions`                                                           | list of sessions                                        |
  |   5   | `tmux new -s session-name`                                                               | new session by session name                             |
  |   6   | `tmux kill-ses -t session-name \ tmux kill-session -t session-name`                      | kill/delete by session name                             |
  |   7   | `tmux a -t session-name \ tmux at -t session-name \ tmux attach-session -t session-name` | attach to a session by session-name                     |
  |   8   | `tmux kill-session i`                                                                    | kill a indexed session                                  |
  |   9   | `tmux kill-session -a`                                                                   | kill/delete current session by session-name             |
  |  10   | `tmux kill-session -a -t session-name`                                                   | kill/delete all sessions by session-name                |
  |  11   | `tmux attach -t session_name`                                                            | creates a new tmux session named session_name           |
  |  12   | `tmux switch -t session_name`                                                            | attaches to an existing tmux session named session_name |
  |  13   | `tmux detach \ tmux -d`                                                                  | detach the currently attached session                   |
  |  14   | `control + b w`                                                                          | session and window preview                              |
  |  15   | `control + b (`                                                                          | move to previous session                                |
  |  16   | `control + b )`                                                                          | move to next session                                    |

- Window (n > new): 
  It is container of panes. tmux has a tabbed interface, but it calls its tabs “Windows”.
  |  SL   | Command                           | Explanation                                          |
  | :---: | :-------------------------------- | :--------------------------------------------------- |
  |   1   | `control + b n`                   | next window                                          |
  |   2   | `control + b c \ tmux new-window` | create a new window                                  |
  |   3   | `control + b ,`                   | rename the current window                            |
  |   4   | `control + b &`                   | close current window                                 |
  |   5   | `control + b w`                   | list windows                                         |
  |   6   | `control + b p`                   | previous window                                      |
  |   7   | `control + b i`                   | switch/select window by index(i)                     |
  |   8   | `control + b l`                   | toggle last active window                            |
  |   9   | `: swap-window -s 2 -t 1`         | reorder window, swap window number 2(src) and 1(dst) |
  |  10   | `: swap-window -t -1`             | move current window to the left by one position      |

- Pane:
  Panes take my development time from bland to awesome.
  |  SL   | Command                                                         | Explanation                                                                                   |
  | :---: | :-------------------------------------------------------------- | :-------------------------------------------------------------------------------------------- |
  |   1   | `control + b ;`                                                 | toggle last active pane                                                                       |
  |   2   | `control + b o`                                                 | switch to next pane                                                                           |
  |   3   | `control + b q`                                                 | show pane numbers                                                                             |
  |   4   | `control + b q i`                                               | switch/select pane by index(i)                                                                |
  |   5   | `control + b z`                                                 | toggle pane zoom                                                                              |
  |   6   | `control + b %`                                                 | split the current pane with a vertical line to create a horizontal layout (: split-window -h) |
  |   7   | `control + b "`                                                 | plit the current with a horizontal line to create a vertical layout (: split-window -v)       |
  |   8   | `control + b !`                                                 | convert pane into a window                                                                    |
  |   9   | `: join-pane -s 2 -t 1`                                         | join two windows as panes (Merge window 2 to window 1 as panes)                               |
  |  10   | `: join-pane -s 2.1 -t 1.0`                                     | move pane from one window to another (Move pane 1 from window 2 to pane after 0 of window 1)  |
  |  11   | `control + b {`                                                 | move the current pane left                                                                    |
  |  12   | `control + b }`                                                 | move the current pane right                                                                   |
  |  13   | `control + b ↑ \ control + b ↓ \ control + b → \ control + b ←` | switch to pane to the direction                                                               |
  |  14   | `control + b + ↑`                                               | resize current pane height(holding second key is optional)                                    |
  |  15   | `control + b control + ↑`                                       | resize current pane height(holding second key is optional)                                    |
  |  16   | `control + b ↓`                                                 | resize current pane height(holding second key is optional)                                    |
  |  17   | `control + b control + ↓`                                       | resize current pane height(holding second key is optional)                                    |
  |  18   | `control + b + →`                                               | resize current pane width(holding second key is optional)                                     |
  |  19   | `control + b control + →`                                       | resize current pane width(holding second key is optional)                                     |
  |  20   | `control + b + ←`                                               | resize current pane width(holding second key is optional)                                     |
  |  21   | `control + b control + ←`                                       | resize current pane width(holding second key is optional)                                     |
  |  22   | `control + b x`                                                 | close current pane                                                                            |
  |  23   | `: setw synchronize-panes`                                      | toggle synchronize-panes(send command to all panes)                                           |
  |  24   | `control + b spacebar`                                          | toggle between pane layouts                                                                   |

Other essential command (: setw -g mode-keys vi) use vi keys in buffer:
  Panes take my development time from bland to awesome.
  |  SL   | Command                 | Explanation                                            |
  | :---: | :---------------------- | :----------------------------------------------------- |
  |   1   | `control + b [`         | enter copy mode                                        |
  |   2   | `control + b ]`         | paste contents of buffer_0                             |
  |   3   | `control + b PgUp`      | enter copy mode and scroll one page up                 |
  |   4   | `/`                     | search forward                                         |
  |   5   | `?`                     | search backward                                        |
  |   6   | `n`                     | next keyword occurance                                 |
  |   7   | `N`                     | previous keyword occurance                             |
  |   8   | `Spacebar`              | start selection                                        |
  |   9   | `Esc`                   | clear selection                                        |
  |  10   | `Enter`                 | copy selection                                         |
  |  11   | `q`                     | quit mode                                              |
  |  12   | `g`                     | go to top line                                         |
  |  13   | `G`                     | go to bottom line                                      |
  |  14   | `↑`                     | scroll up                                              |
  |  15   | `↓`                     | scroll down                                            |
  |  16   | `h`                     | move cursor left                                       |
  |  17   | `j`                     | move cursor down                                       |
  |  18   | `k`                     | move cursor up                                         |
  |  19   | `l`                     | move cursor right                                      |
  |  20   | `w`                     | move cursor forward one word at a time                 |
  |  21   | `b`                     | move cursor backward one word at a time                |
  |  22   | `: show-buffer`         | display buffer_0 contents                              |
  |  23   | `: capture-pane`        | copy entire visible contents of pane to a buffer       |
  |  24   | `: list-buffers`        | show all buffers                                       |
  |  25   | `: choose-buffer`       | show all buffers and paste selected                    |
  |  26   | `: save-buffer buf.txt` | save buffer contents to buf.txt                        |
  |  27   | `: delete-buffer -b 1`  | delete buffer_1                                        |
  |  28   | `control + b :`         | nter command mode                                      |
  |  29   | `control + b ?`         | list key bindings(shortcuts)                           |
  |  30   | `tmux list-keys`        | lists out every bound key and the tmux command it runs |
  |  31   | `tmux list-commands`    | lists out every tmux command and its arguments         |
  |  32   | `tmux info`             | lists out every session, window, pane, its pid, etc.   |

#### Architecture Terminal Multiplexer (tmux)
![Architecture Terminal Multiplexer (tmux)](/img/tmux-server.png)

#### Exit from a window
```bash
exit
```

### Courtesy of Jakir
[![LinkedIn][linkedin-shield-jakir]][linkedin-url-jakir]
[![Facebook-Page][facebook-shield-jakir]][facebook-url-jakir]
[![Youtube][youtube-shield-jakir]][youtube-url-jakir]

### Have a good day, stay with me
<!-- Personal profile -->
[linkedin-shield-jakir]: https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white
[linkedin-url-jakir]: https://www.linkedin.com/in/jakir-ruet/
[facebook-shield-jakir]: https://img.shields.io/badge/Facebook-%231877F2.svg?style=for-the-badge&logo=Facebook&logoColor=white
[facebook-url-jakir]: https://www.facebook.com/jakir-ruet/
[youtube-shield-jakir]: https://img.shields.io/badge/YouTube-%23FF0000.svg?style=for-the-badge&logo=YouTube&logoColor=white
[youtube-url-jakir]: https://www.youtube.com/@mjakaria-ruet/featured

<!-- Company profile -->
[linkedin-shield-lapissoft]: https://img.shields.io/badge/linkedin-%230077B5.svg?style=for-the-badge&logo=linkedin&logoColor=white
[linkedin-url-lapissoft]: https://www.linkedin.com/company/lapis-soft/
[facebook-shield-lapissoft]: https://img.shields.io/badge/Facebook-%231877F2.svg?style=for-the-badge&logo=Facebook&logoColor=white
[facebook-url-lapissoft]: https://www.facebook.com/GoLapisSoft/
[youtube-shield-lapissoft]: https://img.shields.io/badge/YouTube-%23FF0000.svg?style=for-the-badge&logo=YouTube&logoColor=white
[youtube-url-lapissoft]: https://www.youtube.com/@LapisSoft/featured
