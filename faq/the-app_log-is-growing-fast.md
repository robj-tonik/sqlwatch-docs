# The app\_log is growing fast

If your `[dbo].[sqlwatch_app_log]` table is growing fast, there a few things you can try.

### Stop logging INFO messages.

Before version `2.4` INFO messages were being logged by default. INFO are informational messages, similar to highly verbose logging. This was changes in version `2.4` and INFO are not logged by default, only WARNING and ERROR.

You can changes this behaviour in the global config:

```sql
  UPDATE [dbo].[sqlwatch_config]
  SET [config_value] = 0 -- 1 log INFO, 0 do not log INFO
  WHERE [config_id] = 7
```

### Reduce retention period.

Before version `2.4` the default retention period for the `app_log` table was 30 days. This changed to 7 days in the `2.4`. You can set retention period for the `app_log` table in the global config table:

```sql
  UPDATE [dbo].[sqlwatch_config]
  SET [config_value] = 7 --retention days. 
  WHERE [config_id] = 1
```

{% hint style="danger" %}
Please note that before the version `2.4` the retention was not batched up, meaning that the delete was executed in one transactions. If your `app_log` table is large and you are reducing retention significantly in version &lt; `2.4` it may take a while and may also blow the transaction log. If you are on &lt;  `2.4` you may want to truncate the table.
{% endhint %}

### Truncate it.

Before version `2.4` the table's retention was not batched up meaning large deletions would be executed in a single transaction. This could take a long time and could also blow the transaction log. It is perfectly safe to truncate the `app_log` table.

```sql
truncate table [dbo].[sqlwatch_app_log]
```

  

