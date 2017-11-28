---
title: grupos de recursos de toomultiple aaaDeploy recursos do Azure | Microsoft Docs
description: "Mostra como tootarget mais de um recurso do Azure grupo durante a implantação."
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
ms.openlocfilehash: 93a39a26e0ca18dfcb5c6e8de95c38a64186d6de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a><span data-ttu-id="1903d-103">Implantar recursos do Azure toomore que um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="1903d-103">Deploy Azure resources toomore than one resource group</span></span>

<span data-ttu-id="1903d-104">Normalmente, você implanta todos os recursos de saudação em seu modelo tooa único grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="1903d-104">Typically, you deploy all hello resources in your template tooa single resource group.</span></span> <span data-ttu-id="1903d-105">No entanto, há situações em que você deseja toodeploy um conjunto de recursos juntos mas colocá-los em grupos de recursos diferentes.</span><span class="sxs-lookup"><span data-stu-id="1903d-105">However, there are scenarios where you want toodeploy a set of resources together but place them in different resource groups.</span></span> <span data-ttu-id="1903d-106">Por exemplo, você talvez queira toodeploy Olá backup virtual machine para local e o grupo de recursos separado do Azure Site Recovery tooa.</span><span class="sxs-lookup"><span data-stu-id="1903d-106">For example, you may want toodeploy hello backup virtual machine for Azure Site Recovery tooa separate resource group and location.</span></span> <span data-ttu-id="1903d-107">Gerenciador de recursos permite que você toouse aninhado modelos tootarget diferentes grupos de recursos que o grupo de recursos de saudação usado para Olá pai modelo.</span><span class="sxs-lookup"><span data-stu-id="1903d-107">Resource Manager enables you toouse nested templates tootarget different resource groups than hello resource group used for hello parent template.</span></span>

<span data-ttu-id="1903d-108">grupo de recursos de saudação é o contêiner de ciclo de vida de Olá para o aplicativo hello e sua coleção de recursos.</span><span class="sxs-lookup"><span data-stu-id="1903d-108">hello resource group is hello lifecycle container for hello application and its collection of resources.</span></span> <span data-ttu-id="1903d-109">Criar grupo de recursos de saudação fora do modelo Olá e especificar Olá tootarget de grupo de recursos durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="1903d-109">You create hello resource group outside of hello template, and specify hello resource group tootarget during deployment.</span></span> <span data-ttu-id="1903d-110">Para grupos de tooresource uma introdução, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="1903d-110">For an introduction tooresource groups, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="example-template"></a><span data-ttu-id="1903d-111">Modelo de exemplo</span><span class="sxs-lookup"><span data-stu-id="1903d-111">Example template</span></span>

<span data-ttu-id="1903d-112">tootarget um recurso diferente, você deve usar um modelo aninhado ou vinculado durante a implantação.</span><span class="sxs-lookup"><span data-stu-id="1903d-112">tootarget a different resource, you must use a nested or linked template during deployment.</span></span> <span data-ttu-id="1903d-113">Olá `Microsoft.Resources/deployments` tipo de recurso fornece um `resourceGroup` parâmetro que permite que você toospecify um grupo de recursos diferente para Olá aninhados a implantação.</span><span class="sxs-lookup"><span data-stu-id="1903d-113">hello `Microsoft.Resources/deployments` resource type provides a `resourceGroup` parameter that enables you toospecify a different resource group for hello nested deployment.</span></span> <span data-ttu-id="1903d-114">Todos os grupos de recursos de saudação devem existir antes de executar a implantação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1903d-114">All hello resource groups must exist before running hello deployment.</span></span> <span data-ttu-id="1903d-115">exemplo a seguir Hello implanta duas contas de armazenamento - um em grupo de recursos de saudação especificado durante a implantação e um em um grupo de recursos denominado `crossResourceGroupDeployment`:</span><span class="sxs-lookup"><span data-stu-id="1903d-115">hello following example deploys two storage accounts - one in hello resource group specified during deployment, and one in a resource group named `crossResourceGroupDeployment`:</span></span>

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

<span data-ttu-id="1903d-116">Se você definir `resourceGroup` toohello o nome de um grupo de recursos que não existe, a implantação de saudação falha.</span><span class="sxs-lookup"><span data-stu-id="1903d-116">If you set `resourceGroup` toohello name of a resource group that does not exist, hello deployment fails.</span></span> <span data-ttu-id="1903d-117">Se você não fornecer um valor para `resourceGroup`, grupo de recursos pai Olá usa o Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="1903d-117">If you do not provide a value for `resourceGroup`, Resource Manager uses hello parent resource group.</span></span>  

