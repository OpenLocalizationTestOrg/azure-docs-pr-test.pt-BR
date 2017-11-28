---
title: "aaaHow fazer … em informações de aplicativo do Azure | Microsoft Docs"
description: Perguntas Frequentes no Application Insights.
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 48b2b644-92e4-44c3-bc14-068f1bbedd22
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 04/04/2017
ms.author: bwren
ms.openlocfilehash: 89294c3583b7c4e7998143be6d359f2deb3c8f49
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="027fc-103">Como ... no Application Insights?</span><span class="sxs-lookup"><span data-stu-id="027fc-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="027fc-104">Receber um email quando...</span><span class="sxs-lookup"><span data-stu-id="027fc-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="027fc-105">Enviar emails se meu site ficar inativo</span><span class="sxs-lookup"><span data-stu-id="027fc-105">Email if my site goes down</span></span>
<span data-ttu-id="027fc-106">Definir um [teste da Web de disponibilidade](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="027fc-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="027fc-107">Enviar emails de meu site estiver sobrecarregado</span><span class="sxs-lookup"><span data-stu-id="027fc-107">Email if my site is overloaded</span></span>
<span data-ttu-id="027fc-108">Definir um [alerta](app-insights-alerts.md) para **Tempo de resposta do servidor**.</span><span class="sxs-lookup"><span data-stu-id="027fc-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="027fc-109">Um limite entre 1 e 2 segundos deve funcionar.</span><span class="sxs-lookup"><span data-stu-id="027fc-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="027fc-110">Seu aplicativo também pode mostrar sinais de sobrecarga retornando códigos de falha.</span><span class="sxs-lookup"><span data-stu-id="027fc-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="027fc-111">Definir um alerta para **Solicitações com falha**.</span><span class="sxs-lookup"><span data-stu-id="027fc-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="027fc-112">Se você quiser tooset um alerta em **exceções servidor**, talvez seja necessário toodo [alguma configuração adicional](app-insights-asp-net-exceptions.md) dados de pedidos toosee.</span><span class="sxs-lookup"><span data-stu-id="027fc-112">If you want tooset an alert on **Server exceptions**, you might have toodo [some additional setup](app-insights-asp-net-exceptions.md) in order toosee data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="027fc-113">Exceções de email</span><span class="sxs-lookup"><span data-stu-id="027fc-113">Email on exceptions</span></span>
1. [<span data-ttu-id="027fc-114">Configurar monitoramento de exceção</span><span class="sxs-lookup"><span data-stu-id="027fc-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="027fc-115">[Definir um alerta](app-insights-alerts.md) em Olá exceção contagem métrica</span><span class="sxs-lookup"><span data-stu-id="027fc-115">[Set an alert](app-insights-alerts.md) on hello Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="027fc-116">Enviar emails sobre um evento em meu aplicativo</span><span class="sxs-lookup"><span data-stu-id="027fc-116">Email on an event in my app</span></span>
<span data-ttu-id="027fc-117">Vamos supor que você gostaria que tooget um email quando ocorrer um evento específico.</span><span class="sxs-lookup"><span data-stu-id="027fc-117">Let's suppose you'd like tooget an email when a specific event occurs.</span></span> <span data-ttu-id="027fc-118">O Application Insights não oferece esse recurso diretamente, mas pode [enviar um alerta quando uma métrica ultrapassar um limite](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="027fc-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="027fc-119">Alertas podem ser definidos com base em [métricas personalizadas](app-insights-api-custom-events-metrics.md#trackmetric), mas não em eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="027fc-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="027fc-120">Grave algumas tooincrease código uma métrica quando ocorre o evento de saudação:</span><span class="sxs-lookup"><span data-stu-id="027fc-120">Write some code tooincrease a metric when hello event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="027fc-121">ou:</span><span class="sxs-lookup"><span data-stu-id="027fc-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="027fc-122">Como os alertas têm dois estados, você tem toosend um valor baixo quando você considera o alerta Olá toohave foi encerrado:</span><span class="sxs-lookup"><span data-stu-id="027fc-122">Because alerts have two states, you have toosend a low value when you consider hello alert toohave ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="027fc-123">Criar um gráfico em [explorer métrica](app-insights-metrics-explorer.md) toosee o alarme:</span><span class="sxs-lookup"><span data-stu-id="027fc-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) toosee your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="027fc-124">Agora, defina toofire um alerta quando a métrica de saudação fica acima de um valor médio por um curto período:</span><span class="sxs-lookup"><span data-stu-id="027fc-124">Now set an alert toofire when hello metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="027fc-125">Definir Olá média toohello período mínimo.</span><span class="sxs-lookup"><span data-stu-id="027fc-125">Set hello averaging period toohello minimum.</span></span>

<span data-ttu-id="027fc-126">Você receberá emails quando a métrica de saudação fica acima e abaixo do limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="027fc-126">You'll get emails both when hello metric goes above and below hello threshold.</span></span>

<span data-ttu-id="027fc-127">Tooconsider alguns pontos:</span><span class="sxs-lookup"><span data-stu-id="027fc-127">Some points tooconsider:</span></span>

* <span data-ttu-id="027fc-128">Um alerta tem dois estados ("alerta" e "íntegro").</span><span class="sxs-lookup"><span data-stu-id="027fc-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="027fc-129">estado de saudação é avaliado somente quando uma métrica é recebida.</span><span class="sxs-lookup"><span data-stu-id="027fc-129">hello state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="027fc-130">Um email é enviado apenas quando o estado de saudação é alterado.</span><span class="sxs-lookup"><span data-stu-id="027fc-130">An email is sent only when hello state changes.</span></span> <span data-ttu-id="027fc-131">Isso é porque você tem toosend métricas de alta e baixa-valor.</span><span class="sxs-lookup"><span data-stu-id="027fc-131">This is why you have toosend both high and low-value metrics.</span></span>
* <span data-ttu-id="027fc-132">alerta tooevaluate Olá média Olá é assumida de valores hello recebida Olá que precedem o período.</span><span class="sxs-lookup"><span data-stu-id="027fc-132">tooevaluate hello alert, hello average is taken of hello received values over hello preceding period.</span></span> <span data-ttu-id="027fc-133">Isso ocorre sempre que uma métrica é recebida, portanto emails podem ser enviados com mais frequência do que o período Olá definido.</span><span class="sxs-lookup"><span data-stu-id="027fc-133">This occurs every time a metric is received, so emails can be sent more frequently than hello period you set.</span></span>
* <span data-ttu-id="027fc-134">Desde que os emails são enviados na "alerta" e "Íntegro", talvez você queira tooconsider pensando novamente seu evento única como uma condição de dois estados.</span><span class="sxs-lookup"><span data-stu-id="027fc-134">Since emails are sent both on "alert" and "healthy", you might want tooconsider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="027fc-135">Por exemplo, em vez de um evento de "trabalho concluído", ter uma condição de "trabalho em andamento", onde você recebe emails no início de saudação e no final de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="027fc-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at hello start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="027fc-136">Configurar alertas automaticamente</span><span class="sxs-lookup"><span data-stu-id="027fc-136">Set up alerts automatically</span></span>
[<span data-ttu-id="027fc-137">Use o PowerShell toocreate novos alertas</span><span class="sxs-lookup"><span data-stu-id="027fc-137">Use PowerShell toocreate new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-toomanage-application-insights"></a><span data-ttu-id="027fc-138">Use o PowerShell tooManage Application Insights</span><span class="sxs-lookup"><span data-stu-id="027fc-138">Use PowerShell tooManage Application Insights</span></span>
* [<span data-ttu-id="027fc-139">Criar novos recursos</span><span class="sxs-lookup"><span data-stu-id="027fc-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="027fc-140">Criar novos alertas</span><span class="sxs-lookup"><span data-stu-id="027fc-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="027fc-141">Telemetria separada de versões diferentes</span><span class="sxs-lookup"><span data-stu-id="027fc-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="027fc-142">Várias funções em um aplicativo: use um único recurso do Application Insights e filtre cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="027fc-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="027fc-143">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="027fc-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="027fc-144">Separação de desenvolvimento, teste e versões de lançamento: usar recursos diferentes do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="027fc-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="027fc-145">Obter chaves de instrumentação de saudação do Web. config. [Saiba mais](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="027fc-145">Pick up hello instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="027fc-146">Relatando versões de build: adicionar uma propriedade usando um inicializador de telemetria.</span><span class="sxs-lookup"><span data-stu-id="027fc-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="027fc-147">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="027fc-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="027fc-148">Monitorar servidores de back-end e aplicativos de desktop</span><span class="sxs-lookup"><span data-stu-id="027fc-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="027fc-149">[Módulo de SDK do Windows Server Olá Use](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="027fc-149">[Use hello Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="027fc-150">Visualizar dados</span><span class="sxs-lookup"><span data-stu-id="027fc-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="027fc-151">Painel com métricas de vários aplicativos</span><span class="sxs-lookup"><span data-stu-id="027fc-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="027fc-152">No [Metrics Explorer](app-insights-metrics-explorer.md), personalize o gráfico e salve-o como um favorito.</span><span class="sxs-lookup"><span data-stu-id="027fc-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="027fc-153">Fixe-toohello do painel do Azure.</span><span class="sxs-lookup"><span data-stu-id="027fc-153">Pin it toohello Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="027fc-154">Painel com dados de outras fontes e Application Insights</span><span class="sxs-lookup"><span data-stu-id="027fc-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="027fc-155">[Exportar telemetria tooPower BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="027fc-155">[Export telemetry tooPower BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="027fc-156">Ou</span><span class="sxs-lookup"><span data-stu-id="027fc-156">Or</span></span>

* <span data-ttu-id="027fc-157">Use o SharePoint como seu painel e exiba dados em web parts do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="027fc-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="027fc-158">[Use a exportação contínua e análise de fluxo tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="027fc-158">[Use continuous export and Stream Analytics tooexport tooSQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="027fc-159">Usar banco de dados do PowerView tooexamine hello e criar uma web part do SharePoint para PowerView.</span><span class="sxs-lookup"><span data-stu-id="027fc-159">Use PowerView tooexamine hello database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="027fc-160">Filtrar usuários anônimos ou autenticados</span><span class="sxs-lookup"><span data-stu-id="027fc-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="027fc-161">Se os usuários se conectar, você pode definir Olá [autenticado a id de usuário](app-insights-api-custom-events-metrics.md#authenticated-users). (Isso não ocorre automaticamente.)</span><span class="sxs-lookup"><span data-stu-id="027fc-161">If your users sign in, you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="027fc-162">Você pode:</span><span class="sxs-lookup"><span data-stu-id="027fc-162">You can then:</span></span>

* <span data-ttu-id="027fc-163">Pesquisar IDs de usuário específicos</span><span class="sxs-lookup"><span data-stu-id="027fc-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="027fc-164">Filtrar usuários de autenticado ou anônimo tooeither métricas</span><span class="sxs-lookup"><span data-stu-id="027fc-164">Filter metrics tooeither anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="027fc-165">Modificar valores ou nomes de propriedade</span><span class="sxs-lookup"><span data-stu-id="027fc-165">Modify property names or values</span></span>
<span data-ttu-id="027fc-166">Crie um [filtro](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="027fc-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="027fc-167">Isso permite modificar ou filtrar telemetria antes de ser enviada de seu aplicativo tooApplication Insights.</span><span class="sxs-lookup"><span data-stu-id="027fc-167">This lets you modify or filter telemetry before it is sent from your app tooApplication Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="027fc-168">Listar usuários específicos e seu uso</span><span class="sxs-lookup"><span data-stu-id="027fc-168">List specific users and their usage</span></span>
<span data-ttu-id="027fc-169">Se você quiser apenas muito[pesquisa para usuários específicos](#search-specific-users), você pode definir Olá [autenticado a id de usuário](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="027fc-169">If you just want too[search for specific users](#search-specific-users), you can set hello [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="027fc-170">Se você quiser uma lista de usuários com os dados como, por exemplo, quais páginas eles exibem e com qual frequência eles fazem logon, você terá duas opções:</span><span class="sxs-lookup"><span data-stu-id="027fc-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="027fc-171">[Id do conjunto de usuário autenticado](app-insights-api-custom-events-metrics.md#authenticated-users), [Exportar banco de dados tooa](app-insights-code-sample-export-sql-stream-analytics.md) e uso adequado ferramentas tooanalyze seus dados de usuário.</span><span class="sxs-lookup"><span data-stu-id="027fc-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export tooa database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools tooanalyze your user data there.</span></span>
* <span data-ttu-id="027fc-172">Se você tiver somente um pequeno número de usuários, envie eventos personalizados ou métricas, usando dados de saudação de interesse como Olá valor de métrica ou o nome do evento e a id de usuário de saudação de configuração como uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="027fc-172">If you have only a small number of users, send custom events or metrics, using hello data of interest as hello metric value or event name, and setting hello user id as a property.</span></span> <span data-ttu-id="027fc-173">modos de exibição de página tooanalyze, substitua saudação padrão JavaScript trackPageView de chamada.</span><span class="sxs-lookup"><span data-stu-id="027fc-173">tooanalyze page views, replace hello standard JavaScript trackPageView call.</span></span> <span data-ttu-id="027fc-174">tooanalyze telemetria do lado do servidor, use uma telemetria inicializador tooadd Olá id tooall server telemetria do usuário.</span><span class="sxs-lookup"><span data-stu-id="027fc-174">tooanalyze server-side telemetry, use a telemetry initializer tooadd hello user id tooall server telemetry.</span></span> <span data-ttu-id="027fc-175">Você pode, em seguida, as métricas de filtro e de segmento e pesquisas na id de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="027fc-175">You can then filter and segment metrics and searches on hello user id.</span></span>

## <a name="reduce-traffic-from-my-app-tooapplication-insights"></a><span data-ttu-id="027fc-176">Reduzir o tráfego de tooApplication meu aplicativo Insights</span><span class="sxs-lookup"><span data-stu-id="027fc-176">Reduce traffic from my app tooApplication Insights</span></span>
* <span data-ttu-id="027fc-177">Em [Applicationinsights](app-insights-configuration-with-applicationinsights-config.md), desabilite quaisquer módulos que não é necessário, tal coletor de contador de desempenho de saudação.</span><span class="sxs-lookup"><span data-stu-id="027fc-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such hello performance counter collector.</span></span>
* <span data-ttu-id="027fc-178">Use [amostragem e filtragem](app-insights-api-filtering-sampling.md) em Olá SDK.</span><span class="sxs-lookup"><span data-stu-id="027fc-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at hello SDK.</span></span>
* <span data-ttu-id="027fc-179">Nas páginas da web, limite o número de saudação de chamadas Ajax relatados para cada modo de exibição de página.</span><span class="sxs-lookup"><span data-stu-id="027fc-179">In your web pages, Limit hello number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="027fc-180">No trecho de script hello após `instrumentationKey:...` , insira: `,maxAjaxCallsPerView:3` (ou um número adequado).</span><span class="sxs-lookup"><span data-stu-id="027fc-180">In hello script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="027fc-181">Se você estiver usando [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), agregação de saudação de lotes de valores da métrica de computação antes de enviar os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="027fc-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute hello aggregate of batches of metric values before sending hello result.</span></span> <span data-ttu-id="027fc-182">Há uma sobrecarga de TrackMetric() que possibilita isso.</span><span class="sxs-lookup"><span data-stu-id="027fc-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="027fc-183">Saiba mais sobre [preços e cotas](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="027fc-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="027fc-184">Desabilitar telemetria</span><span class="sxs-lookup"><span data-stu-id="027fc-184">Disable telemetry</span></span>
<span data-ttu-id="027fc-185">muito**dinamicamente parar e iniciar** Olá coleta e transmissão de telemetria do servidor de saudação:</span><span class="sxs-lookup"><span data-stu-id="027fc-185">too**dynamically stop and start** hello collection and transmission of telemetry from hello server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="027fc-186">muito**desabilitar os coletores padrão selecionados** - por exemplo, contadores de desempenho, as solicitações HTTP ou dependências - exclua ou comente linhas relevantes Olá [Applicationinsights](app-insights-api-custom-events-metrics.md). Você pode fazer isso, por exemplo, se você quiser toosend seus próprios dados TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="027fc-186">too**disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out hello relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want toosend your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="027fc-187">Exibir contadores de desempenho do sistema</span><span class="sxs-lookup"><span data-stu-id="027fc-187">View system performance counters</span></span>
<span data-ttu-id="027fc-188">Entre Olá métricas, que você pode exibir no metrics explorer são um conjunto de contadores de desempenho do sistema.</span><span class="sxs-lookup"><span data-stu-id="027fc-188">Among hello metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="027fc-189">Há uma folha predefinida intitulada **Servidores** que exibe vários deles.</span><span class="sxs-lookup"><span data-stu-id="027fc-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Abra o recurso Application Insights e clique em Servidores](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="027fc-191">Se você não vir dados do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="027fc-191">If you see no performance counter data</span></span>
* <span data-ttu-id="027fc-192">**Servidor IIS** em seu próprio computador ou em uma VM.</span><span class="sxs-lookup"><span data-stu-id="027fc-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="027fc-193">[Instalar Monitor de Status](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="027fc-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="027fc-194">**Site do Azure** - ainda não há suporte para contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="027fc-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="027fc-195">Há várias métricas, que você pode obter como parte do painel de controle do site do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="027fc-195">There are several metrics you can get as a standard part of hello Azure web site control panel.</span></span>
* <span data-ttu-id="027fc-196">**Servidor Unix** - [Instalar collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="027fc-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="toodisplay-more-performance-counters"></a><span data-ttu-id="027fc-197">toodisplay mais contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="027fc-197">toodisplay more performance counters</span></span>
* <span data-ttu-id="027fc-198">Primeiro, [adicionar um novo gráfico](app-insights-metrics-explorer.md) e veja se Olá contador em Olá básica definido que oferecemos.</span><span class="sxs-lookup"><span data-stu-id="027fc-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if hello counter is in hello basic set that we offer.</span></span>
* <span data-ttu-id="027fc-199">Caso contrário, [adicionar Olá contador toohello conjunto coletado pelo módulo do contador de desempenho de saudação](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="027fc-199">If not, [add hello counter toohello set collected by hello performance counter module](app-insights-performance-counters.md).</span></span>
