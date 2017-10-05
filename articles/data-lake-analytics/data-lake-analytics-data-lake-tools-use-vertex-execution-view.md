---
title: "Usar o Modo de Exibição de Execução de Vértice nas Ferramentas do Data Lake para Visual Studio | Microsoft Docs"
description: "Saiba como usar o Modo de Exibição de Execução de Vértice para examinar trabalhos do Data Lake Analytics."
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
ms.openlocfilehash: b788e7bc8ded86ebd49cc0be73e5b4e1bcbeaba3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-the-vertex-execution-view-in-data-lake-tools-for-visual-studio"></a><span data-ttu-id="6ad2f-103">Usar o Modo de Exibição de Execução de Vértice nas Ferramentas do Data Lake para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="6ad2f-103">Use the Vertex Execution View in Data Lake Tools for Visual Studio</span></span>
<span data-ttu-id="6ad2f-104">Saiba como usar o Modo de Exibição de Execução de Vértice para examinar trabalhos do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-104">Learn how to use the Vertex Execution View to exam Data Lake Analytics jobs.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6ad2f-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="6ad2f-105">Prerequisites</span></span>

<span data-ttu-id="6ad2f-106">Você precisa de conhecimento básico do uso das Ferramentas do Data Lake para Visual Studio para desenvolver scripts U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-106">You need basic knowledge of using Data Lake Tools for Visual Studio to develop U-SQL script.</span></span>  <span data-ttu-id="6ad2f-107">Confira [Tutorial: desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="6ad2f-107">See [Tutorial: develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>

## <a name="open-the-vertex-execution-view"></a><span data-ttu-id="6ad2f-108">Abrir o Modo de Exibição de Execução de Vértice</span><span class="sxs-lookup"><span data-stu-id="6ad2f-108">Open the Vertex Execution View</span></span>
<span data-ttu-id="6ad2f-109">Abra um trabalho de U-SQL em Ferramentas do Data Lake para Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-109">Open a U-SQL job in Data Lake Tools for Visual Studio.</span></span> <span data-ttu-id="6ad2f-110">Clique em **Exibição de Execuções de Vértice** no canto inferior esquerdo.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-110">Click **Vertex Execution View** in the bottom left corner.</span></span> <span data-ttu-id="6ad2f-111">Talvez você receba uma solicitação para carregar perfis primeiro e isso pode demorar algum tempo dependendo de sua conectividade de rede.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-111">You may be prompted to load profiles first and it can take some time depending on your network connectivity.</span></span>

![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-open-vertex-execution-view.png)

## <a name="understand-vertex-execution-view"></a><span data-ttu-id="6ad2f-113">Noções básicas do Modo de Exibição de Execução de Vértice</span><span class="sxs-lookup"><span data-stu-id="6ad2f-113">Understand Vertex Execution View</span></span>
<span data-ttu-id="6ad2f-114">A Exibição de Execuções de Vértice tem três partes:</span><span class="sxs-lookup"><span data-stu-id="6ad2f-114">The Vertex Execution View has three parts:</span></span>

![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view.png)

<span data-ttu-id="6ad2f-116">O **seletor de vértice** à esquerda permite selecionar vértices pelos recursos (como 10 principais dados lidos ou optar por estágio).</span><span class="sxs-lookup"><span data-stu-id="6ad2f-116">The **Vertex selector** on the left lets you select vertices by features (such as top 10 data read, or choose by stage).</span></span> <span data-ttu-id="6ad2f-117">Um dos filtros mais usados é para ver os **vértices no caminho crítico**.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-117">One of the most commonly-used filters is to see the **vertices on critical path**.</span></span> <span data-ttu-id="6ad2f-118">O **Caminho crítico** é a cadeia mais longa de vértices de um trabalho U-SQL.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-118">The **Critical path** is the longest chain of vertices of a U-SQL job.</span></span> <span data-ttu-id="6ad2f-119">Entender o caminho crítico é útil para otimizar seus trabalhos verificando quais vértice demoram mais.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-119">Understanding the critical path is useful for optimizing your jobs by checking which vertex takes the longest time.</span></span>
  
![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane2.png)

<span data-ttu-id="6ad2f-121">O painel central superior mostra o **status de execução de todos os vértices**.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-121">The top center pane shows the **running status of all the vertices**.</span></span>
  
![Modo de Exibição de Execução de Vértice das Ferramentas do Data Lake Analytics](./media/data-lake-analytics-data-lake-tools-use-vertex-execution-view/data-lake-tools-vertex-execution-view-pane3.png)

