---
title: "aaaMonitor e obter informações sobre sua lógica de aplicativo é executado usando o OMS - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Monitorar a execução do seu aplicativo lógica com insights tooget de análise de Log e Operations Management Suite (OMS) e detalhes de depuração mais avançados para solução de problemas e diagnóstico"
author: divyaswarnkar
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/9/2017
ms.author: LADocs; divswa
ms.openlocfilehash: a76fd6d1ff5c0010550be0f991514ce95f659fd6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="761d7-103">Monitorar e obter informações sobre execuções de aplicativo lógico com o OMS (Operations Management Suite) e o Log Analytics</span><span class="sxs-lookup"><span data-stu-id="761d7-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="761d7-104">Para obter informações de depuração mais avançadas e monitoramento, você pode ativar a análise de Log em Olá simultaneamente, quando você cria um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="761d7-104">For monitoring and richer debugging information, you can turn on Log Analytics at hello same time when you create a logic app.</span></span> <span data-ttu-id="761d7-105">Análise de log fornece o diagnóstico, logs e monitoramento para seu aplicativo de lógica é executada por meio do portal do Operations Management Suite (OMS) hello.</span><span class="sxs-lookup"><span data-stu-id="761d7-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through hello Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="761d7-106">Quando você adiciona Olá tooOMS de solução de lógica de gerenciamento de aplicativos, você obterá o status agregado para sua lógica de aplicativo será executado e os detalhes específicos, como status, tempo de execução, o status de reenvio e IDs de correlação.</span><span class="sxs-lookup"><span data-stu-id="761d7-106">When you add hello Logic Apps Management solution tooOMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="761d7-107">Este tópico mostra como tooturn na análise de Log ou instale Olá solução lógica de gerenciamento de aplicativos no OMS para que você pode exibir eventos de tempo de execução e dados para seu aplicativo de lógica de execução.</span><span class="sxs-lookup"><span data-stu-id="761d7-107">This topic shows how tooturn on Log Analytics or install hello Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="761d7-108">toomonitor seus aplicativos existentes da lógica, siga estas etapas muito [ativar o log de diagnóstico e enviar lógica tooOMS de dados de tempo de execução de aplicativo](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="761d7-108">toomonitor your existing logic apps, follow these steps too [turn on diagnostic logging and send logic app runtime data tooOMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="761d7-109">Requisitos</span><span class="sxs-lookup"><span data-stu-id="761d7-109">Requirements</span></span>

<span data-ttu-id="761d7-110">Antes de começar, você precisa toohave um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="761d7-110">Before you start, you need toohave an OMS workspace.</span></span> <span data-ttu-id="761d7-111">Saiba [como toocreate um espaço de trabalho do OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="761d7-111">Learn [how toocreate an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="761d7-112">Ativar o registro em log de diagnóstico durante a criação de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="761d7-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="761d7-113">No [Portal do Azure](https://portal.azure.com), crie um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="761d7-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="761d7-114">Escolha **Novo** > **Enterprise Integration** > **Aplicativo Lógico** > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="761d7-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Criar um aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="761d7-116">Em Olá **criar lógica aplicativo** página, executar essas tarefas, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="761d7-116">In hello **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="761d7-117">Dê um nome para seu aplicativo lógico e selecione sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="761d7-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="761d7-118">Crie ou selecione um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="761d7-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="761d7-119">Definir **análise de Log** muito**em**.</span><span class="sxs-lookup"><span data-stu-id="761d7-119">Set **Log Analytics** too**On**.</span></span> 
   <span data-ttu-id="761d7-120">Espaço de trabalho do OMS hello selecione onde você deseja muito enviar dados para seu aplicativo lógica é executada.</span><span class="sxs-lookup"><span data-stu-id="761d7-120">Select hello OMS workspace where you want too send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="761d7-121">Quando você estiver pronto, escolha **Pin toodashboard** > **criar**.</span><span class="sxs-lookup"><span data-stu-id="761d7-121">When you're ready, choose **Pin toodashboard** > **Create**.</span></span>

      ![Criar aplicativo lógico](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="761d7-123">Após a conclusão dessa etapa, o Azure criará seu aplicativo lógico, que agora está associado ao seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="761d7-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="761d7-124">Além disso, esta etapa instala automaticamente solução de gerenciamento de aplicativos de lógica de saudação em seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="761d7-124">Also, this step also automatically installs hello Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="761d7-125">tooview sua lógica de aplicativo é executado no OMS, [continuar com estas etapas](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="761d7-125">tooview your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-hello-logic-apps-management-solution-in-oms"></a><span data-ttu-id="761d7-126">Instalar a solução de gerenciamento de aplicativos de lógica de saudação do OMS</span><span class="sxs-lookup"><span data-stu-id="761d7-126">Install hello Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="761d7-127">Se você já ativou o Log Analytics durante a criação de seu aplicativo lógico, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="761d7-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="761d7-128">Você já tem a solução de gerenciamento de aplicativos de lógica de Olá instalada no OMS.</span><span class="sxs-lookup"><span data-stu-id="761d7-128">You already have hello Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="761d7-129">Em Olá [portal do Azure](https://portal.azure.com), escolha **mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="761d7-129">In hello [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="761d7-130">Pesquise por "log analytics" enquanto filtra e, em seguida, escolha **Log Analytics**, conforme exibido:</span><span class="sxs-lookup"><span data-stu-id="761d7-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Escolher “Log Analytics”](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="761d7-132">Em **Log Analytics**, encontre e selecione o espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="761d7-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selecionar o espaço de trabalho do OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="761d7-134">Em **Gerenciamento**, escolha **Portal do OMS**.</span><span class="sxs-lookup"><span data-stu-id="761d7-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Escolher “Portal do OMS”](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="761d7-136">Na home page do OMS, se faixa atualização Olá for exibida, escolha faixa Olá para que você atualizar seu espaço de trabalho do OMS primeiro.</span><span class="sxs-lookup"><span data-stu-id="761d7-136">On your OMS homepage, if hello upgrade banner appears, choose hello banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="761d7-137">Então escolha **Galeria de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="761d7-137">Then choose **Solutions Gallery**.</span></span>

   ![Escolha "Galeria de Soluções"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="761d7-139">Em **todas as soluções**, localizar e escolha o bloco de saudação do hello **lógica de gerenciamento de aplicativos** solução.</span><span class="sxs-lookup"><span data-stu-id="761d7-139">Under **All solutions**, find and choose hello tile for hello **Logic Apps Management** solution.</span></span>

   ![Escolha "Gerenciamento de Aplicativos Lógicos"](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="761d7-141">solução de saudação tooinstall em seu espaço de trabalho do OMS, escolha **adicionar**.</span><span class="sxs-lookup"><span data-stu-id="761d7-141">tooinstall hello solution in your OMS workspace, choose **Add**.</span></span>

   ![Escolha "Adicionar" para "Gerenciamento de Aplicativos Lógicos"](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="761d7-143">Exibir as execuções de seu aplicativo lógico em seu espaço de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="761d7-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="761d7-144">Contagem de saudação tooview e o status de sua lógica de aplicativo é executado, página de visão geral de toohello vá para seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="761d7-144">tooview hello count and status for your logic app runs, go toohello overview page for your OMS workspace.</span></span> <span data-ttu-id="761d7-145">Examine os detalhes de saudação na Olá **lógica de gerenciamento de aplicativos** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="761d7-145">Review hello details on hello **Logic Apps Management** tile.</span></span>

   ![Bloco de visão geral mostrando a contagem e o status da execução do aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="761d7-147">Se esse cabeçalho de atualização é exibida em vez de bloco de lógica de gerenciamento de aplicativos de saudação, escolha faixa Olá para que você atualizar seu espaço de trabalho do OMS primeiro.</span><span class="sxs-lookup"><span data-stu-id="761d7-147">If this upgrade banner appears instead of hello Logic Apps Management tile, choose hello banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Atualizar "Espaço de Trabalho do OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="761d7-149">tooview um resumo com mais detalhes sobre seu aplicativo lógica será executado, escolha Olá **lógica de gerenciamento de aplicativos** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="761d7-149">tooview a summary with more details about your logic app runs, choose hello **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="761d7-150">Aqui, as execuções de seu aplicativo lógica são agrupadas por nome ou por status de execução.</span><span class="sxs-lookup"><span data-stu-id="761d7-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Resumo do status das execuções de seu aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="761d7-152">tooview que todos Olá é executado de um aplicativo lógico específico ou de status, linha hello selecione um aplicativo lógico ou um status.</span><span class="sxs-lookup"><span data-stu-id="761d7-152">tooview all hello runs for a specific logic app or status, select hello row for a logic app or a status.</span></span>

   <span data-ttu-id="761d7-153">Aqui está um exemplo que mostra todas as execuções de saudação para um aplicativo lógica específica:</span><span class="sxs-lookup"><span data-stu-id="761d7-153">Here is an example that shows all hello runs for a specific logic app:</span></span>

   ![Exibir execuções de um aplicativo lógico ou um status](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="761d7-155">Olá **reenvio** coluna mostra "Sim" para execuções que resultam de uma execução reenviada.</span><span class="sxs-lookup"><span data-stu-id="761d7-155">hello **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="761d7-156">toofilter esses resultados, você pode executar a filtragem do lado do cliente e do servidor.</span><span class="sxs-lookup"><span data-stu-id="761d7-156">toofilter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="761d7-157">O filtro do cliente: para cada coluna, escolha os filtros de saudação que você deseja.</span><span class="sxs-lookup"><span data-stu-id="761d7-157">Client-side filter: For each column, choose hello filters that you want.</span></span> 
   <span data-ttu-id="761d7-158">Estes são alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="761d7-158">Here are some examples:</span></span>

     ![Exemplo de filtros de coluna](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="761d7-160">Filtro do servidor: toochoose um horário específico janela ou toolimit Olá número de execuções que aparecem, usar o controle de escopo de saudação na parte superior de saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="761d7-160">Server-side filter: toochoose a specific time window or toolimit hello number of runs that appear, use hello scope control at hello top of hello page.</span></span> 
   <span data-ttu-id="761d7-161">Por padrão, apenas 1.000 registros aparecem por vez.</span><span class="sxs-lookup"><span data-stu-id="761d7-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Janela de tempo de saudação de alteração](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="761d7-163">tooview todos os Olá ações e os detalhes para uma execução, específico, selecione uma linha, o que abre a página de pesquisa de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="761d7-163">tooview all hello actions and their details for a specific run, select a row, which opens hello Log Search page.</span></span> 

   * <span data-ttu-id="761d7-164">tooview essas informações em uma tabela, escolha **tabela**.</span><span class="sxs-lookup"><span data-stu-id="761d7-164">tooview this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="761d7-165">consulta de saudação toochange, você pode editar cadeia de caracteres de consulta de saudação na barra de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="761d7-165">toochange hello query, you can edit hello query string in hello search bar.</span></span> 
   <span data-ttu-id="761d7-166">Para ter uma experiência melhor, escolha **Análise Avançada**.</span><span class="sxs-lookup"><span data-stu-id="761d7-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Exibir ações e detalhes da execução de um aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="761d7-168">Aqui na página do Azure Log Analytics hello, você pode atualizar consultas e exibição Olá resulta da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="761d7-168">Here on hello Azure Log Analytics page, you can update queries and view hello results from hello table.</span></span> 
     <span data-ttu-id="761d7-169">Essa consulta usa [Kusto a linguagem de consulta](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que pode ser editado se você quiser tooview diferentes resultados.</span><span class="sxs-lookup"><span data-stu-id="761d7-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want tooview different results.</span></span> 

     ![Azure Log Analytics – modo de exibição de consulta](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="761d7-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="761d7-171">Next steps</span></span>

* [<span data-ttu-id="761d7-172">Monitorar mensagens do B2B</span><span class="sxs-lookup"><span data-stu-id="761d7-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
