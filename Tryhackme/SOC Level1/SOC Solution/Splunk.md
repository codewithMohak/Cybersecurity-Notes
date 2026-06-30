## Splunk is one of the most popular SIEM (Security Information and Event Management) solution used by organization. It help the security teams :
- Collect logs from different devices and systems.
- Analyzing logs to understand what is happening.
- Correlate related events from the multiple log sources in real time.
- Provide better visibility into network and system activities.
- Detect threats faster by generating alerts for suspicious behavior.
![[Pasted image 20260629154535.png]]
## Splunk Components
Splunk has three main components :
- Forwarder
- Indexer
- Search Head
## Splunk Forwarder
Splunk forwarder is a lightweight agent installed on a computer or server that you want to monitor.
Its main job is to :
- Collect logs and data from the system.
- 📤 Send the collected data to the **Splunk server (Splunk Instance)** for analysis.
### Some of the sources are :
- Web server generating web traffic.
- Windows machine generating Windows Event Logs, PowerShell, and Sysmon data.
- Linux host generating host-centric-logs.
- Database generating DB connection requests, response and errors.
![[Pasted image 20260629183558.png]]
The forwarder collects the data from the log sources and sends it to the Splunk Indexer.
## Splunk Indexer 
- Splunk Indexer plays the main role in processing the data it receives from forwarders.
- It parses and normalizes the data into field-value pairs, categorizes it, and stores the results as events, making the processed data easy to search and analyze.
- Now , the data , which is normalized and stored by the indexer, can be searched by the **Search Head**.
## Search Head
- Splunk Search Head is the place within the Search & Reporting App where users can search the indexed logs, as shown below.
![[Pasted image 20260629185744.png]]
- The searches are done using SPL (Search Processing Language), a powerful query language for searching indexed data.
- When the user performs a search, the request is sent to the indexer, and the relevant events are returned as field-value pairs.
- The Search Head also allows you to transform results into presentable tables and visualizations such as pie, bar and column charts as shown below:
## Navigating Splunk
Home screen as shown below :
![[Pasted image 20260629193641.png]]
## Splunk Bar
The top panel is the Splunk Bar as shown below :
![[Pasted image 20260629194123.png]]
In the Splunk Bar, we have the following option available:

- Messages : View system-level notifications and messages.
- Settings: Configure Splunk instance settings.
- Activity: Review the progress of search jobs and processes.
- Help: View tutorials and documentation.
- Find : Search across the App.
## Apps Panel
This panel shows the apps installed for the Splunk instance.
The default app for every Splunk installation is Search & Reporting.
![[Pasted image 20260629203501.png]]
## Explore Splunk
This panel contains quick links to add data to the instance, add new apps, and access the documentation.
![[Pasted image 20260629205545.png]]
## Adding Data
To upload the data successfully, you must follow five steps, which are explained below:

1. **Select Source:** Choose the Log file and the data source.
2. **Select Source Type:** Select what type of logs are being ingested, e.g, JSON, syslog.
3. **Input Settings:** Select the index where these logs will be dumped and the HOSTNAME to be associated with the logs.
4. **Review:** Review all the configurations.
5. **Done:** Complete the upload. Your data will be uploaded successfully and ready to be analyzed.
## Cheat Sheet of Commands
# CMD 1

```
index="vpn_logs" ------> Filename
| stats count ---------> Event occured counts
```
# CMD 2
```
index="vpn_log"
| search UserName="Maleena"
| stats count
```
# CMD 3
```
index="vpn_log"
| search Source_ip="107.14.182.38"
| stats values(UserName) as UserName count
```
# CMD 4
```
index="vpn_log"
| search Source_Country!="France"
| stats count
```
# CMD 5
```
index="vpn_log"
| search Source_ip="107.3.205.58"
| stats count
```
