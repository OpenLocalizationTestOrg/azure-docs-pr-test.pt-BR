---
title: consultas de toowrite aaaHow no Stream Analytics | Microsoft Docs
description: Escrever consultas no Stream Analytics e consultar dados | segmento do roteiro de aprendizagem.
keywords: como toowrite consultas, dados de consulta, escrever uma consulta, escrever consultas
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
ms.openlocfilehash: b943c34f10afd2b21789afbd341c471a5f168729
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toowrite-queries-in-stream-analytics"></a><span data-ttu-id="20149-104">Como as consultas toowrite no Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="20149-104">How toowrite queries in Stream Analytics</span></span>
<span data-ttu-id="20149-105">Escrever consultas para o fluxo de processamento da lógica no Azure Stream Analytics é implementado como uma "consulta permanente" está definida antes de um trabalho é iniciado e executado nos dados que ele atinge o trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="20149-105">Writing queries for stream processing logic in Azure Stream Analytics is implemented as a "standing query" that is defined before a job starts and executed on data as it reaches hello job.</span></span> <span data-ttu-id="20149-106">transformação de dados Olá é expresso em uma linguagem de consulta do tipo SQL, que é basicamente um subconjunto de T-SQL com alguns adicionadas extensões de linguagem como [janelas](https://msdn.microsoft.com/library/azure/dn835019.aspx) usado semântica temporal tooexpress.</span><span class="sxs-lookup"><span data-stu-id="20149-106">hello data transformation is expressed in a SQL-like query language, which is largely a subset of T-SQL with some added language extensions like [Windowing](https://msdn.microsoft.com/library/azure/dn835019.aspx) used tooexpress temporal semantics.</span></span>

## <a name="writing-queries"></a><span data-ttu-id="20149-107">Escrevendo consultas:</span><span class="sxs-lookup"><span data-stu-id="20149-107">Writing Queries:</span></span>
1. <span data-ttu-id="20149-108">No seu trabalho do Stream Analytics no portal de gerenciamento do Azure hello, clique em **consulta**.</span><span class="sxs-lookup"><span data-stu-id="20149-108">In your Stream Analytics Job in hello Azure Management portal, click **Query**.</span></span>
   
    ![Selecionar Consulta](./media/stream-analytics-write-queries/1-stream-analytics-write-queries.png)  
   
    <span data-ttu-id="20149-110">No Portal do Azure do hello, clique em **consulta**.</span><span class="sxs-lookup"><span data-stu-id="20149-110">In hello Azure Portal, click **Query**.</span></span>
   
    ![Selecionar Visualização da Consulta](./media/stream-analytics-write-queries/query-preview-portal.png)  
2. <span data-ttu-id="20149-112">Novos trabalhos tem uma toohelp de modelo de consulta começar.</span><span class="sxs-lookup"><span data-stu-id="20149-112">New jobs have a query template toohelp get you started.</span></span> <span data-ttu-id="20149-113">consulta Olá modelo executa "passagem" a consulta que projetos de todos os campos de eventos de entrada em saída hello.</span><span class="sxs-lookup"><span data-stu-id="20149-113">hello query template performs a "pass-through" query that projects all fields from input events into hello output.</span></span>  
   
   * <span data-ttu-id="20149-114">Se você tiver definido a pelo menos uma entrada e saída do seu trabalho, você pode substituir o espaço reservado de hello "[YourOutputAlias]" e "[YourInputAlias]" campos com aliases de saudação de saudação de entrada e saída que você deseja usar primeiro.</span><span class="sxs-lookup"><span data-stu-id="20149-114">If you have defined at least one input and output for your job, you can replace hello placeholder "[YourOutputAlias]" and "[YourInputAlias]" fields with hello aliases of hello input and output that you wish use first.</span></span> <span data-ttu-id="20149-115">Além disso, você ainda pode criar e teste sua consulta Olá Portal clássico do Azure sem definir entradas e saídas no trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="20149-115">In addition, you can still author and test your query in hello Azure Classic Portal without defining inputs and outputs on hello job.</span></span>
   * <span data-ttu-id="20149-116">Se você quiser tooperform mais processamento de passagem simple, você pode editar a definição de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="20149-116">If you wish tooperform more processing than a simple pass-through, you can edit hello query definition.</span></span> <span data-ttu-id="20149-117">tooget iniciar a criação de consultas, dar uma olhada em alguns padrões são capturados de consulta comum [aqui](stream-analytics-stream-analytics-query-patterns.md).</span><span class="sxs-lookup"><span data-stu-id="20149-117">tooget started with query authoring, take a look at some common query patterns are captured [here](stream-analytics-stream-analytics-query-patterns.md).</span></span>  
   
   ![Janela de Consulta de dados](./media/stream-analytics-write-queries/2-stream-analytics-write-queries.png)  

## <a name="toovalidate-query-data-is-working"></a><span data-ttu-id="20149-119">dados de consulta toovalidate está funcionando:</span><span class="sxs-lookup"><span data-stu-id="20149-119">toovalidate query data is working:</span></span>
<span data-ttu-id="20149-120">Você pode testar sua consulta se comporta como esperado executando-o no navegador de saudação em um ou mais arquivos locais JSON que contém dados de teste.</span><span class="sxs-lookup"><span data-stu-id="20149-120">You can test that your query behaves as expected by running it in hello browser over one or more local JSON files containing test data.</span></span> <span data-ttu-id="20149-121">Isso não iniciar o trabalho de saudação ou ter nenhuma implicação de cobrança.</span><span class="sxs-lookup"><span data-stu-id="20149-121">This will not start hello job or have any billing implications.</span></span>

> [!NOTE]
> <span data-ttu-id="20149-122">Teste de consulta no navegador não é suportada atualmente no hello Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="20149-122">Currently in-browser query testing is not supported in hello Azure Portal.</span></span>  
> 
> 

1. <span data-ttu-id="20149-123">Certifique-se de que não há nenhum erro na consulta de saudação (caso contrário, Olá teste botão será desabilitado) e, em seguida, clique o botão de teste de saudação.</span><span class="sxs-lookup"><span data-stu-id="20149-123">Make sure that there are no errors in hello query (otherwise hello Test button will be disabled) and then click hello Test button.</span></span>  
   
   ![Teste de Consultar de dados](./media/stream-analytics-write-queries/3-stream-analytics-write-queries.png)  
2. <span data-ttu-id="20149-125">Será solicitada toospecify arquivos para cada uma das entradas de saudação referenciadas na consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="20149-125">You will be prompted toospecify files for each of hello inputs referenced in hello query.</span></span> <span data-ttu-id="20149-126">Neste exemplo, a consulta de modelo Olá será deixada como-é, portanto, caixa de diálogo hello está solicitando uma entrada denominada "yourinputalias".</span><span class="sxs-lookup"><span data-stu-id="20149-126">In this example, hello template query is left as-is, so hello dialog is prompting for an input named "yourinputalias".</span></span>  
   
   ![Testar Consulta de dados](./media/stream-analytics-write-queries/4-stream-analytics-write-queries.png)  
3. <span data-ttu-id="20149-128">Procure arquivo de teste de tooa.</span><span class="sxs-lookup"><span data-stu-id="20149-128">Browse tooa test file.</span></span> <span data-ttu-id="20149-129">Vários arquivos de exemplo estão disponíveis em [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) e você também pode recuperar dados de exemplo de suas próprias entradas de fluxo de dados por meio de saudação função dados de exemplo na guia de entradas de saudação.</span><span class="sxs-lookup"><span data-stu-id="20149-129">Several sample files are available on [github](https://github.com/Azure/azure-stream-analytics/tree/master/Sample Data) and you can also retrieve sample data from your own data stream inputs via hello Sample Data function on hello inputs tab.</span></span>  
   
   ![Entrada de Consulta](./media/stream-analytics-write-queries/5-stream-analytics-write-queries.png)  
4. <span data-ttu-id="20149-131">Depois de fechar a caixa de diálogo de Olá, sua consulta será executada em dados de teste hello e você verá resultados Olá final Olá Olá consulta página.</span><span class="sxs-lookup"><span data-stu-id="20149-131">After closing hello dialog, your query will be run over hello test data and you will see hello results at hello bottom of hello Query page.</span></span>  
   
   ![Resumo da Consulta](./media/stream-analytics-write-queries/6-stream-analytics-write-queries.png)  

## <a name="get-help"></a><span data-ttu-id="20149-133">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="20149-133">Get help</span></span>
<span data-ttu-id="20149-134">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="20149-134">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="20149-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="20149-135">Next steps</span></span>
* [<span data-ttu-id="20149-136">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="20149-136">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="20149-137">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="20149-137">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="20149-138">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="20149-138">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="20149-139">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="20149-139">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="20149-140">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="20149-140">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

