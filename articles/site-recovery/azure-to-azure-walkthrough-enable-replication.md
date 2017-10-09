---
title: "a replicação para máquinas virtuais do Azure tooanother região do Azure com o Azure Site Recovery aaaEnable | Microsoft Docs"
description: "Resume as etapas de saudação precisar tooenable replicação tooanother região do Azure para máquinas virtuais do Azure, usando o serviço do Azure Site Recovery Olá"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: a309644f-d36b-4188-bba7-ad45a2d9bede
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 8/01/2017
ms.author: raynew
ms.openlocfilehash: 2fa03db45a18ccb8b9f31ed05589be0dd6d5f031
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="ca0f6-103">Etapa 5: habilitar replicação para VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="ca0f6-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="ca0f6-104">Depois de configurar um [Cofre de serviços de recuperação](azure-to-azure-walkthrough-vault.md), use a replicação de tooenable de artigo de máquinas virtuais (VMs) tooanother região do Azure, com [do Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ca0f6-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article tooenable replication of virtual machines (VMs), tooanother Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="ca0f6-105">replicação tooenable, você definir as configurações de origem e de destino, verifique se a política de replicação hello e selecione VMs que você deseja tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-105">tooenable replication, you set up source and target settings, verify hello replication policy, and select VMs you want tooreplicate.</span></span>

