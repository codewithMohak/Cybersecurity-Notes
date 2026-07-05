# Anomaly Detection
## `Anomaly Detection` means finding unusual or unexpected behavior  in your data.
### For Example , Imagine a data set of 2,000 VPN  logins with just four fields : time of the login, username , source IP, and source country.
#### How would you identify logins from the unexcepted countries, if field statistics don't show any anomalies?

![[Cyber-Security/Attachment/Attachment/Exploring SPL( Search Processing Language) Part 3-1783220130438.webp]]
# Detecting Outliers by Country
## For a US-based user , logging in from the US is expected, but for an EU-based user, it might be the sign of intrusion.
## The `eventstats` command is very similar to the `stats`, but preserves raw event for further processing ; and `where` command is like `search`, but a more powerful.
### Query

```
index=windowslogs
| eventstats count as logins_by_user by user
| eventstats count as logins_by_user_country by user src_country
| eval country_freq=logins_by_user_country/logins_by_user
| where country_freq <0.1
| table _time user scr_ip src_country country_freq
```

![[Exploring SPL( Search Processing Language) Part 3.png]]
# Detecting Outliners by Hour
## Following  a similar approach, you can hunt for logins during anomalous hours.

```
index=vpnlogs
| eval hour= tonumber(strftime(_time, "%H")) + tonumber(strftime(_time, "%H"))/60
| eventstats avg(hour) as typical_hour stdev(hour) as stdev_hour by user
| eval zscore=abs(hour -typical_hour)/stdev_hour
| where zscore>3
| eval hour=round(hour, 2),typical_hour=round(typical_hour,2)
| eval stdev_hour=round(stdev_hour, 2),zscore=round(zscore, 2)
| table _time user src_ip src_country hour typical_hour stdev_hour zscore
| sort- hour_zscore
```

![[Exploring SPL( Search Processing Language) Part 3 png]]