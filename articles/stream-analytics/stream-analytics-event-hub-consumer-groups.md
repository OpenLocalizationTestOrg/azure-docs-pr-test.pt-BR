---
title: Depurar o Stream Analytics do Azure com receptores do hub de eventos | Microsoft Docs
description: "Práticas recomendadas de consulta para consideração de grupos de consumidores dos Hubs de Eventos em trabalhos do Stream Analytics."
keywords: limite do hub de eventos, grupo de consumidores
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
ms.openlocfilehash: 145981d0b5eff0c574c5012c85f43a6318ba4126
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="fc71d-104">Depurar o Stream Analytics do Azure com receptores do hub de eventos</span><span class="sxs-lookup"><span data-stu-id="fc71d-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="fc71d-105">Você pode usar os Hubs de Eventos do Azure no Stream Analytics do Azure para ingerir ou gerar dados de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="fc71d-105">You can use Azure Event Hubs in Azure Stream Analytics to ingest or output data from a job.</span></span> <span data-ttu-id="fc71d-106">Uma prática recomendada para usar Hubs de Eventos é usar vários grupos de consumidores a fim de garantir a escalabilidade do trabalho.</span><span class="sxs-lookup"><span data-stu-id="fc71d-106">A best practice for using Event Hubs is to use multiple consumer groups, to ensure job scalability.</span></span> <span data-ttu-id="fc71d-107">Um dos motivos é que o número de leitores no trabalho do Stream Analytics para uma entrada específica afeta o número de leitores em um único grupo de consumidores.</span><span class="sxs-lookup"><span data-stu-id="fc71d-107">One reason is that the number of readers in the Stream Analytics job for a specific input affects the number of readers in a single consumer group.</span></span> <span data-ttu-id="fc71d-108">O número exato de receptores baseia-se nos detalhes da implementação interna para a lógica de topologia de expansão.</span><span class="sxs-lookup"><span data-stu-id="fc71d-108">The precise number of receivers is based on internal implementation details for the scale-out topology logic.</span></span> <span data-ttu-id="fc71d-109">O número de receptores não é exposto externamente.</span><span class="sxs-lookup"><span data-stu-id="fc71d-109">The number of receivers is not exposed externally.</span></span> <span data-ttu-id="fc71d-110">O número de leitores pode ser alterado na hora de início ou durante os upgrades do trabalho.</span><span class="sxs-lookup"><span data-stu-id="fc71d-110">The number of readers can change either at the job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="fc71d-111">Quando o número de leitores muda durante o upgrade de um trabalho, avisos temporários são gravados nos logs de auditoria.</span><span class="sxs-lookup"><span data-stu-id="fc71d-111">When the number of readers changes during a job upgrade, transient warnings are written to audit logs.</span></span> <span data-ttu-id="fc71d-112">Os trabalhos do Stream Analytics são recuperados automaticamente desses problemas transitórios.</span><span class="sxs-lookup"><span data-stu-id="fc71d-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="fc71d-113">Número de leitores por partição excede o limite de cinco dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="fc71d-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="fc71d-114">Os cenários em que o número de leitores por partição excede o limite de cinco dos Hubs de Eventos incluem os seguintes:</span><span class="sxs-lookup"><span data-stu-id="fc71d-114">Scenarios in which the number of readers per partition exceeds the Event Hubs limit of five include the following:</span></span>

* <span data-ttu-id="fc71d-115">Várias instruções SELECT: se você usar várias instruções SELECT que se refiram à **mesma** entrada do hub de eventos, cada instrução SELECT fará com que um novo receptor seja criado.</span><span class="sxs-lookup"><span data-stu-id="fc71d-115">Multiple SELECT statements: If you use multiple SELECT statements that refer to **same** event hub input, each SELECT statement causes a new receiver to be created.</span></span>
* <span data-ttu-id="fc71d-116">UNION: quando você usa UNION, é possível ter várias entradas que se refiram ao **mesmo** grupo de consumidores e hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="fc71d-116">UNION: When you use a UNION, it's possible to have multiple inputs that refer to the **same** event hub and consumer group.</span></span>
* <span data-ttu-id="fc71d-117">SELF JOIN: quando você usa uma operação SELF JOIN, é possível se referir ao **mesmo** hub de eventos várias vezes.</span><span class="sxs-lookup"><span data-stu-id="fc71d-117">SELF JOIN: When you use a SELF JOIN operation, it's possible to refer to the **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="fc71d-118">Solução</span><span class="sxs-lookup"><span data-stu-id="fc71d-118">Solution</span></span>

<span data-ttu-id="fc71d-119">As práticas recomendadas a seguir podem ajudar a minimizar cenários nos quais o número de leitores por partição excede o limite de cinco de Hubs de Eventos.</span><span class="sxs-lookup"><span data-stu-id="fc71d-119">The following best practices can help mitigate scenarios in which the number of readers per partition exceeds the Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="fc71d-120">Dividir a consulta em várias etapas usando uma cláusula WITH</span><span class="sxs-lookup"><span data-stu-id="fc71d-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="fc71d-121">A cláusula WITH especifica um conjunto de resultados nomeado temporário que pode ser referenciado por uma cláusula FROM na consulta.</span><span class="sxs-lookup"><span data-stu-id="fc71d-121">The WITH clause specifies a temporary named result set that can be referenced by a FROM clause in the query.</span></span> <span data-ttu-id="fc71d-122">Você define a cláusula WITH no escopo de execução de uma única instrução SELECT.</span><span class="sxs-lookup"><span data-stu-id="fc71d-122">You define the WITH clause in the execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="fc71d-123">Por exemplo, em vez desta consulta:</span><span class="sxs-lookup"><span data-stu-id="fc71d-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="fc71d-124">Use esta consulta:</span><span class="sxs-lookup"><span data-stu-id="fc71d-124">Use this query:</span></span>

```
WITH input (
   SELECT * FROM inputEventHub
) as data

SELECT foo
INTO output1
FROM data

SELECT bar
INTO output2
FROM data
…
```

### <a name="ensure-that-inputs-bind-to-different-consumer-groups"></a><span data-ttu-id="fc71d-125">Garantir que as entradas se associem a diferentes grupos de consumidores</span><span class="sxs-lookup"><span data-stu-id="fc71d-125">Ensure that inputs bind to different consumer groups</span></span>

<span data-ttu-id="fc71d-126">Para consultas em que três ou mais entradas estão conectadas ao mesmo grupo de consumidores de Hubs de Eventos, crie grupos de consumidores separados.</span><span class="sxs-lookup"><span data-stu-id="fc71d-126">For queries in which three or more inputs are connected to the same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="fc71d-127">Isso exige a criação de entradas adicionais do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="fc71d-127">This requires the creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="fc71d-128">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="fc71d-128">Get help</span></span>
<span data-ttu-id="fc71d-129">Para obter mais ajuda, teste nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="fc71d-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="fc71d-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fc71d-130">Next steps</span></span>
* [<span data-ttu-id="fc71d-131">Introdução ao Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fc71d-131">Introduction to Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="fc71d-132">Introdução ao Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fc71d-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="fc71d-133">Dimensionar trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fc71d-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="fc71d-134">Referência da linguagem de consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fc71d-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="fc71d-135">Referência da API REST de gerenciamento do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="fc71d-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
