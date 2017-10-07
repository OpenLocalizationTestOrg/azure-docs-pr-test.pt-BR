---
title: recursos do Azure Service Bus aaaCreate usando modelos do Gerenciador de recursos do Azure | Microsoft Docs
description: "Usar o Gerenciador de recursos do Azure modelos tooautomate Olá criação de recursos do barramento de serviço"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 24f6a207-0fa4-49cf-8a58-963f9e2fd655
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm
ms.openlocfilehash: e539902cae307b63ae7c332580e2064761331ec5
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-service-bus-resources-using-azure-resource-manager-templates"></a>Criar recursos do Barramento de Serviço usando modelos do Azure Resource Manager

Este artigo descreve como toocreate e implantar recursos de barramento de serviço usando o provedor de recursos do barramento de serviço hello, PowerShell e modelos do Azure Resource Manager.

Modelos do Gerenciador de recursos do Azure ajudarão-lo a definir Olá toodeploy de recursos para uma solução e toospecify parâmetros e variáveis que permitem valores tooinput para ambientes diferentes. Olá modelo consiste em JSON e expressões que você pode usar valores de tooconstruct para sua implantação. Para obter informações detalhadas sobre como escrever modelos do Gerenciador de recursos do Azure e uma discussão sobre o formato de saudação de modelo, consulte [estrutura e a sintaxe de modelos do Azure Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

> [!NOTE]
> Olá exemplos mostram esse artigo como toouse toocreate do Gerenciador de recursos do Azure um namespace de barramento de serviço e de entidade (fila) de mensagens. Para obter outros exemplos de modelo, visite Olá [Galeria de modelos de início rápido do Azure] [ Azure Quickstart Templates gallery] e procure "Barramento de serviço".
>
>

## <a name="service-bus-resource-manager-templates"></a>Modelos do Gerenciador de Recursos do Barramento de Serviço

Esses modelos do Azure Resource Manager no Barramento de Serviço estão disponíveis para download e implantação. Clique em Olá seguindo os links para obter detalhes sobre cada um, com modelos de toohello links no GitHub:

* [Criar um namespace do Barramento de Serviço](service-bus-resource-manager-namespace.md)
* [Criar um namespace do Barramento de Serviço com fila](service-bus-resource-manager-namespace-queue.md)
* [Criar um namespace do Barramento de Serviço com tópico e assinatura](service-bus-resource-manager-namespace-topic.md)
* [Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)](service-bus-resource-manager-namespace-auth-rule.md)
* [Criar um namespace do Barramento de Serviço com tópico, assinatura e regra](service-bus-resource-manager-namespace-topic-with-rule.md)

## <a name="deploy-with-powershell"></a>Implantação com o PowerShell

Olá procedimento a seguir descreve como toouse PowerShell toodeploy um modelo do Gerenciador de recursos do Azure que cria um **padrão** camada namespace de barramento de serviço e uma fila no namespace. Este exemplo é baseado no hello [criar um namespace de barramento de serviço com a fila](https://github.com/Azure/azure-quickstart-templates/tree/master/201-servicebus-create-queue) modelo. fluxo de trabalho aproximado Olá é o seguinte:

1. Instale o PowerShell.
2. Crie modelo hello e (opcionalmente) um arquivo de parâmetro.
3. No PowerShell, faça logon no tooyour conta do Azure.
4. Crie um novo grupo de recursos se já não tiver um.
5. Testar a implantação de saudação.
6. Se desejar, defina o modo de implantação de saudação.
7. Implante o modelo de saudação.

Para obter informações completas sobre a implantação de modelos do Azure Resource Manager, consulte [Implantar recursos com modelos do Azure Resource Manager][Deploy resources with Azure Resource Manager templates].

### <a name="install-powershell"></a>Instalar o PowerShell

Instale o Azure PowerShell, seguindo as instruções de saudação do [Introdução ao Azure PowerShell](/powershell/azure/get-started-azureps).

### <a name="create-a-template"></a>Criar um modelo

Olá clone ou copie [201 servicebus-criar-fila](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.json) modelo do GitHub:

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2014-04-01-preview/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Service Bus namespace"
            }
        },
        "serviceBusQueueName": {
            "type": "string",
            "metadata": {
                "description": "Name of hello Queue"
            }
        },
        "serviceBusApiVersion": {
            "type": "string",
            "defaultValue": "2015-08-01",
            "metadata": {
                "description": "Service Bus ApiVersion used by hello template"
            }
        }
    },
    "variables": {
        "location": "[resourceGroup().location]",
        "sbVersion": "[parameters('serviceBusApiVersion')]",
        "defaultSASKeyName": "RootManageSharedAccessKey",
        "authRuleResourceId": "[resourceId('Microsoft.ServiceBus/namespaces/authorizationRules', parameters('serviceBusNamespaceName'), variables('defaultSASKeyName'))]"
    },
    "resources": [{
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
                "path": "[parameters('serviceBusQueueName')]"
            }
        }]
    }],
    "outputs": {
        "NamespaceConnectionString": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryConnectionString]"
        },
        "SharedAccessPolicyPrimaryKey": {
            "type": "string",
            "value": "[listkeys(variables('authRuleResourceId'), variables('sbVersion')).primaryKey]"
        }
    }
}
```

### <a name="create-a-parameters-file-optional"></a>Criar um arquivo de parâmetros (opcional)

toouse um arquivo de parâmetros opcionais, Olá cópia [201 servicebus-criar-fila](https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/azuredeploy.parameters.json) arquivo. Substituir valor de saudação do `serviceBusNamespaceName` com o nome de saudação do namespace de barramento de serviço Olá desejado toocreate nesta implantação e substituir o valor de saudação de `serviceBusQueueName` com o nome de saudação da fila de saudação você deseja toocreate.

```json
{
    "$schema": "http://schema.management.azure.com/schemas/2015-01-01/deploymentParameters.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "serviceBusNamespaceName": {
            "value": "<myNamespaceName>"
        },
        "serviceBusQueueName": {
            "value": "<myQueueName>"
        },
        "serviceBusApiVersion": {
            "value": "2015-08-01"
        }
    }
}
```

Para obter mais informações, consulte Olá [parâmetros](../azure-resource-manager/resource-group-template-deploy.md#parameter-files) tópico.

### <a name="log-in-tooazure-and-set-hello-azure-subscription"></a>Faça logon no tooAzure e defina Olá assinatura do Azure

Em um prompt do PowerShell, execute Olá comando a seguir:

```powershell
Login-AzureRmAccount
```

Você é solicitado toolog em tooyour conta do Azure. Depois de fazer logon, execute Olá tooview de comando a seguir as assinaturas disponíveis.

```powershell
Get-AzureRMSubscription
```

Esse comando retorna uma lista de assinaturas do Azure disponíveis. Escolha uma assinatura para Olá a sessão atual executando o comando a seguir de saudação. Substituir `<YourSubscriptionId>` com hello GUID para Olá assinatura do Azure, você deseja toouse.

```powershell
Set-AzureRmContext -SubscriptionID <YourSubscriptionId>
```

### <a name="set-hello-resource-group"></a>Grupo de recursos de saudação do conjunto

Se você não tiver um recurso existente do grupo, crie um novo grupo de recursos com hello * * AzureRmResourceGroup New * * comando. Fornece nome de saudação do grupo de recursos de saudação e local que você deseja toouse. Por exemplo:

```powershell
New-AzureRmResourceGroup -Name MyDemoRG -Location "West US"
```

Se for bem-sucedido, será exibido um resumo do novo grupo de recursos hello.

```powershell
ResourceGroupName : MyDemoRG
Location          : westus
ProvisioningState : Succeeded
Tags              :
ResourceId        : /subscriptions/<GUID>/resourceGroups/MyDemoRG
```

### <a name="test-hello-deployment"></a>Implantação de saudação do teste

Valide a implantação executando Olá `Test-AzureRmResourceGroupDeployment` cmdlet. Ao testar a implantação de hello, forneça parâmetros exatamente como faria ao executar implantação hello.

```powershell
Test-AzureRmResourceGroupDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="create-hello-deployment"></a>Criar implantação Olá

