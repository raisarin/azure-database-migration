# Azure Database Migration
Implementation of a cloud-based database system using the services from Micosoft Azure.
<details>
<summary><h1> Table of Content</h1></summary>
+ dkjfskd
__dlfjsdlkfj
</details>

## Description 
Micosoft Azure provides plentiful and simple to use features. Virtual machine (VM) can be used to establish a production environment, the properties of the VM configured to meet the specification needs of the user. In the VM, application from Micosoft faciliate the migration, backups and restoration of on-premise SQL database. There are simulations that user can perform to verify the integrity and recovery features of on-presmise and cloud database. This project aims to produce a cloud-base database and test the core features provided.

## Azure Project Diagram 
![image](./Images/Azure%20Project%20Diagram.png)
This UML Diagram provides a visual aid for understanding the flowchart of the project as there will multiple interdependent serivces. 
## Milestone 
### Azure Account Setup/Login
Sign up or log into your Azure Account using [Azure Portal](https://portal.azure.com/ "https://portal.azure.com/")

### Milestone 2: Setup production environment
> [!NOTE]
> The following set up is only for Windows 10 environment only and leave options as default if not mentioned.

#### Windows Virtual Machine setup 
##### Virtual machine dashboard
* In the search menu type and select **Virtual Machines**.
* Use create drop menu and choose **Azure virtual machine**. 

##### Create virtual machine 
###### Project 

* Select appropriate **Subscription**.
* Create and name new **Resource Group**. 
###### Instance details
* Add appropriate **Virtual Name**. 
* Select **Region** geopraphically close to user location.
* Select **Image** as **Windows 11 Pro** for this project. 
* Choose **Size** as **B2ms** Standard or General Purpose. 
  * If not found in the drop down menu, click **See all sizes** and find in **B-Series**.
###### Administrator account
* Add **Username** and secure **Password**.
###### Inbound port rules
* In **Public inbound ports** select **Allow selected ports**. This allows select inbound ports to be chosen. 
* For **Select inbound ports** check the option **RDP (3389)**. 
###### Licensing 
* Check the box to confirm eligibility for windows 10/11 license with multi-tenant hosting rights.
##### Finalising virtual machine 
* Select **Review + Create** to initialise validation. 
* Select **Create** button after validation has passed. 
* A new page will appear once the deployment of the virtual machine is complete.

#### Connecting to Windows Virtual Machine
###### Connection set up in Azure portal
* In the search menu type and select **Virtual Machines**.
* Select the name of **Virtual Machine** that has been created.
* Press **Start** if the virtual machine has not been initialised.
* Use the connect drop down menu to select **Connect**.
* **Download RDP file** into local desktop.
###### Connection in Windows desktop
* Search for **Remote Desktop Connection** in Start menu of the local desktop.
* Drag and drop **.rdp** file into the Remote Desktop Connection application. 
* Input the **credentials** of the virtual machine to gain access.
#### SQL Server & SQL Server Management Studio (SSMS) installation in Virtual Machine
##### Installation process
* Use previous method to **connect** to Virtual Machine. 
* Download **SQL Server Installer** from [Microsoft Download Centre](https://go.microsoft.com/fwlink/p/?linkid=2215158&clcid=0x809&culture=en-gb&country=gb "https://go.microsoft.com/fwlink/p/?linkid=2215158&clcid=0x809&culture=en-gb&country=gb").
* Locate and run the **SQL Server installer**.
* Select **Basic** installation type.
* Accept the **License Terms**.
* Choose appropriate **install location**.
* **Select install** to start the installation. 
* **Download SSMS** using prompt shown in the installer.  
* Use the **on-screen instructions** to install SSMS.
##### Connecting SQL Server and SSMS
* Start the **SSMS application**. 
* Enter the **credentials** following the steps below.
    * Server type: **Database Engine**
    * Server name: "Name of virtual machine" or **Localhost**
    * Authentication: **Windows Authentication**
* Press **Connect** to add the database to the Object Explorer.  
#### Create production database 
* Download Micorsoft SQL Server database backup file called [AdventureWorks](https://aicore-portal-public-prod-307050600709.s3.eu-west-1.amazonaws.com/project-files/93dd5a0c-212d-48eb-ad51-df521a9b4e9c/AdventureWorks2022.bak "https://aicore-portal-public-prod-307050600709.s3.eu-west-1.amazonaws.com/project-files/93dd5a0c-212d-48eb-ad51-df521a9b4e9c/AdventureWorks2022.bak").
* Copy the backup file to file location `C:\Program Files\Microsoft SQL Server\MSSQL16.MSSQLSERVER\MSSQL\Backup`. 
* Right click on **Databases**. 
* Choose **Restore Database**.
* In Restore Database window, **select Device** then **click ...** for more options 
* In Select backup devices window, **find and select backup file** in the previously saved file location.
* **Press OK** to initilise the restore process, press OK again when prompted.
### Milestone 3: Migrate to Azure SQL Database
#### Azure SQL Database set up
##### SQL databases dashboard
* Log in to your **Microsoft Azure Portal**. 
* In the search menu type and select **SQL databases**.
* Select **Create** a new database. 
##### Create SQL Database 
###### Project details 
* Select appropriate **Subscription**.
* Create and name new **Resource Group**. 
###### Database details 
* Add appropriate **Database Name**. 
* Click **Create new** Server.
###### Server detials 
* Enter a unique **Server name**. 
* Select **Location** geopraphically close to user location.
###### Authentication 
* For Authenticatioan method **Use SQL authentication**. 
* Add **Server admin login** and secure **Password**.
* Press **OK** to create SQL Database Server.
###### Compute + Storage 
* Select **Configure database**.
* In Service tier, select **Basic (For less demanding workloads)**.
* Press **Apply** to save service configuration.
* Click **Review + create** to create the database.
#### Azure Data Studio installation 
* Nagivate to [Azure Data Studio website](https://docs.microsoft.com/en-us/sql/azure-data-studio/download-azure-data-studio "https://docs.microsoft.com/en-us/sql/azure-data-studio/download-azure-data-studio").
* Find and download **Azure Data Studio user installer for Windows**.
* Install Azure Data Studio using the on-screen instructions. 
##### Azure Data Studio connection to local SQL server Database
* Launch the **Azure Data Studio** application 
* On the left taskbar, select **Connections** and then **New Connections**
###### Connection Details of Local SQL server Database 
* Connection type: Microsoft SQL Server 
* Input type: Parameters 
* Server: **localhost** or name of local SQL server database
* Authentication type: Windows Authentication 
* Database: \<Default\> or AdventureWorks2022
    * Enable Trust server certificate when prompted
* Encrypt: Mandatory (True)
* Trust server certificate: True
Server group: \<Default\>
* Name (optional): Name of database or Leave blank
* Click **Connect**
##### Azure Data Studio connection to Azure SQL Database
* Launch the **Azure Data Studio** application.
* On the left taskbar, select **Connections** and then **New Connections**.
###### Connection Details of Azure SQL Database
* Connection type: Microsoft SQL Server
* Input type: Parameters
* Server: "user-server-name".database.windows.net
    * Microsoft Azure > SQL databases > "User SQL database" > Overview
    * Copy the server name.
* Authentication type: SQL Login
* User name: Server admin login
* Password: Server admin password
* Database: "User SQL database"
* Encrypt: Mandatory (True)
* Trust server certificate: True
Server group: \<Default\>
* Name (optional): Name of database or Leave blank 
> [!NOTE] 
> **Edit Azure SQL Database Security before connecting**
> * Microsoft Azure > SQL databases > "User SQL database" > Overview > Click "User SQL database server" > Left sidebar Security/Networking
> * Enable **Selected Networks** to allow Virtual machine to connect to the server 

* Click **Connect**
##### SQL Server Migration
###### Schema Extension
* In Azure Studio Data Studio, find and click **Extensions** icon in the left sidebar.
* Search and install **SQL Server Schema Compare**.
* Click on Connection icon in the left sidebar. 
* Right click and choose **Schema Compare** on the **local database server**.
###### Schema Compare 
* Click on ... to open Source and Target prompt.
  * Source
    * Type: Database 
    * Server: localhost (default) or "name of user server"
    * Database: AdventureWorks2022
  * Target 
    * Type: Database 
    * Server: "user-server-name".database.windows.net (Azure SQL Database server)
    * Database: name of Azure SQL Database
* Click on **Compare button** on the top left to initialise comparison.   
* Click **Apply button** on the top middle to apply the difference from local database (virtual machine) to cloud database (Azure).
> [!Important] 
> This process only uploads the tables and structure of the database to the cloud **without the values or data**.
#### SQL Data Migration
##### Data Migration extension 
* In Azure Studio Data Studio, find and click **Extensions** icon in the left sidebar.
* Search and install **Azure SQL Migration**.
* Click on Connection icon in the left sidebar. 
* Right click and choose **Manage** on the **local database server**.
* In the new windows, under General click **Azure SQL Migration**.
* Click **Migrate to Azure SQL** 
##### Migrate "user database" to Azure SQL
* Step 1: Databases for assessment
  * Choose **AdventureWorks2022** Database. 
  * Click next.
* Step 2: Assessment summary and SKU recommendations
  * Click next after the assessment has finished.
* Step 3: Target platform & assessment results 
  * Select target type: Azure SQL Database. 
* Step 4: Azure SQL target 
  * Azure account: "User Azure account" 
    * Link user account and follow authentication process.
  > [!Note] 
  > The following details in the next step should be filled automatically ensure they are correct. 

  * Subscription: Choose relevant subcription of the database
  * Location: Location of the database 
  * Resource group: Group linked to database 
  * Azure SQL Database Server: Databse Server for the data migration 
  * Target user name: Login credentials of the server 
  * Target password: Login credentials of the server
  * Press **Connect** when details are correctly inputed.
    * If done correctly, a prompt will show "Connection was success ful. Target databases found: (Number of database in the server)"
  * Select the appropriate **Target database**
  * Click **Next**
* Step 5: Azure Database Migration Service
  * Under **Azure Database Migration Service**, click **Create new** 
    * Create Azure Database Migration Service
      * Resource group: Click **Create new** under Resource group and **add appropriate name**
      * Name: Add **Service Name**
  * Set up integration runtime 
    * Use the link provided to **download and install** the Mircosoft Integration Runtime Configuration Manager.
    * Run the applicaiton.
    * Copy and paste one of the Authentication key in the Register Integration Runtime. (Self-hosted) window 
    * Click **Register** button. 
      * "Self-hosted node is connected to the could service" will be shown in the window.
    * Click **Test connection** button on the bottom right to verify connection. 
    * Click **Done** button to return to previous window interface.
  * Connection status: Text box will show the connection of the service.
    * Press **Refresh** button to retry the connection. 
  * Press **Next** button. 
* Step 6: Data source configuration 
  * User name: "Virtual machine\User"
  * Password: "Virtual machine credentials"
  * Table selection: Check the source and target database are correct
    * Click the box under the select tables to edit number of tables.
    * Select the necessary number of tables
    * Press **Update** button the bottom right. 
  * Press **Run validation** button on the bottom left to test the connectivity. 
    * After the validation process has finish, press **Done**
  * Click on **Next** button. 
  * Press **Start migration** button. 
* In **Migrations tab**, a new row will show the migration services and status. 
* The migration status will show **Succeeded** when completed. 
#### Migration data validation
* Ensure that the data from the local database in the virtual matches the database in the Azure cloud database server.
  * Systemically check that tables name and values have been migrated. 
### Milestone 4: Data Backup and Restore
#### On-premise Database Backup 
##### Virtual Machine Backup 
* Launch the **SQL Server Mangement Studio application (SSMS)**.
* In Object Explorer, connect to **Localhost database server**. 
* Right click the local database.
* Path from **Tasks** to **Back Up...**. 
* Back Up database window will appear. 
  * Source: 
    * Database: AdventureWorks2022
    * Backup type: Full 
    * Backup component: Database 
  * Destination: 
    * Back up to: Disk
    * Path: C:\Program Files\Microsoft SQL Server\MSSQL16.MSSQLSERVER\MSSQL\Backup\
      * This is the default path for backup file in windows.
  * Press OK to execute backup
 * A new window will appear to show "T**he backup of database 'AdventureWorks2022' completed successfully.**"
##### User Local Machine Backup 
* In the virtual machine, use the file explorer application to **navigate to the Backup file**. 
  * Or copy paste the path way into the Windows Search bar to find the file folder 
* Right click and copy the file **"AdventureWorks2022.bak"**
* Minimise the virual machine using the "_" icon at the top to return to user local machine. 
* **Paste backup** file in a secure file location.
#### Blob Storage Backup
##### Storage accounts dashboard
* Log in to your **Microsoft Azure Portal**. 
* In the search menu type and select **storage accounts**.
###### Project details 
* Select appropriate **Subscription**.
* Create new **Resource Group**.
###### Instance details 
* Storage account name: "Relevant name"
* Region: Closest to user location
* Performance: Standard 
* Redundancy: Geo-redundant storage (GRS)
* Press review 
###### Review 
* Preview the details and scroll down 
* Click **Create** 
###### Upload backup to new container 
* **Navigate** Storage accounts > "Storage account name" > Overview > Upload 
* Upload blob 
  * **Copy and drag the backup file** from the backup folder in the virtual machine to the drop window 
  * Create new container
    * Name: Appropriate **name**
    * Anonymous access level: **Private (no anonymous access)**
    * Click **Ok**
  * **Upload** backup file to cloud.
###### Restore Database on Development Environment 
* Using the previous instructions create a new following environments: 
  * Virtual Machine: Sandbox environment for testing feature
  * In Sadbox virtual machine:
    * Download and install **SQL Server** and **SSMS**. 
* Restore database from Backup file: 
  * Login to user Azure portal, Storage account > Containers > "User container with backup file" 
  * Right click and download to Sandbox windows into the SSM backup folder.
  * Use the same process as before in **Create production database** to restore the database.
  * Check the tables and data have been restored properly. 
###### Development Environment Automated Backup
* Launch **SSMS** application. 
* In object Explorer, under Integration Services Catalogs, right click **SQL Server Agent (Agent XPs disbale)
* Click **start** and **Yes** to start service. 
* SQL Server Credential creation
  * **Right click the server** in Object Explorer 
  * Select **New Query**
  * Copy and paste the code block below 
  ``` 
  CREATE CREDENTIAL YourCredentialName
  WITH IDENTITY = 'Your Azure Storage Account Name',
  SECRET = 'Access Key';
  ```
  * **Replace the following details** using information from the Azure storage details 
    * Navigate to Azure portal > Storage accounts > "User storage account" > Security + networking > Access Keys
    * YourCredentialName: "Name of backup"
    * Your Azure Storage Account Name: "Copy and paste Storage account name"
    * Access key: "Copy and paste Key"
  * **Right Click then press Execute** on the code in SSMS
    * A prompt will show "Commands completed successfully."
    * In object Explorer > "User server" > Security > Credentials, the credential created will be present. 
* In Object Explorer then Management, **Right click Maintenance Plan**. 
* Select Maintence Plan Wizard.
  * Information page, press next.
  * Select Plan Properties
    * Name: "Name of Maintenance Plan"
    * Description: "Blank" 
    * Run as: SQL Server Agent service account 
    * Single schedule for the entire plan or no schedule 
    * Schedule: Press Change 
      * New job Schedule
        * Schedule type: Recurring 
        * Frequnecy Occurs: Weekly
        * Press OK 
    * Press **Next >**
  * Select Maintenance Tasks 
    * Select Back Up Database (Full)
    * Press **Next >**
  * Select Maintenance Task Order 
    * Select Back Up Database (Full)
    * Press **Next >**
  * Define Back Up Database (Full) Task 
    * General
      * Database(s): AdventureWorks2022 
      * Back up to: URL
    * Destination: 
      * SQL credential: "User created Credential" 
      * Azure storage container: "Container in the user storage account"
        * Azure portal > Storage accounts > "user storage account" > Data storage > Containers > "Container for backup" 
      * Press **Next >**
  * Select Report Options: 
    * Press **Next >**
  * Complete the Wizard 
    * Press **Finish**
  * Press Close when Status has updated to Success.
* Right click and click **refresh Maintenance Plans**
  * New a plan will appear.
* Right click "User plan" and select **Exectue**
### Milestone 5: Disaster Recovery Simulation 
#### Production Environment Data Loss Testing
* Follow instructions on [Azure Data Studio installation](#azure-data-studio-installation) to download and install Azure Data Studio.
* Follow instructions on [Azure Data Studio connection to Azure SQL Database](#azure-data-studio-connection-to-azure-sql-database) to connect to Azure SQL Database.
* In the Azure Data Studio, servers > Tables. 
* **Choose any table** to edit the values to micic data loss manually. 
* or Use the following method to alter tables. 
  * Right click **Server** and select **New Query** 
  * Use the following code to edit more data values. 
  ```
  -- Intentional Deletion
  DELETE TOP (100)
  FROM TABLE_NAME;

  -- Data Corruption
  UPDATE TOP (100) TABLE_NAME
  SET TABLE_COLUMN_NAME = NULL
  ```
  * Change **TABLE_NAME** and **TABLE_COLUM_NAME** to match your table.
* Right click and select **Select Top 1000** to observer the data loss.
* **Record** the loss of the data for verfication when performing recovery.
#### Azure SQL Database Backup Restoration 
* Navigate to Azure Portal > SQL databases > "SQL database"
* Select **Restore** icon. 
  * Create SQL Database - Restore database
    * Restore point (UTC): Choose time before the data loss testing 
    * Database name: "Choose appropriate name"
    * Click **Review + Create** then **Create**
* After the deployment is completed, in resources, a **new database is created**
* Following instructions on [Azure Data Studio connection to Azure SQL Database](#azure-data-studio-connection-to-azure-sql-database) again to connect to new restored Azure SQL Database.
* Check that the tables that the loss was performed have been recovered properly.
### Milestone 6: Geo Replication and Failover
#### Geo replciation Configuation 
* Navigate to Azure portal > SQL Database
* Select **Previously Restored database**
* Under Data management, Click **Replicas**
* Click **Create relica**
  * Create SQL Database - Geo Replica
    * Database details 
      * Server: Click **Create new**
        * Create SQL Database Server
          * Server name: **Unique server name**
          * Location: **Different from original server**
          * Authentication method: Use SQL authentication 
          * Server admin login: **New credentials**
          * Password: **New credentials**
          * Confirm password: **New credentials**
          * Press **Review + create**
        * Press **Create**

#### Failover and Failback Test
##### Failover group setup 
* Navigate to Azure portal > SQL server
* Select **Server with Restored database** 
* Under Data management, select **Failover groups**
* Click **Add Group**
  * Failover group
    * Failover group name: **New group name**
    * Server: **Select Secondary server**
##### Testing
* Newly added group will appear in the Failover groups
* Click on the **New Failover group**
  * New Failover group 
    * **Failover** 
      * Press **Failover icon**
      * Press **Yes** in the Warning
      * Observe the Roles of the Servers have swapped.
    * **Failback**
      * It is the same process as before
      * Press **Failover icon**
      * Press **Yes** in the Warning
      * Observe the Roles of the Servers are reverted to the original.
### Milestone 7: Microsoft Entra Directory Integration
#### Configuration of Microsoft Entra ID for Azure SQL Database
* Navigate to Azure portal > SQL server
* Click **Primary database server**
* Under Settings, click **Microsoft Entra ID**
* Click **Set Admin**
  * Microsoft Entra ID
    * In the search bar **look up for the User**
    * Check the User
    * Click **Select** button
* Click **Save**
* Under Microsoft Entra admin, the added admin details will appear 
#### Testing Microsoft Entra ID 
* In **Production virtual machine**, launch **Azure Data Studio**
* Add new connection
  * Connection type: Microsoft SQL Server
  * Input type: Parameters
  * Server: "user-primary-database-server".database.windows.net
      * Microsoft Azure > SQL databases > "User primary SQL database" > Overview
      * Copy the server name.
  * Authentication type: Microsoft Entra ID - Universal with MFA support
  * Account: **New added user account**
    * If user account not found, select add an account ..
    * Use the prompt in the browser to verify the account.
  * Database: "Restored SQL database"
  * Encrypt: Mandatory (True)
  * Trust server certificate: True
  Server group: \<Default\>
  * Name (optional): Name of database or Leave blank
* Verfiy the tables and data can be access.
#### DB Reader User
##### Creating User Access
* Navigate to Azure portal > Microsoft Entra ID
* Click add user > Create new user
  * Create new user
    * Basics
      * User principal name: "Name of the new user" @ "Choose appropriate email"
      * Mail nickname: Derive from user principal name
      * Display name: Name of the account
      * Password: Copy auto-generated password
      * Account enabled: Checked
  * Press **Review + create**
  * Click **Create**
* Launch Azure Data Studio in production virtual machine 
* Using the instructions in [Testing Microsoft Entra ID](#testing-microsoft-entra-id) with the admin credentials to gain access to the database.
* Right click the database server.
* Select **New Query**.
* Copy, paste and edit the following code.
>[!Important]
> Only change user email in the brackets
```
CREATE USER [new_user@yourdomain.com] FROMEXTERNAL PROVIDER;
ALTER ROLE db_datareader ADD MEMBER[new_user@yourdomain.com];
```
* Press **Run** icon
* Message will show that "Commands completed successfully."
#### Test User Access
* In the same connection, Right click the server
* Click **Edit Connection**
* Only change account field
  * Drop menu and select **Add an account**
  * Use the browser and **new user credentials** to continue
  * Upon first login, set up a **new password**.
* Connect after verification has been done.
* Test Read only Access
  * Right click any table under Tables
  * Click **Select Top 1000**
  * Copy, past and edit following code.
  ```
  DELETE TOP (1)
  FROM user_chosen_table_name
  ```
* A message will indicate "The DELETE permission was denied on the object".