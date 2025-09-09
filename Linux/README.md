## Phase 0: Foundation & Lab Setup (Week 1)

**Objective:** Prepare the lab and develop fundamental Linux concepts

## Topics

- **RHEL Access:**
    
    - Join the Red Hat Developer Program for a free RHEL subscription (updates included)
        
    - Use a 1:1 clone: AlmaLinux or Rocky Linux (identical for exam purposes)
        
- **Lab Setup:**
    
    - Install a virtualization platform (VirtualBox/VMware Player/Workstation)
        
    - Set up RHEL or a clone in a VM
        
    - Create multiple snapshots (e.g., fresh OS, after user creation, before LVM setup)
        
    - Add extra virtual disks for hands-on storage/LVM practice
        
    - Configure SSH key authentication between your VMs early
        
- **Linux Basics:**
    
    - Filesystem hierarchy (/, /home, /etc, /var, /boot)
        
    - Terminal/Bash basics, absolute vs relative paths, SSH connection
        

**Free Resources:**

- Red Hat Developer: [https://developers.redhat.com/](https://developers.redhat.com/)
    
- Linux Documentation Project: [https://tldp.org/](https://tldp.org/)
    

---

## Phase 1: System Operation & Command Line Mastery (Weeks 2-3)

**Objective:** Control and operate basic system functions; manage users and security

## Topics

- **Command Line:** ls, cd, pwd, cp, mv, rm, mkdir, touch
    
- **File Permissions:** rwx, chmod, chown, chgrp
    
- **User/Group Management:** useradd/usermod/userdel, groupadd/groupmod/groupdel, /etc/passwd, /etc/shadow, /etc/group
    
- **Text File Manipulation:** vim/vi mastery (modal editing, search/replace, editing configs, batch edits); basic use of nano, but be proficient with vim
    
- **I/O Redirection:** <, >, >>, 2>
    
- **Process Management:** ps, top, kill, killall
    

**Practical Tips:**

- Practice reading all questions first, set timeboxes per task (~9 mins/task)[github](https://github.com/ive663/RHCSA)
    
- Get used to skipping tough tasks and returning later
    

**Free Resources:**

- The Linux Command Line (William Shotts): [https://linuxcommand.org/tlcl.php](https://linuxcommand.org/tlcl.php)
    
- Run vimtutor for hands-on vim practice
    

---

## Phase 2: Storage Management (Weeks 4-5)

**Objective:** Partition disks, manage filesystems, and practice LVM

## Topics

- **Partitioning:** Create MBR/GPT partitions with parted
    
- **Filesystems:** mkfs.xfs, mkfs.ext4
    
- **Mounting:** /etc/fstab configuration, mount/umount, understanding UUIDs/labels
    
- **Swap:** Creating swap partitions/files
    
- **LVM:** pvcreate, vgcreate, lvcreate; lvextend, resize2fs, xfs_growfs; troubleshooting LVM boot failures; snapshot/backup LVs
    
- **Stratis:** (Now mandatory) Creating, managing Stratis pools, filesystems[pluralsight](https://www.pluralsight.com/resources/blog/cloud/how-to-prepare-for-the-rhcsa-ex200-exam)
    
- Add virtual disks in VMs for repeated hands-on practice
    

**Free Resources:**

- RHEL Storage Admin Guide: [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html-single/storage_administration_guide/](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html-single/storage_administration_guide/)
    

---

## Phase 2.5: Flatpak & Modern Package Management (NEW, Required for RHEL 10)

**Objective:** Manage software using both RPM/YUM/DNF and Flatpak (new requirement!)

## Topics

- **Flatpak Management:** Install and configure Flatpak, add Flatpak repos, install/remove Flatpak apps[redhat+2](https://www.redhat.com/en/services/training/ex200-red-hat-certified-system-administrator-rhcsa-exam)
    
- **RPM Management:** Continue DNF/YUM practice, group installs, repository config (including Flatpak repos)
    
- **Flatpak vs RPM:** Understand use-cases, troubleshooting, integration
    

**Free Resources:**

- Flatpak: [https://flatpak.org/](https://flatpak.org/)
    

---

## Phase 3: Networking & Secure Access (Week 6)

**Objective:** Configure and troubleshoot network settings; set up SSH securely

## Topics

- **Network Config:** nmcli for IP, mask, gateway, DNS; connection file editing in /etc/NetworkManager/system-connections; IPv6 configs; bond/team interfaces (note teamd deprecation in RHEL 10)[linkedin](https://www.linkedin.com/posts/samir-syed-37b27477_rhel-redhat10-linuxadministration-activity-7317132881758183425-E_Vu)
    
- **Troubleshooting:** ping, ss, ip addr, ip route, hostnamectl, dig/nslookup
    
- **SSH:** Setup key-based authentication, edit /etc/ssh/sshd_config, disable root login, test connectivity
    
- **Review advanced man/apropos searches for networking**
    

**Free Resources:**

- nmcli Cheat Sheet: [https://access.redhat.com/articles/2449441](https://access.redhat.com/articles/2449441)
    

---

## Phase 4: System Administration Deep Dive (Weeks 7-8)

**Objective:** Master process management, systemd, software, scheduling, kernel tuning

## Topics

- **Scheduling:** cron (system and user), at for one-off jobs; write from memory
    
- **Software:** DNF package management, repos (including local and GPG), Flatpak integration
    
- **Systemd:** systemctl (start/stop/status/enable/disable/mask), analyze boot/service failures, manage targets, create custom units, analyze with journalctl (log filtering)
    
- **Kernel Tuning:** sysctl (temporary), /etc/sysctl.d/ (persistent)
    
- **Documentation:** Use man, info, /usr/share/doc, practice advanced lookups[learn.redhat](https://learn.redhat.com/t5/Platform-Linux/EX200-RHCSA-Documentation-during-exam/td-p/13343)
    

**Free Resources:**

- RHEL SysAdmin's Guide: [https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html-single/system_administrators_guide/](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html-single/system_administrators_guide/)
    

---

## Phase 5: Advanced Admin (Weeks 9-10)

**Objective:** Security, firewall, (containers if RHEL 9), scripting

## Topics (Check version – containers may not be tested in RHEL 10)

- **SELinux:** run in enforcing mode, label management with restorecon/chcon, port context with semanage, manage Booleans (policy diagnosis not tested in RHEL 10)
    
- **Firewalld:** Allow/deny services, ports, runtime vs permanent changes
    
- **Containers/Podman:** (RHEL 9 only) podman run/start/stop/list, service integration, troubleshooting basic container issues[qtechbabble.wordpress](https://qtechbabble.wordpress.com/2024/07/07/rhcsa-9-exam-study-points-manage-containers/)youtube
    
- **Shell Scripting:** Shebang, variables, if/else, loops, write scripts that automate series of commands
    

**Free Resources:**

- SELinux guide: [https://opensource.com/business/13/11/selinux-policy-guide](https://opensource.com/business/13/11/selinux-policy-guide)
    
- Podman: [https://podman.io/getting-started/](https://podman.io/getting-started/)
    

---

## Phase 6: Troubleshooting, Integration, and Simulated Practice (Weeks 11-12+)

**Objective:** Practice under exam conditions, integrate all skills, focus on performance

## Activities

- **Recreate Exam Environment:** Minimal install, no GUI, all command line (simulate blackout documentation)
    
- **Practice Exams:** Use community scenarios and GitHub labs; always perform, not just read[github+1](https://github.com/aggressiveHiker/rhcsa9)
    
- **Troubleshooting:** Boot recovery (root password reset, fstab errors, LVM issues, network failures), service failures, SELinux denials, Flatpak issues, repo/config failures
    
- **Verification:** Check your work immediately after every task
    
- **Time Pressure:** Time-box every lab. Skip and revisit difficult problems.
    
- **Documentation Practice:** Use only what’s available on the system (man, info, /usr/share/doc)
    
- **Resources:** RHCSA practice repos on GitHub, Red Hat interactive labs, Linux blogs
    

**Key Skills to Master:**

- Root password recovery (boot interruption)
    
- Diagnosing non-booting systems (storage/network/service issues)
    
- Creating complex LVM setups quickly
    
- Writing and troubleshooting cron jobs from memory
    
- Comprehensive man/info page search strategies
    

**Advice from Successful Candidates:**

- 90% practice, 10% reading/documentation[substack+2](https://substack.com/home/post/p-160306310)
    
- Join online study groups/forums for tips
    
- Peer lab sessions for mutual feedback
    
- Build verification and troubleshooting into all workflows
    
---
