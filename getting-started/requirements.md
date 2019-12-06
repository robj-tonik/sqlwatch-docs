# Minimum Requirements

## System Requirements

### SQL Server



\*\*\*\*

#### 

#### 

\*\*\*\*

#### 



### Integration Services

Data collection into central repository requires SQL Server Integration Service 2012 or higher. 

### Workstation

It is expected that the Power BI Desktop dashboard will be run on a client PC. There are no specific requirements for SQLWATCH apart from Power BI Desktop requirements which can be found on the [Power BI website](https://docs.microsoft.com/en-us/power-bi/desktop-get-the-desktop#minimum-requirements).  

{% hint style="info" %}
If you encounter any problems opening SQLWATCH dashboard please make sure you have the most recent version of PowerBI
{% endhint %}

## Performance Overhead

SQLWATCH is designed with minimum overhead. It utilises [**SQL Server Extended Events \(XES\)**](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events) where possible and [**Dynamic Management Views \(DMV\)**](https://docs.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views) collectors that run every minute by default.

> SQL Server The Extended Events architecture enables users to collect as much or as little data as is necessary to troubleshoot or identify a performance problem. Extended Events is configurable, and it scales very well.

{% hint style="info" %}
I have not observed nor has any performance overhead or increased CPU utilisation been reported to me. If you notice anything suspicious please feed back ASAP.
{% endhint %}

## Storage Utilisation

In version 2.1 schema has been redesigned and storage utilisation reduced by approx 60-80%. In addition, it is also possible and advisable to enable page compression on SQLWATCH data tables and indexes reducing utilisation by further 25-50%. The amount of space used by SQLWATCH depends on the retention period, number of databases on the server and the workload. As a guidance, below is the size of SQLWATCH in my test environment, with data compression enabled, after 30 days of use:

![Top tables after 30 days of use](../.gitbook/assets/image%20%2812%29.png)

{% hint style="info" %}
Appropriate index maintenance must in place in order to make sure table size is not being bloated over time.
{% endhint %}

### Large Environments

In large and busy environments or in environments where space is a concern the following collectors can be disabled to limit the amount of data collected:

* Index Statistics and Histograms 
* Long Queries

Furthermore, retention can be decreased to 1 or 2 days, or central repository deployed to offload data from remote instances.

### Data Compression

The following procedures will enable apply PAGE level compression:

`--table:  
exec [dbo].[usp_sqlwatch_config_set_table_compression]  
  
--index:  
exec [dbo].[usp_sqlwatch_config_set_index_compression]`



