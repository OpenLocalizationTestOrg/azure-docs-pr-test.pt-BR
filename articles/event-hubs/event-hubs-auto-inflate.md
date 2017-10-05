---
title: Escalar verticalmente automaticamente unidade de produtividade do Hub de Eventos do Azure | Microsoft Docs
description: "Habilitar Inflação automática em um namespace para escalar verticalmente automaticamente as unidades de produtividade"
services: event-hubs
documentationcenter: na
author: ShubhaVijayasarathy
manager: timlt
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/12/2017
ms.author: shvija;sethm
ms.openlocfilehash: b085091ea7bfd601efb0eee84144ddd091422d6e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="22ce9-103">Escalar verticalmente automaticamente unidade de produtividade do Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="22ce9-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="22ce9-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="22ce9-104">Overview</span></span>

<span data-ttu-id="22ce9-105">Hubs de Eventos do Azure é uma plataforma de streaming de dados altamente escalonável.</span><span class="sxs-lookup"><span data-stu-id="22ce9-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="22ce9-106">Dessa forma, os clientes do Hubs de Eventos geralmente aumentam seu uso após a migração para o serviço.</span><span class="sxs-lookup"><span data-stu-id="22ce9-106">As such, Event Hubs customers often increase their usage after onboarding to the service.</span></span> <span data-ttu-id="22ce9-107">Tal aumento exige o aumento de TUs (unidades de produtividade) predeterminadas para dimensionar os Hubs de Eventos e lidar com taxas de transferência maiores.</span><span class="sxs-lookup"><span data-stu-id="22ce9-107">Such increases require increasing the predetermined throughput units (TUs) to scale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="22ce9-108">O recurso *inflar automaticamente* dos Hubs de Eventos escala verticalmente automaticamente o número delas para atender às necessidades de uso.</span><span class="sxs-lookup"><span data-stu-id="22ce9-108">The *Auto-inflate* feature of Event Hubs automatically scales up the number of TUs to meet usage needs.</span></span> <span data-ttu-id="22ce9-109">O aumento de TUs evita cenários com limitação, nos quais:</span><span class="sxs-lookup"><span data-stu-id="22ce9-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="22ce9-110">As taxas de entrada de dados excedem as TUs definidas.</span><span class="sxs-lookup"><span data-stu-id="22ce9-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="22ce9-111">As taxas de solicitação de saída de dados excedem as TUs definidas.</span><span class="sxs-lookup"><span data-stu-id="22ce9-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="22ce9-112">Como o Inflar automaticamente funciona</span><span class="sxs-lookup"><span data-stu-id="22ce9-112">How Auto-inflate works</span></span>

<span data-ttu-id="22ce9-113">O tráfego dos Hubs de Eventos é controlado por unidades de produtividade.</span><span class="sxs-lookup"><span data-stu-id="22ce9-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="22ce9-114">Uma única TU permite o ingresso de 1 MB/s ou saída com duas vezes essa quantidade.</span><span class="sxs-lookup"><span data-stu-id="22ce9-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="22ce9-115">Hubs de Evento Standard podem ser configurados com 1-20 unidades de produtividade.</span><span class="sxs-lookup"><span data-stu-id="22ce9-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="22ce9-116">Inflar automaticamente permite que você comece pequeno, com o mínimo de unidades de produtividade necessárias.</span><span class="sxs-lookup"><span data-stu-id="22ce9-116">Auto-inflate enables you to start small with the minimum required throughput units.</span></span> <span data-ttu-id="22ce9-117">O recurso então dimensiona automaticamente para o limite máximo de unidades de produtividade que você precisa, dependendo do aumento de seu tráfego.</span><span class="sxs-lookup"><span data-stu-id="22ce9-117">The feature then scales automatically to the maximum limit of throughput units you need, depending on the increase in your traffic.</span></span> <span data-ttu-id="22ce9-118">O Inflar automaticamente oferece os seguintes benefícios:</span><span class="sxs-lookup"><span data-stu-id="22ce9-118">Auto-inflate provides the following benefits:</span></span>

