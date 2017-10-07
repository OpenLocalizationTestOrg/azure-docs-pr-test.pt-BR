---
title: local do recurso aaaAzure no modelo | Microsoft Docs
description: Mostra como tooset um local para um recurso em um modelo do Gerenciador de recursos do Azure
services: azure-resource-manager
documentationcenter: 
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/03/2017
ms.author: tomfitz
ms.openlocfilehash: f2ad6ca6ac5f34484a2e5e57dd8d67c77dacc41a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="set-resource-location-in-azure-resource-manager-templates"></a>Configure os locais dos recursos de modelos do Azure Resource Manager
Ao implantar um modelo, é necessário fornecer um local para cada recurso. Este tópico mostra como locais de saudação toodetermine que estão disponíveis tooyour assinatura para cada recurso de tipo.

## <a name="determine-supported-locations"></a>Determinar locais com suporte

Para obter uma lista completa de locais com suporte para cada tipo de recurso, consulte [Produtos disponíveis por região](https://azure.microsoft.com/regions/services/). No entanto, sua assinatura pode não ter acesso tooall Olá locais nessa lista. toosee uma lista personalizada de locais que estão disponíveis tooyour assinatura, use o Azure PowerShell ou CLI do Azure. 

Olá exemplo a seguir usa locais de saudação do PowerShell tooget para Olá `Microsoft.Web\sites` tipo de recurso:

```powershell
((Get-AzureRmResourceProvider -ProviderNamespace Microsoft.Web).ResourceTypes | Where-Object ResourceTypeName -eq sites).Locations
```

Olá exemplo a seguir usa locais de saudação tooget 2.0 do CLI do Azure para Olá `Microsoft.Web\sites` tipo de recurso:

```azurecli
az provider show -n Microsoft.Web --query "resourceTypes[?resourceType=='sites'].locations"
```

## <a name="set-location-in-template"></a>Configurar o local no modelo

Depois de determinar os locais de saudação com suporte para os seus recursos, você precisa tooset local no seu modelo. Olá tooset de maneira mais fácil esse valor é toocreate um recurso de grupo em um local que dá suporte a tipos de recurso hello e defina cada local muito`[resourceGroup().location]`. Você pode reimplantar os grupos de tooresource Olá modelos em diferentes locais e não alterar quaisquer valores no modelo de saudação ou parâmetros. 

Olá, exemplo a seguir mostra uma conta de armazenamento que é implantado toohello mesmo local que o grupo de recursos de saudação:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "variables": {
      "storageName": "[concat('storage', uniqueString(resourceGroup().id))]"
    },
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[variables('storageName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

Se precisar de local de saudação toohardcode em seu modelo, forneça o nome de saudação de uma das regiões Olá com suporte. saudação de exemplo a seguir mostra uma conta de armazenamento sempre é implantado tooNorth centro dos EUA:

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "resources": [
    {
      "apiVersion": "2016-01-01",
      "type": "Microsoft.Storage/storageAccounts",
      "name": "[concat('storageloc', uniqueString(resourceGroup().id))]",
      "location": "North Central US",
      "tags": {
        "Dept": "Finance",
        "Environment": "Production"
      },
      "sku": {
        "name": "Standard_LRS"
      },
      "kind": "Storage",
      "properties": { }
    }
    ]
}
```

## <a name="next-steps"></a>Próximas etapas
* Para obter recomendações sobre como toocreate modelos, consulte [práticas recomendadas para a criação de modelos do Azure Resource Manager](resource-manager-template-best-practices.md).

