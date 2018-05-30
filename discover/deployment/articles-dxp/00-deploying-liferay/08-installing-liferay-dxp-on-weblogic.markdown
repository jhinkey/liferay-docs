# Installing @product@ on WebLogic 

Although it's possible to install @product@ in a WebLogic Admin Server, this
isn't recommended. It's best practice to install web apps, including @product@,
to a WebLogic Managed server. Deploying to a Managed Server lets you
start/shutdown @product@ more quickly and facilitates transitioning @product@
into a cluster configuration. This article therefore focuses on installing
@product@ in a Managed Server. 

Before getting started, you should take care of a few things. First, it's 
assumed that your Admin and Managed Servers already exist. See 
[WebLogic's documentation](http://www.oracle.com/technetwork/middleware/weblogic/documentation/index.html) 
for instructions on setting up and configuring Admin and Managed Servers. 

You should also read the following articles to familiarize yourself with
@product@'s general installation steps: 

- [Preparing for Install](/discover/deployment/-/knowledge_base/7-1/preparing-for-install)
- [Installing @product@ Manually](/discover/deployment/-/knowledge_base/7-1/installing-liferay-manually)

And lastly, download these files from the
[Customer Portal](https://web.liferay.com/group/customer/dxp/downloads/digital-enterprise):

- @product@ WAR file
- Dependencies ZIP file
- OSGi JARs ZIP file

Here are the basic steps for installing @product@ on WebLogic:

- [Install @product@ dependencies](#installing-dxp-dependencies)
- [Configure WebLogic for @product@](#weblogic-configuration)
- [Deploy @product@](#deploying-liferay-dxp)

[*Liferay Home*](/discover/deployment/-/knowledge_base/7-1/installing-product#liferay-home)
is a folder for @product@'s `data`, `deploy`, `license`, and `osgi` folders. In
WebLogic, Liferay Home is typically your domain's folder, but you can use any
local folder. 

## Installing @product@ Dependencies [](id=installing-dxp-dependencies)

@product@ depends on JARs from the @product@ dependencies ZIP and OSGi JAR ZIP
files you downloaded. There are also over a dozen other JARs (some are strictly
required) that you should install. 

1.  Extract the following JARs from the dependencies ZIP file to your domain's
    `lib` folder: 
    
    - `com.liferay.petra.concurrent.jar`
    - `com.liferay.petra.executor.jar`
    - `com.liferay.petra.function.jar`
    - `com.liferay.petra.io.jar`
    - `com.liferay.petra.lang.jar`
    - `com.liferay.petra.memory.jar`
    - `com.liferay.petra.nio.jar`
    - `com.liferay.petra.process.jar`
    - `com.liferay.petra.reflect.jar`
    - `com.liferay.petra.string.jar`
    - `com.liferay.registry.api.jar`
    - `hsql.jar`
    - `portal-kernel.jar`
    - `portlet.jar`

2.  Create an `osgi` folder in your Liferay Home. Then extract the folders
    (i.e., `configs`, `core`, and more) from OSGi JARs ZIP file to the `osgi`
    folder. These folders contain the OSGi runtime, required module JARs, and
    configuration files. 

3.  Copy the JDBC driver for your database to your domain's `lib` folder. Don't 
    use HSQL in production. Here are some common JDBC drivers:
    
    - `mariadb.jar` (if needed) - [https://downloads.mariadb.org/](https://downloads.mariadb.org/)
    - `mysql.jar` (if needed) - [http://dev.mysql.com/downloads/connector/j](http://dev.mysql.com/downloads/connector/j)
    - `postgresql.jar` (if needed) - [https://jdbc.postgresql.org/download/postgresql-42.0.0.jar](https://jdbc.postgresql.org/download/postgresql-42.0.0.jar)


Checkpoint:

1.  Your domain's `lib` folder has these JARs:

    - `com.liferay.petra.concurrent.jar`
    - `com.liferay.petra.executor.jar`
    - `com.liferay.petra.function.jar`
    - `com.liferay.petra.io.jar`
    - `com.liferay.petra.lang.jar`
    - `com.liferay.petra.memory.jar`
    - `com.liferay.petra.nio.jar`
    - `com.liferay.petra.process.jar`
    - `com.liferay.petra.reflect.jar`
    - `com.liferay.petra.string.jar`
    - `com.liferay.registry.api.jar`
    - `hsql.jar`
    - `portal-kernel.jar`
    - `portlet.jar`
    - `[your JDBC driver].jar`

2. Your `[Liferay Home]/osgi` folder has these subfolders:

    - `configs`
    - `core`
    - `marketplace`
    - `modules`
    - `portal`
    - `static`
    - `test`
    - `war`

## Configuring WebLogic [](id=weblogic-configuration)

Configuring WebLogic to run @product@ involves these things:

- [Configuring the environment](#configuring-the-environment)
- [Configuring WebLogic's Node Manager](#configuring-weblogics-node-manager)
- [Setting Portal properties](#setting-portal-properties)
- [Data source configuration](#database-configuration) (optional)
- [Mail session configuration](#mail-configuration) (optional)

Start with configuring the environment. 

### Configuring the Environment [](id=configuring-the-environment)

1.  When you configure your domain, make sure to set your `JAVA_HOME` to a 
    @product@-supported JRE. 

2.  Set UTF8 file encoding in your domain's `setDomainEnv.sh` file by
    replacing the following line.

    Old: 

    `JAVA_PROPERTIES="${JAVA_PROPERTIES} ${CLUSTER_PROPERTIES}"`

    New:

    `JAVA_PROPERTIES="-Dfile.encoding=utf8 ${JAVA_PROPERTIES} ${CLUSTER_PROPERTIES}"`

3.  Set variables in these two WebLogic startup scripts:

    - `your-domain/startWebLogic.sh`: This is the Admin Server's startup 
       script. 

    - `your-domain/bin/startWebLogic.sh`: This is the startup script for 
       Managed Servers. 

    Add the following variables to both `startWebLogic.sh` scripts:

        export DERBY_FLAG="false"
        export JAVA_OPTIONS="${JAVA_OPTIONS} -Dfile.encoding=UTF-8 -Djava.net.preferIPv4Stack=true -Duser.timezone=GMT -da:org.apache.lucene... -da:org.aspectj..."
        export MW_HOME="/your/weblogic/directory"
        export USER_MEM_ARGS="-Xmx1024m -XX:MetaspaceSize=512m"

    The `DERBY_FLAG` setting disables the Derby server built into
    WebLogic---@product@ doesn't require Derby server. The remaining settings
    support @product@'s memory requirements, UTF-8 requirement, Lucene usage,
    and Aspect Oriented  Programming via AspectJ. Also make sure to set
    `MW_HOME` to the folder containing your WebLogic server. For example: 

        export MW_HOME="/Users/ray/Oracle/wls12210"

4.  The Node Manager must start the Managed Server using @product@'s memory
    requirements. In the Admin Server's console UI, 
    navigate to the Managed Server that's deploying @product@ and select the 
    *Server Start* tab. Enter the following values into the *Arguments* field: 

        -Xmx2048m -XX:MaxMetaspaceSize=512m

    Click *Save* when you're finished. 

### Configuring WebLogic's Node Manager [](id=configuring-weblogics-node-manager)

WebLogic requires a Node Manager to start and stop managed servers. Before 
installing @product@, you must configure the Node Manager included with your 
WebLogic installation. You'll do this via the 
`domains/your_domain/nodemanager/nodemanager.properties` file. Open this 
file, and set the `SecureListener` property to `false`: 

    SecureListener=false

This setting disables the encryption (SSL) requirement for the Node Manager, 
allowing it to accept unencrypted connections. Although it's possible to run 
@product@ with this property set to `true`, you may encounter difficulties doing 
so. Also note that with `SecureListener` set to `true`, you must configure your 
machine in the Admin Server's console to accept unencrypted connections from the 
Node Manager. To do this, first log in to your Admin Server and select 
*Environment* &rarr; *Machines* from the *Domain Structure* box on the left. 
Click your machine in the table and then select the *Configuration* &rarr; *Node 
Manager* tab. In the *Type* field, select *Plain* from the selector menu, and 
then click *Save*. You must restart your Admin Server for this change to take 
effect. 

If you're running WebLogic on Mac or Linux, you may also need to set the 
`NativeVersionEnabled` property to `false`: 

    NativeVersionEnabled=false

This tells the Node Manager to start in non-native mode. This is required for 
the platforms where WebLogic doesn't provide native Node Manager libraries. 

### Setting Portal Properties [](id=setting-portal-properties)

Before installing @product@, you must set the 
[*Liferay Home*](/discover/deployment/-/knowledge_base/7-0/installing-liferay-portal#liferay-home)
folder's location via the `liferay.home` property in a `portal-ext.properties` 
file.

    liferay.home=/full/path/to/your/liferay/home/folder
    
Remember to change this file path to the location on your machine that you want 
to serve as Liferay Home. 

You can also use this file to override 
[other @product@ properties](@platform-ref@/7.0-latest/propertiesdoc/portal.properties.html) 
that you may need. 

Now that you've created your `portal-ext.properties` file, you must put it 
inside the @product@ WAR file. Expand the @product@ WAR file and place 
`portal-ext.properties` in the `WEB-INF/classes` folder. Later, you can deploy 
the expanded archive to WebLogic. Alternatively, you can re-WAR the expanded 
archive for later deployment. In either case, @product@ reads your property settings 
once it starts up. 

If you need to make any changes to `portal-ext.properties` after @product@ 
deploys, you can find it in your domain's `autodeploy/ROOT/WEB-INF/classes` 
folder. Note that the `autodeploy/ROOT` folder contains the @product@ 
deployment. 

Next, you'll configure your database. 

### Database Configuration [](id=database-configuration)

Use the following procedure if you want WebLogic to manage your database for 
@product@. You can skip this section if you want to use @product@'s built-in 
Hypersonic database. 

1. Log in to your AdminServer console.

2. In the *Domain Structure* tree, find your domain and navigate to 
   *Services* &rarr; *Data Sources*.

3. To create a new data source, click *New* and the data source type. Fill in 
   the *Name* field with  `Liferay Data Source` and the *JNDI Name* field with
   `jdbc/LiferayPool`.  Select the database type. Click *Next* to continue.

4. Select the database driver. Click *Next* to continue.

5. Accept the default settings on this page and click *Next* to move on. 

6. Fill in the database information for your MySQL database. 

7. Add the text 
   `?useUnicode=true&characterEncoding=UTF-8&\useFastDateParsing=false` to the 
   URL line and test the connection. If it works, click *Next*. 

8. Select the target for the data source and click *Finish*. 

9. You must now tell @product@ about the JDBC data source. Create a 
   `portal-ext.propreties` file in your Liferay Home directory, and add the line 
   `jdbc.default.jndi.name=jdbc/LiferayPool`. 

Next, you'll configure your mail session. 

### Mail Configuration [](id=mail-configuration)

If you want WebLogic to manage your mail session, use the following procedure. 
If you want to use Liferay's built-in mail session (recommended), you can skip 
this section. 

1. Start WebLogic and log in to your Admin Server's console.

2. Select *Services* &rarr; *Mail Sessions* from the *Domain Structure* box on 
   the left hand side of your Admin Server's console UI. 

3. Click *New* to begin creating a new mail session. 

4. Name the session *LiferayMail* and give it the JNDI name `mail/MailSession`. 
   Then fill out the *Session Username*, *Session Password*, *Confirm Session 
   Password*, and *JavaMail Properties* fields as necessary for your mail 
   server. See the 
   [WebLogic documentation](http://docs.oracle.com/middleware/1221/wls/FMWCH/pagehelp/Mailcreatemailsessiontitle.html) 
   for more information on these fields. Click *Next* when you're done. 

5. Choose the Managed Server that you'll install @product@ on, and click 
   *Finish*. Then shut down your Managed and Admin Servers. 

6. With your Managed and Admin servers shutdown, add the following property to 
   your `portal-ext.properties` file: 

        mail.session.jndi.name=mail/MailSession

    @product@ references your WebLogic mail session via this property setting. 
    If you've already deployed @product@, you can find your 
    `portal-ext.properties` file in your domain's 
    `autodeploy/ROOT/WEB-INF/classes` folder. 

Your changes will take effect upon restarting your Managed and Admin servers.  

## Deploying @product@ [](id=deploying-liferay-dxp)

As mentioned earlier, although you can deploy @product@ to a WebLogic Admin 
Server, you should instead deploy it to a WebLogic Managed Server. Dedicating 
the Admin Server to managing other servers that run your apps is a best 
practice. 

Follow these steps to deploy @product@ to a Managed Server: 

1. Make sure the Managed Server you want to deploy @product@ to is shut down. 

2. In your Admin Server's console UI, select *Deployments* from the *Domain 
   Structure* box on the left hand side. Then click *Install* to start a new 
   deployment. 

3. Select the @product@ WAR file or its expanded contents on your file system. 
   Alternatively, you can upload the WAR file by clicking the *Upload your 
   file(s)* link. Click *Next*. 

4. Select *Install this deployment as an application* and click *Next*.

5. Select the Managed Server you want to deploy @product@ to, and click *Next*. 

6. If the default name is appropriate for your installation, keep it. 
   Otherwise, give it a name of your choosing and click *Next*. 

7. Click *Finish*. After the deployment finishes, click *Save* if you want to 
   save the configuration.  

8. Start the Managed Server you deployed @product@ to. @product@ precompiles all
   the JSPs, and then launches. 

Nice work! Now you're running @product@ on WebLogic. 
