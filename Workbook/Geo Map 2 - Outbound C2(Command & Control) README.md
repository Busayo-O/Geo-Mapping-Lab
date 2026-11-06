<h1>JWipe - Outbound Network Connections</h1>
Description</h2>
In this project, Microsoft Defender XDR Advanced Hunting and Kusto Query Language (KQL) were used to investigate outbound network connections from monitored devices (Virtual Machines in the Cyber Range).

The analysis identifies public IP addresses that monitored devices communicate with using the DeviceNetworkEvents table. It enriches external IP addresses with geographical information and identifies the number of network connections, affected devices, initiating processes, destination ports, and sample URLs.
<br />

Tools & Technologies Used
-Microsoft Defender XDR
-Microsoft Defender Advanced Hunting
-Microsoft Sentinel
-Azure Monitor Workbooks
-Log Analytics Workspace
-Kusto Query Language (KQL)
-IP Geolocation (geo_info_from_ip_address())
-DeviceNetworkEvents</h2>

- <b>PowerShell</b> 
- <b>Diskpart</b>

<h2>Environments Used </h2>

- <b>Windows 10</b> (21H2)

<h2>Program walk-through:</h2>

<p align="center">
Launch the utility: <br/>
<img src="https://i.imgur.com/62TgaWL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
Select the disk:  <br/>
<img src="https://i.imgur.com/tcTyMUE.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
<br />
<br />
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
