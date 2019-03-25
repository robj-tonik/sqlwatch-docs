# Upgrade

Similarly to the installation, SQLWATCH can be upgraded in various ways.

## Upgrade with dbatools

To upgrade SQLWATCH using dbatools simply re-run the installation with `Install-DbSqlWatch` and it will automatically bring the database schema to the most recent version. If the database is already the most recent version the `Install-DbaSqlWatch` will not make any changes. 

## Upgrade with SqlPackage.exe

To upgrade with the command line utility `SqlPackage.exe` simply re-run the installation and it will automatically bring the database schema to the desired version. 

## Upgrade with SQL Server Management Studio \(SSMS\)

To upgrade using SQL Server Management Studio please follow the installation steps with the only different being that instead of Deploy Data-tier Application you will have to click on the database you want to upgrade \(SQLWATCH\) and select **Upgrade Data-tier Application**

![SSQM Upgrade DacPac](../.gitbook/assets/upgrade-database-dacpac.png)

