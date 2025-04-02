# Advanced Linux Scenario-Based Interview Questions

## 1. Debugging High CPU Usage on a Production Server

### **Scenario:**  
You receive an alert that a production server is running at **100% CPU usage**. How do you investigate and resolve the issue?

### **Solution Approach:**

#### **Check CPU Load:**
```bash
uptime
```

#### **Identify High CPU Processes:**
```bash
top
```
OR
```bash
ps aux --sort=-%cpu | head -5
```

#### **Check System-Wide Load:**
```bash
vmstat 1 10
```

#### **Analyze Process Behavior:**
```bash
strace -p <PID>
```

#### **Kill or Restart the Process (If Needed):**
```bash
kill -9 <PID>
```

#### **Investigate Logs:**
```bash
journalctl -xe
```

---

## 2. Disk Space is Full - How Do You Fix It?

### **Scenario:**  
A production server suddenly runs out of disk space. How do you identify and clean up unnecessary files?

### **Solution Approach:**

#### **Check Disk Usage:**
```bash
df -h
```

#### **Find Large Files & Directories:**
```bash
du -ah / | sort -rh | head -20
```

#### **Check Log Files:**
```bash
ls -lh /var/log
```
Truncate large logs:
```bash
echo "" > /var/log/syslog
```

#### **Find and Delete Old Files:**
```bash
find /var/log -type f -mtime +30 -exec rm -f {} \;
```

#### **Remove Unused Docker Images & Containers (If Applicable):**
```bash
docker system prune -a
```

---

## 3. Application Port is Not Listening

### **Scenario:**  
A web application running on **port 8080** is not accessible. How do you troubleshoot?

### **Solution Approach:**

#### **Check if the Process is Running:**
```bash
ps aux | grep java  # (or nginx, apache, etc.)
```

#### **Check if the Port is Open:**
```bash
netstat -tulnp | grep 8080
```
OR
```bash
ss -tulnp | grep 8080
```

#### **Check Firewall Rules:**
```bash
iptables -L -n | grep 8080
```

#### **Restart the Service:**
```bash
systemctl restart <service-name>
```

---

## 4. SSH Login is Failing

### **Scenario:**  
A user cannot SSH into a server. What steps do you take to troubleshoot?

### **Solution Approach:**

#### **Check SSH Service Status:**
```bash
systemctl status ssh
```

#### **Check Firewall Rules:**
```bash
iptables -L -n | grep 22
```

#### **Check SSH Configuration:**
```bash
cat /etc/ssh/sshd_config | grep -v '^#' | grep PermitRootLogin
```

#### **Check Authentication Logs:**
```bash
tail -50 /var/log/auth.log
```

---

## 5. How Do You Monitor System Performance in Real-Time?

### **Scenario:**  
Your manager asks you to monitor a Linux server’s real-time performance. What tools do you use?

### **Solution Approach:**

#### **Monitor CPU Usage:**
```bash
top
```
OR
```bash
htop
```

#### **Monitor Memory Usage:**
```bash
free -h
```

#### **Monitor Disk I/O:**
```bash
iostat -x 1 5
```

#### **Monitor Network Traffic:**
```bash
iftop
```

#### **Monitor Running Processes:**
```bash
ps aux --sort=-%mem | head -10
```

#### **Monitor Logs in Real-Time:**
```bash
tail -f /var/log/syslog
```

---

## 6. A Cron Job is Not Running – How Do You Fix It?

### **Scenario:**  
A scheduled cron job is not executing. How do you debug it?

### **Solution Approach:**

#### **Check if Cron Service is Running:**
```bash
systemctl status cron
```

#### **Verify Cron Job Entry:**
```bash
crontab -l
```

#### **Check Cron Logs:**
```bash
grep CRON /var/log/syslog
```

#### **Check User Permissions:**
```bash
ls -l /path/to/script.sh
```
Make script executable:
```bash
chmod +x /path/to/script.sh
```

#### **Run the Script Manually:**
```bash
/bin/bash /path/to/script.sh
```

---

## 7. How to Detect and Block Unauthorized SSH Login Attempts?

### **Scenario:**  
A server is under **brute-force SSH attack**. How do you secure it?

### **Solution Approach:**

#### **Check for Unauthorized SSH Login Attempts:**
```bash
grep "Failed password" /var/log/auth.log | wc -l
```

#### **Identify Malicious IPs:**
```bash
grep "Failed password" /var/log/auth.log | awk '{print $11}' | sort | uniq -c | sort -nr | head -10
```

#### **Block Malicious IPs Using iptables:**
```bash
iptables -A INPUT -s <IP> -j DROP
```

#### **Use Fail2Ban to Block Repeated Login Attempts:**
```bash
sudo apt install fail2ban -y
```

#### **Disable Root SSH Login:**
```bash
sed -i 's/PermitRootLogin yes/PermitRootLogin no/' /etc/ssh/sshd_config
systemctl restart sshd
```

---

This Markdown file contains **real-world Linux troubleshooting scenarios** for DevOps interviews. 🚀
