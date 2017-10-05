---
title: "Depuração orientada a dados do Stream Analytics do Azure usando o diagrama de trabalho | Microsoft Docs"
description: "Solucionar problemas do trabalho no Stream Analytics usando o diagrama de trabalho e métricas."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 05/01/2017
ms.author: jeffstok
ms.openlocfilehash: 4e5949232e8377b7697eaebf96eacdc31c4f5422
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="data-driven-debugging-by-using-the-job-diagram"></a><span data-ttu-id="d70ad-103">Depuração orientada a dados usando o diagrama de trabalho</span><span class="sxs-lookup"><span data-stu-id="d70ad-103">Data-driven debugging by using the job diagram</span></span>

<span data-ttu-id="d70ad-104">O diagrama de trabalho na folha **Monitoramento** do Portal do Azure pode ajudar a visualizar o pipeline de trabalho.</span><span class="sxs-lookup"><span data-stu-id="d70ad-104">The job diagram on the **Monitoring** blade in the Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="d70ad-105">Ele mostra entradas, saídas e etapas de consulta.</span><span class="sxs-lookup"><span data-stu-id="d70ad-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="d70ad-106">Você pode usar o diagrama de trabalho para examinar as métricas de cada etapa e isolar mais rapidamente a origem de um problema ao solucioná-lo.</span><span class="sxs-lookup"><span data-stu-id="d70ad-106">You can use the job diagram to examine the metrics for each step, to more quickly isolate the source of a problem when you troubleshoot issues.</span></span>

## <a name="using-the-job-diagram"></a><span data-ttu-id="d70ad-107">Usando o diagrama de trabalho</span><span class="sxs-lookup"><span data-stu-id="d70ad-107">Using the job diagram</span></span>

