---
title: Credential Access Lab
menuTitle: Credential Access Lab
weight: 30
---

This lab will focus on understanding common techniques, and sub-techniques, used by attackers to access credentials on victim machines. We'll then see how some of these specific tactics can be viewed in FortiAnalyzer.

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

1. Click *Incidents* in the FortiEDR [Central Manager](https://xperts2025.fortiedr.com/)
2. Review the incident for *winlogon.exe* on the device *The-Flame* that shows the injected process attempt to connect to credentials.

![](creds1.png?width=500px)

3. Go to *Security Settings > Security Events > [Security Policies](https://xperts2025.fortiedr.com/#/security_settings/security_events/security-policies)*. Expand the *Exfiltration Prevention* policy and review the first rule *Access to Critical System Information*. 

![](vss2.png?width=500px)

4. The *ADVANCED POLICY & RULE DATA* section at the bottom of the windows provide details on specific rules:
> Rule Details
>> A process attempted to access credentials, passwords or other critical information in a suspicious manner. This rule may have been triggered by a malicious process or by a user attempting to get higher credentials for lateral movement or to elevate privileges.

### Detection :mag:

**Process Access** [ID:DS0009](https://attack.mitre.org/datasources/DS0009/)

Monitor for unexpected processes interacting with LSASS.exe.

### FortiAnalyzer Detection :detective:

1. Login to [FortiAnalyzer](https://aws.graun.io/)
2. Navigate to *Incidents & Events > Incidents > MITRE ATT&CK®*
3. Under the column header for the **Credential Access** tactic find the tile for **OS Credential Dumping**. An icon and count displays on the tile. 

![faz_cred_dump](faz_cred.png?width=600px)

4. Mouse over the tile to display information in a tooltip.
5. Click on the Event/Incident count to open a pane for this technique. You can toggle between table views for *Events* and *Incidents*.

![faz_event_incident](faz_event_incident.png?width=600px)

The table view for *Events* includes the following information:

|  Column  | Description |
|-------------------|--------------|
| Event Handler | The event handler that generated the event(s). |
| Severity | The severity of the event(s). |
| Technique | The technique or sub-technique related to the event(s). |
| Affected Endpoints | The number of affected devices. |
| Event Count | The event count related to that event handler and technique or sub-technique. |

The table view for *Incidents* includes the following information:

|  Tab  | Description |
|-------------------|--------------|
| Severity | The severity of the incident(s). |
| Description | The description for the incident. |
| Technique | The technique or sub-technique related to the incident(s). |
| Affected Endpoints | The number of affected endpoints. |
| Incidents | The incident count related to that technique or sub-technique. |

6. Click the incident count to open the *Incidents & Events > Incidents > Incidents* pane in a new tab. 

![faz_incident_count](faz_incident_count.png?width=600px)

7. Review the filtered incidents of the selected technique.

![faz_incident](faz_incident.png?width=600px)

### Going Further :rocket:
- The FortiEDR Threat Hunting free-text query is based on Lucene syntax. The FortiEDR Administration Guide contains an [Appendix](https://docs.fortinet.com/document/fortiedr/6.2.0/administration-guide/142063/appendix-b-lucene-syntax) with detailed information about using lucense syntax in FortiEDR.

### Capture The Flag :checkered_flag:
Passwords are typically stored as hashes. One common method to discover these passwords is to “crack” them. Depending on the complexity of the hash this can be difficult and time consuming, however there are online tools that can attempt to crack passwords and can often easily discover common passwords from hashes. See if you can crack the password of this MD5 hash: **482c811da5d5b4bc6d497ffa98491e38** 
1. What is the clear-text password?