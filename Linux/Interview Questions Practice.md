Repository: https://github.com/chassing/linux-sysadmin-interview-questions
## General Questions
---



## Simple Linux Questions
---
**What is the name and the UID of the administrator user?**

=> The default administrator user on most Unix or Linux systems is called **root**, and its UID is **0**.

**How to list all files, including hidden ones, in a directory?**

=> `ls -a`

**What is the Unix/Linux command to remove a directory and its contents?** 

=> `rm -r <directory-name>` or with force `rm -rf <directory-name>`

**Which command will show you free/used memory? Does free memory exist on Linux?**

=> `free -h` or `cat /proc/meminfo`
Yes, Linux provides the concept of free memory, but much RAM may be used for disk caching and buffers, which can be reclaimed if needed; so "free" memory is effectively available memory plus reclaimable cache.

**How to search for the string "my konfu is the best" in files of a directory recursively?**

=> `grep -r "my konfu is the best" <directory_path>`

**How to connect to a remote server or what is SSH?**

=> SSH stands for Secure Shell; it's a protocol to securely connect to remote systems over a network. You use:

`ssh username@hostname`

to open a secure shell session.

**How to get all environment variables and how can you use them?**

=> Use: `printenv` or `env`

to list all environment variables. You can reference a variable using `${VARNAME}` or set new ones with `export`.

**I get "command not found" when I run ifconfig -a. What can be wrong?**

`ifconfig` may not be installed (modern distros prefer `ip`). Install it with `sudo apt install net-tools` (Debian/Ubuntu) or use `ip a` for interface info.

**What happens if I type TAB-TAB?**

Pressing TAB-TAB triggers shell autocompletion—a list of possible commands or filenames appears for you to choose from.

**What command will show the available disk space on the Unix/Linux system?**

Use: `df -h`

This displays disk usage with sizes in human-readable formats.

**What commands do you know that can be used to check DNS records?**

Use:
- `dig domainname`
- `nslookup domainname`
- `host domainname`  
    For querying DNS records.

**What Unix/Linux commands will alter a file's ownership or permissions**?

- Change ownership: `chown user:group filename`
- Change permissions: `chmod mode filename`

**What does chmod +x FILENAME do?**

It grants execute permission to the file for the user(s) covered by the existing permission bits.

**What does the permission 0750 on a file mean?**

Owner: read, write, execute; Group: read, execute; Others: no access.

**What does the permission 0750 on a directory mean?**

Owner: full access; Group: can list/enter; Others: no access.

**How to add a new system user without login permissions?**

Use: `useradd -M -s /usr/sbin/nologin username`

`-M` prevents home directory creation, and `-s` sets the shell to nologin.

**How to add/remove a group from a user?**

To add: `usermod -aG groupname username`  
To remove: `gpasswd -d username groupname` or edit `/etc/group`.

**What is a bash alias?**

A Bash alias is a shortcut—a custom command that replaces longer commands. Define using:

`alias shortname='command'`

Aliases improve productivity for frequently used commands.

**How do you set the mail address of the root/a user?**

Update `/etc/aliases` (then run `newaliases`), or configure your mail program's settings.

**What does CTRL-c do?**

It sends SIGINT, interrupting and terminating the current foreground process.

**What does CTRL-d do?**

It signals end-of-file (EOF), closing input or logging out from a shell session.

**What does CTRL-z do?**

It sends SIGTSTP, pausing the current process and sending it to the background (stopped state).

**What is in /etc/services?**

It maps well-known network service names (like `http` or `ftp`) to their port numbers and protocols.

**How to redirect STDOUT and STDERR in bash? (> /dev/null 2>&1)**

Redirect output and errors via:

`command > /dev/null 2>&1`

This discards both streams.

**What is the difference between UNIX and Linux?**

UNIX is the original OS (many proprietary variants); Linux is a free/open-source Unix-like kernel and ecosystem.

**What is the difference between Telnet and SSH?**

Telnet is unencrypted; SSH is secure and encrypted. SSH also supports authentication and tunneling.

**Explain the three load averages and what do they indicate. What command can be used to view the load averages?**

The three numbers shown (e.g., in `uptime` or `top`) are averages of system load over the last 1, 5, and 15 minutes. They represent the number of runnable processes.

**Can you name a lower-case letter that is not a valid option for GNU ls?**

The letter `y` is not a recognized option in GNU ls.

