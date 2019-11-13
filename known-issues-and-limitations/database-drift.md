# Database drift

In some cases, you may receive the following error when upgrading from DacPac:

```text
Database has drifted from its registered data-tier application
```

When SQLWATCH is deployed, it registers itself as data-tier application, which adds a record in `msdb.dbo.sysdac_instances`. 

![](../.gitbook/assets/image%20%2823%29.png)

This is userful to identify currently installed version of SQLWATCH.

The error may happen when database objects have been changed since the last deployment, for example, when you deploy SQLWATCH into your existing "dba\_tools" database and add or remove some other tables, not related to SQLWATCH.

## Unregister Data-Tier Application

To work around this issue, we have to unregister data-tier application. This can be done in SQL Server Management Studio:

Right click database -&gt; Tasks -&gt; Delete Data-Tier Application

![](../.gitbook/assets/image%20%2835%29.png)

Alternatively, you can use T-SQL to achieve the same:

```text
declare @instance_id uniqueidentifier
declare @database_name sysname = 'SQLWATCH'

select @instance_id = instance_id
from msdb.dbo.sysdac_instances dp 
where dp.instance_name = @database_name

exec dbo.sp_sysdac_delete_instance 	
    @instance_id = @instance_id
    
exec dbo.sp_sysdac_update_history_entry 	
    @action_id=21,	
    @instance_id=@instance_id,	
    @action_type=14,	
    @dac_object_type=0,	
    @action_status=2,	
    @dac_object_name_pretran=@database_name,	
    @dac_object_name_posttran=@database_name,	
    @sqlscript=NULL,	
    @error_string=N''
```

