# Reports

Reports is a standalone module that can be run on a set schedule, or triggered by an action. For example, we can have a daily "Status" report or even a business process saving generated file to a shared drive. 

Actions can also trigger a report. For example, we can have a Check to check for space left on drives and send us a report when the thresholds are low.

Reports are defined in table `[dbo].[sqlwatch_config_report]` and can be associated with actions in table `[dbo].[sqlwatch_config_report_action]` in a similar manner to how checks are associated with actions

{% hint style="info" %}
Reports are always generated in HTML therefore action must also support HTML tags. If you are using **sp\_send\_mail** set the **@body\_format = 'HTML'**
{% endhint %}

### Report types

Report types are defined in the `[report_definition_type]` column and can be:

#### Templates

This type of the report is self-contained and the final look will be exactly as in the template. When template is specified, the content of the `report_definition` field is passed into `sp_executesql` and passed into action for processing.

```sql
		if @definition_type = 'Template'
			begin
				insert into @template_build
				exec sp_executesql @report_definition

				select @html = [result] from @template_build
				set @html = '<html><head><style>' + @css + '</style><body><p>' + @report_description + '</p>' + @html + '<p>Email sent from SQLWATCH on host: ' + @@SERVERNAME +'
<a href="https://sqlwatch.io">https://sqlwatch.io</a></p></body></html>'
			end
```

This allows building completely custom reports

#### Queries

The Query type is a simpler version of the report. The `report_definition` must be a valid SQL Query which output will be converted to a html table and passed into action for processing.

```sql
		if @definition_type = 'Query'
			begin
				exec [dbo].[usp_sqlwatch_internal_query_to_html_table] @html = @html output, @query = @report_definition

				set @html = '<html><head><style>' + @css + '</style><body><p>' + @report_description + '</p>' + @html + '<p>Email sent from SQLWATCH on host: ' + @@SERVERNAME +'
<a href="https://sqlwatch.io">https://sqlwatch.io</a></p></body></html>'
			end
```

### Report Styling

Each report can have a custom `CSS` style. Styles are defined in table: `[dbo].[sqlwatch_config_report_style]` 

