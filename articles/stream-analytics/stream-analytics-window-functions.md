---
title: "funções de janela de análise de tooStream aaaIntroduction | Microsoft Docs"
description: "Saiba mais sobre as três funções de janela Olá no Stream Analytics (em cascata, de salto, deslizante)."
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
ms.openlocfilehash: 7fc36eb9afb2b28e2791d925d26923145eb38074
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="introduction-toostream-analytics-window-functions"></a><span data-ttu-id="f2623-104">Funções de janela de análise de tooStream de Introdução</span><span class="sxs-lookup"><span data-stu-id="f2623-104">Introduction tooStream Analytics Window functions</span></span>
<span data-ttu-id="f2623-105">Em cenários de streaming em tempo real muitos, é operações de tooperform necessário apenas em dados de saudação contidos no windows temporal.</span><span class="sxs-lookup"><span data-stu-id="f2623-105">In many real time streaming scenarios, it is necessary tooperform operations only on hello data contained in temporal windows.</span></span> <span data-ttu-id="f2623-106">O suporte nativo para funções de janelamento é um recurso principal do Azure Stream Analytics que move agulha Olá na produtividade do desenvolvedor na criação de trabalhos de processamento de fluxo complexas.</span><span class="sxs-lookup"><span data-stu-id="f2623-106">Native support for windowing functions is a key feature of Azure Stream Analytics that moves hello needle on developer productivity in authoring complex stream processing jobs.</span></span> <span data-ttu-id="f2623-107">Análise de fluxo permite que os desenvolvedores toouse [ **em cascata**](https://msdn.microsoft.com/library/dn835055.aspx), [ **Hopping** ](https://msdn.microsoft.com/library/dn835041.aspx) e [ **deslizante** ](https://msdn.microsoft.com/library/dn835051.aspx) operações temporais do windows tooperform no fluxo de dados.</span><span class="sxs-lookup"><span data-stu-id="f2623-107">Stream Analytics enables developers toouse [**Tumbling**](https://msdn.microsoft.com/library/dn835055.aspx), [**Hopping**](https://msdn.microsoft.com/library/dn835041.aspx) and [**Sliding**](https://msdn.microsoft.com/library/dn835051.aspx) windows tooperform temporal operations on streaming data.</span></span> <span data-ttu-id="f2623-108">Vale a pena observar que todos os [janela](https://msdn.microsoft.com/library/dn835019.aspx) operações enviar os resultados em Olá **final** da janela de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2623-108">It is worth noting that all [Window](https://msdn.microsoft.com/library/dn835019.aspx) operations output results at hello **end** of hello window.</span></span> <span data-ttu-id="f2623-109">saída de saudação da janela Olá será evento único com base na função de agregação Olá usada.</span><span class="sxs-lookup"><span data-stu-id="f2623-109">hello output of hello window will be single event based on hello aggregate function used.</span></span> <span data-ttu-id="f2623-110">evento Olá terá o carimbo de hora de saudação do final de saudação da janela de saudação e todas as funções de janela são definidas com um comprimento fixo.</span><span class="sxs-lookup"><span data-stu-id="f2623-110">hello event will have hello time stamp of hello end of hello window and all Window functions are defined with a fixed length.</span></span> <span data-ttu-id="f2623-111">Por último é toonote importante que todas as funções de janela devem ser usadas em uma [ **GROUP BY** ](https://msdn.microsoft.com/library/dn835023.aspx) cláusula.</span><span class="sxs-lookup"><span data-stu-id="f2623-111">Lastly it is important toonote that all Window functions should be used in a [**GROUP BY**](https://msdn.microsoft.com/library/dn835023.aspx) clause.</span></span>

![Conceitos de funções de Janela do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-conceptual.png)

## <a name="tumbling-window"></a><span data-ttu-id="f2623-113">Janela em Cascata</span><span class="sxs-lookup"><span data-stu-id="f2623-113">Tumbling Window</span></span>
<span data-ttu-id="f2623-114">Funções de janela em cascata são usado toosegment um fluxo de dados em segmentos distintos de tempo e executam uma função em relação a elas, como o exemplo hello abaixo.</span><span class="sxs-lookup"><span data-stu-id="f2623-114">Tumbling window functions are used toosegment a data stream into distinct time segments and perform a function against them, such as hello example below.</span></span> <span data-ttu-id="f2623-115">principais diferenciais saudação de uma janela em cascata são que eles se repetir, não se sobrepõem e um evento não pode pertencer toomore que uma janela em cascata.</span><span class="sxs-lookup"><span data-stu-id="f2623-115">hello key differentiators of a Tumbling window are that they repeat, do not overlap and an event cannot belong toomore than one tumbling window.</span></span>

![Introdução às funções de Janela em cascata do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-tumbling-intro.png)

## <a name="hopping-window"></a><span data-ttu-id="f2623-117">Janela de Salto</span><span class="sxs-lookup"><span data-stu-id="f2623-117">Hopping Window</span></span>
<span data-ttu-id="f2623-118">As funções da Janela de Salto pulam para frente um período fixo no tempo.</span><span class="sxs-lookup"><span data-stu-id="f2623-118">Hopping window functions hop forward in time by a fixed period.</span></span> <span data-ttu-id="f2623-119">Pode ser fácil toothink-los como janelas em cascata que podem se sobrepor, portanto eventos podem pertencer a toomore de um conjunto de resultados de janela Hopping.</span><span class="sxs-lookup"><span data-stu-id="f2623-119">It may be easy toothink of them as Tumbling windows that can overlap, so events can belong toomore than one Hopping window result set.</span></span> <span data-ttu-id="f2623-120">toomake uma janela Hopping Olá mesmo como uma janela em cascata um especificaria simplesmente toobe de tamanho de salto Olá Olá mesmo como o tamanho da janela hello.</span><span class="sxs-lookup"><span data-stu-id="f2623-120">toomake a Hopping window hello same as a Tumbling window one would simply specify hello hop size toobe hello same as hello window size.</span></span> 

![Introdução às funções de Janela de salto do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-hopping-intro.png)

## <a name="sliding-window"></a><span data-ttu-id="f2623-122">Janela Deslizante</span><span class="sxs-lookup"><span data-stu-id="f2623-122">Sliding Window</span></span>
<span data-ttu-id="f2623-123">As funções da Janela Deslizante, diferentemente das Janelas em Cascata e de Salto, produzem uma saída **apenas** quando um evento ocorre.</span><span class="sxs-lookup"><span data-stu-id="f2623-123">Sliding window functions, unlike Tumbling or Hopping windows, produce an output **only**  when an event occurs.</span></span> <span data-ttu-id="f2623-124">Cada janela terá pelo menos um evento e Olá continuamente avança por um € (épsilon).</span><span class="sxs-lookup"><span data-stu-id="f2623-124">Every window will have at least one event and hello window continuously moves forward by an € (epsilon).</span></span> <span data-ttu-id="f2623-125">Como as janelas de salto, eventos podem pertencer toomore que uma janela deslizante.</span><span class="sxs-lookup"><span data-stu-id="f2623-125">Like Hopping Windows, events can belong toomore than one Sliding Window.</span></span>

![Introdução às funções de Janela deslizante do Stream Analytics](media/stream-analytics-window-functions/stream-analytics-window-functions-sliding-intro.png)

## <a name="getting-help-with-window-functions"></a><span data-ttu-id="f2623-127">Obtendo ajuda com funções de janela</span><span class="sxs-lookup"><span data-stu-id="f2623-127">Getting help with Window functions</span></span>
<span data-ttu-id="f2623-128">Para obter mais assistência, experimente nosso [Fórum do Stream Analytics do Azure](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span><span class="sxs-lookup"><span data-stu-id="f2623-128">For further assistance, try our [Azure Stream Analytics forum](https://social.msdn.microsoft.com/Forums/en-US/home?forum=AzureStreamAnalytics)</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2623-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2623-129">Next steps</span></span>
* [<span data-ttu-id="f2623-130">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f2623-130">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="f2623-131">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="f2623-131">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="f2623-132">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="f2623-132">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="f2623-133">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="f2623-133">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="f2623-134">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="f2623-134">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

