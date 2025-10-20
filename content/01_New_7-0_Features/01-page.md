---
title: What's New in FortiEDR
menuTitle: What's New in FortiEDR
weight: 5
---
FortiEDR 7.2 offers multiple new features that will move the product line further ahead in terms of capabilities and security coverage. 

## New Dashboards :tv:

EDR 7.2 delivers a new dashboard experience with customizable widgets to create a unique view for each analyst using the console. Improvements to the UI provide FortiEDR administrators a more modern look and feel. 

The following is the previous 6.2 dashboard view:

![](old_dashboard.png?width=500px)

Here is a view of the new 7.0 dashboard:

![](new_dashboard.png?width=500px)

## Changes to the Workflow of Events :man_technologist:

The *Event Viewer* tab is renamed *Incidents* with usability improvements, such as tabbed view of different types of incidents. Clicking on an incident displays the Handle Incident button and an embedded preview of the investigation view within the console where you can perform operations without opening a separate tab.

![new_incidents](new_incidents.png?width=600px)

Clicking the *Investigate* button opens the full investigation view within the console with an *Overview* tab that shows the audit history and policy violation information. 

![new_overview](new_overview.png?width=600px)

The *Event Analysis* tab that shows the full investigation view. You can also switch to full screen or open the investigation view in a new tab using the buttons at the top-right corner.

![new_analysis](new_analysis.png?width=600px)

## Protection for Mobile Devices :iphone:

FortiEDR 7.2 adds protection for mobile devices (Android and iOS) with the following security features:
- (Android only) Real time and scheduled periodic scanning for potential vulnerabilities, such as malicious files or applications, rooted devices, outdated OS versions and kernel, lack of security update, or non-compliant configurations.
- (Android only) Application behavior and network traffic monitoring to detect mobile malware and data exfiltration. FortiEDR prevents the execution or installation of malicious files or applications based on the policy or application verdict.
- Automatic detection of malicious domains and IP addresses with built-in threat intelligence integration

## FortiRecon Integration :telescope:

FortiEDR 7.2 adds integration with [FortiRecon](https://www.fortinet.com/products/fortirecon) for comprehensive visibility into the organization's external attack surface so that analysts can prioritize security alerts and incidents based on risk factors such as severity of vulnerabilities, relevance of threat intelligence feeds, and severity of affected endpoints, ensuring that efforts are focused on addressing the most significant risks to the organization.

The *Communication Control > Applications* page replaces the Vulnerability column with the following two Severity columns with severity ratings for each application and version:
- **NIST Severity** — Rating provided by FortiEDR’s vulnerability scoring system leveraging the NIST Cybersecurity Framework.
- **ACI Severity** — Adversary Centric Intelligence (ACI) rating provided by FortiRecon leveraging FortiGuard Threat Analysts to provide comprehensive coverage of dark web, open source, and technical threat intelligence, including threat actor insights. This information enables administrators to proactively assess risks, respond faster to incidents, better understand their attackers, and protect assets.

## Security Compliance :memo:

The *Inventory > Collectors* page includes the new DISK ENCRYPTION  and DEVICE SECURITY columns which provides insights into the security status of Windows and macOS endpoints.

The device is marked as compliant if two or more of the following criteria are met:

| Windows                    | MacOS |
|--------------------------|---------------|
| Windows Updates | Gatekeeper Status |
| Security Center | System Integrity Protection (SIP) Status |
| User Account Control (UAC) | |