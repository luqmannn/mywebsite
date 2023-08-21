---
title: Powershell cheat sheet
type: page
description: Powershell cheat sheet for IT support
topic: powershell command
---

## Network command

### Reset the TCP/IP configuration back to its default setting
This command is helpful in cases where you are experiencing network connectivity issues due to misconfigured network settings. Keep in mind that resetting the TCP/IP stack will remove any custom network configurations you may have made, including static IP addresses and custom DNS settings. Restarting the computer is required before the default settings take effect.
```
netsh int ip reset
```
```
netsh int ipv6 reset
```

### Reset the Windows Firewall settings back to their default configuration​
Windows command that can be used to reset the Windows Firewall settings back to their default configuration. This command is useful if you are experiencing issues with the Windows Firewall, or if you suspect that your current firewall rules may be causing network connectivity problems. Keep in mind that resetting the Windows Firewall will remove any custom rules or settings you may have configured.
```
netsh advfirewall reset
```
​
### Resets Winsock Catalog to a clean state. 
It will reset the Winsock catalog and may resolve various network-related issues, such as internet connection problems, network errors, and socket-related errors. It is often used as a troubleshooting step when you are experiencing network connectivity problems that are not related to the Windows Firewall or TCP/IP settings. It's always a good idea to create a backup or a system restore point. This precaution can help you revert to a stable state in case anything goes wrong during the process.
```
netsh winsock reset
```
​
### Diagnose and Repair
- These commands should do the same things as the 'Diagnose and Repair' for the network adapter, but is WAY faster!
```
ipconfig /release
ipconfig /renew
arp -d *
nbtstat -R
nbtstat -RR
ipconfig /flushdns
ipconfig /registerdns
```

### Show Wifi password
```
netsh wlan show profile "<wifi-name>" key=clear | findstr Key
```
```
netsh wlan show profile "<wifi-name>" key=clear | Select-String "Key Content|Authentication|Cipher"
```
​
## System command

### List all command history
```
Get-Content (Get-PSReadlineOption).HistorySavePath
```

### Get SHA-256 hash from a file
```
Get-FileHash .\ventoy-1.0.93-windows.zip | Format-List
```

### From SHA-256 hash, do verfication of file integrity
```
$filehash=Get-FileHash .\ventoy-1.0.93-windows.zip
$filehash.hash
$filehash.hash -eq "2e887f24ace92596d5b7b9c21eabc8f9065bfaf43d27833bf0eac96da390114c"
```
- Putting everything together in one-liner as future reference.
```
(Get-FileHash .\ventoy-1.0.93-windows.zip).hash -eq "2e887f24ace92596d5b7b9c21eabc8f9065bfaf43d27833bf0eac96da390114c"
```