# dbachecks

Integration with dbachecks allows SQLWATCH to pick up dbachecks' failures and notify via the SQLWATCH actions mechanism. 

The SQLWATCH check is simply querying the `dbo.dbachecksResults` table for any records where the result equals to 'Failed'. 

dbachecks tables are deployed with SQLWATCH to satisfy the check criteria, however, they can be in another database, in which case the check will need to be modified to reference the correct database:

```text
 @check_id = -48
,@check_name = 'dbachecks failed'
,@check_description = 'This check looks up any dbachceks that have a result of failed. Please check the dbachecks dashboard or tables for details.'
,@check_query = 'select @output=count(*)
from DATABASE.[dbo].[dbachecksResults]
where Result = ''Failed'' AND [Date] >= ''{LAST_CHECK_DATE}'''
```

For information around dbachecks please check their website [https://dbachecks.readthedocs.io](https://dbachecks.readthedocs.io/en/latest/)

