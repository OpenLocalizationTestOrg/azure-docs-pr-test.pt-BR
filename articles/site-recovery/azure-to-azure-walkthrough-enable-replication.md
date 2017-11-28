---
title: "Habilitar a replicação para VMs do Azure para outra região do Azure com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas necessárias para habilitar a replicação para outra região do Azure para VMs do Azure, utilizando o serviço do Azure Site Recovery"
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
ms.openlocfilehash: f426ba4341e61d3c7da820d7d5097b217e94ca0e
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="step-5-enable-replication-for-azure-vms"></a><span data-ttu-id="a1074-103">Etapa 5: habilitar replicação para VMs do Azure</span><span class="sxs-lookup"><span data-stu-id="a1074-103">Step 5: Enable replication for Azure VMs</span></span>


<span data-ttu-id="a1074-104">Após configurar um [Cofre de Serviços de Recuperação](azure-to-azure-walkthrough-vault.md), utilize este artigo para habilitar a replicação de VMs (Máquinas Virtuais) para outra região do Azure, com o [Azure Site Recovery](site-recovery-overview.md).</span><span class="sxs-lookup"><span data-stu-id="a1074-104">After setting up a [Recovery Services vault](azure-to-azure-walkthrough-vault.md), use this article to enable replication of virtual machines (VMs), to another Azure region, with [Azure Site Recovery](site-recovery-overview.md).</span></span> <span data-ttu-id="a1074-105">Para habilitar a replicação, você define as configurações de origem e destino, verifica a política de replicação e seleciona as VMs que deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="a1074-105">To enable replication, you set up source and target settings, verify the replication policy, and select VMs you want to replicate.</span></span>

- <span data-ttu-id="a1074-106">Ao concluir o artigo, suas VMs do Azure deverão ser replicadas para a região do Azure secundária.</span><span class="sxs-lookup"><span data-stu-id="a1074-106">When you finish the article, your Azure VMs should be replicating to the secondary Azure region.</span></span>
- <span data-ttu-id="a1074-107">Publique eventuais comentários no final deste artigo ou no [Fórum dos Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span><span class="sxs-lookup"><span data-stu-id="a1074-107">Post any comments at the bottom of this article, or ask questions in the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr)</span></span>

>[!NOTE]
>
> <span data-ttu-id="a1074-108">Atualmente, a replicação de VM do Azure está em versão prévia.</span><span class="sxs-lookup"><span data-stu-id="a1074-108">Azure VM replication is currently in preview.</span></span>


## <a name="select-the-source"></a><span data-ttu-id="a1074-109">Selecione a origem</span><span class="sxs-lookup"><span data-stu-id="a1074-109">Select the source</span></span> 

1. <span data-ttu-id="a1074-110">Em cofres dos Serviços de Recuperação, clique no nome do cofre > **+Replicar**.</span><span class="sxs-lookup"><span data-stu-id="a1074-110">In Recovery Services vaults, click the vault name > **+Replicate**.</span></span>
2. <span data-ttu-id="a1074-111">Em **fonte**, selecione **Azure - VISUALIZAÇÃO**.</span><span class="sxs-lookup"><span data-stu-id="a1074-111">In **Source**, select **Azure - PREVIEW**.</span></span>
2. <span data-ttu-id="a1074-112">Em **Local de origem**, selecione a fonte de região do Azure em que suas VMs estão sendo executados.</span><span class="sxs-lookup"><span data-stu-id="a1074-112">In **Source location**, select the source Azure region where your VMs are currently running.</span></span>
3. <span data-ttu-id="a1074-113">Selecione o **modelo de implantação de máquina virtual do Azure** para VMs: **Gerenciador de Recursos** ou **Clássico**.</span><span class="sxs-lookup"><span data-stu-id="a1074-113">Select the **Azure virtual machine deployment model** for VMs: **Resource Manager** or **Classic**.</span></span>
4. <span data-ttu-id="a1074-114">Selecione o **Grupo de recursos de origem** para VMs do Gerenciador de Recursos ou **serviço de nuvem** para VMs clássicas.</span><span class="sxs-lookup"><span data-stu-id="a1074-114">Select the **Source resource group** for Resource Manager VMs, or **cloud service** for classic VMs.</span></span>
5. <span data-ttu-id="a1074-115">Clique em **OK** para salvar as configurações.</span><span class="sxs-lookup"><span data-stu-id="a1074-115">Click **OK** to save the settings.</span></span>

    ![Configure a origem](./media/azure-to-azure-walkthrough-enable-replication/source.png)

