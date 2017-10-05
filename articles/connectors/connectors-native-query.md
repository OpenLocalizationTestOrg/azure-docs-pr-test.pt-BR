---
title: "Adicionar a ação de consulta nos aplicativos lógicos | Microsoft Docs"
description: "Visão geral da ação de consulta para executar ações, como filtrar matriz."
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
ms.openlocfilehash: a992fa17a07d6167297c4cf5fe9fb3b58181d7df
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-the-query-action"></a><span data-ttu-id="5bc6c-103">Introdução à ação de consulta</span><span class="sxs-lookup"><span data-stu-id="5bc6c-103">Get started with the query action</span></span>
<span data-ttu-id="5bc6c-104">Usando a ação de consulta, você pode trabalhar com lotes e matrizes para executar os fluxos de trabalho para:</span><span class="sxs-lookup"><span data-stu-id="5bc6c-104">By using the query action, you can work with batches and arrays to accomplish workflows to:</span></span>

* <span data-ttu-id="5bc6c-105">Criar uma tarefa para todos os registros de alta prioridade a partir de um banco de dados.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-105">Create a task for all high-priority records from a database.</span></span>
* <span data-ttu-id="5bc6c-106">Salvar todos os anexos em PDF dos emails em um blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-106">Save all PDF attachments for emails into an Azure blob.</span></span>

