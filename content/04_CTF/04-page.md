---
title: Privilege Escalation Lab
menuTitle: Privilege Escalation Lab
weight: 40
---

In this lab we'll continue to build upon your capabilities to effectively leverage the FortiEDR Threat Hunting module. We'll then learn how events triggered by FortiEDR can be viewed in FortiAnalyzer.

---

### Tactic :gear:

**Privilege Escalation** [ID:TA0004](https://attack.mitre.org/tactics/TA0004/)

The adversary is trying to gain higher-level permissions.

Privilege Escalation consists of techniques that adversaries use to gain higher-level permissions on a system or network. Adversaries can often enter and explore a network with unprivileged access but require elevated permissions to follow through on their objectives.

### Technique :bulb:

**Process Injection** [ID:T1055](https://attack.mitre.org/techniques/T1055/)

Adversaries may inject code into processes in order to evade process-based defenses as well as possibly elevate privileges. Process injection is a method of executing arbitrary code in the address space of a separate live process. Running code in the context of another process may allow access to the process's memory, system/network resources, and possibly elevated privileges. Execution via process injection may also evade detection from security products since the execution is masked under a legitimate process. 

---

### Mitigation :stop_sign:

**Behavior Prevention on Endpoint** [ID:M1040](https://attack.mitre.org/mitigations/M1040/)

Some endpoint security solutions can be configured to block some types of process injection based on common sequences of behavior that occur during the injection process. 

---

### FortiEDR Prevention :police_officer:

During the attack scenario we used a code injection technique to escalate priviliges. FortiEDR has out-of-the-box rules to prevent various types of injection techniques. 

1. Click on *Incidents* in the FortiEDR [Central Manager](https://xperts2025.fortiedr.com/) (`xperts25` / `xPerts_54321$`)
2. Click on the filter icon near the top of the window to open the detailed filtering pane.
![filter_icon](filter_icon.PNG)
3. Using the *Rules* dropdown type `inject` to filter the available rules and then choose the "Injected Thread" rule. Click the *Apply Filters* button.
![injected_thread](injected_thread.png?width=500px)
4. Click on the entry for **control.exe**. Notice that the event graph shows the *control.exe* process injecting into the *winlogon.exe* process.
![inject_event](inject_event.png?width=500px)
5. Click the *Investigate* button to view this event in Investigation View.
6. Click the Event Analysis tab. Here we can see clearly in the provided graphic the steps in the injection along with the MITRE icon indicating once again FortiEDR associating this behavior with a MITRE tactic and technique. 
![investigate_injection](investigate_injection.png?width=500px)
7. Click on the MITRE icon to view the tagged Tactics and Technique.

{{% notice note %}}Some techniques can fall under the category of multiple tactics. In this case we see that process injection is a technique of both the **Privilege Escalation** and **Defense Evasion** tactics.{{% /notice %}}

---

### Detection :mag:

**Process Modification** [ID:DS0009](https://attack.mitre.org/datasources/DS0009/)

Monitor for changes made to processes that may inject code into processes in order to evade process-based defenses as well as possibly elevate privileges.

---

### FortiEDR Detection :detective:

The Threat Hunting  activity events tables area can be used to easily add filters to a query.

When you hover over an item in the table, a green and red button appear to its right. Click the green plus button to include that item as a filter or click the red minus button to exclude that item as a filter.

1. Click *Threat Hunting* in the FortiEDR [Central Manager](https://xperts2025.fortiedr.com/) (`xperts25` / `xPerts_54321$`)
2. Type `control.exe` in the filter dialog box and press *enter* to narrow down the results.
3. Find the entry that has a **source process** of *control.exe* and a **target process** of *winlogon.exe*. Hover over each process and click the green plus button to add it to the filter criteria. 
![green_button](green_button.png?width=500px)
4. Once both processes have been added to the query you can now see how this view resembles what we previously reviewed in the Investigation View.
![filtered_buttons](filtered_activity_buttons.png?width=500px)

---

### FortiAnalyzer Detection :detective:

1. Login to [FortiAnalyzer](https://98.82.30.66/ui/login) (`xperts25` / `xPerts_54321$`)
2. After event handlers start generating events, view events and event details in *Incidents & Events > Event Monitor*.

The Explorer pane allows you to efficiently monitor events using a timeline and quick filters.

![faz_process_injection](faz_process_injection.png?width=600px)

3. Double-click the record for device *JPalm-DC* for the Event Handler *FortiEDR Process Injection* to display the Event Details Pane.

![faz_event_details](faz_event_details.png?width=600px)

This pane is named after the event, and it displays with the following tabs:

|  Tab  | Description |
|-------------------|--------------|
| Event Details | Displays the event details in a formatted view. You can toggle to view the raw JSON. You can use the search bar to find specific information within the event details. |
| Triggering Logs | Displays a sample of logs that triggered the event. You can view the log details in this tab. |
| Rule Summary | Displays information about the event handler rule that triggered the event. This includes the rule name, description, log type, severity, pattern, threshold, and group by information. |
| Comment | Add or edit a comment for the event. |
| Context | Displays a timeline for related events. From the Entity dropdown, select the entity/entities to include in the timeline. |

{{% notice note %}}Review the Event Details listed here and note that a specific MITRE Tech ID has been associated with this event.{{% /notice %}}

---

### Going Further :rocket:
- At the end of 2023, researchers from SafeBreach published a new code injection technique for Windows OS called **"Pool Party"** in the Blackhat EU briefing. This new injection technique was able to bypass vendors such as Crowdstrike, SentinelOne, Microsoft, Palo Alto, and Cybereason. You can find further information and details on how FortiEDR blocked this out-of-the box [here](https://fortiguard.fortinet.com/threat-signal-report/5357/fortiedr-coverage-poolparty-code-injection-technique-1).

---

### [Capture The Flag](http://3.19.227.225:8000/) :checkered_flag:
Review the Event Details for the previously reviewed event in FortiAnalyzer to find the following:

| # | Question/Flag | Points |
|---|---------------|:--------:|
| 1 | The triggered event is a result of a specific FortiAnalyzer Event Handler. What is the Handler ID assigned to this event handler?  | 3 |
| 2 | The source of these events are generated by FortiEDR logs. These are received as raw logs and parsed by FortiAnalyzer. These logs contain extensive information. Based on the FortiEDR logs what Threat Family is associated with this Process Injection event?  | 3 |
| 3 | What FortiEDR Log Parser version was used to parse the current logs?  | 5 |

