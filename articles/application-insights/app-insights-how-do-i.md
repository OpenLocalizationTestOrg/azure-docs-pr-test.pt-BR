---
title: Como... no Azure Application Insights | Microsoft Docs
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
ms.openlocfilehash: ef63e06c0621753e0a706d6efb709b943e38ee42
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="how-do-i--in-application-insights"></a><span data-ttu-id="e8146-103">Como ... no Application Insights?</span><span class="sxs-lookup"><span data-stu-id="e8146-103">How do I ... in Application Insights?</span></span>
## <a name="get-an-email-when-"></a><span data-ttu-id="e8146-104">Receber um email quando...</span><span class="sxs-lookup"><span data-stu-id="e8146-104">Get an email when ...</span></span>
### <a name="email-if-my-site-goes-down"></a><span data-ttu-id="e8146-105">Enviar emails se meu site ficar inativo</span><span class="sxs-lookup"><span data-stu-id="e8146-105">Email if my site goes down</span></span>
<span data-ttu-id="e8146-106">Definir um [teste da Web de disponibilidade](app-insights-monitor-web-app-availability.md).</span><span class="sxs-lookup"><span data-stu-id="e8146-106">Set an [availability web test](app-insights-monitor-web-app-availability.md).</span></span>

### <a name="email-if-my-site-is-overloaded"></a><span data-ttu-id="e8146-107">Enviar emails de meu site estiver sobrecarregado</span><span class="sxs-lookup"><span data-stu-id="e8146-107">Email if my site is overloaded</span></span>
<span data-ttu-id="e8146-108">Definir um [alerta](app-insights-alerts.md) para **Tempo de resposta do servidor**.</span><span class="sxs-lookup"><span data-stu-id="e8146-108">Set an [alert](app-insights-alerts.md) on **Server response time**.</span></span> <span data-ttu-id="e8146-109">Um limite entre 1 e 2 segundos deve funcionar.</span><span class="sxs-lookup"><span data-stu-id="e8146-109">A threshold between 1 and 2 seconds should work.</span></span>

![](./media/app-insights-how-do-i/030-server.png)

<span data-ttu-id="e8146-110">Seu aplicativo também pode mostrar sinais de sobrecarga retornando códigos de falha.</span><span class="sxs-lookup"><span data-stu-id="e8146-110">Your app might also show signs of strain by returning failure codes.</span></span> <span data-ttu-id="e8146-111">Definir um alerta para **Solicitações com falha**.</span><span class="sxs-lookup"><span data-stu-id="e8146-111">Set an alert on **Failed requests**.</span></span>

<span data-ttu-id="e8146-112">Se definir um alerta para **Exceções do servidor**, talvez você precise fazer [algumas configurações adicionais](app-insights-asp-net-exceptions.md) para ver os dados.</span><span class="sxs-lookup"><span data-stu-id="e8146-112">If you want to set an alert on **Server exceptions**, you might have to do [some additional setup](app-insights-asp-net-exceptions.md) in order to see data.</span></span>

### <a name="email-on-exceptions"></a><span data-ttu-id="e8146-113">Exceções de email</span><span class="sxs-lookup"><span data-stu-id="e8146-113">Email on exceptions</span></span>
1. [<span data-ttu-id="e8146-114">Configurar monitoramento de exceção</span><span class="sxs-lookup"><span data-stu-id="e8146-114">Set up exception monitoring</span></span>](app-insights-asp-net-exceptions.md)
2. <span data-ttu-id="e8146-115">[Definir um alerta](app-insights-alerts.md) na métrica de contagem de exceção</span><span class="sxs-lookup"><span data-stu-id="e8146-115">[Set an alert](app-insights-alerts.md) on the Exception count metric</span></span>

