---
title: Impact Lab
menuTitle: Impact Lab
weight: 45
---

When an attack is finally discovered by most organizations it is because attackers have significantly impacted business operations, such as [encrypting data](https://attack.mitre.org/techniques/T1486/). In this lab we'll take a look at a common impact technique. 

### Tactic :gear:

**Impact** [ID:TA0040](https://attack.mitre.org/tactics/TA0040/)

The adversary is trying to manipulate, interrupt, or destroy your systems and data.

Impact consists of techniques that adversaries use to disrupt availability or compromise integrity by manipulating business and operational processes.  

### Technique :bulb:

**Inhibit System Recovery** [ID:T1490](https://attack.mitre.org/techniques/T1490/)

Adversaries may delete or remove built-in data and turn off services designed to aid in the recovery of a corrupted system to prevent recovery. This may deny access to available backups and recovery options.

### Mitigation :stop_sign:

**Data Backup** [ID:M1053](https://attack.mitre.org/mitigations/M1053/)

Consider implementing IT disaster recovery plans that contain procedures for taking regular data backups that can be used to restore organizational data. 

### FortiEDR Prevention :police_officer:

1. Click on *Incidents* in the FortiEDR Central Manager
2. Review the entry for VSSVC.exe.
![](vss1.png?width=500px)
3. Using the skills you've learning in previous labs review this event to identify how FortiEDR is able to alert and block attempts to delete shadow copies.

### Detection :mag:

**Command Execution** [ID:DS0017](https://attack.mitre.org/datasources/DS0017/)

Use process monitoring to monitor the execution and command line parameters of binaries involved in inhibiting system recovery, such as vssadmin, wbadmin, and bcdedit.

### FortiEDR Detection :detective:

After filtering the activity events displayed in the result tables, you can save a query to be redisplayed when needed. Saving a query in this manner also enables you to define it as a scheduled query in order to automate the process of threat detection.

We’ll use our knowledge of use the common practice of shadow copy deletion to inhibit system recovery to create a scheduled query. 

1. Go to *Threat Hunting* in the FortiEDR Central Manager.
2. In the Filters area use the following search criteria: ```Target.Process.CommandLine: ("Delete Shadows \/All \/Quiet")```
3. In the Filters area, at the far right of the page, click the ellipses icon  and select *Save Query*.

![query](save_query.png?width=500px)
 
2. The following displays populated with the current filter definitions. The Category, Device, and Time dropdown menus show the filter selections and the box underneath it shows the actual query string.

![query2](save_query_2.PNG?width=500px)

3. Fill in the *Query Name* and *Description* fields with information that is meaningful to this query. There are various options that can be modified for queries such as creating tags or specifying this as a Community Query, no other modification will be needed for this exercise. We can use the MITRE page for [Inhibit System Recovery](https://attack.mitre.org/techniques/T1490/) to add clarification to this query, try using the following (where *XX* are your initials):

| Query Name | Description |
|------------|-------------|
| XX T1490   | A number of native Windows utilities have been used by adversaries to disable or delete system recovery features: vssadmin.exe can be used to delete all volume shadow copies on a system |

![query3](save_query_3.PNG?width=500px)

4. Check the **Scheduled Query** option to automate the process of detecting threats so that this query is run automatically according to the schedule that you define. For the purposes of this exercise, we will configure the query to run every **15 Minutes** with a **Malicious** classification. A security event is automatically created in the Event Viewer upon detecting threats (query matches). Notifications are sent according to the security event’s definition, such as via email, syslog, and so on. You can also configure playbook actions for the triggered security events from the scheduled query.

![](savequery3.png?width=300px)

5. Click **Save** to save this query so that it is available to be redisplayed, as described below. The system runs the query immediately to verify that it is functional.

6. To display a Saved Query, on the *Filters* area, at the far right of the page, click the eclipsis icon and select *Saved* Queries.  The following displays listing all the queries that were saved using the Save Query option.
![](savequery4.png?width=500px)

{{% notice note %}}Scheduled query options are as follows{{% /notice %}}

| Field                    | Definition |
|--------------------------|---------------|
| Classification           | Select the classification of the Security Event to be issued when the scheduled query has run and found matches. The Classification specifies how malicious the security event is, if at all. Classifications are shown in the Event Viewer, as previously discussed. They can be: <ul><li>Malicious</li><li>Suspicious</li><li>Inconclusive</li><li>Likely Safe</li><li>PUP (Potentially Unwanted Program)</li><li>Safe</li></ul> |
| Repeat Every/On          | These options enable you to define the frequency and schedule when this query will be run.   |
| Trigger Playbook Actions | Specifies whether to allow FortiEDR to trigger the corresponding Playbook action of the triggered security event from the scheduled query. Enabling this checkbox allows FortiEDR to automatically apply the action of the Playbook that is assigned to the Collector Group the triggering device belongs to.   |