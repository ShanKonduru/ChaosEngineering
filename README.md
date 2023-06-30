# ChaosEngineering

# Chaos Engineering - Step by Step guide

## Important Information 
```shell
team id : 6dec412f-9937-46a6-ac41-2f993706a6a1
team secret: 8956e88f-0211-40cc-96e8-8f0211a0cc59
```

### Step #1 Launch command window as Administrator from your desktop machine
#### initiate secured shell using the following command line, SSH stands for 'Secured Shell' -i Stands for '<identity_file>' and last parameter is  [user@]hostIP[:port]
```shell
ssh -i .\chaostraining.pem azureuser@74.235.254.188
```

### Step #2, Add packages needed to install and verify gremlin (already on many systems)
```shell
sudo -i
sudo apt update && sudo apt install -y apt-transport-https dirmngr
```

### Step #3, Add the Gremlin repo
```shell
echo "deb https://deb.gremlin.com/ release non-free" | sudo tee /etc/apt/sources.list.d/gremlin.list
```

### Step #4, Import the GPG key
```shell
	sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 9CDB294B29A5B1E2E00C24C022E8EF3461A50EF6
```

### Step #5, Install Gremlin
```shell
sudo apt update && sudo apt install -y gremlin gremlind
```

### Step #6, Initiaize Gremlin
```shell
sudo -i
gremlin init
```
input team ID <cr>
input team secret <cr>

### Step #7, Gremlin check
#### to check you are connected to gremlin type 
```shell
gremlin check
```
##### Under Auth seciton you should see
```shell
auth
====================================================
Auth Input Type                      : Secret
API Response                         : OK
```

### Step #8, Under Gremlin portal run an attack 
#### Launch Browser 
#### Login to Gremlin Portal
#### Select new Experiment 
#### Select Hosts
#### Choose the IP address of the Host
#### Choose Gremlin - CPU - give make Utilization to 100%
#### Run the experiment on the selected host.
#### In the Gremlin  run a CPU attack for your VM using the Gremlin portal

### Step #9, To check the CPU utilization % from the shell  
#### in the command shell type, to view top few processes
```shell
	top
```

## Docker Commands 

### Step #10, Installing Docker
#### in the command shell type, to view top few processes
```shell
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo apt-key add -
```
#### Got OK as response for the above comand 

### Step #11, Installing appropriate repository
#### in the command shell type, to view top few processes
```shell
sudo add-apt-repository "deb [arch=amd64] https://download.docker.com/linux/ubuntu $(lsb_release -cs) stable"
```
#### Got DONE as response for the above comand 

### Step #12, updates the package index files to get the latest list of available packages in the repositories
#### in the command shell type, to view top few processes
```shell
sudo apt-get update
```
#### Got DONE as response for the above comand 

### Step #13, updates the package index files to get the latest list of available packages in the repositories
#### in the command shell type, to view top few processes
```shell
apt-cache policy docker-ce
```
#### Got NO as response for the above comand 

### Step #14, To install Docker Engine, containerd, and Docker Compose on Ubuntu
```shell
sudo apt-get install docker-ce docker-ce-cli containerd.io
```
#### Got NO as response for the above comand 

### Step #15,  to Check If the Docker Daemon or a Container Is Running
```shell
sudo systemctl status docker
```
#### Got a response for the above comand, need to press Ctrl+C to exit  

### Step #16,  to assign or change user permissions docker users
```shell
sudo usermod -aG docker azureuser
```
#### Got NO as response for the above comand 

## Nginx
### Step #17,  create Index.html page in the vm
```shell
sudo -i
mkdir -p ~/docker-nginx/html
cd ~/docker-nginx/html
nano index.html
```
#### Copy the folowing html code and paste into the index.html
```html
<html>
  <head>
    <title>Sample HTML</title>
    <link
      rel="stylesheet"
      href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0/css/bootstrap.min.css"
      integrity="sha384-Gn5384xqQ1aoWXA+058RXPxPg6fy4IWvTNh0E263XmFcJlSAwiGgFAW/dAiS6JXm"
      crossorigin="anonymous"
    />
  </head>
  <body>
    <div class="container">
      <h1>This is a sample HTML to check our container</h1>
      <p>This signifies nginx container is working fine</p>
      <p>Now i am ready for the attack</p>
    </div>
  </body>
</html>
```
#### To save this file, type Ctrl+x 
#### to save the above file, you need to hit Ctrl+X and then Y

### Step #18,  create Container with name using nginx
```shell
sudo -i
docker run -l service=nginx --name shan-docker-nginx -p 80:80 -d -v ~/docker-nginx/html:/usr/share/nginx/html nginx
```

