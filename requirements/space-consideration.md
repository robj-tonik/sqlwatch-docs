---
description: Community help needed.
---

# Space consideration

Space requirement and growth will vary per environment. The more databases, data files, and workload the bigger the collected data will be. 

In certain environments, with lots of large tables and indexes, index statistics and histogram can grow at a rapid pace. Equally, in environments with lots of activity, XES  and WhoIsActive tables can grow rapidly collecting lots of session data. 

{% hint style="warning" %}
Although database size can be controlled by applying appropriate retention periods, the recommendation is that the SQLWATCH database is capped to ring fence other databases and prevent eating up too much space until the DBA team has learned the storage requirements and growth. Once the team is confident with the growth the cap can be lifted.
{% endhint %}

In some cases it may be required to disable some of the collectors, for example index histogram or even index statistics. 

Some design considerations affect storage requirements, such as the use of 16 bytes long `sequential uniqueidentifier` data types in Primary Keys in order to allow data to be collected in central repository without collisions. Whilst  `smallint` IDENTITY fields would be preferable and with appropriate composite Primary Key would not cause duplication, we would still have to deal with repeating values in destination IDENTITY columns. 

Another benefit of  `uniqueidentifier`  is the fact that Power BI is not able to create schema relations based on multiple columns. It requires one unique column. A work around would require building composite keys in the Power Query which could slow down the data load process and prevent query folding.

An option is to generate our own integer based, random keys \(4 bytes `integer`, 4 times smaller than `GUID`\):

`select convert(int,binary_checksum(newid()))`

Or a time based, similar to a Unix timestamp \(4 bytes `integer`, 4 times smaller than `GUID`\):

`select convert(int,datediff(second,{d '1970-01-01'}, getutcdate()))`

or even with greater capacity and precision \(8 bytes `bigint`, half the size of the `GUID`\):

`select convert(BIGINT,DATEDIFF_BIG(MILLISECOND,{d '1970-01-01'}, getutcdate()))`

Such key would be part of a composite primary key and would not cause collision. However, the last two would require inserting rows one by one. The first one would in fact generate different number for each row in the whole batch but there is no guarantee that they would be unique forever.  The last two options would likely be unique if we delayed each row insert by 1s or 1ms.

**If a community has any good tips, please help.**

