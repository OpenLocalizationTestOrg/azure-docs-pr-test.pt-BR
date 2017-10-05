---
title: "Alta disponibilidade de Máquinas Virtuais do Azure para SAP NetWeaver no SUSE Linux Enterprise Server para aplicativos SAP | Microsoft Docs"
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
ms.openlocfilehash: 16e09797926f29bc18cb05671c986c74f9c2d4f8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-for-sap-netweaver-on-azure-vms-on-suse-linux-enterprise-server-for-sap-applications"></a><span data-ttu-id="72985-103">Alta disponibilidade do SAP NetWeaver em VMs do Azure no SUSE Linux Enterprise Server para aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="72985-103">High availability for SAP NetWeaver on Azure VMs on SUSE Linux Enterprise Server for SAP applications</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="72985-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="72985-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="72985-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="72985-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="72985-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="72985-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="72985-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="72985-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="72985-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="72985-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="72985-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="72985-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="72985-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="72985-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="72985-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="72985-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="72985-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="72985-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>
[1410736]:https://launchpad.support.sap.com/#/notes/1410736

[sap-swcenter]:https://support.sap.com/en/my-support/software-downloads.html

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[suse-drbd-guide]:https://www.suse.com/documentation/sle-ha-12/singlehtml/book_sleha_techguides/book_sleha_techguides.html

[template-multisid-xscs]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-xscs-md%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged-md%2Fazuredeploy.json
[template-file-server]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-file-server-md%2Fazuredeploy.json

[sap-hana-ha]:sap-hana-high-availability.md

<span data-ttu-id="72985-113">Este artigo descreve como implantar as máquinas virtuais, configurar as máquinas virtuais, instalar a estrutura de cluster e instalar um sistema SAP NetWeaver 7.50 com alta disponibilidade.</span><span class="sxs-lookup"><span data-stu-id="72985-113">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework and install a highly available SAP NetWeaver 7.50 system.</span></span>
<span data-ttu-id="72985-114">Nas configurações de exemplo, comandos de instalação etc. A instância do ASCS número 00, a número da instância do ERS 02 e o NWS de ID do sistema SAP são usados.</span><span class="sxs-lookup"><span data-stu-id="72985-114">In the example configurations, installation commands etc. ASCS instance number 00, ERS instance number 02 and SAP System ID NWS is used.</span></span> <span data-ttu-id="72985-115">Os nomes dos recursos (por exemplo, máquinas virtuais, redes virtuais) no exemplo pressupõem que você tenha usado o [modelo convergido][template-converged] com o NWS de ID do sistema SAP para criar os recursos.</span><span class="sxs-lookup"><span data-stu-id="72985-115">The names of the resources (for example virtual machines, virtual networks) in the example assume that you have used the [converged template][template-converged] with SAP system ID NWS to create the resources.</span></span>

<span data-ttu-id="72985-116">Primeiro, leia os seguintes documentos e Notas SAP</span><span class="sxs-lookup"><span data-stu-id="72985-116">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="72985-117">A Nota SAP [1928533], que tem:</span><span class="sxs-lookup"><span data-stu-id="72985-117">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="72985-118">Lista de tamanhos de VM do Azure que têm suporte para a implantação de software SAP</span><span class="sxs-lookup"><span data-stu-id="72985-118">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="72985-119">Informações importantes sobre capacidade para tamanhos de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="72985-119">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="72985-120">Software SAP e combinações de SO (sistema operacional) e banco de dados com suporte</span><span class="sxs-lookup"><span data-stu-id="72985-120">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="72985-121">A versão do kernel do SAP necessária para Windows e para Linux no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="72985-121">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>

