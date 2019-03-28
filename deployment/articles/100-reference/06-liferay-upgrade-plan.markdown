# Liferay Upgrade Plan 

Here are the steps for upgrading Liferay and your custom plugins to @product-ver@. Note, you can upgrade Liferay (steps I and II) and your custom plugins (step III) simultaneously. 

| **Important:** Before executing the upgrade plan, read about upgrading a 
| cluster or upgrading a sharded environment, if that's your situation. 

## Upgrade Steps

<ol type="I">
  <li>If you're on Liferay Portal 6.0.x, <a href="/docs/6-2/deploy/-/knowledge_base/deploy/upgrading-liferay">upgrade to Liferay Portal 6.2</a>. If you're on Liferay Portal 6.1.x, <a href="/docs/7-1/deploy/-/knowledge_base/deploy/upgrading-to-liferay-71">upgrade to @product@ 7.1.</a></li>
  <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/upgrading-to-product-ver">Upgrade your @product@ database and configuration.</a>Note, Preparing a new @product@ production server can be done in parallel with steps <em>A. through C.</em></li>
  <ol type="A">
    <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/planning-for-deprecated-applications">Examine the deprecated applications: Remove unwanted applications from production and note ones to modify after upgrading to @product-ver@.</a></li>
    <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/test-upgrading-a-product-backup-copy">Test upgrading a database copy.</a></li>
    <ol type="1">
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/test-upgrading-a-product-backup-copy#copy-the-production-installation-to-a-test server">Copy the Production Installation to a Test Server.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/test-upgrading-a-product-backup-copy#Copy-the-Production-Backup-to-the-Test-Database">Copy the Production Backup to the Test Database and Save the Logs.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/test-upgrading-a-product-backup-copy#remove-duplicate-web-content-structure-field-names">Remove Duplicate Web Content Structure Field Names.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/test-upgrading-a-product-backup-copy#Find-and-Remove-Unused-Objects">Find and Remove Unused Objects.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/test-upgrading-a-product-backup-copy#Test-product-with-its-Pruned-Database-Copy">Test @product@ with its Pruned Database Copy.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/test-upgrading-a-product-backup-copy#Install-@product-ver@-on-a-Test-Server-and-Configure-it-to-Use-the-Pruned-Database">Install @product-ver@ on a Test Server and Configure it to Use the Pruned Database.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/test-upgrading-a-product-backup-copy#Tune-Your-Database-for-the-Upgrade">Tune Your Database for the Upgrade.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/upgrading-the-product-data">Upgrade the database to @product-ver@ (see step <em>E. Upgrade the @product@ data</em>); then return here.</a></li>
      <li>If the upgrade took too long, search the upgrade log to identify more unused objects. Then restart these steps with a fresh copy of the production database.</li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/test-upgrading-a-product-backup-copy#Test-the-Upgraded-Portal-and-Resolve-Any-Issues">Test the Upgraded Portal and Resolve Any Issues.</a></li>
      <li>Checkpoint: Noted all unused objects and how to remove them</li>
    </ol>
    <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/preparing-to-upgrade-the-product-database">Prepare to upgrade the production database.</a></li>
    <ol type="1">
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/BAR">Remove all noted unused objects.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/BAR">Test @product@ with its pruned database.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/BAR">Upgrade your Marketplace apps.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/BAR">Publish all staged changes to production.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/BAR">Synchronize a complete @product@ backup, including your pruned production database.</a></li>
      <li>Checkpoint: Ready to upgrade the production database</li>
    </ol>
    <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/preparing-a-new-product-server-for-data-upgrade">Prepare a new @product@ server for data upgrade.</a></li>
    <ol type="1">
      <li><a href="/FOO/BAR">Install @product-ver@.</a></li>
      <li><a href="/FOO/BAR">Install the latest fix pack. (DXP only)</a></li>
      <li><a href="/FOO/BAR">Migrate your OSGi configurations. (@product@ 7.0+)</a></li>
      <li><a href="/FOO/BAR">Migrate your portal properties.</a></li>
      <ol type="a">
        <li><a href="/FOO/BAR">Update your portal properties.</a></li>
        <li><a href="/FOO/BAR">Convert applicable properties to OSGi configurations.</a></li>
      </ol>
      <li><a href="/FOO/BAR">Configure your Documents and Media file store.</a></li>
      <li><a href="/FOO/BAR">Disable indexing.</a></li>
      <li>Checkpoint: Prepared the new @product@ production server</li>
    </ol>
    <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/upgrading-the-product-data">Upgrade the @product@ data.</a></li>
    <ol type="1">
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/tuning-your-database-for-the-upgrade">Tune your database for the upgrade.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/configuring-the-data-upgrade">Configure the data upgrade.</a></li>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/upgrading-the-core-using-the-upgrade-tool">Upgrade the core.</a></li>
      <ol type="a">
        <li><a href="/FOO/BAR">Run the data upgrade tool.</a></li>
        <li><a href="/FOO/BAR">Resolve any core upgrade issues.</a></li>
        <li><a href="/FOO/BAR">If the issues were with upgrades to @product@ 7.0 or lower, restore the pruned production database backup.</a></li>
        <li><a href="/FOO/BAR">Upgrade your resolved issues (step <em>a</em>); continue if there were no issues.</a></li>
      </ol>
      <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/upgrading-modules-using-gogo-shell">Upgrade the @product@ modules, if you didn't upgrade them automatically with the core.</a></li>
      <ol type="a">
        <li><a href="/FOO/BAR">Upgrade modules that are ready for upgrade.</a></li>
        <li><a href="/FOO/BAR">Verify upgraded modules.</a></li>
        <li><a href="/FOO/BAR">Resolve any module upgrade issues.</a></li>
        <li><a href="/FOO/BAR">Upgrade your resolved module issues (step <em>a</em>); continue if there were no issues.</a></li>
      </ol>
      <li>Checkpoint: Completed upgrading the database</li>
    </ol>
    <li><a href="/docs/7-2/deploy/-/knowledge_base/deploy/executing-post-upgrade-tasks">Execute post-upgrade Tasks.</a></li>
    <ol type="1">
      <li><a href="/FOO/BAR">Remove the database tunning made for the upgrade process.</a></li>
      <li><a href="/FOO/BAR">Re-enable and re-index the search indexes.</a></li>
      <li><a href="/FOO/BAR">Update web content permissions. (@product@ 7.0 and lower)</a></li>
      <li><a href="/FOO/BAR">Address deprecated apps.</a></li>
      <li>Checkpoint: Completed post-upgrade tasks</li>
    </ol>
  </ol>
  <li>Upgrade your custom plugins to @product-ver@</li>
  <ol type="A">
      <ol type="1">
      </ol>
      <li>Hooks/Overrides/Extensions</li>
      <ol type="1">
          <li>Override/extension (module)</li>
          <li>Liferay core JSP hook (WAR)</li>
          <li>Liferay portlet JSP hook (WAR)</li>
          <li>Service wrapper hook (WAR)</li>
          <li>Language key hook (WAR)</li>
          <li>Model listener hook (WAR)</li>
          <li>Event actions hook (WAR)</li>
          <li>Servlet filter hook (WAR)</li>
          <li>Portal properties hook (WAR)</li>
          <li>Struts action hook (WAR)</li>
      </ol>
      <li>Themes</li>
      <li>Layout Templates</li>
      <li>Framework/feature upgrades</li>
      <ol type="1">
          <li>Using JNDI data source</li>
          <li>Service Builder service invocation</li>
          <li>Service Builder</li>
          <li>Velociy templates (deprecated)</li>
      </ol>
      <li>Portlets</li>
      <ol type="1">
          <li>JSF Portlet</li>
          <li>Spring Portlet MVC</li>
          <li>Liferay MVC Portlet</li>
          <li>GenericPortlet</li>
          <li>Servlet-based Portlet</li>
          <li>Struts 1 Portlet</li>
      </ol>
      <li>Web plugins</li>
      <li>Ext</li>
  </ol>
</ol>
 
## Related Topics

[Upgrading to @product-ver@](/deployment/deployment/-/knowledge_base/7-2/upgrading-to-liferay-72)

[Upgrading a Sharded Environment](/deployment/deployment/-/knowledge_base/7-2/upgrading-sharded-environment)

[Updating a Cluster](/deployment/deployment/-/knowledge_base/7-2/updating-a-cluster)

[From Liferay 6 to 7](/develop/tutorials/-/knowledge_base/7-2/from-liferay-6-to-liferay-7)

[From @product@ 7.x to 7.2](/develop/tutorials/-/knowledge_base/7-2/from-liferay-7-1-to-7-2)

[Implementing Application Data Upgrades](/develop/tutorials/-/knowledge_base/7-2/data-upgrades)
