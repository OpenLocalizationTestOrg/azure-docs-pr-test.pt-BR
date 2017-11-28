---
title: "assinatura de tópico aaaCreate Azure Service Bus namespace usando o modelo do Gerenciador de recursos do Azure | Microsoft Docs"
description: "Criar um namespace do Barramento de Serviço com tópico e assinatura usando um modelo do Azure Resource Manager"
services: service-bus-messaging
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: d3d55200-5c60-4b5f-822d-59974cafff0e
ms.service: service-bus-messaging
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 08/07/2017
ms.author: sethm;shvija
ms.openlocfilehash: 9b5f7d8710e598b73c0a7ea3daf8c300f7fa9ecd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-a-service-bus-namespace-with-topic-and-subscription-using-an-azure-resource-manager-template"></a><span data-ttu-id="5a4d6-103">Criar um namespace do Barramento de Serviço com tópico e assinatura usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="5a4d6-103">Create a Service Bus namespace with topic and subscription using an Azure Resource Manager template</span></span>

<span data-ttu-id="5a4d6-104">Este artigo mostra como toouse um modelo do Gerenciador de recursos do Azure que cria um namespace de barramento de serviço e um tópico e assinatura dentro desse namespace.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace and a topic and subscription within that namespace.</span></span> <span data-ttu-id="5a4d6-105">Você aprenderá como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-105">You will learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="5a4d6-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos</span><span class="sxs-lookup"><span data-stu-id="5a4d6-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="5a4d6-107">Para saber mais sobre a criação de modelos, veja [Criando modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="5a4d6-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="5a4d6-108">Para o modelo completo de Olá, consulte Olá [namespace de barramento de serviço com o tópico e assinatura] [ Service Bus namespace with topic and subscription] modelo.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-108">For hello complete template, see hello [Service Bus namespace with topic and subscription][Service Bus namespace with topic and subscription] template.</span></span>

> [!NOTE]
> <span data-ttu-id="5a4d6-109">saudação do Azure Resource Manager modelos a seguir está disponível para download e implantação.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-109">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="5a4d6-110">Criar um namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="5a4d6-110">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="5a4d6-111">Criar um namespace do Barramento de Serviço com fila</span><span class="sxs-lookup"><span data-stu-id="5a4d6-111">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="5a4d6-112">Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)</span><span class="sxs-lookup"><span data-stu-id="5a4d6-112">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="5a4d6-113">Criar um namespace do Barramento de Serviço com tópico, assinatura e regra</span><span class="sxs-lookup"><span data-stu-id="5a4d6-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="5a4d6-114">toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e procure "Barramento de serviço".</span><span class="sxs-lookup"><span data-stu-id="5a4d6-114">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="5a4d6-115">O que você implantará?</span><span class="sxs-lookup"><span data-stu-id="5a4d6-115">What will you deploy?</span></span>

<span data-ttu-id="5a4d6-116">Com este modelo, você implantará um namespace de Barramento de Serviço com tópico e assinatura.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-116">With this template, you will deploy a Service Bus namespace with topic and subscription.</span></span>

<span data-ttu-id="5a4d6-117">Os [tópicos e as assinaturas do Barramento de Serviço](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) fornecem uma forma de comunicação de um para muitos, em um padrão de *publicação/assinatura*.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-117">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span>

<span data-ttu-id="5a4d6-118">toorun Olá implantação automaticamente, clique em Olá botão a seguir:</span><span class="sxs-lookup"><span data-stu-id="5a4d6-118">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="5a4d6-119">[![Implantar tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="5a4d6-119">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-and-subscription%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="5a4d6-120">parâmetros</span><span class="sxs-lookup"><span data-stu-id="5a4d6-120">Parameters</span></span>

<span data-ttu-id="5a4d6-121">No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-121">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="5a4d6-122">modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-122">hello template includes a section called `Parameters` that contains all of hello parameter values.</span></span> <span data-ttu-id="5a4d6-123">Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-123">You should define a parameter for those values that will vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="5a4d6-124">Não defina parâmetros para valores sempre ficará Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-124">Do not define parameters for values that will always stay hello same.</span></span> <span data-ttu-id="5a4d6-125">Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-125">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="5a4d6-126">modelo de saudação define Olá parâmetros a seguir.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-126">hello template defines hello following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="5a4d6-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="5a4d6-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="5a4d6-128">nome de saudação do hello toocreate de namespace de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-128">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="5a4d6-129">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="5a4d6-129">serviceBusTopicName</span></span>
<span data-ttu-id="5a4d6-130">nome de saudação do tópico de Olá criado no namespace de barramento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-130">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="5a4d6-131">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="5a4d6-131">serviceBusSubscriptionName</span></span>
<span data-ttu-id="5a4d6-132">nome de saudação da assinatura de saudação criada no namespace de barramento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-132">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="5a4d6-133">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="5a4d6-133">serviceBusApiVersion</span></span>
<span data-ttu-id="5a4d6-134">versão de API do barramento de serviço de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-134">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="5a4d6-135">Recursos toodeploy</span><span class="sxs-lookup"><span data-stu-id="5a4d6-135">Resources toodeploy</span></span>
<span data-ttu-id="5a4d6-136">Cria um namespace de Barramento de Serviço padrão do tipo **Mensagens**, com tópico e assinatura.</span><span class="sxs-lookup"><span data-stu-id="5a4d6-136">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription.</span></span>

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
            "name": "[parameters('serviceBusTopicName')]",
            "type": "Topics",
            "dependsOn": [
                "[concat('Microsoft.ServiceBus/namespaces/', parameters('serviceBusNamespaceName'))]"
            ],
            "properties": {
                "path": "[parameters('serviceBusTopicName')]",
            },
            "resources": [{
                "apiVersion": "[variables('sbVersion')]",
                "name": "[parameters('serviceBusSubscriptionName')]",
                "type": "Subscriptions",
                "dependsOn": [
                    "[parameters('serviceBusTopicName')]"
                ],
                "properties": {}
            }]
        }]
    }]
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="5a4d6-137">Implantação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="5a4d6-137">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="5a4d6-138">PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a4d6-138">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="5a4d6-139">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5a4d6-139">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-and-subscription/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="5a4d6-140">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5a4d6-140">Next steps</span></span>
<span data-ttu-id="5a4d6-141">Agora que você criou e implantou recursos usando o Gerenciador de recursos do Azure, Aprenda como toomanage esses recursos exibindo estes artigos:</span><span class="sxs-lookup"><span data-stu-id="5a4d6-141">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="5a4d6-142">Gerenciar o Barramento de Serviço com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="5a4d6-142">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="5a4d6-143">Gerenciar recursos do barramento de serviço com hello Explorador do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="5a4d6-143">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Service Bus namespace with topic and subscription]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-and-subscription/
