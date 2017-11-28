---
title: "Replicar máquinas virtuais do Azure entre regiões do Azure para necessidades de recuperação de desastres: do Azure para o Azure | Microsoft Docs"
description: "Resume as etapas que você precisa para replicar máquinas virtuais do Azure entre regiões do Azure (Azure para Azure) com o serviço do Azure Site Recovery para necessidades de recuperação de desastres."
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
ms.openlocfilehash: 9ca33057f6030fdcc233f6053fdc392d62f8f9f4
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replicate-azure-vms-between-regions-with-azure-site-recovery"></a><span data-ttu-id="2fd3b-103">Você pode replicar VMs do Azure entre regiões usando o Site Recovery</span><span class="sxs-lookup"><span data-stu-id="2fd3b-103">Replicate Azure VMs between regions with Azure Site Recovery</span></span>

>[!NOTE]
>
> <span data-ttu-id="2fd3b-104">Replicação de recuperação de site para máquinas virtuais (VMs) do Azure está atualmente em visualização.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-104">Azure Site Recovery replication for Azure virtual machines (VMs) is currently in preview.</span></span>

<span data-ttu-id="2fd3b-105">Este artigo descreve como replicar computadores físicos locais para o Azure usando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-105">This article describes how to replicate Azure VMs between Azure regions by using the [Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="2fd3b-106">Publique perguntas e comentários na parte inferior deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="2fd3b-106">Post comments and questions at the bottom of this article or on the [Azure Recovery Services forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>

## <a name="disaster-recovery-in-azure"></a><span data-ttu-id="2fd3b-107">Recuperação de desastre no Azure</span><span class="sxs-lookup"><span data-stu-id="2fd3b-107">Disaster recovery in Azure</span></span>

<span data-ttu-id="2fd3b-108">Recursos internos de infraestrutura do Azure contribuem para uma estratégia de disponibilidade robusta e flexível para cargas de trabalho que são executados em máquinas virtuais do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-108">Built-in Azure infrastructure capabilities and features contribute to a robust and resilient availability strategy for workloads that run on Azure VMs.</span></span> <span data-ttu-id="2fd3b-109">No entanto, há muitas razões por que você precisa para planejar a recuperação de desastres entre regiões do Azure:</span><span class="sxs-lookup"><span data-stu-id="2fd3b-109">However, there are many reasons why you need to plan for disaster recovery between Azure regions yourself:</span></span>

- <span data-ttu-id="2fd3b-110">Você precisa atender às diretrizes de conformidade para cargas de trabalho que exigem uma estratégia de recuperação de desastres (BCDR) e continuidade dos negócios e aplicativos específicos.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-110">You need to meet compliance guidelines for specific apps and workloads that require a business continuity and disaster recovery (BCDR) strategy.</span></span>
- <span data-ttu-id="2fd3b-111">Você quer que a capacidade de proteger e recuperar máquinas virtuais do Azure seja com base em suas decisões de negócios e não apenas com base na funcionalidade do Azure embutido.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-111">You want the ability to protect and recover Azure VMs based on your business decisions, and not only based on inbuilt Azure functionality.</span></span>
- <span data-ttu-id="2fd3b-112">Você precisa testar o failover e recuperação de acordo com suas necessidades de negócios e de conformidade, sem afetar a produção.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-112">You need to test failover and recovery in accordance with your business and compliance needs, with no impact on production.</span></span>
- <span data-ttu-id="2fd3b-113">Você precisa fazer failover para a região de recuperação em caso de desastre e failback diretamente para a região de origem original.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-113">You need to fail over to the recovery region in the event of a disaster and fail back to the original source region seamlessly.</span></span>

<span data-ttu-id="2fd3b-114">Use a recuperação de Site para replicação de VM do Azure para o Azure para ajudá-lo a fazer todas essas tarefas.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-114">Use Site Recovery for Azure-to-Azure VM replication to help you do all these tasks.</span></span>


## <a name="why-use-site-recovery"></a><span data-ttu-id="2fd3b-115">Por que usar a Recuperação de Site?</span><span class="sxs-lookup"><span data-stu-id="2fd3b-115">Why use Site Recovery?</span></span>      

