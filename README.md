# Pickle-Rick-CTF
The Pickle Rick challenge/capture the flag


### Penetration Testing | Web Enumeration | Privilege Escalation

**Platform:** TryHackMe  
**Room:** [Pickle Rick](https://tryhackme.com/room/picklerick)  
**Difficulty:** Easy  
**Status:** Completed ✅  
**Author:** PH

---

## Overview

This repository documents my first Capture The Flag (CTF) challenge on TryHackMe.

The objective was to investigate a vulnerable web server, identify exposed information, gain access to the application and locate three hidden ingredients.

The challenge allowed me to practice reconnaissance, web enumeration, Linux commands and privilege escalation.

## 🛠️ Tools & Technologies

- **Nmap:** Network reconnaissance and port scanning
- **Gobuster:** Web directory and file enumeration
- **Linux:** File system exploration and permission analysis
- **Firefox:** Web application inspection
- **Sudo:** Privilege enumeration

## Reconnaissance

I started by scanning the target using Nmap.

```bash
nmap -sS -O -vv -T2 TARGET_IP
```

The scan identified two open TCP ports:

| Port | Service |
|---|---|
| 22 | SSH |
| 80 | HTTP |

![NMAP] (NMAP.png)

The HTTP service became the primary focus of the investigation.

## 🌐 2. Web Enumeration

I inspected the website's HTML source code and discovered a username exposed in an HTML comment.

After that, I used Gobuster to discover accessible resources:

```bash
gobuster dir -u http://TARGET_IP \
-w /usr/share/wordlists/dirb/common.txt
```

The investigation revealed directories and files that provided additional clues.

## 🔐 3. Authentication

During the enumeration process, I found an exposed credential in a publicly accessible file.

Using the discovered information, I authenticated to the application's web portal.

**Security issue:** Sensitive Information Exposure.

## 💻 4. Command Execution

After authentication, I discovered a command execution panel.

I investigated the execution context with Linux commands:

```bash
whoami
pwd
ls -la
```

Some commands were restricted by the application.

However, alternative commands allowed me to continue inspecting accessible files.

## 📂 5. File System Enumeration

I explored the Linux file system to locate the hidden ingredients.

Commands used:

```bash
ls /home
ls -la /home/rick
grep . "filename"
```

This phase reinforced my understanding of Linux directories, file permissions and command execution.

## 🔓 6. Privilege Escalation

I investigated the current user's sudo permissions:

```bash
sudo -l
```

The configuration revealed that the web server user could execute commands as root without password authentication.

This represented a serious privilege-management weakness.

## 🧠 Key Takeaways

- Understanding Nmap results before proceeding with enumeration
- Identifying exposed information in web applications
- Discovering directories and files with Gobuster
- Understanding Linux file permissions
- Investigating sudo misconfigurations
- Following evidence instead of randomly executing tools

## 🏁 Conclusion

Pickle Rick was my first completed TryHackMe CTF.

The challenge helped me connect theoretical cybersecurity knowledge with practical penetration testing techniques.

It also reinforced the importance of enumeration, patience, and understanding why each command is used.

**Room:** https://tryhackme.com/room/picklerick

---

*All techniques were performed in an authorized TryHackMe laboratory environment for educational purposes.*
