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
# <a name="create-a-service-bus-authorization-rule-for-namespace-and-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="5a17c-103">Criar uma regra de autorização do Barramento de Serviço para namespace e fila usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5a17c-103">Create a Service Bus authorization rule for namespace and queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="5a17c-104">Este artigo mostra como toouse um modelo do Gerenciador de recursos do Azure que cria um [regra de autorização](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) para um namespace de barramento de serviço e fila.</span><span class="sxs-lookup"><span data-stu-id="5a17c-104">This article shows how toouse an Azure Resource Manager template that creates an [authorization rule](service-bus-authentication-and-authorization.md#shared-access-signature-authentication) for a Service Bus namespace and queue.</span></span> <span data-ttu-id="5a17c-105">Você aprenderá como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada.</span><span class="sxs-lookup"><span data-stu-id="5a17c-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="5a17c-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos.</span><span class="sxs-lookup"><span data-stu-id="5a17c-106">You can use this template for your own deployments, or customize it toomeet your requirements.</span></span>

<span data-ttu-id="5a17c-107">Para saber mais sobre a criação de modelos, veja [Criando modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="5a17c-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="5a17c-108">Para o modelo completo de Olá, consulte Olá [modelo de regra de autorização do barramento de serviço] [ Service Bus auth rule template] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="5a17c-108">For hello complete template, see hello [Service Bus authorization rule template][Service Bus auth rule template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="5a17c-109">saudação do Azure Resource Manager modelos a seguir está disponível para download e implantação.</span><span class="sxs-lookup"><span data-stu-id="5a17c-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="5a17c-110">Criar um namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="5a17c-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="5a17c-111">Criar um namespace do Barramento de Serviço com fila</span><span class="sxs-lookup"><span data-stu-id="5a17c-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="5a17c-112">Criar um namespace do Barramento de Serviço com tópico e assinatura</span><span class="sxs-lookup"><span data-stu-id="5a17c-112">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="5a17c-113">Criar um namespace do Barramento de Serviço com tópico, assinatura e regra</span><span class="sxs-lookup"><span data-stu-id="5a17c-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="5a17c-114">toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e procure "Barramento de serviço".</span><span class="sxs-lookup"><span data-stu-id="5a17c-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="5a17c-115">O que você implantará?</span><span class="sxs-lookup"><span data-stu-id="5a17c-115">What will you deploy?</span></span>
<span data-ttu-id="5a17c-116">Com esse modelo, você implantará uma regra de autorização do Barramento de Serviço para um namespace e uma entidade de sistema de mensagens (nesse caso, uma fila).</span><span class="sxs-lookup"><span data-stu-id="5a17c-116">With this template, you will deploy a Service Bus authorization rule for a namespace and messaging entity (in this case, a queue).</span></span>

<span data-ttu-id="5a17c-117">O modelo usa [SAS (Assinatura de Acesso Compartilhado)](service-bus-sas.md) para autenticação.</span><span class="sxs-lookup"><span data-stu-id="5a17c-117">This template uses [Shared Access Signature (SAS)](service-bus-sas.md) for authentication.</span></span> <span data-ttu-id="5a17c-118">O SAS permite que aplicativos tooauthenticate tooService barramento usando uma chave de acesso configurada no namespace hello, ou em Olá entidade (fila ou tópico) de mensagens com os direitos específicos associados.</span><span class="sxs-lookup"><span data-stu-id="5a17c-118">SAS enables applications tooauthenticate tooService Bus using an access key configured on hello namespace, or on hello messaging entity (queue or topic) with which specific rights are associated.</span></span> <span data-ttu-id="5a17c-119">Você pode usar essa chave toogenerate um token SAS que os clientes podem usar tooauthenticate tooService barramento.</span><span class="sxs-lookup"><span data-stu-id="5a17c-119">You can then use this key toogenerate a SAS token that clients can in turn use tooauthenticate tooService Bus.</span></span>

<span data-ttu-id="5a17c-120">toorun Olá implantação automaticamente, clique em Olá botão a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a17c-120">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="5a17c-121">[![Implantar tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="5a17c-121">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-auth-rule/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F301-servicebus-create-authrule-namespace-and-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="5a17c-122">parâmetros</span><span class="sxs-lookup"><span data-stu-id="5a17c-122">Parameters</span></span>

<span data-ttu-id="5a17c-123">No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="5a17c-123">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="5a17c-124">modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="5a17c-124">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="5a17c-125">Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="5a17c-125">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="5a17c-126">Não defina parâmetros para valores sempre ficará Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="5a17c-126">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="5a17c-127">Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.</span><span class="sxs-lookup"><span data-stu-id="5a17c-127">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="5a17c-128">modelo de saudação define Olá parâmetros a seguir.</span><span class="sxs-lookup"><span data-stu-id="5a17c-128">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="5a17c-129">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="5a17c-129">serviceBusNamespaceName</span></span>
<span data-ttu-id="5a17c-130">nome de saudação do hello toocreate de namespace de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="5a17c-130">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="namespaceauthorizationrulename"></a><span data-ttu-id="5a17c-131">namespaceAuthorizationRuleName</span><span class="sxs-lookup"><span data-stu-id="5a17c-131">namespaceAuthorizationRuleName</span></span>
<span data-ttu-id="5a17c-132">Olá nome da regra de autorização Olá Olá namespace.</span><span class="sxs-lookup"><span data-stu-id="5a17c-132">hello name of hello authorization rule for hello namespace.</span></span>

```json
"namespaceAuthorizationRuleName ": {
"type": "string"
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="5a17c-133">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="5a17c-133">serviceBusQueueName</span></span>
<span data-ttu-id="5a17c-134">nome de saudação da fila de Olá Olá namespace de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="5a17c-134">hello name of hello queue in hello Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="5a17c-135">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="5a17c-135">serviceBusApiVersion</span></span>
<span data-ttu-id="5a17c-136">versão de API do barramento de serviço de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a17c-136">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="5a17c-137">Recursos toodeploy</span><span class="sxs-lookup"><span data-stu-id="5a17c-137">Resources toodeploy</span></span>
<span data-ttu-id="5a17c-138">Cria um namespace do Barramento de Serviço padrão do tipo **Mensagens**e uma regra de autorização do Barramento de Serviço para o namespace e a entidade.</span><span class="sxs-lookup"><span data-stu-id="5a17c-138">Creates a standard Service Bus namespace of type **Messaging**, and a Service Bus authorization rule for namespace and entity.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="5a17c-139">Implantação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="5a17c-139">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

### <a name="powershell"></a><span data-ttu-id="5a17c-140">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a17c-140">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="5a17c-141">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5a17c-141">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/301-servicebus-create-authrule-namespace-and-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="5a17c-142">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a17c-142">Next steps</span></span>
<span data-ttu-id="5a17c-143">Agora que você criou e implantou recursos usando o Gerenciador de recursos do Azure, Aprenda como toomanage esses recursos exibindo estes artigos:</span><span class="sxs-lookup"><span data-stu-id="5a17c-143">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="5a17c-144">Gerenciar o Barramento de Serviço com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a17c-144">Manage Service Bus with PowerShell</span></span>](service-bus-powershell-how-to-provision.md)
* [<span data-ttu-id="5a17c-145">Gerenciar recursos do barramento de serviço com hello Explorador do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="5a17c-145">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)
* [<span data-ttu-id="5a17c-146">Autenticação e autorização do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="5a17c-146">Service Bus authentication and authorization</span></span>](service-bus-authentication-and-authorization.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus auth rule template]: https://github.com/Azure/azure-quickstart-templates/blob/master/301-servicebus-create-authrule-namespace-and-queue/
