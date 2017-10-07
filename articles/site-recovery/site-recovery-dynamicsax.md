---
title: "aaaReplicate uma implantação do Dynamics AX de várias camada usando o Azure Site Recovery | Microsoft Docs"
description: Este artigo descreve como tooreplicate e proteger usando o Azure Site Recovery do Dynamics AX
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
ms.openlocfilehash: b974315ec50ab2ec43846b3d3f95c7de88b72fc3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-a-multi-tier-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="0306f-103">Replicar um aplicativo do Dynamics AX de várias camadas usando o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0306f-103">Replicate a multi-tier Dynamics AX application using Azure Site Recovery</span></span>

## <a name="overview"></a><span data-ttu-id="0306f-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0306f-104">Overview</span></span>


<span data-ttu-id="0306f-105">O Microsoft Dynamics AX é uma solução ERP mais popular Olá entre o processo de toostandardized empresas em locais, gerenciar recursos e simplificar a conformidade.</span><span class="sxs-lookup"><span data-stu-id="0306f-105">Microsoft Dynamics AX is one of hello most popular ERP solution among enterprises toostandardized process across locations, manage resources and simplifying compliance.</span></span> <span data-ttu-id="0306f-106">Considerando que o aplicativo hello é organização tooan críticos de negócios é muito importante toobe-se de que se qualquer desastre, aplicativo deve estar em execução no tempo mínimo.</span><span class="sxs-lookup"><span data-stu-id="0306f-106">Considering hello application is business critical tooan organization it is very important toobe sure that if any disaster, application should be up and running in minimum time.</span></span>

<span data-ttu-id="0306f-107">Hoje, o Microsoft Dynamics AX não fornece nenhuma funcionalidade integrada de recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="0306f-107">Today, Microsoft Dynamics AX  does not provide any out-of-the-box disaster recovery capabilities.</span></span> <span data-ttu-id="0306f-108">O Microsoft Dynamics AX consiste em vários componentes de servidor como banco de dados do servidor de objeto de aplicativo, Active Directory (AD), SQL Server, SharePoint Server, recuperação de desastres de saudação do Reporting Server etc toomanage de cada um desses componentes manualmente é não apenas cara, mas também propensas a erros.</span><span class="sxs-lookup"><span data-stu-id="0306f-108">Microsoft Dynamics AX consists of many server components like Application Object Server, Active Directory (AD), SQL Database Server, SharePoint Server, Reporting Server etc. toomanage hello disaster recovery of each of these components manually is not only expensive but also error-prone.</span></span>

