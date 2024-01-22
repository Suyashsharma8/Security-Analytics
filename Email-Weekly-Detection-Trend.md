This query displays the weekly detection trends captured by MDO and EOP for Phish, Malware, and Spam.
```KQL
EmailEvents
| where Timestamp > ago(7d)
| where isnotempty(ThreatTypes)
| extend StringtoDynamic = split(ThreatTypes, ", ")
| mv-expand StringtoDynamic
| extend EmailThreat = tostring(StringtoDynamic)
| summarize Case = count() by EmailThreat, bin(Timestamp, 1d)
| render linechart 
