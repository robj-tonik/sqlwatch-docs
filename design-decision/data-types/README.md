# Data Types

Smallest possible data types were used where possible. In case of identity fields, it is always recommended to start with the leftmost value, for example, for **smallint** we should start with -32768:

`IDENTITY(-32768,1)`

This doubles the capacity of the identity field vs when starting from zero. However, when using page or row compression, the following applies:

From Microsoft Docs: [https://docs.microsoft.com/en-us/sql/relational-databases/data-compression/row-compression-implementation](https://docs.microsoft.com/en-us/sql/relational-databases/data-compression/row-compression-implementation)

![](../../.gitbook/assets/image%20%2814%29.png)

Which means that if we use **smallint** data type \(2 bytes\) and start identity from 0, it will only use 1 bytes until 2 bytes are required to accommodate the value. Therefore it is of benefit to start identity at 0, rather than negative leftmost value. If capacity is of concern, it is of more benefit to change the data type to **int** or **bigint** and still start at zero. When it comes to worst and system runs out of identify values, we can reseed with negative values. 