<span data-ttu-id="d70ad-108">No Portal do Azure, enquanto estiver em um trabalho do Stream Analytics, em **SUPORTE + SOLUÇÃO DE PROBLEMAS**, selecione **Diagrama de trabalho**:</span><span class="sxs-lookup"><span data-stu-id="d70ad-108">In the Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagrama de trabalho com métricas - local](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="d70ad-110">Selecione cada etapa da consulta para ver a seção correspondente em um painel de edição de consulta.</span><span class="sxs-lookup"><span data-stu-id="d70ad-110">Select each query step to see the corresponding section in a query editing pane.</span></span> <span data-ttu-id="d70ad-111">Um gráfico de métrica para a etapa é exibido em um painel inferior da página.</span><span class="sxs-lookup"><span data-stu-id="d70ad-111">A metric chart for the step is displayed in a lower pane on the page.</span></span>

![Diagrama de trabalho com métricas - local](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="d70ad-113">Para ver as partições da entrada dos Hubs de Eventos do Azure, selecione **. . .**</span><span class="sxs-lookup"><span data-stu-id="d70ad-113">To see the partitions of the Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="d70ad-114">O menu de contexto é exibido.</span><span class="sxs-lookup"><span data-stu-id="d70ad-114">A context menu appears.</span></span> <span data-ttu-id="d70ad-115">Você também pode ver a fusão de entrada.</span><span class="sxs-lookup"><span data-stu-id="d70ad-115">You also can see the input merger.</span></span>

![Diagrama de trabalho com métricas - expandir partição](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="d70ad-117">Para ver o gráfico de métrica para uma única partição, selecione o nó da partição.</span><span class="sxs-lookup"><span data-stu-id="d70ad-117">To see the metric chart for only a single partition, select the partition node.</span></span> <span data-ttu-id="d70ad-118">As métricas são mostradas na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="d70ad-118">The metrics are shown at the bottom of the page.</span></span>

![Diagrama de trabalho com métricas - mais métricas](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="d70ad-120">Para ver o gráfico de métricas para uma fusão, selecione o nó da fusão.</span><span class="sxs-lookup"><span data-stu-id="d70ad-120">To see the metrics chart for a merger, select the merger node.</span></span> <span data-ttu-id="d70ad-121">O gráfico a seguir mostra que nenhum evento foi removido ou ajustado.</span><span class="sxs-lookup"><span data-stu-id="d70ad-121">The following chart shows that no events were dropped or adjusted.</span></span>

![Diagrama de trabalho com métricas - grade](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="d70ad-123">Para ver os detalhes do valor da métrica e do tempo, aponte para o gráfico.</span><span class="sxs-lookup"><span data-stu-id="d70ad-123">To see the details of the metric value and time, point to the chart.</span></span>

![Diagrama de trabalho com métricas - focalizar](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="d70ad-125">Solucionar problemas usando métricas</span><span class="sxs-lookup"><span data-stu-id="d70ad-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="d70ad-126">A métrica **QueryLastProcessedTime** indica quando uma etapa específica recebeu dados.</span><span class="sxs-lookup"><span data-stu-id="d70ad-126">The **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="d70ad-127">Observando a topologia, você pode trabalhar retroativamente do processador de saída para ver qual etapa não está recebendo dados.</span><span class="sxs-lookup"><span data-stu-id="d70ad-127">By looking at the topology, you can work backward from the output processor to see which step is not receiving data.</span></span> <span data-ttu-id="d70ad-128">Se uma etapa não estiver recebendo dados, vá para a etapa de consulta imediatamente anterior a ela.</span><span class="sxs-lookup"><span data-stu-id="d70ad-128">If a step is not getting data, go to the query step just before it.</span></span> <span data-ttu-id="d70ad-129">Verifique se a etapa de consulta anterior tem uma janela de tempo e se já passou tempo suficiente para a geração de dados.</span><span class="sxs-lookup"><span data-stu-id="d70ad-129">Check whether the preceding query step has a time window, and if enough time has passed for it to output data.</span></span> <span data-ttu-id="d70ad-130">(Observe que essas janelas de tempo são ajustadas com a hora.)</span><span class="sxs-lookup"><span data-stu-id="d70ad-130">(Note that time windows are snapped to the hour.)</span></span>
 
<span data-ttu-id="d70ad-131">Se a etapa de consulta anterior for um processador de entrada, use as métricas de entrada para ajudar a responder às perguntas direcionadas a seguir.</span><span class="sxs-lookup"><span data-stu-id="d70ad-131">If the preceding query step is an input processor, use the input metrics to help answer the following targeted questions.</span></span> <span data-ttu-id="d70ad-132">Elas podem ajudar a determinar se um trabalho está recebendo dados de suas fontes de entrada.</span><span class="sxs-lookup"><span data-stu-id="d70ad-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="d70ad-133">Se a consulta for particionada, examine cada partição.</span><span class="sxs-lookup"><span data-stu-id="d70ad-133">If the query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="d70ad-134">Qual o volume de dados que está sendo lindo?</span><span class="sxs-lookup"><span data-stu-id="d70ad-134">How much data is being read?</span></span>

*   <span data-ttu-id="d70ad-135">**InputEventsSourcesTotal** é o número de unidades de dados lidas.</span><span class="sxs-lookup"><span data-stu-id="d70ad-135">**InputEventsSourcesTotal** is the number of data units read.</span></span> <span data-ttu-id="d70ad-136">Por exemplo, o número de blobs.</span><span class="sxs-lookup"><span data-stu-id="d70ad-136">For example, the number of blobs.</span></span>
*   <span data-ttu-id="d70ad-137">**InputEventsTotal** é o número de eventos lidos.</span><span class="sxs-lookup"><span data-stu-id="d70ad-137">**InputEventsTotal** is the number of events read.</span></span> <span data-ttu-id="d70ad-138">Essa métrica está disponível por partição.</span><span class="sxs-lookup"><span data-stu-id="d70ad-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="d70ad-139">**InputEventsInBytesTotal** é o número de bytes lidos.</span><span class="sxs-lookup"><span data-stu-id="d70ad-139">**InputEventsInBytesTotal** is the number of bytes read.</span></span>
*   <span data-ttu-id="d70ad-140">**InputEventsLastArrivalTime** é atualizado com o tempo na fila de cada evento recebido.</span><span class="sxs-lookup"><span data-stu-id="d70ad-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="d70ad-141">O tempo está avançando?</span><span class="sxs-lookup"><span data-stu-id="d70ad-141">Is time moving forward?</span></span> <span data-ttu-id="d70ad-142">Se eventos reais forem lidos, a pontuação não poderá ser emitida.</span><span class="sxs-lookup"><span data-stu-id="d70ad-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="d70ad-143">**InputEventsLastPunctuationTime** indica quando uma pontuação foi emitida para manter o tempo avançando.</span><span class="sxs-lookup"><span data-stu-id="d70ad-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued to keep time moving forward.</span></span> <span data-ttu-id="d70ad-144">Se a pontuação não for emitida, o fluxo de dados poderá ser bloqueado.</span><span class="sxs-lookup"><span data-stu-id="d70ad-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-the-input"></a><span data-ttu-id="d70ad-145">Há erros na entrada?</span><span class="sxs-lookup"><span data-stu-id="d70ad-145">Are there any errors in the input?</span></span>

*   <span data-ttu-id="d70ad-146">**InputEventsEventDataNullTotal** é uma contagem de eventos que têm dados nulos.</span><span class="sxs-lookup"><span data-stu-id="d70ad-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="d70ad-147">**InputEventsSerializerErrorsTotal** é uma contagem de eventos que não puderam ser desserializados corretamente.</span><span class="sxs-lookup"><span data-stu-id="d70ad-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="d70ad-148">**InputEventsDegradedTotal** é uma contagem de eventos que tiveram um problema diferente de desserialização.</span><span class="sxs-lookup"><span data-stu-id="d70ad-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="d70ad-149">Os eventos estão sendo removidos ou ajustados?</span><span class="sxs-lookup"><span data-stu-id="d70ad-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="d70ad-150">**InputEventsEarlyTotal** é o número de eventos que têm um carimbo de data/hora do aplicativo antes da marca d'água alta.</span><span class="sxs-lookup"><span data-stu-id="d70ad-150">**InputEventsEarlyTotal** is the number of events that have an application timestamp before the high watermark.</span></span>
*   <span data-ttu-id="d70ad-151">**InputEventsLateTotal** é o número de eventos que têm um carimbo de data/hora do aplicativo depois da marca d'água alta.</span><span class="sxs-lookup"><span data-stu-id="d70ad-151">**InputEventsLateTotal** is the number of events that have an application timestamp after the high watermark.</span></span>
*   <span data-ttu-id="d70ad-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** é o número de eventos removidos antes da hora de início do trabalho.</span><span class="sxs-lookup"><span data-stu-id="d70ad-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is the number events dropped before the job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="d70ad-153">Estamos ficando para trás na leitura dos dados?</span><span class="sxs-lookup"><span data-stu-id="d70ad-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="d70ad-154">**InputEventsSourcesBackloggedTotal** informa quantas mensagens mais precisam ser lidas das entradas dos Hubs de Eventos e do Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="d70ad-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need to be read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="d70ad-155">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="d70ad-155">Get help</span></span>
<span data-ttu-id="d70ad-156">Para obter mais ajuda, teste nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="d70ad-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="d70ad-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d70ad-157">Next steps</span></span>
* [<span data-ttu-id="d70ad-158">Introdução ao Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d70ad-158">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="d70ad-159">Introdução ao Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d70ad-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="d70ad-160">Dimensionar trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d70ad-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="d70ad-161">Referência da linguagem de consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d70ad-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="d70ad-162">Referência da API REST de gerenciamento do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="d70ad-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
