---
title: aaaAzure exemplo de Script do PowerShell - implantar modelo | Microsoft Docs
description: Script de exemplo para implantar um modelo do Azure Resource Manager.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 04/19/2017
ms.author: tomfitz
ms.openlocfilehash: 536b8ccecad4ed8a4c4a4139c6bf4600e2eb9405
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-resource-manager-template-deployment---powershell-script"></a><span data-ttu-id="e2ae6-103">Implantação do Azure Resource Manager - script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="e2ae6-103">Azure Resource Manager template deployment - PowerShell script</span></span>

<span data-ttu-id="e2ae6-104">Esse script implanta um grupo de recursos de tooa de modelo do Gerenciador de recursos em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="e2ae6-104">This script deploys a Resource Manager template tooa resource group in your subscription.</span></span>

[!INCLUDE [sample-powershell-install](../../includes/sample-powershell-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a><span data-ttu-id="e2ae6-105">Script de exemplo</span><span class="sxs-lookup"><span data-stu-id="e2ae6-105">Sample script</span></span>

```powershell
<#
 .SYNOPSIS
    Deploys a template tooAzure

 .DESCRIPTION
    Deploys an Azure Resource Manager template
#>

param (
    [Parameter(Mandatory)]
    #hello subscription id where hello template will be deployed.
    [string]$SubscriptionId,  

    [Parameter(Mandatory)]
    #hello resource group where hello template will be deployed. Can be hello name of an existing or a new resource group.
    [string]$ResourceGroupName, 

    #Optional, a resource group location. If specified, will try toocreate a new resource group in this location. If not specified, assumes resource group is existing.
    [string]$ResourceGroupLocation, 

    #hello deployment name.
    [Parameter(Mandatory)]
    [string]$DeploymentName,    

    #Path toohello template file. Defaults tootemplate.json.
    [string]$TemplateFilePath = "template.json",  

    #Path toohello parameters file. Defaults tooparameters.json. If file is not found, will prompt for parameter values based on template.
    [string]$ParametersFilePath = "parameters.json"
)

$ErrorActionPreference = "Stop"

# Login tooAzure and select subscription
Write-Output "Logging in"
Login-AzureRmAccount
Write-Output "Selecting subscription '$SubscriptionId'"
Select-AzureRmSubscription -SubscriptionID $SubscriptionId

# Create or check for existing resource group
$resourceGroup = Get-AzureRmResourceGroup -Name $ResourceGroupName -ErrorAction SilentlyContinue
if ( -not $ResourceGroup ) {
    Write-Output "Could not find resource group '$ResourceGroupName' - will create it"
    if ( -not $ResourceGroupLocation ) {
        $ResourceGroupLocation = Read-Host -Prompt 'Enter location for resource group'
    }
    Write-Output "Creating resource group '$ResourceGroupName' in location '$ResourceGroupLocation'"
    New-AzureRmResourceGroup -Name $resourceGroupName -Location $resourceGroupLocation
}
else {
    Write-Output "Using existing resource group '$ResourceGroupName'"
}

# Start hello deployment
Write-Output "Starting deployment"
if ( Test-Path $ParametersFilePath ) {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath -TemplateParameterFile $ParametersFilePath
}
else {
    New-AzureRmResourceGroupDeployment -ResourceGroupName $ResourceGroupName -TemplateFile $TemplateFilePath
}
``` 

## <a name="clean-up-deployment"></a><span data-ttu-id="e2ae6-106">Limpar implantação</span><span class="sxs-lookup"><span data-stu-id="e2ae6-106">Clean up deployment</span></span> 

<span data-ttu-id="e2ae6-107">Comando a seguir de execução Olá tooremove grupo de recursos de saudação e todos os seus recursos.</span><span class="sxs-lookup"><span data-stu-id="e2ae6-107">Run hello following command tooremove hello resource group and all its resources.</span></span>

```powershell
Remove-AzureRmResourceGroup -Name myResourceGroup
```

## <a name="script-explanation"></a><span data-ttu-id="e2ae6-108">Explicação sobre o script</span><span class="sxs-lookup"><span data-stu-id="e2ae6-108">Script explanation</span></span>

<span data-ttu-id="e2ae6-109">Esse script usa Olá implantação de saudação toocreate comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="e2ae6-109">This script uses hello following commands toocreate hello deployment.</span></span> <span data-ttu-id="e2ae6-110">Cada item na tabela de saudação vincula a documentação específica do toocommand.</span><span class="sxs-lookup"><span data-stu-id="e2ae6-110">Each item in hello table links toocommand specific documentation.</span></span>

| <span data-ttu-id="e2ae6-111">Command</span><span class="sxs-lookup"><span data-stu-id="e2ae6-111">Command</span></span> | <span data-ttu-id="e2ae6-112">Observações</span><span class="sxs-lookup"><span data-stu-id="e2ae6-112">Notes</span></span> |
|---|---|
| [<span data-ttu-id="e2ae6-113">Register-AzureRmResourceProvider</span><span class="sxs-lookup"><span data-stu-id="e2ae6-113">Register-AzureRmResourceProvider</span></span>](/powershell/module/azurerm.resources/register-azurermresourceprovider) | <span data-ttu-id="e2ae6-114">Registra um provedor de recursos para que seus tipos de recursos podem ser implantado tooyour assinatura.</span><span class="sxs-lookup"><span data-stu-id="e2ae6-114">Registers a resource provider so its resource types can be deployed tooyour subscription.</span></span>  |
| [<span data-ttu-id="e2ae6-115">Get-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e2ae6-115">Get-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/get-azurermresourcegroup) | <span data-ttu-id="e2ae6-116">Utiliza grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="e2ae6-116">Gets resource groups.</span></span>  |
| [<span data-ttu-id="e2ae6-117">New-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e2ae6-117">New-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroup) | <span data-ttu-id="e2ae6-118">Cria um grupo de recursos no qual todos os recursos são armazenados.</span><span class="sxs-lookup"><span data-stu-id="e2ae6-118">Creates a resource group in which all resources are stored.</span></span> |
| [<span data-ttu-id="e2ae6-119">New-AzureRmResourceGroupDeployment</span><span class="sxs-lookup"><span data-stu-id="e2ae6-119">New-AzureRmResourceGroupDeployment</span></span>](/powershell/module/azurerm.resources/new-azurermresourcegroupdeployment) | <span data-ttu-id="e2ae6-120">Adiciona um grupo de recursos de tooa de implantação do Azure.</span><span class="sxs-lookup"><span data-stu-id="e2ae6-120">Adds an Azure deployment tooa resource group.</span></span>  |
| [<span data-ttu-id="e2ae6-121">Remove-AzureRmResourceGroup</span><span class="sxs-lookup"><span data-stu-id="e2ae6-121">Remove-AzureRmResourceGroup</span></span>](/powershell/module/azurerm.resources/remove-azurermresourcegroup) | <span data-ttu-id="e2ae6-122">Remove um grupo de recursos e todos os recursos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="e2ae6-122">Removes a resource group and all resources contained within.</span></span> |



## <a name="next-steps"></a><span data-ttu-id="e2ae6-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e2ae6-123">Next steps</span></span>
* <span data-ttu-id="e2ae6-124">Para modelos de toodeploying uma introdução, consulte [implantar recursos com modelos do Gerenciador de recursos e o Azure PowerShell](resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="e2ae6-124">For an introduction toodeploying templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](resource-group-template-deploy.md).</span></span>
* <span data-ttu-id="e2ae6-125">Para obter mais informações sobre a implantação de um modelo que exija um token SAS, veja [Implantar modelo particular com o token SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="e2ae6-125">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
* <span data-ttu-id="e2ae6-126">parâmetros de toodefine no modelo, consulte [criar modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="e2ae6-126">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="e2ae6-127">Para obter diretrizes sobre como as empresas podem usar o Gerenciador de recursos tooeffectively gerenciar assinaturas, consulte [scaffold enterprise do Azure - controle de assinatura prescritivas](resource-manager-subscription-governance.md).</span><span class="sxs-lookup"><span data-stu-id="e2ae6-127">For guidance on how enterprises can use Resource Manager tooeffectively manage subscriptions, see [Azure enterprise scaffold - prescriptive subscription governance](resource-manager-subscription-governance.md).</span></span>

