---
title: "O Azure Stream Analytics: Otimizar seu toouse trabalho unidades de Streaming com eficiência | Microsoft Docs"
description: "Práticas recomendadas de consulta para dimensionamento e desempenho no Stream Analytics do Azure."
keywords: unidade de streaming, desempenho de consulta
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 5ad98b34d625190a879260f54c9eff0294e230cb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-your-job-toouse-streaming-units-efficiently"></a><span data-ttu-id="c4cdd-104">Otimizar seu toouse trabalho unidades de Streaming com eficiência</span><span class="sxs-lookup"><span data-stu-id="c4cdd-104">Optimize your job toouse Streaming Units efficiently</span></span>

<span data-ttu-id="c4cdd-105">O Azure Stream Analytics agrega desempenho hello "peso" da execução de um trabalho em unidades de Streaming (SUs).</span><span class="sxs-lookup"><span data-stu-id="c4cdd-105">Azure Stream Analytics aggregates hello performance "weight" of running a job into Streaming Units (SUs).</span></span> <span data-ttu-id="c4cdd-106">SUs representam os recursos de computação Olá que são consumido tooexecute um trabalho.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-106">SUs represent hello computing resources that are consumed tooexecute a job.</span></span> <span data-ttu-id="c4cdd-107">SUs fornecem um maneira toodescribe Olá relativo de processamento de eventos capacidade com base em uma medida combinada de CPU, memória e leitura e gravação taxas.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-107">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="c4cdd-108">Esse permite capacidade que você se concentre na lógica de consulta hello e remove você da necessidade de considerações de desempenho da camada de armazenamento tooknow, alocar memória para o trabalho manualmente e aproximado Olá CPU core-contagem necessário toorun seu trabalho de maneira oportuna.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-108">This capacity lets you focus on hello query logic and removes you from needing tooknow storage tier performance considerations, allocate memory for your job manually, and approximate hello CPU core-count needed toorun your job in a timely manner.</span></span>

## <a name="how-many-sus-are-required-for-a-job"></a><span data-ttu-id="c4cdd-109">Quantas SUs são necessárias para um trabalho?</span><span class="sxs-lookup"><span data-stu-id="c4cdd-109">How many SUs are required for a job?</span></span>

<span data-ttu-id="c4cdd-110">Escolher número de saudação do SUs necessário para um determinado trabalho depende da configuração de partição de saudação para entradas de saudação e consulta Olá que esteja definida no trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-110">Choosing hello number of required SUs for a particular job depends on hello partition configuration for hello inputs and hello query that's defined within hello job.</span></span> <span data-ttu-id="c4cdd-111">Olá **escala** folha permite tooset Olá número à direita do SUs.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-111">hello **Scale** blade allows you tooset hello right number of SUs.</span></span> <span data-ttu-id="c4cdd-112">É uma prática recomendada tooallocate SUs mais que o necessário.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-112">It is a best practice tooallocate more SUs than needed.</span></span> <span data-ttu-id="c4cdd-113">otimiza o mecanismo de processamento de análise de fluxo de saudação de latência e taxa de transferência no custo de saudação da alocação de memória adicional.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-113">hello Stream Analytics processing engine optimizes for latency and throughput at hello cost of allocating additional memory.</span></span>

<span data-ttu-id="c4cdd-114">Em geral, a prática recomendada de saudação é toostart com 6 SUs para consultas que não usam *PARTITION BY*.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-114">In general, hello best practice is toostart with 6 SUs for queries that don't use *PARTITION BY*.</span></span> <span data-ttu-id="c4cdd-115">Em seguida, determine o ponto central de saudação usando um método de tentativa e erro no qual você modifica número de saudação do SUs após passar representativas quantidades de dados e examinar a métrica de utilização do hello SU %.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-115">Then determine hello sweet spot by using a trial and error method in which you modify hello number of SUs after you pass representative amounts of data and examine hello SU %Utilization metric.</span></span>

