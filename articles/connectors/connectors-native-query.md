---
title: "ação de consulta Olá aaaAdd em aplicativos lógicos | Microsoft Docs"
description: "Visão geral de ação de consulta Olá para executar ações como a matriz de filtro."
services: 
documentationcenter: 
author: jeffhollan
manager: erikre
editor: 
tags: connectors
ms.assetid: 34e702c7-f9e5-4885-9266-fc7404adecfe
ms.service: logic-apps
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/20/2016
ms.author: jehollan
ms.openlocfilehash: 3d4be901e7e6bf1b644057648930667ab34f2124
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-hello-query-action"></a><span data-ttu-id="2836b-103">Introdução à ação de consulta Olá</span><span class="sxs-lookup"><span data-stu-id="2836b-103">Get started with hello query action</span></span>
<span data-ttu-id="2836b-104">Usando a ação de consulta hello, você pode trabalhar com lotes e matrizes tooaccomplish os fluxos de trabalho:</span><span class="sxs-lookup"><span data-stu-id="2836b-104">By using hello query action, you can work with batches and arrays tooaccomplish workflows to:</span></span>

* <span data-ttu-id="2836b-105">Criar uma tarefa para todos os registros de alta prioridade a partir de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="2836b-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="2836b-106">Salvar todos os anexos em PDF dos emails em um blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="2836b-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="2836b-107">tooget iniciado usando a ação de consulta de saudação em um aplicativo de lógica, consulte [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2836b-107">tooget started using hello query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-hello-query-action"></a><span data-ttu-id="2836b-108">Use a ação de consulta de saudação</span><span class="sxs-lookup"><span data-stu-id="2836b-108">Use hello query action</span></span>
<span data-ttu-id="2836b-109">Uma ação é uma operação que é executada pelo fluxo de trabalho de saudação que é definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="2836b-109">An action is an operation that is carried out by hello workflow that is defined in a logic app.</span></span> <span data-ttu-id="2836b-110">[Saiba mais sobre ações](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="2836b-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="2836b-111">ação de consulta Olá atualmente tem uma operação, chamada de matriz de filtro hello, que é exposta no designer de saudação.</span><span class="sxs-lookup"><span data-stu-id="2836b-111">hello query action currently has one operation, called hello filter array, that is exposed in hello designer.</span></span> <span data-ttu-id="2836b-112">Isso permite que você tooquery uma matriz e retornar um conjunto de resultados filtrados.</span><span class="sxs-lookup"><span data-stu-id="2836b-112">This allows you tooquery an array and return a set of filtered results.</span></span>

<span data-ttu-id="2836b-113">Veja como é possível adicioná-lo em um aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="2836b-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="2836b-114">Selecione Olá **nova etapa** botão.</span><span class="sxs-lookup"><span data-stu-id="2836b-114">Select hello **New Step** button.</span></span>
2. <span data-ttu-id="2836b-115">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="2836b-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="2836b-116">Na caixa de pesquisa de ação hello, digite **filtro** Olá toolist **matriz de filtro** ação.</span><span class="sxs-lookup"><span data-stu-id="2836b-116">In hello action search box, type **filter** toolist hello **Filter array** action.</span></span>
   
    ![Selecionar ação de consulta Olá](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="2836b-118">Selecione um toofilter de matriz.</span><span class="sxs-lookup"><span data-stu-id="2836b-118">Select an array toofilter.</span></span> <span data-ttu-id="2836b-119">(hello seguinte captura de tela mostra Olá matriz de resultados de uma pesquisa do Twitter.)</span><span class="sxs-lookup"><span data-stu-id="2836b-119">(hello following screenshot shows hello array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="2836b-120">Crie uma condição tooevaluate em cada item.</span><span class="sxs-lookup"><span data-stu-id="2836b-120">Create a condition tooevaluate on each item.</span></span> <span data-ttu-id="2836b-121">(Olá captura de tela a seguir filtra tweets de usuários que têm mais de 100 seguidores.)</span><span class="sxs-lookup"><span data-stu-id="2836b-121">(hello following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Ação de consulta Olá concluída](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="2836b-123">ação de saudação produzirá uma nova matriz que contém somente os resultados que atendam aos requisitos de filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="2836b-123">hello action will output a new array that contains only results that met hello filter requirements.</span></span>
6. <span data-ttu-id="2836b-124">Clique o canto superior esquerdo de saudação de saudação da barra de ferramentas toosave e sua lógica aplicativo salvará os dois e publicar (Ativar).</span><span class="sxs-lookup"><span data-stu-id="2836b-124">Click hello upper-left corner of hello toolbar toosave, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="2836b-125">Ação de consulta</span><span class="sxs-lookup"><span data-stu-id="2836b-125">Query action</span></span>
<span data-ttu-id="2836b-126">Aqui estão os detalhes de saudação para ação Olá que oferece suporte a esse conector.</span><span class="sxs-lookup"><span data-stu-id="2836b-126">Here are hello details for hello action that this connector supports.</span></span> <span data-ttu-id="2836b-127">conector de saudação tem uma ação possível.</span><span class="sxs-lookup"><span data-stu-id="2836b-127">hello connector has one possible action.</span></span>

| <span data-ttu-id="2836b-128">Ação</span><span class="sxs-lookup"><span data-stu-id="2836b-128">Action</span></span> | <span data-ttu-id="2836b-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="2836b-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2836b-130">Filtrar matriz</span><span class="sxs-lookup"><span data-stu-id="2836b-130">Filter array</span></span> |<span data-ttu-id="2836b-131">Avalia uma condição para cada item em uma matriz e retorna resultados Olá</span><span class="sxs-lookup"><span data-stu-id="2836b-131">Evaluates a condition for each item in an array and returns hello results</span></span> |

## <a name="action-details"></a><span data-ttu-id="2836b-132">Detalhes da ação</span><span class="sxs-lookup"><span data-stu-id="2836b-132">Action details</span></span>
<span data-ttu-id="2836b-133">ação de consulta Olá vem com uma ação possível.</span><span class="sxs-lookup"><span data-stu-id="2836b-133">hello query action comes with one possible action.</span></span> <span data-ttu-id="2836b-134">Olá tabelas a seguir descrevem hello necessárias e os campos de entrada opcionais para ação hello e Olá correspondente saída detalhes associados usando a ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="2836b-134">hello following tables describe hello required and optional input fields for hello action and hello corresponding output details that are associated with using hello action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="2836b-135">Filtrar matriz</span><span class="sxs-lookup"><span data-stu-id="2836b-135">Filter array</span></span>
<span data-ttu-id="2836b-136">Olá seguem campos de entrada para a ação de saudação, que faz uma solicitação HTTP de saída.</span><span class="sxs-lookup"><span data-stu-id="2836b-136">hello following are input fields for hello action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="2836b-137">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="2836b-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="2836b-138">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="2836b-138">Display name</span></span> | <span data-ttu-id="2836b-139">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="2836b-139">Property name</span></span> | <span data-ttu-id="2836b-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="2836b-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2836b-141">De*</span><span class="sxs-lookup"><span data-stu-id="2836b-141">From*</span></span> |<span data-ttu-id="2836b-142">Da</span><span class="sxs-lookup"><span data-stu-id="2836b-142">from</span></span> |<span data-ttu-id="2836b-143">Olá matriz toofilter</span><span class="sxs-lookup"><span data-stu-id="2836b-143">hello array toofilter</span></span> |
| <span data-ttu-id="2836b-144">Condição*</span><span class="sxs-lookup"><span data-stu-id="2836b-144">Condition*</span></span> |<span data-ttu-id="2836b-145">onde</span><span class="sxs-lookup"><span data-stu-id="2836b-145">where</span></span> |<span data-ttu-id="2836b-146">Olá tooevaluate condição para cada item</span><span class="sxs-lookup"><span data-stu-id="2836b-146">hello condition tooevaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="2836b-147">Detalhes de saída</span><span class="sxs-lookup"><span data-stu-id="2836b-147">Output details</span></span>
<span data-ttu-id="2836b-148">Olá seguem detalhes de saída de hello resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="2836b-148">hello following are output details for hello HTTP response.</span></span>

| <span data-ttu-id="2836b-149">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="2836b-149">Property name</span></span> | <span data-ttu-id="2836b-150">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="2836b-150">Data type</span></span> | <span data-ttu-id="2836b-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="2836b-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="2836b-152">Matriz filtrada</span><span class="sxs-lookup"><span data-stu-id="2836b-152">Filtered array</span></span> |<span data-ttu-id="2836b-153">array</span><span class="sxs-lookup"><span data-stu-id="2836b-153">array</span></span> |<span data-ttu-id="2836b-154">Uma matriz que contém um objeto para cada resultado filtrado</span><span class="sxs-lookup"><span data-stu-id="2836b-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="2836b-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2836b-155">Next steps</span></span>
<span data-ttu-id="2836b-156">Agora, experimente a plataforma hello e [criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="2836b-156">Now, try out hello platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="2836b-157">Você pode explorar Olá outros conectores disponíveis em aplicativos lógicos examinando nosso [lista APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="2836b-157">You can explore hello other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

