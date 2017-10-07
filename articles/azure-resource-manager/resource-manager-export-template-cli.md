---
title: modelo do Gerenciador de recursos de aaaExport com CLI do Azure | Microsoft Docs
description: Use o Gerenciador de recursos do Azure e a CLI do Azure tooexport um modelo a partir de um grupo de recursos.
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
ms.openlocfilehash: 2d44a0a6e9717504d4c2a01254d826679b381f22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="export-azure-resource-manager-templates-with-azure-cli"></a><span data-ttu-id="2afbd-103">Exportar modelos do Azure Resource Manager com a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2afbd-103">Export Azure Resource Manager templates with Azure CLI</span></span>

<span data-ttu-id="2afbd-104">Gerenciador de recursos permite que você tooexport um modelo do Gerenciador de recursos de recursos existentes em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="2afbd-104">Resource Manager enables you tooexport a Resource Manager template from existing resources in your subscription.</span></span> <span data-ttu-id="2afbd-105">Você pode usar esse toolearn modelo gerado sobre Olá modelo sintaxe ou tooautomate Olá reimplantação de sua solução, conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="2afbd-105">You can use that generated template toolearn about hello template syntax or tooautomate hello redeployment of your solution as needed.</span></span>

<span data-ttu-id="2afbd-106">É importante toonote que há dois tooexport de formas diferentes um modelo:</span><span class="sxs-lookup"><span data-stu-id="2afbd-106">It is important toonote that there are two different ways tooexport a template:</span></span>

* <span data-ttu-id="2afbd-107">Você pode exportar Olá real do modelo que você usou para uma implantação.</span><span class="sxs-lookup"><span data-stu-id="2afbd-107">You can export hello actual template that you used for a deployment.</span></span> <span data-ttu-id="2afbd-108">modelo exportado Olá inclui todas as variáveis e parâmetros de saudação exatamente como eles eram exibidos no modelo original hello.</span><span class="sxs-lookup"><span data-stu-id="2afbd-108">hello exported template includes all hello parameters and variables exactly as they appeared in hello original template.</span></span> <span data-ttu-id="2afbd-109">Essa abordagem é útil quando você precisa tooretrieve um modelo.</span><span class="sxs-lookup"><span data-stu-id="2afbd-109">This approach is helpful when you need tooretrieve a template.</span></span>
* <span data-ttu-id="2afbd-110">Você pode exportar um modelo que representa o estado atual de Olá Olá do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2afbd-110">You can export a template that represents hello current state of hello resource group.</span></span> <span data-ttu-id="2afbd-111">modelo exportado Olá não é baseado em qualquer modelo que você usou para a implantação.</span><span class="sxs-lookup"><span data-stu-id="2afbd-111">hello exported template is not based on any template that you used for deployment.</span></span> <span data-ttu-id="2afbd-112">Em vez disso, ele cria um modelo que é um instantâneo de saudação do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2afbd-112">Instead, it creates a template that is a snapshot of hello resource group.</span></span> <span data-ttu-id="2afbd-113">modelo exportado Olá tem muitos valores embutidos e provavelmente não tantos parâmetros quantos você definiria normalmente.</span><span class="sxs-lookup"><span data-stu-id="2afbd-113">hello exported template has many hard-coded values and probably not as many parameters as you would typically define.</span></span> <span data-ttu-id="2afbd-114">Essa abordagem é útil quando você modificou o grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2afbd-114">This approach is useful when you have modified hello resource group.</span></span> <span data-ttu-id="2afbd-115">Agora, você precisa de grupo de recursos de saudação toocapture como um modelo.</span><span class="sxs-lookup"><span data-stu-id="2afbd-115">Now, you need toocapture hello resource group as a template.</span></span>

<span data-ttu-id="2afbd-116">Este tópico mostra as duas abordagens.</span><span class="sxs-lookup"><span data-stu-id="2afbd-116">This topic shows both approaches.</span></span>

## <a name="deploy-a-solution"></a><span data-ttu-id="2afbd-117">Implantar uma solução</span><span class="sxs-lookup"><span data-stu-id="2afbd-117">Deploy a solution</span></span>

<span data-ttu-id="2afbd-118">tooillustrate ambas as abordagens para exportar um modelo, vamos começar com a implantação de uma assinatura de tooyour da solução.</span><span class="sxs-lookup"><span data-stu-id="2afbd-118">tooillustrate both approaches for exporting a template, let's start by deploying a solution tooyour subscription.</span></span> <span data-ttu-id="2afbd-119">Se você já tiver um grupo de recursos em sua assinatura que você deseja tooexport, você não tem toodeploy nesta solução.</span><span class="sxs-lookup"><span data-stu-id="2afbd-119">If you already have a resource group in your subscription that you want tooexport, you do not have toodeploy this solution.</span></span> <span data-ttu-id="2afbd-120">No entanto, o restante deste artigo Olá refere-se toohello modelo para esta solução.</span><span class="sxs-lookup"><span data-stu-id="2afbd-120">However, hello remainder of this article refers toohello template for this solution.</span></span> <span data-ttu-id="2afbd-121">script de exemplo Hello implanta uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2afbd-121">hello example script deploys a storage account.</span></span>

