---
title: MITRE ATT&CK
menuTitle: MITRE ATT&CK
weight: 10
---

The goal of this workshop is not to just learn how to use a specific tool, or tools, but to also leverage a common framework used in the InfoSec industry. With that in mind the [MITRE ATT&CK®](https://attack.mitre.org/) framework will serve as a foundational reference tool through the lab exercises. This page provides key information on MITRE ATT&CK® and you'll also use the publicly available MITRE ATT&CK® knowledge base to find information.

We strongly believe that a basic understanding of this framework will make you a better security practitioner. Additionally, you will find MITRE ATT&CK® referenced in may Fortinet products.

## Overview

[MITRE ATT&CK®](https://attack.mitre.org/) is a globally-accessible knowledge base of adversary tactics and techniques based on real-world observations. The ATT&CK knowledge base is used as a foundation for the development of specific threat models and methodologies in the private sector, in government, and in the cybersecurity product and service community.

FortiEDR stands out in its ability to provide rapid insights. It fuses deep analytic capabilities with a detailed understanding of the MITRE ATT&CK framework. This harmonization empowers organizations to anticipate and tackle threats, such as nation-state threats, which pose severe security concerns for enterprises globally.

By leveraging FortiEDR threat hunting capabilities and its ability to identify behavior along the MITRE ATT&CK framework, organizations can pinpoint related [Indicators of Compromise (IOCs)](https://www.fortinet.com/resources/cyberglossary/indicators-of-compromise) with unparalleled precision to enable a proactive stance against potential breach attempts. This holistic approach, rooted in insight and foresight, underscores the pivotal role of FortiEDR within an organization’s security strategy.

In this section, we'll learn how to operationalize MITRE ATT&CK® along with FortiEDR to understand how threat actors operate, and how we can detect and prevent adversary tactics and techniques.

![matrix](matrix.PNG?width=500px)

## Key Concepts

First, we will need to understand some of the main components of the ATT&CK model. During the subsequent investigation steps we'll specifically learn about what are commonly referred to as *Tactics, Techniques, and Procedures (TTPs)*:
- **Tactics**, represents “why” or the reason an adversary is performing an action.
- **Techniques**, represents “how” adversaries achieve tactical goals by performing an action.
- **Sub-techniques**, a more specific or lower-level description of adversarial behavior.
- **Procedures**, specific implementation or in-the-wild use the adversary uses for techniques or sub-techniques.

![TTPs](ttps.PNG?width=500px)

### MITRE ATT&CK® Matrix for Enterprise

We'll first view the MITRE ATT&CK® Matrix for Enterprise which shows the associated tactics and techniques. Click [here](https://attack.mitre.org/matrices/enterprise/) to open the ATT&CK Matrix in a new tab for reference.

![matrix](mitre-attack-enterprise.png?width=500px)

## ATT&CK® Matrix Organization

Tactics represent the "why" of an ATT&CK technique or sub-technique. It is the adversary's tactical goal: the reason for performing an action. The matrix consists of a header row that list the following tactics (in order of typical operation), along with an associated ID for each tactic:

| ID	| Name	| Description |
|-------|-------|-------------|
|TA0043	|Reconnaissance	|The adversary is trying to gather information they can use to plan future operations.|
|TA0042	|Resource Development	|The adversary is trying to establish resources they can use to support operations.|
|TA0001	|Initial Access	|The adversary is trying to get into your network.|
|TA0002	|Execution	|The adversary is trying to run malicious code.|
|TA0003	|Persistence	|The adversary is trying to maintain their foothold.|
|TA0004	|Privilege Escalation	|The adversary is trying to gain higher-level permissions.|
|TA0005	|Defense Evasion	|The adversary is trying to avoid being detected.|
|TA0006	|Credential Access	|The adversary is trying to steal account names and passwords.|
|TA0007	|Discovery	|The adversary is trying to figure out your environment.|
|TA0008	|Lateral Movement	|The adversary is trying to move through your environment.|
|TA0009	|Collection	|The adversary is trying to gather data of interest to their goal.|
|TA0011	|Command and Control	|The adversary is trying to communicate with compromised systems to control them.|
|TA0010	|Exfiltration	|The adversary is trying to steal data.|
|TA0040	|Impact	|The adversary is trying to manipulate, interrupt, or destroy your systems and data.|

Subsequently each **tactic** is comprised of numerous **techniques** (and sub-techniques) that represent 'how' an adversary achieves a tactical goal by performing an action. These too are identified by an ID. For example, the first technique listed for TA0043 Reconnaissance is Active Scanning:

| ID	| Name	| Description |
|-------|-------|-------------|
|T1595	|Active Scanning	|Adversaries may execute active reconnaissance scans to gather information that can be used during targeting. Active scans are those where the adversary probes victim infrastructure via network traffic, as opposed to other forms of reconnaissance that do not involve direct interaction.|

The exercises in the labs will reference the ATT&CK® Matrix as we focus on some specific tactics and techniques and understand how FortiEDR incorporates the ATT&CK® Matrix natively.