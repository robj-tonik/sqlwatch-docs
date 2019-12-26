# How do I check if SQLWATCH is running OK?

SQLWATCH contains many components that are driving by the SQL Agent Jobs. Any failures should manifest in these jobs failing. SQLWATCH also contains a number of built-in "self-check" that ensure smooth execution. You can list any problematic checks with this query.

Running this on the central repository will also evalaute all remote instances, including any import errors:

```sql
select *
from [dbo].[vw_sqlwatch_report_dim_check]
where 
	(
		-- get all critical and warning check:
		(last_check_status in ('CRITICAL','WARNING') or last_check_status is null)
		-- but exclude performance and backup checks:
		and check_id not in (
			-43,-37,-36,-34,-33,-32,-30,-29,-28,-25,-24,-23,-22,
			-20,-19,-18,-17
		)
	-- and list any checks that are failing:
	or last_check_status = 'CHECK ERROR'
)
```



