---
title: "aaaCreate assinatura de tópico do barramento de serviço do Azure e a regra usando o modelo do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Criar um namespace do Barramento de Serviço com tópico, assinatura e regra usando um modelo do Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 9e0aaf58-0214-4bca-bd00-d29c08f9b1bc
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: dbc46da8491aee4d0c73bd4db90c696008920df4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a>Criar um namespace do Barramento de Serviço com tópico, assinatura e regra usando um modelo do Azure Resource Manager

Este artigo mostra como toouse um modelo do Gerenciador de recursos do Azure que cria um namespace de barramento de serviço com um tópico, a assinatura e a regra (filtro). Você aprenderá como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada. Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos

Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].

Para saber mais sobre as práticas e os padrões de convenções de nomenclatura de recursos do Azure, confira [Convenções de nomenclatura recomendandas para os recursos do Azure][Recommended naming conventions for Azure resources].

Para o modelo completo de Olá, consulte Olá [namespace de barramento de serviço com o tópico, a assinatura e a regra] [ Service Bus namespace with topic, subscription, and rule] modelo.

> [!NOTE]
> saudação do Azure Resource Manager modelos a seguir está disponível para download e implantação.
> 
> * [Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)](service-bus-resource-manager-namespace-auth-rule.md)
> * [Criar um namespace do Barramento de Serviço com fila](service-bus-resource-manager-namespace-queue.md)
> * [Criar um namespace do Barramento de Serviço](service-bus-resource-manager-namespace.md)
> * [Criar um namespace do Barramento de Serviço com tópico e assinatura](service-bus-resource-manager-namespace-topic.md)
> 
> toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e pesquisa para o barramento de serviço.
> 
> 

## <a name="what-will-you-deploy"></a>O que você implantará?

Com este modelo, você implantará um namespace de Barramento de Serviço com tópico, assinatura e regra (filtro).

Os [tópicos e as assinaturas do Barramento de Serviço](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) fornecem uma forma de comunicação de um para muitos, em um padrão de *publicação/assinatura*. Ao usar tópicos e assinaturas, componentes de um aplicativo distribuído não se comunicam diretamente com o outro, em vez disso, eles trocam mensagens por meio do tópico que atua como um intermediário. Um tópico de tooa de assinatura é semelhante a uma fila virtual que recebe cópias das mensagens que foram enviadas toohello tópico. Um filtro de assinatura permite que você toospecify quais mensagens enviadas tópico tooa deve aparecer dentro de uma assinatura de tópico específico.

## <a name="what-are-rules-filters"></a>O que são regras (filtros)?

Em muitos cenários, as mensagens com características específicas precisam ser processadas de maneiras diferentes. tooenable isso, você pode configurar assinaturas toofind mensagens que têm propriedades específicas e, em seguida, executam propriedades de toothose modificações. Embora as assinaturas do barramento de serviço vejam todas as mensagens enviadas toohello tópico, você só pode copiar um subconjunto da fila de assinatura virtual de toohello mensagens. Isso é feito usando filtros de assinatura. toolearn mais informações sobre regras (filtros), consulte [regras e ações](service-bus-queues-topics-subscriptions.md#rules-and-actions).

toorun Olá implantação automaticamente, clique em Olá botão a seguir:

[![Implantar tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)

## <a name="parameters"></a>parâmetros

No Gerenciador de recursos do Azure, você deve definir parâmetros para os valores desejados toospecify quando Olá modelo é implantado. modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello. Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando. Não defina parâmetros para valores que permanecem sempre Olá mesmo. Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.

modelo de saudação define Olá parâmetros a seguir:

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
nome de saudação do hello toocreate de namespace de barramento de serviço.

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a>serviceBusTopicName
nome de saudação do tópico de Olá criado no namespace de barramento de serviço hello.

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a>serviceBusSubscriptionName
nome de saudação da assinatura de saudação criada no namespace de barramento de serviço hello.

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a>serviceBusRuleName
nome de saudação do hello rule(filter) criado no namespace de barramento de serviço hello.

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a>serviceBusApiVersion
versão de API do barramento de serviço de saudação do modelo de saudação.

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a>Recursos toodeploy
Cria um namespace de Barramento de Serviço padrão do tipo **Mensagens**, com tópico, assinatura e regras.

```json
 "resources": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "sku": {
            "name": "Standard",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]"
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {},
                "resources": [{
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusRuleName')]",
                    "type": "Rules",
                    "dependsOn": [
                        "[parameters('serviceBusSubscriptionName')]"
                    ],
                    "properties": {
                        "filter": {
                            "sqlExpression": "StoreName = 'Store1'"
                        },
                        "action": {
                            "sqlExpression": "set FilterTag = 'true'"
                        }
                    }
                }]
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>Implantação de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a>CLI do Azure
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a>Próximas etapas
Agora que você criou e implantou recursos usando o Gerenciador de recursos do Azure, Aprenda como toomanage esses recursos exibindo estes artigos:

* [Gerenciar o Barramento de Serviço do Azure](service-bus-management-libraries.md)
* [Gerenciar o Barramento de Serviço com o PowerShell](service-bus-manage-with-ps.md)
* [Gerenciar recursos do barramento de serviço com hello Explorador do barramento de serviço](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

