# Permissions

### SQL Server permissions required for database deployment

In order to install SQLWATCH the following minimum permissions are required:

| Permission | reason |
| :--- | :--- |
| `dbcreator` | Create SQLWATCH database as part of the deployment process |
| `GRANT CREATE ...` | Object creation during the deployment.  |
| `SQLAgentUserRole` | Create SQL Agent jobs |
| `Windows Administrator` | Only when using Windows Scheduled Tasks instead of SQL Agent for collector invocation. Windows Administrator permission will be require in order to create and schedule tasks to run in the background. |

### SQL Server permissions required for data collection

{% hint style="warning" %}
**Not defined**. It is expected that collection will run under local SQL Agent account which will have `sa` rights. However, **this is not a requirement** I just have not got minimum requirements defined for the collectors yet.
{% endhint %}

