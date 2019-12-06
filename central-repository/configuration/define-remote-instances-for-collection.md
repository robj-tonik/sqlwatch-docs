# Define remote instances for collection

To start collecting data from a remote instance, add a reference to the configuration table: `[dbo].[sqlwatch_config_sql_instance]`

![](../../.gitbook/assets/image%20%2845%29.png)

**sql\_instance and hostname**

The `sql_instance` is what `@@SERVERNAME` returns on the remote instance and this is what gets logged in the remote tables and `hostname` is the physical host name to connect to. Most of the time they are the same unless you are connecting via IP \(no DNS records\) or you are connecting to SQL Server on Docker, which has different IP and `servername`. 

**sql\_port**  
Optionally you can specify non standard port to connect 

**sqlwatch\_database\_name**  
Name of the database where SQLWATCH is deployed on the remote instance. Default is SQLWATCH.

**environment**  
Custom label to group servers into specific environments in the PowerBI report.

**is\_active**  
Whether to include instance in the collection or not

**last\_collection\_time and collection\_status**  
Are populated during the collection from the remote instance and indicate last collection time and the status.

