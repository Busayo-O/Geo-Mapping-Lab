<h1> Inbound Authentication Origins – Geographic Threat Analysis</h1>
<h2>Description</h2>
In this project, Microsoft Sentinel / Azure Monitor Workbooks and Kusto Query Language (KQL) was used to investigate the geographic origins of remote authentication attempts against monitored devices(Virtual Machines in the Cyber Range).
The analysis identifies public IP addresses associated with remote logons from the DeviceLogonEvents table, enriches the public source IP addresses with geolocation information, and distinguishes between successful and failed authentication attempts.
It also distinguishes successful and failed authentication attempts to help identify potentially suspicious remote access activity..
<br />

<h3> Tools & Technology Used
  
- Microsoft Sentinel
- Azure Monitor Workbooks
- Microsoft Defender XDR
- Log Analytics Workspace
- Kusto Query Language (KQL)
- IP Geolocation (geo_info_from_ip_address())
- DeviceLogonEvents
  
<h4>How it was deployed </h2>
- Go to **Microsoft Defender portal > Microsoft Sentinel > Threat Management > Workbooks** <br />
- Click ** Add workbook** <br />
- Click ** Advanced Editor** <br />
- Paste the JSON from Workbooks <br />
- Click ** Apply** > **Save** <br />

## Objectives
- Identify the geographic origins of remote authentication attempts.
- Identify public IP addresses connecting to monitored devices(Vm).
- Monitored & differentiate between successful and failed login attempts.
- Identify devices targeted by remote authentication attempts.
- Identify potentially suspicious authentication patterns.
- Determine the number of devices targeted by each source IP.
- Identify accounts associated with authentication activity.
- Highlight unusual geographic authentication patterns.

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


  A)    KQL QUERY-Screenshot showing the query running in Advanced Hunting 
      
<img src="https://i.imgur.com/5iusHUP.png" height="80%" width="80%"/>


  B)  Geolocation Map-Screenshot showing the geographic origins of authentication events using the JSON Script

 <img src="https://i.imgur.com/6jpxeX8.png" height="80%" width="80%" />https://i.imgur.com/6jpxeX8.png     
                                  
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




  

