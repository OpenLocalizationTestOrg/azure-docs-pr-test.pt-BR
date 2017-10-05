---
title: Exportar modelo do Resource Manager com o Azure PowerShell | Microsoft Docs
description: Use o Azure Resource Manager e o Azure PowerShell para exportar um modelo de um grupo de recursos.
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
ms.openlocfilehash: 7543811eb9448222b6e7c266756e68debc7d54be
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-powershell"></a><span data-ttu-id="37731-103">Exportar modelos do Azure Resource Manager com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="37731-103">Export Azure Resource Manager templates with PowerShell</span></span>

<span data-ttu-id="37731-104">O Gerenciador de Recursos permite que você exporte um modelo do Gerenciador de Recursos a partir dos recursos existentes em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="37731-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="37731-105">Você pode usar esse modelo gerado para saber mais sobre a sintaxe do modelo ou automatizar a reimplantação de sua solução, conforme o necessário.</span><span class="sxs-lookup"><span data-stu-id="37731-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="37731-106">É importante observar que há duas maneiras diferentes de exportar um modelo:</span><span class="sxs-lookup"><span data-stu-id="37731-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="37731-107">Você pode exportar o modelo real que usou para uma implantação.</span><span class="sxs-lookup"><span data-stu-id="37731-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="37731-108">O modelo exportado inclui todas as variáveis e parâmetros exatamente como apareceram no modelo original.</span><span class="sxs-lookup"><span data-stu-id="37731-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="37731-109">Essa abordagem é útil quando você precisa recuperar um modelo.</span><span class="sxs-lookup"><span data-stu-id="37731-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="37731-110">Você pode exportar um modelo que representa o estado atual do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="37731-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="37731-111">O modelo exportado não é baseado em nenhum modelo que você usou para a implantação.</span><span class="sxs-lookup"><span data-stu-id="37731-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="37731-112">Ao contrário, ele cria um modelo que é um instantâneo do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="37731-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="37731-113">O modelo exportado tem muitos valores embutidos e provavelmente menos parâmetros do que você normalmente definiria.</span><span class="sxs-lookup"><span data-stu-id="37731-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="37731-114">Essa abordagem é útil quando você modificou o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="37731-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="37731-115">Agora, você precisa capturar o grupo de recursos como um modelo.</span><span class="sxs-lookup"><span data-stu-id="37731-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="37731-116">Este tópico mostra as duas abordagens.</span><span class="sxs-lookup"><span data-stu-id="37731-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="37731-117">Implantar uma solução</span><span class="sxs-lookup"><span data-stu-id="37731-117">Deploy a solution</span></span>

<span data-ttu-id="37731-118">Para ilustrar as duas abordagens de exportação de um modelo, vamos começar implantando uma solução em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="37731-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="37731-119">Se você já tiver um grupo de recursos em sua assinatura que queira exportar, não será preciso implantar essa solução.</span><span class="sxs-lookup"><span data-stu-id="37731-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="37731-120">No entanto, o restante deste artigo refere-se ao modelo dessa solução.</span><span class="sxs-lookup"><span data-stu-id="37731-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="37731-121">O script de exemplo implanta uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="37731-121">The example script deploys a storage account.</span></span>

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="37731-122">Salvar modelo do histórico de implantações</span><span class="sxs-lookup"><span data-stu-id="37731-122">Save template from deployment history</span></span>

<span data-ttu-id="37731-123">Você pode recuperar um modelo do histórico de implantações usando o comando [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate).</span><span class="sxs-lookup"><span data-stu-id="37731-123">You can retrieve a template from your deployment history by using the [Save-AzureRmResourceGroupDeploymentTemplate](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) command.</span></span> <span data-ttu-id="37731-124">O exemplo a seguir salva o modelo implantado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="37731-124">The following example saves the template that you previously deploy:</span></span>

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

<span data-ttu-id="37731-125">Ele retorna o local do modelo.</span><span class="sxs-lookup"><span data-stu-id="37731-125">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

