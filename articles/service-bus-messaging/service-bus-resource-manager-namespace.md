---
title: "namespace de barramento de serviço aaaCreate usando um modelo do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Use o Gerenciador de recursos do Azure modelo toocreate um namespace de barramento de serviço"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: dc0d6482-6344-4cef-8644-d4573639f5e4
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: fddf370affe761a734991ae9b60c1e5825e54ef7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-using-an-azure-resource-manager-template"></a>Criar um namespace do Barramento de Serviço usando um modelo do Azure Resource Manager

Este artigo descreve como toouse um modelo do Gerenciador de recursos do Azure que cria um namespace de barramento de serviço do tipo **mensagens** com um SKU Standard/Basic. artigo Olá também define os parâmetros de saudação que são especificados para a execução de saudação da implantação de saudação. Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.

Para saber mais sobre a criação de modelos, veja [Criando modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].

Para o modelo completo de Olá, consulte Olá [modelo de namespace do barramento de serviço] [ Service Bus namespace template] no GitHub.

> [!NOTE]
> saudação do Azure Resource Manager modelos a seguir está disponível para download e implantação. 
> 
> * [Criar um namespace do Barramento de Serviço com fila](service-bus-resource-manager-namespace-queue.md)
> * [Criar um namespace do Barramento de Serviço com tópico e assinatura](service-bus-resource-manager-namespace-topic.md)
> * [Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)](service-bus-resource-manager-namespace-auth-rule.md)
> * [Criar um namespace do Barramento de Serviço com tópico, assinatura e regra](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e pesquisa para o barramento de serviço.
> 
> 

## <a name="what-will-you-deploy"></a>O que você implantará?
Com esse modelo, você implantará um namespace de Barramento de Serviço com uma SKU [Básica, Standard ou Premium](https://azure.microsoft.com/pricing/details/service-bus/).

toorun Olá implantação automaticamente, clique em Olá botão a seguir:

[![Implantar tooAzure](./media/service-bus-resource-manager-namespace/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-servicebus-create-namespace%2Fazuredeploy.json)

## <a name="parameters"></a>parâmetros
No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado. modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello. Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando. Não defina parâmetros para valores sempre ficará Olá mesmo. Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.

Esse modelo define Olá parâmetros a seguir.

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

### <a name="servicebussku"></a>serviceBusSKU
nome de saudação do hello barramento de serviço [SKU](https://azure.microsoft.com/pricing/details/service-bus/) toocreate.

```json
"serviceBusSku": { 
    "type": "string", 
    "allowedValues": [ 
        "Basic", 
        "Standard",
        "Premium" 
    ], 
    "defaultValue": "Standard", 
    "metadata": { 
        "description": "hello messaging tier for service Bus namespace" 
    } 

```

modelo de saudação define os valores de saudação que são permitidos para este parâmetro (Basic, Standard ou Premium) e atribui um valor padrão (padrão) se nenhum valor for especificado.

Para saber mais sobre os preços do Barramento de Serviço, confira [Preços e cobrança do Barramento de Serviço][Service Bus pricing and billing].

### <a name="servicebusapiversion"></a>serviceBusApiVersion
versão de API do barramento de serviço de saudação do modelo de saudação.

```json
"serviceBusApiVersion": { 
       "type": "string", 
       "defaultValue": "2015-08-01", 
       "metadata": { 
           "description": "Service Bus ApiVersion used by hello template" 
       } 
```

## <a name="resources-toodeploy"></a>Recursos toodeploy
### <a name="service-bus-namespace"></a>Namespace do Barramento de Serviço
Cria um namespace do Barramento de Serviço padrão do tipo **Mensagens**.

```json
"resources": [
    {
        "apiVersion": "[parameters('serviceBusApiVersion')]",
        "name": "[parameters('serviceBusNamespaceName')]",
        "type": "Microsoft.ServiceBus/Namespaces",
        "location": "[variables('location')]",
        "kind": "Messaging",
        "sku": {
            "name": "StandardSku",
            "tier": "Standard"
        },
        "properties": {
        }
    }
]
```

## <a name="commands-toorun-deployment"></a>Implantação de toorun de comandos
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a>PowerShell
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName <resource-group-name> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

### <a name="azure-cli"></a>CLI do Azure
```azurecli
azure config mode arm

azure group deployment create <my-resource-group> <my-deployment-name> --template-uri https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/101-servicebus-create-namespace/azuredeploy.json
```

## <a name="next-steps"></a>Próximas etapas
Agora que você criou e implantou recursos usando o Gerenciador de recursos do Azure, Aprenda como toomanage esses recursos ao ler estes artigos:

* [Gerenciar o Barramento de Serviço com o PowerShell](service-bus-manage-with-ps.md)
* [Gerenciar recursos do barramento de serviço com hello Explorador do barramento de serviço](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace template]: https://github.com/Azure/azure-quickstart-templates/blob/master/101-servicebus-create-namespace/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Service Bus pricing and billing]: service-bus-pricing-billing.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
