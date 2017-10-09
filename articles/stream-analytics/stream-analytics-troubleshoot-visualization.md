---
title: aaaVisualize e solucionar problemas de trabalhos do Stream Analytics | Microsoft Docs
description: "Saiba como toovisualize um trabalho de análise de fluxo de pipeline para solução de problemas usando o recurso de diagrama de diagnóstico de saudação de autoatendimento."
keywords: 
documentationcenter: 
services: stream-analytics
author: jeffstokes72
manager: jhubbard
editor: cgronlun
ms.assetid: d87841cd-c59f-4a46-b46e-8b904fdc12e9
ms.service: stream-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 03/28/2017
ms.author: jeffstok
ms.openlocfilehash: 8a6715be601fdc47b8d9caf4112da161dad22618
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="visualize-and-troubleshoot-stream-analytics-jobs"></a><span data-ttu-id="6e765-103">Visualizar e solucionar problemas com trabalhos do Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6e765-103">Visualize and troubleshoot Stream Analytics jobs</span></span>
<span data-ttu-id="6e765-104">No Stream Analytics, assim como acontece com outras tecnologias baseadas em nuvem, solução de problemas às vezes, é necessário toolook em por que um trabalho não produz saída de hello esperado (ou qualquer saída para essa finalidade).</span><span class="sxs-lookup"><span data-stu-id="6e765-104">In Stream Analytics, as with other cloud-based technologies, troubleshooting is sometimes needed toolook into why a job does not produce hello expected output (or any output for that matter).</span></span> <span data-ttu-id="6e765-105">Com isso em mente, o Stream Analytics fornece a capacidade de saudação para a visualização de um trabalho de streaming.</span><span class="sxs-lookup"><span data-stu-id="6e765-105">With this in mind, Stream Analytics provides hello capability for visualizing a streaming job.</span></span> <span data-ttu-id="6e765-106">Isso também é útil como uma ferramenta de modelagem e tem Olá benefício adicional para aqueles que exigem a documentação de seu trabalho.</span><span class="sxs-lookup"><span data-stu-id="6e765-106">This is also handy as a modeling tool and has hello side benefit for those requiring documentation of their work.</span></span>

<span data-ttu-id="6e765-107">Na visualização de saudação entradas de saudação do painel são visíveis, bem como a consulta hello está sendo executada e, em seguida, todas as saídas de saudação configurado.</span><span class="sxs-lookup"><span data-stu-id="6e765-107">In hello visualization panel hello inputs are visible as well as hello query being executed and then all hello outputs configured.</span></span> <span data-ttu-id="6e765-108">Problemas de conectividade ou a configuração se tornam mais aparentes e também pode ser útil toosee uma representação visual da sua configuração.</span><span class="sxs-lookup"><span data-stu-id="6e765-108">Connectivity or configuration issues can become more apparent and it can also be helpful toosee a visual representation of your configuration.</span></span>

## <a name="using-hello-diagnosis-diagram-tool"></a><span data-ttu-id="6e765-109">Usando a ferramenta de diagrama de diagnóstico Olá</span><span class="sxs-lookup"><span data-stu-id="6e765-109">Using hello diagnosis diagram tool</span></span>
<span data-ttu-id="6e765-110">tooaccess esse visualizador, basta clicar na Olá botão "Diagrama de diagnóstico" hello folha "Configurações" da saudação do trabalho de análise de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e765-110">tooaccess this visualizer, simply click on hello “Diagnosis diagram” button in hello “Settings” blade of hello of hello Stream Analytics job.</span></span>

![stream-analytics-troubleshoot-visualization-diagnosis-diagram](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-diagnosis-diagram1.png)

<span data-ttu-id="6e765-112">Cada entrada e saída é codificado por cores tooindicate Olá estado atual desse componente, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="6e765-112">Every input and output is color coded tooindicate hello current state of that component, as shown below.</span></span>

![stream-analytics-troubleshoot-visualization-input-map](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-input-map.png)

<span data-ttu-id="6e765-114">Quando o usuário de saudação quiser toolook consulta intermediário etapas toounderstand Olá dados fluxo padrões dentro de um trabalho, ferramenta de visualização Olá fornece uma exibição de análise de saudação da consulta Olá em suas etapas de componentes e a sequência de fluxo de saudação.</span><span class="sxs-lookup"><span data-stu-id="6e765-114">When hello user wants toolook at intermediate query steps toounderstand hello data flow patterns inside a job, hello visualization tool provides a view of hello breakdown of hello query into its component steps and hello flow sequence.</span></span> <span data-ttu-id="6e765-115">Clicando em cada etapa de consulta mostrará a seção correspondente de saudação em uma consulta de editar o painel conforme ilustrado.</span><span class="sxs-lookup"><span data-stu-id="6e765-115">Clicking on each query step will show hello corresponding section in a query editing pane as illustrated.</span></span> 

![stream-analytics-troubleshoot-visualization-intermediate-steps](./media/stream-analytics-troubleshoot-visualization/stream-analytics-troubleshoot-visualization-intermediate-steps.png)

## <a name="next-steps"></a><span data-ttu-id="6e765-117">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6e765-117">Next steps</span></span>
* [<span data-ttu-id="6e765-118">Introdução tooAzure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6e765-118">Introduction tooAzure Stream Analytics</span></span>](stream-analytics-introduction.md)
* [<span data-ttu-id="6e765-119">Introdução ao uso do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="6e765-119">Get started using Azure Stream Analytics</span></span>](stream-analytics-real-time-fraud-detection.md)
* [<span data-ttu-id="6e765-120">Dimensionar trabalhos do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="6e765-120">Scale Azure Stream Analytics jobs</span></span>](stream-analytics-scale-jobs.md)
* [<span data-ttu-id="6e765-121">Referência de Linguagem de Consulta do Stream Analytics do Azure</span><span class="sxs-lookup"><span data-stu-id="6e765-121">Azure Stream Analytics Query Language Reference</span></span>](https://msdn.microsoft.com/library/azure/dn834998.aspx)
* [<span data-ttu-id="6e765-122">Referência da API REST do Gerenciamento do Azure Stream Analytics</span><span class="sxs-lookup"><span data-stu-id="6e765-122">Azure Stream Analytics Management REST API Reference</span></span>](https://msdn.microsoft.com/library/azure/dn835031.aspx)

