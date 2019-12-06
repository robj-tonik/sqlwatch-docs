# Removal

SQLWATCH database can be removed in two ways

## Removal with dbatools

Removal command [`Uninstall-DbaSqlWatch`](https://docs.dbatools.io/#Uninstall-DbaSqlWatch)  which removes SQLWATCH objects including database and Agent Jobs.

> The `Uninstall-DbaSqlWatch` will only work if the database was installed using `Install-DbaSqlWatch`

There are safety measures built into the removal process to make sure that only objects deployed by `Install-DbaSqlWatch` are removed, including database. If the deployment was into an existing database this will not be removed, analogically, if user tables were added to the SQLWATCH database post-deployment they were not registered as part of the application and thus they will not be removed and subsequently the database will not be dropped. 

## Removal with T-SQL

If SQLWATCH was installed manually the only way to remove is to manually invoke `DROP DATABASE` and manually remove SQL Agent jobs.

## Removal when using Windows Scheduled Tasks

When using Windows Scheduled Tasks instead of SQL Agent to invoke data collection, please remove Scheduled Tasks manually and any associated PowerShell scripts - these are created manually upon user request and as per User defined Path.



