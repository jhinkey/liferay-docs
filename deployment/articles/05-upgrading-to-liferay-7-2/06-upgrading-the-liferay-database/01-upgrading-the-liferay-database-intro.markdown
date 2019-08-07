---
header-id: upgrading-the-product-data
---

# Upgrading the @product@ Data

[TOC levels=1-4]

Now you're ready to upgrade the @product@ data. The upgrade processes update the
database schema for the core and your installed modules. Verification processes
test the upgrade. Configured verifications for the core and modules run
afterwards, but can be run manually too. 

Here are the ways to upgrade:

-   **Upgrade everything in one shot**:
    Use the upgrade tool to upgrade the core and all the modules. 

-   **Upgrade the core and the modules separately**:
    Use the upgrade tool (recommended) or
    [Gogo shell](/docs/7-2/deploy/-/knowledge_base/d/upgrading-modules-using-gogo-shell) to upgrade the core. Then use Gogo shell to upgrade each module. 

If you are upgrading from Liferay Portal 6.2 or earlier, use the upgrade tool to
upgrade everything. It's the easiest, most comprehensive way to upgrade from
those versions. Since version 7.0, however, @product@'s modular framework lets
you upgrade modules---even the core---individually. A helpful practice for large
databases is to focus first on upgrading the core and your most important
modules; then back up your database before continuing upgrades. Upgrading is
a flexible process that adjusts to your preferences.

| **Note:** Since Liferay DXP 7.1 and since Liferay Portal CE 7.2, data 
| upgrades within a minor version (e.g., DXP 7.2 fix packs and and Portal CE 7.2
| GA releases) are optional. These micro version data schema changes are
| compatible with data throughout a Liferay DXP or Liferay Portal  CE minor
| version (e.g., within 7.2).
| 
| For example, you can install and run with the latest Liferay DXP 7.2 fix packs
| without running the data upgrade tool. You can execute micro  version  data
| schema changes when you want. 
| 
| To refrain from upgrading data on server startup, set
| [`autoUpgrade`](/docs/7-2/deploy/-/knowledge_base/d/configuring-the-data-upgrade)
| to `false` (the default is `true`). 
