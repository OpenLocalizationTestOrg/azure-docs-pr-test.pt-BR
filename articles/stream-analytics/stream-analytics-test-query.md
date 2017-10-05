---
title: Testes de consulta do Stream Analytics do Azure | Microsoft Docs
description: Como testar as consultas em trabalhos do Stream Analytics.
keywords: testar consulta, solucionar problemas da consulta
documentation center: 
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
ms.openlocfilehash: 16bb3f26ec3a69e5204162db9e54a186cf1ec6a6
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="test-azure-stream-analytics-queries-in-the-azure-portal"></a><span data-ttu-id="09691-104">Testar as consultas do Stream Analytics do Azure no portal do Azure</span><span class="sxs-lookup"><span data-stu-id="09691-104">Test Azure Stream Analytics queries in the Azure portal</span></span>

<span data-ttu-id="09691-105">Com o Stream Analytics do Azure, você pode testar consultas no portal do Azure sem a necessidade de iniciar ou interromper um trabalho.</span><span class="sxs-lookup"><span data-stu-id="09691-105">With Azure Stream Analytics, you can test queries in the Azure portal without needing to start or stop a job.</span></span>

## <a name="test-the-input"></a><span data-ttu-id="09691-106">Testar a entrada</span><span class="sxs-lookup"><span data-stu-id="09691-106">Test the input</span></span>

1. <span data-ttu-id="09691-107">Para testar com dados de entrada de exemplo, clique com o botão direito do mouse em qualquer uma de suas entradas e, em seguida, selecione **Carregar dados de exemplo do arquivo**.</span><span class="sxs-lookup"><span data-stu-id="09691-107">To test with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![consulta de teste do editor de consultas do stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="09691-109">Depois que o upload for concluído, clique em **Teste** para testar essa consulta em relação aos dados de exemplo que você forneceu.</span><span class="sxs-lookup"><span data-stu-id="09691-109">After the upload is complete, click **Test** to test this query against the sample data you have provided.</span></span>

    ![dados de exemplo de teste do editor de consultas do stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="09691-111">A saída da consulta é exibida no navegador com um link Baixar resultados, caso você queira salvar a saída do teste para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="09691-111">The output of your query is displayed in the browser, with Download results link should you want to save the test output for later use.</span></span> <span data-ttu-id="09691-112">Agora você pode modificar fácil e iterativamente sua consulta e testá-la repetidamente para ver como a saída muda.</span><span class="sxs-lookup"><span data-stu-id="09691-112">You can now easily and iteratively modify your query and test it repeatedly to see how the output changes.</span></span>

![A saída do exemplo do editor de consultas do Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="09691-114">Com várias saídas usadas em uma consulta, você pode ver os resultados de ambas as saídas separadamente e alterná-los facilmente.</span><span class="sxs-lookup"><span data-stu-id="09691-114">With multiple outputs used in a query, you can see the results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="09691-115">Quando estiver satisfeito com os resultados mostrados no navegador, você poderá salvar sua consulta, iniciar seu trabalho e deixá-lo processar os eventos sem erro.</span><span class="sxs-lookup"><span data-stu-id="09691-115">After you are satisfied with the results shown in the browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="09691-116">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="09691-116">Get help</span></span>

<span data-ttu-id="09691-117">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="09691-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="09691-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="09691-118">Next steps</span></span>

* [<span data-ttu-id="09691-119">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="09691-119">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="09691-120">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="09691-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="09691-121">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="09691-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="09691-122">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="09691-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="09691-123">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="09691-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
