# Removal

SQLWATCH can be removed in two ways

## Automated removal with dbatools

dbatools comes with a removal command [`Uninstall-DbaSqlWatch`](https://docs.dbatools.io/#Uninstall-DbaSqlWatch)  which removes SQLWATCH objects including database and Agent Jobs.

> The `Uninstall-DbaSqlWatch` will only work if the database was installed using `Install-DbaSqlWatch`

There are safety measures built into the removal process to make sure that only objects deployed by `Install-DbaSqlWatch` are removed, including database. If the deployment was into an existing database this will not be removed, analogically, if user tables were added to the SQLWATCH database post-deployment they were not registered as part of the application and thus they will not be removed and subsequently the database will not be dropped. 

## Manual removal with T-SQL

If SQLWATCH was installed manually the only way to remove is to manually invoke `DROP DATABASE` and manually remove SQL Agent job.



