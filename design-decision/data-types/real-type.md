# Real Type

Using approximate data types such as float and real can save lots of storage when the exact number is not required. In case of performance data this is not a problem even if we are out by few KBs in a GB scale.

For example, reading file statistics `sys.dm_io_virtual_file_stats` gives the following value for `num_of_bytes_read`:

1447418880

In a Real data type this would be:

1.447419E+09

Quick conversion to Mega Bytes reveals negligible loss of accuracy:

![](../../.gitbook/assets/image%20%2817%29.png)

![](../../.gitbook/assets/image%20%28105%29.png)

Taking it one step further and simulating even larger number:

![](../../.gitbook/assets/image%20%2887%29.png)

![](../../.gitbook/assets/image%20%285%29.png)

And even bigger 2705311284433920 bytes:

![](../../.gitbook/assets/image%20%289%29.png)

![](../../.gitbook/assets/image%20%2851%29.png)

