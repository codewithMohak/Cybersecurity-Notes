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
# Search Operators
## Free text search :
The easiest way to use SPL is with a free-text search.
>Example
>index = windowslogs alice

The query will search all the events containing alice keyword (case-insensitive).
## Search  Operators :
Splunk operator are the building blocks used to construct any search query.
These operator are used to filter ,remove and refine your search result based on the specific criteria.
Below , we will cover relational, logical , and wildcard operators.
### Relational Operators :
These operators are used to compare to expressions.
They help you filter logs based on specific conditions.

| Operator                      | Example                 | Explanation                                                             |
| ----------------------------- | ----------------------- | ----------------------------------------------------------------------- |
| Equals `=`                    | `UserName=Mark`         | Search all event where `UserName` is equal to `Mark`.                   |
| Not Equal to `!=`             | `UserName !=Mark`       | Search all event in which field name `UserName` is not equal to `Mark`. |
| Less than `<`                 | `Age<10`                | The field `Age` has a value less than to `10`.                          |
| Less than or Equal to `<=`    | `Age<=10`               | The field `Age` has a value less than or equal to `10`.                 |
| Greater Than `>`              | `Outbound_traffic>50`   | The `Outbound_traffic` field is greater than `50`.                      |
| Greater Than or Equal to `>=` | `Outbound_traffic>= 50` | The `Outbound_traffic` field is greater than or equal to `50`.          |
### Example :
Suppose your are investigating an suspicious login.

 Instead of searching all the users
```
index=windowslogs
```

You can ignore the system-generated events:
```
index=windowslogs AccountName!=SYSTEM
```
![[Pasted image 20260701161621.png]]
# Logical Operator :
Splunk support logical operators are used to combine multiple conditions in a search. They work with True and False values.
#### For Example :
- Finds logs where two conditions are true.
- Finds logs where either one of the conditions is true.
- Exclude certain logs.

| Operator | Example                                      | Explanation                                                                |
| -------- | -------------------------------------------- | -------------------------------------------------------------------------- |
| `NOT`    | `NOT UserName=*`                             | Show events where the UserName field does not exist (Different from `!=`). |
| `AND`    | `UserName=David AND IP Address= 10.10.10.10` | Show events where both the condition are true.                             |
| `OR`     | `UserName=David OR UserName=John`            | Show events where either condition is true.                                |
| `IN`     | `UserName IN (David, John)`                  | A shorter way to write  multiple OR conditions.                            |
### Hands on Example :
Suppose this query 
```
index=windowslogs AccountName!=SYSTEM AND AccountName=James
```

It can be also written in such way:
```
index=windowslogs AccountName!=SYSTEM AccountName=James
```

>In Splunk  , when two conditions are written next to each other, AND is implied.

#### What does it means?
- Search inside the windowslogs index.
- Ignore events where AccountName = SYSTEM.
- Show only events where AccountName = James.
So the result is :
> Show all logs of James , but exclude any logs generated by the SYSTEM accounts.

![[Pasted image 20260701164610.png]]
# Wildcards and CIDR Search
## Splunk allow you to search using  wildcards and CDIR notations.
### These are helpful when:
- You don't know the exact value .
- You want to search for a group of similar values.
- You want to search the entire IP Subnet instead of Single Ip address.
# Wildcard (`*`) :
## The `*` symbol means :
> Match anything.
### It replaces one or more unknown characters.
#### Example 1
```
status=*fail*
```
**Meaning:**
Show all the events where the status field contain the word fail.

It matches :
> failed
> failure
> appfail
> loginfailed
#### Example 2
```
DestinationIp=172.*
```
**Meaning:**
Shows all the events where the destination IP starts with 172.

Example matches :
```
172.16.1.5
172.18.5.22
172.20.100.4
172.90.0.1
```

Dose not matches :
```
192.168.1.10
10.0.0.5
```
# CIDR Search
## CIDR (Classless Inter-Domain Routing) let's you search entire network or subnet.
### Example:
```
DestinationIP=172.18.0.0/16
```
**Meaning:**
Shows all the events where the destination IP belongs to the 172.18.x.x network.
![[Pasted image 20260701171155.png]]
# Order of Evaluation 
## When Splunk reads your search query, it follows certain rules to decide which condition to evaluate first. The two most important concepts are :
- Quotes (`" "`)
- Parentheses(`( )`)
# Quotes
## In Splunk , quotation marks `""`  are used to define exact phrases or strings.
## Quotes can be used to escape search operators.
### For Example :
- `index=windowslogs failed login` : Search for the events with failed and login keywords, in any order.
- `index=windowslogs "failed login"` : Search for the exact phrase "failed login", word order matters.
- `index=windowslogs "TO BE OR NOT TO BE"` : Search for the exact phrase containing NOT and OR
# Parentheses
## You can utilize parentheses in Splunk to help group conditions together and control how search is applied.
### For example, imagine you want to search containing alice and bob together or charlie alone.

| Your Search                                    | How Splunk Evaluates it                        |
| ---------------------------------------------- | ---------------------------------------------- |
| `index=windowslogs alice AND bob OR charlie`   | `index=windowslogs alice AND (bob OR charlie)` |
| `index=windowslogs (alice AND bob) OR charlie` | `index=windowslogs (alice AND bob) OR charlie` |

[^1]
[^1]: [[Exploring SPL( Search Processing Language) Part 2]]
