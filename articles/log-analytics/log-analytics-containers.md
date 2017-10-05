---
title: "Solução de Monitoramento de contêiner no Azure Log Analytics | Microsoft Docs"
description: "A solução de Monitoramento de contêiner no Log Analytics ajuda a exibir e gerenciar os hosts de contêiner do Docker e do Windows em um único local."
services: log-analytics
documentationcenter: 
author: bandersmsft
manager: carmonm
editor: 
ms.assetid: e1e4b52b-92d5-4bfa-8a09-ff8c6b5a9f78
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/18/2017
ms.author: magoedte;banders
ms.openlocfilehash: b2e03531ee401f4552198e5dd50fbfe1d970f0e5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="4da72-103">Solução de Monitoramento de contêiner no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4da72-103">Container Monitoring solution in Log Analytics</span></span>

![Símbolo dos Contêineres](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="4da72-105">Este artigo descreve como configurar e usar a solução de Monitoramento de contêiner no Log Analytics, que ajuda você a exibir e gerenciar os hosts de contêiner do Docker e do Windows em uma única localização.</span><span class="sxs-lookup"><span data-stu-id="4da72-105">This article describes how to set up and use the Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="4da72-106">O Docker é um sistema de virtualização de software usado para criar contêineres que automatizam a implantação de software para infraestrutura de TI.</span><span class="sxs-lookup"><span data-stu-id="4da72-106">Docker is a software virtualization system used to create containers that automate software deployment to their IT infrastructure.</span></span>

<span data-ttu-id="4da72-107">A solução mostra quais contêineres estão em execução, qual imagem de contêiner eles estão executando e onde os contêineres estão em execução.</span><span class="sxs-lookup"><span data-stu-id="4da72-107">The solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="4da72-108">Você pode exibir informações detalhadas de auditoria, mostrando os comandos usados com contêineres.</span><span class="sxs-lookup"><span data-stu-id="4da72-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="4da72-109">E você pode solucionar os problemas de contêineres exibindo e pesquisando logs centralizados sem precisar exibir remotamente os hosts do Docker ou do Windows.</span><span class="sxs-lookup"><span data-stu-id="4da72-109">And, you can troubleshoot containers by viewing and searching centralized logs without having to remotely view Docker or Windows hosts.</span></span> <span data-ttu-id="4da72-110">Você pode encontrar contêineres que podem estar com ruídos e consumindo recursos em excesso em um host.</span><span class="sxs-lookup"><span data-stu-id="4da72-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="4da72-111">E você pode exibir o uso de CPU, memória, armazenamento e rede e informações de desempenho centralizadas para contêineres.</span><span class="sxs-lookup"><span data-stu-id="4da72-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="4da72-112">Nos computadores que executam o Windows, você pode centralizar e comparar os logs do Windows Server, do Hyper-V e dos contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="4da72-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="4da72-113">A solução oferece suporte aos orquestradores de contêiner a seguir:</span><span class="sxs-lookup"><span data-stu-id="4da72-113">The solution supports the following container orchestrators:</span></span>

- <span data-ttu-id="4da72-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="4da72-114">Docker Swarm</span></span>
- <span data-ttu-id="4da72-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="4da72-115">DC/OS</span></span>
- <span data-ttu-id="4da72-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="4da72-116">Kubernetes</span></span>
- <span data-ttu-id="4da72-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="4da72-117">Service Fabric</span></span>
- <span data-ttu-id="4da72-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="4da72-118">Red Hat OpenShift</span></span>


<span data-ttu-id="4da72-119">O diagrama a seguir mostra as relações entre os vários hosts e agentes de contêiner com o OMS.</span><span class="sxs-lookup"><span data-stu-id="4da72-119">The following diagram shows the relationships between various container hosts and agents with OMS.</span></span>

![Diagrama de contêineres](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="4da72-121">Requisitos do sistema</span><span class="sxs-lookup"><span data-stu-id="4da72-121">System requirements</span></span>

<span data-ttu-id="4da72-122">Antes de começar, examine os detalhes a seguir para verificar se você atende aos pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="4da72-122">Before starting, review the following details to verify you meet the prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="4da72-123">Suporte de solução de monitoramento de contêiner para Docker Orchestrator e plataforma do SO</span><span class="sxs-lookup"><span data-stu-id="4da72-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="4da72-124">A tabela a seguir descreve a orquestração do Docker e o suporte de monitoramento do sistema operacional do inventário de contêiner, desempenho e registros com o Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4da72-124">The following table outlines the Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="4da72-125">ACS</span><span class="sxs-lookup"><span data-stu-id="4da72-125">ACS</span></span> | <span data-ttu-id="4da72-126">Linux</span><span class="sxs-lookup"><span data-stu-id="4da72-126">Linux</span></span> | <span data-ttu-id="4da72-127">Windows</span><span class="sxs-lookup"><span data-stu-id="4da72-127">Windows</span></span> | <span data-ttu-id="4da72-128">Contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-128">Container</span></span><br><span data-ttu-id="4da72-129">Inventário</span><span class="sxs-lookup"><span data-stu-id="4da72-129">Inventory</span></span> | <span data-ttu-id="4da72-130">Imagem</span><span class="sxs-lookup"><span data-stu-id="4da72-130">Image</span></span><br><span data-ttu-id="4da72-131">Inventário</span><span class="sxs-lookup"><span data-stu-id="4da72-131">Inventory</span></span> | <span data-ttu-id="4da72-132">Nó</span><span class="sxs-lookup"><span data-stu-id="4da72-132">Node</span></span><br><span data-ttu-id="4da72-133">Inventário</span><span class="sxs-lookup"><span data-stu-id="4da72-133">Inventory</span></span> | <span data-ttu-id="4da72-134">Contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-134">Container</span></span><br><span data-ttu-id="4da72-135">Desempenho</span><span class="sxs-lookup"><span data-stu-id="4da72-135">Performance</span></span> | <span data-ttu-id="4da72-136">Contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-136">Container</span></span><br><span data-ttu-id="4da72-137">Evento</span><span class="sxs-lookup"><span data-stu-id="4da72-137">Event</span></span> | <span data-ttu-id="4da72-138">Evento</span><span class="sxs-lookup"><span data-stu-id="4da72-138">Event</span></span><br><span data-ttu-id="4da72-139">Registro</span><span class="sxs-lookup"><span data-stu-id="4da72-139">Log</span></span> | <span data-ttu-id="4da72-140">Contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-140">Container</span></span><br><span data-ttu-id="4da72-141">Registro</span><span class="sxs-lookup"><span data-stu-id="4da72-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="4da72-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="4da72-142">Kubernetes</span></span> | <span data-ttu-id="4da72-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-143">&#8226;</span></span> | <span data-ttu-id="4da72-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-144">&#8226;</span></span> | | <span data-ttu-id="4da72-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-145">&#8226;</span></span> | <span data-ttu-id="4da72-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-146">&#8226;</span></span> | <span data-ttu-id="4da72-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-147">&#8226;</span></span> | <span data-ttu-id="4da72-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-148">&#8226;</span></span> | <span data-ttu-id="4da72-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-149">&#8226;</span></span> | <span data-ttu-id="4da72-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-150">&#8226;</span></span> | <span data-ttu-id="4da72-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-151">&#8226;</span></span> |
| <span data-ttu-id="4da72-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="4da72-152">Mesosphere</span></span><br><span data-ttu-id="4da72-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="4da72-153">DC/OS</span></span> | <span data-ttu-id="4da72-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-154">&#8226;</span></span> | <span data-ttu-id="4da72-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-155">&#8226;</span></span> | | <span data-ttu-id="4da72-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-156">&#8226;</span></span> | <span data-ttu-id="4da72-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-157">&#8226;</span></span> | <span data-ttu-id="4da72-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-158">&#8226;</span></span> | <span data-ttu-id="4da72-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-159">&#8226;</span></span>| <span data-ttu-id="4da72-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-160">&#8226;</span></span> | <span data-ttu-id="4da72-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-161">&#8226;</span></span> | <span data-ttu-id="4da72-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-162">&#8226;</span></span> |
| <span data-ttu-id="4da72-163">Docker</span><span class="sxs-lookup"><span data-stu-id="4da72-163">Docker</span></span><br><span data-ttu-id="4da72-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="4da72-164">Swarm</span></span> | <span data-ttu-id="4da72-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-165">&#8226;</span></span> | <span data-ttu-id="4da72-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-166">&#8226;</span></span> | <span data-ttu-id="4da72-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-167">&#8226;</span></span> | <span data-ttu-id="4da72-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-168">&#8226;</span></span> | <span data-ttu-id="4da72-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-169">&#8226;</span></span> | <span data-ttu-id="4da72-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-170">&#8226;</span></span> | <span data-ttu-id="4da72-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-171">&#8226;</span></span> | <span data-ttu-id="4da72-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-172">&#8226;</span></span> | | <span data-ttu-id="4da72-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-173">&#8226;</span></span> |
| <span data-ttu-id="4da72-174">O Barramento de</span><span class="sxs-lookup"><span data-stu-id="4da72-174">Service</span></span><br><span data-ttu-id="4da72-175">Fabric</span><span class="sxs-lookup"><span data-stu-id="4da72-175">Fabric</span></span> | | | <span data-ttu-id="4da72-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-176">&#8226;</span></span> | <span data-ttu-id="4da72-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-177">&#8226;</span></span> | <span data-ttu-id="4da72-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-178">&#8226;</span></span> | <span data-ttu-id="4da72-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-179">&#8226;</span></span> | <span data-ttu-id="4da72-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-180">&#8226;</span></span> | <span data-ttu-id="4da72-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-181">&#8226;</span></span> | <span data-ttu-id="4da72-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-182">&#8226;</span></span> | <span data-ttu-id="4da72-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-183">&#8226;</span></span> |
| <span data-ttu-id="4da72-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="4da72-184">Red Hat Open</span></span><br><span data-ttu-id="4da72-185">Shift</span><span class="sxs-lookup"><span data-stu-id="4da72-185">Shift</span></span> | | <span data-ttu-id="4da72-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-186">&#8226;</span></span> | | <span data-ttu-id="4da72-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-187">&#8226;</span></span> | <span data-ttu-id="4da72-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-188">&#8226;</span></span>| <span data-ttu-id="4da72-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-189">&#8226;</span></span> | <span data-ttu-id="4da72-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-190">&#8226;</span></span> | <span data-ttu-id="4da72-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-191">&#8226;</span></span> | | <span data-ttu-id="4da72-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-192">&#8226;</span></span> |
| <span data-ttu-id="4da72-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="4da72-193">Windows Server</span></span><br><span data-ttu-id="4da72-194">(autônomo)</span><span class="sxs-lookup"><span data-stu-id="4da72-194">(standalone)</span></span> | | | <span data-ttu-id="4da72-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-195">&#8226;</span></span> | <span data-ttu-id="4da72-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-196">&#8226;</span></span> | <span data-ttu-id="4da72-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-197">&#8226;</span></span> | <span data-ttu-id="4da72-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-198">&#8226;</span></span> | <span data-ttu-id="4da72-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-199">&#8226;</span></span> | <span data-ttu-id="4da72-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-200">&#8226;</span></span> | | <span data-ttu-id="4da72-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-201">&#8226;</span></span> |
| <span data-ttu-id="4da72-202">Linux Server</span><span class="sxs-lookup"><span data-stu-id="4da72-202">Linux Server</span></span><br><span data-ttu-id="4da72-203">(autônomo)</span><span class="sxs-lookup"><span data-stu-id="4da72-203">(standalone)</span></span> | | <span data-ttu-id="4da72-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-204">&#8226;</span></span> | | <span data-ttu-id="4da72-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-205">&#8226;</span></span> | <span data-ttu-id="4da72-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-206">&#8226;</span></span> | <span data-ttu-id="4da72-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-207">&#8226;</span></span> | <span data-ttu-id="4da72-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-208">&#8226;</span></span> | <span data-ttu-id="4da72-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-209">&#8226;</span></span> | | <span data-ttu-id="4da72-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="4da72-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="4da72-211">Versões do Docker com suporte no Linux</span><span class="sxs-lookup"><span data-stu-id="4da72-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="4da72-212">Docker 1.11 a 1.13</span><span class="sxs-lookup"><span data-stu-id="4da72-212">Docker 1.11 to 1.13</span></span>
- <span data-ttu-id="4da72-213">Docker CE e EE v17.06</span><span class="sxs-lookup"><span data-stu-id="4da72-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="4da72-214">As distribuições de Linux x64 têm suporte como hosts de contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="4da72-215">Ubuntu 14.04 LTS e 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="4da72-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="4da72-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="4da72-216">CoreOS(stable)</span></span>
- <span data-ttu-id="4da72-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="4da72-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="4da72-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="4da72-218">openSUSE 13.2</span></span>
- <span data-ttu-id="4da72-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="4da72-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="4da72-220">CentOS 7.2 e 7.3</span><span class="sxs-lookup"><span data-stu-id="4da72-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="4da72-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="4da72-221">SLES 12</span></span>
- <span data-ttu-id="4da72-222">RHEL 7.2 e 7.3</span><span class="sxs-lookup"><span data-stu-id="4da72-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="4da72-223">Red Hat OpenShift Container Platform (OCP) 3.4 e 3.5</span><span class="sxs-lookup"><span data-stu-id="4da72-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="4da72-224">ACS Mesosphere DC/OS 1.7.3 a 1.8.8</span><span class="sxs-lookup"><span data-stu-id="4da72-224">ACS Mesosphere DC/OS 1.7.3 to 1.8.8</span></span>
- <span data-ttu-id="4da72-225">ACS Kubernetes 1.4.5 a 1.6</span><span class="sxs-lookup"><span data-stu-id="4da72-225">ACS Kubernetes 1.4.5 to 1.6</span></span>
- <span data-ttu-id="4da72-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="4da72-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="4da72-227">Sistema operacional Windows com suporte</span><span class="sxs-lookup"><span data-stu-id="4da72-227">Supported Windows operating system</span></span>

- <span data-ttu-id="4da72-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="4da72-228">Windows Server 2016</span></span>
- <span data-ttu-id="4da72-229">Edição de aniversário do Windows 10 (Professional ou Enterprise)</span><span class="sxs-lookup"><span data-stu-id="4da72-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="4da72-230">Versões do Docker do Windows com suporte</span><span class="sxs-lookup"><span data-stu-id="4da72-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="4da72-231">Docker 1.12 e 1.13</span><span class="sxs-lookup"><span data-stu-id="4da72-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="4da72-232">Docker 17.03.0 e mais recente</span><span class="sxs-lookup"><span data-stu-id="4da72-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-the-solution"></a><span data-ttu-id="4da72-233">Instalando e configurando a solução</span><span class="sxs-lookup"><span data-stu-id="4da72-233">Installing and configuring the solution</span></span>
<span data-ttu-id="4da72-234">Use as informações a seguir para instalar e configurar a solução.</span><span class="sxs-lookup"><span data-stu-id="4da72-234">Use the following information to install and configure the solution.</span></span>

1. <span data-ttu-id="4da72-235">Adicione a solução de Monitoramento de contêiner ao seu espaço de trabalho do OMS do [marketplace do Azure](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) ou usando o processo descrito em [Adicionar soluções do Log Analytics por meio da Galeria de Soluções](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-235">Add the Container Monitoring solution to your OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using the process described in [Add Log Analytics solutions from the Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="4da72-236">Instale e use o Docker com um agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="4da72-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="4da72-237">Com base em seu sistema operacional, você pode escolher entre os seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="4da72-237">Based on your operating system, you can choose from the following methods:</span></span>

  * <span data-ttu-id="4da72-238">Em sistemas operacionais Linux com suporte, instale e execute o Docker e, em seguida, instale e configure o [Agente do OMS para Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-238">On supported Linux operating systems, install and run Docker and then install and configure the [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="4da72-239">No CoreOS, você não pode executar o Agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="4da72-239">On CoreOS, you cannot run the OMS Agent for Linux.</span></span> <span data-ttu-id="4da72-240">Em vez disso, você deve executar uma versão em contêiner do Agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="4da72-240">Instead, you run a containerized version of the OMS Agent for Linux.</span></span> <span data-ttu-id="4da72-241">Confira [Hosts de contêiner do Linux incluindo CoreOS](#for-all-linux-container-hosts-including-coreos) ou [Hosts de contêiner do Linux do Azure Governamental incluindo CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) se você estiver trabalhando com contêineres na nuvem do Azure Governamental.</span><span class="sxs-lookup"><span data-stu-id="4da72-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="4da72-242">No Windows Server 2016 e no Windows 10, instale o Mecanismo do Docker e, então, o cliente se conectará a um agente para coletar informações e enviá-las para o Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4da72-242">On Windows Server 2016 and Windows 10, install the Docker Engine and client then connect an agent to gather information and send it to Log Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="4da72-243">Serviços de Contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-243">Container services</span></span>

- <span data-ttu-id="4da72-244">Se você tiver um ambiente do Red Hat OpenShift, confira [Configurar um agente do OMS para Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="4da72-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="4da72-245">Se você tiver um cluster Kubernetes usando o Serviço de Contêiner do Azure, confira [Monitorar um cluster do Serviço de Contêiner do Azure com o Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-245">If you have a Kubernetes cluster using the Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="4da72-246">Se você tiver um cluster de DC/SO do Serviço de Contêiner do Azure, saiba mais em [Monitorar um cluster DC/OS do Serviço de Contêiner do Azure com o Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="4da72-247">Se você tiver um ambiente no modo Docker Swarm, saiba mais em [Configurar um agente do OMS para o Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="4da72-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="4da72-248">Se você usa contêineres com o Service Fabric, saiba mais em [Visão geral do Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="4da72-249">Examine o artigo [Mecanismo do Docker no Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) para obter informações adicionais sobre como instalar e configurar seus Mecanismos do Docker em computadores que executam o Windows.</span><span class="sxs-lookup"><span data-stu-id="4da72-249">Review the [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how to install and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4da72-250">O Docker deve estar em execução **antes** de instalar o [Agente do OMS para Linux](log-analytics-agent-linux.md) em seus hosts de contêiner.</span><span class="sxs-lookup"><span data-stu-id="4da72-250">Docker must be running **before** you install the [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="4da72-251">Se você já tiver instalado o agente antes de instalar o Docker, precisará reinstalar o Agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="4da72-251">If you've already installed the agent before installing Docker, you need to reinstall the OMS Agent for Linux.</span></span> <span data-ttu-id="4da72-252">Para obter mais informações sobre o Docker, consulte o [site do Docker](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="4da72-252">For more information about Docker, see the [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="4da72-253">Hosts de contêiner do Linux</span><span class="sxs-lookup"><span data-stu-id="4da72-253">Linux container hosts</span></span>

<span data-ttu-id="4da72-254">Depois de instalar o Docker, use as seguintes definições para o host do contêiner para configurar o agente para uso com o Docker.</span><span class="sxs-lookup"><span data-stu-id="4da72-254">After you've installed Docker, use the following settings for your container host to configure the agent for use with Docker.</span></span> <span data-ttu-id="4da72-255">Primeiro, você precisa da ID e chave de seu espaço de trabalho do OMS, que podem ser encontradas no Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="4da72-255">First you need your OMS workspace ID and key, which you can find in the Azure portal.</span></span> <span data-ttu-id="4da72-256">Em seu espaço de trabalho, clique em **Início Rápido** > **Computadores** para exibir sua **ID de Espaço de Trabalho** e **Chave Primária**.</span><span class="sxs-lookup"><span data-stu-id="4da72-256">In your workspace, click **Quick Start** > **Computers** to view your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="4da72-257">Copie e cole os dois em seu editor favorito.</span><span class="sxs-lookup"><span data-stu-id="4da72-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="4da72-258">Para todos os hosts de contêiner do Linux, exceto CoreOS</span><span class="sxs-lookup"><span data-stu-id="4da72-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="4da72-259">Para obter mais informações e etapas sobre como instalar o Agente do OMS para Linux, confira [Conectar computadores Linux ao OMS (Operations Management Suite)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-259">For more information and steps on how to install the OMS Agent for Linux, see [Connect your Linux Computers to Operations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="4da72-260">Para todos os hosts de contêiner do Linux, incluindo o CoreOS</span><span class="sxs-lookup"><span data-stu-id="4da72-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="4da72-261">Inicie o contêiner do OMS que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="4da72-261">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="4da72-262">Modifique e use o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4da72-262">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="4da72-263">Para todos os hosts de contêiner do Linux no Azure Governamental, incluindo CoreOS</span><span class="sxs-lookup"><span data-stu-id="4da72-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="4da72-264">Inicie o contêiner do OMS que você deseja monitorar.</span><span class="sxs-lookup"><span data-stu-id="4da72-264">Start the OMS container that you want to monitor.</span></span> <span data-ttu-id="4da72-265">Modifique e use o exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="4da72-265">Modify and use the following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-to-one-in-a-container"></a><span data-ttu-id="4da72-266">Alternância de uso de um agente do Linux instalado para outro em um contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-266">Switching from using an installed Linux agent to one in a container</span></span>
<span data-ttu-id="4da72-267">Se anteriormente você utilizou o agente instalado diretamente e, em vez disso, deseja usar um agente em execução em um contêiner, primeiro você deverá remover o Agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="4da72-267">If you previously used the directly-installed agent and want to instead use an agent running in a container, you must first remove the OMS Agent for Linux.</span></span> <span data-ttu-id="4da72-268">Veja [Desinstalar o Agente do OMS para Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) para entender como desinstalar o agente com êxito.</span><span class="sxs-lookup"><span data-stu-id="4da72-268">See [Uninstalling the OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) to understand how to successfully uninstall the agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="4da72-269">Configurar um agente do OMS para o Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="4da72-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="4da72-270">Execute o Agente do OMS como um serviço global no Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="4da72-270">You can run the OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="4da72-271">Use as informações a seguir para criar um serviço do Agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="4da72-271">Use the following information to create an OMS Agent service.</span></span> <span data-ttu-id="4da72-272">Você precisa inserir a ID do Espaço de Trabalho do OMS e a Chave Primária.</span><span class="sxs-lookup"><span data-stu-id="4da72-272">You need to insert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="4da72-273">Execute o seguinte no nó mestre.</span><span class="sxs-lookup"><span data-stu-id="4da72-273">Run the following on the master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="4da72-274">Configurar um Agente do OMS para o Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="4da72-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="4da72-275">Há três maneiras de adicionar o Agente do OMS para Red Hat OpenShift para começar a coletar dados de monitoramento de contêiner.</span><span class="sxs-lookup"><span data-stu-id="4da72-275">There are three ways to add the OMS Agent to Red Hat OpenShift to start collecting container monitoring data.</span></span>

* <span data-ttu-id="4da72-276">[Instalar o Agente do OMS para Linux](log-analytics-agent-linux.md) diretamente em cada nó do OpenShift</span><span class="sxs-lookup"><span data-stu-id="4da72-276">[Install the OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="4da72-277">[Habilitar a extensão de VM do Log Analytics](log-analytics-azure-vm-extension.md) em cada nó do OpenShift que reside no Azure</span><span class="sxs-lookup"><span data-stu-id="4da72-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="4da72-278">Instalar o Agente do OMS como um daemon-set do OpenShift</span><span class="sxs-lookup"><span data-stu-id="4da72-278">Install the OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="4da72-279">Nesta seção, abordaremos as etapas necessárias para instalar o Agente do OMS como um daemon-set do OpenShift.</span><span class="sxs-lookup"><span data-stu-id="4da72-279">In this section we cover the steps required to install the OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="4da72-280">Faça logon no nó principal do OpenShift e copie o arquivo yaml [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) do GitHub para o nó principal e modifique o valor com sua ID de Espaço de Trabalho do OMS e sua Chave Primária.</span><span class="sxs-lookup"><span data-stu-id="4da72-280">Sign on to the OpenShift master node and copy the yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub to your master node and modify the value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="4da72-281">Execute os seguintes comandos para criar um projeto para OMS e definir a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="4da72-281">Run the following commands to create a project for OMS and set the user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="4da72-282">Para implantar o daemon-set, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4da72-282">To deploy the daemon-set, run the following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="4da72-283">Para verificar se ele está configurado e funcionando corretamente, digite o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4da72-283">To verify it is configured and working correctly, type the following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="4da72-284">e o resultado deve ser semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="4da72-284">and the output should resemble:</span></span>

    ```
    [ocpadmin@khm-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

<span data-ttu-id="4da72-285">Se você quiser usar segredos para proteger sua ID de Espaço de Trabalho do OMS e Chave Primária ao usar o arquivo yaml do daemon-set do Agente do OMS, execute as seguintes etapas.</span><span class="sxs-lookup"><span data-stu-id="4da72-285">If you want to use secrets to secure your OMS Workspace ID and Primary Key when using the OMS Agent daemon-set yaml file, perform the following steps.</span></span>

1. <span data-ttu-id="4da72-286">Faça logon no nó principal do OpenShift e copie o arquivo yaml [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) e o script de geração de segredo [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) do GitHub.</span><span class="sxs-lookup"><span data-stu-id="4da72-286">Sign on to the OpenShift master node and copy the yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="4da72-287">Esse script gerará o arquivo yaml de segredos para a ID de Espaço de Trabalho do OMS e a Chave Primária a fim de proteger suas informações secretas.</span><span class="sxs-lookup"><span data-stu-id="4da72-287">This script will generate the secrets yaml file for OMS Workspace ID and Primary Key to secure your secrete information.</span></span>  
2. <span data-ttu-id="4da72-288">Execute os seguintes comandos para criar um projeto para OMS e definir a conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="4da72-288">Run the following commands to create a project for OMS and set the user account.</span></span> <span data-ttu-id="4da72-289">O script de geração de segredo solicita sua ID de Espaço de trabalho do OMS <WSID> e a Chave Primária <KEY> e, após a conclusão, cria o arquivo ocp-secret.yaml.</span><span class="sxs-lookup"><span data-stu-id="4da72-289">The secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates the ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="4da72-290">Implante o arquivo de segredo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4da72-290">Deploy the secret file by running the following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="4da72-291">Verifique a implantação executando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4da72-291">Verify deployment by running the following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="4da72-292">e o resultado deve ser semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="4da72-292">and the  output should resemble:</span></span>  

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe ds oms  
    Name:           oms  
    Image(s):       microsoft/oms  
    Selector:       name=omsagent  
    Node-Selector:  zone=default  
    Labels:         agentVersion=1.4.0-12  
                    dockerProviderVersion=10.0.0-25  
                    name=omsagent  
    Desired Number of Nodes Scheduled: 3  
    Current Number of Nodes Scheduled: 3  
    Number of Nodes Misscheduled: 0  
    Pods Status:    3 Running / 0 Waiting / 0 Succeeded / 0 Failed  
    No events.  
    ```

6. <span data-ttu-id="4da72-293">Implante o arquivo yaml de daemon-set do Agente do OMS executando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4da72-293">Deploy the OMS Agent daemon-set yaml file by running the following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="4da72-294">Verifique a implantação executando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4da72-294">Verify deployment by running the following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="4da72-295">e o resultado deve ser semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="4da72-295">and the output should resemble:</span></span>

    ```
    [ocpadmin@khocp-master-0 ~]$ oc describe secret omsagent-secret  
    Name:           omsagent-secret  
    Namespace:      omslogging  
    Labels:         <none>  
    Annotations:    <none>  

    Type:   Opaque  

     Data  
     ====  
     KEY:    89 bytes  
     WSID:   37 bytes  
    ```

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="4da72-296">Proteger suas informações secretas do Docker Swarm e Kubernetes</span><span class="sxs-lookup"><span data-stu-id="4da72-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="4da72-297">Proteja sua ID do Espaço de Trabalho do OMS e as Chaves Primárias secretas para os serviços de contêiner Docker Swarm e Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4da72-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="4da72-298">Proteger segredos do Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="4da72-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="4da72-299">Para o Docker Swarm, depois que o segredo da ID do Espaço de Trabalho e a Chave Primária for criado, você poderá executar e criar o serviço do Docker para o OMSagent.</span><span class="sxs-lookup"><span data-stu-id="4da72-299">For Docker Swarm, once the secret for Workspace ID and Primary Key is created, you can run the create the Docker service for OMSagent.</span></span> <span data-ttu-id="4da72-300">Use as informações a seguir para criar suas informações secretas.</span><span class="sxs-lookup"><span data-stu-id="4da72-300">Use the following information to create your secret information.</span></span>

1. <span data-ttu-id="4da72-301">Execute o seguinte no nó mestre.</span><span class="sxs-lookup"><span data-stu-id="4da72-301">Run the following on the master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="4da72-302">Verifique se os segredos foram criados corretamente.</span><span class="sxs-lookup"><span data-stu-id="4da72-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="4da72-303">Execute o comando a seguir para montar os segredos no Agente do OMS em contêineres.</span><span class="sxs-lookup"><span data-stu-id="4da72-303">Run the following command to mount the secrets to the containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="4da72-304">Proteger segredos do Kubernetes com arquivos yaml</span><span class="sxs-lookup"><span data-stu-id="4da72-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="4da72-305">Para o Kubernetes, use um script para gerar o arquivo .yaml de segredos para a ID do Espaço de Trabalho e a Chave Primária.</span><span class="sxs-lookup"><span data-stu-id="4da72-305">For Kubernetes, you use a script to generate the secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="4da72-306">Na página [GitHub do OMS Docker Kubernetes](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes), existem arquivos que você pode usar com ou sem as informações secretas.</span><span class="sxs-lookup"><span data-stu-id="4da72-306">At the [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="4da72-307">O DaemonSet do Agente do OMS Padrão que não tem informações secretas (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="4da72-307">The Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="4da72-308">O arquivo yaml do DaemonSet do Agente do OMS que usa informações secretas (omsagent-ds-secrets.yaml) com scripts de geração de segredo que geram o arquivo yaml de segredos (omsagentsecret.yaml).</span><span class="sxs-lookup"><span data-stu-id="4da72-308">The OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts to generate the secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="4da72-309">Você pode optar por criar DaemonSets do omsagent com ou sem segredos.</span><span class="sxs-lookup"><span data-stu-id="4da72-309">You can choose to create omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="4da72-310">Arquivo yaml do DaemonSet do OMSagent Padrão sem segredos</span><span class="sxs-lookup"><span data-stu-id="4da72-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="4da72-311">Para o arquivo yaml do DaemonSet do Agente do OMS padrão, substitua `<WSID>` e `<KEY>` pela WSID e KEY.</span><span class="sxs-lookup"><span data-stu-id="4da72-311">For the default OMS Agent DaemonSet yaml file, replace the `<WSID>` and `<KEY>` to your WSID and KEY.</span></span> <span data-ttu-id="4da72-312">Copie o arquivo para o nó mestre e execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4da72-312">Copy the file to your master node and run the following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="4da72-313">Arquivo yaml do DaemonSet do OMSagent Padrão com segredos</span><span class="sxs-lookup"><span data-stu-id="4da72-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="4da72-314">Para usar o DaemonSet do Agente do OMS usando informações secretas, crie os segredos primeiro.</span><span class="sxs-lookup"><span data-stu-id="4da72-314">To use OMS Agent DaemonSet using secret information, create the secrets first.</span></span>
    1. <span data-ttu-id="4da72-315">Copie o script e o arquivo de modelo de segredo e verifique se eles estão no mesmo diretório.</span><span class="sxs-lookup"><span data-stu-id="4da72-315">Copy the script and secret template file and make sure they are on the same directory.</span></span>
        - <span data-ttu-id="4da72-316">Script de geração de segredo – secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="4da72-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="4da72-317">modelo de segredo – secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="4da72-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="4da72-318">Execute o script, como no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="4da72-318">Run the script, like the following example.</span></span> <span data-ttu-id="4da72-319">O script solicitará a ID do Espaço de Trabalho do OMS e a Chave Primária e, depois que você inseri-los, o script criará um arquivo .yaml secreto para que você possa executá-lo.</span><span class="sxs-lookup"><span data-stu-id="4da72-319">The script asks for the OMS Workspace ID and Primary Key and after you enter them, the script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="4da72-320">Crie o pod de segredos executando o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4da72-320">Create the secrets pod by running the following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="4da72-321">Para verificar, execute o seguinte:</span><span class="sxs-lookup"><span data-stu-id="4da72-321">To verify, run the following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="4da72-322">O resultado deve ser semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="4da72-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="4da72-323">O resultado deve ser semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="4da72-323">Output should resemble:</span></span>

        ```
        Name:           omsagent-secret
        Namespace:      default
        Labels:         <none>
        Annotations:    <none>

        Type:   Opaque

        Data
        ====
        WSID:   36 bytes
        KEY:    88 bytes
        ```

    5. <span data-ttu-id="4da72-324">Criar o omsagent daemon-set executando ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="4da72-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="4da72-325">Verifique se o DaemonSet do Agente do OMS está em execução, de forma semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="4da72-325">Verify that the OMS Agent DaemonSet is running, similar to the following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="4da72-326">Para o Kubernetes, use um script para gerar o arquivo yaml de segredos para a ID do Espaço de Trabalho e a Chave Primária.</span><span class="sxs-lookup"><span data-stu-id="4da72-326">For Kubernetes, use a script to generate the secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="4da72-327">Use as informações de exemplo a seguir com o [arquivo yaml do omsagent](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) para proteger suas informações secretas.</span><span class="sxs-lookup"><span data-stu-id="4da72-327">Use the following example information with the [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) to secure your secret information.</span></span>

```
keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
Name:           omsagent-secret
Namespace:      default
Labels:         <none>
Annotations:    <none>

Type:   Opaque

Data
====
WSID:   36 bytes
KEY:    88 bytes
```

## <a name="windows-container-hosts"></a><span data-ttu-id="4da72-328">Hosts de contêiner do Windows</span><span class="sxs-lookup"><span data-stu-id="4da72-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="4da72-329">Preparação antes de instalar os agentes do Windows</span><span class="sxs-lookup"><span data-stu-id="4da72-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="4da72-330">Antes de instalar os agentes em computadores que executam o Windows, você precisa configurar o serviço Docker.</span><span class="sxs-lookup"><span data-stu-id="4da72-330">Before you install agents on computers running Windows, you need to configure the Docker service.</span></span> <span data-ttu-id="4da72-331">A configuração permite que o agente do Windows ou a extensão da máquina virtual do Log Analytics use o soquete Docker TCP para que os agentes possam acessar o daemon do Docker remotamente e capturar os dados de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="4da72-331">The configuration allows the Windows agent or the Log Analytics virtual machine extension to use the Docker TCP socket so that the agents can access the Docker daemon remotely and to capture data for monitoring.</span></span>

#### <a name="to-start-docker-and-verify-its-configuration"></a><span data-ttu-id="4da72-332">Iniciar o Docker e verificar sua configuração</span><span class="sxs-lookup"><span data-stu-id="4da72-332">To start Docker and verify its configuration</span></span>

<span data-ttu-id="4da72-333">Há etapas necessárias para configurar o pipe nomeado por TCP para o Windows Server:</span><span class="sxs-lookup"><span data-stu-id="4da72-333">There are steps needed to set up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="4da72-334">No Windows PowerShell, habilite o pipe TCP e o pipe nomeado.</span><span class="sxs-lookup"><span data-stu-id="4da72-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="4da72-335">Configure o Docker com o arquivo de configuração para o pipe TCP e o pipe nomeado.</span><span class="sxs-lookup"><span data-stu-id="4da72-335">Configure Docker with the configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="4da72-336">O arquivo de configuração está localizado em C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="4da72-336">The configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="4da72-337">No arquivo daemon.json, você precisará do seguinte:</span><span class="sxs-lookup"><span data-stu-id="4da72-337">In the daemon.json file, you will need the following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="4da72-338">Para obter mais informações sobre a configuração do daemon do Docker usada com os Contêineres do Windows, consulte [Mecanismo do Docker no Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="4da72-338">For more information about the Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="4da72-339">Instalar agentes do Windows</span><span class="sxs-lookup"><span data-stu-id="4da72-339">Install Windows agents</span></span>

<span data-ttu-id="4da72-340">Para habilitar o monitoramento do contêiner do Windows e do Hyper-V, instale o MMA (Microsoft Monitoring Agent) em computadores com Windows que sejam hosts do contêiner.</span><span class="sxs-lookup"><span data-stu-id="4da72-340">To enable Windows and Hyper-V container monitoring, install the Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="4da72-341">Para computadores que executam o Windows no seu ambiente local, consulte [Conectar computadores Windows ao Log Analytics](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-341">For computers running Windows in your on-premises environment, see [Connect Windows computers to Log Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="4da72-342">Para máquinas virtuais em execução no Azure, conecte-as ao Log Analytics usando a [extensão da máquina virtual](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-342">For virtual machines running in Azure, connect them to Log Analytics using the [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="4da72-343">Você pode monitorar os contêineres do Windows em execução no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4da72-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="4da72-344">No entanto, apenas [máquinas virtuais em execução no Azure](log-analytics-azure-vm-extension.md) e [computadores executando o Windows no seu ambiente local](log-analytics-windows-agents.md) têm suporte atualmente para o Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="4da72-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="4da72-345">Você pode verificar se a solução de Monitoramento de contêiner está definida corretamente para o Windows.</span><span class="sxs-lookup"><span data-stu-id="4da72-345">You can verify that the Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="4da72-346">Para verificar se o pacote de gerenciamento foi baixado corretamente, procure *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="4da72-346">To check whether the management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="4da72-347">Os arquivos devem estar na pasta C:\Arquivos de Programas\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs.</span><span class="sxs-lookup"><span data-stu-id="4da72-347">The files should be in the C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="4da72-348">Componentes da solução</span><span class="sxs-lookup"><span data-stu-id="4da72-348">Solution components</span></span>

<span data-ttu-id="4da72-349">Se você estiver usando agentes do Windows, o pacote de gerenciamento a seguir será instalado em cada computador que possui um agente quando você adicionar essa solução.</span><span class="sxs-lookup"><span data-stu-id="4da72-349">If you are using Windows agents, then the following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="4da72-350">Não é necessária nenhuma configuração nem manutenção do pacote de gerenciamento.</span><span class="sxs-lookup"><span data-stu-id="4da72-350">No configuration or maintenance is required for the management pack.</span></span>

- <span data-ttu-id="4da72-351">*ContainerManagement.xxx* instalado em C:\Arquivos de Programas\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span><span class="sxs-lookup"><span data-stu-id="4da72-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="4da72-352">Detalhes da coleta de dados dos contêineres</span><span class="sxs-lookup"><span data-stu-id="4da72-352">Container data collection details</span></span>
<span data-ttu-id="4da72-353">A solução de Monitoramento de contêineres coleta vários dados de log e métricas de desempenho dos hosts de contêiner e dos contêineres que usam os agentes que você habilitou.</span><span class="sxs-lookup"><span data-stu-id="4da72-353">The Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="4da72-354">Os dados são coletados a cada três minutos pelos tipos de agente a seguir.</span><span class="sxs-lookup"><span data-stu-id="4da72-354">Data is collected every three minutes by the following agent types.</span></span>

- [<span data-ttu-id="4da72-355">Agente do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="4da72-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="4da72-356">Agente do Windows</span><span class="sxs-lookup"><span data-stu-id="4da72-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="4da72-357">Extensão de VM do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="4da72-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="4da72-358">Registros de contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-358">Container records</span></span>

<span data-ttu-id="4da72-359">A tabela a seguir mostra exemplos de registros coletados pela solução de Monitoramento de contêineres e os tipos de dados que aparecem nos resultados da pesquisa de log.</span><span class="sxs-lookup"><span data-stu-id="4da72-359">The following table shows examples of records collected by the Container Monitoring solution and the data types that appear in log search results.</span></span>

| <span data-ttu-id="4da72-360">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="4da72-360">Data type</span></span> | <span data-ttu-id="4da72-361">Tipo de dados na Pesquisa de Log</span><span class="sxs-lookup"><span data-stu-id="4da72-361">Data type in Log Search</span></span> | <span data-ttu-id="4da72-362">Campos</span><span class="sxs-lookup"><span data-stu-id="4da72-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="4da72-363">Desempenho de hosts e contêineres</span><span class="sxs-lookup"><span data-stu-id="4da72-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="4da72-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="4da72-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="4da72-365">Inventário de contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="4da72-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="4da72-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="4da72-367">Inventário de imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="4da72-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="4da72-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="4da72-369">Log do contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="4da72-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="4da72-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="4da72-371">Log do serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="4da72-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="4da72-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="4da72-373">Inventário de nós do contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="4da72-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="4da72-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="4da72-375">Inventário de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="4da72-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="4da72-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="4da72-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="4da72-377">Processo do contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="4da72-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="4da72-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="4da72-379">Eventos de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="4da72-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="4da72-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span><span class="sxs-lookup"><span data-stu-id="4da72-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="4da72-381">Os rótulos anexado aos tipos de dados *PodLabel* são seus próprios rótulos personalizados.</span><span class="sxs-lookup"><span data-stu-id="4da72-381">Labels appended to *PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="4da72-382">Os rótulos PodLabel anexados mostrados na tabela são exemplos.</span><span class="sxs-lookup"><span data-stu-id="4da72-382">The appended PodLabel labels shown in the table are examples.</span></span> <span data-ttu-id="4da72-383">Portanto, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` serão diferentes no conjunto de dados de seu ambiente, e genericamente lembram `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="4da72-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="4da72-384">Monitorar contêineres</span><span class="sxs-lookup"><span data-stu-id="4da72-384">Monitor containers</span></span>
<span data-ttu-id="4da72-385">Depois de habilitar a solução no portal do OMS, o bloco **Contêineres** mostrará informações resumidas sobre seus hosts de contêiner e os contêineres em execução nos hosts.</span><span class="sxs-lookup"><span data-stu-id="4da72-385">After you have the solution enabled in the OMS portal, the **Containers** tile shows summary information about your container hosts and the containers running in hosts.</span></span>

![Bloco Contêineres](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="4da72-387">O bloco mostra uma visão geral de quantos contêineres existem no ambiente e se eles estão com falha, em execução ou parados.</span><span class="sxs-lookup"><span data-stu-id="4da72-387">The tile shows an overview of how many containers you have in the environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-the-containers-dashboard"></a><span data-ttu-id="4da72-388">Usando o painel de Contêineres</span><span class="sxs-lookup"><span data-stu-id="4da72-388">Using the Containers dashboard</span></span>
<span data-ttu-id="4da72-389">Clique no bloco **Contêineres**.</span><span class="sxs-lookup"><span data-stu-id="4da72-389">Click the **Containers** tile.</span></span> <span data-ttu-id="4da72-390">A partir daí, você verá exibições organizadas por:</span><span class="sxs-lookup"><span data-stu-id="4da72-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="4da72-391">**Eventos de Contêiner** - Mostra o status do contêiner, e os computadores com contêineres com falha.</span><span class="sxs-lookup"><span data-stu-id="4da72-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="4da72-392">**Logs do Contêiner** - Mostra um gráfico de arquivos de log gerados com o tempo, e uma lista de computadores com o maior número de arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="4da72-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with the highest number of log files.</span></span>
- <span data-ttu-id="4da72-393">**Eventos de Kubernetes** - Mostra um gráfico de eventos de Kubernetes gerados com o tempo, e uma lista com os motivos de os compartimentos terem gerado os eventos.</span><span class="sxs-lookup"><span data-stu-id="4da72-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of the reasons why pods generated the events.</span></span> <span data-ttu-id="4da72-394">*Esse conjunto de dados é usado somente em ambientes Linux.*</span><span class="sxs-lookup"><span data-stu-id="4da72-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="4da72-395">**Inventário de Namespace de Kubernetes** - Mostra o número de namespaces e compartimentos, e a hierarquia deles.</span><span class="sxs-lookup"><span data-stu-id="4da72-395">**Kubernetes Namespace Inventory** - Shows the number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="4da72-396">*Esse conjunto de dados é usado somente em ambientes Linux.*</span><span class="sxs-lookup"><span data-stu-id="4da72-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="4da72-397">**Inventário de Nó do Contêiner** - Mostra o número de tipos de orquestração usados em nós/hosts do contêiner.</span><span class="sxs-lookup"><span data-stu-id="4da72-397">**Container Node Inventory** - Shows the number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="4da72-398">Os nós/hosts do computador também são listados pelo número de contêineres.</span><span class="sxs-lookup"><span data-stu-id="4da72-398">The computer nodes/hosts are also listed by the number of containers.</span></span> <span data-ttu-id="4da72-399">*Esse conjunto de dados é usado somente em ambientes Linux.*</span><span class="sxs-lookup"><span data-stu-id="4da72-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="4da72-400">**Inventário de Imagens de Contêiner** - Mostra o número total de imagens de contêiner usadas, e o número de tipos de imagem.</span><span class="sxs-lookup"><span data-stu-id="4da72-400">**Container Images Inventory** - Shows the total number of container images used and number of image types.</span></span> <span data-ttu-id="4da72-401">O número de imagens também é listado por marca de imagem.</span><span class="sxs-lookup"><span data-stu-id="4da72-401">The number of images are also listed by the image tag.</span></span>
- <span data-ttu-id="4da72-402">**Status dos Contêineres** - Mostra o número total de computadores host/nós de contêiner com contêineres em execução.</span><span class="sxs-lookup"><span data-stu-id="4da72-402">**Containers Status** - Shows the total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="4da72-403">Os computadores também são listados pelo número de hosts em execução.</span><span class="sxs-lookup"><span data-stu-id="4da72-403">Computers are also listed by the number of running hosts.</span></span>
- <span data-ttu-id="4da72-404">**Processo do Contêiner** - Mostra um gráfico de linhas dos processos de contêiner em execução ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="4da72-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="4da72-405">Os contêineres também são listados por meio da execução do comando/processo dentro dos contêineres.</span><span class="sxs-lookup"><span data-stu-id="4da72-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="4da72-406">*Esse conjunto de dados é usado somente em ambientes Linux.*</span><span class="sxs-lookup"><span data-stu-id="4da72-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="4da72-407">**Desempenho da CPU do Contêiner** - Mostra um gráfico de linhas da utilização média da CPU ao longo do tempo para nós/hosts do computador.</span><span class="sxs-lookup"><span data-stu-id="4da72-407">**Container CPU Performance** - Shows a line chart of the average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="4da72-408">Também lista os nós/hosts do computador com base na utilização média da CPU.</span><span class="sxs-lookup"><span data-stu-id="4da72-408">Also lists the computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="4da72-409">**Desempenho de Memória de Contêiner** - Mostra um gráfico de linhas do uso da memória ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="4da72-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="4da72-410">Também lista a utilização da memória do computador com base no nome da instância.</span><span class="sxs-lookup"><span data-stu-id="4da72-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="4da72-411">**Desempenho do Computador** - Mostra os gráficos de linha do percentual de desempenho da CPU ao longo do tempo, porcentagem de uso da memória ao longo do tempo e megabytes de espaço livre em disco ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="4da72-411">**Computer Performance** - Shows line charts of the percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="4da72-412">Passe o cursor sobre qualquer linha em um gráfico para exibir mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="4da72-412">You can hover over any line in a chart to view more details.</span></span>


<span data-ttu-id="4da72-413">Cada área do painel é uma representação visual de uma pesquisa executada nos dados coletados.</span><span class="sxs-lookup"><span data-stu-id="4da72-413">Each area of the dashboard is a visual representation of a search that is run on collected data.</span></span>

![Painel de Contêineres](./media/log-analytics-containers/containers-dash01.png)

![Painel de Contêineres](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="4da72-416">Na área **Status do Contêiner**, clique na área superior, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="4da72-416">In the **Container Status** area, click the top area, as shown below.</span></span>

![Status dos contêineres](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="4da72-418">A Pesquisa de Log é aberta, exibindo informações sobre o estado de seus contêineres.</span><span class="sxs-lookup"><span data-stu-id="4da72-418">Log Search opens, displaying information about the state of your containers.</span></span>

![Pesquisa de Log para contêineres](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="4da72-420">A partir daqui, você pode editar a consulta de pesquisa para modificá-la para localizar as informações específicas nas quais está interessado.</span><span class="sxs-lookup"><span data-stu-id="4da72-420">From here, you can edit the search query to modify it to find the specific information you're interested in.</span></span> <span data-ttu-id="4da72-421">Para obter mais informações sobre as Pesquisas de Log, consulte [Pesquisas de log no Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="4da72-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="4da72-422">Solucionar problemas localizando um contêiner com falha</span><span class="sxs-lookup"><span data-stu-id="4da72-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="4da72-423">O Log Analytics marca um contêiner como **Com Falha** se ele tiver sido encerrado com um código de saída diferente de zero.</span><span class="sxs-lookup"><span data-stu-id="4da72-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="4da72-424">Você pode conferir uma visão geral dos erros e falhas no ambiente na área **Contêineres com Falha**.</span><span class="sxs-lookup"><span data-stu-id="4da72-424">You can see an overview of the errors and failures in the environment in the **Failed Containers** area.</span></span>

### <a name="to-find-failed-containers"></a><span data-ttu-id="4da72-425">Para localizar contêineres com falha</span><span class="sxs-lookup"><span data-stu-id="4da72-425">To find failed containers</span></span>
1. <span data-ttu-id="4da72-426">Clique na área **Status do Contêiner**.</span><span class="sxs-lookup"><span data-stu-id="4da72-426">Click the **Container Status** area.</span></span>  
   <span data-ttu-id="4da72-427">![status dos contêineres](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="4da72-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="4da72-428">A Pesquisa de Log é aberta e exibe o estado dos contêineres, semelhante ao seguinte.</span><span class="sxs-lookup"><span data-stu-id="4da72-428">Log Search opens and displays the state of your containers, similar to the following.</span></span>  
   ![estado dos contêineres](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="4da72-430">Em seguida, clique no valor agregado de contêineres com falha para exibir mais informações.</span><span class="sxs-lookup"><span data-stu-id="4da72-430">Next, click the aggregated value of failed containers to view additional information.</span></span> <span data-ttu-id="4da72-431">Expanda **mostrar mais** para exibir a ID da imagem.</span><span class="sxs-lookup"><span data-stu-id="4da72-431">Expand **show more** to view the image ID.</span></span>  
   <span data-ttu-id="4da72-432">![contêineres com falha](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="4da72-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="4da72-433">Depois, digite o seguinte na consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="4da72-433">Next, type the following in the search query.</span></span> <span data-ttu-id="4da72-434">`Type=ContainerInventory <ImageID>` para ver detalhes sobre a imagem, como o tamanho da imagem e o número de imagens paradas e com falha.</span><span class="sxs-lookup"><span data-stu-id="4da72-434">`Type=ContainerInventory <ImageID>` to see details about the image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="4da72-435">![contêineres com falha](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="4da72-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="4da72-436">Pesquisar nos logs por dados do contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-436">Search logs for container data</span></span>
<span data-ttu-id="4da72-437">Quando você estiver solucionando um erro específico, pode ajudar ver onde ele está ocorrendo em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="4da72-437">When you're troubleshooting a specific error, it can help to see where it is occurring in your environment.</span></span> <span data-ttu-id="4da72-438">Os tipos de log a seguir ajudarão você a criar consultas para retornar as informações desejadas.</span><span class="sxs-lookup"><span data-stu-id="4da72-438">The following log types will help you create queries to return the information you want.</span></span>


- <span data-ttu-id="4da72-439">**ContainerImageInventory** – use este tipo quando estiver tentando localizar informações organizadas por imagem e para exibir informações da imagem como os tamanhos ou IDs da imagem.</span><span class="sxs-lookup"><span data-stu-id="4da72-439">**ContainerImageInventory** – Use this type when you're trying to find information organized by image and to view image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="4da72-440">**ContainerInventory** – use este tipo quando desejar obter informações sobre a localização do contêiner, quais são seus nomes e quais imagens eles estão executando.</span><span class="sxs-lookup"><span data-stu-id="4da72-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="4da72-441">**ContainerLog** – use este tipo quando desejar localizar entradas e informações de log de erro específicas.</span><span class="sxs-lookup"><span data-stu-id="4da72-441">**ContainerLog** – Use this type when you want to find specific error log information and entries.</span></span>
- <span data-ttu-id="4da72-442">**ContainerNodeInventory_CL** Use este tipo quando você quiser informações sobre o nó/host onde os contêineres residem.</span><span class="sxs-lookup"><span data-stu-id="4da72-442">**ContainerNodeInventory_CL**  Use this type when you want the information about host/node where containers are residing.</span></span> <span data-ttu-id="4da72-443">Ele fornece ao Docker informações de versão, tipo de orquestração, armazenamento e rede.</span><span class="sxs-lookup"><span data-stu-id="4da72-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="4da72-444">**ContainerProcess_CL** Use esse tipo para ver rapidamente o processo em execução dentro do contêiner.</span><span class="sxs-lookup"><span data-stu-id="4da72-444">**ContainerProcess_CL** Use this type to quickly see the process running within the container.</span></span>
- <span data-ttu-id="4da72-445">**ContainerServiceLog** – use este tipo quando estiver tentando localizar informações de trilha de auditoria para o daemon do Docker, como os comandos start, stop, delete ou pull.</span><span class="sxs-lookup"><span data-stu-id="4da72-445">**ContainerServiceLog** – Use this type when you're trying to find audit trail information for the Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="4da72-446">**KubeEvents_CL** Use este tipo para ver os eventos de Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="4da72-446">**KubeEvents_CL**  Use this type to see the Kubernetes events.</span></span>
- <span data-ttu-id="4da72-447">**KubePodInventory_CL** Use este tipo quando quiser entender as informações de hierarquia do cluster.</span><span class="sxs-lookup"><span data-stu-id="4da72-447">**KubePodInventory_CL**  Use this type when you want to understand the cluster hierarchy information.</span></span>


### <a name="to-search-logs-for-container-data"></a><span data-ttu-id="4da72-448">Para pesquisar nos logs por dados do contêiner</span><span class="sxs-lookup"><span data-stu-id="4da72-448">To search logs for container data</span></span>
* <span data-ttu-id="4da72-449">Escolha uma imagem que você saiba que falhou recentemente e encontre os logs de erros dela.</span><span class="sxs-lookup"><span data-stu-id="4da72-449">Choose an image that you know has failed recently and find the error logs for it.</span></span> <span data-ttu-id="4da72-450">Comece localizando um nome de contêiner que está executando a imagem com uma pesquisa **ContainerInventory**.</span><span class="sxs-lookup"><span data-stu-id="4da72-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="4da72-451">Por exemplo, pesquise por `Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="4da72-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="4da72-452">![Pesquisar por contêineres do Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="4da72-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="4da72-453">O nome do contêiner ao lado de **Nome** e pesquise por esses logs.</span><span class="sxs-lookup"><span data-stu-id="4da72-453">The name of the container next to **Name**, and search for those logs.</span></span> <span data-ttu-id="4da72-454">Neste exemplo, é `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="4da72-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="4da72-455">**Exibir informações de desempenho**</span><span class="sxs-lookup"><span data-stu-id="4da72-455">**View performance information**</span></span>

<span data-ttu-id="4da72-456">Quando você começar a construir consultas, pode ajudar ver o que é possível primeiro.</span><span class="sxs-lookup"><span data-stu-id="4da72-456">When you're beginning to construct queries, it can help to see what's possible first.</span></span> <span data-ttu-id="4da72-457">Por exemplo, para ver todos os dados de desempenho, tente uma consulta ampla digitando a seguinte consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="4da72-457">For example, to see all performance data, try a broad query by typing the following search query.</span></span>

```
Type=Perf
```

![desempenho de contêineres](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="4da72-459">Você pode definir o escopo dos dados de desempenho que está vendo para um contêiner específico digitando o nome dele à direita da sua consulta.</span><span class="sxs-lookup"><span data-stu-id="4da72-459">You can scope the performance data you're seeing to a specific container by typing the name of it to the right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="4da72-460">Isso mostra a lista de métricas de desempenho que são coletadas para um contêiner individual.</span><span class="sxs-lookup"><span data-stu-id="4da72-460">That shows the list of performance metrics that are collected for an individual container.</span></span>

![desempenho de contêineres](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="4da72-462">Exemplo de consultas de pesquisa de log</span><span class="sxs-lookup"><span data-stu-id="4da72-462">Example log search queries</span></span>
<span data-ttu-id="4da72-463">Costuma ser útil criar consultas começando com um ou dois exemplos e, em seguida, modificá-los de acordo com seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="4da72-463">It's often useful to build queries starting with an example or two and then modifying them to fit your environment.</span></span> <span data-ttu-id="4da72-464">Como ponto de partida, você pode experimentar com a área **Consultas de Exemplo** para ajudar você a criar consultas mais avançadas.</span><span class="sxs-lookup"><span data-stu-id="4da72-464">As a starting point, you can experiment with the **Sample Queries** area to help you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Consultas de contêineres](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="4da72-466">Salvando as consultas de pesquisa de log</span><span class="sxs-lookup"><span data-stu-id="4da72-466">Saving log search queries</span></span>
<span data-ttu-id="4da72-467">Salvar consultas é um recurso padrão do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="4da72-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="4da72-468">Ao salvá-las, você terá aquelas que considerou úteis acessíveis para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="4da72-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="4da72-469">Depois de criar uma consulta que considerar útil, salve-a clicando em **Favoritos** na parte superior da página Pesquisa de Log.</span><span class="sxs-lookup"><span data-stu-id="4da72-469">After you create a query that you find useful, save it by clicking **Favorites** at the top of the Log Search page.</span></span> <span data-ttu-id="4da72-470">Depois, você pode acessá-la facilmente pela página **Meu Painel**.</span><span class="sxs-lookup"><span data-stu-id="4da72-470">Then you can easily access it later from the **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4da72-471">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4da72-471">Next steps</span></span>
* <span data-ttu-id="4da72-472">[Pesquise nos logs](log-analytics-log-searches.md) para exibir registros de dados de contêiner detalhados.</span><span class="sxs-lookup"><span data-stu-id="4da72-472">[Search logs](log-analytics-log-searches.md) to view detailed container data records.</span></span>
