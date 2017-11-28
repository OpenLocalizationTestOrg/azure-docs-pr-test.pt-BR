---
title: "aaaQuery para mensagens B2B no Operations Management Suite - os aplicativos lógicos do Azure | Microsoft Docs"
description: Criar consultas tootrack AS2, X12 E mensagens EDIFACT no hello Operations Management Suite
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: bb7d9432-b697-44db-aa88-bd16ddfad23f
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/21/2017
ms.author: LADocs; padmavc
ms.openlocfilehash: aee6644ff19add8f074ed5f1725db87b1d3b74b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-hello-microsoft-operations-management-suite-oms"></a><span data-ttu-id="c48eb-103">Mensagens de consulta para AS2, X12 E EDIFACT no hello Microsoft Operations Management Suite (OMS)</span><span class="sxs-lookup"><span data-stu-id="c48eb-103">Query for AS2, X12, and EDIFACT messages in hello Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="c48eb-104">Olá toofind AS2, X 12 ou mensagens EDIFACT que você está acompanhando com [Azure Log Analytics](../log-analytics/log-analytics-overview.md) em Olá [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), você pode criar consultas que filtrem ações com base em específica critérios.</span><span class="sxs-lookup"><span data-stu-id="c48eb-104">toofind hello AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="c48eb-105">Por exemplo, você pode encontrar mensagens baseado em um número de controle de intercâmbio específico.</span><span class="sxs-lookup"><span data-stu-id="c48eb-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="c48eb-106">Requisitos</span><span class="sxs-lookup"><span data-stu-id="c48eb-106">Requirements</span></span>

