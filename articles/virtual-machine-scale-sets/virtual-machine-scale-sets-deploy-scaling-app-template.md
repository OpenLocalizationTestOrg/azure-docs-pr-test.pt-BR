---
title: "aaaDeploy um aplicativo em um conjunto de escala de máquina virtual do Azure | Microsoft Docs"
description: "Saiba toodeploy um aplicativo de dimensionamento automático simples em uma escala de máquina virtual definido usando um modelo do Gerenciador de recursos do Azure."
services: virtual-machine-scale-sets
documentationcenter: 
author: rwike77
manager: timlt
editor: 
tags: azure-resource-manager
ms.assetid: 
ms.service: virtual-machine-scale-sets
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 08/24/2017
ms.author: ryanwi
ms.openlocfilehash: 6fccc310312cabfcdddfcbcd2d154fc5cc440417
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a>Implantar um aplicativo de dimensionamento automático usando um modelo

[Modelos do Gerenciador de recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) é uma ótima maneira toodeploy grupos de recursos relacionados. Este tutorial baseia-se [implantar um conjunto de escala simples](virtual-machine-scale-sets-mvss-start.md) e descreve como toodeploy um aplicativo de dimensionamento automático simples em uma escala definidas usando um modelo do Gerenciador de recursos do Azure.  Você também pode configurar usando o PowerShell, CLI ou o portal de saudação de dimensionamento automático. Para obter mais informações, consulte [Visão geral do dimensionamento automático](virtual-machine-scale-sets-autoscale-overview.md).

## <a name="two-quickstart-templates"></a>Dois modelos de início rápido
Quando você implanta um conjunto de dimensionamento, você pode instalar um novo software em uma imagem de plataforma usando uma [Extensão de VM](../virtual-machines/virtual-machines-windows-extensions-features.md). Uma extensão de VM do Azure é um pequeno aplicativo que fornece tarefas de configuração e automação pós-implantação nas máquinas virtuais do Azure, tais como implantar um aplicativo. Dois modelos diferentes de exemplo são fornecidos no [Azure/azure-quickstart-modelos](https://github.com/Azure/azure-quickstart-templates) que mostram como toodeploy um aplicativo de dimensionamento automático em uma escala definidas usando extensões de VM.

### <a name="python-http-server-on-linux"></a>Servidor HTTP do Python em Linux
Olá [servidor HTTP Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) modelo implanta um aplicativo de dimensionamento automático simples em execução em um conjunto de escala do Linux.  [Garrafa](http://bottlepy.org/docs/dev/), uma estrutura da web do Python e um servidor HTTP simples são implantados em cada VM em escala Olá definida usando um script personalizado extensão de VM. escala de saudação configurar escalas quando a utilização média da CPU em todas as máquinas virtuais é maior que 60% e pode ser dimensionado para baixo quando Olá utilização média da CPU é menos de 30%.

Além disso toohello conjunto de escala de recurso, hello *azuredeploy.json* modelo de exemplo também declara a rede virtual, o endereço IP público, o balanceador de carga e recursos de configurações de dimensionamento automático.  Para obter mais informações sobre como criar esses recursos em um modelo, consulte [Conjunto de dimensionamento Linux com dimensionamento automático](virtual-machine-scale-sets-linux-autoscale.md).

Em Olá *azuredeploy.json* modelo, Olá `extensionProfile` propriedade Olá `Microsoft.Compute/virtualMachineScaleSets` recurso Especifica uma extensão de script personalizado. `fileUris`Especifica o local de script(s) hello. Nesse caso, dois arquivos: *workserver.py*, que define um servidor HTTP simples, e *installserver.sh*, que instala garrafa e inicia Olá servidor HTTP. `commandToExecute`Especifica a saudação comando toorun após a implantação do conjunto de escala de saudação.

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "lapextension",
                "properties": {
                  "publisher": "Microsoft.Azure.Extensions",
                  "type": "CustomScript",
                  "typeHandlerVersion": "2.0",
                  "autoUpgradeMinorVersion": true,
                  "settings": {
                    "fileUris": [
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/installserver.sh",
                      "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/201-vmss-bottle-autoscale/workserver.py"
                    ],
                    "commandToExecute": "bash installserver.sh"
                  }
                }
              }
            ]
          }
