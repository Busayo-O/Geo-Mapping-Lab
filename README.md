<h1> A Sentinel Geomaps - Geo Threat Hunting with Microsoft Sentinel Workbooks</h1>
This is a visual representation of a KQL Query. It turns raw data in the Log Analytics workspace into interactive dashboards(live maps)-from bar charts to geo-maps. This Visualize where threats are coming from and going to.

<h2>Description</h2>
This project- builds a four(4) Geo-Threat-map workbook built in Microsoft Sentinel that natively geolocate IP addresses(i.e enrich IP addresses with location data) traffic to/from the Cyber Range into interactive world maps. This is built on the LOG(N) Pacific Cyber Range- Azure / Microsoft Defender/ Microsoft Sentinel.
<br />

<h2>How it was deployed </h2>
a) Go to **Microsoft Defender portal > Microsoft Sentinel > Threat Management > Workbooks** <br />

b) Click ** Add workbook** <br />

c) Click ** Advanced Editor** <br />

d) Paste the JSON from Workbooks <br />

e) Click ** Apply** > **Save** <br />

<h2>Languages and Utilities Used</h2>

- <b>PowerShell</b> 
- <b>Diskpart</b>

<h2>Program walk-through:</h2>

<p align="center">
(i) Inbound Authentication Origins- Geolocation Analysis: <br/>
<img src="https://i.imgur.com/62TgaWL.png" height="80%" width="80%" alt="Disk Sanitization Steps"/>
  // === Inbound auth origins (geo) ===
  # Inbound Authentication Origins – Geolocation Analysis

## Project Overview
Kusto Query Language (KQL) is used to investigate the geographic origins of remote authentication attempts against monitored devices(Virtual machine in the Cyber Range).
The analysis identifies public IP addresses associated with remote logons, enriches them with geolocation information, and distinguishes between successful and failed authentication attempts.

## Objectives
- Identify the geographic origins of remote authentication attempts.
- Identify public IP addresses initiating remote logons.
- Differentiate successful and failed login attempts.
- Identify devices targeted by remote authentication attempts.
- Identify potentially suspicious authentication patterns.

## Data Source
- **Table:** `DeviceLogonEvents`
- **Platform:** Microsoft Defender XDR
- **Language:** Kusto Query Language (KQL)

## KQL Query

```kql
DeviceLogonEvents
| where RemoteIPType == "Public"
| where isnotempty(RemoteIP)
| where LogonType in ("Network", "RemoteInteractive")
| extend geo = geo_info_from_ip_address(RemoteIP)
| extend Latitude = toreal(geo.latitude),
         Longitude = toreal(geo.longitude),
         Country = tostring(geo.country),
         City = tostring(geo.city)
| where isnotempty(Latitude) and isnotempty(Longitude)
| summarize Attempts = count(),
            Successes = countif(ActionType == "LogonSuccess"),
            Failures = countif(ActionType == "LogonFailed"),
            TargetedDevices = dcount(DeviceName),
            Accounts = make_set(AccountName, 25)
    by RemoteIP, Country, City, Latitude, Longitude
| extend MapLabel = strcat(RemoteIP, " (", Country, ") — ",
                           Successes, " success / ", Attempts, " total")
| project Latitude, Longitude, MapLabel, Attempts,
          Successes, Failures, TargetedDevices,
          RemoteIP, Country, City, Accounts
| order by Successes desc, Attempts desc
```
KQL QUERY-Screenshot showing the query running in Advanced Hunting 
<img src="https://i.imgur.com/5iusHUP.png" height="80%" width="80%"/>
                                  


## Analysis Performed

1. **IP Filtering:** Filters authentication events originating from public IP addresses.
2. **Logon Filtering:** Focuses on Network and RemoteInteractive logon types.
3. **Geolocation Enrichment:** Uses IP geolocation to identify the country, city, latitude, and longitude.
4. **Event Aggregation:** Counts total authentication attempts, successful logins, and failed logins.
5. **Device Analysis:** Identifies the number of distinct devices targeted.
6. **Account Analysis:** Collects account names associated with the authentication attempts.

## Security Value
This analysis helps to:
- Investigate remote authentication activity.
- Identify unusual geographic login origins.
- Detect repeated authentication failures.
- Identify potentially compromised accounts.
- Support threat hunting and incident investigations.

## Expected Output
The query produces geographic coordinates and authentication statistics that is used to plot remote authentication origins on the map.

**Key metrics:**
- Attempts
- Successful logins
- Failed logins
- Targeted devices
- Source IP addresses
- Countries and cities
- Associated accounts

## Conclusion
This demonstrated how KQL is used for security monitoring, authentication analysis, IP geolocation enrichment, and threat hunting within a Microsoft Defender environment.

<img src="https://i.imgur.com/6jpxeX8.png" height="80%" width="80%" />https://i.imgur.com/6jpxeX8.png


  https://docs.google.com/document/d/1Z3lHN_3EdRFZE6E8WKmX_grb33svmscchUeOdFSTXWQ/edit?tab=t.og6nief6l7gc 
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
