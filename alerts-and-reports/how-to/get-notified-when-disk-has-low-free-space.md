---
description: An example of how to approach checks and notifications
---

# Add or modify new check

## Add a new check

In this example we are adding a new check to check the average CPU utilisation in the last 5 minutes:

```sql
exec [dbo].[usp_sqlwatch_user_add_check]
	/* Name of the check, this will appear in the {SUBJECT} parameter: */
	@check_name = 'High CPU Utilistaion % in the last 5 minutes'
	
	/* description of the check: */
	,@check_description = 'In the past 5 minutes, the average CPU utilistaion was higher than expected'
	
	/* SQL Query to perform the check. Must return single value only: */
	,@check_query = 'select avg(cntr_value_calculated) 
from dbo.vw_sqlwatch_report_fact_perf_os_performance_counters
where counter_name = "Processor Time %"
and report_time > dateadd(minute,-5,getutcdate())'

	/* How often do we want this check to run.
	   If set to NULL it will run every time the SQLWATCH-INTERNAL-CHECKS job runs: 
		 Since we are checking for the CPU utilisation in the last 5 minutes, 
		 we are going to run this every 5 minutes: */
	,@check_frequency_minutes = 5
	
	/* Value for warning. If the check returns value greater than this, 
		 it will raise a WARNING status */
	,@check_threshold_warning = '>60'

	/* Value for critical. If the check returns value greater than this, 
		 it will raise a CRITICAL status */
	,@check_threshold_critical = '>80'

	/* Whether the check should be enabled or disabled */
	,@check_enabled = 1

	/* Assosiate with an existing action */
	,@check_action_id = 1

	/* Whether to action every failure or just on first failure.
		 = 0 : When the check fails it will triggen an action on the first failure. 
				   It will not trigger another action until it recovers back to OK and failes again
		 = 1 : When the check fails it will trigger an action, and it will be triggering
					 an action every time the value changes and is not OK. It will NOT trigger
					 another action if the value does not change. We can use "reminders" for that */
	,@action_every_failure = 0

	/* Whether to send a recovery message when check comes back to OK */
	,@action_recovery = 1

	/* Whether to send a "reminder" if the check stays in non OK status */
	,@action_repeat_period_minutes = NULL

	/* Limit of messages per hour, for this check and action only: */
	,@action_hourly_limit = 10

	/* Assosiate action with an existing action template */
	,@action_template_id = 1
```

## Modify existing check

To modify an existing check we can either make a direct table update i.e:

```sql
update [dbo].[sqlwatch_config_check]
    set [check_frequency_minutes] = 10
    where check_id = 1
```

Or we can re-run the procedure with a check\_id to modify and all values will be replaced:

```sql
exec [dbo].[usp_sqlwatch_user_add_check]
	--to modify existin check, pass ID here:
	 @check_id = 1
	,@check_name = 'High CPU Utilistaion % in the last 5 minutes'
	,@check_description = 'In the past 5 minutes, the average CPU utilistaion was higher than expected'
	,@check_query = 'select avg(cntr_value_calculated) 
from dbo.vw_sqlwatch_report_fact_perf_os_performance_counters
where counter_name = ''Processor Time %''
and report_time > dateadd(minute,-5,getutcdate())'
	,@check_frequency_minutes = 5
	,@check_threshold_warning = '>60'
	,@check_threshold_critical = '>80'
	,@check_enabled = 1
	,@check_action_id = -2
	,@action_every_failure = 0
	,@action_recovery = 1
	,@action_repeat_period_minutes = NULL
	,@action_hourly_limit = 10
	,@action_template_id = -1
```

