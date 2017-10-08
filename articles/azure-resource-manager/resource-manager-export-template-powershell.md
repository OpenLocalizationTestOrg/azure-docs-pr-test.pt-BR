---
title: modelo do Gerenciador de recursos de aaaExport com o Azure PowerShell | Microsoft Docs
description: Use o Gerenciador de recursos do Azure e o Azure PowerShell tooexport um modelo a partir de um grupo de recursos.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 9a239b7bce8209326c0e267a4d3d69f7014bdaed
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="417f6-103">Exportar modelos do Azure Resource Manager com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="417f6-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="417f6-104">Gerenciador de recursos permite que você tooexport um modelo do Gerenciador de recursos de recursos existentes em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="417f6-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="417f6-105">Você pode usar esse toolearn modelo gerado sobre Olá modelo sintaxe ou tooautomate Olá reimplantação de sua solução, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="417f6-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="417f6-106">É importante toonote que há dois tooexport de formas diferentes um modelo:</span><span class="sxs-lookup"><span data-stu-id="417f6-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="417f6-107">Você pode exportar Olá real do modelo que você usou para uma implantação.</span><span class="sxs-lookup"><span data-stu-id="417f6-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="417f6-108">modelo exportado Olá inclui todas as variáveis e parâmetros de saudação exatamente como eles eram exibidos no modelo original hello.</span><span class="sxs-lookup"><span data-stu-id="417f6-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="417f6-109">Essa abordagem é útil quando você precisa tooretrieve um modelo.</span><span class="sxs-lookup"><span data-stu-id="417f6-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="417f6-110">Você pode exportar um modelo que representa o estado atual de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="417f6-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="417f6-111">modelo exportado Olá não é baseado em qualquer modelo que você usou para a implantação.</span><span class="sxs-lookup"><span data-stu-id="417f6-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="417f6-112">Em vez disso, ele cria um modelo que é um instantâneo de saudação do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="417f6-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="417f6-113">modelo exportado Olá tem muitos valores embutidos e provavelmente não tantos parâmetros quantos você definiria normalmente.</span><span class="sxs-lookup"><span data-stu-id="417f6-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="417f6-114">Essa abordagem é útil quando você modificou o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="417f6-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="417f6-115">Agora, você precisa de grupo de recursos de saudação toocapture como um modelo.</span><span class="sxs-lookup"><span data-stu-id="417f6-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="417f6-116">Este tópico mostra as duas abordagens.</span><span class="sxs-lookup"><span data-stu-id="417f6-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="417f6-117">Implantar uma solução</span><span class="sxs-lookup"><span data-stu-id="417f6-117">Deploy a solution</span></span>

<span data-ttu-id="417f6-118">tooillustrate ambas as abordagens para exportar um modelo, vamos começar com a implantação de uma assinatura de tooyour da solução.</span><span class="sxs-lookup"><span data-stu-id="417f6-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="417f6-119">Se você já tiver um grupo de recursos em sua assinatura que você deseja tooexport, você não tem toodeploy nesta solução.</span><span class="sxs-lookup"><span data-stu-id="417f6-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="417f6-120">No entanto, o restante deste artigo Olá refere-se toohello modelo para esta solução.</span><span class="sxs-lookup"><span data-stu-id="417f6-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="417f6-121">script de exemplo Hello implanta uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="417f6-121">hello example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="417f6-122">Salvar modelo do histórico de implantações</span><span class="sxs-lookup"><span data-stu-id="417f6-122">Save template from deployment history</span></span>

