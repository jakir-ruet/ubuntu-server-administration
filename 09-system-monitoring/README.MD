### System Tuning?
System tuning refers to optimizing the performance of a computer system by adjusting certain parameters, configurations, and settings. In the context of **Red Hat Enterprise Linux (RHEL)**, system tuning aims to improve the efficiency, speed, and resource management of your server or workstation. This can involve fine-tuning several components, including:

- **CPU:** Adjusting how the CPU performs tasks or manages multiple processes (like setting CPU governor for performance or power savings).
- **Memory (RAM):** Configuring how the system uses memory, including optimizing cache usage, limiting swap usage, or enabling huge pages for large-memory applications.
- **Disk I/O:** Modifying disk scheduling algorithms or file system parameters to improve read/write operations.
- **Network:** Tuning TCP/IP settings for faster data transfer and reducing network latency.
- **Kernel Parameters:** Fine-tuning the Linux kernel parameters (via sysctl) for better system performance under load.

**Tuning Important?**
- **Performance Optimization:** Tuning ensures that your system runs as efficiently as possible, making sure resources (CPU, memory, disk, network) are used optimally.
- **Stability:** Proper tuning can help avoid system crashes or slowdowns by preventing resource exhaustion.
- **Scalability:** Tuning helps systems scale to meet the needs of high-load applications, such as web servers, databases, and enterprise applications.
- **Security:** Some tuning, such as disabling unused services or restricting resource access, can improve the overall security posture of your system.

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
ps      # running process
ps -A   # running process in details
top     # running process realtime
htop     # running process realtime
ps -u   # running process

ps -ef  # process in details (location)
ps aux  # process in details (location)
ps aux | less # process in details (location) less
ps aux | grep terminal # process display which related to terminal
pstree # see the tree of process
ps -C su # see the ps by category
pgrep bash # Find the PID
```

Checking the kill service name and its ID.
```bash
kill -l # kill list
kill -L # kill list
```
Kill the process
```bash
kill -9 PID
```