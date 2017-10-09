---
title: "AAA Azure Stream Analytics controladas por dados depuração usando o diagrama de trabalho Olá | Microsoft Docs"
description: "Solucionar problemas de seu trabalho do Stream Analytics por meio de métricas e diagrama de trabalho hello."
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
ms.openlocfilehash: 1af884d485bebb06b034da01a13f7f8240516571
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="data-driven-debugging-by-using-hello-job-diagram"></a><span data-ttu-id="2879f-103">Depurando usando o diagrama de trabalho Olá controlada por dados</span><span class="sxs-lookup"><span data-stu-id="2879f-103">Data-driven debugging by using hello job diagram</span></span>

<span data-ttu-id="2879f-104">diagrama de trabalho Olá Olá **monitoramento** folha em Olá portal do Azure pode ajudá-lo a visualizar seu pipeline de trabalho.</span><span class="sxs-lookup"><span data-stu-id="2879f-104">hello job diagram on hello **Monitoring** blade in hello Azure portal can help you visualize your job pipeline.</span></span> <span data-ttu-id="2879f-105">Ele mostra entradas, saídas e etapas de consulta.</span><span class="sxs-lookup"><span data-stu-id="2879f-105">It shows inputs, outputs, and query steps.</span></span> <span data-ttu-id="2879f-106">Você pode usar métricas de Olá Olá trabalho diagrama tooexamine para cada etapa, toomore isolar rapidamente a origem de saudação de um problema ao solucionar problemas.</span><span class="sxs-lookup"><span data-stu-id="2879f-106">You can use hello job diagram tooexamine hello metrics for each step, toomore quickly isolate hello source of a problem when you troubleshoot issues.</span></span>

## <a name="using-hello-job-diagram"></a><span data-ttu-id="2879f-107">Usando o diagrama de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="2879f-107">Using hello job diagram</span></span>

<span data-ttu-id="2879f-108">Em Olá portal do Azure, enquanto um trabalho de análise de fluxo, em **suporte + solução de problemas**, selecione **diagrama trabalho**:</span><span class="sxs-lookup"><span data-stu-id="2879f-108">In hello Azure portal, while in a Stream Analytics job, under **SUPPORT + TROUBLESHOOTING**, select **Job diagram**:</span></span>

![Diagrama de trabalho com métricas - local](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-1.png)

<span data-ttu-id="2879f-110">Selecione cada seção correspondente de consulta etapa toosee Olá em uma painel de edição de consulta.</span><span class="sxs-lookup"><span data-stu-id="2879f-110">Select each query step toosee hello corresponding section in a query editing pane.</span></span> <span data-ttu-id="2879f-111">Um gráfico de métrica para a etapa de saudação é exibido em um painel inferior na página de saudação.</span><span class="sxs-lookup"><span data-stu-id="2879f-111">A metric chart for hello step is displayed in a lower pane on hello page.</span></span>

![Diagrama de trabalho com métricas - local](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-2.png)

<span data-ttu-id="2879f-113">partições de saudação toosee de entrada de Hubs de eventos do Azure hello, selecione **...**</span><span class="sxs-lookup"><span data-stu-id="2879f-113">toosee hello partitions of hello Azure Event Hubs input, select **. . .**</span></span> <span data-ttu-id="2879f-114">O menu de contexto é exibido.</span><span class="sxs-lookup"><span data-stu-id="2879f-114">A context menu appears.</span></span> <span data-ttu-id="2879f-115">Você também pode ver fusão de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="2879f-115">You also can see hello input merger.</span></span>

![Diagrama de trabalho com métricas - expandir partição](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-3.png)

<span data-ttu-id="2879f-117">gráfico métrica do hello toosee apenas uma única partição, nó de partição Olá select.</span><span class="sxs-lookup"><span data-stu-id="2879f-117">toosee hello metric chart for only a single partition, select hello partition node.</span></span> <span data-ttu-id="2879f-118">métricas de saudação são mostradas na parte inferior da saudação da página de saudação.</span><span class="sxs-lookup"><span data-stu-id="2879f-118">hello metrics are shown at hello bottom of hello page.</span></span>

![Diagrama de trabalho com métricas - mais métricas](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-4.png)

<span data-ttu-id="2879f-120">gráfico de métricas toosee Olá para uma fusão, nó de fusão Olá select.</span><span class="sxs-lookup"><span data-stu-id="2879f-120">toosee hello metrics chart for a merger, select hello merger node.</span></span> <span data-ttu-id="2879f-121">Olá gráfico a seguir mostra que não há eventos foram descartados ou ajustados.</span><span class="sxs-lookup"><span data-stu-id="2879f-121">hello following chart shows that no events were dropped or adjusted.</span></span>

