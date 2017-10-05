---
title: "Criar uma regra e assinatura de tópicos do Barramento de Serviço do Azure usando o modelo do Azure Resource Manager | Microsoft Docs"
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
ms.openlocfilehash: 35e67d86b42358c4ce28b41beae1ee8e1896e939
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-with-topic-subscription-and-rule-using-an-azure-resource-manager-template"></a><span data-ttu-id="6cfb8-103">Criar um namespace do Barramento de Serviço com tópico, assinatura e regra usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6cfb8-103">Create a Service Bus namespace with topic, subscription, and rule using an Azure Resource Manager template</span></span>

<span data-ttu-id="6cfb8-104">Este artigo mostra como usar um modelo do Azure Resource Manager que cria um namespace do Barramento de Serviço com tópico, assinatura e regra (filtro).</span><span class="sxs-lookup"><span data-stu-id="6cfb8-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace with a topic, subscription, and rule (filter).</span></span> <span data-ttu-id="6cfb8-105">Você aprende como definir quais recursos são implantados e como definir os parâmetros que são especificados quando a implantação é executada.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-105">You learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="6cfb8-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo para atender às suas necessidades</span><span class="sxs-lookup"><span data-stu-id="6cfb8-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="6cfb8-107">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="6cfb8-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="6cfb8-108">Para saber mais sobre as práticas e os padrões de convenções de nomenclatura de recursos do Azure, confira [Convenções de nomenclatura recomendandas para os recursos do Azure][Recommended naming conventions for Azure resources].</span><span class="sxs-lookup"><span data-stu-id="6cfb8-108">For more information about practice and patterns on Azure resources naming conventions, see [Recommended naming conventions for Azure resources][Recommended naming conventions for Azure resources].</span></span>

<span data-ttu-id="6cfb8-109">Para ver o modelo completo, veja o [Modelo de namespace do Barramento de Serviço com tópico, assinatura e regra][Service Bus namespace with topic, subscription, and rule].</span><span class="sxs-lookup"><span data-stu-id="6cfb8-109">For the complete template, see the [Service Bus namespace with topic, subscription, and rule][Service Bus namespace with topic, subscription, and rule] template.</span></span>

