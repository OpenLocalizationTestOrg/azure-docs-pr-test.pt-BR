---
title: "Replicar máquinas virtuais do Azure entre regiões do Azure para necessidades de recuperação de desastres: tooAzure do Azure | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooreplicate Azure VMs entre regiões do Azure (Azure para Azure) com o serviço do Azure Site Recovery Olá para necessidades de recuperação de desastres."
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmon
editor: 
ms.assetid: dab98aa5-9c41-4475-b7dc-2e07ab1cfd18
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/10/2017
ms.author: raynew
ms.openlocfilehash: c4c425af260a9bcc3dd4dcc13da26109e20f03bb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="5966a-103">Você pode replicar VMs do Azure entre regiões usando o Site Recovery</span><span class="sxs-lookup"><span data-stu-id="5966a-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="5966a-104">A replicação do Azure Site Recovery para as máquinas virtuais (VMs) do Azure está atualmente na versão prévia.</span><span class="sxs-lookup"><span data-stu-id="5966a-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="5966a-105">Este artigo descreve como tooreplicate VMs do Azure entre regiões do Azure usando Olá [recuperação de Site](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5966a-105">This article describes how tooreplicate Azure VMs between Azure regions by using hello [Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="5966a-106">Postar perguntas e comentários na parte inferior da saudação deste artigo ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="5966a-106">Post comments and questions at hello bottom of this article or on hello [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="5966a-107">Recuperação de desastre no Azure</span><span class="sxs-lookup"><span data-stu-id="5966a-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="5966a-108">Recursos internos de infraestrutura do Azure contribuem tooa estratégia de disponibilidade robusta e flexível para cargas de trabalho que são executados em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="5966a-108">Built-in Azure infrastructure capabilities and features contribute tooa robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="5966a-109">No entanto, há muitos motivos para você usar tooplan para recuperação de desastres entre regiões do Azure por conta própria:</span><span class="sxs-lookup"><span data-stu-id="5966a-109">However, there are many reasons why you need tooplan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="5966a-110">Você precisa toomeet diretrizes de conformidade para cargas de trabalho que exigem uma estratégia de recuperação (BCDR) de desastres e continuidade dos negócios e aplicativos específicos.</span><span class="sxs-lookup"><span data-stu-id="5966a-110">You need toomeet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="5966a-111">Você deseja Olá capacidade tooprotect e recupere máquinas virtuais do Azure com base em suas decisões de negócios e não apenas com base na funcionalidade do Azure embutida.</span><span class="sxs-lookup"><span data-stu-id="5966a-111">You want hello ability tooprotect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="5966a-112">É necessário tootest failover e recuperação de acordo com suas necessidades de negócios e de conformidade, sem afetar a produção.</span><span class="sxs-lookup"><span data-stu-id="5966a-112">You need tootest failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="5966a-113">Você precisa toofail toohello região de recuperação em caso de saudação de um desastre e falha a região de origem original toohello back perfeitamente.</span><span class="sxs-lookup"><span data-stu-id="5966a-113">You need toofail over toohello recovery region in hello event of a disaster and fail back toohello original source region seamlessly.</span></span>

<span data-ttu-id="5966a-114">Usar o Site Recovery para a VM do Azure para o Azure replicação toohelp você fazer todas essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="5966a-114">Use Site Recovery for Azure-to-Azure VM replication toohelp you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="5966a-115">Por que usar a Recuperação de Site?</span><span class="sxs-lookup"><span data-stu-id="5966a-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="5966a-116">Recuperação de site fornece uma maneira simples de tooreplicate VMs do Azure entre regiões:</span><span class="sxs-lookup"><span data-stu-id="5966a-116">Site Recovery provides a simple way tooreplicate Azure VMs between regions:</span></span>

- <span data-ttu-id="5966a-117">**Implantação automática**.</span><span class="sxs-lookup"><span data-stu-id="5966a-117">**Automatic deployment**.</span></span> <span data-ttu-id="5966a-118">Ao contrário de um modelo de replicação ativa, não é necessário para uma infraestrutura caro e complexo na região secundária hello.</span><span class="sxs-lookup"><span data-stu-id="5966a-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in hello secondary region.</span></span> <span data-ttu-id="5966a-119">Quando você habilitar a replicação, recuperação de Site cria automaticamente recursos Olá necessários na região de destino hello, com base nas configurações de região de origem.</span><span class="sxs-lookup"><span data-stu-id="5966a-119">When you enable replication, Site Recovery automatically creates hello required resources in hello target region, based on source region settings.</span></span>
- <span data-ttu-id="5966a-120">**Controlar regiões**.</span><span class="sxs-lookup"><span data-stu-id="5966a-120">**Control regions**.</span></span> <span data-ttu-id="5966a-121">Recuperação de Site, é possível replicar qualquer região tooany região dentro de um continente.</span><span class="sxs-lookup"><span data-stu-id="5966a-121">With Site Recovery, you can replicate from any region tooany region within a continent.</span></span> <span data-ttu-id="5966a-122">Compare isso com o armazenamento com redundância geográfica com acesso de leitura, que replica de forma assíncrona entre apenas o padrão de [regiões emparelhadas](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).</span><span class="sxs-lookup"><span data-stu-id="5966a-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="5966a-123">Armazenamento com redundância geográfica com acesso de leitura fornece dados de toohello de acesso somente leitura na região de destino hello.</span><span class="sxs-lookup"><span data-stu-id="5966a-123">Read-access geo-redundant storage provides read-only access toohello data in hello target region.</span></span>
- <span data-ttu-id="5966a-124">**A replicação automatizada**.</span><span class="sxs-lookup"><span data-stu-id="5966a-124">**Automated replication**.</span></span> <span data-ttu-id="5966a-125">Recuperação de site fornece replicação contínua automatizada.</span><span class="sxs-lookup"><span data-stu-id="5966a-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="5966a-126">Failover e failback podem ser disparados com um único clique.</span><span class="sxs-lookup"><span data-stu-id="5966a-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="5966a-127">**RTO e RPO**.</span><span class="sxs-lookup"><span data-stu-id="5966a-127">**RTO and RPO**.</span></span> <span data-ttu-id="5966a-128">Recuperação de site aproveita hello Azure da infraestrutura de rede que conecta regiões tookeep RTO e RPO muito baixo.</span><span class="sxs-lookup"><span data-stu-id="5966a-128">Site Recovery takes advantage of hello Azure network infrastructure that connects regions tookeep RTO and RPO very low.</span></span>
- <span data-ttu-id="5966a-129">**Testando**.</span><span class="sxs-lookup"><span data-stu-id="5966a-129">**Testing**.</span></span> <span data-ttu-id="5966a-130">Você pode executar os exercícios de recuperação de desastres com failovers de teste sob demanda, conforme a necessidade, sem afetar a cargas de trabalho de produção ou de replicação contínua.</span><span class="sxs-lookup"><span data-stu-id="5966a-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="5966a-131">**Planos de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="5966a-131">**Recovery plans**.</span></span> <span data-ttu-id="5966a-132">Você pode usar planos de recuperação tooorchestrate failover e failback de todo o aplicativo hello em execução em várias VMs.</span><span class="sxs-lookup"><span data-stu-id="5966a-132">You can use recovery plans tooorchestrate failover and failback of hello entire application running on multiple VMs.</span></span> <span data-ttu-id="5966a-133">recurso de plano de recuperação de saudação tem integração avançada de primeira classe com runbooks de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="5966a-133">hello recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="5966a-134">Resumo da implantação</span><span class="sxs-lookup"><span data-stu-id="5966a-134">Deployment summary</span></span>

<span data-ttu-id="5966a-135">Aqui está um resumo do que você precisa tooset toodo a replicação de máquinas virtuais entre regiões do Azure:</span><span class="sxs-lookup"><span data-stu-id="5966a-135">Here's a summary of what you need toodo tooset up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="5966a-136">Crie um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="5966a-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="5966a-137">cofre Olá contém definições de configuração e coordena a replicação.</span><span class="sxs-lookup"><span data-stu-id="5966a-137">hello vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="5966a-138">Habilite a replicação para Olá VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="5966a-138">Enable replication for hello Azure VMs.</span></span>
3. <span data-ttu-id="5966a-139">Execute um toomake de failover de teste se tudo está funcionando conforme o esperado.</span><span class="sxs-lookup"><span data-stu-id="5966a-139">Run a test failover toomake sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="5966a-140">Você pode verificar Olá [matriz de suporte para replicação de VM do Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="5966a-140">You can check hello [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="5966a-141">Para obter informações sobre como tooconfigure Olá necessária conectividade de saída de rede para máquinas virtuais do Azure para replicação de recuperação de Site, consulte Olá [documento de diretrizes de rede](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="5966a-141">For information on how tooconfigure hello required network outbound connectivity for Azure VMs for Site Recovery replication, see hello [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="5966a-142">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="5966a-142">Before you start</span></span>

* <span data-ttu-id="5966a-143">Sua conta de usuário do Azure precisa toohave determinados [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="5966a-143">Your Azure user account needs toohave certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="5966a-144">Sua assinatura do Azure deve ser habilitado toocreate VMs no local de destino Olá que você deseja toouse como a região de recuperação de desastres de saudação.</span><span class="sxs-lookup"><span data-stu-id="5966a-144">Your Azure subscription should be enabled toocreate VMs in hello target location that you want toouse as hello disaster recovery region.</span></span> <span data-ttu-id="5966a-145">Contate o suporte tooenable Olá cota necessária.</span><span class="sxs-lookup"><span data-stu-id="5966a-145">Contact support tooenable hello required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="5966a-146">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="5966a-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="5966a-147">É recomendável que você crie Olá Cofre de serviços de recuperação no local de saudação onde você deseja que seu tooreplicate VMs.</span><span class="sxs-lookup"><span data-stu-id="5966a-147">We recommend that you create hello Recovery Services vault in hello location where you want your VMs tooreplicate.</span></span> <span data-ttu-id="5966a-148">Por exemplo, se o local de destino é hello central nos, criar hello cofre no **centro dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="5966a-148">For example, if your target location is hello central US, create hello vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="5966a-149">Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="5966a-149">Enable replication</span></span>

<span data-ttu-id="5966a-150">Em **os cofres de serviços de recuperação**, clique em nome do cofre hello.</span><span class="sxs-lookup"><span data-stu-id="5966a-150">In **Recovery Services vaults**, click hello vault name.</span></span> <span data-ttu-id="5966a-151">No cofre hello, clique em Olá **+ replicar** botão.</span><span class="sxs-lookup"><span data-stu-id="5966a-151">In hello vault, click hello **+Replicate** button.</span></span>

### <a name="step-1-configure-hello-source"></a><span data-ttu-id="5966a-152">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="5966a-152">Step 1.</span></span> <span data-ttu-id="5966a-153">Configurar fonte Olá</span><span class="sxs-lookup"><span data-stu-id="5966a-153">Configure hello source</span></span>
1. <span data-ttu-id="5966a-154">Em **fonte**, selecione **Azure - VISUALIZAÇÃO**.</span><span class="sxs-lookup"><span data-stu-id="5966a-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="5966a-155">Em **local de origem**, selecione origem Olá região do Azure em que suas VMs estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="5966a-155">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="5966a-156">Modelo de implantação de saudação Select das suas máquinas virtuais: **Gerenciador de recursos de** ou **clássico**.</span><span class="sxs-lookup"><span data-stu-id="5966a-156">Select hello deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="5966a-157">Selecione Olá **grupo de recursos de origem** para máquinas virtuais do Gerenciador de recursos ou **serviço de nuvem** para VMs clássicas.</span><span class="sxs-lookup"><span data-stu-id="5966a-157">Select hello **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Configurar fonte Olá](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="5966a-159">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="5966a-159">Step 2.</span></span> <span data-ttu-id="5966a-160">Selecionar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="5966a-160">Select virtual machines</span></span>

* <span data-ttu-id="5966a-161">Selecione Olá VMs você deseja tooreplicate e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="5966a-161">Select hello VMs you want tooreplicate, and then click **OK**.</span></span>

    ![Selecione as máquinas virtuais](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="5966a-163">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="5966a-163">Step 3.</span></span> <span data-ttu-id="5966a-164">Configurar definições</span><span class="sxs-lookup"><span data-stu-id="5966a-164">Configure settings</span></span>

1. <span data-ttu-id="5966a-165">padrão de saudação toooverride configurações de destino e especifique as configurações de saudação de sua escolha, clique em **personalizar**.</span><span class="sxs-lookup"><span data-stu-id="5966a-165">toooverride hello default target settings and specify hello settings of your choice, click **Customize**.</span></span> <span data-ttu-id="5966a-166">Para obter mais informações, consulte [Personalizar recursos de destino](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span><span class="sxs-lookup"><span data-stu-id="5966a-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Configurar definições](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="5966a-168">Por padrão, a recuperação de Site cria uma política de replicação que usa instantâneos consistentes com o aplicativo a cada 4 horas e retém pontos de recuperação por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="5966a-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="5966a-169">toocreate uma política com configurações diferentes, clique em **personalizar** Avançar muito**política de replicação**.</span><span class="sxs-lookup"><span data-stu-id="5966a-169">toocreate a policy with different settings, click **Customize** next too**Replication Policy**.</span></span>

    ![Personalizar política](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="5966a-171">provisionar recursos de destino de saudação toostart, clique em **criar recursos de destino**.</span><span class="sxs-lookup"><span data-stu-id="5966a-171">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="5966a-172">O provisionamento demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="5966a-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="5966a-173">Não feche a folha de saudação durante o provisionamento ou precisar de toostart.</span><span class="sxs-lookup"><span data-stu-id="5966a-173">Don't close hello blade during provisioning, or you need toostart over.</span></span>

4. <span data-ttu-id="5966a-174">replicação de tootrigger de saudação selecionada de VM, clique em **habilitar replicação**.</span><span class="sxs-lookup"><span data-stu-id="5966a-174">tootrigger replication of hello selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="5966a-175">Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **configurações** > **trabalhos** > **trabalhos de recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="5966a-175">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="5966a-176">Em **configurações** > **itens replicados**, você pode exibir o status de saudação de VMs e Olá andamento da replicação inicial.</span><span class="sxs-lookup"><span data-stu-id="5966a-176">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="5966a-177">Clique em Olá VM toodrill abaixo em suas configurações.</span><span class="sxs-lookup"><span data-stu-id="5966a-177">Click hello VM toodrill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="5966a-178">Execute um teste de failover</span><span class="sxs-lookup"><span data-stu-id="5966a-178">Run a test failover</span></span>

<span data-ttu-id="5966a-179">Depois de configurar tudo, execute um toomake de failover de teste se que tudo está funcionando conforme o esperado:</span><span class="sxs-lookup"><span data-stu-id="5966a-179">After you set up everything, run a test failover toomake sure everything's working as expected:</span></span>

1. <span data-ttu-id="5966a-180">toofail em um único computador, em **configurações** > **itens duplicados**, clique em Olá VM **+ Failover de teste** ícone.</span><span class="sxs-lookup"><span data-stu-id="5966a-180">toofail over a single machine, in **Settings** > **Replicated Items**, click hello VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="5966a-181">Planejar toofail sobre a recuperação, em **configurações** > **planos de recuperação**, plano de saudação do botão direito do mouse **Failover de teste**.</span><span class="sxs-lookup"><span data-stu-id="5966a-181">toofail over a recovery plan, in **Settings** > **Recovery Plans**, right-click hello plan **Test Failover**.</span></span> <span data-ttu-id="5966a-182">um plano de recuperação de toocreate [, siga estas instruções](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="5966a-182">toocreate a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="5966a-183">Em **Failover de teste**, selecione toowhich de rede virtual do Azure de destino Olá VMs do Azure conectadas após o failover de saudação.</span><span class="sxs-lookup"><span data-stu-id="5966a-183">In **Test Failover**, select hello target Azure virtual network toowhich Azure VMs are connected after hello failover occurs.</span></span>

4. <span data-ttu-id="5966a-184">toostart Olá failover, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="5966a-184">toostart hello failover, click **OK**.</span></span> <span data-ttu-id="5966a-185">tootrack de andamento, clique em Olá VM tooopen suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="5966a-185">tootrack progress, click hello VM tooopen its properties.</span></span> <span data-ttu-id="5966a-186">Ou você pode clicar em Olá **Failover de teste** trabalho em nome do cofre hello > **configurações** > **trabalhos** > **ostrabalhosderecuperaçãodeSite**.</span><span class="sxs-lookup"><span data-stu-id="5966a-186">Or you can click hello **Test Failover** job in hello vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="5966a-187">Depois de saudação failover for concluído, réplica Olá máquina do Azure aparece no portal do Azure de saudação > **máquinas virtuais**.</span><span class="sxs-lookup"><span data-stu-id="5966a-187">After hello failover finishes, hello replica Azure machine appears in hello Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="5966a-188">Certifique-se de que Olá VM é o tamanho apropriado hello, que tenha se conectado toohello apropriado, e rede que está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="5966a-188">Make sure that hello VM is hello appropriate size, that it's connected toohello appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="5966a-189">Olá toodelete VMs que foram criados durante a saudação failover de teste, clique em **failover de teste de limpeza** em Olá replicadas item ou hello plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="5966a-189">toodelete hello VMs that were created during hello test failover, click **Cleanup test failover** on hello replicated item or hello recovery plan.</span></span> <span data-ttu-id="5966a-190">Em **notas**, gravar e salvar todas as observações associadas Olá failover de teste.</span><span class="sxs-lookup"><span data-stu-id="5966a-190">In **Notes**, record and save any observations associated with hello test failover.</span></span> 

<span data-ttu-id="5966a-191">[Saiba mais](site-recovery-test-failover-to-azure.md) sobre failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="5966a-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="5966a-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5966a-192">Next steps</span></span>

<span data-ttu-id="5966a-193">Depois de testar a implantação de saudação:</span><span class="sxs-lookup"><span data-stu-id="5966a-193">After you test hello deployment:</span></span>

- <span data-ttu-id="5966a-194">[Saiba mais](site-recovery-failover.md) sobre os diferentes tipos de failovers e como toorun-los.</span><span class="sxs-lookup"><span data-stu-id="5966a-194">[Learn more](site-recovery-failover.md) about different types of failovers and how toorun them.</span></span>
- <span data-ttu-id="5966a-195">Saiba mais sobre [usando planos de recuperação](site-recovery-create-recovery-plans.md) tooreduce RTO.</span><span class="sxs-lookup"><span data-stu-id="5966a-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) tooreduce RTO.</span></span>
