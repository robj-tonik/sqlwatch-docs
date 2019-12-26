# Configuration

## Report Parameters

{% hint style="warning" %}
You will need to change the parameters supplied with the Dashboard on the first run in order to connect to your Server.
{% endhint %}

{% hint style="info" %}
To open Parameters window, when on the main Dashboard page \(not in Power Query\), navigate to Home -&gt; Edit Queries -&gt; Edit Parameters. 
{% endhint %}

{% hint style="info" %}
There is no need to go into the Query Editor to edit or modify queries or data sources. Everything is handled through the below parameters.
{% endhint %}

![](../.gitbook/assets/image%20%2853%29.png)

![](../.gitbook/assets/image%20%2827%29.png)

### SQL Instance

Name of the SQL Instance to connect to. This could be a stand alone SQLWATCH instance or a central repository. 

### SQLWATCH Database

Name of the SQLWATCH database, by default it will be SQLWATCH unless the solution has been deployed to a non-standard database, such as your existing "DBADMIN" database etc.

{% hint style="info" %}
All the below parameters are different switches to improve load performance. Please read carefully as it will affect your experience.
{% endhint %}

### Repository Filter SQL Instance

When connected to the repository, all SQL Instances in this repository will be shown on the dashboard. Sometimes however, we want to investigate one specific server in which case, we can limit what is being downloaded to the Dashboard and improve performance of PowerBI.

### Report End Time \(datetime\)

Date when the report will end. By default this will be `GETUTCDATE()` and will show all data up until now. To show historical data we can specify any date and time in the past.

Type date and time when you want reporting window to end. Follow the example in the drop down box or select `GETUTCDATE()` to get the most recent, timezone agnostic, data. For example, if you type '2018-12-31 23:59:59' \(note the quotes\), the report will show data up till that time stamp.

### Performance Report Window \(hours\)

How many hours to import going back from the **Report End Time**. For example if this parameter = 4 and **Report End Time** = `GETUTCDATE()` the report will show last 4 hours from now. This way you can travel back in time and see any time slice of historical performance data. You can select from the drop down or type your own.

### Performance Report Aggregation

Report interval is an aggregation factor. For example, 15 minutes interval will group data at source into 15 minutes interval buckets.  It is set based on the Time Window and the longer the window the higher the interval and therefore less granular data downloaded into Power BI.  


The rule of thumb is the higher the **Performance Report Window** the higher the internal window i.e. lower granularity. 

![24 hours window with 5 minute aggregation](../.gitbook/assets/image%20%2810%29.png)

![24 hour window with 60 minute aggregation](../.gitbook/assets/image%20%2845%29.png)

### Performance Report Baselines

Whether to show baselines or not. Baselines required more data to be downloaded.

### Show index analysis

Whether to download index statistics history. You may want to exclude it if you are downloading last few hours of real-time performance problems from a production instance to minimise load.

### Index Analysis Report Window \(hours\)

Index collection happens less frequently than the performance data and therefore it is not always possible to correlate these two. Here we can specify how much index stats data to pull going back from the report end time.

### Index Histogram Visibility

Histograms can be large, by default SQLWATCH will only show most recent histogram. If you want to see histogram for all indexes, select ALL.

### Show disk utilisation

Whether to download disk utilisation history. You may want to exclude it if you are downloading last few hours of real-time performance problems from a production instance to minimise load. Best download disk utilisation out of hours.

### Disk Utilisation Report Window \(days\)

Disk collection happens less frequently than the performance data and therefore it is not always possible to correlate these two. Here we can specify how much disk utilisation stats data to pull going back from the report end time.

### Show WhoIsActive

By default, all WhoIsActive data will be downloaded and plotted on the dashboard. For large periods this may not be desired due to potentially large volumes. You can disable showing WhoIsActive data on the Dashboard.

### Show Agent History

Whether to show SQL Agent Job History on the dashboard

### Agent History Report Window \(hours\)

Here we can specify how much agent history data to pull going back from the report end time.

### Show Performance Analyser

The Generic Performance Analyser tab shows all Performance Counters without aggregation. It's purpose is to drill down into details and to show any custom counters added by users. Only enable it when you have to as it can download quite large amount of data

### Show Baselines

Similar to Performance Report Baselines but relates to the Analyser tab. For example, you may wish to not show only baselines in this tab and not across the entire report or vice-versa.

