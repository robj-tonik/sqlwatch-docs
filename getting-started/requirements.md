# Minimum Requirements

## System Requirements

### SQL Server

{% hint style="success" %}
#### SQL Server Standard and Enterprise

* **2008 R2 SP3** _\(read below\)_
* **2012**
* **2014**
* **2016**
* **2017**
* **2019**
{% endhint %}

{% hint style="success" %}
**SQL Server Express**

Express Edition is supported with **Windows Task Scheduler** in place for SQL Agent. Since version 2.2 Power Shell templates can be generated to help create all relevant tasks and schedules. Task creation tested on **Windows Server 2012** and **Windows Server 2016**.

`exec [dbo].[usp_sqlwatch_config_set_default_agent_jobs] @print_WTS_command = 1`
{% endhint %}

{% hint style="success" %}
#### Virtual Machines in the Cloud

Any Virtual Machine with the above SQL Server version will work in the Cloud \(Azure, AWS, GCP\)
{% endhint %}

{% hint style="info" %}
#### Azure SQL Managed Instances 

According to Microsoft they are 100% compatible with the traditional installation. **However, this has not been tested.**
{% endhint %}

{% hint style="info" %}
**Docker** and **Linux** 

Both are supported except the disk collector which relies on the Windows' WMI interface. Currently there is no equivalent for Linux implemented.
{% endhint %}

{% hint style="warning" %}
#### SQL Server 2008 R2

Whilst not officially supported, SQLWATCH will work on SQL2008 R2 SP3 with few small modifications.

1. Download source code from GitHub and open in Visual Studio with Data Tools. Since Visual Studio 2019, Data Tools are available as an extension. [https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt](https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt)
2. Once the below changes have been implemented, right click on the Project, go to Properties and change Target Platform to SQL 2008. Project should build successfully.

* Extended events sessions will not deploy. They will need to be commented out before deployment.
* Procedure `[dbo].[usp_sqlwatch_internal_get_last_snapshot_time_in_tables]` will need to be modified and the final `with result sets` removed. _This procedure is only used by the central repository which is targeted at SSIS 2012:_
* View `vw_sqlwatch_sys_databases` will need to be modified and join on `left join sys.dm_hadr_availability_replica_states hars` removed. This will force removal of the remaining joins and essentially reverting back issue \#108: [https://github.com/marcingminski/sqlwatch/issues/108](https://github.com/marcingminski/sqlwatch/issues/108)
* Depending on what PowerShell modules are installed in addition to SQL Server, some PowerShell agent steps may not work. As a workaround, These can be triggered from Windows Task Scheduler. _See installation on the Express Edition_.
{% endhint %}

{% hint style="danger" %}
Azure SQL is currently not supported.
{% endhint %}

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

## User Permissions

### SQL Server permissions required for deployment

In order to install SQLWATCH the following minimum permissions are required:

| Permission | reason |
| :--- | :--- |
| `dbcreator` | Create SQLWATCH database as part of the deployment process |
| `GRANT CREATE ...` | Object creation during the deployment.  |
| `SQLAgentUserRole` | Create SQL Agent jobs |
| `Windows Administrator` | Only when using Windows Scheduled Tasks instead of SQL Agent for collector invocation. Windows Administrator permission will be require in order to create and schedule tasks to run in the background. |

### SQL Server permissions required for reports

In order to retrieve data from the SQLWATCH database the following permissions are required:

| Permission | Description |
| :--- | :--- |
| `SELECT` | PowerBI Dashboard utilises Direct Queries to read from SQL views and explicit permissions to tables are not required by the PowerBI users. |

### SQL Server permissions required for data collection

{% hint style="warning" %}
**Not defined**. It is expected that collection will run under local SQL Agent account which will have `sa` rights. However, **this is not a requirement** I just have not got minimum requirements defined for the collectors yet.
{% endhint %}

### SQL Server permissions required for Central Repository

Central Repository requires `SELECT` permission on the remote instances as well as `EXECUTE` permission on the following stored procedures in the central repository:

`dbo.usp_sqlwatch_internal_get_last_snapshot_time_in_tables`

