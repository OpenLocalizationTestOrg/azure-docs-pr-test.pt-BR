---
title: "Máquinas virtuais alta disponibilidade para o SAP NetWeaver no SUSE Linux Enterprise Server para aplicativos SAP de aaaAzure | Microsoft Docs"
description: Guia de alta disponibilidade do SAP NetWeaver no SUSE Linux Enterprise Server para aplicativos SAP
services: virtual-machines-windows,virtual-network,storage
documentationcenter: saponazure
author: mssedusch
manager: timlt
editor: 
tags: azure-resource-manager
keywords: 
ms.assetid: 5e514964-c907-4324-b659-16dd825f6f87
ms.service: virtual-machines-windows
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: infrastructure-services
ms.date: 04/27/2017
ms.author: sedusch
ms.openlocfilehash: e944103df92d5ffec9196189f138e25972bea79f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="c66f3-103">Alta disponibilidade do SAP NetWeaver em VMs do Azure no SUSE Linux Enterprise Server para aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="c66f3-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

[2205917]:https://launchpad.support.sap.com/#/notes/2205917
[1944799]:https://launchpad.support.sap.com/#/notes/1944799
[1928533]:https://launchpad.support.sap.com/#/notes/1928533
[2015553]:https://launchpad.support.sap.com/#/notes/2015553
[2178632]:https://launchpad.support.sap.com/#/notes/2178632
[2191498]:https://launchpad.support.sap.com/#/notes/2191498
[2243692]:https://launchpad.support.sap.com/#/notes/2243692
[1984787]:https://launchpad.support.sap.com/#/notes/1984787
[1999351]:https://launchpad.support.sap.com/#/notes/1999351
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="c66f3-113">Este artigo descreve como máquinas virtuais do toodeploy Olá, configurar máquinas virtuais de hello, instalar o framework de cluster hello e instalar um sistema SAP NetWeaver 7,50 altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="c66f3-113">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="c66f3-114">Em configurações de exemplo hello, comandos de instalação etc. A instância do ASCS número 00, a número da instância do ERS 02 e o NWS de ID do sistema SAP são usados.</span><span class="sxs-lookup"><span data-stu-id="c66f3-114">In hello example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="c66f3-115">Olá nomes de recursos de saudação (por exemplo, máquinas virtuais, redes virtuais) no exemplo hello pressupõem que você usou Olá [convergido modelo] [ template-converged] com recursos de saudação do SAP sistema ID NWS toocreate.</span><span class="sxs-lookup"><span data-stu-id="c66f3-115">hello names of hello resources (for example virtual machines, virtual networks) in hello example assume that you have used hello [converged template][template-converged] with SAP system ID NWS toocreate hello resources.</span></span>

