# Actions

Actions can be either a `T-SQL` or `PowerShell` command, or a pre-defined report. Actions are very flexible and there is no limit as to what can be triggered, as long as it is supported by either `T-SQL` or `PS`

Some of the examples include:

* Sending emails
* Sending Pushover notifications \([https://pushover.net/](https://pushover.net/)\)
* Sending Slack notifications \([https://slack.com/](https://slack.com/)\)
* Saving files to shared drives
* Executing T-SQL queries
* Executing programs
* Interfacing with HTTP protocols and APIs
* Executing pre-defined reports to provide more details about the encountered error
* Pushing data to log management systems \(Splunk, Graylog, Azure Monitor\)

{% hint style="danger" %}
**Due to the potential risk or executing any arbitrary code, the action table should not be writable by non-SA users.**
{% endhint %}

### Actions Log

### Templates

Action support templates



