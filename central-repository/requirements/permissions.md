# Permissions

## SQL Server permissions required for Central Repository

Permissions required on the remote instance:

| Database | Permissions | Description |
| :--- | :--- | :--- |
| SQLWATCH | `db_datareader` | To read data from the remote instance |

Permissions required on the local instance where central repository is:

| Database | Permissions | Description |
| :--- | :--- | :--- |
| SQLWATCH | `db_datareader` | To read data from the local instance |
|  | `db_datawriter` | To write data from the remote instance |
|  | `db_ddladmin` | For bulk inserts |



