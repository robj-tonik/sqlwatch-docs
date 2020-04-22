# Large Environments

## Limitations

There is no limit how many servers can SQLWATCH monitor. It is being deployed in environments with over 3000 servers and due to its decentralised design, there are no "how many servers can the monitoring server monitor" concerns.

## Central Repositories

In large environments it is advisable to create more than one central repository: one or more for Production, one for QA, DEV etc. Instead of putting everything into one bucket, think about how you would like to report and monitor your environment. Perhaps more than one repository for production servers of different  regions or cities, applications, use case, departments etc.

## Data Volumes

In large and busy environments or in environments where space is a concern the following collectors can be disabled to limit the amount of data collected:

* Index Statistics and Histograms 
* Long Queries

Furthermore, retention can be decreased to 1 or 2 days, or central repository deployed to offload data from remote instances.

Please use the Top Tables report in SQL Server Management Studio to get an idea which tables are growing exponentially. 