![Diagrama de trabalho com métricas - grade](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-5.png)

<span data-ttu-id="2879f-123">detalhes de saudação toosee da hora toohello de ponto de gráfico e o valor de métrica hello.</span><span class="sxs-lookup"><span data-stu-id="2879f-123">toosee hello details of hello metric value and time, point toohello chart.</span></span>

![Diagrama de trabalho com métricas - focalizar](./media/stream-analytics-job-diagram-with-metrics/stream-analytics-job-diagram-with-metrics-portal-6.png)

## <a name="troubleshoot-by-using-metrics"></a><span data-ttu-id="2879f-125">Solucionar problemas usando métricas</span><span class="sxs-lookup"><span data-stu-id="2879f-125">Troubleshoot by using metrics</span></span>

<span data-ttu-id="2879f-126">Olá **QueryLastProcessedTime** métrica indica quando uma etapa específica recebeu dados.</span><span class="sxs-lookup"><span data-stu-id="2879f-126">hello **QueryLastProcessedTime** metric indicates when a specific step received data.</span></span> <span data-ttu-id="2879f-127">Examinando topologia hello, você pode trabalhar para trás da saudação saída processador toosee qual etapa não está recebendo dados.</span><span class="sxs-lookup"><span data-stu-id="2879f-127">By looking at hello topology, you can work backward from hello output processor toosee which step is not receiving data.</span></span> <span data-ttu-id="2879f-128">Se uma etapa não está recebendo dados, vá para etapa de consulta toohello antes dele.</span><span class="sxs-lookup"><span data-stu-id="2879f-128">If a step is not getting data, go toohello query step just before it.</span></span> <span data-ttu-id="2879f-129">Verifique se a etapa de consulta anterior hello tem uma janela de tempo, e se tiver passado tempo suficiente para que ele toooutput dados.</span><span class="sxs-lookup"><span data-stu-id="2879f-129">Check whether hello preceding query step has a time window, and if enough time has passed for it toooutput data.</span></span> <span data-ttu-id="2879f-130">(Observe que tempo windows são ajustada toohello horas.)</span><span class="sxs-lookup"><span data-stu-id="2879f-130">(Note that time windows are snapped toohello hour.)</span></span>
 
<span data-ttu-id="2879f-131">Se hello etapa de consulta anterior é um processador de entrada, use Olá métricas entrada toohelp resposta Olá destino perguntas a seguir.</span><span class="sxs-lookup"><span data-stu-id="2879f-131">If hello preceding query step is an input processor, use hello input metrics toohelp answer hello following targeted questions.</span></span> <span data-ttu-id="2879f-132">Elas podem ajudar a determinar se um trabalho está recebendo dados de suas fontes de entrada.</span><span class="sxs-lookup"><span data-stu-id="2879f-132">They can help you determine whether a job is getting data from its input sources.</span></span> <span data-ttu-id="2879f-133">Se a consulta Olá estiver particionada, examine cada partição.</span><span class="sxs-lookup"><span data-stu-id="2879f-133">If hello query is partitioned, examine each partition.</span></span>
 
### <a name="how-much-data-is-being-read"></a><span data-ttu-id="2879f-134">Qual o volume de dados que está sendo lindo?</span><span class="sxs-lookup"><span data-stu-id="2879f-134">How much data is being read?</span></span>

*   <span data-ttu-id="2879f-135">**InputEventsSourcesTotal** é Olá número de unidades de dados de leitura.</span><span class="sxs-lookup"><span data-stu-id="2879f-135">**InputEventsSourcesTotal** is hello number of data units read.</span></span> <span data-ttu-id="2879f-136">Olá, por exemplo, o número de blobs.</span><span class="sxs-lookup"><span data-stu-id="2879f-136">For example, hello number of blobs.</span></span>
*   <span data-ttu-id="2879f-137">**InputEventsTotal** é Olá número de eventos de leitura.</span><span class="sxs-lookup"><span data-stu-id="2879f-137">**InputEventsTotal** is hello number of events read.</span></span> <span data-ttu-id="2879f-138">Essa métrica está disponível por partição.</span><span class="sxs-lookup"><span data-stu-id="2879f-138">This metric is available per partition.</span></span>
*   <span data-ttu-id="2879f-139">**InputEventsInBytesTotal** é Olá número de bytes lidos.</span><span class="sxs-lookup"><span data-stu-id="2879f-139">**InputEventsInBytesTotal** is hello number of bytes read.</span></span>
*   <span data-ttu-id="2879f-140">**InputEventsLastArrivalTime** é atualizado com o tempo na fila de cada evento recebido.</span><span class="sxs-lookup"><span data-stu-id="2879f-140">**InputEventsLastArrivalTime** is updated with every received event's enqueued time.</span></span>
 
