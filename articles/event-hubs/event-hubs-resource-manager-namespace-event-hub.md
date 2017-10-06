---
title: um grupo de namespace e do consumidor de Hubs de eventos do Azure usando um modelo de aaaCreate | Microsoft Docs
description: Criar um namespace de Hubs de Eventos com um Hub de Eventos e um grupo de consumidores usando modelos do Azure Resource Manager
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a>Criar um namespace dos Hubs de Eventos com um hub de eventos e um grupo de consumidores usando um modelo do Azure Resource Manager

Este artigo mostra como toouse um modelo do Gerenciador de recursos do Azure que cria um namespace do tipo de Hubs de eventos, com um evento e um grupo de consumidores. Olá artigo mostra como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada. Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos

Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].

Para o modelo completo de Olá, consulte Olá [modelo de grupo de hub e consumidor de evento] [ Event Hub and consumer group template] no GitHub.

> [!NOTE]
> toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e pesquisa para Hubs de eventos.
> 
> 

## <a name="what-will-you-deploy"></a>O que você implantará?
Com este modelo, você implantará um namespace Hubs de Evento com um hub de eventos e um grupo de consumidores.

[Hubs de eventos](event-hubs-what-is-event-hubs.md) é um evento de processamento de serviço usado tooprovide eventos e telemetria entrada tooAzure em grande escala, com baixa latência e alta confiabilidade.

toorun Olá implantação automaticamente, clique em Olá botão a seguir:

[![Implantar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)

## <a name="parameters"></a>parâmetros
No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado. modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello. Você deve definir um parâmetro para os valores que variam, com base em projeto Olá que estiver implantando ou com base em Olá ambiente toowhich que você está implantando. Não defina parâmetros para valores que permanecem sempre Olá mesmo. Cada valor de parâmetro no modelo de saudação define os recursos de saudação que são implantados.

modelo de saudação define Olá parâmetros a seguir:

### <a name="eventhubnamespacename"></a>eventHubNamespaceName
nome de saudação do hello toocreate de namespace de Hubs de eventos.

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a>eventHubName
nome de saudação do hub de eventos de saudação criado no namespace de Hubs de eventos de saudação.

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a>eventHubConsumerGroupName
nome de saudação do grupo de consumidor Olá criado para o hub de eventos de saudação.

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a>apiVersion
versão de API de saudação do modelo de hello.

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a>Recursos toodeploy
Cria um namespace do tipo **EventHubs**, com um hub de eventos e um grupo de consumidores.

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a>Implantação de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a>CLI do Azure
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a>Próximas etapas
Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:

* [Visão Geral dos Hubs de Eventos](event-hubs-what-is-event-hubs.md)
* [Criar um hub de eventos](event-hubs-create.md)
* [Perguntas frequentes sobre os Hubs de Eventos](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
