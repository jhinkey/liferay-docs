---
header-id: patching-liferay
---

# Updating @product@

[TOC levels=1-4]

While we strive for perfection with every @product@ release, the reality of the
human condition dictates that releases may not be as perfect as originally
intended. That's why Liferay provides updates in GA releases for @product-ver@
following GA1. 

Before applying an update GA release, examine the release notes to determine if
there are data upgrade processes you want to run. An update GA's data upgrades
(micro data upgrades) are optional and revertible. GA *code updates* work fine
without the micro data upgrades. The steps below describe the micro data upgrade
options. 

| **Note:**
| [Updating a cluster](/docs/7-2/deploy/-/knowledge_base/d/updating-a-cluster)
| requires additional considerations.

Here's how to apply an update GA release:

1.  [Back up your @product@ installation](/docs/7-2/deploy/-/knowledge_base/d/backing-up-a-liferay-installation). 

2.  [Download](/docs/7-2/deploy/-/knowledge_base/d/obtaining-product)
    the new GA Liferay WAR file (and supporting libraries) or a @product@
    installation bundle for your application server.  

3.  [Install the new GA Liferay WAR and supporting files on your application server](/docs/7-2/deploy/-/knowledge_base/d/deploying-product)
    or install the @product@ bundle for your application server.  

4.  Copy your
    [OSGi configuration files](/docs/7-2/user/-/knowledge_base/u/understanding-system-configuration-files)
    (i.e., `.config` files), including your documents and media file store
    configurations, to your new server's `[Liferay Home]/osgi/configs`
    folder. 

5.  Migrate your portal properties files to your new server. 

6.  If you want to apply micro data upgrades before starting the server, use the
    [upgrade tool](/docs/7-2/deploy/-/knowledge_base/d/configuring-the-data-upgrade)
    for Core micro data upgrades and
    [Gogo shell](/docs/7-2/deploy/-/knowledge_base/d/upgrading-modules-using-gogo-shell)
    for module micro data upgrades. 

6.  If you applied the micro data upgrades already or you don't want micro data 
    upgrades running automatically on server startup, create a
    [system configuration file](/docs/7-2/user/-/knowledge_base/u/understanding-system-configuration-files)
    called
    `com.liferay.portal.upgrade.internal.configuration.ReleaseManagerConfiguration.config`,
    set property `autoUpgrade="false"` in the file, and copy the file into the
    `[Liferay Home]/osgi/configs` folder. 

7.  Start your updated server. 

| **Remember:** If you haven't applied the GA update's micro data upgrades 
| already, you can use the
| [upgrade tool](/docs/7-2/deploy/-/knowledge_base/d/configuring-the-data-upgrade)
| for Core micro data upgrades and
| [Gogo shell](/docs/7-2/deploy/-/knowledge_base/d/upgrading-modules-using-gogo-shell)
| for module micro data upgrades. 

Congratulations! You're running on the latest @product-ver@ GA release. 
