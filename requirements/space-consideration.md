# Space consideration

Space requirement and growth will vary per environment. The more databases, data files, and workload the bigger the collected data will be. 

In certain environments, with lots of large tables and indexes, index statistics and histogram can grow at a rapid pace. Equally, in environments with lots of activity, XES  and WhoIsActive tables can grow rapidly collecting lots of session data. 

{% hint style="warning" %}
Although database size can be controlled by applying appropriate retention periods, the recommendation is that the SQLWATCH database is capped to ring fence other databases and prevent eating up too much space until the DBA team has learned the storage requirements and growth. Once the team is confident with the growth the cap can be lifted.
{% endhint %}

In some cases it may be required to disable some of the collectors, for example index histogram or even index statistics. 

## Compression

Page level table and index compression is recommended. Table compression can be applied by executing:

`--table:  
exec [dbo].[usp_sqlwatch_config_set_table_compression]  
  
--index:  
exec [dbo].[usp_sqlwatch_config_set_index_compression]`

## Storage Utilisation Guidelines

An example of a SQL Instance with only SQLWATCH database with standard retention after 7 days of operation

#### Data and Index compression enabled \(49M\)

![](../.gitbook/assets/image%20%2865%29.png)

#### Data and Index compression disabled \(181 MB\)

![](../.gitbook/assets/image%20%2819%29.png)

