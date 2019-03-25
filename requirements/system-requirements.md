# System requirements

SQLWATCH has been tested on the following SQL Server versions:

* 2008 R2 SP3
* 2012
* 2014
* 2016
* 2017 \(including docker and linux\*\)

{% hint style="warning" %}
SQLWATCH works on docker and linux except the disk collector which relies on the Windows' WMI interface. 
{% endhint %}

SQL Server Express and Azure SQL are not supported as there is no Agent to invoke data collection. Theoretically, data collection would be possible via SQLCMD triggered from the Windows Task Scheduler or another Standard Edition instance in case of the Express edition and, for example, Azure Runbook in case of Azure SQL but this has not been tested.

