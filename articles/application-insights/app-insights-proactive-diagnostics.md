---
title: "aaaSmart detecção no Azure Application Insights | Microsoft Docs"
description: "O Application Insights executa uma análise automática profunda de telemetria do seu aplicativo e o avisará sobre possíveis problemas de desempenho."
services: application-insights
documentationcenter: windows
author: rakefetj
manager: carmonm
ms.assetid: 2eeb4a35-c7a1-49f7-9b68-4f4b860938b2
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.devlang: na
ms.topic: article
ms.date: 10/31/2016
ms.author: bwren
ms.openlocfilehash: f794476088fc69154eda2077b7a5cdc769fab3a1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="smart-detection-in-application-insights"></a><span data-ttu-id="7aa02-103">Detecção Inteligente no Application Insights</span><span class="sxs-lookup"><span data-stu-id="7aa02-103">Smart Detection in Application Insights</span></span>
 <span data-ttu-id="7aa02-104">A Detecção Inteligente avisa automaticamente sobre possíveis problemas de desempenho no seu aplicativo Web.</span><span class="sxs-lookup"><span data-stu-id="7aa02-104">Smart Detection automatically warns you of potential performance problems in your web application.</span></span> <span data-ttu-id="7aa02-105">Ele executa análise proativa de telemetria Olá que seu aplicativo envia muito[Application Insights](app-insights-overview.md).</span><span class="sxs-lookup"><span data-stu-id="7aa02-105">It performs proactive analysis of hello telemetry that your app sends too[Application Insights](app-insights-overview.md).</span></span> <span data-ttu-id="7aa02-106">Se houver um aumento repentino nas taxas de falha ou nos padrões anormais de desempenho de cliente ou de servidor, você receberá um alerta.</span><span class="sxs-lookup"><span data-stu-id="7aa02-106">If there is a sudden rise in failure rates, or abnormal patterns in client or server performance, you get an alert.</span></span> <span data-ttu-id="7aa02-107">Esse recurso não precisa de nenhuma configuração.</span><span class="sxs-lookup"><span data-stu-id="7aa02-107">This feature needs no configuration.</span></span> <span data-ttu-id="7aa02-108">Ela funciona se o seu aplicativo envia telemetria suficiente.</span><span class="sxs-lookup"><span data-stu-id="7aa02-108">It operates if your application sends enough telemetry.</span></span>

<span data-ttu-id="7aa02-109">Você pode acessar alertas de detecção inteligente de emails de saudação recebidos e na folha de detecção inteligente hello.</span><span class="sxs-lookup"><span data-stu-id="7aa02-109">You can access Smart Detection alerts both from hello emails you receive, and from hello Smart Detection blade.</span></span>

## <a name="review-your-smart-detections"></a><span data-ttu-id="7aa02-110">Revise suas detecções inteligentes</span><span class="sxs-lookup"><span data-stu-id="7aa02-110">Review your Smart Detections</span></span>
<span data-ttu-id="7aa02-111">É possível descobrir as detecções de duas maneiras:</span><span class="sxs-lookup"><span data-stu-id="7aa02-111">You can discover detections in two ways:</span></span>

* <span data-ttu-id="7aa02-112">**Você recebe um email** do Application Insights.</span><span class="sxs-lookup"><span data-stu-id="7aa02-112">**You receive an email** from Application Insights.</span></span> <span data-ttu-id="7aa02-113">Aqui está um exemplo típico:</span><span class="sxs-lookup"><span data-stu-id="7aa02-113">Here's a typical example:</span></span>
  
    ![Alerta de email](./media/app-insights-proactive-diagnostics/03.png)
  
    <span data-ttu-id="7aa02-115">Clique em Olá grande botão tooopen mais detalhes no portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="7aa02-115">Click hello big button tooopen more detail in hello portal.</span></span>
* <span data-ttu-id="7aa02-116">**bloco de detecção inteligente Olá** na visão geral do aplicativo folha mostra uma contagem de alertas recentes.</span><span class="sxs-lookup"><span data-stu-id="7aa02-116">**hello Smart Detection tile** on your app's overview blade shows a count of recent alerts.</span></span> <span data-ttu-id="7aa02-117">Clique em Olá bloco toosee uma lista dos alertas recentes.</span><span class="sxs-lookup"><span data-stu-id="7aa02-117">Click hello tile toosee a list of recent alerts.</span></span>

![Exibir detecções recentes](./media/app-insights-proactive-diagnostics/04.png)

<span data-ttu-id="7aa02-119">Selecione um alerta toosee seus detalhes.</span><span class="sxs-lookup"><span data-stu-id="7aa02-119">Select an alert toosee its details.</span></span>

## <a name="what-problems-are-detected"></a><span data-ttu-id="7aa02-120">Quais problemas foram detectados?</span><span class="sxs-lookup"><span data-stu-id="7aa02-120">What problems are detected?</span></span>
<span data-ttu-id="7aa02-121">Há três tipos de detecção:</span><span class="sxs-lookup"><span data-stu-id="7aa02-121">There are three kinds of detection:</span></span>

