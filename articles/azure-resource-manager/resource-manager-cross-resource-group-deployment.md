---
title: "Implantar recursos do Azure em vários grupos de recursos | Microsoft Docs"
description: "Mostra como escolher mais de um grupo de recursos do Azure durante a implantação."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: tomfitz
ms.openlocfilehash: d8b041213b269775175a810e585103d3c538557f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="deploy-azure-resources-to-more-than-one-resource-group"></a><span data-ttu-id="2511b-103">Implantar recursos do Azure em mais de um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2511b-103">Deploy Azure resources to more than one resource group</span></span>

<span data-ttu-id="2511b-104">Normalmente, você deve implantar todos os recursos em seu modelo em um único grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2511b-104">Typically, you deploy all the resources in your template to a single resource group.</span></span> <span data-ttu-id="2511b-105">No entanto, há situações em que você deseja implantar um conjunto de recursos juntos, mas colocá-los em grupos de recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="2511b-105">However, there are scenarios where you want to deploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="2511b-106">Por exemplo, você talvez queira implantar a máquina virtual de backup do Azure Site Recovery para um local e um grupo de recursos separados.</span><span class="sxs-lookup"><span data-stu-id="2511b-106">For example, you may want to deploy the backup virtual machine for Azure Site Recovery to a separate resource group and location.</span></span> <span data-ttu-id="2511b-107">O Resource Manager permite que você use modelos aninhados para grupos de recursos diferentes do grupo de recursos usado no modelo pai.</span><span class="sxs-lookup"><span data-stu-id="2511b-107">Resource Manager enables you to use nested templates to target different resource groups than the resource group used for the parent template.</span></span>

