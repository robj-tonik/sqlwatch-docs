# SQL Server Configuration

Although there is no specific SQL Server configuration required, some changes may be required in order to capture relevant performance data or to apply table compression to improve storage utilisation.

Although most DBAs will know best what configuration works best in their environment, a number of configuration procedures _`usp_sqlwatch_config_*`_ have been included to make this process easier.

## Blocked process threshold

In order for SQLWATCH to record blocking chains we have to enable The `blocked process threshold`for a specific time threshold. 

`--default threshold will be 15 seconds:  
exec [dbo].[usp_sqlwatch_config_set_blocked_proc_threshold]   
  
--to applly different threshold:  
exec [dbo].[usp_sqlwatch_config_set_blocked_proc_threshold] @threshold_seconds = x` 

## Table compression

You may wish to compress data in SQLWATCH to improve storage utilisation and I/O performance at the cost of CPU utilisation. You can do so by running:

`exec [dbo].[usp_sqlwatch_config_set_table_compression]` 

## Recreate agent jobs

To create all default SQLWATCH agent jobs you can run:

`--add any missing SQLWATCH jobs, will not remove existing SQLWATCH jobs:  
exec [dbo].[usp_sqlwatch_config_set_default_agent_jobs]  
  
--remove existing and recreate all SQLWATCH jobs:  
[dbo].[usp_sqlwatch_config_set_default_agent_jobs]`



