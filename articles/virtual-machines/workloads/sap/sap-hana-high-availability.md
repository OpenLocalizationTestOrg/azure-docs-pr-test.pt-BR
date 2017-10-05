---
title: "Alta disponibilidade do SAP HANA em VMs (máquinas virtuais) do Azure | Microsoft Docs"
description: "Estabeleça alta disponibilidade do SAP HANA em VMs (máquinas virtuais) do Azure."
services: virtual-machines-linux
documentationcenter: 
author: MSSedusch
manager: timlt
editor: 
ms.service: virtual-machines-linux
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: vm-linux
ms.workload: infrastructure
ms.date: 04/25/2017
ms.author: sedusch
ms.openlocfilehash: 951150e621d21037b0adde7287b9f985290d8d11
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="7a0d4-103">Alta disponibilidade do SAP HANA em VMs (máquinas virtuais) do Azure</span><span class="sxs-lookup"><span data-stu-id="7a0d4-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

[dbms-guide]:dbms-guide.md
[deployment-guide]:deployment-guide.md
[planning-guide]:planning-guide.md

<span data-ttu-id="7a0d4-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span><span class="sxs-lookup"><span data-stu-id="7a0d4-104">[2205917]:https://launchpad.support.sap.com/#/notes/2205917</span></span>
<span data-ttu-id="7a0d4-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span><span class="sxs-lookup"><span data-stu-id="7a0d4-105">[1944799]:https://launchpad.support.sap.com/#/notes/1944799</span></span>
<span data-ttu-id="7a0d4-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span><span class="sxs-lookup"><span data-stu-id="7a0d4-106">[1928533]:https://launchpad.support.sap.com/#/notes/1928533</span></span>
<span data-ttu-id="7a0d4-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span><span class="sxs-lookup"><span data-stu-id="7a0d4-107">[2015553]:https://launchpad.support.sap.com/#/notes/2015553</span></span>
<span data-ttu-id="7a0d4-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span><span class="sxs-lookup"><span data-stu-id="7a0d4-108">[2178632]:https://launchpad.support.sap.com/#/notes/2178632</span></span>
<span data-ttu-id="7a0d4-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span><span class="sxs-lookup"><span data-stu-id="7a0d4-109">[2191498]:https://launchpad.support.sap.com/#/notes/2191498</span></span>
<span data-ttu-id="7a0d4-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span><span class="sxs-lookup"><span data-stu-id="7a0d4-110">[2243692]:https://launchpad.support.sap.com/#/notes/2243692</span></span>
<span data-ttu-id="7a0d4-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span><span class="sxs-lookup"><span data-stu-id="7a0d4-111">[1984787]:https://launchpad.support.sap.com/#/notes/1984787</span></span>
<span data-ttu-id="7a0d4-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span><span class="sxs-lookup"><span data-stu-id="7a0d4-112">[1999351]:https://launchpad.support.sap.com/#/notes/1999351</span></span>

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="7a0d4-113">No local, você pode usar a Replicação do Sistema HANA ou o armazenamento compartilhado para estabelecer alta disponibilidade para SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-113">On-premises, you can use either HANA System Replication or use shared storage to establish high availability for SAP HANA.</span></span>
<span data-ttu-id="7a0d4-114">Atualmente, damos suporte apenas à configuração da Replicação do Sistema HANA no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="7a0d4-115">A Replicação do Sistema HANA consiste em um nó mestre e, pelo menos, um nó subordinado.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="7a0d4-116">As alterações de dados no nó mestre são replicadas aos nós subordinados de modo síncrono e assíncrono.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-116">Changes to the data on the master node are replicated to the slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="7a0d4-117">Este artigo descreve como implantar as máquinas virtuais, configurar as máquinas virtuais, instalar a estrutura de cluster, bem como a instalar e configurar a Replicação do Sistema SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-117">This article describes how to deploy the virtual machines, configure the virtual machines, install the cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="7a0d4-118">Nos exemplos de configurações, comandos de instalação etc., são usados o número de instância 03 e o HDB da ID do Sistema HANA.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-118">In the example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="7a0d4-119">Primeiro, leia os seguintes documentos e Notas SAP</span><span class="sxs-lookup"><span data-stu-id="7a0d4-119">Read the following SAP Notes and papers first</span></span>

