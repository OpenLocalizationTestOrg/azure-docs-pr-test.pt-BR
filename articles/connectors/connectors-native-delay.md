---
title: "aaaAdd um atraso na lógica de aplicativos | Microsoft Docs"
description: "Visão geral da saudação atraso e o atraso-até ações e como toouse-los com um aplicativo do Azure lógica."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 915f48bf-3bd8-4656-be73-91a941d0afcd
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/18/2016
ms.author: jehollan
ms.openlocfilehash: e5bc9d639adbddc01ee0f6a4c68716f586d4344a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-delay-and-delay-until-actions"></a><span data-ttu-id="33ad3-103">Introdução ao Olá atraso e o atraso-até ações</span><span class="sxs-lookup"><span data-stu-id="33ad3-103">Get started with hello delay and delay-until actions</span></span>
<span data-ttu-id="33ad3-104">Usando o atraso de saudação e "atraso-até" ações, você pode concluir a cenários de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="33ad3-104">By using hello delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="33ad3-105">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="33ad3-105">For example, you can:</span></span>

* <span data-ttu-id="33ad3-106">Aguarde até que um dia da semana toosend um status de atualização por email.</span><span class="sxs-lookup"><span data-stu-id="33ad3-106">Wait until a weekday toosend a status update over email.</span></span>
* <span data-ttu-id="33ad3-107">Fluxo de trabalho do atraso Olá até que uma chamada HTTP tem toofinish de tempo antes de reiniciar e recuperar resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="33ad3-107">Delay hello workflow until an HTTP call has time toofinish before resuming and retrieving hello result.</span></span>

