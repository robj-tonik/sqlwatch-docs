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
```





