---
description: Minimum requirements for the SQLWATCH data collector and SQL Server Engine
---

# Requirements

{% hint style="success" %}
#### SQL Server Standard and Enterprise

* **2008 R2 SP3** _\(details below\)_
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
#### SQL Server 2008 R2 SP3

Whilst not officially supported, SQLWATCH will work on **SQL Server 2008 R2 SP3** with few small modifications.

1. Download source code from GitHub and open in Visual Studio with Data Tools. Since Visual Studio 2019, Data Tools are available as an extension. [https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt](https://docs.microsoft.com/en-us/sql/ssdt/download-sql-server-data-tools-ssdt)
2. Once the below changes have been implemented, right click on the Project, go to Properties and change Target Platform to SQL 2008. Project should build successfully.

* Extended events sessions will not deploy. They will need to be commented out before deployment.
* Procedure `[dbo].[usp_sqlwatch_internal_get_last_snapshot_time_in_tables]` will need to be modified and the final `with result sets` removed. _This procedure is only used by the central repository which is targeted at SSIS 2012:_
* View `vw_sqlwatch_sys_databases` will need to be modified and join on `left join sys.dm_hadr_availability_replica_states hars` removed. This will force removal of the remaining joins and essentially reverting back issue \#108: [https://github.com/marcingminski/sqlwatch/issues/108](https://github.com/marcingminski/sqlwatch/issues/108)
* Depending on what PowerShell modules are installed in addition to SQL Server, some PowerShell agent steps may not work. As a workaround, These can be triggered from Windows Task Scheduler. _See installation on the Express Edition_.

**SQL Server 2008 R2 prior to SP3 are not supported**
{% endhint %}

{% hint style="danger" %}
Azure SQL is currently not supported.
{% endhint %}

