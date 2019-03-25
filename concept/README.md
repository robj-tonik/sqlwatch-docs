# Concept

SQLWATCH is a decentralised monitoring system with centralised reporting, but without centralised repository. It relies on the SQL Server Agent to invoke data collection and therefore the collection must happen to a local database.

Most enterprise monitoring solutions are centralised which means they often consist of a central repository and monitoring servers, where monitoring servers execute queries on the monitored SQL instance and send the results to the repository. Whilst this approach has a lot of benefits it also requires a set of dedicated monitoring infrastructure, servers, licensing, and network configuration to allow remote access to the monitored instances which can add complexity and increase the cost. Some solutions also require monitoring agent to be installed locally further increasing complexity. Any network outages between the monitoring server and monitored instance could cause gaps in the collected data. 

SQLWATCH has been designed to address some these challenges, especially in a smaller or test environments where dedicated monitoring infrastructure is not feasible. 

Automation and integration with [dbatools ](https://dbatools.io)makes it easy to keep decentralised deployment in sync and up to date.

