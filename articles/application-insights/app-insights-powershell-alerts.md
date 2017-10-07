---
title: aaaUse Powershell tooset alertas no Application Insights | Microsoft Docs
description: "Automatize a configuração de emails de tooget Application Insights sobre as alterações da métricas."
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
ms.openlocfilehash: d68e5f9511bb4015f59175724bc1a4a04ecf43e1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-powershell-tooset-alerts-in-application-insights"></a><span data-ttu-id="eec9d-103">Use o PowerShell tooset alertas no Application Insights</span><span class="sxs-lookup"><span data-stu-id="eec9d-103">Use PowerShell tooset alerts in Application Insights</span></span>
<span data-ttu-id="eec9d-104">Você pode automatizar a configuração de saudação do [alertas](app-insights-alerts.md) na [Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="eec9d-104">You can automate hello configuration of [alerts](app-insights-alerts.md) in [Application Insights](app-insights-overview.md).</span></span>

<span data-ttu-id="eec9d-105">Além disso, você pode [definir webhooks tooautomate alerta tooan resposta](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="eec9d-105">In addition, you can [set webhooks tooautomate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span>

> [!NOTE]
> <span data-ttu-id="eec9d-106">Se você quiser recursos toocreate e alertas em Olá mesmo tempo, considere [usando um modelo do Azure Resource Manager](app-insights-powershell.md).</span><span class="sxs-lookup"><span data-stu-id="eec9d-106">If you want toocreate resources and alerts at hello same time, consider [using an Azure Resource Manager template](app-insights-powershell.md).</span></span>
>
>

## <a name="one-time-setup"></a><span data-ttu-id="eec9d-107">Configuração única</span><span class="sxs-lookup"><span data-stu-id="eec9d-107">One-time setup</span></span>
<span data-ttu-id="eec9d-108">Se você nunca usou o PowerShell com sua assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="eec9d-108">If you haven't used PowerShell with your Azure subscription before:</span></span>

<span data-ttu-id="eec9d-109">Instale o módulo de Powershell do Azure de saudação na máquina Olá onde deseja toorun Olá scripts.</span><span class="sxs-lookup"><span data-stu-id="eec9d-109">Install hello Azure Powershell module on hello machine where you want toorun hello scripts.</span></span>

* <span data-ttu-id="eec9d-110">Instale o [Microsoft Web Platform Installer (v5 ou superior)](http://www.microsoft.com/web/downloads/platform.aspx).</span><span class="sxs-lookup"><span data-stu-id="eec9d-110">Install [Microsoft Web Platform Installer (v5 or higher)](http://www.microsoft.com/web/downloads/platform.aspx).</span></span>
* <span data-ttu-id="eec9d-111">Use-tooinstall Microsoft Azure Powershell</span><span class="sxs-lookup"><span data-stu-id="eec9d-111">Use it tooinstall Microsoft Azure Powershell</span></span>

## <a name="connect-tooazure"></a><span data-ttu-id="eec9d-112">Conecte-se tooAzure</span><span class="sxs-lookup"><span data-stu-id="eec9d-112">Connect tooAzure</span></span>
<span data-ttu-id="eec9d-113">Inicie o PowerShell do Azure e [conectar assinatura tooyour](/powershell/azure/overview):</span><span class="sxs-lookup"><span data-stu-id="eec9d-113">Start Azure PowerShell and [connect tooyour subscription](/powershell/azure/overview):</span></span>

```PowerShell

    Add-AzureAccount
```


## <a name="get-alerts"></a><span data-ttu-id="eec9d-114">Obter alertas</span><span class="sxs-lookup"><span data-stu-id="eec9d-114">Get alerts</span></span>
    Get-AzureAlertRmRule -ResourceGroup "Fabrikam" [-Name "My rule"] [-DetailedOutput]

## <a name="add-alert"></a><span data-ttu-id="eec9d-115">Adicionar alerta</span><span class="sxs-lookup"><span data-stu-id="eec9d-115">Add alert</span></span>
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



## <a name="example-1"></a><span data-ttu-id="eec9d-116">Exemplo 1</span><span class="sxs-lookup"><span data-stu-id="eec9d-116">Example 1</span></span>
<span data-ttu-id="eec9d-117">Enviar email para mim se solicitações de tooHTTP de resposta do servidor de saudação, mais de 5 minutos, a média é menor do que 1 segundo.</span><span class="sxs-lookup"><span data-stu-id="eec9d-117">Email me if hello server's response tooHTTP requests, averaged over 5 minutes, is slower than 1 second.</span></span> <span data-ttu-id="eec9d-118">Meu recurso Application Insights é chamado IceCreamWebApp e está no grupo de recursos Fabrikam.</span><span class="sxs-lookup"><span data-stu-id="eec9d-118">My Application Insights resource is called IceCreamWebApp, and it is in resource group Fabrikam.</span></span> <span data-ttu-id="eec9d-119">Sou proprietário Olá Olá assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="eec9d-119">I am hello owner of hello Azure subscription.</span></span>

<span data-ttu-id="eec9d-120">Olá GUID é o ID de assinatura de saudação (não Olá chave de instrumentação do aplicativo hello).</span><span class="sxs-lookup"><span data-stu-id="eec9d-120">hello GUID is hello subscription ID (not hello instrumentation key of hello application).</span></span>

    Add-AlertRule -Name "slow responses" `
     -Description "email me if hello server responds slowly" `
     -ResourceGroup "Fabrikam" `
     -ResourceId "/subscriptions/00000000-0000-0000-0000-000000000000/resourcegroups/Fabrikam/providers/microsoft.insights/components/IceCreamWebApp" `
     -MetricName "request.duration" `
     -Operator GreaterThan `
     -Threshold 1 `
     -WindowSize 00:05:00 `
     -SendEmailToServiceOwners `
     -Location "East US" -RuleType Metric

## <a name="example-2"></a><span data-ttu-id="eec9d-121">Exemplo 2</span><span class="sxs-lookup"><span data-stu-id="eec9d-121">Example 2</span></span>
<span data-ttu-id="eec9d-122">Tenho um aplicativo em que uso [Trackmetric](app-insights-api-custom-events-metrics.md#trackmetric) tooreport uma métrica denominada "salesPerHour".</span><span class="sxs-lookup"><span data-stu-id="eec9d-122">I have an application in which I use [TrackMetric()](app-insights-api-custom-events-metrics.md#trackmetric) tooreport a metric named "salesPerHour."</span></span> <span data-ttu-id="eec9d-123">Envie um email toomy colegas se "salesPerHour" cair abaixo de 100, a média de mais de 24 horas.</span><span class="sxs-lookup"><span data-stu-id="eec9d-123">Send an email toomy colleagues if "salesPerHour" drops below 100, averaged over 24 hours.</span></span>

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

<span data-ttu-id="eec9d-124">Olá mesma regra pode ser usada para a métrica de saudação relatadas usando Olá [parâmetro medida](app-insights-api-custom-events-metrics.md#properties) da chamada de outro controle como TrackEvent ou trackPageView.</span><span class="sxs-lookup"><span data-stu-id="eec9d-124">hello same rule can be used for hello metric reported by using hello [measurement parameter](app-insights-api-custom-events-metrics.md#properties) of another tracking call such as TrackEvent or trackPageView.</span></span>

## <a name="metric-names"></a><span data-ttu-id="eec9d-125">Nomes de métrica</span><span class="sxs-lookup"><span data-stu-id="eec9d-125">Metric names</span></span>
| <span data-ttu-id="eec9d-126">Nome da métrica</span><span class="sxs-lookup"><span data-stu-id="eec9d-126">Metric name</span></span> | <span data-ttu-id="eec9d-127">Nome da tela</span><span class="sxs-lookup"><span data-stu-id="eec9d-127">Screen name</span></span> | <span data-ttu-id="eec9d-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="eec9d-128">Description</span></span> |
| --- | --- | --- |
| `basicExceptionBrowser.count` |<span data-ttu-id="eec9d-129">Exceções de navegador</span><span class="sxs-lookup"><span data-stu-id="eec9d-129">Browser exceptions</span></span> |<span data-ttu-id="eec9d-130">Contagem de exceções não capturadas lançadas no navegador de saudação.</span><span class="sxs-lookup"><span data-stu-id="eec9d-130">Count of uncaught exceptions thrown in hello browser.</span></span> |
| `basicExceptionServer.count` |<span data-ttu-id="eec9d-131">Exceções do servidor</span><span class="sxs-lookup"><span data-stu-id="eec9d-131">Server exceptions</span></span> |<span data-ttu-id="eec9d-132">Contagem de exceções sem tratamento lançadas pelo aplicativo hello</span><span class="sxs-lookup"><span data-stu-id="eec9d-132">Count of unhandled exceptions thrown by hello app</span></span> |
| `clientPerformance.clientProcess.value` |<span data-ttu-id="eec9d-133">Tempo de processamento do cliente</span><span class="sxs-lookup"><span data-stu-id="eec9d-133">Client processing time</span></span> |<span data-ttu-id="eec9d-134">Tempo entre a recepção o último byte de um documento hello até Olá DOM ser carregado.</span><span class="sxs-lookup"><span data-stu-id="eec9d-134">Time between receiving hello last byte of a document until hello DOM is loaded.</span></span> <span data-ttu-id="eec9d-135">As solicitações assíncronas ainda podem estar sendo processadas.</span><span class="sxs-lookup"><span data-stu-id="eec9d-135">Async requests may still be processing.</span></span> |
| `clientPerformance.networkConnection.value` |<span data-ttu-id="eec9d-136">Tempo de conexão de rede de carregamento de página</span><span class="sxs-lookup"><span data-stu-id="eec9d-136">Page load network connect time</span></span> |<span data-ttu-id="eec9d-137">Navegador de saudação do tempo levará tooconnect toohello rede.</span><span class="sxs-lookup"><span data-stu-id="eec9d-137">Time hello browser takes tooconnect toohello network.</span></span> <span data-ttu-id="eec9d-138">Pode ser 0 se armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="eec9d-138">Can be 0 if cached.</span></span> |
| `clientPerformance.receiveRequest.value` |<span data-ttu-id="eec9d-139">Tempo de resposta de recebimento</span><span class="sxs-lookup"><span data-stu-id="eec9d-139">Receiving response time</span></span> |<span data-ttu-id="eec9d-140">Tempo entre enviar solicitação toostarting tooreceive resposta do navegador.</span><span class="sxs-lookup"><span data-stu-id="eec9d-140">Time between browser sending request toostarting tooreceive response.</span></span> |
| `clientPerformance.sendRequest.value` |<span data-ttu-id="eec9d-141">Tempo de solicitação de envio</span><span class="sxs-lookup"><span data-stu-id="eec9d-141">Send request time</span></span> |<span data-ttu-id="eec9d-142">Tempo levado pela solicitação de toosend do navegador.</span><span class="sxs-lookup"><span data-stu-id="eec9d-142">Time taken by browser toosend request.</span></span> |
| `clientPerformance.total.value` |<span data-ttu-id="eec9d-143">Tempo de carregamento de página do navegador</span><span class="sxs-lookup"><span data-stu-id="eec9d-143">Browser page load time</span></span> |<span data-ttu-id="eec9d-144">Tempo de solicitação do usuário até que o DOM, as imagens, os scripts e as folhas de estilo sejam carregados.</span><span class="sxs-lookup"><span data-stu-id="eec9d-144">Time from user request until DOM, stylesheets, scripts and images are loaded.</span></span> |
| `performanceCounter.available_bytes.value` |<span data-ttu-id="eec9d-145">Memória disponível</span><span class="sxs-lookup"><span data-stu-id="eec9d-145">Available memory</span></span> |<span data-ttu-id="eec9d-146">Memória física disponível imediatamente para um processo ou para uso do sistema.</span><span class="sxs-lookup"><span data-stu-id="eec9d-146">Physical memory immediately available for a process or for system use.</span></span> |
| `performanceCounter.io_data_bytes_per_sec.value` |<span data-ttu-id="eec9d-147">Taxa de processamento de IO</span><span class="sxs-lookup"><span data-stu-id="eec9d-147">Process IO Rate</span></span> |<span data-ttu-id="eec9d-148">Total de bytes por segundo de leitura e escrita toofiles, redes e dispositivos.</span><span class="sxs-lookup"><span data-stu-id="eec9d-148">Total bytes per second read and written toofiles, network and devices.</span></span> |
| `performanceCounter.number_of_exceps_thrown_per_sec.value` |<span data-ttu-id="eec9d-149">taxa de exceção</span><span class="sxs-lookup"><span data-stu-id="eec9d-149">exception rate</span></span> |<span data-ttu-id="eec9d-150">Exceções geradas por segundo.</span><span class="sxs-lookup"><span data-stu-id="eec9d-150">Exceptions thrown per second.</span></span> |
| `performanceCounter.percentage_processor_time.value` |<span data-ttu-id="eec9d-151">CPU do processo</span><span class="sxs-lookup"><span data-stu-id="eec9d-151">Process CPU</span></span> |<span data-ttu-id="eec9d-152">Porcentagem de saudação do tempo decorrido de todos os threads de processo usado por instruções de tooexecution Olá processador no processo de aplicativos de saudação.</span><span class="sxs-lookup"><span data-stu-id="eec9d-152">hello percentage of elapsed time of all process threads used by hello processor tooexecution instructions for hello applications process.</span></span> |
| `performanceCounter.percentage_processor_total.value` |<span data-ttu-id="eec9d-153">Tempo do processador</span><span class="sxs-lookup"><span data-stu-id="eec9d-153">Processor time</span></span> |<span data-ttu-id="eec9d-154">Porcentagem de saudação do tempo Olá processador gasta em threads não ociosos.</span><span class="sxs-lookup"><span data-stu-id="eec9d-154">hello percentage of time that hello processor spends in non-Idle threads.</span></span> |
| `performanceCounter.process_private_bytes.value` |<span data-ttu-id="eec9d-155">Processar bytes particulares</span><span class="sxs-lookup"><span data-stu-id="eec9d-155">Process private bytes</span></span> |<span data-ttu-id="eec9d-156">Memória atribuída exclusivamente toohello monitorados processos do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="eec9d-156">Memory exclusively assigned toohello monitored application's processes.</span></span> |
| `performanceCounter.request_execution_time.value` |<span data-ttu-id="eec9d-157">Tempo de execução de solicitação do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="eec9d-157">ASP.NET request execution time</span></span> |<span data-ttu-id="eec9d-158">Tempo de execução da solicitação mais recente hello.</span><span class="sxs-lookup"><span data-stu-id="eec9d-158">Execution time of hello most recent request.</span></span> |
| `performanceCounter.requests_in_application_queue.value` |<span data-ttu-id="eec9d-159">Solicitações do ASP.NET na fila de execução</span><span class="sxs-lookup"><span data-stu-id="eec9d-159">ASP.NET requests in execution queue</span></span> |<span data-ttu-id="eec9d-160">Comprimento da fila de solicitações de aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="eec9d-160">Length of hello application request queue.</span></span> |
| `performanceCounter.requests_per_sec.value` |<span data-ttu-id="eec9d-161">Taxa de solicitação do ASP.NET</span><span class="sxs-lookup"><span data-stu-id="eec9d-161">ASP.NET request rate</span></span> |<span data-ttu-id="eec9d-162">Taxa de todas as solicitações de aplicativo toohello por segundo do ASP.NET.</span><span class="sxs-lookup"><span data-stu-id="eec9d-162">Rate of all requests toohello application per second from ASP.NET.</span></span> |
| `remoteDependencyFailed.durationMetric.count` |<span data-ttu-id="eec9d-163">Falhas de dependência</span><span class="sxs-lookup"><span data-stu-id="eec9d-163">Dependency failures</span></span> |<span data-ttu-id="eec9d-164">Contagem de chamadas com falha feitas pelos recursos de tooexternal de aplicativos de servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="eec9d-164">Count of failed calls made by hello server application tooexternal resources.</span></span> |
| `request.duration` |<span data-ttu-id="eec9d-165">Tempo de resposta do servidor</span><span class="sxs-lookup"><span data-stu-id="eec9d-165">Server response time</span></span> |<span data-ttu-id="eec9d-166">Tempo entre a receber uma solicitação HTTP e a conclusão do envio Olá resposta.</span><span class="sxs-lookup"><span data-stu-id="eec9d-166">Time between receiving an HTTP request and finishing sending hello response.</span></span> |
| `request.rate` |<span data-ttu-id="eec9d-167">Taxa de solicitação</span><span class="sxs-lookup"><span data-stu-id="eec9d-167">Request rate</span></span> |<span data-ttu-id="eec9d-168">Taxa de todas as solicitações de aplicativo toohello por segundo.</span><span class="sxs-lookup"><span data-stu-id="eec9d-168">Rate of all requests toohello application per second.</span></span> |
| `requestFailed.count` |<span data-ttu-id="eec9d-169">Solicitações falhas</span><span class="sxs-lookup"><span data-stu-id="eec9d-169">Failed requests</span></span> |<span data-ttu-id="eec9d-170">Contagem de solicitações HTTP que resultaram em um código de resposta >= 400</span><span class="sxs-lookup"><span data-stu-id="eec9d-170">Count of HTTP requests that resulted in a response code >= 400</span></span> |
| `view.count` |<span data-ttu-id="eec9d-171">Visualizações de página</span><span class="sxs-lookup"><span data-stu-id="eec9d-171">Page views</span></span> |<span data-ttu-id="eec9d-172">Contagem de solicitações de usuário  cliente para uma página da Web.</span><span class="sxs-lookup"><span data-stu-id="eec9d-172">Count of client user requests for a web page.</span></span> <span data-ttu-id="eec9d-173">O tráfego sintético é filtrado.</span><span class="sxs-lookup"><span data-stu-id="eec9d-173">Synthetic traffic is filtered out.</span></span> |
| <span data-ttu-id="eec9d-174">{o nome de métrica personalizada}</span><span class="sxs-lookup"><span data-stu-id="eec9d-174">{your custom metric name}</span></span> |<span data-ttu-id="eec9d-175">{O nome da métrica}</span><span class="sxs-lookup"><span data-stu-id="eec9d-175">{Your metric name}</span></span> |<span data-ttu-id="eec9d-176">O valor de métrica relatado por [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) ou em Olá [parâmetro medidas de uma chamada de controle](app-insights-api-custom-events-metrics.md#properties).</span><span class="sxs-lookup"><span data-stu-id="eec9d-176">Your metric value reported by [TrackMetric](app-insights-api-custom-events-metrics.md#trackmetric) or in hello [measurements parameter of a tracking call](app-insights-api-custom-events-metrics.md#properties).</span></span> |

<span data-ttu-id="eec9d-177">métricas de saudação são enviadas por módulos de telemetria diferentes:</span><span class="sxs-lookup"><span data-stu-id="eec9d-177">hello metrics are sent by different telemetry modules:</span></span>

| <span data-ttu-id="eec9d-178">Grupo de métricas</span><span class="sxs-lookup"><span data-stu-id="eec9d-178">Metric group</span></span> | <span data-ttu-id="eec9d-179">Módulo de coletor</span><span class="sxs-lookup"><span data-stu-id="eec9d-179">Collector module</span></span> |
| --- | --- |
| <span data-ttu-id="eec9d-180">basicExceptionBrowser,</span><span class="sxs-lookup"><span data-stu-id="eec9d-180">basicExceptionBrowser,</span></span><br/><span data-ttu-id="eec9d-181">clientPerformance,</span><span class="sxs-lookup"><span data-stu-id="eec9d-181">clientPerformance,</span></span><br/><span data-ttu-id="eec9d-182">view</span><span class="sxs-lookup"><span data-stu-id="eec9d-182">view</span></span> |[<span data-ttu-id="eec9d-183">JavaScript do navegador</span><span class="sxs-lookup"><span data-stu-id="eec9d-183">Browser JavaScript</span></span>](app-insights-javascript.md) |
| <span data-ttu-id="eec9d-184">performanceCounter</span><span class="sxs-lookup"><span data-stu-id="eec9d-184">performanceCounter</span></span> |[<span data-ttu-id="eec9d-185">Desempenho</span><span class="sxs-lookup"><span data-stu-id="eec9d-185">Performance</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="eec9d-186">remoteDependencyFailed</span><span class="sxs-lookup"><span data-stu-id="eec9d-186">remoteDependencyFailed</span></span> |[<span data-ttu-id="eec9d-187">Dependência</span><span class="sxs-lookup"><span data-stu-id="eec9d-187">Dependency</span></span>](app-insights-configuration-with-applicationinsights-config.md) |
| <span data-ttu-id="eec9d-188">request,</span><span class="sxs-lookup"><span data-stu-id="eec9d-188">request,</span></span><br/><span data-ttu-id="eec9d-189">requestFailed</span><span class="sxs-lookup"><span data-stu-id="eec9d-189">requestFailed</span></span> |[<span data-ttu-id="eec9d-190">Solicitação do servidor</span><span class="sxs-lookup"><span data-stu-id="eec9d-190">Server request</span></span>](app-insights-configuration-with-applicationinsights-config.md) |

## <a name="webhooks"></a><span data-ttu-id="eec9d-191">Webhooks</span><span class="sxs-lookup"><span data-stu-id="eec9d-191">Webhooks</span></span>
<span data-ttu-id="eec9d-192">Você pode [automatizar o alerta de tooan resposta](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span><span class="sxs-lookup"><span data-stu-id="eec9d-192">You can [automate your response tooan alert](../monitoring-and-diagnostics/insights-webhooks-alerts.md).</span></span> <span data-ttu-id="eec9d-193">O Azure ligará para um endereço web de sua escolha quando um alerta for gerado.</span><span class="sxs-lookup"><span data-stu-id="eec9d-193">Azure will call a web address of your choice when an alert is raised.</span></span>

## <a name="see-also"></a><span data-ttu-id="eec9d-194">Consulte também</span><span class="sxs-lookup"><span data-stu-id="eec9d-194">See also</span></span>
* [<span data-ttu-id="eec9d-195">Script tooconfigure Application Insights</span><span class="sxs-lookup"><span data-stu-id="eec9d-195">Script tooconfigure Application Insights</span></span>](app-insights-powershell-script-create-resource.md)
* [<span data-ttu-id="eec9d-196">Criar recursos de teste da Web e do Application Insights por meio de modelos</span><span class="sxs-lookup"><span data-stu-id="eec9d-196">Create Application Insights and web test resources from templates</span></span>](app-insights-powershell.md)
* [<span data-ttu-id="eec9d-197">Automatizar a combinação de diagnóstico do Microsoft Azure tooApplication Insights</span><span class="sxs-lookup"><span data-stu-id="eec9d-197">Automate coupling Microsoft Azure Diagnostics tooApplication Insights</span></span>](app-insights-powershell-azure-diagnostics.md)
* [<span data-ttu-id="eec9d-198">Automatizar o alerta de tooan de resposta</span><span class="sxs-lookup"><span data-stu-id="eec9d-198">Automate your response tooan alert</span></span>](../monitoring-and-diagnostics/insights-webhooks-alerts.md)