* <span data-ttu-id="7a0d4-120">A Nota SAP [1928533], que tem:</span><span class="sxs-lookup"><span data-stu-id="7a0d4-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="7a0d4-121">Lista de tamanhos de VM do Azure que têm suporte para a implantação de software SAP</span><span class="sxs-lookup"><span data-stu-id="7a0d4-121">List of Azure VM sizes that are supported for the deployment of SAP software</span></span>
  * <span data-ttu-id="7a0d4-122">Informações importantes sobre capacidade para tamanhos de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="7a0d4-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="7a0d4-123">Software SAP e combinações de SO (sistema operacional) e banco de dados com suporte</span><span class="sxs-lookup"><span data-stu-id="7a0d4-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="7a0d4-124">A versão do kernel do SAP necessária para Windows e para Linux no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="7a0d4-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="7a0d4-125">A Nota SAP [2015553] lista pré-requisitos para implantações de software SAP com suporte do SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="7a0d4-126">A Nota SAP [2205917] tem configurações de SO recomendadas para SUSE Linux Enterprise Server para aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="7a0d4-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="7a0d4-127">A Nota SAP [1944799] tem Diretrizes SAP HANA para SUSE Linux Enterprise Server para aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="7a0d4-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="7a0d4-128">A Nota SAP [2178632] contém informações detalhadas sobre todas as métricas de monitoramentos relatadas para o SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="7a0d4-129">A Nota SAP [2191498] tem a versão necessária do SAP Host Agent para Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-129">SAP Note [2191498] has the required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="7a0d4-130">A Nota SAP [2243692] tem informações sobre o licenciamento do SAP no Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="7a0d4-131">A Nota SAP [1984787] tem informações gerais sobre o SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="7a0d4-132">A Nota SAP [1999351] tem informações de solução de problemas adicionais para a Extensão de Monitoramento Avançado do Azure para SAP.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-132">SAP Note [1999351] has additional troubleshooting information for the Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="7a0d4-133">[WIKI da comunidade do SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) tem todas as Notas SAP necessárias para Linux.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="7a0d4-134">[Planejamento e implementação de Máquinas Virtuais do Azure para SAP no Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="7a0d4-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="7a0d4-135">[Implantação de máquinas virtuais do Azure para SAP no Linux (este artigo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="7a0d4-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="7a0d4-136">[Implantação de Máquinas Virtuais do Azure do DBMS para SAP no Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="7a0d4-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="7a0d4-137">[Cenário otimizado de desempenho de SAP HANA SR][suse-hana-ha-guide] O guia contém todas as informações necessárias para definir a configuração local da Replicação do Sistema SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] The guide contains all required information to set up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="7a0d4-138">Use este guia como uma linha de base.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="7a0d4-139">Implantação do Linux</span><span class="sxs-lookup"><span data-stu-id="7a0d4-139">Deploying Linux</span></span>

<span data-ttu-id="7a0d4-140">O agente de recursos para HANA SAP está incluído no SUSE Linux Enterprise Server for SAP Applications.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-140">The resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="7a0d4-141">O Azure Marketplace contém uma imagem para SUSE Linux Enterprise Server for SAP Applications 12 com BYOS (Traga sua própria assinatura) que você pode usar para implantar novas máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-141">The Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use to deploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="7a0d4-142">Implantação manual</span><span class="sxs-lookup"><span data-stu-id="7a0d4-142">Manual Deployment</span></span>

1. <span data-ttu-id="7a0d4-143">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="7a0d4-143">Create a Resource Group</span></span>
1. <span data-ttu-id="7a0d4-144">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="7a0d4-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="7a0d4-145">Crie duas Contas de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="7a0d4-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="7a0d4-146">Crie um Conjunto de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="7a0d4-146">Create an Availability Set</span></span>  
   <span data-ttu-id="7a0d4-147">Defina o máximo de domínio de atualização</span><span class="sxs-lookup"><span data-stu-id="7a0d4-147">Set max update domain</span></span>
1. <span data-ttu-id="7a0d4-148">Crie um Balanceador de Carga (interno)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="7a0d4-149">Selecione a VNET da etapa acima</span><span class="sxs-lookup"><span data-stu-id="7a0d4-149">Select VNET of step above</span></span>
1. <span data-ttu-id="7a0d4-150">Crie a Máquina Virtual 1</span><span class="sxs-lookup"><span data-stu-id="7a0d4-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="7a0d4-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="7a0d4-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="7a0d4-152">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="7a0d4-153">Escolha a Conta de Armazenamento 1</span><span class="sxs-lookup"><span data-stu-id="7a0d4-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="7a0d4-154">Escolha o Conjunto de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="7a0d4-154">Select Availability Set</span></span>  
1. <span data-ttu-id="7a0d4-155">Crie a Máquina Virtual 2</span><span class="sxs-lookup"><span data-stu-id="7a0d4-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="7a0d4-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="7a0d4-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="7a0d4-157">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="7a0d4-158">Escolha a Conta de Armazenamento 2</span><span class="sxs-lookup"><span data-stu-id="7a0d4-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="7a0d4-159">Escolha o Conjunto de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="7a0d4-159">Select Availability Set</span></span>  
1. <span data-ttu-id="7a0d4-160">Adicione Discos de Dados</span><span class="sxs-lookup"><span data-stu-id="7a0d4-160">Add Data Disks</span></span>
1. <span data-ttu-id="7a0d4-161">Configure o balanceador de carga</span><span class="sxs-lookup"><span data-stu-id="7a0d4-161">Configure the load balancer</span></span>
    1. <span data-ttu-id="7a0d4-162">Crie um pool de IPs de front-end</span><span class="sxs-lookup"><span data-stu-id="7a0d4-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="7a0d4-163">Abra o balanceador de carga, escolha o pool de IPs de front-end e clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="7a0d4-163">Open the load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="7a0d4-164">Digite o nome do novo pool de IPs de front-end (por exemplo hana-front-end)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-164">Enter the name of the new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="7a0d4-165">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="7a0d4-165">Click OK</span></span>
        1. <span data-ttu-id="7a0d4-166">Depois que o novo pool de IPs de front-end for criado, anote seu endereço IP</span><span class="sxs-lookup"><span data-stu-id="7a0d4-166">After the new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="7a0d4-167">Crie um pool de back-end</span><span class="sxs-lookup"><span data-stu-id="7a0d4-167">Create a backend pool</span></span>
        1. <span data-ttu-id="7a0d4-168">Abra o balanceador de carga, escolha os pools de back-end e clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="7a0d4-168">Open the load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="7a0d4-169">Digite o nome do novo pool de back-end (por exemplo hana-back-end)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-169">Enter the name of the new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="7a0d4-170">Clique em Adicionar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7a0d4-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="7a0d4-171">Selecione o Conjunto de Disponibilidade criado anteriormente</span><span class="sxs-lookup"><span data-stu-id="7a0d4-171">Select the Availability Set you created earlier</span></span>
        1. <span data-ttu-id="7a0d4-172">Selecione as máquinas virtuais do cluster SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7a0d4-172">Select the virtual machines of the SAP HANA cluster</span></span>
        1. <span data-ttu-id="7a0d4-173">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="7a0d4-173">Click OK</span></span>
    1. <span data-ttu-id="7a0d4-174">Criar uma investigação de integridade</span><span class="sxs-lookup"><span data-stu-id="7a0d4-174">Create a health probe</span></span>
       1. <span data-ttu-id="7a0d4-175">Abra o balanceador de carga, selecione as investigações de integridade e clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="7a0d4-175">Open the load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="7a0d4-176">Digite o nome da nova investigação de integridade (por exemplo, hana-hp)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-176">Enter the name of the new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="7a0d4-177">Escolha TCP como protocolo, porta 625**03**, mantenha o Intervalo como 5 e o Limite de não integridade como 2</span><span class="sxs-lookup"><span data-stu-id="7a0d4-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="7a0d4-178">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="7a0d4-178">Click OK</span></span>
    1. <span data-ttu-id="7a0d4-179">Criar regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="7a0d4-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="7a0d4-180">Clique no balanceador de carga, escolha as regras de balanceamento de carga e clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="7a0d4-180">Open the load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="7a0d4-181">Insira o nome da nova regra de balanceador de carga (por exemplo hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-181">Enter the name of the new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="7a0d4-182">Escolha o endereço IP de front-end, o pool de back-end e a investigação de integridade criados anteriormente (por exemplo hana-front-end)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-182">Select the frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="7a0d4-183">Mantenha o protocolo TCP, insira a porta 3**03**15</span><span class="sxs-lookup"><span data-stu-id="7a0d4-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="7a0d4-184">Aumente o tempo limite de ociosidade para 30 minutos</span><span class="sxs-lookup"><span data-stu-id="7a0d4-184">Increase idle timeout to 30 minutes</span></span>
       1. <span data-ttu-id="7a0d4-185">**Habilite o IP Flutuante**</span><span class="sxs-lookup"><span data-stu-id="7a0d4-185">**Make sure to enable Floating IP**</span></span>
        1. <span data-ttu-id="7a0d4-186">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="7a0d4-186">Click OK</span></span>
        1. <span data-ttu-id="7a0d4-187">Repita as etapas acima para a porta 3**03**17</span><span class="sxs-lookup"><span data-stu-id="7a0d4-187">Repeat the steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="7a0d4-188">Implantar com modelo</span><span class="sxs-lookup"><span data-stu-id="7a0d4-188">Deploy with template</span></span>
<span data-ttu-id="7a0d4-189">Você pode usar um dos modelos de início rápido no github para implantar todos os recursos necessários.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-189">You can use one of the quick start templates on github to deploy all required resources.</span></span> <span data-ttu-id="7a0d4-190">O modelo implanta as máquinas virtuais, o balanceador de carga, o conjunto de disponibilidade etc. Siga estas etapas para implantar o modelo:</span><span class="sxs-lookup"><span data-stu-id="7a0d4-190">The template deploys the virtual machines, the load balancer, availability set etc. Follow these steps to deploy the template:</span></span>

1. <span data-ttu-id="7a0d4-191">Abra o [modelo de banco de dados][template-multisid-db] ou o [modelo convergido][template-converged] no portal do Azure. O modelo de banco de dados cria apenas as regras de balanceamento de carga para um banco de dados, enquanto o modelo convergido também cria as regras de balanceamento de carga para uma instância ASCS/SCS e ERS (apenas Linux).</span><span class="sxs-lookup"><span data-stu-id="7a0d4-191">Open the [database template][template-multisid-db] or the [converged template][template-converged] on the Azure Portal The database template only creates the load-balancing rules for a database whereas the converged template also creates the load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="7a0d4-192">Se você planeja instalar um sistema baseado no SAP NetWeaver e também quer instalar a instância ASCS/SCS nas mesmas máquinas, use o [modelo convergido][template-converged].</span><span class="sxs-lookup"><span data-stu-id="7a0d4-192">If you plan to install an SAP NetWeaver based system and you also want to install the ASCS/SCS instance on the same machines, use the [converged template][template-converged].</span></span>
1. <span data-ttu-id="7a0d4-193">Defina os seguintes parâmetros</span><span class="sxs-lookup"><span data-stu-id="7a0d4-193">Enter the following parameters</span></span>
    1. <span data-ttu-id="7a0d4-194">ID do sistema SAP</span><span class="sxs-lookup"><span data-stu-id="7a0d4-194">Sap System Id</span></span>  
       <span data-ttu-id="7a0d4-195">Insira a ID do sistema SAP do sistema SAP, que você deseja instalar.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-195">Enter the SAP system Id of the SAP system you want to install.</span></span> <span data-ttu-id="7a0d4-196">A Id será usada como um prefixo para os recursos que serão implantados.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-196">The Id will be used as a prefix for the resources that are deployed.</span></span>
    1. <span data-ttu-id="7a0d4-197">Tipo de pilha (aplicável somente se você usar o modelo convergido)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-197">Stack Type (only applicable if you use the converged template)</span></span>  
       <span data-ttu-id="7a0d4-198">Selecionar o tipo de pilha do SAP NetWeaver</span><span class="sxs-lookup"><span data-stu-id="7a0d4-198">Select the SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="7a0d4-199">Tipo de sistema operacional</span><span class="sxs-lookup"><span data-stu-id="7a0d4-199">Os Type</span></span>  
       <span data-ttu-id="7a0d4-200">Selecione uma das distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-200">Select one of the Linux distributions.</span></span> <span data-ttu-id="7a0d4-201">Para este exemplo, selecione SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="7a0d4-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="7a0d4-202">Tipo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="7a0d4-202">Db Type</span></span>  
       <span data-ttu-id="7a0d4-203">Selecionar HANA</span><span class="sxs-lookup"><span data-stu-id="7a0d4-203">Select HANA</span></span>
    1. <span data-ttu-id="7a0d4-204">Tamanho do sistema SAP</span><span class="sxs-lookup"><span data-stu-id="7a0d4-204">Sap System Size</span></span>  
       <span data-ttu-id="7a0d4-205">A quantidade de SAPs que o novo sistema fornecerá.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-205">The amount of SAPS the new system will provide.</span></span> <span data-ttu-id="7a0d4-206">Se você não tiver certeza de quantos SAPs o sistema precisará, pergunte ao seu Parceiro de tecnologia SAP ou Integrador de sistemas</span><span class="sxs-lookup"><span data-stu-id="7a0d4-206">If you are not sure how many SAPS the system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="7a0d4-207">Disponibilidade do sistema</span><span class="sxs-lookup"><span data-stu-id="7a0d4-207">System Availability</span></span>  
       <span data-ttu-id="7a0d4-208">Selecione HA</span><span class="sxs-lookup"><span data-stu-id="7a0d4-208">Select HA</span></span>
    1. <span data-ttu-id="7a0d4-209">Nome de Usuário de Administrador e Senha do Administrador</span><span class="sxs-lookup"><span data-stu-id="7a0d4-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="7a0d4-210">É criado um novo usuário que pode ser usado para fazer logon no computador.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-210">A new user is created that can be used to log on to the machine.</span></span>
    1. <span data-ttu-id="7a0d4-211">Sub-rede Nova ou Existente</span><span class="sxs-lookup"><span data-stu-id="7a0d4-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="7a0d4-212">Determina se uma nova rede virtual e sub-rede devem ser criadas ou se uma sub-rede existente deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="7a0d4-213">Se você já tiver uma rede virtual conectada à sua rede local, selecione a rede existente.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-213">If you already have a virtual network that is connected to your on-premises network, select existing.</span></span>
    1. <span data-ttu-id="7a0d4-214">ID da Sub-rede</span><span class="sxs-lookup"><span data-stu-id="7a0d4-214">Subnet Id</span></span>  
    <span data-ttu-id="7a0d4-215">A ID da sub-rede à qual as máquinas virtuais devem estar conectadas.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-215">The ID of the subnet to which the virtual machines should be connected to.</span></span> <span data-ttu-id="7a0d4-216">Selecione a sub-rede da sua VPN ou a rede virtual da ExpressRoute para conectar a máquina virtual à sua rede local.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-216">Select the subnet of your VPN or Express Route virtual network to connect the virtual machine to your on-premises network.</span></span> <span data-ttu-id="7a0d4-217">A ID geralmente é semelhante a /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="7a0d4-217">The ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="7a0d4-218">Configuração de HA do Linux</span><span class="sxs-lookup"><span data-stu-id="7a0d4-218">Setting up Linux HA</span></span>

<span data-ttu-id="7a0d4-219">Os itens a seguir são prefixados com [A] – aplicável a todos os nós, [1] – aplicável somente ao nó 1 ou [2] – aplicável somente ao nó 2.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-219">The following items are prefixed with either [A] - applicable to all nodes, [1] - only applicable to node 1 or [2] - only applicable to node 2.</span></span>

1. <span data-ttu-id="7a0d4-220">[A] Apenas SLES for SAP BYOS – registre o SLES para poder usar os repositórios</span><span class="sxs-lookup"><span data-stu-id="7a0d4-220">[A] SLES for SAP BYOS only - Register SLES to be able to use the repositories</span></span>
1. <span data-ttu-id="7a0d4-221">[A] Apenas SLES for SAP BYOS – adicione o módulo de nuvem pública</span><span class="sxs-lookup"><span data-stu-id="7a0d4-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="7a0d4-222">[A] Atualize o SLES</span><span class="sxs-lookup"><span data-stu-id="7a0d4-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="7a0d4-223">[1] Habilite o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="7a0d4-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="7a0d4-224">[2] Habilite o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="7a0d4-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert the public key you copied in the last step into the authorized keys file on the second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which to save the key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy the public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="7a0d4-225">[1] Habilite o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="7a0d4-225">[1] Enable ssh access</span></span>
    ```bash
    # insert the public key you copied in the last step into the authorized keys file on the first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="7a0d4-226">[A] Instale a extensão HA</span><span class="sxs-lookup"><span data-stu-id="7a0d4-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="7a0d4-227">[A] Configure o layout do disco</span><span class="sxs-lookup"><span data-stu-id="7a0d4-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="7a0d4-228">LVM</span><span class="sxs-lookup"><span data-stu-id="7a0d4-228">LVM</span></span>  
    <span data-ttu-id="7a0d4-229">Normalmente, é recomendável usar LVM para volumes que armazenam arquivos de log e dados.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-229">We generally recommend to use LVM for volumes that store data and log files.</span></span> <span data-ttu-id="7a0d4-230">O exemplo abaixo pressupõe que as máquinas virtuais tenham quatro discos de dados anexados que devem ser usados para criar dois volumes.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-230">The example below assumes that the virtual machines have four data disks attached that should be used to create two volumes.</span></span>
        * <span data-ttu-id="7a0d4-231">Crie volumes físicos para todos os discos que queira usar.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-231">Create physical volumes for all disks that you want to use.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="7a0d4-232">Crie um grupo de volume para os arquivos de dados, um grupo de volume para os arquivos de log e um para o diretório compartilhado do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7a0d4-232">Create a volume group for the data files, one volume group for the log files and one for the shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="7a0d4-233">Criar os volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="7a0d4-233">Create the logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="7a0d4-234">Crie os diretórios de montagem e copie a UUID de todos os volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="7a0d4-234">Create the mount directories and copy the UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down the id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="7a0d4-235">Crie entradas fstab para os três volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="7a0d4-235">Create fstab entries for the three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="7a0d4-236">Insira esta linha para /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="7a0d4-236">Insert this line to /etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="7a0d4-237">Monte os novos volumes</span><span class="sxs-lookup"><span data-stu-id="7a0d4-237">Mount the new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="7a0d4-238">Discos simples</span><span class="sxs-lookup"><span data-stu-id="7a0d4-238">Plain Disks</span></span>  
       <span data-ttu-id="7a0d4-239">Para sistemas pequenos ou de demonstração, você pode colocar os arquivos de log e dados do HANA em um disco.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="7a0d4-240">Os comandos a seguir criam uma partição em /dev/sdc e a formatam com xfs.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-240">The following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-the-id-of-devsdc1"></a><span data-ttu-id="7a0d4-241">escreva a id de /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="7a0d4-241">write down the id of /dev/sdc1</span></span>
    <span data-ttu-id="7a0d4-242">sudo /sbin/blkid  sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="7a0d4-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line to /etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create the target directory and mount the disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="7a0d4-243">[A] Configure a resolução de nome do host para todos os hosts</span><span class="sxs-lookup"><span data-stu-id="7a0d4-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="7a0d4-244">Você pode usar um servidor DNS ou modificar /etc/hosts em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-244">You can either use a DNS server or modify the /etc/hosts on all nodes.</span></span> <span data-ttu-id="7a0d4-245">Este exemplo mostra como usar o arquivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-245">This example shows how to use the /etc/hosts file.</span></span>
   <span data-ttu-id="7a0d4-246">Substitua o endereço IP e o nome do host nos comandos a seguir</span><span class="sxs-lookup"><span data-stu-id="7a0d4-246">Replace the IP address and the hostname in the following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="7a0d4-247">Insira as seguintes linhas para /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-247">Insert the following lines to /etc/hosts.</span></span> <span data-ttu-id="7a0d4-248">Altere o endereço IP e o nome do host para corresponder ao seu ambiente</span><span class="sxs-lookup"><span data-stu-id="7a0d4-248">Change the IP address and hostname to match your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="7a0d4-249">[1] Instale o Cluster</span><span class="sxs-lookup"><span data-stu-id="7a0d4-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want to continue anyway? [y/N] -> y
    # Network address to bind to (e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish to use SBD? [y/N] -> N
    # Do you wish to configure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="7a0d4-250">[2] Adicione nó ao cluster</span><span class="sxs-lookup"><span data-stu-id="7a0d4-250">[2] Add node to cluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured to start at system boot.
    # WARNING: No watchdog device found. If SBD is used, the cluster will be unable to start without a watchdog.
    # Do you want to continue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="7a0d4-251">[A] Altere a senha hacluster para a mesma senha</span><span class="sxs-lookup"><span data-stu-id="7a0d4-251">[A] Change hacluster password to the same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="7a0d4-252">[A] Configure corosync para usar outro transporte e adicione nodelist.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-252">[A] Configure corosync to use other transport and add nodelist.</span></span> <span data-ttu-id="7a0d4-253">Caso contrário, o cluster não funcionará.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="7a0d4-254">Adicione o conteúdo em negrito a seguir ao arquivo.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-254">Add the following bold content to the file.</span></span>
    
    <pre><code> 
    [...]
      interface { 
          [...] 
      }
      <b>transport:      udpu</b>
    } 
    <b>nodelist {
      node {
        ring0_addr:     < ip address of node 1 >
      }
      node {
        ring0_addr:     < ip address of node 2 > 
      } 
    }</b>
    logging {
      [...]
    </code></pre>

    <span data-ttu-id="7a0d4-255">Em seguida, reinicie o serviço corosync</span><span class="sxs-lookup"><span data-stu-id="7a0d4-255">Then restart the corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="7a0d4-256">[A] Instale os pacotes HANA HA</span><span class="sxs-lookup"><span data-stu-id="7a0d4-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="7a0d4-257">Instalando o SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7a0d4-257">Installing SAP HANA</span></span>

<span data-ttu-id="7a0d4-258">Siga o capítulo 4 do [guia Cenário Otimizado para Desempenho da SR SAP HANA][suse-hana-ha-guide] para instalar a Replicação do Sistema SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-258">Follow chapter 4 of the [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] to install SAP HANA System Replication.</span></span>

1. <span data-ttu-id="7a0d4-259">[A] Execute hdblcm no DVD do HANA</span><span class="sxs-lookup"><span data-stu-id="7a0d4-259">[A] Run hdblcm from the HANA DVD</span></span>
    * <span data-ttu-id="7a0d4-260">Escolha instalação -> 1</span><span class="sxs-lookup"><span data-stu-id="7a0d4-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="7a0d4-261">Selecione os componentes adicionais para instalação -> 1</span><span class="sxs-lookup"><span data-stu-id="7a0d4-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="7a0d4-262">Insira o caminho de instalação [/hana/shared]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-263">Insira o Nome do Host Local [..]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-264">Você deseja adicionar outros hosts ao sistema?</span><span class="sxs-lookup"><span data-stu-id="7a0d4-264">Do you want to add additional hosts to the system?</span></span> <span data-ttu-id="7a0d4-265">(s/n) [n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-266">Insira a ID do Sistema SAP HANA: <SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="7a0d4-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="7a0d4-267">Insira o Número da Instância [00]:</span><span class="sxs-lookup"><span data-stu-id="7a0d4-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="7a0d4-268">Número da instância do HANA.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-268">HANA Instance number.</span></span> <span data-ttu-id="7a0d4-269">Use 03 se você tiver usado o Modelo do Azure ou se tiver seguido o exemplo acima</span><span class="sxs-lookup"><span data-stu-id="7a0d4-269">Use 03 if you used the Azure Template or followed the example above</span></span>
    * <span data-ttu-id="7a0d4-270">Selecione Modo de Banco de Dados/Inserir Índice [1]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-271">Selecione o Uso do Sistema/Inserir Índice [4]:</span><span class="sxs-lookup"><span data-stu-id="7a0d4-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="7a0d4-272">Selecione o Uso do sistema</span><span class="sxs-lookup"><span data-stu-id="7a0d4-272">Select the system Usage</span></span>
    * <span data-ttu-id="7a0d4-273">Informe o Local dos Volumes de Dados [/data/hana/HDB]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-274">Informe o Local dos Volumes de Log [/hana/log/HDB]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-275">Restringir a alocação máxima de memória?</span><span class="sxs-lookup"><span data-stu-id="7a0d4-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="7a0d4-276">[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-277">Insira o Nome do Host do Certificado para o Host '...'</span><span class="sxs-lookup"><span data-stu-id="7a0d4-277">Enter Certificate Host Name For Host '...'</span></span> <span data-ttu-id="7a0d4-278">[...]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-278">[...]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-279">Insira a Senha de Usuário do Agente do Host SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="7a0d4-279">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="7a0d4-280">Confirme a Senha de Usuário do Agente do Host SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="7a0d4-280">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="7a0d4-281">Insira a Senha do Administrador de Sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="7a0d4-281">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="7a0d4-282">Confirme a Senha do Administrador de Sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="7a0d4-282">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="7a0d4-283">Insira o Diretório Base do Administrador de Sistema [/usr/sap/HDB/home]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-283">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-284">Insira o Shell de Logon do Administrador de Sistema [/bin/sh]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-284">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-285">Insira a ID de Usuário do Administrador de Sistema [1001]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-285">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-286">Insira a ID do Grupo de Usuários (sapsys) [79]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-286">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-287">Insira a Senha de Usuário do Banco de Dados (SYSTEM):</span><span class="sxs-lookup"><span data-stu-id="7a0d4-287">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="7a0d4-288">Confirme a Senha de Usuário do Banco de Dados (SYSTEM):</span><span class="sxs-lookup"><span data-stu-id="7a0d4-288">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="7a0d4-289">Reiniciar o sistema após a reinicialização do computador?</span><span class="sxs-lookup"><span data-stu-id="7a0d4-289">Restart system after machine reboot?</span></span> <span data-ttu-id="7a0d4-290">[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="7a0d4-290">[n]: -> ENTER</span></span>
    * <span data-ttu-id="7a0d4-291">Deseja continuar?</span><span class="sxs-lookup"><span data-stu-id="7a0d4-291">Do you want to continue?</span></span> <span data-ttu-id="7a0d4-292">(s/n):</span><span class="sxs-lookup"><span data-stu-id="7a0d4-292">(y/n):</span></span>  
  <span data-ttu-id="7a0d4-293">Valide o resumo e digite s para continuar</span><span class="sxs-lookup"><span data-stu-id="7a0d4-293">Validate the summary and enter y to continue</span></span>
1. <span data-ttu-id="7a0d4-294">[A] Atualize o Agente do Host do SAP</span><span class="sxs-lookup"><span data-stu-id="7a0d4-294">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="7a0d4-295">Baixe o arquivo mais recente do Agente do Host do SAP em [SAP Softwarecenter][sap-swcenter] e execute o comando a seguir para fazer upgrade do agente.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-295">Download the latest SAP Host Agent archive from the [SAP Softwarecenter][sap-swcenter] and run the following command to upgrade the agent.</span></span> <span data-ttu-id="7a0d4-296">Substitua o caminho do arquivo de modo a apontar para o arquivo que você baixou.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-296">Replace the path to the archive to point to the file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path to SAP Host Agent SAR>
    ```

1. <span data-ttu-id="7a0d4-297">[1] Crie uma replicação HANA (como raiz)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-297">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="7a0d4-298">Execute o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-298">Run the following command.</span></span> <span data-ttu-id="7a0d4-299">Não se esqueça de substituir cadeias de caracteres em negrito (HDB da ID do Sistema HANA e o número de instância 03) pelos valores da sua instalação SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-299">Make sure to replace bold strings (HANA System ID HDB and instance number 03) with the values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN TO <b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="7a0d4-300">[A] Criar entrada de repositório de chaves (como raiz)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-300">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="7a0d4-301">[1] Faça o backup do banco de dados backup (como raiz)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-301">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="7a0d4-302">[1] Alterne para o usuário sapsid (por exemplo, hdbadm) e crie o site primário.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-302">[1] Switch to the sapsid user (for example hdbadm) and create the primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="7a0d4-303">[2] Alterne para o usuário sapsid (por exemplo, hdbadm) e crie o site secundário.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-303">[2] Switch to the sapsid user (for example hdbadm) and create the secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="7a0d4-304">Configurar a estrutura do cluster</span><span class="sxs-lookup"><span data-stu-id="7a0d4-304">Configure Cluster Framework</span></span>

<span data-ttu-id="7a0d4-305">Altere as configurações padrão</span><span class="sxs-lookup"><span data-stu-id="7a0d4-305">Change the default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter the following to crm-defaults.txt
<code>
property $id="cib-bootstrap-options" \
  no-quorum-policy="ignore" \
  stonith-enabled="true" \
  stonith-action="reboot" \
  stonith-timeout="150s"
rsc_defaults $id="rsc-options" \
  resource-stickiness="1000" \
  migration-threshold="5000"
op_defaults $id="op-options" \
  timeout="600"
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="7a0d4-306">now we load the file to the cluster</span><span class="sxs-lookup"><span data-stu-id="7a0d4-306">now we load the file to the cluster</span></span>
<span data-ttu-id="7a0d4-307">sudo crm configure load update crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="7a0d4-307">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="7a0d4-308">Criar dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="7a0d4-308">Create STONITH device</span></span>

<span data-ttu-id="7a0d4-309">O dispositivo STONITH usa uma Entidade de Serviço para autorização no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-309">The STONITH device uses a Service Principal to authorize against Microsoft Azure.</span></span> <span data-ttu-id="7a0d4-310">Siga estas etapas para criar uma Entidade de Serviço.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-310">Please follow these steps to create a Service Principal.</span></span>

1. <span data-ttu-id="7a0d4-311">Acesse <https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="7a0d4-311">Go to <https://portal.azure.com></span></span>
1. <span data-ttu-id="7a0d4-312">Abra a folha Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="7a0d4-312">Open the Azure Active Directory blade</span></span>  
   <span data-ttu-id="7a0d4-313">Vá para Propriedades e anote a ID do Diretório.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-313">Go to Properties and write down the Directory Id.</span></span> <span data-ttu-id="7a0d4-314">Essa é a **id de locatário**.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-314">This is the **tenant id**.</span></span>
1. <span data-ttu-id="7a0d4-315">Clique em Registros do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="7a0d4-315">Click App registrations</span></span>
1. <span data-ttu-id="7a0d4-316">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="7a0d4-316">Click Add</span></span>
1. <span data-ttu-id="7a0d4-317">Digite um Nome, selecione Tipo de Aplicativo "Aplicativo Web/API", insira uma URL de logon (por exemplo, http://localhost) e clique em Criar</span><span class="sxs-lookup"><span data-stu-id="7a0d4-317">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="7a0d4-318">A URL de logon não é usada e pode ser qualquer URL válida</span><span class="sxs-lookup"><span data-stu-id="7a0d4-318">The sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="7a0d4-319">Selecione o novo Aplicativo e clique em Chaves na guia Configurações</span><span class="sxs-lookup"><span data-stu-id="7a0d4-319">Select the new App and click Keys in the Settings tab</span></span>
1. <span data-ttu-id="7a0d4-320">Insira uma descrição para uma nova chave, selecione "Nunca expira" e clique em Salvar</span><span class="sxs-lookup"><span data-stu-id="7a0d4-320">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="7a0d4-321">Anote o Valor.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-321">Write down the Value.</span></span> <span data-ttu-id="7a0d4-322">Ele é usado como **senha** da Entidade de Serviço</span><span class="sxs-lookup"><span data-stu-id="7a0d4-322">It is used as the **password** for the Service Principal</span></span>
1. <span data-ttu-id="7a0d4-323">Anote a ID do Aplicativo.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-323">Write down the Application Id.</span></span> <span data-ttu-id="7a0d4-324">Ela é usada como nome de usuário (**id de logon** nas etapas abaixo) da Entidade de Serviço</span><span class="sxs-lookup"><span data-stu-id="7a0d4-324">It is used as the username (**login id** in the steps below) of the Service Principal</span></span>

<span data-ttu-id="7a0d4-325">A Entidade de Serviço não tem permissões para acessar os recursos do Azure por padrão.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-325">The Service Principal does not have permissions to access your Azure resources by default.</span></span> <span data-ttu-id="7a0d4-326">Você precisa fornecer as permissões da Entidade de Serviço para iniciar e parar (desalocar) todas as máquinas virtuais do cluster.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-326">You need to give the Service Principal permissions to start and stop (deallocate) all virtual machines of the cluster.</span></span>

1. <span data-ttu-id="7a0d4-327">Acesse https://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="7a0d4-327">Go to https://portal.azure.com</span></span>
1. <span data-ttu-id="7a0d4-328">Abra a folha Todos os recursos</span><span class="sxs-lookup"><span data-stu-id="7a0d4-328">Open the All resources blade</span></span>
1. <span data-ttu-id="7a0d4-329">Selecione a máquina virtual</span><span class="sxs-lookup"><span data-stu-id="7a0d4-329">Select the virtual machine</span></span>
1. <span data-ttu-id="7a0d4-330">Clique em Controle de acesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="7a0d4-330">Click Access control (IAM)</span></span>
1. <span data-ttu-id="7a0d4-331">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="7a0d4-331">Click Add</span></span>
1. <span data-ttu-id="7a0d4-332">Selecione a função Proprietário</span><span class="sxs-lookup"><span data-stu-id="7a0d4-332">Select the role Owner</span></span>
1. <span data-ttu-id="7a0d4-333">Digite o nome do aplicativo criado acima</span><span class="sxs-lookup"><span data-stu-id="7a0d4-333">Enter the name of the application you created above</span></span>
1. <span data-ttu-id="7a0d4-334">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="7a0d4-334">Click OK</span></span>

<span data-ttu-id="7a0d4-335">Depois de editar as permissões das máquinas virtuais, você pode configurar os dispositivos STONITH no cluster.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-335">After you edited the permissions for the virtual machines, you can configure the STONITH devices in the cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter the following to crm-fencing.txt
# replace the bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="7a0d4-336">now we load the file to the cluster</span><span class="sxs-lookup"><span data-stu-id="7a0d4-336">now we load the file to the cluster</span></span>
<span data-ttu-id="7a0d4-337">sudo crm configure load update crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="7a0d4-337">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="7a0d4-338">Criar recursos do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="7a0d4-338">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number and HANA system id
<code>
primitive rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHanaTopology \
    operations $id="rsc_sap2_<b>HDB</b>_HDB<b>03</b>-operations" \
    op monitor interval="10" timeout="600" \
    op start interval="0" timeout="600" \
    op stop interval="0" timeout="300" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>"

clone cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> rsc_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" clone-node-max="1" target-role="Started" interleave="true"
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="7a0d4-339">now we load the file to the cluster</span><span class="sxs-lookup"><span data-stu-id="7a0d4-339">now we load the file to the cluster</span></span>
<span data-ttu-id="7a0d4-340">sudo crm configure load update crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="7a0d4-340">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter the following to crm-saphana.txt
# replace the bold string with your instance number, HANA system id and the frontend IP address of the Azure load balancer. 
<code>
primitive rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> ocf:suse:SAPHana \
    operations $id="rsc_sap_<b>HDB</b>_HDB<b>03</b>-operations" \
    op start interval="0" timeout="3600" \
    op stop interval="0" timeout="3600" \
    op promote interval="0" timeout="3600" \
    op monitor interval="60" role="Master" timeout="700" \
    op monitor interval="61" role="Slave" timeout="700" \
    params SID="<b>HDB</b>" InstanceNumber="<b>03</b>" PREFER_SITE_TAKEOVER="true" \
    DUPLICATE_PRIMARY_TIMEOUT="7200" AUTOMATED_REGISTER="false"

ms msl_SAPHana_<b>HDB</b>_HDB<b>03</b> rsc_SAPHana_<b>HDB</b>_HDB<b>03</b> \
    meta is-managed="true" notify="true" clone-max="2" clone-node-max="1" \
    target-role="Started" interleave="true"

primitive rsc_ip_<b>HDB</b>_HDB<b>03</b> ocf:heartbeat:IPaddr2 \ 
    meta target-role="Started" is-managed="true" \ 
    operations $id="rsc_ip_<b>HDB</b>_HDB<b>03</b>-operations" \ 
    op monitor interval="10s" timeout="20s" \ 
    params ip="<b>10.0.0.21</b>" 
primitive rsc_nc_<b>HDB</b>_HDB<b>03</b> anything \ 
    params binfile="/usr/bin/nc" cmdline_options="-l -k 625<b>03</b>" \ 
    op monitor timeout=20s interval=10 depth=0 
group g_ip_<b>HDB</b>_HDB<b>03</b> rsc_ip_<b>HDB</b>_HDB<b>03</b> rsc_nc_<b>HDB</b>_HDB<b>03</b>
 
colocation col_saphana_ip_<b>HDB</b>_HDB<b>03</b> 2000: g_ip_<b>HDB</b>_HDB<b>03</b>:Started \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>:Master  
order ord_SAPHana_<b>HDB</b>_HDB<b>03</b> 2000: cln_SAPHanaTopology_<b>HDB</b>_HDB<b>03</b> \ 
    msl_SAPHana_<b>HDB</b>_HDB<b>03</b>
</code>

# <a name="now-we-load-the-file-to-the-cluster"></a><span data-ttu-id="7a0d4-341">now we load the file to the cluster</span><span class="sxs-lookup"><span data-stu-id="7a0d4-341">now we load the file to the cluster</span></span>
<span data-ttu-id="7a0d4-342">sudo crm configure load update crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="7a0d4-342">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="7a0d4-343">Testar configuração do cluster</span><span class="sxs-lookup"><span data-stu-id="7a0d4-343">Test cluster setup</span></span>
<span data-ttu-id="7a0d4-344">O capítulo a seguir descreve como você pode testar sua configuração.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-344">The following chapter describe how you can test your setup.</span></span> <span data-ttu-id="7a0d4-345">Cada teste supõe que você é a raiz e o mestre do SAP HANA está em execução na máquina virtual saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-345">Every test assumes that you are root and the SAP HANA master is running on the virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="7a0d4-346">Teste de isolamento</span><span class="sxs-lookup"><span data-stu-id="7a0d4-346">Fencing Test</span></span>

<span data-ttu-id="7a0d4-347">Você pode testar a configuração do agente de isolamento desabilitando a interface de rede no nó saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-347">You can test the setup of the fencing agent by disabling the network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="7a0d4-348">A máquina virtual agora deve ser reiniciada ou interrompida, dependendo a configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-348">The virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="7a0d4-349">Se você definiu a ação de stonith como desativada, a máquina virtual será interrompida e os recursos serão migrados para a máquina virtual em execução.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-349">If you set the stonith-action to off, the virtual machine will be stopped and the resources are migrated to the running virtual machine.</span></span>

<span data-ttu-id="7a0d4-350">Depois de instalar a máquina virtual novamente, haverá falha na inicialização do recurso SAP HANA como secundário se você tiver definido AUTOMATED_REGISTER="false".</span><span class="sxs-lookup"><span data-stu-id="7a0d4-350">Once you start the virtual machine again, the SAP HANA resource will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="7a0d4-351">Nesse caso, será preciso configurar a instância HANA como secundária executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7a0d4-351">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="7a0d4-352">Teste de um failover manual</span><span class="sxs-lookup"><span data-stu-id="7a0d4-352">Testing a manual failover</span></span>

<span data-ttu-id="7a0d4-353">Você pode testar um failover manual interrompendo o serviço pacemaker no nó saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-353">You can test a manual failover by stopping the pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="7a0d4-354">Após o failover, você pode iniciar o serviço novamente.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-354">After the failover, you can start the service again.</span></span> <span data-ttu-id="7a0d4-355">O recurso SAP HANA em saphanavm1 falhará ao inicializar como secundário se você tiver definido AUTOMATED_REGISTER="false".</span><span class="sxs-lookup"><span data-stu-id="7a0d4-355">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="7a0d4-356">Nesse caso, será preciso configurar a instância HANA como secundária executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7a0d4-356">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="7a0d4-357">Teste de uma migração</span><span class="sxs-lookup"><span data-stu-id="7a0d4-357">Testing a migration</span></span>

<span data-ttu-id="7a0d4-358">Você pode migrar o nó mestre SAP HANA executando o seguinte comando</span><span class="sxs-lookup"><span data-stu-id="7a0d4-358">You can migrate the SAP HANA master node by executing the following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="7a0d4-359">Isso deve migrar o nó mestre SAP HANA e o grupo que contém o endereço IP virtual para saphanavm2.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-359">This should migrate the SAP HANA master node and the group that contains the virtual IP address to saphanavm2.</span></span>
<span data-ttu-id="7a0d4-360">O recurso SAP HANA em saphanavm1 falhará ao inicializar como secundário se você tiver definido AUTOMATED_REGISTER="false".</span><span class="sxs-lookup"><span data-stu-id="7a0d4-360">The SAP HANA resource on saphanavm1 will fail to start as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="7a0d4-361">Nesse caso, será preciso configurar a instância HANA como secundária executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="7a0d4-361">In this case, you need to configure the HANA instance as secondary by executing the following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop the HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="7a0d4-362">A migração cria restrições de local que precisam ser excluídas novamente.</span><span class="sxs-lookup"><span data-stu-id="7a0d4-362">The migration creates location contraints that need to be deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like the following contraint. You should have two contraints, one for the SAP HANA resource and one for the IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="7a0d4-363">Também é necessário limpar o estado do recurso de nó secundário</span><span class="sxs-lookup"><span data-stu-id="7a0d4-363">You also need to cleanup the state of the secondary node resource</span></span>

<pre><code>
# switch back to root and cleanup the failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="7a0d4-364">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7a0d4-364">Next steps</span></span>
* <span data-ttu-id="7a0d4-365">[Planejamento e implementação de Máquinas Virtuais do Azure para SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="7a0d4-365">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="7a0d4-366">[Implantação de Máquinas Virtuais do Azure para SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="7a0d4-366">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="7a0d4-367">[Implantação DBMS de Máquinas Virtuais do Azure para SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="7a0d4-367">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="7a0d4-368">Para saber como estabelecer a alta disponibilidade e planejar a recuperação de desastre do SAP HANA no Azure (instâncias grandes), confira [Alta disponibilidade e recuperação de desastre do SAP HANA (instâncias grandes) no Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="7a0d4-368">To learn how to establish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
