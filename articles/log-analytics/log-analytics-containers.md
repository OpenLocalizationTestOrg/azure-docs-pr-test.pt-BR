---
title: "aaaContainer solução de monitoramento no Azure Log Analytics | Microsoft Docs"
description: "Olá solução de monitoramento de contêiner na análise de Log ajuda a exibir e gerenciar o Docker e Windows hosts de contêiner em um único local."
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
ms.openlocfilehash: 2eed1dd81c22faef78a375fca3ebece9e5300c09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="container-monitoring-solution-in-log-analytics"></a><span data-ttu-id="ecced-103">Solução de Monitoramento de contêiner no Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ecced-103">Container Monitoring solution in Log Analytics</span></span>

![Símbolo dos Contêineres](./media/log-analytics-containers/containers-symbol.png)

<span data-ttu-id="ecced-105">Este artigo descreve como tooset backup e use Olá solução de monitoramento de contêiner na análise de Log, o que ajuda a exibir e gerenciar o Docker e Windows hosts de contêiner em um único local.</span><span class="sxs-lookup"><span data-stu-id="ecced-105">This article describes how tooset up and use hello Container Monitoring solution in Log Analytics, which helps you view and manage your Docker and Windows container hosts in a single location.</span></span> <span data-ttu-id="ecced-106">O docker é um sistema de virtualização de software usado contêineres toocreate automatizam a implantação de software tootheir IT infraestrutura.</span><span class="sxs-lookup"><span data-stu-id="ecced-106">Docker is a software virtualization system used toocreate containers that automate software deployment tootheir IT infrastructure.</span></span>

<span data-ttu-id="ecced-107">Olá mostra de solução que estiver executando contêineres, qual imagem de contêiner que estejam em execução, e onde contêineres estão em execução.</span><span class="sxs-lookup"><span data-stu-id="ecced-107">hello solution shows which containers are running, what container image they’re running, and where containers are running.</span></span> <span data-ttu-id="ecced-108">Você pode exibir informações detalhadas de auditoria, mostrando os comandos usados com contêineres.</span><span class="sxs-lookup"><span data-stu-id="ecced-108">You can view detailed audit information showing commands used with containers.</span></span> <span data-ttu-id="ecced-109">E, você pode solucionar problemas de contêineres exibindo e pesquisando centralizado de logs sem a necessidade de exibição tooremotely Docker ou hosts de Windows.</span><span class="sxs-lookup"><span data-stu-id="ecced-109">And, you can troubleshoot containers by viewing and searching centralized logs without having tooremotely view Docker or Windows hosts.</span></span> <span data-ttu-id="ecced-110">Você pode encontrar contêineres que podem estar com ruídos e consumindo recursos em excesso em um host.</span><span class="sxs-lookup"><span data-stu-id="ecced-110">You can find containers that may be noisy and consuming excess resources on a host.</span></span> <span data-ttu-id="ecced-111">E você pode exibir o uso de CPU, memória, armazenamento e rede e informações de desempenho centralizadas para contêineres.</span><span class="sxs-lookup"><span data-stu-id="ecced-111">And, you can view centralized CPU, memory, storage, and network usage and performance information for containers.</span></span> <span data-ttu-id="ecced-112">Nos computadores que executam o Windows, você pode centralizar e comparar os logs do Windows Server, do Hyper-V e dos contêineres do Docker.</span><span class="sxs-lookup"><span data-stu-id="ecced-112">On computers running Windows, you can centralize and compare logs from Windows Server, Hyper-V, and Docker containers.</span></span> <span data-ttu-id="ecced-113">solução de saudação dá suporte à saudação orchestrators contêiner a seguir:</span><span class="sxs-lookup"><span data-stu-id="ecced-113">hello solution supports hello following container orchestrators:</span></span>

- <span data-ttu-id="ecced-114">Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="ecced-114">Docker Swarm</span></span>
- <span data-ttu-id="ecced-115">DC/OS</span><span class="sxs-lookup"><span data-stu-id="ecced-115">DC/OS</span></span>
- <span data-ttu-id="ecced-116">kubernetes</span><span class="sxs-lookup"><span data-stu-id="ecced-116">Kubernetes</span></span>
- <span data-ttu-id="ecced-117">Service Fabric</span><span class="sxs-lookup"><span data-stu-id="ecced-117">Service Fabric</span></span>
- <span data-ttu-id="ecced-118">Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="ecced-118">Red Hat OpenShift</span></span>


<span data-ttu-id="ecced-119">Olá diagrama a seguir mostra as relações de saudação entre vários hosts de contêiner e agentes com o OMS.</span><span class="sxs-lookup"><span data-stu-id="ecced-119">hello following diagram shows hello relationships between various container hosts and agents with OMS.</span></span>

![Diagrama de contêineres](./media/log-analytics-containers/containers-diagram.png)

## <a name="system-requirements"></a><span data-ttu-id="ecced-121">Requisitos do sistema</span><span class="sxs-lookup"><span data-stu-id="ecced-121">System requirements</span></span>

<span data-ttu-id="ecced-122">Antes de começar, examine Olá tooverify detalhes que você atenda aos pré-requisitos Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="ecced-122">Before starting, review hello following details tooverify you meet hello prerequisites.</span></span>

### <a name="container-monitoring-solution-support-for-docker-orchestrator-and-os-platform"></a><span data-ttu-id="ecced-123">Suporte de solução de monitoramento de contêiner para Docker Orchestrator e plataforma do SO</span><span class="sxs-lookup"><span data-stu-id="ecced-123">Container monitoring solution support for Docker Orchestrator and OS platform</span></span>
<span data-ttu-id="ecced-124">Olá tabela a seguir descreve Olá orquestração de Docker e o sistema operacional monitoramento suporte de inventário de contêiner, desempenho e logs de análise de Log.</span><span class="sxs-lookup"><span data-stu-id="ecced-124">hello following table outlines hello Docker orchestration and operating system monitoring support of container inventory, performance, and logs with Log Analytics.</span></span>   

| | <span data-ttu-id="ecced-125">ACS</span><span class="sxs-lookup"><span data-stu-id="ecced-125">ACS</span></span> | <span data-ttu-id="ecced-126">Linux</span><span class="sxs-lookup"><span data-stu-id="ecced-126">Linux</span></span> | <span data-ttu-id="ecced-127">Windows</span><span class="sxs-lookup"><span data-stu-id="ecced-127">Windows</span></span> | <span data-ttu-id="ecced-128">Contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-128">Container</span></span><br><span data-ttu-id="ecced-129">Inventário</span><span class="sxs-lookup"><span data-stu-id="ecced-129">Inventory</span></span> | <span data-ttu-id="ecced-130">Imagem</span><span class="sxs-lookup"><span data-stu-id="ecced-130">Image</span></span><br><span data-ttu-id="ecced-131">Inventário</span><span class="sxs-lookup"><span data-stu-id="ecced-131">Inventory</span></span> | <span data-ttu-id="ecced-132">Nó</span><span class="sxs-lookup"><span data-stu-id="ecced-132">Node</span></span><br><span data-ttu-id="ecced-133">Inventário</span><span class="sxs-lookup"><span data-stu-id="ecced-133">Inventory</span></span> | <span data-ttu-id="ecced-134">Contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-134">Container</span></span><br><span data-ttu-id="ecced-135">Desempenho</span><span class="sxs-lookup"><span data-stu-id="ecced-135">Performance</span></span> | <span data-ttu-id="ecced-136">Contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-136">Container</span></span><br><span data-ttu-id="ecced-137">Evento</span><span class="sxs-lookup"><span data-stu-id="ecced-137">Event</span></span> | <span data-ttu-id="ecced-138">Evento</span><span class="sxs-lookup"><span data-stu-id="ecced-138">Event</span></span><br><span data-ttu-id="ecced-139">Registro</span><span class="sxs-lookup"><span data-stu-id="ecced-139">Log</span></span> | <span data-ttu-id="ecced-140">Contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-140">Container</span></span><br><span data-ttu-id="ecced-141">Registro</span><span class="sxs-lookup"><span data-stu-id="ecced-141">Log</span></span> |
|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|-----|
| <span data-ttu-id="ecced-142">kubernetes</span><span class="sxs-lookup"><span data-stu-id="ecced-142">Kubernetes</span></span> | <span data-ttu-id="ecced-143">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-143">&#8226;</span></span> | <span data-ttu-id="ecced-144">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-144">&#8226;</span></span> | | <span data-ttu-id="ecced-145">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-145">&#8226;</span></span> | <span data-ttu-id="ecced-146">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-146">&#8226;</span></span> | <span data-ttu-id="ecced-147">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-147">&#8226;</span></span> | <span data-ttu-id="ecced-148">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-148">&#8226;</span></span> | <span data-ttu-id="ecced-149">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-149">&#8226;</span></span> | <span data-ttu-id="ecced-150">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-150">&#8226;</span></span> | <span data-ttu-id="ecced-151">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-151">&#8226;</span></span> |
| <span data-ttu-id="ecced-152">Mesosphere</span><span class="sxs-lookup"><span data-stu-id="ecced-152">Mesosphere</span></span><br><span data-ttu-id="ecced-153">DC/OS</span><span class="sxs-lookup"><span data-stu-id="ecced-153">DC/OS</span></span> | <span data-ttu-id="ecced-154">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-154">&#8226;</span></span> | <span data-ttu-id="ecced-155">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-155">&#8226;</span></span> | | <span data-ttu-id="ecced-156">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-156">&#8226;</span></span> | <span data-ttu-id="ecced-157">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-157">&#8226;</span></span> | <span data-ttu-id="ecced-158">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-158">&#8226;</span></span> | <span data-ttu-id="ecced-159">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-159">&#8226;</span></span>| <span data-ttu-id="ecced-160">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-160">&#8226;</span></span> | <span data-ttu-id="ecced-161">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-161">&#8226;</span></span> | <span data-ttu-id="ecced-162">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-162">&#8226;</span></span> |
| <span data-ttu-id="ecced-163">Docker</span><span class="sxs-lookup"><span data-stu-id="ecced-163">Docker</span></span><br><span data-ttu-id="ecced-164">Swarm</span><span class="sxs-lookup"><span data-stu-id="ecced-164">Swarm</span></span> | <span data-ttu-id="ecced-165">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-165">&#8226;</span></span> | <span data-ttu-id="ecced-166">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-166">&#8226;</span></span> | <span data-ttu-id="ecced-167">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-167">&#8226;</span></span> | <span data-ttu-id="ecced-168">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-168">&#8226;</span></span> | <span data-ttu-id="ecced-169">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-169">&#8226;</span></span> | <span data-ttu-id="ecced-170">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-170">&#8226;</span></span> | <span data-ttu-id="ecced-171">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-171">&#8226;</span></span> | <span data-ttu-id="ecced-172">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-172">&#8226;</span></span> | | <span data-ttu-id="ecced-173">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-173">&#8226;</span></span> |
| <span data-ttu-id="ecced-174">O Barramento de</span><span class="sxs-lookup"><span data-stu-id="ecced-174">Service</span></span><br><span data-ttu-id="ecced-175">Fabric</span><span class="sxs-lookup"><span data-stu-id="ecced-175">Fabric</span></span> | | | <span data-ttu-id="ecced-176">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-176">&#8226;</span></span> | <span data-ttu-id="ecced-177">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-177">&#8226;</span></span> | <span data-ttu-id="ecced-178">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-178">&#8226;</span></span> | <span data-ttu-id="ecced-179">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-179">&#8226;</span></span> | <span data-ttu-id="ecced-180">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-180">&#8226;</span></span> | <span data-ttu-id="ecced-181">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-181">&#8226;</span></span> | <span data-ttu-id="ecced-182">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-182">&#8226;</span></span> | <span data-ttu-id="ecced-183">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-183">&#8226;</span></span> |
| <span data-ttu-id="ecced-184">Red Hat Open</span><span class="sxs-lookup"><span data-stu-id="ecced-184">Red Hat Open</span></span><br><span data-ttu-id="ecced-185">Shift</span><span class="sxs-lookup"><span data-stu-id="ecced-185">Shift</span></span> | | <span data-ttu-id="ecced-186">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-186">&#8226;</span></span> | | <span data-ttu-id="ecced-187">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-187">&#8226;</span></span> | <span data-ttu-id="ecced-188">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-188">&#8226;</span></span>| <span data-ttu-id="ecced-189">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-189">&#8226;</span></span> | <span data-ttu-id="ecced-190">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-190">&#8226;</span></span> | <span data-ttu-id="ecced-191">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-191">&#8226;</span></span> | | <span data-ttu-id="ecced-192">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-192">&#8226;</span></span> |
| <span data-ttu-id="ecced-193">Windows Server</span><span class="sxs-lookup"><span data-stu-id="ecced-193">Windows Server</span></span><br><span data-ttu-id="ecced-194">(autônomo)</span><span class="sxs-lookup"><span data-stu-id="ecced-194">(standalone)</span></span> | | | <span data-ttu-id="ecced-195">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-195">&#8226;</span></span> | <span data-ttu-id="ecced-196">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-196">&#8226;</span></span> | <span data-ttu-id="ecced-197">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-197">&#8226;</span></span> | <span data-ttu-id="ecced-198">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-198">&#8226;</span></span> | <span data-ttu-id="ecced-199">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-199">&#8226;</span></span> | <span data-ttu-id="ecced-200">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-200">&#8226;</span></span> | | <span data-ttu-id="ecced-201">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-201">&#8226;</span></span> |
| <span data-ttu-id="ecced-202">Linux Server</span><span class="sxs-lookup"><span data-stu-id="ecced-202">Linux Server</span></span><br><span data-ttu-id="ecced-203">(autônomo)</span><span class="sxs-lookup"><span data-stu-id="ecced-203">(standalone)</span></span> | | <span data-ttu-id="ecced-204">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-204">&#8226;</span></span> | | <span data-ttu-id="ecced-205">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-205">&#8226;</span></span> | <span data-ttu-id="ecced-206">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-206">&#8226;</span></span> | <span data-ttu-id="ecced-207">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-207">&#8226;</span></span> | <span data-ttu-id="ecced-208">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-208">&#8226;</span></span> | <span data-ttu-id="ecced-209">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-209">&#8226;</span></span> | | <span data-ttu-id="ecced-210">&#8226;</span><span class="sxs-lookup"><span data-stu-id="ecced-210">&#8226;</span></span> |


