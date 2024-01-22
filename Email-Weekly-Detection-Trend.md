This query displays the weekly email detection trends captured by Microsoft defender for Office for Phish, Malware, and Spam using KQL for sentinel.
```KQL
EmailEvents
| where TimeGenerated > ago(7d)
| where isnotempty(ThreatTypes)
| extend StringtoDynamic = split(ThreatTypes, ", ")
| mv-expand StringtoDynamic
| extend EmailThreat = tostring(StringtoDynamic)
| summarize Case = count() by EmailThreat, bin(TimeGenerated, 1d)
| render piechart 
