# Storage Utilisation

SQLWATCH schema has been design with long term storage in mind. If possible, it is advisable to enable page compression on SQLWATCH data tables and indexes reducing utilisation by further 25-50%. The amount of space used by SQLWATCH depends on the retention period, number of databases on the server and the workload. As a guidance, below is the size of SQLWATCH in my test environment, with data compression enabled, after 30 days of use:

![Top tables after 30 days of use](../.gitbook/assets/image%20%2812%29.png)

{% hint style="info" %}
Appropriate index maintenance must in place in order to make sure table size is not being bloated over time.
{% endhint %}