### <a name="email-on-an-event-in-my-app"></a><span data-ttu-id="e8146-116">Enviar emails sobre um evento em meu aplicativo</span><span class="sxs-lookup"><span data-stu-id="e8146-116">Email on an event in my app</span></span>
<span data-ttu-id="e8146-117">Vamos supor que você gostaria de receber um email quando ocorrer um evento específico.</span><span class="sxs-lookup"><span data-stu-id="e8146-117">Let's suppose you'd like to get an email when a specific event occurs.</span></span> <span data-ttu-id="e8146-118">O Application Insights não oferece esse recurso diretamente, mas pode [enviar um alerta quando uma métrica ultrapassar um limite](app-insights-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="e8146-118">Application Insights doesn't provide this facility directly, but it can [send an alert when a metric crosses a threshold](app-insights-alerts.md).</span></span>

<span data-ttu-id="e8146-119">Alertas podem ser definidos com base em [métricas personalizadas](app-insights-api-custom-events-metrics.md#trackmetric), mas não em eventos personalizados.</span><span class="sxs-lookup"><span data-stu-id="e8146-119">Alerts can be set on [custom metrics](app-insights-api-custom-events-metrics.md#trackmetric), though not custom events.</span></span> <span data-ttu-id="e8146-120">Escreva algum código para aumentar uma métrica quando o evento ocorre:</span><span class="sxs-lookup"><span data-stu-id="e8146-120">Write some code to increase a metric when the event occurs:</span></span>

    telemetry.TrackMetric("Alarm", 10);

<span data-ttu-id="e8146-121">ou:</span><span class="sxs-lookup"><span data-stu-id="e8146-121">or:</span></span>

    var measurements = new Dictionary<string,double>();
    measurements ["Alarm"] = 10;
    telemetry.TrackEvent("status", null, measurements);

<span data-ttu-id="e8146-122">Como os alertas têm dois estados, você precisa enviar um valor baixo quando considerar o alerta concluído:</span><span class="sxs-lookup"><span data-stu-id="e8146-122">Because alerts have two states, you have to send a low value when you consider the alert to have ended:</span></span>

    telemetry.TrackMetric("Alarm", 0.5);

<span data-ttu-id="e8146-123">Crie um gráfico no [Metrics Explorer](app-insights-metrics-explorer.md) para ver o alarme:</span><span class="sxs-lookup"><span data-stu-id="e8146-123">Create a chart in [metric explorer](app-insights-metrics-explorer.md) to see your alarm:</span></span>

![](./media/app-insights-how-do-i/010-alarm.png)

<span data-ttu-id="e8146-124">Agora defina um alerta para ser disparado quando a métrica ultrapassar um valor médio por um curto período:</span><span class="sxs-lookup"><span data-stu-id="e8146-124">Now set an alert to fire when the metric goes above a mid value for a short period:</span></span>

![](./media/app-insights-how-do-i/020-threshold.png)

<span data-ttu-id="e8146-125">Defina o período de média como o mínimo.</span><span class="sxs-lookup"><span data-stu-id="e8146-125">Set the averaging period to the minimum.</span></span>

<span data-ttu-id="e8146-126">Quando a métrica ficar acima e abaixo do limite, você receberá emails.</span><span class="sxs-lookup"><span data-stu-id="e8146-126">You'll get emails both when the metric goes above and below the threshold.</span></span>

<span data-ttu-id="e8146-127">Considere o seguinte:</span><span class="sxs-lookup"><span data-stu-id="e8146-127">Some points to consider:</span></span>

* <span data-ttu-id="e8146-128">Um alerta tem dois estados ("alerta" e "íntegro").</span><span class="sxs-lookup"><span data-stu-id="e8146-128">An alert has two states ("alert" and "healthy").</span></span> <span data-ttu-id="e8146-129">O estado é avaliado somente quando uma métrica é recebida.</span><span class="sxs-lookup"><span data-stu-id="e8146-129">The state is evaluated only when a metric is received.</span></span>
* <span data-ttu-id="e8146-130">Um email é enviado apenas quando o estado é alterado.</span><span class="sxs-lookup"><span data-stu-id="e8146-130">An email is sent only when the state changes.</span></span> <span data-ttu-id="e8146-131">Por isso você precisa enviar métricas de valor alto e baixo.</span><span class="sxs-lookup"><span data-stu-id="e8146-131">This is why you have to send both high and low-value metrics.</span></span>
* <span data-ttu-id="e8146-132">Para avaliar o alerta, a média é calculada com base dos valores recebidos no período anterior.</span><span class="sxs-lookup"><span data-stu-id="e8146-132">To evaluate the alert, the average is taken of the received values over the preceding period.</span></span> <span data-ttu-id="e8146-133">Isso ocorre sempre que uma métrica é recebida, para que emails podem ser enviados com mais frequência do que o período definido.</span><span class="sxs-lookup"><span data-stu-id="e8146-133">This occurs every time a metric is received, so emails can be sent more frequently than the period you set.</span></span>
* <span data-ttu-id="e8146-134">Uma vez que os emails são enviados tanto para "alerta" quanto para "íntegro", convém passar a pensar em seu único como uma condição de dois estados.</span><span class="sxs-lookup"><span data-stu-id="e8146-134">Since emails are sent both on "alert" and "healthy", you might want to consider re-thinking your one-shot event as a two-state condition.</span></span> <span data-ttu-id="e8146-135">Por exemplo, em vez de um evento de "trabalho concluído", tenha uma condição de "trabalho em andamento", na qual você recebe emails no início e no final de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="e8146-135">For example, instead of a "job completed" event, have a "job in progress" condition, where you get emails at the start and end of a job.</span></span>

### <a name="set-up-alerts-automatically"></a><span data-ttu-id="e8146-136">Configurar alertas automaticamente</span><span class="sxs-lookup"><span data-stu-id="e8146-136">Set up alerts automatically</span></span>
[<span data-ttu-id="e8146-137">Usar o PowerShell para criar novos alertas</span><span class="sxs-lookup"><span data-stu-id="e8146-137">Use PowerShell to create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="use-powershell-to-manage-application-insights"></a><span data-ttu-id="e8146-138">Usar o PowerShell para gerenciar o Application Insights</span><span class="sxs-lookup"><span data-stu-id="e8146-138">Use PowerShell to Manage Application Insights</span></span>
* [<span data-ttu-id="e8146-139">Criar novos recursos</span><span class="sxs-lookup"><span data-stu-id="e8146-139">Create new resources</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="e8146-140">Criar novos alertas</span><span class="sxs-lookup"><span data-stu-id="e8146-140">Create new alerts</span></span>](app-insights-alerts.md#automation)

## <a name="separate-telemetry-from-different-versions"></a><span data-ttu-id="e8146-141">Telemetria separada de versões diferentes</span><span class="sxs-lookup"><span data-stu-id="e8146-141">Separate telemetry from different versions</span></span>

* <span data-ttu-id="e8146-142">Várias funções em um aplicativo: use um único recurso do Application Insights e filtre cloud_Rolename.</span><span class="sxs-lookup"><span data-stu-id="e8146-142">Multiple roles in an app: Use a single Application Insights resource, and filter on cloud_Rolename.</span></span> [<span data-ttu-id="e8146-143">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="e8146-143">Learn more</span></span>](app-insights-monitor-multi-role-apps.md)
* <span data-ttu-id="e8146-144">Separação de desenvolvimento, teste e versões de lançamento: usar recursos diferentes do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e8146-144">Separating development, test, and release versions: Use different Application Insights resources.</span></span> <span data-ttu-id="e8146-145">Pegue as chaves de instrumentação do web.config. [Saiba mais](app-insights-separate-resources.md)</span><span class="sxs-lookup"><span data-stu-id="e8146-145">Pick up the instrumentation keys from web.config. [Learn more](app-insights-separate-resources.md)</span></span>
* <span data-ttu-id="e8146-146">Relatando versões de build: adicionar uma propriedade usando um inicializador de telemetria.</span><span class="sxs-lookup"><span data-stu-id="e8146-146">Reporting build versions: Add a property using a telemetry initializer.</span></span> [<span data-ttu-id="e8146-147">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="e8146-147">Learn more</span></span>](app-insights-separate-resources.md)

## <a name="monitor-backend-servers-and-desktop-apps"></a><span data-ttu-id="e8146-148">Monitorar servidores de back-end e aplicativos de desktop</span><span class="sxs-lookup"><span data-stu-id="e8146-148">Monitor backend servers and desktop apps</span></span>
<span data-ttu-id="e8146-149">[Use o módulo do SDK do Windows Server](app-insights-windows-desktop.md).</span><span class="sxs-lookup"><span data-stu-id="e8146-149">[Use the Windows Server SDK module](app-insights-windows-desktop.md).</span></span>

## <a name="visualize-data"></a><span data-ttu-id="e8146-150">Visualizar dados</span><span class="sxs-lookup"><span data-stu-id="e8146-150">Visualize data</span></span>
#### <a name="dashboard-with-metrics-from-multiple-apps"></a><span data-ttu-id="e8146-151">Painel com métricas de vários aplicativos</span><span class="sxs-lookup"><span data-stu-id="e8146-151">Dashboard with metrics from multiple apps</span></span>
* <span data-ttu-id="e8146-152">No [Metrics Explorer](app-insights-metrics-explorer.md), personalize o gráfico e salve-o como um favorito.</span><span class="sxs-lookup"><span data-stu-id="e8146-152">In [Metric Explorer](app-insights-metrics-explorer.md), customize your chart and save it as a favorite.</span></span> <span data-ttu-id="e8146-153">Fixe-o no painel do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8146-153">Pin it to the Azure dashboard.</span></span>

#### <a name="dashboard-with-data-from-other-sources-and-application-insights"></a><span data-ttu-id="e8146-154">Painel com dados de outras fontes e Application Insights</span><span class="sxs-lookup"><span data-stu-id="e8146-154">Dashboard with data from other sources and Application Insights</span></span>
* <span data-ttu-id="e8146-155">[Exportar telemetria para o Power BI](app-insights-export-power-bi.md).</span><span class="sxs-lookup"><span data-stu-id="e8146-155">[Export telemetry to Power BI](app-insights-export-power-bi.md).</span></span>

<span data-ttu-id="e8146-156">Ou</span><span class="sxs-lookup"><span data-stu-id="e8146-156">Or</span></span>

* <span data-ttu-id="e8146-157">Use o SharePoint como seu painel e exiba dados em web parts do SharePoint.</span><span class="sxs-lookup"><span data-stu-id="e8146-157">Use SharePoint as your dashboard, displaying data in SharePoint web parts.</span></span> <span data-ttu-id="e8146-158">[Usar exportação contínua e Stream Analytics para exportar para o SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span><span class="sxs-lookup"><span data-stu-id="e8146-158">[Use continuous export and Stream Analytics to export to SQL](app-insights-code-sample-export-sql-stream-analytics.md).</span></span>  <span data-ttu-id="e8146-159">Use o PowerView para examinar o banco de dados e criar uma web part do SharePoint para o PowerView.</span><span class="sxs-lookup"><span data-stu-id="e8146-159">Use PowerView to examine the database, and create a SharePoint web part for PowerView.</span></span>

<a name="search-specific-users"></a>

### <a name="filter-out-anonymous-or-authenticated-users"></a><span data-ttu-id="e8146-160">Filtrar usuários anônimos ou autenticados</span><span class="sxs-lookup"><span data-stu-id="e8146-160">Filter out anonymous or authenticated users</span></span>
<span data-ttu-id="e8146-161">Se os seus usuários se conectarem, você poderá definir a [ID de usuário autenticado](app-insights-api-custom-events-metrics.md#authenticated-users). (Isso não ocorre automaticamente.)</span><span class="sxs-lookup"><span data-stu-id="e8146-161">If your users sign in, you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users). (It doesn't happen automatically.)</span></span>

<span data-ttu-id="e8146-162">Você pode:</span><span class="sxs-lookup"><span data-stu-id="e8146-162">You can then:</span></span>

* <span data-ttu-id="e8146-163">Pesquisar IDs de usuário específicos</span><span class="sxs-lookup"><span data-stu-id="e8146-163">Search on specific user ids</span></span>

![](./media/app-insights-how-do-i/110-search.png)

* <span data-ttu-id="e8146-164">Filtrar métricas para usuários anônimos ou autenticados</span><span class="sxs-lookup"><span data-stu-id="e8146-164">Filter metrics to either anonymous or authenticated users</span></span>

![](./media/app-insights-how-do-i/115-metrics.png)

## <a name="modify-property-names-or-values"></a><span data-ttu-id="e8146-165">Modificar valores ou nomes de propriedade</span><span class="sxs-lookup"><span data-stu-id="e8146-165">Modify property names or values</span></span>
<span data-ttu-id="e8146-166">Crie um [filtro](app-insights-api-filtering-sampling.md#filtering).</span><span class="sxs-lookup"><span data-stu-id="e8146-166">Create a [filter](app-insights-api-filtering-sampling.md#filtering).</span></span> <span data-ttu-id="e8146-167">Isso permite modificar ou filtrar a telemetria antes que ela seja enviada do seu aplicativo para o Application Insights.</span><span class="sxs-lookup"><span data-stu-id="e8146-167">This lets you modify or filter telemetry before it is sent from your app to Application Insights.</span></span>

## <a name="list-specific-users-and-their-usage"></a><span data-ttu-id="e8146-168">Listar usuários específicos e seu uso</span><span class="sxs-lookup"><span data-stu-id="e8146-168">List specific users and their usage</span></span>
<span data-ttu-id="e8146-169">Se desejar apenas [pesquisar usuários específicos](#search-specific-users), poderá definir a [ID de usuário autenticado](app-insights-api-custom-events-metrics.md#authenticated-users).</span><span class="sxs-lookup"><span data-stu-id="e8146-169">If you just want to [search for specific users](#search-specific-users), you can set the [authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users).</span></span>

<span data-ttu-id="e8146-170">Se você quiser uma lista de usuários com os dados como, por exemplo, quais páginas eles exibem e com qual frequência eles fazem logon, você terá duas opções:</span><span class="sxs-lookup"><span data-stu-id="e8146-170">If you want a list of users with data such as what pages they look at or how often they log in, you have two options:</span></span>

* <span data-ttu-id="e8146-171">[Defina a ID de usuário autenticado](app-insights-api-custom-events-metrics.md#authenticated-users), [exporte para um banco de dados](app-insights-code-sample-export-sql-stream-analytics.md) e use ferramentas adequadas para analisar seus dados de usuário.</span><span class="sxs-lookup"><span data-stu-id="e8146-171">[Set authenticated user id](app-insights-api-custom-events-metrics.md#authenticated-users), [export to a database](app-insights-code-sample-export-sql-stream-analytics.md) and use suitable tools to analyze your user data there.</span></span>
* <span data-ttu-id="e8146-172">Se você tiver apenas um pequeno número de usuários, envie métricas ou eventos personalizados usando os dados de interesse, como o valor da métrica ou o nome do evento, definindo a ID de usuário como uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="e8146-172">If you have only a small number of users, send custom events or metrics, using the data of interest as the metric value or event name, and setting the user id as a property.</span></span> <span data-ttu-id="e8146-173">Para analisar os modos de exibição de página, substitua a chamada trackPageView JavaScript padrão.</span><span class="sxs-lookup"><span data-stu-id="e8146-173">To analyze page views, replace the standard JavaScript trackPageView call.</span></span> <span data-ttu-id="e8146-174">Para analisar a telemetria do lado do servidor, use um inicializador de telemetria para adicionar a ID de usuário a todas as telemetria do servidor.</span><span class="sxs-lookup"><span data-stu-id="e8146-174">To analyze server-side telemetry, use a telemetry initializer to add the user id to all server telemetry.</span></span> <span data-ttu-id="e8146-175">Em seguida, filtre e segmente as métricas e pesquisas na ID de usuário.</span><span class="sxs-lookup"><span data-stu-id="e8146-175">You can then filter and segment metrics and searches on the user id.</span></span>

## <a name="reduce-traffic-from-my-app-to-application-insights"></a><span data-ttu-id="e8146-176">Reduzir o tráfego do meu aplicativo no Application Insights</span><span class="sxs-lookup"><span data-stu-id="e8146-176">Reduce traffic from my app to Application Insights</span></span>
* <span data-ttu-id="e8146-177">Em [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), desabilite todos os módulos dos quais você não precisa, como o coletor do contador de desempenho.</span><span class="sxs-lookup"><span data-stu-id="e8146-177">In [ApplicationInsights.config](app-insights-configuration-with-applicationinsights-config.md), disable any modules you don't need, such the performance counter collector.</span></span>
* <span data-ttu-id="e8146-178">Use a [Amostragem e filtragem](app-insights-api-filtering-sampling.md) no SDK.</span><span class="sxs-lookup"><span data-stu-id="e8146-178">Use [Sampling and filtering](app-insights-api-filtering-sampling.md) at the SDK.</span></span>
* <span data-ttu-id="e8146-179">Nas páginas da Web, limite o número de chamadas do Ajax relatadas para cada exibição de página.</span><span class="sxs-lookup"><span data-stu-id="e8146-179">In your web pages, Limit the number of Ajax calls reported for every page view.</span></span> <span data-ttu-id="e8146-180">No trecho de script após `instrumentationKey:...`, insira: `,maxAjaxCallsPerView:3` (ou um número adequado).</span><span class="sxs-lookup"><span data-stu-id="e8146-180">In the script snippet after `instrumentationKey:...` , insert: `,maxAjaxCallsPerView:3` (or a suitable number).</span></span>
* <span data-ttu-id="e8146-181">Se estiver usando o [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), calcule a agregação de lotes de valores de métrica antes de enviar o resultado.</span><span class="sxs-lookup"><span data-stu-id="e8146-181">If you're using [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric), compute the aggregate of batches of metric values before sending the result.</span></span> <span data-ttu-id="e8146-182">Há uma sobrecarga de TrackMetric() que possibilita isso.</span><span class="sxs-lookup"><span data-stu-id="e8146-182">There's an overload of TrackMetric() that provides for that.</span></span>

<span data-ttu-id="e8146-183">Saiba mais sobre [preços e cotas](app-insights-pricing.md).</span><span class="sxs-lookup"><span data-stu-id="e8146-183">Learn more about [pricing and quotas](app-insights-pricing.md).</span></span>

## <a name="disable-telemetry"></a><span data-ttu-id="e8146-184">Desabilitar telemetria</span><span class="sxs-lookup"><span data-stu-id="e8146-184">Disable telemetry</span></span>
<span data-ttu-id="e8146-185">Para **parar e iniciar dinamicamente** a coleta e a transmissão de telemetria do servidor:</span><span class="sxs-lookup"><span data-stu-id="e8146-185">To **dynamically stop and start** the collection and transmission of telemetry from the server:</span></span>

```

    using  Microsoft.ApplicationInsights.Extensibility;

    TelemetryConfiguration.Active.DisableTelemetry = true;
```



<span data-ttu-id="e8146-186">Para **desabilitar os coletores padrão selecionados** - por exemplo, contadores de desempenho, solicitações HTTP ou dependências - exclua ou comente as linhas relevantes em [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). Você poderá fazer isso, por exemplo, se quiser enviar seus próprios dados de TrackRequest.</span><span class="sxs-lookup"><span data-stu-id="e8146-186">To **disable selected standard collectors** - for example, performance counters, HTTP requests, or dependencies - delete or comment out the relevant lines in [ApplicationInsights.config](app-insights-api-custom-events-metrics.md). You could do this, for example, if you want to send your own TrackRequest data.</span></span>

## <a name="view-system-performance-counters"></a><span data-ttu-id="e8146-187">Exibir contadores de desempenho do sistema</span><span class="sxs-lookup"><span data-stu-id="e8146-187">View system performance counters</span></span>
<span data-ttu-id="e8146-188">Entre as métricas que você pode exibir no Metrics Explorer, existe um conjunto de contadores de desempenho do sistema.</span><span class="sxs-lookup"><span data-stu-id="e8146-188">Among the metrics you can show in metrics explorer are a set of system performance counters.</span></span> <span data-ttu-id="e8146-189">Há uma folha predefinida intitulada **Servidores** que exibe vários deles.</span><span class="sxs-lookup"><span data-stu-id="e8146-189">There's a predefined blade titled **Servers** that displays several of them.</span></span>

![Abra o recurso Application Insights e clique em Servidores](./media/app-insights-how-do-i/121-servers.png)

### <a name="if-you-see-no-performance-counter-data"></a><span data-ttu-id="e8146-191">Se você não vir dados do contador de desempenho</span><span class="sxs-lookup"><span data-stu-id="e8146-191">If you see no performance counter data</span></span>
* <span data-ttu-id="e8146-192">**Servidor IIS** em seu próprio computador ou em uma VM.</span><span class="sxs-lookup"><span data-stu-id="e8146-192">**IIS server** on your own machine or on a VM.</span></span> <span data-ttu-id="e8146-193">[Instalar Monitor de Status](app-insights-monitor-performance-live-website-now.md).</span><span class="sxs-lookup"><span data-stu-id="e8146-193">[Install Status Monitor](app-insights-monitor-performance-live-website-now.md).</span></span>
* <span data-ttu-id="e8146-194">**Site do Azure** - ainda não há suporte para contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="e8146-194">**Azure web site** - we don't support performance counters yet.</span></span> <span data-ttu-id="e8146-195">Existem várias métricas que você pode obter como parte padrão do painel de controle do site do Azure.</span><span class="sxs-lookup"><span data-stu-id="e8146-195">There are several metrics you can get as a standard part of the Azure web site control panel.</span></span>
* <span data-ttu-id="e8146-196">**Servidor Unix** - [Instalar collectd](app-insights-java-collectd.md)</span><span class="sxs-lookup"><span data-stu-id="e8146-196">**Unix server** - [Install collectd](app-insights-java-collectd.md)</span></span>

### <a name="to-display-more-performance-counters"></a><span data-ttu-id="e8146-197">Para exibir mais contadores de desempenho</span><span class="sxs-lookup"><span data-stu-id="e8146-197">To display more performance counters</span></span>
* <span data-ttu-id="e8146-198">Primeiro, [adicione um novo gráfico](app-insights-metrics-explorer.md) e veja se o contador está no conjunto básico que oferecemos.</span><span class="sxs-lookup"><span data-stu-id="e8146-198">First, [add a new chart](app-insights-metrics-explorer.md) and see if the counter is in the basic set that we offer.</span></span>
* <span data-ttu-id="e8146-199">Caso contrário, [adicione o contador ao conjunto coletado pelo módulo do contador de desempenho](app-insights-performance-counters.md).</span><span class="sxs-lookup"><span data-stu-id="e8146-199">If not, [add the counter to the set collected by the performance counter module](app-insights-performance-counters.md).</span></span>
