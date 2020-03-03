# Performance Overhead

SQLWATCH is designed with minimum overhead. It utilises [SQL Server Extended Events \(XES\)](https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events) where possible and [Dynamic Management Views \(DMV\)](https://docs.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views) collectors that run every minute by default.

> SQL Server The Extended Events architecture enables users to collect as much or as little data as is necessary to troubleshoot or identify a performance problem. Extended Events is configurable, and it scales very well.

{% hint style="info" %}
I have not observed nor has any performance overhead or increased CPU utilisation been reported to me. If you notice anything suspicious please feed back ASAP.
{% endhint %}

The frequent data collectors such as performance run every minute and take less than a second to execute. There are areas for improvement in the way the XML output from XE sessions is being parsed which will be addressed in the future releases.

The below screenshot shows a 60 seconds of CPU utilisation of the `sqlservr.exe` process. The spike is the performance collection which lasts few milliseconds:

![](../../.gitbook/assets/image%20%2866%29.png)

#### Additional Reading:

{% embed url="https://docs.microsoft.com/en-us/sql/relational-databases/extended-events/extended-events" %}

{% embed url="https://docs.microsoft.com/en-us/sql/relational-databases/system-dynamic-management-views/system-dynamic-management-views" %}



