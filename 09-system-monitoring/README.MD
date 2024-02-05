#### Process Management
Running an instance of a program is called a process. In Linux Process ID (PID) is used to represent the process details. The process will be implemented in Linux in two ways;
1. Background Process
   Depends on the user for input also referred to as interactive processes. For example Office programs.
2. ForegroundProcess
   Runs independently of the user referred to as a non-interactive or automatic process. For example Antivirus programs
***State: ***
A process in Linux can go through different states after it’s created and before it’s terminated. These states are:
- Running
- Sleeping
  - Interruptible sleep
  - Uninterruptible sleep
- Stopped
- Zombie
- A process in a running state means that it is running or it’s ready to run.
- The process is in a sleeping state when it is waiting for a resource to be available.
- A process in Interruptible sleep will wake up to handle signals, whereas a process in Uninterruptible sleep will not.
- A process enters a stopped state when it receives a stop signal.
- Zombie state is when a process is dead but the entry for the process is still present in the table.

The important terminology follows:
|  SL   |   Field   | Description                                 | Example 1 | Example 2 |
| :---: | :-------: | :------------------------------------------ | :-------: | :-------: |
|   1   |   `PID`   | The process ID of each task                 |   1525    |    961    |
|   2   |  `User`   | The username of task owner                  |   Home    |   Root    |
|   3   |   `PR`    | Priority- Can be 20(highest) or -20(lowest) |    20     |    20     |
|   4   |   `NI`    | The nice value of a task                    |     0     |     0     |
|   5   |  `VIRT`   | Virtual memory used (kb)                    |   1775    |   75972   |
|   6   |   `RES`   | Physical memory used (kb)                   |    100    |    51     |
|   7   |   `SHR`   | Shared memory used (kb)                     |    28     |   7952    |
|   8   |    `S`    | There are five Status*                      |     S     |     R     |
|   9   |  `%CPU`   | % of CPU time                               |    1.7    |    1.0    |
|  10   |  `%MEM`   | Physical memory used                        |    10     |    5.1    |
|  11   |  `TIME+`  | Total CPU time                              |  5:05:34  |  2:23:43  |
|  12   | `Command` | Command name                                |   snapd   |  systemd  |

- Status:
  There are five types:
  - ‘D’ = uninterruptible sleep ‘R’ = running
  - ‘S’ = sleeping
  - ‘T’ = traced or stopped
  - ‘Z’ = zombie

Different Commands for Process Management
There are two commands available in Linux to track running processes. These two commands are ‘top’ and ‘ps’.
|  SL   |        Command        | Explanation                                                                                                                               |
| :---: | :-------------------: | :---------------------------------------------------------------------------------------------------------------------------------------- |
|   1   |         `top`         | To track the running processes on your machine you can use the top command. Press q for quit.                                             |
|   2   | `ps (Process Status)` | It displays the currently running processes. However, unlike the top command, the output generated is not in real-time. Press q for quit. |

To get more information using the ps command use:
```bash
ps -u
```
The terminology is as follows:
|  SL   | Command | Explanation                                   |
| :---: | :-----: | :-------------------------------------------- |
|   1   |  `PID`  | Process ID                                    |
|   2   |  `TTY`  | Terminal TYpe                                 |
|   3   | `TIME`  | Total time the process has been running       |
|   4   |  `CMD`  | Name of the command that launches the process |

While the ps command only displays the processes that are currently running, you can also use it to list all the processes.
```bash
ps -A
```
***Stop process:*** Checking the kill service name and its ID.
```bash
kill -l or $kill -L
```