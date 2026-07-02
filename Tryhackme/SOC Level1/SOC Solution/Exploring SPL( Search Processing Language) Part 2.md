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