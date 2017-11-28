---
title: "status de aaaCheck, configurar o log e receber alertas - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Monitorar o status e o desempenho de aplicativos lógicos, registrar dados de diagnóstico e configurar alertas"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 5c1b1e15-3b6c-49dc-98a6-bdbe7cb75339
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 07/21/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 81f186e11a669b710f4c06089597eb5a76f7a44e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-status-set-up-diagnostics-logging-and-turn-on-alerts-for-azure-logic-apps"></a><span data-ttu-id="813d0-103">Monitorar o status, configurar o log de diagnósticos e ativar alertas para os Aplicativo Lógico do Azure</span><span class="sxs-lookup"><span data-stu-id="813d0-103">Monitor status, set up diagnostics logging, and turn on alerts for Azure Logic Apps</span></span>

<span data-ttu-id="813d0-104">Depois de [criar e executar um aplicativo lógico](../logic-apps/logic-apps-create-a-logic-app.md), verifique seu histórico de execuções, histórico de gatilhos, status e desempenho.</span><span class="sxs-lookup"><span data-stu-id="813d0-104">After you [create and run a logic app](../logic-apps/logic-apps-create-a-logic-app.md), you can check its runs history, trigger history, status, and performance.</span></span> <span data-ttu-id="813d0-105">Para monitoramento de eventos em tempo real e depuração mais avançada, configure o [log de diagnósticos](#azure-diagnostics) do aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="813d0-105">For real-time event monitoring and richer debugging, set up [diagnostics logging](#azure-diagnostics) for your logic app.</span></span> <span data-ttu-id="813d0-106">Dessa forma, você poderá [encontrar e exibir eventos](#find-events), como eventos de gatilho, eventos de execução e eventos de ação.</span><span class="sxs-lookup"><span data-stu-id="813d0-106">That way, you can [find and view events](#find-events), like trigger events, run events, and action events.</span></span> <span data-ttu-id="813d0-107">Use também esses [dados de diagnóstico com outros serviços](#extend-diagnostic-data), como o Armazenamento do Azure e os Hubs de Eventos do Azure.</span><span class="sxs-lookup"><span data-stu-id="813d0-107">You can also use this [diagnostics data with other services](#extend-diagnostic-data), like Azure Storage and Azure Event Hubs.</span></span> 

<span data-ttu-id="813d0-108">notificações de tooget sobre falhas ou outros problemas possíveis, configurar [alertas](#add-azure-alerts).</span><span class="sxs-lookup"><span data-stu-id="813d0-108">tooget notifications about failures or other possible problems, set up [alerts](#add-azure-alerts).</span></span> <span data-ttu-id="813d0-109">Por exemplo, você pode criar um alerta que detecta “quando mais de cinco execuções falham em uma hora”.</span><span class="sxs-lookup"><span data-stu-id="813d0-109">For example, you can create an alert that detects "when more than five runs fail in an hour."</span></span> <span data-ttu-id="813d0-110">Você também pode configurar o monitoramento, o acompanhamento e o log de forma programática usando as [propriedades e configurações de evento do Diagnóstico do Azure](#diagnostic-event-properties).</span><span class="sxs-lookup"><span data-stu-id="813d0-110">You can also set up monitoring, tracking, and logging programmatically by using [Azure Diagnostics event settings and properties](#diagnostic-event-properties).</span></span>

## <a name="view-runs-and-trigger-history-for-your-logic-app"></a><span data-ttu-id="813d0-111">Exibir execuções e disparar o histórico do aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="813d0-111">View runs and trigger history for your logic app</span></span>

1. <span data-ttu-id="813d0-112">toofind seu aplicativo lógica Olá [portal do Azure](https://portal.azure.com), em Olá menu principal do Azure, escolha **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="813d0-112">toofind your logic app in hello [Azure portal](https://portal.azure.com), on hello main Azure menu, choose **More services**.</span></span> <span data-ttu-id="813d0-113">Na caixa de pesquisa hello, localizar "aplicativos lógicos" e escolha **aplicativos lógicos**.</span><span class="sxs-lookup"><span data-stu-id="813d0-113">In hello search box, find "logic apps", and choose **Logic apps**.</span></span>

   ![Encontrar o aplicativo lógico](./media/logic-apps-monitor-your-logic-apps/find-your-logic-app.png)

   <span data-ttu-id="813d0-115">Olá portal do Azure mostra todos os aplicativos de lógica de saudação que estão associados a sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="813d0-115">hello Azure portal shows all hello logic apps that are associated with your Azure subscription.</span></span> 

2. <span data-ttu-id="813d0-116">Selecione o aplicativo lógico e, em seguida, escolha **Visão geral**.</span><span class="sxs-lookup"><span data-stu-id="813d0-116">Select your logic app, then choose **Overview**.</span></span>

   <span data-ttu-id="813d0-117">Olá portal do Azure mostra Olá execuções de histórico e o histórico de gatilho para seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="813d0-117">hello Azure portal shows hello runs history and trigger history for your logic app.</span></span> <span data-ttu-id="813d0-118">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="813d0-118">For example:</span></span>

   ![Histórico de execuções e histórico de gatilhos do aplicativo lógico](media/logic-apps-monitor-your-logic-apps/overview.png)

   * <span data-ttu-id="813d0-120">**Executa o histórico** mostra todas as execuções de saudação para seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="813d0-120">**Runs history** shows all hello runs for your logic app.</span></span> 
   * <span data-ttu-id="813d0-121">**Disparar histórico** mostra todas as atividades de gatilho Olá para seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="813d0-121">**Trigger History** shows all hello trigger activity for your logic app.</span></span>

   <span data-ttu-id="813d0-122">Para obter descrições de status, consulte [Solução de problemas do aplicativo lógico](../logic-apps/logic-apps-diagnosing-failures.md).</span><span class="sxs-lookup"><span data-stu-id="813d0-122">For status descriptions, see [Troubleshoot your logic app](../logic-apps/logic-apps-diagnosing-failures.md).</span></span>

   > [!TIP]
   > <span data-ttu-id="813d0-123">Se você não encontrar dados Olá que você espera que, na barra de ferramentas hello, escolha **atualizar**.</span><span class="sxs-lookup"><span data-stu-id="813d0-123">If you don't find hello data that you expect, on hello toolbar, choose **Refresh**.</span></span>

3. <span data-ttu-id="813d0-124">Olá tooview as etapas de uma execução específica, em **executa histórico**, selecione que são executados.</span><span class="sxs-lookup"><span data-stu-id="813d0-124">tooview hello steps from a specific run, under **Runs history**, select that run.</span></span> 

   <span data-ttu-id="813d0-125">modo de exibição de monitor de saudação mostra cada etapa em que são executados.</span><span class="sxs-lookup"><span data-stu-id="813d0-125">hello monitor view shows each step in that run.</span></span> <span data-ttu-id="813d0-126">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="813d0-126">For example:</span></span>

   ![Ações de uma execução específica](media/logic-apps-monitor-your-logic-apps/monitor-view-updated.png)

4. <span data-ttu-id="813d0-128">tooget mais detalhes sobre Olá executar, escolha **detalhes da execução**.</span><span class="sxs-lookup"><span data-stu-id="813d0-128">tooget more details about hello run, choose **Run Details**.</span></span> <span data-ttu-id="813d0-129">Essas informações resumem as etapas de hello, status, entradas e saídas para Olá executar.</span><span class="sxs-lookup"><span data-stu-id="813d0-129">This information summarizes hello steps, status, inputs, and outputs for hello run.</span></span> 

   ![Escolher “Detalhes da Execução”](media/logic-apps-monitor-your-logic-apps/run-details.png)

   <span data-ttu-id="813d0-131">Por exemplo, você pode obter Olá execução **ID de correlação**, que podem ser úteis quando você usar o hello [API REST para aplicativos lógicos](https://docs.microsoft.com/rest/api/logic).</span><span class="sxs-lookup"><span data-stu-id="813d0-131">For example, you can get hello run's **Correlation ID**, which you might need when you use hello [REST API for Logic Apps](https://docs.microsoft.com/rest/api/logic).</span></span>

5. <span data-ttu-id="813d0-132">tooget detalhes sobre uma etapa específica, escolha essa etapa.</span><span class="sxs-lookup"><span data-stu-id="813d0-132">tooget details about a specific step, choose that step.</span></span> <span data-ttu-id="813d0-133">Agora você pode examinar detalhes como entradas, saídas e todos os erros que ocorreram nessa etapa.</span><span class="sxs-lookup"><span data-stu-id="813d0-133">You can now review details like inputs, outputs, and any errors that happened for that step.</span></span> <span data-ttu-id="813d0-134">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="813d0-134">For example:</span></span>

   ![Detalhes da etapa](media/logic-apps-monitor-your-logic-apps/monitor-view-details.png)
   
   > [!NOTE]
   > <span data-ttu-id="813d0-136">Todos os detalhes de tempo de execução e eventos são criptografados no hello serviço de aplicativos lógicos.</span><span class="sxs-lookup"><span data-stu-id="813d0-136">All runtime details and events are encrypted within hello Logic Apps service.</span></span> <span data-ttu-id="813d0-137">Eles são descriptografados apenas quando um usuário solicita tooview esses dados.</span><span class="sxs-lookup"><span data-stu-id="813d0-137">They are decrypted only when a user requests tooview that data.</span></span> <span data-ttu-id="813d0-138">Você também pode controlar o acesso toothese eventos com [o Access RBAC (controle)](../active-directory/role-based-access-control-what-is.md).</span><span class="sxs-lookup"><span data-stu-id="813d0-138">You can also control access toothese events with [Azure Role-Based Access Control (RBAC)](../active-directory/role-based-access-control-what-is.md).</span></span>

6. <span data-ttu-id="813d0-139">tooget detalhes sobre um evento de gatilho específico, volte toohello **visão geral** painel.</span><span class="sxs-lookup"><span data-stu-id="813d0-139">tooget details about a specific trigger event, go back toohello **Overview** pane.</span></span> <span data-ttu-id="813d0-140">Em **disparar histórico**, selecione o evento de gatilho hello.</span><span class="sxs-lookup"><span data-stu-id="813d0-140">Under **Trigger history**, select hello trigger event.</span></span> <span data-ttu-id="813d0-141">Agora você pode examinar detalhes como entradas e saídas, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="813d0-141">You can now review details like inputs and outputs, for example:</span></span>

   ![Detalhes de saída do evento de gatilho](media/logic-apps-monitor-your-logic-apps/trigger-details.png)

<a name="azure-diagnostics"></a>

## <a name="turn-on-diagnostics-logging-for-your-logic-app"></a><span data-ttu-id="813d0-143">Ativar o log de diagnósticos do aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="813d0-143">Turn on diagnostics logging for your logic app</span></span>

<span data-ttu-id="813d0-144">Para uma depuração mais avançada com eventos e detalhes de tempo de execução, configure o log de diagnósticos com o [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="813d0-144">For richer debugging with runtime details and events, you can set up diagnostics logging with [Azure Log Analytics](../log-analytics/log-analytics-overview.md).</span></span> <span data-ttu-id="813d0-145">Análise de log é um serviço em [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) que monitora a sua nuvem locais e ambientes toohelp manter sua disponibilidade e desempenho.</span><span class="sxs-lookup"><span data-stu-id="813d0-145">Log Analytics is a service in [Operations Management Suite (OMS)](../operations-management-suite/operations-management-suite-overview.md) that monitors your cloud and on-premises environments toohelp you maintain their availability and performance.</span></span> 

<span data-ttu-id="813d0-146">Antes de começar, você precisa toohave um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="813d0-146">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="813d0-147">Saiba [como toocreate um espaço de trabalho do OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="813d0-147">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span>

1. <span data-ttu-id="813d0-148">Em Olá [portal do Azure](https://portal.azure.com), localize e selecione o aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="813d0-148">In hello [Azure portal](https://portal.azure.com), find and select your logic app.</span></span> 

2. <span data-ttu-id="813d0-149">No menu de folha de aplicativo de lógica de hello, em **monitoramento**, escolha **diagnóstico** > **configurações de diagnóstico**.</span><span class="sxs-lookup"><span data-stu-id="813d0-149">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Diagnostic Settings**.</span></span>

   ![Vá tooMonitoring, diagnósticos, configurações de diagnóstico](media/logic-apps-monitor-your-logic-apps/logic-app-diagnostics.png)

3. <span data-ttu-id="813d0-151">Em **Configurações de diagnóstico**, escolha **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="813d0-151">Under **Diagnostics settings**, choose **On**.</span></span>

   ![Ativar logs de diagnóstico](media/logic-apps-monitor-your-logic-apps/turn-on-diagnostics-logic-app.png)

4. <span data-ttu-id="813d0-153">Agora selecione categoria de evento e o espaço de trabalho OMS de saudação para registro em log conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="813d0-153">Now select hello OMS workspace and event category for logging as shown:</span></span>

   1. <span data-ttu-id="813d0-154">Selecione **enviar tooLog análise**.</span><span class="sxs-lookup"><span data-stu-id="813d0-154">Select **Send tooLog Analytics**.</span></span> 
   2. <span data-ttu-id="813d0-155">Em **Log Analytics**, escolha **Configurar**.</span><span class="sxs-lookup"><span data-stu-id="813d0-155">Under **Log Analytics**, choose **Configure**.</span></span> 
   3. <span data-ttu-id="813d0-156">Em **espaços de trabalho do OMS**, selecione Olá toouse de espaço de trabalho do OMS para registro em log.</span><span class="sxs-lookup"><span data-stu-id="813d0-156">Under **OMS Workspaces**, select hello OMS workspace toouse for logging.</span></span>
   4. <span data-ttu-id="813d0-157">Em **Log**, selecione Olá **WorkflowRuntime** categoria.</span><span class="sxs-lookup"><span data-stu-id="813d0-157">Under **Log**, select hello **WorkflowRuntime** category.</span></span>
   5. <span data-ttu-id="813d0-158">Escolha o intervalo de métrica de saudação.</span><span class="sxs-lookup"><span data-stu-id="813d0-158">Choose hello metric interval.</span></span>
   6. <span data-ttu-id="813d0-159">Quando terminar, escolha **Salvar**.</span><span class="sxs-lookup"><span data-stu-id="813d0-159">When you're done, choose **Save**.</span></span>

   ![Selecionar o espaço de trabalho do OMS e os dados para log](media/logic-apps-monitor-your-logic-apps/send-diagnostics-data-log-analytics-workspace.png)

<span data-ttu-id="813d0-161">Agora, você pode encontrar eventos e outros dados para eventos de gatilho, eventos de execução e eventos de ação.</span><span class="sxs-lookup"><span data-stu-id="813d0-161">Now, you can find events and other data for trigger events, run events, and action events.</span></span>

<a name="find-events"></a>

## <a name="find-events-and-data-for-your-logic-app"></a><span data-ttu-id="813d0-162">Encontrar eventos e dados do aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="813d0-162">Find events and data for your logic app</span></span>

<span data-ttu-id="813d0-163">toofind e exibir eventos em seu aplicativo lógico, como eventos de gatilho, execute os eventos e eventos de ação, siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="813d0-163">toofind and view events in your logic app, like trigger events, run events, and action events, follow these steps.</span></span>

1. <span data-ttu-id="813d0-164">Em Olá [portal do Azure](https://portal.azure.com), escolha **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="813d0-164">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="813d0-165">Pesquise “log analytics” e, em seguida, escolha **Log Analytics**, conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="813d0-165">Search for "log analytics", then choose **Log Analytics** as shown here:</span></span>

   ![Escolher “Log Analytics”](media/logic-apps-monitor-your-logic-apps/browseloganalytics.png)

2. <span data-ttu-id="813d0-167">Em **Log Analytics**, encontre e selecione o espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="813d0-167">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selecionar o espaço de trabalho do OMS](media/logic-apps-monitor-your-logic-apps/selectla.png)

3. <span data-ttu-id="813d0-169">Em **Gerenciamento**, escolha **Portal do OMS**.</span><span class="sxs-lookup"><span data-stu-id="813d0-169">Under **Management**, choose **OMS Portal**.</span></span>

   ![Escolher “Portal do OMS”](media/logic-apps-monitor-your-logic-apps/omsportalpage.png)

4. <span data-ttu-id="813d0-171">Na home page do OMS, escolha **Pesquisa de Logs**.</span><span class="sxs-lookup"><span data-stu-id="813d0-171">On your OMS home page, choose **Log Search**.</span></span>

   ![Na home page do OMS, escolha “Pesquisa de Logs”](media/logic-apps-monitor-your-logic-apps/logsearch.png)

   <span data-ttu-id="813d0-173">-ou-</span><span class="sxs-lookup"><span data-stu-id="813d0-173">-or-</span></span>

   ![No menu OMS do hello, escolha "Pesquisa de Log"](media/logic-apps-monitor-your-logic-apps/logsearch-2.png)

5. <span data-ttu-id="813d0-175">Na caixa de pesquisa hello, especifique um campo que você deseja toofind e pressione **Enter**.</span><span class="sxs-lookup"><span data-stu-id="813d0-175">In hello search box, specify a field that you want toofind, and press **Enter**.</span></span> <span data-ttu-id="813d0-176">Quando você começa a digitar, o OMS mostra as possíveis correspondências e operações que podem ser usadas.</span><span class="sxs-lookup"><span data-stu-id="813d0-176">When you start typing, OMS shows you possible matches and operations that you can use.</span></span> 

   <span data-ttu-id="813d0-177">Por exemplo, os primeiros 10 eventos toofind Olá que ocorreram, digite e selecione esta consulta de pesquisa: **categoria = WorkflowRuntime | top 10**</span><span class="sxs-lookup"><span data-stu-id="813d0-177">For example, toofind hello top 10 events that happened, enter and select this search query: **Category=WorkflowRuntime |top 10**</span></span>

   ![Inserir a cadeia de pesquisa](media/logic-apps-monitor-your-logic-apps/oms-start-query.png)

   <span data-ttu-id="813d0-179">Saiba mais sobre [como toofind dados na análise de Log](../log-analytics/log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="813d0-179">Learn more about [how toofind data in Log Analytics](../log-analytics/log-analytics-log-searches.md).</span></span>

6. <span data-ttu-id="813d0-180">Na página de resultados Olá, na barra de esquerdo de Olá, escolha o período de tempo de saudação que você deseja tooview.</span><span class="sxs-lookup"><span data-stu-id="813d0-180">On hello results page, in hello left bar, choose hello timeframe that you want tooview.</span></span>
<span data-ttu-id="813d0-181">Escolha de sua consulta adicionando um filtro, toorefine **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="813d0-181">toorefine your query by adding a filter, choose **+Add**.</span></span>

   ![Escolher período de tempo para os resultados da consulta](media/logic-apps-monitor-your-logic-apps/query-results.png)

7. <span data-ttu-id="813d0-183">Em **adicionar filtros**, insira o nome de filtro de saudação para que você pode encontrar o filtro de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="813d0-183">Under **Add Filters**, enter hello filter name so you can find hello filter you want.</span></span> <span data-ttu-id="813d0-184">Selecione o filtro hello e escolha **+ adicionar**.</span><span class="sxs-lookup"><span data-stu-id="813d0-184">Select hello filter, and choose **+Add**.</span></span>

   <span data-ttu-id="813d0-185">Este exemplo usa hello word "status" toofind falha eventos em **AzureDiagnostics**.</span><span class="sxs-lookup"><span data-stu-id="813d0-185">This example uses hello word "status" toofind failed events under **AzureDiagnostics**.</span></span>
   <span data-ttu-id="813d0-186">Olá aqui o filtro para **status_s** já está selecionado.</span><span class="sxs-lookup"><span data-stu-id="813d0-186">Here hello filter for **status_s** is already selected.</span></span>

   ![Selecionar filtro](media/logic-apps-monitor-your-logic-apps/log-search-add-filter.png)

8. <span data-ttu-id="813d0-188">Na barra de esquerda hello, selecione o valor do filtro Olá que você deseja toouse e escolha **aplicar**.</span><span class="sxs-lookup"><span data-stu-id="813d0-188">In hello left bar, select hello filter value that you want toouse, and choose **Apply**.</span></span>

   ![Selecionar valor de filtro e escolher “Aplicar”](media/logic-apps-monitor-your-logic-apps/log-search-apply-filter.png)

9. <span data-ttu-id="813d0-190">Agora retorne toohello consulta que você está criando.</span><span class="sxs-lookup"><span data-stu-id="813d0-190">Now return toohello query that you're building.</span></span> <span data-ttu-id="813d0-191">A consulta é atualizada com o filtro e o valor selecionados.</span><span class="sxs-lookup"><span data-stu-id="813d0-191">Your query is updated with your selected filter and value.</span></span> <span data-ttu-id="813d0-192">Os resultados anteriores agora são filtrados também.</span><span class="sxs-lookup"><span data-stu-id="813d0-192">Your previous results are now filtered too.</span></span>

   ![Retornar tooyour consultas com resultados filtrados](media/logic-apps-monitor-your-logic-apps/log-search-query-filtered-results.png)

10. <span data-ttu-id="813d0-194">Escolha de sua consulta para uso futuro, toosave **salvar**.</span><span class="sxs-lookup"><span data-stu-id="813d0-194">toosave your query for future use, choose **Save**.</span></span> <span data-ttu-id="813d0-195">Saiba [como toosave sua consulta](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span><span class="sxs-lookup"><span data-stu-id="813d0-195">Learn [how toosave your query](../logic-apps/logic-apps-track-b2b-messages-omsportal-query-filter-control-number.md#save-oms-query).</span></span>

<a name="extend-diagnostic-data"></a>

## <a name="extend-how-and-where-you-use-diagnostic-data-with-other-services"></a><span data-ttu-id="813d0-196">Estender como e onde usar os dados de diagnóstico com outros serviços</span><span class="sxs-lookup"><span data-stu-id="813d0-196">Extend how and where you use diagnostic data with other services</span></span>

<span data-ttu-id="813d0-197">Junto com o Azure Log Analytics, você pode estender a maneira de usar os dados de diagnóstico do aplicativo lógico com outros serviços do Azure, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="813d0-197">Along with Azure Log Analytics, you can extend how you use your logic app's diagnostic data with other Azure services, for example:</span></span> 

* [<span data-ttu-id="813d0-198">Arquivar logs do Diagnóstico do Azure no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="813d0-198">Archive Azure Diagnostics Logs in Azure Storage</span></span>](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md)
* [<span data-ttu-id="813d0-199">Fluxo de Logs de diagnóstico do Azure tooAzure Hubs de eventos</span><span class="sxs-lookup"><span data-stu-id="813d0-199">Stream Azure Diagnostics Logs tooAzure Event Hubs</span></span>](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md) 

<span data-ttu-id="813d0-200">Depois, obtenha o monitoramento em tempo real usando a telemetria e a análise de outros serviços, como o [Stream Analytics do Azure](../stream-analytics/stream-analytics-introduction.md) e o [Power BI](../log-analytics/log-analytics-powerbi.md).</span><span class="sxs-lookup"><span data-stu-id="813d0-200">You can then get real-time monitoring by using telemetry and analytics from other services, like [Azure Stream Analytics](../stream-analytics/stream-analytics-introduction.md) and [Power BI](../log-analytics/log-analytics-powerbi.md).</span></span> <span data-ttu-id="813d0-201">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="813d0-201">For example:</span></span>

* [<span data-ttu-id="813d0-202">Dados de fluxo de Hubs de eventos tooStream análise</span><span class="sxs-lookup"><span data-stu-id="813d0-202">Stream data from Event Hubs tooStream Analytics</span></span>](../stream-analytics/stream-analytics-define-inputs.md)
* [<span data-ttu-id="813d0-203">Analisar dados de streaming com o Stream Analytics e criar um painel de análise em tempo real no Power BI</span><span class="sxs-lookup"><span data-stu-id="813d0-203">Analyze streaming data with Stream Analytics and create a real-time analytics dashboard in Power BI</span></span>](../stream-analytics/stream-analytics-power-bi-dashboard.md)

<span data-ttu-id="813d0-204">Com base nas opções de saudação que você deseja configurar, certifique-se de que você primeiro [criar uma conta de armazenamento do Azure](../storage/common/storage-create-storage-account.md) ou [criar um hub de eventos do Azure](../event-hubs/event-hubs-create.md).</span><span class="sxs-lookup"><span data-stu-id="813d0-204">Based on hello options that you want set up, make sure that you first [create an Azure storage account](../storage/common/storage-create-storage-account.md) or [create an Azure event hub](../event-hubs/event-hubs-create.md).</span></span> <span data-ttu-id="813d0-205">Selecione as opções de saudação para onde você deseja que os dados de diagnóstico toosend:</span><span class="sxs-lookup"><span data-stu-id="813d0-205">Then select hello options for where you want toosend diagnostic data:</span></span>

![Enviar dados tooAzure armazenamento conta ou evento de hub](./media/logic-apps-monitor-your-logic-apps/storage-account-event-hubs.png)

> [!NOTE]
> <span data-ttu-id="813d0-207">Períodos de retenção se aplicam somente quando você escolher toouse uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="813d0-207">Retention periods apply only when you choose toouse a storage account.</span></span>

<a name="add-azure-alerts"></a>

## <a name="set-up-alerts-for-your-logic-app"></a><span data-ttu-id="813d0-208">Configurar alertas para o aplicativo lógico</span><span class="sxs-lookup"><span data-stu-id="813d0-208">Set up alerts for your logic app</span></span>

<span data-ttu-id="813d0-209">limites excedidos para o aplicativo lógico, ou métricas específicas toomonitor configurar [alertas no Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="813d0-209">toomonitor specific metrics or exceeded thresholds for your logic app, set up [alerts in Azure](../monitoring-and-diagnostics/monitoring-overview-alerts.md).</span></span> <span data-ttu-id="813d0-210">Saiba mais sobre as [métricas no Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span><span class="sxs-lookup"><span data-stu-id="813d0-210">Learn about [metrics in Azure](../monitoring-and-diagnostics/monitoring-overview-metrics.md).</span></span> 

<span data-ttu-id="813d0-211">tooset alertas sem [Azure Log Analytics](../log-analytics/log-analytics-overview.md), siga estas etapas.</span><span class="sxs-lookup"><span data-stu-id="813d0-211">tooset up alerts without [Azure Log Analytics](../log-analytics/log-analytics-overview.md), follow these steps.</span></span> <span data-ttu-id="813d0-212">Para obter critérios mais avançados de alertas e de ações, [configure o Log Analytics](#azure-diagnostics) também.</span><span class="sxs-lookup"><span data-stu-id="813d0-212">For more advanced alerts criteria and actions, [set up Log Analytics](#azure-diagnostics) too.</span></span>

1. <span data-ttu-id="813d0-213">No menu de folha de aplicativo de lógica de hello, em **monitoramento**, escolha **diagnóstico** > **regras de alerta** > **adicionar alerta**conforme mostrado aqui:</span><span class="sxs-lookup"><span data-stu-id="813d0-213">On hello logic app blade menu, under **Monitoring**, choose **Diagnostics** > **Alert rules** > **Add alert** as shown here:</span></span>

   ![Adicionar um alerta ao aplicativo lógico](media/logic-apps-monitor-your-logic-apps/set-up-alerts.png)

2. <span data-ttu-id="813d0-215">Em Olá **adicionar uma regra de alerta** folha, criar o alerta, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="813d0-215">On hello **Add an alert rule** blade, create your alert as shown:</span></span>

   1. <span data-ttu-id="813d0-216">Em **Recurso**, selecione o aplicativo lógico, caso ainda não esteja selecionado.</span><span class="sxs-lookup"><span data-stu-id="813d0-216">Under **Resource**, select your logic app, if not already selected.</span></span> 
   2. <span data-ttu-id="813d0-217">Dê um nome e uma descrição para o alerta.</span><span class="sxs-lookup"><span data-stu-id="813d0-217">Give a name and description for your alert.</span></span>
   3. <span data-ttu-id="813d0-218">Selecione um **métrica** ou eventos que você deseja tootrack.</span><span class="sxs-lookup"><span data-stu-id="813d0-218">Select a **Metric** or event that you want tootrack.</span></span>
   4. <span data-ttu-id="813d0-219">Selecione um **condição**, especifique um **limite** para métrica hello e selecione Olá **período** para esta métrica de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="813d0-219">Select a **Condition**, specify a **Threshold** for hello metric, and select hello **Period** for monitoring this metric.</span></span>
   5. <span data-ttu-id="813d0-220">Selecione se toosend de email de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="813d0-220">Select whether toosend mail for hello alert.</span></span> 
   6. <span data-ttu-id="813d0-221">Especifique qualquer outro endereço de email para enviar o alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="813d0-221">Specify any other email addresses for sending hello alert.</span></span> 
   <span data-ttu-id="813d0-222">Você também pode especificar uma URL de webhook onde você deseja que o alerta de saudação toosend.</span><span class="sxs-lookup"><span data-stu-id="813d0-222">You can also specify a webhook URL where you want toosend hello alert.</span></span>

   <span data-ttu-id="813d0-223">Por exemplo, essa regra envia um alerta quando cinco ou mais execuções falham em uma hora:</span><span class="sxs-lookup"><span data-stu-id="813d0-223">For example, this rule sends an alert when five or more runs fail in an hour:</span></span>

   ![Criar uma regra de alerta de métrica](media/logic-apps-monitor-your-logic-apps/create-alert-rule.png)

> [!TIP]
> <span data-ttu-id="813d0-225">toorun um aplicativo lógico de um alerta, você pode incluir Olá [gatilho solicitação](../connectors/connectors-native-reqres.md) no fluxo de trabalho, que permite que você execute tarefas como estes exemplos:</span><span class="sxs-lookup"><span data-stu-id="813d0-225">toorun a logic app from an alert, you can include hello [request trigger](../connectors/connectors-native-reqres.md) in your workflow, which lets you perform tasks like these examples:</span></span>
> 
> * [<span data-ttu-id="813d0-226">Lançar tooSlack</span><span class="sxs-lookup"><span data-stu-id="813d0-226">Post tooSlack</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app)
> * [<span data-ttu-id="813d0-227">Enviar um texto</span><span class="sxs-lookup"><span data-stu-id="813d0-227">Send a text</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app)
> * [<span data-ttu-id="813d0-228">Adicionar uma fila de mensagens tooa</span><span class="sxs-lookup"><span data-stu-id="813d0-228">Add a message tooa queue</span></span>](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app)

<a name="diagnostic-event-properties"></a>

## <a name="azure-diagnostics-event-settings-and-details"></a><span data-ttu-id="813d0-229">Configurações e detalhes de eventos do Diagnóstico do Azure</span><span class="sxs-lookup"><span data-stu-id="813d0-229">Azure Diagnostics event settings and details</span></span>

<span data-ttu-id="813d0-230">Cada evento de diagnóstico exibe detalhes sobre a sua lógica de aplicativo e se o evento, por exemplo, status de saudação, hora de início, hora de término e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="813d0-230">Each diagnostic event has details about your logic app and that event, for example, hello status, start time, end time, and so on.</span></span> <span data-ttu-id="813d0-231">tooprogrammatically configurar o monitoramento, rastreamento e registro em log, ou pode usar esses detalhes com hello [API REST para aplicativos do Azure lógica](https://docs.microsoft.com/rest/api/logic) e hello [API REST para diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span><span class="sxs-lookup"><span data-stu-id="813d0-231">tooprogrammatically set up monitoring, tracking, and logging, ou can use these details with hello [REST API for Azure Logic Apps](https://docs.microsoft.com/rest/api/logic) and hello [REST API for Azure Diagnostics](../monitoring-and-diagnostics/monitoring-supported-metrics.md#microsoftlogicworkflows).</span></span>

<span data-ttu-id="813d0-232">Por exemplo, Olá `ActionCompleted` evento tem Olá `clientTrackingId` e `trackedProperties` propriedades que você pode usar para controlar e monitorar:</span><span class="sxs-lookup"><span data-stu-id="813d0-232">For example, hello `ActionCompleted` event has hello `clientTrackingId` and `trackedProperties` properties that you can use for tracking and monitoring:</span></span>

``` json
{
    "time": "2016-07-09T17:09:54.4773148Z",
    "workflowId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP",
    "resourceId": "/SUBSCRIPTIONS/<subscription-ID>/RESOURCEGROUPS/MYRESOURCEGROUP/PROVIDERS/MICROSOFT.LOGIC/WORKFLOWS/MYLOGICAPP/RUNS/08587361146922712057/ACTIONS/HTTP",
    "category": "WorkflowRuntime",
    "level": "Information",
    "operationName": "Microsoft.Logic/workflows/workflowActionCompleted",
    "properties": {
        "$schema": "2016-06-01",
        "startTime": "2016-07-09T17:09:53.4336305Z",
        "endTime": "2016-07-09T17:09:53.5430281Z",
        "status": "Succeeded",
        "code": "OK",
        "resource": {
            "subscriptionId": "<subscription-ID>",
            "resourceGroupName": "MyResourceGroup",
            "workflowId": "cff00d5458f944d5a766f2f9ad142553",
            "workflowName": "MyLogicApp",
            "runId": "08587361146922712057",
            "location": "westus",
            "actionName": "Http"
        },
        "correlation": {
            "actionTrackingId": "e1931543-906d-4d1d-baed-dee72ddf1047",
            "clientTrackingId": "<my-custom-tracking-ID>"
        },
        "trackedProperties": {
            "myTrackedProperty": "<value>"
        }
    }
}
```

* <span data-ttu-id="813d0-233">`clientTrackingId`: Se não for fornecido, o Azure gera essa ID e correlaciona eventos em um aplicativo lógico executado automaticamente, incluindo quaisquer fluxos de trabalho aninhados que são chamados de aplicativo lógico de saudação.</span><span class="sxs-lookup"><span data-stu-id="813d0-233">`clientTrackingId`: If not provided, Azure automatically generates this ID and correlates events across a logic app run, including any nested workflows that are called from hello logic app.</span></span> <span data-ttu-id="813d0-234">Você pode especificar manualmente essa ID de um disparador, passando um `x-ms-client-tracking-id` cabeçalho com o valor de ID personalizado na solicitação de gatilho hello.</span><span class="sxs-lookup"><span data-stu-id="813d0-234">You can manually specify this ID from a trigger by passing a `x-ms-client-tracking-id` header with your custom ID value in hello trigger request.</span></span> <span data-ttu-id="813d0-235">Use um gatilho de solicitação, gatilho HTTP ou gatilho de webhook.</span><span class="sxs-lookup"><span data-stu-id="813d0-235">You can use a request trigger, HTTP trigger, or webhook trigger.</span></span>

* <span data-ttu-id="813d0-236">`trackedProperties`: tootrack entradas ou saídas de dados de diagnóstico, você pode adicionar propriedades rastreadas tooactions na definição de JSON da lógica do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="813d0-236">`trackedProperties`: tootrack inputs or outputs in diagnostics data, you can add tracked properties tooactions in your logic app's JSON definition.</span></span> <span data-ttu-id="813d0-237">Propriedades rastreadas podem controlar somente uma única ação entradas e saídas, mas você pode usar o hello `correlation` propriedades de eventos toocorrelate em ações em uma execução.</span><span class="sxs-lookup"><span data-stu-id="813d0-237">Tracked properties can track only a single action's inputs and outputs, but you can use hello `correlation` properties of events toocorrelate across actions in a run.</span></span>

  <span data-ttu-id="813d0-238">tootrack uma ou mais propriedades, adicionar Olá `trackedProperties` seção e hello propriedades desejadas toohello definição da ação.</span><span class="sxs-lookup"><span data-stu-id="813d0-238">tootrack one or more properties, add hello `trackedProperties` section and hello properties you want toohello action definition.</span></span> <span data-ttu-id="813d0-239">Por exemplo, suponha que você deseja que os dados de tootrack como uma "ID de ordem" em sua telemetria:</span><span class="sxs-lookup"><span data-stu-id="813d0-239">For example, suppose you want tootrack data like an "order ID" in your telemetry:</span></span>

  ``` json
  "myAction": {
    "type": "http",
    "inputs": {
        "uri": "http://uri",
        "headers": {
            "Content-Type": "application/json"
        },
        "body": "@triggerBody()"
    },
    "trackedProperties": {
        "myActionHTTPStatusCode": "@action()['outputs']['statusCode']",
        "myActionHTTPValue": "@action()['outputs']['body']['<content>']",
        "transactionId": "@action()['inputs']['body']['<content>']"
    }
  }
  ```

## <a name="next-steps"></a><span data-ttu-id="813d0-240">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="813d0-240">Next steps</span></span>

* [<span data-ttu-id="813d0-241">Criar modelos para implantação de aplicativos lógicos e gerenciamento de versão</span><span class="sxs-lookup"><span data-stu-id="813d0-241">Create templates for logic app deployment and release management</span></span>](../logic-apps/logic-apps-create-deploy-template.md)
* [<span data-ttu-id="813d0-242">Cenários B2B com o Enterprise Integration Pack</span><span class="sxs-lookup"><span data-stu-id="813d0-242">B2B scenarios with Enterprise Integration Pack</span></span>](../logic-apps/logic-apps-enterprise-integration-overview.md)
* [<span data-ttu-id="813d0-243">Monitorar mensagens do B2B</span><span class="sxs-lookup"><span data-stu-id="813d0-243">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)