# azure-database-migration

Provide insights into the virtual machine setup, SQL Server installation, and the creation of the production database

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
###### Project details
* Select appropriate **Subscription**.
* Create and name new **Resource Group**. 
###### Instance details
* Add appropriate **Virtual Name**. 
* Select **Region** geopraphically close to user location.
* Select **Image** as **Windows 11 Pro** for this project. 
* Choose **Size** as **B2ms** Standard or General Purpose. If not found in the drop down menu, click **See all sizes** and find in **B-Series**.
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
* A new page will show once the depolyment of the virtual machine is complete.

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
##### SQL Server Schema Compare
###### Schema Extension
* In Azure Studio Data Studio, find and click **Extension** icon in the left sidebar.
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
> [!NOTE] 
> This process only uploads the tables and structure of the database to the cloud **without the values or data**.