---
title: "conector do aaaLearn toouse hello Azure Service Bus em seus aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Conecte-se tooAzure toosend de barramento de serviço e receber mensagens. Você pode executar ações como enviar tooqueue, enviar tootopic, receber da fila e receber de assinatura."
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
ms.openlocfilehash: c815ac167c3106ade470ce139d119085558a9497
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-azure-service-bus-connector"></a><span data-ttu-id="54b14-105">Introdução ao conector do Azure Service Bus Olá</span><span class="sxs-lookup"><span data-stu-id="54b14-105">Get started with hello Azure Service Bus connector</span></span>
<span data-ttu-id="54b14-106">Conecte-se tooAzure toosend de barramento de serviço e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="54b14-106">Connect tooAzure Service Bus toosend and receive messages.</span></span> <span data-ttu-id="54b14-107">Você pode executar ações como enviar tooqueue, enviar tootopic, receber da fila e receber de assinatura.</span><span class="sxs-lookup"><span data-stu-id="54b14-107">You can perform actions such as send tooqueue, send tootopic, receive from queue, and receive from subscription.</span></span>

<span data-ttu-id="54b14-108">toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="54b14-108">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="54b14-109">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="54b14-109">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-tooservice-bus"></a><span data-ttu-id="54b14-110">Conecte-se tooService barramento</span><span class="sxs-lookup"><span data-stu-id="54b14-110">Connect tooService Bus</span></span>
<span data-ttu-id="54b14-111">Antes de sua lógica de aplicativo pode acessar qualquer serviço, é necessário primeiro toocreate um serviço de toohello de conexão.</span><span class="sxs-lookup"><span data-stu-id="54b14-111">Before your logic app can access any service, you first need toocreate a connection toohello service.</span></span> <span data-ttu-id="54b14-112">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="54b14-112">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

> [!INCLUDE [Steps toocreate a connection tooAzure Service Bus](../../includes/connectors-create-api-servicebus.md)]
> 
> 

## <a name="use-a-service-bus-trigger"></a><span data-ttu-id="54b14-113">Usar um gatilho do Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="54b14-113">Use a Service Bus trigger</span></span>
<span data-ttu-id="54b14-114">Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="54b14-114">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="54b14-115">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="54b14-115">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>  

> [!INCLUDE [Steps toocreate a Service Bus trigger](../../includes/connectors-create-api-servicebus-trigger.md)]
> 
> 

## <a name="use-a-service-bus-action"></a><span data-ttu-id="54b14-116">Usar uma ação de Barramento de Serviço</span><span class="sxs-lookup"><span data-stu-id="54b14-116">Use a Service Bus action</span></span>
<span data-ttu-id="54b14-117">Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="54b14-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="54b14-118">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="54b14-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

[!INCLUDE [Steps toocreate a Service Bus action](../../includes/connectors-create-api-servicebus-action.md)]

## <a name="connector-specific-details"></a><span data-ttu-id="54b14-119">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="54b14-119">Connector-specific details</span></span>

<span data-ttu-id="54b14-120">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/servicebus/).</span><span class="sxs-lookup"><span data-stu-id="54b14-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/servicebus/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="54b14-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="54b14-121">Next steps</span></span>
<span data-ttu-id="54b14-122">[Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="54b14-122">[Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

