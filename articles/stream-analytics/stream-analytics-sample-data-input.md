---
title: entradas de amostragem AAA no Azure Stream Analytics | Microsoft Docs
description: Identificar problemas ao solucionar problemas em trabalhos do Stream Analytics.
keywords: "entrada de solução de problemas, amostragem de entrada"
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
ms.date: 04/20/2017
ms.author: jeffstok
ms.openlocfilehash: 9637a8664de099eebb8f5654036d2957f4c6b7ce
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="a6838-104">Amostragem do fluxo de entrada do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="a6838-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="a6838-105">Usando o Azure Stream Analytics, você pode criar amostra eventos de entrada que vêm de um arquivo e testar as consultas no portal de saudação sem a necessidade de toostart ou interromper um trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6838-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in hello portal without needing toostart or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="a6838-106">Testando sua consulta</span><span class="sxs-lookup"><span data-stu-id="a6838-106">Testing your query</span></span>

<span data-ttu-id="a6838-107">No painel de detalhes do trabalho do Stream Analytics hello, abra Olá **editor de consultas** folha clicando no nome de consulta de saudação em **consulta**.</span><span class="sxs-lookup"><span data-stu-id="a6838-107">In hello Stream Analytics job details pane, open hello **Query editor** blade by clicking hello query name under **Query**.</span></span> <span data-ttu-id="a6838-108">(Em nosso cenário de exemplo, porque nenhuma consulta tiver sido criada, clique em Olá **< >** espaço reservado.)</span><span class="sxs-lookup"><span data-stu-id="a6838-108">(In our example scenario, because no query has been created yet, click hello **< >** placeholder.)</span></span>

![editor de consultas de análise de fluxo de saudação](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="a6838-110">folha de editor avançado Olá para criar sua consulta é exibida como era na versão anterior do hello.</span><span class="sxs-lookup"><span data-stu-id="a6838-110">hello rich editor blade for creating your query is displayed as it was in hello previous release.</span></span> <span data-ttu-id="a6838-111">Agora folha Olá foi atualizada com um novo painel esquerdo que mostra Olá entradas e saídas que são usadas pela consulta hello e definidas para este trabalho.</span><span class="sxs-lookup"><span data-stu-id="a6838-111">Now hello blade has been updated with a new left pane that shows hello inputs and outputs that are used by hello query and defined for this job.</span></span>

![editor de consultas de análise de fluxo de saudação as entradas e saídas de listas](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="a6838-113">São mostradas também uma entrada adicional e uma saída, que não são definidas.</span><span class="sxs-lookup"><span data-stu-id="a6838-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="a6838-114">Eles vêm Olá novo modelo de consulta que começam com.</span><span class="sxs-lookup"><span data-stu-id="a6838-114">They come from hello new query template that you start with.</span></span> <span data-ttu-id="a6838-115">Alterar, ou até mesmo desaparecer completamente, como editar consulta hello.</span><span class="sxs-lookup"><span data-stu-id="a6838-115">They change, or even disappear altogether, as you edit hello query.</span></span> <span data-ttu-id="a6838-116">Você pode ignorá-las com segurança por ora.</span><span class="sxs-lookup"><span data-stu-id="a6838-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="a6838-117">tootest com dados de entrada de exemplo, qualquer uma das suas entradas e, em seguida, selecione **carregar dados de exemplo do arquivo**.</span><span class="sxs-lookup"><span data-stu-id="a6838-117">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![Olá dados de exemplo do carregamento do Stream Analytics consulta editor de comando de arquivo](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="a6838-119">Após a conclusão do carregamento de saudação, clique em **teste** tootest esta consulta em relação a saudação amostra dos dados que você forneceu.</span><span class="sxs-lookup"><span data-stu-id="a6838-119">After hello upload is complete, click **Test** tootest this query against hello sample data you have just provided.</span></span>

![botão de teste Olá Stream Analytics query editor](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="a6838-121">Se você quiser saída do teste Olá toosave para uso posterior, a saída de saudação da consulta é exibida no navegador de saudação com resultados do download de toohello um link.</span><span class="sxs-lookup"><span data-stu-id="a6838-121">If you want toosave hello test output for later use, hello output of your query is displayed in hello browser with a link toohello download results.</span></span> <span data-ttu-id="a6838-122">Você pode facilmente e iterativamente modificar sua consulta e testá-lo repetidamente toosee como saída de hello é alterado.</span><span class="sxs-lookup"><span data-stu-id="a6838-122">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![A saída do exemplo do editor de consultas do Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="a6838-124">Olá anterior a imagem, uma segunda saída foi adicionada, chamado **HighAvgTempOutput**.</span><span class="sxs-lookup"><span data-stu-id="a6838-124">In hello preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="a6838-125">Quando você usa várias saídas em uma consulta, você pode ver os resultados de saudação para cada saída separadamente e alternar facilmente entre eles.</span><span class="sxs-lookup"><span data-stu-id="a6838-125">When you use multiple outputs in a query, you can see hello results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="a6838-126">Depois que você estiver satisfeito com os resultados de Olá, você pode salvar sua consulta, iniciar o trabalho, sente-se e assista magic Olá da análise de fluxo de.</span><span class="sxs-lookup"><span data-stu-id="a6838-126">After you are satisfied with hello results, you can save your query, start your job, sit back and watch hello magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="a6838-127">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="a6838-127">Get help</span></span>

<span data-ttu-id="a6838-128">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="a6838-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6838-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6838-129">Next steps</span></span>
* [<span data-ttu-id="a6838-130">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a6838-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="a6838-131">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="a6838-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="a6838-132">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="a6838-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="a6838-133">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="a6838-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="a6838-134">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="a6838-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