<span data-ttu-id="417f6-123">Você pode recuperar um modelo de seu histórico de implantação usando Olá [AzureRmResourceGroupDeploymentTemplate salvar](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) comando.</span><span class="sxs-lookup"><span data-stu-id="417f6-123">You can retrieve a template from your deployment history by using hello [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="417f6-124">Olá modelo saudação do exemplo salva anteriormente implantado a seguir:</span><span class="sxs-lookup"><span data-stu-id="417f6-124">hello following example saves hello template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="417f6-125">Ele retorna o local de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="417f6-125">It returns hello location of hello template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="417f6-126">Abra o arquivo hello e observe que é Olá modelo exato usado para a implantação.</span><span class="sxs-lookup"><span data-stu-id="417f6-126">Open hello file, and notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="417f6-127">variáveis e parâmetros de saudação correspondem o modelo de saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="417f6-127">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="417f6-128">Você pode reimplantar esse modelo.</span><span class="sxs-lookup"><span data-stu-id="417f6-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="417f6-129">Exportar grupo de recursos como modelo</span><span class="sxs-lookup"><span data-stu-id="417f6-129">Export resource group as template</span></span>

<span data-ttu-id="417f6-130">Em vez de recuperar um modelo do histórico de implantação hello, você pode recuperar um modelo que representa o estado atual de saudação de um grupo de recursos usando Olá [AzureRmResourceGroup de exportação](/powershell/module/azurerm.resources/export-azurermresourcegroup) comando.</span><span class="sxs-lookup"><span data-stu-id="417f6-130">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="417f6-131">Você usa esse comando quando você fez muitas alterações de grupo de recursos de tooyour e nenhum modelo existente representa todas as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="417f6-131">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="417f6-132">Ele retorna o local de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="417f6-132">It returns hello location of hello template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="417f6-133">Abra o arquivo hello e observe que é diferente do modelo de saudação no GitHub.</span><span class="sxs-lookup"><span data-stu-id="417f6-133">Open hello file, and notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="417f6-134">Ele tem parâmetros diferentes e nenhuma variável.</span><span class="sxs-lookup"><span data-stu-id="417f6-134">It has different parameters and no variables.</span></span> <span data-ttu-id="417f6-135">armazenamento de saudação SKU e local são toovalues embutido.</span><span class="sxs-lookup"><span data-stu-id="417f6-135">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="417f6-136">Olá, exemplo a seguir mostra modelo exportado hello, mas seu modelo tem um nome de parâmetro ligeiramente diferentes:</span><span class="sxs-lookup"><span data-stu-id="417f6-136">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageAccounts_nf3mvst4nqb36standardsa_name": {
      "defaultValue": null,
      "type": "String"
    }
  },
  "variables": {},
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[parameters('storageAccounts_nf3mvst4nqb36standardsa_name')]",
      "apiVersion": "2016-01-01",
      "location": "southcentralus",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="417f6-137">Você pode reutilizar esse modelo, mas requer um nome exclusivo para a conta de armazenamento de saudação de adivinhação.</span><span class="sxs-lookup"><span data-stu-id="417f6-137">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="417f6-138">nome de saudação do parâmetro é ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="417f6-138">hello name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="417f6-139">Personalizar modelo exportado</span><span class="sxs-lookup"><span data-stu-id="417f6-139">Customize exported template</span></span>

<span data-ttu-id="417f6-140">Você pode modificar este modelo toomake-toouse mais fácil e mais flexível.</span><span class="sxs-lookup"><span data-stu-id="417f6-140">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="417f6-141">tooallow para obter mais locais, alteração Olá local propriedade toouse Olá mesmo local que o grupo de recursos de saudação:</span><span class="sxs-lookup"><span data-stu-id="417f6-141">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="417f6-142">tooavoid ter tooguess um nome de uniques para a conta de armazenamento, remover Olá parâmetro de nome de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="417f6-142">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="417f6-143">Adicione um parâmetro para um sufixo de nome de armazenamento e um SKU de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="417f6-143">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

```json
"parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
},
```

<span data-ttu-id="417f6-144">Adicione uma variável que constrói o nome de conta de armazenamento Olá com função de uniqueString hello:</span><span class="sxs-lookup"><span data-stu-id="417f6-144">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="417f6-145">Definir nome de saudação da variável de toohello de conta de armazenamento hello:</span><span class="sxs-lookup"><span data-stu-id="417f6-145">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="417f6-146">Definir Olá SKU toohello parâmetro:</span><span class="sxs-lookup"><span data-stu-id="417f6-146">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="417f6-147">O modelo agora se parece com:</span><span class="sxs-lookup"><span data-stu-id="417f6-147">Your template now looks like:</span></span>

```json
{
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageSuffix": {
      "type": "string",
      "defaultValue": "standardsa"
    },
    "storageAccountType": {
      "defaultValue": "Standard_LRS",
      "allowedValues": [
        "Standard_LRS",
        "Standard_GRS",
        "Standard_ZRS"
      ],
      "type": "string",
      "metadata": {
        "description": "Storage Account type"
      }
    }
  },
  "variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), parameters('storageSuffix'))]"
  },
  "resources": [
    {
      "type": "Microsoft.Storage/storageAccounts",
      "sku": {
        "name": "[parameters('storageAccountType')]",
        "tier": "Standard"
      },
      "kind": "Storage",
      "name": "[variables('storageAccountName')]",
      "apiVersion": "2016-01-01",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {},
      "dependsOn": []
    }
  ]
}
```

<span data-ttu-id="417f6-148">Reimplante o modelo modificado hello.</span><span class="sxs-lookup"><span data-stu-id="417f6-148">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="417f6-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="417f6-149">Next steps</span></span>
* <span data-ttu-id="417f6-150">Para obter informações sobre como usar o hello portal tooexport um modelo, consulte [exportar um modelo do Gerenciador de recursos do Azure de recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="417f6-150">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="417f6-151">parâmetros de toodefine no modelo, consulte [criar modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="417f6-151">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="417f6-152">Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="417f6-152">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
