---
title: "Como configurar saídas de dados para trabalhos do Stream Analytics | Microsoft Docs"
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
ms.openlocfilehash: 1ffa517469da1a8d79917b9747abc97ca3bef463
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-configure-data-outputs-for-stream-analytics-jobs"></a><span data-ttu-id="ccf2e-104">Como configurar saídas de dados para trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ccf2e-104">How to configure data outputs for Stream Analytics jobs</span></span>

<span data-ttu-id="ccf2e-105">Os trabalhos do Stream Analytics do Azure podem ser conectados a uma ou mais saídas de dados, o que define uma conexão com um coletor de dados existente.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-105">Azure Stream Analytics jobs can be connected to one or more data outputs, which define a connection to an existing data sink.</span></span> <span data-ttu-id="ccf2e-106">Conforme o trabalho do Stream Analytics processa e transforma dados de entrada, um fluxo de eventos de saída de dados é gravado na saída do trabalho.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-106">As your Stream Analytics job processes and transforms incoming data, a stream of data output events is written to your job's output.</span></span>

<span data-ttu-id="ccf2e-107">As saídas de dados do Stream Analytics podem ser usadas para dar origem a painéis ou alertas em tempo real, disparar fluxos de trabalho de movimentação de dados ou simplesmente arquivar dados para processamento em lote posteriormente.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-107">Stream Analytics data outputs can be used to source real-time dashboards or alerts, trigger data movement workflows, or simply archive data for batch processing later on.</span></span> <span data-ttu-id="ccf2e-108">O Stream Analytics integra-se perfeitamente a vários serviços do Azure, que são documentados em detalhes aqui.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-108">Stream Analytics has first class integration with several Azure services, which are documented in detail here.</span></span>

<span data-ttu-id="ccf2e-109">Para adicionar uma saída ao trabalho do Stream Analytics:</span><span class="sxs-lookup"><span data-stu-id="ccf2e-109">To add an output to your Stream Analytics job:</span></span>

1. <span data-ttu-id="ccf2e-110">No [Portal do Azure](https://portal.azure.com), abra o seu trabalho e clique em **Saídas** e, em seguida, clique em **Adicionar** na folha Saídas exibida.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-110">In the [Azure portal](https://portal.azure.com), open your job and click **Outputs** and then click **Add** in the Outputs blade that appears.</span></span>
   
    ![Adicionar saídas](./media/stream-analytics-add-outputs/1-stream-analytics-add-outputs.png)  
   
2. <span data-ttu-id="ccf2e-112">Forneça um nome amigável para essa saída na caixa **Alias de saída** .</span><span class="sxs-lookup"><span data-stu-id="ccf2e-112">Provide a friendly name for this output in the **Output Alias** box.</span></span> <span data-ttu-id="ccf2e-113">Esse nome pode ser usado na consulta do seu trabalho posteriormente para fazer referência à saída.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-113">This name can be used in your job's query later on to refer to the output.</span></span>  
   
    <span data-ttu-id="ccf2e-114">Preencha o restante das propriedades de conexão necessárias para se conectar à saída.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-114">Fill in the rest of the required connection properties to connect to your output.</span></span>  <span data-ttu-id="ccf2e-115">Esses campos variam de acordo com o tipo de saída e são definidos em detalhes aqui.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-115">These fields vary by output type and are defined in detail here.</span></span>  
   
    ![Escolher o tipo de movimentação de dados](./media/stream-analytics-add-outputs/2-stream-analytics-add-outputs.png)  
   
3. <span data-ttu-id="ccf2e-117">Dependendo do tipo de saída, talvez seja necessário especificar como os dados são serializados ou formatados.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-117">Depending on the output type, you may need to specify how the data is serialized or formatted.</span></span> <span data-ttu-id="ccf2e-118">As configurações específicas de serialização para cada tipo de saída estão documentadas aqui.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-118">The specific serialization settings for each output type are documented here.</span></span>
   
    <span data-ttu-id="ccf2e-119">Preencha o restante das propriedades de conexão necessárias para se conectar à fonte de dados.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-119">Fill in the rest of the required connection properties to connect to your data source.</span></span> <span data-ttu-id="ccf2e-120">Esses campos variam de acordo com o tipo de entrada e de fonte e são definidos detalhadamente no artigo [Criar trabalho](stream-analytics-create-a-job.md).</span><span class="sxs-lookup"><span data-stu-id="ccf2e-120">These fields vary by type of input and source type and are defined in detail in the [Create Job article](stream-analytics-create-a-job.md).</span></span>  

> [!Note]
>
> <span data-ttu-id="ccf2e-121">Qualquer elemento de saída adicionado ao trabalho deve existir antes de o trabalho ser iniciado e de os eventos começarem a fluir.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-121">Any output element added to the job, must exist before the job is started and events start flowing.</span></span> <span data-ttu-id="ccf2e-122">Por exemplo, se você usar o Armazenamento de Blobs como uma saída, o trabalho não criará uma conta de armazenamento automaticamente.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-122">For example, if you use Blob storage as an output, the job will not create a storage account automatically.</span></span> <span data-ttu-id="ccf2e-123">Ele precisa ser criado pelo usuário antes de o trabalho ASA ser iniciado.</span><span class="sxs-lookup"><span data-stu-id="ccf2e-123">It needs to be created by the user before the ASA job is started.</span></span>
> 
 

## <a name="get-help"></a><span data-ttu-id="ccf2e-124">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="ccf2e-124">Get help</span></span>
<span data-ttu-id="ccf2e-125">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="ccf2e-125">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="ccf2e-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ccf2e-126">Next steps</span></span>
* [<span data-ttu-id="ccf2e-127">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="ccf2e-127">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="ccf2e-128">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="ccf2e-128">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="ccf2e-129">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="ccf2e-129">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="ccf2e-130">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="ccf2e-130">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="ccf2e-131">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="ccf2e-131">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

