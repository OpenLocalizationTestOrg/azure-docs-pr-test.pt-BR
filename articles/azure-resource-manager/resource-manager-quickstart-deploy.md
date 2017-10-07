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
# <a name="deploy-resources-tooazure"></a>Implantar recursos tooAzure

Este tópico mostra como toodeploy recursos tooyour assinatura do Azure. Você pode usar o Azure PowerShell ou CLI do Azure toodeploy um modelo de Gerenciador de recursos que define a infraestrutura de saudação para sua solução.

Para uma introdução tooconcepts do Gerenciador de recursos, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).

## <a name="steps-for-deployment"></a>Etapas para implantação

Este tópico pressupõe que você está implantando Olá [exemplo de modelo de armazenamento](#example-storage-template) neste tópico. Você pode usar um modelo diferente, mas parâmetros Olá que passar são diferentes que é mostrado neste tópico.

Depois de criar um modelo, as etapas gerais para implantar o modelo Olá são:

1. Faça logon na conta tooyour
2. Selecione Olá assinatura toouse (necessário apenas se você tiver várias assinaturas e desejar toouse que não é saudação padrão assinatura)
3. Criar um grupo de recursos
4. Implante o modelo de saudação
5. Verificar o status da implantação

Olá seções a seguir mostram como tooperform as etapas com [PowerShell](#powershell) ou [CLI do Azure](#azure-cli).

## <a name="powershell"></a>PowerShell

1. tooinstall Azure PowerShell, consulte [Introdução aos cmdlets do PowerShell do Azure](/powershell/azure/overview).

2. tooquickly Introdução à implantação, use Olá cmdlets a seguir:

  ```powershell
  Login-AzureRmAccount
  Set-AzureRmContext -SubscriptionID {subscription-id}

  New-AzureRmResourceGroup -Name ExampleGroup -Location "Central US"
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json 
  ```

  Olá `Set-AzureRmContext` cmdlet só é necessário se você quiser toouse uma assinatura diferente de sua assinatura padrão. toosee todas as suas assinaturas e seus IDs, use:

  ```powershell
  Get-AzureRmSubscription
  ```

3. implantação de saudação pode levar toocomplete de alguns minutos. Ao terminar, você verá uma mensagem semelhante à:

  ```powershell
  DeploymentName          : ExampleDeployment
  CorrelationId           : 07b3b233-8367-4a0b-b9bc-7aa189065665
  ResourceGroupName       : ExampleGroup
  ProvisioningState       : Succeeded
  ...
  ```

4. toosee sua conta de armazenamento e o grupo de recursos foram implantadas tooyour assinatura, use:

  ```powershell
  Get-AzureRmResourceGroup -Name ExampleGroup
  Find-AzureRmResource -ResourceGroupNameEquals ExampleGroup
  ```

5. Você pode especificar os parâmetros de modelo como parâmetros do PowerShell ao implantar um modelo. Olá exemplo anterior não incluiu quaisquer parâmetros de modelo, para que foram usados valores padrão de saudação no modelo de saudação. toodeploy outro armazenamento de conta e fornecer valores de parâmetro para o prefixo do nome do armazenamento hello e conta de armazenamento Olá SKU, use:

  ```powershell
  New-AzureRmResourceGroupDeployment -Name ExampleDeployment2 -ResourceGroupName ExampleGroup -TemplateFile c:\MyTemplates\azuredeploy.json -storageNamePrefix "contoso" -storageSKU "Standard_GRS"
  ```

  Agora você tem duas contas de armazenamento no seu grupo de recursos. 

## <a name="azure-cli"></a>CLI do Azure

1. tooinstall CLI do Azure, consulte [instalar o Azure CLI 2.0](/cli/azure/install-az-cli2).

2. tooquickly Introdução à implantação, use Olá comandos a seguir:

  ```azurecli
  az login
  az account set --subscription {subscription-id}

  az group create --name ExampleGroup --location "Central US"
  az group deployment create --name ExampleDeployment --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json
  ```

  Olá `az account set` comando só é necessário se você quiser toouse uma assinatura diferente de sua assinatura padrão. toosee todas as suas assinaturas e seus IDs, use:

  ```azurecli
  az account list
  ```

3. implantação de saudação pode levar toocomplete de alguns minutos. Ao terminar, você verá uma mensagem semelhante à:

  ```azurecli
  "provisioningState": "Succeeded",
  ```

4. toosee sua conta de armazenamento e o grupo de recursos foram implantadas tooyour assinatura, use:

  ```azurecli
  az group show --name ExampleGroup
  az resource list --resource-group ExampleGroup
  ```

5. Você pode especificar os parâmetros de modelo como parâmetros do PowerShell ao implantar um modelo. Olá exemplo anterior não incluiu quaisquer parâmetros de modelo, para que foram usados valores padrão de saudação no modelo de saudação. toodeploy outro armazenamento de conta e fornecer valores de parâmetro para o prefixo do nome do armazenamento hello e conta de armazenamento Olá SKU, use:

  ```azurecli
  az group deployment create --name ExampleDeployment2 --resource-group ExampleGroup --template-file c:\MyTemplates\azuredeploy.json --parameters '{"storageNamePrefix":{"value":"contoso"},"storageSKU":{"value":"Standard_GRS"}}'
  ```

  Agora você tem duas contas de armazenamento no seu grupo de recursos. 

## <a name="example-storage-template"></a>Modelo de armazenamento de exemplo

Use Olá toodeploy do modelo de exemplo uma assinatura de tooyour de conta de armazenamento a seguir:

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

## <a name="next-steps"></a>Próximas etapas

* Para obter informações detalhadas sobre como usar modelos de toodeploy do PowerShell, consulte [implantar recursos com modelos do Gerenciador de recursos e o Azure PowerShell](/azure/azure-resource-manager/resource-group-template-deploy).
* Para obter informações detalhadas sobre como usar modelos de toodeploy CLI do Azure, consulte [implantar recursos com modelos do Gerenciador de recursos e a CLI do Azure](/azure/azure-resource-manager/resource-group-template-deploy-cli).



