---
title: "Introdução às funções de janela do Stream Analytics | Microsoft Docs"
description: "Saiba mais sobre as três funções de Janela no Stream Analytics (em cascata, de salto, deslizante)."
keywords: janela em cascata, janela deslizante, janela de salto
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: 0d8d8717-5d23-43f0-b475-af078ab4627d
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 09915ad747153210f655b152355c551046066a88
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="introduction-to-stream-analytics-window-functions"></a><span data-ttu-id="3bbf2-104">Introdução às funções de janela do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3bbf2-104">Introduction to Stream Analytics Window functions</span></span>
<span data-ttu-id="3bbf2-105">Em muitos cenários de streaming em tempo real, é necessário executar operações apenas nos dados contidos nas janelas temporais.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-105">In many real time streaming scenarios, it is necessary to perform operations only on the data contained in temporal windows.</span></span> <span data-ttu-id="3bbf2-106">O suporte nativo para funções de janela é um importante recurso do Stream Analytics do Azure, que faz toda a diferença na produtividade do desenvolvedor em trabalhos complexos de processamento de fluxo.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves the needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="3bbf2-107">O Stream Analytics permite aos desenvolvedores usar as janelas [**Em cascata**](https://msdn.microsoft.com/library/dn835055.aspx), [**De salto**](https://msdn.microsoft.com/library/dn835041.aspx) e [**Deslizante**](https://msdn.microsoft.com/library/dn835051.aspx) para executar operações temporais nos dados de streaming.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-107">Stream Analytics enables developers to use [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows to perform temporal operations on streaming data.</span></span> <span data-ttu-id="3bbf2-108">Vale a pena observar que toda saída de operações de [Janela](https://msdn.microsoft.com/library/dn835019.aspx) resulta no **fim** da janela.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at the **end** of the window.</span></span> <span data-ttu-id="3bbf2-109">A saída da janela será um evento único baseado na função agregada usada.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-109">The output of the window will be single event based on the aggregate function used.</span></span> <span data-ttu-id="3bbf2-110">O evento terá o carimbo de data/hora do término da janela e todas as funções de Janela serão definidas com um comprimento fixo.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-110">The event will have the time stamp of the end of the window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="3bbf2-111">Por fim, é importante observar que todas as funções de Janela devem ser usadas em uma cláusula [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx).</span><span class="sxs-lookup"><span data-stu-id="3bbf2-111">Lastly it is important to note that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Conceitos de funções de Janela do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="3bbf2-113">Janela em Cascata</span><span class="sxs-lookup"><span data-stu-id="3bbf2-113">Tumbling Window</span></span>
<span data-ttu-id="3bbf2-114">As funções de Janela em Cascata são usadas para segmentar um fluxo de dados em segmentos de tempo distintos e executar uma função neles, como no exemplo abaixo.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-114">Tumbling window functions are used to segment a data stream into distinct time segments and perform a function against them, such as the example below.</span></span> <span data-ttu-id="3bbf2-115">Os principais diferenciais de uma Janela em Cascata são: elas se repetem, não se sobrepõem e um evento não pode pertencer a mais de uma janela em cascata.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-115">The key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong to more than one tumbling window.</span></span>

![Introdução às funções de Janela em cascata do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="3bbf2-117">Janela de Salto</span><span class="sxs-lookup"><span data-stu-id="3bbf2-117">Hopping Window</span></span>
<span data-ttu-id="3bbf2-118">As funções da Janela de Salto pulam para frente um período fixo no tempo.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="3bbf2-119">É fácil pensar nelas como Janelas em Cascata que podem se sobrepor, de modo que os eventos podem pertencer a mais de um conjunto de resultados da Janela de Salto.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-119">It may be easy to think of them as Tumbling windows that can overlap, so events can belong to more than one Hopping window result set.</span></span> <span data-ttu-id="3bbf2-120">Para criar uma Janela de Salto da mesma forma que uma Janela em Cascata, basta especificar o tamanho do salto para ser do mesmo tamanho da janela.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-120">To make a Hopping window the same as a Tumbling window one would simply specify the hop size to be the same as the window size.</span></span> 

![Introdução às funções de Janela de salto do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="3bbf2-122">Janela Deslizante</span><span class="sxs-lookup"><span data-stu-id="3bbf2-122">Sliding Window</span></span>
<span data-ttu-id="3bbf2-123">As funções da Janela Deslizante, diferentemente das Janelas em Cascata e de Salto, produzem uma saída **apenas** quando um evento ocorre.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="3bbf2-124">Cada janela terá pelo menos um evento e a janela move-se continuamente para frente por um € (epsílon).</span><span class="sxs-lookup"><span data-stu-id="3bbf2-124">Every window will have at least one event and the window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="3bbf2-125">Como nas Janelas de Salto, os eventos podem pertencer a mais de uma Janela Deslizante.</span><span class="sxs-lookup"><span data-stu-id="3bbf2-125">Like Hopping Windows, events can belong to more than one Sliding Window.</span></span>

![Introdução às funções de Janela deslizante do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="3bbf2-127">Obtendo ajuda com funções de janela</span><span class="sxs-lookup"><span data-stu-id="3bbf2-127">Getting help with Window functions</span></span>
<span data-ttu-id="3bbf2-128">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="3bbf2-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="3bbf2-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3bbf2-129">Next steps</span></span>
* [<span data-ttu-id="3bbf2-130">Introdução ao Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbf2-130">Introduction to Azure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="3bbf2-131">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbf2-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="3bbf2-132">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbf2-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="3bbf2-133">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="3bbf2-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="3bbf2-134">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="3bbf2-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

