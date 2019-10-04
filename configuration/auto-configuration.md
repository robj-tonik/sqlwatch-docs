# System \(auto\) configuration

SQLWATCH has been designed with low-maintenance in mind and thus several tasks and configuration items are being applied automatically. 

By default, auto configuration runs periodically every **1 hour** and is invoked by job `SQLWATCH-INTERNAL-CONFIG`

**The below procedures are run as part of the Auto configuration job:**

## dbo.sp\_sql\_perf\_mon\_add\_database

This procedure collects databases from `sys.databases` into a dimension table `dbo.sql_perf_mon_database` required for reporting. If new database is created it will not be available in Power BI until this procedure is run. Analogically, this procedure must be run after SQLWATCH has been deployed in for Power BI to show results. 

> Note that this does not impact the actual data collection, only reporting.

