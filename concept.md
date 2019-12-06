# Concept

SQLWATCH is a decentralised SQL Server monitoring framework with centralised reporting and optional, centralised repository. It relies on the SQL Server Agent to invoke local data collection.

Most enterprise monitoring solutions are centralised which means they often consist of a central repository and monitoring servers, where monitoring servers execute queries on the monitored SQL instance and send the results to the repository. Whilst this approach has a lot of benefits it also requires a set of dedicated monitoring infrastructure, servers, licensing, and network configuration to allow remote access to the monitored instances which can add complexity and increase the cost. Some solutions also require monitoring agent to be installed locally further increasing complexity. Any network outages between the monitoring server and monitored instance could cause gaps in the collected data. 

SQLWATCH has been designed to address some these challenges, especially in a smaller or test environments where dedicated monitoring infrastructure is not feasible. 

Automation and integration with [dbatools ](https://dbatools.io)makes it easy to keep decentralised deployment in sync and up to date.

## Components

There are 3 three main and independent components:

### SQLWATCH Database

Database is deployed locally and utilises local agent jobs for data collection. Alternatively, collection can be invoked via local Windows Task Scheduler. **Currently no remote collection is possible**.

### PowerBI Dashboard

The dashboard connects to SQLWATCH database and visualises collected data.

### Central Repository

Optional central repository can be installed to collect data from remote SQLWATCH instances. Note that the repository only loads data from remote SQLWATCH databases into the central database to enable reporting across multiple servers and to enable shorted retention on remote instances. 

