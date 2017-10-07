---
title: "Monitoramento de trabalho de análise de fluxo de aaaUnderstanding | Microsoft Docs"
description: "Noções básicas sobre monitoramento de trabalho do Stream Analytics"
keywords: monitor de consultas
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 5f5cc00f-4a7b-491e-89e1-dbafea46d399
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 36819025c7b2ddbf4b9694522f1b4820407ca5f2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-toomonitor-queries"></a><span data-ttu-id="44636-104">Entender o monitoramento de trabalho do Stream Analytics e como consultas toomonitor</span><span class="sxs-lookup"><span data-stu-id="44636-104">Understand Stream Analytics job monitoring and how toomonitor queries</span></span>

## <a name="introduction-hello-monitor-page"></a><span data-ttu-id="44636-105">Introdução: página de monitor de saudação</span><span class="sxs-lookup"><span data-stu-id="44636-105">Introduction: hello monitor page</span></span>
<span data-ttu-id="44636-106">Olá portal do Azure, as principais métricas de desempenho que podem ser usado toomonitor e solucionar problemas de desempenho de sua consulta e o trabalho de superfície.</span><span class="sxs-lookup"><span data-stu-id="44636-106">hello Azure portal both surface key performance metrics that can be used toomonitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="44636-107">toosee essas métricas, procurar o trabalho de análise de fluxo de toohello você está interessado em ver saudação do modo de exibição e métricas para **monitoramento** seção na página de visão geral de saudação.</span><span class="sxs-lookup"><span data-stu-id="44636-107">toosee these metrics, browse toohello Stream Analytics job you are interested in seeing metrics for and view hello **Monitoring** section on hello Overview page.</span></span>  