### Step #19,  to view if the Container has been creaed or not.
```shell
docker ps -a
```
#### to view whether the service is up and running use the above command 

### Step #20,  Install Gremlin using docker run.
```shell
docker run -d --net=host \
    --cap-add=NET_ADMIN --cap-add=SYS_BOOT --cap-add=SYS_TIME \
    --cap-add=KILL \
    --pid=host \
    -v $PWD/var/lib/gremlin:/var/lib/gremlin \
    -v $PWD/var/log/gremlin:/var/log/gremlin \
    -v /var/run/docker.sock:/var/run/docker.sock \
    -e GREMLIN_TEAM_ID="6dec412f-9937-46a6-ac41-2f993706a6a1" \
    -e GREMLIN_TEAM_SECRET="8956e88f-0211-40cc-96e8-8f0211a0cc59" \
    gremlin/gremlin daemon
```
#### this creates nginx container in the VM

### Step #21,  to view if the Container has been creaed or not.
```shell
docker ps -a
```
#### to view whether the service is up and running use the above command 


## Commands
az account =>Manage Azure subscription information.

az acr	=> Manage private registries with Azure Container Registries.

az ad	=>Manage Azure Active Directory Graph entities needed for Role Based Access Control.

az adp	=> Manage Azure Autonomous Development Platform resources.

az advisor	=> Manage Azure Advisor.

az afd	=> Manage Azure Front Door Standard/Premium. For classical Azure Front Door, please refer https://docs.microsoft.com/en-us/cli/azure/network/front-door?view=azure-cli-latest.

az ai-examples	=> Add AI powered examples to help content.

az aks	=> Manage Azure Kubernetes Services.

az alerts-management	=> Manage Azure Alerts Management Service Resource.

az alias	=> Manage Azure CLI Aliases.

az ams	=> Manage Azure Media Services resources.

az apim	=> Manage Azure API Management services.

az appconfig	=> Manage App Configurations.

az appservice	=> Manage App Service plans.

az arcappliance	=> Commands to manage an Appliance resource.

az arcdata	=> Commands for using Azure Arc-enabled data services.

az aro	=> Manage Azure Red Hat OpenShift clusters.

az artifacts	=> Manage Azure Artifacts.

az attestation	=> Manage Microsoft Azure Attestation (MAA).

az automanage	=> Manage Automanage.

az automation	=> Manage Automation Account.

az azurestackhci=> Manage azurestackhci.

az backup	=> Manage Azure Backups.

az baremetalinstance => (PREVIEW) Manage BareMetal Instances.

az batch	=> Manage Azure Batch.

az batchai	=> Manage Batch AI resources.

az bicep	=> Bicep CLI command group.

az billing	=> Manage Azure Billing.

az billing-benefits => Azure billing benefits commands.

az blockchain	=> Manage blockchain.

az blueprint	=> Commands to manage blueprint.

az boards	=> Manage Azure Boards.

az bot	=> Manage Microsoft Azure Bot Service.

az cache	=> Commands to manage CLI objects cached using the --defer argument.

az capacity	=> Manage capacity resources.

az cdn	=> Manage Azure Content Delivery Networks (CDNs).

az change-analysis=> List changes for resources.

az cli-translator	=> Translate ARM template or REST API to CLI scripts.

az cloud	=> Manage registered Azure clouds.

az cloud-service=> Manage cloud service (extended support).

az cognitiveservices => Manage Azure Cognitive Services accounts.

az communication	=> Manage communication service with communication.

az confcom	=> Commands to generate security policies for confidential containers in Azure.

az confidentialledger => Manage Confidential Ledger.

az config	=> Manage Azure CLI configuration.

az configure	=> Manage Azure CLI configuration. This command is interactive.

az confluent	=> Manage confluent resources.

az connectedk8s	=> Commands to manage connected kubernetes clusters.

az connectedmachine => Manage Connected Machine.

az connectedvmware	=> Commands to manage Connected VMware.

az connection	=> Commands to manage Service Connector local connections which allow local environment to connect Azure Resource. If you want to manage connection for compute service, please run 'az webapp/containerapp/spring connection'.

az consumption	=> Manage consumption of Azure resources.

az container	=> Manage Azure Container Instances.

az containerapp	=> Manage Azure Container Apps.

az cosmosdb	=> Manage Azure Cosmos DB database accounts.

az costmanagement => Manage cost and billing in Azure.

az csvmware	=> Manage Azure VMware Solution by CloudSimple.

az custom-providers => Commands to manage custom providers.

az customlocation	=> Commands to Create, Get, List and Delete CustomLocations.

az databox	=> Manage data box.

az databoxedge	=> Support data box edge device and management.

az databricks	=> Manage databricks workspaces.

az datadog	=> Manage datadog.

