---
title: "Adicionar atraso a aplicativos lógicos | Microsoft Docs"
description: "Visão geral das ações atrasar e atrasar até, e como usá-las como um aplicativo lógico do Azure."
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
ms.openlocfilehash: 5f4f7052d48b4ca4ed91212d970551141e78e852
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-delay-and-delay-until-actions"></a><span data-ttu-id="46cf0-103">Introdução às ações atrasar e atrasar até</span><span class="sxs-lookup"><span data-stu-id="46cf0-103">Get started with the delay and delay-until actions</span></span>
<span data-ttu-id="46cf0-104">Usando as ações atrasar e “atrasar até”, você pode concluir cenários de fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="46cf0-104">By using the delay and "delay-until" actions, you can complete workflow scenarios.</span></span>

<span data-ttu-id="46cf0-105">Por exemplo, você pode:</span><span class="sxs-lookup"><span data-stu-id="46cf0-105">For example, you can:</span></span>

* <span data-ttu-id="46cf0-106">Aguardar até um dia útil para enviar uma atualização de status por email.</span><span class="sxs-lookup"><span data-stu-id="46cf0-106">Wait until a weekday to send a status update over email.</span></span>
* <span data-ttu-id="46cf0-107">Atrasar o fluxo de trabalho até que uma chamada HTTP tenha tempo para ser concluída antes da retomada e da recuperação do resultado.</span><span class="sxs-lookup"><span data-stu-id="46cf0-107">Delay the workflow until an HTTP call has time to finish before resuming and retrieving the result.</span></span>

