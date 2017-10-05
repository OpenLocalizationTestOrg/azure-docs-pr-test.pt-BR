---
title: Exportar modelo do Resource Manager com a CLI do Azure | Microsoft Docs
description: Use o Azure Resource Manager e a CLI do Azure para exportar um modelo de um grupo de recursos.
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.service: azure-resource-manager
ms.devlang: azurecli
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/01/2017
ms.author: tomfitz
ms.openlocfilehash: 617664129a5353e25da1e90c742c4b009db172ef
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="7d058-103">Exportar modelos do Azure Resource Manager com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="7d058-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="7d058-104">O Gerenciador de Recursos permite que você exporte um modelo do Gerenciador de Recursos a partir dos recursos existentes em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="7d058-104">Resource Manager enables you to export a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="7d058-105">Você pode usar esse modelo gerado para saber mais sobre a sintaxe do modelo ou automatizar a reimplantação de sua solução, conforme o necessário.</span><span class="sxs-lookup"><span data-stu-id="7d058-105">You can use that generated template to learn about the template syntax or to automate the redeployment of your solution as needed.</span></span>

<span data-ttu-id="7d058-106">É importante observar que há duas maneiras diferentes de exportar um modelo:</span><span class="sxs-lookup"><span data-stu-id="7d058-106">It is important to note that there are two different ways to export a template:</span></span>

* <span data-ttu-id="7d058-107">Você pode exportar o modelo real que usou para uma implantação.</span><span class="sxs-lookup"><span data-stu-id="7d058-107">You can export the actual template that you used for a deployment.</span></span> <span data-ttu-id="7d058-108">O modelo exportado inclui todas as variáveis e parâmetros exatamente como apareceram no modelo original.</span><span class="sxs-lookup"><span data-stu-id="7d058-108">The exported template includes all the parameters and variables exactly as they appeared in the original template.</span></span> <span data-ttu-id="7d058-109">Essa abordagem é útil quando você precisa recuperar um modelo.</span><span class="sxs-lookup"><span data-stu-id="7d058-109">This approach is helpful when you need to retrieve a template.</span></span>
* <span data-ttu-id="7d058-110">Você pode exportar um modelo que representa o estado atual do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7d058-110">You can export a template that represents the current state of the resource group.</span></span> <span data-ttu-id="7d058-111">O modelo exportado não é baseado em nenhum modelo que você usou para a implantação.</span><span class="sxs-lookup"><span data-stu-id="7d058-111">The exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="7d058-112">Ao contrário, ele cria um modelo que é um instantâneo do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7d058-112">Instead, it creates a template that is a snapshot of the resource group.</span></span> <span data-ttu-id="7d058-113">O modelo exportado tem muitos valores embutidos e provavelmente menos parâmetros do que você normalmente definiria.</span><span class="sxs-lookup"><span data-stu-id="7d058-113">The exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="7d058-114">Essa abordagem é útil quando você modificou o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="7d058-114">This approach is useful when you have modified the resource group.</span></span> <span data-ttu-id="7d058-115">Agora, você precisa capturar o grupo de recursos como um modelo.</span><span class="sxs-lookup"><span data-stu-id="7d058-115">Now, you need to capture the resource group as a template.</span></span>

<span data-ttu-id="7d058-116">Este tópico mostra as duas abordagens.</span><span class="sxs-lookup"><span data-stu-id="7d058-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="7d058-117">Implantar uma solução</span><span class="sxs-lookup"><span data-stu-id="7d058-117">Deploy a solution</span></span>

<span data-ttu-id="7d058-118">Para ilustrar as duas abordagens de exportação de um modelo, vamos começar implantando uma solução em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="7d058-118">To illustrate both approaches for exporting a template, let's start by deploying a solution to your subscription.</span></span> <span data-ttu-id="7d058-119">Se você já tiver um grupo de recursos em sua assinatura que queira exportar, não será preciso implantar essa solução.</span><span class="sxs-lookup"><span data-stu-id="7d058-119">If you already have a resource group in your subscription that you want to export, you do not have to deploy this solution.</span></span> <span data-ttu-id="7d058-120">No entanto, o restante deste artigo refere-se ao modelo dessa solução.</span><span class="sxs-lookup"><span data-stu-id="7d058-120">However, the remainder of this article refers to the template for this solution.</span></span> <span data-ttu-id="7d058-121">O script de exemplo implanta uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7d058-121">The example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="7d058-122">Salvar modelo do histórico de implantações</span><span class="sxs-lookup"><span data-stu-id="7d058-122">Save template from deployment history</span></span>