### <a name="docker-versions-supported-on-linux"></a><span data-ttu-id="ecced-211">Versões do Docker com suporte no Linux</span><span class="sxs-lookup"><span data-stu-id="ecced-211">Docker versions supported on Linux</span></span>

- <span data-ttu-id="ecced-212">Docker 1.11 too1.13</span><span class="sxs-lookup"><span data-stu-id="ecced-212">Docker 1.11 too1.13</span></span>
- <span data-ttu-id="ecced-213">Docker CE e EE v17.06</span><span class="sxs-lookup"><span data-stu-id="ecced-213">Docker CE and EE v17.06</span></span>

### <a name="x64-linux-distributions-supported-as-container-hosts"></a><span data-ttu-id="ecced-214">As distribuições de Linux x64 têm suporte como hosts de contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-214">x64 Linux distributions supported as container hosts</span></span>

- <span data-ttu-id="ecced-215">Ubuntu 14.04 LTS e 16.04 LTS</span><span class="sxs-lookup"><span data-stu-id="ecced-215">Ubuntu 14.04 LTS and 16.04 LTS</span></span>
- <span data-ttu-id="ecced-216">CoreOS(stable)</span><span class="sxs-lookup"><span data-stu-id="ecced-216">CoreOS(stable)</span></span>
- <span data-ttu-id="ecced-217">Amazon Linux 2016.09.0</span><span class="sxs-lookup"><span data-stu-id="ecced-217">Amazon Linux 2016.09.0</span></span>
- <span data-ttu-id="ecced-218">openSUSE 13.2</span><span class="sxs-lookup"><span data-stu-id="ecced-218">openSUSE 13.2</span></span>
- <span data-ttu-id="ecced-219">openSUSE LEAP 42.2</span><span class="sxs-lookup"><span data-stu-id="ecced-219">openSUSE LEAP 42.2</span></span>
- <span data-ttu-id="ecced-220">CentOS 7.2 e 7.3</span><span class="sxs-lookup"><span data-stu-id="ecced-220">CentOS 7.2 and 7.3</span></span>
- <span data-ttu-id="ecced-221">SLES 12</span><span class="sxs-lookup"><span data-stu-id="ecced-221">SLES 12</span></span>
- <span data-ttu-id="ecced-222">RHEL 7.2 e 7.3</span><span class="sxs-lookup"><span data-stu-id="ecced-222">RHEL 7.2 and 7.3</span></span>
- <span data-ttu-id="ecced-223">Red Hat OpenShift Container Platform (OCP) 3.4 e 3.5</span><span class="sxs-lookup"><span data-stu-id="ecced-223">Red Hat OpenShift Container Platform (OCP) 3.4 and 3.5</span></span>
- <span data-ttu-id="ecced-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span><span class="sxs-lookup"><span data-stu-id="ecced-224">ACS Mesosphere DC/OS 1.7.3 too1.8.8</span></span>
- <span data-ttu-id="ecced-225">ACS Kubernetes 1.4.5 too1.6</span><span class="sxs-lookup"><span data-stu-id="ecced-225">ACS Kubernetes 1.4.5 too1.6</span></span>
- <span data-ttu-id="ecced-226">ACS Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="ecced-226">ACS Docker Swarm</span></span>

### <a name="supported-windows-operating-system"></a><span data-ttu-id="ecced-227">Sistema operacional Windows com suporte</span><span class="sxs-lookup"><span data-stu-id="ecced-227">Supported Windows operating system</span></span>

- <span data-ttu-id="ecced-228">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ecced-228">Windows Server 2016</span></span>
- <span data-ttu-id="ecced-229">Edição de aniversário do Windows 10 (Professional ou Enterprise)</span><span class="sxs-lookup"><span data-stu-id="ecced-229">Windows 10 Anniversary Edition (Professional or Enterprise)</span></span>

### <a name="docker-versions-supported-on-windows"></a><span data-ttu-id="ecced-230">Versões do Docker do Windows com suporte</span><span class="sxs-lookup"><span data-stu-id="ecced-230">Docker versions supported on Windows</span></span>

- <span data-ttu-id="ecced-231">Docker 1.12 e 1.13</span><span class="sxs-lookup"><span data-stu-id="ecced-231">Docker 1.12 and 1.13</span></span>
- <span data-ttu-id="ecced-232">Docker 17.03.0 e mais recente</span><span class="sxs-lookup"><span data-stu-id="ecced-232">Docker 17.03.0 and later</span></span>

## <a name="installing-and-configuring-hello-solution"></a><span data-ttu-id="ecced-233">Instalando e configurando a solução Olá</span><span class="sxs-lookup"><span data-stu-id="ecced-233">Installing and configuring hello solution</span></span>
<span data-ttu-id="ecced-234">Use Olá tooinstall informações a seguir e configurar a solução de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecced-234">Use hello following information tooinstall and configure hello solution.</span></span>

