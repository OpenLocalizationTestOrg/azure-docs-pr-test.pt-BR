---
title: toostart aaaHow streaming trabalhos no Stream Analytics | Microsoft Docs
description: Como executar um trabalho de streaming no Stream Analytics do Azure | segmento do roteiro de aprendizagem.
keywords: trabalhos de streaming
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 9d46950f-2b69-49ce-a567-df558c5dd820
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 67aa14860c38cbd0535d0ec4f23729445d0185c0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="how-toorun-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="6b2a9-104">Como toorun um fluxo de trabalho no Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6b2a9-104">How toorun a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="6b2a9-105">Quando um trabalho de entrada, saída e consulta todos os foram especificados que você pode iniciar o trabalho de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6b2a9-105">When a job input, query and output have all been specified you can start hello Stream Analytics job.</span></span>

<span data-ttu-id="6b2a9-106">toostart seu trabalho:</span><span class="sxs-lookup"><span data-stu-id="6b2a9-106">toostart your job:</span></span>

1. <span data-ttu-id="6b2a9-107">No portal clássico do Azure hello, no painel de trabalho hello, clique em **iniciar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="6b2a9-107">In hello Azure Classic portal, from hello job dashboard, click **Start** at hello bottom of hello page.</span></span>
   
   ![Botão Iniciar trabalho](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="6b2a9-109">No portal do Azure de Olá, clique em **iniciar** na parte superior de saudação da sua página de trabalho.</span><span class="sxs-lookup"><span data-stu-id="6b2a9-109">In hello Azure portal, click **Start** at hello top of your job page.</span></span>
   
   ![Botão Iniciar trabalho no Portal do Azure](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="6b2a9-111">Especifique um **iniciar saída** toodetermine valor quando esse trabalho iniciará a produzir a saída.</span><span class="sxs-lookup"><span data-stu-id="6b2a9-111">Specify a **Start Output** value toodetermine when this job will start producing output.</span></span> <span data-ttu-id="6b2a9-112">Olá configuração padrão para trabalhos que não foram iniciados anteriormente é **hora de início do trabalho**, que significa que o trabalho Olá imediatamente Iniciar processamento de dados.</span><span class="sxs-lookup"><span data-stu-id="6b2a9-112">hello default setting for jobs that have not previously been started is **Job Start Time**, which means that hello job will immediately start processing data.</span></span> <span data-ttu-id="6b2a9-113">Você também pode especificar um **personalizado** tempo no hello passado (para consumir dados históricos) ou Olá futura (toodelay processamento até que um tempo futuro).</span><span class="sxs-lookup"><span data-stu-id="6b2a9-113">You can also specify a **Custom** time in hello past (for consuming historical data) or hello future (toodelay processing until a future time).</span></span> <span data-ttu-id="6b2a9-114">Para casos em que um trabalho foi anteriormente iniciado e interrompido, Olá opção **hora da última interrupção** está disponível no trabalho de saudação tooresume ordem de saudação última hora de saída e evitar a perda de dados.</span><span class="sxs-lookup"><span data-stu-id="6b2a9-114">For cases when a job has been previously started and stopped, hello option **Last Stopped Time** is available in order tooresume hello job from hello last output time and avoid data loss.</span></span>  
   
   ![Hora de início do trabalho de streaming](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Hora de início do trabalho de transmissão no Portal do Azure](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="6b2a9-117">Confirme sua seleção.</span><span class="sxs-lookup"><span data-stu-id="6b2a9-117">Confirm your selection.</span></span> <span data-ttu-id="6b2a9-118">status do trabalho Olá alterará muito*iniciando* e em breve moverá muito*executando* depois que o trabalho Olá foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="6b2a9-118">hello job status will change too*Starting* and will shortly move too*Running* once hello job has started.</span></span> <span data-ttu-id="6b2a9-119">Você pode monitorar o progresso de saudação da saudação **iniciar** operação em Olá **Hub de notificação**:</span><span class="sxs-lookup"><span data-stu-id="6b2a9-119">You can monitor hello progress of hello **Start** operation in hello **Notification Hub**:</span></span>
   
   ![andamento do trabalho de streaming](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Andamento do trabalho de transmissão no Portal do Azure](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="6b2a9-122">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="6b2a9-122">Get help</span></span>
<span data-ttu-id="6b2a9-123">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="6b2a9-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="6b2a9-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6b2a9-124">Next steps</span></span>
* [<span data-ttu-id="6b2a9-125">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6b2a9-125">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6b2a9-126">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="6b2a9-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6b2a9-127">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="6b2a9-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6b2a9-128">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="6b2a9-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6b2a9-129">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6b2a9-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

