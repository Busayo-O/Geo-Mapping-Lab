<h1> Outbound Network Connections</h1>
<h2>Description</h2>

In this project, Microsoft Defender XDR Advanced Hunting and Kusto Query Language (KQL) were used to investigate outbound network connections from monitored devices (Virtual Machines in the Cyber Range).

The analysis identifies public IP addresses that monitored devices communicate with using the DeviceNetworkEvents table. It enriches external IP addresses with geographical information and identifies the number of network connections, affected devices, initiating processes, destination ports, and sample URLs.
<br />

<h2>Tools & Technologies Used</h2>

-  Microsoft Defender XDR
-  Microsoft Defender Advanced Hunting
-  Microsoft Sentinel
-  Azure Monitor Workbooks
-  Log Analytics Workspace
-  Kusto Query Language (KQL)
-  IP Geolocation (geo_info_from_ip_address())
-  DeviceNetworkEvents</h2>

<h2>How it was deployed</h2>

-  Signed in to the Microsoft Defender portal.
-  Navigated to Hunting > Advanced Hunting.
-  Selected the DeviceNetworkEvents table.
-  Pasted the KQL query into the query editor.
-  Selected the desired time range.
-  Clicked Run query.
-  Reviewed the results, including remote IP addresses, connection counts, affected devices, processes, and destination ports.
-  Used to visualize geographical locations, created an Azure Monitor Workbook or Microsoft Sentinel Workbook using the query results.
-  Configured a map visualization using the Latitude and Longitude fields.


<h2>Objectives</h2>

- Identified public IP addresses communicating with monitored devices.
- Investigated outbound network connections.
- Identified external geographical destinations.
- Excluded selected common Microsoft-related domains from the analysis.
- Identified devices communicating with external IP addresses.
- Identified processes initiating outbound network connections.
- Identified frequently contacted external IP addresses.
- Analyzed destination ports used during network communication.
- Support network threat hunting and incident investigations.

<h2>Program walk-through:</h2>

<p align="center">
<h2>A) KQL Query – Advanced Hunting:</h2>
 
Screenshot showing the KQL query running successfully in Microsoft Defender Advanced Hunting.: <br/>

<img src="https://i.imgur.com/rks1NQt.png" height="80%" width="80%"/>


<h2>B) Geographic Network Connections Map:</h2>

Screenshot showing the geographical origins of external network connections using the Microsoft Sentinel Workbook.: 

<img src= "https://i.imgur.com/nufKEUn.png" height="80%" width="80%"/>
<br />
<br />


<h2>Analysis Performed:</h2>

-  Public IP Filtering: Identified network connections involving public IP addresses.
-  Geolocation Enrichment: Used IP geolocation to identify the approximate country, state, city, latitude, and longitude associated with external IP addresses.
-  Connection Aggregation: Counted the total number of network connections to each external IP address.
-  Device Analysis: Identified the number of distinct devices communicating with each external IP.
-  Process Analysis: Identified the processes responsible for initiating network connections.
-  Port Analysis: Collected destination ports associated with external network communication.
-  Activity Threshold: Filtered for external IP addresses with at least five recorded connections.
-  Geographic Visualization: Prepared geographical coordinates and labels for map-based security analysis.


<h2> Security Value:</h2>

This analysis helped to:
-  Investigate outbound network communication.
-  Identify unusual external IP addresses.
-  Discover repeated connections to external destinations.
-  Identify processes responsible for network activity.
-  Investigate devices communicating with potentially suspicious IP addresses.
-  Examine unusual destination ports.
-  Support threat hunting and incident response investigations.
-  Improve visibility into external network communication patterns.</h2>

Enter the number of passes: <br/>
<img src="https://i.imgur.com/nCIbXbg.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Confirm your selection:  <br/>
<img src="https://i.imgur.com/cdFHBiU.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Wait for process to complete (may take some time):  <br/>
<img src="https://i.imgur.com/JL945Ga.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Sanitization complete:  <br/>
<img src="https://i.imgur.com/K71yaM2.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Observe the wiped disk:  <br/>
<img src="https://i.imgur.com/AeZkvFQ.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
</p>

<!--
 ```diff
- text in red
+ text in green
! text in orange
# text in gray
@@ text in purple (and bold)@@
```
--!>
m