az datafactory	=> Manage Data Factory.

az datamigration => Manage Data Migration.

az dataprotection => Manage dataprotection.

az datashare	=> Manage Data Share.

az dedicated-hsm => Manage dedicated hsm with hardware security modules.

az demo	=> Demos for designing, developing and demonstrating Azure CLI.

az deployment	 => Manage Azure Resource Manager template deployment at subscription scope.

az deployment-scripts	=> Manage deployment scripts at subscription or resource group scope.

az desktopvirtualization	=> Manage desktop virtualization.

az devcenter	=>  Manage resources with devcenter.

az devops	=> Manage Azure DevOps organization level operations.

az disk	 => Manage Azure Managed Disks.

az disk-access	=> Manage disk access resources.

az disk-encryption-set	=> Disk Encryption Set resource.

az disk-pool	=> Manage Azure disk pool.

az dla	=> Manage Data Lake Analytics accounts, jobs, and catalogs.

az dls	=> Manage Data Lake Store accounts and filesystems.

az dms	=> Manage Azure Data Migration Service (classic) instances.

az dnc	=> Manage Delegated Network.

az dns-resolver	=> Manage Dns Resolver.

az dt	=> Manage Azure Digital Twins solutions & infrastructure.

az dynatrace	=> Manage dynatrace.

az edgeorder	 => Manage Edge Order.

az elastic	=> Manage Microsoft Elastic.

az elastic-san	=> Manage Elastic SAN.

az eventgrid	=> Manage Azure Event Grid topics, domains, domain topics, system topics partner topics, event subscriptions, system topic event subscriptions and partner topic event subscriptions.

az eventhubs	
Eventhubs.

az extension	
Manage and update CLI extensions.

az feature	
Manage resource provider features.

az feedback	
Send feedback to the Azure CLI Team.

az find	
I'm an AI robot, my advice is based on our Azure documentation as well as the usage patterns of Azure CLI and Azure ARM users. Using me improves Azure products and documentation.

az fleet	
Commands to manage fleet.

az fluid-relay	
Manage Fluid Relay.

az footprint	
az functionapp	
Manage function apps. To install the Azure Functions Core tools see https://github.com/Azure/azure-functions-core-tools.

az fzf	
Commands to select active or default objects via fzf.

az grafana	
Commands to manage Azure Grafana instanced.

az graph	
Query the resources managed by Azure Resource Manager.

az group	
Manage resource groups and template deployments.

az guestconfig	
Manage Guest Configuration.

az hack	
Commands to manage resources commonly used for student hacks.

az hanainstance	
(PREVIEW) Manage Azure SAP HANA Instance.

az hdinsight	
Manage HDInsight resources.

az healthbot	
Manage bot with healthbot.

az healthcareapis	
Manage Healthcare Apis.

az hpc-cache	
Commands to manage hpc cache.

az hybridaks	
Manage hybridaks provisioned clusters.

az identity	
Managed Identities.

az image	
Manage custom virtual machine images.

az import-export	
Manage Import Export.

az init	
It's an effortless setting up tool for configs.

az interactive	
Start interactive mode. Installs the Interactive extension if not installed already.

az internet-analyzer	
Commands to manage internet analyzer.

az iot	
Manage Internet of Things (IoT) assets.

az k8s-configuration	
Commands to manage resources from Microsoft.KubernetesConfiguration.

az k8s-extension	
Commands to manage Kubernetes Extensions.

az k8sconfiguration	
Commands to manage Kubernetes configuration.

az keyvault	
Manage KeyVault keys, secrets, and certificates.

az kusto	
Manage Azure Kusto resources.

az lab	
Manage Azure DevTest Labs.

az load	
Manage Azure Load Testing resources.

az lock	
Manage Azure locks.

az logic	
Manage Logic.

az logicapp	
Manage logic apps.

az login	
Log in to Azure.

az logout	
Log out to remove access to Azure subscriptions.

az logz	
Manage Microsoft Logz.

az maintenance	
Manage Maintenance.

az managed-cassandra	
Azure Managed Cassandra.

az managedapp	
Manage template solutions provided and maintained by Independent Software Vendors (ISVs).

az managedservices	
Manage the registration assignments and definitions in Azure.

az managementpartner	
Allows the partners to associate a Microsoft Partner Network(MPN) ID to a user or service principal in the customer's Azure directory.

az maps	
Manage Azure Maps.

az mariadb	
Manage Azure Database for MariaDB servers.

az mesh	
(PREVIEW) Manage Azure Service Fabric Mesh Resources.

az ml	
Manage Azure Machine Learning resources with the Azure CLI ML extension v2.

az ml	
Manage Azure Machine Learning resources with the Azure CLI ML extension v1.

