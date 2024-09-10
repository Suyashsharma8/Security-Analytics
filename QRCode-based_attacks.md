Volume of inbound emails with QR code in last 30 days:

```kql
EmailEvents
| where TimeGenerated > ago(30d)
| where EmailDirection == "Inbound"
| join EmailUrlInfo on NetworkMessageId
| where UrlLocation == "QRCode"
| summarize dcount(NetworkMessageId) by bin(TimeGenerated, 1d)
| render timechart
```

Emails with QR Code Blocked in last 30 days

```kql
EmailEvents
| where TimeGenerated > ago(30d)
| where EmailDirection == "Inbound"
| join EmailUrlInfo on NetworkMessageId
| where UrlLocation == "QRCode"
| where DeliveryAction =="Blocked"
| summarize dcount(NetworkMessageId) by bin(TimeGenerated, 1d)
| render timechart
```
