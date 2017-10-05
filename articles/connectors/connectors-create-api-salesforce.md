---
title: "Aprenda a usar o Conector do Salesforce em seus aplicativos lógicos | Microsoft Docs"
description: "Crie aplicativos lógicos com o serviço de Aplicativo do Azure. O Conector do Salesforce fornece uma API para trabalhar com objetos do Salesforce."
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
ms.openlocfilehash: c2e2efd356382df9404f5c4ed54f24758b2cd22b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-salesforce-connector"></a><span data-ttu-id="03f7a-104">Introdução ao conector do Salesforce</span><span class="sxs-lookup"><span data-stu-id="03f7a-104">Get started with the Salesforce connector</span></span>
<span data-ttu-id="03f7a-105">O Conector do Salesforce fornece uma API para trabalhar com objetos do Salesforce.</span><span class="sxs-lookup"><span data-stu-id="03f7a-105">The Salesforce Connector provides an API to work with Salesforce objects.</span></span>

<span data-ttu-id="03f7a-106">Para usar [qualquer conector](apis-list.md), primeiro é preciso criar um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="03f7a-106">To use [any connector](apis-list.md), you first need to create a logic app.</span></span> <span data-ttu-id="03f7a-107">Você pode começar [criando um aplicativo lógico agora mesmo](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="03f7a-107">You can get started by [creating a logic app now](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="connect-to-salesforce-connector"></a><span data-ttu-id="03f7a-108">Ligar-se ao conector do Salesforce</span><span class="sxs-lookup"><span data-stu-id="03f7a-108">Connect to Salesforce connector</span></span>
<span data-ttu-id="03f7a-109">Para que o aplicativo lógico possa acessar qualquer serviço, crie primeiro uma *conexão* com o serviço.</span><span class="sxs-lookup"><span data-stu-id="03f7a-109">Before your logic app can access any service, you first need to create a *connection* to the service.</span></span> <span data-ttu-id="03f7a-110">Uma [conexão](connectors-overview.md) fornece uma conectividade entre um aplicativo lógico e outro serviço.</span><span class="sxs-lookup"><span data-stu-id="03f7a-110">A [connection](connectors-overview.md) provides connectivity between a logic app and another service.</span></span>  

### <a name="create-a-connection-to-salesforce-connector"></a><span data-ttu-id="03f7a-111">Criar uma conexão com o conector do Salesforce</span><span class="sxs-lookup"><span data-stu-id="03f7a-111">Create a connection to Salesforce connector</span></span>
> [!INCLUDE [Steps to create a connection to Salesforce Connector](../../includes/connectors-create-api-salesforce.md)]
> 
> 

## <a name="use-a-salesforce-connector-trigger"></a><span data-ttu-id="03f7a-112">Usar um gatilho do conector do Salesforce</span><span class="sxs-lookup"><span data-stu-id="03f7a-112">Use a Salesforce connector trigger</span></span>
<span data-ttu-id="03f7a-113">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="03f7a-113">A trigger is an event that can be used to start the workflow defined in a logic app.</span></span> <span data-ttu-id="03f7a-114">[Saiba mais sobre gatilhos](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="03f7a-114">[Learn more about triggers](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce trigger](../../includes/connectors-create-api-salesforce-trigger.md)]
> 
> 

## <a name="add-a-condition"></a><span data-ttu-id="03f7a-115">Adicionar uma condição</span><span class="sxs-lookup"><span data-stu-id="03f7a-115">Add a condition</span></span>
> [!INCLUDE [Steps to create a Salesforce condition](../../includes/connectors-create-api-salesforce-condition.md)]
> 
> 

## <a name="use-a-salesforce-connector-action"></a><span data-ttu-id="03f7a-116">Usar uma ação do conector do Salesforce</span><span class="sxs-lookup"><span data-stu-id="03f7a-116">Use a Salesforce connector action</span></span>
<span data-ttu-id="03f7a-117">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="03f7a-117">An action is an operation carried out by the workflow defined in a logic app.</span></span> <span data-ttu-id="03f7a-118">[Saiba mais sobre ações](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span><span class="sxs-lookup"><span data-stu-id="03f7a-118">[Learn more about actions](../logic-apps/logic-apps-what-are-logic-apps.md#logic-app-concepts).</span></span>

> [!INCLUDE [Steps to create a Salesforce action](../../includes/connectors-create-api-salesforce-action.md)]
> 
> 

## <a name="connector-specific-details"></a><span data-ttu-id="03f7a-119">Detalhes específicos do conector</span><span class="sxs-lookup"><span data-stu-id="03f7a-119">Connector-specific details</span></span>

<span data-ttu-id="03f7a-120">Exiba os gatilhos e ações definidos no swagger e também os limites nos [detalhes do conector](/connectors/salesforce/).</span><span class="sxs-lookup"><span data-stu-id="03f7a-120">View any triggers and actions defined in the swagger, and also see any limits in the [connector details](/connectors/salesforce/).</span></span> 

## <a name="next-steps"></a><span data-ttu-id="03f7a-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03f7a-121">Next steps</span></span>
[<span data-ttu-id="03f7a-122">Criar um aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="03f7a-122">Create a logic app</span></span>](../logic-apps/logic-apps-create-a-logic-app.md)

