# Configuration Items

SQLWATCH is designed to create minimum performance overhead.

There is a number of configuration items exposed to the end user in the `sqlwatch_config*` tables. However, for performance reasons, configuration is limited to the required minimum and some variables are either hard coded or assumed. 

Image a scenario when everything was configurable, the configuration would have to be stored in a table, and configuration value queried with every execution adding to the workload and, sometimes, making it possible for the query optimiser to pick best execution plan.

An example of such approach is in the action logger, where we do not log actions that have nothing to do. If you want to log all actions, you would need to change the below in `usp_sqlwatch_internal_process_actions`

```sql
--by default, we are NOT logging actions that have no action to do, 
--only those that are triggering a valid action or have error:
if @action_type <> 'NONE' or @action_attributes is not null
	begin
		insert into [dbo].[sqlwatch_logger_check_action] 
			(   [sql_instance], [snapshot_type_id], [check_id]
				, [action_id], [snapshot_time], [action_type], [action_attributes])
		select @@SERVERNAME, 18, @check_id, @action_id, @check_snapshot_time
				  , @action_type, @action_attributes
	end
```

There could be hundreds of checks and each check could have dozen of different actions and if we were to check a parameter for each execution, we would be potentially running thousands of queries every minute.

