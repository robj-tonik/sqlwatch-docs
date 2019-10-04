# User configuration

> User configuration defined in this section will never be replaced by subsequent SQLWATCH updates.

## Collection schedule and frequency

Data collection relies on SQL Agent jobs. The jobs' schedules can be modified to fit specific requirements. 

## Data retention periods

Data retention is executed by Agent job `SQLWATCH-INTERNAL-RETENTION`. Each `snapshot_type` has its own retention defined in table `[dbo].[sql_perf_mon_config_snapshot_type]`. 

This approach allows setting different retention for performance data, disk utilisation, query performance and son on. 

Default retention periods:

```text
select * from [dbo].[sql_perf_mon_config_snapshot_type]
```

| snapshot\_id | snapshot\_type\_desc | snapshot\_retention\_days |
| :--- | :--- | :--- |
| 1 | Performance | 7 |

## Performance counters

Performance counters collected by SQLWATCH are defined in table `[dbo].[sql_perf_mon_config_perf_counters]`. Collection of individual performance counters can be set using the boolean `collect` column. Disabling the default performance counter collectors will stop them from being shown on the default dashboard. New collectors can be added to the list if required. 

Please note the `instance_name` is dynamic and contains actual names of objects i.e. database names. The collection definition takes this into account with a dynamic approach:

| definition instance\_name | actual instance\_name |
| :--- | :--- |
| Literal valid instance name i.e. 'Elapsed Time:Total\(ms\)' or ''  | Will translate to literal 'Elapsed Time:Total\(ms\)' or '' Not e that instance name must a valid instance |
| \_Total | Will only include '\_Total' instances. This is useful if we only want to collect high level aggregates and are not interested in low level objects i.e. datbase |
| &lt;\* !\_Total&gt; | Will not include '\_Total' instances, i.e. it will collect any other instances for this particular `counter_name` but not totals. This is useful if we want to collect low level objects i.e. datbase performance and will be aggregating and calcualting totals, for example in Power BI. In this case there is no value in collecting totals.  |

