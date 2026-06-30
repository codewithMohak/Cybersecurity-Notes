# Initial Access via Malicious office Document

## Summary :
### Malware Staging Activity Detected 
### The Process chain:
```
WINWORD.exe openend Macro-Enabled document invoice.docm 
↡
The document marco spawned CMD
↡
File saved to the public folder
↡
CMD executed cURL to fetch a remote playload from the external domain
```
## File Disposition
- File was written on the disk.
- File was not executed.
## Assessment 
> Behavioral consistent with malware staging tactics   ---- a technique where the attacker pre-positions the payload for later execution.
# Detection Details :
## Severity : High.
## Host : DESKTOP-HR01.
## Detection Time : Jun 18Th 2026 at 19:25

# Risk Assessment :

## MITRE ATT&CK Tactic
**Initial Access**
## Technique
**T1566.001 - Spearphishing Attachment**