- <span data-ttu-id="ca0f6-106">Quando você terminar de artigo hello, suas VMs do Azure deve estar replicando toohello região secundária do Azure.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-106">When you finish hello article, your Azure VMs should be replicating toohello secondary Azure region.</span></span>
- <span data-ttu-id="ca0f6-107">Lançar os comentários na parte inferior da saudação deste artigo, ou fazer perguntas no hello [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="ca0f6-107">Post any comments at hello bottom of this article, or ask questions in hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="ca0f6-108">Atualmente, a replicação de VM do Azure está em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-hello-source"></a><span data-ttu-id="ca0f6-109">Selecione a fonte de saudação</span><span class="sxs-lookup"><span data-stu-id="ca0f6-109">Select hello source</span></span> 

1. <span data-ttu-id="ca0f6-110">Cofres de serviços de recuperação, clique em nome do cofre hello > **+ replicar**.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-110">In Recovery Services vaults, click hello vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="ca0f6-111">Em **fonte**, selecione **Azure - VISUALIZAÇÃO**.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="ca0f6-112">Em **local de origem**, selecione origem Olá região do Azure em que suas VMs estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-112">In **Source location**, select hello source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="ca0f6-113">Selecione Olá **modelo de implantação de máquina virtual do Azure** para VMs: **Gerenciador de recursos de** ou **clássico**.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-113">Select hello **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="ca0f6-114">Selecione Olá **grupo de recursos de origem** para VMs do Gerenciador de recursos, ou **serviço de nuvem** para VMs clássicas.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-114">Select hello **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="ca0f6-115">Clique em **Okey** toosave configurações de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-115">Click **OK** toosave hello settings.</span></span>

    ![Configurar fonte Olá](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-hello-vms"></a><span data-ttu-id="ca0f6-117">Selecione Olá VMs</span><span class="sxs-lookup"><span data-stu-id="ca0f6-117">Select hello VMs</span></span>

<span data-ttu-id="ca0f6-118">Recuperação de site recupera uma lista de saudação que VMs associadas com assinatura hello e serviço de nuvem/grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-118">Site Recovery retrieves a list of hello VMs associated with hello subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="ca0f6-119">Em **máquinas virtuais**, selecione VMs Olá deseja tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-119">In **Virtual Machines**, select hello VMs you want tooreplicate.</span></span>
2. <span data-ttu-id="ca0f6-120">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-120">Click **OK**.</span></span>

    ![Selecione as máquinas virtuais](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="ca0f6-122">Configurar definições</span><span class="sxs-lookup"><span data-stu-id="ca0f6-122">Configure settings</span></span>

<span data-ttu-id="ca0f6-123">Recuperação de site fornece configurações padrão para a região de destino da saudação (com base nas configurações de região de origem de saudação) e a política de replicação hello:</span><span class="sxs-lookup"><span data-stu-id="ca0f6-123">Site Recovery provisions default settings for hello target region (based on hello source region settings), and hello replication policy:</span></span>

   - <span data-ttu-id="ca0f6-124">**Local de destino**: região de destino Olá desejar toouse para recuperação de desastres.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-124">**Target location**: hello target region you want toouse for disaster recovery.</span></span> <span data-ttu-id="ca0f6-125">É recomendável que o local de destino Olá corresponde ao local de Olá do Cofre de recuperação de Site hello.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-125">We recommend that hello target location matches hello location of hello Site Recovery vault.</span></span>
   - <span data-ttu-id="ca0f6-126">**Grupo de recursos de destino**: toowhich do grupo de recursos VMs do Azure na região de destino Olá pertencerão após o failover.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-126">**Target resource group**: Resource group toowhich Azure VMs in hello target region will belong after failover.</span></span> <span data-ttu-id="ca0f6-127">Por padrão, a recuperação de Site cria um novo grupo de recursos na região de destino Olá com um sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="ca0f6-127">By default, Site Recovery creates a new resource group in hello target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="ca0f6-128">**Rede virtual de destino**: rede Olá em qual VMs do Azure no hello região de destino serão localizado após o failover.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-128">**Target virtual network**: hello network in which Azure VMs in hello target region will be located after failover.</span></span> <span data-ttu-id="ca0f6-129">Por padrão, a recuperação de Site cria uma nova rede virtual (e sub-redes) na região de destino Olá com um sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="ca0f6-129">By default, Site Recovery creates a new virtual network (and subnets) in hello target region with an "asr" suffix.</span></span> <span data-ttu-id="ca0f6-130">Esta rede é mapeada tooyour rede de origem.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-130">This network is mapped tooyour source network.</span></span> <span data-ttu-id="ca0f6-131">Observe que você pode atribuir um endereço IP específico após o failover de uma máquina virtual, se você precisar tooretain Olá mesmo endereço IP em locais de origem e destino hello.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-131">Note that you can assign a specific IP address after failover of a VM, if you need tooretain hello same IP address in hello source and target locations.</span></span> 
   - <span data-ttu-id="ca0f6-132">**Contas de armazenamento de cache**: recuperação de Site usa uma conta de armazenamento na região de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-132">**Cache storage accounts**: Site Recovery uses a storage account in hello source region.</span></span> <span data-ttu-id="ca0f6-133">Alterações nas máquinas virtuais de origem são enviadas toothis conta, antes do local de destino do toohello de replicação.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-133">Changes on source VMs are sent toothis account, before replication toohello target location.</span></span> 
   - <span data-ttu-id="ca0f6-134">**Contas de armazenamento de destino**: por padrão, a recuperação de Site cria uma nova conta de armazenamento na região de destino hello, origem de saudação toomirror conta de armazenamento da VM.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in hello target region, toomirror hello source VM storage account.</span></span>
   -  <span data-ttu-id="ca0f6-135">**Conjuntos de disponibilidade de destino**: por padrão, a recuperação de Site cria uma novo conjunto de disponibilidade no região de destino hello, com o sufixo de "asr" hello.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-135">**Target availability sets**: By default, Site Recovery creates a new availability set in hello target region, with hello "asr" suffix.</span></span> 
   - <span data-ttu-id="ca0f6-136">**Nome da política de replicação**: nome da política.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="ca0f6-137">**Retenção de ponto de recuperação**: por padrão, o Site Recovery mantém os pontos de recuperação por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="ca0f6-138">É possível configurar um valor entre 1 e 72 horas.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="ca0f6-139">**Frequência de instantâneo consistente com o aplicativo**: por padrão, o Site Recovery obtém um instantâneo consistente com o aplicativo a cada 4 horas.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="ca0f6-140">É possível configurar qualquer valor entre 1 e 12 horas.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="ca0f6-141">Os dados são replicados continuamente:</span><span class="sxs-lookup"><span data-stu-id="ca0f6-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="ca0f6-142">Os pontos de recuperação consistentes com falha mantêm uma ordem de gravação de dados consistente quando criados.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="ca0f6-143">Esse tipo de ponto de recuperação é geralmente suficiente se seu aplicativo é projetado toorecover em caso de falha sem inconsistências de dados</span><span class="sxs-lookup"><span data-stu-id="ca0f6-143">This type of recovery point is usually sufficient if your app is designed toorecover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="ca0f6-144">Os pontos de recuperação consistentes com falha são gerados a cada poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="ca0f6-145">Usando essas toofail de pontos de recuperação sobre e recuperar suas VMs fornece um ponto de RPO (objetivo recuperação) na ordem de saudação de minutos.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-145">Using these recovery points toofail over and recover your VMs provides a Recovery Point Objective (RPO) in hello order of minutes.</span></span>
    - <span data-ttu-id="ca0f6-146">Pontos de recuperação consistentes com o aplicativo (na consistência de ordem de toowrite adição) Verifique se os aplicativos em execução concluir todas as operações e liberar buffers toodisk (pausas de aplicativo).</span><span class="sxs-lookup"><span data-stu-id="ca0f6-146">App-consistent recovery points (in addition toowrite-order consistency) ensure that running apps complete all operations and flush buffers toodisk (application quiescing).</span></span> <span data-ttu-id="ca0f6-147">É recomendável utilizar esses pontos de recuperação para aplicativos de banco de dados, como SQL Server, Oracle e Exchange.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Configurar definições](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="ca0f6-149">Modificar configurações</span><span class="sxs-lookup"><span data-stu-id="ca0f6-149">Modify settings</span></span>

<span data-ttu-id="ca0f6-150">Se você quiser toomodify configurações de política de replicação e de destino, Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="ca0f6-150">If you want toomodify target and replication policy settings, do hello following:</span></span>

1. <span data-ttu-id="ca0f6-151">tooview ou modificar as configurações de destino, clique em **configurações**.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-151">tooview or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="ca0f6-152">configurações de destino do toooverride saudação padrão, clique em **personalizar**.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-152">toooverride hello default target settings, click **Customize**.</span></span> <span data-ttu-id="ca0f6-153">É possível especificar um grupo de recursos de destino, uma rede virtual, um conjunto de disponibilidade e uma conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="ca0f6-154">Você só pode adicionar conjuntos de disponibilidade se as VMs são parte de um conjunto na região de origem de saudação.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-154">You can only add availability sets if VMs are part of a set in hello source region.</span></span>

    ![Configurar definições](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="ca0f6-156">configurações de replicação de toooverride para pontos de recuperação e instantâneos consistentes com o aplicativo, clique em **personalizar** Avançar muito**política de replicação**.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-156">toooverride replication settings for recovery points and app-consistent snapshots, click **Customize** next too**Replication Policy**.</span></span>
 
    ![Configurar definições](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="ca0f6-158">provisionar recursos de destino de saudação toostart, clique em **criar recursos de destino**.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-158">toostart provisioning hello target resources, click **Create target resources**.</span></span> <span data-ttu-id="ca0f6-159">O provisionamento demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="ca0f6-160">Não feche a folha de saudação durante o provisionamento, ou você terá toostart sobre.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-160">Don't close hello blade during provisioning, or you'll have toostart over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="ca0f6-161">Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="ca0f6-161">Enable replication</span></span>

1. <span data-ttu-id="ca0f6-162">Em **Configurações**, clique em **Habilitar replicação**.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="ca0f6-163">Isso permite que a replicação inicial da saudação VMs que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-163">This enables initial replication of hello VMs you selected.</span></span> <span data-ttu-id="ca0f6-164">Status de replicação inicial pode levar algum tempo toorefresh.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-164">Initial replication status might take some time toorefresh.</span></span> <span data-ttu-id="ca0f6-165">Clique em **atualização** status mais recente do tooget hello.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-165">Click **Refresh** tooget hello latest status.</span></span>

2. <span data-ttu-id="ca0f6-166">Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **configurações** > **trabalhos** > **trabalhos de recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-166">You can track progress of hello **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="ca0f6-167">Em **configurações** > **itens replicados**, você pode exibir o status de saudação de VMs e Olá andamento da replicação inicial.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-167">In **Settings** > **Replicated Items**, you can view hello status of VMs and hello initial replication progress.</span></span> <span data-ttu-id="ca0f6-168">Clique em Olá VM toodrill abaixo em suas configurações.</span><span class="sxs-lookup"><span data-stu-id="ca0f6-168">Click hello VM toodrill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="ca0f6-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ca0f6-169">Next steps</span></span>

<span data-ttu-id="ca0f6-170">Vá muito[etapa 6: executar um failover de teste](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="ca0f6-170">Go too[Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
