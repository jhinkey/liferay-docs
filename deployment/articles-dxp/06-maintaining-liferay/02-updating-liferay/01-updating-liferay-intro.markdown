---
header-id: patching-liferay
---

# Patching @product@

[TOC levels=1-4]

While we strive for perfection with every @product@ release, the reality of the
human condition dictates that releases may not be as perfect as originally
intended. But we've planned for that. Included with every @product@ bundle is a
Patching Tool that handles installing two types of patches: fix packs and
hotfixes. 

| **Important:** Make sure to
| [back up your @product@ installation and database](/docs/7-2/deploy/-/knowledge_base/d/backing-up-a-liferay-installation)
| regularly, especially before patching. Certain fix packs (service packs) can 
| include data/schema changes (micro data upgrades)---they're optional and 
| revertible. 
|
| If you want to apply micro data upgrades before starting the server, use the
| [upgrade tool](/docs/7-2/deploy/-/knowledge_base/d/configuring-the-data-upgrade)
| for Core micro data upgrades and
| [Gogo shell](/docs/7-2/deploy/-/knowledge_base/d/upgrading-modules-using-gogo-shell)
| for module micro data upgrades. 
|
| If you apply micro data upgrades before restarting your server or you don't 
| want micro data upgrades running automatically on server startup, create a
| [system configuration file](/docs/7-2/user/-/knowledge_base/u/understanding-system-configuration-files)
| called
| `com.liferay.portal.upgrade.internal.configuration.ReleaseManagerConfiguration.config`,
| set property `autoUpgrade="false"` in the file, and copy the file into the
| `[Liferay Home]/osgi/configs` folder. You can skip applying micro data 
| upgrades altogether or apply them whenever you want using the upgrade tool and
| Gogo shell. 

| **Note:** [Patching a cluster](/docs/7-2/deploy/-/knowledge_base/d/updating-a-cluster)
| requires additional considerations.
