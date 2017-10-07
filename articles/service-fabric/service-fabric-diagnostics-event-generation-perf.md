---
title: "aaaAzure monitoramento de desempenho do serviço de malha | Microsoft Docs"
description: "Saiba mais sobre os contadores de desempenho para o monitoramento e diagnóstico de clusters do Azure Service Fabric."
services: service-fabric
documentationcenter: .net
author: dkkapur
manager: timlt
editor: 
ms.assetid: 
ms.service: service-fabric
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: NA
ms.date: 06/30/2017
ms.author: dekapur
ms.openlocfilehash: 54d4c62b7250a1f70b0898ba07ae5a37716f4cf4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="b36dd-103">Métricas de desempenho</span><span class="sxs-lookup"><span data-stu-id="b36dd-103">Performance metrics</span></span>

<span data-ttu-id="b36dd-104">Métricas devem ser coletados toounderstand Olá desempenho do cluster, bem como Olá aplicativos em execução.</span><span class="sxs-lookup"><span data-stu-id="b36dd-104">Metrics should be collected toounderstand hello performance of your cluster as well as hello applications running in it.</span></span> <span data-ttu-id="b36dd-105">Para clusters de malha do serviço, recomendamos coletar Olá contadores de desempenho a seguir.</span><span class="sxs-lookup"><span data-stu-id="b36dd-105">For Service Fabric clusters, we recommend collecting hello following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="b36dd-106">Nós</span><span class="sxs-lookup"><span data-stu-id="b36dd-106">Nodes</span></span>

<span data-ttu-id="b36dd-107">Para máquinas de saudação no seu cluster, considere coletando Olá toobetter entender Olá carga em cada computador e fazer cluster apropriados dimensionamento decisões de contadores de desempenho a seguir.</span><span class="sxs-lookup"><span data-stu-id="b36dd-107">For hello machines in your cluster, consider collecting hello following performance counters toobetter understand hello load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="b36dd-108">Categoria do Contador</span><span class="sxs-lookup"><span data-stu-id="b36dd-108">Counter Category</span></span> | <span data-ttu-id="b36dd-109">Nome do contador</span><span class="sxs-lookup"><span data-stu-id="b36dd-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="b36dd-110">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="b36dd-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="b36dd-111">Média Tamanho de Fila de Leitura de Disco</span><span class="sxs-lookup"><span data-stu-id="b36dd-111">Avg. Disk Read Queue Length</span></span> |
| <span data-ttu-id="b36dd-112">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="b36dd-112">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="b36dd-113">Média Tamanho de Fila de Gravação de Disco</span><span class="sxs-lookup"><span data-stu-id="b36dd-113">Avg. Disk Write Queue Length</span></span> |
| <span data-ttu-id="b36dd-114">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="b36dd-114">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="b36dd-115">Média de segundos/Leitura do Disco</span><span class="sxs-lookup"><span data-stu-id="b36dd-115">Avg. Disk sec/Read</span></span> |
| <span data-ttu-id="b36dd-116">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="b36dd-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="b36dd-117">Média de segundos/Gravação do Disco</span><span class="sxs-lookup"><span data-stu-id="b36dd-117">Avg. Disk sec/Write</span></span> |
| <span data-ttu-id="b36dd-118">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="b36dd-118">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="b36dd-119">Leituras de Disco/s </span><span class="sxs-lookup"><span data-stu-id="b36dd-119">Disk Reads/sec</span></span> |
| <span data-ttu-id="b36dd-120">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="b36dd-120">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="b36dd-121">Bytes Lidos no Disco/s </span><span class="sxs-lookup"><span data-stu-id="b36dd-121">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="b36dd-122">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="b36dd-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="b36dd-123">Gravações de Disco/s</span><span class="sxs-lookup"><span data-stu-id="b36dd-123">Disk Writes/sec</span></span> |
| <span data-ttu-id="b36dd-124">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="b36dd-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="b36dd-125">Bytes Gravados no Disco/s</span><span class="sxs-lookup"><span data-stu-id="b36dd-125">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="b36dd-126">Memória</span><span class="sxs-lookup"><span data-stu-id="b36dd-126">Memory</span></span> | <span data-ttu-id="b36dd-127">MBytes Disponíveis</span><span class="sxs-lookup"><span data-stu-id="b36dd-127">Available MBytes</span></span> |
| <span data-ttu-id="b36dd-128">PagingFile</span><span class="sxs-lookup"><span data-stu-id="b36dd-128">PagingFile</span></span> | <span data-ttu-id="b36dd-129">% Uso</span><span class="sxs-lookup"><span data-stu-id="b36dd-129">% Usage</span></span> |
| <span data-ttu-id="b36dd-130">Processo(Total)</span><span class="sxs-lookup"><span data-stu-id="b36dd-130">Process(Total)</span></span> | <span data-ttu-id="b36dd-131">% Tempo do Processador</span><span class="sxs-lookup"><span data-stu-id="b36dd-131">% Processor Time</span></span> |
| <span data-ttu-id="b36dd-132">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-132">Process (per service)</span></span> | <span data-ttu-id="b36dd-133">% Tempo do Processador</span><span class="sxs-lookup"><span data-stu-id="b36dd-133">% Processor Time</span></span> |
| <span data-ttu-id="b36dd-134">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-134">Process (per service)</span></span> | <span data-ttu-id="b36dd-135">ID do Processo</span><span class="sxs-lookup"><span data-stu-id="b36dd-135">ID Process</span></span> |
| <span data-ttu-id="b36dd-136">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-136">Process (per service)</span></span> | <span data-ttu-id="b36dd-137">Bytes Particulares</span><span class="sxs-lookup"><span data-stu-id="b36dd-137">Private Bytes</span></span> |
| <span data-ttu-id="b36dd-138">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-138">Process (per service)</span></span> | <span data-ttu-id="b36dd-139">Contagem de Threads</span><span class="sxs-lookup"><span data-stu-id="b36dd-139">Thread Count</span></span> |
| <span data-ttu-id="b36dd-140">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-140">Process (per service)</span></span> | <span data-ttu-id="b36dd-141">Bytes Virtuais</span><span class="sxs-lookup"><span data-stu-id="b36dd-141">Virtual Bytes</span></span> |
| <span data-ttu-id="b36dd-142">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-142">Process (per service)</span></span> | <span data-ttu-id="b36dd-143">Conjunto de Trabalho</span><span class="sxs-lookup"><span data-stu-id="b36dd-143">Working Set</span></span> |
| <span data-ttu-id="b36dd-144">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-144">Process (per service)</span></span> | <span data-ttu-id="b36dd-145">Conjunto de Trabalho - Particular</span><span class="sxs-lookup"><span data-stu-id="b36dd-145">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="b36dd-146">Aplicativos e serviços de .NET</span><span class="sxs-lookup"><span data-stu-id="b36dd-146">.NET applications and services</span></span>

