---
title: aaaDebug Stream Analytics do Azure com receptores de evento de hub | Microsoft Docs
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
ms.openlocfilehash: 89821e6273151de43b5e42d907e547c939e24824
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-azure-stream-analytics-with-event-hub-receivers"></a><span data-ttu-id="9013e-104">Depurar o Stream Analytics do Azure com receptores do hub de eventos</span><span class="sxs-lookup"><span data-stu-id="9013e-104">Debug Azure Stream Analytics with event hub receivers</span></span>

<span data-ttu-id="9013e-105">Você pode usar os Hubs de eventos do Azure no Azure Stream Analytics tooingest ou saída de dados de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="9013e-105">You can use Azure Event Hubs in Azure Stream Analytics tooingest or output data from a job.</span></span> <span data-ttu-id="9013e-106">Uma prática recomendada para usar Hubs de eventos é toouse vários grupos de consumidores, tooensure escalabilidade de trabalho.</span><span class="sxs-lookup"><span data-stu-id="9013e-106">A best practice for using Event Hubs is toouse multiple consumer groups, tooensure job scalability.</span></span> <span data-ttu-id="9013e-107">Uma razão é que o número de Olá de leitores em trabalho do Stream Analytics Olá para uma entrada específica afeta número Olá de leitores em um grupo único consumidor.</span><span class="sxs-lookup"><span data-stu-id="9013e-107">One reason is that hello number of readers in hello Stream Analytics job for a specific input affects hello number of readers in a single consumer group.</span></span> <span data-ttu-id="9013e-108">número preciso de saudação de destinatários baseia-se nos detalhes de implementação interna Olá expansão topologia lógica.</span><span class="sxs-lookup"><span data-stu-id="9013e-108">hello precise number of receivers is based on internal implementation details for hello scale-out topology logic.</span></span> <span data-ttu-id="9013e-109">número de saudação de destinatários não está exposto externamente.</span><span class="sxs-lookup"><span data-stu-id="9013e-109">hello number of receivers is not exposed externally.</span></span> <span data-ttu-id="9013e-110">número de saudação de leitores de pode ser alterado na hora de início do trabalho de saudação ou durante as atualizações do trabalho.</span><span class="sxs-lookup"><span data-stu-id="9013e-110">hello number of readers can change either at hello job start time or during job upgrades.</span></span>

> [!NOTE]
> <span data-ttu-id="9013e-111">Quando o número de saudação de leitores alterado durante uma atualização de trabalho, transitórios avisos são gravados tooaudit logs.</span><span class="sxs-lookup"><span data-stu-id="9013e-111">When hello number of readers changes during a job upgrade, transient warnings are written tooaudit logs.</span></span> <span data-ttu-id="9013e-112">Os trabalhos do Stream Analytics são recuperados automaticamente desses problemas transitórios.</span><span class="sxs-lookup"><span data-stu-id="9013e-112">Stream Analytics jobs automatically recover from these transient issues.</span></span>

## <a name="number-of-readers-per-partition-exceeds-event-hubs-limit-of-five"></a><span data-ttu-id="9013e-113">Número de leitores por partição excede o limite de cinco dos Hubs de Eventos</span><span class="sxs-lookup"><span data-stu-id="9013e-113">Number of readers per partition exceeds Event Hubs limit of five</span></span>

<span data-ttu-id="9013e-114">Cenários no qual Olá número de leitores por partição excede o limite de Hubs de eventos de saudação de cinco incluem o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="9013e-114">Scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five include hello following:</span></span>

* <span data-ttu-id="9013e-115">Várias instruções SELECT: se você usar várias instruções SELECT que fazem referência muito**mesmo** hub de eventos de entrada, cada instrução SELECT faz com que um novo toobe de destinatário criado.</span><span class="sxs-lookup"><span data-stu-id="9013e-115">Multiple SELECT statements: If you use multiple SELECT statements that refer too**same** event hub input, each SELECT statement causes a new receiver toobe created.</span></span>
* <span data-ttu-id="9013e-116">UNIÃO: Quando você usa uma união, é possível toohave várias entradas que fazem referência toohello **mesmo** grupo de consumidor e hub de eventos.</span><span class="sxs-lookup"><span data-stu-id="9013e-116">UNION: When you use a UNION, it's possible toohave multiple inputs that refer toohello **same** event hub and consumer group.</span></span>
* <span data-ttu-id="9013e-117">AUTOJUNÇÃO: Quando você usa uma operação JOIN de AUTOATENDIMENTO, é possível toorefer toohello **mesmo** hub de eventos várias vezes.</span><span class="sxs-lookup"><span data-stu-id="9013e-117">SELF JOIN: When you use a SELF JOIN operation, it's possible toorefer toohello **same** event hub multiple times.</span></span>

