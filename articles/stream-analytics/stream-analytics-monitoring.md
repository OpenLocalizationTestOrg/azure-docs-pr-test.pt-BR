---
title: "Noções básicas sobre monitoramento de trabalho do Stream Analytics | Microsoft Docs"
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
ms.openlocfilehash: 13d96807a5591ec88deda19ea73cfedc07078433
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="understand-stream-analytics-job-monitoring-and-how-to-monitor-queries"></a><span data-ttu-id="bc67f-104">Noções básicas sobre o monitoramento de trabalhos do Stream Analytics e como monitorar consultas</span><span class="sxs-lookup"><span data-stu-id="bc67f-104">Understand Stream Analytics job monitoring and how to monitor queries</span></span>

## <a name="introduction-the-monitor-page"></a><span data-ttu-id="bc67f-105">Introdução: Página do monitor</span><span class="sxs-lookup"><span data-stu-id="bc67f-105">Introduction: The monitor page</span></span>
<span data-ttu-id="bc67f-106">O Portal do Azure exibe as principais métricas de desempenho que podem ser usadas para monitorar e solucionar problemas de desempenho de seus trabalhos e consultas.</span><span class="sxs-lookup"><span data-stu-id="bc67f-106">The Azure portal both surface key performance metrics that can be used to monitor and troubleshoot your query and job performance.</span></span> <span data-ttu-id="bc67f-107">Para ver essas métricas, procure o trabalho do Stream Analytics em cujas métricas você está interessado em ver e exiba a seção **Monitoramento** na página de visão geral.</span><span class="sxs-lookup"><span data-stu-id="bc67f-107">To see these metrics, browse to the Stream Analytics job you are interested in seeing metrics for and view the **Monitoring** section on the Overview page.</span></span>  

![Link de monitoramento](./media/stream-analytics-monitoring/02-stream-analytics-monitoring-block.png)

<span data-ttu-id="bc67f-109">A janela será exibida conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="bc67f-109">The window will appear as shown:</span></span>

![Painel de Trabalho de monitoramento](./media/stream-analytics-monitoring/01-stream-analytics-monitoring.png)  

