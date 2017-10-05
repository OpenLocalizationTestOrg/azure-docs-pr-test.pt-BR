---
title: "Consulta de mensagens B2B no Operations Management Suite – Aplicativo Lógico do Azure | Microsoft Docs"
description: Criar consultas para acompanhar mensagens AS2, X12 e EDIFACT no Operations Management Suite
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
ms.openlocfilehash: 2748d3d3daf7c13dca05f663a4a088598e1b3605
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="query-for-as2-x12-and-edifact-messages-in-the-microsoft-operations-management-suite-oms"></a><span data-ttu-id="0b1d6-103">Consultar mensagens AS2, X12 e EDIFACT no Microsoft OMS (Operations Management Suite)</span><span class="sxs-lookup"><span data-stu-id="0b1d6-103">Query for AS2, X12, and EDIFACT messages in the Microsoft Operations Management Suite (OMS)</span></span>

<span data-ttu-id="0b1d6-104">Para encontrar as mensagens AS2, X12 e EDIFACT que você está acompanhando com o [Azure Log Analytics](../log-analytics/log-analytics-overview.md) no [OMS (Operations Management Suite)](../operations-management-suite/operations-management-suite-overview.md), crie consultas que filtram ações com base em critérios específicos.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-104">To find the AS2, X12, or EDIFACT messages that you're tracking with [Azure Log Analytics](../log-analytics/log-analytics-overview.md) in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md), you can create queries that filter actions based on specific criteria.</span></span> <span data-ttu-id="0b1d6-105">Por exemplo, você pode encontrar mensagens baseado em um número de controle de intercâmbio específico.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-105">For example, you can find messages based on a specific interchange control number.</span></span>

## <a name="requirements"></a><span data-ttu-id="0b1d6-106">Requisitos</span><span class="sxs-lookup"><span data-stu-id="0b1d6-106">Requirements</span></span>

* <span data-ttu-id="0b1d6-107">Um aplicativo lógico configurado com o log de diagnósticos.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-107">A logic app that's set up with diagnostics logging.</span></span> <span data-ttu-id="0b1d6-108">Saiba [como criar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md) e [como configurar o log para esse aplicativo lógico](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="0b1d6-108">Learn [how to create a logic app](../logic-apps/logic-apps-create-a-logic-app.md) and [how to set up logging for that logic app](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

* <span data-ttu-id="0b1d6-109">Uma conta de integração configurada com o monitoramento e log.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-109">An integration account that's set up with monitoring and logging.</span></span> <span data-ttu-id="0b1d6-110">Saiba [como criar uma conta de integração](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) e [como configurar o monitoramento e log para essa conta](../logic-apps/logic-apps-monitor-b2b-message.md).</span><span class="sxs-lookup"><span data-stu-id="0b1d6-110">Learn [how to create an integration account](../logic-apps/logic-apps-enterprise-integration-create-integration-account.md) and [how to set up monitoring and logging for that account](../logic-apps/logic-apps-monitor-b2b-message.md).</span></span>

