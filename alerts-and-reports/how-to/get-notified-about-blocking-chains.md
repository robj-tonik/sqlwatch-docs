# Add new report

In this example we are adding a new report

```sql
		exec [dbo].[usp_sqlwatch_user_add_report] 
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