az mobile-network	
Manage mobile network.

az monitor	
Manage the Azure Monitor Service.

az mysql	
Manage Azure Database for MySQL servers.

az netappfiles	
Manage Azure NetApp Files (ANF) Resources.

az network	
Manage Azure Network resources.

az network-function	
Manage network function.

az networkcloud	
Manage Network Cloud resources.

az networkfabric	
Manage Azure Network Fabric Management Service API.

az next	
Recommend the possible next set of commands to take.

az nginx	
Manage NGINX deployment resources.

az notification-hub	
Manage Notification Hubs.

az offazure	
Manage on-premise resources for migrate.

az orbital	
Azure Orbital Ground Station as-a-Service (GSaaS).

az partnercenter	
Partner Center management.

az peering	
Manage peering.

az pipelines	
Manage Azure Pipelines.

az policy	
Manage resource policies.

az portal	
Manage Portal.

az postgres	
Manage Azure Database for PostgreSQL servers.

az powerbi	
Manage PowerBI resources.

az ppg	
Manage Proximity Placement Groups.

az private-link	
Private-link association CLI command group.

az provider	
Manage resource providers.

az providerhub	
Manage resources with ProviderHub.

az purview	
Manage Purview.

az quantum	
Manage Azure Quantum Workspaces and submit jobs to Azure Quantum Providers.

az qumulo	
Manage qumulo.

az quota	
Manage Azure Quota Extension API.

az redis	
Manage dedicated Redis caches for your Azure applications.

az redisenterprise	
Manage the redisenterprise cache.

az relay	
Manage Azure Relay Service namespaces, WCF relays, hybrid connections, and rules.

az remote-rendering-account	
Manage remote rendering account with mixed reality.

az repos	
Manage Azure Repos.

az reservations	
Azure Reservations.

az resource	
Manage Azure resources.

az resource-mover	
Manage Resource Mover Service API.

az resourcemanagement	
Resourcemanagement CLI command group.

az rest	
Invoke a custom request.

az restore-point	
Manage restore point with res.

az role	
Manage user roles for access control with Azure Active Directory and service principals.

az sapmonitor	
(PREVIEW) Manage Azure SAP Monitor.

az scenario	
E2E Scenario Usage Guidance.

az scvmm	
Commands for managing Arc for SCVMM resources.

az search	
Manage Azure Search services, admin keys and query keys.

az security	
Manage your security posture with Microsoft Defender for Cloud.

az self-help	
Azure SelfHelp will help you troubleshoot issues with Azure resources.

az self-test	
Runs a self-test of the CLI.

az sentinel	
Manage Microsoft Sentinel.

az serial-console	
Connect to the Serial Console of a Linux/Windows Virtual Machine or VMSS Instance.

az servicebus	
Servicebus.
az sf	=>Manage and administer Azure Service Fabric clusters.
az sig	=>Manage shared image gallery.
az signalr	=>Manage Azure SignalR Service.
az snapshot	=>Manage point-in-time copies of managed disks, native blobs, or other snapshots.
az spatial-anchors-account	=>Manage spatial anchor account with mixed reality.
az spring	=>Commands to manage Azure Spring Apps.
az spring-cloud	=>Commands to manage Azure Spring Cloud.
az sql	=>Manage Azure SQL Databases and Data Warehouses.
az ssh	=> SSH into resources (Azure VMs, Arc servers, etc) using AAD issued openssh certificates.
az sshkey	=>Manage ssh public key with vm.
az stack-hci	=>Manage Azure Stack HCI.
az staticwebapp	=>Manage static apps.
az storage	=>Manage Azure Cloud Storage resources.
az storage-mover	=>Manage top-level Storage Mover resource.
az storagesync	=>Manage Azure File Sync.
az stream-analytics	=>Manage Stream Analytics.
az support	=>Manage Azure support resource.
az survey	=>Take Azure CLI survey.
az synapse	=>Manage and operate Synapse Workspace, Spark Pool, SQL Pool.
az tag	=>Tag Management on a resource.
az term	=>Manage marketplace agreement with marketplaceordering.
az ts	=Manage template specs at subscription or resource group scope.
az tsi	=>Manage Azure Time Series Insights.
az upgrade	=>Upgrade Azure CLI and extensions.
az version	=>Show the versions of Azure CLI modules and extensions in JSON format by default or format configured by --output.
az vm	=>Manage Linux or Windows virtual machines.
az vmss	=>Manage groupings of virtual machines in an Azure Virtual Machine Scale Set (VMSS).
az vmware	=>Commands to manage Azure VMware Solution.
az webapp	=>Manage web apps.
az webpubsub	=>Commands to manage Webpubsub.
az workloads	=>Manage workloads.
