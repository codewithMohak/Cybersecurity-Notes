# Filtering Results
## In Splunk , commands are linked together using a pipe symbol `|`. Each pipe passes the output of one command into the next, allowing you to refine your result step by step.
![[Pasted image 20260702114916.png]] 
# Useful Filtering Commands
## Fields
## The `fields` command controls which fields appears in the search results.
## Instead of showing hundreds of fields, it displays only the ones you care about.
```
index=windowslogs | fields host User SourceIp
```
![[Pasted image 20260702132051.png]]
# Dedup
## The dedup command removes the duplicate values from the search results.
### For Example 
If our logs contain seven distinct IP addresses in the **SourceIp** , the result will return seven events, one for each unique IP.
![[Pasted image 20260702132910.png]]
# Rename
## The `Rename` command is used to change the name of a field in your search results. This can help improves the readability of your search results, especially if the original  fields are too long or not suitable.
```
index=windowslogs 
| fields EventID User Image Hostname SourceIp
| rename User as Employee
```
![[Pasted image 20260703000048.png]]
### This Command is also useful to flatten JSON or XML subfields.
#### For Example , for a JSON log entry  like `{"request" :{"path" : "/admin","ip :" 10.0.0.2"}}`
#### Splunk will create two fields : `request.path` and `request.ip` . If you don't want to type prefix every time , consider removing it like in the example below:
```
index=jsondata
| rename request.* as *
```
# Regex Command 
## The `regex` command filters search results using patterns instead of exact words.
## Think of it like this :
>Normal Search : Find an exact word.
>Regex Search : Find anything that matches a pattern.
### If you want to find every executable file, you don't want to search one by one.
```
index=windowslogs
| regex Image="\.exe$"
```
![[Pasted image 20260703004714.png]]
# Structure Results
## When working with the log data , raw search results can be overwhelming , and some event may not be relevant to the investigation.
## SPL command enable you to filters, order and format these results, allowing you to focus on the most important information.
# Table Command
## The `table ` command allows you to select only the field that you are interested in viewing and display them in a clean , readable format.
## This is especially useful when building the timelines, investigation specific hosts or users , or comparing multiple fields.
```
index=windowslogs
| table _time EventID Hostname SourceName
```
# Useful Structuring Commands
## These command help us to:
- View only a few events.
- Sort events.
- Reverse their order.
- Make investigation easier.

| Command   | Example                          | Explanation                                                                                                      |
| --------- | -------------------------------- | ---------------------------------------------------------------------------------------------------------------- |
| `head`    | `index=windowslogs \| head 20`   | Return the first (newest) `20` events, without waiting for the complete results. It help to speed up the search. |
| `tail`    | `index=windowslogs \| tail 10`   | Return the last (oldest) `10` events, without waiting for the complete results. It help to speed up the search.  |
| `sort`    | `index=windowslogs \| sort User` | This will sort the log order in the alphabetical order in the fields.                                            |
| `reverse` | `index=windowslogs \| reverse`   | This command will reverse the order the of the events.                                                           |
# Timelining with Table
## The `table` command can be used to create timelines that help analysts visualize how events unfolded.
## By organizing the key fields, we  can reconstruct the sequence of actions that occurred on a system.
```
index=windowslogs Hostname= Salena.Adam
| table_time Hostname EventID Category 
| reverse
```
![[Pasted image 20260703091839.png]]
# Subsearch
## A `Subsearch` is simply a search  inside  another search.
## Syntax 
```
[search ...]
```
### Everything inside `[ ]` runs first.
# Why do we need Subsearch?
## Imagine you have two different logs.
## Process Creations logs(Sysmon)

| EventID | Image          | User  | LogonId |
| ------- | -------------- | ----- | ------- |
| 1       | cmd.exe        | James | 0x1234  |
| 1       | powershell.exe | Alice | 0x5678  |

This tells you:
- Which process is executed.
- Which user executed it.
But it doesn't tell you how the user logged in.
# Login log (Windows Security)

| EventID | TargetLogonId | LogonType | IP Address |
| ------- | ------------- | --------- | ---------- |
| 4624    | 0x1234        | 10        | 10.10.10.5 |
| 4624    | 0x5678        | 2         | Local      |

This tells you:
- Login type.
- IP address.
But it **doesn't tell you** which process was executed.
```
index-windowslogs EventID=1
| join LogonId
  [search index=windowslogs EventID=4624
  | rename TragetLogonId as LogonId
  | fields LogonId LogonType IpAddress]
| table_time Image User LogonType IpAddress
```
![[Pasted image 20260703092916.png]]
