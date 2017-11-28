---
title: "taxa de transferência tooincrease trabalhos de análise de fluxo de aaaScale | Microsoft Docs"
description: "Saiba como os trabalhos de análise de fluxo de tooscale configurar partições de entrada, ajustando a definição de consulta hello e definindo unidades de streaming de trabalhos."
keywords: "streaming de dados, processamento de dados de streaming, ajuste de análise"
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 7e857ddb-71dd-4537-b7ab-4524335d7b35
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/22/2017
ms.author: jeffstok
ms.openlocfilehash: 4ba8f6b2f8bfebd52cfa07696b501b42cda21f75
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-azure-stream-analytics-jobs-tooincrease-stream-data-processing-throughput"></a><span data-ttu-id="74aec-104">Escala do Azure Stream Analytics trabalhos tooincrease fluxo processamento de dados de taxa de transferência</span><span class="sxs-lookup"><span data-stu-id="74aec-104">Scale Azure Stream Analytics jobs tooincrease stream data processing throughput</span></span>
<span data-ttu-id="74aec-105">Este artigo mostra como tootune um Stream Analytics consultar tooincrease a taxa de transferência para trabalhos de análise de fluxo contínuo.</span><span class="sxs-lookup"><span data-stu-id="74aec-105">This article shows you how tootune a Stream Analytics query tooincrease throughput for Streaming Analytics jobs.</span></span> <span data-ttu-id="74aec-106">Você aprenderá como tooscale do Stream Analytics trabalhos configurando partições de entrada, definição de consulta de análise de ajuste hello e calcular e configuração de trabalho *unidades de streaming* (SUs).</span><span class="sxs-lookup"><span data-stu-id="74aec-106">You learn how tooscale Stream Analytics jobs by configuring input partitions, tuning hello analytics query definition, and calculating and setting job *streaming units* (SUs).</span></span> 

## <a name="what-are-hello-parts-of-a-stream-analytics-job"></a><span data-ttu-id="74aec-107">Quais são Olá partes de um trabalho do Stream Analytics?</span><span class="sxs-lookup"><span data-stu-id="74aec-107">What are hello parts of a Stream Analytics job?</span></span>
<span data-ttu-id="74aec-108">Uma definição de trabalho de Stream Analytics inclui entradas, consulta e saída.</span><span class="sxs-lookup"><span data-stu-id="74aec-108">A Stream Analytics job definition includes inputs, a query, and output.</span></span> <span data-ttu-id="74aec-109">As entradas são onde o trabalho Olá lê o fluxo de dados de saudação do.</span><span class="sxs-lookup"><span data-stu-id="74aec-109">Inputs are where hello job reads hello data stream from.</span></span> <span data-ttu-id="74aec-110">consulta Hello é fluxo de entrada hello dados tootransform usado e saída de hello é onde o trabalho Olá envia os resultados do trabalho Olá para.</span><span class="sxs-lookup"><span data-stu-id="74aec-110">hello query is used tootransform hello data input stream, and hello output is where hello job sends hello job results to.</span></span>  

