---
title: "Olá aaaUse modo de execução de vértice no Data Lake Tools para Visual Studio | Microsoft Docs"
description: "Saiba como toouse Olá trabalhos de análise Data Lake tooexam exibição de execuções de vértice."
services: data-lake-analytics
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 5366d852-e7d6-44cf-a88c-e9f52f15f7df
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 10/13/2016
ms.author: jgao
ms.openlocfilehash: fb54d2af8a32aa27a54ff50a73c1b4903677a21e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="8f9d1-103">Olá Use exibição de execuções de vértice no Data Lake Tools para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8f9d1-103">Use hello Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="8f9d1-104">Saiba como toouse Olá trabalhos de análise Data Lake tooexam exibição de execuções de vértice.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-104">Learn how toouse hello Vertex Execution View tooexam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8f9d1-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="8f9d1-105">Prerequisites</span></span>

<span data-ttu-id="8f9d1-106">É necessário um conhecimento básico de como usar Data Lake Tools para o script do Visual Studio toodevelop U-SQL.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-106">You need basic knowledge of using Data Lake Tools for Visual Studio toodevelop U-SQL script.</span></span>  <span data-ttu-id="8f9d1-107">Confira [Tutorial: desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="8f9d1-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-hello-vertex-execution-view"></a><span data-ttu-id="8f9d1-108">Olá abrir modo de execução de vértice</span><span class="sxs-lookup"><span data-stu-id="8f9d1-108">Open hello Vertex Execution View</span></span>
<span data-ttu-id="8f9d1-109">Abra um trabalho de U-SQL em Ferramentas do Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="8f9d1-110">Clique em **exibição de execuções de vértice** no canto do hello inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-110">Click **Vertex Execution View** in hello bottom left corner.</span></span> <span data-ttu-id="8f9d1-111">Você pode ser perfis tooload solicitada pela primeira vez e pode levar algum tempo dependendo de sua conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-111">You may be prompted tooload profiles first and it can take some time depending on your network connectivity.</span></span>

![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="8f9d1-113">Noções básicas do Modo de Exibição de Execução de Vértice</span><span class="sxs-lookup"><span data-stu-id="8f9d1-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="8f9d1-114">Olá vértice execução exibição tem três partes:</span><span class="sxs-lookup"><span data-stu-id="8f9d1-114">hello Vertex Execution View has three parts:</span></span>

![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="8f9d1-116">Olá **seletor de vértice** permite esquerdo Olá você seleciona vértices pelos recursos (como top 10 dados de leitura, ou optar por estágio).</span><span class="sxs-lookup"><span data-stu-id="8f9d1-116">hello **Vertex selector** on hello left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="8f9d1-117">Um dos filtros usados com mais frequência do hello é Olá toosee **vértices no caminho crítico**.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-117">One of hello most commonly-used filters is toosee hello **vertices on critical path**.</span></span> <span data-ttu-id="8f9d1-118">Olá **caminho crítico** Olá a cadeia mais longa dos vértices de um trabalho de U-SQL.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-118">hello **Critical path** is hello longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="8f9d1-119">Caminho crítico de saudação compreensão é útil para otimizar seus trabalhos verificando quais vértice leva tempo mais longo de saudação.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-119">Understanding hello critical path is useful for optimizing your jobs by checking which vertex takes hello longest time.</span></span>
  
![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="8f9d1-121">painel da parte superior central de saudação mostra Olá **executando o status de todos os vértices de saudação**.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-121">hello top center pane shows hello **running status of all hello vertices**.</span></span>
  
![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="8f9d1-123">Painel de central Olá inferior mostra informações sobre cada vértice:</span><span class="sxs-lookup"><span data-stu-id="8f9d1-123">hello bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="8f9d1-124">Nome de processo: nome de saudação da instância de vértice hello.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-124">Process Name: hello name of hello vertex instance.</span></span> <span data-ttu-id="8f9d1-125">Ele é composto por diferentes partes em StageName|VertexName|VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="8f9d1-126">Por exemplo, vértice de .v1 [62] Olá SV7_Split representa Olá segunda instância em execução (.v1, índice a partir de 0) do número de vértice 62 no estágio SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-126">For example, hello SV7_Split[62].v1 vertex stands for hello second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="8f9d1-127">Gravadas/leitura total de dados: dados saudação foram lida/gravada por este vértice.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-127">Total Data Read/Written: hello data was read/written by this vertex.</span></span>
* <span data-ttu-id="8f9d1-128">Status de estado/saída: Olá status final quando vértice Olá é finalizada.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-128">State/Exit Status: hello final status when hello vertex is ended.</span></span>
* <span data-ttu-id="8f9d1-129">Tipo de falha do código de saída: erro de saudação ao vértice Olá falha.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-129">Exit Code/Failure Type: hello error when hello vertex failed.</span></span>
* <span data-ttu-id="8f9d1-130">Motivo da criação: Por que vértice Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-130">Creation Reason: Why hello vertex was created.</span></span>
* <span data-ttu-id="8f9d1-131">Latência de fila do recurso latência/processo latência/NP: Olá tempo para Olá vértice toowait para toostay na fila hello, tooprocess dados e recursos.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-131">Resource Latency/Process Latency/PN Queue Latency: hello time taken for hello vertex toowait for resources, tooprocess data, and toostay in hello queue.</span></span>
* <span data-ttu-id="8f9d1-132">GUID de processo/criador: GUID vértice de execução atual hello ou seu criador.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-132">Process/Creator GUID: GUID for hello current running vertex or its creator.</span></span>
* <span data-ttu-id="8f9d1-133">Versão: instância Olá N-ésimo da saudação executando vértice (o sistema Olá pode agendar novas instâncias de um vértice para muitos motivos, por exemplo, o failover, computação redundância, etc.)</span><span class="sxs-lookup"><span data-stu-id="8f9d1-133">Version: hello N-th instance of hello running vertex (hello system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="8f9d1-134">Hora da Criação da Versão.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-134">Version Created Time.</span></span>
* <span data-ttu-id="8f9d1-135">Processar criar Iniciar processo/tempo na fila tempo/processo Iniciar tempo/processo concluir tempo: criação; iniciado o processo de vértice de saudação Quando o processo de vértice de saudação começa tooqueue; Olá quando determinados início do processo de vértice; Quando hello determinados vértice é concluída.</span><span class="sxs-lookup"><span data-stu-id="8f9d1-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when hello vertex process starts creation; when hello vertex process starts tooqueue; when hello certain vertex process starts; when hello certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8f9d1-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8f9d1-136">Next steps</span></span>
* <span data-ttu-id="8f9d1-137">toolog informações de diagnóstico, consulte [acessar logs de diagnóstico para análise do Azure Data Lake](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="8f9d1-137">toolog diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="8f9d1-138">toosee uma consulta mais complexa, consulte [site analisar logs usando a análise do Azure Data Lake](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="8f9d1-138">toosee a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="8f9d1-139">detalhes do trabalho tooview, consulte [navegador de trabalho de uso e a exibição de trabalho de trabalhos da análise Azure Data lake](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="8f9d1-139">tooview job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
