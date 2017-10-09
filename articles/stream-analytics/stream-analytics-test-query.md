---
title: "testes de consulta de análise de fluxo de aaaAzure | Microsoft Docs"
description: Como tootest suas consultas em trabalhos do Stream Analytics.
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
ms.openlocfilehash: 3b141d98332fdc170e696e181c8446796a86f78e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="test-azure-stream-analytics-queries-in-hello-azure-portal"></a><span data-ttu-id="975cf-104">Testar as consultas de análise de fluxo do Azure em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="975cf-104">Test Azure Stream Analytics queries in hello Azure portal</span></span>

<span data-ttu-id="975cf-105">Com o Azure Stream Analytics, você pode testar as consultas em Olá portal do Azure sem a necessidade de toostart ou interromper um trabalho.</span><span class="sxs-lookup"><span data-stu-id="975cf-105">With Azure Stream Analytics, you can test queries in hello Azure portal without needing toostart or stop a job.</span></span>

## <a name="test-hello-input"></a><span data-ttu-id="975cf-106">Entrada de saudação do teste</span><span class="sxs-lookup"><span data-stu-id="975cf-106">Test hello input</span></span>

1. <span data-ttu-id="975cf-107">tootest com dados de entrada de exemplo, qualquer uma das suas entradas e, em seguida, selecione **carregar dados de exemplo do arquivo**.</span><span class="sxs-lookup"><span data-stu-id="975cf-107">tootest with sample input data, right-click any of your inputs, and then select **Upload sample data from file**.</span></span>

    ![consulta de teste do editor de consultas do stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-upload.png)

2. <span data-ttu-id="975cf-109">Após a conclusão do carregamento de saudação, clique em **teste** tootest esta consulta em relação a saudação amostra dos dados que você forneceu.</span><span class="sxs-lookup"><span data-stu-id="975cf-109">After hello upload is complete, click **Test** tootest this query against hello sample data you have provided.</span></span>

    ![dados de exemplo de teste do editor de consultas do stream analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-test.png)

<span data-ttu-id="975cf-111">saída de Hello da consulta é exibida no navegador hello, com um link para Download resultados você deseja saída do teste Olá toosave para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="975cf-111">hello output of your query is displayed in hello browser, with Download results link should you want toosave hello test output for later use.</span></span> <span data-ttu-id="975cf-112">Você pode facilmente e iterativamente modificar sua consulta e testá-lo repetidamente toosee como saída de hello é alterado.</span><span class="sxs-lookup"><span data-stu-id="975cf-112">You can now easily and iteratively modify your query and test it repeatedly toosee how hello output changes.</span></span>

![A saída do exemplo do editor de consultas do Stream Analytics](media/stream-analytics-test-query/stream-analytics-test-query-editor-samples-output.png)

<span data-ttu-id="975cf-114">Com várias saídas usadas em uma consulta, você pode ver os resultados de saudação para ambas as saídas separadamente e alternar facilmente entre eles.</span><span class="sxs-lookup"><span data-stu-id="975cf-114">With multiple outputs used in a query, you can see hello results for both outputs separately and easily toggle between them.</span></span>

<span data-ttu-id="975cf-115">Quando estiver satisfeito com os resultados de Olá mostrados no navegador hello, salvar sua consulta, iniciar o trabalho e permitem que ele processa os eventos sem erro.</span><span class="sxs-lookup"><span data-stu-id="975cf-115">After you are satisfied with hello results shown in hello browser, you can save your query, start your job, and let it process events without error.</span></span>

## <a name="get-help"></a><span data-ttu-id="975cf-116">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="975cf-116">Get help</span></span>

<span data-ttu-id="975cf-117">Para obter mais assistência, experimente nosso [fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="975cf-117">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics).</span></span>

## <a name="next-steps"></a><span data-ttu-id="975cf-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="975cf-118">Next steps</span></span>

* [<span data-ttu-id="975cf-119">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="975cf-119">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="975cf-120">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="975cf-120">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="975cf-121">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="975cf-121">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="975cf-122">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="975cf-122">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="975cf-123">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="975cf-123">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)