<span data-ttu-id="5bc6c-107">Para começar a usar a ação de consulta em um aplicativo lógico, consulte [Criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5bc6c-107">To get started using the query action in a logic app, see [Create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span>

## <a name="use-the-query-action"></a><span data-ttu-id="5bc6c-108">Usar a ação de consulta</span><span class="sxs-lookup"><span data-stu-id="5bc6c-108">Use the query action</span></span>
<span data-ttu-id="5bc6c-109">Uma ação é uma operação executada pelo fluxo de trabalho definido em um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-109">An action is an operation that is carried out by the workflow that is defined in a logic app.</span></span> <span data-ttu-id="5bc6c-110">[Saiba mais sobre ações](connectors-overview.md).</span><span class="sxs-lookup"><span data-stu-id="5bc6c-110">[Learn more about actions](connectors-overview.md).</span></span>  

<span data-ttu-id="5bc6c-111">Atualmente, a ação de consulta tem uma operação, chamada matriz de filtro, que é exposta no designer.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-111">The query action currently has one operation, called the filter array, that is exposed in the designer.</span></span> <span data-ttu-id="5bc6c-112">Isso permite que você consulte uma matriz e retorne um conjunto de resultados filtrados.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-112">This allows you to query an array and return a set of filtered results.</span></span>

<span data-ttu-id="5bc6c-113">Veja como é possível adicioná-lo em um aplicativo lógico:</span><span class="sxs-lookup"><span data-stu-id="5bc6c-113">Here's how you can add it in a logic app:</span></span>

1. <span data-ttu-id="5bc6c-114">Selecione o botão **Nova Etapa** .</span><span class="sxs-lookup"><span data-stu-id="5bc6c-114">Select the **New Step** button.</span></span>
2. <span data-ttu-id="5bc6c-115">Escolha **Adicionar uma ação**.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-115">Choose **Add an action**.</span></span>
3. <span data-ttu-id="5bc6c-116">Na caixa de pesquisa da ação, digite **filtro** para listar a ação **Filtrar matriz**.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-116">In the action search box, type **filter** to list the **Filter array** action.</span></span>
   
    ![Selecionar a ação de consulta](./media/connectors-native-query/using-action-1.png)
4. <span data-ttu-id="5bc6c-118">Selecione uma matriz para filtrar.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-118">Select an array to filter.</span></span> <span data-ttu-id="5bc6c-119">(A captura de tela a seguir mostra a matriz de resultados de uma pesquisa do Twitter.)</span><span class="sxs-lookup"><span data-stu-id="5bc6c-119">(The following screenshot shows the array of results from a Twitter search.)</span></span>
5. <span data-ttu-id="5bc6c-120">Crie uma condição para avaliar em cada item.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-120">Create a condition to evaluate on each item.</span></span> <span data-ttu-id="5bc6c-121">(A captura de tela a seguir filtra os tweets dos usuários que têm mais de 100 seguidores.)</span><span class="sxs-lookup"><span data-stu-id="5bc6c-121">(The following screenshot filters tweets from users who have more than 100 followers.)</span></span>
   
    ![Concluir a ação de consulta](./media/connectors-native-query/using-action-2.png)
   
    <span data-ttu-id="5bc6c-123">A ação produzirá uma nova matriz que contém somente os resultados que atendem aos requisitos do filtro.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-123">The action will output a new array that contains only results that met the filter requirements.</span></span>
6. <span data-ttu-id="5bc6c-124">Clique no canto superior esquerdo da barra de ferramentas para salvar e seu aplicativo lógico será salvo e publicado (ativado).</span><span class="sxs-lookup"><span data-stu-id="5bc6c-124">Click the upper-left corner of the toolbar to save, and your logic app will both save and publish (activate).</span></span>

## <a name="query-action"></a><span data-ttu-id="5bc6c-125">Ação de consulta</span><span class="sxs-lookup"><span data-stu-id="5bc6c-125">Query action</span></span>
<span data-ttu-id="5bc6c-126">Veja os detalhes da ação com suporte deste conector.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-126">Here are the details for the action that this connector supports.</span></span> <span data-ttu-id="5bc6c-127">O conector tem uma ação possível.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-127">The connector has one possible action.</span></span>

| <span data-ttu-id="5bc6c-128">Ação</span><span class="sxs-lookup"><span data-stu-id="5bc6c-128">Action</span></span> | <span data-ttu-id="5bc6c-129">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bc6c-129">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5bc6c-130">Filtrar matriz</span><span class="sxs-lookup"><span data-stu-id="5bc6c-130">Filter array</span></span> |<span data-ttu-id="5bc6c-131">Avalia uma condição para cada item em uma matriz e retorna os resultados</span><span class="sxs-lookup"><span data-stu-id="5bc6c-131">Evaluates a condition for each item in an array and returns the results</span></span> |

## <a name="action-details"></a><span data-ttu-id="5bc6c-132">Detalhes da ação</span><span class="sxs-lookup"><span data-stu-id="5bc6c-132">Action details</span></span>
<span data-ttu-id="5bc6c-133">A ação de consulta vem com uma ação possível.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-133">The query action comes with one possible action.</span></span> <span data-ttu-id="5bc6c-134">As tabelas a seguir descrevem os campos de entrada obrigatórios e opcionais para a ação e os detalhes de saída correspondentes associados ao uso da ação.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-134">The following tables describe the required and optional input fields for the action and the corresponding output details that are associated with using the action.</span></span>

### <a name="filter-array"></a><span data-ttu-id="5bc6c-135">Filtrar matriz</span><span class="sxs-lookup"><span data-stu-id="5bc6c-135">Filter array</span></span>
<span data-ttu-id="5bc6c-136">Estes são os campos de entrada para a ação, o que cria uma solicitação HTTP de saída.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-136">The following are input fields for the action, which makes an HTTP outbound request.</span></span>
<span data-ttu-id="5bc6c-137">Um * significa que é um campo obrigatório.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-137">A * means that it is a required field.</span></span>

| <span data-ttu-id="5bc6c-138">Nome de exibição</span><span class="sxs-lookup"><span data-stu-id="5bc6c-138">Display name</span></span> | <span data-ttu-id="5bc6c-139">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="5bc6c-139">Property name</span></span> | <span data-ttu-id="5bc6c-140">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bc6c-140">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5bc6c-141">De*</span><span class="sxs-lookup"><span data-stu-id="5bc6c-141">From*</span></span> |<span data-ttu-id="5bc6c-142">de</span><span class="sxs-lookup"><span data-stu-id="5bc6c-142">from</span></span> |<span data-ttu-id="5bc6c-143">A matriz a ser filtrada</span><span class="sxs-lookup"><span data-stu-id="5bc6c-143">The array to filter</span></span> |
| <span data-ttu-id="5bc6c-144">Condição*</span><span class="sxs-lookup"><span data-stu-id="5bc6c-144">Condition*</span></span> |<span data-ttu-id="5bc6c-145">onde</span><span class="sxs-lookup"><span data-stu-id="5bc6c-145">where</span></span> |<span data-ttu-id="5bc6c-146">A condição a ser avaliada para cada item</span><span class="sxs-lookup"><span data-stu-id="5bc6c-146">The condition to evaluate for each item</span></span> |

<br>

### <a name="output-details"></a><span data-ttu-id="5bc6c-147">Detalhes de saída</span><span class="sxs-lookup"><span data-stu-id="5bc6c-147">Output details</span></span>
<span data-ttu-id="5bc6c-148">A seguir, os detalhes de saída para a resposta HTTP.</span><span class="sxs-lookup"><span data-stu-id="5bc6c-148">The following are output details for the HTTP response.</span></span>

| <span data-ttu-id="5bc6c-149">Nome da propriedade</span><span class="sxs-lookup"><span data-stu-id="5bc6c-149">Property name</span></span> | <span data-ttu-id="5bc6c-150">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="5bc6c-150">Data type</span></span> | <span data-ttu-id="5bc6c-151">Descrição</span><span class="sxs-lookup"><span data-stu-id="5bc6c-151">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="5bc6c-152">Matriz filtrada</span><span class="sxs-lookup"><span data-stu-id="5bc6c-152">Filtered array</span></span> |<span data-ttu-id="5bc6c-153">array</span><span class="sxs-lookup"><span data-stu-id="5bc6c-153">array</span></span> |<span data-ttu-id="5bc6c-154">Uma matriz que contém um objeto para cada resultado filtrado</span><span class="sxs-lookup"><span data-stu-id="5bc6c-154">An array that contains an object for each filtered result</span></span> |

## <a name="next-steps"></a><span data-ttu-id="5bc6c-155">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5bc6c-155">Next steps</span></span>
<span data-ttu-id="5bc6c-156">Agora, experimente a plataforma e [crie um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="5bc6c-156">Now, try out the platform and [create a logic app](../logic-apps/logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="5bc6c-157">Você pode explorar os outros conectores disponíveis em aplicativos lógicos examinando nossa [lista de APIs](apis-list.md).</span><span class="sxs-lookup"><span data-stu-id="5bc6c-157">You can explore the other available connectors in logic apps by looking at our [APIs list](apis-list.md).</span></span>