```

### <a name="aspnet-mvc-application-on-windows"></a>Aplicativo ASP.NET MVC no Windows
Olá [aplicativo ASP.NET MVC no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modelo implanta um aplicativo ASP.NET MVC simples em execução no IIS no conjunto de escala do Windows.  O IIS e hello aplicativo MVC são implantados usando Olá [(DSC) de configuração de estado desejado do PowerShell](virtual-machine-scale-sets-dsc.md) extensão da VM.  escala de saudação configurar escalas (na instância VM por vez) quando a utilização da CPU é maior que 50% para 5 minutos. 

Além disso toohello conjunto de escala de recurso, hello *azuredeploy.json* modelo de exemplo também declara a rede virtual, o endereço IP público, o balanceador de carga e recursos de configurações de dimensionamento automático. Esse modelo também demonstra a atualização de aplicativo.  Para obter mais informações sobre como criar esses recursos em um modelo, consulte [Conjunto de dimensionamento Windows com dimensionamento automático](virtual-machine-scale-sets-windows-autoscale.md).

Em Olá *azuredeploy.json* modelo, Olá `extensionProfile` propriedade Olá `Microsoft.Compute/virtualMachineScaleSets` recurso Especifica um [configuração de estado desejado (DSC)](virtual-machine-scale-sets-dsc.md) extensão que instala o IIS e um padrão aplicativo Web de um pacote de WebDeploy.  Olá *IISInstall.ps1* script instala o IIS na máquina virtual de saudação e é encontrado em Olá *DSC* pasta.  aplicativo de web MVC Olá foi encontrado no hello *WebDeploy* pasta.  script de instalação do Hello caminhos toohello e aplicativo web de saudação são definidos no hello `powershelldscZip` e `webDeployPackage` parâmetros em Olá *azuredeploy.parameters.json* arquivo. 

```json
          "extensionProfile": {
            "extensions": [
              {
                "name": "Microsoft.Powershell.DSC",
                "properties": {
                  "publisher": "Microsoft.Powershell",
                  "type": "DSC",
                  "typeHandlerVersion": "2.9",
                  "autoUpgradeMinorVersion": true,
                  "forceUpdateTag": "[parameters('powershelldscUpdateTagVersion')]",
                  "settings": {
                    "configuration": {
                      "url": "[variables('powershelldscZipFullPath')]",
                      "script": "IISInstall.ps1",
                      "function": "InstallIIS"
                    },
                    "configurationArguments": {
                      "nodeName": "localhost",
                      "WebDeployPackagePath": "[variables('webDeployPackageFullPath')]"
                    }
                  }
                }
              }
            ]
          }
```

## <a name="deploy-hello-template"></a>Implante o modelo de saudação
Olá Olá toodeploy da maneira mais simples [servidor HTTP Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [aplicativo ASP.NET MVC no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modelo é Olá toouse **implantar tooAzure** botão encontrado em Olá nos arquivos Leiame de saudação no GitHub.  Você também pode usar modelos de exemplo do PowerShell ou CLI do Azure toodeploy hello.

### <a name="powershell"></a>PowerShell
Saudação de cópia [servidor HTTP Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [aplicativo ASP.NET MVC no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) arquivos Olá GitHub repositório tooa pasta no computador local.  Olá abrir *azuredeploy.parameters.json* arquivo e atualização valores de padrão de saudação do hello `vmssName`, `adminUsername`, e `adminPassword` parâmetros. Salvar Olá script do PowerShell a seguir muito*deploy.ps1* em Olá mesma pasta Olá *azuredeploy.json* modelo. saudação de modelo executar toodeploy Olá exemplo *deploy.ps1* script a partir de uma janela de comando do PowerShell.

```powershell
param(
 [Parameter(Mandatory=$True)]
 [string]
 $subscriptionId,

 [Parameter(Mandatory=$True)]
 [string]
 $resourceGroupName,

 [string]
 $resourceGroupLocation,

 [Parameter(Mandatory=$True)]
 [string]
 $deploymentName,

 [string]
 $templateFilePath = "template.json",

 [string]
 $parametersFilePath = "parameters.json"
)

