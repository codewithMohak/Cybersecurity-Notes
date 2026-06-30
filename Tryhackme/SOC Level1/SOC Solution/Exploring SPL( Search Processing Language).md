## Splunk is a powerful Security Information and Event Management(SIEM) platform that allow you to search, visualize and investigate the log data.
## Its Search Processing Language (SPL) is the key to turning larger volumes of data into practical results.
## Learning Objectives
- Understand how SPL processes and filters log data.
- Chain and supply SPL command effectively.
- Visualize log data with charts and statistic.
- Apply your SPL skills to use anomaly detection.
# Search & Reporting
## Splunk's Search & Reporting App is the default interface used for searching and analyzing data on the Splunk home page.
## It has various functionalities that assist analyst in improving the search experience.
### Upon accessing the app, we discover several functionalities:
- Search Head
- Time picker
- Search History
- Data Summary 
![[Pasted image 20260630175900.png]]
## Your First Search
To search logs in Splunk, you use the **Search Head**.
![[Pasted image 20260630190748.png]]The first query is:
```
index=windowslogs
```
or
```
index = windowslogs
```
Both are correct.
# Field Sidebar
## When Splunk display logs, it automatically extracts useful information called field.
## The field sidebar is on the left side of the search page.
### It help us to understand what's inside logs.
#### Selected Fields:
These are the fields  Splunk show by default.
#### Interesting Fields:
Pulls the interesting fields it finds and display them in the left panel.
#### Numeric Fields `#`:
This symbol  represents fields that contain numerical values.
#### Alpha- numeric Fields `α` :
The alpha symbol represents finds that contains strings(text values).
#### Count :
The number of events containing the listed field.
#### More available fields :
If more field are available, they can be accessed and selected here.
