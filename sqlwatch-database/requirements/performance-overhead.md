# Performance Overhead

SQLWATCH is designed with minimum overhead. It utilises [**SQL Server Extended Events \(XES\)**](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events) where possible and [**Dynamic Management Views \(DMV\)**](https://docs.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views) collectors that run every minute by default.

> SQL Server The Extended Events architecture enables users to collect as much or as little data as is necessary to troubleshoot or identify a performance problem. Extended Events is configurable, and it scales very well.

{% hint style="info" %}
I have not observed nor has any performance overhead or increased CPU utilisation been reported to me. If you notice anything suspicious please feed back ASAP.
{% endhint %}

