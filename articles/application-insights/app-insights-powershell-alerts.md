---
title: Usar o PowerShell para configurar alertas no Application Insights | Microsoft Docs
description: "Automatize a configuração do Application Insights para receber emails sobre alterações de métricas."
services: application-insights
documentationcenter: 
author: CFreemanwa
manager: carmonm
ms.assetid: 05d6a9e0-77a2-4a35-9052-a7768d23a196
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: 64675c51abf80daa3a55220f910aa8fdee1042ca
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="use-powershell-to-set-alerts-in-application-insights"></a><span data-ttu-id="43e97-103">Usar o PowerShell para configurar alertas no Application Insights</span><span class="sxs-lookup"><span data-stu-id="43e97-103">Use PowerShell to set alerts in Application Insights</span></span>
<span data-ttu-id="43e97-104">Você pode automatizar a configuração de [alertas](app-insights-alerts.md) no [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="43e97-104">You can automate the configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="43e97-105">Além disso, você pode [definir webhooks para automatizar sua resposta a um alerta](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="43e97-105">In addition, you can [set webhooks to automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="43e97-106">Se você quiser criar alertas e recursos ao mesmo tempo, considere [usar um modelo do Azure Resource Manager](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="43e97-106">If you want to create resources and alerts at the same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="43e97-107">Configuração única</span><span class="sxs-lookup"><span data-stu-id="43e97-107">One-time setup</span></span>
<span data-ttu-id="43e97-108">Se você nunca usou o PowerShell com sua assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="43e97-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="43e97-109">Instale o módulo do Azure Powershell no computador em que você deseja executar os scripts.</span><span class="sxs-lookup"><span data-stu-id="43e97-109">Install the Azure Powershell module on the machine where you want to run the scripts.</span></span>

* <span data-ttu-id="43e97-110">Instale o [Microsoft Web Platform Installer (v5 ou superior)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="43e97-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="43e97-111">Use-o para instalar o Microsoft Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="43e97-111">Use it to install Microsoft Azure Powershell</span></span>

## <a name="connect-to-azure"></a><span data-ttu-id="43e97-112">Conecte-se ao Azure</span><span class="sxs-lookup"><span data-stu-id="43e97-112">Connect to Azure</span></span>
<span data-ttu-id="43e97-113">Inicie o Azure PowerShell e [conecte-se à sua assinatura](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="43e97-113">Start Azure PowerShell and [connect to your subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="43e97-114">Obter alertas</span><span class="sxs-lookup"><span data-stu-id="43e97-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="43e97-115">Adicionar alerta</span><span class="sxs-lookup"><span data-stu-id="43e97-115">Add alert</span></span>
    Add-AlertRule  -Name "{ALERT NAME}" -Description "{TEXT}" `
     -ResourceGroup "{GROUP NAME}" `
     -ResourceId "/subscriptions/{SUBSCRIPTION ID}/resourcegroups/{GROUP NAME}/providers/microsoft.insights/components/{APP RESOURCE NAME}" `
     -MetricName "{METRIC NAME}" `
     -Operator GreaterThan  `
     -Threshold {NUMBER}   `
     -WindowSize {HH:MM:SS}  `
     [-SendEmailToServiceOwners] `
     [-CustomEmails "EMAIL1@X.COM","EMAIL2@Y.COM" ] `
     -Location "East US" // must be East US at present
     -RuleType Metric



## <a name="example-1"></a><span data-ttu-id="43e97-116">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="43e97-116">Example 1</span></span>
<span data-ttu-id="43e97-117">Enviar email se a resposta do servidor às solicitações HTTP, em média no prazo de 5 minutos, demorar mais de 1 segundo.</span><span class="sxs-lookup"><span data-stu-id="43e97-117">Email me if the server's response to HTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="43e97-118">Meu recurso Application Insights é chamado IceCreamWebApp e está no grupo de recursos Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="43e97-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="43e97-119">Sou o proprietário da assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="43e97-119">I am the owner of the Azure subscription.</span></span>

<span data-ttu-id="43e97-120">O GUID é a ID da assinatura (não a chave de instrumentação do aplicativo).</span><span class="sxs-lookup"><span data-stu-id="43e97-120">The GUID is the subscription ID (not the instrumentation key of the application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if the server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="43e97-121">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="43e97-121">Example 2</span></span>
<span data-ttu-id="43e97-122">Tenho um aplicativo em que uso o [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) para relatar uma métrica chamada "salesPerHour".</span><span class="sxs-lookup"><span data-stu-id="43e97-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) to report a metric named "salesPerHour."</span></span> <span data-ttu-id="43e97-123">Envie um email para meus colegas se "salesPerHour" cair abaixo de 100, em média no prazo de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="43e97-123">Send an email to my colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

    Add-AlertRule -Name "poor sales" `
     -Description "slow sales alert" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "salesPerHour" `
     -Operator LessThan `
     -Threshold 100 `
     -WindowSize 24:00:00 `
     -CustomEmails "satish@fabrikam.com","lei@fabrikam.com" `
     -Location "East US" -RuleType Metric

<span data-ttu-id="43e97-124">A mesma regra pode ser usada para a métrica relatada usando o [parâmetro de medida](app-insights-api-custom-events-metrics.md#properties) de outra chamada de controle, como TrackEvent ou trackPageView.</span><span class="sxs-lookup"><span data-stu-id="43e97-124">The same rule can be used for the metric reported by using the [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="43e97-125">Nomes de métrica</span><span class="sxs-lookup"><span data-stu-id="43e97-125">Metric names</span></span>
| <span data-ttu-id="43e97-126">Nome da métrica</span><span class="sxs-lookup"><span data-stu-id="43e97-126">Metric name</span></span> | <span data-ttu-id="43e97-127">Nome da tela</span><span class="sxs-lookup"><span data-stu-id="43e97-127">Screen name</span></span> | <span data-ttu-id="43e97-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="43e97-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="43e97-129">Exceções de navegador</span><span class="sxs-lookup"><span data-stu-id="43e97-129">Browser exceptions</span></span> |<span data-ttu-id="43e97-130">Contagem de exceções não identificadas lançadas no navegador.</span><span class="sxs-lookup"><span data-stu-id="43e97-130">Count of uncaught exceptions thrown in the browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="43e97-131">Exceções do servidor</span><span class="sxs-lookup"><span data-stu-id="43e97-131">Server exceptions</span></span> |<span data-ttu-id="43e97-132">Contagem de exceções sem tratamento lançadas pelo aplicativo</span><span class="sxs-lookup"><span data-stu-id="43e97-132">Count of unhandled exceptions thrown by the app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="43e97-133">Tempo de processamento do cliente</span><span class="sxs-lookup"><span data-stu-id="43e97-133">Client processing time</span></span> |<span data-ttu-id="43e97-134">Tempo entre o recebimento do último byte de um documento até que o DOM seja carregado.</span><span class="sxs-lookup"><span data-stu-id="43e97-134">Time between receiving the last byte of a document until the DOM is loaded.</span></span> <span data-ttu-id="43e97-135">As solicitações assíncronas ainda podem estar sendo processadas.</span><span class="sxs-lookup"><span data-stu-id="43e97-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="43e97-136">Tempo de conexão de rede de carregamento de página</span><span class="sxs-lookup"><span data-stu-id="43e97-136">Page load network connect time</span></span> |<span data-ttu-id="43e97-137">Tempo que leva para o navegador se conectar à rede.</span><span class="sxs-lookup"><span data-stu-id="43e97-137">Time the browser takes to connect to the network.</span></span> <span data-ttu-id="43e97-138">Pode ser 0 se armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="43e97-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="43e97-139">Tempo de resposta de recebimento</span><span class="sxs-lookup"><span data-stu-id="43e97-139">Receiving response time</span></span> |<span data-ttu-id="43e97-140">Tempo entre o envio da solicitação do navegador e o início do recebimento de resposta.</span><span class="sxs-lookup"><span data-stu-id="43e97-140">Time between browser sending request to starting to receive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="43e97-141">Tempo de solicitação de envio</span><span class="sxs-lookup"><span data-stu-id="43e97-141">Send request time</span></span> |<span data-ttu-id="43e97-142">Tempo gasto pelo navegador para enviar a solicitação.</span><span class="sxs-lookup"><span data-stu-id="43e97-142">Time taken by browser to send request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="43e97-143">Tempo de carregamento de página do navegador</span><span class="sxs-lookup"><span data-stu-id="43e97-143">Browser page load time</span></span> |<span data-ttu-id="43e97-144">Tempo de solicitação do usuário até que o DOM, as imagens, os scripts e as folhas de estilo sejam carregados.</span><span class="sxs-lookup"><span data-stu-id="43e97-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="43e97-145">Memória disponível</span><span class="sxs-lookup"><span data-stu-id="43e97-145">Available memory</span></span> |<span data-ttu-id="43e97-146">Memória física disponível imediatamente para um processo ou para uso do sistema.</span><span class="sxs-lookup"><span data-stu-id="43e97-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="43e97-147">Taxa de processamento de IO</span><span class="sxs-lookup"><span data-stu-id="43e97-147">Process IO Rate</span></span> |<span data-ttu-id="43e97-148">Total de bytes por segundo lidos e gravados em arquivos, rede e dispositivos.</span><span class="sxs-lookup"><span data-stu-id="43e97-148">Total bytes per second read and written to files, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="43e97-149">taxa de exceção</span><span class="sxs-lookup"><span data-stu-id="43e97-149">exception rate</span></span> |<span data-ttu-id="43e97-150">Exceções geradas por segundo.</span><span class="sxs-lookup"><span data-stu-id="43e97-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="43e97-151">CPU do processo</span><span class="sxs-lookup"><span data-stu-id="43e97-151">Process CPU</span></span> |<span data-ttu-id="43e97-152">A porcentagem de tempo decorrido em todos os threads do processo usados pelo processador para executar instruções do processo dos aplicativos.</span><span class="sxs-lookup"><span data-stu-id="43e97-152">The percentage of elapsed time of all process threads used by the processor to execution instructions for the applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="43e97-153">Tempo do processador</span><span class="sxs-lookup"><span data-stu-id="43e97-153">Processor time</span></span> |<span data-ttu-id="43e97-154">A porcentagem de tempo que o processador gasta em threads ocupados.</span><span class="sxs-lookup"><span data-stu-id="43e97-154">The percentage of time that the processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="43e97-155">Processar bytes particulares</span><span class="sxs-lookup"><span data-stu-id="43e97-155">Process private bytes</span></span> |<span data-ttu-id="43e97-156">Memória atribuída exclusivamente aos processos do aplicativo monitorado.</span><span class="sxs-lookup"><span data-stu-id="43e97-156">Memory exclusively assigned to the monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="43e97-157">Tempo de execução de solicitação do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="43e97-157">ASP.NET request execution time</span></span> |<span data-ttu-id="43e97-158">Tempo de execução da solicitação mais recente.</span><span class="sxs-lookup"><span data-stu-id="43e97-158">Execution time of the most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="43e97-159">Solicitações do ASP.NET na fila de execução</span><span class="sxs-lookup"><span data-stu-id="43e97-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="43e97-160">Comprimento da fila de solicitação de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="43e97-160">Length of the application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="43e97-161">Taxa de solicitação do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="43e97-161">ASP.NET request rate</span></span> |<span data-ttu-id="43e97-162">Taxa de todas as solicitações para o aplicativo por segundo do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="43e97-162">Rate of all requests to the application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="43e97-163">Falhas de dependência</span><span class="sxs-lookup"><span data-stu-id="43e97-163">Dependency failures</span></span> |<span data-ttu-id="43e97-164">Contagem de falhas de chamadas feitas pelo aplicativo servidor para recursos externos.</span><span class="sxs-lookup"><span data-stu-id="43e97-164">Count of failed calls made by the server application to external resources.</span></span> |
| `request.duration` |<span data-ttu-id="43e97-165">Tempo de resposta do servidor</span><span class="sxs-lookup"><span data-stu-id="43e97-165">Server response time</span></span> |<span data-ttu-id="43e97-166">Tempo entre o recebimento de uma solicitação HTTP e a finalização do envio da resposta.</span><span class="sxs-lookup"><span data-stu-id="43e97-166">Time between receiving an HTTP request and finishing sending the response.</span></span> |
| `request.rate` |<span data-ttu-id="43e97-167">Taxa de solicitação</span><span class="sxs-lookup"><span data-stu-id="43e97-167">Request rate</span></span> |<span data-ttu-id="43e97-168">Taxa de todas as solicitações para o aplicativo por segundo.</span><span class="sxs-lookup"><span data-stu-id="43e97-168">Rate of all requests to the application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="43e97-169">Solicitações falhas</span><span class="sxs-lookup"><span data-stu-id="43e97-169">Failed requests</span></span> |<span data-ttu-id="43e97-170">Contagem de solicitações HTTP que resultaram em um código de resposta >= 400</span><span class="sxs-lookup"><span data-stu-id="43e97-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="43e97-171">Visualizações de página</span><span class="sxs-lookup"><span data-stu-id="43e97-171">Page views</span></span> |<span data-ttu-id="43e97-172">Contagem de solicitações de usuário  cliente para uma página da Web.</span><span class="sxs-lookup"><span data-stu-id="43e97-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="43e97-173">O tráfego sintético é filtrado.</span><span class="sxs-lookup"><span data-stu-id="43e97-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="43e97-174">{o nome de métrica personalizada}</span><span class="sxs-lookup"><span data-stu-id="43e97-174">{your custom metric name}</span></span> |<span data-ttu-id="43e97-175">{O nome da métrica}</span><span class="sxs-lookup"><span data-stu-id="43e97-175">{Your metric name}</span></span> |<span data-ttu-id="43e97-176">O valor de métrica relatado pelo [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) ou o [parâmetro de medidas de uma chamada de controle](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="43e97-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in the [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="43e97-177">As métricas são enviadas por diferentes módulos de telemetria:</span><span class="sxs-lookup"><span data-stu-id="43e97-177">The metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="43e97-178">Grupo de métricas</span><span class="sxs-lookup"><span data-stu-id="43e97-178">Metric group</span></span> | <span data-ttu-id="43e97-179">Módulo de coletor</span><span class="sxs-lookup"><span data-stu-id="43e97-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="43e97-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="43e97-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="43e97-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="43e97-181">clientPerformance,</span></span><br/><span data-ttu-id="43e97-182">view</span><span class="sxs-lookup"><span data-stu-id="43e97-182">view</span></span> |[<span data-ttu-id="43e97-183">JavaScript do navegador</span><span class="sxs-lookup"><span data-stu-id="43e97-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="43e97-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="43e97-184">performanceCounter</span></span> |[<span data-ttu-id="43e97-185">Desempenho</span><span class="sxs-lookup"><span data-stu-id="43e97-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="43e97-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="43e97-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="43e97-187">Dependência</span><span class="sxs-lookup"><span data-stu-id="43e97-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="43e97-188">request,</span><span class="sxs-lookup"><span data-stu-id="43e97-188">request,</span></span><br/><span data-ttu-id="43e97-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="43e97-189">requestFailed</span></span> |[<span data-ttu-id="43e97-190">Solicitação do servidor</span><span class="sxs-lookup"><span data-stu-id="43e97-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="43e97-191">Webhooks</span><span class="sxs-lookup"><span data-stu-id="43e97-191">Webhooks</span></span>
<span data-ttu-id="43e97-192">Você pode [automatizar sua resposta a um alerta](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="43e97-192">You can [automate your response to an alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="43e97-193">O Azure ligará para um endereço web de sua escolha quando um alerta for gerado.</span><span class="sxs-lookup"><span data-stu-id="43e97-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="43e97-194">Consulte também</span><span class="sxs-lookup"><span data-stu-id="43e97-194">See also</span></span>
* [<span data-ttu-id="43e97-195">Script para configurar o Application Insights</span><span class="sxs-lookup"><span data-stu-id="43e97-195">Script to configure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="43e97-196">Criar recursos de teste da Web e do Application Insights por meio de modelos</span><span class="sxs-lookup"><span data-stu-id="43e97-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="43e97-197">Automatizar o acoplamento do Diagnóstico do Microsoft Azure ao Application Insights</span><span class="sxs-lookup"><span data-stu-id="43e97-197">Automate coupling Microsoft Azure Diagnostics to Application Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="43e97-198">Automatizar sua resposta a um alerta</span><span class="sxs-lookup"><span data-stu-id="43e97-198">Automate your response to an alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
