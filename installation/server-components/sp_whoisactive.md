# sp\_WhoIsActive

SQLWATCH can log output from Adam Machanic's, fantastic `sp_WhoIsAcitve` which can also be installed using dbatools:

`Install-DbaWhoIsActive -SqlInstance YourServer -Database master`

SQLWATCH will look for `sp_WhoIsActive` in either the master database or the database where the SQLWATCH is installed \(default SQLWATCH but it could any database\)

`Install-DbaWhoIsActive -SqlInstance YourServer -Database SQLWATCH`

