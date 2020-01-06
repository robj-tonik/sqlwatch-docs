# Performance

A lot of work went into optimisation and reducing impact on the SQL database when querying data as well as reducing resources required for Power BI to render data. However, there few things to consider when it comes to the Power BI Performance:

## Data Volumes

This is the most important factor. It is obvious that the more data Power BI downloads, the more it has to process and render. 

There are some clever mechanisms built into Power BI such as High Density Sampling which reduce the amount of data rendered with minimised loss of granularity:

{% embed url="https://docs.microsoft.com/en-us/power-bi/desktop-high-density-sampling" %}

However, first and foremost, download less data into Power BI to make it run fast.

* Reduce time window
* Reduce granularity by increasing aggregation
* Only download what you want to see
* Hide baselines
* Filter Central Repository

## Performance Analyser

Recent versions of Power BI come with performance analyser that will show you what Power BI spends most time on when rendering report. You can use this to understand where the bottlenecks are. 









### Report Time Window

Reduce the Report Time Window parameter to download less data.

### Report Aggregation



### Unused Sets

If you are investigating last 60 minutes of production performance issues, perhaps you do not need to see last 24 hours worth of Agent Job history, index statistics or disk utilisation. Make sure you are setting report parameters correctly to limit what is being downloaded to Power BI

![](../.gitbook/assets/image%20%2830%29.png)

### Baselines

Baselines are fantastic way to compare same periods of time in an offset. For example, Same hour but yesterday, same day but last week etc. However, they also require more data to be downloaded. Only enable baselines if you have to.

![](../.gitbook/assets/image%20%2834%29.png)

### Generic Performance Analyser

The Generic Performance Analyser tab shows all Performance Counters without aggregation. It's purpose is to drill down into details. Only enable it when you are debugging performance issues. 

![](../.gitbook/assets/image%20%2867%29.png)

### Filter Central Repository

When using Central Repository, data for all servers is downloaded into Power BI. If you are investigating specific SQL Instance, you can apply filter so only data for this instance is downloaded:

![](../.gitbook/assets/image%20%2850%29.png)

## 