* <span data-ttu-id="7aa02-122">[Detecção inteligente - anomalias de falha](app-insights-proactive-failure-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="7aa02-122">[Smart detection - Failure Anomalies](app-insights-proactive-failure-diagnostics.md).</span></span> <span data-ttu-id="7aa02-123">Podemos usar o aprendizado de máquina tooset taxa de saudação esperada de solicitações com falha para seu aplicativo, correlacionando com carga e outros fatores.</span><span class="sxs-lookup"><span data-stu-id="7aa02-123">We use machine learning tooset hello expected rate of failed requests for your app, correlating with load and other factors.</span></span> <span data-ttu-id="7aa02-124">Se a taxa de falha Olá ficar fora envelope esperado hello, podemos enviar um alerta.</span><span class="sxs-lookup"><span data-stu-id="7aa02-124">If hello failure rate goes outside hello expected envelope, we send an alert.</span></span>
* <span data-ttu-id="7aa02-125">[Detecção inteligente - anomalias de desempenho](app-insights-proactive-performance-diagnostics.md).</span><span class="sxs-lookup"><span data-stu-id="7aa02-125">[Smart detection - Performance Anomalies](app-insights-proactive-performance-diagnostics.md).</span></span> <span data-ttu-id="7aa02-126">Você receberá notificações se o tempo de resposta de uma duração da operação ou dependência está diminuindo toohistorical em comparação com linha de base ou se é identificar um padrão anormal no tempo de resposta ou tempo de carregamento de página.</span><span class="sxs-lookup"><span data-stu-id="7aa02-126">You get notifications if response time of an operation or dependency duration is slowing down compared toohistorical baseline or if we identify an anomalous pattern in response time or page load time.</span></span>   
* <span data-ttu-id="7aa02-127">[Detecção inteligente - problemas do Serviço em Nuvem do Azure](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span><span class="sxs-lookup"><span data-stu-id="7aa02-127">[Smart detection - Azure Cloud Service issues](https://azure.microsoft.com/blog/proactive-notifications-on-cloud-service-issues-with-azure-diagnostics-and-application-insights/).</span></span> <span data-ttu-id="7aa02-128">Você obterá alertas se seu aplicativo estiver hospedado nos Serviços de Nuvem do Azure e se uma instância de função tiver falhas de inicialização, reciclagem frequente ou falhas no tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="7aa02-128">You get alerts if your app is hosted in Azure Cloud Services and a role instance has startup failures, frequent recycling, or runtime crashes.</span></span>

<span data-ttu-id="7aa02-129">(links de ajuda de saudação em cada notificação levam artigos relevantes toohello.)</span><span class="sxs-lookup"><span data-stu-id="7aa02-129">(hello help links in each notification take you toohello relevant articles.)</span></span>

## <a name="video"></a><span data-ttu-id="7aa02-130">Vídeo</span><span class="sxs-lookup"><span data-stu-id="7aa02-130">Video</span></span>

> [!VIDEO https://channel9.msdn.com/events/Connect/2016/112/player]

## <a name="next-steps"></a><span data-ttu-id="7aa02-131">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7aa02-131">Next steps</span></span>
<span data-ttu-id="7aa02-132">Essas ferramentas de diagnóstico ajudam a inspecionar a telemetria de saudação do seu aplicativo:</span><span class="sxs-lookup"><span data-stu-id="7aa02-132">These diagnostic tools help you inspect hello telemetry from your app:</span></span>

* [<span data-ttu-id="7aa02-133">Metrics explorer</span><span class="sxs-lookup"><span data-stu-id="7aa02-133">Metric explorer</span></span>](app-insights-metrics-explorer.md)
* [<span data-ttu-id="7aa02-134">Gerenciador de pesquisas</span><span class="sxs-lookup"><span data-stu-id="7aa02-134">Search explorer</span></span>](app-insights-diagnostic-search.md)
* [<span data-ttu-id="7aa02-135">Analytics - linguagem de consulta poderosa</span><span class="sxs-lookup"><span data-stu-id="7aa02-135">Analytics - powerful query language</span></span>](app-insights-analytics-tour.md)

<span data-ttu-id="7aa02-136">A Detecção Inteligente é totalmente automática.</span><span class="sxs-lookup"><span data-stu-id="7aa02-136">Smart Detection is completely automatic.</span></span> <span data-ttu-id="7aa02-137">Mas você queria tooset alguns alertas mais?</span><span class="sxs-lookup"><span data-stu-id="7aa02-137">But maybe you'd like tooset up some more alerts?</span></span>

* [<span data-ttu-id="7aa02-138">Alertas de métrica configurados manualmente</span><span class="sxs-lookup"><span data-stu-id="7aa02-138">Manually configured metric alerts</span></span>](app-insights-alerts.md)
* [<span data-ttu-id="7aa02-139">Testes de disponibilidade na Web</span><span class="sxs-lookup"><span data-stu-id="7aa02-139">Availability web tests</span></span>](app-insights-monitor-web-app-availability.md) 

