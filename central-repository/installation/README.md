# Installation

## SQL Database

Please refer to the SQLWATCH Database Installation section

## SQL Server Integration Package

{% hint style="info" %}
It is assumed that the SSIS Server is installed and configured and that the SSISDB has been initialised and the environment is operational.
{% endhint %}

{% embed url="https://docs.microsoft.com/en-us/sql/integration-services/install-windows/install-integration-services" %}

### Deploy ISPAC

Each SQLWATCH release will include [ISPAC \(Integration Services Project Deployment File Format\)](https://docs.microsoft.com/en-us/openspecs/sql_data_portability/ms-ispac/). 

{% embed url="https://www.youtube.com/watch?v=RKfOBlTXk\_A&feature=youtu.be" %}

Official Microsoft Guide:

{% embed url="https://docs.microsoft.com/en-us/sql/integration-services/packages/deploy-integration-services-ssis-projects-and-packages?view=sql-server-ver15" %}

### Deploy from Visual Studio Project

If you prefer, you can also deploy packages directly from the source in Visual Studio.

