---
title: aaaExport tooPower BI do Application Insights | Microsoft Docs
description: As consultas do Analytics podem ser exibidas no Power BI.
services: application-insights
documentationcenter: 
author: noamben
manager: carmonm
ms.assetid: 7f13ea66-09dc-450f-b8f9-f40fdad239f2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/18/2016
ms.author: bwren
ms.openlocfilehash: 6668cd7f4e0fbf41695972617f5f8ec207356659
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="93864-103">Alimentar o Power BI do Application Insights</span><span class="sxs-lookup"><span data-stu-id="93864-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="93864-104">O [Power BI](http://www.powerbi.com/) é um conjunto de ferramentas de análise de negócios que ajudam a analisar dados e a compartilhar informações.</span><span class="sxs-lookup"><span data-stu-id="93864-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="93864-105">Painéis avançados estão disponíveis em cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="93864-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="93864-106">Você pode combinar dados de várias fontes, incluindo consultas do Analytics do [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="93864-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="93864-107">Há três métodos recomendados de exportação tooPower de dados do Application Insights BI.</span><span class="sxs-lookup"><span data-stu-id="93864-107">There are three recommended methods of exporting Application Insights data tooPower BI.</span></span> <span data-ttu-id="93864-108">Você pode usá-los separadamente ou em conjunto.</span><span class="sxs-lookup"><span data-stu-id="93864-108">You can use them separately or together.</span></span>

