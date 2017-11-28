---
title: "gatilho de recorrência Olá aaaAdd em aplicativos lógicos | Microsoft Docs"
description: "Visão geral de gatilho de recorrência Olá e como toouse com um aplicativo do Azure lógica."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 51dd4f22-7dc5-41af-a0a9-e7148378cd50
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e7c625c382a88a1e7cdfff4ddc0caf55727232bd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-recurrence-trigger"></a><span data-ttu-id="e0879-103">Introdução ao gatilho de recorrência Olá</span><span class="sxs-lookup"><span data-stu-id="e0879-103">Get started with hello recurrence trigger</span></span>
<span data-ttu-id="e0879-104">Usando o gatilho de recorrência hello, você pode criar fluxos de trabalho poderosos na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="e0879-104">By using hello recurrence trigger, you can create powerful workflows in hello cloud.</span></span>

<span data-ttu-id="e0879-105">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="e0879-105">For example, you can:</span></span>

* <span data-ttu-id="e0879-106">Agende um fluxo de trabalho toorun um procedimento armazenado SQL diariamente.</span><span class="sxs-lookup"><span data-stu-id="e0879-106">Schedule a workflow toorun a SQL stored procedure every day.</span></span>
* <span data-ttu-id="e0879-107">Um resumo de todos os tweets dentro Olá última semana sobre um determinado hashtag de email.</span><span class="sxs-lookup"><span data-stu-id="e0879-107">Email a summary of all tweets within hello last week about a certain hashtag.</span></span>

<span data-ttu-id="e0879-108">tooget iniciado usando o gatilho de recorrência de saudação em um aplicativo de lógica, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e0879-108">tooget started using hello recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="e0879-109">Usar um gatilho de recorrência</span><span class="sxs-lookup"><span data-stu-id="e0879-109">Use a recurrence trigger</span></span>
<span data-ttu-id="e0879-110">Um gatilho é um evento que pode ser usado toostart Olá fluxo de trabalho é definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="e0879-110">A trigger is an event that can be used toostart hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="e0879-111">[Saiba mais sobre gatilhos](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="e0879-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="e0879-112">Aqui está uma sequência de exemplo de como tooset backup uma recorrência disparar em um aplicativo de lógica:</span><span class="sxs-lookup"><span data-stu-id="e0879-112">Here’s an example sequence of how tooset up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="e0879-113">Adicionar Olá **recorrência** disparador como primeira etapa Olá em um aplicativo de lógica.</span><span class="sxs-lookup"><span data-stu-id="e0879-113">Add hello **Recurrence** trigger as hello first step in a logic app.</span></span>
2. <span data-ttu-id="e0879-114">Preencha os parâmetros Olá Olá intervalo de recorrência.</span><span class="sxs-lookup"><span data-stu-id="e0879-114">Fill in hello parameters for hello recurrence interval.</span></span>

<span data-ttu-id="e0879-115">Olá lógica aplicativo agora inicia uma execução depois de cada intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="e0879-115">hello logic app now starts a run after each interval of time.</span></span>

![Gatilho HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="e0879-117">Detalhes do gatilho</span><span class="sxs-lookup"><span data-stu-id="e0879-117">Trigger details</span></span>
<span data-ttu-id="e0879-118">gatilho de recorrência Olá tem Olá propriedades que você pode configurar a seguir.</span><span class="sxs-lookup"><span data-stu-id="e0879-118">hello recurrence trigger has hello following properties that you can configure.</span></span>

<span data-ttu-id="e0879-119">Ele dispara um aplicativo lógico depois de um intervalo de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="e0879-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="e0879-120">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="e0879-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="e0879-121">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="e0879-121">Display name</span></span> | <span data-ttu-id="e0879-122">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="e0879-122">Property name</span></span> | <span data-ttu-id="e0879-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="e0879-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="e0879-124">Frequência*</span><span class="sxs-lookup"><span data-stu-id="e0879-124">Frequency*</span></span> |<span data-ttu-id="e0879-125">frequência</span><span class="sxs-lookup"><span data-stu-id="e0879-125">frequency</span></span> |<span data-ttu-id="e0879-126">unidade de saudação de tempo: `Second`, `Minute`, `Hour`, `Day`, ou `Year`.</span><span class="sxs-lookup"><span data-stu-id="e0879-126">hello unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="e0879-127">Intervalo*</span><span class="sxs-lookup"><span data-stu-id="e0879-127">Interval*</span></span> |<span data-ttu-id="e0879-128">intervalo</span><span class="sxs-lookup"><span data-stu-id="e0879-128">interval</span></span> |<span data-ttu-id="e0879-129">intervalo de saudação do hello atribuído a frequência de recorrência de saudação.</span><span class="sxs-lookup"><span data-stu-id="e0879-129">hello interval of hello given frequency for hello recurrence.</span></span> |
| <span data-ttu-id="e0879-130">Fuso horário</span><span class="sxs-lookup"><span data-stu-id="e0879-130">Time Zone</span></span> |<span data-ttu-id="e0879-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="e0879-131">timeZone</span></span> |<span data-ttu-id="e0879-132">Se uma hora de início for fornecida sem uma diferença UTC, este fuso horário será usado.</span><span class="sxs-lookup"><span data-stu-id="e0879-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="e0879-133">Hora de início</span><span class="sxs-lookup"><span data-stu-id="e0879-133">Start time</span></span> |<span data-ttu-id="e0879-134">startTime</span><span class="sxs-lookup"><span data-stu-id="e0879-134">startTime</span></span> |<span data-ttu-id="e0879-135">hora de início de saudação em [formato ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="e0879-135">hello start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="e0879-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e0879-136">Next steps</span></span>
<span data-ttu-id="e0879-137">Agora, experimente a plataforma hello e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="e0879-137">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="e0879-138">Você pode explorar Olá outros conectores disponíveis em aplicativos lógicos examinando nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="e0879-138">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

