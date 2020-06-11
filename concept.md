# Concept

SQLWATCH was primarily developed for decentralised Performance Monitoring, ad-hoc Performance Testing and Performance Data Logging in Production Environments for later analysis. It relies on the SQL Server Agent to invoke local data collection.

> Each SQL Server monitors itself and alerts only when it needs attention. Power BI Report can be used to analyse historical performance data.

To meet the popular demand for central reporting, an optional centralised reporting repository was recently introduced. 

Most enterprise monitoring solutions are centralised which means they often consist of a central repository and monitoring servers, where monitoring servers execute queries against the monitored SQL instance and send the results back to the repository. Whilst this approach has a lot of benefits it also requires a set of dedicated monitoring infrastructure, servers, licensing, and network configuration to allow remote access to the monitored instances which can add complexity and increase the cost. It can also become single point of failure and a bottleneck. Some solutions also require monitoring agent to be installed locally further increasing complexity. Any network outages between the monitoring server and monitored instance could cause gaps in the collected data. 

SQLWATCH has been designed to address some these challenges, especially in a smaller or test environments where dedicated monitoring infrastructure is not feasible. 

Automation and integration with [dbatools ](https://dbatools.io)makes it easy to keep decentralised deployment in sync and up to date.

{% embed url="https://dbatools.io/" %}

## Components

There are 3 three main and independent components:

### SQLWATCH Database

Database is deployed locally and utilises local SQL agent jobs for data collection. Alternatively, collection can be invoked via local Windows Task Scheduler. **Currently no remote collection is possible**.

### PowerBI Dashboard

The dashboard connects to SQLWATCH database and visualises collected data.

### Central Repository

Optional central repository can be installed to collect data from remote SQLWATCH instances. Note that the repository only loads data from remote SQLWATCH databases into the central database to enable reporting across multiple servers and to enable shortened retention on remote instances. The Central repository database is just ordinary SQLWATCH database where data from remote databases is being loaded with SQL Server Integration package \(SSIS\) or via linked server.

