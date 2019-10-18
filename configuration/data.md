---
description: First-run configuration.
---

# Post-deployment configuration

Default configuration is applied during deployment and although there is no manual post-deployment configuration required the collection will not start until the job `SQLWATCH-INTERNAL-META-CONFIG` runs. The job is scheduled to run every 1 hour but can be run manually post-deployment to speed up data collection.

This job is responsible for collection dimension objects, i.e. list of databases, tables, indexes etc for the normalised schema. Equally, when new database or table is added, any metric that relates to this database or table will not be collected until the job `SQLWATCH-INTERNAL-META-CONFIG` runs again. This is to improve performance of the performance collector job and avoid getting list of relatively static objects every minute. 

