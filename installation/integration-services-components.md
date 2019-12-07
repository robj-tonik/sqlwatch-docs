# Integration Services components

SQLWATCH Central Repostory requires Integration Services package in order to collect data from remote instance. It can be deployed from Visual Studio project of ISPAC included in the release. 

The Project consists of two packages: Control Package and the Worker Package. 

![](../.gitbook/assets/image%20%2873%29.png)

## Package Configuration

### Control package

The control package `control_import.dtsx` is responsible for orchestrating multi-threaded data collection and execution of the Worker Package `import_remote_data.dtsx`

![](../.gitbook/assets/image%20%2854%29.png)

#### Parameters

**number\_of\_parallel\_collectors**  
Number of threads for parallel collection. If this is set to &gt; 1, then multiple servers will be collected in parallel, in addition to each collector data flow being run in parallel, according to the MaxConcurrentExecutables parameter. Be careful as running parallel collectors may be slower than single thread. Make sure central repository can sustain the workload. Maximum allowed parallel threads are 8.

**repository\_database**  
Name of the database where the central repository is. Default SQLWATCH.

**repository\_instance\_name**  
Name of the SQL Server instance where the central repository is hosted.

**repository\_password**  
SQL Password to access central repository or blank for Windows authentication.

**repository\_user\_name**  
SQL User to access central repository or blank for Windows authentication.

### Worker Package

The worker package `import_remote_data.dtsx` is responsible for the actual data collection from remote instances into the central repository. 

![](../.gitbook/assets/image%20%2891%29.png)

#### Parameters

**last\_snapshot\_offset\_minutes**  
Offset in minutes to increase delta time slice. By default only data since last snapshot will be collected from the remote instance. We may increase this and go further beyond that to cover any gaps. Behind the scenes this translates to `[snapshot_time] > dateadd(minute,-@last_snapshot_offset_minutes,[last_snapshot_time])`

{% hint style="warning" %}
Not currently used, reserved for future use
{% endhint %}

**remote\_instance\_name**  
SQL Instance to collect data from. This parameters is passed from the control package during run time.

**remote\_password**  
SQL Password for the remote instance or blank for Windows authentication.

**remote\_user\_name**  
SQL User for the remote instance or blank for Windows authentication.

{% hint style="info" %}
In the current implementation it is not possible to specify different accounts for accessing remote instances. This means that when using SQL Authentication all instances must have the same SQL User and Password. When using Windows authentication this is usually not a problem as the SSIS runs under a context of one the SQL agent or proxy account
{% endhint %}

**repository\_database**  
Name of the database where the central repository is. Default SQLWATCH.

**repository\_instance\_name**  
Name of the SQL Server instance where the central repository is hosted.

**repository\_password**  
SQL Password to access central repository or blank for Windows authentication.

**repository\_user\_name**  
SQL User to access central repository or blank for Windows authentication.

