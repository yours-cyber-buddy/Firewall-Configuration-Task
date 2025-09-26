# References from this Repo

You can find all step-by-step instructions, screenshots, and configuration files inside the repository:

--- 

- Windows Firewall setup: `/Windows/Windows_Firewall_Steps.md`  
- UFW (Linux) setup: `/Linux/UFW Steps.md`  
- Screenshots: `/Windows/Creating screenshots/`, `/Windows/Testing screenshots/`, `/Linux/Creating Screenshots/`, `/Linux/Testing screenshots/`  
- Configuration backups: `/Windows/firewall-after-TF4.wfw`, `/Windows/firewall-backup-before.wfw`


## References (Web)

This file lists all the references, documentation, and resources used while working on the Firewall Configuration Task. It is divided into two sections: resources used directly in the project, and additional learning resources.

---

## References Used in Repo

### Windows Firewall

* Microsoft Docs — [Windows Defender Firewall with Advanced Security Overview](https://learn.microsoft.com/en-us/windows/security/operating-system-security/network-security/windows-firewall/windows-firewall-with-advanced-security)
* PowerShell Reference — [NetSecurity Module (PowerShell)](https://learn.microsoft.com/en-us/powershell/module/netsecurity/?view=windowsserver2022-ps)
* Windows Firewall Export/Import rules: [Export or Import Firewall Policy](https://learn.microsoft.com/en-us/windows/security/operating-system-security/network-security/windows-firewall/configure-the-windows-firewall-to-allow-or-block-specific-programs)

### Linux (UFW)

* Ubuntu Community Docs — [UFW (Uncomplicated Firewall)](https://help.ubuntu.com/community/UFW)
* Ubuntu Server Security Guide — [UFW Quick Reference](https://ubuntu.com/server/docs/security-firewall)
* Kali Linux Tools — UFW package info: `sudo apt show ufw`

### General Firewall & Networking

* IANA Port Numbers List — [Service Name and Transport Protocol Port Number Registry](https://www.iana.org/assignments/service-names-port-numbers/service-names-port-numbers.xhtml)
* Nmap Documentation — [Nmap Reference Guide](https://nmap.org/book/man.html)
* Netcat basics (for testing connections) — [Netcat Cheat Sheet](https://www.sans.org/blog/netcat-the-swss-army-knife/)

---

## Additional Learning Resources (Optional)

* Understanding Stateful vs Stateless Firewalls — [Firewall Basics](https://www.cisco.com/c/en/us/products/security/firewalls/what-is-a-firewall.html)
* Inbound vs Outbound Rules Explanation — [Network Security Concepts](https://www.varonis.com/blog/inbound-outbound-firewall-rules)
* Common Firewall Mistakes & Best Practices — [SANS Network Security](https://www.sans.org/white-papers/)
* Tutorials for Linux Firewall Management — [Linuxize UFW Guide](https://linuxize.com/post/ufw-commands/)