<span data-ttu-id="c66f3-116">Saudação de leitura a seguir observações sobre o SAP e documentos primeiro</span><span class="sxs-lookup"><span data-stu-id="c66f3-116">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="c66f3-117">A Nota SAP [1928533], que tem:</span><span class="sxs-lookup"><span data-stu-id="c66f3-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="c66f3-118">Lista de tamanhos de VM do Azure que têm suporte para implantação de saudação do software SAP</span><span class="sxs-lookup"><span data-stu-id="c66f3-118">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="c66f3-119">Informações importantes sobre capacidade para tamanhos de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="c66f3-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="c66f3-120">Software SAP e combinações de SO (sistema operacional) e banco de dados com suporte</span><span class="sxs-lookup"><span data-stu-id="c66f3-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="c66f3-121">A versão do kernel do SAP necessária para Windows e para Linux no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="c66f3-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="c66f3-122">A Nota SAP [2015553] lista pré-requisitos para implantações de software SAP com suporte do SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="c66f3-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="c66f3-123">A Nota SAP [2205917] tem configurações de SO recomendadas para SUSE Linux Enterprise Server para aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="c66f3-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="c66f3-124">A Nota SAP [1944799] tem Diretrizes SAP HANA para SUSE Linux Enterprise Server para aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="c66f3-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="c66f3-125">A Nota SAP [2178632] contém informações detalhadas sobre todas as métricas de monitoramentos relatadas para o SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="c66f3-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="c66f3-126">Nota da SAP [2191498] Olá exigiu versão SAP Host Agent para Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="c66f3-126">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="c66f3-127">A Nota SAP [2243692] tem informações sobre o licenciamento do SAP no Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="c66f3-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="c66f3-128">A Nota SAP [1984787] tem informações gerais sobre o SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="c66f3-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="c66f3-129">Nota da SAP [1999351] tem informações adicionais de solução de problemas para hello Azure extensão de monitoramento aprimorada para SAP.</span><span class="sxs-lookup"><span data-stu-id="c66f3-129">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="c66f3-130">[WIKI da comunidade do SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) tem todas as Notas SAP necessárias para Linux.</span><span class="sxs-lookup"><span data-stu-id="c66f3-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="c66f3-131">[Planejamento e implementação de Máquinas Virtuais do Azure para SAP no Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="c66f3-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="c66f3-132">[Implantação de máquinas virtuais do Azure para SAP no Linux (este artigo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="c66f3-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="c66f3-133">[Implantação de Máquinas Virtuais do Azure do DBMS para SAP no Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="c66f3-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="c66f3-134">[Cenário otimizado para desempenho da SR SAP HANA][suse-hana-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="c66f3-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="c66f3-135">Guia de saudação contém tooset de todas as informações necessárias a replicação de sistema do SAP HANA local.</span><span class="sxs-lookup"><span data-stu-id="c66f3-135">hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="c66f3-136">Use este guia como uma linha de base.</span><span class="sxs-lookup"><span data-stu-id="c66f3-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="c66f3-137">[Armazenamento de NFS altamente disponível com DRBD e Pacemaker] [ suse-drbd-guide] guia Olá contém todos os tooset as informações necessárias a um servidor NFS altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="c66f3-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] hello guide contains all required information tooset up a highly available NFS server.</span></span> <span data-ttu-id="c66f3-138">Use este guia como uma linha de base.</span><span class="sxs-lookup"><span data-stu-id="c66f3-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="c66f3-139">Visão geral</span><span class="sxs-lookup"><span data-stu-id="c66f3-139">Overview</span></span>

<span data-ttu-id="c66f3-140">alta disponibilidade tooachieve, SAP NetWeaver requer um servidor NFS.</span><span class="sxs-lookup"><span data-stu-id="c66f3-140">tooachieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="c66f3-141">Olá servidor é configurado em um cluster separado e pode ser usado por vários sistemas SAP.</span><span class="sxs-lookup"><span data-stu-id="c66f3-141">hello NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![Visão geral da Alta Disponibilidade do SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="c66f3-143">Olá servidor NFS, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver es e banco de dados do SAP HANA Olá usar nome de máquina virtual e endereços IP virtuais.</span><span class="sxs-lookup"><span data-stu-id="c66f3-143">hello NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and hello SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="c66f3-144">No Azure, um balanceador de carga é necessário toouse um endereço IP virtual.</span><span class="sxs-lookup"><span data-stu-id="c66f3-144">On Azure, a load balancer is required toouse a virtual IP address.</span></span> <span data-ttu-id="c66f3-145">Olá lista a seguir mostra a configuração Olá Olá do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="c66f3-145">hello following list shows hello configuration of hello load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="c66f3-146">Servidor NFS</span><span class="sxs-lookup"><span data-stu-id="c66f3-146">NFS Server</span></span>
* <span data-ttu-id="c66f3-147">Configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="c66f3-147">Frontend configuration</span></span>
  * <span data-ttu-id="c66f3-148">Endereço IP 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="c66f3-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="c66f3-149">Configuração de back-end</span><span class="sxs-lookup"><span data-stu-id="c66f3-149">Backend configuration</span></span>
  * <span data-ttu-id="c66f3-150">Conectado tooprimary interfaces de rede de todas as máquinas virtuais que devem fazer parte do cluster NFS Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-150">Connected tooprimary network interfaces of all virtual machines that should be part of hello NFS cluster</span></span>
* <span data-ttu-id="c66f3-151">Porta de Investigação</span><span class="sxs-lookup"><span data-stu-id="c66f3-151">Probe Port</span></span>
  * <span data-ttu-id="c66f3-152">Porta 61000</span><span class="sxs-lookup"><span data-stu-id="c66f3-152">Port 61000</span></span>
* <span data-ttu-id="c66f3-153">Regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="c66f3-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="c66f3-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-154">2049 TCP</span></span> 
  * <span data-ttu-id="c66f3-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="c66f3-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="c66f3-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="c66f3-156">(A)SCS</span></span>
* <span data-ttu-id="c66f3-157">Configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="c66f3-157">Frontend configuration</span></span>
  * <span data-ttu-id="c66f3-158">Endereço IP 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="c66f3-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="c66f3-159">Configuração de back-end</span><span class="sxs-lookup"><span data-stu-id="c66f3-159">Backend configuration</span></span>
  * <span data-ttu-id="c66f3-160">Interfaces de rede conectados tooprimary de todas as máquinas virtuais que devem ser parte de saudação (A) SCS/es cluster</span><span class="sxs-lookup"><span data-stu-id="c66f3-160">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="c66f3-161">Porta de Investigação</span><span class="sxs-lookup"><span data-stu-id="c66f3-161">Probe Port</span></span>
  * <span data-ttu-id="c66f3-162">Porta 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="c66f3-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="c66f3-163">Regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="c66f3-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="c66f3-164">32**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="c66f3-165">36**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="c66f3-166">39**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="c66f3-167">81**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="c66f3-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="c66f3-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="c66f3-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="c66f3-171">ERS</span><span class="sxs-lookup"><span data-stu-id="c66f3-171">ERS</span></span>
* <span data-ttu-id="c66f3-172">Configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="c66f3-172">Frontend configuration</span></span>
  * <span data-ttu-id="c66f3-173">Endereço IP 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="c66f3-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="c66f3-174">Configuração de back-end</span><span class="sxs-lookup"><span data-stu-id="c66f3-174">Backend configuration</span></span>
  * <span data-ttu-id="c66f3-175">Interfaces de rede conectados tooprimary de todas as máquinas virtuais que devem ser parte de saudação (A) SCS/es cluster</span><span class="sxs-lookup"><span data-stu-id="c66f3-175">Connected tooprimary network interfaces of all virtual machines that should be part of hello (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="c66f3-176">Porta de Investigação</span><span class="sxs-lookup"><span data-stu-id="c66f3-176">Probe Port</span></span>
  * <span data-ttu-id="c66f3-177">Porta 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="c66f3-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="c66f3-178">Regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="c66f3-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="c66f3-179">33**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="c66f3-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="c66f3-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="c66f3-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="c66f3-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="c66f3-183">SAP HANA</span></span>
* <span data-ttu-id="c66f3-184">Configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="c66f3-184">Frontend configuration</span></span>
  * <span data-ttu-id="c66f3-185">Endereço IP 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="c66f3-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="c66f3-186">Configuração de back-end</span><span class="sxs-lookup"><span data-stu-id="c66f3-186">Backend configuration</span></span>
  * <span data-ttu-id="c66f3-187">Conectado tooprimary interfaces de rede de todas as máquinas virtuais que devem fazer parte do cluster do HANA Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-187">Connected tooprimary network interfaces of all virtual machines that should be part of hello HANA cluster</span></span>
* <span data-ttu-id="c66f3-188">Porta de Investigação</span><span class="sxs-lookup"><span data-stu-id="c66f3-188">Probe Port</span></span>
  * <span data-ttu-id="c66f3-189">Porta 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="c66f3-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="c66f3-190">Regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="c66f3-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="c66f3-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="c66f3-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="c66f3-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="c66f3-193">Configuração de um servidor NFS altamente disponível</span><span class="sxs-lookup"><span data-stu-id="c66f3-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="c66f3-194">Implantação do Linux</span><span class="sxs-lookup"><span data-stu-id="c66f3-194">Deploying Linux</span></span>

<span data-ttu-id="c66f3-195">Hello Azure Marketplace contém uma imagem para SUSE Linux Enterprise Server para 12 de aplicativos SAP que você pode usar máquinas virtuais da nova toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c66f3-195">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span>
<span data-ttu-id="c66f3-196">Você pode usar um dos modelos de início rápido de saudação no github toodeploy todos os recursos necessários.</span><span class="sxs-lookup"><span data-stu-id="c66f3-196">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="c66f3-197">modelo de saudação implanta máquinas virtuais de saudação, o balanceador de carga hello, disponibilidade definida etc. Siga o modelo de saudação de toodeploy essas etapas:</span><span class="sxs-lookup"><span data-stu-id="c66f3-197">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="c66f3-198">Olá abrir [modelo de servidor de arquivo do SAP] [ template-file-server] em Olá portal do Azure</span><span class="sxs-lookup"><span data-stu-id="c66f3-198">Open hello [SAP file server template][template-file-server] in hello Azure portal</span></span>   
1. <span data-ttu-id="c66f3-199">Digite hello parâmetros a seguir</span><span class="sxs-lookup"><span data-stu-id="c66f3-199">Enter hello following parameters</span></span>
   1. <span data-ttu-id="c66f3-200">Prefixo de recursos</span><span class="sxs-lookup"><span data-stu-id="c66f3-200">Resource Prefix</span></span>  
      <span data-ttu-id="c66f3-201">Insira o prefixo Olá deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="c66f3-201">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="c66f3-202">valor de saudação é usado como um prefixo para recursos de saudação que são implantados.</span><span class="sxs-lookup"><span data-stu-id="c66f3-202">hello value is used as a prefix for hello resources that are deployed.</span></span>
   2. <span data-ttu-id="c66f3-203">Tipo de sistema operacional</span><span class="sxs-lookup"><span data-stu-id="c66f3-203">Os Type</span></span>  
      <span data-ttu-id="c66f3-204">Selecione uma saudação distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="c66f3-204">Select one of hello Linux distributions.</span></span> <span data-ttu-id="c66f3-205">Para este exemplo, selecione SLES 12</span><span class="sxs-lookup"><span data-stu-id="c66f3-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="c66f3-206">Nome de Usuário de Administrador e Senha do Administrador</span><span class="sxs-lookup"><span data-stu-id="c66f3-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="c66f3-207">Um novo usuário é criado que pode ser usado toolog toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="c66f3-207">A new user is created that can be used toolog on toohello machine.</span></span>
   4. <span data-ttu-id="c66f3-208">ID da Sub-rede</span><span class="sxs-lookup"><span data-stu-id="c66f3-208">Subnet Id</span></span>  
      <span data-ttu-id="c66f3-209">Olá ID das máquinas virtuais do hello sub-rede toowhich Olá deve ser conectado ao.</span><span class="sxs-lookup"><span data-stu-id="c66f3-209">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="c66f3-210">Deixe em branco se você desejar toocreate uma nova rede virtual ou selecione Olá sub-rede de sua VPN ou rota expressa rede virtual tooconnect Olá máquina virtual tooyour na rede local.</span><span class="sxs-lookup"><span data-stu-id="c66f3-210">Leave empty if you want toocreate a new virtual network or select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="c66f3-211">Olá ID geralmente parece com /subscriptions/**&lt;id da assinatura&gt;**/resourceGroups/**&lt;nome do grupo de recursos&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nome de rede virtual&gt;**/subnets/**&lt;nome da sub-rede&gt;**</span><span class="sxs-lookup"><span data-stu-id="c66f3-211">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="c66f3-212">Instalação</span><span class="sxs-lookup"><span data-stu-id="c66f3-212">Installation</span></span>

<span data-ttu-id="c66f3-213">Olá itens a seguir são prefixados com um **[A]** -nós tooall aplicável, **[1]** -toonode aplicável apenas 1 ou **[2]** -somente aplicável toonode 2.</span><span class="sxs-lookup"><span data-stu-id="c66f3-213">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="c66f3-214">**[A]** Atualizar o SLES</span><span class="sxs-lookup"><span data-stu-id="c66f3-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="c66f3-215">**[1]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="c66f3-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="c66f3-216">**[2]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="c66f3-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="c66f3-217">**[1]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="c66f3-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="c66f3-218">**[A]** Instalar a extensão HA</span><span class="sxs-lookup"><span data-stu-id="c66f3-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="c66f3-219">**[A]** Configurar a resolução de nome do host</span><span class="sxs-lookup"><span data-stu-id="c66f3-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="c66f3-220">Você pode usar um servidor DNS ou modificar /etc/hosts Olá em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="c66f3-220">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="c66f3-221">Este exemplo mostra como toouse Olá arquivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="c66f3-221">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="c66f3-222">Substituir endereço IP de saudação e nome de host Olá no hello comandos a seguir</span><span class="sxs-lookup"><span data-stu-id="c66f3-222">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="c66f3-223">Inserir saudação linhas muito/etc/hosts a seguir.</span><span class="sxs-lookup"><span data-stu-id="c66f3-223">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="c66f3-224">Alterar o ambiente de saudação IP toomatch de endereço e o nome do host</span><span class="sxs-lookup"><span data-stu-id="c66f3-224">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="c66f3-225">**[1]** Instalar o Cluster</span><span class="sxs-lookup"><span data-stu-id="c66f3-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="c66f3-226">**[2]**  Adicionar nó toocluster</span><span class="sxs-lookup"><span data-stu-id="c66f3-226">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="c66f3-227">**[A]**  Alteração hacluster senha toohello mesma senha</span><span class="sxs-lookup"><span data-stu-id="c66f3-227">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="c66f3-228">**[A]**  Configurar corosync toouse outro transporte e adicionar nodelist.</span><span class="sxs-lookup"><span data-stu-id="c66f3-228">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="c66f3-229">Caso contrário, o cluster não funcionará.</span><span class="sxs-lookup"><span data-stu-id="c66f3-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="c66f3-230">Adicione Olá negrito toohello conteúdo de arquivo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c66f3-230">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>prod-nfs-0</b>
      ring0_addr:10.0.0.5
     }
     node {
      # IP address of <b>prod-nfs-1</b>
      ring0_addr:10.0.0.6
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="c66f3-231">Em seguida, reinicie o serviço de corosync Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-231">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="c66f3-232">**[A]** Instalar componentes drbd</span><span class="sxs-lookup"><span data-stu-id="c66f3-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="c66f3-233">**[A]**  Criar uma partição para o dispositivo de drbd Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-233">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="c66f3-234">**[A]** Criar configurações de LVM</span><span class="sxs-lookup"><span data-stu-id="c66f3-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="c66f3-235">**[A]**  Dispositivo de drbd criar hello NFS</span><span class="sxs-lookup"><span data-stu-id="c66f3-235">**[A]** Create hello NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="c66f3-236">Inserir configuração Olá para o novo dispositivo de drbd hello e sair</span><span class="sxs-lookup"><span data-stu-id="c66f3-236">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_nfs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>prod-nfs-0</b> {
         address   <b>10.0.0.5</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
      on <b>prod-nfs-1</b> {
         address   <b>10.0.0.6</b>:7790;
         device    /dev/drbd0;
         disk      /dev/vg_NFS/NWS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="c66f3-237">Criar um dispositivo drbd hello e iniciá-lo</span><span class="sxs-lookup"><span data-stu-id="c66f3-237">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="c66f3-238">**[1]** Ignorar a sincronização inicial</span><span class="sxs-lookup"><span data-stu-id="c66f3-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="c66f3-239">**[1]**  Nó primário do conjunto Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-239">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="c66f3-240">**[1]**  Aguarde até que novos dispositivos de drbd Olá são sincronizados</span><span class="sxs-lookup"><span data-stu-id="c66f3-240">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="c66f3-241">**[1]**  Criar sistemas de arquivos no hello drbd dispositivos</span><span class="sxs-lookup"><span data-stu-id="c66f3-241">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="c66f3-242">Configurar a estrutura do cluster</span><span class="sxs-lookup"><span data-stu-id="c66f3-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="c66f3-243">**[1]**  Alterar as configurações padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="c66f3-243">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="c66f3-244">**[1]**  Configuração de cluster Adicionar Olá NFS drbd dispositivo toohello</span><span class="sxs-lookup"><span data-stu-id="c66f3-244">**[1]** Add hello NFS drbd device toohello cluster configuration</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_nfs \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_nfs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_nfs drbd_<b>NWS</b>_nfs \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="c66f3-245">**[1]**  Servidor criar Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-245">**[1]** Create hello NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="c66f3-246">**[1]**  Criar recursos de sistema de arquivos NFS Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-246">**[1]** Create hello NFS File System resources</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive fs_<b>NWS</b>_sapmnt \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/srv/nfs/<b>NWS</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# group g-<b>NWS</b>_nfs fs_<b>NWS</b>_sapmnt

   crm(live)configure# order o-<b>NWS</b>_drbd_before_nfs inf: \
     ms-drbd_<b>NWS</b>_nfs:promote g-<b>NWS</b>_nfs:start
   
   crm(live)configure# colocation col-<b>NWS</b>_nfs_on_drbd inf: \
     g-<b>NWS</b>_nfs ms-drbd_<b>NWS</b>_nfs:Master

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="c66f3-247">**[1]**  Criar hello exportações NFS</span><span class="sxs-lookup"><span data-stu-id="c66f3-247">**[1]** Create hello NFS exports</span></span>

   <pre><code>
   sudo mkdir /srv/nfs/<b>NWS</b>/sidsys
   sudo mkdir /srv/nfs/<b>NWS</b>/sapmntsid
   sudo mkdir /srv/nfs/<b>NWS</b>/trans

   sudo crm configure

   crm(live)configure# primitive exportfs_<b>NWS</b> \
     ocf:heartbeat:exportfs \
     params directory="/srv/nfs/<b>NWS</b>" \
     options="rw,no_root_squash" \
     clientspec="*" fsid=0 \
     wait_for_leasetime_on_stop=true \
     op monitor interval="30s"

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add exportfs_<b>NWS</b>

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="c66f3-248">**[1]**  Criar um recurso IP virtual e a investigação de integridade para o balanceador de carga interno Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-248">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive vip_<b>NWS</b>_nfs IPaddr2 \
     params ip=<b>10.0.0.4</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_nfs anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 610<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0

   crm(live)configure# modgroup g-<b>NWS</b>_nfs add nc_<b>NWS</b>_nfs
   crm(live)configure# modgroup g-<b>NWS</b>_nfs add vip_<b>NWS</b>_nfs

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="c66f3-249">Criar dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="c66f3-249">Create STONITH device</span></span>

<span data-ttu-id="c66f3-250">dispositivo STONITH Olá usa tooauthorize uma entidade de serviço no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c66f3-250">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="c66f3-251">Siga essas etapas toocreate uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="c66f3-251">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="c66f3-252">Vá muito<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="c66f3-252">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="c66f3-253">Folha de Active Directory do Azure Olá aberto</span><span class="sxs-lookup"><span data-stu-id="c66f3-253">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="c66f3-254">Vá tooProperties e anote Olá ID de diretório. Isso é hello **id de locatário**.</span><span class="sxs-lookup"><span data-stu-id="c66f3-254">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="c66f3-255">Clique em Registros do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="c66f3-255">Click App registrations</span></span>
1. <span data-ttu-id="c66f3-256">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="c66f3-256">Click Add</span></span>
1. <span data-ttu-id="c66f3-257">Digite um Nome, selecione Tipo de Aplicativo "Aplicativo Web/API", insira uma URL de logon (por exemplo, http://localhost) e clique em Criar</span><span class="sxs-lookup"><span data-stu-id="c66f3-257">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="c66f3-258">URL de entrada Hello não é usado e pode ser qualquer URL válido</span><span class="sxs-lookup"><span data-stu-id="c66f3-258">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="c66f3-259">Selecione Olá novo aplicativo e clique em chaves no guia de configurações de saudação</span><span class="sxs-lookup"><span data-stu-id="c66f3-259">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="c66f3-260">Insira uma descrição para uma nova chave, selecione "Nunca expira" e clique em Salvar</span><span class="sxs-lookup"><span data-stu-id="c66f3-260">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="c66f3-261">Anote o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66f3-261">Write down hello Value.</span></span> <span data-ttu-id="c66f3-262">Ele é usado como Olá **senha** para Olá entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="c66f3-262">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="c66f3-263">Anote a saudação ID do aplicativo. Ele é usado como Olá username (**id de logon** nas etapas de saudação abaixo) de saudação entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="c66f3-263">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="c66f3-264">Olá entidade de serviço não tem permissões tooaccess seus recursos do Azure por padrão.</span><span class="sxs-lookup"><span data-stu-id="c66f3-264">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="c66f3-265">Você precisa toogive toostart de permissões de entidade de serviço de saudação e parar (desalocar) todas as máquinas virtuais do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c66f3-265">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="c66f3-266">Vá toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="c66f3-266">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="c66f3-267">Abrir Olá folha de todos os recursos</span><span class="sxs-lookup"><span data-stu-id="c66f3-267">Open hello All resources blade</span></span>
1. <span data-ttu-id="c66f3-268">Selecione a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="c66f3-268">Select hello virtual machine</span></span>
1. <span data-ttu-id="c66f3-269">Clique em Controle de acesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="c66f3-269">Click Access control (IAM)</span></span>
1. <span data-ttu-id="c66f3-270">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="c66f3-270">Click Add</span></span>
1. <span data-ttu-id="c66f3-271">Selecione a função hello proprietário</span><span class="sxs-lookup"><span data-stu-id="c66f3-271">Select hello role Owner</span></span>
1. <span data-ttu-id="c66f3-272">Insira nome de saudação do aplicativo hello criado acima</span><span class="sxs-lookup"><span data-stu-id="c66f3-272">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="c66f3-273">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="c66f3-273">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="c66f3-274">**[1]**  Criar hello STONITH dispositivos</span><span class="sxs-lookup"><span data-stu-id="c66f3-274">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="c66f3-275">Depois de editar permissões Olá para máquinas virtuais de hello, você pode configurar dispositivos STONITH de saudação em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c66f3-275">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="c66f3-276">**[1]**  Habilitar o uso de saudação de um dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="c66f3-276">**[1]** Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="c66f3-277">Configuração do (A)SCS</span><span class="sxs-lookup"><span data-stu-id="c66f3-277">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="c66f3-278">Implantação do Linux</span><span class="sxs-lookup"><span data-stu-id="c66f3-278">Deploying Linux</span></span>

<span data-ttu-id="c66f3-279">Hello Azure Marketplace contém uma imagem para SUSE Linux Enterprise Server para 12 de aplicativos SAP que você pode usar máquinas virtuais da nova toodeploy.</span><span class="sxs-lookup"><span data-stu-id="c66f3-279">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use toodeploy new virtual machines.</span></span> <span data-ttu-id="c66f3-280">imagem do marketplace Olá contém agente de recurso Olá para SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="c66f3-280">hello marketplace image contains hello resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="c66f3-281">Você pode usar um dos modelos de início rápido de saudação no github toodeploy todos os recursos necessários.</span><span class="sxs-lookup"><span data-stu-id="c66f3-281">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="c66f3-282">modelo de saudação implanta máquinas virtuais de saudação, o balanceador de carga hello, disponibilidade definida etc. Siga o modelo de saudação de toodeploy essas etapas:</span><span class="sxs-lookup"><span data-stu-id="c66f3-282">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="c66f3-283">Olá abrir [modelo ASCS/SCS várias SID] [ template-multisid-xscs] ou hello [convergido modelo] [ template-converged] em Olá Olá portal do Azure ASCS/SCS somente modelo cria regras de balanceamento de carga de saudação para hello ASCS/SCS do SAP NetWeaver e instâncias de ES (Linux) enquanto o modelo convergida Olá também cria regras de balanceamento de carga Olá para um banco de dados (por exemplo, Microsoft SQL Server ou SAP HANA).</span><span class="sxs-lookup"><span data-stu-id="c66f3-283">Open hello [ASCS/SCS Multi SID template][template-multisid-xscs] or hello [converged template][template-converged] on hello Azure portal hello ASCS/SCS template only creates hello load-balancing rules for hello SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas hello converged template also creates hello load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="c66f3-284">Se você planejar tooinstall um sistema baseados no SAP NetWeaver e você deseja que o banco de dados do tooinstall Olá na Olá mesmas máquinas, use Olá [convergido modelo][template-converged].</span><span class="sxs-lookup"><span data-stu-id="c66f3-284">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello database on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="c66f3-285">Digite hello parâmetros a seguir</span><span class="sxs-lookup"><span data-stu-id="c66f3-285">Enter hello following parameters</span></span>
   1. <span data-ttu-id="c66f3-286">Prefixo de recurso (somente modelo multi-SID do ASCS/SCS)</span><span class="sxs-lookup"><span data-stu-id="c66f3-286">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="c66f3-287">Insira o prefixo Olá deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="c66f3-287">Enter hello prefix you want toouse.</span></span> <span data-ttu-id="c66f3-288">valor de saudação é usado como um prefixo para recursos de saudação que são implantados.</span><span class="sxs-lookup"><span data-stu-id="c66f3-288">hello value is used as a prefix for hello resources that are deployed.</span></span>
   3. <span data-ttu-id="c66f3-289">ID do sistema SAP (somente modelo convergido)</span><span class="sxs-lookup"><span data-stu-id="c66f3-289">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="c66f3-290">Insira o sistema SAP de hello, Id de saudação sistema SAP que você deseja tooinstall.</span><span class="sxs-lookup"><span data-stu-id="c66f3-290">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="c66f3-291">Olá Id é usado como um prefixo para recursos de saudação que são implantados.</span><span class="sxs-lookup"><span data-stu-id="c66f3-291">hello Id is used as a prefix for hello resources that are deployed.</span></span>
   4. <span data-ttu-id="c66f3-292">Tipo de Pilha</span><span class="sxs-lookup"><span data-stu-id="c66f3-292">Stack Type</span></span>  
      <span data-ttu-id="c66f3-293">Selecione o tipo de pilha do SAP NetWeaver Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-293">Select hello SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="c66f3-294">Tipo de sistema operacional</span><span class="sxs-lookup"><span data-stu-id="c66f3-294">Os Type</span></span>  
      <span data-ttu-id="c66f3-295">Selecione uma saudação distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="c66f3-295">Select one of hello Linux distributions.</span></span> <span data-ttu-id="c66f3-296">Para este exemplo, selecione SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="c66f3-296">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="c66f3-297">Tipo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="c66f3-297">Db Type</span></span>  
      <span data-ttu-id="c66f3-298">Selecionar HANA</span><span class="sxs-lookup"><span data-stu-id="c66f3-298">Select HANA</span></span>
   7. <span data-ttu-id="c66f3-299">Tamanho do sistema SAP</span><span class="sxs-lookup"><span data-stu-id="c66f3-299">Sap System Size</span></span>  
      <span data-ttu-id="c66f3-300">quantidade de saudação do sistema novo do SAPS Olá fornece.</span><span class="sxs-lookup"><span data-stu-id="c66f3-300">hello amount of SAPS hello new system provides.</span></span> <span data-ttu-id="c66f3-301">Se não tiver certeza do sistema de saudação SAPS quantos requer, peça ao seu parceiro de tecnologia do SAP ou o integrador de sistema</span><span class="sxs-lookup"><span data-stu-id="c66f3-301">If you are not sure how many SAPS hello system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="c66f3-302">Disponibilidade do sistema</span><span class="sxs-lookup"><span data-stu-id="c66f3-302">System Availability</span></span>  
      <span data-ttu-id="c66f3-303">Selecione HA</span><span class="sxs-lookup"><span data-stu-id="c66f3-303">Select HA</span></span>
   9. <span data-ttu-id="c66f3-304">Nome de Usuário de Administrador e Senha do Administrador</span><span class="sxs-lookup"><span data-stu-id="c66f3-304">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="c66f3-305">Um novo usuário é criado que pode ser usado toolog toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="c66f3-305">A new user is created that can be used toolog on toohello machine.</span></span>
   10. <span data-ttu-id="c66f3-306">ID da Sub-rede</span><span class="sxs-lookup"><span data-stu-id="c66f3-306">Subnet Id</span></span>  
   <span data-ttu-id="c66f3-307">Olá ID das máquinas virtuais do hello sub-rede toowhich Olá deve ser conectado ao.</span><span class="sxs-lookup"><span data-stu-id="c66f3-307">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span>  <span data-ttu-id="c66f3-308">Deixe em branco se você quiser toocreate uma nova rede virtual ou selecione Olá mesma sub-rede que é usado ou criado como parte da implantação do servidor NFS hello.</span><span class="sxs-lookup"><span data-stu-id="c66f3-308">Leave empty if you want toocreate a new virtual network or select hello same subnet that you used or created as part of hello NFS server deployment.</span></span> <span data-ttu-id="c66f3-309">Olá ID geralmente parece com /subscriptions/**&lt;id da assinatura&gt;**/resourceGroups/**&lt;nome do grupo de recursos&gt;**/providers/ Microsoft.Network/virtualNetworks/**&lt;nome de rede virtual&gt;**/subnets/**&lt;nome da sub-rede&gt;**</span><span class="sxs-lookup"><span data-stu-id="c66f3-309">hello ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="c66f3-310">Instalação</span><span class="sxs-lookup"><span data-stu-id="c66f3-310">Installation</span></span>

<span data-ttu-id="c66f3-311">Olá itens a seguir são prefixados com um **[A]** -nós tooall aplicável, **[1]** -toonode aplicável apenas 1 ou **[2]** -somente aplicável toonode 2.</span><span class="sxs-lookup"><span data-stu-id="c66f3-311">hello following items are prefixed with either **[A]** - applicable tooall nodes, **[1]** - only applicable toonode 1 or **[2]** - only applicable toonode 2.</span></span>

1. <span data-ttu-id="c66f3-312">**[A]** Atualizar o SLES</span><span class="sxs-lookup"><span data-stu-id="c66f3-312">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="c66f3-313">**[1]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="c66f3-313">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="c66f3-314">**[2]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="c66f3-314">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy hello public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="c66f3-315">**[1]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="c66f3-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="c66f3-316">**[A]** Instalar a extensão HA</span><span class="sxs-lookup"><span data-stu-id="c66f3-316">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="c66f3-317">**[A]** Atualizar agentes de recurso SAP</span><span class="sxs-lookup"><span data-stu-id="c66f3-317">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="c66f3-318">Um patch para o pacote de recursos agentes Olá é necessário toouse Olá nova configuração, que é descrita neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c66f3-318">A patch for hello resource-agents package is required toouse hello new configuration, that is described in this article.</span></span> <span data-ttu-id="c66f3-319">Você pode verificar, se o patch de saudação já está instalado com o comando a seguir de saudação</span><span class="sxs-lookup"><span data-stu-id="c66f3-319">You can check, if hello patch is already installed with hello following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="c66f3-320">saída de Hello deve ser semelhante a</span><span class="sxs-lookup"><span data-stu-id="c66f3-320">hello output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="c66f3-321">Se o comando grep de saudação não encontrar o parâmetro IS_ERS hello, você precisa tooinstall patch de saudação listado em [Olá SUSE página de download](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="c66f3-321">If hello grep command does not find hello IS_ERS parameter, you need tooinstall hello patch listed on [hello SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="c66f3-322">**[A]** Configurar a resolução de nome do host</span><span class="sxs-lookup"><span data-stu-id="c66f3-322">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="c66f3-323">Você pode usar um servidor DNS ou modificar /etc/hosts Olá em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="c66f3-323">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="c66f3-324">Este exemplo mostra como toouse Olá arquivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="c66f3-324">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="c66f3-325">Substituir endereço IP de saudação e nome de host Olá no hello comandos a seguir</span><span class="sxs-lookup"><span data-stu-id="c66f3-325">Replace hello IP address and hello hostname in hello following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="c66f3-326">Inserir saudação linhas muito/etc/hosts a seguir.</span><span class="sxs-lookup"><span data-stu-id="c66f3-326">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="c66f3-327">Alterar o ambiente de saudação IP toomatch de endereço e o nome do host</span><span class="sxs-lookup"><span data-stu-id="c66f3-327">Change hello IP address and hostname toomatch your environment</span></span>   
   
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="c66f3-328">**[1]** Instalar o Cluster</span><span class="sxs-lookup"><span data-stu-id="c66f3-328">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want toocontinue anyway? [y/N] -> y
   # Network address toobind too(for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish toouse SBD? [y/N] -> N
   # Do you wish tooconfigure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="c66f3-329">**[2]**  Adicionar nó toocluster</span><span class="sxs-lookup"><span data-stu-id="c66f3-329">**[2]** Add node toocluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured toostart at system boot.
   # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
   # Do you want toocontinue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="c66f3-330">**[A]**  Alteração hacluster senha toohello mesma senha</span><span class="sxs-lookup"><span data-stu-id="c66f3-330">**[A]** Change hacluster password toohello same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="c66f3-331">**[A]**  Configurar corosync toouse outro transporte e adicionar nodelist.</span><span class="sxs-lookup"><span data-stu-id="c66f3-331">**[A]** Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="c66f3-332">Caso contrário, o cluster não funcionará.</span><span class="sxs-lookup"><span data-stu-id="c66f3-332">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="c66f3-333">Adicione Olá negrito toohello conteúdo de arquivo a seguir.</span><span class="sxs-lookup"><span data-stu-id="c66f3-333">Add hello following bold content toohello file.</span></span>
   
   <pre><code> 
   [...]
     interface { 
        [...] 
     }
     <b>transport:      udpu</b>
   } 
   <b>nodelist {
     node {
      # IP address of <b>nws-cl-0</b>
      ring0_addr:     10.0.0.14
     }
     node {
      # IP address of <b>nws-cl-1</b>
      ring0_addr:     10.0.0.13
     } 
   }</b>
   logging {
     [...]
   </code></pre>

   <span data-ttu-id="c66f3-334">Em seguida, reinicie o serviço de corosync Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-334">Then restart hello corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="c66f3-335">**[A]** Instalar componentes drbd</span><span class="sxs-lookup"><span data-stu-id="c66f3-335">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="c66f3-336">**[A]**  Criar uma partição para o dispositivo de drbd Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-336">**[A]** Create a partition for hello drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="c66f3-337">**[A]** Criar configurações de LVM</span><span class="sxs-lookup"><span data-stu-id="c66f3-337">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="c66f3-338">**[A]**  Dispositivo de drbd criar hello SCS</span><span class="sxs-lookup"><span data-stu-id="c66f3-338">**[A]** Create hello SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="c66f3-339">Inserir configuração Olá para o novo dispositivo de drbd hello e sair</span><span class="sxs-lookup"><span data-stu-id="c66f3-339">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ascs {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7791;
         device    /dev/drbd0;
         disk      /dev/vg_NWS/NWS_ASCS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="c66f3-340">Criar um dispositivo drbd hello e iniciá-lo</span><span class="sxs-lookup"><span data-stu-id="c66f3-340">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="c66f3-341">**[A]**  Dispositivo de drbd criar hello es</span><span class="sxs-lookup"><span data-stu-id="c66f3-341">**[A]** Create hello ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="c66f3-342">Inserir configuração Olá para o novo dispositivo de drbd hello e sair</span><span class="sxs-lookup"><span data-stu-id="c66f3-342">Insert hello configuration for hello new drbd device and exit</span></span>

   <pre><code>
   resource <b>NWS</b>_ers {
      protocol     C;
      disk {
         on-io-error       pass_on;
      }
      on <b>nws-cl-0</b> {
         address   <b>10.0.0.14</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
      on <b>nws-cl-1</b> {
         address   <b>10.0.0.13</b>:7792;
         device    /dev/drbd1;
         disk      /dev/vg_NWS/NWS_ERS;
         meta-disk internal;
      }
   }
   </code></pre>

   <span data-ttu-id="c66f3-343">Criar um dispositivo drbd hello e iniciá-lo</span><span class="sxs-lookup"><span data-stu-id="c66f3-343">Create hello drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="c66f3-344">**[1]** Ignorar a sincronização inicial</span><span class="sxs-lookup"><span data-stu-id="c66f3-344">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="c66f3-345">**[1]**  Nó primário do conjunto Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-345">**[1]** Set hello primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="c66f3-346">**[1]**  Aguarde até que novos dispositivos de drbd Olá são sincronizados</span><span class="sxs-lookup"><span data-stu-id="c66f3-346">**[1]** Wait until hello new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:93991268 nr:0 dw:93991268 dr:93944920 al:383 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 1: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:6047920 nr:0 dw:6047920 dr:6039112 al:34 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   # 2: cs:<b>Connected</b> ro:Primary/Secondary ds:<b>UpToDate/UpToDate</b> C r-----
   #     ns:5142732 nr:0 dw:5142732 dr:5133924 al:30 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="c66f3-347">**[1]**  Criar sistemas de arquivos no hello drbd dispositivos</span><span class="sxs-lookup"><span data-stu-id="c66f3-347">**[1]** Create file systems on hello drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="c66f3-348">Configurar a estrutura do cluster</span><span class="sxs-lookup"><span data-stu-id="c66f3-348">Configure Cluster Framework</span></span>

<span data-ttu-id="c66f3-349">**[1]**  Alterar as configurações padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="c66f3-349">**[1]** Change hello default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="c66f3-350">Preparar para a instalação do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c66f3-350">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="c66f3-351">**[A]**  Saudação criar os diretórios compartilhados</span><span class="sxs-lookup"><span data-stu-id="c66f3-351">**[A]** Create hello shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="c66f3-352">**[A]**  Configurar o autofs</span><span class="sxs-lookup"><span data-stu-id="c66f3-352">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="c66f3-353">Crie um arquivo com</span><span class="sxs-lookup"><span data-stu-id="c66f3-353">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="c66f3-354">Reiniciar autofs toomount novos compartilhamentos Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-354">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="c66f3-355">**[A]** Configurar arquivo de permuta</span><span class="sxs-lookup"><span data-stu-id="c66f3-355">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="c66f3-356">Reiniciar alteração de Olá Olá agente tooactivate</span><span class="sxs-lookup"><span data-stu-id="c66f3-356">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="c66f3-357">Instalação do ASCS/ERS do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c66f3-357">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="c66f3-358">**[1]**  Criar um recurso IP virtual e a investigação de integridade para o balanceador de carga interno Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-358">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ASCS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ascs" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ASCS drbd_<b>NWS</b>_ASCS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ASCS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd0 \
     directory=/usr/sap/<b>NWS</b>/ASCS<b>00</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ASCS IPaddr2 \
     params ip=<b>10.0.0.10</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ASCS anything \
     params binfile="/usr/bin/nc" cmdline_options="-l -k 620<b>00</b>" \
     op monitor timeout=20s interval=10 depth=0
   
   crm(live)configure# group g-<b>NWS</b>_ASCS nc_<b>NWS</b>_ASCS vip_<b>NWS</b>_ASCS fs_<b>NWS</b>_ASCS \
      meta resource-stickiness=3000

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ASCS inf: \
     ms-drbd_<b>NWS</b>_ASCS:promote g-<b>NWS</b>_ASCS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ASCS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ASCS:Master g-<b>NWS</b>_ASCS
   
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="c66f3-359">Certifique-se de que o status de saudação do cluster é okey e que todos os recursos são iniciados.</span><span class="sxs-lookup"><span data-stu-id="c66f3-359">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="c66f3-360">Não é importante em quais recursos de saudação do nó estão em execução.</span><span class="sxs-lookup"><span data-stu-id="c66f3-360">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node nws-cl-1: standby
   # <b>Online: [ nws-cl-0 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      Stopped: [ nws-cl-1 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   </code></pre>

1. <span data-ttu-id="c66f3-361">**[1]** Instalar o ASCS do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c66f3-361">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="c66f3-362">Instalar o SAP NetWeaver ASCS como raiz no primeiro nó de saudação usando um nome de host virtual que mapeia o endereço IP toohello de configuração de front-end de Balanceador de carga de saudação para Olá ASCS por exemplo <b>nws ascs</b>, <b>10.0.0.10</b>e número de instância Olá que você usou para investigação Olá Olá do balanceador de carga, por exemplo <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="c66f3-362">Install SAP NetWeaver ASCS as root on hello first node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and hello instance number that you used for hello probe of hello load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="c66f3-363">Você pode usar o hello sapinst parâmetro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst de tooconnect um usuário não-raiz.</span><span class="sxs-lookup"><span data-stu-id="c66f3-363">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="c66f3-364">**[1]**  Criar um recurso IP virtual e a investigação de integridade para o balanceador de carga interno Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-364">**[1]** Create a virtual IP resource and health-probe for hello internal load balancer</span></span>

   <pre><code>
   sudo crm node standby <b>nws-cl-0</b>
   sudo crm node online <b>nws-cl-1</b>
   sudo crm configure

   crm(live)configure# primitive drbd_<b>NWS</b>_ERS \
     ocf:linbit:drbd \
     params drbd_resource="<b>NWS</b>_ers" \
     op monitor interval="15" role="Master" \
     op monitor interval="30" role="Slave"

   crm(live)configure# ms ms-drbd_<b>NWS</b>_ERS drbd_<b>NWS</b>_ERS \
     meta master-max="1" master-node-max="1" clone-max="2" \
     clone-node-max="1" notify="true"

   crm(live)configure# primitive fs_<b>NWS</b>_ERS \
     ocf:heartbeat:Filesystem \
     params device=/dev/drbd1 \
     directory=/usr/sap/<b>NWS</b>/ERS<b>02</b>  \
     fstype=xfs \
     op monitor interval="10s"

   crm(live)configure# primitive vip_<b>NWS</b>_ERS IPaddr2 \
     params ip=<b>10.0.0.11</b> cidr_netmask=24 \
     op monitor interval=10 timeout=20

   crm(live)configure# primitive nc_<b>NWS</b>_ERS anything \
    params binfile="/usr/bin/nc" cmdline_options="-l -k 621<b>02</b>" \
    op monitor timeout=20s interval=10 depth=0

   crm(live)configure# group g-<b>NWS</b>_ERS nc_<b>NWS</b>_ERS vip_<b>NWS</b>_ERS fs_<b>NWS</b>_ERS

   crm(live)configure# order o-<b>NWS</b>_drbd_before_ERS inf: \
     ms-drbd_<b>NWS</b>_ERS:promote g-<b>NWS</b>_ERS:start
   
   crm(live)configure# colocation col-<b>NWS</b>_ERS_on_drbd inf: \
     ms-drbd_<b>NWS</b>_ERS:Master g-<b>NWS</b>_ERS
   
   crm(live)configure# commit
   # WARNING: Resources nc_NWS_ASCS,nc_NWS_ERS,nc_NWS_nfs violate uniqueness for parameter "binfile": "/usr/bin/nc"
   # Do you still want toocommit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="c66f3-365">Certifique-se de que o status de saudação do cluster é okey e que todos os recursos são iniciados.</span><span class="sxs-lookup"><span data-stu-id="c66f3-365">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="c66f3-366">Não é importante em quais recursos de saudação do nó estão em execução.</span><span class="sxs-lookup"><span data-stu-id="c66f3-366">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Node <b>nws-cl-0: standby</b>
   # <b>Online: [ nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      Stopped: [ nws-cl-0 ]
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="c66f3-367">**[2]** Instalar o ERS do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c66f3-367">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="c66f3-368">Instalar o SAP NetWeaver es como raiz no nó de segundo hello usando um nome de host virtual que mapeia o endereço IP toohello de configuração de front-end de Balanceador de carga de saudação para Olá es por exemplo <b>nws es</b>, <b>10.0.0.11</b> e o número de instância Olá que você usou para investigação Olá Olá do balanceador de carga, por exemplo <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="c66f3-368">Install SAP NetWeaver ERS as root on hello second node using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and hello instance number that you used for hello probe of hello load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="c66f3-369">Você pode usar o hello sapinst parâmetro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst de tooconnect um usuário não-raiz.</span><span class="sxs-lookup"><span data-stu-id="c66f3-369">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="c66f3-370">Use SWPM SP 20 PL 05 ou superior.</span><span class="sxs-lookup"><span data-stu-id="c66f3-370">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="c66f3-371">Versões anteriores não definir corretamente as permissões de saudação e haverá falha na instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66f3-371">Lower versions do not set hello permissions correctly and hello installation will fail.</span></span>
   > 

1. <span data-ttu-id="c66f3-372">**[1]**  Adaptar Olá ASCS/SCS e es instância perfis</span><span class="sxs-lookup"><span data-stu-id="c66f3-372">**[1]** Adapt hello ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="c66f3-373">Perfil do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="c66f3-373">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change hello restart command tooa start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add hello keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="c66f3-374">Perfil do ERS</span><span class="sxs-lookup"><span data-stu-id="c66f3-374">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add hello following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="c66f3-375">**[A]** Configurar Keep Alive</span><span class="sxs-lookup"><span data-stu-id="c66f3-375">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="c66f3-376">a comunicação entre o servidor de aplicativos do SAP NetWeaver hello e hello ASCS/SCS Olá é roteada por meio de um balanceador de carga de software.</span><span class="sxs-lookup"><span data-stu-id="c66f3-376">hello communication between hello SAP NetWeaver application server and hello ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="c66f3-377">o balanceador de carga Olá desconecta conexões inativas após um tempo limite configurável.</span><span class="sxs-lookup"><span data-stu-id="c66f3-377">hello load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="c66f3-378">tooprevent isso você precisa tooset um parâmetro hello perfil ASCS/SCS do SAP NetWeaver e alterar configurações do sistema Linux hello.</span><span class="sxs-lookup"><span data-stu-id="c66f3-378">tooprevent this you need tooset a parameter in hello SAP NetWeaver ASCS/SCS profile and change hello Linux system settings.</span></span> <span data-ttu-id="c66f3-379">Leia a [Nota SAP 1410736][1410736] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="c66f3-379">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="c66f3-380">Olá ASCS/SCS perfil parâmetro enfileirar/encni/set_so_keepalive já foi adicionado na última etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="c66f3-380">hello ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in hello last step.</span></span>

   <pre><code> 
   # Change hello Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="c66f3-381">**[A]**  Configurar os usuários do SAP Olá após a instalação de saudação</span><span class="sxs-lookup"><span data-stu-id="c66f3-381">**[A]** Configure hello SAP users after hello installation</span></span>
 
   <pre><code>
   # Add sidadm toohello haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="c66f3-382">**[1]**  Adicionar Olá ASCS e SAP es toohello sapservice arquivo services</span><span class="sxs-lookup"><span data-stu-id="c66f3-382">**[1]** Add hello ASCS and ERS SAP services toohello sapservice file</span></span>

   <span data-ttu-id="c66f3-383">Adicione Olá ASCS serviço entrada toohello segundo nó e cópia Olá es entrada toohello primeiro nó de serviço.</span><span class="sxs-lookup"><span data-stu-id="c66f3-383">Add hello ASCS service entry toohello second node and copy hello ERS service entry toohello first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="c66f3-384">**[1]**  Criar recursos de cluster Olá SAP</span><span class="sxs-lookup"><span data-stu-id="c66f3-384">**[1]** Create hello SAP cluster resources</span></span>

   <pre><code>
   sudo crm configure property maintenance-mode="true"

   sudo crm configure

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ASCS<b>00</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ASCS<b>00</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ASCS<b>00</b>_<b>nws-ascs</b>" \
    AUTOMATIC_RECOVER=false \
    meta resource-stickiness=5000 failure-timeout=60 migration-threshold=1 priority=10

   crm(live)configure# primitive rsc_sap_<b>NWS</b>_ERS<b>02</b> SAPInstance \
    operations $id=rsc_sap_<b>NWS</b>_ERS<b>02</b>-operations \
    op monitor interval=11 timeout=60 on_fail=restart \
    params InstanceName=<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b> START_PROFILE="/sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>" AUTOMATIC_RECOVER=false IS_ERS=true \
    meta priority=1000

   crm(live)configure# modgroup g-<b>NWS</b>_ASCS add rsc_sap_<b>NWS</b>_ASCS<b>00</b>
   crm(live)configure# modgroup g-<b>NWS</b>_ERS add rsc_sap_<b>NWS</b>_ERS<b>02</b>

   crm(live)configure# colocation col_sap_<b>NWS</b>_no_both -5000: g-<b>NWS</b>_ERS g-<b>NWS</b>_ASCS
   crm(live)configure# location loc_sap_<b>NWS</b>_failover_to_ers rsc_sap_<b>NWS</b>_ASCS<b>00</b> rule 2000: runs_ers_<b>NWS</b> eq 1
   crm(live)configure# order ord_sap_<b>NWS</b>_first_start_ascs Optional: rsc_sap_<b>NWS</b>_ASCS<b>00</b>:start rsc_sap_<b>NWS</b>_ERS<b>02</b>:stop symmetrical=false

   crm(live)configure# commit
   crm(live)configure# exit

   sudo crm configure property maintenance-mode="false"
   sudo crm node online <b>nws-cl-0</b>
   </code></pre>

   <span data-ttu-id="c66f3-385">Certifique-se de que o status de saudação do cluster é okey e que todos os recursos são iniciados.</span><span class="sxs-lookup"><span data-stu-id="c66f3-385">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="c66f3-386">Não é importante em quais recursos de saudação do nó estão em execução.</span><span class="sxs-lookup"><span data-stu-id="c66f3-386">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # Online: <b>[ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   </code></pre>

### <a name="create-stonith-device"></a><span data-ttu-id="c66f3-387">Criar dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="c66f3-387">Create STONITH device</span></span>

<span data-ttu-id="c66f3-388">dispositivo STONITH Olá usa tooauthorize uma entidade de serviço no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="c66f3-388">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="c66f3-389">Siga essas etapas toocreate uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="c66f3-389">Follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="c66f3-390">Vá muito<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="c66f3-390">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="c66f3-391">Folha de Active Directory do Azure Olá aberto</span><span class="sxs-lookup"><span data-stu-id="c66f3-391">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="c66f3-392">Vá tooProperties e anote Olá ID de diretório. Isso é hello **id de locatário**.</span><span class="sxs-lookup"><span data-stu-id="c66f3-392">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="c66f3-393">Clique em Registros do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="c66f3-393">Click App registrations</span></span>
1. <span data-ttu-id="c66f3-394">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="c66f3-394">Click Add</span></span>
1. <span data-ttu-id="c66f3-395">Digite um Nome, selecione Tipo de Aplicativo "Aplicativo Web/API", insira uma URL de logon (por exemplo, http://localhost) e clique em Criar</span><span class="sxs-lookup"><span data-stu-id="c66f3-395">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="c66f3-396">URL de entrada Hello não é usado e pode ser qualquer URL válido</span><span class="sxs-lookup"><span data-stu-id="c66f3-396">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="c66f3-397">Selecione Olá novo aplicativo e clique em chaves no guia de configurações de saudação</span><span class="sxs-lookup"><span data-stu-id="c66f3-397">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="c66f3-398">Insira uma descrição para uma nova chave, selecione "Nunca expira" e clique em Salvar</span><span class="sxs-lookup"><span data-stu-id="c66f3-398">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="c66f3-399">Anote o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66f3-399">Write down hello Value.</span></span> <span data-ttu-id="c66f3-400">Ele é usado como Olá **senha** para Olá entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="c66f3-400">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="c66f3-401">Anote a saudação ID do aplicativo. Ele é usado como Olá username (**id de logon** nas etapas de saudação abaixo) de saudação entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="c66f3-401">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="c66f3-402">Olá entidade de serviço não tem permissões tooaccess seus recursos do Azure por padrão.</span><span class="sxs-lookup"><span data-stu-id="c66f3-402">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="c66f3-403">Você precisa toogive toostart de permissões de entidade de serviço de saudação e parar (desalocar) todas as máquinas virtuais do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c66f3-403">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="c66f3-404">Vá toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="c66f3-404">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="c66f3-405">Abrir Olá folha de todos os recursos</span><span class="sxs-lookup"><span data-stu-id="c66f3-405">Open hello All resources blade</span></span>
1. <span data-ttu-id="c66f3-406">Selecione a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="c66f3-406">Select hello virtual machine</span></span>
1. <span data-ttu-id="c66f3-407">Clique em Controle de acesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="c66f3-407">Click Access control (IAM)</span></span>
1. <span data-ttu-id="c66f3-408">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="c66f3-408">Click Add</span></span>
1. <span data-ttu-id="c66f3-409">Selecione a função hello proprietário</span><span class="sxs-lookup"><span data-stu-id="c66f3-409">Select hello role Owner</span></span>
1. <span data-ttu-id="c66f3-410">Insira nome de saudação do aplicativo hello criado acima</span><span class="sxs-lookup"><span data-stu-id="c66f3-410">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="c66f3-411">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="c66f3-411">Click OK</span></span>

#### <a name="1-create-hello-stonith-devices"></a><span data-ttu-id="c66f3-412">**[1]**  Criar hello STONITH dispositivos</span><span class="sxs-lookup"><span data-stu-id="c66f3-412">**[1]** Create hello STONITH devices</span></span>

<span data-ttu-id="c66f3-413">Depois de editar permissões Olá para máquinas virtuais de hello, você pode configurar dispositivos STONITH de saudação em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="c66f3-413">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre><code>
sudo crm configure

# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-hello-use-of-a-stonith-device"></a><span data-ttu-id="c66f3-414">**[1]**  Habilitar o uso de saudação de um dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="c66f3-414">**[1]** Enable hello use of a STONITH device</span></span>

<span data-ttu-id="c66f3-415">Habilitar o uso de saudação de um dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="c66f3-415">Enable hello use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="c66f3-416">Instalar banco de dados</span><span class="sxs-lookup"><span data-stu-id="c66f3-416">Install database</span></span>

<span data-ttu-id="c66f3-417">Neste exemplo, uma replicação de sistema do SAP HANA está instalada e configurada.</span><span class="sxs-lookup"><span data-stu-id="c66f3-417">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="c66f3-418">SAP HANA será executado no mesmo cluster como hello ASCS/SCS do SAP NetWeaver e es de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66f3-418">SAP HANA will run in hello same cluster as hello SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="c66f3-419">Você também pode instalar o SAP HANA em um cluster dedicado.</span><span class="sxs-lookup"><span data-stu-id="c66f3-419">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="c66f3-420">Veja [Alta disponibilidade do SAP HANA em VMs (máquinas virtuais) do Azure][sap-hana-ha] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="c66f3-420">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="c66f3-421">Preparar para a instalação do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="c66f3-421">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="c66f3-422">Normalmente, é recomendável usar LVM para volumes que armazenam arquivos de log e dados.</span><span class="sxs-lookup"><span data-stu-id="c66f3-422">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="c66f3-423">Para fins de teste, você também pode escolher arquivo de log e dados de saudação de toostore diretamente em um disco simples.</span><span class="sxs-lookup"><span data-stu-id="c66f3-423">For testing purposes, you can also choose toostore hello data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="c66f3-424">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="c66f3-424">**[A]** LVM</span></span>  
   <span data-ttu-id="c66f3-425">Olá exemplo a seguir supõe que máquinas virtuais de saudação tiver quatro discos de dados anexados que devem ser usado toocreate dois volumes.</span><span class="sxs-lookup"><span data-stu-id="c66f3-425">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
   
   <span data-ttu-id="c66f3-426">Crie volumes físicos de todos os discos que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="c66f3-426">Create physical volumes for all disks that you want toouse.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="c66f3-427">Criar um grupo de volumes para arquivos de dados hello, um grupo de volumes para arquivos de log hello e um diretório compartilhado de saudação do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="c66f3-427">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="c66f3-428">Criar hello volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="c66f3-428">Create hello logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="c66f3-429">Criar diretórios de montagem hello e copie Olá UUID de todos os volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="c66f3-429">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="c66f3-430">Crie entradas de autofs para Olá três volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="c66f3-430">Create autofs entries for hello three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="c66f3-431">Inserir essa linha toosudo vi /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="c66f3-431">Insert this line toosudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="c66f3-432">Montar Olá novos volumes</span><span class="sxs-lookup"><span data-stu-id="c66f3-432">Mount hello new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="c66f3-433">**[A]** Discos simples</span><span class="sxs-lookup"><span data-stu-id="c66f3-433">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="c66f3-434">Para sistemas pequenos ou de demonstração, você pode colocar os arquivos de log e dados do HANA em um disco.</span><span class="sxs-lookup"><span data-stu-id="c66f3-434">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="c66f3-435">Olá comandos a seguir criar uma partição em /dev/sdc e formate-o com xfs.</span><span class="sxs-lookup"><span data-stu-id="c66f3-435">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down hello id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="c66f3-436">Inserir essa linha too/etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="c66f3-436">Insert this line too/etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="c66f3-437">Criar o diretório de destino hello e montar o disco de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66f3-437">Create hello target directory and mount hello disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="c66f3-438">Instalando o SAP HANA</span><span class="sxs-lookup"><span data-stu-id="c66f3-438">Installing SAP HANA</span></span>

<span data-ttu-id="c66f3-439">Olá etapas a seguir se baseiam no capítulo 4 do hello [guia de cenário de otimização de desempenho do SAP HANA SR] [ suse-hana-ha-guide] tooinstall replicação de sistema do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="c66f3-439">hello following steps are based on chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span> <span data-ttu-id="c66f3-440">Leia antes de continuar a instalação de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66f3-440">Please read it before you continue hello installation.</span></span>

1. <span data-ttu-id="c66f3-441">**[A]**  Executar hdblcm de saudação HANA DVD</span><span class="sxs-lookup"><span data-stu-id="c66f3-441">**[A]** Run hdblcm from hello HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="c66f3-442">**[A]** Atualizar o Agente do Host do SAP</span><span class="sxs-lookup"><span data-stu-id="c66f3-442">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="c66f3-443">Baixe o arquivo de SAP Host Agent mais recente de saudação do hello [SAP Softwarecenter] [ sap-swcenter] e execução hello comando tooupgrade Olá agente a seguir.</span><span class="sxs-lookup"><span data-stu-id="c66f3-443">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="c66f3-444">Substitua saudação caminho toohello toopoint toohello arquivo baixado.</span><span class="sxs-lookup"><span data-stu-id="c66f3-444">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path tooSAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="c66f3-445">**[1]** Criar uma replicação HANA (como raiz)</span><span class="sxs-lookup"><span data-stu-id="c66f3-445">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="c66f3-446">Execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="c66f3-446">Run hello following command.</span></span> <span data-ttu-id="c66f3-447">Verifique se tooreplace negrito cadeias de caracteres (HANA HDB de ID de sistema e instância número 03) com valores de saudação da instalação do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="c66f3-447">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="c66f3-448">**[A]** Criar entrada de repositório de chaves (como raiz)</span><span class="sxs-lookup"><span data-stu-id="c66f3-448">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="c66f3-449">**[1]** Fazer o backup do banco de dados backup (como raiz)</span><span class="sxs-lookup"><span data-stu-id="c66f3-449">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="c66f3-450">**[1]**  Alternar toohello HANA sapsid usuário e criar o site primário hello.</span><span class="sxs-lookup"><span data-stu-id="c66f3-450">**[1]** Switch toohello HANA sapsid user and create hello primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="c66f3-451">**[2]**  Alternar toohello HANA sapsid usuário e criar site secundário hello.</span><span class="sxs-lookup"><span data-stu-id="c66f3-451">**[2]** Switch toohello HANA sapsid user and create hello secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="c66f3-452">**[1]** Criar os recursos de cluster do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="c66f3-452">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="c66f3-453">Primeiro, crie uma topologia de saudação.</span><span class="sxs-lookup"><span data-stu-id="c66f3-453">First, create hello topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number and HANA system id
   
   crm(live)configure# primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b>   ocf:suse:SAPHanaTopology \
     operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
     op monitor interval="10" timeout="600" \
     op start interval="0" timeout="600" \
     op stop interval="0" timeout="300" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"
    
   crm(live)configure# clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>
   
   <span data-ttu-id="c66f3-454">Em seguida, crie Olá recursos HANA</span><span class="sxs-lookup"><span data-stu-id="c66f3-454">Next, create hello HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
    
   crm(live)configure# primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
     operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
     op start interval="0" timeout="3600" \
     op stop interval="0" timeout="3600" \
     op promote interval="0" timeout="3600" \
     op monitor interval="60" role="Master" timeout="700" \
     op monitor interval="61" role="Slave" timeout="700" \
     params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
     DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"
    
   crm(live)configure# ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
     meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
     target-role="Started" interleave="true"
    
   crm(live)configure# primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
     meta target-role="Started" is-managed="true" \ 
     operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
     op monitor interval="10s" timeout="20s" \ 
     params ip="<b>10.0.0.12</b>" 

   crm(live)configure# primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
     params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
     op monitor timeout=20s interval=10 depth=0 

   crm(live)configure# group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  

   crm(live)configure# order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
     msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
    
   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

   <span data-ttu-id="c66f3-455">Certifique-se de que o status de saudação do cluster é okey e que todos os recursos são iniciados.</span><span class="sxs-lookup"><span data-stu-id="c66f3-455">Make sure that hello cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="c66f3-456">Não é importante em quais recursos de saudação do nó estão em execução.</span><span class="sxs-lookup"><span data-stu-id="c66f3-456">It is not important on which node hello resources are running.</span></span>

   <pre><code>
   sudo crm_mon -r

   # <b>Online: [ nws-cl-0 nws-cl-1 ]</b>
   # 
   # Full list of resources:
   # 
   #  Master/Slave Set: ms-drbd_NWS_ASCS [drbd_NWS_ASCS]
   #      <b>Masters: [ nws-cl-1 ]</b>
   #      <b>Slaves: [ nws-cl-0 ]</b>
   #  Resource Group: g-NWS_ASCS
   #      nc_NWS_ASCS        (ocf::heartbeat:anything):      <b>Started nws-cl-1</b>
   #      vip_NWS_ASCS       (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-1</b>
   #      fs_NWS_ASCS        (ocf::heartbeat:Filesystem):    <b>Started nws-cl-1</b>
   #      rsc_sap_NWS_ASCS00 (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-1</b>
   #  Master/Slave Set: ms-drbd_NWS_ERS [drbd_NWS_ERS]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g-NWS_ERS
   #      nc_NWS_ERS (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   #      vip_NWS_ERS        (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      fs_NWS_ERS (ocf::heartbeat:Filesystem):    <b>Started nws-cl-0</b>
   #      rsc_sap_NWS_ERS02  (ocf::heartbeat:SAPInstance):   <b>Started nws-cl-0</b>
   #  Clone Set: cln_SAPHanaTopology_HDB_HDB03 [rsc_SAPHanaTopology_HDB_HDB03]
   #      <b>Started: [ nws-cl-0 nws-cl-1 ]</b>
   #  Master/Slave Set: msl_SAPHana_HDB_HDB03 [rsc_SAPHana_HDB_HDB03]
   #      <b>Masters: [ nws-cl-0 ]</b>
   #      <b>Slaves: [ nws-cl-1 ]</b>
   #  Resource Group: g_ip_HDB_HDB03
   #      rsc_ip_HDB_HDB03   (ocf::heartbeat:IPaddr2):       <b>Started nws-cl-0</b>
   #      rsc_nc_HDB_HDB03   (ocf::heartbeat:anything):      <b>Started nws-cl-0</b>
   # rsc_st_azure_1  (stonith:fence_azure_arm):      <b>Started nws-cl-0</b>
   # rsc_st_azure_2  (stonith:fence_azure_arm):      <b>Started nws-cl-1</b>
   </code></pre>

1. <span data-ttu-id="c66f3-457">**[1]**  Instância de banco de dados do instalar Olá SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c66f3-457">**[1]** Install hello SAP NetWeaver database instance</span></span>

   <span data-ttu-id="c66f3-458">Instalar Olá instância de banco de dados SAP NetWeaver como raiz usando um nome de host virtual que mapeia o endereço IP toohello de configuração de front-end de Balanceador de carga de saudação do banco de dados de saudação por exemplo <b>nws db</b> e <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="c66f3-458">Install hello SAP NetWeaver database instance as root using a virtual hostname that maps toohello IP address of hello load balancer frontend configuration for hello database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="c66f3-459">Você pode usar o hello sapinst parâmetro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst de tooconnect um usuário não-raiz.</span><span class="sxs-lookup"><span data-stu-id="c66f3-459">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="c66f3-460">Instalação de servidor de aplicativos do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c66f3-460">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="c66f3-461">Siga essas etapas tooinstall um servidor de aplicativos SAP.</span><span class="sxs-lookup"><span data-stu-id="c66f3-461">Follow these steps tooinstall an SAP application server.</span></span> <span data-ttu-id="c66f3-462">Olá etapas abaixo supõem que você instale o servidor de aplicativos de saudação em um servidor diferente do hello ASCS/SCS e servidores do HANA.</span><span class="sxs-lookup"><span data-stu-id="c66f3-462">hello steps bellow assume that you install hello application server on a server different from hello ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="c66f3-463">Caso contrário, algumas das etapas de saudação abaixo (como configurar a resolução de nome de host) não são necessários.</span><span class="sxs-lookup"><span data-stu-id="c66f3-463">Otherwise some of hello steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="c66f3-464">Configurar a resolução de nome do host</span><span class="sxs-lookup"><span data-stu-id="c66f3-464">Setup host name resolution</span></span>    
   <span data-ttu-id="c66f3-465">Você pode usar um servidor DNS ou modificar /etc/hosts Olá em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="c66f3-465">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="c66f3-466">Este exemplo mostra como toouse Olá arquivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="c66f3-466">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="c66f3-467">Substituir endereço IP de saudação e nome de host Olá no hello comandos a seguir</span><span class="sxs-lookup"><span data-stu-id="c66f3-467">Replace hello IP address and hello hostname in hello following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="c66f3-468">Inserir saudação linhas muito/etc/hosts a seguir.</span><span class="sxs-lookup"><span data-stu-id="c66f3-468">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="c66f3-469">Alterar o ambiente de saudação IP toomatch de endereço e o nome do host</span><span class="sxs-lookup"><span data-stu-id="c66f3-469">Change hello IP address and hostname toomatch your environment</span></span>    
    
   <pre><code>
   # IP address of hello load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of hello load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of hello load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of hello application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="c66f3-470">Criar o diretório de sapmnt Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-470">Create hello sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="c66f3-471">Configurar o autofs</span><span class="sxs-lookup"><span data-stu-id="c66f3-471">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add hello following line toohello file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="c66f3-472">Criar um novo arquivo com</span><span class="sxs-lookup"><span data-stu-id="c66f3-472">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add hello following lines toohello file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="c66f3-473">Reiniciar autofs toomount novos compartilhamentos Olá</span><span class="sxs-lookup"><span data-stu-id="c66f3-473">Restart autofs toomount hello new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="c66f3-474">Configurar arquivo de permuta</span><span class="sxs-lookup"><span data-stu-id="c66f3-474">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set hello property ResourceDisk.EnableSwap tooy
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set hello size of hello SWAP file with property ResourceDisk.SwapSizeMB
   # hello free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check hello SWAP space with command swapon
   # Size of hello swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="c66f3-475">Reiniciar alteração de Olá Olá agente tooactivate</span><span class="sxs-lookup"><span data-stu-id="c66f3-475">Restart hello Agent tooactivate hello change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="c66f3-476">Instalar o servidor de aplicativos do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="c66f3-476">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="c66f3-477">Instale um servidor de aplicativos do SAP NetWeaver primário ou adicional.</span><span class="sxs-lookup"><span data-stu-id="c66f3-477">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="c66f3-478">Você pode usar o hello sapinst parâmetro SAPINST_REMOTE_ACCESS_USER tooallow toosapinst de tooconnect um usuário não-raiz.</span><span class="sxs-lookup"><span data-stu-id="c66f3-478">You can use hello sapinst parameter SAPINST_REMOTE_ACCESS_USER tooallow a non-root user tooconnect toosapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="c66f3-479">Atualizar o repositório seguro do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="c66f3-479">Update SAP HANA secure store</span></span>

   <span data-ttu-id="c66f3-480">Saudação de atualização segura do SAP HANA armazenar toopoint toohello virtual nome do programa de instalação de replicação de sistema do SAP HANA hello.</span><span class="sxs-lookup"><span data-stu-id="c66f3-480">Update hello SAP HANA secure store toopoint toohello virtual name of hello SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="c66f3-481">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c66f3-481">Next steps</span></span>
* <span data-ttu-id="c66f3-482">[Planejamento e implementação de Máquinas Virtuais do Azure para SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="c66f3-482">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="c66f3-483">[Implantação de Máquinas Virtuais do Azure para SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="c66f3-483">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="c66f3-484">[Implantação DBMS de Máquinas Virtuais do Azure para SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="c66f3-484">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="c66f3-485">toolearn como tooestablish alta disponibilidade e o plano de recuperação de desastres do HANA SAP no Azure (instâncias grandes), consulte [SAP HANA (instâncias grandes) alta disponibilidade e recuperação de desastres no Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="c66f3-485">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="c66f3-486">toolearn como tooestablish alta disponibilidade e o plano de recuperação de desastres do HANA SAP em VMs do Azure, consulte [disponibilidade alta do SAP HANA em máquinas virtuais do Azure (VMs)][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="c66f3-486">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>
