# Install with SSMS

## Introduction

SQL Server Management Studio \(SSMS\) is a free, integrated development environment \(IDE\) for SQL Server.

{% embed url="https://docs.microsoft.com/en-us/sql/ssms/download-sql-server-management-studio-ssms" %}

## Prerequisites

1. SQL Server Management Studio that supports DacPac deployment must be installed prior to installation. This can either be on a client PC or server.

## Installation

Download the required release from our [GitHub Releases](https://github.com/marcingminski/sqlwatch/releases) and unzip. In this example we are using C:\Temp

Connect to the desired SQL Server, right click on Databases and select Deploy Data-Tier Application:

![SSMS Deploy Data-tier Application](../../.gitbook/assets/deploy_datatier_application.png)

Find the SQLWATCH.dacpac you have downloaded and unzipped

![DacPac deploy set source package path](../../.gitbook/assets/deploy_datatier_application_find_file.png)

Specify database name, default and recommended is SQLWATCH:

![DacPac deploy set target database name](../../.gitbook/assets/deploy_datatier_application_set_name.png)

Click next for a summary screen and Next one more time to execute deployment. It can take a minute or two:

![DacPac deploy summary screen](../../.gitbook/assets/deploy_datatier_application_deploy.png)

