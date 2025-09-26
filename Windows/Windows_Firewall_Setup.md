# Windows Firewall Setup

## Overview

In this task, we configured and tested firewall rules on **Windows** using PowerShell. The goal was to understand how inbound and outbound traffic can be controlled and how to test the rules we applied. All screenshots are referenced in their respective folders.

## Firewall Rules Implemented

We implemented the following rules:

### Inbound Rules:

1. **Block Telnet (Port 23)**
2. **Block HTTP (Port 80)**
3. **Allow HTTPS (Port 443)**
4. **Block RDP (Port 3389)**

### Outbound Rules:

5. **Block SMTP (Port 25)**
6. **Block traffic to specific IP (123.45.67.89)**

### ICMP Rule:

* **Block inbound Ping (ICMP Echo Request)**

## Step-by-Step Setup (PowerShell)

### 1. Backup Firewall Configuration

```powershell
netsh advfirewall export "C:\Temp\firewall-backup-before.wfw"
```

* Screenshot: `Creating screenshots/Before changes.png`

### 2. Adding Rules

```powershell
# Inbound Rules
New-NetFirewallRule -DisplayName "TF4_Block_Telnet_In" -Direction Inbound -Action Block -Protocol TCP -LocalPort 23 -Profile Any
New-NetFirewallRule -DisplayName "TF4_Block_HTTP_In" -Direction Inbound -Action Block -Protocol TCP -LocalPort 80 -Profile Any
New-NetFirewallRule -DisplayName "TF4_Allow_HTTPS_In" -Direction Inbound -Action Allow -Protocol TCP -LocalPort 443 -Profile Any
New-NetFirewallRule -DisplayName "TF4_Block_RDP_In" -Direction Inbound -Action Block -Protocol TCP -LocalPort 3389 -Profile Any

# Outbound Rules
New-NetFirewallRule -DisplayName "TF4_Block_SMTP_Out" -Direction Outbound -Action Block -Protocol TCP -RemotePort 25 -Profile Any
New-NetFirewallRule -DisplayName "TF4_Block_OutTo_123.45.67.89" -Direction Outbound -Action Block -RemoteAddress 123.45.67.89 -Profile Any

# ICMP (Ping) Block
New-NetFirewallRule -DisplayName "TF4_Block_ICMP_In" -Direction Inbound -Protocol ICMPv4 -Action Block -Profile Any
```

* Screenshots:

  * `Creating screenshots/Created rules.png`
  * `Creating screenshots/Creating firewall rules.png`
  * `Creating screenshots/new inbound created rules.png`
  * `Creating screenshots/New outbound created rules.png`

### 3. Verify Rules

```powershell
Get-NetFirewallRule -DisplayName "TF4_*" | Format-Table DisplayName,Direction,Enabled,Action
```

### 4. Testing Rules

* HTTP block: `Testing screenshots/HTTP block.png` → Could not connect to server
* HTTPS block: `Testing screenshots/HTTPS block.png` → Connection allowed
* ICMP block: `Testing screenshots/ICMP block.png` → Ping failed / timeout
* Outbound block to 123.45.67.89: `Testing screenshots/Outbound block to 123.45.67.89.png` → Connection failed
* RDP block: `Testing screenshots/RDP block.png` → Connection failed
* SMTP block: `Testing screenshots/SMTP block.png` → Connection failed
* Telnet block: `Testing screenshots/Telnet block.png` → Connection timed out

### 5. Export Final Configuration

```powershell
netsh advfirewall export "C:\Temp\firewall-after-TF4.wfw"
```

* File: `firewall-after-TF4.wfw`

### 6. Cleanup / Restore

* Remove rules manually:

```powershell
Get-NetFirewallRule -DisplayName "TF4_*" | Remove-NetFirewallRule
```

* Restoration screenshot: `Restoration screenshot/Deleting created rules.png`
* Backup file: `firewall-backup-before.wfw`

## Observations

* ICMP ping takes longer to timeout; this is expected.
* All rules worked as intended.
* RDP testing on Kali requires `rdesktop` or `xfreerdp`.
* Outbound blocks and SMTP rules verified successfully.

## Notes

* Perform tests in a sandbox/test environment.
* Run PowerShell as Administrator.
* Backup firewall before making changes.
* Rule names use `TF4_` prefix for Task rules.

## References

* PowerShell firewall commands documentation: [https://learn.microsoft.com/en-us/powershell/module/netsecurity/](https://learn.microsoft.com/en-us/powershell/module/netsecurity/)
* Windows Firewall overview: [https://learn.microsoft.com/en-us/windows/security/threat-protection/windows-firewall/windows-firewall-with-advanced-security](https://learn.microsoft.com/en-us/windows/security/threat-protection/windows-firewall/windows-firewall-with-advanced-security)
