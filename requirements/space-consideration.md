# Space consideration

Space requirement and growth will vary per environment. The more databases, data files, and workload the bigger the collected data will be. 

In certain environments, with lots of large tables and indexes, index statistics and histogram can grow at a rapid pace. Equally, in environments with lots of activity, XES  and WhoIsActive tables can grow rapidly collecting lots of session data. 

{% hint style="warning" %}
Although database size can be controlled by applying appropriate retention periods, the recommendation is that the SQLWATCH database is capped to ring fence other databases and prevent eating up too much space until the DBA team has learned the storage requirements and growth. Once the team is confident with the growth the cap can be lifted.
{% endhint %}

In some cases it may be required to disable some of the collectors, for example index histogram or even index statistics. 

## Compression

Page level table and index compression is recommended. Table compression can be applied by executing:

`exec [dbo].[usp_sqlwatch_config_set_table_compression]`

## Design Considerations that impact storage utilisation. 

Some design considerations affect storage requirements, such as the use of 16 bytes long `sequential uniqueidentifier` data types in Primary Keys in order to allow data to be collected in central repository without collisions. Whilst `smallint` IDENTITY fields would be preferable and with appropriate composite Primary Key would not cause duplication, the Power BI is not able to create schema relations based on multiple columns. It requires one unique column. A work around would require building composite keys in the Power Query which could slow down the data load process and prevent query folding \(as it was in version 1.x\).



