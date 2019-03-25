# Storage requirements

The amount of space used by SQLWATCH depends on the retention period and the number of databases on a server. On a server with 10 databases and 7 days retention, the size is around 1.8 GB with majority occupied by `wait_stats` and `performance_counters`

![](../.gitbook/assets/sqlwatch_table_storage.png)