* <span data-ttu-id="c48eb-107">Um aplicativo lógico configurado com o log de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="c48eb-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="c48eb-108">Saiba [como toocreate um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) e [como tooset o registro em log para esse aplicativo lógica](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="c48eb-108">Learn [how toocreate a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how tooset up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="c48eb-109">Uma conta de integração configurada com o monitoramento e log.</span><span class="sxs-lookup"><span data-stu-id="c48eb-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="c48eb-110">Saiba [como uma conta de integração de toocreate](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) e [como tooset o monitoramento e registro em log para essa conta](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="c48eb-110">Learn [how toocreate an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how tooset up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="c48eb-111">Se você ainda não o fez, [publicar dados de diagnóstico tooLog análise](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) e [configurar mensagens de rastreamento no OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="c48eb-111">If you haven't already, [publish diagnostic data tooLog Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c48eb-112">Depois que você cumpriu requisitos anteriores hello, você deve ter um espaço de trabalho Olá [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="c48eb-112">After you've met hello previous requirements, you should have a workspace in hello [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="c48eb-113">Você deve usar Olá mesmo espaço de trabalho do OMS para controlar a comunicação de B2B no OMS.</span><span class="sxs-lookup"><span data-stu-id="c48eb-113">You should use hello same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="c48eb-114">Se você não tiver um espaço de trabalho do OMS, saiba [como toocreate um espaço de trabalho do OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c48eb-114">If you don't have an OMS workspace, learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-hello-operations-management-suite-portal"></a><span data-ttu-id="c48eb-115">Criar consultas de mensagem com filtros no portal do Operations Management Suite Olá</span><span class="sxs-lookup"><span data-stu-id="c48eb-115">Create message queries with filters in hello Operations Management Suite portal</span></span>

<span data-ttu-id="c48eb-116">Este exemplo mostra como você pode encontrar mensagens com base no número de controle de intercâmbio.</span><span class="sxs-lookup"><span data-stu-id="c48eb-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="c48eb-117">Se você souber o nome de espaço de trabalho do OMS, vá home page do espaço de trabalho de tooyour (`https://{your-workspace-name}.portal.mms.microsoft.com`) e iniciar na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="c48eb-117">If you know your OMS workspace name, go tooyour workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="c48eb-118">Caso contrário, comece na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="c48eb-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="c48eb-119">Em Olá [portal do Azure](https://portal.azure.com), escolha **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-119">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="c48eb-120">Pesquise “log analytics” e, em seguida, escolha **Log Analytics**, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="c48eb-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Encontrar o Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="c48eb-122">Em **Log Analytics**, encontre e selecione o espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="c48eb-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Selecionar o espaço de trabalho do OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="c48eb-124">Em **Gerenciamento**, escolha **Portal do OMS**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Escolher o portal do OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="c48eb-126">Na home page do OMS, escolha **Pesquisa de Logs**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-126">On your OMS home page, choose **Log Search**.</span></span>

   ![Na home page do OMS, escolha “Pesquisa de Logs”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="c48eb-128">-ou-</span><span class="sxs-lookup"><span data-stu-id="c48eb-128">-or-</span></span>

   ![No menu OMS do hello, escolha "Pesquisa de Log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="c48eb-130">Na caixa de pesquisa hello, insira um campo que você deseja toofind e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-130">In hello search box, enter a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="c48eb-131">Quando você começa a digitar, o OMS mostra as possíveis correspondências e operações que podem ser usadas.</span><span class="sxs-lookup"><span data-stu-id="c48eb-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="c48eb-132">Saiba mais sobre [como toofind dados na análise de Log](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="c48eb-132">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="c48eb-133">Este exemplo pesquisa eventos com **Type=AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Começar a digitar a cadeia de consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="c48eb-135">Na barra de esquerda hello, escolha Olá período de tempo que você deseja tooview.</span><span class="sxs-lookup"><span data-stu-id="c48eb-135">In hello left bar, choose hello timeframe that you want tooview.</span></span> <span data-ttu-id="c48eb-136">tooadd uma consulta de tooyour de filtro, escolha **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-136">tooadd a filter tooyour query, choose **+Add**.</span></span>

   ![Adicionar filtro tooquery](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="c48eb-138">Em **adicionar filtros**, insira o nome de filtro de saudação para que você pode encontrar o filtro de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="c48eb-138">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="c48eb-139">Selecione o filtro hello e escolha **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-139">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="c48eb-140">número de controle de intercâmbio de saudação toofind, este exemplo procura a palavra hello "intercâmbio" e seleciona **event_record_messageProperties_interchangeControlNumber_s** como filtro de saudação.</span><span class="sxs-lookup"><span data-stu-id="c48eb-140">toofind hello interchange control number, this example searches for hello word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as hello filter.</span></span>

   ![Selecionar filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="c48eb-142">Na barra de esquerda hello, selecione o valor do filtro Olá que você deseja toouse e escolha **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-142">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   <span data-ttu-id="c48eb-143">Este exemplo seleciona o número de controle de intercâmbio Olá para mensagens de saudação que desejamos.</span><span class="sxs-lookup"><span data-stu-id="c48eb-143">This example selects hello interchange control number for hello messages we want.</span></span>

   ![Selecionar o valor do filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="c48eb-145">Agora retorne toohello consulta que você está criando.</span><span class="sxs-lookup"><span data-stu-id="c48eb-145">Now return toohello query that you're building.</span></span> <span data-ttu-id="c48eb-146">A consulta foi atualizada com o evento de filtro e o valor selecionado.</span><span class="sxs-lookup"><span data-stu-id="c48eb-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="c48eb-147">Os resultados anteriores agora são filtrados também.</span><span class="sxs-lookup"><span data-stu-id="c48eb-147">Your previous results are now filtered too.</span></span>

    ![Retornar tooyour consultas com resultados filtrados](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="c48eb-149">Salvar a consulta para uso futuro</span><span class="sxs-lookup"><span data-stu-id="c48eb-149">Save your query for future use</span></span>

1. <span data-ttu-id="c48eb-150">Da consulta em Olá **pesquisa de Log** escolha **salvar**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-150">From your query on hello **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="c48eb-151">Dê um nome à consulta, selecione uma categoria e escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Dê um nome à consulta e uma categoria](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="c48eb-153">tooview sua consulta, escolha **Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-153">tooview your query, choose **Favorites**.</span></span>

   ![Escolher “Favoritos”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="c48eb-155">Em **pesquisas salvas**, selecione a consulta para que você pode exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c48eb-155">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="c48eb-156">consulta de saudação tooupdate para que você possa encontrar resultados diferentes, editar consulta hello.</span><span class="sxs-lookup"><span data-stu-id="c48eb-156">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Selecionar a consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-hello-operations-management-suite-portal"></a><span data-ttu-id="c48eb-158">Localizar e executar consultas salvas no portal do Operations Management Suite Olá</span><span class="sxs-lookup"><span data-stu-id="c48eb-158">Find and run saved queries in hello Operations Management Suite portal</span></span>

1. <span data-ttu-id="c48eb-159">Abra a home page do espaço de trabalho do OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) e escolha **Pesquisa de Logs**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![Na home page do OMS, escolha “Pesquisa de Logs”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="c48eb-161">-ou-</span><span class="sxs-lookup"><span data-stu-id="c48eb-161">-or-</span></span>

   ![No menu OMS do hello, escolha "Pesquisa de Log"](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="c48eb-163">Em Olá **pesquisa de Log** da home page, escolha **Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="c48eb-163">On hello **Log Search** home page, choose **Favorites**.</span></span>

   ![Escolher “Favoritos”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="c48eb-165">Em **pesquisas salvas**, selecione a consulta para que você pode exibir resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="c48eb-165">Under **Saved Searches**, select your query so that you can view hello results.</span></span> <span data-ttu-id="c48eb-166">consulta de saudação tooupdate para que você possa encontrar resultados diferentes, editar consulta hello.</span><span class="sxs-lookup"><span data-stu-id="c48eb-166">tooupdate hello query so you can find different results, edit hello query.</span></span>

   ![Selecionar a consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="c48eb-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c48eb-168">Next steps</span></span>

* [<span data-ttu-id="c48eb-169">Esquemas de acompanhamento de AS2</span><span class="sxs-lookup"><span data-stu-id="c48eb-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="c48eb-170">Esquemas de acompanhamento de X12</span><span class="sxs-lookup"><span data-stu-id="c48eb-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="c48eb-171">Esquemas de acompanhamento personalizado</span><span class="sxs-lookup"><span data-stu-id="c48eb-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)