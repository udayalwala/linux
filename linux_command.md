
# Advance Linux Commands Cheatsheet

---

## 1. Disk Usage
```bash
du -sh *
```
Show human-readable disk usage summary of files and directories.

---

## 2. Enable Password Authentication for SSH
Edit the SSH configuration:
```bash
sudo vi /etc/ssh/sshd_config
```
Set:
```nginx
PasswordAuthentication yes
```
Restart SSH:
```bash
sudo systemctl restart sshd
```

---

## 3. awk — Powerful Text Processing

### Example 1: Print Specific Columns  
`employees.txt`:
```
John 28 Developer
Alice 32 Manager
Bob 25 Tester
```
Command:
```bash
awk '{print $1, $3}' employees.txt
```
Output:
```
John Developer
Alice Manager
Bob Tester
```

### Example 2: Match a Pattern  
`logs.txt`:
```
INFO Starting service
ERROR Disk full
INFO Service running
ERROR Memory leak
```
Command:
```bash
awk '/ERROR/' logs.txt
```
Output:
```
ERROR Disk full
ERROR Memory leak
```

### Example 3: Using Custom Field Separator (CSV)  
`data.csv`:
```
John,Developer,50000
Alice,Manager,70000
Bob,Tester,40000
```
Command:
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
Manage multiple terminal sessions easily.

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
Runs `df -h` every 2 seconds.

---

## 7. chattr — Change File Attributes
```bash
chattr +i important.txt
```
Make file immutable (cannot be changed or deleted).

---

## 8. sed — Stream Editor
```bash
sed -i 's/foo/bar/g' file.txt
```
Replace all “foo” with “bar” in the file.

---

## 9. Kubernetes `kubectl cp`
Copy files between Kubernetes pods and local system:

Pod → Local:
```bash
kubectl cp -n <namespace> <pod-name>:<path> <local-destination>
```

Local → Pod:
```bash
kubectl cp -n <namespace> <local-source> <pod-name>:<path>
```

Example:
```bash
kubectl cp mynginx-ff886775c-mzjz2:/usr/share/nginx/html/index.html /home/uday/index.html
kubectl cp /home/uday/index.html mynginx-ff886775c-mzjz2:/usr/share/nginx/html/index.html
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
Command:
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
Write output to a file **and** display it on the terminal:
```bash
echo "Hello, welcome!" | tee output.txt
```
Append another line:
```bash
echo "uday" | tee -a output.txt
```
Check file content:
```bash
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
Or using `rm`:
```bash
find /opt/opendj/logs/ -type f -name "errors.*" -mtime +15 -exec rm -f {} \;
```

---

## 13. jq — JSON Processor
Pretty-print JSON:
```bash
cat data.json | jq .
```

Example JSON:
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

Extract a top-level key:
```bash
jq '.name' data.json
```
Output:
```
"Alice"
```

Extract nested keys:
```bash
jq '.address.city' data.json
```
Output:
```
"New York"
```

Combine multiple fields:
```bash
jq '{person: .name, location: .address.city}' data.json
```

---

## 14. Networking Commands

### netstat — Show Network Connections
```bash
netstat -tuln
```

### telnet — Network Testing Tool
```bash
telnet example.com 80
```

### dmesg — Kernel Logs
Displays kernel ring buffer messages:
```bash
dmesg
```

### ping — Test Network Reachability
```bash
ping -c 4 google.com
```

### traceroute — Trace Network Path
```bash
traceroute example.com
```

---

## 15. lsof — List Open Files
List open files on port 80:
```bash
lsof -i :80
```

---

## 16. nc (Netcat) — Port Testing
Test if port 22 (SSH) is open:
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

### uptime — System Load Average
```bash
uptime
```

### stat — File Metadata
```bash
stat /var/log/syslog
```

### vmstat — Virtual Memory Stats
```bash
vmstat 2 5
```

### free — Memory Usage
```bash
free -h
```

---

## 24. File & Permission Commands

### mount — Mount Filesystem
```bash
sudo mount /dev/sdb1 /mnt/usb
```

### chmod — Change File Permissions
```bash
chmod 755 script.sh
```

### chown — Change File Owner
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

### Add User
```bash
sudo useradd -m -s /bin/bash devops
```

### Set Password
```bash
sudo passwd devops
```

### Delete User
```bash
sudo userdel -r devops
```

### Modify User (Add to Group)
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