toocreate Olá nova execução de implantação, Olá `New-AzureRmResourceGroupDeployment` cmdlet e forneça os parâmetros necessários do hello quando solicitado. parâmetros de saudação incluem um nome para sua implantação, nome de saudação do seu grupo de recursos e o caminho de saudação ou o arquivo de modelo de toohello de URL. Se hello **modo** parâmetro não for especificado, Olá valor padrão de **Incremental** é usado. Para saber mais, consulte [Implantações incrementais e completas](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments).

Olá prompts de comando a seguir é para parâmetros de saudação três na janela do PowerShell hello:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

toospecify um arquivo de parâmetros em vez disso, use Olá comando a seguir.

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -TemplateParameterFile <path tooparameters file>\azuredeploy.parameters.json
```

Você também pode usar parâmetros embutido quando você executa o cmdlet de implantação de saudação. comando Olá é o seguinte:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json -parameterName "parameterValue"
```

toorun um [completa](../azure-resource-manager/resource-group-template-deploy.md#incremental-and-complete-deployments) de implantação, Olá conjunto **modo** parâmetro muito**concluir**:

```powershell
New-AzureRmResourceGroupDeployment -Name MyDemoDeployment -Mode Complete -ResourceGroupName MyDemoRG -TemplateFile <path tootemplate file>\azuredeploy.json
```

### <a name="verify-hello-deployment"></a>Verificar a implantação de saudação
Se os recursos de saudação são implantados com êxito, um resumo de implantação de saudação é exibido na janela do PowerShell Olá:

```powershell
DeploymentName    : MyDemoDeployment
ResourceGroupName : MyDemoRG
ProvisioningState : Succeeded
Timestamp         : 4/19/2016 10:38:30 PM
Mode              : Incremental
TemplateLink      :
Parameters        :
                    Name             Type                       Value
                    ===============  =========================  ==========
                    serviceBusNamespaceName  String             <namespaceName>
                    serviceBusQueueName  String                 <queueName>
                    serviceBusApiVersion  String                2015-08-01

```

## <a name="next-steps"></a>Próximas etapas
Agora você viu fluxo de trabalho básico hello e comandos para a implantação de um modelo do Gerenciador de recursos do Azure. Para obter mais informações, visite Olá links a seguir:

* [Visão geral do Azure Resource Manager][Azure Resource Manager overview]
* [Implantar recursos com modelos do Resource Manager e o Azure PowerShell][Deploy resources with Azure Resource Manager templates]
* [Criando modelos do Gerenciador de Recursos do Azure](../azure-resource-manager/resource-group-authoring-templates.md)

[Azure Resource Manager overview]: ../azure-resource-manager/resource-group-overview.md
[Deploy resources with Azure Resource Manager templates]: ../azure-resource-manager/resource-group-template-deploy.md
[Azure Quickstart Templates gallery]: https://azure.microsoft.com/documentation/templates/?term=service+bus
