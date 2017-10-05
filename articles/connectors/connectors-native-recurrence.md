---
title: "Adicionar o gatilho de recorrência em aplicativos lógicos | Microsoft Docs"
description: "Visão geral do gatilho de recorrência e como usá-lo com um aplicativo lógico do Azure."
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
ms.openlocfilehash: fe558958c316c8dba42163e277ae01451f712e5a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-recurrence-trigger"></a><span data-ttu-id="03eec-103">Introdução ao gatilho de recorrência</span><span class="sxs-lookup"><span data-stu-id="03eec-103">Get started with the recurrence trigger</span></span>
<span data-ttu-id="03eec-104">Usando o gatilho de recorrência, você pode criar fluxos de trabalho poderosos na nuvem.</span><span class="sxs-lookup"><span data-stu-id="03eec-104">By using the recurrence trigger, you can create powerful workflows in the cloud.</span></span>

<span data-ttu-id="03eec-105">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="03eec-105">For example, you can:</span></span>

* <span data-ttu-id="03eec-106">Agendar um fluxo de trabalho para executar um procedimento armazenado SQL todos os dias.</span><span class="sxs-lookup"><span data-stu-id="03eec-106">Schedule a workflow to run a SQL stored procedure every day.</span></span>
* <span data-ttu-id="03eec-107">Enviar por email um resumo de todos os tweets da semana passada sobre uma determinada hashtag.</span><span class="sxs-lookup"><span data-stu-id="03eec-107">Email a summary of all tweets within the last week about a certain hashtag.</span></span>

<span data-ttu-id="03eec-108">Para começar a usar o gatilho de recorrência em um aplicativo lógico, confira [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="03eec-108">To get started using the recurrence trigger in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-a-recurrence-trigger"></a><span data-ttu-id="03eec-109">Usar um gatilho de recorrência</span><span class="sxs-lookup"><span data-stu-id="03eec-109">Use a recurrence trigger</span></span>
<span data-ttu-id="03eec-110">Um gatilho é um evento que pode ser usado para iniciar o fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="03eec-110">A trigger is an event that can be used to start the workflow that is defined in a logic app.</span></span> <span data-ttu-id="03eec-111">[Saiba mais sobre gatilhos](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="03eec-111">[Learn more about triggers](connectors-overview.md).</span></span>

<span data-ttu-id="03eec-112">Veja uma sequência de exemplo de como configurar um gatilho de recorrência em um aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="03eec-112">Here’s an example sequence of how to set up a recurrence trigger in a logic app:</span></span>

1. <span data-ttu-id="03eec-113">Adicione o gatilho **Recorrência** como a primeira etapa em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="03eec-113">Add the **Recurrence** trigger as the first step in a logic app.</span></span>
2. <span data-ttu-id="03eec-114">Preencha os parâmetros para o intervalo de recorrência.</span><span class="sxs-lookup"><span data-stu-id="03eec-114">Fill in the parameters for the recurrence interval.</span></span>

<span data-ttu-id="03eec-115">O aplicativo lógico iniciará uma execução depois de cada intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="03eec-115">The logic app now starts a run after each interval of time.</span></span>

![Gatilho HTTP](./media/connectors-native-recurrence/using-trigger.png)

## <a name="trigger-details"></a><span data-ttu-id="03eec-117">Detalhes do gatilho</span><span class="sxs-lookup"><span data-stu-id="03eec-117">Trigger details</span></span>
<span data-ttu-id="03eec-118">O gatilho de recorrência tem as propriedades a seguir que você pode configurar.</span><span class="sxs-lookup"><span data-stu-id="03eec-118">The recurrence trigger has the following properties that you can configure.</span></span>

<span data-ttu-id="03eec-119">Ele dispara um aplicativo lógico depois de um intervalo de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="03eec-119">It fires a logic app after a specified time interval.</span></span>
<span data-ttu-id="03eec-120">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="03eec-120">A * means that it is a required field.</span></span>

| <span data-ttu-id="03eec-121">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="03eec-121">Display name</span></span> | <span data-ttu-id="03eec-122">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="03eec-122">Property name</span></span> | <span data-ttu-id="03eec-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="03eec-123">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="03eec-124">Frequência*</span><span class="sxs-lookup"><span data-stu-id="03eec-124">Frequency*</span></span> |<span data-ttu-id="03eec-125">frequência</span><span class="sxs-lookup"><span data-stu-id="03eec-125">frequency</span></span> |<span data-ttu-id="03eec-126">A unidade de tempo: `Second`, `Minute`, `Hour`, `Day` ou `Year`.</span><span class="sxs-lookup"><span data-stu-id="03eec-126">The unit of time: `Second`, `Minute`, `Hour`, `Day`, or `Year`.</span></span> |
| <span data-ttu-id="03eec-127">Intervalo*</span><span class="sxs-lookup"><span data-stu-id="03eec-127">Interval*</span></span> |<span data-ttu-id="03eec-128">intervalo</span><span class="sxs-lookup"><span data-stu-id="03eec-128">interval</span></span> |<span data-ttu-id="03eec-129">O intervalo da frequência determinada para a recorrência.</span><span class="sxs-lookup"><span data-stu-id="03eec-129">The interval of the given frequency for the recurrence.</span></span> |
| <span data-ttu-id="03eec-130">Fuso horário</span><span class="sxs-lookup"><span data-stu-id="03eec-130">Time Zone</span></span> |<span data-ttu-id="03eec-131">timeZone</span><span class="sxs-lookup"><span data-stu-id="03eec-131">timeZone</span></span> |<span data-ttu-id="03eec-132">Se uma hora de início for fornecida sem uma diferença UTC, este fuso horário será usado.</span><span class="sxs-lookup"><span data-stu-id="03eec-132">If a start time is provided without a UTC offset, this time zone will be used.</span></span> |
| <span data-ttu-id="03eec-133">Hora de início</span><span class="sxs-lookup"><span data-stu-id="03eec-133">Start time</span></span> |<span data-ttu-id="03eec-134">startTime</span><span class="sxs-lookup"><span data-stu-id="03eec-134">startTime</span></span> |<span data-ttu-id="03eec-135">A hora de início no [formato ISO 8601](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span><span class="sxs-lookup"><span data-stu-id="03eec-135">The start time in [ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601#Combined_date_and_time_representations).</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="03eec-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="03eec-136">Next steps</span></span>
<span data-ttu-id="03eec-137">Agora, experimente a plataforma e [crie um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="03eec-137">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="03eec-138">Você pode explorar os outros conectores disponíveis em aplicativos lógicos examinando nossa [lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="03eec-138">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

