# cp1-criacao-recursos-nuvem

#### Implantação de Recursos de Aplicação Web com Azure CLI
<details>
<summary>Ex1</summary>

```bash
# Definir variáveis

vinicius [ ~ ]$ resourceGroupName="DimDimResources"           # Nome do grupo de recursos
location="eastus"                             # Região onde os recursos serão criados
vmName="DimDiRM94266"                         # Nome da máquina virtual
vmSize="Standard_DS2_v2"                      # Tamanho da máquina virtual
image="UbuntuLTS"                             # Imagem do sistema operacional
tags="Ambiente=Desenvolvimento Projeto=DimDimCloud" # Tags para a máquina virtual

# Informações necessárias do úsuario

vinicius [ ~ ]$ read -p "Nome do disco: " diskName             # Nome do disco
read -p "Tamanho do disco em GB: " diskSizeGB  # Tamanho do disco em GB
read -p "Nome da Rede Virtual: " vnetName      # Nome da Rede Virtual
read -p "Nome do Grupo de Segurança de Rede: " nsgName  # Nome do Grupo de Segurança de Rede
read -p "Nome de usuário: " username           # Nome de usuário para a VM
read -s -p "Senha: " password                  # Solicitar senha de forma segura

# Criar grupo de recursos

vinicius [ ~ ]$ az group create --name $resourceGroupName --location $location

# Criar máquina virtual

vinicius [ ~ ]$ az vm create \
  --resource-group $resourceGroupName \
  --name $vmName \
  --image $image \
  --size $vmSize \
  --admin-username $username \
  --admin-password $password \
  --authentication-type password \
  --nsg $nsgName \
  --vnet-name $vnetName \
  --os-disk-size-gb $diskSizeGB \
  --tags $tags

```

</details>
  
#### criar WebApp .net cloud shell bash