## <a name="select-the-vms"></a><span data-ttu-id="a1074-117">Selecione as VMs</span><span class="sxs-lookup"><span data-stu-id="a1074-117">Select the VMs</span></span>

<span data-ttu-id="a1074-118">O Site Recovery recupera uma lista das VMs associadas ao serviço de nuvem/grupo de recursos e assinatura.</span><span class="sxs-lookup"><span data-stu-id="a1074-118">Site Recovery retrieves a list of the VMs associated with the subscription and resource group/cloud service.</span></span>

1. <span data-ttu-id="a1074-119">Em **Máquinas Virtuais**, selecione as VMs que deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="a1074-119">In **Virtual Machines**, select the VMs you want to replicate.</span></span>
2. <span data-ttu-id="a1074-120">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="a1074-120">Click **OK**.</span></span>

    ![Selecione as máquinas virtuais](./media/azure-to-azure-walkthrough-enable-replication/vms.png)


## <a name="configure-settings"></a><span data-ttu-id="a1074-122">Configurar definições</span><span class="sxs-lookup"><span data-stu-id="a1074-122">Configure settings</span></span>

<span data-ttu-id="a1074-123">O Site Recovery provisiona configurações padrão para a região de destino (baseado nas configurações da região de origem) e a política de replicação:</span><span class="sxs-lookup"><span data-stu-id="a1074-123">Site Recovery provisions default settings for the target region (based on the source region settings), and the replication policy:</span></span>

   - <span data-ttu-id="a1074-124">**Localização de destino**: a região de destino que você deseja utilizar para recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="a1074-124">**Target location**: The target region you want to use for disaster recovery.</span></span> <span data-ttu-id="a1074-125">É recomendável que a localização de destino corresponda à localização do cofre do Site Recovery.</span><span class="sxs-lookup"><span data-stu-id="a1074-125">We recommend that the target location matches the location of the Site Recovery vault.</span></span>
   - <span data-ttu-id="a1074-126">**Grupo de recursos de destino**: grupo de recursos para o qual as VMs do Azure na região de destino pertencerão após o failover.</span><span class="sxs-lookup"><span data-stu-id="a1074-126">**Target resource group**: Resource group to which Azure VMs in the target region will belong after failover.</span></span> <span data-ttu-id="a1074-127">Por padrão, o Site Recovery cria um novo grupo de recursos na região de destino com um sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="a1074-127">By default, Site Recovery creates a new resource group in the target region with an "asr" suffix.</span></span> 
   - <span data-ttu-id="a1074-128">**Rede virtual de destino**: a rede na qual as VMs Azure na região alvo serão localizadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="a1074-128">**Target virtual network**: The network in which Azure VMs in the target region will be located after failover.</span></span> <span data-ttu-id="a1074-129">Por padrão, o Site Recovery cria uma nova rede virtual (e sub-redes) na região de destino com um sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="a1074-129">By default, Site Recovery creates a new virtual network (and subnets) in the target region with an "asr" suffix.</span></span> <span data-ttu-id="a1074-130">Essa rede é mapeada para sua rede de origem.</span><span class="sxs-lookup"><span data-stu-id="a1074-130">This network is mapped to your source network.</span></span> <span data-ttu-id="a1074-131">Observe que é possível atribuir um endereço IP específico após o failover de uma VM, se você precisar reter o mesmo endereço IP nas localizações de origem e destino.</span><span class="sxs-lookup"><span data-stu-id="a1074-131">Note that you can assign a specific IP address after failover of a VM, if you need to retain the same IP address in the source and target locations.</span></span> 
   - <span data-ttu-id="a1074-132">**Contas de armazenamento de cache**: o Site Recovery utiliza uma conta de armazenamento na região de origem.</span><span class="sxs-lookup"><span data-stu-id="a1074-132">**Cache storage accounts**: Site Recovery uses a storage account in the source region.</span></span> <span data-ttu-id="a1074-133">As alterações nas VMs de origem são enviadas para essa conta, antes da replicação para a localização de destino.</span><span class="sxs-lookup"><span data-stu-id="a1074-133">Changes on source VMs are sent to this account, before replication to the target location.</span></span> 
   - <span data-ttu-id="a1074-134">**Contas de armazenamento de destino**: por padrão, o Site Recovery cria uma nova conta de armazenamento na região de destino, para espelhar a conta de armazenamento da VM de origem.</span><span class="sxs-lookup"><span data-stu-id="a1074-134">**Target storage accounts**: By default, Site Recovery creates a new storage account in the target region, to mirror the source VM storage account.</span></span>
   -  <span data-ttu-id="a1074-135">**Conjuntos de disponibilidade de destino**: por padrão, o Site Recovery cria um novo conjunto de disponibilidade na região de destino, com o sufixo "asr".</span><span class="sxs-lookup"><span data-stu-id="a1074-135">**Target availability sets**: By default, Site Recovery creates a new availability set in the target region, with the "asr" suffix.</span></span> 
   - <span data-ttu-id="a1074-136">**Nome da política de replicação**: nome da política.</span><span class="sxs-lookup"><span data-stu-id="a1074-136">**Replication policy name**: Policy name.</span></span>
   - <span data-ttu-id="a1074-137">**Retenção de ponto de recuperação**: por padrão, o Site Recovery mantém os pontos de recuperação por 24 horas.</span><span class="sxs-lookup"><span data-stu-id="a1074-137">**Recovery point retention**: By default Site Recovery keeps recovery points for 24 hours.</span></span> <span data-ttu-id="a1074-138">É possível configurar um valor entre 1 e 72 horas.</span><span class="sxs-lookup"><span data-stu-id="a1074-138">You can configure a value between 1 and 72 hours.</span></span>
   - <span data-ttu-id="a1074-139">**Frequência de instantâneo consistente com o aplicativo**: por padrão, o Site Recovery obtém um instantâneo consistente com o aplicativo a cada 4 horas.</span><span class="sxs-lookup"><span data-stu-id="a1074-139">**App-consistent snapshot frequency**: By default Site Recovery takes an app-consistent snapshot every 4 hours.</span></span> <span data-ttu-id="a1074-140">É possível configurar qualquer valor entre 1 e 12 horas.</span><span class="sxs-lookup"><span data-stu-id="a1074-140">You can configure any value between 1 and 12 hours.</span></span> <span data-ttu-id="a1074-141">Os dados são replicados continuamente:</span><span class="sxs-lookup"><span data-stu-id="a1074-141">Data is replicated continuously:</span></span>
    - <span data-ttu-id="a1074-142">Os pontos de recuperação consistentes com falha mantêm uma ordem de gravação de dados consistente quando criados.</span><span class="sxs-lookup"><span data-stu-id="a1074-142">Crash-consistent recovery points maintain consistent data write-order when created.</span></span> <span data-ttu-id="a1074-143">Este tipo de ponto de recuperação geralmente é suficiente se o seu aplicativo for projetado para recuperar de uma falha sem inconsistências de dados</span><span class="sxs-lookup"><span data-stu-id="a1074-143">This type of recovery point is usually sufficient if your app is designed to recover from a crash without data inconsistencies</span></span>
    - <span data-ttu-id="a1074-144">Os pontos de recuperação consistentes com falha são gerados a cada poucos minutos.</span><span class="sxs-lookup"><span data-stu-id="a1074-144">Crash-consistent recovery points are generated every few minutes.</span></span> <span data-ttu-id="a1074-145">O uso desses pontos de recuperação para fazer failover e recuperar suas VMs fornece um RPO (Objetivo do Ponto de Recuperação) na ordem dos minutos.</span><span class="sxs-lookup"><span data-stu-id="a1074-145">Using these recovery points to fail over and recover your VMs provides a Recovery Point Objective (RPO) in the order of minutes.</span></span>
    - <span data-ttu-id="a1074-146">Pontos de recuperação consistente com o aplicativo (além da consistência de ordem de gravação) garantem que a execução de aplicativos conclua todas as operações e libere os buffers para disco (fechando o aplicativo).</span><span class="sxs-lookup"><span data-stu-id="a1074-146">App-consistent recovery points (in addition to write-order consistency) ensure that running apps complete all operations and flush buffers to disk (application quiescing).</span></span> <span data-ttu-id="a1074-147">É recomendável utilizar esses pontos de recuperação para aplicativos de banco de dados, como SQL Server, Oracle e Exchange.</span><span class="sxs-lookup"><span data-stu-id="a1074-147">We recommend you use these recovery points for database apps such as SQL Server, Oracle, and Exchange.</span></span>
        
    ![Configurar definições](./media/azure-to-azure-walkthrough-enable-replication/settings.png)