<span data-ttu-id="6ad2f-123">O painel central inferior mostra informações sobre cada vértice:</span><span class="sxs-lookup"><span data-stu-id="6ad2f-123">The bottom center pane shows information about each vertex:</span></span>
* <span data-ttu-id="6ad2f-124">Nome do Processo: o nome da instância do vértice.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-124">Process Name: The name of the vertex instance.</span></span> <span data-ttu-id="6ad2f-125">Ele é composto por diferentes partes em StageName|VertexName|VertexRunInstance.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-125">It is composed of different parts in StageName|VertexName|VertexRunInstance.</span></span> <span data-ttu-id="6ad2f-126">Por exemplo, o vértice de SV7_Split[62].v1 representa a segunda instância em execução (.v1, índice que começa em 0) do vértice número 62 no estágio SV7_Split.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-126">For example, the SV7_Split[62].v1 vertex stands for the second running instance (.v1, index starting from 0) of Vertex number 62 in Stage SV7_Split.</span></span>
* <span data-ttu-id="6ad2f-127">Leitura/Gravação Total de Dados: os dados foram lidos/gravados por esse vértice.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-127">Total Data Read/Written: The data was read/written by this vertex.</span></span>
* <span data-ttu-id="6ad2f-128">Estado/Status de Saída: o status final quando o vértice é encerrado.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-128">State/Exit Status: The final status when the vertex is ended.</span></span>
* <span data-ttu-id="6ad2f-129">Código de Saída/Tipo de Falha: o erro no momento da falha do vértice.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-129">Exit Code/Failure Type: The error when the vertex failed.</span></span>
* <span data-ttu-id="6ad2f-130">Motivo da Criação: por que o vértice foi criado.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-130">Creation Reason: Why the vertex was created.</span></span>
* <span data-ttu-id="6ad2f-131">Latência do Recurso/Latência do processo/ Latência da Fila de PN: o tempo necessário para o vértice aguardar recursos, processar dados e permanecer na fila.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-131">Resource Latency/Process Latency/PN Queue Latency: the time taken for the vertex to wait for resources, to process data, and to stay in the queue.</span></span>
* <span data-ttu-id="6ad2f-132">GUID do Processo/Criador: o GUID do vértice em execução no momento ou de seu criador.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-132">Process/Creator GUID: GUID for the current running vertex or its creator.</span></span>
* <span data-ttu-id="6ad2f-133">Versão: a enésima instância do vértice em execução (o sistema pode agendar novas instâncias de um vértice por vários motivos, por exemplo, para failover, redundância de computação etc.)</span><span class="sxs-lookup"><span data-stu-id="6ad2f-133">Version: the N-th instance of the running vertex (the system might schedule new instances of a vertex for many reasons, for example failover, compute redundancy, etc.)</span></span>
* <span data-ttu-id="6ad2f-134">Hora da Criação da Versão.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-134">Version Created Time.</span></span>
* <span data-ttu-id="6ad2f-135">Hora de Início da Criação do Processo/Hora de Enfileiramento do Processo/Hora de Início do processo/Hora de Conclusão do Processo: quando o processo do vértice começa a criação; quando o processo do vértice começa a enfileirar; quando o processo do vértice especificado começa; quando o vértice especificado é concluído.</span><span class="sxs-lookup"><span data-stu-id="6ad2f-135">Process Create Start Time/Process Queued Time/Process Start Time/Process Complete Time: when the vertex process starts creation; when the vertex process starts to queue; when the certain vertex process starts; when the certain vertex is completed.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6ad2f-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ad2f-136">Next steps</span></span>
* <span data-ttu-id="6ad2f-137">Para registrar em log as informações de diagnóstico, veja [Acessando os logs de diagnóstico para o Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span><span class="sxs-lookup"><span data-stu-id="6ad2f-137">To log diagnostics information, see [Accessing diagnostics logs for Azure Data Lake Analytics](data-lake-analytics-diagnostic-logs.md)</span></span>
* <span data-ttu-id="6ad2f-138">Para ver uma consulta mais complexa, consulte [Analisar logs de site usando a Análise Data Lake do Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="6ad2f-138">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="6ad2f-139">Para ver detalhes do trabalho, confira [Usar o Navegador de Trabalhos e o Modo de Exibição de Trabalho para trabalhos do Azure Data Lake Analytics](data-lake-analytics-data-lake-tools-view-jobs.md)</span><span class="sxs-lookup"><span data-stu-id="6ad2f-139">To view job details, see [Use Job Browser and Job View for Azure Data lake Analytics jobs](data-lake-analytics-data-lake-tools-view-jobs.md)</span></span>
