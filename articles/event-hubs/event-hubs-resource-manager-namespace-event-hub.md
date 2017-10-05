---
title: Criar grupo de consumidores e namespace de Hubs de Eventos do Azure usando um modelo | Microsoft Docs
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
ms.openlocfilehash: eb9a80eec0326aaa605cb8b21aecbaeec94ff212
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-an-event-hubs-namespace-with-event-hub-and-consumer-group-using-an-azure-resource-manager-template"></a><span data-ttu-id="97db9-103">Criar um namespace dos Hubs de Eventos com um hub de eventos e um grupo de consumidores usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="97db9-103">Create an Event Hubs namespace with event hub and consumer group using an Azure Resource Manager template</span></span>

<span data-ttu-id="97db9-104">Este artigo mostra como usar um modelo do Azure Resource Manager que cria um namespace do tipo Hubs de Eventos com um Hub de Eventos e um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="97db9-104">This article shows how to use an Azure Resource Manager template that creates a namespace of type Event Hubs, with one event hub and one consumer group.</span></span> <span data-ttu-id="97db9-105">O artigo mostra como definir quais recursos são implantados e como definir os parâmetros que são especificados quando a implantação é executada.</span><span class="sxs-lookup"><span data-stu-id="97db9-105">The article shows how to define which resources are deployed and how to define parameters that are specified when the deployment is executed.</span></span> <span data-ttu-id="97db9-106">Você pode usar este modelo para suas próprias implantações ou personalizá-lo para atender às suas necessidades</span><span class="sxs-lookup"><span data-stu-id="97db9-106">You can use this template for your own deployments, or customize it to meet your requirements</span></span>

<span data-ttu-id="97db9-107">Para obter mais informações sobre a criação de modelos, consulte [Criação de Modelos do Azure Resource Manager][Authoring Azure Resource Manager templates].</span><span class="sxs-lookup"><span data-stu-id="97db9-107">For more information about creating templates, see [Authoring Azure Resource Manager templates][Authoring Azure Resource Manager templates].</span></span>

<span data-ttu-id="97db9-108">Para ver o modelo completo, consulte o [Modelo de hub de eventos e grupo de consumidores][Event Hub and consumer group template] no GitHub.</span><span class="sxs-lookup"><span data-stu-id="97db9-108">For the complete template, see the [Event hub and consumer group template][Event Hub and consumer group template] on GitHub.</span></span>

> [!NOTE]
> <span data-ttu-id="97db9-109">Para verificar os modelos mais recentes, visite a galeria [Modelos de Início Rápido do Azure][Azure Quickstart Templates] e procure por Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="97db9-109">To check for the latest templates, visit the [Azure Quickstart Templates][Azure Quickstart Templates] gallery and search for Event Hubs.</span></span>
> 
> 

## <a name="what-will-you-deploy"></a><span data-ttu-id="97db9-110">O que você implantará?</span><span class="sxs-lookup"><span data-stu-id="97db9-110">What will you deploy?</span></span>
<span data-ttu-id="97db9-111">Com este modelo, você implantará um namespace Hubs de Evento com um hub de eventos e um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="97db9-111">With this template, you will deploy an Event Hubs namespace with an event hub and a consumer group.</span></span>

<span data-ttu-id="97db9-112">[Hubs de Eventos](event-hubs-what-is-event-hubs.md) é um serviço de processamento de eventos usado para fornecer entrada a telemetria e eventos para o Azure em grande escala, com baixa latência e alta confiabilidade.</span><span class="sxs-lookup"><span data-stu-id="97db9-112">[Event Hubs](event-hubs-what-is-event-hubs.md) is an event processing service used to provide event and telemetry ingress to Azure at massive scale, with low latency and high reliability.</span></span>

<span data-ttu-id="97db9-113">Para executar a implantação automaticamente, clique no seguinte botão:</span><span class="sxs-lookup"><span data-stu-id="97db9-113">To run the deployment automatically, click the following button:</span></span>

