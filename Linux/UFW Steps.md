# UFW Steps - Linux (Kali) - Task 4

## Overview

I installed and configured **UFW** (Uncomplicated Firewall) on my Kali VM and added a set of inbound and outbound rules to harden the machine for scanning work. I did this on a fresh Kali install (I installed Kali a few days ago and UFW was not present). After installing UFW it had no custom rules — only the default policy: **deny incoming, allow outgoing**. I configured several rules, tested outbound rules locally (because I didn’t have a second machine for inbound testing), and captured screenshots for proof.

---

## What I installed and environment

* Installed UFW using apt: `sudo apt install ufw -y`
* UFW status before changes: `Status: active` with default `deny (incoming), allow (outgoing)` and no custom rules.

Screenshots saved to: `Linux/Creating Screenshots/UFW status.png`

---

## Rules I configured

I added the following UFW rules. I kept the system locked down because I use Kali for local scanning and tools only (no public web services hosted).

### Inbound rules (deny incoming)

1. `sudo ufw deny in 23/tcp`  — Block Telnet
2. `sudo ufw deny in 21/tcp`  — Block FTP
3. `sudo ufw deny in 3389/tcp` — Block RDP (if any RDP service is exposed)
4. `sudo ufw deny in 137:139/tcp` — Block NetBIOS/NetBIOS-SSN range
5. `sudo ufw deny in 445/tcp` — Block SMB
6. `sudo ufw deny in 25/tcp` — Block SMTP inbound (if not running mail server)

### Outbound rules (deny outgoing)

7. `sudo ufw deny out 25/tcp` — Block outbound SMTP
8. `sudo ufw deny out 23/tcp` — Block outbound Telnet
9. `sudo ufw deny out to 123.45.67.89` — Block outbound to specific IP (demo)

> Note: UFW automatically created IPv6 versions of these rules as well on my system.

Screenshots of the rule list: `Linux/Creating Screenshots/All created rules.png` and `Linux/Creating Screenshots/Indbound deny rules.png` and  `Linux/Creating Screenshots/Outbound deny rules.png` .

---

## Step-by-step commands I ran

> Run each command in a terminal on the Kali VM.

```bash
# install
sudo apt update
sudo apt install ufw -y

# enable (if not already)
sudo ufw enable

# inbound deny rules
sudo ufw deny in 23/tcp
sudo ufw deny in 21/tcp
sudo ufw deny in 3389/tcp
sudo ufw deny in 137:139/tcp
sudo ufw deny in 445/tcp
sudo ufw deny in 25/tcp

# outbound deny rules
sudo ufw deny out 25/tcp
sudo ufw deny out 23/tcp
sudo ufw deny out to 123.45.67.89

# check rules (numbered list)
sudo ufw status numbered

# check verbose status
sudo ufw status verbose
```

---

## Testing (what I tested and how)

I could only reliably test **outbound** rules from the Kali VM (because I didn’t have another machine ready to test inbound). For each outbound test I ran commands and saved the terminal output as screenshots in `Linux/Testing screenshots/`.

### Outbound tests I ran locally

* **Outbound SMTP (port 25) test** — expected: fail

  ```bash
  telnet 192.168.31.2 25
  ```

  Screenshot: `Linux/Testing screenshots/SMTP check.png`

* **Outbound Telnet (port 23) test** — expected: fail

  ```bash
  nc -vz 192.168.31.2 23
  ```

  reenshot: `Linux/Testing screenshots/Telnet check.png`

* **Outbound to specific IP** — expected: fail

  ```bash
  curl  http://123.45.67.89
  ```

  Screenshot: `Linux/Testing screenshots/Outbound to specific ip check.png`

---

## Inbound testing note

I did not have another VM or machine on the same network to reliably test inbound blocks (UFW does not block loopback). When I get another test machine, the inbound tests to verify Telnet/FTP/RDP/SMB/SMTP blocking will be performed and screenshots will be added.

---

## Cleanup & restore

If you want to remove the rules which are aleady added or reset UFW:

```bash
# delete specific numbered rule
sudo ufw status numbered
sudo ufw delete <rule-number>

# or reset everything 
sudo ufw reset
sudo ufw enable
```

## Observations

* UFW made it quick to add deny rules for common insecure services.
* Outbound rules behaved as expected blocked outgoing connections to SMTP/Telnet/demonstration IP.
* IPv6 duplicates were auto-created on my system.

---

## Notes / Tips

* Keep default `deny incoming` and `allow outgoing` unless you want very strict egress control.
* Be careful when enabling UFW on a remote machine enable SSH access first if you need remote admin.
* Use `sudo ufw status numbered` often so you can delete rules by number if needed.

---

## References

* UFW manual: [https://help.ubuntu.com/community/UFW](https://help.ubuntu.com/community/UFW)
* UFW commands quick ref[erence: ](https://ubuntu.com/server/docs/security-firewall)[https://ubuntu.com/server/docs/security-firewall](https://ubuntu.com/server/docs/security-firewall)
