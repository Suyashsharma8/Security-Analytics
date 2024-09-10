This workbook is used to visualize the different threat types received from the MDTI connector to Sentinel.

```kql
ThreatIntelligenceIndicator
| summarize Total = count() by ThreatType
| render piechart with(title="Threat Intelligence Threat Types")
```