## <a name="solution"></a><span data-ttu-id="9013e-118">Solução</span><span class="sxs-lookup"><span data-stu-id="9013e-118">Solution</span></span>

<span data-ttu-id="9013e-119">Olá práticas recomendadas a seguir podem ajudar a reduzir os cenários no qual Olá número de leitores por partição excede o limite de Hubs de eventos de saudação de cinco.</span><span class="sxs-lookup"><span data-stu-id="9013e-119">hello following best practices can help mitigate scenarios in which hello number of readers per partition exceeds hello Event Hubs limit of five.</span></span>

### <a name="split-your-query-into-multiple-steps-by-using-a-with-clause"></a><span data-ttu-id="9013e-120">Dividir a consulta em várias etapas usando uma cláusula WITH</span><span class="sxs-lookup"><span data-stu-id="9013e-120">Split your query into multiple steps by using a WITH clause</span></span>

<span data-ttu-id="9013e-121">cláusula WITH de saudação especifica um conjunto de resultados nomeado temporário que pode ser referenciado por uma cláusula FROM da consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="9013e-121">hello WITH clause specifies a temporary named result set that can be referenced by a FROM clause in hello query.</span></span> <span data-ttu-id="9013e-122">Você define a cláusula WITH de saudação em escopo de execução de saudação de uma única instrução SELECT.</span><span class="sxs-lookup"><span data-stu-id="9013e-122">You define hello WITH clause in hello execution scope of a single SELECT statement.</span></span>

<span data-ttu-id="9013e-123">Por exemplo, em vez desta consulta:</span><span class="sxs-lookup"><span data-stu-id="9013e-123">For example, instead of this query:</span></span>

```
SELECT foo 
INTO output1
FROM inputEventHub

SELECT bar
INTO output2
FROM inputEventHub 
…
```

<span data-ttu-id="9013e-124">Use esta consulta:</span><span class="sxs-lookup"><span data-stu-id="9013e-124">Use this query:</span></span>

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

### <a name="ensure-that-inputs-bind-toodifferent-consumer-groups"></a><span data-ttu-id="9013e-125">Certifique-se de que entradas vinculam grupos de consumidores toodifferent</span><span class="sxs-lookup"><span data-stu-id="9013e-125">Ensure that inputs bind toodifferent consumer groups</span></span>

<span data-ttu-id="9013e-126">Para consultas de três ou mais entradas são conectado toohello mesmo consumidor de Hubs de eventos de grupo, criar grupos de consumidores separado.</span><span class="sxs-lookup"><span data-stu-id="9013e-126">For queries in which three or more inputs are connected toohello same Event Hubs consumer group, create separate consumer groups.</span></span> <span data-ttu-id="9013e-127">Isso exige a criação de saudação de entradas adicionais de análise de fluxo.</span><span class="sxs-lookup"><span data-stu-id="9013e-127">This requires hello creation of additional Stream Analytics inputs.</span></span>


## <a name="get-help"></a><span data-ttu-id="9013e-128">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="9013e-128">Get help</span></span>
<span data-ttu-id="9013e-129">Para obter mais ajuda, teste nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span><span class="sxs-lookup"><span data-stu-id="9013e-129">For additional assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9013e-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9013e-130">Next steps</span></span>
* [<span data-ttu-id="9013e-131">Introdução tooStream análise</span><span class="sxs-lookup"><span data-stu-id="9013e-131">Introduction tooStream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="9013e-132">Introdução ao Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9013e-132">Get started with Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="9013e-133">Dimensionar trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9013e-133">Scale Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="9013e-134">Referência da linguagem de consulta do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9013e-134">Stream Analytics query language reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="9013e-135">Referência da API REST de gerenciamento do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="9013e-135">Stream Analytics management REST API reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
