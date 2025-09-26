---
title: ATT&CK in FAZ
menuTitle: ATT&CK in FAZ
weight: 20
---

With the appropriate license, you can leverage the ATT&CK® matrix in the FortiAnalyzer GUI:
- Incidents & Events > Incidents > MITRE ATT&CK®

FortiAnalyzer associates incident and event information with the relevant tactics and techniques. FortiAnalyzer also displays coverage in the MITRE ATT&CK matrices, so you can determine which [event handlers](https://docs.fortinet.com/document/fortianalyzer/7.6.4/administration-guide/444315/event-handlers) help to cover specific tactics and techniques.

### ATT&CK®

You can review incident and event information organized within the MITRE ATT&CK matrix from the Attack tab. Each technique includes a hyperlink to the relevant information at https://attack.mitre.org/techniques. You can filter the matrix using the time frame dropdown, and you can refresh the matrix as needed.

![faz_attack](faz_attack.png?width=600px)

If there are events associated with the technique, an icon and count displays on the tile. A separate icon and count displays for the associated incidents as well. Mouse over the tile to display the information in a tooltip. If there are sub-techniques, the tooltip breaks down which sub-technique the events and incidents are associated with.

### Coverage

You can review event handler coverage according to the MITRE ATT&CK matrix from the Coverage tab.

![faz_coverage](faz_coverage.png?width=600px)

When a basic or correlation event handler is associated with a technique, it will be included as part of the coverage for that technique. The tile displays an icon and count for associated event handlers. Mouse over the tile to display the information in a tooltip. This includes the total event handler count and a breakdown of the count for each sub-technique, if they are available.

{{% notice info %}}One event handler can be associated to multiple techniques and sub-techniques.{{% /notice %}}

Click a tile with coverage to open a table view of event handlers for that technique. 

![faz_details](faz_coverage2.png?width=600px)

The table includes the following information:

| Column	| Description |
|-------|-------------|
|State	|The state of the event handler: *Enabled or Disabled*.|
|Event Handlers	|The name of the event handler. Click the name to view the event handler configuration.|
|Description | The description of the event handler.|
|Technique |The technique or sub-technique(s) associated with the event handler. If there are multiple sub-techniques associated with the event handler, the count will be provided in this column. Click the count to display which sub-techniques are associated with the event handler.|

