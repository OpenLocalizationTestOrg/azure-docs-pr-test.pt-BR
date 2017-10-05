---
title: "Implantar um aplicativo em um conjunto de dimensionamento de máquinas virtuais do Azure | Microsoft Docs"
description: "Saiba como implantar um aplicativo de dimensionamento automático simples em um conjunto de dimensionamento de máquinas virtuais usando um modelo do Azure Resource Manager."
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
ms.openlocfilehash: 07883a33382cc660b043c99872312a9e77228253
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="d2467-103">Implantar um aplicativo de dimensionamento automático usando um modelo</span><span class="sxs-lookup"><span data-stu-id="d2467-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="d2467-104">Os [modelos do Azure Resource Manager](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) são uma excelente maneira de implantar grupos de recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="d2467-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way to deploy groups of related resources.</span></span> <span data-ttu-id="d2467-105">Esse tutorial se baseia em [Implantar um conjunto de dimensionamento simples](virtual-machine-scale-sets-mvss-start.md) e descreve como implantar um aplicativo de dimensionamento automático simples em um conjunto de dimensionamento usando um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="d2467-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how to deploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="d2467-106">Também é possível configurar o dimensionamento automático usando o PowerShell, a CLI ou o portal.</span><span class="sxs-lookup"><span data-stu-id="d2467-106">You can also set up autoscaling using PowerShell, CLI, or the portal.</span></span> <span data-ttu-id="d2467-107">Para obter mais informações, consulte [Visão geral do dimensionamento automático](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="d2467-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="d2467-108">Dois modelos de início rápido</span><span class="sxs-lookup"><span data-stu-id="d2467-108">Two quickstart templates</span></span>
<span data-ttu-id="d2467-109">Quando você implanta um conjunto de dimensionamento, você pode instalar um novo software em uma imagem de plataforma usando uma [Extensão de VM](../virtual-machines/virtual-machines-windows-extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="d2467-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="d2467-110">Uma extensão de VM do Azure é um pequeno aplicativo que fornece tarefas de configuração e automação pós-implantação nas máquinas virtuais do Azure, tais como implantar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2467-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="d2467-111">Dois modelos diferentes de exemplo são fornecidos em [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates), que mostram como implantar um aplicativo de dimensionamento automático em um conjunto de dimensionamento usando extensões de VM.</span><span class="sxs-lookup"><span data-stu-id="d2467-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how to deploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="d2467-112">Servidor HTTP do Python em Linux</span><span class="sxs-lookup"><span data-stu-id="d2467-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="d2467-113">O modelo de exemplo do [servidor HTTP do Python em Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) implanta um aplicativo de dimensionamento automático simples em execução em um conjunto de dimensionamento do Linux.</span><span class="sxs-lookup"><span data-stu-id="d2467-113">The [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="d2467-114">O [Bottle](http://bottlepy.org/docs/dev/), uma estrutura da Web Python e um servidor HTTP simples são implantados em cada VM no conjunto de dimensionamento usando uma extensão de VM de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="d2467-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in the scale set using a custom script VM extension.</span></span> <span data-ttu-id="d2467-115">O conjunto de dimensionamento escala verticalmente quando a utilização média da CPU em todas as VMs é maior que 60% e reduz verticalmente quando a utilização média da CPU é menor que 30%.</span><span class="sxs-lookup"><span data-stu-id="d2467-115">The scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when the average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="d2467-116">Além do recurso de conjunto de dimensionamento, o modelo de exemplo *azuredeploy.json* também declara endereço IP público, rede virtual, balanceador de carga e recursos de configurações de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="d2467-116">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="d2467-117">Para obter mais informações sobre como criar esses recursos em um modelo, consulte [Conjunto de dimensionamento Linux com dimensionamento automático](virtual-machine-scale-sets-linux-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="d2467-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="d2467-118">No modelo *azuredeploy.json*, a propriedade `extensionProfile` do recurso `Microsoft.Compute/virtualMachineScaleSets` especifica uma extensão de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="d2467-118">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="d2467-119">`fileUris` especifica o local dos scripts.</span><span class="sxs-lookup"><span data-stu-id="d2467-119">`fileUris` specifies the script(s) location.</span></span> <span data-ttu-id="d2467-120">Nesse caso, são dois arquivos: *workserver.py*, que define um servidor HTTP simples e *installserver.sh*, que instala o Bottle e inicia o servidor HTTP.</span><span class="sxs-lookup"><span data-stu-id="d2467-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts the HTTP server.</span></span> <span data-ttu-id="d2467-121">`commandToExecute` especifica o comando a ser executado depois que o conjunto de dimensionamento tiver sido implantado.</span><span class="sxs-lookup"><span data-stu-id="d2467-121">`commandToExecute` specifies the command to run after the scale set has been deployed.</span></span>

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

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="d2467-122">Aplicativo ASP.NET MVC no Windows</span><span class="sxs-lookup"><span data-stu-id="d2467-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="d2467-123">O modelo de exemplo do [aplicativo ASP.NET MVC no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) implanta um aplicativo simples do ASP.NET MVC em execução no IIS no conjunto de dimensionamento do Windows.</span><span class="sxs-lookup"><span data-stu-id="d2467-123">The [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="d2467-124">O IIS e o aplicativo MVC são implantados usando a extensão de VM de [DSC (configuração de estado desejado) do PowerShell](virtual-machine-scale-sets-dsc.md).</span><span class="sxs-lookup"><span data-stu-id="d2467-124">IIS and the MVC app are deployed using the [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="d2467-125">O conjunto de dimensionamento escala verticalmente (uma instância VM por vez) quando a utilização de CPU é maior que 50% por 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="d2467-125">The scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="d2467-126">Além do recurso de conjunto de dimensionamento, o modelo de exemplo *azuredeploy.json* também declara endereço IP público, rede virtual, balanceador de carga e recursos de configurações de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="d2467-126">In addition to the scale set resource, the *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="d2467-127">Esse modelo também demonstra a atualização de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="d2467-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="d2467-128">Para obter mais informações sobre como criar esses recursos em um modelo, consulte [Conjunto de dimensionamento Windows com dimensionamento automático](virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="d2467-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="d2467-129">No modelo *azuredeploy.json*, a propriedade `extensionProfile` do recurso `Microsoft.Compute/virtualMachineScaleSets` especifica uma extensão de [DSC (configuração de estado desejado)](virtual-machine-scale-sets-dsc.md) que instala o IIS e um aplicativo Web padrão de um pacote WebDeploy.</span><span class="sxs-lookup"><span data-stu-id="d2467-129">In the *azuredeploy.json* template, the `extensionProfile` property of the `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="d2467-130">O script *IISInstall.ps1* instala o IIS na máquina virtual e é encontrado na pasta *DSC*.</span><span class="sxs-lookup"><span data-stu-id="d2467-130">The *IISInstall.ps1* script installs IIS on the virtual machine and is found in the *DSC* folder.</span></span>  <span data-ttu-id="d2467-131">O aplicativo Web MVC é encontrado na pasta *WebDeploy*.</span><span class="sxs-lookup"><span data-stu-id="d2467-131">The MVC web app is found in the *WebDeploy* folder.</span></span>  <span data-ttu-id="d2467-132">Os caminhos para o script de instalação e o aplicativo Web são definidos nos parâmetros `powershelldscZip` e `webDeployPackage` do arquivo *azuredeploy.parameters.json*.</span><span class="sxs-lookup"><span data-stu-id="d2467-132">The paths to the install script and the web app are defined in the `powershelldscZip` and `webDeployPackage` parameters in the *azuredeploy.parameters.json* file.</span></span> 

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

## <a name="deploy-the-template"></a><span data-ttu-id="d2467-133">Implantar o modelo</span><span class="sxs-lookup"><span data-stu-id="d2467-133">Deploy the template</span></span>
<span data-ttu-id="d2467-134">A maneira mais simples de implantar o modelo [Servidor HTTP do Python em Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [Aplicativo ASP.NET MVC no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) é usar o botão **Implantar no Azure** encontrado na nos arquivos Leiame no GitHub.</span><span class="sxs-lookup"><span data-stu-id="d2467-134">The simplest way to deploy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is to use the **Deploy to Azure** button found in the in the readme files in GitHub.</span></span>  <span data-ttu-id="d2467-135">Você também pode usar o PowerShell ou a CLI do Azure para implantar os modelos de exemplo.</span><span class="sxs-lookup"><span data-stu-id="d2467-135">You can also use PowerShell or Azure CLI to deploy the sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="d2467-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d2467-136">PowerShell</span></span>
<span data-ttu-id="d2467-137">Copie os arquivos do [Servidor HTTP do Python em Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [Aplicativo ASP.NET MVC no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) do repositório do GitHub para uma pasta no computador local.</span><span class="sxs-lookup"><span data-stu-id="d2467-137">Copy the [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from the GitHub repo to a folder on your local computer.</span></span>  <span data-ttu-id="d2467-138">Abra o arquivo *azuredeploy.parameters.json* e atualize os valores padrão dos parâmetros `vmssName`, `adminUsername` e `adminPassword`.</span><span class="sxs-lookup"><span data-stu-id="d2467-138">Open the *azuredeploy.parameters.json* file and update the default values of the `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="d2467-139">Salve o script do PowerShell a seguir em *deploy. ps1* na mesma pasta do modelo *azuredeploy.json*.</span><span class="sxs-lookup"><span data-stu-id="d2467-139">Save the following PowerShell script to *deploy.ps1* in the same folder as the *azuredeploy.json* template.</span></span> <span data-ttu-id="d2467-140">Para implantar o modelo de exemplo, execute o script *deploy.ps1* de uma janela de comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="d2467-140">To deploy the sample template run the *deploy.ps1* script from a PowerShell command window.</span></span>

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
    Write-Host "Resource group '$resourceGroupName' does not exist. To create a new resource group, please enter a location.";
    if(!$resourceGroupLocation) {
        $resourceGroupLocation = Read-Host "resourceGroupLocation";
    }
    Write-Host "Creating resource group '$resourceGroupName' in location '$resourceGroupLocation'";
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else{
    Write-Host "Using existing resource group '$resourceGroupName'";
}

# Start the deployment
Write-Host "Starting deployment...";
if(Test-Path $parametersFilePath) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath -TemplateParameterFile $parametersFilePath;
} else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $resourceGroupName -TemplateFile $templateFilePath;
}
```

### <a name="azure-cli"></a><span data-ttu-id="d2467-141">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d2467-141">Azure CLI</span></span>
```azurecli
#!/bin/bash
set -euo pipefail
IFS=$'\n\t'

# -e: immediately exit if any command has a non-zero exit status
# -o: prevents errors in a pipeline from being masked
# IFS new value is less likely to cause confusing bugs when looping arrays or arguments (e.g. $@)

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
    echo "Enter a location below to create a new resource group else skip this"
    echo "ResourceGroupLocation:"
    read resourceGroupLocation
fi

#templateFile Path - template file to be used
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

#login to azure using your credentials
az account show 1> /dev/null

if [ $? != 0 ];
then
    az login
fi

#set the default subscription id
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

## <a name="next-steps"></a><span data-ttu-id="d2467-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d2467-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