<span data-ttu-id="c4cdd-116">A análise de fluxo do Azure mantém os eventos em uma janela chamada hello "reordenar buffer" antes de iniciar qualquer processamento.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-116">Azure Stream Analytics keeps events in a window called hello “reorder buffer” before it starts any processing.</span></span> <span data-ttu-id="c4cdd-117">Eventos são classificados na janela de reordenar Olá por hora e operações subsequentes são executadas em eventos Olá temporariamente classificado.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-117">Events are sorted within hello reorder window by time, and subsequent operations are performed on hello temporally sorted events.</span></span> <span data-ttu-id="c4cdd-118">Reordenar eventos por hora garante que esse operador Olá tem visibilidade de todos os eventos Olá Olá estipulado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-118">Reordering events by time ensures that hello operator has visibility into all hello events in hello stipulated timeframe.</span></span> <span data-ttu-id="c4cdd-119">Ele também permite operador Olá executar processamento requisito hello e produzir uma saída.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-119">It also lets hello operator perform hello requisite processing and produce an output.</span></span> <span data-ttu-id="c4cdd-120">Um efeito colateral esse mecanismo é que o processamento está atrasado por duração de saudação da janela de reordenar hello.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-120">A side effect of this mechanism is that processing is delayed by hello duration of hello reorder window.</span></span> <span data-ttu-id="c4cdd-121">espaço de memória de saudação do trabalho de saudação (que afeta o consumo SU) é uma função do tamanho de saudação desse número de janela e hello reordenar de eventos contidos nele.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-121">hello memory footprint of hello job (which affects SU consumption) is a function of hello size of this reorder window and hello number of events contained within it.</span></span>

> [!NOTE]
> <span data-ttu-id="c4cdd-122">Quando o número de saudação de leitores de alterado durante as atualizações do trabalho, transitórios avisos são gravados tooaudit logs.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-122">When hello number of readers changes during job upgrades, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="c4cdd-123">Os trabalhos do Stream Analytics são recuperados automaticamente desses problemas transitórios.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-123">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="common-high-memory-causes-for-high-su-usage-for-running-jobs"></a><span data-ttu-id="c4cdd-124">Causas comuns de memória alta para alto uso de SU na execução de trabalhos</span><span class="sxs-lookup"><span data-stu-id="c4cdd-124">Common high-memory causes for high SU usage for running jobs</span></span>

### <a name="high-cardinality-for-group-by"></a><span data-ttu-id="c4cdd-125">Alta cardinalidade para GROUP BY</span><span class="sxs-lookup"><span data-stu-id="c4cdd-125">High cardinality for GROUP BY</span></span>

<span data-ttu-id="c4cdd-126">cardinalidade Olá de eventos de entrada determina o uso de memória para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-126">hello cardinality of incoming events dictates memory usage for hello job.</span></span>

