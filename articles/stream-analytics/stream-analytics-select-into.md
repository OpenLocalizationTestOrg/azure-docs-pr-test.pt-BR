---
title: consultas aaaDebug Stream Analytics do Azure usando SELECT INTO | Microsoft Docs
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
ms.openlocfilehash: 27e41af1a6ea06b4509d07a3a67087490d0ec1fd
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="debug-queries-by-using-select-into-statements"></a><span data-ttu-id="75606-103">Depurar consultas usando instruções SELECT INTO</span><span class="sxs-lookup"><span data-stu-id="75606-103">Debug queries by using SELECT INTO statements</span></span>

<span data-ttu-id="75606-104">No processamento de dados em tempo real, saber quais dados Olá parece no meio de saudação do hello consulta pode ser úteis.</span><span class="sxs-lookup"><span data-stu-id="75606-104">In real-time data processing, knowing what hello data looks like in hello middle of hello query can be helpful.</span></span> <span data-ttu-id="75606-105">Como as entradas ou etapas de um trabalho do Stream Analytics do Azure podem ser lidas várias vezes, você pode escrever instruções SELECT INTO extras.</span><span class="sxs-lookup"><span data-stu-id="75606-105">Because inputs or steps of an Azure Stream Analytics job can be read multiple times, you can write extra SELECT INTO statements.</span></span> <span data-ttu-id="75606-106">Isso gera dados intermediários para armazenamento e permite que você inspecione a exatidão de saudação do dados hello, assim como *Assista variáveis* quando você depura um programa.</span><span class="sxs-lookup"><span data-stu-id="75606-106">Doing so outputs intermediate data into storage and lets you inspect hello correctness of hello data, just as *watch variables* do when you debug a program.</span></span>

## <a name="use-select-into-toocheck-hello-data-stream"></a><span data-ttu-id="75606-107">Use SELECT INTO toocheck Olá fluxo de dados</span><span class="sxs-lookup"><span data-stu-id="75606-107">Use SELECT INTO toocheck hello data stream</span></span>

<span data-ttu-id="75606-108">Olá seguinte exemplo de consulta em um trabalho do Stream Analytics do Azure tem um fluxo de entrada, duas entradas de dados de referência e uma saída tooAzure armazenamento de tabela.</span><span class="sxs-lookup"><span data-stu-id="75606-108">hello following example query in an Azure Stream Analytics job has one stream input, two reference data inputs, and an output tooAzure Table Storage.</span></span> <span data-ttu-id="75606-109">consulta de saudação associa dados de hub de eventos hello e dois blobs tooget Olá nome e categoria de informações de referência:</span><span class="sxs-lookup"><span data-stu-id="75606-109">hello query joins data from hello event hub and two reference blobs tooget hello name and category information:</span></span>

![Exemplo de consulta SELECT INTO](./media/stream-analytics-select-into/stream-analytics-select-into-query1.png)

<span data-ttu-id="75606-111">Observe que Olá trabalho está em execução, mas nenhum evento sendo produzido na saída de hello.</span><span class="sxs-lookup"><span data-stu-id="75606-111">Note that hello job is running, but no events are being produced in hello output.</span></span> <span data-ttu-id="75606-112">Em Olá **monitoramento** lado a lado, mostrada aqui, você pode ver que a entrada hello está produzindo dados, mas você não souber qual etapa da saudação **INGRESSAR** causado todos Olá toobe eventos descartado.</span><span class="sxs-lookup"><span data-stu-id="75606-112">On hello **Monitoring** tile, shown here, you can see that hello input is producing data, but you don’t know which step of hello **JOIN** caused all hello events toobe dropped.</span></span>

![bloco de monitoramento de saudação](./media/stream-analytics-select-into/stream-analytics-select-into-monitor.png)
 
<span data-ttu-id="75606-114">Nessa situação, você pode adicionar alguns extras instruções SELECT INTO muito "" resultados intermediários de junção hello e dados de saudação que será lido da entrada hello.</span><span class="sxs-lookup"><span data-stu-id="75606-114">In this situation, you can add a few extra SELECT INTO statements too“log” hello intermediate JOIN results and hello data that's read from hello input.</span></span>

<span data-ttu-id="75606-115">Neste exemplo, adicionamos duas novas "saídas temporárias".</span><span class="sxs-lookup"><span data-stu-id="75606-115">In this example, we've added two new “temporary outputs.”</span></span> <span data-ttu-id="75606-116">Elas podem ser qualquer coletor desejado.</span><span class="sxs-lookup"><span data-stu-id="75606-116">They can be any sink you like.</span></span> <span data-ttu-id="75606-117">Aqui, usamos o Armazenamento do Azure como um exemplo:</span><span class="sxs-lookup"><span data-stu-id="75606-117">Here we use Azure Storage as an example:</span></span>

