---
title: Lateral Movement Lab
menuTitle: Lateral Movement Lab
weight: 35
---
In this lesson we'll explore how adversaries may use multiple tactics to achieve a particular action. One of the ways that adversaries use multiple tactics is when attempting to move laterally through a network. Following through on their primary objective often requires exploring the network to find their target and subsequently gaining access to it. Reaching their objective often involves pivoting through multiple systems and accounts to gain further access. Adversaries might install their own remote access tools to accomplish Lateral Movement or use legitimate credentials with native network and operating system tools, which may be stealthier.

We'll look specifically at how Lockbit ransomware uses multiple tactics to achieve lateral movement.

### Tactic :gear:

**Lateral Movement** [ID:TA0008](https://attack.mitre.org/tactics/TA0008/)

The adversary is trying to move through your environment.

---

{{% notice note %}}Lockbit will actually use a reconnaissance tactic to scan the network for other IPs that can be used for lateral movement.{{% /notice %}}

### Tactic :gear:

**Reconnaissance** [ID: TA0043](https://attack.mitre.org/tactics/TA0043/)

The adversary is trying to gather information they can use to plan future operations. Reconnaissance consists of techniques that involve adversaries actively or passively gathering information that can be used to support targeting.

### Technique :bulb:

**Active Scanning** [ID:T1595](https://attack.mitre.org/techniques/T1595/)

Adversaries may execute active reconnaissance scans to gather information that can be used during targeting. Active scans are those where the adversary probes victim infrastructure via network traffic, as opposed to other forms of reconnaissance that do not involve direct interaction.

### Sub-Technique :bulb:

**Scanning IP Blocks** [ID: T1595.001](https://attack.mitre.org/techniques/T1595/001/)

Adversaries may scan victim IP blocks to gather information that can be used during targeting. 

### Mitigation :stop_sign:

**Pre-Compromise** [ID:M1056](https://attack.mitre.org/mitigations/M1056/)

This technique cannot be easily mitigated with default system tools.

### FortiEDR Prevention :police_officer:

FortiEDR has out-of-the-box policies that are comprised of comprehensive rules that offer extensive protection. In many cases, other vendors require that users manually create these rules which entails in-depth knowledge of how to identify a myriad of attacker's techniques.

Of particular interest to the *Reconnaissance* tactic is FortiEDR's **Exfiltration Prevention** policy. This policy enables FortiEDR to distinguish which connection establishment requests are malicious ones. 

1. Click on *Security Settings > Security Events > Security Policies* in the FortiEDR Central Manager.
2. Click on *Exfiltration Prevention* to expand the policy and show all subsequent rules. 
![exfil_prevent](exfil_prevention.png?width=500px)

The SECURITY POLICIES page displays a row for each security policy. Each policy row can be expanded to show the rules that it contains.

The following information is defined per security policy:

| Information Field | Description |
|-------------------|--------------|
|Policy Name        |The policy name appears in the left most column. The policy name is defined when the policy is created. The name of the Default Policy cannot be changed.|
|Rule Name          |FortiEDR’s proprietary rules come predefined and are the primary component of FortiEDR’s proprietary security solution. This column displays a short description for the purpose of this rule.|
|Action             |Specifies the action that is enforced when this rule is violated. |
|State              |(Enabled/Disabled) This option allows you to disable/enable this rule. FortiEDR’s rules have been created as a result of extensive expertise and experience. Therefore, we do not recommend disabling any of them.|

{{% notice tip %}}You can expand the ADVANCED POLICY & RULES DATA area at the bottom left of the window to display a more detailed description of what the rule does and how it works.{{% /notice %}}

### Detection :mag:

**Network Traffic Flow** [ID:DS0029](https://attack.mitre.org/datasources/DS0029/#Network%20Traffic%20Flow)

Monitor network data for uncommon data flows. Processes utilizing the network that do not normally have network communication or have never been seen before are suspicious.

### FortiEDR Detection :detective:

The LockBit ransomware scans for ports 135 and 445 which is captured by the FortiEDR threat hunting telemetry. Port 135 is used for RPC client-server communication and 445 is used for authentication and file sharing. We'll learn how to use **facets** to quickly identify this activity.

The continuous, realtime collection of Threat Hunting data produces numerous activity events. The sheer volume of activity data can make working directly with these activity events seem cumbersome at times. Therefore, FortiEDR uses **facets** to summarize the data displayed in the results tables. **Facets** are predefined in FortiEDR and represent the same data that is displayed in the results tables, but in an aggregated form. As such, facets represent the aggregation of the values in the results tables.

1. Login to the FortiEDR Central Manager.
2. Click on *Threat Hunting*.
3. In the Filters dialog box simple type `Lockbit.exe` and press enter. This will display numerous entries in the Activities Event Table.
4. Click the small *triangle* below the *filter* section to reveal the **Facets and Results Tables**.
![facets](facet_triangle.png?width=500px)

Each individual facet pane summarizes the top five items for that facet. For example, in the Type (action) facet below, the facet lists the top five actions, based on the filters applied in the query. The number at the top in parentheses () indicates the total number of different values for this facet in the results table, in this case 16. In this case, the top five actions are Library Loaded, File Write, File Rename, File Create, and Process Creation.

![facets_more](facet_more.png?width=500px)

5. Click the **More** link to display additional facets.

Facets provide an easy-to-use mechanism to aggregate the results in the Activity Events tables. In addition, you can also further narrow the results in the Activity Events table directly from the facets by including or excluding specific values. For example, when you hover over an item in a facet pane, a green and red button appear in its row. 

6. In the **Remote Port** table hover over ports 135 and 445 and click the green plus button to include that item as a filter. Both items will be highlighted in green indicating they have been marked as an inclusion filter.
7. Click the **Apply** button to apply the additional filtering criteria to the threat hunting query.

![facet_apply](facet_apply.png?width=500px)

 In addition, it creates a chip (indicated by the arrow in the following picture), which represents the additional filters and displays it at the top of the Facets area.

 ![facet_chip](facet_chip.png?width=500px)

 Hovering over a chip enables you to remove, disable or copy it, as follows:

 ![alt text](facet_hover.png)

 | Tool | Definition |
|-------------------|--------------|
|Remove|The chip is removed and the Facets and Result tables are updated accordingly.|
|Disable|A disabled chip no longer affects the results. The Facets and the Results tabs are updated as if the chip was removed.|
|Copy|The chip content is copied to memory and can be pasted into the query for further editing.|

{{% notice info %}}Once the broadcast domain is identified LockBit will scan the network iterating from the network ID address and incrementing up to the broadcast address trying to connect over ports 135 or 445, if successful it will try to encrypt the network hosts.{{% /notice %}}

### Going Further :rocket:
- The [FortiGuard Managed Detection and Response (MDR)](https://www.fortinet.com/solutions/enterprise-midsize-business/mdr) Service is designed for customers of the FortiEDR advanced endpoint security platform. This team of threat experts monitors, reviews and analyzes every alert, proactively hunts threats, and takes actions on behalf of customers to ensure they are protected according to their risk profile.
