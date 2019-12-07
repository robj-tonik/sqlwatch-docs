# Notifications

The Notifications Engine is much more than just an alerting module. If fully customisable and flexible actions engine that enables SQLWATCH to not only monitor critical metrics  \(on top of its collection\) but also perform different actions based on thresholds.

## Concept

Actions are triggered by out of bounds checks \(triggers\). Checks are very simple and lightweight queries that can run actions if the returned value is not what we expect.

Checks are executed by an agent job every minute and can call multiple actions. Normally an action is called when the check returns WARNING or CRITICAL status, or, when it recovers from WARNING or CRITICAL back to OK \(RECOVERY\)

Actions are added to the queue to be processed by the queue processor \(another Agent Job\)

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
**Due to the fact that actions can execute arbitrary code, the action table should not be writable by non-SA users.**
{% endhint %}

## Example Notifications

Notifications are triggered on the back of a check and deliver simple but informational, text or HTML based alerts. More sophisticated notifications can be achieved by using reports.

### Pushover

![](../.gitbook/assets/image%20%2865%29.png)

### Email

![](../.gitbook/assets/image%20%2869%29.png)



