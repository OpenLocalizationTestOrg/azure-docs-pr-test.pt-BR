---
title: "namespace de barramento de serviço do Azure aaaCreate e a fila usando o modelo do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Criar um namespace e uma fila do Barramento de Serviço usando um modelo do Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: a6bfb5fd-7b98-4588-8aa1-9d5f91b599b6
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: f230878b7c557bdd80d74da0de5a85ba4ee99ef1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a>Criar um namespace e uma fila do Barramento de Serviço usando um modelo do Azure Resource Manager

Este artigo mostra como toouse um modelo do Gerenciador de recursos do Azure que cria um namespace de barramento de serviço e uma fila no namespace. Você aprenderá como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada. Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.

Para saber mais sobre a criação de modelos, veja [Criando modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].

Para o modelo completo de Olá, consulte Olá [modelo de namespace e fila do barramento de serviço] [ Service Bus namespace and queue template] no GitHub.

> [!NOTE]
> saudação do Azure Resource Manager modelos a seguir está disponível para download e implantação.
> 
> * [Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)](service-bus-resource-manager-namespace-auth-rule.md)
> * [Criar um namespace do Barramento de Serviço com tópico e assinatura](service-bus-resource-manager-namespace-topic.md)
> * [Criar um namespace do Barramento de Serviço](service-bus-resource-manager-namespace.md)
> * [Criar um namespace do Barramento de Serviço com tópico, assinatura e regra](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e procure "Barramento de serviço".
> 
> 

## <a name="what-will-you-deploy"></a>O que você implantará?

Com este modelo, você implantará um namespace de Barramento de Serviço com uma fila.

[Filas do barramento de serviço](service-bus-queues-topics-subscriptions.md#queues) oferecem primeiro a entrar, tooone de entrega de mensagem PEPS (primeiro) ou mais consumidores concorrentes.

toorun Olá implantação automaticamente, clique em Olá botão a seguir:

[![Implantar tooAzure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)

## <a name="parameters"></a>parâmetros

No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado. modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello. Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando. Não defina parâmetros para valores sempre ficará Olá mesmo. Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.

modelo de saudação define Olá parâmetros a seguir.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
nome de saudação do hello toocreate de namespace de barramento de serviço.

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of hello Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a>serviceBusQueueName
nome de saudação da fila de Olá criada no namespace de barramento de serviço hello.

```json
"serviceBusQueueName": {
"type": "string"
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
Cria um namespace de Barramento de Serviço padrão do tipo **Mensagens**, com uma fila.

```json
"resources ": [{
        "apiVersion": "[variables('sbVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "resources": [{
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusQueueName')]",
            "type": "Queues",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusQueueName')]",
            }
        }]
    }]
```

## <a name="commands-toorun-deployment"></a>Implantação de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a>PowerShell

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a>CLI do Azure

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a>Próximas etapas
Agora que você criou e implantou recursos usando o Gerenciador de recursos do Azure, Aprenda como toomanage esses recursos exibindo estes artigos:

* [Gerenciar o Barramento de Serviço com o PowerShell](service-bus-manage-with-ps.md)
* [Gerenciar recursos do barramento de serviço com hello Explorador do barramento de serviço](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
