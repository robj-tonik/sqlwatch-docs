# Send notifications to Slack and Teams

This is work in progress, in the meantime, please see this blogpost: 

{% embed url="https://sqlwatch.io/blog/how-to-send-notification-to-microsoft-teams/" %}

The integration with Slack is similar and also entails triggering a WebHook. The configuration is slightly different to Teams:

```text
$webhookurl = "https://hooks.slack.com/services/xxx"
$body = ConvertTo-Json @{
    pretext = "{SUBJECT}"
    text = "{BODY}"
}

Invoke-RestMethod `
    -Uri $webhookurl `
    -Method Post `
    -Body $body `
    -ContentType 'application/json'
```



