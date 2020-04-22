# Add or modify report

## Add new report

```sql
		exec [dbo].[usp_sqlwatch_user_add_report] 
		
			/* Title of the report: */
			,@report_title = 'Disk Utilisation Report'
			
			/* Description: */
			,@report_description = ''
			
			/* Single Query or an entire Template: */
			,@report_definition = 'select [Volume]=[volume_name]
      ,[Days Until Full] = [days_until_full]
      ,[Total Space] = [total_space_formatted]
      ,[Free Space] = [free_space_formatted] + " (" + [free_space_percentage_formatted] + ")"
      ,[Growth] = [growth_bytes_per_day_formatted]
  from [dbo].[vw_sqlwatch_report_dim_os_volume]'
  	
  		/* Type of the report, either Template or Query: */
			,@report_definition_type = 'Query'
			
			/* Assosiate with an existing action: */
			,@report_action_id  = -1
```

Alternatively we can insert directly into the report table:

```sql
insert into [dbo].[sqlwatch_config_report]
    values (...)
```

## Modify existing report

To modify existing report we can either update the report table:

```sql
update [dbo].[sqlwatch_config_report]
    set [report_definition] = '...'
    where report_id = 1
```

Or we can re-run the procedure passing the ID of the report we want to update/replace:

```sql
		exec [dbo].[usp_sqlwatch_user_add_report] 
			--pass ID of the report to update / replace:
		  ,@report_id = 1
			,@report_title = 'Disk Utilisation Report'
			,@report_description = ''
			,@report_definition = 'select [Volume]=[volume_name]
      ,[Days Until Full] = [days_until_full]
      ,[Total Space] = [total_space_formatted]
      ,[Free Space] = [free_space_formatted] + '' ('' + [free_space_percentage_formatted] + '')''
      ,[Growth] = [growth_bytes_per_day_formatted]
  from [dbo].[vw_sqlwatch_report_dim_os_volume]'
			,@report_definition_type = 'Query'
			,@report_action_id  = -1
```

Delete Report

To delete an existing report you can simply delete it from the table which will also delete any associations:

```sql
delete from [dbo].[sqlwatch_config_report]
    where report_id = 1
```

{% hint style="info" %}
Note that you cannot delete a report if an action is using it. You will first have to remove that action or update the `[action_report_id]` so it does not reference that report
{% endhint %}



