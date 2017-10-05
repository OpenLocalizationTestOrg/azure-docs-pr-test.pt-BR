---
title: "Monitorar e obter informações sobre as execuções de seu aplicativo lógico usando o OMS – Aplicativo Lógico do Azure | Microsoft Docs"
description: "Monitorar as execuções de seu aplicativo lógico com o Log Analytics e o OMS (Operations Management Suite) para obter informações ideias e detalhes de depuração mais avançados para solução de problemas e diagnóstico"
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
ms.openlocfilehash: 0e9f0ef3c87b5c0da1cc4ad16d37178c8f5c9625
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="monitor-and-get-insights-about-logic-app-runs-with-operations-management-suite-oms-and-log-analytics"></a><span data-ttu-id="9542f-103">Monitorar e obter informações sobre execuções de aplicativo lógico com o OMS (Operations Management Suite) e o Log Analytics</span><span class="sxs-lookup"><span data-stu-id="9542f-103">Monitor and get insights about logic app runs with Operations Management Suite (OMS) and Log Analytics</span></span>

<span data-ttu-id="9542f-104">Para obter informações monitoramento e depuração mais detalhadas, ative o Log Analytics durante a criação de um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="9542f-104">For monitoring and richer debugging information, you can turn on Log Analytics at the same time when you create a logic app.</span></span> <span data-ttu-id="9542f-105">O Log Analytics fornece o registro em log de diagnóstico e o monitoramento de suas execuções de aplicativo lógico por meio do portal do OMS (Operations Management Suite).</span><span class="sxs-lookup"><span data-stu-id="9542f-105">Log Analytics provides diagnostics logging and monitoring for your logic app runs through the Operations Management Suite (OMS) portal.</span></span> <span data-ttu-id="9542f-106">Quando você adiciona a solução de Gerenciamento de Aplicativos Lógicos ao OMS, você obtém o status agregado das execuções de seu aplicativo lógico e detalhes específicos, como status, tempo de execução, status de reenvio e IDs de correlação.</span><span class="sxs-lookup"><span data-stu-id="9542f-106">When you add the Logic Apps Management solution to OMS, you get aggregated status for your logic app runs and specific details like status, execution time, resubmission status, and correlation IDs.</span></span>

