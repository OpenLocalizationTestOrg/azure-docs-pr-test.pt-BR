---
title: "dados de tooconfigure aaaHow saídas para trabalhos do Stream Analytics | Microsoft Docs"
description: "Configurar saídas para trabalhos do Stream Analytics | segmento do roteiro de aprendizagem."
keywords: "dados de saída, movimentação de dados"
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: cgronlun
ms.assetid: 3bbea3da-bfce-4af1-a15e-d4b23874034f
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 04/26/2017
ms.author: samacha
ms.openlocfilehash: c5d89e9e9f9211d3e778580c071dd53d56aed9fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-tooconfigure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="5be30-104">Como os dados tooconfigure saídas para trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5be30-104">How tooconfigure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="5be30-105">Trabalhos do Stream Analytics do Azure podem ser conectado tooone ou mais saídas de dados, que definem um coletor de dados existente de conexão tooan.</span><span class="sxs-lookup"><span data-stu-id="5be30-105">Azure Stream Analytics jobs can be connected tooone or more data outputs, which define a connection tooan existing data sink.</span></span> <span data-ttu-id="5be30-106">Como o trabalho do Stream Analytics processa e transforma os dados de entrada, um fluxo de dados de eventos de saída é gravado saída tooyour do trabalho.</span><span class="sxs-lookup"><span data-stu-id="5be30-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written tooyour job's output.</span></span>

<span data-ttu-id="5be30-107">Saídas de fluxo de dados de análise podem ser painéis em tempo real usado toosource ou alertas, gatilho fluxos de trabalho de movimentação de dados ou simplesmente arquivar dados para processamento em lote posteriormente.</span><span class="sxs-lookup"><span data-stu-id="5be30-107">Stream Analytics data outputs can be used toosource real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="5be30-108">O Stream Analytics integra-se perfeitamente a vários serviços do Azure, que são documentados em detalhes aqui.</span><span class="sxs-lookup"><span data-stu-id="5be30-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="5be30-109">tooadd um trabalho de análise de fluxo de tooyour de saída:</span><span class="sxs-lookup"><span data-stu-id="5be30-109">tooadd an output tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="5be30-110">Em Olá [portal do Azure](https://portal.azure.com), abra seu trabalho e clique em **saídas** e, em seguida, clique em **adicionar** na folha de saídas de saudação que aparece.</span><span class="sxs-lookup"><span data-stu-id="5be30-110">In hello [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in hello Outputs blade that appears.</span></span>
   
    ![Adicionar saídas](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="5be30-112">Forneça um nome amigável para essa saída no hello **Alias de saída** caixa.</span><span class="sxs-lookup"><span data-stu-id="5be30-112">Provide a friendly name for this output in hello **Output Alias** box.</span></span> <span data-ttu-id="5be30-113">Esse nome pode ser usado na consulta do trabalho posteriormente na saída de toohello toorefer.</span><span class="sxs-lookup"><span data-stu-id="5be30-113">This name can be used in your job's query later on toorefer toohello output.</span></span>  
   
    <span data-ttu-id="5be30-114">Preencha o restante Olá Olá necessário conexão propriedades tooconnect tooyour saída.</span><span class="sxs-lookup"><span data-stu-id="5be30-114">Fill in hello rest of hello required connection properties tooconnect tooyour output.</span></span>  <span data-ttu-id="5be30-115">Esses campos variam de acordo com o tipo de saída e são definidos em detalhes aqui.</span><span class="sxs-lookup"><span data-stu-id="5be30-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Escolher o tipo de movimentação de dados](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="5be30-117">Dependendo do tipo de saída de hello, talvez seja necessário toospecify como dados de saudação são serializados ou formatados.</span><span class="sxs-lookup"><span data-stu-id="5be30-117">Depending on hello output type, you may need toospecify how hello data is serialized or formatted.</span></span> <span data-ttu-id="5be30-118">configurações de serialização específico Olá para cada tipo de saída são documentadas aqui.</span><span class="sxs-lookup"><span data-stu-id="5be30-118">hello specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="5be30-119">Preencha o restante de Olá Olá necessária conexão propriedades tooconnect tooyour da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="5be30-119">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="5be30-120">Esses campos variam de acordo com o tipo de entrada e origem e são definidos em detalhes em Olá [artigo criar trabalho](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="5be30-120">These fields vary by type of input and source type and are defined in detail in hello [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="5be30-121">Qualquer trabalho de toohello adicionado do elemento de saída, deve existir antes Olá trabalho é iniciado e eventos que fluem de início.</span><span class="sxs-lookup"><span data-stu-id="5be30-121">Any output element added toohello job, must exist before hello job is started and events start flowing.</span></span> <span data-ttu-id="5be30-122">Por exemplo, se você usar o armazenamento de Blob como uma saída, o trabalho de saudação não criará uma conta de armazenamento automaticamente.</span><span class="sxs-lookup"><span data-stu-id="5be30-122">For example, if you use Blob storage as an output, hello job will not create a storage account automatically.</span></span> <span data-ttu-id="5be30-123">Ele precisa toobe criado pelo usuário Olá antes Olá ASA trabalho é iniciado.</span><span class="sxs-lookup"><span data-stu-id="5be30-123">It needs toobe created by hello user before hello ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="5be30-124">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="5be30-124">Get help</span></span>
<span data-ttu-id="5be30-125">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="5be30-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="5be30-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5be30-126">Next steps</span></span>
* [<span data-ttu-id="5be30-127">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5be30-127">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="5be30-128">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5be30-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="5be30-129">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5be30-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="5be30-130">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="5be30-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="5be30-131">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="5be30-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

