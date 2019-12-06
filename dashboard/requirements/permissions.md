# Permissions

### Windows permissions

A normal Windows User account is enough to open and refresh the Power BI reports. An Administrative access will be required to Install Power BI Desktop. Please refer to the Power BI installation guide:

{% embed url="https://powerbi.microsoft.com/en-us/desktop/" %}

### SQL Server permissions required for reports

In order to retrieve data from the SQLWATCH database the following permissions are required:

| Permission | Description |
| :--- | :--- |
| `SELECT` | PowerBI Dashboard utilises Direct Queries to read from SQL views and explicit permissions to tables are not required by the PowerBI users. |

