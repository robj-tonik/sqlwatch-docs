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
**Due to the fact that actions can execute arbitrary code, the action table should not be writable by non-SA users.**
{% endhint %}

### Definition

Action definition is stored in table `[dbo].[sqlwatch_config_action]`

![\[dbo\].\[sqlwatch\_config\_action\]](../../.gitbook/assets/image%20%2849%29.png)

#### Action executable

Executable can either be a command `action_exec` or a report `action_report_id` but not both. The `action_exec` expects optional parameters `{SUBJECT}` and `{BODY}` which are defined by the template.

If action triggers a report, the content of the report will be embedded in the `{BODY}` and action associated with the given report called instead:

```text
                     check -> action -> report -> action
```

This way we can also call stand alone reports that are not triggered by checks, for example daily or weekly Server overview report or even business reports.

Actions are executed by a PowerShell step in the SQL Server agent job and there are currently two types supported `T-SQL` and `PowerShell` which are invoked by either by `Invoke-SqlCmd` or `Invoke-Expression`

### Templates

Actions support templates. For example, we may want a short description in the Pushover notification and more details in an email notification. 

Templates are defined in `[dbo].[sqlwatch_config_check_action_template]`. Each status \(OK, WARNING and CRITICAL\) has its own subject and body templates which generate `{SUBJECT}` and `{BODY}` content required by the `action_exec`

To make it easier to build custom templates, a number of variables have been exposed for the end user:

| Variable | Description |
| :--- | :--- |
| {CHECK\_STATUS} | Status of the check \(OK,WARNING,CRITICAL\) |
| {CHECK\_NAME} | Name of the check |
| {CHECK\_ID} | ID of the check |
| {CHECK\_DESCRIPTION} | Description of the check |
| {SQL\_INSTANCE} | @@SERVERNAME |
| {CHECK\_QUERY} | Query executed by the check |
| {CHECK\_VALUE} | Value returned by the check |
| {CHECK\_LAST\_VALUE} | Value returned by the previous check. Useful for context. |
| {CHECK\_LAST\_STATUS} | Status of the previous check. |
| {LAST\_STATUS\_CHANGE} | Date Time when last status change has occurred.  |
| {CHECK\_TIME} | Date Time of the current check |
| {THRESHOLD\_WARNING} | Value of the warning threshold |
| {THRESHOLD\_CRITICAL} | Value of the critical threshold |

For example, if we have a simple check that does not call a report, the following plain text template:

```text
Check: {CHECK_NAME} ( CheckId: {CHECK_ID} )

Current status:  {CHECK_STATUS}
Current value: {CHECK_VALUE}

Previous value: {CHECK_LAST_VALUE}
Previous status: {CHECK_LAST_STATUS}
Previous change: {LAST_STATUS_CHANGE}

SQL instance: {SQL_INSTANCE}
Alert time: {CHECK_TIME}

Warning threshold: {THRESHOLD_WARNING}
Critical threshold: {THRESHOLD_CRITICAL}

--- Check Description:

{CHECK_DESCRIPTION}

--- Check Query:

{CHECK_QUERY}

---

Sent from SQLWATCH on host: {SQL_INSTANCE}
https://docs.sqlwatch.io
```

Will result in the following content:

![](../../.gitbook/assets/image%20%2834%29.png)

In addition, actions that trigger reports have these variables exposed:

| Variable | Description |
| :--- | :--- |
| {REPORT\_TITLE} | Report title |
| {REPORT\_DESCRIPTION} | Report description |
| {REPORT\_CONTENT} | Report content \(output from the report execution in HTML\) |

For example, if we have a check that calls **Disk Utilisation Report**, the following action template \(note the `HTML` tags and the **Report Content** section\):

```text
<p>Check: {CHECK_NAME} ( CheckId: {CHECK_ID} )</p>

<p>Current status:  {CHECK_STATUS}
<br>Current value: {CHECK_VALUE}</p>

<p>Previous value: {CHECK_LAST_VALUE}
<br>Previous status: {CHECK_LAST_STATUS}
<br>Previous change: {LAST_STATUS_CHANGE}</p>

<p>SQL instance: {SQL_INSTANCE}
<br>Alert time: {CHECK_TIME}</p>

<p>Warning threshold: {THRESHOLD_WARNING}
<br>Critical threshold: {THRESHOLD_CRITICAL}</p>

<p>--- Check Description:</p>

<p>{CHECK_DESCRIPTION}</p>

<p>--- Check Query:</p>

<p><pre style="background:#E0E0E0;padding:5px;"><code>{CHECK_QUERY}</code></pre></p>

<p>--- Report Content:</p></p>

<p><b>{REPORT_TITLE}</b></p>
<p>{REPORT_DESCRIPTION}</p>
<p>{REPORT_CONTENT}</p>

<p>Sent from SQLWATCH on host: {SQL_INSTANCE}</p>
<p><a href="https://docs.sqlwatch.io">https://docs.sqlwatch.io</a> </p>
```

Will generate the following report:

![](../../.gitbook/assets/image%20%289%29.png)

### Attributes

Each action's attributes are defined for each in the association table `[dbo].[sqlwatch_config_check_action]` and can differ for each combination of check and action

<table>
  <thead>
    <tr>
      <th style="text-align:left">Attribute</th>
      <th style="text-align:left">Type</th>
      <th style="text-align:left">Description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td style="text-align:left">action_every_failure</td>
      <td style="text-align:left">Boolean</td>
      <td style="text-align:left">
        <p>Tells whether to notify about subsequent failures or just the first occurrence.
          <br
          />When set to FALSE the action will only trigger on the first occurrence
          of the check going from OK to non OK status.</p>
        <p>When set to TRUE the action will trigger every time the check returns
          a non OK status.</p>
      </td>
    </tr>
    <tr>
      <td style="text-align:left">action_recovery</td>
      <td style="text-align:left">Boolean</td>
      <td style="text-align:left">Tells whether to trigger an action when the check recovers from non OK
        status to OK. This could be handy if we want to be notified that the problem
        has been resolved.</td>
    </tr>
    <tr>
      <td style="text-align:left">action_repeat_period_minutes</td>
      <td style="text-align:left">Numeric</td>
      <td style="text-align:left">Number of minutes to repeat action. Only applies when the &quot;action_every_failure&quot;
        is set to FALSE and will send a repeat notification every x minutes. This
        is handy if we want to be repeated daily or hourly about alerts that do
        not require urgent attention, for example low disk alert.</td>
    </tr>
    <tr>
      <td style="text-align:left">action_hourly_limit</td>
      <td style="text-align:left">Numeric</td>
      <td style="text-align:left">Maximum number of actions that can be triggered per hour to avoid flooding.</td>
    </tr>
    <tr>
      <td style="text-align:left">action_template_id</td>
      <td style="text-align:left">Numeric</td>
      <td style="text-align:left">ID of the action template</td>
    </tr>
  </tbody>
</table>