### <a name="is-time-moving-forward-if-actual-events-are-read-punctuation-might-not-be-issued"></a><span data-ttu-id="2879f-141">O tempo está avançando?</span><span class="sxs-lookup"><span data-stu-id="2879f-141">Is time moving forward?</span></span> <span data-ttu-id="2879f-142">Se eventos reais forem lidos, a pontuação não poderá ser emitida.</span><span class="sxs-lookup"><span data-stu-id="2879f-142">If actual events are read, punctuation might not be issued.</span></span>

*   <span data-ttu-id="2879f-143">**InputEventsLastPunctuationTime** indica quando uma pontuação foi emitida tookeep tempo mover para a frente.</span><span class="sxs-lookup"><span data-stu-id="2879f-143">**InputEventsLastPunctuationTime** indicates when a punctuation was issued tookeep time moving forward.</span></span> <span data-ttu-id="2879f-144">Se a pontuação não for emitida, o fluxo de dados poderá ser bloqueado.</span><span class="sxs-lookup"><span data-stu-id="2879f-144">If punctuation is not issued, data flow can get blocked.</span></span>
 
### <a name="are-there-any-errors-in-hello-input"></a><span data-ttu-id="2879f-145">Há erros na entrada Olá?</span><span class="sxs-lookup"><span data-stu-id="2879f-145">Are there any errors in hello input?</span></span>

*   <span data-ttu-id="2879f-146">**InputEventsEventDataNullTotal** é uma contagem de eventos que têm dados nulos.</span><span class="sxs-lookup"><span data-stu-id="2879f-146">**InputEventsEventDataNullTotal** is a count of events that have null data.</span></span>
*   <span data-ttu-id="2879f-147">**InputEventsSerializerErrorsTotal** é uma contagem de eventos que não puderam ser desserializados corretamente.</span><span class="sxs-lookup"><span data-stu-id="2879f-147">**InputEventsSerializerErrorsTotal** is a count of events that could not be deserialized correctly.</span></span>
*   <span data-ttu-id="2879f-148">**InputEventsDegradedTotal** é uma contagem de eventos que tiveram um problema diferente de desserialização.</span><span class="sxs-lookup"><span data-stu-id="2879f-148">**InputEventsDegradedTotal** is a count of events that had an issue other than with deserialization.</span></span>
 
### <a name="are-events-being-dropped-or-adjusted"></a><span data-ttu-id="2879f-149">Os eventos estão sendo removidos ou ajustados?</span><span class="sxs-lookup"><span data-stu-id="2879f-149">Are events being dropped or adjusted?</span></span>

*   <span data-ttu-id="2879f-150">**InputEventsEarlyTotal** é Olá número de eventos que têm um carimbo de hora do aplicativo antes de marca d'água alta de saudação.</span><span class="sxs-lookup"><span data-stu-id="2879f-150">**InputEventsEarlyTotal** is hello number of events that have an application timestamp before hello high watermark.</span></span>
*   <span data-ttu-id="2879f-151">**InputEventsLateTotal** é Olá número de eventos que têm um carimbo de hora do aplicativo após a marca d'água alta de saudação.</span><span class="sxs-lookup"><span data-stu-id="2879f-151">**InputEventsLateTotal** is hello number of events that have an application timestamp after hello high watermark.</span></span>
*   <span data-ttu-id="2879f-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** está Olá eventos número descartados antes da hora de início do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="2879f-152">**InputEventsDroppedBeforeApplicationStartTimeTotal** is hello number events dropped before hello job start time.</span></span>
 
### <a name="are-we-falling-behind-in-reading-data"></a><span data-ttu-id="2879f-153">Estamos ficando para trás na leitura dos dados?</span><span class="sxs-lookup"><span data-stu-id="2879f-153">Are we falling behind in reading data?</span></span>

*   <span data-ttu-id="2879f-154">**InputEventsSourcesBackloggedTotal** informa quantas mensagens mais precisam toobe ler para entradas de Hubs de eventos e o Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="2879f-154">**InputEventsSourcesBackloggedTotal** tells you how many more messages need toobe read for Event Hubs and Azure IoT Hub inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="2879f-155">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="2879f-155">Get help</span></span>
<span data-ttu-id="2879f-156">Para obter mais ajuda, teste nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="2879f-156">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="2879f-157">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2879f-157">Next steps</span></span>
* [<span data-ttu-id="2879f-158">Introdução tooStream análise</span><span class="sxs-lookup"><span data-stu-id="2879f-158">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="2879f-159">Introdução ao Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2879f-159">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="2879f-160">Dimensionar trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2879f-160">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="2879f-161">Referência da linguagem de consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2879f-161">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="2879f-162">Referência da API REST de gerenciamento do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="2879f-162">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