## <a name="metrics-available-for-stream-analytics"></a><span data-ttu-id="bc67f-111">Métricas disponíveis para o Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bc67f-111">Metrics available for Stream Analytics</span></span>
| <span data-ttu-id="bc67f-112">Métrica</span><span class="sxs-lookup"><span data-stu-id="bc67f-112">Metric</span></span>                 | <span data-ttu-id="bc67f-113">Definição</span><span class="sxs-lookup"><span data-stu-id="bc67f-113">Definition</span></span>                               |
| ---------------------- | ---------------------------------------- |
| <span data-ttu-id="bc67f-114">% de utilização do SU</span><span class="sxs-lookup"><span data-stu-id="bc67f-114">SU % Utilization</span></span>       | <span data-ttu-id="bc67f-115">A utilização das unidades de Streaming é atribuída a um trabalho na guia Escala do trabalho.</span><span class="sxs-lookup"><span data-stu-id="bc67f-115">The utilization of the Streaming Unit(s) assigned to a job from the Scale tab of the job.</span></span> <span data-ttu-id="bc67f-116">Se esse indicador alcançar 80% ou acima, há grande probabilidade de que o processamento de eventos se atrase ou pare.</span><span class="sxs-lookup"><span data-stu-id="bc67f-116">Should this indicator reach 80%, or above, there is high probability that event processing may be delayed or stopped making progress.</span></span> |
| <span data-ttu-id="bc67f-117">Eventos de entrada</span><span class="sxs-lookup"><span data-stu-id="bc67f-117">Input Events</span></span>           | <span data-ttu-id="bc67f-118">Quantidade de dados recebidos pelo trabalho do Stream Analytics, em termos de eventos.</span><span class="sxs-lookup"><span data-stu-id="bc67f-118">Amount of data received by the Stream Analytics job, in number of events.</span></span> <span data-ttu-id="bc67f-119">Isso pode ser usado para validar que os eventos estão sendo enviados para a fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="bc67f-119">This can be used to validate that events are being sent to the input source.</span></span> |
| <span data-ttu-id="bc67f-120">Eventos de saída</span><span class="sxs-lookup"><span data-stu-id="bc67f-120">Output Events</span></span>          | <span data-ttu-id="bc67f-121">Quantidade de dados enviados pelo trabalho do Stream Analytics para o destino de saída, em números de evento.</span><span class="sxs-lookup"><span data-stu-id="bc67f-121">Amount of data sent by the Stream Analytics job to the output target, in number of events.</span></span> |
| <span data-ttu-id="bc67f-122">Eventos fora de ordem</span><span class="sxs-lookup"><span data-stu-id="bc67f-122">Out-of-Order Events</span></span>    | <span data-ttu-id="bc67f-123">Número de eventos recebidos fora de ordem que foram descartados ou que receberam um carimbo de data/hora ajustado, com base na Política de ordenação de evento.</span><span class="sxs-lookup"><span data-stu-id="bc67f-123">Number of events received out of order that were either dropped or given an adjusted timestamp, based on the Event Ordering Policy.</span></span> <span data-ttu-id="bc67f-124">Isso pode ser afetado pela configuração da definição da Janela de tolerância fora de ordem.</span><span class="sxs-lookup"><span data-stu-id="bc67f-124">This can be impacted by the configuration of the Out of Order Tolerance Window setting.</span></span> |
| <span data-ttu-id="bc67f-125">Erros de conversão de dados</span><span class="sxs-lookup"><span data-stu-id="bc67f-125">Data Conversion Errors</span></span> | <span data-ttu-id="bc67f-126">Número de erros de conversão de dados gerado por um trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="bc67f-126">Number of data conversion errors incurred by a Stream Analytics job.</span></span> |
| <span data-ttu-id="bc67f-127">Erros de tempo de execução</span><span class="sxs-lookup"><span data-stu-id="bc67f-127">Runtime Errors</span></span>         | <span data-ttu-id="bc67f-128">O número total de erros que ocorrem durante a execução de um trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="bc67f-128">The total number of errors that happen during execution of a Stream Analytics job.</span></span> |
| <span data-ttu-id="bc67f-129">Eventos de entrada atrasados</span><span class="sxs-lookup"><span data-stu-id="bc67f-129">Late Input Events</span></span>      | <span data-ttu-id="bc67f-130">Número de eventos que chegam atrasados da fonte que podem ter sido descartados ou ter tido o carimbo de data/hora ajustado, com base na configuração de Política de ordenação de eventos da configuração da definição da Janela de tolerância de chegada atrasada.</span><span class="sxs-lookup"><span data-stu-id="bc67f-130">Number of events arriving late from the source which have either been dropped or their timestamp has been adjusted, based on the Event Ordering Policy configuration of the Late Arrival Tolerance Window setting.</span></span> |
| <span data-ttu-id="bc67f-131">Solicitações de função</span><span class="sxs-lookup"><span data-stu-id="bc67f-131">Function Requests</span></span>      | <span data-ttu-id="bc67f-132">Número de chamadas à função Azure Machine Learning (se presente).</span><span class="sxs-lookup"><span data-stu-id="bc67f-132">Number of calls to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="bc67f-133">Solicitações de função com falha</span><span class="sxs-lookup"><span data-stu-id="bc67f-133">Failed Function Requests</span></span> | <span data-ttu-id="bc67f-134">Número de chamadas à função Azure Machine Learning com falha (se presente).</span><span class="sxs-lookup"><span data-stu-id="bc67f-134">Number of failed Azure Machine Learning function calls (if present).</span></span> |
| <span data-ttu-id="bc67f-135">Eventos de função</span><span class="sxs-lookup"><span data-stu-id="bc67f-135">Function Events</span></span>        | <span data-ttu-id="bc67f-136">Número de eventos enviados à função Azure Machine Learning (se presente).</span><span class="sxs-lookup"><span data-stu-id="bc67f-136">Number of events sent to the Azure Machine Learning function (if present).</span></span> |
| <span data-ttu-id="bc67f-137">Bytes de evento de entrada</span><span class="sxs-lookup"><span data-stu-id="bc67f-137">Input Event Bytes</span></span>      | <span data-ttu-id="bc67f-138">Quantidade de dados recebidos pelo trabalho do Stream Analytics, em bytes.</span><span class="sxs-lookup"><span data-stu-id="bc67f-138">Amount of data received by the Stream Analytics job, in bytes.</span></span> <span data-ttu-id="bc67f-139">Isso pode ser usado para validar que os eventos estão sendo enviados para a fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="bc67f-139">This can be used to validate that events are being sent to the input source.</span></span> |


## <a name="customizing-monitoring-in-the-azure-portal"></a><span data-ttu-id="bc67f-140">Personalizando o Monitoramento no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="bc67f-140">Customizing Monitoring in the Azure portal</span></span>
<span data-ttu-id="bc67f-141">Você pode ajustar o tipo de gráfico, as métricas mostradas e o intervalo de hora nas configurações de Editar Gráfico.</span><span class="sxs-lookup"><span data-stu-id="bc67f-141">You can adjust the type of chart, metrics shown, and time range in the Edit Chart settings.</span></span> <span data-ttu-id="bc67f-142">Para obter detalhes, veja [Como personalizar o monitoramento](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="bc67f-142">For details, see [How to Customize Monitoring](../monitoring-and-diagnostics/insights-how-to-customize-monitoring.md).</span></span>

  ![Gráfico do Tempo do Monitor de Consultas](./media/stream-analytics-monitoring/08-stream-analytics-monitoring.png)  


## <a name="get-help"></a><span data-ttu-id="bc67f-144">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="bc67f-144">Get help</span></span>
<span data-ttu-id="bc67f-145">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="bc67f-145">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="bc67f-146">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="bc67f-146">Next steps</span></span>
* [<span data-ttu-id="bc67f-147">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="bc67f-147">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="bc67f-148">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="bc67f-148">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="bc67f-149">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="bc67f-149">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="bc67f-150">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="bc67f-150">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="bc67f-151">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="bc67f-151">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

