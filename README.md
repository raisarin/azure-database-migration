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
#### SQL Server and SQL Server Management Studio (SSMS) installation in Virtual Machine
##### Installation 
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


https://aicore-portal-public-prod-307050600709.s3.eu-west-1.amazonaws.com/project-files/93dd5a0c-212d-48eb-ad51-df521a9b4e9c/AdventureWorks2022.bak