* <span data-ttu-id="0b1d6-111">Se você ainda não fez isso, [publique dados de diagnóstico no Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) e [configure o acompanhamento de mensagens no OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span><span class="sxs-lookup"><span data-stu-id="0b1d6-111">If you haven't already, [publish diagnostic data to Log Analytics](../logic-apps/logic-apps-track-b2b-messages-omsportal.md) and [set up message tracking in OMS](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).</span></span>

> [!NOTE]
> <span data-ttu-id="0b1d6-112">Depois de atender os requisitos anteriores, você deverá ter um espaço de trabalho no [OMS (Operations Management Suite)](../operations-management-suite/operations-management-suite-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0b1d6-112">After you've met the previous requirements, you should have a workspace in the [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md).</span></span> <span data-ttu-id="0b1d6-113">Você deve usar o mesmo espaço de trabalho do OMS para acompanhar a comunicação B2B no OMS.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-113">You should use the same OMS workspace for tracking your B2B communication in OMS.</span></span> 
>  
> <span data-ttu-id="0b1d6-114">Se você não tiver um espaço de trabalho do OMS, saiba [como criar um espaço de trabalho do OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="0b1d6-114">If you don't have an OMS workspace, learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

## <a name="create-message-queries-with-filters-in-the-operations-management-suite-portal"></a><span data-ttu-id="0b1d6-115">Criar consultas de mensagens com filtros no portal do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="0b1d6-115">Create message queries with filters in the Operations Management Suite portal</span></span>

<span data-ttu-id="0b1d6-116">Este exemplo mostra como você pode encontrar mensagens com base no número de controle de intercâmbio.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-116">This example shows how you can find messages based on their interchange control number.</span></span>

> [!TIP] 
> <span data-ttu-id="0b1d6-117">Se você souber o nome do espaço de trabalho do OMS, acesse a home page do espaço de trabalho (`https://{your-workspace-name}.portal.mms.microsoft.com`) e comece na etapa 4.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-117">If you know your OMS workspace name, go to your workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and start at Step 4.</span></span> <span data-ttu-id="0b1d6-118">Caso contrário, comece na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-118">Otherwise, start at Step 1.</span></span>

1. <span data-ttu-id="0b1d6-119">No [portal do Azure](https://portal.azure.com), escolha **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-119">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="0b1d6-120">Pesquise “log analytics” e, em seguida, escolha **Log Analytics**, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="0b1d6-120">Search for "log analytics", and then choose **Log Analytics** as shown here:</span></span>

   ![Encontrar o Log Analytics](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/browseloganalytics.png)

2. <span data-ttu-id="0b1d6-122">Em **Log Analytics**, encontre e selecione o espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-122">Under **Log Analytics**, find and select your OMS workspace.</span></span>

   ![Selecionar o espaço de trabalho do OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/selectla.png)

3. <span data-ttu-id="0b1d6-124">Em **Gerenciamento**, escolha **Portal do OMS**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-124">Under **Management**, choose **OMS Portal**.</span></span>

   ![Escolher o portal do OMS](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/omsportalpage.png)

4. <span data-ttu-id="0b1d6-126">Na home page do OMS, escolha **Pesquisa de Logs**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-126">On your OMS home page, choose **Log Search**.</span></span>

   ![Na home page do OMS, escolha “Pesquisa de Logs”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="0b1d6-128">-ou-</span><span class="sxs-lookup"><span data-stu-id="0b1d6-128">-or-</span></span>

   ![No menu do OMS, escolha “Pesquisa de Logs”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

5. <span data-ttu-id="0b1d6-130">Na caixa de pesquisa, insira um campo que você deseja encontrar e, em seguida, pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-130">In the search box, enter a field that you want to find, and press **Enter**.</span></span> <span data-ttu-id="0b1d6-131">Quando você começa a digitar, o OMS mostra as possíveis correspondências e operações que podem ser usadas.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-131">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> <span data-ttu-id="0b1d6-132">Saiba mais sobre [como encontrar dados no Log Analytics](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="0b1d6-132">Learn more about [how to find data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

   <span data-ttu-id="0b1d6-133">Este exemplo pesquisa eventos com **Type=AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-133">This example searches for events with **Type=AzureDiagnostics**.</span></span>

   ![Começar a digitar a cadeia de consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-start-query.png)

6. <span data-ttu-id="0b1d6-135">Na barra à esquerda, escolha o período de tempo que você deseja exibir.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-135">In the left bar, choose the timeframe that you want to view.</span></span> <span data-ttu-id="0b1d6-136">Para adicionar um filtro à consulta, escolha **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-136">To add a filter to your query, choose **+Add**.</span></span>

   ![Adicionar um filtro à consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/query1.png)

7. <span data-ttu-id="0b1d6-138">Em **Adicionar Filtros**, insira o nome do filtro para encontrar o filtro desejado.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-138">Under **Add Filters**, enter the filter name so you can find the filter you want.</span></span> <span data-ttu-id="0b1d6-139">Selecione o filtro e escolha **+Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-139">Select the filter, and choose **+Add**.</span></span>

   <span data-ttu-id="0b1d6-140">Para encontrar o número de controle de intercâmbio, este exemplo pesquisa a palavra “intercâmbio” e seleciona **event_record_messageProperties_interchangeControlNumber_s** como o filtro.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-140">To find the interchange control number, this example searches for the word "interchange", and selects **event_record_messageProperties_interchangeControlNumber_s** as the filter.</span></span>

   ![Selecionar filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-add-filter.png)

9. <span data-ttu-id="0b1d6-142">Na barra à esquerda, selecione o valor de filtro que você deseja usar e escolha **Aplicar**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-142">In the left bar, select the filter value that you want to use, and choose **Apply**.</span></span>

   <span data-ttu-id="0b1d6-143">Este exemplo seleciona o número de controle de intercâmbio para as mensagens desejadas.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-143">This example selects the interchange control number for the messages we want.</span></span>

   ![Selecionar o valor do filtro](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-select-filter-value.png)

10. <span data-ttu-id="0b1d6-145">Agora, retorne à consulta que está sendo criada.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-145">Now return to the query that you're building.</span></span> <span data-ttu-id="0b1d6-146">A consulta foi atualizada com o evento de filtro e o valor selecionado.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-146">Your query has been updated with your selected filter event and value.</span></span> <span data-ttu-id="0b1d6-147">Os resultados anteriores agora são filtrados também.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-147">Your previous results are now filtered too.</span></span>

    ![Retornar à consulta com os resultados filtrados](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-filtered-results.png)

<a name="save-oms-query"></a>

## <a name="save-your-query-for-future-use"></a><span data-ttu-id="0b1d6-149">Salvar a consulta para uso futuro</span><span class="sxs-lookup"><span data-stu-id="0b1d6-149">Save your query for future use</span></span>

1. <span data-ttu-id="0b1d6-150">Na consulta, na página **Pesquisa de Logs**, escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-150">From your query on the **Log Search** page, choose **Save**.</span></span> <span data-ttu-id="0b1d6-151">Dê um nome à consulta, selecione uma categoria e escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-151">Give your query a name, select a category, and choose **Save**.</span></span>

   ![Dê um nome à consulta e uma categoria](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-save.png)

2. <span data-ttu-id="0b1d6-153">Para exibir a consulta, escolha **Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-153">To view your query, choose **Favorites**.</span></span>

   ![Escolher “Favoritos”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-query-favorites.png)

3. <span data-ttu-id="0b1d6-155">Em **Pesquisas Salvas**, selecione a consulta, de modo que você possa exibir os resultados.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-155">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="0b1d6-156">Para atualizar a consulta, de modo que você possa encontrar resultados diferentes, edite-a.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-156">To update the query so you can find different results, edit the query.</span></span>

   ![Selecionar a consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="find-and-run-saved-queries-in-the-operations-management-suite-portal"></a><span data-ttu-id="0b1d6-158">Encontrar e executar as consultas salvas no portal do Operations Management Suite</span><span class="sxs-lookup"><span data-stu-id="0b1d6-158">Find and run saved queries in the Operations Management Suite portal</span></span>

1. <span data-ttu-id="0b1d6-159">Abra a home page do espaço de trabalho do OMS (`https://{your-workspace-name}.portal.mms.microsoft.com`) e escolha **Pesquisa de Logs**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-159">Open your OMS workspace home page (`https://{your-workspace-name}.portal.mms.microsoft.com`), and choose **Log Search**.</span></span>

   ![Na home page do OMS, escolha “Pesquisa de Logs”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch.png)

   <span data-ttu-id="0b1d6-161">-ou-</span><span class="sxs-lookup"><span data-stu-id="0b1d6-161">-or-</span></span>

   ![No menu do OMS, escolha “Pesquisa de Logs”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/logsearch-2.png)

2. <span data-ttu-id="0b1d6-163">Na home page da **Pesquisa de Logs**, escolha **Favoritos**.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-163">On the **Log Search** home page, choose **Favorites**.</span></span>

   ![Escolher “Favoritos”](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-favorites.png)

3. <span data-ttu-id="0b1d6-165">Em **Pesquisas Salvas**, selecione a consulta, de modo que você possa exibir os resultados.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-165">Under **Saved Searches**, select your query so that you can view the results.</span></span> <span data-ttu-id="0b1d6-166">Para atualizar a consulta, de modo que você possa encontrar resultados diferentes, edite-a.</span><span class="sxs-lookup"><span data-stu-id="0b1d6-166">To update the query so you can find different results, edit the query.</span></span>

   ![Selecionar a consulta](media/logic-apps-track-b2b-messages-omsportal-query-filter-control-number/oms-log-search-find-favorites.png)

## <a name="next-steps"></a><span data-ttu-id="0b1d6-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0b1d6-168">Next steps</span></span>

* [<span data-ttu-id="0b1d6-169">Esquemas de acompanhamento de AS2</span><span class="sxs-lookup"><span data-stu-id="0b1d6-169">AS2 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)
* [<span data-ttu-id="0b1d6-170">Esquemas de acompanhamento de X12</span><span class="sxs-lookup"><span data-stu-id="0b1d6-170">X12 tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-x12-tracking-schema.md)
* [<span data-ttu-id="0b1d6-171">Esquemas de acompanhamento personalizado</span><span class="sxs-lookup"><span data-stu-id="0b1d6-171">Custom tracking schemas</span></span>](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md)