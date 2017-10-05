---
title: Entradas de amostragem no Stream Analytics do Azure | Microsoft Docs
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
ms.openlocfilehash: 0bb66090b5025d57f5ca8f30713aef4e444fa8e7
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="azure-stream-analytics-input-stream-sampling"></a><span data-ttu-id="084bf-104">Amostragem do fluxo de entrada do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="084bf-104">Azure Stream Analytics input-stream sampling</span></span>

<span data-ttu-id="084bf-105">Usando o Stream Analytics do Azure, você pode criar uma amostra dos eventos de entrada que acompanham um arquivo e testar consultas no portal sem a necessidade de iniciar ou interromper um trabalho.</span><span class="sxs-lookup"><span data-stu-id="084bf-105">By using Azure Stream Analytics, you can sample input events that come from a file and test queries in the portal without needing to start or stop a job.</span></span>

## <a name="testing-your-query"></a><span data-ttu-id="084bf-106">Testando sua consulta</span><span class="sxs-lookup"><span data-stu-id="084bf-106">Testing your query</span></span>

<span data-ttu-id="084bf-107">No painel de detalhes de trabalho do Stream Analytics, abra a folha **Editor de Consultas** clicando no nome da consulta em **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="084bf-107">In the Stream Analytics job details pane, open the **Query editor** blade by clicking the query name under **Query**.</span></span> <span data-ttu-id="084bf-108">(No nosso cenário de exemplo, como ainda não foi criada nenhuma consulta, clique no espaço reservado **< >**.)</span><span class="sxs-lookup"><span data-stu-id="084bf-108">(In our example scenario, because no query has been created yet, click the **< >** placeholder.)</span></span>

![O editor de consultas do Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor.png)

<span data-ttu-id="084bf-110">A folha do editor avançado para criar sua consulta é exibida como era na versão anterior.</span><span class="sxs-lookup"><span data-stu-id="084bf-110">The rich editor blade for creating your query is displayed as it was in the previous release.</span></span> <span data-ttu-id="084bf-111">Agora a folha foi atualizada com um novo painel à esquerda que mostra as entradas e saídas que são usadas pela consulta e definidas para esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="084bf-111">Now the blade has been updated with a new left pane that shows the inputs and outputs that are used by the query and defined for this job.</span></span>

![As listas de entradas e saídas do editor de consultas do Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-highlight.png)

<span data-ttu-id="084bf-113">São mostradas também uma entrada adicional e uma saída, que não são definidas.</span><span class="sxs-lookup"><span data-stu-id="084bf-113">Also shown are an additional input and output, which are not defined.</span></span> <span data-ttu-id="084bf-114">Elas são provenientes do novo modelo de consulta com que você começa.</span><span class="sxs-lookup"><span data-stu-id="084bf-114">They come from the new query template that you start with.</span></span> <span data-ttu-id="084bf-115">Elas mudam, ou até mesmo desaparecem, conforme você edita a consulta.</span><span class="sxs-lookup"><span data-stu-id="084bf-115">They change, or even disappear altogether, as you edit the query.</span></span> <span data-ttu-id="084bf-116">Você pode ignorá-las com segurança por ora.</span><span class="sxs-lookup"><span data-stu-id="084bf-116">You can safely ignore them for now.</span></span>

<span data-ttu-id="084bf-117">Para testar com dados de entrada de exemplo, clique com o botão direito do mouse em qualquer uma de suas entradas e, em seguida, selecione **Carregar dados de exemplo do arquivo**.</span><span class="sxs-lookup"><span data-stu-id="084bf-117">To test with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

![O comando Carregar dados de exemplo do arquivo do editor de consultas do Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-upload.png)

<span data-ttu-id="084bf-119">Depois que o upload for concluído, clique em **Teste** para testar essa consulta em relação aos dados de exemplo que você forneceu.</span><span class="sxs-lookup"><span data-stu-id="084bf-119">After the upload is complete, click **Test** to test this query against the sample data you have just provided.</span></span>

![O botão Testar do editor de consultas do Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-test.png)

<span data-ttu-id="084bf-121">Se você deseja salvar a saída do teste para uso posterior, a saída da consulta é exibida no navegador com um link para os resultados do download.</span><span class="sxs-lookup"><span data-stu-id="084bf-121">If you want to save the test output for later use, the output of your query is displayed in the browser with a link to the download results.</span></span> <span data-ttu-id="084bf-122">Agora você pode modificar fácil e iterativamente sua consulta e testá-la repetidamente para ver como a saída muda.</span><span class="sxs-lookup"><span data-stu-id="084bf-122">You can now easily and iteratively modify your query and test it repeatedly to see how the output changes.</span></span>

![A saída do exemplo do editor de consultas do Stream Analytics](media/stream-analytics-sample-data-input/stream-analytics-query-editor-samples-output.png)

<span data-ttu-id="084bf-124">Na imagem anterior, uma segunda saída foi adicionada, chamada **HighAvgTempOutput**.</span><span class="sxs-lookup"><span data-stu-id="084bf-124">In the preceding image, a second output has been added, called **HighAvgTempOutput**.</span></span>

<span data-ttu-id="084bf-125">Ao usar várias saídas em uma consulta, você pode ver os resultados de cada saída separadamente e alterná-los facilmente.</span><span class="sxs-lookup"><span data-stu-id="084bf-125">When you use multiple outputs in a query, you can see the results for each output separately and easily toggle between them.</span></span>

<span data-ttu-id="084bf-126">Depois que estiver satisfeito com os resultados, você poderá salvar sua consulta, iniciar seu trabalho, sentar-se e assistir à mágica do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="084bf-126">After you are satisfied with the results, you can save your query, start your job, sit back and watch the magic of Stream Analytics.</span></span>

## <a name="get-help"></a><span data-ttu-id="084bf-127">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="084bf-127">Get help</span></span>

<span data-ttu-id="084bf-128">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="084bf-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="084bf-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="084bf-129">Next steps</span></span>
* [<span data-ttu-id="084bf-130">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="084bf-130">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="084bf-131">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="084bf-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="084bf-132">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="084bf-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="084bf-133">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="084bf-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="084bf-134">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="084bf-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
