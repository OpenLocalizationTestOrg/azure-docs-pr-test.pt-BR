---
title: Exportar para o Power BI do Application Insights | Microsoft Docs
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
ms.openlocfilehash: 350a65b1c6432baf258e014c9e63133d2b29e34f
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="feed-power-bi-from-application-insights"></a><span data-ttu-id="77014-103">Alimentar o Power BI do Application Insights</span><span class="sxs-lookup"><span data-stu-id="77014-103">Feed Power BI from Application Insights</span></span>
<span data-ttu-id="77014-104">O [Power BI](http://www.powerbi.com/) é um conjunto de ferramentas de análise de negócios que ajudam a analisar dados e a compartilhar informações.</span><span class="sxs-lookup"><span data-stu-id="77014-104">[Power BI](http://www.powerbi.com/) is a suite of business analytics tools that help you analyze data and share insights.</span></span> <span data-ttu-id="77014-105">Painéis avançados estão disponíveis em cada dispositivo.</span><span class="sxs-lookup"><span data-stu-id="77014-105">Rich dashboards are available on every device.</span></span> <span data-ttu-id="77014-106">Você pode combinar dados de várias fontes, incluindo consultas do Analytics do [Azure Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="77014-106">You can combine data from many sources, including Analytics queries from [Azure Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="77014-107">Há três métodos recomendados para exportar dados do Application Insights para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="77014-107">There are three recommended methods of exporting Application Insights data to Power BI.</span></span> <span data-ttu-id="77014-108">Você pode usá-los separadamente ou em conjunto.</span><span class="sxs-lookup"><span data-stu-id="77014-108">You can use them separately or together.</span></span>

* <span data-ttu-id="77014-109">[**Adaptador do Power BI**](#power-pi-adapter) -configure um painel completo de telemetria do seu aplicativo.</span><span class="sxs-lookup"><span data-stu-id="77014-109">[**Power BI adapter**](#power-pi-adapter) - set up a complete dashboard of telemetry from your app.</span></span> <span data-ttu-id="77014-110">O conjunto de gráficos é predefinido, mas você pode adicionar suas próprias consultas de outras fontes.</span><span class="sxs-lookup"><span data-stu-id="77014-110">The set of charts is predefined, but you can add your own queries from any other sources.</span></span>
* <span data-ttu-id="77014-111">[**Exportar as consultas do Analytics**](#export-analytics-queries) -escreva qualquer consulta que quiser usando o Analytics e exporte-a para o Power BI.</span><span class="sxs-lookup"><span data-stu-id="77014-111">[**Export Analytics queries**](#export-analytics-queries) - write any query you want using Analytics, and export it to Power BI.</span></span> <span data-ttu-id="77014-112">Você pode colocar essa consulta em um painel com outros dados.</span><span class="sxs-lookup"><span data-stu-id="77014-112">You can place this query on a dashboard along with any other data.</span></span>
* <span data-ttu-id="77014-113">[**Exportação contínua e Stream Analytics**](app-insights-export-stream-analytics.md) – isso envolve mais trabalho para configurar.</span><span class="sxs-lookup"><span data-stu-id="77014-113">[**Continuous export and Stream Analytics**](app-insights-export-stream-analytics.md) - This involves more work to set up.</span></span> <span data-ttu-id="77014-114">Será útil se você quiser manter os dados por longos períodos.</span><span class="sxs-lookup"><span data-stu-id="77014-114">It is useful if you want to keep your data for long periods.</span></span> <span data-ttu-id="77014-115">Caso contrário, os outros métodos serão recomendados.</span><span class="sxs-lookup"><span data-stu-id="77014-115">Otherwise, the other methods are recommended.</span></span>

## <a name="power-bi-adapter"></a><span data-ttu-id="77014-116">Adaptador do Power BI</span><span class="sxs-lookup"><span data-stu-id="77014-116">Power BI adapter</span></span>
<span data-ttu-id="77014-117">Esse método cria um painel completo de telemetria para você.</span><span class="sxs-lookup"><span data-stu-id="77014-117">This method creates a complete dashboard of telemetry for you.</span></span> <span data-ttu-id="77014-118">O conjunto de dados inicial é predefinido, mas você pode adicionar mais dados a ele.</span><span class="sxs-lookup"><span data-stu-id="77014-118">The initial data set is predefined, but you can add more data to it.</span></span>

### <a name="get-the-adapter"></a><span data-ttu-id="77014-119">Obter o adaptador</span><span class="sxs-lookup"><span data-stu-id="77014-119">Get the adapter</span></span>
1. <span data-ttu-id="77014-120">Entre no [Power BI](https://app.powerbi.com/).</span><span class="sxs-lookup"><span data-stu-id="77014-120">Sign in to [Power BI](https://app.powerbi.com/).</span></span>
2. <span data-ttu-id="77014-121">Abra **Obter Dados**, **Serviços**, **Application Insights**</span><span class="sxs-lookup"><span data-stu-id="77014-121">Open **Get Data**, **Services**, **Application Insights**</span></span>
   
    ![Obter da fonte de dados do Application Insights](./media/app-insights-export-power-bi/power-bi-adapter.png)
3. <span data-ttu-id="77014-123">Forneça os detalhes do seu recurso Application Insights.</span><span class="sxs-lookup"><span data-stu-id="77014-123">Provide the details of your Application Insights resource.</span></span>
   
    ![Obter da fonte de dados do Application Insights](./media/app-insights-export-power-bi/azure-subscription-resource-group-name.png)
4. <span data-ttu-id="77014-125">Aguarde um minuto ou dois para que os dados sejam importados.</span><span class="sxs-lookup"><span data-stu-id="77014-125">Wait a minute or two for the data to be imported.</span></span>
   
    ![Adaptador do Power BI](./media/app-insights-export-power-bi/010.png)

<span data-ttu-id="77014-127">Você pode editar o painel, combinando os gráficos do Application Insights a outros de outras fontes e a consultas do Analytics.</span><span class="sxs-lookup"><span data-stu-id="77014-127">You can edit the dashboard, combining the Application Insights charts with those of other sources, and with Analytics queries.</span></span> <span data-ttu-id="77014-128">Há uma galeria de visualização onde você pode obter mais gráficos e cada um deles possui parâmetros que podem ser definidos.</span><span class="sxs-lookup"><span data-stu-id="77014-128">There's a visualization gallery where you can get more charts, and each chart has a parameters you can set.</span></span>

<span data-ttu-id="77014-129">Após a importação inicial, o painel e os relatórios continuarão a ser atualizados diariamente.</span><span class="sxs-lookup"><span data-stu-id="77014-129">After the initial import, the dashboard and the reports continue to update daily.</span></span> <span data-ttu-id="77014-130">Você pode controlar o agendamento de atualização no conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="77014-130">You can control the refresh schedule on the dataset.</span></span>

## <a name="export-analytics-queries"></a><span data-ttu-id="77014-131">Exportar consultas do Analytics</span><span class="sxs-lookup"><span data-stu-id="77014-131">Export Analytics queries</span></span>
<span data-ttu-id="77014-132">Essa rota permite escrever qualquer consulta do Analytics desejada e então exportá-la para um painel.</span><span class="sxs-lookup"><span data-stu-id="77014-132">This route allows you to write any Analytics query you like, and then export that to a Power BI dashboard.</span></span> <span data-ttu-id="77014-133">(Você pode adicionar ao painel criado pelo adaptador).</span><span class="sxs-lookup"><span data-stu-id="77014-133">(You can add to the dashboard created by the adapter.)</span></span>

### <a name="one-time-install-power-bi-desktop"></a><span data-ttu-id="77014-134">Uma vez: instalar o Power BI Desktop</span><span class="sxs-lookup"><span data-stu-id="77014-134">One time: install Power BI Desktop</span></span>
<span data-ttu-id="77014-135">Para importar sua consulta do Application Insights, você deve usar a versão da área de trabalho do Power BI.</span><span class="sxs-lookup"><span data-stu-id="77014-135">To import your Application Insights query, you use the desktop version of Power BI.</span></span> <span data-ttu-id="77014-136">Mas, em seguida, você poderá publicá-la na Web ou em seu espaço de trabalho de nuvem do Power BI.</span><span class="sxs-lookup"><span data-stu-id="77014-136">But then you can publish it to the web or to your Power BI cloud workspace.</span></span> 

<span data-ttu-id="77014-137">Instalar o [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span><span class="sxs-lookup"><span data-stu-id="77014-137">Install [Power BI Desktop](https://powerbi.microsoft.com/en-us/desktop/).</span></span>

### <a name="export-an-analytics-query"></a><span data-ttu-id="77014-138">Exportar uma consulta do Analytics</span><span class="sxs-lookup"><span data-stu-id="77014-138">Export an Analytics query</span></span>
1. <span data-ttu-id="77014-139">[Abra o Analytics e escreva sua consulta](app-insights-analytics-tour.md).</span><span class="sxs-lookup"><span data-stu-id="77014-139">[Open Analytics and write your query](app-insights-analytics-tour.md).</span></span>
2. <span data-ttu-id="77014-140">Teste e ajuste a consulta até ficar satisfeito com os resultados.</span><span class="sxs-lookup"><span data-stu-id="77014-140">Test and refine the query until you're happy with the results.</span></span>

   <span data-ttu-id="77014-141">**Certifique-se de que a consulta seja executada corretamente no Analytics antes de ser exportada.**</span><span class="sxs-lookup"><span data-stu-id="77014-141">**Make sure that the query runs correctly in Analytics before you export it.**</span></span>
3. <span data-ttu-id="77014-142">No menu **Exportar**, escolha **Power BI (M)**.</span><span class="sxs-lookup"><span data-stu-id="77014-142">On the **Export** menu, choose **Power BI (M)**.</span></span> <span data-ttu-id="77014-143">Salve o arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="77014-143">Save the text file.</span></span>
   
    ![Exportar a consulta do Power BI](./media/app-insights-export-power-bi/analytics-export-power-bi.png)
4. <span data-ttu-id="77014-145">No Power BI Desktop, selecione **Obter Dados, Consulta em Branco** e, então, no editor de consultas, em **Exibir**, selecione **Editor Avançado de Consultas**.</span><span class="sxs-lookup"><span data-stu-id="77014-145">In Power BI Desktop select **Get Data, Blank Query** and then in the query editor, under **View** select **Advanced Query Editor**.</span></span>

    <span data-ttu-id="77014-146">Cole o script M Language exportado no Editor Avançado de Consultas.</span><span class="sxs-lookup"><span data-stu-id="77014-146">Paste the exported M Language script into the Advanced Query Editor.</span></span>

    ![Editor avançado de consultas](./media/app-insights-export-power-bi/power-bi-import-analytics-query.png)

1. <span data-ttu-id="77014-148">Talvez seja necessário fornecer credenciais para permitir que o Power BI acesse o Azure.</span><span class="sxs-lookup"><span data-stu-id="77014-148">You might have to provide credentials to allow Power BI to access Azure.</span></span> <span data-ttu-id="77014-149">Use a ‘conta organizacional’ para entrar com sua conta da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="77014-149">Use 'organizational account' to sign in with your Microsoft account.</span></span>
   
    ![Forneça credenciais do Azure para permitir que o Power BI execute sua consulta do Application Insights](./media/app-insights-export-power-bi/power-bi-import-sign-in.png)

    <span data-ttu-id="77014-151">(Se você precisar verificar as credenciais, use o comando de menu Configurações de Fonte de Dados no Editor de Consultas.</span><span class="sxs-lookup"><span data-stu-id="77014-151">(If you need to verify the credentials, use the Data Source Settings menu command in the Query Editor.</span></span> <span data-ttu-id="77014-152">Tome cuidado para especificar as credenciais usadas para o Azure, que podem ser diferentes das suas credenciais para o Power BI.)</span><span class="sxs-lookup"><span data-stu-id="77014-152">Take care to specify the credentials you use for Azure, which might be different from your credentials for Power BI.)</span></span>
2. <span data-ttu-id="77014-153">Escolha uma visualização para a sua consulta e selecione os campos dos eixos x, y e a dimensão de segmentação.</span><span class="sxs-lookup"><span data-stu-id="77014-153">Choose a visualization for your query and select the fields for x-axis, y-axis, and segmenting dimension.</span></span>
   
    ![Selecionar visualização](./media/app-insights-export-power-bi/power-bi-analytics-visualize.png)
3. <span data-ttu-id="77014-155">Publique seu relatório em seu espaço de trabalho de nuvem do Power BI.</span><span class="sxs-lookup"><span data-stu-id="77014-155">Publish your report to your Power BI cloud workspace.</span></span> <span data-ttu-id="77014-156">A partir daí, você pode inserir uma versão sincronizada em outras páginas da Web.</span><span class="sxs-lookup"><span data-stu-id="77014-156">From there, you can embed a synchronized version into other web pages.</span></span>
   
    ![Selecionar visualização](./media/app-insights-export-power-bi/publish-power-bi.png)
4. <span data-ttu-id="77014-158">Atualize o relatório manualmente em intervalos ou configure uma atualização agendada na página de opções.</span><span class="sxs-lookup"><span data-stu-id="77014-158">Refresh the report manually at intervals, or set up a scheduled refresh on the options page.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="77014-159">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="77014-159">Troubleshooting</span></span>

### <a name="401-or-403-unauthorized"></a><span data-ttu-id="77014-160">401 ou 403 Não Autorizado</span><span class="sxs-lookup"><span data-stu-id="77014-160">401 or 403 Unauthorized</span></span> 
<span data-ttu-id="77014-161">Isso pode acontecer se o token de atualização não foi atualizado.</span><span class="sxs-lookup"><span data-stu-id="77014-161">This can happen if your refesh token has not been updated.</span></span> <span data-ttu-id="77014-162">Repita estas etapas para garantir que você ainda terá acesso.</span><span class="sxs-lookup"><span data-stu-id="77014-162">Try these steps to ensure you still have access.</span></span> <span data-ttu-id="77014-163">Se você tem acesso e a atualização das credenciais não funciona, abra um tíquete de suporte.</span><span class="sxs-lookup"><span data-stu-id="77014-163">If you do have access and refershing the credentials does not work, please open a support ticket.</span></span>

1. <span data-ttu-id="77014-164">Faça logon no Portal do Azure e certifique-se de que você pode acessar o recurso</span><span class="sxs-lookup"><span data-stu-id="77014-164">Log into the Azure Portal and make sure you can access the resource</span></span>
2. <span data-ttu-id="77014-165">Tente atualizar as credenciais para o painel</span><span class="sxs-lookup"><span data-stu-id="77014-165">Try to refresh the credentials for the Dashboard</span></span>

### <a name="502-bad-gateway"></a><span data-ttu-id="77014-166">502 Gateway Incorreto</span><span class="sxs-lookup"><span data-stu-id="77014-166">502 Bad Gateway</span></span>
<span data-ttu-id="77014-167">Isso geralmente é causado por uma Consulta de análise que retorna um número de dados excessivo.</span><span class="sxs-lookup"><span data-stu-id="77014-167">This is usually caused by an Analytics query that returns too much data.</span></span> <span data-ttu-id="77014-168">Você deve tentar usar um intervalo de tempo menor ou usar as funções [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) ou [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) apenas [projeto](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) nos campos necessários.</span><span class="sxs-lookup"><span data-stu-id="77014-168">You should try using a smaller time range or by using the [ago](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#ago) or [startofweek/startofmonth](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#startofweek) functions only [project](https://docs.microsoft.com/en-us/azure/application-insights/app-insights-analytics-reference#project-operator) the fields you need.</span></span>

<span data-ttu-id="77014-169">Se reduzir o conjunto de dados da consulta de análise não atender às suas necessidades, considere o uso da [API](https://dev.applicationinsights.io/documentation/overview) para efetuar pull de um conjunto de dados maior.</span><span class="sxs-lookup"><span data-stu-id="77014-169">If reducing the dataset coming from the Analytics query doesn't meet your requirements you should consider using the [API](https://dev.applicationinsights.io/documentation/overview) to pull a larger dataset.</span></span> <span data-ttu-id="77014-170">Aqui estão as instruções sobre como converter a exportação de consulta M para usar a API.</span><span class="sxs-lookup"><span data-stu-id="77014-170">Here are instructions on how to convert the M-Query export to use the API.</span></span>

1. <span data-ttu-id="77014-171">Criar uma [chave de API](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span><span class="sxs-lookup"><span data-stu-id="77014-171">Create an [API Key](https://dev.applicationinsights.io/documentation/Authorization/API-key-and-App-ID)</span></span>
2. <span data-ttu-id="77014-172">Atualiza o script M do Power BI que você exportou da análise, substituindo a URL do ARM pela API AI (consulte o exemplo abaixo)</span><span class="sxs-lookup"><span data-stu-id="77014-172">Update the Power BI M script that you exported from Analytics by replacing the ARM URL with AI API (see example below)</span></span>
   * <span data-ttu-id="77014-173">Substituir **https://management.azure.com/subscriptions/...**</span><span class="sxs-lookup"><span data-stu-id="77014-173">Replace **https://management.azure.com/subscriptions/...**</span></span>
   * <span data-ttu-id="77014-174">por **https://api.applicationinsights.io/beta/apps/...**</span><span class="sxs-lookup"><span data-stu-id="77014-174">with, **https://api.applicationinsights.io/beta/apps/...**</span></span>
3. <span data-ttu-id="77014-175">Finalmente, atualizar as credenciais para as básicas e usar sua chave de API</span><span class="sxs-lookup"><span data-stu-id="77014-175">Finally, update credentials to basic, and use your API Key</span></span>
  

<span data-ttu-id="77014-176">**Script existente**</span><span class="sxs-lookup"><span data-stu-id="77014-176">**Existing Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://management.azure.com/subscriptions/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx/resourcegroups//providers/microsoft.insights/components//api/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```
<span data-ttu-id="77014-177">**Script atualizado**</span><span class="sxs-lookup"><span data-stu-id="77014-177">**Updated Script**</span></span>
 ```
 Source = Json.Document(Web.Contents("https://api.applicationinsights.io/beta/apps/<APPLICATION_ID>/query?api-version=2014-12-01-preview",[Query=[#"csl"="requests",#"x-ms-app"="AAPBI"],Timeout=#duration(0,0,4,0)]))
 ```

## <a name="about-sampling"></a><span data-ttu-id="77014-178">Sobre amostragem</span><span class="sxs-lookup"><span data-stu-id="77014-178">About sampling</span></span>
<span data-ttu-id="77014-179">Se seu aplicativo enviar muitos dados, a funcionalidade de amostragem adaptável poderá operar e enviar apenas uma porcentagem da sua telemetria.</span><span class="sxs-lookup"><span data-stu-id="77014-179">If your application sends a lot of data, the adaptive sampling feature may operate and send only a percentage of your telemetry.</span></span> <span data-ttu-id="77014-180">Isso também será verdadeiro se você tiver definido manualmente a amostragem no SDK ou na ingestão.</span><span class="sxs-lookup"><span data-stu-id="77014-180">The same is true if you have manually set sampling either in the SDK or on ingestion.</span></span> [<span data-ttu-id="77014-181">Saiba mais sobre amostragem.</span><span class="sxs-lookup"><span data-stu-id="77014-181">Learn more about sampling.</span></span>](app-insights-sampling.md)


## <a name="next-steps"></a><span data-ttu-id="77014-182">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="77014-182">Next steps</span></span>
* [<span data-ttu-id="77014-183">Power BI - Saiba mais</span><span class="sxs-lookup"><span data-stu-id="77014-183">Power BI - Learn</span></span>](http://www.powerbi.com/learning/)
* [<span data-ttu-id="77014-184">Tutorial do Analytics</span><span class="sxs-lookup"><span data-stu-id="77014-184">Analytics tutorial</span></span>](app-insights-analytics-tour.md)

