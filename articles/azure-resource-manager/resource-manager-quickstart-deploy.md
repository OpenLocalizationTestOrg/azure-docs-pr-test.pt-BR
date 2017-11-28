---
title: aaaDeploy recursos tooAzure | Microsoft Docs
description: "Use tooAzure de recursos toodeploy Azure PowerShell ou CLI do Azure. Olá recursos são definidos em um modelo do Gerenciador de recursos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 02/16/2017
ms.author: tomfitz
ms.openlocfilehash: 0cd3f8ad45af1fb85c78899b56f6807d00b859f5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deploy-resources-tooazure"></a><span data-ttu-id="2c692-104">Implantar recursos tooAzure</span><span class="sxs-lookup"><span data-stu-id="2c692-104">Deploy resources tooAzure</span></span>

<span data-ttu-id="2c692-105">Este tópico mostra como toodeploy recursos tooyour assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="2c692-105">This topic shows how toodeploy resources tooyour Azure subscription.</span></span> <span data-ttu-id="2c692-106">Você pode usar o Azure PowerShell ou CLI do Azure toodeploy um modelo de Gerenciador de recursos que define a infraestrutura de saudação para sua solução.</span><span class="sxs-lookup"><span data-stu-id="2c692-106">You can use either Azure PowerShell or Azure CLI toodeploy a Resource Manager template that defines hello infrastructure for your solution.</span></span>

<span data-ttu-id="2c692-107">Para uma introdução tooconcepts do Gerenciador de recursos, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2c692-107">For an introduction tooconcepts of Resource Manager, see [Azure Resource Manager overview](resource-group-overview.md).</span></span>

## <a name="steps-for-deployment"></a><span data-ttu-id="2c692-108">Etapas para implantação</span><span class="sxs-lookup"><span data-stu-id="2c692-108">Steps for deployment</span></span>

