---
title: Como escrever consultas em Stream Analytics| Microsoft Docs
description: Escrever consultas no Stream Analytics e consultar dados | segmento do roteiro de aprendizagem.
keywords: como escrever consultas, dados de consulta, escrever uma consulta, escrever consultas
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0e9cdadd-0ee0-4bee-b65b-4a06fb863c95
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: b44b0658a06761a805708e7fdeba9e3b2cf9d3ab
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-write-queries-in-stream-analytics"></a><span data-ttu-id="10d19-104">Como escrever consultas em Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10d19-104">How to write queries in Stream Analytics</span></span>
<span data-ttu-id="10d19-105">Escrevendo consulta para lógica de processamento de fluxo no Stream Analytics do Azure é implementada como uma "consulta permanente" que é definida antes de um trabalho ser iniciado e executado em dados assim que ela atinge o trabalho.</span><span class="sxs-lookup"><span data-stu-id="10d19-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches the job.</span></span> <span data-ttu-id="10d19-106">A transformação de dados é expressa em uma linguagem de consulta do tipo SQL, que é basicamente um subconjunto de T-SQL com algumas extensões de linguagem adicionadas como [Janelas](https://msdn.microsoft.com/library/azure/dn835019.aspx) usadas para expressar semânticas temporais.</span><span class="sxs-lookup"><span data-stu-id="10d19-106">The data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used to express temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="10d19-107">Escrevendo consultas:</span><span class="sxs-lookup"><span data-stu-id="10d19-107">Writing Queries:</span></span>
1. <span data-ttu-id="10d19-108">Em seu trabalho do Stream Analytics no portal de Gerenciamento do Azure, clique em **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="10d19-108">In your Stream Analytics Job in the Azure Management portal, click **Query**.</span></span>
   
    ![Selecionar Consulta](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="10d19-110">No portal do Azure, clique em **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="10d19-110">In the Azure Portal, click **Query**.</span></span>
   
    ![Selecionar Visualização da Consulta](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="10d19-112">Os novos trabalhos têm um modelo de consulta que ajuda você a começar.</span><span class="sxs-lookup"><span data-stu-id="10d19-112">New jobs have a query template to help get you started.</span></span> <span data-ttu-id="10d19-113">O modelo de consulta executa uma consulta de "passagem" que projeta todos os campos dos eventos de entrada na saída.</span><span class="sxs-lookup"><span data-stu-id="10d19-113">The query template performs a "pass-through" query that projects all fields from input events into the output.</span></span>  
   
   * <span data-ttu-id="10d19-114">Se tiver definido pelo menos uma entrada e saída para seu trabalho, você poderá substituir os campos de espaço reservado "[YourOutputAlias]" e "[YourInputAlias]" pelos aliases da entrada e saída que deseja usar primeiro.</span><span class="sxs-lookup"><span data-stu-id="10d19-114">If you have defined at least one input and output for your job, you can replace the placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with the aliases of the input and output that you wish use first.</span></span> <span data-ttu-id="10d19-115">Além disso, você ainda pode criar e testar sua consulta no portal clássico do Azure sem definir entradas e saídas no trabalho.</span><span class="sxs-lookup"><span data-stu-id="10d19-115">In addition, you can still author and test your query in the Azure Classic Portal without defining inputs and outputs on the job.</span></span>
   * <span data-ttu-id="10d19-116">Se quiser executar mais processamento do que uma simples passagem, você pode editar a definição da consulta.</span><span class="sxs-lookup"><span data-stu-id="10d19-116">If you wish to perform more processing than a simple pass-through, you can edit the query definition.</span></span> <span data-ttu-id="10d19-117">Para começar a criar uma consulta, veja alguns padrões comuns de consulta capturados [aqui](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="10d19-117">To get started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Janela de Consulta de dados](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="to-validate-query-data-is-working"></a><span data-ttu-id="10d19-119">Para validar que os dados da consulta estão funcionando:</span><span class="sxs-lookup"><span data-stu-id="10d19-119">To validate query data is working:</span></span>
<span data-ttu-id="10d19-120">Você pode testar se sua consulta se comporta conforme esperado executando-a no navegador em um ou mais arquivos JSON locais contendo dados de teste.</span><span class="sxs-lookup"><span data-stu-id="10d19-120">You can test that your query behaves as expected by running it in the browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="10d19-121">Isso não iniciará o trabalho nem terá nenhuma implicação de faturamento.</span><span class="sxs-lookup"><span data-stu-id="10d19-121">This will not start the job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="10d19-122">Atualmente, não há suporte para o teste de consulta no navegador no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="10d19-122">Currently in-browser query testing is not supported in the Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="10d19-123">Verifique se não há erros na consulta (caso contrário, o botão Testar será desabilitado) e clique no botão Testar.</span><span class="sxs-lookup"><span data-stu-id="10d19-123">Make sure that there are no errors in the query (otherwise the Test button will be disabled) and then click the Test button.</span></span>  
   
   ![Teste de Consultar de dados](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="10d19-125">Será solicitado que você especifique arquivos para cada uma das entradas referenciadas na consulta.</span><span class="sxs-lookup"><span data-stu-id="10d19-125">You will be prompted to specify files for each of the inputs referenced in the query.</span></span> <span data-ttu-id="10d19-126">Neste exemplo, a consulta do modelo é deixada como está, de modo que a caixa de diálogo está solicitando uma entrada denominada "yourinputalias".</span><span class="sxs-lookup"><span data-stu-id="10d19-126">In this example, the template query is left as-is, so the dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![Testar Consulta de dados](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="10d19-128">Procure um arquivo de teste.</span><span class="sxs-lookup"><span data-stu-id="10d19-128">Browse to a test file.</span></span> <span data-ttu-id="10d19-129">Vários exemplos de arquivos estão disponíveis no [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) e você também pode recuperar exemplos de dados de suas próprias entradas de transmissão de dados por meio da função Dados de Exemplo na guia de entradas.</span><span class="sxs-lookup"><span data-stu-id="10d19-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via the Sample Data function on the inputs tab.</span></span>  
   
   ![Entrada de Consulta](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="10d19-131">Depois de fechar a caixa de diálogo, sua consulta será executada sobre os dados de teste e você verá os resultados na parte inferior da página Consulta.</span><span class="sxs-lookup"><span data-stu-id="10d19-131">After closing the dialog, your query will be run over the test data and you will see the results at the bottom of the Query page.</span></span>  
   
   ![Resumo da Consulta](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="10d19-133">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="10d19-133">Get help</span></span>
<span data-ttu-id="10d19-134">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="10d19-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="10d19-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="10d19-135">Next steps</span></span>
* [<span data-ttu-id="10d19-136">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="10d19-136">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="10d19-137">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="10d19-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="10d19-138">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="10d19-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="10d19-139">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="10d19-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="10d19-140">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="10d19-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