1. <span data-ttu-id="ecced-235">Adicionar Olá monitoramento de contêiner solução tooyour OMS espaço de trabalho de [do Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) ou usando o processo de saudação descrito em [soluções de análise de Log adicionar da Galeria de soluções de saudação](log-analytics-add-solutions.md).</span><span class="sxs-lookup"><span data-stu-id="ecced-235">Add hello Container Monitoring solution tooyour OMS workspace from [Azure marketplace](https://azuremarketplace.microsoft.com/marketplace/apps/Microsoft.ContainersOMS?tab=Overview) or by using hello process described in [Add Log Analytics solutions from hello Solutions Gallery](log-analytics-add-solutions.md).</span></span>

2. <span data-ttu-id="ecced-236">Instale e use o Docker com um agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="ecced-236">Install and use Docker with an OMS agent.</span></span>  <span data-ttu-id="ecced-237">Com base no seu sistema operacional, você pode escolher Olá métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ecced-237">Based on your operating system, you can choose from hello following methods:</span></span>

  * <span data-ttu-id="ecced-238">Em sistemas operacionais Linux com suporte, instale e execute Docker e, em seguida, instalar e configurar Olá [agente do OMS para Linux](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ecced-238">On supported Linux operating systems, install and run Docker and then install and configure hello [OMS Agent for Linux](log-analytics-agent-linux.md).</span></span>  
  * <span data-ttu-id="ecced-239">Em CoreOS, você não pode executar Olá agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="ecced-239">On CoreOS, you cannot run hello OMS Agent for Linux.</span></span> <span data-ttu-id="ecced-240">Em vez disso, você deve executar uma versão em contêineres de saudação do agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="ecced-240">Instead, you run a containerized version of hello OMS Agent for Linux.</span></span> <span data-ttu-id="ecced-241">Confira [Hosts de contêiner do Linux incluindo CoreOS](#for-all-linux-container-hosts-including-coreos) ou [Hosts de contêiner do Linux do Azure Governamental incluindo CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) se você estiver trabalhando com contêineres na nuvem do Azure Governamental.</span><span class="sxs-lookup"><span data-stu-id="ecced-241">Review [Linux container hosts including CoreOS](#for-all-linux-container-hosts-including-coreos) or [Azure Government Linux container hosts including CoreOS](#for-all-azure-government-linux-container-hosts-including-coreos) if you are working with containers in Azure Government Cloud.</span></span>
  * <span data-ttu-id="ecced-242">No Windows Server 2016 e Windows 10, instale Olá mecanismo do Docker e o cliente e informações de toogather um agente de conexão e enviá-lo tooLog análise.</span><span class="sxs-lookup"><span data-stu-id="ecced-242">On Windows Server 2016 and Windows 10, install hello Docker Engine and client then connect an agent toogather information and send it tooLog Analytics.</span></span>  

### <a name="container-services"></a><span data-ttu-id="ecced-243">Serviços de Contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-243">Container services</span></span>

- <span data-ttu-id="ecced-244">Se você tiver um ambiente do Red Hat OpenShift, confira [Configurar um agente do OMS para Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span><span class="sxs-lookup"><span data-stu-id="ecced-244">If you have a Red Hat OpenShift environment, review [Configure an OMS agent for Red Hat OpenShift](#configure-an-oms-agent-for-red-hat-openshift).</span></span>
- <span data-ttu-id="ecced-245">Se você tiver um cluster de Kubernetes usando Olá serviço de contêiner do Azure, examine [monitorar um cluster do serviço de contêiner do Azure com o Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span><span class="sxs-lookup"><span data-stu-id="ecced-245">If you have a Kubernetes cluster using hello Azure Container Service, review [Monitor an Azure Container Service cluster with Microsoft Operations Management Suite (OMS)](../container-service/kubernetes/container-service-kubernetes-oms.md).</span></span>
- <span data-ttu-id="ecced-246">Se você tiver um cluster de DC/SO do Serviço de Contêiner do Azure, saiba mais em [Monitorar um cluster DC/OS do Serviço de Contêiner do Azure com o Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span><span class="sxs-lookup"><span data-stu-id="ecced-246">If you have an Azure Container Service DC/OS cluster, learn more at [Monitor an Azure Container Service DC/OS cluster with Operations Management Suite](../container-service/dcos-swarm/container-service-monitoring-oms.md).</span></span>
- <span data-ttu-id="ecced-247">Se você tiver um ambiente no modo Docker Swarm, saiba mais em [Configurar um agente do OMS para o Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span><span class="sxs-lookup"><span data-stu-id="ecced-247">If you have a Docker Swarm mode environment, learn more at [Configure an OMS agent for Docker Swarm](#configure-an-oms-agent-for-docker-swarm).</span></span>
- <span data-ttu-id="ecced-248">Se você usa contêineres com o Service Fabric, saiba mais em [Visão geral do Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ecced-248">If you use containers with Service Fabric, learn more at [Overview of Azure Service Fabric](../service-fabric/service-fabric-overview.md).</span></span>
- <span data-ttu-id="ecced-249">Saudação de revisão [mecanismo do Docker no Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) artigo para obter informações adicionais sobre como tooinstall e configurar os mecanismos de Docker em computadores que executam o Windows.</span><span class="sxs-lookup"><span data-stu-id="ecced-249">Review hello [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon) article for additional information about how tooinstall and configure your Docker Engines on computers running Windows.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ecced-250">Deve estar executando o docker **antes de** instalar Olá [agente do OMS para Linux](log-analytics-agent-linux.md) em seus hosts de contêiner.</span><span class="sxs-lookup"><span data-stu-id="ecced-250">Docker must be running **before** you install hello [OMS Agent for Linux](log-analytics-agent-linux.md) on your container hosts.</span></span> <span data-ttu-id="ecced-251">Se você já tiver instalado o agente de saudação antes de instalar o Docker, será necessário tooreinstall Olá agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="ecced-251">If you've already installed hello agent before installing Docker, you need tooreinstall hello OMS Agent for Linux.</span></span> <span data-ttu-id="ecced-252">Para obter mais informações sobre o Docker, consulte Olá [site Docker](https://www.docker.com).</span><span class="sxs-lookup"><span data-stu-id="ecced-252">For more information about Docker, see hello [Docker website](https://www.docker.com).</span></span>


## <a name="linux-container-hosts"></a><span data-ttu-id="ecced-253">Hosts de contêiner do Linux</span><span class="sxs-lookup"><span data-stu-id="ecced-253">Linux container hosts</span></span>

<span data-ttu-id="ecced-254">Depois de instalar o Docker, use Olá seguindo as configurações para o agente de saudação do contêiner host tooconfigure para uso com o Docker.</span><span class="sxs-lookup"><span data-stu-id="ecced-254">After you've installed Docker, use hello following settings for your container host tooconfigure hello agent for use with Docker.</span></span> <span data-ttu-id="ecced-255">Primeiro, é necessário a ID do espaço de trabalho do OMS e a chave, o que você pode encontrar no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="ecced-255">First you need your OMS workspace ID and key, which you can find in hello Azure portal.</span></span> <span data-ttu-id="ecced-256">No espaço de trabalho, clique em **início rápido** > **computadores** tooview sua **ID do espaço de trabalho** e **chave primária**.</span><span class="sxs-lookup"><span data-stu-id="ecced-256">In your workspace, click **Quick Start** > **Computers** tooview your **Workspace ID** and **Primary Key**.</span></span>  <span data-ttu-id="ecced-257">Copie e cole os dois em seu editor favorito.</span><span class="sxs-lookup"><span data-stu-id="ecced-257">Copy and paste both into your favorite editor.</span></span>

### <a name="for-all-linux-container-hosts-except-coreos"></a><span data-ttu-id="ecced-258">Para todos os hosts de contêiner do Linux, exceto CoreOS</span><span class="sxs-lookup"><span data-stu-id="ecced-258">For all Linux container hosts except CoreOS</span></span>

- <span data-ttu-id="ecced-259">Para obter mais informações e etapas sobre como tooinstall Olá agente do OMS para Linux, consulte [conectar seu tooOperations de computadores Linux Management Suite (OMS)](log-analytics-agent-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ecced-259">For more information and steps on how tooinstall hello OMS Agent for Linux, see [Connect your Linux Computers tooOperations Management Suite (OMS)](log-analytics-agent-linux.md).</span></span>

### <a name="for-all-linux-container-hosts-including-coreos"></a><span data-ttu-id="ecced-260">Para todos os hosts de contêiner do Linux, incluindo o CoreOS</span><span class="sxs-lookup"><span data-stu-id="ecced-260">For all Linux container hosts including CoreOS</span></span>

<span data-ttu-id="ecced-261">Inicie o contêiner OMS Olá que você deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="ecced-261">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="ecced-262">Modifique e use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ecced-262">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -e WSID="your workspace id" -e KEY="your key" -h=`hostname` -p 127.0.0.1:25225:25225 --name="omsagent" --restart=always microsoft/oms
```

### <a name="for-all-azure-government-linux-container-hosts-including-coreos"></a><span data-ttu-id="ecced-263">Para todos os hosts de contêiner do Linux no Azure Governamental, incluindo CoreOS</span><span class="sxs-lookup"><span data-stu-id="ecced-263">For all Azure Government Linux container hosts including CoreOS</span></span>

<span data-ttu-id="ecced-264">Inicie o contêiner OMS Olá que você deseja toomonitor.</span><span class="sxs-lookup"><span data-stu-id="ecced-264">Start hello OMS container that you want toomonitor.</span></span> <span data-ttu-id="ecced-265">Modifique e use Olá exemplo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ecced-265">Modify and use hello following example:</span></span>

```
sudo docker run --privileged -d -v /var/run/docker.sock:/var/run/docker.sock -v /var/log:/var/log -e WSID="your workspace id" -e KEY="your key" -e DOMAIN="opinsights.azure.us" -p 127.0.0.1:25225:25225 -p 127.0.0.1:25224:25224/udp --name="omsagent" -h=`hostname` --restart=always microsoft/oms
```

### <a name="switching-from-using-an-installed-linux-agent-tooone-in-a-container"></a><span data-ttu-id="ecced-266">Alternando do usando um tooone de agente Linux instalado em um contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-266">Switching from using an installed Linux agent tooone in a container</span></span>
<span data-ttu-id="ecced-267">Se você anteriormente usada agente instalado diretamente do hello e deseja tooinstead usar um agente em execução em um contêiner, você deve primeiro remover Olá agente do OMS para Linux.</span><span class="sxs-lookup"><span data-stu-id="ecced-267">If you previously used hello directly-installed agent and want tooinstead use an agent running in a container, you must first remove hello OMS Agent for Linux.</span></span> <span data-ttu-id="ecced-268">Consulte [Olá de desinstalação do agente do OMS para Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand como toosuccessfully desinstalar Olá agente.</span><span class="sxs-lookup"><span data-stu-id="ecced-268">See [Uninstalling hello OMS Agent for Linux](log-analytics-agent-linux.md#uninstalling-the-oms-agent-for-linux) toounderstand how toosuccessfully uninstall hello agent.</span></span>  

### <a name="configure-an-oms-agent-for-docker-swarm"></a><span data-ttu-id="ecced-269">Configurar um agente do OMS para o Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="ecced-269">Configure an OMS agent for Docker Swarm</span></span>

<span data-ttu-id="ecced-270">Você pode executar Olá agente do OMS como um serviço global em Docker Swarm.</span><span class="sxs-lookup"><span data-stu-id="ecced-270">You can run hello OMS Agent as a global service on Docker Swarm.</span></span> <span data-ttu-id="ecced-271">Use Olá toocreate informações sobre um serviço de agente do OMS a seguir.</span><span class="sxs-lookup"><span data-stu-id="ecced-271">Use hello following information toocreate an OMS Agent service.</span></span> <span data-ttu-id="ecced-272">É necessário tooinsert sua ID de espaço de trabalho do OMS e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="ecced-272">You need tooinsert your OMS Workspace ID and Primary Key.</span></span>

- <span data-ttu-id="ecced-273">Execute o seguinte de Olá no nó mestre hello.</span><span class="sxs-lookup"><span data-stu-id="ecced-273">Run hello following on hello master node.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock  -e WSID="<WORKSPACE ID>" -e KEY="<PRIMARY KEY>" -p 25225:25225 -p 25224:25224/udp  --restart-condition=on-failure microsoft/oms
    ```

### <a name="configure-an-oms-agent-for-red-hat-openshift"></a><span data-ttu-id="ecced-274">Configurar um Agente do OMS para o Red Hat OpenShift</span><span class="sxs-lookup"><span data-stu-id="ecced-274">Configure an OMS Agent for Red Hat OpenShift</span></span>
<span data-ttu-id="ecced-275">Há três maneiras tooadd Olá agente do OMS tooRed Hat OpenShift toostart coleta contêiner dados de monitoramento.</span><span class="sxs-lookup"><span data-stu-id="ecced-275">There are three ways tooadd hello OMS Agent tooRed Hat OpenShift toostart collecting container monitoring data.</span></span>

* <span data-ttu-id="ecced-276">[Instalar Olá agente do OMS para Linux](log-analytics-agent-linux.md) diretamente em cada nó de OpenShift</span><span class="sxs-lookup"><span data-stu-id="ecced-276">[Install hello OMS Agent for Linux](log-analytics-agent-linux.md) directly on each OpenShift node</span></span>  
* <span data-ttu-id="ecced-277">[Habilitar a extensão de VM do Log Analytics](log-analytics-azure-vm-extension.md) em cada nó do OpenShift que reside no Azure</span><span class="sxs-lookup"><span data-stu-id="ecced-277">[Enable Log Analytics VM Extension](log-analytics-azure-vm-extension.md) on each OpenShift node residing in Azure</span></span>  
* <span data-ttu-id="ecced-278">Instalar Olá agente do OMS como um conjunto de daemon OpenShift</span><span class="sxs-lookup"><span data-stu-id="ecced-278">Install hello OMS Agent as a OpenShift daemon-set</span></span>  

<span data-ttu-id="ecced-279">Nesta seção, abordaremos Olá etapas tooinstall necessário Olá agente do OMS como um conjunto de daemon OpenShift.</span><span class="sxs-lookup"><span data-stu-id="ecced-279">In this section we cover hello steps required tooinstall hello OMS Agent as an OpenShift daemon-set.</span></span>  

1. <span data-ttu-id="ecced-280">Logon toohello OpenShift nó e cópia Olá yaml arquivo mestre [omsagent.yaml ocp](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) do GitHub tooyour mestre nó e modificar o valor de saudação com sua ID de espaço de trabalho do OMS e sua chave primária.</span><span class="sxs-lookup"><span data-stu-id="ecced-280">Sign on toohello OpenShift master node and copy hello yaml file [ocp-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-omsagent.yaml) from GitHub tooyour master node and modify hello value with your OMS Workspace ID and with your Primary Key.</span></span>
2. <span data-ttu-id="ecced-281">Executar um projeto de saudação toocreate comandos a seguir para OMS e definir a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecced-281">Run hello following commands toocreate a project for OMS and set hello user account.</span></span>

    ```
    oadm new-project omslogging --node-selector='zone=default'
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="ecced-282">Olá toodeploy conjunto de daemon, execute o seguinte de saudação:</span><span class="sxs-lookup"><span data-stu-id="ecced-282">toodeploy hello daemon-set, run hello following:</span></span>

    `oc create -f ocp-omsagent.yaml`

5. <span data-ttu-id="ecced-283">tooverify está configurado e funcionando corretamente, digite o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="ecced-283">tooverify it is configured and working correctly, type hello following:</span></span>

    `oc describe daemonset omsagent`  

    <span data-ttu-id="ecced-284">e a saída de hello deve se parecer com:</span><span class="sxs-lookup"><span data-stu-id="ecced-284">and hello output should resemble:</span></span>

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

<span data-ttu-id="ecced-285">Se você quiser toouse segredos toosecure sua ID de espaço de trabalho do OMS e a chave primária ao usar arquivo de conjunto daemon yaml de agente do OMS hello, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="ecced-285">If you want toouse secrets toosecure your OMS Workspace ID and Primary Key when using hello OMS Agent daemon-set yaml file, perform hello following steps.</span></span>

1. <span data-ttu-id="ecced-286">Logon toohello OpenShift nó e cópia Olá yaml arquivo mestre [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) e o segredo Gerando script [secretgen.sh ocp](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) do GitHub.</span><span class="sxs-lookup"><span data-stu-id="ecced-286">Sign on toohello OpenShift master node and copy hello yaml file [ocp-ds-omsagent.yaml](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-ds-omsagent.yaml) and secret generating script [ocp-secretgen.sh](https://github.com/Microsoft/OMS-docker/blob/master/OpenShift/ocp-secretgen.sh) from GitHub.</span></span>  <span data-ttu-id="ecced-287">Esse script vai gerar arquivo de yaml de segredos Olá para ID de espaço de trabalho do OMS e a chave primária toosecure seu secrete informações.</span><span class="sxs-lookup"><span data-stu-id="ecced-287">This script will generate hello secrets yaml file for OMS Workspace ID and Primary Key toosecure your secrete information.</span></span>  
2. <span data-ttu-id="ecced-288">Executar um projeto de saudação toocreate comandos a seguir para OMS e definir a conta de usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecced-288">Run hello following commands toocreate a project for OMS and set hello user account.</span></span> <span data-ttu-id="ecced-289">segredo de saudação Gerando script solicita sua ID de espaço de trabalho do OMS <WSID> e a chave primária <KEY> e após a conclusão, ele cria o arquivo de ocp-secret.yaml de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecced-289">hello secret generating script asks for your OMS Workspace ID <WSID> and Primary Key <KEY> and upon completion, it creates hello ocp-secret.yaml file.</span></span>  

    ```
    oadm new-project omslogging --node-selector='zone=default'  
    oc project omslogging  
    oc create serviceaccount omsagent  
    oadm policy add-cluster-role-to-user cluster-reader   system:serviceaccount:omslogging:omsagent  
    oadm policy add-scc-to-user privileged system:serviceaccount:omslogging:omsagent  
    ```

4. <span data-ttu-id="ecced-290">Implante arquivo secreto Olá executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ecced-290">Deploy hello secret file by running hello following:</span></span>

    `oc create -f ocp-secret.yaml`

5. <span data-ttu-id="ecced-291">Verifique se a implantação executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ecced-291">Verify deployment by running hello following:</span></span>

    `oc describe secret omsagent-secret`  

    <span data-ttu-id="ecced-292">e a saída de hello deve se parecer com:</span><span class="sxs-lookup"><span data-stu-id="ecced-292">and hello  output should resemble:</span></span>  

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

6. <span data-ttu-id="ecced-293">Implante arquivo de conjunto de daemon yaml agente do OMS Olá executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ecced-293">Deploy hello OMS Agent daemon-set yaml file by running hello following:</span></span>

    `oc create -f ocp-ds-omsagent.yaml`  

7. <span data-ttu-id="ecced-294">Verifique se a implantação executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ecced-294">Verify deployment by running hello following:</span></span>

    `oc describe ds oms`

    <span data-ttu-id="ecced-295">e a saída de hello deve se parecer com:</span><span class="sxs-lookup"><span data-stu-id="ecced-295">and hello output should resemble:</span></span>

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

### <a name="secure-your-secret-information-for-docker-swarm-and-kubernetes"></a><span data-ttu-id="ecced-296">Proteger suas informações secretas do Docker Swarm e Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ecced-296">Secure your secret information for Docker Swarm and Kubernetes</span></span>

<span data-ttu-id="ecced-297">Proteja sua ID do Espaço de Trabalho do OMS e as Chaves Primárias secretas para os serviços de contêiner Docker Swarm e Kubernetes.</span><span class="sxs-lookup"><span data-stu-id="ecced-297">You can secure your secret OMS Workspace ID and Primary Keys for Docker Swarm and Kubernetes container services.</span></span>

#### <a name="secure-secrets-for-docker-swarm"></a><span data-ttu-id="ecced-298">Proteger segredos do Docker Swarm</span><span class="sxs-lookup"><span data-stu-id="ecced-298">Secure secrets for Docker Swarm</span></span>

<span data-ttu-id="ecced-299">Para Docker Swarm, quando segredo Olá para o ID do espaço de trabalho e a chave primária é criado, você pode executar Olá criar serviço do Docker Olá para OMSagent.</span><span class="sxs-lookup"><span data-stu-id="ecced-299">For Docker Swarm, once hello secret for Workspace ID and Primary Key is created, you can run hello create hello Docker service for OMSagent.</span></span> <span data-ttu-id="ecced-300">Use suas informações de segredo de Olá toocreate informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="ecced-300">Use hello following information toocreate your secret information.</span></span>

1. <span data-ttu-id="ecced-301">Execute o seguinte de Olá no nó mestre hello.</span><span class="sxs-lookup"><span data-stu-id="ecced-301">Run hello following on hello master node.</span></span>

    ```
    echo "WSID" | docker secret create WSID -
    echo "KEY" | docker secret create KEY -
    ```

2. <span data-ttu-id="ecced-302">Verifique se os segredos foram criados corretamente.</span><span class="sxs-lookup"><span data-stu-id="ecced-302">Verify that secrets were created properly.</span></span>

    ```
    keiko@swarmm-master-13957614-0:/run# sudo docker secret ls
    ```

    ```
    ID                          NAME                CREATED             UPDATED
    j2fj153zxy91j8zbcitnjxjiv   WSID                43 minutes ago      43 minutes ago
    l9rh3n987g9c45zffuxdxetd9   KEY                 38 minutes ago      38 minutes ago
    ```

3. <span data-ttu-id="ecced-303">Olá execução após o comando toomount Olá segredos toohello em contêineres do agente do OMS.</span><span class="sxs-lookup"><span data-stu-id="ecced-303">Run hello following command toomount hello secrets toohello containerized OMS Agent.</span></span>

    ```
    sudo docker service create  --name omsagent --mode global  --mount type=bind,source=/var/run/docker.sock,destination=/var/run/docker.sock --secret source=WSID,target=WSID --secret source=KEY,target=KEY  -p 25225:25225 -p 25224:25224/udp --restart-condition=on-failure microsoft/oms
    ```

#### <a name="secure-secrets-for-kubernetes-with-yaml-files"></a><span data-ttu-id="ecced-304">Proteger segredos do Kubernetes com arquivos yaml</span><span class="sxs-lookup"><span data-stu-id="ecced-304">Secure secrets for Kubernetes with yaml files</span></span>

<span data-ttu-id="ecced-305">Para Kubernetes, você pode usar um arquivo de yaml script toogenerate Olá segredos para a ID do espaço de trabalho e a chave primária.</span><span class="sxs-lookup"><span data-stu-id="ecced-305">For Kubernetes, you use a script toogenerate hello secrets yaml file for your Workspace ID and Primary Key.</span></span> <span data-ttu-id="ecced-306">Em Olá [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) página, os arquivos que você pode usar com ou sem informações de segredo.</span><span class="sxs-lookup"><span data-stu-id="ecced-306">At hello [OMS Docker Kubernetes GitHub](https://github.com/Microsoft/OMS-docker/tree/master/Kubernetes) page, there are files that you can use with or without your secret information.</span></span>

- <span data-ttu-id="ecced-307">saudação padrão DaemonSet de agente do OMS não tem informações secretas (omsagent.yaml)</span><span class="sxs-lookup"><span data-stu-id="ecced-307">hello Default OMS Agent DaemonSet does not have secret information (omsagent.yaml)</span></span>
- <span data-ttu-id="ecced-308">arquivo de yaml Olá DaemonSet de agente do OMS usa informações secretas (omsagent-ds-secrets.yaml) com secreta arquivo geração de scripts toogenerate Olá segredos yaml (omsagentsecret.yaml).</span><span class="sxs-lookup"><span data-stu-id="ecced-308">hello OMS Agent DaemonSet yaml file uses secret information (omsagent-ds-secrets.yaml) with secret generation scripts toogenerate hello secrets yaml (omsagentsecret.yaml) file.</span></span>

<span data-ttu-id="ecced-309">Você pode escolher toocreate omsagent DaemonSets com ou sem segredos.</span><span class="sxs-lookup"><span data-stu-id="ecced-309">You can choose toocreate omsagent DaemonSets with or without secrets.</span></span>

##### <a name="default-omsagent-daemonset-yaml-file-without-secrets"></a><span data-ttu-id="ecced-310">Arquivo yaml do DaemonSet do OMSagent Padrão sem segredos</span><span class="sxs-lookup"><span data-stu-id="ecced-310">Default OMSagent DaemonSet yaml file without secrets</span></span>

- <span data-ttu-id="ecced-311">Para o arquivo yaml do saudação padrão DaemonSet de agente do OMS, substitua Olá `<WSID>` e `<KEY>` tooyour WSID e a chave.</span><span class="sxs-lookup"><span data-stu-id="ecced-311">For hello default OMS Agent DaemonSet yaml file, replace hello `<WSID>` and `<KEY>` tooyour WSID and KEY.</span></span> <span data-ttu-id="ecced-312">Copiar nó mestre da saudação arquivo tooyour e seguir Olá execução:</span><span class="sxs-lookup"><span data-stu-id="ecced-312">Copy hello file tooyour master node and run hello following:</span></span>

    ```
    sudo kubectl create -f omsagent.yaml
    ```

##### <a name="default-omsagent-daemonset-yaml-file-with-secrets"></a><span data-ttu-id="ecced-313">Arquivo yaml do DaemonSet do OMSagent Padrão com segredos</span><span class="sxs-lookup"><span data-stu-id="ecced-313">Default OMSagent DaemonSet yaml file with secrets</span></span>

1. <span data-ttu-id="ecced-314">toouse DaemonSet de agente do OMS usando informações secretas, criar segredos Olá primeiro.</span><span class="sxs-lookup"><span data-stu-id="ecced-314">toouse OMS Agent DaemonSet using secret information, create hello secrets first.</span></span>
    1. <span data-ttu-id="ecced-315">Copie o script hello e arquivo de modelo de segredo e verifique se estão em uma saudação mesmo diretório.</span><span class="sxs-lookup"><span data-stu-id="ecced-315">Copy hello script and secret template file and make sure they are on hello same directory.</span></span>
        - <span data-ttu-id="ecced-316">Script de geração de segredo – secret-gen.sh</span><span class="sxs-lookup"><span data-stu-id="ecced-316">Secret generating script - secret-gen.sh</span></span>
        - <span data-ttu-id="ecced-317">modelo de segredo – secret-template.yaml</span><span class="sxs-lookup"><span data-stu-id="ecced-317">secret template - secret-template.yaml</span></span>
    2. <span data-ttu-id="ecced-318">Execute script hello, como Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="ecced-318">Run hello script, like hello following example.</span></span> <span data-ttu-id="ecced-319">script Hello solicita Olá ID do espaço de trabalho do OMS e a chave primária e depois que você inseri-los, script hello cria um arquivo de segredo yaml para possam ser executados.</span><span class="sxs-lookup"><span data-stu-id="ecced-319">hello script asks for hello OMS Workspace ID and Primary Key and after you enter them, hello script creates a secret yaml file so you can run it.</span></span>   

        ```
        #> sudo bash ./secret-gen.sh
        ```

    3. <span data-ttu-id="ecced-320">Crie pod de segredos Olá executando Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ecced-320">Create hello secrets pod by running hello following:</span></span>
        ```
        sudo kubectl create -f omsagentsecret.yaml
        ```

    4. <span data-ttu-id="ecced-321">tooverify, execute Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="ecced-321">tooverify, run hello following:</span></span>

        ```
        keiko@ubuntu16-13db:~# sudo kubectl get secrets
        ```

        <span data-ttu-id="ecced-322">O resultado deve ser semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="ecced-322">Output should resemble:</span></span>

        ```
        NAME                  TYPE                                  DATA      AGE
        default-token-gvl91   kubernetes.io/service-account-token   3         50d
        omsagent-secret       Opaque                                2         1d
        ```

        ```
        keiko@ubuntu16-13db:~# sudo kubectl describe secrets omsagent-secret
        ```

        <span data-ttu-id="ecced-323">O resultado deve ser semelhante a este:</span><span class="sxs-lookup"><span data-stu-id="ecced-323">Output should resemble:</span></span>

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

    5. <span data-ttu-id="ecced-324">Criar o omsagent daemon-set executando ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span><span class="sxs-lookup"><span data-stu-id="ecced-324">Create your omsagent daemon-set by running ``` sudo kubectl create -f omsagent-ds-secrets.yaml ```</span></span>

2. <span data-ttu-id="ecced-325">Verifique se esse Olá que daemonset de agente do OMS está em execução, toohello semelhante a seguir:</span><span class="sxs-lookup"><span data-stu-id="ecced-325">Verify that hello OMS Agent DaemonSet is running, similar toohello following:</span></span>

    ```
    keiko@ubuntu16-13db:~# sudo kubectl get ds omsagent
    ```

    ```
    NAME       DESIRED   CURRENT   NODE-SELECTOR   AGE
    omsagent   3         3         <none>          1h
    ```


<span data-ttu-id="ecced-326">Para Kubernetes, use um arquivo de yaml de segredos do script toogenerate Olá para o ID do espaço de trabalho e chave primária.</span><span class="sxs-lookup"><span data-stu-id="ecced-326">For Kubernetes, use a script toogenerate hello secrets yaml file for Workspace ID and Primary Key.</span></span> <span data-ttu-id="ecced-327">Saudação de uso a seguir exemplos de informações com hello [omsagent yaml arquivo](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure suas informações secretas.</span><span class="sxs-lookup"><span data-stu-id="ecced-327">Use hello following example information with hello [omsagent yaml file](https://github.com/Microsoft/OMS-docker/blob/master/Kubernetes/omsagent.yaml) toosecure your secret information.</span></span>

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

## <a name="windows-container-hosts"></a><span data-ttu-id="ecced-328">Hosts de contêiner do Windows</span><span class="sxs-lookup"><span data-stu-id="ecced-328">Windows container hosts</span></span>

### <a name="preparation-before-installing-windows-agents"></a><span data-ttu-id="ecced-329">Preparação antes de instalar os agentes do Windows</span><span class="sxs-lookup"><span data-stu-id="ecced-329">Preparation before installing Windows agents</span></span>

<span data-ttu-id="ecced-330">Antes de instalar agentes em computadores que executam o Windows, você precisa de serviço de Docker de saudação tooconfigure.</span><span class="sxs-lookup"><span data-stu-id="ecced-330">Before you install agents on computers running Windows, you need tooconfigure hello Docker service.</span></span> <span data-ttu-id="ecced-331">configuração de saudação permite Olá Windows agente ou hello análise de Log máquina virtual extensão toouse hello de soquete TCP de Docker para que os agentes Olá podem acessar o daemon do Docker Olá remotamente e toocapture dados para o monitoramento.</span><span class="sxs-lookup"><span data-stu-id="ecced-331">hello configuration allows hello Windows agent or hello Log Analytics virtual machine extension toouse hello Docker TCP socket so that hello agents can access hello Docker daemon remotely and toocapture data for monitoring.</span></span>

#### <a name="toostart-docker-and-verify-its-configuration"></a><span data-ttu-id="ecced-332">toostart Docker e verifique se sua configuração</span><span class="sxs-lookup"><span data-stu-id="ecced-332">toostart Docker and verify its configuration</span></span>

<span data-ttu-id="ecced-333">Há etapas necessárias tooset backup TCP pipe nomeado para o Windows Server:</span><span class="sxs-lookup"><span data-stu-id="ecced-333">There are steps needed tooset up TCP named pipe for Windows Server:</span></span>

1. <span data-ttu-id="ecced-334">No Windows PowerShell, habilite o pipe TCP e o pipe nomeado.</span><span class="sxs-lookup"><span data-stu-id="ecced-334">In Windows PowerShell, enable TCP pipe and named pipe.</span></span>

    ```
    Stop-Service docker
    dockerd --unregister-service
    dockerd --register-service -H npipe:// -H 0.0.0.0:2375  
    Start-Service docker
    ```

2. <span data-ttu-id="ecced-335">Configurar o Docker com o arquivo de configuração de saudação do pipe TCP e o pipe nomeado.</span><span class="sxs-lookup"><span data-stu-id="ecced-335">Configure Docker with hello configuration file for TCP pipe and named pipe.</span></span> <span data-ttu-id="ecced-336">arquivo de configuração de saudação está localizado em C:\ProgramData\docker\config\daemon.json.</span><span class="sxs-lookup"><span data-stu-id="ecced-336">hello configuration file is located at C:\ProgramData\docker\config\daemon.json.</span></span>

    <span data-ttu-id="ecced-337">Arquivo daemon JSON hello, você precisará seguir hello:</span><span class="sxs-lookup"><span data-stu-id="ecced-337">In hello daemon.json file, you will need hello following:</span></span>

    ```
    {
    "hosts": ["tcp://0.0.0.0:2375", "npipe://"]
    }
    ```

<span data-ttu-id="ecced-338">Para obter mais informações sobre a configuração de daemon do Docker Olá usada com contêineres do Windows, consulte [mecanismo do Docker no Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span><span class="sxs-lookup"><span data-stu-id="ecced-338">For more information about hello Docker daemon configuration used with Windows Containers, see [Docker Engine on Windows](https://docs.microsoft.com/virtualization/windowscontainers/manage-docker/configure-docker-daemon).</span></span>


### <a name="install-windows-agents"></a><span data-ttu-id="ecced-339">Instalar agentes do Windows</span><span class="sxs-lookup"><span data-stu-id="ecced-339">Install Windows agents</span></span>

<span data-ttu-id="ecced-340">tooenable Windows e contêiner do Hyper-V de monitoramento, instale Olá agente de monitoramento da Microsoft (MMA) em computadores com Windows que são hosts de contêiner.</span><span class="sxs-lookup"><span data-stu-id="ecced-340">tooenable Windows and Hyper-V container monitoring, install hello Microsoft Monitoring Agent (MMA) on Windows computers that are container hosts.</span></span> <span data-ttu-id="ecced-341">Para computadores que executam o Windows em seu ambiente local, consulte [Windows conectar computadores tooLog análise](log-analytics-windows-agents.md).</span><span class="sxs-lookup"><span data-stu-id="ecced-341">For computers running Windows in your on-premises environment, see [Connect Windows computers tooLog Analytics](log-analytics-windows-agents.md).</span></span> <span data-ttu-id="ecced-342">Para máquinas virtuais em execução no Azure, conecte-os tooLog análise usando Olá [extensão da máquina virtual](log-analytics-azure-vm-extension.md).</span><span class="sxs-lookup"><span data-stu-id="ecced-342">For virtual machines running in Azure, connect them tooLog Analytics using hello [virtual machine extension](log-analytics-azure-vm-extension.md).</span></span>

<span data-ttu-id="ecced-343">Você pode monitorar os contêineres do Windows em execução no Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ecced-343">You can monitor Windows containers running on Service Fabric.</span></span> <span data-ttu-id="ecced-344">No entanto, apenas [máquinas virtuais em execução no Azure](log-analytics-azure-vm-extension.md) e [computadores executando o Windows no seu ambiente local](log-analytics-windows-agents.md) têm suporte atualmente para o Service Fabric.</span><span class="sxs-lookup"><span data-stu-id="ecced-344">However, only [virtual machines running in Azure](log-analytics-azure-vm-extension.md) and [computers running Windows in your on-premises environment](log-analytics-windows-agents.md) are currently supported for Service Fabric.</span></span>

<span data-ttu-id="ecced-345">Você pode verificar que essa solução de monitoramento de contêiner hello está definida corretamente para o Windows.</span><span class="sxs-lookup"><span data-stu-id="ecced-345">You can verify that hello Container Monitoring solution is set correctly for Windows.</span></span> <span data-ttu-id="ecced-346">toocheck se o pacote de gerenciamento de saudação foi download corretamente, procure *ContainerManagement.xxx*.</span><span class="sxs-lookup"><span data-stu-id="ecced-346">toocheck whether hello management pack was download properly, look for *ContainerManagement.xxx*.</span></span> <span data-ttu-id="ecced-347">Olá arquivos devem ser na pasta C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecced-347">hello files should be in hello C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs folder.</span></span>


## <a name="solution-components"></a><span data-ttu-id="ecced-348">Componentes da solução</span><span class="sxs-lookup"><span data-stu-id="ecced-348">Solution components</span></span>

<span data-ttu-id="ecced-349">Se você estiver usando agentes do Windows, em seguida, hello seguinte pacote de gerenciamento é instalado em cada computador com um agente quando você adicionar essa solução.</span><span class="sxs-lookup"><span data-stu-id="ecced-349">If you are using Windows agents, then hello following management pack is installed on each computer with an agent when you add this solution.</span></span> <span data-ttu-id="ecced-350">Nenhuma configuração ou a manutenção é necessária para o pacote de gerenciamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecced-350">No configuration or maintenance is required for hello management pack.</span></span>

- <span data-ttu-id="ecced-351">*ContainerManagement.xxx* instalado em C:\Arquivos de Programas\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span><span class="sxs-lookup"><span data-stu-id="ecced-351">*ContainerManagement.xxx* installed in C:\Program Files\Microsoft Monitoring Agent\Agent\Health Service State\Management Packs</span></span>

## <a name="container-data-collection-details"></a><span data-ttu-id="ecced-352">Detalhes da coleta de dados dos contêineres</span><span class="sxs-lookup"><span data-stu-id="ecced-352">Container data collection details</span></span>
<span data-ttu-id="ecced-353">Olá solução de monitoramento de contêiner coleta vários dados de log e métricas de desempenho de hosts de contêiner e contêineres usando agentes que permitem a você.</span><span class="sxs-lookup"><span data-stu-id="ecced-353">hello Container Monitoring solution collects various performance metrics and log data from container hosts and containers using agents that you enable.</span></span>

<span data-ttu-id="ecced-354">Dados são coletados a cada três minutos por Olá seguintes tipos de agente.</span><span class="sxs-lookup"><span data-stu-id="ecced-354">Data is collected every three minutes by hello following agent types.</span></span>

- [<span data-ttu-id="ecced-355">Agente do OMS para Linux</span><span class="sxs-lookup"><span data-stu-id="ecced-355">OMS Agent for Linux</span></span>](log-analytics-linux-agents.md)
- [<span data-ttu-id="ecced-356">Agente do Windows</span><span class="sxs-lookup"><span data-stu-id="ecced-356">Windows agent</span></span>](log-analytics-windows-agents.md)
- [<span data-ttu-id="ecced-357">Extensão de VM do Log Analytics</span><span class="sxs-lookup"><span data-stu-id="ecced-357">Log Analytics VM extension</span></span>](log-analytics-azure-vm-extension.md)


### <a name="container-records"></a><span data-ttu-id="ecced-358">Registros de contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-358">Container records</span></span>

<span data-ttu-id="ecced-359">Olá tabela a seguir mostra exemplos de registros coletados pela solução de monitoramento de contêiner de saudação e tipos de dados de saudação que aparecem nos resultados da pesquisa de log.</span><span class="sxs-lookup"><span data-stu-id="ecced-359">hello following table shows examples of records collected by hello Container Monitoring solution and hello data types that appear in log search results.</span></span>

| <span data-ttu-id="ecced-360">Tipo de dados</span><span class="sxs-lookup"><span data-stu-id="ecced-360">Data type</span></span> | <span data-ttu-id="ecced-361">Tipo de dados na Pesquisa de Log</span><span class="sxs-lookup"><span data-stu-id="ecced-361">Data type in Log Search</span></span> | <span data-ttu-id="ecced-362">Campos</span><span class="sxs-lookup"><span data-stu-id="ecced-362">Fields</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ecced-363">Desempenho de hosts e contêineres</span><span class="sxs-lookup"><span data-stu-id="ecced-363">Performance for hosts and containers</span></span> | `Type=Perf` | <span data-ttu-id="ecced-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ecced-364">Computer, ObjectName, CounterName &#40;%Processor Time, Disk Reads MB, Disk Writes MB, Memory Usage MB, Network Receive Bytes, Network Send Bytes, Processor Usage sec, Network&#41;, CounterValue,TimeGenerated, CounterPath, SourceSystem</span></span> |
| <span data-ttu-id="ecced-365">Inventário de contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-365">Container inventory</span></span> | `Type=ContainerInventory` | <span data-ttu-id="ecced-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span><span class="sxs-lookup"><span data-stu-id="ecced-366">TimeGenerated, Computer, container name, ContainerHostname, Image, ImageTag, ContainerState, ExitCode, EnvironmentVar, Command, CreatedTime, StartedTime, FinishedTime, SourceSystem, ContainerID, ImageID</span></span> |
| <span data-ttu-id="ecced-367">Inventário de imagem de contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-367">Container image inventory</span></span> | `Type=ContainerImageInventory` | <span data-ttu-id="ecced-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span><span class="sxs-lookup"><span data-stu-id="ecced-368">TimeGenerated, Computer, Image, ImageTag, ImageSize, VirtualSize, Running, Paused, Stopped, Failed, SourceSystem, ImageID, TotalContainer</span></span> |
| <span data-ttu-id="ecced-369">Log do contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-369">Container log</span></span> | `Type=ContainerLog` | <span data-ttu-id="ecced-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="ecced-370">TimeGenerated, Computer, image ID, container name, LogEntrySource, LogEntry, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="ecced-371">Log do serviço de contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-371">Container service log</span></span> | `Type=ContainerServiceLog`  | <span data-ttu-id="ecced-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span><span class="sxs-lookup"><span data-stu-id="ecced-372">TimeGenerated, Computer, TimeOfCommand, Image, Command, SourceSystem, ContainerID</span></span> |
| <span data-ttu-id="ecced-373">Inventário de nós do contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-373">Container node inventory</span></span> | `Type=ContainerNodeInventory_CL`| <span data-ttu-id="ecced-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ecced-374">TimeGenerated, Computer, ClassName_s, DockerVersion_s, OperatingSystem_s, Volume_s, Network_s, NodeRole_s, OrchestratorType_s, InstanceID_g, SourceSystem</span></span>|
| <span data-ttu-id="ecced-375">Inventário de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ecced-375">Kubernetes inventory</span></span> | `Type=KubePodInventory_CL` | <span data-ttu-id="ecced-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ecced-376">TimeGenerated, Computer, PodLabel_deployment_s, PodLabel_deploymentconfig_s, PodLabel_docker_registry_s, Name_s, Namespace_s, PodStatus_s, PodIp_s, PodUid_g, PodCreationTimeStamp_t, SourceSystem</span></span> |
| <span data-ttu-id="ecced-377">Processo do contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-377">Container process</span></span> | `Type=ContainerProcess_CL` | <span data-ttu-id="ecced-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span><span class="sxs-lookup"><span data-stu-id="ecced-378">TimeGenerated, Computer, Pod_s, Namespace_s, ClassName_s, InstanceID_s, Uid_s, PID_s, PPID_s, C_s, STIME_s, Tty_s, TIME_s, Cmd_s, Id_s, Name_s, SourceSystem</span></span> |
| <span data-ttu-id="ecced-379">Eventos de Kubernetes</span><span class="sxs-lookup"><span data-stu-id="ecced-379">Kubernetes events</span></span> | `Type=KubeEvents_CL` | <span data-ttu-id="ecced-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span><span class="sxs-lookup"><span data-stu-id="ecced-380">TimeGenerated, Computer, Name_s, ObjectKind_s, Namespace_s, Reason_s, Type_s, SourceComponent_s, SourceSystem, Message</span></span> |

<span data-ttu-id="ecced-381">Rótulos anexados muito*PodLabel* tipos de dados são seus próprios rótulos personalizados.</span><span class="sxs-lookup"><span data-stu-id="ecced-381">Labels appended too*PodLabel* data types are your own custom labels.</span></span> <span data-ttu-id="ecced-382">Olá acrescentados rótulos PodLabel mostrados na tabela de saudação são exemplos.</span><span class="sxs-lookup"><span data-stu-id="ecced-382">hello appended PodLabel labels shown in hello table are examples.</span></span> <span data-ttu-id="ecced-383">Portanto, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` serão diferentes no conjunto de dados de seu ambiente, e genericamente lembram `PodLabel_yourlabel_s`.</span><span class="sxs-lookup"><span data-stu-id="ecced-383">So, `PodLabel_deployment_s`, `PodLabel_deploymentconfig_s`, `PodLabel_docker_registry_s` will differ in your environment's data set and generically resemble `PodLabel_yourlabel_s`.</span></span>


## <a name="monitor-containers"></a><span data-ttu-id="ecced-384">Monitorar contêineres</span><span class="sxs-lookup"><span data-stu-id="ecced-384">Monitor containers</span></span>
<span data-ttu-id="ecced-385">Depois de ter solução Olá habilitada no portal do OMS hello, Olá **contêineres** bloco mostra informações resumidas sobre os hosts de contêiner e os contêineres de saudação em execução em hosts.</span><span class="sxs-lookup"><span data-stu-id="ecced-385">After you have hello solution enabled in hello OMS portal, hello **Containers** tile shows summary information about your container hosts and hello containers running in hosts.</span></span>

![Bloco Contêineres](./media/log-analytics-containers/containers-title.png)

<span data-ttu-id="ecced-387">bloco de saudação mostra uma visão geral de contêineres quantos você tem no ambiente hello e se está falha, em execução ou parado.</span><span class="sxs-lookup"><span data-stu-id="ecced-387">hello tile shows an overview of how many containers you have in hello environment and whether they're failed, running, or stopped.</span></span>

### <a name="using-hello-containers-dashboard"></a><span data-ttu-id="ecced-388">Usando o painel de contêineres de saudação</span><span class="sxs-lookup"><span data-stu-id="ecced-388">Using hello Containers dashboard</span></span>
<span data-ttu-id="ecced-389">Clique em Olá **contêineres** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="ecced-389">Click hello **Containers** tile.</span></span> <span data-ttu-id="ecced-390">A partir daí, você verá exibições organizadas por:</span><span class="sxs-lookup"><span data-stu-id="ecced-390">From there you'll see views organized by:</span></span>

- <span data-ttu-id="ecced-391">**Eventos de Contêiner** - Mostra o status do contêiner, e os computadores com contêineres com falha.</span><span class="sxs-lookup"><span data-stu-id="ecced-391">**Container Events** - Shows container status and computers with failed containers.</span></span>
- <span data-ttu-id="ecced-392">**Logs do contêiner** -mostra um gráfico dos arquivos de log do contêiner gerado com o tempo e uma lista de computadores com o número mais alto de saudação de arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="ecced-392">**Container Logs** - Shows a chart of container log files generated over time and a list of computers with hello highest number of log files.</span></span>
- <span data-ttu-id="ecced-393">**Eventos de Kubernetes** -mostra um gráfico de Kubernetes eventos gerados por hora e uma lista de motivos Olá por compartimentos gerados eventos hello.</span><span class="sxs-lookup"><span data-stu-id="ecced-393">**Kubernetes Events** - Shows a chart of Kubernetes events generated over time and a list of hello reasons why pods generated hello events.</span></span> <span data-ttu-id="ecced-394">*Esse conjunto de dados é usado somente em ambientes Linux.*</span><span class="sxs-lookup"><span data-stu-id="ecced-394">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="ecced-395">**Inventário de Namespace Kubernetes** - mostra o número de saudação de namespaces e compartimentos e mostra sua hierarquia.</span><span class="sxs-lookup"><span data-stu-id="ecced-395">**Kubernetes Namespace Inventory** - Shows hello number of namespaces and pods and shows their hierarchy.</span></span> <span data-ttu-id="ecced-396">*Esse conjunto de dados é usado somente em ambientes Linux.*</span><span class="sxs-lookup"><span data-stu-id="ecced-396">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="ecced-397">**Inventário de nó do contêiner** -mostra o número Olá dos tipos de orquestração usado em nós/hosts de contêiner.</span><span class="sxs-lookup"><span data-stu-id="ecced-397">**Container Node Inventory** - Shows hello number of orchestration types used on container nodes/hosts.</span></span> <span data-ttu-id="ecced-398">Olá computador nós/hosts também são listados pelo número de saudação de contêineres.</span><span class="sxs-lookup"><span data-stu-id="ecced-398">hello computer nodes/hosts are also listed by hello number of containers.</span></span> <span data-ttu-id="ecced-399">*Esse conjunto de dados é usado somente em ambientes Linux.*</span><span class="sxs-lookup"><span data-stu-id="ecced-399">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="ecced-400">**Inventário de imagens de contêiner** -mostra o número total de saudação de imagens de contêiner usado e número de tipos de imagem.</span><span class="sxs-lookup"><span data-stu-id="ecced-400">**Container Images Inventory** - Shows hello total number of container images used and number of image types.</span></span> <span data-ttu-id="ecced-401">número de saudação de imagens também é listado por marca de imagem hello.</span><span class="sxs-lookup"><span data-stu-id="ecced-401">hello number of images are also listed by hello image tag.</span></span>
- <span data-ttu-id="ecced-402">**Status de contêineres** -mostra o número total de saudação do contêiner de computadores de host/nós que têm contêineres em execução.</span><span class="sxs-lookup"><span data-stu-id="ecced-402">**Containers Status** - Shows hello total number of container nodes/host computers that have running containers.</span></span> <span data-ttu-id="ecced-403">Computadores também estarão listados pelo número de saudação da execução de hosts.</span><span class="sxs-lookup"><span data-stu-id="ecced-403">Computers are also listed by hello number of running hosts.</span></span>
- <span data-ttu-id="ecced-404">**Processo do Contêiner** - Mostra um gráfico de linhas dos processos de contêiner em execução ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="ecced-404">**Container Process** - Shows a line chart of container processes running over time.</span></span> <span data-ttu-id="ecced-405">Os contêineres também são listados por meio da execução do comando/processo dentro dos contêineres.</span><span class="sxs-lookup"><span data-stu-id="ecced-405">Containers are also listed by running command/process within containers.</span></span> <span data-ttu-id="ecced-406">*Esse conjunto de dados é usado somente em ambientes Linux.*</span><span class="sxs-lookup"><span data-stu-id="ecced-406">*This data set is used only in Linux environments.*</span></span>
- <span data-ttu-id="ecced-407">**Desempenho de CPU do contêiner** -mostra um gráfico de linha de saudação utilização média da CPU ao longo do tempo para nós/hosts do computador.</span><span class="sxs-lookup"><span data-stu-id="ecced-407">**Container CPU Performance** - Shows a line chart of hello average CPU utilization over time for computer nodes/hosts.</span></span> <span data-ttu-id="ecced-408">Também lista Olá computador nós/hosts com base na média de utilização da CPU.</span><span class="sxs-lookup"><span data-stu-id="ecced-408">Also lists hello computer nodes/hosts based on average CPU utilization.</span></span>
- <span data-ttu-id="ecced-409">**Desempenho de Memória de Contêiner** - Mostra um gráfico de linhas do uso da memória ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="ecced-409">**Container Memory Performance** - Shows a line chart of memory usage over time.</span></span> <span data-ttu-id="ecced-410">Também lista a utilização da memória do computador com base no nome da instância.</span><span class="sxs-lookup"><span data-stu-id="ecced-410">Also lists computer memory utilization based on instance name.</span></span>
- <span data-ttu-id="ecced-411">**Desempenho do computador** -mostra os gráficos de linhas de por cento de saudação do desempenho da CPU ao longo do tempo, porcentagem de uso de memória ao longo do tempo e megabytes de espaço livre em disco ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="ecced-411">**Computer Performance** - Shows line charts of hello percent of CPU performance over time, percent of memory usage over time, and megabytes of free disk space over time.</span></span> <span data-ttu-id="ecced-412">Você pode passar por qualquer linha em um gráfico tooview obter mais detalhes.</span><span class="sxs-lookup"><span data-stu-id="ecced-412">You can hover over any line in a chart tooview more details.</span></span>


<span data-ttu-id="ecced-413">Cada área do painel de saudação é uma representação visual de uma pesquisa que é executada em dados coletados.</span><span class="sxs-lookup"><span data-stu-id="ecced-413">Each area of hello dashboard is a visual representation of a search that is run on collected data.</span></span>

![Painel de Contêineres](./media/log-analytics-containers/containers-dash01.png)

![Painel de Contêineres](./media/log-analytics-containers/containers-dash02.png)

<span data-ttu-id="ecced-416">Em Olá **Status contêiner** área, clique em área superior do hello, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="ecced-416">In hello **Container Status** area, click hello top area, as shown below.</span></span>

![Status dos contêineres](./media/log-analytics-containers/containers-status.png)

<span data-ttu-id="ecced-418">Pesquisa de log é aberto, exibindo informações sobre o estado de saudação de seus contêineres.</span><span class="sxs-lookup"><span data-stu-id="ecced-418">Log Search opens, displaying information about hello state of your containers.</span></span>

![Pesquisa de Log para contêineres](./media/log-analytics-containers/containers-log-search.png)

<span data-ttu-id="ecced-420">A partir daqui, você pode editar Olá toomodify de consulta de pesquisa-informações específicas de saudação toofind você está interessado.</span><span class="sxs-lookup"><span data-stu-id="ecced-420">From here, you can edit hello search query toomodify it toofind hello specific information you're interested in.</span></span> <span data-ttu-id="ecced-421">Para obter mais informações sobre as Pesquisas de Log, consulte [Pesquisas de log no Log Analytics](log-analytics-log-searches.md).</span><span class="sxs-lookup"><span data-stu-id="ecced-421">For more information about Log Searches, see [Log searches in Log Analytics](log-analytics-log-searches.md).</span></span>

## <a name="troubleshoot-by-finding-a-failed-container"></a><span data-ttu-id="ecced-422">Solucionar problemas localizando um contêiner com falha</span><span class="sxs-lookup"><span data-stu-id="ecced-422">Troubleshoot by finding a failed container</span></span>

<span data-ttu-id="ecced-423">O Log Analytics marca um contêiner como **Com Falha** se ele tiver sido encerrado com um código de saída diferente de zero.</span><span class="sxs-lookup"><span data-stu-id="ecced-423">Log Analytics marks a container as **Failed** if it has exited with a non-zero exit code.</span></span> <span data-ttu-id="ecced-424">Você pode ver uma visão geral de erros de saudação e falhas no ambiente Olá Olá **falha contêineres** área.</span><span class="sxs-lookup"><span data-stu-id="ecced-424">You can see an overview of hello errors and failures in hello environment in hello **Failed Containers** area.</span></span>

### <a name="toofind-failed-containers"></a><span data-ttu-id="ecced-425">contêineres de toofind falhou</span><span class="sxs-lookup"><span data-stu-id="ecced-425">toofind failed containers</span></span>
1. <span data-ttu-id="ecced-426">Clique em Olá **Status contêiner** área.</span><span class="sxs-lookup"><span data-stu-id="ecced-426">Click hello **Container Status** area.</span></span>  
   <span data-ttu-id="ecced-427">![status dos contêineres](./media/log-analytics-containers/containers-status.png)</span><span class="sxs-lookup"><span data-stu-id="ecced-427">![containers status](./media/log-analytics-containers/containers-status.png)</span></span>
2. <span data-ttu-id="ecced-428">Pesquisa de log é aberto e exibe o estado de saudação de seus contêineres, toohello semelhante a seguir.</span><span class="sxs-lookup"><span data-stu-id="ecced-428">Log Search opens and displays hello state of your containers, similar toohello following.</span></span>  
   ![estado dos contêineres](./media/log-analytics-containers/containers-log-search.png)
3. <span data-ttu-id="ecced-430">Em seguida, clique em valor Olá agregado de informações adicionais de tooview contêineres com falha.</span><span class="sxs-lookup"><span data-stu-id="ecced-430">Next, click hello aggregated value of failed containers tooview additional information.</span></span> <span data-ttu-id="ecced-431">Expanda **Mostrar mais** ID de imagem tooview hello.</span><span class="sxs-lookup"><span data-stu-id="ecced-431">Expand **show more** tooview hello image ID.</span></span>  
   <span data-ttu-id="ecced-432">![contêineres com falha](./media/log-analytics-containers/containers-state-failed.png)</span><span class="sxs-lookup"><span data-stu-id="ecced-432">![failed containers](./media/log-analytics-containers/containers-state-failed.png)</span></span>  
4. <span data-ttu-id="ecced-433">Em seguida, digite o seguinte Olá Olá consulta de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="ecced-433">Next, type hello following in hello search query.</span></span> <span data-ttu-id="ecced-434">`Type=ContainerInventory <ImageID>`toosee os detalhes sobre a imagem hello como o tamanho da imagem e o número de imagens parados e com falha.</span><span class="sxs-lookup"><span data-stu-id="ecced-434">`Type=ContainerInventory <ImageID>` toosee details about hello image such as image size and number of stopped and failed images.</span></span>  
   <span data-ttu-id="ecced-435">![contêineres com falha](./media/log-analytics-containers/containers-failed04.png)</span><span class="sxs-lookup"><span data-stu-id="ecced-435">![failed containers](./media/log-analytics-containers/containers-failed04.png)</span></span>

## <a name="search-logs-for-container-data"></a><span data-ttu-id="ecced-436">Pesquisar nos logs por dados do contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-436">Search logs for container data</span></span>
<span data-ttu-id="ecced-437">Quando você estiver solucionando um erro específico, isso poderá ajudar toosee onde ele está ocorrendo em seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="ecced-437">When you're troubleshooting a specific error, it can help toosee where it is occurring in your environment.</span></span> <span data-ttu-id="ecced-438">Olá tipos de log a seguir ajudará você a criar consultas de informações de saudação tooreturn desejadas.</span><span class="sxs-lookup"><span data-stu-id="ecced-438">hello following log types will help you create queries tooreturn hello information you want.</span></span>


- <span data-ttu-id="ecced-439">**ContainerImageInventory** – Use este tipo quando você estiver tentando toofind informações organizadas por informações de imagem de imagem e tooview como IDs de imagem ou tamanhos.</span><span class="sxs-lookup"><span data-stu-id="ecced-439">**ContainerImageInventory** – Use this type when you're trying toofind information organized by image and tooview image information such as image IDs or sizes.</span></span>
- <span data-ttu-id="ecced-440">**ContainerInventory** – use este tipo quando desejar obter informações sobre a localização do contêiner, quais são seus nomes e quais imagens eles estão executando.</span><span class="sxs-lookup"><span data-stu-id="ecced-440">**ContainerInventory** – Use this type when you want information about container location, what their names are, and what images they're running.</span></span>
- <span data-ttu-id="ecced-441">**ContainerLog** – Use este tipo quando você deseja informações de log de erro específicas toofind e entradas.</span><span class="sxs-lookup"><span data-stu-id="ecced-441">**ContainerLog** – Use this type when you want toofind specific error log information and entries.</span></span>
- <span data-ttu-id="ecced-442">**ContainerNodeInventory_CL** usar este tipo quando você deseja Olá informações sobre o nó do host onde residem os contêineres.</span><span class="sxs-lookup"><span data-stu-id="ecced-442">**ContainerNodeInventory_CL**  Use this type when you want hello information about host/node where containers are residing.</span></span> <span data-ttu-id="ecced-443">Ele fornece ao Docker informações de versão, tipo de orquestração, armazenamento e rede.</span><span class="sxs-lookup"><span data-stu-id="ecced-443">It provides you Docker version, orchestration type, storage, and network information.</span></span>
- <span data-ttu-id="ecced-444">**ContainerProcess_CL** tooquickly esse tipo de uso consulte processo Olá em execução dentro do contêiner de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecced-444">**ContainerProcess_CL** Use this type tooquickly see hello process running within hello container.</span></span>
- <span data-ttu-id="ecced-445">**ContainerServiceLog** – Use este tipo quando estiver tentando toofind informações sobre a trilha de auditoria para hello daemon do Docker, como iniciar, interromper, excluir ou comandos de pull.</span><span class="sxs-lookup"><span data-stu-id="ecced-445">**ContainerServiceLog** – Use this type when you're trying toofind audit trail information for hello Docker daemon, such as start, stop, delete, or pull commands.</span></span>
- <span data-ttu-id="ecced-446">**KubeEvents_CL** usar esse tipo toosee Olá Kubernetes os eventos.</span><span class="sxs-lookup"><span data-stu-id="ecced-446">**KubeEvents_CL**  Use this type toosee hello Kubernetes events.</span></span>
- <span data-ttu-id="ecced-447">**KubePodInventory_CL** usar esse tipo de informações da hierarquia toounderstand Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="ecced-447">**KubePodInventory_CL**  Use this type when you want toounderstand hello cluster hierarchy information.</span></span>


### <a name="toosearch-logs-for-container-data"></a><span data-ttu-id="ecced-448">logs de toosearch para dados de contêiner</span><span class="sxs-lookup"><span data-stu-id="ecced-448">toosearch logs for container data</span></span>
* <span data-ttu-id="ecced-449">Escolha uma imagem que você sabe que falhou recentemente e localizar os logs de erros de saudação para ele.</span><span class="sxs-lookup"><span data-stu-id="ecced-449">Choose an image that you know has failed recently and find hello error logs for it.</span></span> <span data-ttu-id="ecced-450">Comece localizando um nome de contêiner que está executando a imagem com uma pesquisa **ContainerInventory**.</span><span class="sxs-lookup"><span data-stu-id="ecced-450">Start by finding a container name that is running that image with a **ContainerInventory** search.</span></span> <span data-ttu-id="ecced-451">Por exemplo, pesquise por `Type=ContainerInventory ubuntu Failed`</span><span class="sxs-lookup"><span data-stu-id="ecced-451">For example, search for `Type=ContainerInventory ubuntu Failed`</span></span>  
    <span data-ttu-id="ecced-452">![Pesquisar por contêineres do Ubuntu](./media/log-analytics-containers/search-ubuntu.png)</span><span class="sxs-lookup"><span data-stu-id="ecced-452">![Search for Ubuntu containers](./media/log-analytics-containers/search-ubuntu.png)</span></span>

  <span data-ttu-id="ecced-453">Olá nome do contêiner de saudação Avançar muito**nome**e pesquise esses logs.</span><span class="sxs-lookup"><span data-stu-id="ecced-453">hello name of hello container next too**Name**, and search for those logs.</span></span> <span data-ttu-id="ecced-454">Neste exemplo, é `Type=ContainerLog cranky_stonebreaker`.</span><span class="sxs-lookup"><span data-stu-id="ecced-454">In this example, it is `Type=ContainerLog cranky_stonebreaker`.</span></span>

<span data-ttu-id="ecced-455">**Exibir informações de desempenho**</span><span class="sxs-lookup"><span data-stu-id="ecced-455">**View performance information**</span></span>

<span data-ttu-id="ecced-456">Quando você está começando a consultas tooconstruct, ela pode ajudar a toosee que é possível primeiro.</span><span class="sxs-lookup"><span data-stu-id="ecced-456">When you're beginning tooconstruct queries, it can help toosee what's possible first.</span></span> <span data-ttu-id="ecced-457">Por exemplo, a consulta toosee pesquisar todos os dados de desempenho, tente uma consulta ampla digitando Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="ecced-457">For example, toosee all performance data, try a broad query by typing hello following search query.</span></span>

```
Type=Perf
```

![desempenho de contêineres](./media/log-analytics-containers/containers-perf01.png)

<span data-ttu-id="ecced-459">Você pode definir o escopo de dados de desempenho de saudação que você esteja vendo contêiner específico tooa digitando o nome hello dele toohello à direita da sua consulta.</span><span class="sxs-lookup"><span data-stu-id="ecced-459">You can scope hello performance data you're seeing tooa specific container by typing hello name of it toohello right of your query.</span></span>

```
Type=Perf <containerName>
```

<span data-ttu-id="ecced-460">Que mostra a lista de saudação de métricas de desempenho são coletadas para um contêiner individual.</span><span class="sxs-lookup"><span data-stu-id="ecced-460">That shows hello list of performance metrics that are collected for an individual container.</span></span>

![desempenho de contêineres](./media/log-analytics-containers/containers-perf03.png)

## <a name="example-log-search-queries"></a><span data-ttu-id="ecced-462">Exemplo de consultas de pesquisa de log</span><span class="sxs-lookup"><span data-stu-id="ecced-462">Example log search queries</span></span>
<span data-ttu-id="ecced-463">É geralmente útil toobuild consulta começando com um ou dois exemplos e, em seguida, modificá-los toofit seu ambiente.</span><span class="sxs-lookup"><span data-stu-id="ecced-463">It's often useful toobuild queries starting with an example or two and then modifying them toofit your environment.</span></span> <span data-ttu-id="ecced-464">Como ponto de partida, você pode experimentar Olá **exemplos de consultas** toohelp área criar consultas mais avançadas.</span><span class="sxs-lookup"><span data-stu-id="ecced-464">As a starting point, you can experiment with hello **Sample Queries** area toohelp you build more advanced queries.</span></span>

[!include[log-analytics-log-search-nextgeneration](../../includes/log-analytics-log-search-nextgeneration.md)]

![Consultas de contêineres](./media/log-analytics-containers/containers-queries.png)


## <a name="saving-log-search-queries"></a><span data-ttu-id="ecced-466">Salvando as consultas de pesquisa de log</span><span class="sxs-lookup"><span data-stu-id="ecced-466">Saving log search queries</span></span>
<span data-ttu-id="ecced-467">Salvar consultas é um recurso padrão do Log Analytics.</span><span class="sxs-lookup"><span data-stu-id="ecced-467">Saving queries is a standard feature in Log Analytics.</span></span> <span data-ttu-id="ecced-468">Ao salvá-las, você terá aquelas que considerou úteis acessíveis para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="ecced-468">By saving them, you'll have those that you've found useful handy for future use.</span></span>

<span data-ttu-id="ecced-469">Depois de criar uma consulta que sejam úteis, salvá-lo clicando em **Favoritos** na parte superior de saudação da página de pesquisa de Log de saudação.</span><span class="sxs-lookup"><span data-stu-id="ecced-469">After you create a query that you find useful, save it by clicking **Favorites** at hello top of hello Log Search page.</span></span> <span data-ttu-id="ecced-470">Em seguida, você pode acessá-lo facilmente mais tarde da saudação **meu painel** página.</span><span class="sxs-lookup"><span data-stu-id="ecced-470">Then you can easily access it later from hello **My Dashboard** page.</span></span>

## <a name="next-steps"></a><span data-ttu-id="ecced-471">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ecced-471">Next steps</span></span>
* <span data-ttu-id="ecced-472">[Pesquisar logs](log-analytics-log-searches.md) tooview detalhadas registros de dados de contêiner.</span><span class="sxs-lookup"><span data-stu-id="ecced-472">[Search logs](log-analytics-log-searches.md) tooview detailed container data records.</span></span>