- <span data-ttu-id="22ce9-119">Um mecanismo eficiente de colocação em escala para começar pequeno e escalar verticalmente conforme o crescimento.</span><span class="sxs-lookup"><span data-stu-id="22ce9-119">An efficient scaling mechanism to start small and scale up as you grow.</span></span>
- <span data-ttu-id="22ce9-120">Dimensione automaticamente para o limite superior especificado sem problemas de limitação.</span><span class="sxs-lookup"><span data-stu-id="22ce9-120">Automatically scale to the specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="22ce9-121">Mais controle sobre a colocação em escala, já que você controla quando e quanto dimensionar.</span><span class="sxs-lookup"><span data-stu-id="22ce9-121">More control over scaling, as you control when and how much to scale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="22ce9-122">Habilitar o Inflar automaticamente em um namespace</span><span class="sxs-lookup"><span data-stu-id="22ce9-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="22ce9-123">Você pode habilitar ou desabilitar o Inflar automaticamente em um namespace usando qualquer um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="22ce9-123">You can enable or disable Auto-inflate on a namespace using either of the following methods:</span></span>

1. <span data-ttu-id="22ce9-124">O [Portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="22ce9-124">The [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="22ce9-125">Um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="22ce9-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-the-portal"></a><span data-ttu-id="22ce9-126">Habilitar Inflar automaticamente por meio do Portal</span><span class="sxs-lookup"><span data-stu-id="22ce9-126">Enable Auto-inflate through the portal</span></span>

<span data-ttu-id="22ce9-127">Você pode habilitar o recurso Inflar automaticamente em um namespace durante a criação de um namespace de Hubs de Eventos:</span><span class="sxs-lookup"><span data-stu-id="22ce9-127">You can enable the Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="22ce9-128">Com essa opção habilitada, você pode começar pequeno em suas unidades de produtividade e escalar verticalmente à medida que suas necessidades de seu uso aumentam.</span><span class="sxs-lookup"><span data-stu-id="22ce9-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="22ce9-129">O limite superior para inflação não afeta os preços, que dependem do número de TUs usadas por hora.</span><span class="sxs-lookup"><span data-stu-id="22ce9-129">The upper limit for inflation does not affect pricing, which depends on the number of TUs used per hour.</span></span>

<span data-ttu-id="22ce9-130">Você também pode habilitar o Inflar automaticamente usando a opção **Dimensionar** na folha de configurações no portal:</span><span class="sxs-lookup"><span data-stu-id="22ce9-130">You can also enable Auto-inflate using the **Scale** option on the settings blade in the portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="22ce9-131">Habilitar Inflar automaticamente usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="22ce9-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="22ce9-132">Você pode habilitar o Inflar automaticamente durante uma implantação de modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="22ce9-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="22ce9-133">Por exemplo, defina a propriedade `isAutoInflateEnabled` como **true** e defina `maximumThroughputUnits` como 10.</span><span class="sxs-lookup"><span data-stu-id="22ce9-133">For example, set the `isAutoInflateEnabled` property to **true** and set `maximumThroughputUnits` to 10.</span></span>

```json
"resources": [
        {
            "apiVersion": "2017-04-01",
            "name": "[parameters('namespaceName')]",
            "type": "Microsoft.EventHub/Namespaces",
            "location": "[variables('location')]",
            "sku": {
                "name": "Standard",
                "tier": "Standard"
            },
            "properties": {
                "isAutoInflateEnabled": true,
                "maximumThroughputUnits": 10
            },
            "resources": [
                {
                    "apiVersion": "2017-04-01",
                    "name": "[parameters('eventHubName')]",
                    "type": "EventHubs",
                    "dependsOn": [
                        "[concat('Microsoft.EventHub/namespaces/', parameters('namespaceName'))]"
                    ],
                    "properties": {},
                    "resources": [
                        {
                            "apiVersion": "2017-04-01",
                            "name": "[parameters('consumerGroupName')]",
                            "type": "ConsumerGroups",
                            "dependsOn": [
                                "[parameters('eventHubName')]"
                            ],
                            "properties": {}
                        }
                    ]
                }
            ]
        }
    ]
```

<span data-ttu-id="22ce9-134">Para ver o modelo completo, consulte o modelo [Criar namespace de Hubs de Eventos e habilitar inflar](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) no GitHub.</span><span class="sxs-lookup"><span data-stu-id="22ce9-134">For the complete template, see the [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="22ce9-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="22ce9-135">Next steps</span></span>

<span data-ttu-id="22ce9-136">Você pode saber mais sobre Hubs de Eventos visitando os links abaixo:</span><span class="sxs-lookup"><span data-stu-id="22ce9-136">You can learn more about Event Hubs by visiting the following links:</span></span>

* [<span data-ttu-id="22ce9-137">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="22ce9-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="22ce9-138">Criar um Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="22ce9-138">Create an Event Hub</span></span>](event-hubs-create.md)
