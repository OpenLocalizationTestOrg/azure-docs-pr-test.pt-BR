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
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="ec0b5-103">Criar um namespace do Barramento de Serviço com tópico, assinatura e regra usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ec0b5-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="ec0b5-104">Este artigo mostra como toouse um modelo do Gerenciador de recursos do Azure que cria um namespace de barramento de serviço com um tópico, a assinatura e a regra (filtro).</span><span class="sxs-lookup"><span data-stu-id="ec0b5-104">This article shows how toouse an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="ec0b5-105">Você aprenderá como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-105">You learn how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="ec0b5-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos</span><span class="sxs-lookup"><span data-stu-id="ec0b5-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="ec0b5-107">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="ec0b5-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="ec0b5-108">Para saber mais sobre as práticas e os padrões de convenções de nomenclatura de recursos do Azure, confira [Convenções de nomenclatura recomendandas para os recursos do Azure][Recommended naming conventions for Azure resources].</span><span class="sxs-lookup"><span data-stu-id="ec0b5-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="ec0b5-109">Para o modelo completo de Olá, consulte Olá [namespace de barramento de serviço com o tópico, a assinatura e a regra] [ Service Bus namespace with topic, subscription, and rule] modelo.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-109">For hello complete template, see hello [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="ec0b5-110">saudação do Azure Resource Manager modelos a seguir está disponível para download e implantação.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-110">hello following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="ec0b5-111">Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)</span><span class="sxs-lookup"><span data-stu-id="ec0b5-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="ec0b5-112">Criar um namespace do Barramento de Serviço com fila</span><span class="sxs-lookup"><span data-stu-id="ec0b5-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="ec0b5-113">Criar um namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="ec0b5-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="ec0b5-114">Criar um namespace do Barramento de Serviço com tópico e assinatura</span><span class="sxs-lookup"><span data-stu-id="ec0b5-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="ec0b5-115">toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e pesquisa para o barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-115">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="ec0b5-116">O que você implantará?</span><span class="sxs-lookup"><span data-stu-id="ec0b5-116">What will you deploy?</span></span>

<span data-ttu-id="ec0b5-117">Com este modelo, você implantará um namespace de Barramento de Serviço com tópico, assinatura e regra (filtro).</span><span class="sxs-lookup"><span data-stu-id="ec0b5-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="ec0b5-118">Os [tópicos e as assinaturas do Barramento de Serviço](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) fornecem uma forma de comunicação de um para muitos, em um padrão de *publicação/assinatura*.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="ec0b5-119">Ao usar tópicos e assinaturas, componentes de um aplicativo distribuído não se comunicam diretamente com o outro, em vez disso, eles trocam mensagens por meio do tópico que atua como um intermediário. Um tópico de tooa de assinatura é semelhante a uma fila virtual que recebe cópias das mensagens que foram enviadas toohello tópico.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription tooa topic resembles a virtual queue that receives copies of messages that were sent toohello topic.</span></span> <span data-ttu-id="ec0b5-120">Um filtro de assinatura permite que você toospecify quais mensagens enviadas tópico tooa deve aparecer dentro de uma assinatura de tópico específico.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-120">A filter on subscription enables you toospecify which messages sent tooa topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="ec0b5-121">O que são regras (filtros)?</span><span class="sxs-lookup"><span data-stu-id="ec0b5-121">What are rules (filters)?</span></span>

<span data-ttu-id="ec0b5-122">Em muitos cenários, as mensagens com características específicas precisam ser processadas de maneiras diferentes.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="ec0b5-123">tooenable isso, você pode configurar assinaturas toofind mensagens que têm propriedades específicas e, em seguida, executam propriedades de toothose modificações.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-123">tooenable this, you can configure subscriptions toofind messages that have specific properties and then perform modifications toothose properties.</span></span> <span data-ttu-id="ec0b5-124">Embora as assinaturas do barramento de serviço vejam todas as mensagens enviadas toohello tópico, você só pode copiar um subconjunto da fila de assinatura virtual de toohello mensagens.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-124">Although Service Bus subscriptions see all messages sent toohello topic, you can only copy a subset of those messages toohello virtual subscription queue.</span></span> <span data-ttu-id="ec0b5-125">Isso é feito usando filtros de assinatura.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="ec0b5-126">toolearn mais informações sobre regras (filtros), consulte [regras e ações](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="ec0b5-126">toolearn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="ec0b5-127">toorun Olá implantação automaticamente, clique em Olá botão a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec0b5-127">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="ec0b5-128">[![Implantar tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="ec0b5-128">[![Deploy tooAzure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="ec0b5-129">parâmetros</span><span class="sxs-lookup"><span data-stu-id="ec0b5-129">Parameters</span></span>

<span data-ttu-id="ec0b5-130">No Gerenciador de recursos do Azure, você deve definir parâmetros para os valores desejados toospecify quando Olá modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-130">With Azure Resource Manager, you should define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="ec0b5-131">modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-131">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="ec0b5-132">Você deve definir um parâmetro para os valores que variam com base no projeto Olá que estiver implantando ou com base no ambiente de saudação que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-132">You should define a parameter for those values that vary based on hello project you are deploying or based on hello environment you are deploying to.</span></span> <span data-ttu-id="ec0b5-133">Não defina parâmetros para valores que permanecem sempre Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-133">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="ec0b5-134">Cada valor de parâmetro é usado em Olá modelo toodefine Olá recursos implantados.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-134">Each parameter value is used in hello template toodefine hello resources that are deployed.</span></span>

<span data-ttu-id="ec0b5-135">modelo de saudação define Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec0b5-135">hello template defines hello following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="ec0b5-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="ec0b5-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="ec0b5-137">nome de saudação do hello toocreate de namespace de barramento de serviço.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-137">hello name of hello Service Bus namespace toocreate.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="ec0b5-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="ec0b5-138">serviceBusTopicName</span></span>
<span data-ttu-id="ec0b5-139">nome de saudação do tópico de Olá criado no namespace de barramento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-139">hello name of hello topic created in hello Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="ec0b5-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="ec0b5-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="ec0b5-141">nome de saudação da assinatura de saudação criada no namespace de barramento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-141">hello name of hello subscription created in hello Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="ec0b5-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="ec0b5-142">serviceBusRuleName</span></span>
<span data-ttu-id="ec0b5-143">nome de saudação do hello rule(filter) criado no namespace de barramento de serviço hello.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-143">hello name of hello rule(filter) created in hello Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="ec0b5-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="ec0b5-144">serviceBusApiVersion</span></span>
<span data-ttu-id="ec0b5-145">versão de API do barramento de serviço de saudação do modelo de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-145">hello Service Bus API version of hello template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-toodeploy"></a><span data-ttu-id="ec0b5-146">Recursos toodeploy</span><span class="sxs-lookup"><span data-stu-id="ec0b5-146">Resources toodeploy</span></span>
<span data-ttu-id="ec0b5-147">Cria um namespace de Barramento de Serviço padrão do tipo **Mensagens**, com tópico, assinatura e regras.</span><span class="sxs-lookup"><span data-stu-id="ec0b5-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

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

## <a name="commands-toorun-deployment"></a><span data-ttu-id="ec0b5-148">Implantação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="ec0b5-148">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="ec0b5-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec0b5-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="ec0b5-150">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="ec0b5-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="ec0b5-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ec0b5-151">Next steps</span></span>
<span data-ttu-id="ec0b5-152">Agora que você criou e implantou recursos usando o Gerenciador de recursos do Azure, Aprenda como toomanage esses recursos exibindo estes artigos:</span><span class="sxs-lookup"><span data-stu-id="ec0b5-152">Now that you've created and deployed resources using Azure Resource Manager, learn how toomanage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="ec0b5-153">Gerenciar o Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="ec0b5-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="ec0b5-154">Gerenciar o Barramento de Serviço com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="ec0b5-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="ec0b5-155">Gerenciar recursos do barramento de serviço com hello Explorador do barramento de serviço</span><span class="sxs-lookup"><span data-stu-id="ec0b5-155">Manage Service Bus resources with hello Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

