---
description: First-run configuration.
---

# Post-deployment configuration

Default configuration is applied during deployment and although there is no manual post-deployment configuration required there are few things to be aware of. 

SQLWATCH creates database dimension form `sys.databases` and stores it in the table `dbo.sql_perf_mon_database` for reporting purposes. By default, this collection happens every hour.

The Power BI dashboard will not show any database-level data until the database dimension is populated. If you cannot wait for the next scheduled run, the auto-configuration can be invoked manually by running job `SQLWATCH-INTERNAL-CONFIG`. 

> Performance data collection is independent of the database dimension table and will be collected from the moment SQLWATCH is deployed.

You can read more about Auto Configuration routines in the Auto Configuration section. 

