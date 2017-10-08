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
# <a name="export-azure-resource-manager-templates-with-powershell"></a>Exportar modelos do Azure Resource Manager com o PowerShell

Gerenciador de recursos permite que você tooexport um modelo do Gerenciador de recursos de recursos existentes em sua assinatura. Você pode usar esse toolearn modelo gerado sobre Olá modelo sintaxe ou tooautomate Olá reimplantação de sua solução, conforme necessário.

É importante toonote que há dois tooexport de formas diferentes um modelo:

* Você pode exportar Olá real do modelo que você usou para uma implantação. modelo exportado Olá inclui todas as variáveis e parâmetros de saudação exatamente como eles eram exibidos no modelo original hello. Essa abordagem é útil quando você precisa tooretrieve um modelo.
* Você pode exportar um modelo que representa o estado atual de Olá Olá do grupo de recursos. modelo exportado Olá não é baseado em qualquer modelo que você usou para a implantação. Em vez disso, ele cria um modelo que é um instantâneo de saudação do grupo de recursos. modelo exportado Olá tem muitos valores embutidos e provavelmente não tantos parâmetros quantos você definiria normalmente. Essa abordagem é útil quando você modificou o grupo de recursos de saudação. Agora, você precisa de grupo de recursos de saudação toocapture como um modelo.

Este tópico mostra as duas abordagens.

## <a name="deploy-a-solution"></a>Implantar uma solução

tooillustrate ambas as abordagens para exportar um modelo, vamos começar com a implantação de uma assinatura de tooyour da solução. Se você já tiver um grupo de recursos em sua assinatura que você deseja tooexport, você não tem toodeploy nesta solução. No entanto, o restante deste artigo Olá refere-se toohello modelo para esta solução. script de exemplo Hello implanta uma conta de armazenamento.

```powershell
New-AzureRmResourceGroup -Name ExampleGroup -Location "South Central US"
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -DeploymentName NewStorage
  -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-storage-account-create/azuredeploy.json
```  

## <a name="save-template-from-deployment-history"></a>Salvar modelo do histórico de implantações

Você pode recuperar um modelo de seu histórico de implantação usando Olá [AzureRmResourceGroupDeploymentTemplate salvar](/powershell/module/azurerm.resources/save-azurermresourcegroupdeploymenttemplate) comando. Olá modelo saudação do exemplo salva anteriormente implantado a seguir:

```powershell
Save-AzureRmResourceGroupDeploymentTemplate -ResourceGroupName ExampleGroup -DeploymentName NewStorage
```

Ele retorna o local de saudação do modelo de saudação.

```powershell
Path
----
C:\Users\exampleuser\NewStorage.json
```

Abra o arquivo hello e observe que é Olá modelo exato usado para a implantação. variáveis e parâmetros de saudação correspondem o modelo de saudação do GitHub. Você pode reimplantar esse modelo.

## <a name="export-resource-group-as-template"></a>Exportar grupo de recursos como modelo

Em vez de recuperar um modelo do histórico de implantação hello, você pode recuperar um modelo que representa o estado atual de saudação de um grupo de recursos usando Olá [AzureRmResourceGroup de exportação](/powershell/module/azurerm.resources/export-azurermresourcegroup) comando. Você usa esse comando quando você fez muitas alterações de grupo de recursos de tooyour e nenhum modelo existente representa todas as alterações de saudação.

```powershell
Export-AzureRmResourceGroup -ResourceGroupName ExampleGroup
```

Ele retorna o local de saudação do modelo de saudação.

```powershell
Path
----
C:\Users\exampleuser\ExampleGroup.json
```

Abra o arquivo hello e observe que é diferente do modelo de saudação no GitHub. Ele tem parâmetros diferentes e nenhuma variável. armazenamento de saudação SKU e local são toovalues embutido. Olá, exemplo a seguir mostra modelo exportado hello, mas seu modelo tem um nome de parâmetro ligeiramente diferentes:

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

Você pode reutilizar esse modelo, mas requer um nome exclusivo para a conta de armazenamento de saudação de adivinhação. nome de saudação do parâmetro é ligeiramente diferente.

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName ExampleGroup `
  -TemplateFile C:\Users\exampleuser\ExampleGroup.json `
  -storageAccounts_nf3mvst4nqb36standardsa_name tfnewstorage0501
```

## <a name="customize-exported-template"></a>Personalizar modelo exportado

Você pode modificar este modelo toomake-toouse mais fácil e mais flexível. tooallow para obter mais locais, alteração Olá local propriedade toouse Olá mesmo local que o grupo de recursos de saudação:

```json
"location": "[resourceGroup().location]",
```

tooavoid ter tooguess um nome de uniques para a conta de armazenamento, remover Olá parâmetro de nome de conta de armazenamento hello. Adicione um parâmetro para um sufixo de nome de armazenamento e um SKU de armazenamento:

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

Adicione uma variável que constrói o nome de conta de armazenamento Olá com função de uniqueString hello:

```json
"variables": {
    "storageAccountName": "[concat(uniquestring(resourceGroup().id), 'standardsa')]"
  },
```

Definir nome de saudação da variável de toohello de conta de armazenamento hello:

```json
"name": "[variables('storageAccountName')]",
```

Definir Olá SKU toohello parâmetro:

```json
"sku": {
    "name": "[parameters('storageAccountType')]",
    "tier": "Standard"
},
```

O modelo agora se parece com:

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

Reimplante o modelo modificado hello.

## <a name="next-steps"></a>Próximas etapas
* Para obter informações sobre como usar o hello portal tooexport um modelo, consulte [exportar um modelo do Gerenciador de recursos do Azure de recursos existentes](resource-manager-export-template.md).
* parâmetros de toodefine no modelo, consulte [criar modelos](resource-group-authoring-templates.md#parameters).
* Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).
