# Add or modify action

## Add new action

To add new action we can execute a stored procedure:

```sql
exec [dbo].[usp_sqlwatch_user_add_action]
	,@action_description = 'Send Email to DBAs using sp_send_mail  (HTML)'
	,@action_exec_type = 'T-SQL'
	,@action_exec = 'exec msdb.dbo.sp_send_dbmail @recipients = ''dba@yourcompany.com'',
@subject = ''{SUBJECT}'',
@body = ''{BODY}'',
@profile_name=''DBA'',
@body_format = ''HTML'''
	,@action_enabled = 0
```

Or insert directly into the action table:

```sql
insert into [dbo].[sqlwatch_config_action]
values (...)
```

## Modify existing action

To modify existing action, we can either re-run the procedure passing action\_id:

```sql
exec [dbo].[usp_sqlwatch_user_add_action]
	 -- pass action id to replace / update:
	 @action_id = 1
	,@action_description = 'Send Email to DBAs using sp_send_mail  (HTML)'
	,@action_exec_type = 'T-SQL'
	,@action_exec = 'exec msdb.dbo.sp_send_dbmail @recipients = ''dba@yourcompany.com'',
@subject = ''{SUBJECT}'',
@body = ''{BODY}'',
@profile_name=''DBA'',
@body_format = ''HTML'''
	,@action_enabled = 0
```

Or we can update action table directly:

```sql
update [dbo].[sqlwatch_config_action]
    set ...
    where action_id = 1
```

## Delete Action

To delete existing action simply delete it from the actions table and all associated logger records will also be deleted:

```sql
delete from [dbo].[sqlwatch_config_action]
    where action_id = 1
```

{% hint style="info" %}
Note that you cannot delete an action if there are checks or reports using that action. Please first delete or disassociate checks and reports and then delete the action.
{% endhint %}

