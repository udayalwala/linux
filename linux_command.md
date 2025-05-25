
# 🐧 Advance Linux Commands Cheatsheet

> A comprehensive and practical collection of advanced Linux commands for developers, sysadmins, and DevOps engineers.

---

## 📚 Table of Contents

1. [Disk Usage](#1-disk-usage)  
2. [Enable Password Authentication for SSH](#2-enable-password-authentication-for-ssh)  
3. [awk — Powerful Text Processing](#3-awk--powerful-text-processing)  
4. [tmux — Terminal Multiplexer](#4-tmux--terminal-multiplexer)  
5. [dig — DNS Lookup](#5-dig--dns-lookup)  
6. [watch — Run Command Repeatedly](#6-watch--run-command-repeatedly)  
7. [chattr — Change File Attributes](#7-chattr--change-file-attributes)  
8. [sed — Stream Editor](#8-sed--stream-editor)  
9. [kubectl cp — Kubernetes File Copy](#9-kubernetes-kubectl-cp)  
10. [sort & uniq — Sort and Remove Duplicates](#10-sort--uniq--sort-and-remove-duplicates)  
11. [tee — Output to File & Terminal](#11-tee--output-to-file--terminal)  
12. [Find & Delete Old Files](#12-find--delete-files-older-than-15-days)  
13. [jq — JSON Processor](#13-jq--json-processor)  
14. [Networking Commands](#14-networking-commands)  
15. [lsof — List Open Files](#15-lsof--list-open-files)  
16. [nc — Port Testing](#16-nc-netcat--port-testing)  
17. [rsync — Remote File Sync](#17-rsync--remote-file-sync)  
18. [xargs — Build Commands from Input](#18-xargs--build-command-lines-from-input)  
19. [journalctl — View Logs](#19-journalctl--view-logs)  
20. [tcpdump — Capture Packets](#20-tcpdump--capture-packets)  
21. [crontab — Schedule Jobs](#21-crontab--schedule-jobs)  
22. [Kubernetes Pod Resource Usage](#22-kubernetes-pod-resource-usage)  
23. [System Info Commands](#23-system-info-commands)  
24. [File & Permission Commands](#24-file--permission-commands)  
25. [nohup — Background Tasks](#25-nohup--run-command-in-background)  
26. [User Management](#26-user-management)  
27. [Process Management](#27-process-management)  
28. [CPU Info](#28-cpu-info)  

---

## 1. Disk Usage
```bash
du -sh *
```
> Show human-readable disk usage summary of files and directories.

---

## 2. Enable Password Authentication for SSH
Edit the SSH configuration:
```bash
sudo vi /etc/ssh/sshd_config
```

Set the following:
```nginx
PasswordAuthentication yes
```

Restart the SSH service:
```bash
sudo systemctl restart sshd
```

---

## 3. awk — Powerful Text Processing

### 📄 Example 1: Print Specific Columns  
`employees.txt`:
```
John 28 Developer
Alice 32 Manager
Bob 25 Tester
```
```bash
awk '{print $1, $3}' employees.txt
```

Output:
```
John Developer
Alice Manager
Bob Tester
```

---

### 🧩 Example 2: Match a Pattern  
`logs.txt`:
```
INFO Starting service
ERROR Disk full
INFO Service running
ERROR Memory leak
```
```bash
awk '/ERROR/' logs.txt
```

Output:
```
ERROR Disk full
ERROR Memory leak
```

---

### 🧮 Example 3: Using CSV Separator  
`data.csv`:
```
John,Developer,50000
Alice,Manager,70000
Bob,Tester,40000
```
```bash
awk -F',' '{print $1, $3}' data.csv
```

Output:
```
John 50000
Alice 70000
Bob 40000
```

---

## 4. tmux — Terminal Multiplexer
```bash
tmux new -s mysession
```
> Create and manage multiple terminal sessions.

---

## 5. dig — DNS Lookup
```bash
dig google.com +short
```

---

## 6. watch — Run Command Repeatedly
```bash
watch -n 2 df -h
```
> Runs `df -h` every 2 seconds.

---

## 7. chattr — Change File Attributes
```bash
chattr +i important.txt
```
> Make file immutable (protect from changes/deletion).

---

## 8. sed — Stream Editor
```bash
sed -i 's/foo/bar/g' file.txt
```
> Replace all occurrences of `foo` with `bar`.

---

## 9. Kubernetes `kubectl cp`
Copy files between Kubernetes pods and your local system:

➡️ Pod → Local:
```bash
kubectl cp -n <namespace> <pod-name>:<path> <local-destination>
```

⬅️ Local → Pod:
```bash
kubectl cp -n <namespace> <local-source> <pod-name>:<path>
```

Example:
```bash
kubectl cp mynginx:/usr/share/nginx/html/index.html ~/index.html
kubectl cp ~/index.html mynginx:/usr/share/nginx/html/index.html
```

---

## 10. sort & uniq — Sort and Remove Duplicates

`fruits.txt`:
```
apple
banana
orange
apple
banana
grape
```
```bash
sort fruits.txt | uniq
```

Output:
```
apple
banana
grape
orange
```

---

## 11. tee — Output to File & Terminal
```bash
echo "Hello, welcome!" | tee output.txt
echo "uday" | tee -a output.txt
cat output.txt
```

Output:
```
Hello, welcome!
uday
```

---

## 12. Find & Delete Files Older Than 15 Days
```bash
find /opt/opendj/logs/ -type f -name "errors.*" -mtime +15 -delete
```
Or:
```bash
find /opt/opendj/logs/ -type f -name "errors.*" -mtime +15 -exec rm -f {} \;
```

---

## 13. jq — JSON Processor

Pretty print:
```bash
jq . data.json
```

Sample JSON:
```json
{
  "name": "Alice",
  "age": 30,
  "skills": ["bash", "python", "jq"],
  "address": {
    "city": "New York",
    "zip": "10001"
  }
}
```

Extract fields:
```bash
jq '.name' data.json
jq '.address.city' data.json
jq '{person: .name, location: .address.city}' data.json
```

---

## 14. Networking Commands

- **netstat** — View network connections  
  ```bash
  netstat -tuln
  ```

- **telnet** — Test connectivity  
  ```bash
  telnet example.com 80
  ```

- **dmesg** — Kernel ring buffer  
  ```bash
  dmesg
  ```

- **ping** — Test reachability  
  ```bash
  ping -c 4 google.com
  ```

- **traceroute** — Trace packet path  
  ```bash
  traceroute example.com
  ```

---

## 15. lsof — List Open Files
```bash
lsof -i :80
```

---

## 16. nc (Netcat) — Port Testing
```bash
nc -zv 192.168.1.10 22
```

---

## 17. rsync — Remote File Sync
```bash
rsync -avz /src/ user@host:/dest/
```

---

## 18. xargs — Build Command Lines from Input
```bash
find /var/log -name "*.log" | xargs grep "ERROR"
ls *.txt | xargs gzip
```

---

## 19. journalctl — View Logs
```bash
journalctl -u jenkins.service --since "1 hour ago"
```

---

## 20. tcpdump — Capture Packets
```bash
sudo tcpdump -i eth0 port 80
```

---

## 21. crontab — Schedule Jobs
```bash
crontab -e
```

---

## 22. Kubernetes Pod Resource Usage
```bash
kubectl top pods
```

---

## 23. System Info Commands

- **uptime** — Load average  
  ```bash
  uptime
  ```

- **stat** — File metadata  
  ```bash
  stat /var/log/syslog
  ```

- **vmstat** — Memory stats  
  ```bash
  vmstat 2 5
  ```

- **free** — Memory usage  
  ```bash
  free -h
  ```

---

## 24. File & Permission Commands

- Mount filesystem:  
  ```bash
  sudo mount /dev/sdb1 /mnt/usb
  ```

- Change permissions:  
  ```bash
  chmod 755 script.sh
  ```

- Change ownership:  
  ```bash
  sudo chown john:john /var/www/index.html
  ```

---

## 25. nohup — Run Command in Background
```bash
nohup ./long_script.sh &
```

---

## 26. User Management

- Add user:  
  ```bash
  sudo useradd -m -s /bin/bash devops
  ```

- Set password:  
  ```bash
  sudo passwd devops
  ```

- Delete user:  
  ```bash
  sudo userdel -r devops
  ```

- Add to group:  
  ```bash
  sudo usermod -aG docker devops
  ```

---

## 27. Process Management
```bash
ps aux | less
```

---

## 28. CPU Info
```bash
lscpu
```

---
