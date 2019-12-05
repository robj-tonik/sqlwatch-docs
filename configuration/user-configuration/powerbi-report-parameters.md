# PowerBI Report Parameters

{% hint style="warning" %}
Needs updating for version 2.2
{% endhint %}

## SQL Instance

Name of the SQL Instance to connect to. This could be a stand alone SQLWATCH instance or a central repository. 

## SQLWATCH Database

Name of the SQLWATCH database, by default it will be SQLWATCH unless the solution has been deployed to a non-standard database, such as your existing DBADMIN database etc.

## Repository Filter SQL Instance

When connected to the repository, all SQL Instances will be shown on the dashboard. Sometimes however, we want to investigate one specific server in which case, we can limit what is being downloaded to the Dashboard and improve performance of PowerBI.

## Report End Time \(datetime\)

Date when the report will end. By default this will be GETUTCDATE\(\) and will show all data up until now. To show historical data we can specify any date and time in the past.

Type date and time when you want reporting window to end. Follow the example in the drop down box or select GETUTCDATE\(\) to get the most recent, timezone agnostic, data. For example, if you type '2018-12-31 23:59:59' \(note the quotes\), the report will show data up till that time stamp.

## Performance Report Window \(hours\)

How many hours to import going back from the **Report End Time**. For example if this parameter = 4 and **Report End Time** = GETUTCDATE\(\) the report will show last 4 hours from now. This way you can travel back in time and see any time slice of historical performance data. You can select from the drop down or type your own.

## Performance Report Interval \(minutes\)

For cumulative metrics we need to calculate delta between two points in time. This parameter specifies the interval window for delta calculation. 

By default, the interval calculation happens automatically based on the below formula:

```text
            when @report_window <= 1 then 2
            when @report_window <= 4 then 5
            when @report_window <= 24 then 15
            when @report_window <= 168 then 60
            when @report_window <= 720 then 360
```

Which means for 1 hour worth of data the granularity will 2 minutes and for 7 days it will be 1 hour.

The rule of thumb is the higher the **Performance Report Window** the higher the internal window i.e. lower granularity. 

![24 hours window with 5 minute interval](../../.gitbook/assets/image%20%288%29.png)

![24 hour window with 60 minute interval](../../.gitbook/assets/image%20%2833%29.png)

The parameter can be overridden by the user

## Show index analysis

All Index history will be downloaded. You may want to exclude it if you are downloading last few hours of real-time performance problems from a production instance to minimise load.

## Index Analysis Report Window \(days\)

Index collection happens less frequently than the performance data and therefore it is not always possible to correlate these two. Here we can specify how much index stats data to pull going back from the report end time.

## Index Histogram Visibility

Histograms can be large, by default SQLWATCH will only show most recent histogram. If you want to see histogram for all indexes, select ALL.

## Show disk utilisation

All disk utilisation will be downloaded. You may want to exclude it if you are downloading last few hours of real-time performance problems from a production instance to minimise load. Best download disk utilisation out of hours.

## Disk Utilisation Report Window \(days\)

Disk collection happens less frequently than the performance data and therefore it is not always possible to correlate these two. Here we can specify how much disk utilisation stats data to pull going back from the report end time.

## Show WhoIsActive

By default, all WhoIsActive data will be downloaded and plotted on the dashboard. For large periods this may not be desired due to potentially large volumes. You can disable showing WhoIsActive data on the Dashboard.

## Show Agent History

Whether to show SQL Agent Job History on the dashboard

## Agent History Report Window \(days\)

Here we can specify how much agent history data to pull going back from the report end time.

## Command timeout in minutes

Timeout after which Power BI will give up pulling data. This is to protect SQL Server in case of misbehaving queries or if your repository has grown to an unmanageable size. 1 minute should be more than enough however, you can set it to match your setup. If do, please make sure to understand the impact the root cause of timeouts!



