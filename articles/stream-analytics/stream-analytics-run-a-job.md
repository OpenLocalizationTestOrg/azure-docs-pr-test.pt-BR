---
title: "Como iniciar trabalhos de transmissão por streaming no Stream Analytics | Microsoft Docs"
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
ms.openlocfilehash: 9a3ff37a893b0f29a2ac2eda6cd50687ee779ead
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="how-to-run-a-streaming-job-in-azure-stream-analytics"></a><span data-ttu-id="49fc6-104">Como executar um trabalho de streaming no Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="49fc6-104">How to run a streaming job in Azure Stream Analytics</span></span>
<span data-ttu-id="49fc6-105">Quando uma entrada, consulta e saída de trabalho forem especificadas, você poderá iniciar o trabalho do Stream Analytics.</span><span class="sxs-lookup"><span data-stu-id="49fc6-105">When a job input, query and output have all been specified you can start the Stream Analytics job.</span></span>

<span data-ttu-id="49fc6-106">Para iniciar o trabalho:</span><span class="sxs-lookup"><span data-stu-id="49fc6-106">To start your job:</span></span>

1. <span data-ttu-id="49fc6-107">No portal clássico do Azure, no painel de trabalho, clique em **Iniciar** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="49fc6-107">In the Azure Classic portal, from the job dashboard, click **Start** at the bottom of the page.</span></span>
   
   ![Botão Iniciar trabalho](./media/stream-analytics-run-a-job/1-stream-analytics-run-a-job.png)  
   
   <span data-ttu-id="49fc6-109">No portal do Azure, clique em **Iniciar** na parte superior da página de trabalho.</span><span class="sxs-lookup"><span data-stu-id="49fc6-109">In the Azure portal, click **Start** at the top of your job page.</span></span>
   
   ![Botão Iniciar trabalho no Portal do Azure](./media/stream-analytics-run-a-job/4-stream-analytics-run-a-job.png)  
2. <span data-ttu-id="49fc6-111">Especifique um valor de **Iniciar Saída** para determinar quando esse trabalho começará a produzir uma saída.</span><span class="sxs-lookup"><span data-stu-id="49fc6-111">Specify a **Start Output** value to determine when this job will start producing output.</span></span> <span data-ttu-id="49fc6-112">A configuração padrão para trabalhos que não foram iniciados anteriormente é **Hora de Início do Trabalho**, o que significa que o trabalho começará imediatamente a processar os dados.</span><span class="sxs-lookup"><span data-stu-id="49fc6-112">The default setting for jobs that have not previously been started is **Job Start Time**, which means that the job will immediately start processing data.</span></span> <span data-ttu-id="49fc6-113">Você também pode especificar um tempo **Personalizado** no passado (para o consumo de dados históricos) ou no futuro (para atrasar o processamento até um momento futuro).</span><span class="sxs-lookup"><span data-stu-id="49fc6-113">You can also specify a **Custom** time in the past (for consuming historical data) or the future (to delay processing until a future time).</span></span> <span data-ttu-id="49fc6-114">Para os casos em que um trabalho foi anteriormente iniciado e interrompido, a opção **Hora da Última Interrupção** está disponível para retomar o trabalho da última hora de saída e evitar a perda de dados.</span><span class="sxs-lookup"><span data-stu-id="49fc6-114">For cases when a job has been previously started and stopped, the option **Last Stopped Time** is available in order to resume the job from the last output time and avoid data loss.</span></span>  
   
   ![Hora de início do trabalho de streaming](./media/stream-analytics-run-a-job/2-stream-analytics-run-a-job.png)  
   
   ![Hora de início do trabalho de transmissão no Portal do Azure](./media/stream-analytics-run-a-job/5-stream-analytics-run-a-job.png)  
3. <span data-ttu-id="49fc6-117">Confirme sua seleção.</span><span class="sxs-lookup"><span data-stu-id="49fc6-117">Confirm your selection.</span></span> <span data-ttu-id="49fc6-118">O status do trabalho será alterado para *Iniciando* e logo mudará para *Em execução* quando o trabalho for iniciado.</span><span class="sxs-lookup"><span data-stu-id="49fc6-118">The job status will change to *Starting* and will shortly move to *Running* once the job has started.</span></span> <span data-ttu-id="49fc6-119">Você pode monitorar o andamento da operação **Iniciar** no **Hub de Notificação**:</span><span class="sxs-lookup"><span data-stu-id="49fc6-119">You can monitor the progress of the **Start** operation in the **Notification Hub**:</span></span>
   
   ![andamento do trabalho de streaming](./media/stream-analytics-run-a-job/3-stream-analytics-run-a-job.png)  
   
   ![Andamento do trabalho de transmissão no Portal do Azure](./media/stream-analytics-run-a-job/6-stream-analytics-run-a-job.png)  

## <a name="get-help"></a><span data-ttu-id="49fc6-122">Obter ajuda</span><span class="sxs-lookup"><span data-stu-id="49fc6-122">Get help</span></span>
<span data-ttu-id="49fc6-123">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="49fc6-123">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="49fc6-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="49fc6-124">Next steps</span></span>
* [<span data-ttu-id="49fc6-125">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="49fc6-125">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="49fc6-126">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="49fc6-126">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="49fc6-127">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="49fc6-127">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="49fc6-128">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="49fc6-128">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="49fc6-129">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="49fc6-129">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