![Adicionando instruções SELECT INTO extras](./media/stream-analytics-select-into/stream-analytics-select-into-outputs.png)

<span data-ttu-id="75606-119">Em seguida, você pode reescrever consulta hello como esta:</span><span class="sxs-lookup"><span data-stu-id="75606-119">You can then rewrite hello query like this:</span></span>

![Consulta SELECT INTO reescrita](./media/stream-analytics-select-into/stream-analytics-select-into-query2.png)

<span data-ttu-id="75606-121">Agora, iniciar o trabalho de saudação e permitir sua execução por alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="75606-121">Now start hello job again, and let it run for a few minutes.</span></span> <span data-ttu-id="75606-122">Em seguida, consulta temp1 e temp2 com saudação do Visual Studio Cloud Explorer tooproduce tabelas a seguir:</span><span class="sxs-lookup"><span data-stu-id="75606-122">Then query temp1 and temp2 with Visual Studio Cloud Explorer tooproduce hello following tables:</span></span>

<span data-ttu-id="75606-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span><span class="sxs-lookup"><span data-stu-id="75606-123">**temp1 table**
![SELECT INTO temp1 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-1.png)</span></span>

<span data-ttu-id="75606-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span><span class="sxs-lookup"><span data-stu-id="75606-124">**temp2 table**
![SELECT INTO temp2 table](./media/stream-analytics-select-into/stream-analytics-select-into-temp-table-2.png)</span></span>

<span data-ttu-id="75606-125">Como você pode ver, temp1 e temp2 tem dados e coluna de nome de saudação é populada corretamente em temp2.</span><span class="sxs-lookup"><span data-stu-id="75606-125">As you can see, temp1 and temp2 both have data, and hello name column is populated correctly in temp2.</span></span> <span data-ttu-id="75606-126">No entanto, como ainda não há dados na saída, algo está errado:</span><span class="sxs-lookup"><span data-stu-id="75606-126">However, because there is still no data in output, something is wrong:</span></span>

![SELECT INTO output1 table with no data](./media/stream-analytics-select-into/stream-analytics-select-into-out-table-1.png)

<span data-ttu-id="75606-128">Por Olá dados de amostra, você pode ser quase certo de que o problema de saudação é com hello segundo junção.</span><span class="sxs-lookup"><span data-stu-id="75606-128">By sampling hello data, you can be almost certain that hello issue is with hello second JOIN.</span></span> <span data-ttu-id="75606-129">Você pode baixar dados de referência de saudação do blob hello e dar uma olhada:</span><span class="sxs-lookup"><span data-stu-id="75606-129">You can download hello reference data from hello blob and take a look:</span></span>

![SELECT INTO ref table](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-1.png)

<span data-ttu-id="75606-131">Como você pode ver, o formato de saudação do hello GUID nesses dados de referência é diferente do formato de saudação do hello [] na coluna temp2.</span><span class="sxs-lookup"><span data-stu-id="75606-131">As you can see, hello format of hello GUID in this reference data is different from hello format of hello [from] column in temp2.</span></span> <span data-ttu-id="75606-132">É por isso que dados saudação não chegarem na output1 conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="75606-132">That’s why hello data didn’t arrive in output1 as expected.</span></span>

<span data-ttu-id="75606-133">Você pode corrigir o formato de dados hello, carregá-lo tooreference blob e tente novamente:</span><span class="sxs-lookup"><span data-stu-id="75606-133">You can fix hello data format, upload it tooreference blob, and try again:</span></span>

![SELECT INTO temp table](./media/stream-analytics-select-into/stream-analytics-select-into-ref-table-2.png)

<span data-ttu-id="75606-135">Neste momento, dados de saudação na saída de hello são formatados e preenchidos conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="75606-135">This time, hello data in hello output is formatted and populated as expected.</span></span>

![SELECT INTO final table](./media/stream-analytics-select-into/stream-analytics-select-into-final-table.png)


## <a name="get-help"></a><span data-ttu-id="75606-137">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="75606-137">Get help</span></span>

<span data-ttu-id="75606-138">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="75606-138">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="75606-139">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="75606-139">Next steps</span></span>

* [<span data-ttu-id="75606-140">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="75606-140">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="75606-141">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="75606-141">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="75606-142">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="75606-142">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="75606-143">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="75606-143">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="75606-144">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="75606-144">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