<span data-ttu-id="46cf0-108">Para começar a usar a ação atrasar em um aplicativo lógico, confira [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="46cf0-108">To get started using the delay action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-delay-actions"></a><span data-ttu-id="46cf0-109">Usar as ações atrasar</span><span class="sxs-lookup"><span data-stu-id="46cf0-109">Use the delay actions</span></span>
<span data-ttu-id="46cf0-110">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="46cf0-110">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="46cf0-111">[Saiba mais sobre ações](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="46cf0-111">[Learn more about actions](connectors-overview.md).</span></span>

<span data-ttu-id="46cf0-112">Veja uma sequência de exemplos de como usar uma etapa de atraso em um aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="46cf0-112">Here’s an example sequence of how to use a delay step in a logic app:</span></span>

1. <span data-ttu-id="46cf0-113">Depois de adicionar um gatilho, clique em **Nova Etapa** para adicionar uma ação.</span><span class="sxs-lookup"><span data-stu-id="46cf0-113">After adding a trigger, click **New Step** to add an action.</span></span>
2. <span data-ttu-id="46cf0-114">Procure por **atrasar** para exibir as ações atrasar.</span><span class="sxs-lookup"><span data-stu-id="46cf0-114">Search for **delay** to bring up the delay actions.</span></span> <span data-ttu-id="46cf0-115">Neste exemplo, escolheremos **Atrasar**.</span><span class="sxs-lookup"><span data-stu-id="46cf0-115">In this example, we will select **Delay**.</span></span>
   
    ![Ações atrasar](./media/connectors-native-delay/using-action-1.png)
3. <span data-ttu-id="46cf0-117">Preencha qualquer uma das propriedades de ação para configurar o atraso.</span><span class="sxs-lookup"><span data-stu-id="46cf0-117">Complete any of the action properties to configure the delay.</span></span>
   
    ![Configuração de atraso](./media/connectors-native-delay/using-action-2.png)
4. <span data-ttu-id="46cf0-119">Clique em **Salvar** para publicar e ativar o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="46cf0-119">Click **Save** to publish and activate the logic app.</span></span>

## <a name="action-details"></a><span data-ttu-id="46cf0-120">Detalhes da ação</span><span class="sxs-lookup"><span data-stu-id="46cf0-120">Action details</span></span>
<span data-ttu-id="46cf0-121">O gatilho de recorrência tem as propriedades a seguir que podem ser configuradas.</span><span class="sxs-lookup"><span data-stu-id="46cf0-121">The recurrence trigger has the following properties that can be configured.</span></span>

### <a name="delay-action"></a><span data-ttu-id="46cf0-122">Ação atrasar</span><span class="sxs-lookup"><span data-stu-id="46cf0-122">Delay action</span></span>
<span data-ttu-id="46cf0-123">Essa ação atrasa a execução por um determinado intervalo de tempo.</span><span class="sxs-lookup"><span data-stu-id="46cf0-123">This action delays the run for a certain time interval.</span></span>
<span data-ttu-id="46cf0-124">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="46cf0-124">A * means that it is a required field.</span></span>

| <span data-ttu-id="46cf0-125">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="46cf0-125">Display name</span></span> | <span data-ttu-id="46cf0-126">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="46cf0-126">Property name</span></span> | <span data-ttu-id="46cf0-127">Descrição</span><span class="sxs-lookup"><span data-stu-id="46cf0-127">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="46cf0-128">Contagem*</span><span class="sxs-lookup"><span data-stu-id="46cf0-128">Count*</span></span> |<span data-ttu-id="46cf0-129">count</span><span class="sxs-lookup"><span data-stu-id="46cf0-129">count</span></span> |<span data-ttu-id="46cf0-130">O número de unidades de tempo a serem atrasadas</span><span class="sxs-lookup"><span data-stu-id="46cf0-130">The number of time units to delay</span></span> |
| <span data-ttu-id="46cf0-131">Unidade*</span><span class="sxs-lookup"><span data-stu-id="46cf0-131">Unit*</span></span> |<span data-ttu-id="46cf0-132">unit</span><span class="sxs-lookup"><span data-stu-id="46cf0-132">unit</span></span> |<span data-ttu-id="46cf0-133">A unidade de tempo: `Second`, `Minute`, `Hour`, ou `Day`</span><span class="sxs-lookup"><span data-stu-id="46cf0-133">The unit of time: `Second`, `Minute`, `Hour`, or `Day`</span></span> |

<br>

### <a name="delay-until-action"></a><span data-ttu-id="46cf0-134">Ação atrasar até</span><span class="sxs-lookup"><span data-stu-id="46cf0-134">Delay-until action</span></span>
<span data-ttu-id="46cf0-135">Essa ação atrasa a execução até uma data/hora especificada.</span><span class="sxs-lookup"><span data-stu-id="46cf0-135">This action delays the run until a specified date/time.</span></span>
<span data-ttu-id="46cf0-136">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="46cf0-136">A * means that it is a required field.</span></span>

| <span data-ttu-id="46cf0-137">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="46cf0-137">Display name</span></span> | <span data-ttu-id="46cf0-138">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="46cf0-138">Property name</span></span> | <span data-ttu-id="46cf0-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="46cf0-139">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="46cf0-140">Ano*</span><span class="sxs-lookup"><span data-stu-id="46cf0-140">Year*</span></span> |<span data-ttu-id="46cf0-141">timestamp</span><span class="sxs-lookup"><span data-stu-id="46cf0-141">timestamp</span></span> |<span data-ttu-id="46cf0-142">O ano até o qual atrasar (GMT)</span><span class="sxs-lookup"><span data-stu-id="46cf0-142">The year to delay until (GMT)</span></span> |
| <span data-ttu-id="46cf0-143">Mês*</span><span class="sxs-lookup"><span data-stu-id="46cf0-143">Month*</span></span> |<span data-ttu-id="46cf0-144">timestamp</span><span class="sxs-lookup"><span data-stu-id="46cf0-144">timestamp</span></span> |<span data-ttu-id="46cf0-145">O mês até o qual atrasar (GMT)</span><span class="sxs-lookup"><span data-stu-id="46cf0-145">The month to delay until (GMT)</span></span> |
| <span data-ttu-id="46cf0-146">Dia*</span><span class="sxs-lookup"><span data-stu-id="46cf0-146">Day*</span></span> |<span data-ttu-id="46cf0-147">timestamp</span><span class="sxs-lookup"><span data-stu-id="46cf0-147">timestamp</span></span> |<span data-ttu-id="46cf0-148">O dia até o qual atrasar (GMT)</span><span class="sxs-lookup"><span data-stu-id="46cf0-148">The day to delay until (GMT)</span></span> |

<br>

## <a name="next-steps"></a><span data-ttu-id="46cf0-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="46cf0-149">Next steps</span></span>
<span data-ttu-id="46cf0-150">Agora, experimente a plataforma e [crie um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="46cf0-150">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="46cf0-151">Você pode explorar os outros conectores disponíveis em aplicativos lógicos examinando nossa [lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="46cf0-151">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

