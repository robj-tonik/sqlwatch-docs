# Upgrade

SQLWATCH has been developed in Visual Studio which is based on [Declarative Deployment Model](https://blogs.msdn.microsoft.com/gertd/2009/06/05/declarative-database-development/). This means that when database is deployed, the deployment mechanism works out what needs to be done in order to bring the target database to the desired version.

{% embed url="https://blogs.msdn.microsoft.com/gertd/2009/06/05/declarative-database-development/" %}

Summarising, to upgrade SQLWATCH database one simply follows the installation process. The only exception is when using SSMS, there is an explicit Upgrade Option in the database context:

![](../../.gitbook/assets/image%20%2854%29.png)

## Challenges

Whilst declarative deployment makes the development very easy and deployment very reliable \(either all or nothing\) it can be a bottleneck when large schema changes are required. For example, migrating data type from UNIQUE IDENTIFIER to INTEGER would fail as such conversion is impossible. When this happens, manual migrations scripts are required which will be noted in the release notes.



