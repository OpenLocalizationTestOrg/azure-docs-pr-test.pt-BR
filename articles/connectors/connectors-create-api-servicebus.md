---
title: "Saiba como usar o conector do Barramento de Serviço do Azure nos seus aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Conecte-se ao Barramento de Serviço do Azure para enviar e receber mensagens. Você pode executar ações como enviar para a fila, enviar para o tópico, receber da fila e receber da assinatura."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: d6d14f5f-2126-4e33-808e-41de08e6721f
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 08/02/2016
ms.author: mandia; ladocs
ms.openlocfilehash: 1e2ce06f5993280dbdb67121849591e67f7979e9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-azure-service-bus-connector"></a><span data-ttu-id="c64d2-105">Introdução ao conector do Barramento de Serviço do Azure</span><span class="sxs-lookup"><span data-stu-id="c64d2-105">Get started with the Azure Service Bus connector</span></span>
<span data-ttu-id="c64d2-106">Conecte-se ao Barramento de Serviço do Azure para enviar e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="c64d2-106">Connect to Azure Service Bus to send and receive messages.</span></span> <span data-ttu-id="c64d2-107">Você pode executar ações como enviar para a fila, enviar para o tópico, receber da fila e receber da assinatura.</span><span class="sxs-lookup"><span data-stu-id="c64d2-107">You can perform actions such as send to queue, send to topic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="c64d2-108">Para usar [qualquer conector](apis-list.md), primeiro é preciso criar um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="c64d2-108">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="c64d2-109">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c64d2-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-service-bus"></a><span data-ttu-id="c64d2-110">Conectar-se ao Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="c64d2-110">Connect to Service Bus</span></span>
<span data-ttu-id="c64d2-111">Para que o aplicativo lógico possa acessar qualquer serviço, crie primeiro uma conexão com o serviço.</span><span class="sxs-lookup"><span data-stu-id="c64d2-111">Before your logic app can access any service, you first need to create a connection to the service.</span></span> <span data-ttu-id="c64d2-112">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="c64d2-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps to create a connection to Azure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="c64d2-113">Usar um gatilho do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="c64d2-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="c64d2-114">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="c64d2-114">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="c64d2-115">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c64d2-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps to create a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="c64d2-116">Usar uma ação de Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="c64d2-116">Use a Service Bus action</span></span>
<span data-ttu-id="c64d2-117">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="c64d2-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="c64d2-118">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="c64d2-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps to create a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="c64d2-119">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="c64d2-119">Connector-specific details</span></span>

<span data-ttu-id="c64d2-120">Exiba os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="c64d2-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="c64d2-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c64d2-121">Next steps</span></span>
<span data-ttu-id="c64d2-122">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="c64d2-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