<span data-ttu-id="b36dd-147">Olá coletar contadores a seguir se você estiver implantando o .NET de serviços de cluster tooyour.</span><span class="sxs-lookup"><span data-stu-id="b36dd-147">Collect hello following counters if you are deploying .NET services tooyour cluster.</span></span> 

| <span data-ttu-id="b36dd-148">Categoria do Contador</span><span class="sxs-lookup"><span data-stu-id="b36dd-148">Counter Category</span></span> | <span data-ttu-id="b36dd-149">Nome do contador</span><span class="sxs-lookup"><span data-stu-id="b36dd-149">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="b36dd-150">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-150">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="b36dd-151">ID do Processo</span><span class="sxs-lookup"><span data-stu-id="b36dd-151">Process ID</span></span> |
| <span data-ttu-id="b36dd-152">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-152">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="b36dd-153">Nº Total de Bytes confirmados</span><span class="sxs-lookup"><span data-stu-id="b36dd-153"># Total committed Bytes</span></span> |
| <span data-ttu-id="b36dd-154">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="b36dd-155">N º Total de Bytes reservados</span><span class="sxs-lookup"><span data-stu-id="b36dd-155"># Total reserved Bytes</span></span> |
| <span data-ttu-id="b36dd-156">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="b36dd-157">N º de Bytes em todos os Heaps</span><span class="sxs-lookup"><span data-stu-id="b36dd-157"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="b36dd-158">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="b36dd-159">Nº de Coleções Geração 0</span><span class="sxs-lookup"><span data-stu-id="b36dd-159"># Gen 0 Collections</span></span> |
| <span data-ttu-id="b36dd-160">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="b36dd-161">Nº de Coleções Geração 1</span><span class="sxs-lookup"><span data-stu-id="b36dd-161"># Gen 1 Collections</span></span> |
| <span data-ttu-id="b36dd-162">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="b36dd-163">Nº de Coleções Geração 2</span><span class="sxs-lookup"><span data-stu-id="b36dd-163"># Gen 2 Collections</span></span> |
| <span data-ttu-id="b36dd-164">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="b36dd-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="b36dd-165">% de Tempo na GC</span><span class="sxs-lookup"><span data-stu-id="b36dd-165">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="b36dd-166">Contadores de desempenho personalizados do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="b36dd-166">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="b36dd-167">O Service Fabric gera uma quantidade significativa de contadores de desempenho personalizados.</span><span class="sxs-lookup"><span data-stu-id="b36dd-167">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="b36dd-168">Se você tiver Olá SDK instalado, você pode ver lista abrangente de saudação em seu computador Windows em seu aplicativo do Monitor de desempenho (Iniciar > Monitor de desempenho).</span><span class="sxs-lookup"><span data-stu-id="b36dd-168">If you have hello SDK installed, you can see hello comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="b36dd-169">Em aplicativos de saudação você está implantando tooyour cluster, se você estiver usando Reliable Actors, adicione countes de `Service Fabric Actor` e `Service Fabric Actor Method` categorias (consulte [Service Fabric confiável atores diagnóstico](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="b36dd-169">In hello applications you are deploying tooyour cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="b36dd-170">Se você usar os Reliable Services, teremos as categorias de contadores `Service Fabric Service` e `Service Fabric Service Method` das quais você deverá coletar contadores.</span><span class="sxs-lookup"><span data-stu-id="b36dd-170">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="b36dd-171">Se você usar coleções confiável, é recomendável adicionar Olá `Avg. Transaction ms/Commit` de saudação `Service Fabric Transactional Replicator` toocollect latência de confirmação média Olá por métrica da transação.</span><span class="sxs-lookup"><span data-stu-id="b36dd-171">If you use Reliable Collections, we recommend adding hello `Avg. Transaction ms/Commit` from hello `Service Fabric Transactional Replicator` toocollect hello average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="b36dd-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b36dd-172">Next steps</span></span>

* <span data-ttu-id="b36dd-173">Saiba mais sobre [geração de eventos no nível de plataforma Olá](service-fabric-diagnostics-event-generation-infra.md) na malha do serviço</span><span class="sxs-lookup"><span data-stu-id="b36dd-173">Learn more about [event generation at hello platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="b36dd-174">Coletar métricas de desempenho por meio dos [Diagnóstico do Azure](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="b36dd-174">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
