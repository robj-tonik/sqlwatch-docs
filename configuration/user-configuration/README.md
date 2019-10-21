# User configuration

> User configuration defined in this section will never be replaced by subsequent SQLWATCH updates.

## Collection schedule and frequency

Data collection relies on SQL Agent jobs. The jobs' schedules can be modified to fit specific requirements. 

## Data retention periods

Data retention is executed by Agent job `SQLWATCH-INTERNAL-RETENTION`. Each `snapshot_type` has its own retention defined in table `[dbo].[sqlwatch_config_snapshot_type]`. 

This approach allows setting different retention for performance data, disk utilisation, query performance and son on. 

Default retention periods:

```text
SELECT * FROM [dbo].[sqlwatch_config_snapshot_type]
```

| snapshot\_id | snapshot\_type\_desc | snapshot\_retention\_days |
| :--- | :--- | :--- |
| 1 | Performance | 7 |
| 2 | Disk Utilisation Database | 365 |
| 3 | Missing indexes | 30 |
| 6 | XES Waits | 7 |
| 7 | XES Long Queries | 7 |
| 8 | XES Waits | 30 |
| 9 | XES Blockers | 30 |
| 10 | XES Query Processing | 30 |
| 11 | WhoIsActive | 3 |
| 14 | Index Stats | 90 |
| 15 | Index Histogram | 90 |
| 16 | Agent History | 365 |
| 17 | Disk Utilisation OS | 365 |

## Performance counters

Performance counters collected by SQLWATCH are defined in table `[dbo].[sqlwatch_config_performance_counters]`. Collection of individual performance counters can be set using the Boolean `collect` column. Disabling the default performance counter collectors will stop them from being shown on the default dashboard. New collectors can be added to the list if required. 

Please note the `instance_name` is dynamic and contains actual names of objects i.e. database names. The collection definition takes this into account with a dynamic approach:

| definition instance\_name | actual instance\_name |
| :--- | :--- |
| Literal valid instance name i.e. 'Elapsed Time:Total\(ms\)' or ''  | Will translate to literal 'Elapsed Time:Total\(ms\)' or '' Not e that instance name must a valid instance |
| \_Total | Will only include '\_Total' instances. This is useful if we only want to collect high level aggregates and are not interested in low level objects i.e. database |
| &lt;\* !\_Total&gt; | Will not include '\_Total' instances, i.e. it will collect any other instances for this particular `counter_name` but not totals. This is useful if we want to collect low level objects i.e. database performance and will be aggregating and calculating totals, for example in Power BI. In this case there is no value in collecting totals.  |

## Central Repository Configuration

{% hint style="info" %}
Please see installation section to find out how to install and configure the integration services package required by the central repository
{% endhint %}

To start collecting data from a remote instance, add a reference to the configuration table: `[dbo].[sqlwatch_config_sql_instance]`

![](../../.gitbook/assets/image%20%2812%29.png)

**sql\_instance and hostname**

The `sql_instance` is what `@@SERVERNAME` returns on the remote instance and this is what gets logged in the remote tables and `hostname` is the physical host name to connect to. Most of the time they are the same unless you are connecting via IP \(no DNS records\) or you are connecting to SQL Server on Docker, which has different IP and `servername`. 

**sql\_port**  
Optionally you can specify non standard port to connect 

**sqlwatch\_database\_name**  
Name of the database where SQLWATCH is deployed on the remote instance. Default is SQLWATCH.

**environment**  
Custom label to group servers into specific environments in the PowerBI report.

**is\_active**  
Whether to include instance in the collection or not

**last\_collection\_time and collection\_status**  
Are populated during the collection from the remote instance and indicate last collection time and the status.

