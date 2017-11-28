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
# <a name="deploy-an-autoscaling-app-using-a-template"></a><span data-ttu-id="f1408-103">Implantar um aplicativo de dimensionamento automático usando um modelo</span><span class="sxs-lookup"><span data-stu-id="f1408-103">Deploy an autoscaling app using a template</span></span>

<span data-ttu-id="f1408-104">[Modelos do Gerenciador de recursos do Azure](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) é uma ótima maneira toodeploy grupos de recursos relacionados.</span><span class="sxs-lookup"><span data-stu-id="f1408-104">[Azure Resource Manager templates](https://docs.microsoft.com/azure/azure-resource-manager/resource-group-overview#template-deployment) are a great way toodeploy groups of related resources.</span></span> <span data-ttu-id="f1408-105">Este tutorial baseia-se [implantar um conjunto de escala simples](virtual-machine-scale-sets-mvss-start.md) e descreve como toodeploy um aplicativo de dimensionamento automático simples em uma escala definidas usando um modelo do Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="f1408-105">This tutorial builds on [Deploy a simple scale set](virtual-machine-scale-sets-mvss-start.md) and describes how toodeploy a simple autoscaling application on a scale set using an Azure Resource Manager template.</span></span>  <span data-ttu-id="f1408-106">Você também pode configurar usando o PowerShell, CLI ou o portal de saudação de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="f1408-106">You can also set up autoscaling using PowerShell, CLI, or hello portal.</span></span> <span data-ttu-id="f1408-107">Para obter mais informações, consulte [Visão geral do dimensionamento automático](virtual-machine-scale-sets-autoscale-overview.md).</span><span class="sxs-lookup"><span data-stu-id="f1408-107">For more information, see [Autoscale overview](virtual-machine-scale-sets-autoscale-overview.md).</span></span>

## <a name="two-quickstart-templates"></a><span data-ttu-id="f1408-108">Dois modelos de início rápido</span><span class="sxs-lookup"><span data-stu-id="f1408-108">Two quickstart templates</span></span>
<span data-ttu-id="f1408-109">Quando você implanta um conjunto de dimensionamento, você pode instalar um novo software em uma imagem de plataforma usando uma [Extensão de VM](../virtual-machines/virtual-machines-windows-extensions-features.md).</span><span class="sxs-lookup"><span data-stu-id="f1408-109">When you deploy a scale set you can install new software on a platform image using a [VM Extension](../virtual-machines/virtual-machines-windows-extensions-features.md).</span></span> <span data-ttu-id="f1408-110">Uma extensão de VM do Azure é um pequeno aplicativo que fornece tarefas de configuração e automação pós-implantação nas máquinas virtuais do Azure, tais como implantar um aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1408-110">A VM extension is a small application that provides post-deployment configuration and automation tasks on Azure virtual machines, such as deploying an app.</span></span> <span data-ttu-id="f1408-111">Dois modelos diferentes de exemplo são fornecidos no [Azure/azure-quickstart-modelos](https://github.com/Azure/azure-quickstart-templates) que mostram como toodeploy um aplicativo de dimensionamento automático em uma escala definidas usando extensões de VM.</span><span class="sxs-lookup"><span data-stu-id="f1408-111">Two different sample templates are provided in [Azure/azure-quickstart-templates](https://github.com/Azure/azure-quickstart-templates) which show how toodeploy an autoscaling application onto a scale set using VM extensions.</span></span>

### <a name="python-http-server-on-linux"></a><span data-ttu-id="f1408-112">Servidor HTTP do Python em Linux</span><span class="sxs-lookup"><span data-stu-id="f1408-112">Python HTTP server on Linux</span></span>
<span data-ttu-id="f1408-113">Olá [servidor HTTP Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) modelo implanta um aplicativo de dimensionamento automático simples em execução em um conjunto de escala do Linux.</span><span class="sxs-lookup"><span data-stu-id="f1408-113">hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) sample template deploys a simple autoscaling application running on a Linux scale set.</span></span>  <span data-ttu-id="f1408-114">[Garrafa](http://bottlepy.org/docs/dev/), uma estrutura da web do Python e um servidor HTTP simples são implantados em cada VM em escala Olá definida usando um script personalizado extensão de VM.</span><span class="sxs-lookup"><span data-stu-id="f1408-114">[Bottle](http://bottlepy.org/docs/dev/), a Python web framework, and a simple HTTP server are deployed on each VM in hello scale set using a custom script VM extension.</span></span> <span data-ttu-id="f1408-115">escala de saudação configurar escalas quando a utilização média da CPU em todas as máquinas virtuais é maior que 60% e pode ser dimensionado para baixo quando Olá utilização média da CPU é menos de 30%.</span><span class="sxs-lookup"><span data-stu-id="f1408-115">hello scale set scales up when average CPU utilization across all VMs is greater than 60% and scales down when hello average CPU utilization is less than 30%.</span></span>

<span data-ttu-id="f1408-116">Além disso toohello conjunto de escala de recurso, hello *azuredeploy.json* modelo de exemplo também declara a rede virtual, o endereço IP público, o balanceador de carga e recursos de configurações de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="f1408-116">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span>  <span data-ttu-id="f1408-117">Para obter mais informações sobre como criar esses recursos em um modelo, consulte [Conjunto de dimensionamento Linux com dimensionamento automático](virtual-machine-scale-sets-linux-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="f1408-117">For more information on creating these resources in a template, see [Linux scale set with autoscale](virtual-machine-scale-sets-linux-autoscale.md).</span></span>

<span data-ttu-id="f1408-118">Em Olá *azuredeploy.json* modelo, Olá `extensionProfile` propriedade Olá `Microsoft.Compute/virtualMachineScaleSets` recurso Especifica uma extensão de script personalizado.</span><span class="sxs-lookup"><span data-stu-id="f1408-118">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a custom script extension.</span></span> <span data-ttu-id="f1408-119">`fileUris`Especifica o local de script(s) hello.</span><span class="sxs-lookup"><span data-stu-id="f1408-119">`fileUris` specifies hello script(s) location.</span></span> <span data-ttu-id="f1408-120">Nesse caso, dois arquivos: *workserver.py*, que define um servidor HTTP simples, e *installserver.sh*, que instala garrafa e inicia Olá servidor HTTP.</span><span class="sxs-lookup"><span data-stu-id="f1408-120">In this case, two files: *workserver.py*, which defines a simple HTTP server, and *installserver.sh*, which installs Bottle and starts hello HTTP server.</span></span> <span data-ttu-id="f1408-121">`commandToExecute`Especifica a saudação comando toorun após a implantação do conjunto de escala de saudação.</span><span class="sxs-lookup"><span data-stu-id="f1408-121">`commandToExecute` specifies hello command toorun after hello scale set has been deployed.</span></span>

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

### <a name="aspnet-mvc-application-on-windows"></a><span data-ttu-id="f1408-122">Aplicativo ASP.NET MVC no Windows</span><span class="sxs-lookup"><span data-stu-id="f1408-122">ASP.NET MVC application on Windows</span></span>
<span data-ttu-id="f1408-123">Olá [aplicativo ASP.NET MVC no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modelo implanta um aplicativo ASP.NET MVC simples em execução no IIS no conjunto de escala do Windows.</span><span class="sxs-lookup"><span data-stu-id="f1408-123">hello [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) sample template deploys a simple ASP.NET MVC app running in IIS on Windows scale set.</span></span>  <span data-ttu-id="f1408-124">O IIS e hello aplicativo MVC são implantados usando Olá [(DSC) de configuração de estado desejado do PowerShell](virtual-machine-scale-sets-dsc.md) extensão da VM.</span><span class="sxs-lookup"><span data-stu-id="f1408-124">IIS and hello MVC app are deployed using hello [PowerShell desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) VM extension.</span></span>  <span data-ttu-id="f1408-125">escala de saudação configurar escalas (na instância VM por vez) quando a utilização da CPU é maior que 50% para 5 minutos.</span><span class="sxs-lookup"><span data-stu-id="f1408-125">hello scale set scales up (on VM instance at a time) when CPU utilization is greater than 50% for 5 minutes.</span></span> 

<span data-ttu-id="f1408-126">Além disso toohello conjunto de escala de recurso, hello *azuredeploy.json* modelo de exemplo também declara a rede virtual, o endereço IP público, o balanceador de carga e recursos de configurações de dimensionamento automático.</span><span class="sxs-lookup"><span data-stu-id="f1408-126">In addition toohello scale set resource, hello *azuredeploy.json* sample template also declares virtual network, public IP address, load balancer, and autoscale settings resources.</span></span> <span data-ttu-id="f1408-127">Esse modelo também demonstra a atualização de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f1408-127">This template also demonstrates application upgrade.</span></span>  <span data-ttu-id="f1408-128">Para obter mais informações sobre como criar esses recursos em um modelo, consulte [Conjunto de dimensionamento Windows com dimensionamento automático](virtual-machine-scale-sets-windows-autoscale.md).</span><span class="sxs-lookup"><span data-stu-id="f1408-128">For more information on creating these resources in a template, see [Windows scale set with autoscale](virtual-machine-scale-sets-windows-autoscale.md).</span></span>

<span data-ttu-id="f1408-129">Em Olá *azuredeploy.json* modelo, Olá `extensionProfile` propriedade Olá `Microsoft.Compute/virtualMachineScaleSets` recurso Especifica um [configuração de estado desejado (DSC)](virtual-machine-scale-sets-dsc.md) extensão que instala o IIS e um padrão aplicativo Web de um pacote de WebDeploy.</span><span class="sxs-lookup"><span data-stu-id="f1408-129">In hello *azuredeploy.json* template, hello `extensionProfile` property of hello `Microsoft.Compute/virtualMachineScaleSets` resource specifies a [desired state configuration (DSC)](virtual-machine-scale-sets-dsc.md) extension which installs IIS and a default web app from a WebDeploy package.</span></span>  <span data-ttu-id="f1408-130">Olá *IISInstall.ps1* script instala o IIS na máquina virtual de saudação e é encontrado em Olá *DSC* pasta.</span><span class="sxs-lookup"><span data-stu-id="f1408-130">hello *IISInstall.ps1* script installs IIS on hello virtual machine and is found in hello *DSC* folder.</span></span>  <span data-ttu-id="f1408-131">aplicativo de web MVC Olá foi encontrado no hello *WebDeploy* pasta.</span><span class="sxs-lookup"><span data-stu-id="f1408-131">hello MVC web app is found in hello *WebDeploy* folder.</span></span>  <span data-ttu-id="f1408-132">script de instalação do Hello caminhos toohello e aplicativo web de saudação são definidos no hello `powershelldscZip` e `webDeployPackage` parâmetros em Olá *azuredeploy.parameters.json* arquivo.</span><span class="sxs-lookup"><span data-stu-id="f1408-132">hello paths toohello install script and hello web app are defined in hello `powershelldscZip` and `webDeployPackage` parameters in hello *azuredeploy.parameters.json* file.</span></span> 

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

## <a name="deploy-hello-template"></a><span data-ttu-id="f1408-133">Implante o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="f1408-133">Deploy hello template</span></span>
<span data-ttu-id="f1408-134">Olá Olá toodeploy da maneira mais simples [servidor HTTP Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [aplicativo ASP.NET MVC no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) modelo é Olá toouse **implantar tooAzure** botão encontrado em Olá nos arquivos Leiame de saudação no GitHub.</span><span class="sxs-lookup"><span data-stu-id="f1408-134">hello simplest way toodeploy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) template is toouse hello **Deploy tooAzure** button found in hello in hello readme files in GitHub.</span></span>  <span data-ttu-id="f1408-135">Você também pode usar modelos de exemplo do PowerShell ou CLI do Azure toodeploy hello.</span><span class="sxs-lookup"><span data-stu-id="f1408-135">You can also use PowerShell or Azure CLI toodeploy hello sample templates.</span></span>

### <a name="powershell"></a><span data-ttu-id="f1408-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="f1408-136">PowerShell</span></span>
<span data-ttu-id="f1408-137">Saudação de cópia [servidor HTTP Python no Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) ou [aplicativo ASP.NET MVC no Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) arquivos Olá GitHub repositório tooa pasta no computador local.</span><span class="sxs-lookup"><span data-stu-id="f1408-137">Copy hello [Python HTTP server on Linux](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-bottle-autoscale) or [ASP.NET MVC application on Windows](https://github.com/Azure/azure-quickstart-templates/tree/master/201-vmss-windows-webapp-dsc-autoscale) files from hello GitHub repo tooa folder on your local computer.</span></span>  <span data-ttu-id="f1408-138">Olá abrir *azuredeploy.parameters.json* arquivo e atualização valores de padrão de saudação do hello `vmssName`, `adminUsername`, e `adminPassword` parâmetros.</span><span class="sxs-lookup"><span data-stu-id="f1408-138">Open hello *azuredeploy.parameters.json* file and update hello default values of hello `vmssName`, `adminUsername`, and `adminPassword` parameters.</span></span> <span data-ttu-id="f1408-139">Salvar Olá script do PowerShell a seguir muito*deploy.ps1* em Olá mesma pasta Olá *azuredeploy.json* modelo.</span><span class="sxs-lookup"><span data-stu-id="f1408-139">Save hello following PowerShell script too*deploy.ps1* in hello same folder as hello *azuredeploy.json* template.</span></span> <span data-ttu-id="f1408-140">saudação de modelo executar toodeploy Olá exemplo *deploy.ps1* script a partir de uma janela de comando do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="f1408-140">toodeploy hello sample template run hello *deploy.ps1* script from a PowerShell command window.</span></span>

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

### <a name="azure-cli"></a><span data-ttu-id="f1408-141">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="f1408-141">Azure CLI</span></span>
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

## <a name="next-steps"></a><span data-ttu-id="f1408-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f1408-142">Next steps</span></span>

[!INCLUDE [mvss-next-steps-include](../../includes/mvss-next-steps.md)]
