---
title: Adicionar uma entrada de dados aos seus trabalhos do Stream Analytics | Microsoft Docs
description: "Saiba como conectar uma fonte de dados ao trabalho do Stream Analytics como fluxo de entrada de dados de Hubs de Eventos ou dados de referência armazenamento de Blob."
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
ms.openlocfilehash: 8bdbcf78f2892cbd1e1cc09cef220dff08dd9490
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="add-a-streaming-data-input-or-reference-data-to-a-stream-analytics-job"></a><span data-ttu-id="edbc6-104">Adicionar um fluxo de entrada ou dados de referência a um trabalho do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="edbc6-104">Add a streaming data input or reference data to a Stream Analytics job</span></span>
<span data-ttu-id="edbc6-105">Saiba como conectar uma fonte de dados ao trabalho do Stream Analytics como fluxo de entrada de dados de Hubs de Eventos ou dados de referência do armazenamento de Blobs.</span><span class="sxs-lookup"><span data-stu-id="edbc6-105">Learn how to hook up a data source to your Stream Analytics job as streaming data input from Event Hubs or reference data from Blob storage.</span></span>

<span data-ttu-id="edbc6-106">Os trabalhos do Stream Analytics do Azure podem ser conectados a uma ou mais entradas de dados, o que define uma conexão com uma fonte de dados existente.</span><span class="sxs-lookup"><span data-stu-id="edbc6-106">Azure Stream Analytics jobs can be connected to one data input or more, each of which define a connection to an existing data source.</span></span> <span data-ttu-id="edbc6-107">Como os dados são enviados a essa fonte de dados, eles são consumidos pelo trabalho do Stream Analytics e processados em tempo real como dados de streaming.</span><span class="sxs-lookup"><span data-stu-id="edbc6-107">As data is sent to that data source, it is consumed by the Stream Analytics job and processed in real time as streaming data.</span></span> <span data-ttu-id="edbc6-108">O Stream Analytics tem integração de primeira classe com [Hubs de eventos do Azure](https://azure.microsoft.com/services/event-hubs/) e [Armazenamento de Blobs do Azure](../storage/blobs/storage-dotnet-how-to-use-blobs.md) dentro e fora da assinatura do trabalho.</span><span class="sxs-lookup"><span data-stu-id="edbc6-108">Stream Analytics has first class integration with [Azure Event Hubs](https://azure.microsoft.com/services/event-hubs/) and [Azure Blob storage](../storage/blobs/storage-dotnet-how-to-use-blobs.md) both within and outside of the job's subscription.</span></span>

<span data-ttu-id="edbc6-109">Este artigo é uma etapa do [roteiro de aprendizagem do Stream Analytics](/documentation/learning-paths/stream-analytics/).</span><span class="sxs-lookup"><span data-stu-id="edbc6-109">This article is a step in the [Stream Analytics learning path](/documentation/learning-paths/stream-analytics/).</span></span>

## <a name="data-input-streaming-data-and-reference-data"></a><span data-ttu-id="edbc6-110">Entrada de dados: dados de transmissão e dados de referência</span><span class="sxs-lookup"><span data-stu-id="edbc6-110">Data input: Streaming data and reference data</span></span>
<span data-ttu-id="edbc6-111">Há dois tipos de entradas diferentes no Stream Analytics: fluxos de dados e dados de referência.</span><span class="sxs-lookup"><span data-stu-id="edbc6-111">There are two distinct types of inputs in Stream Analytics: data streams and reference data.</span></span>

* <span data-ttu-id="edbc6-112">**Fluxos de dados**: os trabalhos do Stream Analytics devem incluir pelo menos uma entrada de fluxo de dados para ser consumida e transformada pelo trabalho.</span><span class="sxs-lookup"><span data-stu-id="edbc6-112">**Data Streams**: Stream Analytics jobs must include at least one data stream input to be consumed and transformed by the job.</span></span> <span data-ttu-id="edbc6-113">O Armazenamento de Blob do Azure e os Hubs de Eventos do Azure têm suporte como fontes de entrada de fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="edbc6-113">Azure Blob storage and Azure Event Hubs are supported as data stream input sources.</span></span> <span data-ttu-id="edbc6-114">Os Hubs de Eventos do Azure são usados para coletar fluxos de eventos de dispositivos conectados, serviços e aplicativos.</span><span class="sxs-lookup"><span data-stu-id="edbc6-114">Azure Event Hubs are used to collect event streams from connected devices, services and applications.</span></span> <span data-ttu-id="edbc6-115">O armazenamento Blob do Azure pode ser usado como uma fonte de entrada para ingerir dados em massa como um fluxo.</span><span class="sxs-lookup"><span data-stu-id="edbc6-115">Azure Blob storage can be used as an input source for ingesting bulk data as a stream.</span></span>  
* <span data-ttu-id="edbc6-116">**Dados de referência**: o Stream Analytics oferece suporte a um segundo tipo de entrada auxiliar chamado de dados de referência.</span><span class="sxs-lookup"><span data-stu-id="edbc6-116">**Reference data**: Stream Analytics supports a second type of auxiliary input called reference data.</span></span>  <span data-ttu-id="edbc6-117">Ao contrário dos dados em movimento, esses dados são estáticos ou se modificam lentamente.</span><span class="sxs-lookup"><span data-stu-id="edbc6-117">As opposed to data in motion, this data is static or slowing changing.</span></span>  <span data-ttu-id="edbc6-118">Geralmente, são usados para executar pesquisas e correlações com fluxos de dados a fim de criar um conjunto de dados mais rico.</span><span class="sxs-lookup"><span data-stu-id="edbc6-118">It is typically used for performing look-ups and correlations with data streams to create a richer data set.</span></span>  <span data-ttu-id="edbc6-119">O Armazenamento de Blob do Azure é a única fonte de entrada com suporte para dados de referência.</span><span class="sxs-lookup"><span data-stu-id="edbc6-119">Azure Blob storage is currently the only supported input source for reference data.</span></span>  

<span data-ttu-id="edbc6-120">Para adicionar uma entrada ao trabalho do Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="edbc6-120">To add an input to your Stream Analytics job:</span></span>

1. <span data-ttu-id="edbc6-121">No portal do Azure, clique em **Entradas** e, em seguida, em **Adicionar uma Entrada** em seu trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="edbc6-121">In the Azure portal click **Inputs** and then click **Add an Input** in your Stream Analytics job.</span></span>
   
    ![Portal clássico do Azure - adicionar uma entrada.](./media/stream-analytics-add-inputs/1-stream-analytics-add-inputs.png)  
   
    <span data-ttu-id="edbc6-123">No portal do Azure, clique no bloco **Entradas** no seu trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="edbc6-123">In the Azure portal click the **Inputs** tile in your Stream Analytics job.</span></span>  
   
    ![Portal do Azure - adicionar entrada de dados.](./media/stream-analytics-add-inputs/7-stream-analytics-add-inputs.png)  
2. <span data-ttu-id="edbc6-125">Especifique o tipo de entrada: **Fluxo de dados** ou **Dados de referência**.</span><span class="sxs-lookup"><span data-stu-id="edbc6-125">Specify the type of the input: either **Data stream** or **Reference data**.</span></span>
   
    ![Adicionar a entrada de dados correta, transmitidos por streaming ou de referência](./media/stream-analytics-add-inputs/2-stream-analytics-add-inputs.png)  
   
    ![Adicionar a entrada de dados correta, transmitidos por streaming ou de referência](./media/stream-analytics-add-inputs/8-stream-analytics-add-inputs.png)  
3. <span data-ttu-id="edbc6-128">Se criar uma entrada de Fluxo de Dados, especifique o tipo de fonte para a entrada.</span><span class="sxs-lookup"><span data-stu-id="edbc6-128">If creating a Data Stream input, specify the source type for the input.</span></span>  <span data-ttu-id="edbc6-129">Essa etapa pode ser ignorada durante a criação dos Dados de Referência, pois atualmente há suporte apenas para o armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="edbc6-129">This step can be skipped during Reference Data creation as only Blob storage is supported at this time.</span></span>
   
    ![Adicionar a entrada de dados do streaming de dados](./media/stream-analytics-add-inputs/3-stream-analytics-add-inputs.png)  
   
    ![Adicionar a entrada de dados do streaming de dados](./media/stream-analytics-add-inputs/9-stream-analytics-add-inputs.png)  
4. <span data-ttu-id="edbc6-132">Forneça um nome amigável para essa entrada na caixa Alias de Entrada.</span><span class="sxs-lookup"><span data-stu-id="edbc6-132">Provide a friendly name for this input in the Input Alias box.</span></span>  <span data-ttu-id="edbc6-133">Esse nome será usado na consulta do trabalho posteriormente para fazer referência à entrada.</span><span class="sxs-lookup"><span data-stu-id="edbc6-133">This name will be used in your job's query later on to refer to the input.</span></span>
   
    <span data-ttu-id="edbc6-134">Preencha o restante das propriedades de conexão necessárias para se conectar à fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="edbc6-134">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="edbc6-135">Esses campos variam de acordo com o tipo de entrada e de fonte e são definidos detalhadamente [aqui](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="edbc6-135">These fields vary by type of input and source type and are defined in detail [here](stream-analytics-create-a-job.md).</span></span>  
   
    ![Adicionar entrada de dados do hub de eventos](./media/stream-analytics-add-inputs/4-stream-analytics-add-inputs.png)  
5. <span data-ttu-id="edbc6-137">Especifique as configurações de serialização para os dados de entrada:</span><span class="sxs-lookup"><span data-stu-id="edbc6-137">Specify the serialization settings for the input data:</span></span>
   
   * <span data-ttu-id="edbc6-138">Para garantir que suas consultas funcionem da maneira esperada, especifique o **formato de serialização de evento** de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="edbc6-138">To make sure your queries work the way you expect, specify the **Event Serialization Format** of incoming data.</span></span>  <span data-ttu-id="edbc6-139">Os formatos de serialização com suporte são JSON, CSV e Avro.</span><span class="sxs-lookup"><span data-stu-id="edbc6-139">Supported serialization formats are JSON, CSV, and Avro.</span></span>
   * <span data-ttu-id="edbc6-140">Verifique a **Codificação** para os dados.</span><span class="sxs-lookup"><span data-stu-id="edbc6-140">Verify the **Encoding** for the data.</span></span>  <span data-ttu-id="edbc6-141">UTF-8 é o único formato de codificação com suporte no momento.</span><span class="sxs-lookup"><span data-stu-id="edbc6-141">UTF-8 is the only supported encoding format at this time.</span></span>
     
     ![Configurações de serialização de dados para entrada de dados](./media/stream-analytics-add-inputs/5-stream-analytics-add-inputs.png)  
     
     ![Configurações de serialização de dados para entrada de dados](./media/stream-analytics-add-inputs/10-stream-analytics-add-inputs.png)  
6. <span data-ttu-id="edbc6-144">Depois de concluir a criação da entrada, o Stream Analytics verificará se ele pode se conectar à fonte de entrada.</span><span class="sxs-lookup"><span data-stu-id="edbc6-144">After completing the input creation, Stream Analytics will verify that it can connect to the input source.</span></span>  <span data-ttu-id="edbc6-145">Você pode exibir o status da operação Testar Conexão no Hub de notificação.</span><span class="sxs-lookup"><span data-stu-id="edbc6-145">You can view the status of the Test Connection operation in the Notification hub.</span></span>
   
    ![Testar conexão da entrada de dados de streaming](./media/stream-analytics-add-inputs/6-stream-analytics-add-inputs.png)  
   
    ![Testar conexão da entrada de dados de streaming](./media/stream-analytics-add-inputs/11-stream-analytics-add-inputs.png)  

## <a name="get-help-with-streaming-data-inputs"></a><span data-ttu-id="edbc6-148">Obter ajuda com a transmissão de entradas de dados</span><span class="sxs-lookup"><span data-stu-id="edbc6-148">Get help with streaming data inputs</span></span>
<span data-ttu-id="edbc6-149">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="edbc6-149">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="edbc6-150">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="edbc6-150">Next steps</span></span>
* [<span data-ttu-id="edbc6-151">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="edbc6-151">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="edbc6-152">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="edbc6-152">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="edbc6-153">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="edbc6-153">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="edbc6-154">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="edbc6-154">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="edbc6-155">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="edbc6-155">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

