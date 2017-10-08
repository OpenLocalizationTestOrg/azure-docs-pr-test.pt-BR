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
# <a name="deploy-azure-resources-toomore-than-one-resource-group"></a>Implantar recursos do Azure toomore que um grupo de recursos

Normalmente, você implanta todos os recursos de saudação em seu modelo tooa único grupo de recursos. No entanto, há situações em que você deseja toodeploy um conjunto de recursos juntos mas colocá-los em grupos de recursos diferentes. Por exemplo, você talvez queira toodeploy Olá backup virtual machine para local e o grupo de recursos separado do Azure Site Recovery tooa. Gerenciador de recursos permite que você toouse aninhado modelos tootarget diferentes grupos de recursos que o grupo de recursos de saudação usado para Olá pai modelo.

grupo de recursos de saudação é o contêiner de ciclo de vida de Olá para o aplicativo hello e sua coleção de recursos. Criar grupo de recursos de saudação fora do modelo Olá e especificar Olá tootarget de grupo de recursos durante a implantação. Para grupos de tooresource uma introdução, consulte [visão geral do Gerenciador de recursos do Azure](resource-group-overview.md).

## <a name="example-template"></a>Modelo de exemplo

tootarget um recurso diferente, você deve usar um modelo aninhado ou vinculado durante a implantação. Olá `Microsoft.Resources/deployments` tipo de recurso fornece um `resourceGroup` parâmetro que permite que você toospecify um grupo de recursos diferente para Olá aninhados a implantação. Todos os grupos de recursos de saudação devem existir antes de executar a implantação de saudação. exemplo a seguir Hello implanta duas contas de armazenamento - um em grupo de recursos de saudação especificado durante a implantação e um em um grupo de recursos denominado `crossResourceGroupDeployment`:

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

Se você definir `resourceGroup` toohello o nome de um grupo de recursos que não existe, a implantação de saudação falha. Se você não fornecer um valor para `resourceGroup`, grupo de recursos pai Olá usa o Gerenciador de recursos.  

## <a name="deploy-hello-template"></a>Implante o modelo de saudação

modelo de exemplo hello toodeploy, você pode usar o portal hello, o Azure PowerShell ou CLI do Azure. Para o Azure PowerShell ou a CLI do Azure, você pode usar uma versão de maio de 2017 ou posterior. exemplos de Olá presumem que você salvou o modelo de saudação localmente como um arquivo chamado **crossrgdeployment.json**.

Para o PowerShell:

```powershell
Login-AzureRmAccount

New-AzureRmResourceGroup -Name mainResourceGroup -Location "South Central US"
New-AzureRmResourceGroup -Name crossResourceGroupDeployment -Location "Central US"
New-AzureRmResourceGroupDeployment -Name ExampleDeployment -ResourceGroupName mainResourceGroup `
  -TemplateFile c:\MyTemplates\crossrgdeployment.json
```

Para a CLI do Azure:

```azurecli
az login

az group create --name mainResourceGroup --location "South Central US"
az group create --name crossResourceGroupDeployment --location "Central US"
az group deployment create \
    --name ExampleDeployment \
    --resource-group mainResourceGroup \
    --template-file crossrgdeployment.json
```

Após a implantação ser concluída, você verá dois grupos de recursos. Cada grupo de recursos contém uma conta de armazenamento.

## <a name="use-resourcegroup-function"></a>Use a função resourceGroup()

Para cruzada implantações de grupos de recursos, hello [resouceGroup() função](resource-group-template-functions-resource.md#resourcegroup) resolve diferente com base em como você especifica o modelo aninhado hello. 

Se você inserir um modelo dentro de outro modelo, resouceGroup() modelo aninhado Olá resolve toohello grupo de recursos de pai. Um modelo incorporado usa Olá formato a seguir:

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

Se você vincular um modelo separado tooa, resouceGroup() no modelo vinculado Olá resolve toohello grupo de recursos aninhados. Um modelo vinculado usa Olá formato a seguir:

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

## <a name="next-steps"></a>Próximas etapas

* toounderstand como toodefine parâmetros em seu modelo, consulte [entender a estrutura de saudação e a sintaxe de modelos do Azure Resource Manager](resource-group-authoring-templates.md).
* Para dicas sobre como resolver erros de implantação, consulte [Solução de erros comuns de implantação do Azure com o Azure Resource Manager](resource-manager-common-deployment-errors.md).
* Para obter mais informações sobre a implantação de um modelo que exija um token SAS, veja [Implantar modelo particular com o token SAS](resource-manager-powershell-sas-token.md).