<span data-ttu-id="9542f-107">Este tópico mostra como ativar o Log Analytics ou instalar a solução de Gerenciamento de Aplicativos Lógicos no OMS, para que você possa exibir eventos de tempo de execução e dados para a execução de seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="9542f-107">This topic shows how to turn on Log Analytics or install the Logic Apps Management solution in OMS so you can view runtime events and data for your logic app run.</span></span>

 > [!TIP]
 > <span data-ttu-id="9542f-108">Para monitorar seus aplicativos lógicos existentes, execute estas etapas para [ativar o registro em log de diagnóstico e enviar dados de tempo de execução do aplicativo lógica para o OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span><span class="sxs-lookup"><span data-stu-id="9542f-108">To monitor your existing logic apps, follow these steps to [turn on diagnostic logging and send logic app runtime data to OMS](../logic-apps/logic-apps-monitor-your-logic-apps.md#azure-diagnostics).</span></span>

## <a name="requirements"></a><span data-ttu-id="9542f-109">Requisitos</span><span class="sxs-lookup"><span data-stu-id="9542f-109">Requirements</span></span>

<span data-ttu-id="9542f-110">Antes de começar, você precisa ter um espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="9542f-110">Before you start, you need to have an OMS workspace.</span></span> <span data-ttu-id="9542f-111">Saiba [como criar um espaço de trabalho do OMS](../log-analytics/log-analytics-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9542f-111">Learn [how to create an OMS workspace](../log-analytics/log-analytics-get-started.md).</span></span> 

## <a name="turn-on-diagnostics-logging-when-creating-logic-apps"></a><span data-ttu-id="9542f-112">Ativar o registro em log de diagnóstico durante a criação de aplicativos lógicos</span><span class="sxs-lookup"><span data-stu-id="9542f-112">Turn on diagnostics logging when creating logic apps</span></span>

1. <span data-ttu-id="9542f-113">No [Portal do Azure](https://portal.azure.com), crie um aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="9542f-113">In [Azure portal](https://portal.azure.com), create a logic app.</span></span> <span data-ttu-id="9542f-114">Escolha **Novo** > **Enterprise Integration** > **Aplicativo Lógico** > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9542f-114">Choose **New** > **Enterprise Integration** > **Logic App** > **Create**.</span></span>

   ![Criar um aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/find-logic-apps-azure.png)

2. <span data-ttu-id="9542f-116">Na página **Criar aplicativo lógico**, execute essas tarefas, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="9542f-116">In the **Create logic app** page, perform these tasks as shown:</span></span>

   1. <span data-ttu-id="9542f-117">Dê um nome para seu aplicativo lógico e selecione sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="9542f-117">Provide a name for your logic app and select your Azure subscription.</span></span> 
   2. <span data-ttu-id="9542f-118">Crie ou selecione um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="9542f-118">Create or select an Azure resource group.</span></span>
   3. <span data-ttu-id="9542f-119">Defina **Log Analytics** como **Ativado**.</span><span class="sxs-lookup"><span data-stu-id="9542f-119">Set **Log Analytics** to **On**.</span></span> 
   <span data-ttu-id="9542f-120">Selecione o espaço de trabalho do OMS para o qual você deseja enviar dados para suas execuções de aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="9542f-120">Select the OMS workspace where you want to send data for your logic app runs.</span></span> 
   4. <span data-ttu-id="9542f-121">Quando você estiver pronto, escolha **Fixar no painel** > **Criar**.</span><span class="sxs-lookup"><span data-stu-id="9542f-121">When you're ready, choose **Pin to dashboard** > **Create**.</span></span>

      ![Criar aplicativo lógico](./media/logic-apps-monitor-your-logic-apps-oms/create-logic-app.png)

      <span data-ttu-id="9542f-123">Após a conclusão dessa etapa, o Azure criará seu aplicativo lógico, que agora está associado ao seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="9542f-123">After you finish this step, Azure creates your logic app, which is now associated with your OMS workspace.</span></span> 
      <span data-ttu-id="9542f-124">Além disso, essa etapa também instala automaticamente a solução de Gerenciamento de Aplicativos Lógicos em seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="9542f-124">Also, this step also automatically installs the Logic Apps Management solution in your OMS workspace.</span></span>

3. <span data-ttu-id="9542f-125">Para exibir as execuções de seu aplicativo lógico no OMS, [continue com estas etapas](#view-logic-app-runs-oms).</span><span class="sxs-lookup"><span data-stu-id="9542f-125">To view your logic app runs in OMS, [continue with these steps](#view-logic-app-runs-oms).</span></span>

## <a name="install-the-logic-apps-management-solution-in-oms"></a><span data-ttu-id="9542f-126">Instalar a solução de Gerenciamento de Aplicativos Lógicos no OMS</span><span class="sxs-lookup"><span data-stu-id="9542f-126">Install the Logic Apps Management solution in OMS</span></span>

<span data-ttu-id="9542f-127">Se você já ativou o Log Analytics durante a criação de seu aplicativo lógico, ignore esta etapa.</span><span class="sxs-lookup"><span data-stu-id="9542f-127">If you already turned on Log Analytics when you created your logic app, skip this step.</span></span> <span data-ttu-id="9542f-128">Você já tem a solução de Gerenciamento de Aplicativos Lógicos instalada no OMS.</span><span class="sxs-lookup"><span data-stu-id="9542f-128">You already have the Logic Apps Management solution installed in OMS.</span></span>

1. <span data-ttu-id="9542f-129">No [portal do Azure](https://portal.azure.com), escolha **Mais serviços**.</span><span class="sxs-lookup"><span data-stu-id="9542f-129">In the [Azure portal](https://portal.azure.com), choose **More Services**.</span></span> <span data-ttu-id="9542f-130">Pesquise por "log analytics" enquanto filtra e, em seguida, escolha **Log Analytics**, conforme exibido:</span><span class="sxs-lookup"><span data-stu-id="9542f-130">Search for "log analytics" as your filter, and choose **Log Analytics** as shown:</span></span>

   ![Escolher “Log Analytics”](media/logic-apps-monitor-your-logic-apps-oms/find-log-analytics.png)

2. <span data-ttu-id="9542f-132">Em **Log Analytics**, encontre e selecione o espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="9542f-132">Under **Log Analytics**, find and select your OMS workspace.</span></span> 

   ![Selecionar o espaço de trabalho do OMS](media/logic-apps-monitor-your-logic-apps-oms/select-logic-app.png)

3. <span data-ttu-id="9542f-134">Em **Gerenciamento**, escolha **Portal do OMS**.</span><span class="sxs-lookup"><span data-stu-id="9542f-134">Under **Management**, choose **OMS Portal**.</span></span>

   ![Escolher “Portal do OMS”](media/logic-apps-monitor-your-logic-apps-oms/oms-portal-page.png)

4. <span data-ttu-id="9542f-136">Na home page do OMS, se a faixa de atualização for exibida, escolha a faixa para que você atualizar seu espaço de trabalho do OMS primeiro.</span><span class="sxs-lookup"><span data-stu-id="9542f-136">On your OMS homepage, if the upgrade banner appears, choose the banner so that you upgrade your OMS workspace first.</span></span> <span data-ttu-id="9542f-137">Então escolha **Galeria de Soluções**.</span><span class="sxs-lookup"><span data-stu-id="9542f-137">Then choose **Solutions Gallery**.</span></span>

   ![Escolha "Galeria de Soluções"](media/logic-apps-monitor-your-logic-apps-oms/solutions-gallery.png)

5. <span data-ttu-id="9542f-139">Em **Todas as soluções**, localize e escolha o bloco para a solução **Gerenciamento de Aplicativos Lógicos**.</span><span class="sxs-lookup"><span data-stu-id="9542f-139">Under **All solutions**, find and choose the tile for the **Logic Apps Management** solution.</span></span>

   ![Escolha "Gerenciamento de Aplicativos Lógicos"](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-management-tile2.png)

6. <span data-ttu-id="9542f-141">Para instalar a solução em seu espaço de trabalho do OMS, escolha **Adicionar**.</span><span class="sxs-lookup"><span data-stu-id="9542f-141">To install the solution in your OMS workspace, choose **Add**.</span></span>

   ![Escolha "Adicionar" para "Gerenciamento de Aplicativos Lógicos"](media/logic-apps-monitor-your-logic-apps-oms/add-logic-apps-management-solution.png)

<a name="view-logic-app-runs-oms"></a>

## <a name="view-your-logic-app-runs-in-your-oms-workspace"></a><span data-ttu-id="9542f-143">Exibir as execuções de seu aplicativo lógico em seu espaço de trabalho do OMS</span><span class="sxs-lookup"><span data-stu-id="9542f-143">View your logic app runs in your OMS workspace</span></span>

1. <span data-ttu-id="9542f-144">Para exibir a contagem e o status das execuções de seu aplicativo lógico, acesse a página de visão geral de seu espaço de trabalho do OMS.</span><span class="sxs-lookup"><span data-stu-id="9542f-144">To view the count and status for your logic app runs, go to the overview page for your OMS workspace.</span></span> <span data-ttu-id="9542f-145">Examine os detalhes no bloco **Gerenciamento de Aplicativos Lógicos**.</span><span class="sxs-lookup"><span data-stu-id="9542f-145">Review the details on the **Logic Apps Management** tile.</span></span>

   ![Bloco de visão geral mostrando a contagem e o status da execução do aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/overview.png)

   > [!Note]
   > <span data-ttu-id="9542f-147">Se esse cabeçalho de atualização é exibida em vez do bloco de lógica de gerenciamento de aplicativos, escolha a faixa para que você atualizar seu espaço de trabalho do OMS primeiro.</span><span class="sxs-lookup"><span data-stu-id="9542f-147">If this upgrade banner appears instead of the Logic Apps Management tile, choose the banner so that you upgrade your OMS workspace first.</span></span>
  
   > ![Atualizar "Espaço de Trabalho do OMS"](media/logic-apps-monitor-your-logic-apps-oms/oms-upgrade-banner.png)

2. <span data-ttu-id="9542f-149">Para exibir um resumo com mais detalhes sobre as execuções de seu aplicativo lógico, escolha o bloco **Gerenciamento de Aplicativos Lógicos**.</span><span class="sxs-lookup"><span data-stu-id="9542f-149">To view a summary with more details about your logic app runs, choose the **Logic Apps Management** tile.</span></span>

   <span data-ttu-id="9542f-150">Aqui, as execuções de seu aplicativo lógica são agrupadas por nome ou por status de execução.</span><span class="sxs-lookup"><span data-stu-id="9542f-150">Here, your logic app runs are grouped by name or by execution status.</span></span>

   ![Resumo do status das execuções de seu aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/logic-apps-runs-summary.png)
   
3. <span data-ttu-id="9542f-152">Para exibir todas as execuções de um aplicativo lógico específico ou status, selecione a linha de um aplicativo lógico ou um status.</span><span class="sxs-lookup"><span data-stu-id="9542f-152">To view all the runs for a specific logic app or status, select the row for a logic app or a status.</span></span>

   <span data-ttu-id="9542f-153">Veja um exemplo que mostra todas as execuções de um aplicativo lógico específico:</span><span class="sxs-lookup"><span data-stu-id="9542f-153">Here is an example that shows all the runs for a specific logic app:</span></span>

   ![Exibir execuções de um aplicativo lógico ou um status](media/logic-apps-monitor-your-logic-apps-oms/logic-app-run-details.png)

   > [!NOTE]
   > <span data-ttu-id="9542f-155">A coluna **Reenvio** mostra "Sim" para execuções resultantes de uma execução reenviada.</span><span class="sxs-lookup"><span data-stu-id="9542f-155">The **Resubmission** column shows "Yes" for runs that result from a resubmitted run.</span></span>

4. <span data-ttu-id="9542f-156">Para filtrar esses resultados, execute a filtragem tanto no lado do cliente quanto no lado do servidor.</span><span class="sxs-lookup"><span data-stu-id="9542f-156">To filter these results, you can perform both client-side and server-side filtering.</span></span>

   * <span data-ttu-id="9542f-157">Filtro no lado do cliente: para cada coluna, escolha os filtros desejados.</span><span class="sxs-lookup"><span data-stu-id="9542f-157">Client-side filter: For each column, choose the filters that you want.</span></span> 
   <span data-ttu-id="9542f-158">Estes são alguns exemplos:</span><span class="sxs-lookup"><span data-stu-id="9542f-158">Here are some examples:</span></span>

     ![Exemplo de filtros de coluna](media/logic-apps-monitor-your-logic-apps-oms/filters.png)

   * <span data-ttu-id="9542f-160">Filtro no lado do servidor: para escolher um período específico, ou para limitar o número de execuções exibidas, use o controle de escopo na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="9542f-160">Server-side filter: To choose a specific time window or to limit the number of runs that appear, use the scope control at the top of the page.</span></span> 
   <span data-ttu-id="9542f-161">Por padrão, apenas 1.000 registros aparecem por vez.</span><span class="sxs-lookup"><span data-stu-id="9542f-161">By default, only 1,000 records appear at a time.</span></span> 
   
     ![Alterar o período](media/logic-apps-monitor-your-logic-apps-oms/change-interval.png)
 
5. <span data-ttu-id="9542f-163">Para exibir todas as ações e os detalhes de uma execução específica, selecione uma linha, o que abrirá a página Pesquisa de Log.</span><span class="sxs-lookup"><span data-stu-id="9542f-163">To view all the actions and their details for a specific run, select a row, which opens the Log Search page.</span></span> 

   * <span data-ttu-id="9542f-164">Para exibir essas informações em uma tabela, escolha **Tabela**.</span><span class="sxs-lookup"><span data-stu-id="9542f-164">To view this information in a table, choose **Table**.</span></span>
   * <span data-ttu-id="9542f-165">Para alterar a consulta, edite a cadeia de consulta na barra de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="9542f-165">To change the query, you can edit the query string in the search bar.</span></span> 
   <span data-ttu-id="9542f-166">Para ter uma experiência melhor, escolha **Análise Avançada**.</span><span class="sxs-lookup"><span data-stu-id="9542f-166">For a better experience, choose **Advanced Analytics**.</span></span>

     ![Exibir ações e detalhes da execução de um aplicativo lógico](media/logic-apps-monitor-your-logic-apps-oms/log-search-page.png)

     <span data-ttu-id="9542f-168">Aqui na página do Azure Log Analytics, você pode atualizar consultas e exibir os resultados da tabela.</span><span class="sxs-lookup"><span data-stu-id="9542f-168">Here on the Azure Log Analytics page, you can update queries and view the results from the table.</span></span> 
     <span data-ttu-id="9542f-169">Essa consulta usa a [linguagem de consulta Kusto](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), que pode ser editada se você quiser exibir resultados diferentes.</span><span class="sxs-lookup"><span data-stu-id="9542f-169">This query uses [Kusto query language](https://docs.loganalytics.io/learn/tutorials/getting_started_with_queries.html), which you can edit if you want to view different results.</span></span> 

     ![Azure Log Analytics – modo de exibição de consulta](media/logic-apps-monitor-your-logic-apps-oms/query.png)

## <a name="next-steps"></a><span data-ttu-id="9542f-171">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9542f-171">Next steps</span></span>

* [<span data-ttu-id="9542f-172">Monitorar mensagens do B2B</span><span class="sxs-lookup"><span data-stu-id="9542f-172">Monitor B2B messages</span></span>](../logic-apps/logic-apps-monitor-b2b-message.md)