<span data-ttu-id="37731-126">Abra o arquivo e observe que é o modelo exato que foi usado para implantação.</span><span class="sxs-lookup"><span data-stu-id="37731-126">Open the file, and notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="37731-127">Os parâmetros e as variáveis correspondem ao modelo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="37731-127">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="37731-128">Você pode reimplantar esse modelo.</span><span class="sxs-lookup"><span data-stu-id="37731-128">You can redeploy this template.</span></span>

## <a name="export-resource-group-as-template"></a><span data-ttu-id="37731-129">Exportar grupo de recursos como modelo</span><span class="sxs-lookup"><span data-stu-id="37731-129">Export resource group as template</span></span>

<span data-ttu-id="37731-130">Em vez de recuperar um modelo do histórico de implantações, você pode recuperar um modelo que representa o estado atual de um grupo de recursos usando o comando [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup).</span><span class="sxs-lookup"><span data-stu-id="37731-130">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [Export-AzureRmResourceGroup](/powershell/module/azurerm.resources/export-azurermresourcegroup) command.</span></span> <span data-ttu-id="37731-131">Use esse comando quando você fez muitas alterações no seu grupo de recursos e nenhum modelo existente representa todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="37731-131">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

<span data-ttu-id="37731-132">Ele retorna o local do modelo.</span><span class="sxs-lookup"><span data-stu-id="37731-132">It returns the location of the template.</span></span>

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

<span data-ttu-id="37731-133">Abra o arquivo e observe que ele é diferente do modelo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="37731-133">Open the file, and notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="37731-134">Ele tem parâmetros diferentes e nenhuma variável.</span><span class="sxs-lookup"><span data-stu-id="37731-134">It has different parameters and no variables.</span></span> <span data-ttu-id="37731-135">O SKU e o local de armazenamento são embutidos em código para valores.</span><span class="sxs-lookup"><span data-stu-id="37731-135">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="37731-136">O exemplo abaixo mostra o modelo exportado, mas seu modelo tem um nome de parâmetro ligeiramente diferente:</span><span class="sxs-lookup"><span data-stu-id="37731-136">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

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

<span data-ttu-id="37731-137">Você pode reimplantar esse modelo, mas ele exige a suposição de um nome exclusivo para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="37731-137">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="37731-138">O nome do parâmetro é ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="37731-138">The name of your parameter is slightly different.</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a><span data-ttu-id="37731-139">Personalizar modelo exportado</span><span class="sxs-lookup"><span data-stu-id="37731-139">Customize exported template</span></span>

<span data-ttu-id="37731-140">Você pode modificar esse modelo para facilitar o uso e torná-lo mais flexível.</span><span class="sxs-lookup"><span data-stu-id="37731-140">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="37731-141">Para permitir mais locais, altere a propriedade de local para usar o mesmo local do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="37731-141">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="37731-142">Para não ter que supor um nome exclusivo para a conta de armazenamento, remova o parâmetro do nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="37731-142">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="37731-143">Adicione um parâmetro para um sufixo de nome de armazenamento e um SKU de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="37731-143">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="37731-144">Adicione uma variável que construa o nome da conta de armazenamento com a função uniqueString:</span><span class="sxs-lookup"><span data-stu-id="37731-144">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="37731-145">Defina o nome da conta de armazenamento para a variável:</span><span class="sxs-lookup"><span data-stu-id="37731-145">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="37731-146">Defina o SKU para o parâmetro:</span><span class="sxs-lookup"><span data-stu-id="37731-146">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="37731-147">O modelo agora se parece com:</span><span class="sxs-lookup"><span data-stu-id="37731-147">Your template now looks like:</span></span>

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

<span data-ttu-id="37731-148">Reimplante o modelo modificado.</span><span class="sxs-lookup"><span data-stu-id="37731-148">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="37731-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="37731-149">Next steps</span></span>
* <span data-ttu-id="37731-150">Para obter informações sobre como usar o portal para exportar um modelo, confira [Exportar um modelo do Azure Resource Manager de recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="37731-150">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="37731-151">Para definir os parâmetros no modelo, consulte [Criando modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="37731-151">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="37731-152">Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="37731-152">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>
