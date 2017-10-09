---
title: "escala de aaaAutomatically unidades de taxa de transferência de Hubs de eventos do Azure | Microsoft Docs"
description: "Habilitar aumentar automaticamente em uma escala de tooautomatically namespace unidades de taxa de transferência"
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
ms.openlocfilehash: 0f5216bcd619ccddc1fd4063a2f0131bfa36c7d4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="automatically-scale-up-azure-event-hubs-throughput-units"></a><span data-ttu-id="12566-103">Escalar verticalmente automaticamente unidade de produtividade do Hub de Eventos do Azure</span><span class="sxs-lookup"><span data-stu-id="12566-103">Automatically scale up Azure Event Hubs throughput units</span></span>

## <a name="overview"></a><span data-ttu-id="12566-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="12566-104">Overview</span></span>

<span data-ttu-id="12566-105">Hubs de Eventos do Azure é uma plataforma de streaming de dados altamente escalonável.</span><span class="sxs-lookup"><span data-stu-id="12566-105">Azure Event Hubs is a highly scalable data streaming platform.</span></span> <span data-ttu-id="12566-106">Dessa forma, os clientes de Hubs de eventos geralmente aumentam seu uso depois integração toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="12566-106">As such, Event Hubs customers often increase their usage after onboarding toohello service.</span></span> <span data-ttu-id="12566-107">Esses aumentos exigem crescentes Olá predeterminado taxa de transferência unidades (elas) tooscale Hubs de eventos e lidar com taxas de transferência maior.</span><span class="sxs-lookup"><span data-stu-id="12566-107">Such increases require increasing hello predetermined throughput units (TUs) tooscale Event Hubs and handle larger transfer rates.</span></span> <span data-ttu-id="12566-108">Olá *aumentar automaticamente* recurso dos Hubs de eventos dimensiona automaticamente número de saudação de necessidades de uso de toomeet elas.</span><span class="sxs-lookup"><span data-stu-id="12566-108">hello *Auto-inflate* feature of Event Hubs automatically scales up hello number of TUs toomeet usage needs.</span></span> <span data-ttu-id="12566-109">O aumento de TUs evita cenários com limitação, nos quais:</span><span class="sxs-lookup"><span data-stu-id="12566-109">Increasing TUs prevents throttling scenarios, in which:</span></span>

* <span data-ttu-id="12566-110">As taxas de entrada de dados excedem as TUs definidas.</span><span class="sxs-lookup"><span data-stu-id="12566-110">Data ingress rates exceed set TUs.</span></span>
* <span data-ttu-id="12566-111">As taxas de solicitação de saída de dados excedem as TUs definidas.</span><span class="sxs-lookup"><span data-stu-id="12566-111">Data egress request rates exceed set TUs.</span></span>

## <a name="how-auto-inflate-works"></a><span data-ttu-id="12566-112">Como o Inflar automaticamente funciona</span><span class="sxs-lookup"><span data-stu-id="12566-112">How Auto-inflate works</span></span>

<span data-ttu-id="12566-113">O tráfego dos Hubs de Eventos é controlado por unidades de produtividade.</span><span class="sxs-lookup"><span data-stu-id="12566-113">Event Hubs traffic is controlled by throughput units.</span></span> <span data-ttu-id="12566-114">Uma única TU permite o ingresso de 1 MB/s ou saída com duas vezes essa quantidade.</span><span class="sxs-lookup"><span data-stu-id="12566-114">A single TU allows 1 MB per second of ingress and twice that amount of egress.</span></span> <span data-ttu-id="12566-115">Hubs de Evento Standard podem ser configurados com 1-20 unidades de produtividade.</span><span class="sxs-lookup"><span data-stu-id="12566-115">Standard Event Hubs can be configured with 1-20 throughput units.</span></span> <span data-ttu-id="12566-116">Aumentar automaticamente habilita toostart pequeno com unidades de taxa de transferência mínima necessária de saudação.</span><span class="sxs-lookup"><span data-stu-id="12566-116">Auto-inflate enables you toostart small with hello minimum required throughput units.</span></span> <span data-ttu-id="12566-117">recurso Olá expande automaticamente toohello o limite máximo de unidades de taxa de transferência que precisar, dependendo de aumento de saudação de seu tráfego.</span><span class="sxs-lookup"><span data-stu-id="12566-117">hello feature then scales automatically toohello maximum limit of throughput units you need, depending on hello increase in your traffic.</span></span> <span data-ttu-id="12566-118">Aumentar automaticamente fornece Olá benefícios a seguir:</span><span class="sxs-lookup"><span data-stu-id="12566-118">Auto-inflate provides hello following benefits:</span></span>

