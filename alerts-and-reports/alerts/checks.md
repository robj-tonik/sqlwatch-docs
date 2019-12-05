# Checks

Checks are simple and very fast queries that return only one value. For example, average CPU utilisation over the last 5 minutes:

```sql
select avg(cntr_value_calculated) 
from dbo.vw_sqlwatch_report_fact_perf_os_performance_counters
where counter_name = 'Processor Time %'
and report_time > dateadd(minute,-5,getutcdate())
```

The result of the check are compared to the given thresholds:

![](../../.gitbook/assets/image%20%2841%29.png)

There are three possible status, based on the comparison:

**OK**, **WARNING** or **CRITICAL**.

Based on the above example, if the average CPU utilisation is below 60%, the check will return an OK status. If it is above 60% but below 80%, it will return WARNING and if over 80%, it fill return CRITICAL status. Check outputs and statuses are logged in a table:

![\[dbo\].\[sqlwatch\_logger\_check\]](../../.gitbook/assets/image%20%2849%29.png)

If the check does not return an OK status, it can optionally trigger an action. Alternatively, if it comes back from a WARNING or a CRITICAL status, it can trigger a recovery message informing that that the problem has been resolved. 

### Association with Actions

Checks are associated with actions in the `[dbo].[sqlwatch_config_check_action]` table. This way one check can call multiple different actions.

![](../../.gitbook/assets/image%20%2835%29.png)





