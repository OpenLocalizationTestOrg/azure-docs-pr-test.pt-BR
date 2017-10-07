---
title: "aaaHigh disponibilidade do SAP HANA em máquinas virtuais do Azure (VMs) | Microsoft Docs"
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
ms.openlocfilehash: dcb9bb70594f9d97f8a888cec76300bcbe0bf1ac
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="high-availability-of-sap-hana-on-azure-virtual-machines-vms"></a><span data-ttu-id="96828-103">Alta disponibilidade do SAP HANA em VMs (máquinas virtuais) do Azure</span><span class="sxs-lookup"><span data-stu-id="96828-103">High Availability of SAP HANA on Azure Virtual Machines (VMs)</span></span>

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

[hana-ha-guide-replication]:sap-hana-high-availability.md#14c19f65-b5aa-4856-9594-b81c7e4df73d
[hana-ha-guide-shared-storage]:sap-hana-high-availability.md#498de331-fa04-490b-997c-b078de457c9d

[suse-hana-ha-guide]:https://www.suse.com/docrep/documents/ir8w88iwu7/suse_linux_enterprise_server_for_sap_applications_12_sp1.pdf
[sap-swcenter]:https://launchpad.support.sap.com/#/softwarecenter
[template-multisid-db]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-multi-sid-db%2Fazuredeploy.json
[template-converged]:https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2Fsap-3-tier-marketplace-image-converged%2Fazuredeploy.json

<span data-ttu-id="96828-113">No local, você pode usar a replicação de sistema HANA ou usar o armazenamento compartilhado tooestablish alta disponibilidade para o SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="96828-113">On-premises, you can use either HANA System Replication or use shared storage tooestablish high availability for SAP HANA.</span></span>
<span data-ttu-id="96828-114">Atualmente, damos suporte apenas à configuração da Replicação do Sistema HANA no Azure.</span><span class="sxs-lookup"><span data-stu-id="96828-114">We currently only support setting up HANA System Replication on Azure.</span></span> <span data-ttu-id="96828-115">A Replicação do Sistema HANA consiste em um nó mestre e, pelo menos, um nó subordinado.</span><span class="sxs-lookup"><span data-stu-id="96828-115">SAP HANA Replication consists of one master node and at least one slave node.</span></span> <span data-ttu-id="96828-116">Alterações toohello dados no nó mestre Olá são replicados nós de subordinado toohello forma síncrona ou assíncrona.</span><span class="sxs-lookup"><span data-stu-id="96828-116">Changes toohello data on hello master node are replicated toohello slave nodes synchronously or asynchronously.</span></span>

<span data-ttu-id="96828-117">Este artigo descreve como máquinas virtuais do toodeploy Olá, configurar máquinas virtuais de hello, instalar o framework de cluster hello, instalar e configurar a replicação de sistema do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="96828-117">This article describes how toodeploy hello virtual machines, configure hello virtual machines, install hello cluster framework, install and configure SAP HANA System Replication.</span></span>
<span data-ttu-id="96828-118">Em configurações de exemplo hello, número da instância etc. 03 de comandos de instalação e HANA HDB de ID de sistema é usado.</span><span class="sxs-lookup"><span data-stu-id="96828-118">In hello example configurations, installation commands etc. instance number 03 and HANA System ID HDB is used.</span></span>

<span data-ttu-id="96828-119">Saudação de leitura a seguir observações sobre o SAP e documentos primeiro</span><span class="sxs-lookup"><span data-stu-id="96828-119">Read hello following SAP Notes and papers first</span></span>

* <span data-ttu-id="96828-120">A Nota SAP [1928533], que tem:</span><span class="sxs-lookup"><span data-stu-id="96828-120">SAP Note [1928533], which has:</span></span>
  * <span data-ttu-id="96828-121">Lista de tamanhos de VM do Azure que têm suporte para implantação de saudação do software SAP</span><span class="sxs-lookup"><span data-stu-id="96828-121">List of Azure VM sizes that are supported for hello deployment of SAP software</span></span>
  * <span data-ttu-id="96828-122">Informações importantes sobre capacidade para tamanhos de VM do Azure</span><span class="sxs-lookup"><span data-stu-id="96828-122">Important capacity information for Azure VM sizes</span></span>
  * <span data-ttu-id="96828-123">Software SAP e combinações de SO (sistema operacional) e banco de dados com suporte</span><span class="sxs-lookup"><span data-stu-id="96828-123">Supported SAP software, and operating system (OS) and database combinations</span></span>
  * <span data-ttu-id="96828-124">A versão do kernel do SAP necessária para Windows e para Linux no Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="96828-124">Required SAP kernel version for Windows and Linux on Microsoft Azure</span></span>
