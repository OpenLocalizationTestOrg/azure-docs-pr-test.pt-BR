---
title: "Criar namespace e fila do Barramento de Serviço do Azure usando um modelo do Azure Resource Manager | Microsoft Docs"
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
ms.openlocfilehash: 4358130a2c8e897a0fdd1f9560f766d6e22db4d2
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="create-a-service-bus-namespace-and-a-queue-using-an-azure-resource-manager-template"></a><span data-ttu-id="d3dc5-103">Criar um namespace e uma fila do Barramento de Serviço usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="d3dc5-103">Create a Service Bus namespace and a queue using an Azure Resource Manager template</span></span>

<span data-ttu-id="d3dc5-104">Este artigo mostra como usar um modelo do Azure Resource Manager que cria um namespace e uma fila do Barramento de Serviço nesse namespace.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-104">This article shows how to use an Azure Resource Manager template that creates a Service Bus namespace and a queue within that namespace.</span></span> <span data-ttu-id="d3dc5-105">Você aprenderá como definir quais recursos são implantados e como definir os parâmetros que são especificados quando a implantação é executada.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-105">You will learn how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="d3dc5-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo para atender às suas necessidades.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-106">You can use this template for your own deployments, or customize it to meet your requirements.</span></span>

<span data-ttu-id="d3dc5-107">Para saber mais sobre a criação de modelos, veja [Criando modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="d3dc5-107">For more information about creating templates, please see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="d3dc5-108">Para ver o modelo completo, consulte o [Modelo de namespace e fila do Barramento de Serviço][Service Bus namespace and queue template] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-108">For the complete template, see the [Service Bus namespace and queue template][Service Bus namespace and queue template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="d3dc5-109">Os modelos do Azure Resource Manager a seguir estão disponíveis para download e implantação.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-109">The following Azure Resource Manager templates are available for download and deployment.</span></span>
> 
> * [<span data-ttu-id="d3dc5-110">Create a Service Bus namespace with queue and authorization rule (Criar um namespace de Barramento de Serviço com fila e regra de autorização)</span><span class="sxs-lookup"><span data-stu-id="d3dc5-110">Create a Service Bus namespace with queue and authorization rule</span></span>](service-bus-resource-manager-namespace-auth-rule.md)
> * [<span data-ttu-id="d3dc5-111">Criar um namespace do Barramento de Serviço com tópico e assinatura</span><span class="sxs-lookup"><span data-stu-id="d3dc5-111">Create a Service Bus namespace with topic and subscription</span></span>](service-bus-resource-manager-namespace-topic.md)
> * [<span data-ttu-id="d3dc5-112">Criar um namespace do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="d3dc5-112">Create a Service Bus namespace</span></span>](service-bus-resource-manager-namespace.md)
> * [<span data-ttu-id="d3dc5-113">Criar um namespace do Barramento de Serviço com tópico, assinatura e regra</span><span class="sxs-lookup"><span data-stu-id="d3dc5-113">Create a Service Bus namespace with topic, subscription, and rule</span></span>](service-bus-resource-manager-namespace-topic-with-rule.md)
> 
> <span data-ttu-id="d3dc5-114">Para verificar os modelos mais recentes, visite a galeria [Modelos de Início Rápido do Azure][Azure Quickstart Templates] e pesquise "Barramento de Serviço".</span><span class="sxs-lookup"><span data-stu-id="d3dc5-114">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for "Service Bus."</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="d3dc5-115">O que você implantará?</span><span class="sxs-lookup"><span data-stu-id="d3dc5-115">What will you deploy?</span></span>

<span data-ttu-id="d3dc5-116">Com este modelo, você implantará um namespace de Barramento de Serviço com uma fila.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-116">With this template, you will deploy a Service Bus namespace with a queue.</span></span>

<span data-ttu-id="d3dc5-117">As [filas do Barramento de Serviço](service-bus-queues-topics-subscriptions.md#queues) oferecem entrega de mensagem do tipo PEPS (primeiro a entrar, primeiro a sair) para um ou mais consumidores concorrentes.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-117">[Service Bus queues](service-bus-queues-topics-subscriptions.md#queues) offer First In, First Out (FIFO) message delivery to one or more competing consumers.</span></span>

<span data-ttu-id="d3dc5-118">Para executar a implantação automaticamente, clique no seguinte botão:</span><span class="sxs-lookup"><span data-stu-id="d3dc5-118">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="d3dc5-119">[![Implantar no Azure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="d3dc5-119">[![Deploy to Azure](./media/service-bus-resource-manager-namespace-queue/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-servicebus-create-queue%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="d3dc5-120">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="d3dc5-120">Parameters</span></span>

<span data-ttu-id="d3dc5-121">Com o Gerenciador de Recursos do Azure, você define parâmetros para os valores que deseja especificar quando o modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-121">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="d3dc5-122">O modelo inclui uma seção chamada `Parameters` , que contém todos os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-122">The template includes a section called `Parameters` that contains all of the parameter values.</span></span> <span data-ttu-id="d3dc5-123">Você deve definir um parâmetro para os valores que variam de acordo com o projeto que você está implantando ou com o ambiente em que a implantação ocorre.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-123">You should define a parameter for those values that will vary based on the project you are deploying or based on the environment you are deploying to.</span></span> <span data-ttu-id="d3dc5-124">Não defina parâmetros para valores que permanecem sempre os mesmos.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-124">Do not define parameters for values that will always stay the same.</span></span> <span data-ttu-id="d3dc5-125">Cada valor de parâmetro é usado no modelo para definir os recursos que são implantados.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-125">Each parameter value is used in the template to define the resources that are deployed.</span></span>

<span data-ttu-id="d3dc5-126">O modelo define os parâmetros a seguir.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-126">The template defines the following parameters.</span></span>

### <a name="servicebusnamespacename"></a><span data-ttu-id="d3dc5-127">serviceBusNamespaceName</span><span class="sxs-lookup"><span data-stu-id="d3dc5-127">serviceBusNamespaceName</span></span>
<span data-ttu-id="d3dc5-128">O nome do namespace do Barramento de Serviço a ser criado.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-128">The name of the Service Bus namespace to create.</span></span>

```json
"serviceBusNamespaceName": {
"type": "string",
"metadata": { 
    "description": "Name of the Service Bus namespace" 
    }
}
```

### <a name="servicebusqueuename"></a><span data-ttu-id="d3dc5-129">serviceBusQueueName</span><span class="sxs-lookup"><span data-stu-id="d3dc5-129">serviceBusQueueName</span></span>
<span data-ttu-id="d3dc5-130">O nome da fila criada no namespace do Barramento de Serviço.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-130">The name of the queue created in the Service Bus namespace.</span></span>

```json
"serviceBusQueueName": {
"type": "string"
}
```

### <a name="servicebusapiversion"></a><span data-ttu-id="d3dc5-131">serviceBusApiVersion</span><span class="sxs-lookup"><span data-stu-id="d3dc5-131">serviceBusApiVersion</span></span>
<span data-ttu-id="d3dc5-132">A versão da API do Barramento de Serviço do modelo.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-132">The Service Bus API version of the template.</span></span>

```json
"serviceBusApiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="d3dc5-133">Recursos a implantar</span><span class="sxs-lookup"><span data-stu-id="d3dc5-133">Resources to deploy</span></span>
<span data-ttu-id="d3dc5-134">Cria um namespace de Barramento de Serviço padrão do tipo **Mensagens**, com uma fila.</span><span class="sxs-lookup"><span data-stu-id="d3dc5-134">Creates a standard Service Bus namespace of type **Messaging**, with a queue.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="d3dc5-135">Comandos para executar a implantação</span><span class="sxs-lookup"><span data-stu-id="d3dc5-135">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="d3dc5-136">PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3dc5-136">PowerShell</span></span>

```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="azure-cli"></a><span data-ttu-id="d3dc5-137">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="d3dc5-137">Azure CLI</span></span>

```azurecli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri <https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-servicebus-create-queue/azuredeploy.json>
```

## <a name="next-steps"></a><span data-ttu-id="d3dc5-138">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d3dc5-138">Next steps</span></span>
<span data-ttu-id="d3dc5-139">Agora que você criou e implantou recursos usando o Azure Resource Manager, saiba como gerenciar esses recursos consultando estes artigos:</span><span class="sxs-lookup"><span data-stu-id="d3dc5-139">Now that you've created and deployed resources using Azure Resource Manager, learn how to manage these resources by viewing these articles:</span></span>

* [<span data-ttu-id="d3dc5-140">Gerenciar o Barramento de Serviço com o PowerShell</span><span class="sxs-lookup"><span data-stu-id="d3dc5-140">Manage Service Bus with PowerShell</span></span>](service-bus-manage-with-ps.md)
* [<span data-ttu-id="d3dc5-141">Gerenciar recursos do Barramento de Serviço com o Service Bus Explorer</span><span class="sxs-lookup"><span data-stu-id="d3dc5-141">Manage Service Bus resources with the Service Bus Explorer</span></span>](https://github.com/paolosalvatori/ServiceBusExplorer/releases)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Service Bus namespace and queue template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-servicebus-create-queue/
[Azure Quickstart Templates]: https://azure.microsoft.com/documentation/templates/?term=service+bus
[Learn more about Service Bus queues]: service-bus-queues-topics-subscriptions.md
[Using Azure PowerShell with Azure Resource Manager]: ../azure-resource-manager/powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../azure-resource-manager/xplat-cli-azure-resource-manager.md
