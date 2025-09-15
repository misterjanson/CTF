---
title: Execution Lab
menuTitle: Execution Lab
weight: 10
---

In this lab we'll learn how FortiEDR deals with the malicous files used during the attack scenario. We'll also learn how powerful FortiEDR's Threat Hunting module is and understand the information it provides to identify behaviors associated with attacker's tactics and techniques.

{{% notice note %}}If you refer to the MITRE ATT&CK Matrix the first three tactics of [Reconnaissance](https://attack.mitre.org/tactics/TA0043/), [Resource Development](https://attack.mitre.org/tactics/TA0042/), and [Initial Access](https://attack.mitre.org/tactics/TA0001/) would typically precede Execution. We will not cover all tactics in-depth during the course of these labs.{{% /notice %}}

### Tactic :gear:

**Execution** [ID: TA0002](https://attack.mitre.org/tactics/TA0002/)

The adversary is trying to run malicious code.

Execution consists of techniques that result in adversary-controlled code running on a local or remote system. Techniques that run malicious code are often paired with techniques from all other tactics to achieve broader goals, like exploring a network or stealing data. 

### Technique :bulb:

**User Execution** [ID: T1204](https://attack.mitre.org/techniques/T1204/)

An adversary may rely upon specific actions by a user in order to gain execution. Users may be subjected to social engineering to get them to execute malicious code by, for example, opening a malicious document file or link. In our scenario we simulated a simple version of this where a user downloaded a malicious file from a cloned website. The web server configured in Kali Linux allowed us to simulate this.

### Sub-Technique :bulb:

**Malicious File** [ID: T1204.002](https://attack.mitre.org/techniques/T1204/002/)

An adversary may rely upon a user opening a malicious file in order to gain execution. Users may be subjected to social engineering to get them to open a file that will lead to code execution. This was the case in our scenario where the user was a target of social engineering. These types of attacks are commonly observed as follow-on behavior from a [Spearfishing Attachment](https://attack.mitre.org/techniques/T1566/001/).

### Mitigation :stop_sign:

**Execution Prevention** [ID: M1038](https://attack.mitre.org/mitigations/M1038/)

Block execution of code on a system through application control, and/or script blocking.

### FortiEDR Prevention :police_officer:

FortiEDR provides multiple out-of-the-box policies. Each policy comes with multiple highly intelligent rules that enforce it. In regards to how FortiEDR can stop the malicious file that was executed in the attack scenario let's look at a FortiEDR security policy.

1. Login to the FortiEDR [Central Manager](https://xperts2025.fortiedr.com/)
2. Click on *Security Settings > Security Events > [Security Policies](https://xperts2025.fortiedr.com/#/security_settings/security_events/security-policies).*
3. The Security Policies page displays a row for each security policy. Each policy row can be expanded to show the rules that it contains. In this case we'll focus on the *Execution Prevention* policy. This policy blocks the execution of files that are identified as malicious or suspected to be malicious. For this policy, each file is analyzed to find evidence for malicious activity.

The following information is defined per security policy:

| Information Field | Description |
|-------------------|--------------|
|Policy Name        |The policy name appears in the left most column. The policy name is defined when the policy is created. The name of the Default Policy cannot be changed.|
|Rule               |FortiEDR’s proprietary rules come predefined and are the primary component of FortiEDR’s proprietary security solution. This column displays a short description for the purpose of this rule.|
|Action             |Specifies the action that is enforced when this rule is violated. |
|State              |(Enabled/Disabled) This option allows you to disable/enable this rule. FortiEDR’s rules have been created as a result of extensive expertise and experience. Therefore, we do not recommend disabling any of them.|

{{% notice tip %}}You can expand the ADVANCED POLICY & RULES DATA area at the bottom left of the window to display a more detailed description of what the rule does and how it works.{{% /notice %}}

1. Click on the Execution Prevention policy to expand the policy to show the associated rules that comprise the policy.
2. Click on the first rule of the policy *Malicious File Detected*. Note that by default this rule is set to **block** and is **enabled**.
![execution_prevention](execution_prevention_policy.png?width=500px)
1. Click on *ADVANCED POLICY & RULES DATA* at the bottom of the window to display information about this rule.
2. Notice the *RULE DETAILS*:
> The file was identified as malicious by our machine-learning engine or by other means, based on analysis of the file.

This rule provides a proven first layer of defense via a custom-built, kernel-level next-generation
machine-learning-based antivirus (NGAV) engine that prevents infection from advanced
attacks like ransomware in real time.

In this case the *Malicous File Detected* rule will satisfy the recommendation by MITRE to **mitigate** execution on a system. Let's review this rule in action for the *Windows_Update.exe* file that was downloaded during the attack scenario.

1. Click on [Incidents](https://xperts2025.fortiedr.com/#/incidents) in the FortiEDR [Central Manager](https://xperts2025.fortiedr.com/) and click on the line for *Windows_Update.exe* to expand a list of events. Incidents are shown descending by default (from newest to oldest).

![windows_update_event](windows_update_event.png?width=500px)

2. Select the earliest event in the timeline. In addition to textual information that is displayed, the Event Graph tab provides an image depicting the process chain, such as connection establishment and data alteration, up to the action that was blocked.

![](event_graph.png?width=500px)

The picture is shown as a timeline from left to right (meaning that the left process happened before the others). Activity event types or actions are represented by a curved line with an arrow, called an "edge". An edge can be one activity event/action or an aggregation of several. The numbered arrows indicate the sequence of actions and specify the action that was performed, such as Process Creation, Socket Close, Block and so on. Edges may also have icons below them indicating classification or violation of certain rules and MITRE & Behavior models. Click on an icon for more detailed information.

4. Click on the red explanation icon to display the FortiEDR rule that was triggered for this incident.
![](mal_file.png?width=500px)

Note that the *Malicious File Detected* rule was triggered for *Windows_Update.exe*. 

5. Click the blue *Investigate* button for this incident to open the *Investigation View* windows.

![incident_icon](incident_icon.PNG)

The Investigation View window provides a comprehensive overview and event analysis of an incident. In this case we'll make note of the fact that the Overview shows *Violated Policies*. In the case of *Windows_Update.exe* we can clearly see the *Malicious File Detected* rule was triggered. 

![incident_overview](incident_overview.png?width=500px)

{{% notice note %}}Keep in mind as we review these incidents that FortiEDR is running in **Simulation** mode. This allows the threats in the attack scenario to execute so that we can gain further insight into the behavior of these threats. If FortiEDR was set to **Prevention** mode the *Windows_Update.exe* file would have been blocked once the *Malicious File Detected* rule was triggered.{{% /notice %}}

As we can see here FortiEDR's default rules have the ability to satisfy MITRE's suggestion for mitigation by using some form of execution control.

### Detection :mag:

**File Creation** [ID: DS0022](https://attack.mitre.org/datasources/DS0022/)

Monitor for newly constructed files that are downloaded and executed on the user's computer.

### FortiEDR Detection :detective:

FortiEDR’s Threat Hunting functionality enables you to search for many types of Indicators of Compromise (IOCs) and malware across your entire environment in order to enable enhanced detection. Searching can be based on various attributes of files, registry keys and values, network, processes, event log and activity event types. The attributes are useful when considering MITRE's detection recommendations.

1. Access the Threat Hunting page by clicking *Threat Hunting* in the FortiEDR [Central Manager](https://xperts2025.fortiedr.com/).

The Threat Hunting page contains the following areas:

- Filters
- Facets
- Activity Events Tables
- Details Pane

![](thovw2.png?width=500px)

FortiEDR categorizes the various actions into the following categories:

|     Action                  |     Description                                                                                                                                                                 |
|-----------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|     Registry Key Actions    |     All targets are either registry keys or registry values and all actions are registry-related, such as Key Created, Key Deleted, Value Set and so on.                    |
|     File Actions            |     All targets identify the target file on which the action was performed, and all actions are file-related, such as File Create, File Delete, File Rename and so on.    |
|     Process Actions       |     The target is another process, and all actions are process related, such as Process Termination, Process Creation, Executable Loaded and so on.                         |
|     Network Actions       |     The target is a network item (such as connection or URL) and all actions are Network related, such as Socket Connect, Socket Close and Socket Bind.                     |
|     Event Log Actions     |     The only action is Log Entry Created and relates to the logs of the operating

We'll use this information to quickly take a look at the initial creation of the Lockbit.exe ransomware file:

2. In the Filters dialog box simple type `Lockbit.exe` and press enter. This will display numerous entries in the Activities Event Table. Let's narrow that down.
![01_TH](01_threat_hunt.png?width=500px)
3. Click the **File** actions header to show only file activities of Lockbit.exe.
4. Click on the **TIME** column header to sort the events ascending, so that we can view the oldest events first.
![02_TH](02_threat_hunting.png?width=500px)
5. Locate an entry with the type of "File Create".
6. Click anywhere in this row of the Activity Events table to display more details about the specific activity event in a Details pane on the right. The Details pane for an activity event contains a Summary tab, one or two other tabs, and the Investigation View button. The selected row is marked by a green border on its left.
![](file_create.png?width=500px)
The Details pane for an activity event contains a Summary tab, one or two other tabs, and the Investigation View button, as follows:
![04_TH](04_threat_hunt.png?width=500px)
    - **Summary Tab**: This tab specifies a summary of the activity event. At the top of the tab, it shows details about the endpoint, including the endpoint and its IP, path, operating system, and so on. The area below the endpoint section shows the source process and its detail. The area below the source graphically shows the action again, which is the activity event type, as well as some additional data regarding the action, if any. The area at the bottom of the pane shows the target and its details. You can click the Expand or Collapse arrows in an area of this pane to show or hide additional relevant details, respectively.
    - **Process Tab**: This tab shows additional details about the source process.
    ![05_TH](05_threat_hunt.PNG?width=500px)
    - **Target Tab**: This tab only displays if the target is of type Process or File, and details additional data regarding such.
    - **Investigation View Button**: This button opens a graphical Investigation View of the activity events details: source, action and target. The graphical view provides the ability to add more activity events to the graph and show the relationship and timeline of the occurrence of those activities for better understanding of the flow of activity events.
8. Take time to explore the information presented in the *Details Pane*.

{{% notice warning %}}Get in the habit of using the **Clear All** option in the Filters area of the Threat Hunting Module. Click the elipsis and choose *Clear All* prior to running a new query. In some cases it may also be necessary to increase the time range of a query by using the **Time** drop down and selecting the appropriate range.{{% /notice %}}


### Going Further :rocket:

MITRE ATT&CK also provides information on threat [groups](https://attack.mitre.org/groups/) that are tracked by common names in the security community. Read about the [Sandworm Team](https://attack.mitre.org/groups/G0034/) that has been attributed to Russia's General Staff Main Intelligence Directorate (GRU) Main Center for Special Technologies (GTsST) military unit 74455. You can also read about [campaigns](https://attack.mitre.org/campaigns/) associated with these groups. For example, MITRE documents the Sandworm Team's techniques used during the [2015 Ukraine Electric Power Attack](https://attack.mitre.org/campaigns/C0028/).