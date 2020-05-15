# Primary Keys

Database has been designed with non-identifying relations with natural keys where possible. This reduces the number of required joins to denormalise schema for consumption and thus increases read performance at a slightly increased storage utilisation.

An example would be the use of `@@SERVERNAME` as a `sql_instance` and `snapshot_time` in all tables rather than numerical IDs.

This allows us to simply query the data table applying where clause on server and time, instead of joining back to the time and server tables to get the actual values. 

snapshot\_time is stored as 6 bytes long `datatime2(0)` so not much bigger than 4 byte long `integer` if we were to use identity field. `sql_instance` however is stored as `varchar(32)` as the server name can be made of 15 characters host name and 17 characters instance name. 

