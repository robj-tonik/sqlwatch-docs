# Collation conflict

## Abstract

If you encounter collation conflict during installation it means that your server’s collation is different to the SQLWATCH database collation and SQL cannot handle string comparisons.

We use the `Latin1_General_CI_AS` collation.

There are two ways to solve this

## Option 1: **Manually create an empty database**

By default, SQL Server creates new databases with the default servers' collaction unless othwerise specified. The collation cannot be changed once the database has been created. By manually creating SQLWATCH database will force default collation:

```text
CREATE DATABASE [SQLWATCH]
GO
```

Once the empty shell database has been created we can proceed with installation as usual.

## Option 2: Rebuild project into the desired target collation

If the above does not meet your requirements you can load the database solution in Visual Studio \(please follow "Deploy from source code" guide for details\) , change database collation to the desired value and rebuild and deploy.