<span data-ttu-id="33ad3-108">tooget iniciado usando a ação de atraso de saudação em um aplicativo de lógica, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="33ad3-108">tooget started using hello delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-delay-actions"></a><span data-ttu-id="33ad3-109">Use as ações de atraso de saudação</span><span class="sxs-lookup"><span data-stu-id="33ad3-109">Use hello delay actions</span></span>
<span data-ttu-id="33ad3-110">Uma ação é uma operação que é executada pelo fluxo de trabalho de saudação que é definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="33ad3-110">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="33ad3-111">[Saiba mais sobre ações](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="33ad3-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="33ad3-112">Aqui está uma sequência de exemplo de como um atraso de toouse etapa em um aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="33ad3-112">Here’s an example sequence of how toouse a delay step in a logic app:</span></span>

1. <span data-ttu-id="33ad3-113">Depois de adicionar um gatilho, clique em **nova etapa** tooadd uma ação.</span><span class="sxs-lookup"><span data-stu-id="33ad3-113">After adding a trigger, click **New Step** tooadd an action.</span></span>
2. <span data-ttu-id="33ad3-114">Procurar **atraso** toobring as ações de atraso de saudação.</span><span class="sxs-lookup"><span data-stu-id="33ad3-114">Search for **delay** toobring up hello delay actions.</span></span> <span data-ttu-id="33ad3-115">Neste exemplo, escolheremos **Atrasar**.</span><span class="sxs-lookup"><span data-stu-id="33ad3-115">In this example, we will select **Delay**.</span></span>
   
    ![Ações atrasar](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="33ad3-117">Conclua qualquer atraso de Olá Olá ação propriedades tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="33ad3-117">Complete any of hello action properties tooconfigure hello delay.</span></span>
   
    ![Configuração de atraso](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="33ad3-119">Clique em **salvar** toopublish e ativar o aplicativo de lógica de saudação.</span><span class="sxs-lookup"><span data-stu-id="33ad3-119">Click **Save** toopublish and activate hello logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="33ad3-120">Detalhes da ação</span><span class="sxs-lookup"><span data-stu-id="33ad3-120">Action details</span></span>
<span data-ttu-id="33ad3-121">gatilho de recorrência Olá tem Olá seguintes propriedades que podem ser configuradas.</span><span class="sxs-lookup"><span data-stu-id="33ad3-121">hello recurrence trigger has hello following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="33ad3-122">Ação atrasar</span><span class="sxs-lookup"><span data-stu-id="33ad3-122">Delay action</span></span>
<span data-ttu-id="33ad3-123">Execute este Olá atrasos de ação para um determinado intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="33ad3-123">This action delays hello run for a certain time interval.</span></span>
<span data-ttu-id="33ad3-124">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="33ad3-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="33ad3-125">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="33ad3-125">Display name</span></span> | <span data-ttu-id="33ad3-126">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="33ad3-126">Property name</span></span> | <span data-ttu-id="33ad3-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="33ad3-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33ad3-128">Contagem*</span><span class="sxs-lookup"><span data-stu-id="33ad3-128">Count*</span></span> |<span data-ttu-id="33ad3-129">count</span><span class="sxs-lookup"><span data-stu-id="33ad3-129">count</span></span> |<span data-ttu-id="33ad3-130">número de saudação do toodelay de unidades de tempo</span><span class="sxs-lookup"><span data-stu-id="33ad3-130">hello number of time units toodelay</span></span> |
| <span data-ttu-id="33ad3-131">Unidade*</span><span class="sxs-lookup"><span data-stu-id="33ad3-131">Unit*</span></span> |<span data-ttu-id="33ad3-132">unit</span><span class="sxs-lookup"><span data-stu-id="33ad3-132">unit</span></span> |<span data-ttu-id="33ad3-133">unidade de saudação de tempo: `Second`, `Minute`, `Hour`, ou`Day`</span><span class="sxs-lookup"><span data-stu-id="33ad3-133">hello unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="33ad3-134">Ação atrasar até</span><span class="sxs-lookup"><span data-stu-id="33ad3-134">Delay-until action</span></span>
<span data-ttu-id="33ad3-135">Essa ação atrasa Olá seja executada até que uma data/hora especificada.</span><span class="sxs-lookup"><span data-stu-id="33ad3-135">This action delays hello run until a specified date/time.</span></span>
<span data-ttu-id="33ad3-136">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="33ad3-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="33ad3-137">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="33ad3-137">Display name</span></span> | <span data-ttu-id="33ad3-138">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="33ad3-138">Property name</span></span> | <span data-ttu-id="33ad3-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="33ad3-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="33ad3-140">Ano*</span><span class="sxs-lookup"><span data-stu-id="33ad3-140">Year*</span></span> |<span data-ttu-id="33ad3-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="33ad3-141">timestamp</span></span> |<span data-ttu-id="33ad3-142">Olá ano toodelay até (GMT)</span><span class="sxs-lookup"><span data-stu-id="33ad3-142">hello year toodelay until (GMT)</span></span> |
| <span data-ttu-id="33ad3-143">Mês*</span><span class="sxs-lookup"><span data-stu-id="33ad3-143">Month*</span></span> |<span data-ttu-id="33ad3-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="33ad3-144">timestamp</span></span> |<span data-ttu-id="33ad3-145">Olá mês toodelay até (GMT)</span><span class="sxs-lookup"><span data-stu-id="33ad3-145">hello month toodelay until (GMT)</span></span> |
| <span data-ttu-id="33ad3-146">Dia*</span><span class="sxs-lookup"><span data-stu-id="33ad3-146">Day*</span></span> |<span data-ttu-id="33ad3-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="33ad3-147">timestamp</span></span> |<span data-ttu-id="33ad3-148">Olá toodelay dia até (GMT)</span><span class="sxs-lookup"><span data-stu-id="33ad3-148">hello day toodelay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="33ad3-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="33ad3-149">Next steps</span></span>
<span data-ttu-id="33ad3-150">Agora, experimente a plataforma hello e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="33ad3-150">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="33ad3-151">Você pode explorar Olá outros conectores disponíveis em aplicativos lógicos examinando nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="33ad3-151">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