## <a name="deploy-hello-template"></a><span data-ttu-id="1903d-118">Implante o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="1903d-118">Deploy hello template</span></span>

<span data-ttu-id="1903d-119">modelo de exemplo hello toodeploy, você pode usar o portal hello, o Azure PowerShell ou CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="1903d-119">toodeploy hello example template, you can use hello portal, Azure PowerShell, or Azure CLI.</span></span> <span data-ttu-id="1903d-120">Para o Azure PowerShell ou a CLI do Azure, você pode usar uma versão de maio de 2017 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1903d-120">For Azure PowerShell or Azure CLI, you must use a release from May 2017 or later.</span></span> <span data-ttu-id="1903d-121">exemplos de Olá presumem que você salvou o modelo de saudação localmente como um arquivo chamado **crossrgdeployment.json**.</span><span class="sxs-lookup"><span data-stu-id="1903d-121">hello examples assume you have saved hello template locally as a file named **crossrgdeployment.json**.</span></span>

<span data-ttu-id="1903d-122">Para o PowerShell:</span><span class="sxs-lookup"><span data-stu-id="1903d-122">For PowerShell:</span></span>

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

<span data-ttu-id="1903d-123">Para a CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="1903d-123">For Azure CLI:</span></span>

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

<span data-ttu-id="1903d-124">Após a implantação ser concluída, você verá dois grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="1903d-124">After deployment completes, you see two resource groups.</span></span> <span data-ttu-id="1903d-125">Cada grupo de recursos contém uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1903d-125">Each resource group contains a storage account.</span></span>

## <a name="use-resourcegroup-function"></a><span data-ttu-id="1903d-126">Use a função resourceGroup()</span><span class="sxs-lookup"><span data-stu-id="1903d-126">Use resourceGroup() function</span></span>

<span data-ttu-id="1903d-127">Para cruzada implantações de grupos de recursos, hello [resouceGroup() função](resource-group-template-functions-resource.md#resourcegroup) resolve diferente com base em como você especifica o modelo aninhado hello.</span><span class="sxs-lookup"><span data-stu-id="1903d-127">For cross resource group deployments, hello [resouceGroup() function](resource-group-template-functions-resource.md#resourcegroup) resolves differently based on how you specify hello nested template.</span></span> 

<span data-ttu-id="1903d-128">Se você inserir um modelo dentro de outro modelo, resouceGroup() modelo aninhado Olá resolve toohello grupo de recursos de pai.</span><span class="sxs-lookup"><span data-stu-id="1903d-128">If you embed one template within another template, resouceGroup() in hello nested template resolves toohello parent resource group.</span></span> <span data-ttu-id="1903d-129">Um modelo incorporado usa Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="1903d-129">An embedded template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "embeddedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "template": {
        ...
        resourceGroup() refers tooparent resource group
    }
}
```

<span data-ttu-id="1903d-130">Se você vincular um modelo separado tooa, resouceGroup() no modelo vinculado Olá resolve toohello grupo de recursos aninhados.</span><span class="sxs-lookup"><span data-stu-id="1903d-130">If you link tooa separate template, resouceGroup() in hello linked template resolves toohello nested resource group.</span></span> <span data-ttu-id="1903d-131">Um modelo vinculado usa Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="1903d-131">A linked template uses hello following format:</span></span>

```json
"apiVersion": "2017-05-10",
"name": "linkedTemplate",
"type": "Microsoft.Resources/deployments",
"resourceGroup": "crossResourceGroupDeployment",
"properties": {
    "mode": "Incremental",
    "templateLink": {
        ...
        resourceGroup() in linked template refers toolinked resource group
    }
}
```

## <a name="next-steps"></a><span data-ttu-id="1903d-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1903d-132">Next steps</span></span>

* <span data-ttu-id="1903d-133">toounderstand como toodefine parâmetros em seu modelo, consulte [entender a estrutura de saudação e a sintaxe de modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="1903d-133">toounderstand how toodefine parameters in your template, see [Understand hello structure and syntax of Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>
* <span data-ttu-id="1903d-134">Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="1903d-134">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
* <span data-ttu-id="1903d-135">Para obter mais informações sobre a implantação de um modelo que exija um token SAS, veja [Implantar modelo particular com o token SAS](resource-manager-powershell-sas-token.md).</span><span class="sxs-lookup"><span data-stu-id="1903d-135">For information about deploying a template that requires a SAS token, see [Deploy private template with SAS token](resource-manager-powershell-sas-token.md).</span></span>
