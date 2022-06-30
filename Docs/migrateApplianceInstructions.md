# AZURE MIGRATE APPLIANCE SETUP/CONFIGURATION

*Authored by:*

*Shane Neff*

*Senior Cloud Solution Architect- Microsoft*

*6/29/2022*

---

## AZURE MIGRATE OVERVIEW

Azure Migrate provides a central hub to track discovery, assessment, and migration of your on-premises apps and workloads and private and public cloud VMs to Azure. The hub provides Azure Migrate tools for assessment and migration and third-party ISV offerings


The [Azure Migrate](https://docs.microsoft.com/en-us/azure/migrate/migrate-services-overview) service....




Azure Migrate: [Discovery and assessment tool](https://docs.microsoft.com/en-us/azure/migrate/migrate-services-overview#azure-migrate-discovery-and-assessment-tool)

- Azure readiness: Assesses whether on-premises servers are ready for migration to Azure
- Azure sizing: Estimates the size of Azure VMs
- Azure cost estimation: Estimates costs for running on-premises servers in Azure.
- Dependency analysis: Identifies cross-server dependencies and optimization strategies for moving interdependent servers to Azure

To enable server migrations

---

## AZURE MIGRATE APPLIANCE OVERVIEW

Discovery and assessment use a lightweight Azure Migrate appliance that you deploy on-premises

- The appliance runs on a VM or physical server
- The appliance discovers on-premises servers. It also continually sends server metadata and performance data to Azure Migrate
- Appliance discovery is agentless. Nothing is installed on discovered servers


- Changes performed on Windows servers (these are all performed when the preparation script is run): https://docs.microsoft.com/en-us/azure/migrate/prepare-for-agentless-migration#changes-performed-on-windows-servers
- 

---

## AZURE MIGRATE ARCHITECTURE

[Azure Migrate Agentless architecture](https://docs.microsoft.com/en-us/azure/migrate/prepare-for-agentless-migration)

---

## AZURE MIGRATE: SERVER MIGRATION TOOL

The Azure Migrate: [Server Migration tool](https://docs.microsoft.com/en-us/azure/migrate/migrate-services-overview#azure-migrate-server-migration-tool) helps in migrating servers to Azure

- On-premises VMware VMs: Migrate VMs to Azure using agentless or agent-based migration
     - For agentless migration, Server Migration uses the same appliance that is used by Discovery and assessment tool for discovery and assessment of servers

---

## SYSTEM REQUIREMENTS 

### VMware Requirements

- vCenter Server running 5.5, 6.0, 6.5, 6.7 or 7.0 
- ESXi host running version 5.5 or later

### Azure Migrate appliance

[Azure Migrate appliance System Requirements](https://docs.microsoft.com/en-us/azure/migrate/migrate-appliance)


- Windows Server 2008 or later
- 

---




## NETWORK REQUIREMENTS

The Azure Migrate appliance needs connectivity to the internet.

When you deploy the appliance, Azure Migrate does a connectivity check to the required URLs.
You need to allow access to all URLs in the list. If you're doing assessment only, you can skip the URLs that are marked as required for VMware agentless migration.
If you're using a URL-based proxy to connect to the internet, make sure that the proxy resolves any CNAME records received while looking up the URLs


| URL                                                                                                                                                                                	| Details                                                                                              	|
|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------	|------------------------------------------------------------------------------------------------------	|
| *.portal.azure.com                                                                                                                                                                 	| Navigate to the Azure portal.                                                                        	|
| *.windows.net<br>*.msftauth.net<br>*.msauth.net<br>*.microsoft.com<br>*.live.com<br>*.office.com<br>*.microsoftonline.com<br>*.microsoftonline-p.com<br>*.microsoftazuread-sso.com 	| Used for access control and identity management by Azure Active Directory                            	|
| management.azure.com                                                                                                                                                               	| Used for resource deployments and management operations                                              	|
| *.services.visualstudio.com                                                                                                                                                        	| Upload appliance logs used for internal monitoring.                                                  	|
| *.vault.azure.net                                                                                                                                                                  	| Manage secrets in the Azure Key Vault.<br>Note: Ensure servers to replicate have access to this.     	|
| aka.ms/*                                                                                                                                                                           	| Allow access to these links; used to download and install the latest updates for appliance services. 	|
| download.microsoft.com/download                                                                                                                                                    	| Allow downloads from Microsoft download center.                                                      	|
| *.servicebus.windows.net                                                                                                                                                           	| Communication between the appliance and the Azure Migrate service.                                   	|
| *.discoverysrv.windowsazure.com<br>*.migration.windowsazure.com                                                                                                                    	| Connect to Azure Migrate service URLs.                                                               	|
| *.hypervrecoverymanager.windowsazure.com                                                                                                                                           	| Used for VMware agentless migration<br><br>Connect to Azure Migrate service URLs.                    	|
| *.blob.core.windows.net                                                                                                                                                            	| Used for VMware agentless migration<br><br>Upload data to storage for migration.                     	|

---

## CONFIGURATION STEPS

- Deploy as new server running on vCenter Server using OVA template
- Download VM Agent Installer: https://go.microsoft.com/fwlink/?LinkID=394789

---

## ON-PREMISES CONFIGURATION

[Set up an appliance for servers in a VMware environment](https://docs.microsoft.com/en-us/azure/migrate/how-to-set-up-appliance-vmware)

- Deploy by using an OVA template
- Download the OVA template
- Create the appliance server
- Verify appliance access to Azure
- Configure the appliance
- Set up prerequisites and register the appliance

---

### Start continuous discovery

Complete the setup steps in the appliance configuration manager to prepare for and start discovery

### Provide server credentials

---

### Start discovery


---

### Provide vCenter Server details
The appliance must connect to vCenter Server to discover the configuration and performance data of the servers:

---


## AZURE CONFIGURATION

To support HA/DR requirements, this solution will leverage [Region Pairs](https://docs.microsoft.com/en-gb/azure/availability-zones/cross-region-replication-azure#azure-cross-region-replication-pairings-for-all-geographies)

Region selection: West Europe- it is a region pair B and it's paired region is Northern Europe, which is located in Northern Ireland