<span data-ttu-id="74aec-111">Um trabalho requer pelo menos uma fonte de entrada para streaming de dados.</span><span class="sxs-lookup"><span data-stu-id="74aec-111">A job requires at least one input source for data streaming.</span></span> <span data-ttu-id="74aec-112">Olá fonte de entrada de fluxo de dados pode ser armazenado em um hub de eventos do Azure ou no armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="74aec-112">hello data stream input source can be stored in an Azure event hub or in Azure blob storage.</span></span> <span data-ttu-id="74aec-113">Para obter mais informações, consulte [tooAzure de Introdução do Stream Analytics](stream-analytics-introduction.md) e [começar a usar o Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span><span class="sxs-lookup"><span data-stu-id="74aec-113">For more information, see [Introduction tooAzure Stream Analytics](stream-analytics-introduction.md) and [Get started using Azure Stream Analytics](stream-analytics-real-time-fraud-detection.md).</span></span>

## <a name="partitions-in-event-hubs-and-azure-storage"></a><span data-ttu-id="74aec-114">Partições em Hubs de evento ou armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="74aec-114">Partitions in event hubs and Azure storage</span></span>
<span data-ttu-id="74aec-115">Dimensionamento de um trabalho do Stream Analytics aproveita partições Olá entrada ou saída.</span><span class="sxs-lookup"><span data-stu-id="74aec-115">Scaling a Stream Analytics job takes advantage of partitions in hello input or output.</span></span> <span data-ttu-id="74aec-116">Particionamento permite que você divida dados em subconjuntos com base em uma chave de partição.</span><span class="sxs-lookup"><span data-stu-id="74aec-116">Partitioning lets you divide data into subsets based on a partition key.</span></span> <span data-ttu-id="74aec-117">Um processo que consome dados hello (como um trabalho de análise de fluxo) pode consumir e gravar diferentes partições em paralelo, o que aumenta a taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="74aec-117">A process that consumes hello data (such as a Streaming Analytics job) can consume and write different partitions in parallel, which increases throughput.</span></span> <span data-ttu-id="74aec-118">Quando você trabalha com Streaming Analytics, você pode tirar proveito do particionamento em Hubs de eventos e em armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="74aec-118">When you work with Streaming Analytics, you can take advantage of partitioning in event hubs and in Blob storage.</span></span> 

<span data-ttu-id="74aec-119">Para obter mais informações sobre partições, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="74aec-119">For more information about partitions, see hello following articles:</span></span>

* [<span data-ttu-id="74aec-120">Visão geral dos recursos de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="74aec-120">Event Hubs features overview</span></span>](../event-hubs/event-hubs-features.md#partitions)
* [<span data-ttu-id="74aec-121">Particionamento de dados</span><span class="sxs-lookup"><span data-stu-id="74aec-121">Data partitioning</span></span>](https://docs.microsoft.com/azure/architecture/best-practices/data-partitioning#partitioning-azure-blob-storage)


## <a name="streaming-units-sus"></a><span data-ttu-id="74aec-122">Unidades de streaming (SUs)</span><span class="sxs-lookup"><span data-stu-id="74aec-122">Streaming units (SUs)</span></span>
<span data-ttu-id="74aec-123">Unidades (SUs) representam Olá recursos de streaming e computação de energia que são necessários na ordem tooexecute um trabalho do Stream Analytics do Azure.</span><span class="sxs-lookup"><span data-stu-id="74aec-123">Streaming units (SUs) represent hello resources and computing power that are required in order tooexecute an Azure Stream Analytics job.</span></span> <span data-ttu-id="74aec-124">SUs fornecem um maneira toodescribe Olá relativo de processamento de eventos capacidade com base em uma medida combinada de CPU, memória e leitura e gravação taxas.</span><span class="sxs-lookup"><span data-stu-id="74aec-124">SUs provide a way toodescribe hello relative event processing capacity based on a blended measure of CPU, memory, and read and write rates.</span></span> <span data-ttu-id="74aec-125">Cada SU corresponde tooroughly 1 MB/segundo de taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="74aec-125">Each SU corresponds tooroughly 1 MB/second of throughput.</span></span> 

<span data-ttu-id="74aec-126">Escolhendo o SUs quantos são necessários para um determinado trabalho depende na configuração de partição Olá para entradas de saudação e consulta Olá definidas para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="74aec-126">Choosing how many SUs are required for a particular job depends on hello partition configuration for hello inputs and on hello query defined for hello job.</span></span> <span data-ttu-id="74aec-127">Você pode selecionar a cota de tooyour em SUs para um trabalho.</span><span class="sxs-lookup"><span data-stu-id="74aec-127">You can select up tooyour quota in SUs for a job.</span></span> <span data-ttu-id="74aec-128">Por padrão, cada assinatura do Azure tem uma cota de backup too50 SUs para todos os trabalhos de análise de saudação em uma região específica.</span><span class="sxs-lookup"><span data-stu-id="74aec-128">By default, each Azure subscription has a quota of up too50 SUs for all hello analytics jobs in a specific region.</span></span> <span data-ttu-id="74aec-129">tooincrease SUs para suas assinaturas além essa cota, entre em contato com [Microsoft Support](http://support.microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="74aec-129">tooincrease SUs for your subscriptions beyond this quota, contact [Microsoft Support](http://support.microsoft.com).</span></span> <span data-ttu-id="74aec-130">Os valores válidos para o SUs por trabalho são 1, 3, 6 e em incrementos de 6.</span><span class="sxs-lookup"><span data-stu-id="74aec-130">Valid values for SUs per job are 1, 3, 6, and up in increments of 6.</span></span>

## <a name="embarrassingly-parallel-jobs"></a><span data-ttu-id="74aec-131">Trabalhos embaraçosamente paralelos</span><span class="sxs-lookup"><span data-stu-id="74aec-131">Embarrassingly parallel jobs</span></span>
<span data-ttu-id="74aec-132">Um *paralelo* trabalho é cenário mais escalonável hello, temos no Azure Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="74aec-132">An *embarrassingly parallel* job is hello most scalable scenario we have in Azure Stream Analytics.</span></span> <span data-ttu-id="74aec-133">Ele se conecta a uma partição da instância de entrada tooone Olá da partição de tooone Olá consulta de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="74aec-133">It connects one partition of hello input tooone instance of hello query tooone partition of hello output.</span></span> <span data-ttu-id="74aec-134">Esse paralelismo tem Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="74aec-134">This parallelism has hello following requirements:</span></span>

1. <span data-ttu-id="74aec-135">Se sua lógica de consulta depende Olá a mesma chave que está sendo processado por Olá mesma instância de consulta, você deve assegurar-se de que eventos Olá vão toohello mesma partição de sua entrada.</span><span class="sxs-lookup"><span data-stu-id="74aec-135">If your query logic depends on hello same key being processed by hello same query instance, you must make sure that hello events go toohello same partition of your input.</span></span> <span data-ttu-id="74aec-136">Para hubs de eventos, isso significa que os dados de evento de saudação devem ter Olá **PartitionKey** conjunto de valor.</span><span class="sxs-lookup"><span data-stu-id="74aec-136">For event hubs, this means that hello event data must have hello **PartitionKey** value set.</span></span> <span data-ttu-id="74aec-137">Como alternativa, você pode usar os remetentes particionados.</span><span class="sxs-lookup"><span data-stu-id="74aec-137">Alternatively, you can use partitioned senders.</span></span> <span data-ttu-id="74aec-138">Para o armazenamento de blob, isso significa que os eventos de saudação são enviados toohello mesma pasta de partição.</span><span class="sxs-lookup"><span data-stu-id="74aec-138">For blob storage, this means that hello events are sent toohello same partition folder.</span></span> <span data-ttu-id="74aec-139">Se sua lógica de consulta não requer Olá a mesma chave toobe processada por Olá mesma instância de consulta, você pode ignorar esse requisito.</span><span class="sxs-lookup"><span data-stu-id="74aec-139">If your query logic does not require hello same key toobe processed by hello same query instance, you can ignore this requirement.</span></span> <span data-ttu-id="74aec-140">Um exemplo disso seria uma consulta simples de seleção/projeto/filtro.</span><span class="sxs-lookup"><span data-stu-id="74aec-140">An example of this logic would be a simple select-project-filter query.</span></span>  

2. <span data-ttu-id="74aec-141">Depois de saudação dados são dispostos no lado de entrada hello, assegure-se de que sua consulta está particionada.</span><span class="sxs-lookup"><span data-stu-id="74aec-141">Once hello data is laid out on hello input side, you must make sure that your query is partitioned.</span></span> <span data-ttu-id="74aec-142">Isso exige que você toouse **Partition By** em todas as etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="74aec-142">This requires you toouse **Partition By** in all hello steps.</span></span> <span data-ttu-id="74aec-143">Várias etapas são permitidas, mas todos eles devem ser particionados por Olá mesma chave.</span><span class="sxs-lookup"><span data-stu-id="74aec-143">Multiple steps are allowed, but they all must be partitioned by hello same key.</span></span> <span data-ttu-id="74aec-144">Atualmente, Olá chave de particionamento deve ser definido muito**PartitionId** em ordem para Olá trabalho toobe totalmente paralelo.</span><span class="sxs-lookup"><span data-stu-id="74aec-144">Currently, hello partitioning key must be set too**PartitionId** in order for hello job toobe fully parallel.</span></span>  

3. <span data-ttu-id="74aec-145">Atualmente, somente Hubs de eventos e armazenamento de Blobs permitem a saída particionada.</span><span class="sxs-lookup"><span data-stu-id="74aec-145">Currently only event hubs and blob storage support partitioned output.</span></span> <span data-ttu-id="74aec-146">Saída do hub de eventos, você deve configurar Olá partição chave toobe **PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="74aec-146">For event hub output, you must configure hello partition key toobe **PartitionId**.</span></span> <span data-ttu-id="74aec-147">Saída do armazenamento de blob, você não tem toodo, nada.</span><span class="sxs-lookup"><span data-stu-id="74aec-147">For blob storage output, you don't have toodo anything.</span></span>  

4. <span data-ttu-id="74aec-148">número de saudação de partições de entrada deve ser igual Olá número de partições de saída.</span><span class="sxs-lookup"><span data-stu-id="74aec-148">hello number of input partitions must equal hello number of output partitions.</span></span> <span data-ttu-id="74aec-149">Atualmente, o armazenamento de Blobs de saída não suporta partições.</span><span class="sxs-lookup"><span data-stu-id="74aec-149">Blob storage output doesn't currently support partitions.</span></span> <span data-ttu-id="74aec-150">Mas isso é okey, porque ele herda Olá esquema da consulta upstream Olá de particionamento.</span><span class="sxs-lookup"><span data-stu-id="74aec-150">But that's okay, because it inherits hello partitioning scheme of hello upstream query.</span></span> <span data-ttu-id="74aec-151">Exemplos de valores de partição que permitem um trabalho totalmente paralelo:</span><span class="sxs-lookup"><span data-stu-id="74aec-151">Here are examples of partition values that allow a fully parallel job:</span></span>  

   * <span data-ttu-id="74aec-152">8 partições de entrada de Hubs de Eventos e 8 partições de saída de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="74aec-152">8 event hub input partitions and 8 event hub output partitions</span></span>
   * <span data-ttu-id="74aec-153">8 partições de entrada de Hubs de Eventos e Saída de armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="74aec-153">8 event hub input partitions and blob storage output</span></span>  
   * <span data-ttu-id="74aec-154">8 partições de entrada de armazenamento de Blobs e Saída de armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="74aec-154">8 blob storage input partitions and blob storage output</span></span>  
   * <span data-ttu-id="74aec-155">8 partições de entrada de armazenamento de Blobs e 8 partições de saída de Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="74aec-155">8 blob storage input partitions and 8 event hub output partitions</span></span>  

<span data-ttu-id="74aec-156">Olá seções a seguir discutem alguns cenários de exemplo que são excessivamente paralelos.</span><span class="sxs-lookup"><span data-stu-id="74aec-156">hello following sections discuss some example scenarios that are embarrassingly parallel.</span></span>

### <a name="simple-query"></a><span data-ttu-id="74aec-157">Consulta simples</span><span class="sxs-lookup"><span data-stu-id="74aec-157">Simple query</span></span>

* <span data-ttu-id="74aec-158">Entrada: Hub de eventos com 8 partições</span><span class="sxs-lookup"><span data-stu-id="74aec-158">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="74aec-159">Saída: Hub de eventos com 8 partições</span><span class="sxs-lookup"><span data-stu-id="74aec-159">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="74aec-160">Consulta:</span><span class="sxs-lookup"><span data-stu-id="74aec-160">Query:</span></span>

    SELECT TollBoothId
    FROM Input1 Partition By PartitionId
    WHERE TollBoothId > 100

<span data-ttu-id="74aec-161">Essa consulta é um filtro simples.</span><span class="sxs-lookup"><span data-stu-id="74aec-161">This query is a simple filter.</span></span> <span data-ttu-id="74aec-162">Portanto, não precisamos tooworry sobre o particionamento de entrada hello que está sendo enviada toohello hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="74aec-162">Therefore, we don't need tooworry about partitioning hello input that is being sent toohello event hub.</span></span> <span data-ttu-id="74aec-163">Observe que essa consulta Olá inclui **partição por PartitionId**, portanto, ela preenche o requisito #2 anteriores.</span><span class="sxs-lookup"><span data-stu-id="74aec-163">Notice that hello query includes **Partition By PartitionId**, so it fulfills requirement #2 from earlier.</span></span> <span data-ttu-id="74aec-164">Saída de hello, precisamos de saída do hub de eventos do tooconfigure Olá no conjunto de chaves de partição Olá trabalho toohave Olá muito**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="74aec-164">For hello output, we need tooconfigure hello event hub output in hello job toohave hello parition key set too**PartitionId**.</span></span> <span data-ttu-id="74aec-165">Uma última verificação está toomake se Olá número de partições de entrada é igual toohello número de partições de saída.</span><span class="sxs-lookup"><span data-stu-id="74aec-165">One last check is toomake sure that hello number of input partitions is equal toohello number of output partitions.</span></span>

### <a name="query-with-a-grouping-key"></a><span data-ttu-id="74aec-166">Consulta com chave de agrupamento</span><span class="sxs-lookup"><span data-stu-id="74aec-166">Query with a grouping key</span></span>

* <span data-ttu-id="74aec-167">Entrada: Hub de eventos com 8 partições</span><span class="sxs-lookup"><span data-stu-id="74aec-167">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="74aec-168">Saída: Armazenamento de Blobs</span><span class="sxs-lookup"><span data-stu-id="74aec-168">Output: Blob storage</span></span>

<span data-ttu-id="74aec-169">Consulta:</span><span class="sxs-lookup"><span data-stu-id="74aec-169">Query:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="74aec-170">Esta consulta tem uma chave de agrupamento.</span><span class="sxs-lookup"><span data-stu-id="74aec-170">This query has a grouping key.</span></span> <span data-ttu-id="74aec-171">Portanto, Olá mesmo toobe principais necessidades processada pelo Olá mesmo consultar instâncias, o que significa que eventos devem ser enviados toohello hub de eventos de modo particionado.</span><span class="sxs-lookup"><span data-stu-id="74aec-171">Therefore, hello same key needs toobe processed by hello same query instance, which means that events must be sent toohello event hub in a partitioned manner.</span></span> <span data-ttu-id="74aec-172">Mas qual chave deve ser usada?</span><span class="sxs-lookup"><span data-stu-id="74aec-172">But which key should be used?</span></span> <span data-ttu-id="74aec-173">**PartitionId** é um conceito de lógica de trabalho.</span><span class="sxs-lookup"><span data-stu-id="74aec-173">**PartitionId** is a job-logic concept.</span></span> <span data-ttu-id="74aec-174">Olá chave nos preocupamos realmente é **TollBoothId**, portanto Olá **PartitionKey** valor dos dados de evento Olá deve ser **TollBoothId**.</span><span class="sxs-lookup"><span data-stu-id="74aec-174">hello key we actually care about is **TollBoothId**, so hello **PartitionKey** value of hello event data should be **TollBoothId**.</span></span> <span data-ttu-id="74aec-175">Podemos fazer isso na consulta Olá definindo **Partition By** muito**PartitionId**.</span><span class="sxs-lookup"><span data-stu-id="74aec-175">We do this in hello query by setting **Partition By** too**PartitionId**.</span></span> <span data-ttu-id="74aec-176">Como saída de hello é o armazenamento de blob, não precisamos tooworry sobre como configurar um valor de chave de partição, de acordo com o requisito #4.</span><span class="sxs-lookup"><span data-stu-id="74aec-176">Since hello output is blob storage, we don't need tooworry about configuring a partition key value, as per requirement #4.</span></span>

### <a name="multi-step-query-with-a-grouping-key"></a><span data-ttu-id="74aec-177">Consulta de várias etapas com chave de agrupamento</span><span class="sxs-lookup"><span data-stu-id="74aec-177">Multi-step query with a grouping key</span></span>
* <span data-ttu-id="74aec-178">Entrada: Hub de eventos com 8 partições</span><span class="sxs-lookup"><span data-stu-id="74aec-178">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="74aec-179">Saída: Instância de Hub de eventos com 8 partições</span><span class="sxs-lookup"><span data-stu-id="74aec-179">Output: Event hub instance with 8 partitions</span></span>

<span data-ttu-id="74aec-180">Consulta:</span><span class="sxs-lookup"><span data-stu-id="74aec-180">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="74aec-181">Esta consulta tem uma chave de agrupamento, Olá assim mesmo toobe principais necessidades processada pelo Olá mesma instância de consulta.</span><span class="sxs-lookup"><span data-stu-id="74aec-181">This query has a grouping key, so hello same key needs toobe processed by hello same query instance.</span></span> <span data-ttu-id="74aec-182">Podemos usar Olá a mesma estratégia como no exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="74aec-182">We can use hello same strategy as in hello previous example.</span></span> <span data-ttu-id="74aec-183">Nesse caso, a consulta de saudação tem várias etapas.</span><span class="sxs-lookup"><span data-stu-id="74aec-183">In this case, hello query has multiple steps.</span></span> <span data-ttu-id="74aec-184">Cada etapa tem **Partition By PartitionId**?</span><span class="sxs-lookup"><span data-stu-id="74aec-184">Does each step have **Partition By PartitionId**?</span></span> <span data-ttu-id="74aec-185">Sim, então consulta Olá preenche o requisito #3.</span><span class="sxs-lookup"><span data-stu-id="74aec-185">Yes, so hello query fulfills requirement #3.</span></span> <span data-ttu-id="74aec-186">Saída de hello, precisamos chave de partição Olá tooset muito**PartitionId**, conforme discutido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="74aec-186">For hello output, we need tooset hello partition key too**PartitionId**, as discussed earlier.</span></span> <span data-ttu-id="74aec-187">Também é possível observar que ele tem Olá mesmo número de partições como entrada hello.</span><span class="sxs-lookup"><span data-stu-id="74aec-187">We can also see that it has hello same number of partitions as hello input.</span></span>

## <a name="example-scenarios-that-are-not-embarrassingly-parallel"></a><span data-ttu-id="74aec-188">Cenários de exemplo que *não* são embaraçosamente paralelos</span><span class="sxs-lookup"><span data-stu-id="74aec-188">Example scenarios that are *not* embarrassingly parallel</span></span>

<span data-ttu-id="74aec-189">Na seção anterior do hello, mostramos alguns cenários em paralelos.</span><span class="sxs-lookup"><span data-stu-id="74aec-189">In hello previous section, we showed some embarrassingly parallel scenarios.</span></span> <span data-ttu-id="74aec-190">Nesta seção, vamos discutir os cenários que não atendem a todos os Olá requisitos toobe paralelo.</span><span class="sxs-lookup"><span data-stu-id="74aec-190">In this section, we discuss scenarios that don't meet all hello requirements toobe embarrassingly parallel.</span></span> 

### <a name="mismatched-partition-count"></a><span data-ttu-id="74aec-191">Contagem de partições incompatível</span><span class="sxs-lookup"><span data-stu-id="74aec-191">Mismatched partition count</span></span>
* <span data-ttu-id="74aec-192">Entrada: Hub de eventos com 8 partições</span><span class="sxs-lookup"><span data-stu-id="74aec-192">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="74aec-193">Saída: Hub de eventos com 32 partições</span><span class="sxs-lookup"><span data-stu-id="74aec-193">Output: Event hub with 32 partitions</span></span>

<span data-ttu-id="74aec-194">Nesse caso, não importa qual consulta Olá é.</span><span class="sxs-lookup"><span data-stu-id="74aec-194">In this case, it doesn't matter what hello query is.</span></span> <span data-ttu-id="74aec-195">Se a contagem de partição de entrada hello não coincidir com a contagem de partições de saída de hello, topologia de saudação não é paralela.</span><span class="sxs-lookup"><span data-stu-id="74aec-195">If hello input partition count doesn't match hello output partition count, hello topology isn't embarrassingly parallel.</span></span>

### <a name="not-using-event-hubs-or-blob-storage-as-output"></a><span data-ttu-id="74aec-196">Não usando Hubs de Eventos ou armazenamento de Blobs como saída</span><span class="sxs-lookup"><span data-stu-id="74aec-196">Not using event hubs or blob storage as output</span></span>
* <span data-ttu-id="74aec-197">Entrada: Hub de eventos com 8 partições</span><span class="sxs-lookup"><span data-stu-id="74aec-197">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="74aec-198">Saída: PowerBI</span><span class="sxs-lookup"><span data-stu-id="74aec-198">Output: PowerBI</span></span>

<span data-ttu-id="74aec-199">Atualmente, a saída do PowerBI não suporta particionamento.</span><span class="sxs-lookup"><span data-stu-id="74aec-199">PowerBI output doesn't currently support partitioning.</span></span> <span data-ttu-id="74aec-200">Portanto, esse cenário não é embaraçosamente paralelo.</span><span class="sxs-lookup"><span data-stu-id="74aec-200">Therefore, this scenario is not embarrassingly parallel.</span></span>

### <a name="multi-step-query-with-different-partition-by-values"></a><span data-ttu-id="74aec-201">Consulta de várias etapas com diferentes valores por partição</span><span class="sxs-lookup"><span data-stu-id="74aec-201">Multi-step query with different Partition By values</span></span>
* <span data-ttu-id="74aec-202">Entrada: Hub de eventos com 8 partições</span><span class="sxs-lookup"><span data-stu-id="74aec-202">Input: Event hub with 8 partitions</span></span>
* <span data-ttu-id="74aec-203">Saída: Hub de eventos com 8 partições</span><span class="sxs-lookup"><span data-stu-id="74aec-203">Output: Event hub with 8 partitions</span></span>

<span data-ttu-id="74aec-204">Consulta:</span><span class="sxs-lookup"><span data-stu-id="74aec-204">Query:</span></span>

    WITH Step1 AS (
    SELECT COUNT(*) AS Count, TollBoothId, PartitionId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1 Partition By TollBoothId
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="74aec-205">Como você pode ver, Olá segunda etapa usa **TollBoothId** como Olá chave de particionamento.</span><span class="sxs-lookup"><span data-stu-id="74aec-205">As you can see, hello second step uses **TollBoothId** as hello partitioning key.</span></span> <span data-ttu-id="74aec-206">Esta etapa não é Olá mesmo como primeira etapa do hello e, portanto, requer nos toodo uma ordem aleatória.</span><span class="sxs-lookup"><span data-stu-id="74aec-206">This step is not hello same as hello first step, and it therefore requires us toodo a shuffle.</span></span> 

<span data-ttu-id="74aec-207">Olá exemplos anteriores mostram alguns trabalhos do Stream Analytics que está de acordo com muito (ou não) em uma topologia em paralela.</span><span class="sxs-lookup"><span data-stu-id="74aec-207">hello preceding examples show some Stream Analytics jobs that conform too(or don't) an embarrassingly parallel topology.</span></span> <span data-ttu-id="74aec-208">Se eles estão em conformidade, eles têm o potencial de saudação para expansão máxima.</span><span class="sxs-lookup"><span data-stu-id="74aec-208">If they do conform, they have hello potential for maximum scale.</span></span> <span data-ttu-id="74aec-209">Para trabalhos que não se encaixam em nenhum desses perfis, as diretrizes de expansão estarão disponíveis em atualizações futuras.</span><span class="sxs-lookup"><span data-stu-id="74aec-209">For jobs that don't fit one of these profiles, scaling guidance will be available in future updates.</span></span> <span data-ttu-id="74aec-210">Por enquanto, use diretrizes gerais de saudação em Olá seções a seguir.</span><span class="sxs-lookup"><span data-stu-id="74aec-210">For now, use hello general guidance in hello following sections.</span></span>

## <a name="calculate-hello-maximum-streaming-units-of-a-job"></a><span data-ttu-id="74aec-211">Calcular a saudação unidades de streaming de máximo de um trabalho</span><span class="sxs-lookup"><span data-stu-id="74aec-211">Calculate hello maximum streaming units of a job</span></span>
<span data-ttu-id="74aec-212">número total de saudação de unidades de streaming que pode ser usado por um trabalho do Stream Analytics depende do número Olá das etapas de consulta Olá definidos para trabalho hello e número de saudação de partições para cada etapa.</span><span class="sxs-lookup"><span data-stu-id="74aec-212">hello total number of streaming units that can be used by a Stream Analytics job depends on hello number of steps in hello query defined for hello job and hello number of partitions for each step.</span></span>

### <a name="steps-in-a-query"></a><span data-ttu-id="74aec-213">Etapas de uma consulta</span><span class="sxs-lookup"><span data-stu-id="74aec-213">Steps in a query</span></span>
<span data-ttu-id="74aec-214">Uma consulta pode ter uma ou mais etapas.</span><span class="sxs-lookup"><span data-stu-id="74aec-214">A query can have one or many steps.</span></span> <span data-ttu-id="74aec-215">Cada etapa é uma subconsulta definida por Olá **WITH** palavra-chave.</span><span class="sxs-lookup"><span data-stu-id="74aec-215">Each step is a subquery defined by hello **WITH** keyword.</span></span> <span data-ttu-id="74aec-216">consulta Olá fora Olá **WITH** palavra-chave (apenas uma consulta) também é contado como uma etapa, como Olá **selecione** instrução Olá consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="74aec-216">hello query that is outside hello **WITH** keyword (one query only) is also counted as a step, such as hello **SELECT** statement in hello following query:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute,3), TollBoothId

<span data-ttu-id="74aec-217">Esta consulta tem duas etapas.</span><span class="sxs-lookup"><span data-stu-id="74aec-217">This query has two steps.</span></span>

> [!NOTE]
> <span data-ttu-id="74aec-218">Essa consulta é abordada em mais detalhes posteriormente neste artigo hello.</span><span class="sxs-lookup"><span data-stu-id="74aec-218">This query is discussed in more detail later in hello article.</span></span>
>  

### <a name="partition-a-step"></a><span data-ttu-id="74aec-219">Uma etapa de partição</span><span class="sxs-lookup"><span data-stu-id="74aec-219">Partition a step</span></span>
<span data-ttu-id="74aec-220">Particionamento de uma etapa requer Olá condições a seguir:</span><span class="sxs-lookup"><span data-stu-id="74aec-220">Partitioning a step requires hello following conditions:</span></span>

* <span data-ttu-id="74aec-221">fonte de entrada Hello deve ser particionado.</span><span class="sxs-lookup"><span data-stu-id="74aec-221">hello input source must be partitioned.</span></span> 
* <span data-ttu-id="74aec-222">Olá **selecione** instrução de consulta Olá deve ler de uma fonte de entrada particionada.</span><span class="sxs-lookup"><span data-stu-id="74aec-222">hello **SELECT** statement of hello query must read from a partitioned input source.</span></span>
* <span data-ttu-id="74aec-223">consulta de saudação na etapa Olá deve ter Olá **Partition By** palavra-chave.</span><span class="sxs-lookup"><span data-stu-id="74aec-223">hello query within hello step must have hello **Partition By** keyword.</span></span>

<span data-ttu-id="74aec-224">Quando uma consulta for particionada, eventos de entrada hello são processados e agregados na partição separada grupos e saídas de eventos são geradas para cada um dos grupos de saudação.</span><span class="sxs-lookup"><span data-stu-id="74aec-224">When a query is partitioned, hello input events are processed and aggregated in separate partition groups, and outputs events are generated for each of hello groups.</span></span> <span data-ttu-id="74aec-225">Se você quiser uma agregação combinada, você deve criar um segundo tooaggregate de etapa não particionado.</span><span class="sxs-lookup"><span data-stu-id="74aec-225">If you want a combined aggregate, you must create a second non-partitioned step tooaggregate.</span></span>

### <a name="calculate-hello-max-streaming-units-for-a-job"></a><span data-ttu-id="74aec-226">Calcule o máximo de saudação unidades para um trabalho de streaming</span><span class="sxs-lookup"><span data-stu-id="74aec-226">Calculate hello max streaming units for a job</span></span>
<span data-ttu-id="74aec-227">Juntas, todas as etapas não particionado podem escalar verticalmente toosix unidades (SUs) para um trabalho de análise de fluxo de streaming.</span><span class="sxs-lookup"><span data-stu-id="74aec-227">All non-partitioned steps together can scale up toosix streaming units (SUs) for a Stream Analytics job.</span></span> <span data-ttu-id="74aec-228">SUs tooadd, uma etapa devem ser particionado.</span><span class="sxs-lookup"><span data-stu-id="74aec-228">tooadd SUs, a step must be partitioned.</span></span> <span data-ttu-id="74aec-229">Cada partição pode ter seis unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="74aec-229">Each partition can have six SUs.</span></span>

<table border="1">
<tr><th><span data-ttu-id="74aec-230">Consultar</span><span class="sxs-lookup"><span data-stu-id="74aec-230">Query</span></span></th><th><span data-ttu-id="74aec-231">SUs máxima para o trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="74aec-231">Max SUs for hello job</span></span></th></td>

<tr><td>
<ul>
<li><span data-ttu-id="74aec-232">consulta de saudação contém uma etapa.</span><span class="sxs-lookup"><span data-stu-id="74aec-232">hello query contains one step.</span></span></li>
<li><span data-ttu-id="74aec-233">etapa Olá não está particionada.</span><span class="sxs-lookup"><span data-stu-id="74aec-233">hello step is not partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="74aec-234">6</span><span class="sxs-lookup"><span data-stu-id="74aec-234">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="74aec-235">fluxo de dados de entrada Hello é particionado por 3.</span><span class="sxs-lookup"><span data-stu-id="74aec-235">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="74aec-236">consulta de saudação contém uma etapa.</span><span class="sxs-lookup"><span data-stu-id="74aec-236">hello query contains one step.</span></span></li>
<li><span data-ttu-id="74aec-237">etapa Hello está particionada.</span><span class="sxs-lookup"><span data-stu-id="74aec-237">hello step is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="74aec-238">18</span><span class="sxs-lookup"><span data-stu-id="74aec-238">18</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="74aec-239">consulta de saudação contém duas etapas.</span><span class="sxs-lookup"><span data-stu-id="74aec-239">hello query contains two steps.</span></span></li>
<li><span data-ttu-id="74aec-240">Nenhuma das etapas de saudação é particionada.</span><span class="sxs-lookup"><span data-stu-id="74aec-240">Neither of hello steps is partitioned.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="74aec-241">6</span><span class="sxs-lookup"><span data-stu-id="74aec-241">6</span></span></td></tr>

<tr><td>
<ul>
<li><span data-ttu-id="74aec-242">fluxo de dados de entrada Hello é particionado por 3.</span><span class="sxs-lookup"><span data-stu-id="74aec-242">hello input data stream is partitioned by 3.</span></span></li>
<li><span data-ttu-id="74aec-243">consulta de saudação contém duas etapas.</span><span class="sxs-lookup"><span data-stu-id="74aec-243">hello query contains two steps.</span></span> <span data-ttu-id="74aec-244">etapa de entrada Hello está particionada e Olá segunda etapa não é.</span><span class="sxs-lookup"><span data-stu-id="74aec-244">hello input step is partitioned and hello second step is not.</span></span></li>
<li><span data-ttu-id="74aec-245">Olá <strong>selecione</strong> lê de declaração de entrada hello particionada.</span><span class="sxs-lookup"><span data-stu-id="74aec-245">hello <strong>SELECT</strong> statement reads from hello partitioned input.</span></span></li>
</ul>
</td>
<td><span data-ttu-id="74aec-246">24 (18 para as etapas particionadas + 6 para as etapas não particionadas)</span><span class="sxs-lookup"><span data-stu-id="74aec-246">24 (18 for partitioned steps + 6 for non-partitioned steps)</span></span></td></tr>
</table>

### <a name="examples-of-scaling"></a><span data-ttu-id="74aec-247">Exemplos de escala</span><span class="sxs-lookup"><span data-stu-id="74aec-247">Examples of scaling</span></span>

<span data-ttu-id="74aec-248">Olá, consulta a seguir calcula Olá número de carros dentro de uma janela de três minutos passando por uma estação de pedágio que tem três tollbooths.</span><span class="sxs-lookup"><span data-stu-id="74aec-248">hello following query calculates hello number of cars within a three-minute window going through a toll station that has three tollbooths.</span></span> <span data-ttu-id="74aec-249">Essa consulta pode ser dimensionada toosix SUs.</span><span class="sxs-lookup"><span data-stu-id="74aec-249">This query can be scaled up toosix SUs.</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="74aec-250">toouse mais SUs para Olá consulta, ambos Olá fluxo de dados de entrada e consulta Olá deve ser particionada.</span><span class="sxs-lookup"><span data-stu-id="74aec-250">toouse more SUs for hello query, both hello input data stream and hello query must be partitioned.</span></span> <span data-ttu-id="74aec-251">Como partição de fluxo de dados hello está definida too3, hello seguinte consulta modificada pode ser dimensionada too18 SUs:</span><span class="sxs-lookup"><span data-stu-id="74aec-251">Since hello data stream partition is set too3, hello following modified query can be scaled up too18 SUs:</span></span>

    SELECT COUNT(*) AS Count, TollBoothId
    FROM Input1 Partition By PartitionId
    GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId

<span data-ttu-id="74aec-252">Quando uma consulta for particionada, eventos de entrada hello são processados e agregados em grupos de partição separada.</span><span class="sxs-lookup"><span data-stu-id="74aec-252">When a query is partitioned, hello input events are processed and aggregated in separate partition groups.</span></span> <span data-ttu-id="74aec-253">Eventos de saída também são gerados para cada um dos grupos de saudação.</span><span class="sxs-lookup"><span data-stu-id="74aec-253">Output events are also generated for each of hello groups.</span></span> <span data-ttu-id="74aec-254">O particionamento pode fazer com que alguns resultados inesperados quando hello **GROUP BY** campo não é uma chave de partição Olá no fluxo de dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="74aec-254">Partitioning can cause some unexpected results when hello **GROUP BY** field is not hello partition key in hello input data stream.</span></span> <span data-ttu-id="74aec-255">Por exemplo, Olá **TollBoothId** campo na consulta anterior Olá não é chave de partição de saudação do **Entrada1**.</span><span class="sxs-lookup"><span data-stu-id="74aec-255">For example, hello **TollBoothId** field in hello previous query is not hello partition key of **Input1**.</span></span> <span data-ttu-id="74aec-256">resultado de saudação é que hello dados de pedágio #1 possam ser distribuídos em várias partições.</span><span class="sxs-lookup"><span data-stu-id="74aec-256">hello result is that hello data from TollBooth #1 can be spread in multiple partitions.</span></span>

<span data-ttu-id="74aec-257">Cada Olá **Entrada1** partições serão processadas separadamente pela análise de fluxo.</span><span class="sxs-lookup"><span data-stu-id="74aec-257">Each of hello **Input1** partitions will be processed separately by Stream Analytics.</span></span> <span data-ttu-id="74aec-258">Como resultado, vários registros de contagem de carro Olá para Olá mesmo pedágio em Olá mesma janela em cascata será criada.</span><span class="sxs-lookup"><span data-stu-id="74aec-258">As a result, multiple records of hello car count for hello same tollbooth in hello same Tumbling window will be created.</span></span> <span data-ttu-id="74aec-259">Se a chave de partição de entrada hello não pode ser alterado, esse problema pode ser corrigido adicionando uma etapa de partição não, como no exemplo a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="74aec-259">If hello input partition key can't be changed, this problem can be fixed by adding a non-partition step, as in hello following example:</span></span>

    WITH Step1 AS (
        SELECT COUNT(*) AS Count, TollBoothId
        FROM Input1 Partition By PartitionId
        GROUP BY TumblingWindow(minute, 3), TollBoothId, PartitionId
    )

    SELECT SUM(Count) AS Count, TollBoothId
    FROM Step1
    GROUP BY TumblingWindow(minute, 3), TollBoothId

<span data-ttu-id="74aec-260">Essa consulta pode ser dimensionado too24 SUs.</span><span class="sxs-lookup"><span data-stu-id="74aec-260">This query can be scaled too24 SUs.</span></span>

> [!NOTE]
> <span data-ttu-id="74aec-261">Se você estiver unindo os dois fluxos, certifique-se de que fluxos Olá são particionados por chave de partição de saudação da coluna de saudação que você use toocreate Olá junções.</span><span class="sxs-lookup"><span data-stu-id="74aec-261">If you are joining two streams, make sure that hello streams are partitioned by hello partition key of hello column that you use toocreate hello joins.</span></span> <span data-ttu-id="74aec-262">Também, certifique-se de que você tenha Olá mesmo número de partições em ambos os fluxos.</span><span class="sxs-lookup"><span data-stu-id="74aec-262">Also make sure that you have hello same number of partitions in both streams.</span></span>
> 
> 

## <a name="configure-stream-analytics-streaming-units"></a><span data-ttu-id="74aec-263">Configurar as unidades de streaming do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="74aec-263">Configure Stream Analytics streaming units</span></span>

1. <span data-ttu-id="74aec-264">Entrar toohello [portal do Azure](https://portal.azure.com).</span><span class="sxs-lookup"><span data-stu-id="74aec-264">Sign in toohello [Azure portal](https://portal.azure.com).</span></span>
2. <span data-ttu-id="74aec-265">Na lista de saudação de recursos, localize o trabalho de análise de fluxo de saudação que você deseja tooscale e abra-o.</span><span class="sxs-lookup"><span data-stu-id="74aec-265">In hello list of resources, find hello Stream Analytics job that you want tooscale and then open it.</span></span>
3. <span data-ttu-id="74aec-266">Em Olá trabalho folha, em **configurar**, clique em **escala**.</span><span class="sxs-lookup"><span data-stu-id="74aec-266">In hello job blade, under **Configure**, click **Scale**.</span></span>

    ![Configuração de trabalho do Stream Analytics no Portal do Azure][img.stream.analytics.preview.portal.settings.scale]

4. <span data-ttu-id="74aec-268">Use Olá controle deslizante tooset hello SUs para trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="74aec-268">Use hello slider tooset hello SUs for hello job.</span></span> <span data-ttu-id="74aec-269">Observe que você está limitado toospecific configurações de SU.</span><span class="sxs-lookup"><span data-stu-id="74aec-269">Notice that you are limited toospecific SU settings.</span></span>


## <a name="monitor-job-performance"></a><span data-ttu-id="74aec-270">Monitorar o desempenho do trabalho</span><span class="sxs-lookup"><span data-stu-id="74aec-270">Monitor job performance</span></span>
<span data-ttu-id="74aec-271">Usando Olá portal do Azure, você pode controlar taxa de transferência de saudação de um trabalho:</span><span class="sxs-lookup"><span data-stu-id="74aec-271">Using hello Azure portal, you can track hello throughput of a job:</span></span>

![Análise de fluxo do Azure, monitorar trabalhos][img.stream.analytics.monitor.job]

<span data-ttu-id="74aec-273">Calcule taxa de transferência de saudação esperada de carga de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="74aec-273">Calculate hello expected throughput of hello workload.</span></span> <span data-ttu-id="74aec-274">Se a taxa de transferência de saudação é menor do que o esperado, ajustar a partição de entrada hello, ajustar a consulta hello e adicionar SUs tooyour trabalho.</span><span class="sxs-lookup"><span data-stu-id="74aec-274">If hello throughput is less than expected, tune hello input partition, tune hello query, and add SUs tooyour job.</span></span>


## <a name="visualize-stream-analytics-throughput-at-scale-hello-raspberry-pi-scenario"></a><span data-ttu-id="74aec-275">Visualizar a taxa de transferência do Stream Analytics em escala: cenário de Pi framboesa Olá</span><span class="sxs-lookup"><span data-stu-id="74aec-275">Visualize Stream Analytics throughput at scale: hello Raspberry Pi scenario</span></span>
<span data-ttu-id="74aec-276">toohelp que você entender como os trabalhos do Stream Analytics escala, realizamos uma experiência com base na entrada de um dispositivo de framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="74aec-276">toohelp you understand how Stream Analytics jobs scale, we performed an experiment based on input from a Raspberry Pi device.</span></span> <span data-ttu-id="74aec-277">Esse teste vamos ver o efeito de saudação na taxa de transferência de várias partições e unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="74aec-277">This experiment let us see hello effect on throughput of multiple streaming units and partitions.</span></span>

<span data-ttu-id="74aec-278">Nesse cenário, o dispositivo de saudação envia hub de eventos de tooan sensor dados (clientes).</span><span class="sxs-lookup"><span data-stu-id="74aec-278">In this scenario, hello device sends sensor data (clients) tooan event hub.</span></span> <span data-ttu-id="74aec-279">Análise de fluxo contínuo processa dados saudação e envia um alerta ou estatísticas como um hub de eventos de tooanother de saída.</span><span class="sxs-lookup"><span data-stu-id="74aec-279">Streaming Analytics processes hello data and sends an alert or statistics as an output tooanother event hub.</span></span> 

<span data-ttu-id="74aec-280">cliente Olá envia dados de sensor no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="74aec-280">hello client sends sensor data in JSON format.</span></span> <span data-ttu-id="74aec-281">a saída de dados Olá também está no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="74aec-281">hello data output is also in JSON format.</span></span> <span data-ttu-id="74aec-282">dados de saudação tem esta aparência:</span><span class="sxs-lookup"><span data-stu-id="74aec-282">hello data looks like this:</span></span>

    {"devicetime":"2014-12-11T02:24:56.8850110Z","hmdt":42.7,"temp":72.6,"prss":98187.75,"lght":0.38,"dspl":"R-PI Olivier's Office"}

<span data-ttu-id="74aec-283">Olá consulta a seguir é usado toosend um alerta quando uma luz é desligada:</span><span class="sxs-lookup"><span data-stu-id="74aec-283">hello following query is used toosend an alert when a light is switched off:</span></span>

    SELECT AVG(lght),
     "LightOff" as AlertText
    FROM input TIMESTAMP
    BY devicetime
     WHERE
        lght< 0.05 GROUP BY TumblingWindow(second, 1)

### <a name="measure-throughput"></a><span data-ttu-id="74aec-284">Medida de taxa de transferência</span><span class="sxs-lookup"><span data-stu-id="74aec-284">Measure throughput</span></span>

<span data-ttu-id="74aec-285">Nesse contexto, a taxa de transferência é a quantidade Olá de dados de entrada processados pela análise de fluxo em um determinado período de tempo.</span><span class="sxs-lookup"><span data-stu-id="74aec-285">In this context, throughput is hello amount of input data processed by Stream Analytics in a fixed amount of time.</span></span> <span data-ttu-id="74aec-286">(É medido por 10 minutos). dados de entrada tooachieve Olá melhor throughput de processamento para hello, entrada de fluxo de dados hello e consulta Olá foram particionadas.</span><span class="sxs-lookup"><span data-stu-id="74aec-286">(We measured for 10 minutes.) tooachieve hello best processing throughput for hello input data, both hello data stream input and hello query were  partitioned.</span></span> <span data-ttu-id="74aec-287">Incluímos **Count ()** em Olá consulta toomeasure quantos eventos de entrada foram processados.</span><span class="sxs-lookup"><span data-stu-id="74aec-287">We included **COUNT()** in hello query toomeasure how many input events were processed.</span></span> <span data-ttu-id="74aec-288">toomake se Olá trabalho foi não simplesmente aguardando toocome eventos de entrada, cada partição do hub de evento de entrada hello foi pré-carregado com cerca de 300 MB de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="74aec-288">toomake sure hello job was not simply waiting for input events toocome, each partition of hello input event hub was preloaded with about 300 MB of input data.</span></span>

<span data-ttu-id="74aec-289">Olá tabela a seguir mostra os resultados de saudação que vimos quando a partição correspondente Olá contagens hubs de eventos e aumentamos o número de saudação de unidades de streaming.</span><span class="sxs-lookup"><span data-stu-id="74aec-289">hello following table shows hello results we saw when we increased hello number of streaming units and hello corresponding partition counts in event hubs.</span></span>  

<table border="1">
<tr><th><span data-ttu-id="74aec-290">Partições de entrada</span><span class="sxs-lookup"><span data-stu-id="74aec-290">Input Partitions</span></span></th><th><span data-ttu-id="74aec-291">Partições de saída</span><span class="sxs-lookup"><span data-stu-id="74aec-291">Output Partitions</span></span></th><th><span data-ttu-id="74aec-292">Unidades de streaming</span><span class="sxs-lookup"><span data-stu-id="74aec-292">Streaming Units</span></span></th><th><span data-ttu-id="74aec-293">Taxa de transferência mantida</span><span class="sxs-lookup"><span data-stu-id="74aec-293">Sustained Throughput</span></span>
</th></td>

<tr><td><span data-ttu-id="74aec-294">12</span><span class="sxs-lookup"><span data-stu-id="74aec-294">12</span></span></td>
<td><span data-ttu-id="74aec-295">12</span><span class="sxs-lookup"><span data-stu-id="74aec-295">12</span></span></td>
<td><span data-ttu-id="74aec-296">6</span><span class="sxs-lookup"><span data-stu-id="74aec-296">6</span></span></td>
<td><span data-ttu-id="74aec-297">4,06 MB/s</span><span class="sxs-lookup"><span data-stu-id="74aec-297">4.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="74aec-298">12</span><span class="sxs-lookup"><span data-stu-id="74aec-298">12</span></span></td>
<td><span data-ttu-id="74aec-299">12</span><span class="sxs-lookup"><span data-stu-id="74aec-299">12</span></span></td>
<td><span data-ttu-id="74aec-300">12</span><span class="sxs-lookup"><span data-stu-id="74aec-300">12</span></span></td>
<td><span data-ttu-id="74aec-301">8,06 MB/s</span><span class="sxs-lookup"><span data-stu-id="74aec-301">8.06 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="74aec-302">48</span><span class="sxs-lookup"><span data-stu-id="74aec-302">48</span></span></td>
<td><span data-ttu-id="74aec-303">48</span><span class="sxs-lookup"><span data-stu-id="74aec-303">48</span></span></td>
<td><span data-ttu-id="74aec-304">48</span><span class="sxs-lookup"><span data-stu-id="74aec-304">48</span></span></td>
<td><span data-ttu-id="74aec-305">38,32 MB/s</span><span class="sxs-lookup"><span data-stu-id="74aec-305">38.32 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="74aec-306">192</span><span class="sxs-lookup"><span data-stu-id="74aec-306">192</span></span></td>
<td><span data-ttu-id="74aec-307">192</span><span class="sxs-lookup"><span data-stu-id="74aec-307">192</span></span></td>
<td><span data-ttu-id="74aec-308">192</span><span class="sxs-lookup"><span data-stu-id="74aec-308">192</span></span></td>
<td><span data-ttu-id="74aec-309">172,67 MB/s</span><span class="sxs-lookup"><span data-stu-id="74aec-309">172.67 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="74aec-310">480</span><span class="sxs-lookup"><span data-stu-id="74aec-310">480</span></span></td>
<td><span data-ttu-id="74aec-311">480</span><span class="sxs-lookup"><span data-stu-id="74aec-311">480</span></span></td>
<td><span data-ttu-id="74aec-312">480</span><span class="sxs-lookup"><span data-stu-id="74aec-312">480</span></span></td>
<td><span data-ttu-id="74aec-313">454,27 MB/s</span><span class="sxs-lookup"><span data-stu-id="74aec-313">454.27 MB/s</span></span></td>
</tr>

<tr><td><span data-ttu-id="74aec-314">720</span><span class="sxs-lookup"><span data-stu-id="74aec-314">720</span></span></td>
<td><span data-ttu-id="74aec-315">720</span><span class="sxs-lookup"><span data-stu-id="74aec-315">720</span></span></td>
<td><span data-ttu-id="74aec-316">720</span><span class="sxs-lookup"><span data-stu-id="74aec-316">720</span></span></td>
<td><span data-ttu-id="74aec-317">609,69 MB/s</span><span class="sxs-lookup"><span data-stu-id="74aec-317">609.69 MB/s</span></span></td>
</tr>
</table>

<span data-ttu-id="74aec-318">E hello, gráfico a seguir mostra uma visualização de relação de saudação entre SUs e taxa de transferência.</span><span class="sxs-lookup"><span data-stu-id="74aec-318">And hello following graph shows a visualization of hello relationship between SUs and throughput.</span></span>

![img.stream.analytics.perfgraph][img.stream.analytics.perfgraph]

## <a name="get-help"></a><span data-ttu-id="74aec-320">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="74aec-320">Get help</span></span>
<span data-ttu-id="74aec-321">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="74aec-321">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="74aec-322">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="74aec-322">Next steps</span></span>
* [<span data-ttu-id="74aec-323">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="74aec-323">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="74aec-324">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="74aec-324">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="74aec-325">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="74aec-325">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="74aec-326">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="74aec-326">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

<!--Image references-->

[img.stream.analytics.monitor.job]: ./media/stream-analytics-scale-jobs/StreamAnalytics.job.monitor-NewPortal.png
[img.stream.analytics.configure.scale]: ./media/stream-analytics-scale-jobs/StreamAnalytics.configure.scale.png
[img.stream.analytics.perfgraph]: ./media/stream-analytics-scale-jobs/perf.png
[img.stream.analytics.streaming.units.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsStreamingUnitsExample.jpg
[img.stream.analytics.preview.portal.settings.scale]: ./media/stream-analytics-scale-jobs/StreamAnalyticsPreviewPortalJobSettings-NewPortal.png   

<!--Link references-->

[microsoft.support]: http://support.microsoft.com
[azure.management.portal]: http://manage.windowsazure.com
[azure.event.hubs.developer.guide]: http://msdn.microsoft.com/library/azure/dn789972.aspx

[stream.analytics.introduction]: stream-analytics-introduction.md
[stream.analytics.get.started]: stream-analytics-real-time-fraud-detection.md
[stream.analytics.query.language.reference]: http://go.microsoft.com/fwlink/?LinkID=513299
[stream.analytics.rest.api.reference]: http://go.microsoft.com/fwlink/?LinkId=517301

