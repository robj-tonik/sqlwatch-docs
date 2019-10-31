# Login failed error when running disk logger

In some cases you may be getting the following error when running Step 2 of the SQLWATCH-LOGGER-DISK-UTILISATION Agent Job:

```text
Cannot open database "SQLWATCH" requested by the login. The login failed.  Login failed for user 'HOME\SQL-TEST-1$'
```

This is because PowerShell jobs run under a SQL Agent context and this means they may not have permissions to the SQL Server and the SQLWATCH database.

> SQLWATCH will not alter your server security configuration or permissions or create any accounts. If you do encounter this error you will have to fix it manually. Depending on your environment, there may be different ways to address this, some more appropriate and some less, again, depending on your setup.

The recomended and most secure way is to create a [SQL Agent Proxy Account](https://docs.microsoft.com/en-us/sql/ssms/agent/create-a-sql-server-agent-proxy?view=sql-server-2017) and grant this account db\_datawriter and db\_datareader roles in the SQLWATCH database. This account will need appropriate access to read OS disks. This account will ONLY have access you have created.

An alternative and slightly easier way is to grant `db_datawriter` and `db_datareader` roles to the login reported in the error in the SQLWATCH database. However, in this case, we may be granting permission to the SQLWATCH database to an account that perhaps should not have such access. Please be sure you are familiar with the security configuration in your environment. In our example this would be:

```text
USE [master]
GO
CREATE LOGIN [HOME\SQL-TEST-1$] FROM WINDOWS
GO
USE [SQLWATCH]
GO
CREATE USER [HOME\SQL-TEST-1$] FOR LOGIN [HOME\SQL-TEST-1$]
GO
ALTER ROLE [db_datawriter] ADD MEMBER [HOME\SQL-TEST-1$]
GO
ALTER ROLE [db_datareader] ADD MEMBER [HOME\SQL-TEST-1$]
GO
```