* <span data-ttu-id="93864-109">[**Adaptador do Power BI**](#power-pi-adapter) -configure um painel completo de telemetria do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="93864-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="93864-110">conjunto de saudação de gráficos é predefinido, mas você pode adicionar suas próprias consultas de outras fontes.</span><span class="sxs-lookup"><span data-stu-id="93864-110">hello set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="93864-111">[**Exportar as consultas analíticas** ](#export-analytics-queries) -gravar qualquer consulta desejado usando a análise e exportá-lo tooPower BI.</span><span class="sxs-lookup"><span data-stu-id="93864-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it tooPower BI.</span></span> <span data-ttu-id="93864-112">Você pode colocar essa consulta em um painel com outros dados.</span><span class="sxs-lookup"><span data-stu-id="93864-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="93864-113">[**A exportação contínua e análise de fluxo** ](app-insights-export-stream-analytics.md) -isso envolve mais tooset de trabalho para cima.</span><span class="sxs-lookup"><span data-stu-id="93864-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work tooset up.</span></span> <span data-ttu-id="93864-114">É útil se você quiser tookeep seus dados por longos períodos.</span><span class="sxs-lookup"><span data-stu-id="93864-114">It is useful if you want tookeep your data for long periods.</span></span> <span data-ttu-id="93864-115">Caso contrário, hello outros métodos são recomendados.</span><span class="sxs-lookup"><span data-stu-id="93864-115">Otherwise, hello other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="93864-116">Adaptador do Power BI</span><span class="sxs-lookup"><span data-stu-id="93864-116">Power BI adapter</span></span>
<span data-ttu-id="93864-117">Esse método cria um painel completo de telemetria para você.</span><span class="sxs-lookup"><span data-stu-id="93864-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="93864-118">o conjunto de dados inicial Olá é predefinido, mas você pode adicionar mais tooit de dados.</span><span class="sxs-lookup"><span data-stu-id="93864-118">hello initial data set is predefined, but you can add more data tooit.</span></span>

### <a name="get-hello-adapter"></a><span data-ttu-id="93864-119">Obter adaptador Olá</span><span class="sxs-lookup"><span data-stu-id="93864-119">Get hello adapter</span></span>
1. <span data-ttu-id="93864-120">Entrar muito[Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="93864-120">Sign in too[Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="93864-121">Abra **Obter Dados**, **Serviços**, **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="93864-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Obter da fonte de dados do Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="93864-123">Forneça detalhes de saudação do recurso do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="93864-123">Provide hello details of your Application Insights resource.</span></span>
   
    ![Obter da fonte de dados do Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="93864-125">Aguarde um minuto ou dois para Olá toobe de dados importado.</span><span class="sxs-lookup"><span data-stu-id="93864-125">Wait a minute or two for hello data toobe imported.</span></span>
   
    ![Adaptador do Power BI](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="93864-127">Você pode editar o painel hello, a combinação de gráficos do Application Insights Olá com as outras fontes e com consultas de análise.</span><span class="sxs-lookup"><span data-stu-id="93864-127">You can edit hello dashboard, combining hello Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="93864-128">Há uma galeria de visualização onde você pode obter mais gráficos e cada um deles possui parâmetros que podem ser definidos.</span><span class="sxs-lookup"><span data-stu-id="93864-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="93864-129">Após a importação inicial hello, painel hello e relatórios Olá continuar tooupdate diariamente.</span><span class="sxs-lookup"><span data-stu-id="93864-129">After hello initial import, hello dashboard and hello reports continue tooupdate daily.</span></span> <span data-ttu-id="93864-130">Você pode controlar o agendamento de atualização de Olá Olá conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="93864-130">You can control hello refresh schedule on hello dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="93864-131">Exportar consultas do Analytics</span><span class="sxs-lookup"><span data-stu-id="93864-131">Export Analytics queries</span></span>
<span data-ttu-id="93864-132">Ela permite que você toowrite qualquer análise de consulta que você deseja e, em seguida, exportar esse painel do Power BI tooa.</span><span class="sxs-lookup"><span data-stu-id="93864-132">This route allows you toowrite any Analytics query you like, and then export that tooa Power BI dashboard.</span></span> <span data-ttu-id="93864-133">(Você pode adicionar toohello painel criado pelo adaptador hello.)</span><span class="sxs-lookup"><span data-stu-id="93864-133">(You can add toohello dashboard created by hello adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="93864-134">Uma vez: instalar o Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="93864-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="93864-135">tooimport consulta Application Insights, você usar a versão de área de trabalho de saudação do Power BI.</span><span class="sxs-lookup"><span data-stu-id="93864-135">tooimport your Application Insights query, you use hello desktop version of Power BI.</span></span> <span data-ttu-id="93864-136">Mas, em seguida, você poderá publicá-lo toohello web ou tooyour o espaço de trabalho do Power BI nuvem.</span><span class="sxs-lookup"><span data-stu-id="93864-136">But then you can publish it toohello web or tooyour Power BI cloud workspace.</span></span> 

<span data-ttu-id="93864-137">Instalar o [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="93864-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="93864-138">Exportar uma consulta do Analytics</span><span class="sxs-lookup"><span data-stu-id="93864-138">Export an Analytics query</span></span>
1. <span data-ttu-id="93864-139">[Abra o Analytics e escreva sua consulta](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="93864-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="93864-140">Teste e ajuste a consulta Olá até que você estiver satisfeito com os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="93864-140">Test and refine hello query until you're happy with hello results.</span></span>

   <span data-ttu-id="93864-141">**Verifique se essa consulta Olá é executado corretamente em análise antes de exportá-lo.**</span><span class="sxs-lookup"><span data-stu-id="93864-141">**Make sure that hello query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="93864-142">Em Olá **exportar** menu, escolha **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="93864-142">On hello **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="93864-143">Salve o arquivo de texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="93864-143">Save hello text file.</span></span>
   
    ![Exportar a consulta do Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="93864-145">No Power BI Desktop, selecione **obter dados, a consulta em branco** e, em seguida, em Olá editor de consultas, em **exibição** selecione **Editor de consulta avançada**.</span><span class="sxs-lookup"><span data-stu-id="93864-145">In Power BI Desktop select **Get Data, Blank Query** and then in hello query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="93864-146">Colar hello exportada linguagem M script no hello Editor de consulta avançada.</span><span class="sxs-lookup"><span data-stu-id="93864-146">Paste hello exported M Language script into hello Advanced Query Editor.</span></span>

    ![Editor avançado de consultas](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="93864-148">Você pode ter tooprovide credenciais tooallow Power BI tooaccess do Azure.</span><span class="sxs-lookup"><span data-stu-id="93864-148">You might have tooprovide credentials tooallow Power BI tooaccess Azure.</span></span> <span data-ttu-id="93864-149">Use 'conta organizacional' toosign com sua conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="93864-149">Use 'organizational account' toosign in with your Microsoft account.</span></span>
   
    ![Forneça as credenciais do Azure tooenable Power BI toorun sua consulta Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="93864-151">(Se você precisar de credenciais de saudação tooverify, use comando de menu de configurações de fonte de dados Olá no hello Editor de consultas.</span><span class="sxs-lookup"><span data-stu-id="93864-151">(If you need tooverify hello credentials, use hello Data Source Settings menu command in hello Query Editor.</span></span> <span data-ttu-id="93864-152">Tome cuidado credenciais de saudação toospecify usadas para o Azure, que pode ser diferente das suas credenciais para o Power BI.)</span><span class="sxs-lookup"><span data-stu-id="93864-152">Take care toospecify hello credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="93864-153">Escolha uma visualização da consulta e selecionar campos de saudação para o eixo x, y e segmentando a dimensão.</span><span class="sxs-lookup"><span data-stu-id="93864-153">Choose a visualization for your query and select hello fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Selecionar visualização](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="93864-155">Publica seu espaço de trabalho de nuvem do relatório tooyour Power BI.</span><span class="sxs-lookup"><span data-stu-id="93864-155">Publish your report tooyour Power BI cloud workspace.</span></span> <span data-ttu-id="93864-156">A partir daí, você pode inserir uma versão sincronizada em outras páginas da Web.</span><span class="sxs-lookup"><span data-stu-id="93864-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Selecionar visualização](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="93864-158">Atualizar relatório Olá manualmente em intervalos ou configurar uma atualização agendada na página de opções de saudação.</span><span class="sxs-lookup"><span data-stu-id="93864-158">Refresh hello report manually at intervals, or set up a scheduled refresh on hello options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="93864-159">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="93864-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="93864-160">401 ou 403 Não Autorizado</span><span class="sxs-lookup"><span data-stu-id="93864-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="93864-161">Isso pode acontecer se o token de atualização não foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="93864-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="93864-162">Tente tooensure essas etapas que você ainda terá acesso.</span><span class="sxs-lookup"><span data-stu-id="93864-162">Try these steps tooensure you still have access.</span></span> <span data-ttu-id="93864-163">Se você tem acesso e credenciais de saudação refershing não funcionar, abra um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="93864-163">If you do have access and refershing hello credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="93864-164">Faça logon no hello Portal do Azure e certificar-se de que você pode acessar o recurso de saudação</span><span class="sxs-lookup"><span data-stu-id="93864-164">Log into hello Azure Portal and make sure you can access hello resource</span></span>
2. <span data-ttu-id="93864-165">Tente toorefresh credenciais Olá Olá painel</span><span class="sxs-lookup"><span data-stu-id="93864-165">Try toorefresh hello credentials for hello Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="93864-166">502 Gateway Incorreto</span><span class="sxs-lookup"><span data-stu-id="93864-166">502 Bad Gateway</span></span>
<span data-ttu-id="93864-167">Isso geralmente é causado por uma Consulta de análise que retorna um número de dados excessivo.</span><span class="sxs-lookup"><span data-stu-id="93864-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="93864-168">Você deve tentar usar um intervalo de tempo menor ou usando Olá [atrás](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) ou [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) funciona apenas [projeto](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) Olá campos necessários.</span><span class="sxs-lookup"><span data-stu-id="93864-168">You should try using a smaller time range or by using hello [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) hello fields you need.</span></span>

<span data-ttu-id="93864-169">Se reduzir Olá de conjunto de dados provenientes de consulta de análise de saudação não atender às suas necessidades considere usar Olá [API](https://dev.applicationinsights.io/documentation/overview) toopull um conjunto de dados maior.</span><span class="sxs-lookup"><span data-stu-id="93864-169">If reducing hello dataset coming from hello Analytics query doesn't meet your requirements you should consider using hello [API](https://dev.applicationinsights.io/documentation/overview) toopull a larger dataset.</span></span> <span data-ttu-id="93864-170">Aqui estão as instruções sobre como tooconvert Olá consulta M exportar Olá toouse API.</span><span class="sxs-lookup"><span data-stu-id="93864-170">Here are instructions on how tooconvert hello M-Query export toouse hello API.</span></span>

1. <span data-ttu-id="93864-171">Criar uma [chave de API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span><span class="sxs-lookup"><span data-stu-id="93864-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="93864-172">Saudação de atualização script M do Power BI que você exportou da análise, substituindo Olá ARM URL com a API do AI (veja o exemplo abaixo)</span><span class="sxs-lookup"><span data-stu-id="93864-172">Update hello Power BI M script that you exported from Analytics by replacing hello ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="93864-173">Substituir **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="93864-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="93864-174">por **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="93864-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="93864-175">Finalmente, atualizar credenciais toobasic e usar sua chave de API</span><span class="sxs-lookup"><span data-stu-id="93864-175">Finally, update credentials toobasic, and use your API Key</span></span>
  

<span data-ttu-id="93864-176">**Script existente**</span><span class="sxs-lookup"><span data-stu-id="93864-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="93864-177">**Script atualizado**</span><span class="sxs-lookup"><span data-stu-id="93864-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="93864-178">Sobre amostragem</span><span class="sxs-lookup"><span data-stu-id="93864-178">About sampling</span></span>
<span data-ttu-id="93864-179">Se seu aplicativo envia um lote de dados, o recurso de amostragem adaptável de saudação pode operar e enviar apenas uma porcentagem da sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="93864-179">If your application sends a lot of data, hello adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="93864-180">Olá que mesmo é verdadeiro se você tiver configurado o amostragem manualmente no hello SDK ou na inclusão.</span><span class="sxs-lookup"><span data-stu-id="93864-180">hello same is true if you have manually set sampling either in hello SDK or on ingestion.</span></span> [<span data-ttu-id="93864-181">Saiba mais sobre amostragem.</span><span class="sxs-lookup"><span data-stu-id="93864-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="93864-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="93864-182">Next steps</span></span>
* [<span data-ttu-id="93864-183">Power BI - Saiba mais</span><span class="sxs-lookup"><span data-stu-id="93864-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="93864-184">Tutorial do Analytics</span><span class="sxs-lookup"><span data-stu-id="93864-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

