---
description: DacPac
---

# Data-Tier Application Package

Data-Tier Application Package \(DacPac\) is a logical schema definition package that contains all database objects in one single file. 

You can read more abot DacPac in [Microsoft Docs](https://docs.microsoft.com/en-us/sql/relational-databases/data-tier-applications/data-tier-applications)

All SQLWATCH installations are based on DacPacs and each SQLWATCH [GitHub Release](https://github.com/marcingminski/sqlwatch/releases) contains the necessary Packages: 

| Package | Description |
| :--- | :--- |
| **SQLWATCH.dacpac** | The SQLWATCH database including reference data and Agent Jobs |
| **master.dacpac** | Required for the deployment to validate internal references to the master database. The master database WILL NOT be affected in anyway. |
| **msdb.dacpac** | Required for the deployment to validate internal references to the msdb database but the msdb database WILL NOT be affected in anyway. |