![Link de monitoramento](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="44636-109">janela Hello serão exibidos conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="44636-109">hello window will appear as shown:</span></span>

![Painel de Trabalho de monitoramento](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="44636-111">Métricas disponíveis para o Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="44636-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="44636-112">Métrica</span><span class="sxs-lookup"><span data-stu-id="44636-112">Metric</span></span>                 | <span data-ttu-id="44636-113">Definição</span><span class="sxs-lookup"><span data-stu-id="44636-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="44636-114">% de utilização do SU</span><span class="sxs-lookup"><span data-stu-id="44636-114">SU % Utilization</span></span>       | <span data-ttu-id="44636-115">utilização de saudação do hello unidades de Streaming atribuído tooa trabalho na guia de escala de saudação do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="44636-115">hello utilization of hello Streaming Unit(s) assigned tooa job from hello Scale tab of hello job.</span></span> <span data-ttu-id="44636-116">Se esse indicador alcançar 80% ou acima, há grande probabilidade de que o processamento de eventos se atrase ou pare.</span><span class="sxs-lookup"><span data-stu-id="44636-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="44636-117">Eventos de entrada</span><span class="sxs-lookup"><span data-stu-id="44636-117">Input Events</span></span>           | <span data-ttu-id="44636-118">Quantidade de dados recebidos pelo trabalho do Stream Analytics hello, no número de eventos.</span><span class="sxs-lookup"><span data-stu-id="44636-118">Amount of data received by hello Stream Analytics job, in number of events.</span></span> <span data-ttu-id="44636-119">Isso pode ser usado toovalidate que os eventos estão sendo enviados toohello fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="44636-119">This can be used toovalidate that events are being sent toohello input source.</span></span> |
| <span data-ttu-id="44636-120">Eventos de saída</span><span class="sxs-lookup"><span data-stu-id="44636-120">Output Events</span></span>          | <span data-ttu-id="44636-121">Quantidade de dados enviados pelo Olá Stream Analytics trabalho toohello destino de saída, no número de eventos.</span><span class="sxs-lookup"><span data-stu-id="44636-121">Amount of data sent by hello Stream Analytics job toohello output target, in number of events.</span></span> |
| <span data-ttu-id="44636-122">Eventos fora de ordem</span><span class="sxs-lookup"><span data-stu-id="44636-122">Out-of-Order Events</span></span>    | <span data-ttu-id="44636-123">Número de eventos recebidos fora de ordem que foram descartados ou que receberam um carimbo de hora ajustado com base em Olá diretiva de ordenação de eventos.</span><span class="sxs-lookup"><span data-stu-id="44636-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on hello Event Ordering Policy.</span></span> <span data-ttu-id="44636-124">Isso pode ser afetado pela configuração de saudação da configuração da janela de tolerância de fora de ordem de saudação.</span><span class="sxs-lookup"><span data-stu-id="44636-124">This can be impacted by hello configuration of hello Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="44636-125">Erros de conversão de dados</span><span class="sxs-lookup"><span data-stu-id="44636-125">Data Conversion Errors</span></span> | <span data-ttu-id="44636-126">Número de erros de conversão de dados gerado por um trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="44636-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="44636-127">Erros de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="44636-127">Runtime Errors</span></span>         | <span data-ttu-id="44636-128">Olá total de erros que ocorrem durante a execução de um trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="44636-128">hello total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="44636-129">Eventos de entrada atrasados</span><span class="sxs-lookup"><span data-stu-id="44636-129">Late Input Events</span></span>      | <span data-ttu-id="44636-130">Número de eventos que chegam tarde de origem Olá que pode ter sido descartado ou seu carimbo de data foi ajustado, com base na configuração de diretiva de ordenação de eventos de saudação da configuração de janela de tolerância da chegada tardia hello.</span><span class="sxs-lookup"><span data-stu-id="44636-130">Number of events arriving late from hello source which have either been dropped or their timestamp has been adjusted, based on hello Event Ordering Policy configuration of hello Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="44636-131">Solicitações de função</span><span class="sxs-lookup"><span data-stu-id="44636-131">Function Requests</span></span>      | <span data-ttu-id="44636-132">Número de chamadas toohello função de aprendizado de máquina do Azure (se houver).</span><span class="sxs-lookup"><span data-stu-id="44636-132">Number of calls toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="44636-133">Solicitações de função com falha</span><span class="sxs-lookup"><span data-stu-id="44636-133">Failed Function Requests</span></span> | <span data-ttu-id="44636-134">Número de chamadas à função Azure Machine Learning com falha (se presente).</span><span class="sxs-lookup"><span data-stu-id="44636-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="44636-135">Eventos de função</span><span class="sxs-lookup"><span data-stu-id="44636-135">Function Events</span></span>        | <span data-ttu-id="44636-136">Número de eventos enviados toohello função de aprendizado de máquina do Azure (se houver).</span><span class="sxs-lookup"><span data-stu-id="44636-136">Number of events sent toohello Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="44636-137">Bytes de evento de entrada</span><span class="sxs-lookup"><span data-stu-id="44636-137">Input Event Bytes</span></span>      | <span data-ttu-id="44636-138">Quantidade de dados recebidos pelo trabalho do Stream Analytics hello, em bytes.</span><span class="sxs-lookup"><span data-stu-id="44636-138">Amount of data received by hello Stream Analytics job, in bytes.</span></span> <span data-ttu-id="44636-139">Isso pode ser usado toovalidate que os eventos estão sendo enviados toohello fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="44636-139">This can be used toovalidate that events are being sent toohello input source.</span></span> |


## <a name="customizing-monitoring-in-hello-azure-portal"></a><span data-ttu-id="44636-140">Personalizando o monitoramento no hello portal do Azure</span><span class="sxs-lookup"><span data-stu-id="44636-140">Customizing Monitoring in hello Azure portal</span></span>
<span data-ttu-id="44636-141">Você pode ajustar o tipo de gráfico, as métricas mostrados, hello e intervalo nas configurações do hello Editar gráfico de tempo.</span><span class="sxs-lookup"><span data-stu-id="44636-141">You can adjust hello type of chart, metrics shown, and time range in hello Edit Chart settings.</span></span> <span data-ttu-id="44636-142">Para obter detalhes, consulte [como tooCustomize monitoramento](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="44636-142">For details, see [How tooCustomize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Gráfico do Tempo do Monitor de Consultas](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="44636-144">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="44636-144">Get help</span></span>
<span data-ttu-id="44636-145">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="44636-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="44636-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="44636-146">Next steps</span></span>
* [<span data-ttu-id="44636-147">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="44636-147">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="44636-148">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="44636-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="44636-149">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="44636-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="44636-150">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="44636-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="44636-151">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="44636-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

