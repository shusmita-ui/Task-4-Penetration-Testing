# John the Ripper - Password Cracking

## 1. Objective

To demonstrate password hash extraction and offline password cracking using John the Ripper in the authorized Metasploitable2 laboratory environment.

---

## 2. Target Information

- Target: Metasploitable2
- Target IP: `192.168.133.128`
- Tool: John the Ripper
- Wordlist: `rockyou.txt`

---

## 3. Collecting Password Files

On the Metasploitable2 system, the password database files were copied for the authorized lab exercise:

```bash
cat /etc/passwd > /tmp/passwd.txt
cat /etc/shadow > /tmp/shadow.txt

The files were then copied to the msfadmin user's home directory so they could be transferred to the Kali machine.


4. Transferring Files to Kali

The files were transferred using SCP:

scp -o HostKeyAlgorithms=+ssh-rsa msfadmin@192.168.133.128:/home/msfadmin/passwd.txt .
scp -o HostKeyAlgorithms=+ssh-rsa msfadmin@192.168.133.128:/home/msfadmin/shadow.txt .
5. Creating the Hash File

The /etc/passwd and /etc/shadow files were combined using unshadow:

unshadow passwd.txt shadow.txt > hashes.txt

This generated the file:

hashes.txt
6. Cracking the Password Hashes

John the Ripper was executed using the RockYou wordlist:

john --wordlist=/usr/share/wordlists/rockyou.txt hashes.txt

To display the cracked passwords:

john --show hashes.txt
7. Results

John identified 7 MD5crypt password hashes.

The following 3 passwords were successfully cracked:

Username	Cracked Password
sys	batman
klog	123456789
service	service

Result:

3 password hashes cracked, 4 left

Therefore, 3 out of 7 password hashes were successfully cracked using the RockYou wordlist.

8. Security Impact

Weak passwords can be recovered through offline password-cracking attacks when password hashes are exposed.

Potential risks include:

Unauthorized account access
Credential reuse attacks
Privilege escalation
Data exposure
Further system compromise
9. Mitigation

Recommended security measures:

Use strong and unique passwords.
Avoid dictionary-based and predictable passwords.
Use secure password-hashing algorithms with appropriate salting.
Protect /etc/shadow and other credential stores.
Restrict privileged access.
Monitor authentication activity.
Change compromised passwords immediately.
Use multi-factor authentication where possible.
10. Conclusion

The exercise demonstrated how weak passwords can be recovered from exposed password hashes using an offline dictionary attack.

Strong passwords, secure password hashing, and proper protection of credential files are important for reducing password-cracking risks.

Disclaimer

This password-cracking exercise was performed only against the intentionally vulnerable Metasploitable2 virtual machine in an authorized cybersecurity laboratory environment.