<span data-ttu-id="2511b-108">O grupo de recursos é o contêiner de ciclo de vida do aplicativo e de sua coleção de recursos.</span><span class="sxs-lookup"><span data-stu-id="2511b-108">The resource group is the lifecycle container for the application and its collection of resources.</span></span> <span data-ttu-id="2511b-109">Crie o grupo de recursos fora do modelo e especifique o grupo de recursos de destino durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="2511b-109">You create the resource group outside of the template, and specify the resource group to target during deployment.</span></span> <span data-ttu-id="2511b-110">Para obter uma introdução sobre grupos de recursos, confira [Visão geral do Azure Resource Manager](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2511b-110">For an introduction to resource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="2511b-111">Modelo de exemplo</span><span class="sxs-lookup"><span data-stu-id="2511b-111">Example template</span></span>

<span data-ttu-id="2511b-112">Para buscar um recurso diferente, você deve usar um modelo aninhado ou vinculado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="2511b-112">To target a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="2511b-113">O tipo de recurso `Microsoft.Resources/deployments` fornece um parâmetro `resourceGroup` que permite que você especifique um grupo de recursos diferente para a implantação aninhada.</span><span class="sxs-lookup"><span data-stu-id="2511b-113">The `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you to specify a different resource group for the nested deployment.</span></span> <span data-ttu-id="2511b-114">Todos os grupos de recursos devem existir antes da execução da implantação.</span><span class="sxs-lookup"><span data-stu-id="2511b-114">All the resource groups must exist before running the deployment.</span></span> <span data-ttu-id="2511b-115">O exemplo a seguir implanta duas contas de armazenamento: uma no grupo de recursos especificado durante a implantação e outra em um grupo de recursos denominado `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="2511b-115">The following example deploys two storage accounts - one in the resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "StorageAccountName1": {
            "type": "string"
        },
        "StorageAccountName2": {
            "type": "string"
        }
    },
    "variables": {},
    "resources": [
        {
            "apiVersion": "2017-05-10",
            "name": "nestedTemplate",
            "type": "Microsoft.Resources/deployments",
            "resourceGroup": "crossResourceGroupDeployment",
            "properties": {
                "mode": "Incremental",
                "template": {
                    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
                    "contentVersion": "1.0.0.0",
                    "parameters": {},
                    "variables": {},
                    "resources": [
                        {
                            "type": "Microsoft.Storage/storageAccounts",
                            "name": "[parameters('StorageAccountName2')]",
                            "apiVersion": "2015-06-15",
                            "location": "West US",
                            "properties": {
                                "accountType": "Standard_LRS"
                            }
                        }
                    ]
                },
                "parameters": {}
            }
        },
        {
            "type": "Microsoft.Storage/storageAccounts",
            "name": "[parameters('StorageAccountName1')]",
            "apiVersion": "2015-06-15",
            "location": "West US",
            "properties": {
                "accountType": "Standard_LRS"
            }
        }
    ]
}
```

<span data-ttu-id="2511b-116">Se você definir `resourceGroup` como o nome de um grupo de recursos que não existe, a implantação falhará.</span><span class="sxs-lookup"><span data-stu-id="2511b-116">If you set `resourceGroup` to the name of a resource group that does not exist, the deployment fails.</span></span> <span data-ttu-id="2511b-117">Se você não fornecer um valor para `resourceGroup`, o Resource Manager usará o grupo de recursos pai.</span><span class="sxs-lookup"><span data-stu-id="2511b-117">If you do not provide a value for `resourceGroup`, Resource Manager uses the parent resource group.</span></span>  

## <a name="deploy-the-template"></a><span data-ttu-id="2511b-118">Implantar o modelo</span><span class="sxs-lookup"><span data-stu-id="2511b-118">Deploy the template</span></span>

<span data-ttu-id="2511b-119">Para implantar o modelo de exemplo, você poderá usar o portal, o Azure PowerShell ou a CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="2511b-119">To deploy the example template, you can use the portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="2511b-120">Para o Azure PowerShell ou a CLI do Azure, você pode usar uma versão de maio de 2017 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="2511b-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="2511b-121">Os exemplos pressupõem que você salvou o modelo localmente como um arquivo denominado **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="2511b-121">The examples assume you have saved the template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="2511b-122">Para o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="2511b-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="2511b-123">Para a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="2511b-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="2511b-124">Após a implantação ser concluída, você verá dois grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="2511b-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="2511b-125">Cada grupo de recursos contém uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2511b-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="2511b-126">Use a função resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="2511b-126">Use resourceGroup() function</span></span>

<span data-ttu-id="2511b-127">Para a implantações de grupos de recursos cruzados, a [função resouceGroup()](resource-group-template-functions-resource.md#resourcegroup) é resolvida de forma diferente com base em como você especifica o modelo aninhado.</span><span class="sxs-lookup"><span data-stu-id="2511b-127">For cross resource group deployments, the [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify the nested template.</span></span> 

<span data-ttu-id="2511b-128">Se você inserir um modelo dentro de outro modelo, a resouceGroup() no modelo aninhado será resolvida para o grupo de recursos pai.</span><span class="sxs-lookup"><span data-stu-id="2511b-128">If you embed one template within another template, resouceGroup() in the nested template resolves to the parent resource group.</span></span> <span data-ttu-id="2511b-129">Um modelo incorporado usa o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="2511b-129">An embedded template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers to parent resource group
    }
}
```

<span data-ttu-id="2511b-130">Se você vincular a um modelo separado, a resouceGroup() no modelo vinculado será resolvida para o grupo de recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="2511b-130">If you link to a separate template, resouceGroup() in the linked template resolves to the nested resource group.</span></span> <span data-ttu-id="2511b-131">Um modelo incorporado usa o seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="2511b-131">A linked template uses the following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers to linked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="2511b-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2511b-132">Next steps</span></span>

* <span data-ttu-id="2511b-133">Para entender como definir parâmetros em seu modelo, confira [Noções básicas de estrutura e sintaxe dos modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="2511b-133">To understand how to define parameters in your template, see [Understand the structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="2511b-134">Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="2511b-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="2511b-135">Para obter mais informações sobre a implantação de um modelo que exija um token SAS, veja [Implantar modelo particular com o token SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="2511b-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
