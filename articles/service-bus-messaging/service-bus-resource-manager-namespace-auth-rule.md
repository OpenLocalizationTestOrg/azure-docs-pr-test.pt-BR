---
title: "regra de autorização do barramento de serviço aaaCreate usando o modelo do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Criar uma regra de autorização do Barramento de Serviço para namespace e fila usando um modelo do Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 7f1443a0-5fa8-4d90-8637-1a977ef0b1f0
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 48df97849281d3b47e9d722d4e821c874644be59
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a>Criar uma regra de autorização do Barramento de Serviço para namespace e fila usando um modelo do Azure Resource Manager

Este artigo mostra como toouse um modelo do Gerenciador de recursos do Azure que cria um [regra de autorização](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) para um namespace de barramento de serviço e fila. Você aprenderá como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada. Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.

Para saber mais sobre a criação de modelos, veja [Criando modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].

Para o modelo completo de Olá, consulte Olá [modelo de regra de autorização do barramento de serviço] [ Service Bus auth rule template] no GitHub.

> [!NOTE]
> saudação do Azure Resource Manager modelos a seguir está disponível para download e implantação.
> 
> * [Criar um namespace do Barramento de Serviço](service-bus-resource-manager-namespace.md)
> * [Criar um namespace do Barramento de Serviço com fila](service-bus-resource-manager-namespace-queue.md)
> * [Criar um namespace do Barramento de Serviço com tópico e assinatura](service-bus-resource-manager-namespace-topic.md)
> * [Criar um namespace do Barramento de Serviço com tópico, assinatura e regra](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e procure "Barramento de serviço".
> 
> 

## <a name="what-will-you-deploy"></a>O que você implantará?
Com esse modelo, você implantará uma regra de autorização do Barramento de Serviço para um namespace e uma entidade de sistema de mensagens (nesse caso, uma fila).

O modelo usa [SAS (Assinatura de Acesso Compartilhado)](service-bus-sas.md) para autenticação. O SAS permite que aplicativos tooauthenticate tooService barramento usando uma chave de acesso configurada no namespace hello, ou em Olá entidade (fila ou tópico) de mensagens com os direitos específicos associados. Você pode usar essa chave toogenerate um token SAS que os clientes podem usar tooauthenticate tooService barramento.

toorun Olá implantação automaticamente, clique em Olá botão a seguir:

[![Implantar tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)

## <a name="parameters"></a>parâmetros

No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado. modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello. Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando. Não defina parâmetros para valores sempre ficará Olá mesmo. Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.

modelo de saudação define Olá parâmetros a seguir.

### <a name="servicebusnamespacename"></a>serviceBusNamespaceName
nome de saudação do hello toocreate de namespace de barramento de serviço.

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a>namespaceAuthorizationRuleName
Olá nome da regra de autorização Olá Olá namespace.

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a>serviceBusQueueName
nome de saudação da fila de Olá Olá namespace de barramento de serviço.

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
Cria um namespace do Barramento de Serviço padrão do tipo **Mensagens**e uma regra de autorização do Barramento de Serviço para o namespace e a entidade.

```json
"resources": [
        {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[parameters('serviceBusNamespaceName')]",
            "type": "Microsoft.ServiceBus/namespaces",
            "location": "[variables('location')]",
            "kind": "Messaging",
            "sku": {
                "name": "StandardSku",
                "tier": "Standard"
            },
            "resources": [
                {
                    "apiVersion": "[variables('sbVersion')]",
                    "name": "[parameters('serviceBusQueueName')]",
                    "type": "Queues",
                    "dependsOn": [
                        "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
                    ],
                    "properties": {
                        "path": "[parameters('serviceBusQueueName')]"
                    },
                    "resources": [
                        {
                            "apiVersion": "[variables('sbVersion')]",
                            "name": "[parameters('queueAuthorizationRuleName')]",
                            "type": "authorizationRules",
                            "dependsOn": [
                                "[parameters('serviceBusQueueName')]"
                            ],
                            "properties": {
                                "Rights": ["Listen"]
                            }
                        }
                    ]
                }
            ]
        }, {
            "apiVersion": "[variables('sbVersion')]",
            "name": "[variables('namespaceAuthRuleName')]",
            "type": "Microsoft.ServiceBus/namespaces/authorizationRules",
            "dependsOn": ["[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"],
            "location": "[resourceGroup().location]",
            "properties": {
                "Rights": ["Send"]
            }
        }
    ]
```

## <a name="commands-toorun-deployment"></a>Implantação de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a>CLI do Azure
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a>Próximas etapas
Agora que você criou e implantou recursos usando o Gerenciador de recursos do Azure, Aprenda como toomanage esses recursos exibindo estes artigos:

* [Gerenciar o Barramento de Serviço com o PowerShell](service-bus-powershell-how-to-provision.md)
* [Gerenciar recursos do barramento de serviço com hello Explorador do barramento de serviço](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [Autenticação e autorização do Barramento de Serviço](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
