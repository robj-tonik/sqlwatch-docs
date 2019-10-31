# Power BI Joins

Power BI can only build schema relations based on one column. SQLWATCH is using non-identifying relations design pattern and therefore it is using composite primary keys that use more than one column to make up a key. This will not work in Power BI.

For example, we can have database with ID 1 on all servers but in combination with a server name they create unique values as there can only be one database with ID 1 on each of the servers. 

A work around to make this work in Power BI is to add custom step in Power Query and add a custom column with key columns concatenated into one.

Or, use unique identifier data types that will ensure global uniqueness. 

However, unique identifiers will have significant impact on storage utilisation performance. Even with the use of sequential identifiers performance is not guaranteed. 

A better performing and more flexible approach is to move this concatenation to the database engine and apply in the reporting views, on demand:

`pbi_sqlwatch_database_id = sql_instance + '.DB.' + convert(varchar(10),sqlwatch_database_id)`

![](../.gitbook/assets/image%20%282%29.png)

This will reduce number of Power Query transformations to minimum and will be re-usable across different reporting platforms. 

