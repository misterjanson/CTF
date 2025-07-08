---
title: Credential Access Lab
menuTitle: Credential Access Lab
weight: 30
---

This lab will focus on understanding common techniques, and sub-techniques, used by attackers to access credentials on victim machines. 

### Tactic :gear:

**Credential Access** [ID:TA0006](https://attack.mitre.org/tactics/TA0006/)

The adversary is trying to steal account names and passwords.

Credential Access consists of techniques for stealing credentials like account names and passwords. Techniques used to get credentials include keylogging or credential dumping.

### Technique :bulb:

**OS Credential Dumping** [ID:T1003](https://attack.mitre.org/techniques/T1003/)

Adversaries may attempt to dump credentials to obtain account login and credential material, normally in the form of a hash or a clear text password. Credentials can be obtained from OS caches, memory, or structures. Credentials can then be used to perform Lateral Movement and access restricted information.

### Sub-Technique :bulb:

**LSASS Memory** [ID:T1003.001](https://attack.mitre.org/techniques/T1003/001/)

Adversaries may attempt to access credential material stored in the process memory of the Local Security Authority Subsystem Service (LSASS). After a user logs on, the system generates and stores a variety of credential materials in LSASS process memory. 

### Mitigation :stop_sign:

**Privileged Account Management** [ID:M1026](https://attack.mitre.org/mitigations/M1026/)

Do not put user or admin domain accounts in the local administrator groups across systems unless they are tightly controlled, as this is often equivalent to having a local administrator account with the same password on all systems. Follow best practices for design and administration of an enterprise network to limit privileged account use across administrative tiers. Solutions like [FortiPAM](https://www.fortinet.com/products/fortipam) can fill this need for organizations.

### FortiEDR Prevention :police_officer:

FortiEDR has the ability to block credential access attemps out-of-the-box.

1. Click *Incidents* in the FortiEDR Central Manager
2. Review the incident for *winlogon.exe* on the device *The-Flame* that shows the injected process attempt to connect to credentials.
![](creds1.png?width=500px)
3. Go to *Security Settings > Security Events > Security Policies*. Expand the *Exfiltration Prevention* policy and review the first rule *Access to Critical System Information*. 
![](vss2.png?width=500px)
4. The *ADVANCED POLICY & RULE DATA* section at the bottom of the windows provide details on specific rules:
> Rule Details
>> A process attempted to access credentials, passwords or other critical information in a suspicious manner. This rule may have been triggered by a malicious process or by a user attempting to get higher credentials for lateral movement or to elevate privileges.

### Detection :mag:

**Process Access** [ID:DS0009](https://attack.mitre.org/datasources/DS0009/)

Monitor for unexpected processes interacting with LSASS.exe.

### FortiEDR Detection :detective:

1. Go to *Threat Hunting* in the FortiEDR Central Manager.
2. Do a free text query for `lsass.exe`
3. Review the various entries of processes that are observed interacting with the [Local Security Authority Subsystem Service](https://en.wikipedia.org/wiki/Local_Security_Authority_Subsystem_Service)
4. Make note of whether lsass.exe is the source process or the target process. How might you compare this difference in behavior to identify possible malicious behavior from normal behavior?
![](lsass.png?width=500px)

### Going Further :rocket:
- The FortiEDR Threat Hunting free-text query is based on Lucene syntax. The FortiEDR Administration Guide contains an [Appendix](https://docs.fortinet.com/document/fortiedr/6.2.0/administration-guide/142063/appendix-b-lucene-syntax) with detailed information about using lucense syntax in FortiEDR.