<#
.SYNOPSIS
    Registers RPs
#>
Function RegisterRP {
    Param(
        [string]$ResourceProviderNamespace
    )

    Write-Host "Registering resource provider '$ResourceProviderNamespace'";
    Register-AzureRmResourceProvider -ProviderNamespace $ResourceProviderNamespace;
}

#******************************************************************************
# Script body
# Execution begins here
#******************************************************************************
$ErrorActionPreference = "Stop"

# sign in
Write-Host "Logging in...";
Login-AzureRmAccount;

# select subscription
Write-Host "Selecting subscription '$subscriptionId'";
Select-AzureRmSubscription -SubscriptionID $subscriptionId;

# Register RPs
$resourceProviders = @("microsoft.compute","microsoft.insights","microsoft.network");
if($resourceProviders.length) {
    Write-Host "Registering resource providers"
    foreach($resourceProvider in $resourceProviders) {
        RegisterRP($resourceProvider);
    }
}

#Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $resourceGroupName -ErrorAction SilentlyContinue
if(!$resourceGroup)
{
    Write-Host "Resource group '$resourceGroupName' does not exist. toocreate a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start hello deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a>CLI do Azure
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely toocause confusing bugs when looping arrays or arguments (e.g. $@)

usage() { echo "Usage: $0 -i <subscriptionId> -g <resourceGroupName> -n <deploymentName> -l <resourceGroupLocation>" 1>&2; exit 1; }

declare subscriptionId=""
declare resourceGroupName=""
declare deploymentName=""
declare resourceGroupLocation=""

# Initialize parameters specified from command line
while getopts ":i:g:n:l:" arg; do
    case "${arg}" in
        i)
            subscriptionId=${OPTARG}
            ;;
        g)
            resourceGroupName=${OPTARG}
            ;;
        n)
            deploymentName=${OPTARG}
            ;;
        l)
            resourceGroupLocation=${OPTARG}
            ;;
        esac
done
shift $((OPTIND-1))

#Prompt for parameters is some required parameters are missing
if [[ -z "$subscriptionId" ]]; then
    echo "Subscription Id:"
    read subscriptionId
    [[ "${subscriptionId:?}" ]]
fi

if [[ -z "$resourceGroupName" ]]; then
    echo "ResourceGroupName:"
    read resourceGroupName
    [[ "${resourceGroupName:?}" ]]
fi

if [[ -z "$deploymentName" ]]; then
    echo "DeploymentName:"
    read deploymentName
fi

if [[ -z "$resourceGroupLocation" ]]; then
    echo "Enter a location below toocreate a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file toobe used
templateFilePath="template.json"

if [ ! -f "$templateFilePath" ]; then
    echo "$templateFilePath not found"
    exit 1
fi

#parameter file path
parametersFilePath="parameters.json"

if [ ! -f "$parametersFilePath" ]; then
    echo "$parametersFilePath not found"
    exit 1
fi

if [ -z "$subscriptionId" ] || [ -z "$resourceGroupName" ] || [ -z "$deploymentName" ]; then
    echo "Either one of subscriptionId, resourceGroupName, deploymentName is empty"
    usage
fi

#login tooazure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set hello default subscription id
az account set --name $subscriptionId

set +e

#Check for existing RG
az group show $resourceGroupName 1> /dev/null

if [ $? != 0 ]; then
    echo "Resource group with name" $resourceGroupName "could not be found. Creating new resource group.."
    set -e
    (
        set -x
        az group create --name $resourceGroupName --location $resourceGroupLocation 1> /dev/null
    )
    else
    echo "Using existing resource group..."
fi

#Start deployment
echo "Starting deployment..."
(
    set -x
    az group deployment create --name $deploymentName --resource-group $resourceGroupName --template-file $templateFilePath --parameters $parametersFilePath
)

if [ $?  == 0 ];
 then
    echo "Template has been successfully deployed"
fi
```

## <a name="next-steps"></a>Próximas etapas

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
