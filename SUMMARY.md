# Table of contents

* [Welcome](README.md)
* [Concept](concept.md)

## SQLWATCH Database

* [Requirements](sqlwatch-database/requirements/README.md)
  * [Permissions](sqlwatch-database/requirements/permissions.md)
  * [Performance Overhead](sqlwatch-database/requirements/performance-overhead.md)
  * [Storage Utilisation](sqlwatch-database/requirements/storage-utilisation.md)
* [Installation](sqlwatch-database/installation/README.md)
  * [Install with dbatools](sqlwatch-database/installation/dbatools.md)
  * [Install with SqlPackage](sqlwatch-database/installation/installing-with-sqlpackage.exe.md)
  * [Install with SSMS](sqlwatch-database/installation/install-with-ssms.md)
  * [Deploy from source code](sqlwatch-database/installation/deploy-from-sources.md)
  * [Optional Components](sqlwatch-database/installation/optional-components.md)
  * [Upgrade](sqlwatch-database/installation/upgrade.md)
  * [Removal](sqlwatch-database/installation/removal.md)
  * [Downgrade](sqlwatch-database/installation/downgrade.md)
* [Configuration](sqlwatch-database/configuration-1.md)
* [Known Issues](sqlwatch-database/known-issues/README.md)
  * [Collation conflict](sqlwatch-database/known-issues/collation-conflict.md)
  * [Database drift](sqlwatch-database/known-issues/database-drift.md)
  * [Login failed error when running disk logger](sqlwatch-database/known-issues/login-failed-error-when-running-disk-logger.md)
  * [Deadlock when creating database](sqlwatch-database/known-issues/deadlock-when-creating-database.md)
* [Notifications](notifications/README.md)
  * [Checks](notifications/checks.md)
  * [Actions](notifications/actions.md)
  * [Reports](notifications/reports.md)
  * [How To](notifications/how-to/README.md)
    * [Add or modify check](notifications/how-to/get-notified-when-disk-has-low-free-space.md)
    * [Add or modify action](notifications/how-to/add-or-modify-action.md)
    * [Add or modify report](notifications/how-to/get-notified-about-blocking-chains.md)
  * [Process Flow](notifications/process-flow.md)
* [Large Environments](large-environments.md)

## Central Repository

* [Requirements](central-repository/requirements/README.md)
  * [Permissions](central-repository/requirements/permissions.md)
* [Installation](central-repository/installation/README.md)
  * [Removal](central-repository/installation/removal.md)
  * [Upgrade](central-repository/installation/upgrade.md)
* [Configuration](central-repository/configuration.md)
* [Known Issues](central-repository/known-issues.md)

## Power BI Dashboard <a id="dashboard"></a>

* [Requirements](dashboard/requirements/README.md)
  * [Permissions](dashboard/requirements/permissions.md)
* [Installation](dashboard/installation.md)
* [Configuration](dashboard/configuration.md)
* [Known Issues](dashboard/known-issues/README.md)
  * [Power BI Load Errors](dashboard/known-issues/power-bi-load-errors.md)
* [Performance](dashboard/performance.md)

## Design Decision

* [Relations](design-decision/relations.md)
* [Trend Tables](design-decision/trend-tables.md)
* [Data Types](design-decision/data-types/README.md)
  * [Real Type](design-decision/data-types/real-type.md)
* [Primary Keys](design-decision/primary-keys.md)
* [Data Compression](design-decision/data-compression.md)
* [Configuration Items](design-decision/configuration-items.md)

## Reference

* [Data-Tier Application Package](reference/data-tier-application-package.md)

## Hot Fixes <a id="fixes"></a>

## FAQ

* [How do I check if SQLWATCH is running OK?](faq/how-do-i-check-if-sqlwatch-is-running-all-ok.md)
* [I am not seeing any data in Power BI](faq/i-am-not-seeing-any-data-in-power-bi.md)
* [Can I modify default checks?](faq/can-i-modify-default-checks.md)

