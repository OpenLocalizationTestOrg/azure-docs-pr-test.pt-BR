---
title: "Replicar uma implantação do Dynamics AX de várias camadas usando o Azure Site Recovery | Microsoft Docs"
description: Este artigo descreve como replicar e proteger o Dynamics AX usando o Azure Site Recovery
services: site-recovery
documentationcenter: 
author: asgang
manager: rochakm
editor: 
ms.assetid: 9126f5e8-e9ed-4c31-b6b4-bf969c12c184
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/24/2017
ms.author: asgang
ms.openlocfilehash: 03127c8f4841b67436c4819628319705af0b2cd5
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="aa66a-103">Replicar um aplicativo do Dynamics AX de várias camadas usando o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="aa66a-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="aa66a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="aa66a-104">Overview</span></span>


<span data-ttu-id="aa66a-105">O Microsoft Dynamics AX é uma das mais populares soluções de ERP entre as empresas para padronizar o processo entre locais, gerenciar recursos e simplificar a conformidade.</span><span class="sxs-lookup"><span data-stu-id="aa66a-105">Microsoft Dynamics AX is one of the most popular ERP solution among enterprises to standardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="aa66a-106">Considerando que o aplicativo é crítico para os negócios de uma organização, é muito importante ter certeza de que, em caso de desastre, o aplicativo estará em execução no tempo mínimo.</span><span class="sxs-lookup"><span data-stu-id="aa66a-106">Considering the application is business critical to an organization it is very important to be sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="aa66a-107">Hoje, o Microsoft Dynamics AX não fornece nenhuma funcionalidade integrada de recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="aa66a-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="aa66a-108">O Microsoft Dynamics AX consiste em vários componentes de servidor como o Servidor de Objetos de Aplicativo, o AD (Active Directory), o servidor de Banco de Dados SQL, o SharePoint Server, o Servidor de Relatórios, etc. Gerenciar a recuperação de desastre de cada um desses componentes manualmente não é apenas caro mas também propenso a erros.</span><span class="sxs-lookup"><span data-stu-id="aa66a-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. To manage the disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="aa66a-109">Este artigo explica em detalhes sobre como você pode criar uma solução de recuperação de desastre para seu aplicativo Dynamics AX usando o [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="aa66a-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="aa66a-110">Ele também aborda failovers planejados/não planejados/de teste usando o plano de recuperação com um único clique, configurações com suporte e pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="aa66a-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="aa66a-111">A solução de recuperação de desastre baseada no Azure Site Recovery é totalmente testada, certificada e recomendada pelo Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="aa66a-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="aa66a-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aa66a-112">Prerequisites</span></span>

<span data-ttu-id="aa66a-113">A implementação de recuperação de desastre para aplicativos do Dynamics AX usando o Azure Site Recovery requer os pré-requisitos a seguir concluídos.</span><span class="sxs-lookup"><span data-stu-id="aa66a-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires the following pre-requisites completed.</span></span>

<span data-ttu-id="aa66a-114">•   Uma implantação local do Dynamics AX foi configurada</span><span class="sxs-lookup"><span data-stu-id="aa66a-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="aa66a-115">•   Um cofre dos Serviços do Azure Site Recovery foi criado em uma assinatura do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="aa66a-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="aa66a-116">•   Se o Azure for seu site de recuperação, execute a ferramenta de Avaliação de Prontidão de Máquina Virtual do Azure nas VMs, a fim de garantir que elas sejam compatíveis com as VMs do Azure e com os Serviços do Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="aa66a-116">•   If Azure is your recovery site, run the Azure Virtual Machine Readiness Assessment tool  on VMs to ensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="aa66a-117">Suporte do Site Recovery</span><span class="sxs-lookup"><span data-stu-id="aa66a-117">Site Recovery support</span></span>

<span data-ttu-id="aa66a-118">Para a finalidade de criação deste artigo, usamos as máquinas virtuais do VMware com o Dynamics AX 2012 R3 no Windows Server 2012 R2 Enterprise.</span><span class="sxs-lookup"><span data-stu-id="aa66a-118">For the purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="aa66a-119">Já que a replicação do Site Recovery é independente do aplicativo, as recomendações fornecidas aqui devem servir também para os cenários a seguir.</span><span class="sxs-lookup"><span data-stu-id="aa66a-119">As site recovery replication is application agnostic, the recommendations provided here are expected to hold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="aa66a-120">Origem e destino</span><span class="sxs-lookup"><span data-stu-id="aa66a-120">Source and target</span></span>

<span data-ttu-id="aa66a-121">**Cenário**</span><span class="sxs-lookup"><span data-stu-id="aa66a-121">**Scenario**</span></span> | <span data-ttu-id="aa66a-122">**Para um site secundário**</span><span class="sxs-lookup"><span data-stu-id="aa66a-122">**To a secondary site**</span></span> | <span data-ttu-id="aa66a-123">**Para o Azure**</span><span class="sxs-lookup"><span data-stu-id="aa66a-123">**To Azure**</span></span>
--- | --- | ---
<span data-ttu-id="aa66a-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="aa66a-124">**Hyper-V**</span></span> | <span data-ttu-id="aa66a-125">Sim</span><span class="sxs-lookup"><span data-stu-id="aa66a-125">Yes</span></span> | <span data-ttu-id="aa66a-126">Sim</span><span class="sxs-lookup"><span data-stu-id="aa66a-126">Yes</span></span>
<span data-ttu-id="aa66a-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="aa66a-127">**VMware**</span></span> | <span data-ttu-id="aa66a-128">Sim</span><span class="sxs-lookup"><span data-stu-id="aa66a-128">Yes</span></span> | <span data-ttu-id="aa66a-129">Sim</span><span class="sxs-lookup"><span data-stu-id="aa66a-129">Yes</span></span>
<span data-ttu-id="aa66a-130">**Servidor físico**</span><span class="sxs-lookup"><span data-stu-id="aa66a-130">**Physical server**</span></span> | <span data-ttu-id="aa66a-131">Sim</span><span class="sxs-lookup"><span data-stu-id="aa66a-131">Yes</span></span> | <span data-ttu-id="aa66a-132">Sim</span><span class="sxs-lookup"><span data-stu-id="aa66a-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="aa66a-133">Habilitar a DR do aplicativo Dynamics AX usando o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="aa66a-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="aa66a-134">Proteger o aplicativo Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="aa66a-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="aa66a-135">Cada componente do Dynamics AX precisa ser protegido para habilitar a replicação e a recuperação completas do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="aa66a-135">Each component of the Dynamics AX needs to be protected to enable the complete application replication and recovery.</span></span> <span data-ttu-id="aa66a-136">Esta seção aborda:</span><span class="sxs-lookup"><span data-stu-id="aa66a-136">This section covers:</span></span>

<span data-ttu-id="aa66a-137">**1. Proteção do Active Directory**</span><span class="sxs-lookup"><span data-stu-id="aa66a-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="aa66a-138">**2. Proteção da Camada SQL**</span><span class="sxs-lookup"><span data-stu-id="aa66a-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="aa66a-139">**3. Proteção de Aplicativo e as Camadas da Web**</span><span class="sxs-lookup"><span data-stu-id="aa66a-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="aa66a-140">**4. Configuração de rede**</span><span class="sxs-lookup"><span data-stu-id="aa66a-140">**4. Networking configuration**</span></span>

<span data-ttu-id="aa66a-141">**5. Plano de Recuperação**</span><span class="sxs-lookup"><span data-stu-id="aa66a-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="aa66a-142">1. Instalação do AD e replicação de DNS</span><span class="sxs-lookup"><span data-stu-id="aa66a-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="aa66a-143">O Active Directory é necessário no site de DR para o aplicativo Dynamics AX funcionar.</span><span class="sxs-lookup"><span data-stu-id="aa66a-143">Active Directory is required on the DR site for Dynamics AX application to function.</span></span> <span data-ttu-id="aa66a-144">Há duas opções recomendadas com base na complexidade do ambiente local do cliente.</span><span class="sxs-lookup"><span data-stu-id="aa66a-144">There are two recommended choices based on the complexity of the customer’s on-premises environment.</span></span>

<span data-ttu-id="aa66a-145">**Opção 1**</span><span class="sxs-lookup"><span data-stu-id="aa66a-145">**Option 1**</span></span>

<span data-ttu-id="aa66a-146">Se o cliente tem um número pequeno de aplicativos e um único controlador de domínio para todo o site local e eles estão apresentando falhas em todo o site conjuntamente, é recomendável usar a replicação do ASR para replicar o computador do DC para um site secundário (isso é aplicável tanto de site a site quando de site para o Azure).</span><span class="sxs-lookup"><span data-stu-id="aa66a-146">If the customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over the entire site together, then we recommend using ASR-Replication to replicate the DC machine to secondary site (applicable for both Site to Site and Site to Azure).</span></span>

<span data-ttu-id="aa66a-147">**Opção 2**</span><span class="sxs-lookup"><span data-stu-id="aa66a-147">**Option 2**</span></span>

<span data-ttu-id="aa66a-148">Se o cliente tem um grande número de aplicativos e está executando uma floresta do Active Directory e se fará failover de poucos aplicativos por vez, é recomendável configurar um controlador de domínio adicional no site de DR (em um site secundário ou no Azure).</span><span class="sxs-lookup"><span data-stu-id="aa66a-148">If the customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on the DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="aa66a-149">Consulte [guia complementar para tornar um controlador de domínio disponível no site de DR](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="aa66a-149">Please refer to [companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="aa66a-150">Para o restante deste documento, presumiremos que um DC está disponível no site de DR.</span><span class="sxs-lookup"><span data-stu-id="aa66a-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="aa66a-151">2. Configurar a Replicação do SQL Server</span><span class="sxs-lookup"><span data-stu-id="aa66a-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="aa66a-152">Consulte o guia complementar para obter diretrizes técnicas detalhadas sobre a opção recomendada para proteger a [camada SQL](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="aa66a-152">Please refer to companion guide  for detailed technical guidance on the recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="aa66a-153">3. Habilitar a proteção do cliente Dynamics AX e VMs AOS</span><span class="sxs-lookup"><span data-stu-id="aa66a-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="aa66a-154">Executar configuração relevante do Azure Site Recovery com base em as VMs estarem sendo implantadas em [Hyper-V](site-recovery-hyper-v-site-to-azure.md) ou [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="aa66a-154">Perform relevant Azure Site Recovery configuration based on whether the VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="aa66a-155">A frequência de falha consistente recomendada para configurar é 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="aa66a-155">Recommended Crash consistent frequency to configure is 15 minutes.</span></span>
>

<span data-ttu-id="aa66a-156">O instantâneo abaixo mostra o status de proteção de VMs componentes do Dynamics no cenário de proteção 'Site de VMware para Azure'.</span><span class="sxs-lookup"><span data-stu-id="aa66a-156">The below snapshot shows the protection status of Dynamics component VMs in ‘VMware site to Azure’ protection scenario.</span></span>
<span data-ttu-id="aa66a-157">![Itens protegidos ](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="aa66a-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="aa66a-158">4. Configurar Rede</span><span class="sxs-lookup"><span data-stu-id="aa66a-158">4. Configure Networking</span></span>
<span data-ttu-id="aa66a-159">Definir as Configurações de Rede e de Computação de VM</span><span class="sxs-lookup"><span data-stu-id="aa66a-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="aa66a-160">Para as VMs do AOS e do cliente AX, defina as configurações de rede no Azure Site Recovery para que as redes VMs sejam anexadas à rede de DR correta após o failover.</span><span class="sxs-lookup"><span data-stu-id="aa66a-160">For the AX client and AOS VMs configure network settings in Azure Site Recovery so that the VM networks get attached to the right DR network after failover.</span></span> <span data-ttu-id="aa66a-161">Verifique se a rede de DR para essas camadas é roteável para a camada SQL.</span><span class="sxs-lookup"><span data-stu-id="aa66a-161">Ensure the DR network for these tiers is routable to the SQL tier.</span></span>

<span data-ttu-id="aa66a-162">Você pode selecionar a VM nos itens replicados para definir as configurações de rede, conforme mostrado no instantâneo a seguir.</span><span class="sxs-lookup"><span data-stu-id="aa66a-162">You can select the VM in the replicated items to configure the network settings as shown in the snapshot below.</span></span>

* <span data-ttu-id="aa66a-163">Para servidores AOS, selecione o conjunto de disponibilidade correto.</span><span class="sxs-lookup"><span data-stu-id="aa66a-163">For AOS servers select the correct availability set.</span></span>

* <span data-ttu-id="aa66a-164">Se você estiver usando um IP estático, especifique o IP que você deseja usar na máquina virtual nas ![Configurações de Rede](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png) do campo **IP de Destino**</span><span class="sxs-lookup"><span data-stu-id="aa66a-164">If you are using a static IP then specify the IP that you want the virtual machine to take in the **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="aa66a-165">5. Criar um plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="aa66a-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="aa66a-166">Crie um plano de recuperação no Azure Site Recovery para automatizar o processo de failover.</span><span class="sxs-lookup"><span data-stu-id="aa66a-166">You can create a recovery plan in Azure Site Recovery to automate the failover process.</span></span> <span data-ttu-id="aa66a-167">Adicione a camada de aplicativos e a camada da Web no plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="aa66a-167">Add app tier and web tier in the Recovery Plan.</span></span> <span data-ttu-id="aa66a-168">Ordene-as em grupos diferentes, para que o front-end se desligue antes da camada de aplicativos.</span><span class="sxs-lookup"><span data-stu-id="aa66a-168">Order them in different groups so that the front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="aa66a-169">Selecione o cofre do Azure Site Recovery em sua assinatura e clique no bloco “Planos de Recuperação”.</span><span class="sxs-lookup"><span data-stu-id="aa66a-169">Select the Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="aa66a-170">Clique em '+ Plano de recuperação' e especifique um nome.</span><span class="sxs-lookup"><span data-stu-id="aa66a-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="aa66a-171">Selecione a 'Origem' e o 'Destino'.</span><span class="sxs-lookup"><span data-stu-id="aa66a-171">Select the ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="aa66a-172">O destino pode ser o Azure ou um site secundário.</span><span class="sxs-lookup"><span data-stu-id="aa66a-172">The target can be Azure or secondary site.</span></span> <span data-ttu-id="aa66a-173">Caso escolha o Azure, você deverá especificar o modelo de implantação</span><span class="sxs-lookup"><span data-stu-id="aa66a-173">In case you choose Azure, you must specify the deployment model</span></span>

![Criar Plano de Recuperação](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="aa66a-175">Selecione as VMs do AOS e de cliente para o plano de recuperação e clique em ✓.</span><span class="sxs-lookup"><span data-stu-id="aa66a-175">Select the AOS and client VMs to the recovery plan and click ✓.</span></span>
<span data-ttu-id="aa66a-176">![Criar Plano de Recuperação](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="aa66a-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Plano de Recuperação](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="aa66a-178">Você pode personalizar o plano de recuperação do aplicativo Dynamics AX adicionando várias etapas, conforme detalhado abaixo.</span><span class="sxs-lookup"><span data-stu-id="aa66a-178">You can customize the recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="aa66a-179">O instantâneo acima mostra o plano de recuperação completo depois de adicionar todas as etapas.</span><span class="sxs-lookup"><span data-stu-id="aa66a-179">The above snapshot shows the complete recovery plan after adding all the steps.</span></span>

<span data-ttu-id="aa66a-180">*Etapas:*</span><span class="sxs-lookup"><span data-stu-id="aa66a-180">*Steps:*</span></span>

<span data-ttu-id="aa66a-181">*1. Etapas de failover do SQL Server*</span><span class="sxs-lookup"><span data-stu-id="aa66a-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="aa66a-182">Consulte o guia complementar ['Solução de recuperação de desastres do SQL Server'](site-recovery-sql.md) para obter detalhes sobre etapas de recuperação específicas para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="aa66a-182">Refer to [‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific to SQL server.</span></span>

<span data-ttu-id="aa66a-183">*2. Grupo de Failover 1: fazer failover das VMs do AOS*</span><span class="sxs-lookup"><span data-stu-id="aa66a-183">*2. Failover Group 1: Fail over the AOS VMs*</span></span>

<span data-ttu-id="aa66a-184">Verifique se o ponto de recuperação selecionado está tão próximo quanto possível do PIT do banco de dados, mas não à frente dele.</span><span class="sxs-lookup"><span data-stu-id="aa66a-184">Make sure that the recovery point selected is as close as possible to the database PIT but not ahead.</span></span>

<span data-ttu-id="aa66a-185">*3. Script: adicionar balanceador de carga (apenas E-A)* Adicione um script (por meio da Automação do Azure) depois do aparecimento do grupo de VMs do AOS para adicionar um balanceador de carga para ele.</span><span class="sxs-lookup"><span data-stu-id="aa66a-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up to add a load balancer to it.</span></span> <span data-ttu-id="aa66a-186">Você pode usar um script para realizar essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="aa66a-186">You can use a script to do this task.</span></span> <span data-ttu-id="aa66a-187">Consulte o artigo [como adicionar balanceador de carga para DR de aplicativos de várias camadas](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="aa66a-187">Refer article [how to add load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="aa66a-188">*4. Grupo de Failover 2: fazer failover das VMs do cliente do AX.*</span><span class="sxs-lookup"><span data-stu-id="aa66a-188">*4. Failover Group 2: Fail over the AX client VMs.*</span></span>
<span data-ttu-id="aa66a-189">Faça failover das VMs da camada da Web como parte do plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="aa66a-189">Fail over the web tier VMs as part of the recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="aa66a-190">Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="aa66a-190">Doing a test failover</span></span>

<span data-ttu-id="aa66a-191">Consulte os guias complementares 'Solução de recuperação de desastres do AD' e 'Solução de recuperação de desastre do SQL Server' para considerações específicas para o AD e o SQL Server, respectivamente, durante o failover de teste.</span><span class="sxs-lookup"><span data-stu-id="aa66a-191">Refer to ‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific to AD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="aa66a-192">Vá para o Portal do Azure e selecione seu cofre do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="aa66a-192">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="aa66a-193">Clique no plano de recuperação criado para o Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="aa66a-193">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="aa66a-194">Clique em 'Failover de Teste'.</span><span class="sxs-lookup"><span data-stu-id="aa66a-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="aa66a-195">Selecione a rede virtual para iniciar o processo de failover de teste.</span><span class="sxs-lookup"><span data-stu-id="aa66a-195">Select the virtual network to start the test fail-over process.</span></span>
5.  <span data-ttu-id="aa66a-196">Quando o ambiente secundário estiver funcionando, você poderá executar sua validações.</span><span class="sxs-lookup"><span data-stu-id="aa66a-196">Once the secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="aa66a-197">Após a conclusão das validações, selecione 'Validações concluídas', e o ambiente do failover de teste será limpo.</span><span class="sxs-lookup"><span data-stu-id="aa66a-197">Once the validations are complete, you can select ‘Validations complete’ and the test failover environment will be cleaned.</span></span>

<span data-ttu-id="aa66a-198">Siga [este guia](site-recovery-test-failover-to-azure.md) fazer um failover de teste.</span><span class="sxs-lookup"><span data-stu-id="aa66a-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) to do a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="aa66a-199">Executar um failover</span><span class="sxs-lookup"><span data-stu-id="aa66a-199">Doing a failover</span></span>

1.  <span data-ttu-id="aa66a-200">Vá para o Portal do Azure e selecione seu cofre do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="aa66a-200">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="aa66a-201">Clique no plano de recuperação criado para o Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="aa66a-201">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="aa66a-202">Clique em 'Failover' e selecione 'Failover'.</span><span class="sxs-lookup"><span data-stu-id="aa66a-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="aa66a-203">Selecione a rede de destino e clique no ícone de verificação ✓ para iniciar o processo de failover.</span><span class="sxs-lookup"><span data-stu-id="aa66a-203">Select the target network and click ✓ to start the failover process.</span></span>

<span data-ttu-id="aa66a-204">Siga [este guia](site-recovery-failover.md) quando estiver realizando um failover.</span><span class="sxs-lookup"><span data-stu-id="aa66a-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="aa66a-205">Executar um Failback</span><span class="sxs-lookup"><span data-stu-id="aa66a-205">Perform a Failback</span></span>

<span data-ttu-id="aa66a-206">Consulte o guia complementar 'Solução de DR do SQL Server' para considerações específicas para o SQL Server durante o failback.</span><span class="sxs-lookup"><span data-stu-id="aa66a-206">Refer to ‘SQL Server DR Solution ’ companion guide for considerations specific to SQL server during Failback.</span></span>

1.  <span data-ttu-id="aa66a-207">Vá para o Portal do Azure e selecione seu cofre do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="aa66a-207">Go to Azure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="aa66a-208">Clique no plano de recuperação criado para o Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="aa66a-208">Click on the recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="aa66a-209">Clique em 'Failover' e selecione o failover.</span><span class="sxs-lookup"><span data-stu-id="aa66a-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="aa66a-210">Clique em 'Alterar Direção'.</span><span class="sxs-lookup"><span data-stu-id="aa66a-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="aa66a-211">Selecione as opções apropriadas – de sincronização de dados e de criação de VMs</span><span class="sxs-lookup"><span data-stu-id="aa66a-211">Select the appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="aa66a-212">Clique em ✓ para iniciar o processo de 'Failback'.</span><span class="sxs-lookup"><span data-stu-id="aa66a-212">Click ✓ to start the ‘Failback’ process.</span></span>


<span data-ttu-id="aa66a-213">Siga [estas diretrizes](site-recovery-failback-azure-to-vmware.md) quando estiver realizando um failback.</span><span class="sxs-lookup"><span data-stu-id="aa66a-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="aa66a-214">Resumo</span><span class="sxs-lookup"><span data-stu-id="aa66a-214">Summary</span></span>
<span data-ttu-id="aa66a-215">Com o Azure Site Recovery, você pode criar um plano totalmente automatizado de recuperação de desastre para seu aplicativo do Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="aa66a-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="aa66a-216">Você poderá iniciar o failover em segundos e de qualquer lugar, caso haja uma interrupção e fazer o aplicativo funcionar em questão de minutos.</span><span class="sxs-lookup"><span data-stu-id="aa66a-216">You can initiate the failover within seconds from anywhere in the event of a disruption and get the application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aa66a-217">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aa66a-217">Next steps</span></span>
<span data-ttu-id="aa66a-218">Leia [Quais cargas de trabalho posso proteger?](site-recovery-workload.md) para saber mais sobre como proteger as cargas de trabalho corporativas com o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="aa66a-218">Read [What workloads can I protect?](site-recovery-workload.md) to learn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