- <span data-ttu-id="12566-119">Um eficiente toostart mecanismo escala pequena e a escala se você aumentam.</span><span class="sxs-lookup"><span data-stu-id="12566-119">An efficient scaling mechanism toostart small and scale up as you grow.</span></span>
- <span data-ttu-id="12566-120">Dimensione automaticamente o limite superior especificado em toohello sem problemas de limitação.</span><span class="sxs-lookup"><span data-stu-id="12566-120">Automatically scale toohello specified upper limit without throttling issues.</span></span>
- <span data-ttu-id="12566-121">Mais controle sobre o dimensionamento, como controlar quando e quanto tooscale.</span><span class="sxs-lookup"><span data-stu-id="12566-121">More control over scaling, as you control when and how much tooscale.</span></span>

## <a name="enable-auto-inflate-on-a-namespace"></a><span data-ttu-id="12566-122">Habilitar o Inflar automaticamente em um namespace</span><span class="sxs-lookup"><span data-stu-id="12566-122">Enable Auto-inflate on a namespace</span></span>

<span data-ttu-id="12566-123">Você pode habilitar ou desabilitar a aumentar automaticamente em um namespace usando qualquer um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="12566-123">You can enable or disable Auto-inflate on a namespace using either of hello following methods:</span></span>

1. <span data-ttu-id="12566-124">Olá [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="12566-124">hello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="12566-125">Um modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="12566-125">An Azure Resource Manager template.</span></span>

### <a name="enable-auto-inflate-through-hello-portal"></a><span data-ttu-id="12566-126">Habilitar aumentar automaticamente por meio do portal Olá</span><span class="sxs-lookup"><span data-stu-id="12566-126">Enable Auto-inflate through hello portal</span></span>

<span data-ttu-id="12566-127">Você pode habilitar o recurso de aumentar automaticamente de saudação em um namespace durante a criação de um namespace de Hubs de eventos:</span><span class="sxs-lookup"><span data-stu-id="12566-127">You can enable hello Auto-inflate feature on a namespace when creating an Event Hubs namespace:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate1.png)

<span data-ttu-id="12566-128">Com essa opção habilitada, você pode começar pequeno em suas unidades de produtividade e escalar verticalmente à medida que suas necessidades de seu uso aumentam.</span><span class="sxs-lookup"><span data-stu-id="12566-128">With this option enabled, you can start small on your throughput units and scale up as your usage needs increase.</span></span> <span data-ttu-id="12566-129">Hello limite superior para inflação não afeta os preços, que depende de vários Olá elas usada por hora.</span><span class="sxs-lookup"><span data-stu-id="12566-129">hello upper limit for inflation does not affect pricing, which depends on hello number of TUs used per hour.</span></span>

<span data-ttu-id="12566-130">Você também pode habilitar inflar automática usando Olá **escala** opção na folha de configurações de saudação no portal de saudação:</span><span class="sxs-lookup"><span data-stu-id="12566-130">You can also enable Auto-inflate using hello **Scale** option on hello settings blade in hello portal:</span></span>
 
![](./media/event-hubs-auto-inflate/event-hubs-auto-inflate2.png)

### <a name="enable-auto-inflate-using-an-azure-resource-manager-template"></a><span data-ttu-id="12566-131">Habilitar Inflar automaticamente usando um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="12566-131">Enable Auto-Inflate using an Azure Resource Manager template</span></span>

<span data-ttu-id="12566-132">Você pode habilitar o Inflar automaticamente durante uma implantação de modelo do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="12566-132">You can enable Auto-inflate during an Azure Resource Manager template deployment.</span></span> <span data-ttu-id="12566-133">Por exemplo, o conjunto Olá `isAutoInflateEnabled` propriedade muito**true** e defina `maximumThroughputUnits` too10.</span><span class="sxs-lookup"><span data-stu-id="12566-133">For example, set hello `isAutoInflateEnabled` property too**true** and set `maximumThroughputUnits` too10.</span></span>

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

<span data-ttu-id="12566-134">Para o modelo completo de Olá, consulte Olá [namespace criar Hubs de eventos e habilitar inflar](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) modelo no GitHub.</span><span class="sxs-lookup"><span data-stu-id="12566-134">For hello complete template, see hello [Create Event Hubs namespace and enable inflate](https://github.com/Azure/azure-quickstart-templates/tree/master/201-eventhubs-create-namespace-and-enable-inflate) template on GitHub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="12566-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12566-135">Next steps</span></span>

<span data-ttu-id="12566-136">Você pode aprender mais sobre os Hubs de eventos visitando Olá links a seguir:</span><span class="sxs-lookup"><span data-stu-id="12566-136">You can learn more about Event Hubs by visiting hello following links:</span></span>

* [<span data-ttu-id="12566-137">Visão Geral dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="12566-137">Event Hubs overview</span></span>](event-hubs-what-is-event-hubs.md)
* [<span data-ttu-id="12566-138">Criar um Hub de Eventos</span><span class="sxs-lookup"><span data-stu-id="12566-138">Create an Event Hub</span></span>](event-hubs-create.md)
