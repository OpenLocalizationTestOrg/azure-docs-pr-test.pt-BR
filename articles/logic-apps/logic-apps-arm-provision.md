---
title: "aaaCreate um aplicativo lógico usando um modelo no Azure | Microsoft Docs"
description: "Use um modelo de Gerenciador de recursos do Azure toodeploy um aplicativo lógico para definir fluxos de trabalho."
services: logic-apps
documentationcenter: 
author: MandiOhlinger
manager: anneta
editor: 
ms.assetid: 7574cc7c-e5a1-4b7c-97f6-0cffb1a5d536
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2016
ms.author: LADocs; mandia
ms.openlocfilehash: efbacb534fc7f11e9b593aae4383480ce3a1752f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-logic-app-using-a-template"></a>Crie um Aplicativo Lógico usando um modelo
Modelos fornecem uma maneira rápida toouse conectores diferentes dentro de um aplicativo de lógica. Aplicativos lógicos inclui modelos do Gerenciador de recursos do Azure para toocreate um aplicativo de lógica que pode ser usado toodefine fluxos de trabalho comerciais. Você pode definir quais recursos são implantados e como toodefine parâmetros quando você implanta o aplicativo lógico. Você pode usar este modelo para seus próprios cenários de negócios ou personalizá-lo toomeet seus requisitos.

Para obter mais detalhes sobre propriedades do aplicativo hello lógica, consulte [lógica de API de gerenciamento de fluxo de trabalho de aplicativo](https://msdn.microsoft.com/library/azure/mt643788.aspx). 

Para obter exemplos de definição de saudação em si, consulte [definições de aplicativo de lógica de autor](logic-apps-author-definitions.md). 

Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md).

Para o modelo do hello completa, consulte [modelo de aplicativo lógico](https://github.com/Azure/azure-quickstart-templates/blob/master/101-logic-app-create/azuredeploy.json).

## <a name="what-you-deploy"></a>O que você implanta
Neste modelo, você implanta um aplicativo lógico.

implantação de saudação toorun automaticamente, selecione Olá botão a seguir:  

[![Implantar tooAzure](media/logic-apps-arm-provision/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-logic-app-create%2Fazuredeploy.json)

## <a name="parameters"></a>parâmetros
[!INCLUDE [app-service-logic-deploy-parameters](../../includes/app-service-logic-deploy-parameters.md)]

### <a name="testuri"></a>testUri
     "testUri": {
        "type": "string",
        "defaultValue": "http://azure.microsoft.com/en-us/status/feed/"
      }

## <a name="resources-toodeploy"></a>Recursos toodeploy
### <a name="logic-app"></a>Aplicativo lógico
Cria um aplicativo de lógica de saudação.

modelos de saudação usa um valor de parâmetro para o nome do aplicativo hello lógica. Ele define o local de saudação do hello lógica aplicativo toohello mesmo local que o grupo de recursos de saudação. 

Esta definição específica é executado uma vez por hora e pings Olá local especificado em Olá **testUri** parâmetro. 

    {
      "type": "Microsoft.Logic/workflows",
      "apiVersion": "2016-06-01",
      "name": "[parameters('logicAppName')]",
      "location": "[resourceGroup().location]",
      "tags": {
        "displayName": "LogicApp"
      },
      "properties": {
        "definition": {
          "$schema": "http://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
          "contentVersion": "1.0.0.0",
          "parameters": {
            "testURI": {
              "type": "string",
              "defaultValue": "[parameters('testUri')]"
            }
          },
          "triggers": {
            "recurrence": {
              "type": "recurrence",
              "recurrence": {
                "frequency": "Hour",
                "interval": 1
              }
            }
          },
          "actions": {
            "http": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('testUri')"
              },
              "runAfter": {}
            }
          },
          "outputs": {}
        },
        "parameters": {}
      }
    }


## <a name="commands-toorun-deployment"></a>Implantação de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
    New-AzureRmResourceGroupDeployment -TemplateUri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -ResourceGroupName ExampleDeployGroup

### <a name="azure-cli"></a>CLI do Azure
    azure group deployment create --template-uri https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-logic-app-create/azuredeploy.json -g ExampleDeployGroup