<span data-ttu-id="2c692-109">Este tópico pressupõe que você está implantando Olá [exemplo de modelo de armazenamento](#example-storage-template) neste tópico.</span><span class="sxs-lookup"><span data-stu-id="2c692-109">This topic assumes you are deploying hello [example storage template](#example-storage-template) in this topic.</span></span> <span data-ttu-id="2c692-110">Você pode usar um modelo diferente, mas parâmetros Olá que passar são diferentes que é mostrado neste tópico.</span><span class="sxs-lookup"><span data-stu-id="2c692-110">You can use a different template, but hello parameters you pass are different than what is shown in this topic.</span></span>

<span data-ttu-id="2c692-111">Depois de criar um modelo, as etapas gerais para implantar o modelo Olá são:</span><span class="sxs-lookup"><span data-stu-id="2c692-111">After creating a template, hello general steps for deploying your template are:</span></span>

1. <span data-ttu-id="2c692-112">Faça logon na conta tooyour</span><span class="sxs-lookup"><span data-stu-id="2c692-112">Log in tooyour account</span></span>
2. <span data-ttu-id="2c692-113">Selecione Olá assinatura toouse (necessário apenas se você tiver várias assinaturas e desejar toouse que não é saudação padrão assinatura)</span><span class="sxs-lookup"><span data-stu-id="2c692-113">Select hello subscription toouse (only necessary if you have multiple subscriptions, and you want toouse one that is not hello default subscription)</span></span>
3. <span data-ttu-id="2c692-114">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="2c692-114">Create a resource group</span></span>
4. <span data-ttu-id="2c692-115">Implante o modelo de saudação</span><span class="sxs-lookup"><span data-stu-id="2c692-115">Deploy hello template</span></span>
5. <span data-ttu-id="2c692-116">Verificar o status da implantação</span><span class="sxs-lookup"><span data-stu-id="2c692-116">Check your deployment status</span></span>

<span data-ttu-id="2c692-117">Olá seções a seguir mostram como tooperform as etapas com [PowerShell](#powershell) ou [CLI do Azure](#azure-cli).</span><span class="sxs-lookup"><span data-stu-id="2c692-117">hello following sections show how tooperform those steps with [PowerShell](#powershell) or [Azure CLI](#azure-cli).</span></span>

## <a name="powershell"></a><span data-ttu-id="2c692-118">PowerShell</span><span class="sxs-lookup"><span data-stu-id="2c692-118">PowerShell</span></span>

1. <span data-ttu-id="2c692-119">tooinstall Azure PowerShell, consulte [Introdução aos cmdlets do PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2c692-119">tooinstall Azure PowerShell, see [Get started with Azure PowerShell cmdlets](/powershell/azure/overview).</span></span>

2. <span data-ttu-id="2c692-120">tooquickly Introdução à implantação, use Olá cmdlets a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c692-120">tooquickly get started with deployment, use hello following cmdlets:</span></span>

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  <span data-ttu-id="2c692-121">Olá `Set-AzureRmContext` cmdlet só é necessário se você quiser toouse uma assinatura diferente de sua assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="2c692-121">hello `Set-AzureRmContext` cmdlet is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="2c692-122">toosee todas as suas assinaturas e seus IDs, use:</span><span class="sxs-lookup"><span data-stu-id="2c692-122">toosee all your subscriptions and their IDs, use:</span></span>

  ```powershell
  Get-AzureRmSubscription
  ```

3. <span data-ttu-id="2c692-123">implantação de saudação pode levar toocomplete de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2c692-123">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="2c692-124">Ao terminar, você verá uma mensagem semelhante à:</span><span class="sxs-lookup"><span data-stu-id="2c692-124">When it finishes, you see a message similar to:</span></span>

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. <span data-ttu-id="2c692-125">toosee sua conta de armazenamento e o grupo de recursos foram implantadas tooyour assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="2c692-125">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. <span data-ttu-id="2c692-126">Você pode especificar os parâmetros de modelo como parâmetros do PowerShell ao implantar um modelo.</span><span class="sxs-lookup"><span data-stu-id="2c692-126">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="2c692-127">Olá exemplo anterior não incluiu quaisquer parâmetros de modelo, para que foram usados valores padrão de saudação no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c692-127">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="2c692-128">toodeploy outro armazenamento de conta e fornecer valores de parâmetro para o prefixo do nome do armazenamento hello e conta de armazenamento Olá SKU, use:</span><span class="sxs-lookup"><span data-stu-id="2c692-128">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  <span data-ttu-id="2c692-129">Agora você tem duas contas de armazenamento no seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2c692-129">You now have two storage accounts in your resource group.</span></span> 

## <a name="azure-cli"></a><span data-ttu-id="2c692-130">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="2c692-130">Azure CLI</span></span>

1. <span data-ttu-id="2c692-131">tooinstall CLI do Azure, consulte [instalar o Azure CLI 2.0](/cli/azure/install-az-cli2).</span><span class="sxs-lookup"><span data-stu-id="2c692-131">tooinstall Azure CLI, see [Install Azure CLI 2.0](/cli/azure/install-az-cli2).</span></span>

2. <span data-ttu-id="2c692-132">tooquickly Introdução à implantação, use Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c692-132">tooquickly get started with deployment, use hello following commands:</span></span>

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  <span data-ttu-id="2c692-133">Olá `az account set` comando só é necessário se você quiser toouse uma assinatura diferente de sua assinatura padrão.</span><span class="sxs-lookup"><span data-stu-id="2c692-133">hello `az account set` command is only needed if you want toouse a subscription other than your default subscription.</span></span> <span data-ttu-id="2c692-134">toosee todas as suas assinaturas e seus IDs, use:</span><span class="sxs-lookup"><span data-stu-id="2c692-134">toosee all your subscriptions and their IDs, use:</span></span>

  ```azurecli
  az account list
  ```

3. <span data-ttu-id="2c692-135">implantação de saudação pode levar toocomplete de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2c692-135">hello deployment can take a few minutes toocomplete.</span></span> <span data-ttu-id="2c692-136">Ao terminar, você verá uma mensagem semelhante à:</span><span class="sxs-lookup"><span data-stu-id="2c692-136">When it finishes, you see a message similar to:</span></span>

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. <span data-ttu-id="2c692-137">toosee sua conta de armazenamento e o grupo de recursos foram implantadas tooyour assinatura, use:</span><span class="sxs-lookup"><span data-stu-id="2c692-137">toosee that your resource group and storage account were deployed tooyour subscription, use:</span></span>

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. <span data-ttu-id="2c692-138">Você pode especificar os parâmetros de modelo como parâmetros do PowerShell ao implantar um modelo.</span><span class="sxs-lookup"><span data-stu-id="2c692-138">You can specify template parameters as PowerShell parameters when deploying a template.</span></span> <span data-ttu-id="2c692-139">Olá exemplo anterior não incluiu quaisquer parâmetros de modelo, para que foram usados valores padrão de saudação no modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="2c692-139">hello earlier example did not include any template parameters, so hello default values in hello template were used.</span></span> <span data-ttu-id="2c692-140">toodeploy outro armazenamento de conta e fornecer valores de parâmetro para o prefixo do nome do armazenamento hello e conta de armazenamento Olá SKU, use:</span><span class="sxs-lookup"><span data-stu-id="2c692-140">toodeploy another storage account, and provide parameter values for hello storage name prefix and hello storage account SKU, use:</span></span>

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  <span data-ttu-id="2c692-141">Agora você tem duas contas de armazenamento no seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="2c692-141">You now have two storage accounts in your resource group.</span></span> 

## <a name="example-storage-template"></a><span data-ttu-id="2c692-142">Modelo de armazenamento de exemplo</span><span class="sxs-lookup"><span data-stu-id="2c692-142">Example storage template</span></span>

<span data-ttu-id="2c692-143">Use Olá toodeploy do modelo de exemplo uma assinatura de tooyour de conta de armazenamento a seguir:</span><span class="sxs-lookup"><span data-stu-id="2c692-143">Use hello following example template toodeploy a storage account tooyour subscription:</span></span>

```json
{
  "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "storageNamePrefix": {
      "type": "string",
      "maxLength": 11,
      "defaultValue": "storage",
      "metadata": {
        "description": "hello value toouse for starting hello storage account name."
      }
    },
    "storageSKU": {
      "type": "string",
      "allowedValues": [
        "Standard_LRS",
        "Standard_ZRS",
        "Standard_GRS",
        "Standard_RAGRS",
        "Premium_LRS"
      ],
      "defaultValue": "Standard_LRS",
      "metadata": {
        "description": "hello type of replication toouse for hello storage account."
      }
    }
  },
  "variables": {
    "storageName": "[concat(parameters('storageNamePrefix'), uniqueString(resourceGroup().id))]"
  },
  "resources": [
    {
      "name": "[variables('storageName')]",
      "type": "Microsoft.Storage/storageAccounts",
      "apiVersion": "2016-05-01",
      "sku": {
        "name": "[parameters('storageSKU')]"
      },
      "kind": "Storage",
      "location": "[resourceGroup().location]",
      "tags": {},
      "properties": {
      }
    }
  ],
  "outputs": {  }
}
```

## <a name="next-steps"></a><span data-ttu-id="2c692-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2c692-144">Next steps</span></span>

* <span data-ttu-id="2c692-145">Para obter informações detalhadas sobre como usar modelos de toodeploy do PowerShell, consulte [implantar recursos com modelos do Gerenciador de recursos e o Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span><span class="sxs-lookup"><span data-stu-id="2c692-145">For detailed information about using PowerShell toodeploy templates, see [Deploy resources with Resource Manager templates and Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).</span></span>
* <span data-ttu-id="2c692-146">Para obter informações detalhadas sobre como usar modelos de toodeploy CLI do Azure, consulte [implantar recursos com modelos do Gerenciador de recursos e a CLI do Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span><span class="sxs-lookup"><span data-stu-id="2c692-146">For detailed information about using Azure CLI toodeploy templates, see [Deploy resources with Resource Manager templates and Azure CLI](/azure/azure-resource-manager/resource-group-template-deploy-cli).</span></span>