> [!NOTE]
> <span data-ttu-id="6cfb8-110">Os modelos do Azure Resource Manager a seguir estão disponíveis para download e implantação.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-110">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="6cfb8-111">Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)</span><span class="sxs-lookup"><span data-stu-id="6cfb8-111">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="6cfb8-112">Criar um namespace do Barramento de Serviço com fila</span><span class="sxs-lookup"><span data-stu-id="6cfb8-112">Create a Service Bus namespace with queue</span></span>](service-bus-resource-manager-namespace-queue.md)
> * [<span data-ttu-id="6cfb8-113">Criar um namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="6cfb8-113">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="6cfb8-114">Criar um namespace do Barramento de Serviço com tópico e assinatura</span><span class="sxs-lookup"><span data-stu-id="6cfb8-114">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> 
> <span data-ttu-id="6cfb8-115">Para verificar os modelos mais recentes, visite a galeria [Modelos de Início Rápido do Azure][Azure Quickstart Templates] e pesquise por Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-115">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Service Bus.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="6cfb8-116">O que você implantará?</span><span class="sxs-lookup"><span data-stu-id="6cfb8-116">What will you deploy?</span></span>

<span data-ttu-id="6cfb8-117">Com este modelo, você implantará um namespace de Barramento de Serviço com tópico, assinatura e regra (filtro).</span><span class="sxs-lookup"><span data-stu-id="6cfb8-117">With this template, you deploy a Service Bus namespace with topic, subscription, and rule (filter).</span></span>

<span data-ttu-id="6cfb8-118">Os [tópicos e as assinaturas do Barramento de Serviço](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) fornecem uma forma de comunicação de um para muitos, em um padrão de *publicação/assinatura*.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-118">[Service Bus topics and subscriptions](service-bus-queues-topics-subscriptions.md#topics-and-subscriptions) provide a one-to-many form of communication, in a *publish/subscribe* pattern.</span></span> <span data-ttu-id="6cfb8-119">Ao usar tópicos e assinaturas, componentes de um aplicativo distribuído não se comunicam diretamente uns com os outros, mas trocam mensagens por meio de tópico que age como um intermediário. Uma assinatura para um tópico é semelhante a uma fila virtual que recebe cópias das mensagens enviadas ao tópico.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-119">When using topics and subscriptions, components of a distributed application do not communicate directly with each other, instead they exchange messages via topic that acts as an intermediary.A subscription to a topic resembles a virtual queue that receives copies of messages that were sent to the topic.</span></span> <span data-ttu-id="6cfb8-120">Um filtro na assinatura permite que você especifique quais mensagens enviadas a um tópico devem aparecer dentro de uma assinatura específica do tópico.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-120">A filter on subscription enables you to specify which messages sent to a topic should appear within a specific topic subscription.</span></span>

## <a name="what-are-rules-filters"></a><span data-ttu-id="6cfb8-121">O que são regras (filtros)?</span><span class="sxs-lookup"><span data-stu-id="6cfb8-121">What are rules (filters)?</span></span>

<span data-ttu-id="6cfb8-122">Em muitos cenários, as mensagens com características específicas precisam ser processadas de maneiras diferentes.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-122">In many scenarios, messages that have specific characteristics must be processed in different ways.</span></span> <span data-ttu-id="6cfb8-123">Para habilitar isso, você pode configurar assinaturas para localizar as mensagens com as propriedades específicas e, em seguida, realizar determinadas modificações nessas propriedades.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-123">To enable this, you can configure subscriptions to find messages that have specific properties and then perform modifications to those properties.</span></span> <span data-ttu-id="6cfb8-124">Embora as assinaturas do Barramento de Serviço vejam todas as mensagens enviadas para o tópico, você só poderá copiar um subconjunto dessas mensagens para a fila de assinatura virtual.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-124">Although Service Bus subscriptions see all messages sent to the topic, you can only copy a subset of those messages to the virtual subscription queue.</span></span> <span data-ttu-id="6cfb8-125">Isso é feito usando filtros de assinatura.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-125">This is accomplished using subscription filters.</span></span> <span data-ttu-id="6cfb8-126">Para saber mais sobre regras (filtros), consulte [Regras e ações](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span><span class="sxs-lookup"><span data-stu-id="6cfb8-126">To learn more about rules (filters), see [Rules and actions](service-bus-queues-topics-subscriptions.md#rules-and-actions).</span></span>

<span data-ttu-id="6cfb8-127">Para executar a implantação automaticamente, clique no seguinte botão:</span><span class="sxs-lookup"><span data-stu-id="6cfb8-127">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="6cfb8-128">[![Implantar no Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="6cfb8-128">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-topic/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-topic-subscription-rule%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="6cfb8-129">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="6cfb8-129">Parameters</span></span>

<span data-ttu-id="6cfb8-130">Com o Azure Resource Manager, você define parâmetros para os valores que deseja especificar quando o modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-130">With Azure Resource Manager, you should define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="6cfb8-131">O modelo inclui uma seção chamada `Parameters` , que contém todos os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-131">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="6cfb8-132">Você deve definir um parâmetro para os valores que variam de acordo com o projeto que você está implantando ou com o ambiente em que a implantação ocorre.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-132">You should define a parameter for those values that vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="6cfb8-133">Não defina parâmetros para valores que permanecem sempre os mesmos.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-133">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="6cfb8-134">Cada valor de parâmetro é usado no modelo para definir os recursos que são implantados.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-134">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="6cfb8-135">O modelo define os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="6cfb8-135">The template defines the following parameters:</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="6cfb8-136">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="6cfb8-136">serviceBusNamespaceName</span></span>
<span data-ttu-id="6cfb8-137">O nome do namespace do Barramento de Serviço a ser criado.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-137">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string"
}
```

### <a name="servicebustopicname"></a><span data-ttu-id="6cfb8-138">serviceBusTopicName</span><span class="sxs-lookup"><span data-stu-id="6cfb8-138">serviceBusTopicName</span></span>
<span data-ttu-id="6cfb8-139">O nome do tópico criado no namespace do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-139">The name of the topic created in the Service Bus namespace.</span></span>

```json
"serviceBusTopicName": {
"type": "string"
}
```

### <a name="servicebussubscriptionname"></a><span data-ttu-id="6cfb8-140">serviceBusSubscriptionName</span><span class="sxs-lookup"><span data-stu-id="6cfb8-140">serviceBusSubscriptionName</span></span>
<span data-ttu-id="6cfb8-141">O nome da assinatura criada no namespace do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-141">The name of the subscription created in the Service Bus namespace.</span></span>

```json
"serviceBusSubscriptionName": {
"type": "string"
}
```
### <a name="servicebusrulename"></a><span data-ttu-id="6cfb8-142">serviceBusRuleName</span><span class="sxs-lookup"><span data-stu-id="6cfb8-142">serviceBusRuleName</span></span>
<span data-ttu-id="6cfb8-143">O nome da regra (filtro) criada no namespace do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-143">The name of the rule(filter) created in the Service Bus namespace.</span></span>

```json
   "serviceBusRuleName": {
   "type": "string",
  }
```
### <a name="servicebusapiversion"></a><span data-ttu-id="6cfb8-144">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="6cfb8-144">serviceBusApiVersion</span></span>
<span data-ttu-id="6cfb8-145">A versão da API do Barramento de Serviço do modelo.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-145">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```
## <a name="resources-to-deploy"></a><span data-ttu-id="6cfb8-146">Recursos a implantar</span><span class="sxs-lookup"><span data-stu-id="6cfb8-146">Resources to deploy</span></span>
<span data-ttu-id="6cfb8-147">Cria um namespace de Barramento de Serviço padrão do tipo **Mensagens**, com tópico, assinatura e regras.</span><span class="sxs-lookup"><span data-stu-id="6cfb8-147">Creates a standard Service Bus namespace of type **Messaging**, with topic and subscription and rules.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="6cfb8-148">Comandos para executar a implantação</span><span class="sxs-lookup"><span data-stu-id="6cfb8-148">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="6cfb8-149">PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cfb8-149">PowerShell</span></span>
```powershell
New-AzureResourceGroupDeployment -Name \<deployment-name\> -ResourceGroupName \<resource-group-name\> -TemplateUri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="6cfb8-150">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6cfb8-150">Azure CLI</span></span>
```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-topic-subscription-rule/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="6cfb8-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6cfb8-151">Next steps</span></span>
<span data-ttu-id="6cfb8-152">Agora que você criou e implantou recursos usando o Azure Resource Manager, saiba como gerenciar esses recursos consultando estes artigos:</span><span class="sxs-lookup"><span data-stu-id="6cfb8-152">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="6cfb8-153">Gerenciar o Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="6cfb8-153">Manage Azure Service Bus</span></span>](service-bus-management-libraries.md)
* [<span data-ttu-id="6cfb8-154">Gerenciar o Barramento de Serviço com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="6cfb8-154">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="6cfb8-155">Gerenciar recursos do Barramento de Serviço com o Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="6cfb8-155">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus topics and subscriptions]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
[Recommended naming conventions for Azure resources]: ../guidance/guidance-naming-conventions.md
[Service Bus namespace with topic, subscription, and rule]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-topic-subscription-rule/
[Service Bus queues, topics, and subscriptions]: service-bus-queues-topics-subscriptions.md