<span data-ttu-id="97db9-114">[![Implantar no Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span><span class="sxs-lookup"><span data-stu-id="97db9-114">[![Deploy to Azure](./media/event-hubs-resource-manager-namespace-event-hub/deploybutton.png)](https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F201-event-hubs-create-event-hub-and-consumer-group%2Fazuredeploy.json)</span></span>

## <a name="parameters"></a><span data-ttu-id="97db9-115">Parâmetros</span><span class="sxs-lookup"><span data-stu-id="97db9-115">Parameters</span></span>
<span data-ttu-id="97db9-116">Com o Gerenciador de Recursos do Azure, você define parâmetros para os valores que deseja especificar quando o modelo é implantado.</span><span class="sxs-lookup"><span data-stu-id="97db9-116">With Azure Resource Manager, you define parameters for values you want to specify when the template is deployed.</span></span> <span data-ttu-id="97db9-117">O modelo inclui uma seção chamada `Parameters` , que contém todos os valores de parâmetro.</span><span class="sxs-lookup"><span data-stu-id="97db9-117">The template includes a section called `Parameters` that contains all the parameter values.</span></span> <span data-ttu-id="97db9-118">Você deve definir um parâmetro para os valores que variam de acordo com o projeto que você está implantando ou com o ambiente em que você está implantando.</span><span class="sxs-lookup"><span data-stu-id="97db9-118">You should define a parameter for those values that will vary, based on the project you are deploying or based on the environment to which you are deploying.</span></span> <span data-ttu-id="97db9-119">Não defina parâmetros para valores que permanecem sempre os mesmos.</span><span class="sxs-lookup"><span data-stu-id="97db9-119">Do not define parameters for values that always stay the same.</span></span> <span data-ttu-id="97db9-120">Cada valor de parâmetro no modelo define os recursos que são implantados.</span><span class="sxs-lookup"><span data-stu-id="97db9-120">Each parameter value in the template defines the resources that are deployed.</span></span>

<span data-ttu-id="97db9-121">O modelo define os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="97db9-121">The template defines the following parameters:</span></span>

### <a name="eventhubnamespacename"></a><span data-ttu-id="97db9-122">eventHubNamespaceName</span><span class="sxs-lookup"><span data-stu-id="97db9-122">eventHubNamespaceName</span></span>
<span data-ttu-id="97db9-123">O nome do namespace Hubs de Evento a criar.</span><span class="sxs-lookup"><span data-stu-id="97db9-123">The name of the Event Hubs namespace to create.</span></span>

```json
"eventHubNamespaceName": {
"type": "string"
}
```

### <a name="eventhubname"></a><span data-ttu-id="97db9-124">eventHubName</span><span class="sxs-lookup"><span data-stu-id="97db9-124">eventHubName</span></span>
<span data-ttu-id="97db9-125">O nome do hub de eventos criado no namespace Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="97db9-125">The name of the event hub created in the Event Hubs namespace.</span></span>

```json
"eventHubName": {
"type": "string"
}
```

### <a name="eventhubconsumergroupname"></a><span data-ttu-id="97db9-126">eventHubConsumerGroupName</span><span class="sxs-lookup"><span data-stu-id="97db9-126">eventHubConsumerGroupName</span></span>
<span data-ttu-id="97db9-127">O nome do grupo de consumidores criado para o hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="97db9-127">The name of the consumer group created for the event hub.</span></span>

```json
"eventHubConsumerGroupName": {
"type": "string"
}
```

### <a name="apiversion"></a><span data-ttu-id="97db9-128">apiVersion</span><span class="sxs-lookup"><span data-stu-id="97db9-128">apiVersion</span></span>
<span data-ttu-id="97db9-129">A versão da API do modelo.</span><span class="sxs-lookup"><span data-stu-id="97db9-129">The API version of the template.</span></span>

```json
"apiVersion": {
"type": "string"
}
```

## <a name="resources-to-deploy"></a><span data-ttu-id="97db9-130">Recursos a implantar</span><span class="sxs-lookup"><span data-stu-id="97db9-130">Resources to deploy</span></span>
<span data-ttu-id="97db9-131">Cria um namespace do tipo **EventHubs**, com um hub de eventos e um grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="97db9-131">Creates a namespace of type **EventHubs**, with an event hub and a consumer group.</span></span>

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

## <a name="commands-to-run-deployment"></a><span data-ttu-id="97db9-132">Comandos para executar a implantação</span><span class="sxs-lookup"><span data-stu-id="97db9-132">Commands to run deployment</span></span>
[!INCLUDE [app-service-deploy-commands](../../includes/app-service-deploy-commands.md)]

## <a name="powershell"></a><span data-ttu-id="97db9-133">PowerShell</span><span class="sxs-lookup"><span data-stu-id="97db9-133">PowerShell</span></span>
```powershell
New-AzureRmResourceGroupDeployment -ResourceGroupName \<resource-group-name\> -TemplateFile https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json
```

## <a name="azure-cli"></a><span data-ttu-id="97db9-134">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="97db9-134">Azure CLI</span></span>
```cli
azure config mode arm

azure group deployment create \<my-resource-group\> \<my-deployment-name\> --template-uri [https://raw.githubusercontent.com/azure/azure-quickstart-templates/master/201-event-hubs-create-event-hub-and-consumer-group/azuredeploy.json][]
```

## <a name="next-steps"></a><span data-ttu-id="97db9-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="97db9-135">Next steps</span></span>
<span data-ttu-id="97db9-136">Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:</span><span class="sxs-lookup"><span data-stu-id="97db9-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="97db9-137">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="97db9-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="97db9-138">Criar um hub de eventos</span><span class="sxs-lookup"><span data-stu-id="97db9-138">Create an event hub</span></span>](event-hubs-create.md)
* [<span data-ttu-id="97db9-139">Perguntas frequentes sobre os Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="97db9-139">Event Hubs FAQ</span></span>](event-hubs-faq.md)

[Authoring Azure Resource Manager templates]: ../azure-resource-manager/resource-group-authoring-templates.md
[Azure Quickstart Templates]:  https://azure.microsoft.com/documentation/templates/?term=event+hubs
[Using Azure PowerShell with Azure Resource Manager]: ../powershell-azure-resource-manager.md
[Using the Azure CLI for Mac, Linux, and Windows with Azure Resource Management]: ../xplat-cli-azure-resource-manager.md
[Event hub and consumer group template]: https://github.com/Azure/azure-quickstart-templates/blob/master/201-event-hubs-create-event-hub-and-consumer-group/