```azurecli
az group create --name ExampleGroup --location "Central US"
az group deployment create \
    --name NewStorage \
    --resource-group ExampleGroup \
    --template-uri "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json" \
```  

## <a name="save-template-from-deployment-history"></a><span data-ttu-id="2afbd-122">Salvar modelo do histórico de implantações</span><span class="sxs-lookup"><span data-stu-id="2afbd-122">Save template from deployment history</span></span>

<span data-ttu-id="2afbd-123">Você pode recuperar um modelo de seu histórico de implantação usando Olá [exportação de implantação de grupo az](/cli/azure/group/deployment#export) comando.</span><span class="sxs-lookup"><span data-stu-id="2afbd-123">You can retrieve a template from your deployment history by using hello [az group deployment export](/cli/azure/group/deployment#export) command.</span></span> <span data-ttu-id="2afbd-124">Olá modelo saudação do exemplo salva anteriormente implantado a seguir:</span><span class="sxs-lookup"><span data-stu-id="2afbd-124">hello following example saves hello template that you previously deploy:</span></span>

```azurecli
az group deployment export --name NewStorage --resource-group ExampleGroup
```

<span data-ttu-id="2afbd-125">Retorna o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2afbd-125">It returns hello template.</span></span> <span data-ttu-id="2afbd-126">Copie Olá JSON e salve como um arquivo.</span><span class="sxs-lookup"><span data-stu-id="2afbd-126">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="2afbd-127">Observe que é Olá modelo exato usado para a implantação.</span><span class="sxs-lookup"><span data-stu-id="2afbd-127">Notice that it is hello exact template you used for deployment.</span></span> <span data-ttu-id="2afbd-128">variáveis e parâmetros de saudação correspondem o modelo de saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="2afbd-128">hello parameters and variables match hello template from GitHub.</span></span> <span data-ttu-id="2afbd-129">Você pode reimplantar esse modelo.</span><span class="sxs-lookup"><span data-stu-id="2afbd-129">You can redeploy this template.</span></span>


## <a name="export-resource-group-as-template"></a><span data-ttu-id="2afbd-130">Exportar grupo de recursos como modelo</span><span class="sxs-lookup"><span data-stu-id="2afbd-130">Export resource group as template</span></span>

<span data-ttu-id="2afbd-131">Em vez de recuperar um modelo do histórico de implantação hello, você pode recuperar um modelo que representa o estado atual de saudação de um grupo de recursos usando Olá [exportação de grupo az](/cli/azure/group#export) comando.</span><span class="sxs-lookup"><span data-stu-id="2afbd-131">Instead of retrieving a template from hello deployment history, you can retrieve a template that represents hello current state of a resource group by using hello [az group export](/cli/azure/group#export) command.</span></span> <span data-ttu-id="2afbd-132">Você usa esse comando quando você fez muitas alterações de grupo de recursos de tooyour e nenhum modelo existente representa todas as alterações de saudação.</span><span class="sxs-lookup"><span data-stu-id="2afbd-132">You use this command when you have made many changes tooyour resource group and no existing template represents all hello changes.</span></span>

```azurecli
az group export --name ExampleGroup
```

<span data-ttu-id="2afbd-133">Retorna o modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2afbd-133">It returns hello template.</span></span> <span data-ttu-id="2afbd-134">Copie Olá JSON e salve como um arquivo.</span><span class="sxs-lookup"><span data-stu-id="2afbd-134">Copy hello JSON, and save as a file.</span></span> <span data-ttu-id="2afbd-135">Observe que é diferente do modelo de saudação no GitHub.</span><span class="sxs-lookup"><span data-stu-id="2afbd-135">Notice that it is different than hello template in GitHub.</span></span> <span data-ttu-id="2afbd-136">Ele tem parâmetros diferentes e nenhuma variável.</span><span class="sxs-lookup"><span data-stu-id="2afbd-136">It has different parameters and no variables.</span></span> <span data-ttu-id="2afbd-137">armazenamento de saudação SKU e local são toovalues embutido.</span><span class="sxs-lookup"><span data-stu-id="2afbd-137">hello storage SKU and location are hard-coded toovalues.</span></span> <span data-ttu-id="2afbd-138">Olá, exemplo a seguir mostra modelo exportado hello, mas seu modelo tem um nome de parâmetro ligeiramente diferentes:</span><span class="sxs-lookup"><span data-stu-id="2afbd-138">hello following example shows hello exported template, but your template has a slightly different parameter name:</span></span>

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

<span data-ttu-id="2afbd-139">Você pode reutilizar esse modelo, mas requer um nome exclusivo para a conta de armazenamento de saudação de adivinhação.</span><span class="sxs-lookup"><span data-stu-id="2afbd-139">You can redeploy this template, but it requires guessing a unique name for hello storage account.</span></span> <span data-ttu-id="2afbd-140">nome de saudação do parâmetro é ligeiramente diferente.</span><span class="sxs-lookup"><span data-stu-id="2afbd-140">hello name of your parameter is slightly different.</span></span>

```azurecli
az group deployment create --name NewStorage --resource-group ExampleGroup \
  --template-file examplegroup.json \
  --parameters "{\"storageAccounts_mcyzaljiv7qncstandardsa_name\":{\"value\":\"tfstore0501\"}}"
```

## <a name="customize-exported-template"></a><span data-ttu-id="2afbd-141">Personalizar modelo exportado</span><span class="sxs-lookup"><span data-stu-id="2afbd-141">Customize exported template</span></span>

<span data-ttu-id="2afbd-142">Você pode modificar este modelo toomake-toouse mais fácil e mais flexível.</span><span class="sxs-lookup"><span data-stu-id="2afbd-142">You can modify this template toomake it easier toouse and more flexible.</span></span> <span data-ttu-id="2afbd-143">tooallow para obter mais locais, alteração Olá local propriedade toouse Olá mesmo local que o grupo de recursos de saudação:</span><span class="sxs-lookup"><span data-stu-id="2afbd-143">tooallow for more locations, change hello location property toouse hello same location as hello resource group:</span></span>

```json
"location": "[resourceGroup().location]",
```

<span data-ttu-id="2afbd-144">tooavoid ter tooguess um nome de uniques para a conta de armazenamento, remover Olá parâmetro de nome de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="2afbd-144">tooavoid having tooguess a uniques name for storage account, remove hello parameter for hello storage account name.</span></span> <span data-ttu-id="2afbd-145">Adicione um parâmetro para um sufixo de nome de armazenamento e um SKU de armazenamento:</span><span class="sxs-lookup"><span data-stu-id="2afbd-145">Add a parameter for a storage name suffix, and a storage SKU:</span></span>

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

<span data-ttu-id="2afbd-146">Adicione uma variável que constrói o nome de conta de armazenamento Olá com função de uniqueString hello:</span><span class="sxs-lookup"><span data-stu-id="2afbd-146">Add a variable that constructs hello storage account name with hello uniqueString function:</span></span>

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

<span data-ttu-id="2afbd-147">Definir nome de saudação da variável de toohello de conta de armazenamento hello:</span><span class="sxs-lookup"><span data-stu-id="2afbd-147">Set hello name of hello storage account toohello variable:</span></span>

```json
"name": "[variables('storageAccountName')]",
```

<span data-ttu-id="2afbd-148">Definir Olá SKU toohello parâmetro:</span><span class="sxs-lookup"><span data-stu-id="2afbd-148">Set hello SKU toohello parameter:</span></span>

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

<span data-ttu-id="2afbd-149">O modelo agora se parece com:</span><span class="sxs-lookup"><span data-stu-id="2afbd-149">Your template now looks like:</span></span>

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

<span data-ttu-id="2afbd-150">Reimplante o modelo modificado hello.</span><span class="sxs-lookup"><span data-stu-id="2afbd-150">Redeploy hello modified template.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2afbd-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2afbd-151">Next steps</span></span>
* <span data-ttu-id="2afbd-152">Para obter informações sobre como usar o hello portal tooexport um modelo, consulte [exportar um modelo do Gerenciador de recursos do Azure de recursos existentes](resource-manager-export-template.md).</span><span class="sxs-lookup"><span data-stu-id="2afbd-152">For information about using hello portal tooexport a template, see [Export an Azure Resource Manager template from existing resources](resource-manager-export-template.md).</span></span>
* <span data-ttu-id="2afbd-153">parâmetros de toodefine no modelo, consulte [criar modelos](resource-group-authoring-templates.md#parameters).</span><span class="sxs-lookup"><span data-stu-id="2afbd-153">toodefine parameters in template, see [Authoring templates](resource-group-authoring-templates.md#parameters).</span></span>
* <span data-ttu-id="2afbd-154">Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).</span><span class="sxs-lookup"><span data-stu-id="2afbd-154">For tips on resolving common deployment errors, see [Troubleshoot common Azure deployment errors with Azure Resource Manager](resource-manager-common-deployment-errors.md).</span></span>