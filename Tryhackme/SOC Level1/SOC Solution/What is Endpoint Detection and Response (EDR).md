## Endpoint Detection and Response (EDR) is a software is used by security operations teams to detect , contain, investigation and remediation cyberattack such as ransomware and other malware.

## Why is EDR important?
- There are many benefits that underscore why EDR is important in cybersecurity, but the key reason is to **detect and mitigate** damage from **cyberthreats** and prevent **data exfiltration** to bad actors.
- EDR is important because it helps :
  1. **Reduce attack surfaces and eliminates blind spots.**
  2. **Blocks sophisticated cyberattacks.**
  3. **Proactively hunts threats and automate remediation.**
  4. **Increases the efficiency and speed security operations.**
  5. **Integrate detection and response with SIEM , SOAR, XDR, and Security operation solutions.**
## How does an EDR works?
![[Pasted image 20260617222539.png]]
![[Pasted image 20260617222644.png]]
## EDR Telemetry
### What is Telemetry?
Telemetry is a detailed data collected from an endpoint about everything happening on it, such as processes , network connections, files, commands, and registry changes.
### Collected Telemetry
- Usually many activities are going on in the endpoints, most of which are legitimates.
- Let's take a brief look at some of the telemetry that it collects:
  1. **Process Executions and Terminations :**
     It keeps track of all the running and idle processes, which helps to identify suspicious child-parent process relationships, suspicious executables initiating a process, malware payload, etc.
  2. **Network Connections** :
     All the endpoints' network connections are monitored, which helps identify any connection to a C2 server, unusual port usage, data exfiltration, or lateral movement within the network.
  3. **Command Line Activity** :
     It captures all the commands executed on the endpoints in CMD, PowerShell, etc., which helps to identify malicious command execution, obfuscated PowerShell script executions, which are often missed by a traditional antivirus.
  4. **Files and Folders Modifications** :
     Threat actors modify different files and folders during data staging, ransomware executions, and malicious file dropping. The EDR tracks this.
  5. **Registry Modifications** :
     The registry is a goldmine of information about the configurations in a Windows system. There are many registry modifications that occur during a malicious activity, and most of these are monitored by the EDR.
### Detection and Response Capabilities
### Detection :
- Based on telemetry received from the endpoints, some advance detection techniques are applied to this data. Some of these techniques includes :
  1. Behavioral Detection
  2. Anomaly Detection
  3. Indicator of compromise(IOC) Matching
  4. MITRE ATT&CK Mapping
  5. Machine Learning Detection

## **Behavioral Detection** :
-  Instead of only checking if a file is known malware , EDR looks at what the file is doing .
-  Sometimes malware looks harmless but behaves suspiciously.
  -  Example:![[Pasted image 20260618010438.png]]
-  Behavioral Detection looks at suspicious actions and behaviors instead of only looking for known malware signatures.
## **Anomaly Detection** :
   - Anomaly Detection finds activities that are different from the normal behavior of the endpoint.
   - **Example:** On one of the endpoints, a process modifies an auto-start registry key, which is not a common behavior on the endpoint.
## Indicator of Compromises (IOC) Matching :
   - Malicious IP address
   - Malicious file hash
   - Malicious domain
   - Known malware filename
- Example :
  - User downloaded malware.exe ↦Hash Value is generated ↦ Hash value is compared with EDR threat intelligence database.
- IOC Matching compares files, IPs, domains, and hashes against known threat intelligence databases.
## **MITRE ATT&CK Mapping** :
   - Any activity flagged by the EDR is not only marked as malicious or suspicious but also mapped with the MITRE Tactic and Technique (attack stage) that the particular activity was on.
   - **Example:** If the EDR flags the creation of a scheduled task for any reason, it will likely map this activity to the following:
     - Tactic: Persistence
	- Technique: Scheduled Task/Job.
## Machine Learning Detection :
   - Some attack look normal when viewed one action at a time.
   - Machine learning looks at the entire chain of events.
- Example :
  ```
Word
 ↓
PowerShell
 ↓
Download Payload
 ↓
Persistence
  ```
  - Machine Learning detects complex attack patterns by analyzing the complete sequence of activities instead of a single event.
### Response :
Think of it like this :
![[Pasted image 20260618124409.png]]
- **The purpose of response is to contain, stop, and  investigate  the attack.**
1. **Isolate Host :**
2. **Terminate process :**
3. **Quarantine** :
4. **Remote Access** :
5. **Artefact Collection** :

## Isolate Host :
### What does it means?
- Disconnect the infected computer from the network.
## Why ?
- Attacker often start with one computer and then move to others.
### Example :
- A larger company laptop is communicating with a ransomware servers.
### Easy Definition
> Isolate Host disconnects an infected endpoint from the network to stop the attack from spreading.

## Terminate Process :
### What does it means?
- Stops the malicious program that is currently running.
### Why not always isolate?
- Some system runs  critical business operations.
### For Example :
- Bank Servers.
- Hospital Servers.
- Production Servers.
Disconnecting  them causes  major business problems.
### Easy Definition
> Terminate process  stops a running malicious program without disconnecting  the entire endpoint.
## Quarantine :
### What does it means ?
- Moves  a suspicious or malicious file to a safe location.
## Example
File found:
```
virus.exe
```
EDR quarantines it.
```
virus.exe     
 ↓
Quarantine Area
```
### Easy Definition :
> Quarantine moves a suspicious file to an isolated files to an isolated location where it cannot run.
## Remote Access :
### What it means?
- The analyst remotely  open a shell  on the endpoint.
### Why?
- Sometimes built-in EDR action are not enough 
### The analyst may need to:
- Run commands
- Check files
- Collect evidence
- Run scripts
- Investigate deeper
### Easy Definition
> Remote Access allows analysts to remotely investigate and control an endpoint through a command shell.
## Artefact Collection
### What does it means?
- Collect evidence from the endpoint for investigation.
### Common Artefacts

### Memory Dump

A snapshot of RAM.

Can reveal:

- Malware
- Passwords
- Running processes
### Event Logs

Windows logs showing:

```
Login EventsErrorsProcess CreationSecurity Events
```
### Folder Contents

Analysts may collect:

```
DownloadsTemp FolderDesktop Files
```

to investigate malware.
### Registry Hives

Useful for finding:

- Persistence
- Startup entries
- Malware configurations

### Easy Definition
> Artefact Collection gathers evidence from an endpoint for forensic investigation and reporting.