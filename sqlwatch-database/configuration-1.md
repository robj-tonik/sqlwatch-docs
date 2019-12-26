# Configuration

> User configuration defined in this section will never be replaced by subsequent SQLWATCH updates.

## Local collector jobs

All jobs are enabled by default with the exception of the `SQLWATCH-LOGGER-WHOISACTIVE` which is only enabled when `sp_WhoIsActive` is found either in the `master`  or the `SQLWATCH`  database. If not found in either, the job is deployed in a disabled state. 

## Default collection schedule

Data collection relies on SQL Agent jobs. Although it recommended to use default schedules, they can be modified to fit specific requirements.

Default schedules:

| Job Name | Schedule |
| :--- | :--- |
| `SQLWATCH-INTERNAL-ACTIONS` | Every 15 Seconds |
| `SQLWATCH-INTERNAL-CHECKS` | Every 1 Minute |
| `SQLWATCH-INTERNAL-CONFIG` | Every 1 Hour |
| `SQLWATCH-INTERNAL-RETENTION` | Every 1 Hour |
| `SQLWATCH-INTERNAL-TRENDS` | Every 1 Hour |
| `SQLWATCH-LOGGER-AGENT-HISTORY` | Every 10 Minutes |
| `SQLWATCH-LOGGER-DISK-UTILISATION` | Every 1 Hour |
| `SQLWATCH-LOGGER-INDEXES` | Every 6 Hours |
| `SQLWATCH-LOGGER-PERFORMANCE` | Every 1 Minutes |
| `SQLWATCH-LOGGER-WHOISACTIVE` | Every 15 Seconds |

## Data retention periods

Data retention is executed by Agent job `SQLWATCH-INTERNAL-RETENTION`. Each `snapshot_type` has its own retention defined in table `[dbo].[sqlwatch_config_snapshot_type]`. 

This approach allows setting different retention for performance data, disk utilisation, query performance and son on. 

Default retention periods:

```text
SELECT * FROM [dbo].[sqlwatch_config_snapshot_type]
```

| Snapshot Type | Description | Retention Days | Trend Retention Days |
| :--- | :--- | :--- | :--- |
| 1 | Performance | 8 |  |
| 2 | Disk Utilisation Database | 365 |  |
| 3 | Missing indexes | 32 |  |
| 6 | XES Waits | 8 |  |
| 7 | XES Long Queries | 8 |  |
| 8 | XES Waits | 32 |  |
| 9 | XES Blockers | 32 |  |
| 10 | XES Query Processing | 32 |  |
| 11 | WhoIsActive | 3 |  |
| 14 | Index Stats | 90 |  |
| 15 | Index Histogram | 90 |  |
| 16 | Agent History | 365 |  |
| 17 | Disk Utilisation OS | 365 |  |
| 18 | Checks | 7 |  |
| 19 | Actions | 2 | 730 |
| 20 | Reports | 2 | 730 |
| 21 | Log | 2 | 730 |

## Performance counters

Performance counters collected by SQLWATCH are defined in table `[dbo].[sqlwatch_config_performance_counters]`. 

Collection of individual performance counters can be set using the Boolean `collect` column. Disabling the default performance counter collectors will stop them from being collected and therefore shown on the default dashboard. New collectors can be added to the list if required. 

Please note the `instance_name` is dynamic and contains actual names of objects i.e. database names. The collection definition takes this into account with a dynamic approach:

| Definition | Description |
| :--- | :--- |
| Literal valid instance name i.e. 'Elapsed Time:Total\(ms\)' or ''  | Will translate to literal 'Elapsed Time:Total\(ms\)' or '' Not e that instance name must a valid instance |
| \_Total | Will only include '\_Total' instances. This is useful if we only want to collect high level aggregates and are not interested in low level objects i.e. database |
| &lt;\* !\_Total&gt; | Will not include '\_Total' instances, i.e. it will collect any other instances for this particular `counter_name` but not totals. This is useful if we want to collect low level objects i.e. database performance and will be aggregating and calculating totals, for example in Power BI. In this case there is no value in collecting totals.  |

## Extended Events Sessions \(XES\)

A number of Extended Events Sessions are also deployed with SQLWATCH in a disabled state. This is because some DBAs will have their own XES sessions and we would not want to interfere without prior notice. However, certain functionality will not be available, for the full experience please enable SQWLATCH sessions.

![](../.gitbook/assets/image%20%2889%29.png)

```text
ALTER EVENT SESSION SQLWATCH_blockers ON SERVER
STATE = start;

ALTER EVENT SESSION SQLWATCH_long_queries ON SERVER
STATE = start;

ALTER EVENT SESSION SQLWATCH_waits ON SERVER
STATE = start;
```

## Blocked Process Monitor

In order for SQLWATCH to record blocking chains we have to enable The `blocked process threshold`for a specific time threshold. 

{% embed url="https://docs.microsoft.com/en-us/sql/database-engine/configure-windows/blocked-process-threshold-server-configuration-option?view=sql-server-ver15" %}

```text
exec sp_configure 'show advanced options', 1 ;  
RECONFIGURE ;  
exec sp_configure 'blocked process threshold', 20 ;  
RECONFIGURE ;  
```

To make this easier, a procedure has been included in SQLWATCH that will enable the Blocked Process Monitor and set the threshold to 15 \(or user specified\) seconds: 

```text
--default threshold will be 15 seconds:
exec [dbo].[usp_sqlwatch_config_set_blocked_proc_threshold] 

--to applly different threshold:
exec [dbo].[usp_sqlwatch_config_set_blocked_proc_threshold] @threshold_seconds = x 
```

## Table and Index compression

You may wish to compress data in SQLWATCH to improve storage utilisation and I/O performance at the cost of CPU utilisation. You can do so by running:

```text
exec [dbo].[usp_sqlwatch_config_set_table_compression];
exec [dbo].[usp_sqlwatch_config_set_index_compression];
```

## Recreate agent jobs

To create all default SQLWATCH agent jobs you can run:

```text
--add any missing SQLWATCH jobs, will not remove existing SQLWATCH jobs:
exec [dbo].[usp_sqlwatch_config_set_default_agent_jobs]

--remove existing and recreate all SQLWATCH jobs:
exec [dbo].[usp_sqlwatch_config_set_default_agent_jobs] @remove_existing = 1
```