<span data-ttu-id="0306f-109">Este artigo explica em detalhes sobre como você pode criar uma solução de recuperação de desastre para seu aplicativo Dynamics AX usando o [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="0306f-109">This article explains in detail about how you can create a disaster recovery solution for your Dynamics AX application using [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="0306f-110">Ele também aborda failovers planejados/não planejados/de teste usando o plano de recuperação com um único clique, configurações com suporte e pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="0306f-110">It also covers planned/unplanned/test failovers using one-click recovery plan, supported configurations, and prerequisites.</span></span>
<span data-ttu-id="0306f-111">A solução de recuperação de desastre baseada no Azure Site Recovery é totalmente testada, certificada e recomendada pelo Microsoft Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="0306f-111">Azure Site Recovery based disaster recovery solution is fully tested, certified, and recommended by Microsoft Dynamics AX.</span></span>



## <a name="prerequisites"></a><span data-ttu-id="0306f-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0306f-112">Prerequisites</span></span>

<span data-ttu-id="0306f-113">Implementação de recuperação de desastres para o aplicativo Dynamics AX usando o Azure Site Recovery requer Olá concluídos os pré-requisitos a seguir.</span><span class="sxs-lookup"><span data-stu-id="0306f-113">Implementing disaster recovery for Dynamics AX application using Azure Site Recovery requires hello following pre-requisites completed.</span></span>

<span data-ttu-id="0306f-114">•   Uma implantação local do Dynamics AX foi configurada</span><span class="sxs-lookup"><span data-stu-id="0306f-114">•   An on-premises Dynamics AX deployment has been set up</span></span>

<span data-ttu-id="0306f-115">•   Um cofre dos Serviços do Azure Site Recovery foi criado em uma assinatura do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="0306f-115">•   Azure Site Recovery Services vault has been created in Microsoft Azure subscription</span></span>

<span data-ttu-id="0306f-116">• Se seu site de recuperação do Azure é executar Olá avaliação de prontidão de máquina Virtual do Azure ferramenta tooensure VMs que são compatíveis com VMs do Azure e serviços de recuperação de Site do Azure</span><span class="sxs-lookup"><span data-stu-id="0306f-116">•   If Azure is your recovery site, run hello Azure Virtual Machine Readiness Assessment tool  on VMs tooensure that they are compatible with Azure VMs and Azure Site Recovery Services</span></span>


## <a name="site-recovery-support"></a><span data-ttu-id="0306f-117">Suporte do Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0306f-117">Site Recovery support</span></span>

<span data-ttu-id="0306f-118">Para finalidade de saudação de criação deste artigo, as máquinas virtuais VMware com 2012R3 do Dynamics AX no Windows Server 2012 R2 Enterprise foram usadas.</span><span class="sxs-lookup"><span data-stu-id="0306f-118">For hello purpose of creating this article, VMware virtual machines with Dynamics AX  2012R3 on Windows Server 2012 R2 Enterprise were used.</span></span> <span data-ttu-id="0306f-119">Como a replicação de recuperação de site é independente do aplicativo, fornecidas recomendações Olá aqui são toohold esperado nos cenários a seguir também.</span><span class="sxs-lookup"><span data-stu-id="0306f-119">As site recovery replication is application agnostic, hello recommendations provided here are expected toohold on following scenarios as well.</span></span>

### <a name="source-and-target"></a><span data-ttu-id="0306f-120">Origem e destino</span><span class="sxs-lookup"><span data-stu-id="0306f-120">Source and target</span></span>

<span data-ttu-id="0306f-121">**Cenário**</span><span class="sxs-lookup"><span data-stu-id="0306f-121">**Scenario**</span></span> | <span data-ttu-id="0306f-122">**site secundário tooa**</span><span class="sxs-lookup"><span data-stu-id="0306f-122">**tooa secondary site**</span></span> | <span data-ttu-id="0306f-123">**tooAzure**</span><span class="sxs-lookup"><span data-stu-id="0306f-123">**tooAzure**</span></span>
--- | --- | ---
<span data-ttu-id="0306f-124">**Hyper-V**</span><span class="sxs-lookup"><span data-stu-id="0306f-124">**Hyper-V**</span></span> | <span data-ttu-id="0306f-125">Sim</span><span class="sxs-lookup"><span data-stu-id="0306f-125">Yes</span></span> | <span data-ttu-id="0306f-126">Sim</span><span class="sxs-lookup"><span data-stu-id="0306f-126">Yes</span></span>
<span data-ttu-id="0306f-127">**VMware**</span><span class="sxs-lookup"><span data-stu-id="0306f-127">**VMware**</span></span> | <span data-ttu-id="0306f-128">Sim</span><span class="sxs-lookup"><span data-stu-id="0306f-128">Yes</span></span> | <span data-ttu-id="0306f-129">Sim</span><span class="sxs-lookup"><span data-stu-id="0306f-129">Yes</span></span>
<span data-ttu-id="0306f-130">**Servidor físico**</span><span class="sxs-lookup"><span data-stu-id="0306f-130">**Physical server**</span></span> | <span data-ttu-id="0306f-131">Sim</span><span class="sxs-lookup"><span data-stu-id="0306f-131">Yes</span></span> | <span data-ttu-id="0306f-132">Sim</span><span class="sxs-lookup"><span data-stu-id="0306f-132">Yes</span></span>

## <a name="enable-dr-of-dynamics-ax-application-using-azure-site-recovery"></a><span data-ttu-id="0306f-133">Habilitar a DR do aplicativo Dynamics AX usando o Azure Site Recovery</span><span class="sxs-lookup"><span data-stu-id="0306f-133">Enable DR of Dynamics AX application using Azure Site Recovery</span></span>
### <a name="protect-your-dynamics-ax-application"></a><span data-ttu-id="0306f-134">Proteger o aplicativo Dynamics AX</span><span class="sxs-lookup"><span data-stu-id="0306f-134">Protect your Dynamics AX application</span></span>
<span data-ttu-id="0306f-135">Cada componente do hello Dynamics AX necessidades toobe protegido tooenable Olá aplicativo completo replicação e a recuperação.</span><span class="sxs-lookup"><span data-stu-id="0306f-135">Each component of hello Dynamics AX needs toobe protected tooenable hello complete application replication and recovery.</span></span> <span data-ttu-id="0306f-136">Esta seção aborda:</span><span class="sxs-lookup"><span data-stu-id="0306f-136">This section covers:</span></span>

<span data-ttu-id="0306f-137">**1. Proteção do Active Directory**</span><span class="sxs-lookup"><span data-stu-id="0306f-137">**1. Protection of Active Directory**</span></span>

<span data-ttu-id="0306f-138">**2. Proteção da Camada SQL**</span><span class="sxs-lookup"><span data-stu-id="0306f-138">**2. Protection of SQL Tier**</span></span>

<span data-ttu-id="0306f-139">**3. Proteção de Aplicativo e as Camadas da Web**</span><span class="sxs-lookup"><span data-stu-id="0306f-139">**3. Protection of App and Web Tiers**</span></span>

<span data-ttu-id="0306f-140">**4. Configuração de rede**</span><span class="sxs-lookup"><span data-stu-id="0306f-140">**4. Networking configuration**</span></span>

<span data-ttu-id="0306f-141">**5. Plano de Recuperação**</span><span class="sxs-lookup"><span data-stu-id="0306f-141">**5. Recovery Plan**</span></span>

### <a name="1-setup-ad-and-dns-replication"></a><span data-ttu-id="0306f-142">1. Instalação do AD e replicação de DNS</span><span class="sxs-lookup"><span data-stu-id="0306f-142">1. Setup AD and DNS replication</span></span>

<span data-ttu-id="0306f-143">Active Directory é necessário no local de recuperação de desastres Olá para toofunction de aplicativo do Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="0306f-143">Active Directory is required on hello DR site for Dynamics AX application toofunction.</span></span> <span data-ttu-id="0306f-144">Há duas opções recomendadas com base em complexidade Olá Olá do local do ambiente de cliente.</span><span class="sxs-lookup"><span data-stu-id="0306f-144">There are two recommended choices based on hello complexity of hello customer’s on-premises environment.</span></span>

<span data-ttu-id="0306f-145">**Opção 1**</span><span class="sxs-lookup"><span data-stu-id="0306f-145">**Option 1**</span></span>

<span data-ttu-id="0306f-146">Se Olá cliente tiver um pequeno número de aplicativos e um único controlador de domínio para seu todo site local e será estar falhando em todo o site Olá juntos, em seguida, é recomendável usar a replicação de ASR tooreplicate Olá DC máquina toosecondary site ( aplicável para o Site tooSite e tooAzure do Site).</span><span class="sxs-lookup"><span data-stu-id="0306f-146">If hello customer has a small number of applications and a single domain controller for his entire on-premises site and will be failing over hello entire site together, then we recommend using ASR-Replication tooreplicate hello DC machine toosecondary site (applicable for both Site tooSite and Site tooAzure).</span></span>

<span data-ttu-id="0306f-147">**Opção 2**</span><span class="sxs-lookup"><span data-stu-id="0306f-147">**Option 2**</span></span>

<span data-ttu-id="0306f-148">Se cliente Olá tem um grande número de aplicativos e está em execução para uma floresta do Active Directory e será failover alguns aplicativos cada vez, é recomendável configurar um controlador de domínio no site Olá DR (site secundário ou no Azure).</span><span class="sxs-lookup"><span data-stu-id="0306f-148">If hello customer has a large number of applications and is running an Active Directory forest and will fail-over few applications at a time, then we recommend setting up an additional domain controller on hello DR site (secondary site or in Azure).</span></span>

<span data-ttu-id="0306f-149">Consulte também[guia complementar de tornar um controlador de domínio disponível no site de recuperação de desastres](site-recovery-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="0306f-149">Please refer too[companion guide on making a domain controller available on DR site](site-recovery-active-directory.md).</span></span> <span data-ttu-id="0306f-150">Para o restante deste documento, presumiremos que um DC está disponível no site de DR.</span><span class="sxs-lookup"><span data-stu-id="0306f-150">For remainder of this document we will assume a DC is available on DR site.</span></span>

### <a name="2-setup-sql-server-replication"></a><span data-ttu-id="0306f-151">2. Configurar a Replicação do SQL Server</span><span class="sxs-lookup"><span data-stu-id="0306f-151">2. Setup SQL Server replication</span></span>
<span data-ttu-id="0306f-152">Consulte o guia de toocompanion para orientações técnicas detalhadas sobre Olá recomendado a opção para proteger [SQL camadas](site-recovery-sql.md).</span><span class="sxs-lookup"><span data-stu-id="0306f-152">Please refer toocompanion guide  for detailed technical guidance on hello recommended option for protecting [SQL tier](site-recovery-sql.md).</span></span>

### <a name="3-enable-protection-for-dynamics-ax-client-and-aos-vms"></a><span data-ttu-id="0306f-153">3. Habilitar a proteção do cliente Dynamics AX e VMs AOS</span><span class="sxs-lookup"><span data-stu-id="0306f-153">3. Enable protection for Dynamics AX client and AOS VMs</span></span>
<span data-ttu-id="0306f-154">Execute a configuração do Azure Site Recovery relevante com base em Olá VMs implantadas em [Hyper-V](site-recovery-hyper-v-site-to-azure.md) ou na [VMware](site-recovery-vmware-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="0306f-154">Perform relevant Azure Site Recovery configuration based on whether hello VMs are deployed on [Hyper-V](site-recovery-hyper-v-site-to-azure.md) or on [VMware](site-recovery-vmware-to-azure.md).</span></span>

> [!TIP]
> <span data-ttu-id="0306f-155">Tooconfigure de frequência consistente de falha recomendado é de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="0306f-155">Recommended Crash consistent frequency tooconfigure is 15 minutes.</span></span>
>

<span data-ttu-id="0306f-156">Olá abaixo instantâneo mostra o status de proteção de saudação de VMs de componente do Dynamics no cenário de proteção 'TooAzure de site VMware'.</span><span class="sxs-lookup"><span data-stu-id="0306f-156">hello below snapshot shows hello protection status of Dynamics component VMs in ‘VMware site tooAzure’ protection scenario.</span></span>
<span data-ttu-id="0306f-157">![Itens protegidos ](./media/site-recovery-dynamics-ax/protecteditems.png)</span><span class="sxs-lookup"><span data-stu-id="0306f-157">![Protected items ](./media/site-recovery-dynamics-ax/protecteditems.png)</span></span>

### <a name="4-configure-networking"></a><span data-ttu-id="0306f-158">4. Configurar Rede</span><span class="sxs-lookup"><span data-stu-id="0306f-158">4. Configure Networking</span></span>
<span data-ttu-id="0306f-159">Definir as Configurações de Rede e de Computação de VM</span><span class="sxs-lookup"><span data-stu-id="0306f-159">Configure VM Compute and Network Settings</span></span>

<span data-ttu-id="0306f-160">Olá AX e do cliente AOS VMs definir configurações de rede no Azure Site Recovery para que redes VM Olá toohello anexado à direita DR rede após o failover.</span><span class="sxs-lookup"><span data-stu-id="0306f-160">For hello AX client and AOS VMs configure network settings in Azure Site Recovery so that hello VM networks get attached toohello right DR network after failover.</span></span> <span data-ttu-id="0306f-161">Certifique-se de rede de DR Olá para essas camadas é roteável toohello SQL camadas.</span><span class="sxs-lookup"><span data-stu-id="0306f-161">Ensure hello DR network for these tiers is routable toohello SQL tier.</span></span>

<span data-ttu-id="0306f-162">Você pode selecionar Olá VM em Olá replicadas configurações de rede itens tooconfigure Olá conforme mostrado no instantâneo de saudação abaixo.</span><span class="sxs-lookup"><span data-stu-id="0306f-162">You can select hello VM in hello replicated items tooconfigure hello network settings as shown in hello snapshot below.</span></span>

* <span data-ttu-id="0306f-163">Para servidores do AOS selecione conjunto de disponibilidade correto de saudação.</span><span class="sxs-lookup"><span data-stu-id="0306f-163">For AOS servers select hello correct availability set.</span></span>

* <span data-ttu-id="0306f-164">Se você estiver usando um endereço IP estático, especifique Olá IP que você deseja Olá tootake de máquina virtual em Olá **IP de destino** campo ![as configurações de rede](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span><span class="sxs-lookup"><span data-stu-id="0306f-164">If you are using a static IP then specify hello IP that you want hello virtual machine tootake in hello **Target IP** field ![Network Settings ](./media/site-recovery-dynamics-ax/vmpropertiesaos1.png)</span></span>



### <a name="5-creating-a-recovery-plan"></a><span data-ttu-id="0306f-165">5. Criar um plano de recuperação</span><span class="sxs-lookup"><span data-stu-id="0306f-165">5. Creating a recovery plan</span></span>

<span data-ttu-id="0306f-166">Você pode criar um plano de recuperação no processo de failover do Azure Site Recovery tooautomate hello.</span><span class="sxs-lookup"><span data-stu-id="0306f-166">You can create a recovery plan in Azure Site Recovery tooautomate hello failover process.</span></span> <span data-ttu-id="0306f-167">Adicione camada de aplicativo e a camada da web em Olá plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="0306f-167">Add app tier and web tier in hello Recovery Plan.</span></span> <span data-ttu-id="0306f-168">Ordene-as em diferentes grupos de forma que Olá front-end desligamento antes da camada de aplicativo.</span><span class="sxs-lookup"><span data-stu-id="0306f-168">Order them in different groups so that hello front-end shutdown before app tier.</span></span>

1)  <span data-ttu-id="0306f-169">Selecione o cofre do Azure Site Recovery Olá em sua assinatura e clique no bloco 'Planos de recuperação'.</span><span class="sxs-lookup"><span data-stu-id="0306f-169">Select hello Azure Site Recovery vault in your subscription and click on ‘Recovery Plans’ tile.</span></span>

2)  <span data-ttu-id="0306f-170">Clique em '+ Plano de recuperação' e especifique um nome.</span><span class="sxs-lookup"><span data-stu-id="0306f-170">Click on ‘+ Recovery plan and specify a name.</span></span>

3)  <span data-ttu-id="0306f-171">Selecione hello 'Fonte' e 'Target'.</span><span class="sxs-lookup"><span data-stu-id="0306f-171">Select hello ‘Source’ and ‘Target’.</span></span> <span data-ttu-id="0306f-172">destino de saudação pode ser o site do Azure ou secundário.</span><span class="sxs-lookup"><span data-stu-id="0306f-172">hello target can be Azure or secondary site.</span></span> <span data-ttu-id="0306f-173">Caso escolha do Azure, você deve especificar o modelo de implantação de saudação</span><span class="sxs-lookup"><span data-stu-id="0306f-173">In case you choose Azure, you must specify hello deployment model</span></span>

![Criar Plano de Recuperação](./media/site-recovery-dynamics-ax/recoveryplancreation1.png)

4)  <span data-ttu-id="0306f-175">Selecione Olá AOS e um plano de recuperação do cliente VMs toohello e clique em ✓.</span><span class="sxs-lookup"><span data-stu-id="0306f-175">Select hello AOS and client VMs toohello recovery plan and click ✓.</span></span>
<span data-ttu-id="0306f-176">![Criar Plano de Recuperação](./media/site-recovery-dynamics-ax/selectvms.png)</span><span class="sxs-lookup"><span data-stu-id="0306f-176">![Create Recovery Plan](./media/site-recovery-dynamics-ax/selectvms.png)</span></span>


![Plano de Recuperação](./media/site-recovery-dynamics-ax/recoveryplan.png)

<span data-ttu-id="0306f-178">Você pode personalizar o plano de recuperação de saudação para o aplicativo Dynamics AX adicionando várias etapas, conforme detalhado abaixo.</span><span class="sxs-lookup"><span data-stu-id="0306f-178">You can customize hello recovery plan for Dynamics AX application by adding various steps as detailed below.</span></span> <span data-ttu-id="0306f-179">Olá acima instantâneo mostra Olá plano de recuperação completo depois de adicionar todas as etapas de saudação.</span><span class="sxs-lookup"><span data-stu-id="0306f-179">hello above snapshot shows hello complete recovery plan after adding all hello steps.</span></span>

<span data-ttu-id="0306f-180">*Etapas:*</span><span class="sxs-lookup"><span data-stu-id="0306f-180">*Steps:*</span></span>

<span data-ttu-id="0306f-181">*1. Etapas de failover do SQL Server*</span><span class="sxs-lookup"><span data-stu-id="0306f-181">*1. SQL Server fail over steps*</span></span>

<span data-ttu-id="0306f-182">Consulte também['Solução de recuperação de desastres do SQL Server'](site-recovery-sql.md) guia complementar para obter detalhes sobre o servidor de tooSQL específica de etapas de recuperação.</span><span class="sxs-lookup"><span data-stu-id="0306f-182">Refer too[‘SQL Server DR Solution’](site-recovery-sql.md) companion guide  for details about recovery steps specific tooSQL server.</span></span>

<span data-ttu-id="0306f-183">*2. Failover de grupo 1: Failover Olá AOS VMs*</span><span class="sxs-lookup"><span data-stu-id="0306f-183">*2. Failover Group 1: Fail over hello AOS VMs*</span></span>

<span data-ttu-id="0306f-184">Certifique-se de que o ponto de recuperação de saudação selecionado é mais próximo possível toohello banco de dados PIT mas não em frente.</span><span class="sxs-lookup"><span data-stu-id="0306f-184">Make sure that hello recovery point selected is as close as possible toohello database PIT but not ahead.</span></span>

<span data-ttu-id="0306f-185">*3. Script: Balanceador de carga adicionar (somente E-A)* adicionar um script (por meio da automação do Azure) depois do grupo AOS VM surge tooadd um tooit de Balanceador de carga.</span><span class="sxs-lookup"><span data-stu-id="0306f-185">*3. Script: Add load balancer (Only E-A)* Add a script (via Azure automation) after AOS VM group comes up tooadd a load balancer tooit.</span></span> <span data-ttu-id="0306f-186">Você pode usar um script toodo essa tarefa.</span><span class="sxs-lookup"><span data-stu-id="0306f-186">You can use a script toodo this task.</span></span> <span data-ttu-id="0306f-187">Consulte o artigo [como tooadd balanceador de carga de aplicativo multicamadas DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span><span class="sxs-lookup"><span data-stu-id="0306f-187">Refer article [how tooadd load balancer for multi-tier application DR](https://azure.microsoft.com/blog/cloud-migration-and-disaster-recovery-of-load-balanced-multi-tier-applications-using-azure-site-recovery/)</span></span>

<span data-ttu-id="0306f-188">*4. Failover de grupo 2: Failover de cliente do AX Olá VMs.*</span><span class="sxs-lookup"><span data-stu-id="0306f-188">*4. Failover Group 2: Fail over hello AX client VMs.*</span></span>
<span data-ttu-id="0306f-189">Failover Olá web da camada de máquinas virtuais como parte do plano de recuperação de saudação.</span><span class="sxs-lookup"><span data-stu-id="0306f-189">Fail over hello web tier VMs as part of hello recovery plan.</span></span>


### <a name="doing-a-test-failover"></a><span data-ttu-id="0306f-190">Executar um failover de teste</span><span class="sxs-lookup"><span data-stu-id="0306f-190">Doing a test failover</span></span>

<span data-ttu-id="0306f-191">Consulte too'AD DR Solution ' e 'Solução de recuperação de desastres do SQL Server' os guias complementares para tooAD específicas de considerações e o SQL server respectivamente durante o Failover de teste.</span><span class="sxs-lookup"><span data-stu-id="0306f-191">Refer too‘AD DR Solution ’ and ‘SQL Server DR solution ’ companion guides for considerations specific tooAD and SQL server respectively during Test Failover.</span></span>

1.  <span data-ttu-id="0306f-192">Vá tooAzure portal e selecione seu Cofre de recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="0306f-192">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="0306f-193">Clique no plano de recuperação de saudação criado do Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="0306f-193">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="0306f-194">Clique em 'Failover de Teste'.</span><span class="sxs-lookup"><span data-stu-id="0306f-194">Click on ‘Test Failover’.</span></span>
4.  <span data-ttu-id="0306f-195">Selecione o processo de failover de teste Olá Olá rede virtual toostart.</span><span class="sxs-lookup"><span data-stu-id="0306f-195">Select hello virtual network toostart hello test fail-over process.</span></span>
5.  <span data-ttu-id="0306f-196">Após ambiente secundário hello, você pode executar a validação.</span><span class="sxs-lookup"><span data-stu-id="0306f-196">Once hello secondary environment is up, you can perform your validations.</span></span>
6.  <span data-ttu-id="0306f-197">Depois que as validações de saudação estiverem concluídas, você pode selecionar 'Validações Concluir' e ambiente de failover de teste hello serão limpos.</span><span class="sxs-lookup"><span data-stu-id="0306f-197">Once hello validations are complete, you can select ‘Validations complete’ and hello test failover environment will be cleaned.</span></span>

<span data-ttu-id="0306f-198">Execute [neste guia](site-recovery-test-failover-to-azure.md) toodo um failover de teste.</span><span class="sxs-lookup"><span data-stu-id="0306f-198">Follow [this guidance](site-recovery-test-failover-to-azure.md) toodo a test failover.</span></span>

### <a name="doing-a-failover"></a><span data-ttu-id="0306f-199">Executar um failover</span><span class="sxs-lookup"><span data-stu-id="0306f-199">Doing a failover</span></span>

1.  <span data-ttu-id="0306f-200">Vá tooAzure portal e selecione seu Cofre de recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="0306f-200">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="0306f-201">Clique no plano de recuperação de saudação criado do Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="0306f-201">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="0306f-202">Clique em 'Failover' e selecione 'Failover'.</span><span class="sxs-lookup"><span data-stu-id="0306f-202">Click on ‘Failover’ and select ‘ Failover’.</span></span>
4.  <span data-ttu-id="0306f-203">Selecione a rede de destino hello e clique em processo de failover do ✓ toostart hello.</span><span class="sxs-lookup"><span data-stu-id="0306f-203">Select hello target network and click ✓ toostart hello failover process.</span></span>

<span data-ttu-id="0306f-204">Siga [este guia](site-recovery-failover.md) quando estiver realizando um failover.</span><span class="sxs-lookup"><span data-stu-id="0306f-204">Follow [this guidance](site-recovery-failover.md) when you are doing a failover.</span></span>

### <a name="perform-a-failback"></a><span data-ttu-id="0306f-205">Executar um Failback</span><span class="sxs-lookup"><span data-stu-id="0306f-205">Perform a Failback</span></span>

<span data-ttu-id="0306f-206">Consulte too'SQL solução de recuperação de desastres do servidor ' guia complementar para o servidor de tooSQL específicas de considerações durante o Failback.</span><span class="sxs-lookup"><span data-stu-id="0306f-206">Refer too‘SQL Server DR Solution ’ companion guide for considerations specific tooSQL server during Failback.</span></span>

1.  <span data-ttu-id="0306f-207">Vá tooAzure portal e selecione seu Cofre de recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="0306f-207">Go tooAzure  portal and select your Site Recovery vault.</span></span>
2.  <span data-ttu-id="0306f-208">Clique no plano de recuperação de saudação criado do Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="0306f-208">Click on hello recovery plan created for Dynamics AX.</span></span>
3.  <span data-ttu-id="0306f-209">Clique em 'Failover' e selecione o failover.</span><span class="sxs-lookup"><span data-stu-id="0306f-209">Click on ‘Failover’ and select failover.</span></span>
4.  <span data-ttu-id="0306f-210">Clique em 'Alterar Direção'.</span><span class="sxs-lookup"><span data-stu-id="0306f-210">Click on ‘Change Direction’.</span></span>
5.  <span data-ttu-id="0306f-211">Selecionar opções apropriadas Olá - sincronização de dados e opções de criação de VM</span><span class="sxs-lookup"><span data-stu-id="0306f-211">Select hello appropriate options - data synchronization and VM creation options</span></span>
6.  <span data-ttu-id="0306f-212">Clique em ✓ toostart Olá '' Failback' processo.</span><span class="sxs-lookup"><span data-stu-id="0306f-212">Click ✓ toostart hello ‘Failback’ process.</span></span>


<span data-ttu-id="0306f-213">Siga [estas diretrizes](site-recovery-failback-azure-to-vmware.md) quando estiver realizando um failback.</span><span class="sxs-lookup"><span data-stu-id="0306f-213">Follow [this guidance](site-recovery-failback-azure-to-vmware.md) when you are doing a failback.</span></span>

##<a name="summary"></a><span data-ttu-id="0306f-214">Resumo</span><span class="sxs-lookup"><span data-stu-id="0306f-214">Summary</span></span>
<span data-ttu-id="0306f-215">Com o Azure Site Recovery, você pode criar um plano totalmente automatizado de recuperação de desastre para seu aplicativo do Dynamics AX.</span><span class="sxs-lookup"><span data-stu-id="0306f-215">Using Azure Site Recovery, you can create a complete automated disaster recovery plan for your Dynamics AX application.</span></span> <span data-ttu-id="0306f-216">Você pode iniciar failover hello dentro de segundos de qualquer lugar no hello evento de interrupção e obter o aplicativo hello em funcionamento em minutos.</span><span class="sxs-lookup"><span data-stu-id="0306f-216">You can initiate hello failover within seconds from anywhere in hello event of a disruption and get hello application up and running in minutes.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0306f-217">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0306f-217">Next steps</span></span>
<span data-ttu-id="0306f-218">Leitura [que cargas de trabalho posso proteger?](site-recovery-workload.md) toolearn mais sobre como proteger as cargas de trabalho com o Azure Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="0306f-218">Read [What workloads can I protect?](site-recovery-workload.md) toolearn more about protecting enterprise workloads with Azure Site Recovery.</span></span>
