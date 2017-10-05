---
title: Depurar consultas do Stream Analytics do Azure usando SELECT INTO | Microsoft Docs
description: "Consulta intermediária com dados de exemplo usando instruções SELECT INTO no Stream Analytics"
keywords: 
services: stream-analytics
documentationcenter: 
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9952e2cf-b335-4a5c-8f45-8d3e1eda2e20
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: b05222c6d6f4fc2c5b847dd75ff7e29352cd538c
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="5152f-103">Depurar consultas usando instruções SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="5152f-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="5152f-104">No processamento de dados em tempo real, saber qual será a aparência dos dados no meio da consulta pode ser útil.</span><span class="sxs-lookup"><span data-stu-id="5152f-104">In real-time data processing, knowing what the data looks like in the middle of the query can be helpful.</span></span> <span data-ttu-id="5152f-105">Como as entradas ou etapas de um trabalho do Stream Analytics do Azure podem ser lidas várias vezes, você pode escrever instruções SELECT INTO extras.</span><span class="sxs-lookup"><span data-stu-id="5152f-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="5152f-106">Ao fazer isso, dados intermediários são gerados no armazenamento que permitem a você inspecionar a exatidão dos dados, assim como as *variáveis de inspeção* fazem quando você depura um programa.</span><span class="sxs-lookup"><span data-stu-id="5152f-106">Doing so outputs intermediate data into storage and lets you inspect the correctness of the data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-to-check-the-data-stream"></a><span data-ttu-id="5152f-107">Usar SELECT INTO para verificar o fluxo de dados</span><span class="sxs-lookup"><span data-stu-id="5152f-107">Use SELECT INTO to check the data stream</span></span>

<span data-ttu-id="5152f-108">O exemplo de consulta a seguir em um trabalho do Stream Analytics do Azure tem uma entrada de fluxo, duas entradas de dados de referência e uma saída para o Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="5152f-108">The following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output to Azure Table Storage.</span></span> <span data-ttu-id="5152f-109">A consulta une dados do hub de eventos e dois blobs de referência para obter informações de nome e categoria:</span><span class="sxs-lookup"><span data-stu-id="5152f-109">The query joins data from the event hub and two reference blobs to get the name and category information:</span></span>

![Exemplo de consulta SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="5152f-111">Observe que o trabalho está em execução, mas não há eventos sendo gerados na saída.</span><span class="sxs-lookup"><span data-stu-id="5152f-111">Note that the job is running, but no events are being produced in the output.</span></span> <span data-ttu-id="5152f-112">No bloco **Monitoramento**, mostrado aqui, você pode ver que a entrada está gerando dados, mas não dá para saber qual etapa de **JOIN** fez com que todos os eventos fossem removidos.</span><span class="sxs-lookup"><span data-stu-id="5152f-112">On the **Monitoring** tile, shown here, you can see that the input is producing data, but you don’t know which step of the **JOIN** caused all the events to be dropped.</span></span>

![O bloco Monitoramento](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="5152f-114">Nesse caso, é possível adicionar algumas instruções extras SELECT INTO para "registrar em log" os resultados intermediários de JOIN e os dados que são lidos da entrada.</span><span class="sxs-lookup"><span data-stu-id="5152f-114">In this situation, you can add a few extra SELECT INTO statements to “log” the intermediate JOIN results and the data that's read from the input.</span></span>

<span data-ttu-id="5152f-115">Neste exemplo, adicionamos duas novas "saídas temporárias".</span><span class="sxs-lookup"><span data-stu-id="5152f-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="5152f-116">Elas podem ser qualquer coletor desejado.</span><span class="sxs-lookup"><span data-stu-id="5152f-116">They can be any sink you like.</span></span> <span data-ttu-id="5152f-117">Aqui, usamos o Armazenamento do Azure como um exemplo:</span><span class="sxs-lookup"><span data-stu-id="5152f-117">Here we use Azure Storage as an example:</span></span>

![Adicionando instruções SELECT INTO extras](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="5152f-119">Assim, você pode reescrever a consulta desta forma:</span><span class="sxs-lookup"><span data-stu-id="5152f-119">You can then rewrite the query like this:</span></span>

![Consulta SELECT INTO reescrita](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="5152f-121">Agora, reinicie o trabalho e deixe ele ser executado por alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5152f-121">Now start the job again, and let it run for a few minutes.</span></span> <span data-ttu-id="5152f-122">Em seguida, consulte temp1 e temp2 com o Cloud Explorer do Visual Studio para gerar as seguintes tabelas:</span><span class="sxs-lookup"><span data-stu-id="5152f-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer to produce the following tables:</span></span>

<span data-ttu-id="5152f-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="5152f-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="5152f-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="5152f-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="5152f-125">Como você pode ver, temp1 e temp2 têm dados e a coluna de nome é preenchida corretamente em temp2.</span><span class="sxs-lookup"><span data-stu-id="5152f-125">As you can see, temp1 and temp2 both have data, and the name column is populated correctly in temp2.</span></span> <span data-ttu-id="5152f-126">No entanto, como ainda não há dados na saída, algo está errado:</span><span class="sxs-lookup"><span data-stu-id="5152f-126">However, because there is still no data in output, something is wrong:</span></span>

![SELECT INTO output1 table with no data](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="5152f-128">Pela amostragem de dados, você pode ter quase certeza de que o problema é com o segundo JOIN.</span><span class="sxs-lookup"><span data-stu-id="5152f-128">By sampling the data, you can be almost certain that the issue is with the second JOIN.</span></span> <span data-ttu-id="5152f-129">Você pode baixar os dados de referência do blob e dar uma olhada:</span><span class="sxs-lookup"><span data-stu-id="5152f-129">You can download the reference data from the blob and take a look:</span></span>

![SELECT INTO ref table](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="5152f-131">Como você pode ver, o formato do GUID nos dados de referência é diferente do formato da coluna [from] em temp2.</span><span class="sxs-lookup"><span data-stu-id="5152f-131">As you can see, the format of the GUID in this reference data is different from the format of the [from] column in temp2.</span></span> <span data-ttu-id="5152f-132">Por esse motivo, os dados não chegaram em output1 como esperado.</span><span class="sxs-lookup"><span data-stu-id="5152f-132">That’s why the data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="5152f-133">É possível corrigir o formato dos dados, carregá-los no blob de referência e tentar novamente:</span><span class="sxs-lookup"><span data-stu-id="5152f-133">You can fix the data format, upload it to reference blob, and try again:</span></span>

![SELECT INTO temp table](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="5152f-135">Dessa vez, os dados na saída são formatados e preenchidos conforme esperado.</span><span class="sxs-lookup"><span data-stu-id="5152f-135">This time, the data in the output is formatted and populated as expected.</span></span>

![SELECT INTO final table](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="5152f-137">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="5152f-137">Get help</span></span>

<span data-ttu-id="5152f-138">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="5152f-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5152f-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5152f-139">Next steps</span></span>

* [<span data-ttu-id="5152f-140">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5152f-140">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="5152f-141">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5152f-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5152f-142">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5152f-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5152f-143">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5152f-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5152f-144">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5152f-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

