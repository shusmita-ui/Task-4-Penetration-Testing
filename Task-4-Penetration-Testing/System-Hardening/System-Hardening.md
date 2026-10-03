# System Hardening

## 1. Objective

To improve the security of the Kali Linux laboratory system by applying security updates, configuring a firewall, and disabling an unnecessary service.

---

## 2. Security Updates

First, the package repository information was updated:

```bash
sudo apt update

Available package upgrades were then installed:

sudo apt upgrade -y
Purpose

Regular security updates help protect the system against known vulnerabilities and outdated software.

3. Firewall Configuration

UFW (Uncomplicated Firewall) was configured to restrict incoming network connections.

Set the default incoming policy to deny:

sudo ufw default deny incoming

Allow outgoing connections:

sudo ufw default allow outgoing

SSH access was allowed:

sudo ufw allow 22/tcp

The firewall was enabled:

sudo ufw enable

Firewall status was verified:

sudo ufw status verbose
Configuration Result

The firewall was active with:

Default incoming: DENY
Default outgoing: ALLOW
SSH port 22/tcp: ALLOW

This provides a basic layer of network access control.

4. Disabling an Unused Service

The ModemManager service was selected as an unnecessary service for this VMware-based laboratory environment.

The service was stopped:

sudo systemctl stop ModemManager

The service was disabled from starting automatically:

sudo systemctl disable ModemManager

Its status was checked:

systemctl status ModemManager
Purpose

Disabling unnecessary services reduces the number of active components and can reduce the system's attack surface.

```
5. Hardening Measures Applied
Security Measure	Action
Security Updates	apt update and apt upgrade
Firewall	UFW enabled
Incoming Traffic	Default DENY
Outgoing Traffic	Default ALLOW
SSH	Port 22 allowed
Unused Service	ModemManager disabled
6. Security Benefits

The applied hardening measures help to:

Reduce exposure to known vulnerabilities
Restrict unnecessary incoming connections
Reduce the number of running services
Minimize the attack surface
Improve basic network security
7. Recommendations

Additional hardening measures that can be considered include:

Remove unnecessary packages and services.
Use strong authentication.
Disable unused network ports.
Regularly apply security updates.
Monitor system logs.
Use least-privilege access.
Regularly perform vulnerability assessments.
Keep production systems separate from testing environments.
8. Conclusion

System hardening was performed by applying security updates, configuring UFW firewall rules, and disabling an unnecessary service.

These measures provide basic protection by reducing the attack surface and controlling network access.

Disclaimer

The hardening activities were performed on the authorized Kali Linux laboratory system used for the cybersecurity practical.