* <span data-ttu-id="96828-125">A Nota SAP [2015553] lista pré-requisitos para implantações de software SAP com suporte do SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="96828-125">SAP Note [2015553] lists prerequisites for SAP-supported SAP software deployments in Azure.</span></span>
* <span data-ttu-id="96828-126">A Nota SAP [2205917] tem configurações de SO recomendadas para SUSE Linux Enterprise Server para aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="96828-126">SAP Note [2205917] has recommended OS settings for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="96828-127">A Nota SAP [1944799] tem Diretrizes SAP HANA para SUSE Linux Enterprise Server para aplicativos SAP</span><span class="sxs-lookup"><span data-stu-id="96828-127">SAP Note [1944799] has SAP HANA Guidelines for SUSE Linux Enterprise Server for SAP Applications</span></span>
* <span data-ttu-id="96828-128">A Nota SAP [2178632] contém informações detalhadas sobre todas as métricas de monitoramentos relatadas para o SAP no Azure.</span><span class="sxs-lookup"><span data-stu-id="96828-128">SAP Note [2178632] has detailed information about all monitoring metrics reported for SAP in Azure.</span></span>
* <span data-ttu-id="96828-129">Nota da SAP [2191498] Olá exigiu versão SAP Host Agent para Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="96828-129">SAP Note [2191498] has hello required SAP Host Agent version for Linux in Azure.</span></span>
* <span data-ttu-id="96828-130">A Nota SAP [2243692] tem informações sobre o licenciamento do SAP no Linux no Azure.</span><span class="sxs-lookup"><span data-stu-id="96828-130">SAP Note [2243692] has information about SAP licensing on Linux in Azure.</span></span>
* <span data-ttu-id="96828-131">A Nota SAP [1984787] tem informações gerais sobre o SUSE Linux Enterprise Server 12.</span><span class="sxs-lookup"><span data-stu-id="96828-131">SAP Note [1984787] has general information about SUSE Linux Enterprise Server 12.</span></span>
* <span data-ttu-id="96828-132">Nota da SAP [1999351] tem informações adicionais de solução de problemas para hello Azure extensão de monitoramento aprimorada para SAP.</span><span class="sxs-lookup"><span data-stu-id="96828-132">SAP Note [1999351] has additional troubleshooting information for hello Azure Enhanced Monitoring Extension for SAP.</span></span>
* <span data-ttu-id="96828-133">[WIKI da comunidade do SAP](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) tem todas as Notas SAP necessárias para Linux.</span><span class="sxs-lookup"><span data-stu-id="96828-133">[SAP Community WIKI](https://wiki.scn.sap.com/wiki/display/HOME/SAPonLinuxNotes) has all required SAP Notes for Linux.</span></span>
* <span data-ttu-id="96828-134">[Planejamento e implementação de Máquinas Virtuais do Azure para SAP no Linux][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="96828-134">[Azure Virtual Machines planning and implementation for SAP on Linux][planning-guide]</span></span>
* <span data-ttu-id="96828-135">[Implantação de máquinas virtuais do Azure para SAP no Linux (este artigo)][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="96828-135">[Azure Virtual Machines deployment for SAP on Linux (this article)][deployment-guide]</span></span>
* <span data-ttu-id="96828-136">[Implantação de Máquinas Virtuais do Azure do DBMS para SAP no Linux][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="96828-136">[Azure Virtual Machines DBMS deployment for SAP on Linux][dbms-guide]</span></span>
* <span data-ttu-id="96828-137">[Cenário de otimização de desempenho do SAP HANA SR] [ suse-hana-ha-guide] guia Olá contém tooset de todas as informações necessárias a replicação de sistema do SAP HANA local.</span><span class="sxs-lookup"><span data-stu-id="96828-137">[SAP HANA SR Performance Optimized Scenario][suse-hana-ha-guide] hello guide contains all required information tooset up SAP HANA System Replication on-premises.</span></span> <span data-ttu-id="96828-138">Use este guia como uma linha de base.</span><span class="sxs-lookup"><span data-stu-id="96828-138">Use this guide as a baseline.</span></span>

## <a name="deploying-linux"></a><span data-ttu-id="96828-139">Implantação do Linux</span><span class="sxs-lookup"><span data-stu-id="96828-139">Deploying Linux</span></span>

<span data-ttu-id="96828-140">Agente de recurso Olá para o SAP HANA está incluído no SUSE Linux Enterprise Server para aplicativos SAP.</span><span class="sxs-lookup"><span data-stu-id="96828-140">hello resource agent for SAP HANA is included in SUSE Linux Enterprise Server for SAP Applications.</span></span>
<span data-ttu-id="96828-141">Hello Azure Marketplace contém uma imagem para SUSE Linux Enterprise Server para 12 de aplicativos SAP com BYOS (Traga sua própria assinatura) que você pode usar máquinas virtuais da nova toodeploy.</span><span class="sxs-lookup"><span data-stu-id="96828-141">hello Azure Marketplace contains an image for SUSE Linux Enterprise Server for SAP Applications 12 with BYOS (Bring Your Own Subscription) that you can use toodeploy new virtual machines.</span></span>

### <a name="manual-deployment"></a><span data-ttu-id="96828-142">Implantação manual</span><span class="sxs-lookup"><span data-stu-id="96828-142">Manual Deployment</span></span>

1. <span data-ttu-id="96828-143">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="96828-143">Create a Resource Group</span></span>
1. <span data-ttu-id="96828-144">Criar uma rede virtual</span><span class="sxs-lookup"><span data-stu-id="96828-144">Create a Virtual Network</span></span>
1. <span data-ttu-id="96828-145">Crie duas Contas de Armazenamento</span><span class="sxs-lookup"><span data-stu-id="96828-145">Create two Storage Accounts</span></span>
1. <span data-ttu-id="96828-146">Crie um Conjunto de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="96828-146">Create an Availability Set</span></span>  
   <span data-ttu-id="96828-147">Defina o máximo de domínio de atualização</span><span class="sxs-lookup"><span data-stu-id="96828-147">Set max update domain</span></span>
1. <span data-ttu-id="96828-148">Crie um Balanceador de Carga (interno)</span><span class="sxs-lookup"><span data-stu-id="96828-148">Create a Load Balancer (internal)</span></span>  
   <span data-ttu-id="96828-149">Selecione a VNET da etapa acima</span><span class="sxs-lookup"><span data-stu-id="96828-149">Select VNET of step above</span></span>
1. <span data-ttu-id="96828-150">Crie a Máquina Virtual 1</span><span class="sxs-lookup"><span data-stu-id="96828-150">Create Virtual Machine 1</span></span>  
   <span data-ttu-id="96828-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="96828-151">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="96828-152">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="96828-152">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="96828-153">Escolha a Conta de Armazenamento 1</span><span class="sxs-lookup"><span data-stu-id="96828-153">Select Storage Account 1</span></span>  
   <span data-ttu-id="96828-154">Escolha o Conjunto de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="96828-154">Select Availability Set</span></span>  
1. <span data-ttu-id="96828-155">Crie a Máquina Virtual 2</span><span class="sxs-lookup"><span data-stu-id="96828-155">Create Virtual Machine 2</span></span>  
   <span data-ttu-id="96828-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span><span class="sxs-lookup"><span data-stu-id="96828-156">https://portal.azure.com/#create/suse-byos.sles-for-sap-byos12-sp1</span></span>  
   <span data-ttu-id="96828-157">SLES For SAP Applications 12 SP1 (BYOS)</span><span class="sxs-lookup"><span data-stu-id="96828-157">SLES For SAP Applications 12 SP1 (BYOS)</span></span>  
   <span data-ttu-id="96828-158">Escolha a Conta de Armazenamento 2</span><span class="sxs-lookup"><span data-stu-id="96828-158">Select Storage Account 2</span></span>   
   <span data-ttu-id="96828-159">Escolha o Conjunto de Disponibilidade</span><span class="sxs-lookup"><span data-stu-id="96828-159">Select Availability Set</span></span>  
1. <span data-ttu-id="96828-160">Adicione Discos de Dados</span><span class="sxs-lookup"><span data-stu-id="96828-160">Add Data Disks</span></span>
1. <span data-ttu-id="96828-161">Configure o balanceador de carga Olá</span><span class="sxs-lookup"><span data-stu-id="96828-161">Configure hello load balancer</span></span>
    1. <span data-ttu-id="96828-162">Crie um pool de IPs de front-end</span><span class="sxs-lookup"><span data-stu-id="96828-162">Create a frontend IP pool</span></span>
        1. <span data-ttu-id="96828-163">Abra o balanceador de carga hello, selecione o pool IP de front-end e clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="96828-163">Open hello load balancer, select frontend IP pool and click Add</span></span>
        1. <span data-ttu-id="96828-164">Digite nome Olá Olá novo front-end do pool de IP (por exemplo hana-front-end)</span><span class="sxs-lookup"><span data-stu-id="96828-164">Enter hello name of hello new frontend IP pool (for example hana-frontend)</span></span>
       1. <span data-ttu-id="96828-165">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="96828-165">Click OK</span></span>
        1. <span data-ttu-id="96828-166">Depois que o novo pool IP de front-end Olá é criado, anote o endereço IP</span><span class="sxs-lookup"><span data-stu-id="96828-166">After hello new frontend IP pool is created, write down its IP address</span></span>
    1. <span data-ttu-id="96828-167">Crie um pool de back-end</span><span class="sxs-lookup"><span data-stu-id="96828-167">Create a backend pool</span></span>
        1. <span data-ttu-id="96828-168">Abra o balanceador de carga hello, selecione os pools de back-end e clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="96828-168">Open hello load balancer, select backend pools and click Add</span></span>
        1. <span data-ttu-id="96828-169">Insira nome de saudação do pool de back-end novo hello (por exemplo hana-back-end)</span><span class="sxs-lookup"><span data-stu-id="96828-169">Enter hello name of hello new backend pool (for example hana-backend)</span></span>
        1. <span data-ttu-id="96828-170">Clique em Adicionar uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="96828-170">Click Add a virtual machine</span></span>
        1. <span data-ttu-id="96828-171">Selecione Olá criado anteriormente do conjunto de disponibilidade</span><span class="sxs-lookup"><span data-stu-id="96828-171">Select hello Availability Set you created earlier</span></span>
        1. <span data-ttu-id="96828-172">Selecione as máquinas virtuais de saudação do cluster do SAP HANA Olá</span><span class="sxs-lookup"><span data-stu-id="96828-172">Select hello virtual machines of hello SAP HANA cluster</span></span>
        1. <span data-ttu-id="96828-173">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="96828-173">Click OK</span></span>
    1. <span data-ttu-id="96828-174">Criar uma investigação de integridade</span><span class="sxs-lookup"><span data-stu-id="96828-174">Create a health probe</span></span>
       1. <span data-ttu-id="96828-175">Abra o balanceador de carga hello, selecione investigações de integridade e clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="96828-175">Open hello load balancer, select health probes and click Add</span></span>
        1. <span data-ttu-id="96828-176">Insira o nome de saudação do teste de integridade novo hello (por exemplo, hana-hp)</span><span class="sxs-lookup"><span data-stu-id="96828-176">Enter hello name of hello new health probe (for example hana-hp)</span></span>
        1. <span data-ttu-id="96828-177">Escolha TCP como protocolo, porta 625**03**, mantenha o Intervalo como 5 e o Limite de não integridade como 2</span><span class="sxs-lookup"><span data-stu-id="96828-177">Select TCP as protocol, port 625**03**, keep Interval 5 and Unhealthy threshold 2</span></span>
        1. <span data-ttu-id="96828-178">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="96828-178">Click OK</span></span>
    1. <span data-ttu-id="96828-179">Criar regras de balanceamento de carga</span><span class="sxs-lookup"><span data-stu-id="96828-179">Create load balancing rules</span></span>
        1. <span data-ttu-id="96828-180">Abra o balanceador de carga hello, selecione as regras de balanceamento de carga e clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="96828-180">Open hello load balancer, select load balancing rules and click Add</span></span>
        1. <span data-ttu-id="96828-181">Insira nome de saudação da nova regra de Balanceador de carga hello (por exemplo hana-lb-3**03**15)</span><span class="sxs-lookup"><span data-stu-id="96828-181">Enter hello name of hello new load balancer rule (for example hana-lb-3**03**15)</span></span>
        1. <span data-ttu-id="96828-182">Endereço IP de front-end Select hello, pool de back-end e integridade teste que você criou anteriormente (por exemplo hana-front-end)</span><span class="sxs-lookup"><span data-stu-id="96828-182">Select hello frontend IP address, backend pool and health probe you created earlier (for example hana-frontend)</span></span>
        1. <span data-ttu-id="96828-183">Mantenha o protocolo TCP, insira a porta 3**03**15</span><span class="sxs-lookup"><span data-stu-id="96828-183">Keep protocol TCP, enter port 3**03**15</span></span>
        1. <span data-ttu-id="96828-184">Aumentar o tempo limite de ociosidade too30 minutos</span><span class="sxs-lookup"><span data-stu-id="96828-184">Increase idle timeout too30 minutes</span></span>
       1. <span data-ttu-id="96828-185">**Certifique-se de que tooenable IP flutuante**</span><span class="sxs-lookup"><span data-stu-id="96828-185">**Make sure tooenable Floating IP**</span></span>
        1. <span data-ttu-id="96828-186">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="96828-186">Click OK</span></span>
        1. <span data-ttu-id="96828-187">Repita as etapas de saudação acima para a porta 3**03**17</span><span class="sxs-lookup"><span data-stu-id="96828-187">Repeat hello steps above for port 3**03**17</span></span>

### <a name="deploy-with-template"></a><span data-ttu-id="96828-188">Implantar com modelo</span><span class="sxs-lookup"><span data-stu-id="96828-188">Deploy with template</span></span>
<span data-ttu-id="96828-189">Você pode usar um dos modelos de início rápido de saudação no github toodeploy todos os recursos necessários.</span><span class="sxs-lookup"><span data-stu-id="96828-189">You can use one of hello quick start templates on github toodeploy all required resources.</span></span> <span data-ttu-id="96828-190">modelo de saudação implanta máquinas virtuais de saudação, o balanceador de carga hello, disponibilidade definida etc. Siga o modelo de saudação de toodeploy essas etapas:</span><span class="sxs-lookup"><span data-stu-id="96828-190">hello template deploys hello virtual machines, hello load balancer, availability set etc. Follow these steps toodeploy hello template:</span></span>

1. <span data-ttu-id="96828-191">Olá abrir [modelo de banco de dados] [ template-multisid-db] ou hello [convergido modelo] [ template-converged] em Olá Portal de modelo de banco de dados de saudação só cria Olá regras de balanceamento de carga para um banco de dados enquanto também cria um modelo convergida Olá Olá regras de balanceamento de carga para um ASCS/SCS e uma instância de ES (Linux).</span><span class="sxs-lookup"><span data-stu-id="96828-191">Open hello [database template][template-multisid-db] or hello [converged template][template-converged] on hello Azure Portal hello database template only creates hello load-balancing rules for a database whereas hello converged template also creates hello load-balancing rules for an ASCS/SCS and ERS (Linux only) instance.</span></span> <span data-ttu-id="96828-192">Se você planejar tooinstall um sistema baseados no SAP NetWeaver e deseja também tooinstall Olá ASCS/SCS de instância em Olá mesmo máquinas, use Olá [convergido modelo][template-converged].</span><span class="sxs-lookup"><span data-stu-id="96828-192">If you plan tooinstall an SAP NetWeaver based system and you also want tooinstall hello ASCS/SCS instance on hello same machines, use hello [converged template][template-converged].</span></span>
1. <span data-ttu-id="96828-193">Digite hello parâmetros a seguir</span><span class="sxs-lookup"><span data-stu-id="96828-193">Enter hello following parameters</span></span>
    1. <span data-ttu-id="96828-194">ID do sistema SAP</span><span class="sxs-lookup"><span data-stu-id="96828-194">Sap System Id</span></span>  
       <span data-ttu-id="96828-195">Insira o sistema SAP de hello, Id de saudação sistema SAP que você deseja tooinstall.</span><span class="sxs-lookup"><span data-stu-id="96828-195">Enter hello SAP system Id of hello SAP system you want tooinstall.</span></span> <span data-ttu-id="96828-196">Olá Id será usado como um prefixo para recursos de saudação que são implantados.</span><span class="sxs-lookup"><span data-stu-id="96828-196">hello Id will be used as a prefix for hello resources that are deployed.</span></span>
    1. <span data-ttu-id="96828-197">Tipo de pilha (aplicável somente se você usar o modelo convergida Olá)</span><span class="sxs-lookup"><span data-stu-id="96828-197">Stack Type (only applicable if you use hello converged template)</span></span>  
       <span data-ttu-id="96828-198">Selecione o tipo de pilha do SAP NetWeaver Olá</span><span class="sxs-lookup"><span data-stu-id="96828-198">Select hello SAP NetWeaver stack type</span></span>
    1. <span data-ttu-id="96828-199">Tipo de sistema operacional</span><span class="sxs-lookup"><span data-stu-id="96828-199">Os Type</span></span>  
       <span data-ttu-id="96828-200">Selecione uma saudação distribuições do Linux.</span><span class="sxs-lookup"><span data-stu-id="96828-200">Select one of hello Linux distributions.</span></span> <span data-ttu-id="96828-201">Para este exemplo, selecione SLES 12 BYOS</span><span class="sxs-lookup"><span data-stu-id="96828-201">For this example, select SLES 12 BYOS</span></span>
    1. <span data-ttu-id="96828-202">Tipo de banco de dados</span><span class="sxs-lookup"><span data-stu-id="96828-202">Db Type</span></span>  
       <span data-ttu-id="96828-203">Selecionar HANA</span><span class="sxs-lookup"><span data-stu-id="96828-203">Select HANA</span></span>
    1. <span data-ttu-id="96828-204">Tamanho do sistema SAP</span><span class="sxs-lookup"><span data-stu-id="96828-204">Sap System Size</span></span>  
       <span data-ttu-id="96828-205">quantidade de saudação do sistema novo do SAPS Olá fornecerá.</span><span class="sxs-lookup"><span data-stu-id="96828-205">hello amount of SAPS hello new system will provide.</span></span> <span data-ttu-id="96828-206">Se não tiver certeza do sistema de saudação SAPS quantos exigirá, peça ao seu parceiro de tecnologia do SAP ou o integrador de sistema</span><span class="sxs-lookup"><span data-stu-id="96828-206">If you are not sure how many SAPS hello system will require, please ask your SAP Technology Partner or System Integrator</span></span>
    1. <span data-ttu-id="96828-207">Disponibilidade do sistema</span><span class="sxs-lookup"><span data-stu-id="96828-207">System Availability</span></span>  
       <span data-ttu-id="96828-208">Selecione HA</span><span class="sxs-lookup"><span data-stu-id="96828-208">Select HA</span></span>
    1. <span data-ttu-id="96828-209">Nome de Usuário de Administrador e Senha do Administrador</span><span class="sxs-lookup"><span data-stu-id="96828-209">Admin Username and Admin Password</span></span>  
       <span data-ttu-id="96828-210">Um novo usuário é criado que pode ser usado toolog toohello máquina.</span><span class="sxs-lookup"><span data-stu-id="96828-210">A new user is created that can be used toolog on toohello machine.</span></span>
    1. <span data-ttu-id="96828-211">Sub-rede Nova ou Existente</span><span class="sxs-lookup"><span data-stu-id="96828-211">New Or Existing Subnet</span></span>  
       <span data-ttu-id="96828-212">Determina se uma nova rede virtual e sub-rede devem ser criadas ou se uma sub-rede existente deve ser usada.</span><span class="sxs-lookup"><span data-stu-id="96828-212">Determines whether a new virtual network and subnet should be created or an existing subnet should be used.</span></span> <span data-ttu-id="96828-213">Se você já tiver uma rede virtual que é a rede de local tooyour conectado, selecione existente.</span><span class="sxs-lookup"><span data-stu-id="96828-213">If you already have a virtual network that is connected tooyour on-premises network, select existing.</span></span>
    1. <span data-ttu-id="96828-214">ID da Sub-rede</span><span class="sxs-lookup"><span data-stu-id="96828-214">Subnet Id</span></span>  
    <span data-ttu-id="96828-215">Olá ID das máquinas virtuais do hello sub-rede toowhich Olá deve ser conectado ao.</span><span class="sxs-lookup"><span data-stu-id="96828-215">hello ID of hello subnet toowhich hello virtual machines should be connected to.</span></span> <span data-ttu-id="96828-216">Selecione a sub-rede de saudação de sua VPN ou rota expressa rede virtual tooconnect Olá máquina virtual tooyour na rede local.</span><span class="sxs-lookup"><span data-stu-id="96828-216">Select hello subnet of your VPN or Express Route virtual network tooconnect hello virtual machine tooyour on-premises network.</span></span> <span data-ttu-id="96828-217">Olá ID geralmente parece com /subscriptions/`<subscription id`> /resourceGroups/`<resource group name`> /providers/Microsoft.Network/virtualNetworks/`<virtual network name`> /subnets/`<subnet name`></span><span class="sxs-lookup"><span data-stu-id="96828-217">hello ID usually looks like /subscriptions/`<subscription id`>/resourceGroups/`<resource group name`>/providers/Microsoft.Network/virtualNetworks/`<virtual network name`>/subnets/`<subnet name`></span></span>

## <a name="setting-up-linux-ha"></a><span data-ttu-id="96828-218">Configuração de HA do Linux</span><span class="sxs-lookup"><span data-stu-id="96828-218">Setting up Linux HA</span></span>

<span data-ttu-id="96828-219">Olá itens a seguir é prefixado com um [A] - nós tooall aplicável, [1] toonode aplicável somente - aplicável apenas toonode [2] ou 1 - 2.</span><span class="sxs-lookup"><span data-stu-id="96828-219">hello following items are prefixed with either [A] - applicable tooall nodes, [1] - only applicable toonode 1 or [2] - only applicable toonode 2.</span></span>

1. <span data-ttu-id="96828-220">[A] SLES para SAP BYOS somente - repositórios de saudação do SLES registrar toobe toouse capaz</span><span class="sxs-lookup"><span data-stu-id="96828-220">[A] SLES for SAP BYOS only - Register SLES toobe able toouse hello repositories</span></span>
1. <span data-ttu-id="96828-221">[A] Apenas SLES for SAP BYOS – adicione o módulo de nuvem pública</span><span class="sxs-lookup"><span data-stu-id="96828-221">[A] SLES for SAP BYOS only - Add public-cloud module</span></span>
1. <span data-ttu-id="96828-222">[A] Atualize o SLES</span><span class="sxs-lookup"><span data-stu-id="96828-222">[A] Update SLES</span></span>
    ```bash
    sudo zypper update

    ```

1. <span data-ttu-id="96828-223">[1] Habilite o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="96828-223">[1] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key
    sudo cat /root/.ssh/id_dsa.pub
    ```

2. <span data-ttu-id="96828-224">[2] Habilite o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="96828-224">[2] Enable ssh access</span></span>
    ```bash
    sudo ssh-keygen -tdsa

    # insert hello public key you copied in hello last step into hello authorized keys file on hello second server
    sudo vi /root/.ssh/authorized_keys
    
    # Enter file in which toosave hello key (/root/.ssh/id_dsa): -> ENTER
    # Enter passphrase (empty for no passphrase): -> ENTER
    # Enter same passphrase again: -> ENTER
    
    # copy hello public key    
    sudo cat /root/.ssh/id_dsa.pub
    ```

1. <span data-ttu-id="96828-225">[1] Habilite o acesso ssh</span><span class="sxs-lookup"><span data-stu-id="96828-225">[1] Enable ssh access</span></span>
    ```bash
    # insert hello public key you copied in hello last step into hello authorized keys file on hello first server
    sudo vi /root/.ssh/authorized_keys
    
    ```

1. <span data-ttu-id="96828-226">[A] Instale a extensão HA</span><span class="sxs-lookup"><span data-stu-id="96828-226">[A] Install HA extension</span></span>
    ```bash
    sudo zypper install sle-ha-release fence-agents
    
    ```

1. <span data-ttu-id="96828-227">[A] Configure o layout do disco</span><span class="sxs-lookup"><span data-stu-id="96828-227">[A] Setup disk layout</span></span>
    1. <span data-ttu-id="96828-228">LVM</span><span class="sxs-lookup"><span data-stu-id="96828-228">LVM</span></span>  
    <span data-ttu-id="96828-229">Geralmente, é recomendável toouse LVM para volumes que armazenam dados e arquivos de log.</span><span class="sxs-lookup"><span data-stu-id="96828-229">We generally recommend toouse LVM for volumes that store data and log files.</span></span> <span data-ttu-id="96828-230">Olá exemplo a seguir supõe que máquinas virtuais de saudação tiver quatro discos de dados anexados que devem ser usado toocreate dois volumes.</span><span class="sxs-lookup"><span data-stu-id="96828-230">hello example below assumes that hello virtual machines have four data disks attached that should be used toocreate two volumes.</span></span>
        * <span data-ttu-id="96828-231">Crie volumes físicos de todos os discos que você deseja toouse.</span><span class="sxs-lookup"><span data-stu-id="96828-231">Create physical volumes for all disks that you want toouse.</span></span>
    <pre><code>
    sudo pvcreate /dev/sdc
    sudo pvcreate /dev/sdd
    sudo pvcreate /dev/sde
    sudo pvcreate /dev/sdf
    </code></pre>
        * <span data-ttu-id="96828-232">Criar um grupo de volumes para arquivos de dados hello, um grupo de volumes para arquivos de log hello e um diretório compartilhado de saudação do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="96828-232">Create a volume group for hello data files, one volume group for hello log files and one for hello shared directory of SAP HANA</span></span>
    <pre><code>
    sudo vgcreate vg_hana_data /dev/sdc /dev/sdd
    sudo vgcreate vg_hana_log /dev/sde
    sudo vgcreate vg_hana_shared /dev/sdf
    </code></pre>
        * <span data-ttu-id="96828-233">Criar hello volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="96828-233">Create hello logical volumes</span></span>
    <pre><code>
    sudo lvcreate -l 100%FREE -n hana_data vg_hana_data
    sudo lvcreate -l 100%FREE -n hana_log vg_hana_log
    sudo lvcreate -l 100%FREE -n hana_shared vg_hana_shared
    sudo mkfs.xfs /dev/vg_hana_data/hana_data
    sudo mkfs.xfs /dev/vg_hana_log/hana_log
    sudo mkfs.xfs /dev/vg_hana_shared/hana_shared
    </code></pre>
        * <span data-ttu-id="96828-234">Criar diretórios de montagem hello e copie Olá UUID de todos os volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="96828-234">Create hello mount directories and copy hello UUID of all logical volumes</span></span>
    <pre><code>
    sudo mkdir -p /hana/data
    sudo mkdir -p /hana/log
    sudo mkdir -p /hana/shared
    # write down hello id of /dev/vg_hana_data/hana_data, /dev/vg_hana_log/hana_log and /dev/vg_hana_shared/hana_shared
    sudo blkid
    </code></pre>
        * <span data-ttu-id="96828-235">Crie entradas de fstab para Olá três volumes lógicos</span><span class="sxs-lookup"><span data-stu-id="96828-235">Create fstab entries for hello three logical volumes</span></span>
    <pre><code>
    sudo vi /etc/fstab
    </code></pre>
    <span data-ttu-id="96828-236">Inserir essa linha muito/etc/fstab</span><span class="sxs-lookup"><span data-stu-id="96828-236">Insert this line too/etc/fstab</span></span>
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_data/hana_data&gt;</b> /hana/data xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_log/hana_log&gt;</b> /hana/log xfs  defaults,nofail  0  2
    /dev/disk/by-uuid/<b>&lt;UUID of /dev/vg_hana_shared/hana_shared&gt;</b> /hana/shared xfs  defaults,nofail  0  2
    </code></pre>
        * <span data-ttu-id="96828-237">Montar Olá novos volumes</span><span class="sxs-lookup"><span data-stu-id="96828-237">Mount hello new volumes</span></span>
    <pre><code>
    sudo mount -a
    </code></pre>
    1. <span data-ttu-id="96828-238">Discos simples</span><span class="sxs-lookup"><span data-stu-id="96828-238">Plain Disks</span></span>  
       <span data-ttu-id="96828-239">Para sistemas pequenos ou de demonstração, você pode colocar os arquivos de log e dados do HANA em um disco.</span><span class="sxs-lookup"><span data-stu-id="96828-239">For small or demo systems, you can place your HANA data and log files on one disk.</span></span> <span data-ttu-id="96828-240">Olá comandos a seguir criar uma partição em /dev/sdc e formate-o com xfs.</span><span class="sxs-lookup"><span data-stu-id="96828-240">hello following commands create a partition on /dev/sdc and format it with xfs.</span></span>
    ```bash
    sudo fdisk /dev/sdc
    sudo mkfs.xfs /dev/sdc1
    
    # <a name="write-down-hello-id-of-devsdc1"></a><span data-ttu-id="96828-241">Anote a id de saudação do /dev/sdc1</span><span class="sxs-lookup"><span data-stu-id="96828-241">write down hello id of /dev/sdc1</span></span>
    <span data-ttu-id="96828-242">sudo /sbin/blkid  sudo vi /etc/fstab</span><span class="sxs-lookup"><span data-stu-id="96828-242">sudo /sbin/blkid  sudo vi /etc/fstab</span></span>
    ```

    Insert this line too/etc/fstab
    <pre><code>
    /dev/disk/by-uuid/<b>&lt;UUID&gt;</b> /hana xfs  defaults,nofail  0  2
    </code></pre>

    Create hello target directory and mount hello disk.

    ```bash
    sudo mkdir /hana
    sudo mount -a
    ```

1. <span data-ttu-id="96828-243">[A] Configure a resolução de nome do host para todos os hosts</span><span class="sxs-lookup"><span data-stu-id="96828-243">[A] Setup host name resolution for all hosts</span></span>  
    <span data-ttu-id="96828-244">Você pode usar um servidor DNS ou modificar /etc/hosts Olá em todos os nós.</span><span class="sxs-lookup"><span data-stu-id="96828-244">You can either use a DNS server or modify hello /etc/hosts on all nodes.</span></span> <span data-ttu-id="96828-245">Este exemplo mostra como toouse Olá arquivo /etc/hosts.</span><span class="sxs-lookup"><span data-stu-id="96828-245">This example shows how toouse hello /etc/hosts file.</span></span>
   <span data-ttu-id="96828-246">Substituir endereço IP de saudação e nome de host Olá no hello comandos a seguir</span><span class="sxs-lookup"><span data-stu-id="96828-246">Replace hello IP address and hello hostname in hello following commands</span></span>
    ```bash
    sudo vi /etc/hosts
    ```
    <span data-ttu-id="96828-247">Inserir saudação linhas muito/etc/hosts a seguir.</span><span class="sxs-lookup"><span data-stu-id="96828-247">Insert hello following lines too/etc/hosts.</span></span> <span data-ttu-id="96828-248">Alterar o ambiente de saudação IP toomatch de endereço e o nome do host</span><span class="sxs-lookup"><span data-stu-id="96828-248">Change hello IP address and hostname toomatch your environment</span></span>    
    
    <pre><code>
    <b>&lt;IP address of host 1&gt; &lt;hostname of host 1&gt;</b>
    <b>&lt;IP address of host 2&gt; &lt;hostname of host 2&gt;</b>
    </code></pre>

1. <span data-ttu-id="96828-249">[1] Instale o Cluster</span><span class="sxs-lookup"><span data-stu-id="96828-249">[1] Install Cluster</span></span>
    ```bash
    sudo ha-cluster-init
    
    # Do you want toocontinue anyway? [y/N] -> y
    # Network address toobind too(e.g.: 192.168.1.0) [10.79.227.0] -> ENTER
    # Multicast address (e.g.: 239.x.x.x) [239.174.218.125] -> ENTER
    # Multicast port [5405] -> ENTER
    # Do you wish toouse SBD? [y/N] -> N
    # Do you wish tooconfigure an administration IP? [y/N] -> N
    ```
        
1. <span data-ttu-id="96828-250">[2] adicionar nó toocluster</span><span class="sxs-lookup"><span data-stu-id="96828-250">[2] Add node toocluster</span></span>
    ```bash
    sudo ha-cluster-join
        
    # WARNING: NTP is not configured toostart at system boot.
    # WARNING: No watchdog device found. If SBD is used, hello cluster will be unable toostart without a watchdog.
    # Do you want toocontinue anyway? [y/N] -> y
    # IP address or hostname of existing node (e.g.: 192.168.1.1) [] -> IP address of node 1 e.g. 10.0.0.5
    # /root/.ssh/id_dsa already exists - overwrite? [y/N] N
    ```

1. <span data-ttu-id="96828-251">[A] alteração hacluster senha toohello mesma senha</span><span class="sxs-lookup"><span data-stu-id="96828-251">[A] Change hacluster password toohello same password</span></span>
    ```bash
    sudo passwd hacluster
    
    ```

1. <span data-ttu-id="96828-252">[A] configurar corosync toouse outro transporte e adicionar nodelist.</span><span class="sxs-lookup"><span data-stu-id="96828-252">[A] Configure corosync toouse other transport and add nodelist.</span></span> <span data-ttu-id="96828-253">Caso contrário, o cluster não funcionará.</span><span class="sxs-lookup"><span data-stu-id="96828-253">Cluster will not work otherwise.</span></span>
    ```bash
    sudo vi /etc/corosync/corosync.conf    
    
    ```

    <span data-ttu-id="96828-254">Adicione Olá negrito toohello conteúdo de arquivo a seguir.</span><span class="sxs-lookup"><span data-stu-id="96828-254">Add hello following bold content toohello file.</span></span>
    
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

    <span data-ttu-id="96828-255">Em seguida, reinicie o serviço de corosync Olá</span><span class="sxs-lookup"><span data-stu-id="96828-255">Then restart hello corosync service</span></span>

    ```bash
    sudo service corosync restart
    
    ```

1. <span data-ttu-id="96828-256">[A] Instale os pacotes HANA HA</span><span class="sxs-lookup"><span data-stu-id="96828-256">[A] Install HANA HA packages</span></span>  
    ```bash
    sudo zypper install SAPHanaSR
    
    ```

## <a name="installing-sap-hana"></a><span data-ttu-id="96828-257">Instalando o SAP HANA</span><span class="sxs-lookup"><span data-stu-id="96828-257">Installing SAP HANA</span></span>

<span data-ttu-id="96828-258">Siga o capítulo 4 de saudação [guia de cenário de otimização de desempenho do SAP HANA SR] [ suse-hana-ha-guide] tooinstall replicação de sistema do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="96828-258">Follow chapter 4 of hello [SAP HANA SR Performance Optimized Scenario guide][suse-hana-ha-guide] tooinstall SAP HANA System Replication.</span></span>

1. <span data-ttu-id="96828-259">[A] executar hdblcm Olá HANA DVD</span><span class="sxs-lookup"><span data-stu-id="96828-259">[A] Run hdblcm from hello HANA DVD</span></span>
    * <span data-ttu-id="96828-260">Escolha instalação -> 1</span><span class="sxs-lookup"><span data-stu-id="96828-260">Choose installation -> 1</span></span>
    * <span data-ttu-id="96828-261">Selecione os componentes adicionais para instalação -> 1</span><span class="sxs-lookup"><span data-stu-id="96828-261">Select additional components for installation -> 1</span></span>
    * <span data-ttu-id="96828-262">Insira o caminho de instalação [/hana/shared]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-262">Enter Installation Path [/hana/shared]: -> ENTER</span></span>
    * <span data-ttu-id="96828-263">Insira o Nome do Host Local [..]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-263">Enter Local Host Name [..]: -> ENTER</span></span>
    * <span data-ttu-id="96828-264">Você deseja que o sistema de toohello tooadd hosts adicionais?</span><span class="sxs-lookup"><span data-stu-id="96828-264">Do you want tooadd additional hosts toohello system?</span></span> <span data-ttu-id="96828-265">(s/n) [n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-265">(y/n) [n]: -> ENTER</span></span>
    * <span data-ttu-id="96828-266">Insira a ID do Sistema SAP HANA: <SID of HANA e.g. HDB></span><span class="sxs-lookup"><span data-stu-id="96828-266">Enter SAP HANA System ID: <SID of HANA e.g. HDB></span></span>
    * <span data-ttu-id="96828-267">Insira o Número da Instância [00]:</span><span class="sxs-lookup"><span data-stu-id="96828-267">Enter Instance Number [00]:</span></span>   
  <span data-ttu-id="96828-268">Número da instância do HANA.</span><span class="sxs-lookup"><span data-stu-id="96828-268">HANA Instance number.</span></span> <span data-ttu-id="96828-269">Use 03 se usado Olá modelo do Azure ou seguido exemplo hello acima</span><span class="sxs-lookup"><span data-stu-id="96828-269">Use 03 if you used hello Azure Template or followed hello example above</span></span>
    * <span data-ttu-id="96828-270">Selecione Modo de Banco de Dados/Inserir Índice [1]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-270">Select Database Mode / Enter Index [1]: -> ENTER</span></span>
    * <span data-ttu-id="96828-271">Selecione o Uso do Sistema/Inserir Índice [4]:</span><span class="sxs-lookup"><span data-stu-id="96828-271">Select System Usage / Enter Index [4]:</span></span>  
  <span data-ttu-id="96828-272">Selecione o sistema de saudação uso</span><span class="sxs-lookup"><span data-stu-id="96828-272">Select hello system Usage</span></span>
    * <span data-ttu-id="96828-273">Informe o Local dos Volumes de Dados [/data/hana/HDB]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-273">Enter Location of Data Volumes [/hana/data/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="96828-274">Informe o Local dos Volumes de Log [/hana/log/HDB]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-274">Enter Location of Log Volumes [/hana/log/HDB]: -> ENTER</span></span>
    * <span data-ttu-id="96828-275">Restringir a alocação máxima de memória?</span><span class="sxs-lookup"><span data-stu-id="96828-275">Restrict maximum memory allocation?</span></span> <span data-ttu-id="96828-276">[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-276">[n]: -> ENTER</span></span>
    * <span data-ttu-id="96828-277">Insira o nome de Host do certificado para o Host '...' [...]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-277">Enter Certificate Host Name For Host '...' [...]: -> ENTER</span></span>
    * <span data-ttu-id="96828-278">Insira a Senha de Usuário do Agente do Host SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="96828-278">Enter SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="96828-279">Confirme a Senha de Usuário do Agente do Host SAP (sapadm):</span><span class="sxs-lookup"><span data-stu-id="96828-279">Confirm SAP Host Agent User (sapadm) Password:</span></span>
    * <span data-ttu-id="96828-280">Insira a Senha do Administrador de Sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="96828-280">Enter System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="96828-281">Confirme a Senha do Administrador de Sistema (hdbadm):</span><span class="sxs-lookup"><span data-stu-id="96828-281">Confirm System Administrator (hdbadm) Password:</span></span>
    * <span data-ttu-id="96828-282">Insira o Diretório Base do Administrador de Sistema [/usr/sap/HDB/home]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-282">Enter System Administrator Home Directory [/usr/sap/HDB/home]: -> ENTER</span></span>
    * <span data-ttu-id="96828-283">Insira o Shell de Logon do Administrador de Sistema [/bin/sh]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-283">Enter System Administrator Login Shell [/bin/sh]: -> ENTER</span></span>
    * <span data-ttu-id="96828-284">Insira a ID de Usuário do Administrador de Sistema [1001]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-284">Enter System Administrator User ID [1001]: -> ENTER</span></span>
    * <span data-ttu-id="96828-285">Insira a ID do Grupo de Usuários (sapsys) [79]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-285">Enter ID of User Group (sapsys) [79]: -> ENTER</span></span>
    * <span data-ttu-id="96828-286">Insira a Senha de Usuário do Banco de Dados (SYSTEM):</span><span class="sxs-lookup"><span data-stu-id="96828-286">Enter Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="96828-287">Confirme a Senha de Usuário do Banco de Dados (SYSTEM):</span><span class="sxs-lookup"><span data-stu-id="96828-287">Confirm Database User (SYSTEM) Password:</span></span>
    * <span data-ttu-id="96828-288">Reiniciar o sistema após a reinicialização do computador?</span><span class="sxs-lookup"><span data-stu-id="96828-288">Restart system after machine reboot?</span></span> <span data-ttu-id="96828-289">[n]: -> ENTER</span><span class="sxs-lookup"><span data-stu-id="96828-289">[n]: -> ENTER</span></span>
    * <span data-ttu-id="96828-290">Você deseja toocontinue?</span><span class="sxs-lookup"><span data-stu-id="96828-290">Do you want toocontinue?</span></span> <span data-ttu-id="96828-291">(s/n):</span><span class="sxs-lookup"><span data-stu-id="96828-291">(y/n):</span></span>  
  <span data-ttu-id="96828-292">Validar Olá resumo e digite y toocontinue</span><span class="sxs-lookup"><span data-stu-id="96828-292">Validate hello summary and enter y toocontinue</span></span>
1. <span data-ttu-id="96828-293">[A] Atualize o Agente do Host do SAP</span><span class="sxs-lookup"><span data-stu-id="96828-293">[A] Upgrade SAP Host Agent</span></span>  
  <span data-ttu-id="96828-294">Baixe o arquivo de SAP Host Agent mais recente de saudação do hello [SAP Softwarecenter] [ sap-swcenter] e execução hello comando tooupgrade Olá agente a seguir.</span><span class="sxs-lookup"><span data-stu-id="96828-294">Download hello latest SAP Host Agent archive from hello [SAP Softwarecenter][sap-swcenter] and run hello following command tooupgrade hello agent.</span></span> <span data-ttu-id="96828-295">Substitua saudação caminho toohello toopoint toohello arquivo baixado.</span><span class="sxs-lookup"><span data-stu-id="96828-295">Replace hello path toohello archive toopoint toohello file you downloaded.</span></span>
    ```bash
    sudo /usr/sap/hostctrl/exe/saphostexec -upgrade -archive <path tooSAP Host Agent SAR>
    ```

1. <span data-ttu-id="96828-296">[1] Crie uma replicação HANA (como raiz)</span><span class="sxs-lookup"><span data-stu-id="96828-296">[1] Create HANA replication (as root)</span></span>  
    <span data-ttu-id="96828-297">Execute Olá comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="96828-297">Run hello following command.</span></span> <span data-ttu-id="96828-298">Verifique se tooreplace negrito cadeias de caracteres (HANA HDB de ID de sistema e instância número 03) com valores de saudação da instalação do SAP HANA.</span><span class="sxs-lookup"><span data-stu-id="96828-298">Make sure tooreplace bold strings (HANA System ID HDB and instance number 03) with hello values of your SAP HANA installation.</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> 'CREATE USER <b>hdb</b>hasync PASSWORD "<b>passwd</b>"' 
    hdbsql -u system -i <b>03</b> 'GRANT DATA ADMIN too<b>hdb</b>hasync' 
    hdbsql -u system -i <b>03</b> 'ALTER USER <b>hdb</b>hasync DISABLE PASSWORD LIFETIME' 
    </code></pre>

1. <span data-ttu-id="96828-299">[A] Criar entrada de repositório de chaves (como raiz)</span><span class="sxs-lookup"><span data-stu-id="96828-299">[A] Create keystore entry (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbuserstore SET <b>hdb</b>haloc localhost:3<b>03</b>15 <b>hdb</b>hasync <b>passwd</b>
    </code></pre>
1. <span data-ttu-id="96828-300">[1] Faça o backup do banco de dados backup (como raiz)</span><span class="sxs-lookup"><span data-stu-id="96828-300">[1] Backup database (as root)</span></span>
    <pre><code>
    PATH="$PATH:/usr/sap/<b>HDB</b>/HDB<b>03</b>/exe"
    hdbsql -u system -i <b>03</b> "BACKUP DATA USING FILE ('<b>initialbackup</b>')" 
    </code></pre>
1. <span data-ttu-id="96828-301">[1] alterne toohello sapsid usuário (por exemplo, hdbadm) e criar o site primário hello.</span><span class="sxs-lookup"><span data-stu-id="96828-301">[1] Switch toohello sapsid user (for example hdbadm) and create hello primary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    hdbnsutil -sr_enable –-name=<b>SITE1</b>
    </code></pre>
1. <span data-ttu-id="96828-302">[2] alterne toohello sapsid usuário (por exemplo, hdbadm) e criar site secundário hello.</span><span class="sxs-lookup"><span data-stu-id="96828-302">[2] Switch toohello sapsid user (for example hdbadm) and create hello secondary site.</span></span>
    <pre><code>
    su - <b>hdb</b>adm
    sapcontrol -nr <b>03</b> -function StopWait 600 10
    hdbnsutil -sr_register --remoteHost=<b>saphanavm1</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE2</b> 
    </code></pre>

## <a name="configure-cluster-framework"></a><span data-ttu-id="96828-303">Configurar a estrutura do cluster</span><span class="sxs-lookup"><span data-stu-id="96828-303">Configure Cluster Framework</span></span>

<span data-ttu-id="96828-304">Alterar as configurações padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="96828-304">Change hello default settings</span></span>

<pre>
sudo vi crm-defaults.txt
# enter hello following toocrm-defaults.txt
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="96828-305">Agora podemos carregar o cluster de toohello arquivo hello</span><span class="sxs-lookup"><span data-stu-id="96828-305">now we load hello file toohello cluster</span></span>
<span data-ttu-id="96828-306">sudo crm configure load update crm-defaults.txt</span><span class="sxs-lookup"><span data-stu-id="96828-306">sudo crm configure load update crm-defaults.txt</span></span>
</pre>

### <a name="create-stonith-device"></a><span data-ttu-id="96828-307">Criar dispositivo STONITH</span><span class="sxs-lookup"><span data-stu-id="96828-307">Create STONITH device</span></span>

<span data-ttu-id="96828-308">dispositivo STONITH Olá usa tooauthorize uma entidade de serviço no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="96828-308">hello STONITH device uses a Service Principal tooauthorize against Microsoft Azure.</span></span> <span data-ttu-id="96828-309">Siga essas etapas toocreate uma entidade de serviço.</span><span class="sxs-lookup"><span data-stu-id="96828-309">Please follow these steps toocreate a Service Principal.</span></span>

1. <span data-ttu-id="96828-310">Vá muito<https://portal.azure.com></span><span class="sxs-lookup"><span data-stu-id="96828-310">Go too<https://portal.azure.com></span></span>
1. <span data-ttu-id="96828-311">Folha de Active Directory do Azure Olá aberto</span><span class="sxs-lookup"><span data-stu-id="96828-311">Open hello Azure Active Directory blade</span></span>  
   <span data-ttu-id="96828-312">Vá tooProperties e anote Olá ID de diretório. Isso é hello **id de locatário**.</span><span class="sxs-lookup"><span data-stu-id="96828-312">Go tooProperties and write down hello Directory Id. This is hello **tenant id**.</span></span>
1. <span data-ttu-id="96828-313">Clique em Registros do Aplicativo</span><span class="sxs-lookup"><span data-stu-id="96828-313">Click App registrations</span></span>
1. <span data-ttu-id="96828-314">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="96828-314">Click Add</span></span>
1. <span data-ttu-id="96828-315">Digite um Nome, selecione Tipo de Aplicativo "Aplicativo Web/API", insira uma URL de logon (por exemplo, http://localhost) e clique em Criar</span><span class="sxs-lookup"><span data-stu-id="96828-315">Enter a Name, select Application Type "Web app/API", enter a sign-on URL (for example http://localhost) and click Create</span></span>
1. <span data-ttu-id="96828-316">URL de entrada Hello não é usado e pode ser qualquer URL válido</span><span class="sxs-lookup"><span data-stu-id="96828-316">hello sign-on URL is not used and can be any valid URL</span></span>
1. <span data-ttu-id="96828-317">Selecione Olá novo aplicativo e clique em chaves no guia de configurações de saudação</span><span class="sxs-lookup"><span data-stu-id="96828-317">Select hello new App and click Keys in hello Settings tab</span></span>
1. <span data-ttu-id="96828-318">Insira uma descrição para uma nova chave, selecione "Nunca expira" e clique em Salvar</span><span class="sxs-lookup"><span data-stu-id="96828-318">Enter a description for a new key, select "Never expires" and click Save</span></span>
1. <span data-ttu-id="96828-319">Anote o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="96828-319">Write down hello Value.</span></span> <span data-ttu-id="96828-320">Ele é usado como Olá **senha** para Olá entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="96828-320">It is used as hello **password** for hello Service Principal</span></span>
1. <span data-ttu-id="96828-321">Anote a saudação ID do aplicativo. Ele é usado como Olá username (**id de logon** nas etapas de saudação abaixo) de saudação entidade de serviço</span><span class="sxs-lookup"><span data-stu-id="96828-321">Write down hello Application Id. It is used as hello username (**login id** in hello steps below) of hello Service Principal</span></span>

<span data-ttu-id="96828-322">Olá entidade de serviço não tem permissões tooaccess seus recursos do Azure por padrão.</span><span class="sxs-lookup"><span data-stu-id="96828-322">hello Service Principal does not have permissions tooaccess your Azure resources by default.</span></span> <span data-ttu-id="96828-323">Você precisa toogive toostart de permissões de entidade de serviço de saudação e parar (desalocar) todas as máquinas virtuais do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="96828-323">You need toogive hello Service Principal permissions toostart and stop (deallocate) all virtual machines of hello cluster.</span></span>

1. <span data-ttu-id="96828-324">Vá toohttps://portal.azure.com</span><span class="sxs-lookup"><span data-stu-id="96828-324">Go toohttps://portal.azure.com</span></span>
1. <span data-ttu-id="96828-325">Abrir Olá folha de todos os recursos</span><span class="sxs-lookup"><span data-stu-id="96828-325">Open hello All resources blade</span></span>
1. <span data-ttu-id="96828-326">Selecione a máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="96828-326">Select hello virtual machine</span></span>
1. <span data-ttu-id="96828-327">Clique em Controle de acesso (IAM)</span><span class="sxs-lookup"><span data-stu-id="96828-327">Click Access control (IAM)</span></span>
1. <span data-ttu-id="96828-328">Clique em Adicionar</span><span class="sxs-lookup"><span data-stu-id="96828-328">Click Add</span></span>
1. <span data-ttu-id="96828-329">Selecione a função hello proprietário</span><span class="sxs-lookup"><span data-stu-id="96828-329">Select hello role Owner</span></span>
1. <span data-ttu-id="96828-330">Insira nome de saudação do aplicativo hello criado acima</span><span class="sxs-lookup"><span data-stu-id="96828-330">Enter hello name of hello application you created above</span></span>
1. <span data-ttu-id="96828-331">Clique em OK</span><span class="sxs-lookup"><span data-stu-id="96828-331">Click OK</span></span>

<span data-ttu-id="96828-332">Depois de editar permissões Olá para máquinas virtuais de hello, você pode configurar dispositivos STONITH de saudação em cluster hello.</span><span class="sxs-lookup"><span data-stu-id="96828-332">After you edited hello permissions for hello virtual machines, you can configure hello STONITH devices in hello cluster.</span></span>

<pre>
sudo vi crm-fencing.txt
# enter hello following toocrm-fencing.txt
# replace hello bold string with your subscription id, resource group, tenant id, service principal id and password
<code>
primitive rsc_st_azure_1 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

primitive rsc_st_azure_2 stonith:fence_azure_arm \
    params subscriptionId="<b>subscription id</b>" resourceGroup="<b>resource group</b>" tenantId="<b>tenant id</b>" login="<b>login id</b>" passwd="<b>password</b>"

colocation col_st_azure -2000: rsc_st_azure_1:Started rsc_st_azure_2:Started
</code>

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="96828-333">Agora podemos carregar o cluster de toohello arquivo hello</span><span class="sxs-lookup"><span data-stu-id="96828-333">now we load hello file toohello cluster</span></span>
<span data-ttu-id="96828-334">sudo crm configure load update crm-fencing.txt</span><span class="sxs-lookup"><span data-stu-id="96828-334">sudo crm configure load update crm-fencing.txt</span></span>
</pre>

### <a name="create-sap-hana-resources"></a><span data-ttu-id="96828-335">Criar recursos do SAP HANA</span><span class="sxs-lookup"><span data-stu-id="96828-335">Create SAP HANA resources</span></span>

<pre>
sudo vi crm-saphanatop.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number and HANA system id
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="96828-336">Agora podemos carregar o cluster de toohello arquivo hello</span><span class="sxs-lookup"><span data-stu-id="96828-336">now we load hello file toohello cluster</span></span>
<span data-ttu-id="96828-337">sudo crm configure load update crm-saphanatop.txt</span><span class="sxs-lookup"><span data-stu-id="96828-337">sudo crm configure load update crm-saphanatop.txt</span></span>
</pre>

<pre>
sudo vi crm-saphana.txt
# enter hello following toocrm-saphana.txt
# replace hello bold string with your instance number, HANA system id and hello frontend IP address of hello Azure load balancer. 
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

# <a name="now-we-load-hello-file-toohello-cluster"></a><span data-ttu-id="96828-338">Agora podemos carregar o cluster de toohello arquivo hello</span><span class="sxs-lookup"><span data-stu-id="96828-338">now we load hello file toohello cluster</span></span>
<span data-ttu-id="96828-339">sudo crm configure load update crm-saphana.txt</span><span class="sxs-lookup"><span data-stu-id="96828-339">sudo crm configure load update crm-saphana.txt</span></span>
</pre>

### <a name="test-cluster-setup"></a><span data-ttu-id="96828-340">Testar configuração do cluster</span><span class="sxs-lookup"><span data-stu-id="96828-340">Test cluster setup</span></span>
<span data-ttu-id="96828-341">Olá capítulo a seguir descreve como você pode testar sua instalação.</span><span class="sxs-lookup"><span data-stu-id="96828-341">hello following chapter describe how you can test your setup.</span></span> <span data-ttu-id="96828-342">Cada teste pressupõe que são raiz e o mestre do SAP HANA hello está sendo executado no hello saphanavm1 de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="96828-342">Every test assumes that you are root and hello SAP HANA master is running on hello virtual machine saphanavm1.</span></span>

#### <a name="fencing-test"></a><span data-ttu-id="96828-343">Teste de isolamento</span><span class="sxs-lookup"><span data-stu-id="96828-343">Fencing Test</span></span>

<span data-ttu-id="96828-344">Você pode testar a instalação do agente de isolamento de saudação Olá desabilitando a interface de rede de saudação no nó saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="96828-344">You can test hello setup of hello fencing agent by disabling hello network interface on node saphanavm1.</span></span>

<pre><code>
sudo ifdown eth0
</code></pre>

<span data-ttu-id="96828-345">máquina virtual de saudação agora deve obter reiniciada ou interrompida, dependendo da configuração do cluster.</span><span class="sxs-lookup"><span data-stu-id="96828-345">hello virtual machine should now get restarted or stopped depending on your cluster configuration.</span></span>
<span data-ttu-id="96828-346">Se você definir Olá stonith ação toooff, máquina virtual de saudação será interrompida e recursos de saudação são migrado toohello máquina virtual em execução.</span><span class="sxs-lookup"><span data-stu-id="96828-346">If you set hello stonith-action toooff, hello virtual machine will be stopped and hello resources are migrated toohello running virtual machine.</span></span>

<span data-ttu-id="96828-347">Assim que você iniciar a máquina virtual de saudação novamente, Olá recursos SAP HANA falhará toostart como secundário se você definir AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="96828-347">Once you start hello virtual machine again, hello SAP HANA resource will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="96828-348">Nesse caso, você precisa tooconfigure Olá HANA instância secundária executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="96828-348">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b>

# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-manual-failover"></a><span data-ttu-id="96828-349">Teste de um failover manual</span><span class="sxs-lookup"><span data-stu-id="96828-349">Testing a manual failover</span></span>

<span data-ttu-id="96828-350">Você pode testar um failover manual, interrompendo o serviço de pacemaker de saudação no nó saphanavm1.</span><span class="sxs-lookup"><span data-stu-id="96828-350">You can test a manual failover by stopping hello pacemaker service on node saphanavm1.</span></span>
<pre><code>
service pacemaker stop
</code></pre>

<span data-ttu-id="96828-351">Após o failover hello, você pode iniciar o serviço de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="96828-351">After hello failover, you can start hello service again.</span></span> <span data-ttu-id="96828-352">Olá recursos SAP HANA em saphanavm1 falhará toostart como secundário se você definir AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="96828-352">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="96828-353">Nesse caso, você precisa tooconfigure Olá HANA instância secundária executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="96828-353">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
service pacemaker start
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 


# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

#### <a name="testing-a-migration"></a><span data-ttu-id="96828-354">Teste de uma migração</span><span class="sxs-lookup"><span data-stu-id="96828-354">Testing a migration</span></span>

<span data-ttu-id="96828-355">Você pode migrar o nó principal do SAP HANA Olá executando o comando a seguir de saudação</span><span class="sxs-lookup"><span data-stu-id="96828-355">You can migrate hello SAP HANA master node by executing hello following command</span></span>
<pre><code>
crm resource migrate msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
crm resource migrate g_ip_<b>HDB</b>_HDB<b>03</b> <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="96828-356">Isso deve migrar o nó mestre do SAP HANA hello e grupo Olá que contém toosaphanavm2 de endereço IP virtual hello.</span><span class="sxs-lookup"><span data-stu-id="96828-356">This should migrate hello SAP HANA master node and hello group that contains hello virtual IP address toosaphanavm2.</span></span>
<span data-ttu-id="96828-357">Olá recursos SAP HANA em saphanavm1 falhará toostart como secundário se você definir AUTOMATED_REGISTER = "false".</span><span class="sxs-lookup"><span data-stu-id="96828-357">hello SAP HANA resource on saphanavm1 will fail toostart as secondary if you set AUTOMATED_REGISTER="false".</span></span> <span data-ttu-id="96828-358">Nesse caso, você precisa tooconfigure Olá HANA instância secundária executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="96828-358">In this case, you need tooconfigure hello HANA instance as secondary by executing hello following command:</span></span>

<pre><code>
su - <b>hdb</b>adm

# Stop hello HANA instance just in case it is running
sapcontrol -nr <b>03</b> -function StopWait 600 10
hdbnsutil -sr_register --remoteHost=<b>saphanavm2</b> --remoteInstance=<b>03</b> --replicationMode=sync --name=<b>SITE1</b> 
</code></pre>

<span data-ttu-id="96828-359">migração de saudação cria restrições de local que precisam toobe excluída novamente.</span><span class="sxs-lookup"><span data-stu-id="96828-359">hello migration creates location contraints that need toobe deleted again.</span></span>

<pre><code>
crm configure edited

# delete location contraints that are named like hello following contraint. You should have two contraints, one for hello SAP HANA resource and one for hello IP address group.
location cli-prefer-g_ip_<b>HDB</b>_HDB<b>03</b> g_ip_<b>HDB</b>_HDB<b>03</b> role=Started inf: <b>saphanavm2</b>
</code></pre>

<span data-ttu-id="96828-360">Você também precisa toocleanup estado de saudação do recurso de nó secundário Olá</span><span class="sxs-lookup"><span data-stu-id="96828-360">You also need toocleanup hello state of hello secondary node resource</span></span>

<pre><code>
# switch back tooroot and cleanup hello failed state
exit
crm resource cleanup msl_SAPHana_<b>HDB</b>_HDB<b>03</b> <b>saphanavm1</b>
</code></pre>

## <a name="next-steps"></a><span data-ttu-id="96828-361">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="96828-361">Next steps</span></span>
* <span data-ttu-id="96828-362">[Planejamento e implementação de Máquinas Virtuais do Azure para SAP][planning-guide]</span><span class="sxs-lookup"><span data-stu-id="96828-362">[Azure Virtual Machines planning and implementation for SAP][planning-guide]</span></span>
* <span data-ttu-id="96828-363">[Implantação de Máquinas Virtuais do Azure para SAP][deployment-guide]</span><span class="sxs-lookup"><span data-stu-id="96828-363">[Azure Virtual Machines deployment for SAP][deployment-guide]</span></span>
* <span data-ttu-id="96828-364">[Implantação DBMS de Máquinas Virtuais do Azure para SAP][dbms-guide]</span><span class="sxs-lookup"><span data-stu-id="96828-364">[Azure Virtual Machines DBMS deployment for SAP][dbms-guide]</span></span>
* <span data-ttu-id="96828-365">toolearn como tooestablish alta disponibilidade e o plano de recuperação de desastres do HANA SAP no Azure (instâncias grandes), consulte [SAP HANA (instâncias grandes) alta disponibilidade e recuperação de desastres no Azure](hana-overview-high-availability-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="96828-365">toolearn how tooestablish high availability and plan for disaster recovery of SAP HANA on Azure (large instances), see [SAP HANA (large instances) high availability and disaster recovery on Azure](hana-overview-high-availability-disaster-recovery.md).</span></span> 
