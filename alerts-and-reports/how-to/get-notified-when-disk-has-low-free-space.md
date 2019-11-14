---
description: An example of how to approach checks and notifications
---

# Get notified when disk has low free space

Suppose we want to be notified about disks running low on space. Say we want a warning when the disk is below 15% of free space and a critical notification when the free space drops below 5%

Following the alerts concept, first we need a check to check how much space there is

### Write the check query

Checks are simple queries that must return exactly one value. In our case the query will be returning percentage of space free on disk C:\ 

```sql
select [free_space_percentage]
from [dbo].[vw_sqlwatch_report_dim_os_volume]
where volume_name = 'C:\'
```

This data will be stored in `[check_query]`

### Define thresholds 

Think about realistic thresholds. Alerts are to trigger you to do an action rather than just be deleted and forgotten about. If you set thresholds too high you will get the impression that you may have "plenty of time to deal with it" and may forget about it. If you set thresholds to low you may not have enough time to deal with the issue before the server goes down.

For our check we have assumed WARNING below 15% and CRITICAL alert if the space drops below 5%

This data will be stored in `[check_threshold_warning]` and `[check_threshold_critical]`

### Define check frequency 

Checks are triggered by an agent job that runs every minute. Some checks may run every minute, however in our case we are going to run this check every 15 minutes.

This will be stored in `[check_frequency_minutes]`

### Name and Description

Finally, give this check a name and description. This is what you will see on the alert and the email so make sure it is descriptive and meaningful to you.

These values will be in `[check_name]` and `[check_description]` 

### Insert into checks table 

Once we have all the information we can insert into the check table

```sql
INSERT INTO [dbo].[sqlwatch_config_check]
           ([sql_instance]
           ,[check_name]
           ,[check_description]
           ,[check_query]
           ,[check_frequency_minutes]
           ,[check_threshold_warning]
           ,[check_threshold_critical]
           ,[check_enabled])
     VALUES
           (@@SERVERNAME
           ,'Disk Free %: C:\'
           ,'Disk C:\ has low free space. It may run out of space soon, depending on the growth.'
           ,'select [free_space_percentage]
from [dbo].[vw_sqlwatch_report_dim_os_volume]
where volume_name = ''C:\'''
           ,15
           ,'<15'
           ,'<5'
           ,1)
           
--return id of the newly created check:
declare @check_id smallint
select @check_id = SCOPE_IDENTITY()
select @check_id
```

Once the check runs you will be able to see results in `[dbo].[sqlwatch_logger_check]` table.

### Associate check with action

Creating check on its own will not send an alert just yet. Actions are what makes things happen. We have to tell the check which action to trigger when it fails. Note in the previous script we have returned an ID of the newly created check `select SCOPE_IDENTITY()`. Suppose we have an existing action \(Id: 1\) that will send us an email. 

![](../../.gitbook/assets/image%20%2851%29.png)

We can associate our newly created check with action 1. For this, we need to insert a row in the association table: 

```sql
INSERT INTO [dbo].[sqlwatch_config_check_action]
           ([sql_instance]
           ,[check_id]
           ,[action_id]
           ,[action_every_failure]
           ,[action_recovery]
           ,[action_repeat_period_minutes]
           ,[action_hourly_limit]
           ,[action_template_id])
     VALUES
           (@@SERVERNAME
           ,@check_id --check id from the previous query where we created a new check
           ,1 --id of the action we want this check to trigger
           ,0 --we do not want to be notified about every failure. just the first occurence
           ,1 --we want to be notified when the disks returns back to normal
           ,1440 --we want a reminder every day when the disk is below threshold
           ,2 --do not send more than 2 notifications per hour
           ,1 --assosiate with the default action template
		   )
```

That's it. Now when the disk drops below the set thresholds we are going to get an email.

