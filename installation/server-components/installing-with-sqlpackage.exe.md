# Install with SqlPackage

## Introduction

`SqlPackage.exe` is a command line utility that automates SQL Server database deployments. This command comes with SQL Server Management Studio \(SSMS\) and is located in the ...\DAC\bin folder:

`C:\Program Files (x86)\Microsoft SQL Server\140\DAC\bin\SqlPackage.exe`

> Where 140 is the version of installed Management Studio. Your version and path may be different to the example above.

You can read more about `SqlPackage.exe` in [Microsoft Docs](https://docs.microsoft.com/en-us/sql/tools/sqlpackage)

## Prerequisites

1. SqlPackage.exe must be installed on the computer running installation.

## Installation

Download the required release from our [GitHub Releases](https://github.com/marcingminski/sqlwatch/releases) and unzip. In this example we are using C:\Temp

An example command to install SQLWATCH:

```text
SqlPackage.exe 
    /Action:Publish 
    /SourceFile:C:\Temp\SQLWATCH.dacpac 
    /TargetDatabaseName:SQLWATCH 
    /TargetServerName:YOURSQLSERVER 
    /p:RegisterDataTierApplication=True
```

