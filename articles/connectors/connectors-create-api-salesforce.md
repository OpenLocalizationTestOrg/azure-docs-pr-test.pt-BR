---
title: "aaaLearn toouse Olá conector da equipe de vendas em seus aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. Olá, equipe de vendas conector fornece toowork uma API com objetos do Salesforce."
services: logic-apps
documentationcenter: .net,nodejs,java
author: MandiOhlinger
manager: anneta
editor: 
tags: connectors
ms.assetid: 54fe5af8-7d2a-4da8-94e7-15d029e029bf
ms.service: logic-apps
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: integration
ms.date: 10/05/2016
ms.author: mandia; ladocs
ms.openlocfilehash: b14b41fa8a4648b4f0090472dc0f9575bf13a2ad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-salesforce-connector"></a><span data-ttu-id="817ab-104">Introdução ao conector do Salesforce Olá</span><span class="sxs-lookup"><span data-stu-id="817ab-104">Get started with hello Salesforce connector</span></span>
<span data-ttu-id="817ab-105">Olá, equipe de vendas conector fornece toowork uma API com objetos do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="817ab-105">hello Salesforce Connector provides an API toowork with Salesforce objects.</span></span>

<span data-ttu-id="817ab-106">toouse [qualquer conector](apis-list.md), primeiro é necessário toocreate um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="817ab-106">toouse [any connector](apis-list.md), you first need toocreate a logic app.</span></span> <span data-ttu-id="817ab-107">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="817ab-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-toosalesforce-connector"></a><span data-ttu-id="817ab-108">Conecte-se o conector de tooSalesforce</span><span class="sxs-lookup"><span data-stu-id="817ab-108">Connect tooSalesforce connector</span></span>
<span data-ttu-id="817ab-109">Antes de sua lógica de aplicativo pode acessar qualquer serviço, primeiro é necessário toocreate um *conexão* toohello service.</span><span class="sxs-lookup"><span data-stu-id="817ab-109">Before your logic app can access any service, you first need toocreate a *connection* toohello service.</span></span> <span data-ttu-id="817ab-110">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="817ab-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-toosalesforce-connector"></a><span data-ttu-id="817ab-111">Criar um conector de tooSalesforce de conexão</span><span class="sxs-lookup"><span data-stu-id="817ab-111">Create a connection tooSalesforce connector</span></span>
> [!INCLUDE [Steps toocreate a connection tooSalesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="817ab-112">Usar um gatilho do conector do Salesforce</span><span class="sxs-lookup"><span data-stu-id="817ab-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="817ab-113">Um gatilho é um evento que pode ser o fluxo de trabalho do hello toostart usado definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="817ab-113">A trigger is an event that can be used toostart hello workflow defined in a logic app.</span></span> <span data-ttu-id="817ab-114">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="817ab-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="817ab-115">Adicionar uma condição</span><span class="sxs-lookup"><span data-stu-id="817ab-115">Add a condition</span></span>
> [!INCLUDE [Steps toocreate a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="817ab-116">Usar uma ação do conector do Salesforce</span><span class="sxs-lookup"><span data-stu-id="817ab-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="817ab-117">Uma ação é uma operação executada pelo fluxo de trabalho Olá definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="817ab-117">An action is an operation carried out by hello workflow defined in a logic app.</span></span> <span data-ttu-id="817ab-118">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="817ab-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps toocreate a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="817ab-119">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="817ab-119">Connector-specific details</span></span>

<span data-ttu-id="817ab-120">Exibir quaisquer gatilhos e ações definidas em swagger Olá e também os limites de saudação [detalhes conector](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="817ab-120">View any triggers and actions defined in hello swagger, and also see any limits in hello [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="817ab-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="817ab-121">Next steps</span></span>
[<span data-ttu-id="817ab-122">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="817ab-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