<span data-ttu-id="7d058-123">Você pode recuperar um modelo do histórico de implantações usando o comando [az group deployment export](/cli/azure/group/deployment#export).</span><span class="sxs-lookup"><span data-stu-id="7d058-123">You can retrieve a template from your deployment history by using the [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="7d058-124">O exemplo a seguir salva o modelo implantado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="7d058-124">The following example saves the template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="7d058-125">Retorna o modelo.</span><span class="sxs-lookup"><span data-stu-id="7d058-125">It returns the template.</span></span> <span data-ttu-id="7d058-126">Copie o JSON e salve como um arquivo.</span><span class="sxs-lookup"><span data-stu-id="7d058-126">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="7d058-127">Observe que é o modelo exato que foi usado para implantação.</span><span class="sxs-lookup"><span data-stu-id="7d058-127">Notice that it is the exact template you used for deployment.</span></span> <span data-ttu-id="7d058-128">Os parâmetros e as variáveis correspondem ao modelo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="7d058-128">The parameters and variables match the template from GitHub.</span></span> <span data-ttu-id="7d058-129">Você pode reimplantar esse modelo.</span><span class="sxs-lookup"><span data-stu-id="7d058-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="7d058-130">Exportar grupo de recursos como modelo</span><span class="sxs-lookup"><span data-stu-id="7d058-130">Export resource group as template</span></span>

<span data-ttu-id="7d058-131">Em vez de recuperar um modelo do histórico de implantações, você pode recuperar um modelo que representa o estado atual de um grupo de recursos usando o comando [az group export](/cli/azure/group#export).</span><span class="sxs-lookup"><span data-stu-id="7d058-131">Instead of retrieving a template from the deployment history, you can retrieve a template that represents the current state of a resource group by using the [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="7d058-132">Use esse comando quando você fez muitas alterações no seu grupo de recursos e nenhum modelo existente representa todas as alterações.</span><span class="sxs-lookup"><span data-stu-id="7d058-132">You use this command when you have made many changes to your resource group and no existing template represents all the changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="7d058-133">Retorna o modelo.</span><span class="sxs-lookup"><span data-stu-id="7d058-133">It returns the template.</span></span> <span data-ttu-id="7d058-134">Copie o JSON e salve como um arquivo.</span><span class="sxs-lookup"><span data-stu-id="7d058-134">Copy the JSON, and save as a file.</span></span> <span data-ttu-id="7d058-135">Observe que ele é diferente do modelo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="7d058-135">Notice that it is different than the template in GitHub.</span></span> <span data-ttu-id="7d058-136">Ele tem parâmetros diferentes e nenhuma variável.</span><span class="sxs-lookup"><span data-stu-id="7d058-136">It has different parameters and no variables.</span></span> <span data-ttu-id="7d058-137">O SKU e o local de armazenamento são embutidos em código para valores.</span><span class="sxs-lookup"><span data-stu-id="7d058-137">The storage SKU and location are hard-coded to values.</span></span> <span data-ttu-id="7d058-138">O exemplo abaixo mostra o modelo exportado, mas seu modelo tem um nome de parâmetro ligeiramente diferente:</span><span class="sxs-lookup"><span data-stu-id="7d058-138">The following example shows the exported template, but your template has a slightly different parameter name:</span></span>

```json
{
  "parameters": {
    "storageAccounts_mcyzaljiv7qncstandardsa_name": {
      "type": "String",
      "defaultValue": null
    }
  },
  "variables": {},
  "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "resources": [
    {
      "tags": {},
      "dependsOn": [],
      "apiVersion": "2016-01-01",
      "sku": {
        "name": "Standard_LRS",
        "tier": "Standard"
      },
      "kind": "Storage",
      "type": "Microsoft.Storage/storageAccounts",
      "location": "centralus",
      "name": "[parameters('storageAccounts_mcyzaljiv7qncstandardsa_name')]",
      "properties": {}
    }
  ],
  "contentVersion": "1.0.0.0"
}
```

<span data-ttu-id="7d058-139">Você pode reimplantar esse modelo, mas ele exige a suposição de um nome exclusivo para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7d058-139">You can redeploy this template, but it requires guessing a unique name for the storage account.</span></span> <span data-ttu-id="7d058-140">O nome do parâmetro é ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="7d058-140">The name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="7d058-141">Personalizar modelo exportado</span><span class="sxs-lookup"><span data-stu-id="7d058-141">Customize exported template</span></span>

<span data-ttu-id="7d058-142">Você pode modificar esse modelo para facilitar o uso e torná-lo mais flexível.</span><span class="sxs-lookup"><span data-stu-id="7d058-142">You can modify this template to make it easier to use and more flexible.</span></span> <span data-ttu-id="7d058-143">Para permitir mais locais, altere a propriedade de local para usar o mesmo local do grupo de recursos:</span><span class="sxs-lookup"><span data-stu-id="7d058-143">To allow for more locations, change the location property to use the same location as the resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="7d058-144">Para não ter que supor um nome exclusivo para a conta de armazenamento, remova o parâmetro do nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="7d058-144">To avoid having to guess a uniques name for storage account, remove the parameter for the storage account name.</span></span> <span data-ttu-id="7d058-145">Adicione um parâmetro para um sufixo de nome de armazenamento e um SKU de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="7d058-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="7d058-146">Adicione uma variável que construa o nome da conta de armazenamento com a função uniqueString:</span><span class="sxs-lookup"><span data-stu-id="7d058-146">Add a variable that constructs the storage account name with the uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="7d058-147">Defina o nome da conta de armazenamento para a variável:</span><span class="sxs-lookup"><span data-stu-id="7d058-147">Set the name of the storage account to the variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="7d058-148">Defina o SKU para o parâmetro:</span><span class="sxs-lookup"><span data-stu-id="7d058-148">Set the SKU to the parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="7d058-149">O modelo agora se parece com:</span><span class="sxs-lookup"><span data-stu-id="7d058-149">Your template now looks like:</span></span>

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

<span data-ttu-id="7d058-150">Reimplante o modelo modificado.</span><span class="sxs-lookup"><span data-stu-id="7d058-150">Redeploy the modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7d058-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7d058-151">Next steps</span></span>
* <span data-ttu-id="7d058-152">Para obter informações sobre como usar o portal para exportar um modelo, confira [Exportar um modelo do Azure Resource Manager de recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="7d058-152">For information about using the portal to export a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="7d058-153">Para definir os parâmetros no modelo, consulte [Criando modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="7d058-153">To define parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="7d058-154">Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="7d058-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>