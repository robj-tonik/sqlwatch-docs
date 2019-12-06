---
description: Minimum requirements to host Central Repository
---

# Requirements

## SQL Database

Central Repository is just another SQLWATCH database, the same requirements and principles apply. Although any existing SQLWATCH database can become central repository at any point in time it is recommended to have it on a dedicated host due to the potential workload and performance overhead as it will be downloading data from the remote SQLWATCH  databases into the central location.

The Central Repository Server will also be monitored locally, in the same way as any other SQLWATCH deployment.

## SQL Integration Service \(SSIS\)

SSIS Package is used to download data from remote SQLWATCH databases.

{% hint style="success" %}
SQL Server Integration Services 2012 and higher
{% endhint %}

The Central Repository database does not have to be hosted on the SSIS server, in other words, there can be dedicated SQL Server hosting the central repository and one or more dedicated SSIS Servers.

{% embed url="https://docs.microsoft.com/en-us/sql/integration-services/sql-server-integration-services" %}

