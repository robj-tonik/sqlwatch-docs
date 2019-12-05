# Requirements

## SQL Server requirements

The target platform for SQLWATCH is SQL Server 2012\*. It has been tested on the following SQL Server versions:

{% hint style="success" %}
* ~~2008 R2 SP3 \(read below\)~~
* 2012
* 2014
* 2016
* 2017 \(including docker and linux\*\)
* 2019
{% endhint %}

{% hint style="info" %}
* SQL Server on docker and Linux are supported except the disk collector which relies on the Windows' WMI interface. Currently there is no equivalent in bash implemented.
{% endhint %}

Azure SQL are not supported as there is no Agent to invoke data collection. Theoretically, data collection would be possible via SQLCMD triggered from the Windows Task Scheduler or another Standard Edition instance in case of the Express edition and, for example, Azure Runbook in case of Azure SQL but this has not been tested.

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

## Integration Services requirements

Data collection into central repository requires SQL Server Integration Service 2012 or higher. 

## Workstation requirements

It is expected that the Power BI Desktop dashboard will be run on a client PC. There are no specific requirements for SQLWATCH apart from Power BI Desktop requirements which can be found on the [Power BI website](https://docs.microsoft.com/en-us/power-bi/desktop-get-the-desktop#minimum-requirements).  

## Storage utilisation

In version 2.0 schema has been redesigned and storage utilisation reduced by approx 60-80%. In addition, it is also possible and advisable to enable page compression on SQLWATCH reducing utilisation by further 25%. The amount of space used by SQLWATCH depends on the retention period and the number of databases on a server. On a server with 10 databases the growth is approx 100 MB per day

## Permissions

### SQL Server permissions required for deployment

In order to install SQLWATCH the following minimum permissions are required:

| Permission | reason |
| :--- | :--- |
| `dbcreator` | Create SQLWATCH database as part of the deployment process |
| `GRANT CREATE ...` | Object creation during the deployment.  |
| `SQLAgentUserRole` | Create SQL Agent jobs |

### SQL Server permissions required for operation

In order to retrieve data from the SQLWATCH database the following permissions are required:

| Permission | Description |
| :--- | :--- |
| `db_datareader` | Read data from all tables and views |
| `EXECUTE` scalar functions | Scalar functions are required as part of data retrieval. |