### <a name="modify-settings"></a><span data-ttu-id="a1074-149">Modificar configurações</span><span class="sxs-lookup"><span data-stu-id="a1074-149">Modify settings</span></span>

<span data-ttu-id="a1074-150">Se deseja modificar as configurações de política de replicação e destino, faça o seguinte:</span><span class="sxs-lookup"><span data-stu-id="a1074-150">If you want to modify target and replication policy settings, do the following:</span></span>

1. <span data-ttu-id="a1074-151">Para exibir ou modificar as configurações de destino, clique em **Configurações**.</span><span class="sxs-lookup"><span data-stu-id="a1074-151">To view or modify target settings, click **Settings**.</span></span>
2. <span data-ttu-id="a1074-152">Para substituir as configurações de destino padrão, clique em **Personalizar**.</span><span class="sxs-lookup"><span data-stu-id="a1074-152">To override the default target settings, click **Customize**.</span></span> <span data-ttu-id="a1074-153">É possível especificar um grupo de recursos de destino, uma rede virtual, um conjunto de disponibilidade e uma conta de armazenamento de destino.</span><span class="sxs-lookup"><span data-stu-id="a1074-153">You can specify a target resource group, virtual network, availability set, and target storage account.</span></span> <span data-ttu-id="a1074-154">Somente será possível adicionar conjuntos de disponibilidade se as VMs forem parte de um conjunto na região de origem.</span><span class="sxs-lookup"><span data-stu-id="a1074-154">You can only add availability sets if VMs are part of a set in the source region.</span></span>

    ![Configurar definições](./media/azure-to-azure-walkthrough-enable-replication/customize-target.png)