**What is a Linux kernel module?**

It's a piece of code that can be dynamically loaded/unloaded into the kernel to add functionality (e.g., device drivers).

**Walk me through the steps in booting into single user mode to troubleshoot a problem.**

Edit the boot grub entry: append `single` or `init=/bin/bash` to kernel parameters. Reboot; you'll get root shell with minimal services.

**Walk me through the steps you'd take to troubleshoot a 404 error on a web application you administer.**

Check web server config (virtual host/document root), examine log files (access/error logs), verify file existence and permissions, test routing, and inspect firewall/URL rewrite settings.

**What is ICMP protocol? Why do you need to use?**

ICMP (Internet Control Message Protocol) is a network-layer protocol used to send diagnostic, error, and operational messages (e.g., via ping) to aid in troubleshooting and network health monitoring.

---

## Medium Level Questions

**What do the following commands do and how would you use them?: Command Descriptions and Usage**

- **tee**: Reads from standard input and writes to both standard output and files; useful for logging piped output while still viewing it. Example: `ls | tee list.txt` saves output to `list.txt` and displays it.
- **awk**: Powerful text processing tool for extracting and manipulating data from files, commonly used for column extraction and reporting. Example: `awk '{print $2}' file.txt` prints the second column.
- **tr**: Translates or deletes characters from input, such as changing case or removing characters. Example: `echo ABC | tr 'A-Z' 'a-z'` outputs `abc`.
- **cut**: Removes (extracts) sections from each line of input, usually by delimiter or character position. Example: `cut -d',' -f1 file.csv` for first CSV column.
- **tac**: Like `cat`, but prints lines in reverse order. Example: `tac file.txt`.
- **curl**: Transfers data from or to a server via URLs, supporting a variety of protocols; often used for API calls and debugging. Example: `curl https://example.com`.
- **wget**: Non-interactive network downloader, often used for downloading files or web content in scripts. Example: `wget http://example.com/file.zip`.
- **watch**: Runs a command periodically (every 2 seconds by default) and shows results fullscreen. Example: `watch ls`.
- **head**: Displays the first N lines of a file (default: 10). Example: `head log.txt`.
- **tail**: Shows the last N lines (default: 10); use `-f` to follow growing files. Example: `tail -f log.txt`.
- **less**: Interactive pager for viewing file content one screen at a time (navigate easily). Example: `less longfile.txt`.
- **cat**: Concatenates and outputs file content; also used to create or append files. Example: `cat file1 file2`.
- **touch**: Creates an empty file or updates the modification/access time of an existing file. Example: `touch newfile.txt`.
- **sar**: System Activity Reporter; displays historical system performance data such as CPU, memory, disk, etc.
- **netstat**: Displays network connections, routing tables, interface statistics, and more. Example: `netstat -tuln`.
- **tcpdump**: Captures and displays network packets for analysis. Example: `sudo tcpdump -i eth0 port 80`.
- **lsof**: Lists open files and their associated processes. Example: `lsof -i` displays open network connections.

**What does an `&` after a command do?**
- **`&` after a command**: Runs the command in the background, freeing the shell for other input. Example: `sleep 60 &`.

**What does `& disown` after a command do?**
- **`& disown` after a command**: Runs the command in the background and detaches it from the current terminal, preventing termination if the shell exits. Example: `sleep 60 & disown`.

**What is a packet filter and how does it work?**
- **Packet filter**: A firewall feature that inspects packet headers and decides (using rules like IP/protocol/port) whether to allow or block network traffic. It works at the network layer, enforcing security policies by filtering, forwarding, or dropping packets.

**What is Virtual Memory?**
- **Virtual Memory**: An abstraction that combines physical RAM with disk space (swap) to provide processes with more memory than is physically available, facilitating multitasking and preventing process interference.

**What is swap and what is it used for?**
- **Swap**: Dedicated disk space used when RAM is exhausted; the OS moves inactive memory pages there to free RAM for active tasks. It can slow performance but helps prevent out-of-memory errors.

**What is an A record, an NS record, a PTR record, a CNAME record, an MX record?**

|Record|Description|
|---|---|
|**A**|Maps hostname to IPv4 address|
|**NS**|Delegates a zone to authoritative name servers|
|**PTR**|Maps IP address to hostname (reverse DNS)|
|**CNAME**|Alias for another domain name|
|**MX**|Mail exchange; specifies mail server for a domain|
