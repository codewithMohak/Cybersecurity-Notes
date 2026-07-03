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

![[Pasted image 20260702132051.png|697]]
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
# Transforming Commands
## `Transforming Commands` allow you to change the raw event data into the useful, summaries and visualizations.
## General Transformational Commands

| Command | Example                                  | Exaplanation                                |
| ------- | ---------------------------------------- | ------------------------------------------- |
| top     | `index=windowslogs \| top User limit=5`  | Show the users that appear most frequently. |
| rare    | `index=windowslogs \| rare User limit=5` | It shows the least common values.           |
# Highlight  Command 
## The `highlight` command does not filter or change the log.
## It simply highlights  specific words  when viewing logs in Raw mode.
```
index=windowslogs
| highlight User EventID Image "Process accessed"
```

![[Pasted image 20260703132654.png]]
# Stats Command
## The `stats` command summarize  data by performing calculation like :
- Count
- Sum
- Average
- Maximum
- Minimum
Instead of showing every log , it gives you statistics.

```
index=windowslogs
| stats count by EventID
```
# Sort the Results

```
index=windowslogs
| stats count by EventID
| sort EventID
```
# Common `stats` Functions

| Function | Example                   | Explaination                                          |
| -------- | ------------------------- | ----------------------------------------------------- |
| Average  | `stats avg(ProcessCount)` | Calculate the average value of the chosen field.      |
| Max      | `stats max(Price)`        | Return the maximum  value of the chosen field.        |
| Min      | `stats min(UserAge)`      | Return the minimum value of the chosen field.         |
| Sum      | `stats sum(Cost)`         | Return the sum of the chosen field vlalues.           |
| Count    | `stats count by SourceIp` | Return the number of occurrences of the chosen field. |

# Chart 
## The `chart` command is similar to `stats`, but it's designed for the visualizations.

```
index=windowslogs
| chart count by User
```

![[Pasted image 20260703145252.png]]
# Timechart
## The `timechart` command shows how data change over time.

```
index=windowslogs Image!=""
| timechart span=30m count by Image limit=5
```
# Data Enrichment and Field Manipulation
# IP Location
## The `IP Location` command adds geographical information to IP addresses.

```
index=windowslogs
| iplocation SourceIp
| stats count by Country
```

![[Pasted image 20260703181613.png]]
# Lookup
## A `lookup` adds  extra information from an external file.

```
index=windowslogs
| lookup user_roles Hostname OUTPUT UserRole
| stats count by Hostname UserRole
```

![[Pasted image 20260703184600.png]]
# Eval
## The `eval` command is used to create a new fields or modifies existing ones.
```
index=windowslogs
| eval LogonTypeDesc = case(LogonType == 3, "Network Logon" , LogonType ==5, "Service")
| stats count by LogonType LogonTypeDesc
```

![[Pasted image 20260703185354.png]]

# Next Continuous [[Exploring SPL( Search Processing Language) Part 3]]