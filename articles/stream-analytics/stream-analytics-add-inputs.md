---
title: "aaaAdd um dados tooyour trabalhos de análise de fluxo de entrada | Microsoft Docs"
description: "Saiba como toohook a uma fonte de dados tooyour análise de fluxo de trabalho como fluxo de entrada de dados de Hubs de eventos ou referência de dados de armazenamento de blob."
keywords: dados de entrada, streaming de dados
documentationcenter: 
services: stream-analytics
author: samacha
manager: jhubbard
editor: 
ms.assetid: 9e59bd24-2a80-4ecb-b6b2-309a07c70bcd
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: samacha
ms.openlocfilehash: 674000268fcdf9bc000af3e2f166cb66f1366922
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-tooa-stream-analytics-job"></a><span data-ttu-id="3c12c-104">Adicionar um fluxo dados de entrada ou referência dados tooa trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3c12c-104">Add a streaming data input or reference data tooa Stream Analytics job</span></span>
<span data-ttu-id="3c12c-105">Saiba como toohook a uma fonte de dados tooyour análise de fluxo de trabalho como fluxo de entrada de dados de Hubs de eventos ou referência de dados do armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="3c12c-105">Learn how toohook up a data source tooyour Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="3c12c-106">Trabalhos do Stream Analytics do Azure podem ser conectado tooone entrada de dados ou mais, cada um dos quais definir uma fonte de dados conexão tooan existente.</span><span class="sxs-lookup"><span data-stu-id="3c12c-106">Azure Stream Analytics jobs can be connected tooone data input or more, each of which define a connection tooan existing data source.</span></span> <span data-ttu-id="3c12c-107">Como os dados são enviados a fonte de dados toothat, é consumido pelo trabalho de análise de fluxo de saudação e processado em tempo real, como fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="3c12c-107">As data is sent toothat data source, it is consumed by hello Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="3c12c-108">Análise de fluxo tem integração de primeira classe com [Hubs de eventos do Azure](https://azure.microsoft.com/services/event-hubs/) e [armazenamento de BLOBs do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) dentro e fora de assinatura do trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="3c12c-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of hello job's subscription.</span></span>

<span data-ttu-id="3c12c-109">Este artigo é uma etapa Olá [caminho de aprendizagem do Stream Analytics](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="3c12c-109">This article is a step in hello [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="3c12c-110">Entrada de dados: dados de transmissão e dados de referência</span><span class="sxs-lookup"><span data-stu-id="3c12c-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="3c12c-111">Há dois tipos de entradas diferentes no Stream Analytics: fluxos de dados e dados de referência.</span><span class="sxs-lookup"><span data-stu-id="3c12c-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="3c12c-112">**Fluxos de dados**: trabalhos do Stream Analytics devem incluir pelo menos um dados fluxo entrada toobe consumidos e transformados por trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="3c12c-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input toobe consumed and transformed by hello job.</span></span> <span data-ttu-id="3c12c-113">O Armazenamento de Blob do Azure e os Hubs de Eventos do Azure têm suporte como fontes de entrada de fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="3c12c-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="3c12c-114">Hubs de eventos do Azure são fluxos de eventos usado toocollect dos dispositivos conectados, serviços e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="3c12c-114">Azure Event Hubs are used toocollect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="3c12c-115">O armazenamento Blob do Azure pode ser usado como uma fonte de entrada para ingerir dados em massa como um fluxo.</span><span class="sxs-lookup"><span data-stu-id="3c12c-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="3c12c-116">**Dados de referência**: o Stream Analytics oferece suporte a um segundo tipo de entrada auxiliar chamado de dados de referência.</span><span class="sxs-lookup"><span data-stu-id="3c12c-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="3c12c-117">Como toodata contrário em movimento, esses dados são estáticos ou lenta de alteração.</span><span class="sxs-lookup"><span data-stu-id="3c12c-117">As opposed toodata in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="3c12c-118">Ela é normalmente usada para realizar pesquisas e correlações com fluxos de dados toocreate um valioso conjunto de dados.</span><span class="sxs-lookup"><span data-stu-id="3c12c-118">It is typically used for performing look-ups and correlations with data streams toocreate a richer data set.</span></span>  <span data-ttu-id="3c12c-119">Armazenamento de BLOBs do Azure está atualmente a fonte de entrada hello só tem suportada para dados de referência.</span><span class="sxs-lookup"><span data-stu-id="3c12c-119">Azure Blob storage is currently hello only supported input source for reference data.</span></span>  

<span data-ttu-id="3c12c-120">tooadd um trabalho de análise de fluxo de entrada tooyour:</span><span class="sxs-lookup"><span data-stu-id="3c12c-120">tooadd an input tooyour Stream Analytics job:</span></span>

1. <span data-ttu-id="3c12c-121">No portal do Azure de saudação clique **entradas** e, em seguida, clique em **adicionar uma entrada** no trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3c12c-121">In hello Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Portal clássico do Azure - adicionar uma entrada.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="3c12c-123">No hello Azure portal clique Olá **entradas** lado a lado em seu trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="3c12c-123">In hello Azure portal click hello **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Portal do Azure - adicionar entrada de dados.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="3c12c-125">Especificar o tipo de saudação de entrada hello: qualquer **fluxo de dados** ou **dados de referência**.</span><span class="sxs-lookup"><span data-stu-id="3c12c-125">Specify hello type of hello input: either **Data stream** or **Reference data**.</span></span>
   
    ![Adicionar dados corretos Olá de entrada, streaming ou referência](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Adicionar dados corretos Olá de entrada, streaming ou referência](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="3c12c-128">Se criar uma entrada de fluxo de dados, especifique o tipo de fonte de Olá Olá entrada.</span><span class="sxs-lookup"><span data-stu-id="3c12c-128">If creating a Data Stream input, specify hello source type for hello input.</span></span>  <span data-ttu-id="3c12c-129">Essa etapa pode ser ignorada durante a criação dos Dados de Referência, pois atualmente há suporte apenas para o armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="3c12c-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Adicionar a entrada de dados do streaming de dados](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Adicionar a entrada de dados do streaming de dados](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="3c12c-132">Forneça um nome amigável para esta entrada no hello caixa Alias de entrada.</span><span class="sxs-lookup"><span data-stu-id="3c12c-132">Provide a friendly name for this input in hello Input Alias box.</span></span>  <span data-ttu-id="3c12c-133">Esse nome será usado na consulta do trabalho posteriormente na entrada de toohello toorefer.</span><span class="sxs-lookup"><span data-stu-id="3c12c-133">This name will be used in your job's query later on toorefer toohello input.</span></span>
   
    <span data-ttu-id="3c12c-134">Preencha o restante de Olá Olá necessária conexão propriedades tooconnect tooyour da fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="3c12c-134">Fill in hello rest of hello required connection properties tooconnect tooyour data source.</span></span> <span data-ttu-id="3c12c-135">Esses campos variam de acordo com o tipo de entrada e de fonte e são definidos detalhadamente [aqui](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="3c12c-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Adicionar entrada de dados do hub de eventos](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="3c12c-137">Especifique configurações de serialização Olá Olá para dados de entrada:</span><span class="sxs-lookup"><span data-stu-id="3c12c-137">Specify hello serialization settings for hello input data:</span></span>
   
   * <span data-ttu-id="3c12c-138">toomake que suas consultas funcionem de maneira Olá esperada, especifique Olá **formato de serialização de evento** de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="3c12c-138">toomake sure your queries work hello way you expect, specify hello **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="3c12c-139">Os formatos de serialização com suporte são JSON, CSV e Avro.</span><span class="sxs-lookup"><span data-stu-id="3c12c-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="3c12c-140">Verifique se Olá **codificação** para dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c12c-140">Verify hello **Encoding** for hello data.</span></span>  <span data-ttu-id="3c12c-141">UTF-8 é Olá somente suporte para formato de codificação no momento.</span><span class="sxs-lookup"><span data-stu-id="3c12c-141">UTF-8 is hello only supported encoding format at this time.</span></span>
     
     ![Configurações de serialização de dados para dados de entrada hello](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Configurações de serialização de dados para dados de entrada hello](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="3c12c-144">Depois de concluir a criação de entrada hello, análise de fluxo vai verificar que ele possa se conectar a fonte de entrada toohello.</span><span class="sxs-lookup"><span data-stu-id="3c12c-144">After completing hello input creation, Stream Analytics will verify that it can connect toohello input source.</span></span>  <span data-ttu-id="3c12c-145">Você pode exibir o status de saudação do hello operação de Conexão de teste no hub de notificação de saudação.</span><span class="sxs-lookup"><span data-stu-id="3c12c-145">You can view hello status of hello Test Connection operation in hello Notification hub.</span></span>
   
    ![Testar a conexão de saudação de fluxo de dados de entrada](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Testar a conexão de saudação de fluxo de dados de entrada](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="3c12c-148">Obter ajuda com a transmissão de entradas de dados</span><span class="sxs-lookup"><span data-stu-id="3c12c-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="3c12c-149">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="3c12c-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3c12c-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3c12c-150">Next steps</span></span>
* [<span data-ttu-id="3c12c-151">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3c12c-151">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3c12c-152">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="3c12c-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3c12c-153">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="3c12c-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3c12c-154">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="3c12c-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3c12c-155">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3c12c-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