* <span data-ttu-id="72985-122">A Nota SAP [2015553] lista pré-requisitos para implantações de software SAP com suporte do SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="72985-122">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="72985-123">A Nota SAP [2205917] tem configurações de SO recomendadas para SUSE Linux Enterprise Server para aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="72985-123">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="72985-124">A Nota SAP [1944799] tem Diretrizes SAP HANA para SUSE Linux Enterprise Server para aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="72985-124">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="72985-125">A Nota SAP [2178632] contém informações detalhadas sobre todas as métricas de monitoramentos relatadas para o SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="72985-125">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="72985-126">A Nota SAP [2191498] tem a versão necessária do SAP Host Agent para Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="72985-126">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="72985-127">A Nota SAP [2243692] tem informações sobre o licenciamento do SAP no Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="72985-127">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="72985-128">A Nota SAP [1984787] tem informações gerais sobre o SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="72985-128">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="72985-129">A Nota SAP [1999351] tem informações de solução de problemas adicionais para a Extensão de Monitoramento Avançado do Azure para SAP.</span><span class="sxs-lookup"><span data-stu-id="72985-129">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="72985-130">[WIKI da comunidade do SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) tem todas as Notas SAP necessárias para Linux.</span><span class="sxs-lookup"><span data-stu-id="72985-130">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="72985-131">[Planejamento e implementação de Máquinas Virtuais do Azure para SAP no Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="72985-131">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="72985-132">[Implantação de máquinas virtuais do Azure para SAP no Linux (este artigo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="72985-132">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="72985-133">[Implantação de Máquinas Virtuais do Azure do DBMS para SAP no Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="72985-133">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="72985-134">[Cenário otimizado para desempenho da SR SAP HANA][suse-hana-ha-guide]</span><span class="sxs-lookup"><span data-stu-id="72985-134">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide]</span></span>  
  <span data-ttu-id="72985-135">O guia contém todas as informações necessárias para configurar a Replicação do Sistema SAP HANA no local.</span><span class="sxs-lookup"><span data-stu-id="72985-135">The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="72985-136">Use este guia como uma linha de base.</span><span class="sxs-lookup"><span data-stu-id="72985-136">Use this guide as a baseline.</span></span>
* <span data-ttu-id="72985-137">[Armazenamento de NFS altamente disponível com DRBD e Pacemaker][suse-drbd-guide] O guia contém todas as informações necessárias para configurar um servidor NFS altamente disponível.</span><span class="sxs-lookup"><span data-stu-id="72985-137">[Highly Available NFS Storage with DRBD and Pacemaker][suse-drbd-guide] The guide contains all required information to set up a highly available NFS server.</span></span> <span data-ttu-id="72985-138">Use este guia como uma linha de base.</span><span class="sxs-lookup"><span data-stu-id="72985-138">Use this guide as a baseline.</span></span>


## <a name="overview"></a><span data-ttu-id="72985-139">Visão geral</span><span class="sxs-lookup"><span data-stu-id="72985-139">Overview</span></span>

<span data-ttu-id="72985-140">Para obter alta disponibilidade, o SAP NetWeaver requer um servidor NFS.</span><span class="sxs-lookup"><span data-stu-id="72985-140">To achieve high availability, SAP NetWeaver requires an NFS server.</span></span> <span data-ttu-id="72985-141">O servidor NFS está configurado em um cluster separado e pode ser usado por vários sistemas SAP.</span><span class="sxs-lookup"><span data-stu-id="72985-141">The NFS server is configured in a separate cluster and can be used by multiple SAP systems.</span></span>

![Visão geral da Alta Disponibilidade do SAP NetWeaver](./media/high-availability-guide-suse/img_001.png)

<span data-ttu-id="72985-143">O servidor NFS, ASCS do SAP NetWeaver, SCS do SAP NetWeaver, ERS do SAP NetWeaver e o banco de dados SAP HANA usam um nome do host virtual e endereços IP virtuais.</span><span class="sxs-lookup"><span data-stu-id="72985-143">The NFS server, SAP NetWeaver ASCS, SAP NetWeaver SCS, SAP NetWeaver ERS and the SAP HANA database use virtual hostname and virtual IP addresses.</span></span> <span data-ttu-id="72985-144">No Azure, um balanceador de carga é necessário para usar um endereço IP virtual.</span><span class="sxs-lookup"><span data-stu-id="72985-144">On Azure, a load balancer is required to use a virtual IP address.</span></span> <span data-ttu-id="72985-145">A lista a seguir mostra a configuração do balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="72985-145">The following list shows the configuration of the load balancer.</span></span>

### <a name="nfs-server"></a><span data-ttu-id="72985-146">Servidor NFS</span><span class="sxs-lookup"><span data-stu-id="72985-146">NFS Server</span></span>
* <span data-ttu-id="72985-147">Configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="72985-147">Frontend configuration</span></span>
  * <span data-ttu-id="72985-148">Endereço IP 10.0.0.4</span><span class="sxs-lookup"><span data-stu-id="72985-148">IP address 10.0.0.4</span></span>
* <span data-ttu-id="72985-149">Configuração de back-end</span><span class="sxs-lookup"><span data-stu-id="72985-149">Backend configuration</span></span>
  * <span data-ttu-id="72985-150">Conectado aos adaptadores de rede primários de todas as máquinas virtuais que devem ser parte do cluster NFS</span><span class="sxs-lookup"><span data-stu-id="72985-150">Connected to primary network interfaces of all virtual machines that should be part of the NFS cluster</span></span>
* <span data-ttu-id="72985-151">Porta de Investigação</span><span class="sxs-lookup"><span data-stu-id="72985-151">Probe Port</span></span>
  * <span data-ttu-id="72985-152">Porta 61000</span><span class="sxs-lookup"><span data-stu-id="72985-152">Port 61000</span></span>
* <span data-ttu-id="72985-153">Regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="72985-153">Loadbalancing rules</span></span>
  * <span data-ttu-id="72985-154">2049 TCP</span><span class="sxs-lookup"><span data-stu-id="72985-154">2049 TCP</span></span> 
  * <span data-ttu-id="72985-155">2049 UDP</span><span class="sxs-lookup"><span data-stu-id="72985-155">2049 UDP</span></span>

### <a name="ascs"></a><span data-ttu-id="72985-156">(A)SCS</span><span class="sxs-lookup"><span data-stu-id="72985-156">(A)SCS</span></span>
* <span data-ttu-id="72985-157">Configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="72985-157">Frontend configuration</span></span>
  * <span data-ttu-id="72985-158">Endereço IP 10.0.0.10</span><span class="sxs-lookup"><span data-stu-id="72985-158">IP address 10.0.0.10</span></span>
* <span data-ttu-id="72985-159">Configuração de back-end</span><span class="sxs-lookup"><span data-stu-id="72985-159">Backend configuration</span></span>
  * <span data-ttu-id="72985-160">Conectado aos adaptadores de rede primários de todas as máquinas virtuais que devem ser parte do cluster (A)SCS/ERS</span><span class="sxs-lookup"><span data-stu-id="72985-160">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="72985-161">Porta de Investigação</span><span class="sxs-lookup"><span data-stu-id="72985-161">Probe Port</span></span>
  * <span data-ttu-id="72985-162">Porta 620**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="72985-162">Port 620**&lt;nr&gt;**</span></span>
* <span data-ttu-id="72985-163">Regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="72985-163">Loadbalancing rules</span></span>
  * <span data-ttu-id="72985-164">32**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="72985-164">32**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="72985-165">36**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="72985-165">36**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="72985-166">39**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="72985-166">39**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="72985-167">81**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="72985-167">81**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="72985-168">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="72985-168">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="72985-169">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="72985-169">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="72985-170">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="72985-170">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="ers"></a><span data-ttu-id="72985-171">ERS</span><span class="sxs-lookup"><span data-stu-id="72985-171">ERS</span></span>
* <span data-ttu-id="72985-172">Configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="72985-172">Frontend configuration</span></span>
  * <span data-ttu-id="72985-173">Endereço IP 10.0.0.11</span><span class="sxs-lookup"><span data-stu-id="72985-173">IP address 10.0.0.11</span></span>
* <span data-ttu-id="72985-174">Configuração de back-end</span><span class="sxs-lookup"><span data-stu-id="72985-174">Backend configuration</span></span>
  * <span data-ttu-id="72985-175">Conectado aos adaptadores de rede primários de todas as máquinas virtuais que devem ser parte do cluster (A)SCS/ERS</span><span class="sxs-lookup"><span data-stu-id="72985-175">Connected to primary network interfaces of all virtual machines that should be part of the (A)SCS/ERS cluster</span></span>
* <span data-ttu-id="72985-176">Porta de Investigação</span><span class="sxs-lookup"><span data-stu-id="72985-176">Probe Port</span></span>
  * <span data-ttu-id="72985-177">Porta 621**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="72985-177">Port 621**&lt;nr&gt;**</span></span>
* <span data-ttu-id="72985-178">Regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="72985-178">Loadbalancing rules</span></span>
  * <span data-ttu-id="72985-179">33**&lt;nr&gt;** TCP</span><span class="sxs-lookup"><span data-stu-id="72985-179">33**&lt;nr&gt;** TCP</span></span>
  * <span data-ttu-id="72985-180">5**&lt;nr&gt;**13 TCP</span><span class="sxs-lookup"><span data-stu-id="72985-180">5**&lt;nr&gt;**13 TCP</span></span>
  * <span data-ttu-id="72985-181">5**&lt;nr&gt;**14 TCP</span><span class="sxs-lookup"><span data-stu-id="72985-181">5**&lt;nr&gt;**14 TCP</span></span>
  * <span data-ttu-id="72985-182">5**&lt;nr&gt;**16 TCP</span><span class="sxs-lookup"><span data-stu-id="72985-182">5**&lt;nr&gt;**16 TCP</span></span>

### <a name="sap-hana"></a><span data-ttu-id="72985-183">SAP HANA</span><span class="sxs-lookup"><span data-stu-id="72985-183">SAP HANA</span></span>
* <span data-ttu-id="72985-184">Configuração de front-end</span><span class="sxs-lookup"><span data-stu-id="72985-184">Frontend configuration</span></span>
  * <span data-ttu-id="72985-185">Endereço IP 10.0.0.12</span><span class="sxs-lookup"><span data-stu-id="72985-185">IP address 10.0.0.12</span></span>
* <span data-ttu-id="72985-186">Configuração de back-end</span><span class="sxs-lookup"><span data-stu-id="72985-186">Backend configuration</span></span>
  * <span data-ttu-id="72985-187">Conectado aos adaptadores de rede primários de todas as máquinas virtuais que devem ser parte do cluster HANA</span><span class="sxs-lookup"><span data-stu-id="72985-187">Connected to primary network interfaces of all virtual machines that should be part of the HANA cluster</span></span>
* <span data-ttu-id="72985-188">Porta de Investigação</span><span class="sxs-lookup"><span data-stu-id="72985-188">Probe Port</span></span>
  * <span data-ttu-id="72985-189">Porta 625**&lt;nr&gt;**</span><span class="sxs-lookup"><span data-stu-id="72985-189">Port 625**&lt;nr&gt;**</span></span>
* <span data-ttu-id="72985-190">Regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="72985-190">Loadbalancing rules</span></span>
  * <span data-ttu-id="72985-191">3**&lt;nr&gt;**15 TCP</span><span class="sxs-lookup"><span data-stu-id="72985-191">3**&lt;nr&gt;**15 TCP</span></span>
  * <span data-ttu-id="72985-192">3**&lt;nr&gt;**17 TCP</span><span class="sxs-lookup"><span data-stu-id="72985-192">3**&lt;nr&gt;**17 TCP</span></span>

## <a name="setting-up-a-highly-available-nfs-server"></a><span data-ttu-id="72985-193">Configuração de um servidor NFS altamente disponível</span><span class="sxs-lookup"><span data-stu-id="72985-193">Setting up a highly available NFS server</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="72985-194">Implantação do Linux</span><span class="sxs-lookup"><span data-stu-id="72985-194">Deploying Linux</span></span>

<span data-ttu-id="72985-195">O Azure Marketplace contém uma imagem para SUSE Linux Enterprise Server for SAP Applications 12 que você pode usar para implantar novas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="72985-195">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span>
<span data-ttu-id="72985-196">Você pode usar um dos modelos de início rápido no github para implantar todos os recursos necessários.</span><span class="sxs-lookup"><span data-stu-id="72985-196">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="72985-197">O modelo implanta as máquinas virtuais, o balanceador de carga, o conjunto de disponibilidade etc. Siga estas etapas para implantar o modelo:</span><span class="sxs-lookup"><span data-stu-id="72985-197">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="72985-198">Abra o [modelo de servidor de arquivo do SAP][template-file-server] no Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="72985-198">Open the [SAP file server template][template-file-server] in the Azure portal</span></span>   
1. <span data-ttu-id="72985-199">Defina os seguintes parâmetros</span><span class="sxs-lookup"><span data-stu-id="72985-199">Enter the following parameters</span></span>
   1. <span data-ttu-id="72985-200">Prefixo de recursos</span><span class="sxs-lookup"><span data-stu-id="72985-200">Resource Prefix</span></span>  
      <span data-ttu-id="72985-201">Digite o prefixo que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="72985-201">Enter the prefix you want to use.</span></span> <span data-ttu-id="72985-202">O valor é usado como um prefixo para os recursos que serão implantados.</span><span class="sxs-lookup"><span data-stu-id="72985-202">The value is used as a prefix for the resources that are deployed.</span></span>
   2. <span data-ttu-id="72985-203">Tipo de sistema operacional</span><span class="sxs-lookup"><span data-stu-id="72985-203">Os Type</span></span>  
      <span data-ttu-id="72985-204">Selecione uma das distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="72985-204">Select one of the Linux distributions.</span></span> <span data-ttu-id="72985-205">Para este exemplo, selecione SLES 12</span><span class="sxs-lookup"><span data-stu-id="72985-205">For this example, select SLES 12</span></span>
   3. <span data-ttu-id="72985-206">Nome de Usuário de Administrador e Senha do Administrador</span><span class="sxs-lookup"><span data-stu-id="72985-206">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="72985-207">É criado um novo usuário que pode ser usado para fazer logon no computador.</span><span class="sxs-lookup"><span data-stu-id="72985-207">A new user is created that can be used to log on to the machine.</span></span>
   4. <span data-ttu-id="72985-208">ID da Sub-rede</span><span class="sxs-lookup"><span data-stu-id="72985-208">Subnet Id</span></span>  
      <span data-ttu-id="72985-209">A ID da sub-rede à qual as máquinas virtuais devem estar conectadas.</span><span class="sxs-lookup"><span data-stu-id="72985-209">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="72985-210">Deixe vazio se você deseja criar uma nova rede virtual ou selecione a sub-rede da sua VPN ou a rede virtual da ExpressRoute para conectar a máquina virtual à sua rede local.</span><span class="sxs-lookup"><span data-stu-id="72985-210">Leave empty if you want to create a new virtual network or select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="72985-211">A ID geralmente tem esta aparência: /subscriptions/**&lt;id da assinatura&gt;**/resourceGroups/**&lt;nome do grupo de recursos&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;nome de rede virtual&gt;**/subnets/**&lt;nome da sub-rede&gt;**</span><span class="sxs-lookup"><span data-stu-id="72985-211">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="72985-212">Instalação</span><span class="sxs-lookup"><span data-stu-id="72985-212">Installation</span></span>

<span data-ttu-id="72985-213">Os itens a seguir são prefixados com **[A]** – aplicável a todos os nós, **[1]** – aplicável somente ao nó 1 ou **[2]** – aplicável somente ao nó 2.</span><span class="sxs-lookup"><span data-stu-id="72985-213">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="72985-214">**[A]** Atualizar o SLES</span><span class="sxs-lookup"><span data-stu-id="72985-214">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="72985-215">**[1]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="72985-215">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="72985-216">**[2]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="72985-216">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="72985-217">**[1]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="72985-217">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="72985-218">**[A]** Instalar a extensão HA</span><span class="sxs-lookup"><span data-stu-id="72985-218">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="72985-219">**[A]** Configurar a resolução de nome do host</span><span class="sxs-lookup"><span data-stu-id="72985-219">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="72985-220">Você pode usar um servidor DNS ou modificar /etc/hosts em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="72985-220">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="72985-221">Este exemplo mostra como usar o arquivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="72985-221">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="72985-222">Substitua o endereço IP e o nome do host nos comandos a seguir</span><span class="sxs-lookup"><span data-stu-id="72985-222">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="72985-223">Insira as seguintes linhas para /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="72985-223">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="72985-224">Altere o endereço IP e o nome do host para corresponder ao seu ambiente</span><span class="sxs-lookup"><span data-stu-id="72985-224">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   </code></pre>

1. <span data-ttu-id="72985-225">**[1]** Instalar o Cluster</span><span class="sxs-lookup"><span data-stu-id="72985-225">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="72985-226">**[2]** Adicionar nó ao cluster</span><span class="sxs-lookup"><span data-stu-id="72985-226">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="72985-227">**[A]** Alterar a senha hacluster para a mesma senha</span><span class="sxs-lookup"><span data-stu-id="72985-227">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="72985-228">**[A]** Configurar corosync para usar outro transporte e adicione nodelist.</span><span class="sxs-lookup"><span data-stu-id="72985-228">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="72985-229">Caso contrário, o cluster não funcionará.</span><span class="sxs-lookup"><span data-stu-id="72985-229">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="72985-230">Adicione o conteúdo em negrito a seguir ao arquivo.</span><span class="sxs-lookup"><span data-stu-id="72985-230">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="72985-231">Em seguida, reinicie o serviço corosync</span><span class="sxs-lookup"><span data-stu-id="72985-231">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="72985-232">**[A]** Instalar componentes drbd</span><span class="sxs-lookup"><span data-stu-id="72985-232">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="72985-233">**[A]** Criar uma partição para o dispositivo drbd</span><span class="sxs-lookup"><span data-stu-id="72985-233">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="72985-234">**[A]** Criar configurações de LVM</span><span class="sxs-lookup"><span data-stu-id="72985-234">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_NFS /dev/sdc1
   sudo lvcreate -l 100%FREE -n <b>NWS</b> vg_NFS
   </code></pre>

1. <span data-ttu-id="72985-235">**[A]** Criar o dispositivo drbd do NFS</span><span class="sxs-lookup"><span data-stu-id="72985-235">**[A]** Create the NFS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_nfs.res
   </code></pre>

   <span data-ttu-id="72985-236">Inserir a configuração para o novo dispositivo drbd e sair</span><span class="sxs-lookup"><span data-stu-id="72985-236">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="72985-237">Criar o dispositivo drbd e iniciá-lo</span><span class="sxs-lookup"><span data-stu-id="72985-237">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_nfs
   sudo drbdadm up <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="72985-238">**[1]** Ignorar a sincronização inicial</span><span class="sxs-lookup"><span data-stu-id="72985-238">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="72985-239">**[1]**  Definir o nó principal</span><span class="sxs-lookup"><span data-stu-id="72985-239">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_nfs
   </code></pre>

1. <span data-ttu-id="72985-240">**[1]** Aguardar até que os novos dispositivos drbd sejam sincronizados</span><span class="sxs-lookup"><span data-stu-id="72985-240">**[1]** Wait until the new drbd devices are synchronized</span></span>

   <pre><code>
   sudo cat /proc/drbd

   # version: 8.4.6 (api:1/proto:86-101)
   # GIT-hash: 833d830e0152d1e457fa7856e71e11248ccf3f70 build by abuild@sheep14, 2016-05-09 23:14:56
   # 0: cs:Connected ro:Primary/Secondary ds:UpToDate/UpToDate C r-----
   #    ns:0 nr:0 dw:0 dr:912 al:8 bm:0 lo:0 pe:0 ua:0 ap:0 ep:1 wo:f oos:0
   </code></pre>

1. <span data-ttu-id="72985-241">**[1]** Criar sistemas de arquivos nos dispositivos drbd</span><span class="sxs-lookup"><span data-stu-id="72985-241">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="72985-242">Configurar a estrutura do cluster</span><span class="sxs-lookup"><span data-stu-id="72985-242">Configure Cluster Framework</span></span>

1. <span data-ttu-id="72985-243">**[1]** Alterar as configurações padrão</span><span class="sxs-lookup"><span data-stu-id="72985-243">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="72985-244">**[1]** Adicionar o dispositivo de drbd do NFS à configuração do cluster</span><span class="sxs-lookup"><span data-stu-id="72985-244">**[1]** Add the NFS drbd device to the cluster configuration</span></span>

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

1. <span data-ttu-id="72985-245">**[1]** Criar o servidor NFS</span><span class="sxs-lookup"><span data-stu-id="72985-245">**[1]** Create the NFS server</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# primitive nfsserver \
     systemd:nfs-server \
     op monitor interval="30s"

   crm(live)configure# clone cl-nfsserver nfsserver interleave="true"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

1. <span data-ttu-id="72985-246">**[1]** Criar os recursos do sistema de arquivos NFS</span><span class="sxs-lookup"><span data-stu-id="72985-246">**[1]** Create the NFS File System resources</span></span>

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

1. <span data-ttu-id="72985-247">**[1]** Criar as exportações do NFS</span><span class="sxs-lookup"><span data-stu-id="72985-247">**[1]** Create the NFS exports</span></span>

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

1. <span data-ttu-id="72985-248">**[1]** Criar um recurso de IP virtual e a investigação de integridade para o balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="72985-248">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="72985-249">Criar dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="72985-249">Create STONITH device</span></span>

<span data-ttu-id="72985-250">O dispositivo STONITH usa uma Entidade de Serviço para autorização no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="72985-250">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="72985-251">Siga estas etapas para criar uma Entidade de Serviço.</span><span class="sxs-lookup"><span data-stu-id="72985-251">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="72985-252">Acesse <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="72985-252">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="72985-253">Abra a folha Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72985-253">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="72985-254">Vá para Propriedades e anote a ID do Diretório.</span><span class="sxs-lookup"><span data-stu-id="72985-254">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="72985-255">Essa é a **id de locatário**.</span><span class="sxs-lookup"><span data-stu-id="72985-255">This is the **tenant id**.</span></span>
1. <span data-ttu-id="72985-256">Clique em Registros do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="72985-256">Click App registrations</span></span>
1. <span data-ttu-id="72985-257">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="72985-257">Click Add</span></span>
1. <span data-ttu-id="72985-258">Digite um Nome, selecione Tipo de Aplicativo "Aplicativo Web/API", insira uma URL de logon (por exemplo, http://localhost) e clique em Criar</span><span class="sxs-lookup"><span data-stu-id="72985-258">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="72985-259">A URL de logon não é usada e pode ser qualquer URL válida</span><span class="sxs-lookup"><span data-stu-id="72985-259">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="72985-260">Selecione o novo Aplicativo e clique em Chaves na guia Configurações</span><span class="sxs-lookup"><span data-stu-id="72985-260">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="72985-261">Insira uma descrição para uma nova chave, selecione "Nunca expira" e clique em Salvar</span><span class="sxs-lookup"><span data-stu-id="72985-261">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="72985-262">Anote o Valor.</span><span class="sxs-lookup"><span data-stu-id="72985-262">Write down the Value.</span></span> <span data-ttu-id="72985-263">Ele é usado como **senha** da Entidade de Serviço</span><span class="sxs-lookup"><span data-stu-id="72985-263">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="72985-264">Anote a ID do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="72985-264">Write down the Application Id.</span></span> <span data-ttu-id="72985-265">Ela é usada como nome de usuário (**id de logon** nas etapas abaixo) da Entidade de Serviço</span><span class="sxs-lookup"><span data-stu-id="72985-265">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="72985-266">A Entidade de Serviço não tem permissões para acessar os recursos do Azure por padrão.</span><span class="sxs-lookup"><span data-stu-id="72985-266">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="72985-267">Você precisa fornecer as permissões da Entidade de Serviço para iniciar e parar (desalocar) todas as máquinas virtuais do cluster.</span><span class="sxs-lookup"><span data-stu-id="72985-267">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="72985-268">Acesse https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="72985-268">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="72985-269">Abra a folha Todos os recursos</span><span class="sxs-lookup"><span data-stu-id="72985-269">Open the All resources blade</span></span>
1. <span data-ttu-id="72985-270">Selecione a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="72985-270">Select the virtual machine</span></span>
1. <span data-ttu-id="72985-271">Clique em Controle de acesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="72985-271">Click Access control (IAM)</span></span>
1. <span data-ttu-id="72985-272">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="72985-272">Click Add</span></span>
1. <span data-ttu-id="72985-273">Selecione a função Proprietário</span><span class="sxs-lookup"><span data-stu-id="72985-273">Select the role Owner</span></span>
1. <span data-ttu-id="72985-274">Digite o nome do aplicativo criado acima</span><span class="sxs-lookup"><span data-stu-id="72985-274">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="72985-275">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="72985-275">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="72985-276">**[1]** Criar os dispositivos STONITH</span><span class="sxs-lookup"><span data-stu-id="72985-276">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="72985-277">Depois de editar as permissões das máquinas virtuais, você pode configurar os dispositivos STONITH no cluster.</span><span class="sxs-lookup"><span data-stu-id="72985-277">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="72985-278">**[1]** Habilitar o uso de um dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="72985-278">**[1]** Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="setting-up-ascs"></a><span data-ttu-id="72985-279">Configuração do (A)SCS</span><span class="sxs-lookup"><span data-stu-id="72985-279">Setting up (A)SCS</span></span>

### <a name="deploying-linux"></a><span data-ttu-id="72985-280">Implantação do Linux</span><span class="sxs-lookup"><span data-stu-id="72985-280">Deploying Linux</span></span>

<span data-ttu-id="72985-281">O Azure Marketplace contém uma imagem para SUSE Linux Enterprise Server for SAP Applications 12 que você pode usar para implantar novas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="72985-281">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 that you can use to deploy new virtual machines.</span></span> <span data-ttu-id="72985-282">A imagem do Marketplace contém o agente de recurso para SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="72985-282">The marketplace image contains the resource agent for SAP NetWeaver.</span></span>

<span data-ttu-id="72985-283">Você pode usar um dos modelos de início rápido no github para implantar todos os recursos necessários.</span><span class="sxs-lookup"><span data-stu-id="72985-283">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="72985-284">O modelo implanta as máquinas virtuais, o balanceador de carga, o conjunto de disponibilidade etc. Siga estas etapas para implantar o modelo:</span><span class="sxs-lookup"><span data-stu-id="72985-284">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="72985-285">Abra o [modelo multi-SID do ASCS/SCS][template-multisid-xscs] ou o [modelo convergido][template-converged] no Portal do Azure. O modelo de ASCS/SCS cria apenas as regras de balanceamento de carga para instâncias ERS (somente Linux) e ASCS/SCS do SAP NetWeaver, enquanto o modelo convergido também cria as regras de balanceamento de carga para um banco de dados (por exemplo, Microsoft SQL Server ou SAP HANA).</span><span class="sxs-lookup"><span data-stu-id="72985-285">Open the [ASCS/SCS Multi SID template][template-multisid-xscs] or the [converged template][template-converged] on the Azure portal The ASCS/SCS template only creates the load-balancing rules for the SAP NetWeaver ASCS/SCS and ERS (Linux only) instances whereas the converged template also creates the load-balancing rules for a database (for example Microsoft SQL Server or SAP HANA).</span></span> <span data-ttu-id="72985-286">Se você planeja instalar um sistema baseado no SAP NetWeaver e também quer instalar o banco de dados nos mesmos computadores, use o [modelo convergido][template-converged].</span><span class="sxs-lookup"><span data-stu-id="72985-286">If you plan to install an SAP NetWeaver based system and you also want to install the database on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="72985-287">Defina os seguintes parâmetros</span><span class="sxs-lookup"><span data-stu-id="72985-287">Enter the following parameters</span></span>
   1. <span data-ttu-id="72985-288">Prefixo de recurso (somente modelo multi-SID do ASCS/SCS)</span><span class="sxs-lookup"><span data-stu-id="72985-288">Resource Prefix (ASCS/SCS Multi SID template only)</span></span>  
      <span data-ttu-id="72985-289">Digite o prefixo que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="72985-289">Enter the prefix you want to use.</span></span> <span data-ttu-id="72985-290">O valor é usado como um prefixo para os recursos que serão implantados.</span><span class="sxs-lookup"><span data-stu-id="72985-290">The value is used as a prefix for the resources that are deployed.</span></span>
   3. <span data-ttu-id="72985-291">ID do sistema SAP (somente modelo convergido)</span><span class="sxs-lookup"><span data-stu-id="72985-291">Sap System Id (converged template only)</span></span>  
      <span data-ttu-id="72985-292">Insira a ID do sistema SAP do sistema SAP, que você deseja instalar.</span><span class="sxs-lookup"><span data-stu-id="72985-292">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="72985-293">A ID é usada como um prefixo para os recursos que serão implantados.</span><span class="sxs-lookup"><span data-stu-id="72985-293">The Id is used as a prefix for the resources that are deployed.</span></span>
   4. <span data-ttu-id="72985-294">Tipo de Pilha</span><span class="sxs-lookup"><span data-stu-id="72985-294">Stack Type</span></span>  
      <span data-ttu-id="72985-295">Selecionar o tipo de pilha do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="72985-295">Select the SAP NetWeaver stack type</span></span>
   5. <span data-ttu-id="72985-296">Tipo de sistema operacional</span><span class="sxs-lookup"><span data-stu-id="72985-296">Os Type</span></span>  
      <span data-ttu-id="72985-297">Selecione uma das distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="72985-297">Select one of the Linux distributions.</span></span> <span data-ttu-id="72985-298">Para este exemplo, selecione SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="72985-298">For this example, select SLES 12 BYOS</span></span>
   6. <span data-ttu-id="72985-299">Tipo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="72985-299">Db Type</span></span>  
      <span data-ttu-id="72985-300">Selecionar HANA</span><span class="sxs-lookup"><span data-stu-id="72985-300">Select HANA</span></span>
   7. <span data-ttu-id="72985-301">Tamanho do sistema SAP</span><span class="sxs-lookup"><span data-stu-id="72985-301">Sap System Size</span></span>  
      <span data-ttu-id="72985-302">A quantidade de SAPs que o novo sistema fornece.</span><span class="sxs-lookup"><span data-stu-id="72985-302">The amount of SAPS the new system provides.</span></span> <span data-ttu-id="72985-303">Se não tiver certeza de quantos SAPS o sistema precisará, pergunte ao Parceiro de Tecnologia SAP ou ao Integrador de Sistemas</span><span class="sxs-lookup"><span data-stu-id="72985-303">If you are not sure how many SAPS the system requires, please ask your SAP Technology Partner or System Integrator</span></span>
   8. <span data-ttu-id="72985-304">Disponibilidade do sistema</span><span class="sxs-lookup"><span data-stu-id="72985-304">System Availability</span></span>  
      <span data-ttu-id="72985-305">Selecione HA</span><span class="sxs-lookup"><span data-stu-id="72985-305">Select HA</span></span>
   9. <span data-ttu-id="72985-306">Nome de Usuário de Administrador e Senha do Administrador</span><span class="sxs-lookup"><span data-stu-id="72985-306">Admin Username and Admin Password</span></span>  
      <span data-ttu-id="72985-307">É criado um novo usuário que pode ser usado para fazer logon no computador.</span><span class="sxs-lookup"><span data-stu-id="72985-307">A new user is created that can be used to log on to the machine.</span></span>
   10. <span data-ttu-id="72985-308">ID da Sub-rede</span><span class="sxs-lookup"><span data-stu-id="72985-308">Subnet Id</span></span>  
   <span data-ttu-id="72985-309">A ID da sub-rede à qual as máquinas virtuais devem estar conectadas.</span><span class="sxs-lookup"><span data-stu-id="72985-309">The ID of the subnet to which the virtual machines should be connected to.</span></span>  <span data-ttu-id="72985-310">Deixe em branco se você deseja criar uma nova rede virtual ou selecione a mesma sub-rede usada ou criada como parte da implantação do servidor NFS.</span><span class="sxs-lookup"><span data-stu-id="72985-310">Leave empty if you want to create a new virtual network or select the same subnet that you used or created as part of the NFS server deployment.</span></span> <span data-ttu-id="72985-311">A ID geralmente tem esta aparência: /subscriptions/**&lt;id da assinatura&gt;**/resourceGroups/**&lt;nome do grupo de recursos&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;nome de rede virtual&gt;**/subnets/**&lt;nome da sub-rede&gt;**</span><span class="sxs-lookup"><span data-stu-id="72985-311">The ID usually looks like /subscriptions/**&lt;subscription id&gt;**/resourceGroups/**&lt;resource group name&gt;**/providers/Microsoft.Network/virtualNetworks/**&lt;virtual network name&gt;**/subnets/**&lt;subnet name&gt;**</span></span>

### <a name="installation"></a><span data-ttu-id="72985-312">Instalação</span><span class="sxs-lookup"><span data-stu-id="72985-312">Installation</span></span>

<span data-ttu-id="72985-313">Os itens a seguir são prefixados com **[A]** – aplicável a todos os nós, **[1]** – aplicável somente ao nó 1 ou **[2]** – aplicável somente ao nó 2.</span><span class="sxs-lookup"><span data-stu-id="72985-313">The following items are prefixed with either **[A]** - applicable to all nodes, **[1]** - only applicable to node 1 or **[2]** - only applicable to node 2.</span></span>

1. <span data-ttu-id="72985-314">**[A]** Atualizar o SLES</span><span class="sxs-lookup"><span data-stu-id="72985-314">**[A]** Update SLES</span></span>

   <pre><code>
   sudo zypper update
   </code></pre>

1. <span data-ttu-id="72985-315">**[1]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="72985-315">**[1]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

2. <span data-ttu-id="72985-316">**[2]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="72985-316">**[2]** Enable ssh access</span></span>

   <pre><code>
   sudo ssh-keygen -tdsa

   # insert the public key you copied in the last step into the authorized keys file on the second server
   sudo vi /root/.ssh/authorized_keys
   
   # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
   # Enter passphrase (empty for no passphrase): -> ENTER
   # Enter same passphrase again: -> ENTER
   
   # copy the public key   
   sudo cat /root/.ssh/id_dsa.pub
   </code></pre>

1. <span data-ttu-id="72985-317">**[1]** Habilitar o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="72985-317">**[1]** Enable ssh access</span></span>

   <pre><code>
   # insert the public key you copied in the last step into the authorized keys file on the first server
   sudo vi /root/.ssh/authorized_keys
   </code></pre>

1. <span data-ttu-id="72985-318">**[A]** Instalar a extensão HA</span><span class="sxs-lookup"><span data-stu-id="72985-318">**[A]** Install HA extension</span></span>
   
   <pre><code>
   sudo zypper install sle-ha-release fence-agents
   </code></pre>

1. <span data-ttu-id="72985-319">**[A]** Atualizar agentes de recurso SAP</span><span class="sxs-lookup"><span data-stu-id="72985-319">**[A]** Update SAP resource agents</span></span>  
   
   <span data-ttu-id="72985-320">Um patch para o pacote de agentes de recurso é necessário para usar a nova configuração, que é descrita neste artigo.</span><span class="sxs-lookup"><span data-stu-id="72985-320">A patch for the resource-agents package is required to use the new configuration, that is described in this article.</span></span> <span data-ttu-id="72985-321">Você pode verificar, se o patch já está instalado com o comando a seguir</span><span class="sxs-lookup"><span data-stu-id="72985-321">You can check, if the patch is already installed with the following command</span></span>

   <pre><code>
   sudo grep 'parameter name="IS_ERS"' /usr/lib/ocf/resource.d/heartbeat/SAPInstance
   </code></pre>

   <span data-ttu-id="72985-322">A saída deverá ser semelhante a</span><span class="sxs-lookup"><span data-stu-id="72985-322">The output should be similar to</span></span>

   <pre><code>
   &lt;parameter name="IS_ERS" unique="0" required="0"&gt;
   </code></pre>

   <span data-ttu-id="72985-323">Se o comando grep não localizar o parâmetro IS_ERS, você precisará instalar o patch listado na [página de download do SUSE](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span><span class="sxs-lookup"><span data-stu-id="72985-323">If the grep command does not find the IS_ERS parameter, you need to install the patch listed on [the SUSE download page](https://download.suse.com/patch/finder/#bu=suse&familyId=&productId=&dateRange=&startDate=&endDate=&priority=&architecture=&keywords=resource-agents)</span></span>

   <pre><code>
   # example for patch for SLES 12 SP1
   sudo zypper in -t patch SUSE-SLE-HA-12-SP1-2017-885=1
   # example for patch for SLES 12 SP2
   sudo zypper in -t patch SUSE-SLE-HA-12-SP2-2017-886=1
   </code></pre>

1. <span data-ttu-id="72985-324">**[A]** Configurar a resolução de nome do host</span><span class="sxs-lookup"><span data-stu-id="72985-324">**[A]** Setup host name resolution</span></span>   

   <span data-ttu-id="72985-325">Você pode usar um servidor DNS ou modificar /etc/hosts em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="72985-325">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="72985-326">Este exemplo mostra como usar o arquivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="72985-326">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="72985-327">Substitua o endereço IP e o nome do host nos comandos a seguir</span><span class="sxs-lookup"><span data-stu-id="72985-327">Replace the IP address and the hostname in the following commands</span></span>

   <pre><code>
   sudo vi /etc/hosts
   </code></pre>
   
   <span data-ttu-id="72985-328">Insira as seguintes linhas para /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="72985-328">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="72985-329">Altere o endereço IP e o nome do host para corresponder ao seu ambiente</span><span class="sxs-lookup"><span data-stu-id="72985-329">Change the IP address and hostname to match your environment</span></span>   
   
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   </code></pre>

1. <span data-ttu-id="72985-330">**[1]** Instalar o Cluster</span><span class="sxs-lookup"><span data-stu-id="72985-330">**[1]** Install Cluster</span></span>
   
   <pre><code>
   sudo ha-cluster-init
   
   # Do you want to continue anyway? [y/N] -> y
   # Network address to bind to (for example: 192.168.1.0) [10.79.227.0] -> ENTER
   # Multicast address (for example: 239.x.x.x) [239.174.218.125] -> ENTER
   # Multicast port [5405] -> ENTER
   # Do you wish to use SBD? [y/N] -> N
   # Do you wish to configure an administration IP? [y/N] -> N
   </code></pre>

1. <span data-ttu-id="72985-331">**[2]** Adicionar nó ao cluster</span><span class="sxs-lookup"><span data-stu-id="72985-331">**[2]** Add node to cluster</span></span>
   
   <pre><code> 
   sudo ha-cluster-join

   # WARNING: NTP is not configured to start at system boot.
   # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
   # Do you want to continue anyway? [y/N] -> y
   # IP address or hostname of existing node (for example: 192.168.1.1) [] -> IP address of node 1 for example 10.0.0.10
   # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
   </code></pre>

1. <span data-ttu-id="72985-332">**[A]** Alterar a senha hacluster para a mesma senha</span><span class="sxs-lookup"><span data-stu-id="72985-332">**[A]** Change hacluster password to the same password</span></span>

   <pre><code> 
   sudo passwd hacluster
   </code></pre>

1. <span data-ttu-id="72985-333">**[A]** Configurar corosync para usar outro transporte e adicione nodelist.</span><span class="sxs-lookup"><span data-stu-id="72985-333">**[A]** Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="72985-334">Caso contrário, o cluster não funcionará.</span><span class="sxs-lookup"><span data-stu-id="72985-334">Cluster will not work otherwise.</span></span>
   
   <pre><code> 
   sudo vi /etc/corosync/corosync.conf   
   </code></pre>

   <span data-ttu-id="72985-335">Adicione o conteúdo em negrito a seguir ao arquivo.</span><span class="sxs-lookup"><span data-stu-id="72985-335">Add the following bold content to the file.</span></span>
   
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

   <span data-ttu-id="72985-336">Em seguida, reinicie o serviço corosync</span><span class="sxs-lookup"><span data-stu-id="72985-336">Then restart the corosync service</span></span>

   <pre><code>
   sudo service corosync restart
   </code></pre>

1. <span data-ttu-id="72985-337">**[A]** Instalar componentes drbd</span><span class="sxs-lookup"><span data-stu-id="72985-337">**[A]** Install drbd components</span></span>

   <pre><code>
   sudo zypper install drbd drbd-kmp-default drbd-utils
   </code></pre>

1. <span data-ttu-id="72985-338">**[A]** Criar uma partição para o dispositivo drbd</span><span class="sxs-lookup"><span data-stu-id="72985-338">**[A]** Create a partition for the drbd device</span></span>

   <pre><code>
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdc'
   </code></pre>

1. <span data-ttu-id="72985-339">**[A]** Criar configurações de LVM</span><span class="sxs-lookup"><span data-stu-id="72985-339">**[A]** Create LVM configurations</span></span>

   <pre><code>
   sudo pvcreate /dev/sdc1   
   sudo vgcreate vg_<b>NWS</b> /dev/sdc1
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ASCS vg_<b>NWS</b>
   sudo lvcreate -l 50%FREE -n <b>NWS</b>_ERS vg_<b>NWS</b>
   </code></pre>

1. <span data-ttu-id="72985-340">**[A]** Criar o dispositivo drbd do SCS</span><span class="sxs-lookup"><span data-stu-id="72985-340">**[A]** Create the SCS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ascs.res
   </code></pre>

   <span data-ttu-id="72985-341">Inserir a configuração para o novo dispositivo drbd e sair</span><span class="sxs-lookup"><span data-stu-id="72985-341">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="72985-342">Criar o dispositivo drbd e iniciá-lo</span><span class="sxs-lookup"><span data-stu-id="72985-342">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ascs
   sudo drbdadm up <b>NWS</b>_ascs
   </code></pre>

1. <span data-ttu-id="72985-343">**[A]** Criar o dispositivo drbd do ERS</span><span class="sxs-lookup"><span data-stu-id="72985-343">**[A]** Create the ERS drbd device</span></span>

   <pre><code>
   sudo vi /etc/drbd.d/<b>NWS</b>_ers.res
   </code></pre>

   <span data-ttu-id="72985-344">Inserir a configuração para o novo dispositivo drbd e sair</span><span class="sxs-lookup"><span data-stu-id="72985-344">Insert the configuration for the new drbd device and exit</span></span>

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

   <span data-ttu-id="72985-345">Criar o dispositivo drbd e iniciá-lo</span><span class="sxs-lookup"><span data-stu-id="72985-345">Create the drbd device and start it</span></span>

   <pre><code>
   sudo drbdadm create-md <b>NWS</b>_ers
   sudo drbdadm up <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="72985-346">**[1]** Ignorar a sincronização inicial</span><span class="sxs-lookup"><span data-stu-id="72985-346">**[1]** Skip initial synchronization</span></span>

   <pre><code>
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ascs
   sudo drbdadm new-current-uuid --clear-bitmap <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="72985-347">**[1]**  Definir o nó principal</span><span class="sxs-lookup"><span data-stu-id="72985-347">**[1]** Set the primary node</span></span>

   <pre><code>
   sudo drbdadm primary --force <b>NWS</b>_ascs
   sudo drbdadm primary --force <b>NWS</b>_ers
   </code></pre>

1. <span data-ttu-id="72985-348">**[1]** Aguardar até que os novos dispositivos drbd sejam sincronizados</span><span class="sxs-lookup"><span data-stu-id="72985-348">**[1]** Wait until the new drbd devices are synchronized</span></span>

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

1. <span data-ttu-id="72985-349">**[1]** Criar sistemas de arquivos nos dispositivos drbd</span><span class="sxs-lookup"><span data-stu-id="72985-349">**[1]** Create file systems on the drbd devices</span></span>

   <pre><code>
   sudo mkfs.xfs /dev/drbd0
   sudo mkfs.xfs /dev/drbd1
   </code></pre>


### <a name="configure-cluster-framework"></a><span data-ttu-id="72985-350">Configurar a estrutura do cluster</span><span class="sxs-lookup"><span data-stu-id="72985-350">Configure Cluster Framework</span></span>

<span data-ttu-id="72985-351">**[1]** Alterar as configurações padrão</span><span class="sxs-lookup"><span data-stu-id="72985-351">**[1]** Change the default settings</span></span>

   <pre><code>
   sudo crm configure

   crm(live)configure# rsc_defaults resource-stickiness="1"

   crm(live)configure# commit
   crm(live)configure# exit
   </code></pre>

## <a name="prepare-for-sap-netweaver-installation"></a><span data-ttu-id="72985-352">Preparar para a instalação do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="72985-352">Prepare for SAP NetWeaver installation</span></span>

1. <span data-ttu-id="72985-353">**[A]** Criar os diretórios compartilhados</span><span class="sxs-lookup"><span data-stu-id="72985-353">**[A]** Create the shared directories</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans
   sudo mkdir -p /usr/sap/<b>NWS</b>/SYS

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   sudo chattr +i /usr/sap/<b>NWS</b>/SYS
   </code></pre>

1. <span data-ttu-id="72985-354">**[A]**  Configurar o autofs</span><span class="sxs-lookup"><span data-stu-id="72985-354">**[A]** Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="72985-355">Crie um arquivo com</span><span class="sxs-lookup"><span data-stu-id="72985-355">Create a file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   /usr/sap/<b>NWS</b>/SYS -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sidsys
   </code></pre>

   <span data-ttu-id="72985-356">Reiniciar o autofs para montar os novos compartilhamentos</span><span class="sxs-lookup"><span data-stu-id="72985-356">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="72985-357">**[A]** Configurar arquivo de permuta</span><span class="sxs-lookup"><span data-stu-id="72985-357">**[A]** Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="72985-358">Reiniciar o agente para ativar a alteração</span><span class="sxs-lookup"><span data-stu-id="72985-358">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

### <a name="installing-sap-netweaver-ascsers"></a><span data-ttu-id="72985-359">Instalação do ASCS/ERS do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="72985-359">Installing SAP NetWeaver ASCS/ERS</span></span>

1. <span data-ttu-id="72985-360">**[1]** Criar um recurso de IP virtual e a investigação de integridade para o balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="72985-360">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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

   <span data-ttu-id="72985-361">Verifique se o status do cluster é ok e se todos os recursos estão iniciados.</span><span class="sxs-lookup"><span data-stu-id="72985-361">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="72985-362">Não importa em qual nó os recursos estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="72985-362">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="72985-363">**[1]** Instalar o ASCS do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="72985-363">**[1]** Install SAP NetWeaver ASCS</span></span>  

   <span data-ttu-id="72985-364">Instalar o ASCS do SAP NetWeaver como raiz no primeiro nó usando um nome de host virtual que mapeia para o endereço IP de configuração de front-end do balanceador de carga para o ASCS, por exemplo, <b>nws-ascs</b>, <b>10.0.0.10</b> e o número de instância que você usou para a investigação do balanceador de carga, por exemplo, <b>00</b>.</span><span class="sxs-lookup"><span data-stu-id="72985-364">Install SAP NetWeaver ASCS as root on the first node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ASCS for example <b>nws-ascs</b>, <b>10.0.0.10</b> and the instance number that you used for the probe of the load balancer for example <b>00</b>.</span></span>

   <span data-ttu-id="72985-365">Você pode usar o parâmetro sapinst SAPINST_REMOTE_ACCESS_USER para permitir que um usuário não raiz se conecte ao sapinst.</span><span class="sxs-lookup"><span data-stu-id="72985-365">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="72985-366">**[1]** Criar um recurso de IP virtual e a investigação de integridade para o balanceador de carga interno</span><span class="sxs-lookup"><span data-stu-id="72985-366">**[1]** Create a virtual IP resource and health-probe for the internal load balancer</span></span>

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
   # Do you still want to commit (y/n)? y

   crm(live)configure# exit
   
   </code></pre>
 
   <span data-ttu-id="72985-367">Verifique se o status do cluster é ok e se todos os recursos estão iniciados.</span><span class="sxs-lookup"><span data-stu-id="72985-367">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="72985-368">Não importa em qual nó os recursos estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="72985-368">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="72985-369">**[2]** Instalar o ERS do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="72985-369">**[2]** Install SAP NetWeaver ERS</span></span>  

   <span data-ttu-id="72985-370">Instalar o ERS do SAP NetWeaver como raiz no segundo nó usando um nome de host virtual que mapeia para o endereço IP de configuração de front-end do balanceador de carga para o ERS, por exemplo, <b>nws-ers</b>, <b>10.0.0.11</b> e o número de instância que você usou para a investigação do balanceador de carga, por exemplo, <b>02</b>.</span><span class="sxs-lookup"><span data-stu-id="72985-370">Install SAP NetWeaver ERS as root on the second node using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the ERS for example <b>nws-ers</b>, <b>10.0.0.11</b> and the instance number that you used for the probe of the load balancer for example <b>02</b>.</span></span>

   <span data-ttu-id="72985-371">Você pode usar o parâmetro sapinst SAPINST_REMOTE_ACCESS_USER para permitir que um usuário não raiz se conecte ao sapinst.</span><span class="sxs-lookup"><span data-stu-id="72985-371">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

   > [!NOTE]
   > <span data-ttu-id="72985-372">Use SWPM SP 20 PL 05 ou superior.</span><span class="sxs-lookup"><span data-stu-id="72985-372">Please use SWPM SP 20 PL 05 or higher.</span></span> <span data-ttu-id="72985-373">Versões anteriores não configurarão as permissões corretamente e a instalação falhará.</span><span class="sxs-lookup"><span data-stu-id="72985-373">Lower versions do not set the permissions correctly and the installation will fail.</span></span>
   > 

1. <span data-ttu-id="72985-374">**[1]** Adaptar os perfis de instância do ASCS/SCS e do ERS</span><span class="sxs-lookup"><span data-stu-id="72985-374">**[1]** Adapt the ASCS/SCS and ERS instance profiles</span></span>
 
   * <span data-ttu-id="72985-375">Perfil do ASCS/SCS</span><span class="sxs-lookup"><span data-stu-id="72985-375">ASCS/SCS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_<b>ASCS00</b>_<b>nws-ascs</b>

   # Change the restart command to a start command
   #Restart_Program_01 = local $(_EN) pf=$(_PF)
   Start_Program_01 = local $(_EN) pf=$(_PF)

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector

   # Add the keep alive parameter
   enque/encni/set_so_keepalive = true
   </code></pre>

   * <span data-ttu-id="72985-376">Perfil do ERS</span><span class="sxs-lookup"><span data-stu-id="72985-376">ERS profile</span></span>

   <pre><code> 
   sudo vi /sapmnt/<b>NWS</b>/profile/<b>NWS</b>_ERS<b>02</b>_<b>nws-ers</b>

   # Add the following lines
   service/halib = $(DIR_CT_RUN)/saphascriptco.so
   service/halib_cluster_connector = /usr/bin/sap_suse_cluster_connector
   </code></pre>


1. <span data-ttu-id="72985-377">**[A]** Configurar Keep Alive</span><span class="sxs-lookup"><span data-stu-id="72985-377">**[A]** Configure Keep Alive</span></span>

   <span data-ttu-id="72985-378">A comunicação entre o servidor de aplicativos do SAP NetWeaver e o ASCS/SCS é roteada por meio de um balanceador de carga de software.</span><span class="sxs-lookup"><span data-stu-id="72985-378">The communication between the SAP NetWeaver application server and the ASCS/SCS is routed through a software load balancer.</span></span> <span data-ttu-id="72985-379">O balanceador de carga desconecta conexões inativas após um tempo limite configurável.</span><span class="sxs-lookup"><span data-stu-id="72985-379">The load balancer disconnects inactive connections after a configurable timeout.</span></span> <span data-ttu-id="72985-380">Para evitar isso, você precisa definir um parâmetro no perfil do SAP NetWeaver ASCS/SCS e alterar as configurações do sistema Linux.</span><span class="sxs-lookup"><span data-stu-id="72985-380">To prevent this you need to set a parameter in the SAP NetWeaver ASCS/SCS profile and change the Linux system settings.</span></span> <span data-ttu-id="72985-381">Leia a [Nota SAP 1410736][1410736] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="72985-381">Please read [SAP Note 1410736][1410736] for more information.</span></span>
   
   <span data-ttu-id="72985-382">O parâmetro enque/encni/set_so_keepalive do perfil do ASCS/SCS já foi adicionado na última etapa.</span><span class="sxs-lookup"><span data-stu-id="72985-382">The ASCS/SCS profile parameter enque/encni/set_so_keepalive was already added in the last step.</span></span>

   <pre><code> 
   # Change the Linux system configuration
   sudo sysctl net.ipv4.tcp_keepalive_time=120
   </code></pre>

1. <span data-ttu-id="72985-383">**[A]** Configurar os usuários do SAP após a instalação</span><span class="sxs-lookup"><span data-stu-id="72985-383">**[A]** Configure the SAP users after the installation</span></span>
 
   <pre><code>
   # Add sidadm to the haclient group
   sudo usermod -aG haclient <b>nws</b>adm   
   </code></pre>

1. <span data-ttu-id="72985-384">**[1]** Adicionar os serviços de ERS SAP ASCS ao arquivo sapservice</span><span class="sxs-lookup"><span data-stu-id="72985-384">**[1]** Add the ASCS and ERS SAP services to the sapservice file</span></span>

   <span data-ttu-id="72985-385">Adicione a entrada de serviço do ASCS ao segundo nó e copie a entrada de serviço de ERS para o primeiro nó.</span><span class="sxs-lookup"><span data-stu-id="72985-385">Add the ASCS service entry to the second node and copy the ERS service entry to the first node.</span></span>

   <pre><code>
   cat /usr/sap/sapservices | grep ASCS<b>00</b> | sudo ssh <b>nws-cl-1</b> "cat >>/usr/sap/sapservices"
   sudo ssh <b>nws-cl-1</b> "cat /usr/sap/sapservices" | grep ERS<b>02</b> | sudo tee -a /usr/sap/sapservices
   </code></pre>

1. <span data-ttu-id="72985-386">**[1]** Criar os recursos de cluster do SAP</span><span class="sxs-lookup"><span data-stu-id="72985-386">**[1]** Create the SAP cluster resources</span></span>

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

   <span data-ttu-id="72985-387">Verifique se o status do cluster é ok e se todos os recursos estão iniciados.</span><span class="sxs-lookup"><span data-stu-id="72985-387">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="72985-388">Não importa em qual nó os recursos estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="72985-388">It is not important on which node the resources are running.</span></span>

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

### <a name="create-stonith-device"></a><span data-ttu-id="72985-389">Criar dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="72985-389">Create STONITH device</span></span>

<span data-ttu-id="72985-390">O dispositivo STONITH usa uma Entidade de Serviço para autorização no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="72985-390">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="72985-391">Siga estas etapas para criar uma Entidade de Serviço.</span><span class="sxs-lookup"><span data-stu-id="72985-391">Follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="72985-392">Acesse <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="72985-392">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="72985-393">Abra a folha Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="72985-393">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="72985-394">Vá para Propriedades e anote a ID do Diretório.</span><span class="sxs-lookup"><span data-stu-id="72985-394">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="72985-395">Essa é a **id de locatário**.</span><span class="sxs-lookup"><span data-stu-id="72985-395">This is the **tenant id**.</span></span>
1. <span data-ttu-id="72985-396">Clique em Registros do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="72985-396">Click App registrations</span></span>
1. <span data-ttu-id="72985-397">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="72985-397">Click Add</span></span>
1. <span data-ttu-id="72985-398">Digite um Nome, selecione Tipo de Aplicativo "Aplicativo Web/API", insira uma URL de logon (por exemplo, http://localhost) e clique em Criar</span><span class="sxs-lookup"><span data-stu-id="72985-398">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="72985-399">A URL de logon não é usada e pode ser qualquer URL válida</span><span class="sxs-lookup"><span data-stu-id="72985-399">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="72985-400">Selecione o novo Aplicativo e clique em Chaves na guia Configurações</span><span class="sxs-lookup"><span data-stu-id="72985-400">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="72985-401">Insira uma descrição para uma nova chave, selecione "Nunca expira" e clique em Salvar</span><span class="sxs-lookup"><span data-stu-id="72985-401">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="72985-402">Anote o Valor.</span><span class="sxs-lookup"><span data-stu-id="72985-402">Write down the Value.</span></span> <span data-ttu-id="72985-403">Ele é usado como **senha** da Entidade de Serviço</span><span class="sxs-lookup"><span data-stu-id="72985-403">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="72985-404">Anote a ID do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="72985-404">Write down the Application Id.</span></span> <span data-ttu-id="72985-405">Ela é usada como nome de usuário (**id de logon** nas etapas abaixo) da Entidade de Serviço</span><span class="sxs-lookup"><span data-stu-id="72985-405">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="72985-406">A Entidade de Serviço não tem permissões para acessar os recursos do Azure por padrão.</span><span class="sxs-lookup"><span data-stu-id="72985-406">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="72985-407">Você precisa fornecer as permissões da Entidade de Serviço para iniciar e parar (desalocar) todas as máquinas virtuais do cluster.</span><span class="sxs-lookup"><span data-stu-id="72985-407">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="72985-408">Acesse https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="72985-408">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="72985-409">Abra a folha Todos os recursos</span><span class="sxs-lookup"><span data-stu-id="72985-409">Open the All resources blade</span></span>
1. <span data-ttu-id="72985-410">Selecione a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="72985-410">Select the virtual machine</span></span>
1. <span data-ttu-id="72985-411">Clique em Controle de acesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="72985-411">Click Access control (IAM)</span></span>
1. <span data-ttu-id="72985-412">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="72985-412">Click Add</span></span>
1. <span data-ttu-id="72985-413">Selecione a função Proprietário</span><span class="sxs-lookup"><span data-stu-id="72985-413">Select the role Owner</span></span>
1. <span data-ttu-id="72985-414">Digite o nome do aplicativo criado acima</span><span class="sxs-lookup"><span data-stu-id="72985-414">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="72985-415">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="72985-415">Click OK</span></span>

#### <a name="1-create-the-stonith-devices"></a><span data-ttu-id="72985-416">**[1]** Criar os dispositivos STONITH</span><span class="sxs-lookup"><span data-stu-id="72985-416">**[1]** Create the STONITH devices</span></span>

<span data-ttu-id="72985-417">Depois de editar as permissões das máquinas virtuais, você pode configurar os dispositivos STONITH no cluster.</span><span class="sxs-lookup"><span data-stu-id="72985-417">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre><code>
sudo crm configure

# replace the bold string with your subscription id, resource group, tenant id, service principal id and password

crm(live)configure# primitive rsc_st_azure_1 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# primitive rsc_st_azure_2 stonith:fence_azure_arm \
   params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

crm(live)configure# colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started

crm(live)configure# commit
crm(live)configure# exit
</code></pre>

#### <a name="1-enable-the-use-of-a-stonith-device"></a><span data-ttu-id="72985-418">**[1]** Habilitar o uso de um dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="72985-418">**[1]** Enable the use of a STONITH device</span></span>

<span data-ttu-id="72985-419">Habilitar o uso de um dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="72985-419">Enable the use of a STONITH device</span></span>

<pre><code>
sudo crm configure property stonith-enabled=true 
</code></pre>

## <a name="install-database"></a><span data-ttu-id="72985-420">Instalar banco de dados</span><span class="sxs-lookup"><span data-stu-id="72985-420">Install database</span></span>

<span data-ttu-id="72985-421">Neste exemplo, uma replicação de sistema do SAP HANA está instalada e configurada.</span><span class="sxs-lookup"><span data-stu-id="72985-421">In this example an SAP HANA System Replication is installed and configured.</span></span> <span data-ttu-id="72985-422">O SAP HANA será executado no mesmo cluster que o ASCS/SCS e o ERS do SAP NetWeaver.</span><span class="sxs-lookup"><span data-stu-id="72985-422">SAP HANA will run in the same cluster as the SAP NetWeaver ASCS/SCS and ERS.</span></span> <span data-ttu-id="72985-423">Você também pode instalar o SAP HANA em um cluster dedicado.</span><span class="sxs-lookup"><span data-stu-id="72985-423">You can also install SAP HANA on a dedicated cluster.</span></span> <span data-ttu-id="72985-424">Veja [Alta disponibilidade do SAP HANA em VMs (máquinas virtuais) do Azure][sap-hana-ha] para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="72985-424">See [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha] for more information.</span></span>

### <a name="prepare-for-sap-hana-installation"></a><span data-ttu-id="72985-425">Preparar para a instalação do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="72985-425">Prepare for SAP HANA installation</span></span>

<span data-ttu-id="72985-426">Normalmente, é recomendável usar LVM para volumes que armazenam arquivos de log e dados.</span><span class="sxs-lookup"><span data-stu-id="72985-426">We generally recommend using LVM for volumes that store data and log files.</span></span> <span data-ttu-id="72985-427">Para fins de teste, você também pode escolher armazenar os dados e o arquivo de log diretamente em um disco simples.</span><span class="sxs-lookup"><span data-stu-id="72985-427">For testing purposes, you can also choose to store the data and log file directly on a plain disk.</span></span>

1. <span data-ttu-id="72985-428">**[A]** LVM</span><span class="sxs-lookup"><span data-stu-id="72985-428">**[A]** LVM</span></span>  
   <span data-ttu-id="72985-429">O exemplo abaixo pressupõe que as máquinas virtuais tenham quatro discos de dados anexados que devem ser usados para criar dois volumes.</span><span class="sxs-lookup"><span data-stu-id="72985-429">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
   
   <span data-ttu-id="72985-430">Crie volumes físicos para todos os discos que queira usar.</span><span class="sxs-lookup"><span data-stu-id="72985-430">Create physical volumes for all disks that you want to use.</span></span>
   
   <pre><code>
   sudo pvcreate /dev/sdd
   sudo pvcreate /dev/sde
   sudo pvcreate /dev/sdf
   sudo pvcreate /dev/sdg
   </code></pre>
   
   <span data-ttu-id="72985-431">Crie um grupo de volume para os arquivos de dados, um grupo de volume para os arquivos de log e um para o diretório compartilhado do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="72985-431">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
   
   <pre><code>
   sudo vgcreate vg_hana_data /dev/sdd /dev/sde
   sudo vgcreate vg_hana_log /dev/sdf
   sudo vgcreate vg_hana_shared /dev/sdg
   </code></pre>
   
   <span data-ttu-id="72985-432">Criar os volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="72985-432">Create the logical volumes</span></span>
   
   <pre><code>
   sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
   sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
   sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
   sudo mkfs.xfs /dev/vg_hana_data/hana_data
   sudo mkfs.xfs /dev/vg_hana_log/hana_log
   sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
   </code></pre>
   
   <span data-ttu-id="72985-433">Crie os diretórios de montagem e copie a UUID de todos os volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="72985-433">Create the mount directories and copy the UUID of all logical volumes</span></span>
   
   <pre><code>
   sudo mkdir -p /hana/data
   sudo mkdir -p /hana/log
   sudo mkdir -p /hana/shared
   sudo chattr +i /hana/data
   sudo chattr +i /hana/log
   sudo chattr +i /hana/shared
   # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
   sudo blkid
   </code></pre>
   
   <span data-ttu-id="72985-434">Criar entradas autofs para os três volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="72985-434">Create autofs entries for the three logical volumes</span></span>
   
   <pre><code>
   sudo vi /etc/auto.direct
   </code></pre>
   
   <span data-ttu-id="72985-435">Inserir essa linha em sudo vi /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="72985-435">Insert this line to sudo vi /etc/auto.direct</span></span>
   
   <pre><code>
   /hana/data -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b>
   /hana/log -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b>
   /hana/shared -fstype=xfs :UUID=<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b>
   </code></pre>
   
   <span data-ttu-id="72985-436">Monte os novos volumes</span><span class="sxs-lookup"><span data-stu-id="72985-436">Mount the new volumes</span></span>
   
   <pre><code>
   sudo service autofs restart 
   </code></pre>

1. <span data-ttu-id="72985-437">**[A]** Discos simples</span><span class="sxs-lookup"><span data-stu-id="72985-437">**[A]** Plain Disks</span></span>  

   <span data-ttu-id="72985-438">Para sistemas pequenos ou de demonstração, você pode colocar os arquivos de log e dados do HANA em um disco.</span><span class="sxs-lookup"><span data-stu-id="72985-438">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="72985-439">Os comandos a seguir criam uma partição em /dev/sdc e a formatam com xfs.</span><span class="sxs-lookup"><span data-stu-id="72985-439">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
   ```bash
   sudo sh -c 'echo -e "n\n\n\n\n\nw\n" | fdisk /dev/sdd'
   sudo mkfs.xfs /dev/sdd1
   
   # write down the id of /dev/sdd1
   sudo /sbin/blkid
   sudo vi /etc/auto.direct
   ```
   
   <span data-ttu-id="72985-440">Inserir essa linha em /etc/auto.direct</span><span class="sxs-lookup"><span data-stu-id="72985-440">Insert this line to /etc/auto.direct</span></span>
   <pre><code>
   /hana -fstype=xfs :UUID=<b>&lt;UUID&gt;</b>
   </code></pre>
   
   <span data-ttu-id="72985-441">Crie o diretório de destino e monte o disco.</span><span class="sxs-lookup"><span data-stu-id="72985-441">Create the target directory and mount the disk.</span></span>
   
   <pre><code>
   sudo mkdir /hana
   sudo chattr +i /hana
   sudo service autofs restart
   </code></pre>

### <a name="installing-sap-hana"></a><span data-ttu-id="72985-442">Instalando o SAP HANA</span><span class="sxs-lookup"><span data-stu-id="72985-442">Installing SAP HANA</span></span>

<span data-ttu-id="72985-443">As etapas a seguir se baseiam no capítulo 4 do [guia Cenário Otimizado para Desempenho da SR SAP HANA][suse-hana-ha-guide] para instalar a Replicação do Sistema SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="72985-443">The following steps are based on chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span> <span data-ttu-id="72985-444">Leia antes de continuar a instalação.</span><span class="sxs-lookup"><span data-stu-id="72985-444">Please read it before you continue the installation.</span></span>

1. <span data-ttu-id="72985-445">**[A]** Executar hdblcm no DVD do HANA</span><span class="sxs-lookup"><span data-stu-id="72985-445">**[A]** Run hdblcm from the HANA DVD</span></span>
   
   <pre><code>
   sudo hdblcm --sid=<b>HDB</b> --number=<b>03</b> --action=install --batch --password=<b>&lt;password&gt;</b> --system_user_password=<b>&lt;password for system user&gt;</b>

   sudo /hana/shared/<b>HDB</b>/hdblcm/hdblcm --action=configure_internal_network --listen_interface=internal --internal_network=<b>10.0.0/24</b> --password=<b>&lt;password for system user&gt;</b> --batch
   </code></pre>

1. <span data-ttu-id="72985-446">**[A]** Atualizar o Agente do Host do SAP</span><span class="sxs-lookup"><span data-stu-id="72985-446">**[A]** Upgrade SAP Host Agent</span></span>

   <span data-ttu-id="72985-447">Baixe o arquivo mais recente do Agente do Host do SAP em [SAP Softwarecenter][sap-swcenter] e execute o comando a seguir para fazer upgrade do agente.</span><span class="sxs-lookup"><span data-stu-id="72985-447">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="72985-448">Substitua o caminho do arquivo de modo a apontar para o arquivo que você baixou.</span><span class="sxs-lookup"><span data-stu-id="72985-448">Replace the path to the archive to point to the file you downloaded.</span></span>
   <pre><code>
   sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <b>&lt;path to SAP Host Agent SAR&gt;</b> 
   </code></pre>

1. <span data-ttu-id="72985-449">**[1]** Criar uma replicação HANA (como raiz)</span><span class="sxs-lookup"><span data-stu-id="72985-449">**[1]** Create HANA replication (as root)</span></span>  

   <span data-ttu-id="72985-450">Execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="72985-450">Run the following command.</span></span> <span data-ttu-id="72985-451">Não se esqueça de substituir cadeias de caracteres em negrito (HDB da ID do Sistema HANA e o número de instância 03) pelos valores da sua instalação SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="72985-451">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
   hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
   hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
   </code></pre>

1. <span data-ttu-id="72985-452">**[A]** Criar entrada de repositório de chaves (como raiz)</span><span class="sxs-lookup"><span data-stu-id="72985-452">**[A]** Create keystore entry (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>&lt;passwd&gt;</b>
   </code></pre>

1. <span data-ttu-id="72985-453">**[1]** Fazer o backup do banco de dados backup (como raiz)</span><span class="sxs-lookup"><span data-stu-id="72985-453">**[1]** Backup database (as root)</span></span>

   <pre><code>
   PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
   hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
   </code></pre>

1. <span data-ttu-id="72985-454">**[1]** Mudar para o usuário sapsid (por exemplo, hdbadm) do HANA e criar o site primário.</span><span class="sxs-lookup"><span data-stu-id="72985-454">**[1]** Switch to the HANA sapsid user and create the primary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   hdbnsutil -sr_enable –-name=<b>SITE1</b>
   </code></pre>

1. <span data-ttu-id="72985-455">**[2]** Mudar para o usuário sapsid (por exemplo, hdbadm) do HANA e criar o site secundário.</span><span class="sxs-lookup"><span data-stu-id="72985-455">**[2]** Switch to the HANA sapsid user and create the secondary site.</span></span>

   <pre><code>
   su - <b>hdb</b>adm
   sapcontrol -nr <b>03</b> -function StopWait 600 10
   hdbnsutil -sr_register --remoteHost=<b>nws-cl-0</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
   </code></pre>

1. <span data-ttu-id="72985-456">**[1]** Criar os recursos de cluster do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="72985-456">**[1]** Create SAP HANA cluster resources</span></span>

   <span data-ttu-id="72985-457">Primeiro, crie a topologia.</span><span class="sxs-lookup"><span data-stu-id="72985-457">First, create the topology.</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number and HANA system id
   
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
   
   <span data-ttu-id="72985-458">Em seguida, crie os recursos do HANA</span><span class="sxs-lookup"><span data-stu-id="72985-458">Next, create the HANA resources</span></span>
   
   <pre><code>
   sudo crm configure

   # replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
    
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

   <span data-ttu-id="72985-459">Verifique se o status do cluster é ok e se todos os recursos estão iniciados.</span><span class="sxs-lookup"><span data-stu-id="72985-459">Make sure that the cluster status is ok and that all resources are started.</span></span> <span data-ttu-id="72985-460">Não importa em qual nó os recursos estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="72985-460">It is not important on which node the resources are running.</span></span>

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

1. <span data-ttu-id="72985-461">**[1]** Instalar a instância de banco de dados do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="72985-461">**[1]** Install the SAP NetWeaver database instance</span></span>

   <span data-ttu-id="72985-462">Instale a instância de banco de dados do SAP NetWeaver como raiz usando um nome de host virtual que mapeia para o endereço IP de configuração de front-end do balanceador de carga para o banco de dados, por exemplo, <b>nws-db</b> e <b>10.0.0.12</b>.</span><span class="sxs-lookup"><span data-stu-id="72985-462">Install the SAP NetWeaver database instance as root using a virtual hostname that maps to the IP address of the load balancer frontend configuration for the database for example <b>nws-db</b> and <b>10.0.0.12</b>.</span></span>

   <span data-ttu-id="72985-463">Você pode usar o parâmetro sapinst SAPINST_REMOTE_ACCESS_USER para permitir que um usuário não raiz se conecte ao sapinst.</span><span class="sxs-lookup"><span data-stu-id="72985-463">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

## <a name="sap-netweaver-application-server-installation"></a><span data-ttu-id="72985-464">Instalação de servidor de aplicativos do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="72985-464">SAP NetWeaver application server installation</span></span>

<span data-ttu-id="72985-465">Siga estas etapas para instalar um servidor de aplicativos SAP.</span><span class="sxs-lookup"><span data-stu-id="72985-465">Follow these steps to install an SAP application server.</span></span> <span data-ttu-id="72985-466">As etapas abaixo pressupõem que você instale o servidor de aplicativos em um servidor diferente dos servidores do ASCS/SCS e do HANA.</span><span class="sxs-lookup"><span data-stu-id="72985-466">The steps bellow assume that you install the application server on a server different from the ASCS/SCS and HANA servers.</span></span> <span data-ttu-id="72985-467">Caso contrário, algumas das etapas abaixo (como configurar a resolução de nome do host) não são necessárias.</span><span class="sxs-lookup"><span data-stu-id="72985-467">Otherwise some of the steps below (like configuring host name resolution) are not needed.</span></span>

1. <span data-ttu-id="72985-468">Configurar a resolução de nome do host</span><span class="sxs-lookup"><span data-stu-id="72985-468">Setup host name resolution</span></span>    
   <span data-ttu-id="72985-469">Você pode usar um servidor DNS ou modificar /etc/hosts em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="72985-469">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="72985-470">Este exemplo mostra como usar o arquivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="72985-470">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="72985-471">Substitua o endereço IP e o nome do host nos comandos a seguir</span><span class="sxs-lookup"><span data-stu-id="72985-471">Replace the IP address and the hostname in the following commands</span></span>
   ```bash
   sudo vi /etc/hosts
   ```
   <span data-ttu-id="72985-472">Insira as seguintes linhas para /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="72985-472">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="72985-473">Altere o endereço IP e o nome do host para corresponder ao seu ambiente</span><span class="sxs-lookup"><span data-stu-id="72985-473">Change the IP address and hostname to match your environment</span></span>    
    
   <pre><code>
   # IP address of the load balancer frontend configuration for NFS
   <b>10.0.0.4 nws-nfs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ASCS/SCS
   <b>10.0.0.10 nws-ascs</b>
   # IP address of the load balancer frontend configuration for SAP NetWeaver ERS
   <b>10.0.0.11 nws-ers</b>
   # IP address of the load balancer frontend configuration for database
   <b>10.0.0.12 nws-db</b>
   # IP address of the application server
   <b>10.0.0.8 nws-di-0</b>
   </code></pre>

1. <span data-ttu-id="72985-474">Criar o diretório sapmnt</span><span class="sxs-lookup"><span data-stu-id="72985-474">Create the sapmnt directory</span></span>

   <pre><code>
   sudo mkdir -p /sapmnt/<b>NWS</b>
   sudo mkdir -p /usr/sap/trans

   sudo chattr +i /sapmnt/<b>NWS</b>
   sudo chattr +i /usr/sap/trans
   </code></pre>

1. <span data-ttu-id="72985-475">Configurar o autofs</span><span class="sxs-lookup"><span data-stu-id="72985-475">Configure autofs</span></span>
 
   <pre><code>
   sudo vi /etc/auto.master

   # Add the following line to the file, save and exit
   +auto.master
   /- /etc/auto.direct
   </code></pre>

   <span data-ttu-id="72985-476">Criar um novo arquivo com</span><span class="sxs-lookup"><span data-stu-id="72985-476">Create a new file with</span></span>

   <pre><code>
   sudo vi /etc/auto.direct

   # Add the following lines to the file, save and exit
   /sapmnt/<b>NWS</b> -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/sapmntsid
   /usr/sap/trans -nfsvers=4,nosymlink,sync <b>nws-nfs</b>:/trans
   </code></pre>

   <span data-ttu-id="72985-477">Reiniciar o autofs para montar os novos compartilhamentos</span><span class="sxs-lookup"><span data-stu-id="72985-477">Restart autofs to mount the new shares</span></span>

   <pre><code>
   sudo systemctl enable autofs
   sudo service autofs restart
   </code></pre>

1. <span data-ttu-id="72985-478">Configurar arquivo de permuta</span><span class="sxs-lookup"><span data-stu-id="72985-478">Configure SWAP file</span></span>
 
   <pre><code>
   sudo vi /etc/waagent.conf

   # Set the property ResourceDisk.EnableSwap to y
   # Create and use swapfile on resource disk.
   ResourceDisk.EnableSwap=<b>y</b>

   # Set the size of the SWAP file with property ResourceDisk.SwapSizeMB
   # The free space of resource disk varies by virtual machine size. Make sure that you do not set a value that is too big. You can check the SWAP space with command swapon
   # Size of the swapfile.
   ResourceDisk.SwapSizeMB=<b>2000</b>
   </code></pre>

   <span data-ttu-id="72985-479">Reiniciar o agente para ativar a alteração</span><span class="sxs-lookup"><span data-stu-id="72985-479">Restart the Agent to activate the change</span></span>

   <pre><code>
   sudo service waagent restart
   </code></pre>

1. <span data-ttu-id="72985-480">Instalar o servidor de aplicativos do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="72985-480">Install SAP NetWeaver application server</span></span>

   <span data-ttu-id="72985-481">Instale um servidor de aplicativos do SAP NetWeaver primário ou adicional.</span><span class="sxs-lookup"><span data-stu-id="72985-481">Install a primary or additional SAP NetWeaver applications server.</span></span>

   <span data-ttu-id="72985-482">Você pode usar o parâmetro sapinst SAPINST_REMOTE_ACCESS_USER para permitir que um usuário não raiz se conecte ao sapinst.</span><span class="sxs-lookup"><span data-stu-id="72985-482">You can use the sapinst parameter SAPINST_REMOTE_ACCESS_USER to allow a non-root user to connect to sapinst.</span></span>

   <pre><code>
   sudo &lt;swpm&gt;/sapinst SAPINST_REMOTE_ACCESS_USER=<b>sapadmin</b>
   </code></pre>

1. <span data-ttu-id="72985-483">Atualizar o repositório seguro do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="72985-483">Update SAP HANA secure store</span></span>

   <span data-ttu-id="72985-484">Atualize o repositório seguro do SAP HANA para apontar para o nome virtual do programa de instalação da replicação de sistema do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="72985-484">Update the SAP HANA secure store to point to the virtual name of the SAP HANA System Replication setup.</span></span>
   <pre><code>
   su - <b>nws</b>adm
   hdbuserstore SET DEFAULT <b>nws-db</b>:3<b>03</b>15 <b>SAPABAP1</b> <b>&lt;password of ABAP schema&gt;</b>
   </code></pre>

## <a name="next-steps"></a><span data-ttu-id="72985-485">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72985-485">Next steps</span></span>
* <span data-ttu-id="72985-486">[Planejamento e implementação de Máquinas Virtuais do Azure para SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="72985-486">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="72985-487">[Implantação de Máquinas Virtuais do Azure para SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="72985-487">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="72985-488">[Implantação DBMS de Máquinas Virtuais do Azure para SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="72985-488">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="72985-489">Para saber como estabelecer a alta disponibilidade e o plano de recuperação de desastres do SAP HANA no Azure (instâncias grandes), confira [Alta disponibilidade e recuperação de desastres do SAP HANA (instâncias grandes) no Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="72985-489">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span>
* <span data-ttu-id="72985-490">Para saber como estabelecer a alta disponibilidade e o plano de recuperação de desastre do SAP HANA em VMs do Azure, confira [Alta disponibilidade do SAP HANA em VMs (Máquinas Virtuais) do Azure][sap-hana-ha]</span><span class="sxs-lookup"><span data-stu-id="72985-490">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure VMs, see [High Availability of SAP HANA on Azure Virtual Machines (VMs)][sap-hana-ha]</span></span>