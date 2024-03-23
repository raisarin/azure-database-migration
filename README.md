# azure-database-migration

Provide insights into the virtual machine setup, SQL Server installation, and the creation of the production database

## Milestone 
### Azure Account Setup/Login
Sign up or log into your Azure Account using [Azure Portal](https://portal.azure.com/ "https://portal.azure.com/")

### Milestone 2: Setup production environment

#### Windows Virtual Machine setup 
##### Virtual machine dashboard
* Look and select for "Virtual Machines" in the search menu.
* Use create drop menu and choose Azure virtual machine. 
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
###### Finalising virtual machine 
* Select **Review + Create**, this will initialise validation. 
* Once validation has passed, select **Create** button. 
* A new page will show once the depolyment of the viraul machine is complete
#### SQL Server installation 

#### Production database 
