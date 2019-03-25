# Installing with dbatools

SQLWATCH can be installed across multiple-servers using dbatools:

```text
Install-DbaSqlWatch -SqlInstance Server1, Server2, Server3 -Database SQLWATCH
```

[![Watch this short clip](http://img.youtube.com/vi/W38osuBv_Q8/0.jpg)](http://www.youtube.com/watch?v=W38osuBv_Q8)

> The `Install-DbaSqlWatch` was designed for unattended multi-server installations. It will download the latest release and unpack it, including the Power BI dashboard, into its own temporary directory.

## Beta releases \(pre-releases\)

Beta release can be installed with a `-PreRelease` switch:

```text
Install-DbaSqlWatch -SqlInstance DevServer1 -Database SQLWATCH -PreRelease
```

