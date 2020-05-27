# Data Compression

SQLWATCH comes with two stored procedures that will enable page level data compression on tables and indexes:

`exec [dbo].[usp_sqlwatch_config_set_table_compression]  
exec [dbo].[usp_sqlwatch_config_set_index_compression]`

or

`exec [dbo].[usp_sqlwatch_config_enable_compression_sqlwatch_tables]  
exec [dbo].[usp_sqlwatch_config_enable_compression_sqlwatch_indexes]`

Compression is not enabled by default as this is something each DBA should manage individually. There are many factors that need to be taken into account when enabling data compression. Not all Editions of SQL Server support data compression and whilst some do, such as latest Standard Editions, they have limited resources allocated to compression threads and thus the process may take longer than on the Enterprise Editions. 

