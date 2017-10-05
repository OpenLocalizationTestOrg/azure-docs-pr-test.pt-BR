---
title: Monitoramento de desempenho do Azure Service Fabric | Microsoft Docs
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
ms.openlocfilehash: 9d63148c182c705b6b49733c59ed8fdd13872d72
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="performance-metrics"></a><span data-ttu-id="6d8fe-103">Métricas de desempenho</span><span class="sxs-lookup"><span data-stu-id="6d8fe-103">Performance metrics</span></span>

<span data-ttu-id="6d8fe-104">As métricas devem ser coletadas para entender o desempenho de seu cluster, bem como os aplicativos em execução nele.</span><span class="sxs-lookup"><span data-stu-id="6d8fe-104">Metrics should be collected to understand the performance of your cluster as well as the applications running in it.</span></span> <span data-ttu-id="6d8fe-105">Para clusters do Service Fabric, recomendamos coletar os seguintes contadores de desempenho.</span><span class="sxs-lookup"><span data-stu-id="6d8fe-105">For Service Fabric clusters, we recommend collecting the following performance counters.</span></span>

## <a name="nodes"></a><span data-ttu-id="6d8fe-106">Nós</span><span class="sxs-lookup"><span data-stu-id="6d8fe-106">Nodes</span></span>

<span data-ttu-id="6d8fe-107">Para as máquinas em seu cluster, considere a possibilidade de coletar os seguintes contadores de desempenho a fim de entender melhor a carga em cada computador e tomar decisões apropriadas sobre o dimensionamento do cluster.</span><span class="sxs-lookup"><span data-stu-id="6d8fe-107">For the machines in your cluster, consider collecting the following performance counters to better understand the load on each machine and make appropriate cluster scaling decisions.</span></span>

