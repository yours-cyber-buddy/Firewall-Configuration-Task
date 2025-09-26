# Firewall Configuration Task (Windows & Linux)

## Overview

In this task, I configured and tested firewalls on both **Windows** and **Linux (Kali)** systems. The goal was to learn **basic firewall management**, create **inbound and outbound rules**, and understand how a firewall **filters network traffic**.

> ⚠ Note: This work was done in a sandbox environment on virtual machines. Never perform these steps on production systems or networks without proper permission.

---

## Purpose & Objectives

**Purpose:**

* Learn to configure firewalls on Windows and Linux.
* Understand how firewalls block or allow network traffic.

**Objectives:**

* Configure inbound and outbound rules.
* Test rules to confirm traffic filtering.
* Document the process and results with screenshots.
* Maintain backups for restoration.

---

## Environment & Setup

### Windows VM

* Used **PowerShell** for all firewall configurations.
* Screenshots and backups saved in `/Windows/` folder.
* All steps and commands documented in `Windows_Firewall_Steps.md`.

### Linux VM (Kali)

* Installed and configured **UFW (Uncomplicated Firewall)**.
* Screenshots saved in `/Linux/Creating Screenshots/` and `/Linux/Testing screenshots/`.
* Steps documented in `UFW Steps.md`.

> Screenshots, configuration files, and proof of commands are all included in the repository folders for reference.

---

## Step-by-Step Workflow

### Windows Firewall

1. Open PowerShell as Administrator.
2. Backup existing firewall rules: `firewall-backup-before.wfw`
3. Create inbound rules to block common insecure services:

   * Telnet (23)
   * FTP (21)
   * RDP (3389)
   * NetBIOS (137-139)
   * SMB (445)
   * SMTP (25)
4. Create outbound rules for demonstration/testing:

   * SMTP (25)
   * Telnet (23)
   * Outbound to specific IP (123.45.67.89)
5. Test each rule and capture results.
6. Restore firewall using backup if needed.
7. Screenshots saved in `/Windows/Creating screenshots/`, `/Windows/Testing screenshots/`, and `/Windows/Restoration screenshot/`.

### Linux (Kali) - UFW

1. Install UFW: `sudo apt install ufw -y`
2. Enable UFW: `sudo ufw enable`
3. Check default policy: incoming denied, outgoing allowed.
4. Add inbound deny rules:

   * Telnet (23)
   * FTP (21)
   * RDP (3389)
   * NetBIOS range (137-139)
   * SMB (445)
   * SMTP (25)
5. Add outbound deny rules:

   * SMTP (25)
   * Telnet (23)
   * Outbound to specific IP (123.45.67.89)
6. Test outbound rules locally using commands like `telnet`, `nc`, `curl`.
7. Screenshots saved in `/Linux/Creating Screenshots/` and `/Linux/Testing screenshots/`.
8. Cleanup or reset: `sudo ufw reset` if needed.

---

## Observations & Notes

* Windows Firewall rules can be easily managed using PowerShell.
* UFW simplifies firewall configuration on Linux.
* Outbound and Inbound rules were successfully tested (inbound testing requires another machine).
* IPv6 rules are automatically added on both systems.
* Always verify rules with `status` and `status numbered` commands.
* Keep default policies unless stricter control is needed.

---

## Repository Structure

``/Firewall-Configuration-Task/ 
│
├── README.md                             # This file - explanation, steps, summary
│
├── /Windows/                             # Windows Firewall work
│   ├── Windows_Firewall_Steps.md
│   ├── Creating screenshots/
│   │   ├── Before changes.png
│   │   ├── Created rules.png
│   │   ├── Creating firewall rules.png
│   │   ├── new inbound created rules.png
│   │   ├── New outbound created rules.png
│   ├── Testing screenshots/
│   │   ├── HTTP block.png
│   │   ├── HTTPS block.png
│   │   ├── ICMP block.png
│   │   ├── Outbound block to 123.45.67.89.png
│   │   ├── RDP block.png
│   │   ├── SMTP block.png
│   │   ├── Telnet block.png
│   ├── Restoration screenshot/
│   │   ├── Deleting created rules.png
│   ├── firewall-after-TF4.wfw
│   ├── firewall-backup-before.wfw
│
├── /Linux/                               # Linux UFW work
│   ├── UFW Steps.md
│   ├── Creating Screenshots/
│   │   ├── All created rules.png
│   │   ├── Indbound deny rules.png
│   │   ├── Outbound deny rules.png
│   │   ├── UFW status.png
│   ├── Testing screenshots/
│   │   ├── Outbound to specific ip check.png
│   │   ├── SMTP check.png
│   │   ├── Telnet check.png
│
└── References.md``

---
## References

For all commands, configurations, and learning resources, see `References.md` in this repo.

