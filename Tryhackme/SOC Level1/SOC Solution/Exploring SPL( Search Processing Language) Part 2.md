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