---
title: Command & Control Lab
menuTitle: Command & Control Lab
weight: 40
---

This lab will focus on identifying Command and Control (C2) activity. In addition, we'll see how FortiEDR's Automated Incident Response (AIR) playbooks can automate immediate responses to these communication channels. We'll also learn how FortiAnalyzer can add enrichment to events automatically.

---

### Tactic :gear:

**Command and Control** [ID:TA0011](https://attack.mitre.org/tactics/TA0011/)

The adversary is trying to communicate with compromised systems to control them.

Command and Control consists of techniques that adversaries may use to communicate with systems under their control within a victim network. Adversaries commonly attempt to mimic normal, expected traffic to avoid detection. There are many ways an adversary can establish command and control with various levels of stealth depending on the victim’s network structure and defenses.  

### Technique :bulb:

**Application Layer Protocol** [ID:T1071](https://attack.mitre.org/techniques/T1071/)

Adversaries may communicate using OSI application layer protocols to avoid detection/network filtering by blending in with existing traffic. Commands to the remote system, and often the results of those commands, will be embedded within the protocol traffic between the client and server.

#### Sub-Technique :bulb:

**Web Protocols** [ID:T1071.001](https://attack.mitre.org/techniques/T1071/001/)

Adversaries may communicate using application layer protocols associated with web traffic to avoid detection/network filtering by blending in with existing traffic. 

---

### Mitigation :stop_sign:

**Network Intrusion Prevention** [ID:M1031](https://attack.mitre.org/mitigations/M1031/)

Network intrusion detection and prevention systems that use network signatures to identify traffic for specific adversary malware can be used to mitigate activity at the network level. 

---

### FortiEDR Prevention :police_officer:

1. Click on *Incidents* in the FortiEDR [Central Manager](https://xperts2025.fortiedr.com/) (`xperts25` / `xPerts_54321$`)
2. Find the incident where *cloud.exe* is spawned as a child process of *Windows_Update.exe*
3. Review the event graph, noting that *cloud.exe* is making a network connection to IP *1.123.37.68*. Click on the *Investigate* button.

![](cc1.png?width=500px)

4. Select the *Event Analysis* tab for this incident.

![](cc2.png)

5. Click on the elipsis for *Incident Response* and expand the *Malicous* entry to reveal the Automatic Incident Response action.

![](cc3.png?width=500px)

In this case FortiEDR has leveraged an integration with a FortiGate to block this IP due to a malicious classification.

6. Click the elipsis for *Automated Analysis* and then expand the *Network & Extended Data* section.

![](cc4.png?width=500px)

FortiEDR native integration with [FortiGuard Labs](https://www.fortinet.com/fortiguard/labs) allows up-to-date intelligence, supporting real-time incident classification to enable accurate incident response playbook activation.

#### Playbooks

The FortiEDR Playbooks feature determines which automatic actions are triggered, based on the classification of a security event. Playbook policies enable administrators to preconfigure the action(s) to be automatically executed according to a security event’s classification. 

1. Select *SECURITY SETTINGS > Playbooks*. The AUTOMATED INCIDENT RESPONSE – PLAYBOOKS page displays a row for each Playbook policy.
2. Expand the **Default Playbook** policy row to show the actions it contains.

![](AIR.png?width=600px)

Playbook policy actions are divided into the following types:
- Notifications
- Investigation
- Remediation
- Custom

Each of these categories contains different types of actions that can be performed when a security event is triggered.

3. Note that *Remediation* actions can be one of the following types:
  - Terminate process
  - Delete file
  - Clean persistent data
  - Block address on Firewall

4. Note that in our case the *Block address on Firewall* remediation is configured to block *Malicious* and *Suspicious* events on the firewall named *"HQ"*. This action ensures that connections to remote malicious addresses that are associated with the security event are blocked. A Firewall Connector must already be configured in order to perform this action.

---

### Detection :mag:

**Network Traffic Flow** [ID:DS0029](https://attack.mitre.org/datasources/DS0029/)

Monitor for web traffic to/from known-bad or suspicious domains and analyze traffic flows that do not follow the expected protocol standards and traffic flows.

---

### FortiAnalyzer Detection :detective:

1. Login to [FortiAnalyzer](https://98.82.30.66/ui/login/) (`xperts25` / `xPerts_54321$`)
2. Go to the *Incidents & Events > Indicators* pane which consolidates all detected indicators for centralized analysis. This streamlines threat evaluation and enables SOC analysts to take swift action to mitigate risks.

![faz_indicators](faz_indicators.png?width=600px)

3. Double-click on the entry for IP 1.123.37.68 to view the indicator enrichment.

![faz_enrich](faz_enrich.png?width=600px)

4. Review the details in the *Enrich* pane. When indicators are enriched, FortiAnalyzer will display the following information:

| Section | Description |
|---------|-------------|
| FortiGuard CTS | Displays the indicator confidence, IOC tags, IOC, antivirus, and web filter categories. |
| VirusTotal Summary | Displays a Risk Summary, a Detection tab, and a Details tab. |
| Risk Summary | Displays detailed security vendor analysis, presenting a comprehensive list indicating whether each vendor has detected the indicator, along with their assigned risk category if detected. |
| Detection | Displays detailed security vendor analysis, presenting a comprehensive list indicating whether each vendor has detected the indicator, along with their assigned risk category if detected. |
| Details | Displays the Whois Summary and Whois Lookup, providing essential information such as organization details, address, data source, and contact information. |

5. Go to *Incidents & Events > Automation > Playbook Monitor* and double-click the *Indicator Enrichment* playbook that was triggered.

![faz_playbook](faz_playbook.png?width=600px)

Playbooks improve response times and reduce manual workload. In this case the *Indicator Enrichment* playbook uses different [connectors](https://docs.fortinet.com/document/fortianalyzer/7.6.4/administration-guide/885830/active-connectors) (VirusTotal and FortiGuard). The indicator enrichment feature empowers security analysts by providing them with comprehensive threat intelligence on identified IP addresses, domains, and URLs. This enriched context allows for a deeper understanding of security incidents, leading to more informed and effective response decisions.

---

### Going Further :rocket:
- Learn more about [C2](https://www.fortinet.com/resources/cyberglossary/command-and-control-attacks) attacks using Fortinet's cyber glossary.

---

### [Capture The Flag](http://3.19.227.225:8000/) :checkered_flag:

| # | Question/Flag | Points |
|---|---------------|:--------:|
| 1 | Once *Windows_Update.exe* was executed it spawned another process named *cloud.exe*. This process began making a connection to an Australian IP address that served as Command & Control. What remote port at this IP address was being contacted?  | 3 |
| 2 | The FAZ connector for VirusTotal support multipe actions. These actions use specific parameters. What is the full parameter for the *Query IP* action?  | 5 |


