---
title: um grupo de namespace e do consumidor de Hubs de eventos do Azure usando um modelo de aaaCreate | Microsoft Docs
description: Criar um namespace de Hubs de Eventos com um Hub de Eventos e um grupo de consumidores usando modelos do Azure Resource Manager
services: event-hubs
documentationcenter: .net
author: sethmanheim
manager: timlt
editor: 
ms.assetid: 28bb4591-1fd7-444f-a327-4e67e8878798
ms.service: event-hubs
ms.devlang: tbd
ms.topic: article
ms.tgt_pltfrm: dotnet
ms.workload: na
ms.date: 06/12/2017
ms.author: sethm;shvija
ms.openlocfilehash: 74b0d6b3fbe848705e2c20e628aa4e5269b53edb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="8b826-103">Criar um namespace dos Hubs de Eventos com um hub de eventos e um grupo de consumidores usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="8b826-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="8b826-104">Este artigo mostra como toouse um modelo do Gerenciador de recursos do Azure que cria um namespace do tipo de Hubs de eventos, com um evento e um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="8b826-104">This article shows how toouse an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="8b826-105">Olá artigo mostra como toodefine quais recursos são implantados e como toodefine parâmetros que são especificados quando a implantação de saudação for executada.</span><span class="sxs-lookup"><span data-stu-id="8b826-105">hello article shows how toodefine which resources are deployed and how toodefine parameters that are specified when hello deployment is executed.</span></span> <span data-ttu-id="8b826-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo toomeet seus requisitos</span><span class="sxs-lookup"><span data-stu-id="8b826-106">You can use this template for your own deployments, or customize it toomeet your requirements</span></span>

<span data-ttu-id="8b826-107">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="8b826-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="8b826-108">Para o modelo completo de Olá, consulte Olá [modelo de grupo de hub e consumidor de evento] [ Event Hub and consumer group template] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="8b826-108">For hello complete template, see hello [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="8b826-109">toocheck para modelos de hello mais recentes, visite Olá [modelos de início rápido do Azure] [ Azure Quickstart Templates] galeria e pesquisa para Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="8b826-109">toocheck for hello latest templates, visit hello [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="8b826-110">O que você implantará?</span><span class="sxs-lookup"><span data-stu-id="8b826-110">What will you deploy?</span></span>
<span data-ttu-id="8b826-111">Com este modelo, você implantará um namespace Hubs de Evento com um hub de eventos e um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="8b826-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="8b826-112">[Hubs de eventos](event-hubs-what-is-event-hubs.md) é um evento de processamento de serviço usado tooprovide eventos e telemetria entrada tooAzure em grande escala, com baixa latência e alta confiabilidade.</span><span class="sxs-lookup"><span data-stu-id="8b826-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used tooprovide event and telemetry ingress tooAzure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="8b826-113">toorun Olá implantação automaticamente, clique em Olá botão a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b826-113">toorun hello deployment automatically, click hello following button:</span></span>

<span data-ttu-id="8b826-114">[![Implantar tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="8b826-114">[![Deploy tooAzure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="8b826-115">parâmetros</span><span class="sxs-lookup"><span data-stu-id="8b826-115">Parameters</span></span>
<span data-ttu-id="8b826-116">No Gerenciador de recursos do Azure, você define parâmetros para os valores desejados toospecify quando Olá modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="8b826-116">With Azure Resource Manager, you define parameters for values you want toospecify when hello template is deployed.</span></span> <span data-ttu-id="8b826-117">modelo de saudação inclui uma seção chamada `Parameters` que contém todos os valores de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="8b826-117">hello template includes a section called `Parameters` that contains all hello parameter values.</span></span> <span data-ttu-id="8b826-118">Você deve definir um parâmetro para os valores que variam, com base em projeto Olá que estiver implantando ou com base em Olá ambiente toowhich que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="8b826-118">You should define a parameter for those values that will vary, based on hello project you are deploying or based on hello environment toowhich you are deploying.</span></span> <span data-ttu-id="8b826-119">Não defina parâmetros para valores que permanecem sempre Olá mesmo.</span><span class="sxs-lookup"><span data-stu-id="8b826-119">Do not define parameters for values that always stay hello same.</span></span> <span data-ttu-id="8b826-120">Cada valor de parâmetro no modelo de saudação define os recursos de saudação que são implantados.</span><span class="sxs-lookup"><span data-stu-id="8b826-120">Each parameter value in hello template defines hello resources that are deployed.</span></span>

<span data-ttu-id="8b826-121">modelo de saudação define Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b826-121">hello template defines hello following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="8b826-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="8b826-122">eventHubNamespaceName</span></span>
<span data-ttu-id="8b826-123">nome de saudação do hello toocreate de namespace de Hubs de eventos.</span><span class="sxs-lookup"><span data-stu-id="8b826-123">hello name of hello Event Hubs namespace toocreate.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="8b826-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="8b826-124">eventHubName</span></span>
<span data-ttu-id="8b826-125">nome de saudação do hub de eventos de saudação criado no namespace de Hubs de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b826-125">hello name of hello event hub created in hello Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="8b826-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="8b826-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="8b826-127">nome de saudação do grupo de consumidor Olá criado para o hub de eventos de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b826-127">hello name of hello consumer group created for hello event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="8b826-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="8b826-128">apiVersion</span></span>
<span data-ttu-id="8b826-129">versão de API de saudação do modelo de hello.</span><span class="sxs-lookup"><span data-stu-id="8b826-129">hello API version of hello template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-toodeploy"></a><span data-ttu-id="8b826-130">Recursos toodeploy</span><span class="sxs-lookup"><span data-stu-id="8b826-130">Resources toodeploy</span></span>
<span data-ttu-id="8b826-131">Cria um namespace do tipo **EventHubs**, com um hub de eventos e um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="8b826-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

```json
"resources":[  
      {  
         "apiVersion":"[variables('ehVersion')]",
         "name":"[parameters('namespaceName')]",
         "type":"Microsoft.EventHub/namespaces",
         "location":"[variables('location')]",
         "sku":{  
            "name":"Standard",
            "tier":"Standard"
         },
         "resources":[  
            {  
               "apiVersion":"[variables('ehVersion')]",
               "name":"[parameters('eventHubName')]",
               "type":"EventHubs",
               "dependsOn":[  
                  "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
               ],
               "properties":{  
                  "path":"[parameters('eventHubName')]"
               },
               "resources":[  
                  {  
                     "apiVersion":"[variables('ehVersion')]",
                     "name":"[parameters('consumerGroupName')]",
                     "type":"ConsumerGroups",
                     "dependsOn":[  
                        "[parameters('eventHubName')]"
                     ],
                     "properties":{  

                     }
                  }
               ]
            }
         ]
      }
   ],
```

## <a name="commands-toorun-deployment"></a><span data-ttu-id="8b826-132">Implantação de toorun de comandos</span><span class="sxs-lookup"><span data-stu-id="8b826-132">Commands toorun deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="8b826-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="8b826-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="8b826-134">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="8b826-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="8b826-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b826-135">Next steps</span></span>
<span data-ttu-id="8b826-136">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b826-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="8b826-137">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="8b826-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="8b826-138">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="8b826-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="8b826-139">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="8b826-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using hello Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