<span data-ttu-id="2fd3b-116">Recuperação de site fornece uma maneira simples para replicar máquinas virtuais do Azure entre regiões:</span><span class="sxs-lookup"><span data-stu-id="2fd3b-116">Site Recovery provides a simple way to replicate Azure VMs between regions:</span></span>

- <span data-ttu-id="2fd3b-117">**Implantação automática**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-117">**Automatic deployment**.</span></span> <span data-ttu-id="2fd3b-118">Ao contrário de um modelo de replicação ativa, não há necessidade para uma infraestrutura cara e complexa na região secundária.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-118">Unlike an active-active replication model, there's no need for an expensive and complex infrastructure in the secondary region.</span></span> <span data-ttu-id="2fd3b-119">Quando você habilitar a replicação, a recuperação de Site cria automaticamente os recursos necessários na região de destino, com base nas configurações de região de origem.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-119">When you enable replication, Site Recovery automatically creates the required resources in the target region, based on source region settings.</span></span>
- <span data-ttu-id="2fd3b-120">**Controlar regiões**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-120">**Control regions**.</span></span> <span data-ttu-id="2fd3b-121">Com a Recuperação de Site, você pode replicar de qualquer região para qualquer região dentro de um continente.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-121">With Site Recovery, you can replicate from any region to any region within a continent.</span></span> <span data-ttu-id="2fd3b-122">Compare isso com o armazenamento com redundância geográfica com acesso de leitura, que replica de forma assíncrona entre apenas o padrão de [regiões emparelhadas](https://docs.microsoft.com/azure/best-practices-availability-paired-regions).</span><span class="sxs-lookup"><span data-stu-id="2fd3b-122">Compare this with read-access geo-redundant storage, which replicates asynchronously between standard [paired regions](https://docs.microsoft.com/azure/best-practices-availability-paired-regions) only.</span></span> <span data-ttu-id="2fd3b-123">Armazenamento com redundância geográfica com acesso de leitura fornece acesso somente de leitura aos dados na região de destino.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-123">Read-access geo-redundant storage provides read-only access to the data in the target region.</span></span>
- <span data-ttu-id="2fd3b-124">**A replicação automatizada**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-124">**Automated replication**.</span></span> <span data-ttu-id="2fd3b-125">Recuperação de site fornece replicação contínua automatizada.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-125">Site Recovery provides automated continuous replication.</span></span> <span data-ttu-id="2fd3b-126">Failover e failback podem ser disparados com um único clique.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-126">Failover and failback can be triggered with a single click.</span></span>
- <span data-ttu-id="2fd3b-127">**RTO e RPO**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-127">**RTO and RPO**.</span></span> <span data-ttu-id="2fd3b-128">Recuperação de site aproveita a infraestrutura de rede do Azure que se conecta a regiões para manter o RTO e RPO muito baixos.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-128">Site Recovery takes advantage of the Azure network infrastructure that connects regions to keep RTO and RPO very low.</span></span>
- <span data-ttu-id="2fd3b-129">**Testando**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-129">**Testing**.</span></span> <span data-ttu-id="2fd3b-130">Você pode executar os exercícios de recuperação de desastres com failovers de teste sob demanda, conforme a necessidade, sem afetar a cargas de trabalho de produção ou de replicação contínua.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-130">You can run disaster-recovery drills with on-demand test failovers, as and when needed, without affecting your production workloads or ongoing replication.</span></span>
- <span data-ttu-id="2fd3b-131">**Planos de recuperação**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-131">**Recovery plans**.</span></span> <span data-ttu-id="2fd3b-132">Você pode usar planos de recuperação para fazer failover e failback de todo o aplicativo em execução em várias VMs.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-132">You can use recovery plans to orchestrate failover and failback of the entire application running on multiple VMs.</span></span> <span data-ttu-id="2fd3b-133">O recurso de plano de recuperação tem integração avançada de primeira classe com runbooks de automação do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-133">The recovery plan feature has rich first-class integration with Azure automation runbooks.</span></span>


## <a name="deployment-summary"></a><span data-ttu-id="2fd3b-134">Resumo da implantação</span><span class="sxs-lookup"><span data-stu-id="2fd3b-134">Deployment summary</span></span>

<span data-ttu-id="2fd3b-135">Aqui está um resumo do que você precisa fazer para configurar a replicação de máquinas virtuais entre regiões do Azure:</span><span class="sxs-lookup"><span data-stu-id="2fd3b-135">Here's a summary of what you need to do to set up replication of VMs between Azure regions:</span></span>

1. <span data-ttu-id="2fd3b-136">Crie um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-136">Create a Recovery Services vault.</span></span> <span data-ttu-id="2fd3b-137">O cofre contém definições de configuração e organiza a replicação.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-137">The vault contains configuration settings and orchestrates replication.</span></span>
2. <span data-ttu-id="2fd3b-138">Habilite a replicação para as VMs do Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-138">Enable replication for the Azure VMs.</span></span>
3. <span data-ttu-id="2fd3b-139">Execute um failover de teste para verificar se tudo está funcionando como esperado.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-139">Run a test failover to make sure that everything's working as expected.</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="2fd3b-140">Você pode verificar a [matriz de suporte para replicação de VM do Azure](./site-recovery-support-matrix-azure-to-azure.md).</span><span class="sxs-lookup"><span data-stu-id="2fd3b-140">You can check the [support matrix for Azure VM replication](./site-recovery-support-matrix-azure-to-azure.md).</span></span>

>[!IMPORTANT]
>
> <span data-ttu-id="2fd3b-141">Para obter informações sobre como configurar a conectividade de saída de rede necessária para VMs do Azure para replicação de recuperação de Site, consulte o [documento de diretrizes de rede](./site-recovery-azure-to-azure-networking-guidance.md).</span><span class="sxs-lookup"><span data-stu-id="2fd3b-141">For information on how to configure the required network outbound connectivity for Azure VMs for Site Recovery replication, see the [networking guidance document](./site-recovery-azure-to-azure-networking-guidance.md).</span></span>

### <a name="before-you-start"></a><span data-ttu-id="2fd3b-142">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="2fd3b-142">Before you start</span></span>

* <span data-ttu-id="2fd3b-143">Sua conta de usuário do Azure precisa ter certas [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) para habilitar a replicação de uma nova máquina virtual para o Azure.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-143">Your Azure user account needs to have certain [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of an Azure virtual machine.</span></span>
* <span data-ttu-id="2fd3b-144">Sua assinatura deve ser habilitada para criar VMs do Azure na região de destino que você planeja usar como a região de recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-144">Your Azure subscription should be enabled to create VMs in the target location that you want to use as the disaster recovery region.</span></span> <span data-ttu-id="2fd3b-145">Contate o suporte para habilitar a cota necessária.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-145">Contact support to enable the required quota.</span></span>

## <a name="create-a-recovery-services-vault"></a><span data-ttu-id="2fd3b-146">Criar um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="2fd3b-146">Create a Recovery Services vault</span></span>

[!INCLUDE [site-recovery-create-vault](../../includes/site-recovery-create-vault.md)]

>[!NOTE]
>
> <span data-ttu-id="2fd3b-147">É recomendável que você crie o cofre de serviços de recuperação no local onde você deseja suas VMs para replicar.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-147">We recommend that you create the Recovery Services vault in the location where you want your VMs to replicate.</span></span> <span data-ttu-id="2fd3b-148">Por exemplo, se o local de destino é centro dos EUA, crie o cofre no **centro dos EUA**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-148">For example, if your target location is the central US, create the vault in **Central US**.</span></span>

## <a name="enable-replication"></a><span data-ttu-id="2fd3b-149">Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="2fd3b-149">Enable replication</span></span>

<span data-ttu-id="2fd3b-150">Em **Cofres dos Serviços de Recuperação**, selecione o cofre.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-150">In **Recovery Services vaults**, click the vault name.</span></span> <span data-ttu-id="2fd3b-151">No cofre, clique no botão **+ replicar**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-151">In the vault, click the **+Replicate** button.</span></span>

### <a name="step-1-configure-the-source"></a><span data-ttu-id="2fd3b-152">Etapa 1.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-152">Step 1.</span></span> <span data-ttu-id="2fd3b-153">Configure a origem</span><span class="sxs-lookup"><span data-stu-id="2fd3b-153">Configure the source</span></span>
1. <span data-ttu-id="2fd3b-154">Em **fonte**, selecione **Azure - VISUALIZAÇÃO**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-154">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="2fd3b-155">Em **Local de origem**, selecione a fonte de região do Azure em que suas VMs estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-155">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="2fd3b-156">Especifique o modelo de implantação a ser usado: **Gerenciador de Recursos** ou **Clássico**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-156">Select the deployment model of your VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="2fd3b-157">Selecione o **Grupo de recursos de origem** para máquinas virtuais do Gerenciador de Recursos ou **serviço de nuvem** para VMs clássicas.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-157">Select the **Source resource group** for Resource Manager VMs or **cloud service** for classic VMs.</span></span>

    ![Configure a origem](./media/site-recovery-azure-to-azure/source.png)

### <a name="step-2-select-virtual-machines"></a><span data-ttu-id="2fd3b-159">Etapa 2.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-159">Step 2.</span></span> <span data-ttu-id="2fd3b-160">Selecionar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="2fd3b-160">Select virtual machines</span></span>

* <span data-ttu-id="2fd3b-161">Selecione as máquinas virtuais que você deseja replicar e, em seguida, clique em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-161">Select the VMs you want to replicate, and then click **OK**.</span></span>

    ![Selecione as máquinas virtuais](./media/site-recovery-azure-to-azure/vms.png)

### <a name="step-3-configure-settings"></a><span data-ttu-id="2fd3b-163">Etapa 3.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-163">Step 3.</span></span> <span data-ttu-id="2fd3b-164">Configurar definições</span><span class="sxs-lookup"><span data-stu-id="2fd3b-164">Configure settings</span></span>

1. <span data-ttu-id="2fd3b-165">Para substituir as configurações padrão de destino e especificar as configurações de sua escolha, clique em **Personalizar**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-165">To override the default target settings and specify the settings of your choice, click **Customize**.</span></span> <span data-ttu-id="2fd3b-166">Para obter mais informações, consulte [Personalizar recursos de destino](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span><span class="sxs-lookup"><span data-stu-id="2fd3b-166">For more information, see [Customize target resources](site-recovery-replicate-azure-to-azure.md##customize-target-resources).</span></span>

    ![Configurar definições](./media/site-recovery-azure-to-azure/settings.png)


2. <span data-ttu-id="2fd3b-168">Por padrão, a recuperação de Site cria uma política de replicação que usa instantâneos consistentes com o aplicativo a cada 4 horas e retém pontos de recuperação por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-168">By default, Site Recovery creates a replication policy that takes app-consistent snapshots every 4 hours and retains recovery points for 24 hours.</span></span> <span data-ttu-id="2fd3b-169">Para criar uma política com configurações diferentes, clique em **Personalizar** lado a **Política de Replicação**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-169">To create a policy with different settings, click **Customize** next to **Replication Policy**.</span></span>

    ![Personalizar política](./media/site-recovery-azure-to-azure/customize-policy.png)

3. <span data-ttu-id="2fd3b-171">Para iniciar o provisionamento de recursos de destino, clique em **Criar recursos de destino**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-171">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="2fd3b-172">O provisionamento demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-172">Provisioning takes a minute or so.</span></span> <span data-ttu-id="2fd3b-173">Não feche a folha durante o provisionamento, ou você precisará começar novamente.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-173">Don't close the blade during provisioning, or you need to start over.</span></span>

4. <span data-ttu-id="2fd3b-174">Para disparar a replicação da máquina virtual selecionada, clique em **Habilitar replicação**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-174">To trigger replication of the selected VM, click **Enable replication**.</span></span>

5. <span data-ttu-id="2fd3b-175">Você pode acompanhar o progresso do trabalho **Habilitar Proteção** em **Configurações** > **Trabalhos** > **Trabalhos de Recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-175">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

6. <span data-ttu-id="2fd3b-176">Em **Configurações** > **Itens Replicados**, você pode exibir o status das máquinas virtuais e o andamento da replicação inicial.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-176">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="2fd3b-177">Clique em VM para fazer uma busca detalhada em suas configurações.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-177">Click the VM to drill down into its settings.</span></span>

## <a name="run-a-test-failover"></a><span data-ttu-id="2fd3b-178">Execute um teste de failover</span><span class="sxs-lookup"><span data-stu-id="2fd3b-178">Run a test failover</span></span>

<span data-ttu-id="2fd3b-179">Depois de configurar tudo, execute um failover de teste para garantir que tudo esteja funcionando conforme o esperado:</span><span class="sxs-lookup"><span data-stu-id="2fd3b-179">After you set up everything, run a test failover to make sure everything's working as expected:</span></span>

1. <span data-ttu-id="2fd3b-180">Para fazer failover em um único computador, em **Configurações** > **Itens Replicados**, clique no ícone da VM **+Failover de Teste**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-180">To fail over a single machine, in **Settings** > **Replicated Items**, click the VM **+Test Failover** icon.</span></span>

2. <span data-ttu-id="2fd3b-181">Para fazer failover de um plano de recuperação, em **Configurações** > **Planos de Recuperação**, clique com o botão direito do mouse no plano **Failover de Teste**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-181">To fail over a recovery plan, in **Settings** > **Recovery Plans**, right-click the plan **Test Failover**.</span></span> <span data-ttu-id="2fd3b-182">Para criar um plano de recuperação, [siga estas instruções](site-recovery-create-recovery-plans.md).</span><span class="sxs-lookup"><span data-stu-id="2fd3b-182">To create a recovery plan, [follow these instructions](site-recovery-create-recovery-plans.md).</span></span> 

3. <span data-ttu-id="2fd3b-183">Em **Failover de Teste**, selecione a rede do Azure à qual as VMs do Azure serão conectadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-183">In **Test Failover**, select the target Azure virtual network to which Azure VMs are connected after the failover occurs.</span></span>

4. <span data-ttu-id="2fd3b-184">Para iniciar o failover, clique em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-184">To start the failover, click **OK**.</span></span> <span data-ttu-id="2fd3b-185">Para acompanhar o progresso, clique na VM para abrir suas propriedades.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-185">To track progress, click the VM to open its properties.</span></span> <span data-ttu-id="2fd3b-186">Ou você pode clicar no trabalho **Failover de teste** no nome do cofre > **Configurações** > **Trabalhos** > **Trabalhos de Recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-186">Or you can click the **Test Failover** job in the vault name > **Settings** > **Jobs** > **Site Recovery jobs**.</span></span>

5. <span data-ttu-id="2fd3b-187">Após a conclusão do failover, você também deve conseguir ver a réplica do computador Azure exibida no Portal do Azure > **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-187">After the failover finishes, the replica Azure machine appears in the Azure portal > **Virtual Machines**.</span></span> <span data-ttu-id="2fd3b-188">Verifique se a VM é do tamanho apropriado, se está conectada à rede adequada e se está em execução.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-188">Make sure that the VM is the appropriate size, that it's connected to the appropriate network, and that it's running.</span></span>

6. <span data-ttu-id="2fd3b-189">Para excluir as VMs que foram criadas durante o failover de teste, clique em **Failover de teste de limpeza** no item replicado ou no plano de recuperação.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-189">To delete the VMs that were created during the test failover, click **Cleanup test failover** on the replicated item or the recovery plan.</span></span> <span data-ttu-id="2fd3b-190">Em **Observações**, registre e salve todas as observações associadas ao failover de teste.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-190">In **Notes**, record and save any observations associated with the test failover.</span></span> 

<span data-ttu-id="2fd3b-191">[Saiba mais](site-recovery-test-failover-to-azure.md) sobre failovers de teste.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-191">[Learn more](site-recovery-test-failover-to-azure.md) about test failovers.</span></span>


## <a name="next-steps"></a><span data-ttu-id="2fd3b-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2fd3b-192">Next steps</span></span>

<span data-ttu-id="2fd3b-193">Depois de você testar a implantação:</span><span class="sxs-lookup"><span data-stu-id="2fd3b-193">After you test the deployment:</span></span>

- <span data-ttu-id="2fd3b-194">[Saiba mais](site-recovery-failover.md) sobre diferentes tipos de failovers e como executá-los.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-194">[Learn more](site-recovery-failover.md) about different types of failovers and how to run them.</span></span>
- <span data-ttu-id="2fd3b-195">Saiba mais sobre [usando planos de recuperação](site-recovery-create-recovery-plans.md) para reduzir o RTO.</span><span class="sxs-lookup"><span data-stu-id="2fd3b-195">Learn more about [using recovery plans](site-recovery-create-recovery-plans.md) to reduce RTO.</span></span>
