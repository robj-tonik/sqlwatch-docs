# Relations

Relation between tables are enforced with primary and foreign keys, with cascade actions where appropriate. 

The exception are action and check tables, where we had to "detach" logger tables from config tables in order to import logger into central repository without also importing config tables. Configuration tables are defined for a local scope only and for that reason the `sql_instance` is not part of the primary key.

In this instance, cascade actions are handled by triggers:

![](../.gitbook/assets/image%20%2846%29.png)

## Entity Relationship Diagram

![SQLWATCH 2.3 ERD](../.gitbook/assets/sqlwatch_2.3.png)