3. <span data-ttu-id="a1074-156">Para substituir as configurações de replicação para pontos de recuperação e snapshots consistentes com o aplicativo, clique em **Personalizar** próximo à **Política de Replicação**.</span><span class="sxs-lookup"><span data-stu-id="a1074-156">To override replication settings for recovery points and app-consistent snapshots, click **Customize** next to **Replication Policy**.</span></span>
 
    ![Configurar definições](./media/azure-to-azure-walkthrough-enable-replication/customize-policy.png)

4. <span data-ttu-id="a1074-158">Para iniciar o provisionamento de recursos de destino, clique em **Criar recursos de destino**.</span><span class="sxs-lookup"><span data-stu-id="a1074-158">To start provisioning the target resources, click **Create target resources**.</span></span> <span data-ttu-id="a1074-159">O provisionamento demora alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a1074-159">Provisioning takes a minute or so.</span></span> <span data-ttu-id="a1074-160">Não feche a folha durante o provisionamento ou será necessário começar tudo novamente.</span><span class="sxs-lookup"><span data-stu-id="a1074-160">Don't close the blade during provisioning, or you'll have to start over.</span></span>




## <a name="enable-replication"></a><span data-ttu-id="a1074-161">Habilitar a replicação</span><span class="sxs-lookup"><span data-stu-id="a1074-161">Enable replication</span></span>

1. <span data-ttu-id="a1074-162">Em **Configurações**, clique em **Habilitar replicação**.</span><span class="sxs-lookup"><span data-stu-id="a1074-162">In **Settings**, click **Enable replication**.</span></span> <span data-ttu-id="a1074-163">Isso permite a replicação inicial das VMs selecionadas.</span><span class="sxs-lookup"><span data-stu-id="a1074-163">This enables initial replication of the VMs you selected.</span></span> <span data-ttu-id="a1074-164">O status da replicação inicial pode levar algum tempo para atualizar.</span><span class="sxs-lookup"><span data-stu-id="a1074-164">Initial replication status might take some time to refresh.</span></span> <span data-ttu-id="a1074-165">Clique em **Atualizar** para obter o status mais recente.</span><span class="sxs-lookup"><span data-stu-id="a1074-165">Click **Refresh** to get the latest status.</span></span>

2. <span data-ttu-id="a1074-166">Você pode acompanhar o progresso do trabalho **Habilitar Proteção** em **Configurações** > **Trabalhos** > **Trabalhos de Recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="a1074-166">You can track progress of the **Enable protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span>

3. <span data-ttu-id="a1074-167">Em **Configurações** > **Itens Replicados**, você pode exibir o status das máquinas virtuais e o andamento da replicação inicial.</span><span class="sxs-lookup"><span data-stu-id="a1074-167">In **Settings** > **Replicated Items**, you can view the status of VMs and the initial replication progress.</span></span> <span data-ttu-id="a1074-168">Clique em VM para fazer uma busca detalhada em suas configurações.</span><span class="sxs-lookup"><span data-stu-id="a1074-168">Click the VM to drill down into its settings.</span></span>



## <a name="next-steps"></a><span data-ttu-id="a1074-169">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a1074-169">Next steps</span></span>

<span data-ttu-id="a1074-170">Acesse a [Etapa 6: executar um failover de teste](azure-to-azure-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="a1074-170">Go to [Step 6: Run a test failover](azure-to-azure-walkthrough-test-failover.md)</span></span>