| <span data-ttu-id="6d8fe-108">Categoria do Contador</span><span class="sxs-lookup"><span data-stu-id="6d8fe-108">Counter Category</span></span> | <span data-ttu-id="6d8fe-109">Nome do contador</span><span class="sxs-lookup"><span data-stu-id="6d8fe-109">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="6d8fe-110">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-110">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6d8fe-111">Média</span><span class="sxs-lookup"><span data-stu-id="6d8fe-111">Avg.</span></span> <span data-ttu-id="6d8fe-112">Tamanho de Fila de Leitura de Disco</span><span class="sxs-lookup"><span data-stu-id="6d8fe-112">Disk Read Queue Length</span></span> |
| <span data-ttu-id="6d8fe-113">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-113">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6d8fe-114">Média</span><span class="sxs-lookup"><span data-stu-id="6d8fe-114">Avg.</span></span> <span data-ttu-id="6d8fe-115">Tamanho de Fila de Gravação de Disco</span><span class="sxs-lookup"><span data-stu-id="6d8fe-115">Disk Write Queue Length</span></span> |
| <span data-ttu-id="6d8fe-116">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-116">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6d8fe-117">Média</span><span class="sxs-lookup"><span data-stu-id="6d8fe-117">Avg.</span></span> <span data-ttu-id="6d8fe-118">de segundos/Leitura do Disco</span><span class="sxs-lookup"><span data-stu-id="6d8fe-118">Disk sec/Read</span></span> |
| <span data-ttu-id="6d8fe-119">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-119">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6d8fe-120">Média</span><span class="sxs-lookup"><span data-stu-id="6d8fe-120">Avg.</span></span> <span data-ttu-id="6d8fe-121">de segundos/Gravação do Disco</span><span class="sxs-lookup"><span data-stu-id="6d8fe-121">Disk sec/Write</span></span> |
| <span data-ttu-id="6d8fe-122">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-122">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6d8fe-123">Leituras de Disco/s </span><span class="sxs-lookup"><span data-stu-id="6d8fe-123">Disk Reads/sec</span></span> |
| <span data-ttu-id="6d8fe-124">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-124">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6d8fe-125">Bytes Lidos no Disco/s </span><span class="sxs-lookup"><span data-stu-id="6d8fe-125">Disk Read Bytes/sec</span></span> |
| <span data-ttu-id="6d8fe-126">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-126">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6d8fe-127">Gravações de Disco/s</span><span class="sxs-lookup"><span data-stu-id="6d8fe-127">Disk Writes/sec</span></span> |
| <span data-ttu-id="6d8fe-128">PhysicalDisk(per Disco)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-128">PhysicalDisk(per Disk)</span></span> | <span data-ttu-id="6d8fe-129">Bytes Gravados no Disco/s</span><span class="sxs-lookup"><span data-stu-id="6d8fe-129">Disk Write Bytes/sec</span></span> |
| <span data-ttu-id="6d8fe-130">Memória</span><span class="sxs-lookup"><span data-stu-id="6d8fe-130">Memory</span></span> | <span data-ttu-id="6d8fe-131">MBytes Disponíveis</span><span class="sxs-lookup"><span data-stu-id="6d8fe-131">Available MBytes</span></span> |
| <span data-ttu-id="6d8fe-132">PagingFile</span><span class="sxs-lookup"><span data-stu-id="6d8fe-132">PagingFile</span></span> | <span data-ttu-id="6d8fe-133">% Uso</span><span class="sxs-lookup"><span data-stu-id="6d8fe-133">% Usage</span></span> |
| <span data-ttu-id="6d8fe-134">Processo(Total)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-134">Process(Total)</span></span> | <span data-ttu-id="6d8fe-135">% Tempo do Processador</span><span class="sxs-lookup"><span data-stu-id="6d8fe-135">% Processor Time</span></span> |
| <span data-ttu-id="6d8fe-136">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-136">Process (per service)</span></span> | <span data-ttu-id="6d8fe-137">% Tempo do Processador</span><span class="sxs-lookup"><span data-stu-id="6d8fe-137">% Processor Time</span></span> |
| <span data-ttu-id="6d8fe-138">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-138">Process (per service)</span></span> | <span data-ttu-id="6d8fe-139">ID do Processo</span><span class="sxs-lookup"><span data-stu-id="6d8fe-139">ID Process</span></span> |
| <span data-ttu-id="6d8fe-140">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-140">Process (per service)</span></span> | <span data-ttu-id="6d8fe-141">Bytes Particulares</span><span class="sxs-lookup"><span data-stu-id="6d8fe-141">Private Bytes</span></span> |
| <span data-ttu-id="6d8fe-142">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-142">Process (per service)</span></span> | <span data-ttu-id="6d8fe-143">Contagem de Threads</span><span class="sxs-lookup"><span data-stu-id="6d8fe-143">Thread Count</span></span> |
| <span data-ttu-id="6d8fe-144">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-144">Process (per service)</span></span> | <span data-ttu-id="6d8fe-145">Bytes Virtuais</span><span class="sxs-lookup"><span data-stu-id="6d8fe-145">Virtual Bytes</span></span> |
| <span data-ttu-id="6d8fe-146">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-146">Process (per service)</span></span> | <span data-ttu-id="6d8fe-147">Conjunto de Trabalho</span><span class="sxs-lookup"><span data-stu-id="6d8fe-147">Working Set</span></span> |
| <span data-ttu-id="6d8fe-148">Processo (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-148">Process (per service)</span></span> | <span data-ttu-id="6d8fe-149">Conjunto de Trabalho - Particular</span><span class="sxs-lookup"><span data-stu-id="6d8fe-149">Working Set - Private</span></span> |

## <a name="net-applications-and-services"></a><span data-ttu-id="6d8fe-150">Aplicativos e serviços de .NET</span><span class="sxs-lookup"><span data-stu-id="6d8fe-150">.NET applications and services</span></span>

<span data-ttu-id="6d8fe-151">Colete os contadores a seguir se você estiver implantando serviços .NET em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="6d8fe-151">Collect the following counters if you are deploying .NET services to your cluster.</span></span> 

| <span data-ttu-id="6d8fe-152">Categoria do Contador</span><span class="sxs-lookup"><span data-stu-id="6d8fe-152">Counter Category</span></span> | <span data-ttu-id="6d8fe-153">Nome do contador</span><span class="sxs-lookup"><span data-stu-id="6d8fe-153">Counter Name</span></span> |
| --- | --- |
| <span data-ttu-id="6d8fe-154">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-154">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6d8fe-155">ID do Processo</span><span class="sxs-lookup"><span data-stu-id="6d8fe-155">Process ID</span></span> |
| <span data-ttu-id="6d8fe-156">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-156">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6d8fe-157">Nº Total de Bytes confirmados</span><span class="sxs-lookup"><span data-stu-id="6d8fe-157"># Total committed Bytes</span></span> |
| <span data-ttu-id="6d8fe-158">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-158">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6d8fe-159">N º Total de Bytes reservados</span><span class="sxs-lookup"><span data-stu-id="6d8fe-159"># Total reserved Bytes</span></span> |
| <span data-ttu-id="6d8fe-160">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-160">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6d8fe-161">N º de Bytes em todos os Heaps</span><span class="sxs-lookup"><span data-stu-id="6d8fe-161"># Bytes in all Heaps</span></span> |
| <span data-ttu-id="6d8fe-162">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-162">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6d8fe-163">Nº de Coleções Geração 0</span><span class="sxs-lookup"><span data-stu-id="6d8fe-163"># Gen 0 Collections</span></span> |
| <span data-ttu-id="6d8fe-164">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-164">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6d8fe-165">Nº de Coleções Geração 1</span><span class="sxs-lookup"><span data-stu-id="6d8fe-165"># Gen 1 Collections</span></span> |
| <span data-ttu-id="6d8fe-166">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-166">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6d8fe-167">Nº de Coleções Geração 2</span><span class="sxs-lookup"><span data-stu-id="6d8fe-167"># Gen 2 Collections</span></span> |
| <span data-ttu-id="6d8fe-168">Memória CLR .NET (por serviço)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-168">.NET CLR Memory (per service)</span></span> | <span data-ttu-id="6d8fe-169">% de Tempo na GC</span><span class="sxs-lookup"><span data-stu-id="6d8fe-169">% Time in GC</span></span> |

### <a name="service-fabrics-custom-performance-counters"></a><span data-ttu-id="6d8fe-170">Contadores de desempenho personalizados do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6d8fe-170">Service Fabric's custom performance counters</span></span>

<span data-ttu-id="6d8fe-171">O Service Fabric gera uma quantidade significativa de contadores de desempenho personalizados.</span><span class="sxs-lookup"><span data-stu-id="6d8fe-171">Service Fabric generates a substantial amount of custom performance counters.</span></span> <span data-ttu-id="6d8fe-172">Se o SDK estiver instalado, você poderá ver a lista abrangente em seu computador com Windows em seu aplicativo de Monitor de Desempenho (Iniciar > Monitor de Desempenho).</span><span class="sxs-lookup"><span data-stu-id="6d8fe-172">If you have the SDK installed, you can see the comprehensive list on your Windows machine in your Performance Monitor application (Start > Performance Monitor).</span></span> 

<span data-ttu-id="6d8fe-173">Nos aplicativos que você está implantando em seu cluster, se você estiver usando Reliable Actors, adicione contadores das categorias `Service Fabric Actor` e `Service Fabric Actor Method` (consulte [Diagnósticos de Reliable Actors do Service Fabric](service-fabric-reliable-actors-diagnostics.md)).</span><span class="sxs-lookup"><span data-stu-id="6d8fe-173">In the applications you are deploying to your cluster, if you are using Reliable Actors, add countes from `Service Fabric Actor` and `Service Fabric Actor Method` categories (see [Service Fabric Reliable Actors Diagnostics](service-fabric-reliable-actors-diagnostics.md)).</span></span>

<span data-ttu-id="6d8fe-174">Se você usar os Reliable Services, teremos as categorias de contadores `Service Fabric Service` e `Service Fabric Service Method` das quais você deverá coletar contadores.</span><span class="sxs-lookup"><span data-stu-id="6d8fe-174">If you use Reliable Services, we similarly have `Service Fabric Service` and `Service Fabric Service Method` counter categories that you should collect counters from.</span></span> 

<span data-ttu-id="6d8fe-175">Se você usar Coleções Confiáveis, recomendamos adicionar o `Avg. Transaction ms/Commit` do `Service Fabric Transactional Replicator` para coletar a latência média de confirmação por métrica da transação.</span><span class="sxs-lookup"><span data-stu-id="6d8fe-175">If you use Reliable Collections, we recommend adding the `Avg. Transaction ms/Commit` from the `Service Fabric Transactional Replicator` to collect the average commit latency per transaction metric.</span></span>


## <a name="next-steps"></a><span data-ttu-id="6d8fe-176">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6d8fe-176">Next steps</span></span>

* <span data-ttu-id="6d8fe-177">Saiba mais sobre a [geração de eventos no nível de plataforma](service-fabric-diagnostics-event-generation-infra.md) do Service Fabric</span><span class="sxs-lookup"><span data-stu-id="6d8fe-177">Learn more about [event generation at the platform level](service-fabric-diagnostics-event-generation-infra.md) in Service Fabric</span></span>
* <span data-ttu-id="6d8fe-178">Coletar métricas de desempenho por meio dos [Diagnóstico do Azure](service-fabric-diagnostics-event-aggregation-wad.md)</span><span class="sxs-lookup"><span data-stu-id="6d8fe-178">Collect performance metrics through [Azure Diagnostics](service-fabric-diagnostics-event-aggregation-wad.md)</span></span>