<span data-ttu-id="c4cdd-127">Por exemplo, em `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, Olá número associado **clusterizado** é cardinalidade Olá de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-127">For example, in `SELECT count(*) from input group by clustered, tumblingwindow (minutes, 5)`, hello number associated with **clustered** is hello cardinality of hello query.</span></span>

<span data-ttu-id="c4cdd-128">toomitigate problemas causados por alta cardinalidade, expansão consulta Olá aumentando partições usando **PARTITION BY**.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-128">toomitigate issues that are caused by high cardinality, scale out hello query by increasing partitions using **PARTITION BY**.</span></span>

```
Select count(*) from input
Partition By clusterid
GROUP BY clustered tumblingwindow (minutes, 5)
```

<span data-ttu-id="c4cdd-129">Olá inúmeros *clusterizado* é Olá cardinalidade de GROUP BY aqui.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-129">hello number of *clustered* is hello cardinality of GROUP BY here.</span></span>

<span data-ttu-id="c4cdd-130">Após a consulta Olá for particionada, ele distribuída por vários nós.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-130">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="c4cdd-131">Como resultado, Olá número de eventos que entram em cada nó é reduzido, que por sua vez reduz o tamanho de saudação do buffer de reordenar hello.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-131">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> <span data-ttu-id="c4cdd-132">Você também deve dividir partições do hub de eventos por id de partição.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-132">You should also partition event hub partitions by partitionid.</span></span>

### <a name="high-unmatched-event-count-for-join"></a><span data-ttu-id="c4cdd-133">Alta contagem de eventos sem correspondência para JOIN</span><span class="sxs-lookup"><span data-stu-id="c4cdd-133">High unmatched event count for JOIN</span></span>

<span data-ttu-id="c4cdd-134">número de saudação de eventos não correspondentes em uma junção afeta utilização de memória de saudação de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-134">hello number of unmatched events in a JOIN affects hello memory utilization of hello query.</span></span> <span data-ttu-id="c4cdd-135">Por exemplo, execute uma consulta que está procurando toofind Olá inúmeros impressões de anúncio que gera cliques:</span><span class="sxs-lookup"><span data-stu-id="c4cdd-135">For example, take a query that is looking toofind hello number of ad impressions that generates clicks:</span></span>

```
SELECT id from clicks INNER JOIN,
impressions on impressions.id = clicks.id AND DATEDIFF(hour, impressions, clicks) between 0 AND 10
```

<span data-ttu-id="c4cdd-136">Nesse cenário, é possível que vários anúncios sejam mostrados e poucos cliques sejam gerados.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-136">In this scenario, it is possible that many ads are shown and few clicks are generated.</span></span> <span data-ttu-id="c4cdd-137">Esse é um resultado exigiria Olá trabalho tookeep todos os eventos de saudação na janela de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-137">Such a result would require hello job tookeep all hello events within hello time window.</span></span> <span data-ttu-id="c4cdd-138">quantidade de saudação de memória consumida é a taxa de evento e o tamanho de janela toohello proporcional.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-138">hello amount of memory consumed is proportional toohello window size and event rate.</span></span> 

<span data-ttu-id="c4cdd-139">toomitigate nessa situação, a expansão de consulta Olá aumentando partições usando PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-139">toomitigate this situation, scale out hello query by increasing partitions by using PARTITION BY.</span></span> 

<span data-ttu-id="c4cdd-140">Após a consulta Olá for particionada, ele distribuída por vários nós de processamento.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-140">After hello query is partitioned, it is spread out over multiple processing nodes.</span></span> <span data-ttu-id="c4cdd-141">Como resultado, Olá número de eventos que entram em cada nó é reduzido, que por sua vez reduz o tamanho de saudação do buffer de reordenar hello.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-141">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span>

### <a name="large-number-of-out-of-order-events"></a><span data-ttu-id="c4cdd-142">Grande número de eventos fora de ordem</span><span class="sxs-lookup"><span data-stu-id="c4cdd-142">Large number of out of order events</span></span> 

<span data-ttu-id="c4cdd-143">Um grande número de eventos fora de ordem dentro de uma janela de tempo grande faz com que o tamanho de saudação do hello "reordenar buffer" toobe maior.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-143">A large number of out of order events within a large time window causes hello size of hello "reorder buffer" toobe larger.</span></span> <span data-ttu-id="c4cdd-144">toomitigate nessa situação, a consulta de saudação escala aumentando partições usando PARTITION BY.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-144">toomitigate this situation, scale hello query by increasing partitions by using PARTITION BY.</span></span> <span data-ttu-id="c4cdd-145">Após a consulta Olá for particionada, ele distribuída por vários nós.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-145">After hello query is partitioned, it is spread out over multiple nodes.</span></span> <span data-ttu-id="c4cdd-146">Como resultado, Olá número de eventos que entram em cada nó é reduzido, que por sua vez reduz o tamanho de saudação do buffer de reordenar hello.</span><span class="sxs-lookup"><span data-stu-id="c4cdd-146">As a result, hello number of events coming into each node is reduced, which in turn reduces hello size of hello reorder buffer.</span></span> 


## <a name="get-help"></a><span data-ttu-id="c4cdd-147">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="c4cdd-147">Get help</span></span>
<span data-ttu-id="c4cdd-148">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="c4cdd-148">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c4cdd-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c4cdd-149">Next steps</span></span>
* [<span data-ttu-id="c4cdd-150">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="c4cdd-150">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="c4cdd-151">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="c4cdd-151">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="c4cdd-152">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="c4cdd-152">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="c4cdd-153">Referência de linguagem de consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="c4cdd-153">Azure Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="c4cdd-154">Referência da API REST do Gerenciamento do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="c4cdd-154">Azure Stream Analytics Management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
