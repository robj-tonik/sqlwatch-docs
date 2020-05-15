# Install with dbatools

## Introduction

[dbatools ](https://dbatools.io/)is a free PowerShell module with over 500 SQL Server best practice, administration, development and migration commands included. 

## Prerequisites

1. [dbatools ](https://dbatools.io/)must be installed on the computer running installation and the computer must have internet access in order to download SQLWATCH release. Best practice is to run installation from a client PC and not on the server.

{% embed url="https://dbatools.io/" %}

## Stable releases

SQLWATCH can be installed across multiple-servers using dbatools:

```text
Install-DbaSqlWatch -SqlInstance Server1, Server2, Server3 -Database SQLWATCH
```

Watch this short clip showing how to install SQLWATCH with `Install-DbaSqlWatch` :

[![Watch this short clip](http://img.youtube.com/vi/W38osuBv_Q8/0.jpg)](http://www.youtube.com/watch?v=W38osuBv_Q8)

> The `Install-DbaSqlWatch` was designed for unattended multi-server installations. It will download the latest release and unpack it, including the Power BI dashboard, into its own temporary directory.

## Beta releases \(pre-releases\)

Beta release can be installed with a `-PreRelease` switch:

```text
Install-DbaSqlWatch -SqlInstance DevServer1 -Database SQLWATCH -PreRelease
```

> Beta releases can contain bugs and are **not** suitable for production deployments.

