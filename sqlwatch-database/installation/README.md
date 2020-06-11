# Installation

Server components are installed on each monitored SQL Server instance and consist of the SQLWATCH database and SQL Agent jobs.

{% hint style="danger" %}
SQLWATCH has been developed in Visual Studio Data Tools and the base for deployments are Data Application Tier Packages \(DacPac\). [There are some important factors that one should be aware of before deploying DacPac which one can read here.](../../reference/data-tier-application-package.md)
{% endhint %}

{% hint style="success" %}
There are several ways to install server side components and each way will deploy all the required objects, including Agent Jobs, reference data and apply default configuration.
{% endhint %}

{% hint style="warning" %}
Even though each stable release of SQLWATCH has been tested and is production ready you should still test it in your environment first.
{% endhint %}



