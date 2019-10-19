# Structure

## Stored Procedures

### usp\_sqlwatch\_config\_\*

Configuration helpers to help apply relevant, and optional, configuration to SQL Server Instance. To be run by the user on demand, **not scheduled**. 

### usp\_sqlwatch\_internal\_\*

Procedures used internally by SQLWATCH.

### usp\_sqlwatch\_logger\_\*

Data Collectors scheduled by the Agent Jobs.

### usp\_sqlwatch\_report\_\*

Interface procedures generating standardised report data, currently used by Power BI but can be used by any other reporting tool. As of version 2.0 they are being written and expanded. Not all metrics are covered yet.