<details>
<summary>Ex2</summary>
```bash
felipe [ ~ ]$ #criando grupo de recurso
felipe [ ~ ]$ az group create --name DimDimAppResources --location westeurope
{
  "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources",
  "location": "westeurope",
  "managedBy": null,
  "name": "DimDimAppResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
felipe [ ~ ]$ #Criando serviço de aplicativo
felipe [ ~ ]$ az appservice plan create --name DimDimAppPlan --resource-group DimDimAppResources --sku FREE
{
  "elasticScaleEnabled": false,
  "extendedLocation": null,
  "freeOfferExpirationTime": null,
  "geoRegion": "West Europe",
  "hostingEnvironmentProfile": null,
  "hyperV": false,
  "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/serverfarms/DimDimAppPlan",
  "isSpot": false,
  "isXenon": false,
  "kind": "app",
  "kubeEnvironmentProfile": null,
  "location": "westeurope",
  "maximumElasticWorkerCount": 1,
  "maximumNumberOfWorkers": 0,
  "name": "DimDimAppPlan",
  "numberOfSites": 0,
  "numberOfWorkers": 0,
  "perSiteScaling": false,
  "provisioningState": "Succeeded",
  "reserved": false,
  "resourceGroup": "DimDimAppResources",
  "sku": {
    "capabilities": null,
    "capacity": 0,
    "family": "F",
    "locations": null,
    "name": "F1",
    "size": "F1",
    "skuCapacity": null,
    "tier": "Free"
  },
  "spotExpirationTime": null,
  "status": "Ready",
  "subscription": "da9a6d86-ab87-497a-8d8a-d98185d23cea",
  "tags": null,
  "targetWorkerCount": 0,
  "targetWorkerSizeId": 0,
  "type": "Microsoft.Web/serverfarms",
  "workerTierName": null,
  "zoneRedundant": false
}
felipe [ ~ ]$ az webapp list-runtimes --os-type windows
[
  "dotnet:7",
  "dotnet:6",
  "ASPNET:V4.8",
  "ASPNET:V3.5",
  "NODE:18LTS",
  "NODE:16LTS",
  "java:1.8:Java SE:8",
  "java:11:Java SE:11",
  "java:17:Java SE:17",
  "java:1.8:TOMCAT:10.0",
  "java:11:TOMCAT:10.0",
  "java:17:TOMCAT:10.0",
  "java:1.8:TOMCAT:9.0",
  "java:11:TOMCAT:9.0",
  "java:17:TOMCAT:9.0",
  "java:1.8:TOMCAT:8.5",
  "java:11:TOMCAT:8.5",
  "java:17:TOMCAT:8.5"
]
felipe [ ~ ]$ az webapp create --name WebAppRM94266e --resource-group DimDimAppResources --plan DimDimAppPlan --runtime "dotnet:7"
{
  "availabilityState": "Normal",
  "clientAffinityEnabled": true,
  "clientCertEnabled": false,
  "clientCertExclusionPaths": null,
  "clientCertMode": "Required",
  "cloningInfo": null,
  "containerSize": 0,
  "customDomainVerificationId": "EE71DDAE164806A5409EF03B4B10766153DA1768306685C710957DFB7DCAD3EE",
  "dailyMemoryTimeQuota": 0,
  "defaultHostName": "webapprm94266e.azurewebsites.net",
  "enabled": true,
  "enabledHostNames": [
    "webapprm94266e.azurewebsites.net",
    "webapprm94266e.scm.azurewebsites.net"
  ],
  "extendedLocation": null,
  "ftpPublishingUrl": "ftps://waws-prod-am2-485.ftp.azurewebsites.windows.net/site/wwwroot",
  "hostNameSslStates": [
    {
      "certificateResourceId": null,
      "hostType": "Standard",
      "ipBasedSslResult": null,
      "ipBasedSslState": "NotConfigured",
      "name": "webapprm94266e.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "toUpdateIpBasedSsl": null,
      "virtualIp": null
    },
    {
      "certificateResourceId": null,
      "hostType": "Repository",
      "ipBasedSslResult": null,
      "ipBasedSslState": "NotConfigured",
      "name": "webapprm94266e.scm.azurewebsites.net",
      "sslState": "Disabled",
      "thumbprint": null,
      "toUpdate": null,
      "toUpdateIpBasedSsl": null,
      "virtualIp": null
    }
  ],
  "hostNames": [
    "webapprm94266e.azurewebsites.net"
  ],
  "hostNamesDisabled": false,
  "hostingEnvironmentProfile": null,
  "httpsOnly": false,
  "hyperV": false,
  "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/sites/WebAppRM94266e",
  "identity": null,
  "inProgressOperationId": null,
  "isDefaultContainer": null,
  "isXenon": false,
  "keyVaultReferenceIdentity": "SystemAssigned",
  "kind": "app",
  "lastModifiedTimeUtc": "2023-09-07T17:11:44.576666",
  "location": "West Europe",
  "maxNumberOfWorkers": null,
  "name": "WebAppRM94266e",
  "outboundIpAddresses": "20.76.202.176,20.76.202.219,20.76.202.251,20.76.203.229,20.76.205.16,20.76.205.70,20.50.2.79",
  "possibleOutboundIpAddresses": "20.76.202.176,20.76.202.219,20.76.202.251,20.76.203.229,20.76.205.16,20.76.205.70,20.101.200.78,20.101.200.94,20.101.200.121,20.101.200.155,20.101.200.187,20.101.200.225,20.101.200.231,20.101.200.232,20.101.201.11,20.101.201.21,20.101.201.31,20.101.201.33,20.101.201.34,20.101.201.38,20.101.201.60,20.101.201.73,20.101.201.110,20.101.200.229,20.101.200.244,20.101.200.245,20.101.201.1,20.101.201.4,20.101.201.5,20.101.201.14,20.50.2.79",
  "publicNetworkAccess": null,
  "redundancyMode": "None",
  "repositorySiteName": "WebAppRM94266e",
  "reserved": false,
  "resourceGroup": "DimDimAppResources",
  "scmSiteAlsoStopped": false,
  "serverFarmId": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/serverfarms/DimDimAppPlan",
  "siteConfig": {
    "acrUseManagedIdentityCreds": false,
    "acrUserManagedIdentityId": null,
    "alwaysOn": false,
    "antivirusScanEnabled": null,
    "apiDefinition": null,
    "apiManagementConfig": null,
    "appCommandLine": null,
    "appSettings": null,
    "autoHealEnabled": null,
    "autoHealRules": null,
    "autoSwapSlotName": null,
    "azureMonitorLogCategories": null,
    "azureStorageAccounts": null,
    "connectionStrings": null,
    "cors": null,
    "customAppPoolIdentityAdminState": null,
    "customAppPoolIdentityTenantState": null,
    "defaultDocuments": null,
    "detailedErrorLoggingEnabled": null,
    "documentRoot": null,
    "elasticWebAppScaleLimit": 0,
    "experiments": null,
    "fileChangeAuditEnabled": null,
    "ftpsState": null,
    "functionAppScaleLimit": null,
    "functionsRuntimeScaleMonitoringEnabled": null,
    "handlerMappings": null,
    "healthCheckPath": null,
    "http20Enabled": false,
    "http20ProxyFlag": null,
    "httpLoggingEnabled": null,
    "ipSecurityRestrictions": [
      {
        "action": "Allow",
        "description": "Allow all access",
        "headers": null,
        "ipAddress": "Any",
        "name": "Allow all",
        "priority": 2147483647,
        "subnetMask": null,
        "subnetTrafficTag": null,
        "tag": null,
        "vnetSubnetResourceId": null,
        "vnetTrafficTag": null
      }
    ],
    "ipSecurityRestrictionsDefaultAction": null,
    "javaContainer": null,
    "javaContainerVersion": null,
    "javaVersion": null,
    "keyVaultReferenceIdentity": null,
    "limits": null,
    "linuxFxVersion": "",
    "loadBalancing": null,
    "localMySqlEnabled": null,
    "logsDirectorySizeLimit": null,
    "machineKey": null,
    "managedPipelineMode": null,
    "managedServiceIdentityId": null,
    "metadata": null,
    "minTlsCipherSuite": null,
    "minTlsVersion": null,
    "minimumElasticInstanceCount": 0,
    "netFrameworkVersion": null,
    "nodeVersion": null,
    "numberOfWorkers": 1,
    "phpVersion": null,
    "powerShellVersion": null,
    "preWarmedInstanceCount": null,
    "publicNetworkAccess": null,
    "publishingPassword": null,
    "publishingUsername": null,
    "push": null,
    "pythonVersion": null,
    "remoteDebuggingEnabled": null,
    "remoteDebuggingVersion": null,
    "requestTracingEnabled": null,
    "requestTracingExpirationTime": null,
    "routingRules": null,
    "runtimeADUser": null,
    "runtimeADUserPassword": null,
    "scmIpSecurityRestrictions": [
      {
        "action": "Allow",
        "description": "Allow all access",
        "headers": null,
        "ipAddress": "Any",
        "name": "Allow all",
        "priority": 2147483647,
        "subnetMask": null,
        "subnetTrafficTag": null,
        "tag": null,
        "vnetSubnetResourceId": null,
        "vnetTrafficTag": null
      }
    ],
    "scmIpSecurityRestrictionsDefaultAction": null,
    "scmIpSecurityRestrictionsUseMain": null,
    "scmMinTlsVersion": null,
    "scmType": null,
    "sitePort": null,
    "storageType": null,
    "supportedTlsCipherSuites": null,
    "tracingOptions": null,
    "use32BitWorkerProcess": null,
    "virtualApplications": null,
    "vnetName": null,
    "vnetPrivatePortsCount": null,
    "vnetRouteAllEnabled": null,
    "webSocketsEnabled": null,
    "websiteTimeZone": null,
    "winAuthAdminState": null,
    "winAuthTenantState": null,
    "windowsConfiguredStacks": null,
    "windowsFxVersion": null,
    "xManagedServiceIdentityId": null
  },
  "slotSwapStatus": null,
  "state": "Running",
  "storageAccountRequired": false,
  "suspendedTill": null,
  "tags": null,
  "targetSwapSlot": null,
  "trafficManagerHostNames": null,
  "type": "Microsoft.Web/sites",
  "usageState": "Normal",
  "virtualNetworkSubnetId": null,
  "vnetContentShareEnabled": false,
  "vnetImagePullEnabled": false,
  "vnetRouteAllEnabled": false
}
felipe [ ~ ]$ az group list --output table
Name                        Location    Status
--------------------------  ----------  ---------
DimDimAppResources          westeurope  Succeeded
cloud-shell-storage-eastus  eastus      Succeeded
felipe [ ~ ]$ az group show --name DimDimAppResources
{
  "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources",
  "location": "westeurope",
  "managedBy": null,
  "name": "DimDimAppResources",
  "properties": {
    "provisioningState": "Succeeded"
  },
  "tags": null,
  "type": "Microsoft.Resources/resourceGroups"
}
felipe [ ~ ]$ az appservice plan list --resource-group DimDimAppResources
[
  {
    "elasticScaleEnabled": false,
    "extendedLocation": null,
    "freeOfferExpirationTime": null,
    "hostingEnvironmentProfile": null,
    "hyperV": false,
    "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/serverfarms/DimDimAppPlan",
    "isSpot": false,
    "isXenon": false,
    "kind": "app",
    "kubeEnvironmentProfile": null,
    "location": "West Europe",
    "maximumElasticWorkerCount": 1,
    "maximumNumberOfWorkers": 1,
    "name": "DimDimAppPlan",
    "numberOfSites": 1,
    "numberOfWorkers": 0,
    "perSiteScaling": false,
    "provisioningState": "Succeeded",
    "reserved": false,
    "resourceGroup": "DimDimAppResources",
    "sku": {
      "capabilities": null,
      "capacity": 0,
      "family": "F",
      "locations": null,
      "name": "F1",
      "size": "F1",
      "skuCapacity": null,
      "tier": "Free"
    },
    "spotExpirationTime": null,
    "status": "Ready",
    "tags": null,
    "targetWorkerCount": 0,
    "targetWorkerSizeId": 0,
    "type": "Microsoft.Web/serverfarms",
    "workerTierName": null,
    "zoneRedundant": false
  }
]
felipe [ ~ ]$ az webapp list --resource-group DimDimAppResources
[
  {
    "appServicePlanId": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/serverfarms/DimDimAppPlan",
    "availabilityState": "Normal",
    "clientAffinityEnabled": true,
    "clientCertEnabled": false,
    "clientCertExclusionPaths": null,
    "clientCertMode": "Required",
    "cloningInfo": null,
    "containerSize": 0,
    "customDomainVerificationId": "EE71DDAE164806A5409EF03B4B10766153DA1768306685C710957DFB7DCAD3EE",
    "dailyMemoryTimeQuota": 0,
    "defaultHostName": "webapprm94266.azurewebsites.net",
    "enabled": true,
    "enabledHostNames": [
      "webapprm94266.azurewebsites.net",
      "webapprm94266.scm.azurewebsites.net"
    ],
    "extendedLocation": null,
    "hostNameSslStates": [
      {
        "certificateResourceId": null,
        "hostType": "Standard",
        "ipBasedSslResult": null,
        "ipBasedSslState": "NotConfigured",
        "name": "webapprm94266.azurewebsites.net",
        "sslState": "Disabled",
        "thumbprint": null,
        "toUpdate": null,
        "toUpdateIpBasedSsl": null,
        "virtualIp": null
      },
      {
        "certificateResourceId": null,
        "hostType": "Repository",
        "ipBasedSslResult": null,
        "ipBasedSslState": "NotConfigured",
        "name": "webapprm94266.scm.azurewebsites.net",
        "sslState": "Disabled",
        "thumbprint": null,
        "toUpdate": null,
        "toUpdateIpBasedSsl": null,
        "virtualIp": null
      }
    ],
    "hostNames": [
      "webapprm94266.azurewebsites.net"
    ],
    "hostNamesDisabled": false,
    "hostingEnvironmentProfile": null,
    "httpsOnly": false,
    "hyperV": false,
    "id": "/subscriptions/da9a6d86-ab87-497a-8d8a-d98185d23cea/resourceGroups/DimDimAppResources/providers/Microsoft.Web/sites/WebAppRM94266",
    "identity": null,
    "inProgressOperationId": null,
    "isDefaultContainer": null,
    "isXenon": false,
    "keyVaultReferenceIdentity": "SystemAssigned",
    "kind": "app",
    "lastModifiedTimeUtc": "2023-09-07T17:09:06.340000",
    "location": "West Europe",
    "maxNumberOfWorkers": null,
    "name": "WebAppRM94266",
    "outboundIpAddresses": "20.76.202.176,20.76.202.219,20.76.202.251,20.76.203.229,20.76.205.16,20.76.205.70,20.50.2.79",
    "possibleOutboundIpAddresses": "20.76.202.176,20.76.202.219,20.76.202.251,20.76.203.229,20.76.205.16,20.76.205.70,20.101.200.78,20.101.200.94,20.101.200.121,20.101.200.155,20.101.200.187,20.101.200.225,20.101.200.231,20.101.200.232,20.101.201.11,20.101.201.21,20.101.201.31,20.101.201.33,20.101.201.34,20.101.201.38,20.101.201.60,20.101.201.73,20.101.201.110,20.101.200.229,20.101.200.244,20.101.200.245,20.101.201.1,20.101.201.4,20.101.201.5,20.101.201.14,20.50.2.79",
    "publicNetworkAccess": null,
    "redundancyMode": "None",
    "repositorySiteName": "WebAppRM94266",
    "reserved": false,
    "resourceGroup": "DimDimAppResources",
    "scmSiteAlsoStopped": false,
    "siteConfig": {
      "acrUseManagedIdentityCreds": false,
      "acrUserManagedIdentityId": null,
      "alwaysOn": false,
      "antivirusScanEnabled": null,
      "apiDefinition": null,
      "apiManagementConfig": null,
      "appCommandLine": null,
      "appSettings": null,
      "autoHealEnabled": null,
      "autoHealRules": null,
      "autoSwapSlotName": null,
      "azureMonitorLogCategories": null,
      "azureStorageAccounts": null,
      "connectionStrings": null,
      "cors": null,
      "customAppPoolIdentityAdminState": null,
      "customAppPoolIdentityTenantState": null,
      "defaultDocuments": null,
      "detailedErrorLoggingEnabled": null,
      "documentRoot": null,
      "elasticWebAppScaleLimit": null,
      "experiments": null,
      "fileChangeAuditEnabled": null,
      "ftpsState": null,
      "functionAppScaleLimit": 0,
      "functionsRuntimeScaleMonitoringEnabled": null,
      "handlerMappings": null,
      "healthCheckPath": null,
      "http20Enabled": true,
      "http20ProxyFlag": null,
      "httpLoggingEnabled": null,
      "ipSecurityRestrictions": null,
      "ipSecurityRestrictionsDefaultAction": null,
      "javaContainer": null,
      "javaContainerVersion": null,
      "javaVersion": null,
      "keyVaultReferenceIdentity": null,
      "limits": null,
      "linuxFxVersion": "",
      "loadBalancing": null,
      "localMySqlEnabled": null,
      "logsDirectorySizeLimit": null,
      "machineKey": null,
      "managedPipelineMode": null,
      "managedServiceIdentityId": null,
      "metadata": null,
      "minTlsCipherSuite": null,
      "minTlsVersion": null,
      "minimumElasticInstanceCount": 0,
      "netFrameworkVersion": null,
      "nodeVersion": null,
      "numberOfWorkers": 1,
      "phpVersion": null,
      "powerShellVersion": null,
      "preWarmedInstanceCount": null,
      "publicNetworkAccess": null,
      "publishingPassword": null,
      "publishingUsername": null,
      "push": null,
      "pythonVersion": null,
      "remoteDebuggingEnabled": null,
      "remoteDebuggingVersion": null,
      "requestTracingEnabled": null,
      "requestTracingExpirationTime": null,
      "routingRules": null,
      "runtimeADUser": null,
      "runtimeADUserPassword": null,
      "scmIpSecurityRestrictions": null,
      "scmIpSecurityRestrictionsDefaultAction": null,
      "scmIpSecurityRestrictionsUseMain": null,
      "scmMinTlsVersion": null,
      "scmType": null,
      "sitePort": null,
      "storageType": null,
      "supportedTlsCipherSuites": null,
      "tracingOptions": null,
      "use32BitWorkerProcess": null,
      "virtualApplications": null,
      "vnetName": null,
      "vnetPrivatePortsCount": null,
      "vnetRouteAllEnabled": null,
      "webSocketsEnabled": null,
      "websiteTimeZone": null,
      "winAuthAdminState": null,
      "winAuthTenantState": null,
      "windowsConfiguredStacks": null,
      "windowsFxVersion": null,
      "xManagedServiceIdentityId": null
    },
    "slotSwapStatus": null,
    "state": "Running",
    "storageAccountRequired": false,
    "suspendedTill": null,
    "tags": null,
    "targetSwapSlot": null,
    "trafficManagerHostNames": null,
    "type": "Microsoft.Web/sites",
    "usageState": "Normal",
    "virtualNetworkSubnetId": null,
    "vnetContentShareEnabled": false,
    "vnetImagePullEnabled": false,
    "vnetRouteAllEnabled": false
  }
]
```
</details>
