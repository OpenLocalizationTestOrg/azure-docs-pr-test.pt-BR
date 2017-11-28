---
title: "Habilitar a replicação de VMs VMware que replicam para o Azure com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas necessárias para habilitar a replicação de VMs VMware para o Azure, usando o serviço Azure Site Recovery"
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: 519c5559-7032-4954-b8b5-f24f5242a954
ms.service: site-recovery
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/27/2017
ms.author: raynew
ms.openlocfilehash: 470b9ddd8df4a4e74ec7174f79020c252323e502
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-11-enable-replication-for-vmware-virtual-machines-to-azure"></a><span data-ttu-id="f2767-103">Etapa 11: Habilitar replicação de máquinas virtuais VMware para o Azure</span><span class="sxs-lookup"><span data-stu-id="f2767-103">Step 11: Enable replication for VMware virtual machines to Azure</span></span>


<span data-ttu-id="f2767-104">Este artigo descreve como habilitar a replicação de VMs VMware locais para o Azure, usando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2767-104">This article describes how to enable replication for on-premises VMware virtual machines to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="f2767-105">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="f2767-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>


## <a name="before-you-start"></a><span data-ttu-id="f2767-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="f2767-106">Before you start</span></span>

- <span data-ttu-id="f2767-107">As VMs VMware devem ter o [componente Serviço de mobilidade instalado](vmware-walkthrough-install-mobility.md).</span><span class="sxs-lookup"><span data-stu-id="f2767-107">VMware VMs must have the [Mobility service component installed](vmware-walkthrough-install-mobility.md).</span></span> <span data-ttu-id="f2767-108">- Se uma VM for preparada para a instalação por push, o servidor de processo instalará automaticamente o serviço Mobilidade quando você habilitar a replicação.</span><span class="sxs-lookup"><span data-stu-id="f2767-108">- If a VM is prepared for push installation, the process server automatically installs the Mobility service when you enable replication.</span></span>
- <span data-ttu-id="f2767-109">Sua conta de usuário do Azure precisa de [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) específicas para habilitar a replicação de uma VM para o Azure</span><span class="sxs-lookup"><span data-stu-id="f2767-109">Your Azure user account needs specific [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a VM to Azure</span></span>
- <span data-ttu-id="f2767-110">Quando você adiciona ou modifica as VMs, pode levar 15 minutos ou mais para que as alterações entrem em vigor e para que apareçam no portal.</span><span class="sxs-lookup"><span data-stu-id="f2767-110">When you add or modify VMs, it can take up to 15 minutes or longer for changes to take effect, and for them to appear in the portal.</span></span>
- <span data-ttu-id="f2767-111">Você pode verificar a hora da última descoberta de VMs em **Servidores de Configuração** > **Último Contato às**.</span><span class="sxs-lookup"><span data-stu-id="f2767-111">You can check the last discovered time for VMs in **Configuration Servers** > **Last Contact At**.</span></span>
- <span data-ttu-id="f2767-112">Para adicionar VMs sem esperar pela descoberta agendada, realce o servidor de configuração (não clique nele) e clique em **Atualizar**.</span><span class="sxs-lookup"><span data-stu-id="f2767-112">To add VMs without waiting for the scheduled discovery, highlight the configuration server (don’t click it), and click **Refresh**.</span></span>



## <a name="exclude-disks-from-replication"></a><span data-ttu-id="f2767-113">Excluir discos da replicação</span><span class="sxs-lookup"><span data-stu-id="f2767-113">Exclude disks from replication</span></span>

<span data-ttu-id="f2767-114">Por padrão, todos os discos em um computador são replicados.</span><span class="sxs-lookup"><span data-stu-id="f2767-114">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="f2767-115">Você pode excluir discos da replicação.</span><span class="sxs-lookup"><span data-stu-id="f2767-115">You can exclude disks from replication.</span></span> <span data-ttu-id="f2767-116">Por exemplo, talvez você não queira replicar discos com dados temporários ou dados atualizados cada vez que um computador ou um aplicativo é reiniciado (por exemplo, pagefile.sys ou SQL Server tempdb).</span><span class="sxs-lookup"><span data-stu-id="f2767-116">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="f2767-117">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="f2767-117">Learn more</span></span>](site-recovery-exclude-disk.md)

## <a name="replicate-vms"></a><span data-ttu-id="f2767-118">Replicar VMs</span><span class="sxs-lookup"><span data-stu-id="f2767-118">Replicate VMs</span></span>

<span data-ttu-id="f2767-119">Antes de começar, assista a uma rápida visão geral em vídeo</span><span class="sxs-lookup"><span data-stu-id="f2767-119">Before you start, watch a quick video overview</span></span>

>[!VIDEO https://channel9.msdn.com/Series/Azure-Site-Recovery/VMware-to-Azure-with-ASR-Video3-Protect-VMware-Virtual-Machines/player]

1. <span data-ttu-id="f2767-120">Clique em **Etapa 2: replicar aplicativo** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="f2767-120">Click **Step 2: Replicate application** > **Source**.</span></span>
2. <span data-ttu-id="f2767-121">Em **Origem**, selecione o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="f2767-121">In **Source**, select the configuration server.</span></span>
3. <span data-ttu-id="f2767-122">Em **Tipo de máquina**, selecione **Máquinas Virtuais**.</span><span class="sxs-lookup"><span data-stu-id="f2767-122">In **Machine type**, select **Virtual Machines**.</span></span>
4. <span data-ttu-id="f2767-123">Em **Hipervisor do vCenter/vSphere**, selecione o servidor vCenter que gerencia o host vSphere ou selecione o host.</span><span class="sxs-lookup"><span data-stu-id="f2767-123">In **vCenter/vSphere Hypervisor**, select the vCenter server that manages the vSphere host, or select the host.</span></span>
5. <span data-ttu-id="f2767-124">Selecione o servidor de processo.</span><span class="sxs-lookup"><span data-stu-id="f2767-124">Select the process server.</span></span> <span data-ttu-id="f2767-125">Se você não criou nenhum servidor de processo adicional, esse será o servidor de configuração.</span><span class="sxs-lookup"><span data-stu-id="f2767-125">If you haven't created any additional process servers this will be the configuration server.</span></span> <span data-ttu-id="f2767-126">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2767-126">Then click **OK**.</span></span>

    ![Habilitar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication2.png)

6. <span data-ttu-id="f2767-128">Em **Destino**, selecione a assinatura e o grupo de recursos em que você deseja criar as VMs com failover.</span><span class="sxs-lookup"><span data-stu-id="f2767-128">In **Target**, select the subscription and the resource group in which you want to create the failed over VMs.</span></span> <span data-ttu-id="f2767-129">Escolha o modelo de implantação que você deseja usar no Azure (clássico ou gerenciamento de recursos) para as VMs do failover.</span><span class="sxs-lookup"><span data-stu-id="f2767-129">Choose the deployment model that you want to use in Azure (classic or resource management), for the failed over VMs.</span></span>


7. <span data-ttu-id="f2767-130">Selecione a conta de armazenamento do Azure que você deseja usar para replicar os dados.</span><span class="sxs-lookup"><span data-stu-id="f2767-130">Select the Azure storage account you want to use for replicating data.</span></span> <span data-ttu-id="f2767-131">Se não quiser usar uma conta que já configurou, você poderá criar uma nova.</span><span class="sxs-lookup"><span data-stu-id="f2767-131">If you don't want to use an account you've already set up, you can create a new one.</span></span>

8. <span data-ttu-id="f2767-132">Selecione a rede e a sub-rede do Azure às quais as VMs do Azure se conectarão quando forem criadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="f2767-132">Select the Azure network and subnet to which Azure VMs will connect, when they're created after failover.</span></span> <span data-ttu-id="f2767-133">Selecione **Configurar agora para computadores selecionados** para aplicar a configuração de rede a todos os computadores selecionados para proteção.</span><span class="sxs-lookup"><span data-stu-id="f2767-133">Select **Configure now for selected machines**, to apply the network setting to all machines you select for protection.</span></span> <span data-ttu-id="f2767-134">Selecione **Configurar mais tarde** para selecionar a rede do Azure por computador.</span><span class="sxs-lookup"><span data-stu-id="f2767-134">Select **Configure later** to select the Azure network per machine.</span></span> <span data-ttu-id="f2767-135">Se não quiser usar uma rede existente, você poderá criar uma.</span><span class="sxs-lookup"><span data-stu-id="f2767-135">If you don't want to use an existing network, you can create one.</span></span>

    ![Habilitar a replicação](./media/vmware-walkthrough-enable-replication/enable-rep3.png)
9. <span data-ttu-id="f2767-137">Em **Máquinas Virtuais** > **Selecionar máquinas virtuais**, clique e selecione cada máquina que você deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="f2767-137">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="f2767-138">Você só pode selecionar computadores para os quais a replicação pode ser habilitada.</span><span class="sxs-lookup"><span data-stu-id="f2767-138">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="f2767-139">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2767-139">Then click **OK**.</span></span>

    ![Habilitar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication5.png)
10. <span data-ttu-id="f2767-141">Em **Propriedades** > **Configurar propriedades**, selecione a conta que será usada pelo servidor de processo para instalar automaticamente o serviço de Mobilidade no computador.</span><span class="sxs-lookup"><span data-stu-id="f2767-141">In **Properties** > **Configure properties**, select the account that will be used by the process server to automatically install the Mobility service on the machine.</span></span>
11. <span data-ttu-id="f2767-142">Por padrão, todos os discos são replicados.</span><span class="sxs-lookup"><span data-stu-id="f2767-142">By default all disks are replicated.</span></span> <span data-ttu-id="f2767-143">Clique em **Todos os Discos** e desmarque os discos que você não deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="f2767-143">Click **All Disks** and clear any disks you don't want to replicate.</span></span> <span data-ttu-id="f2767-144">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2767-144">Then click **OK**.</span></span> <span data-ttu-id="f2767-145">Você pode definir propriedades de VM adicionais posteriormente.</span><span class="sxs-lookup"><span data-stu-id="f2767-145">You can set additional VM properties later.</span></span>

    ![Habilitar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication6.png)
11. <span data-ttu-id="f2767-147">Em **Configurações de replicação** > **Definir configurações de replicação**, verifique se a política de replicação correta está selecionada.</span><span class="sxs-lookup"><span data-stu-id="f2767-147">In **Replication settings** > **Configure replication settings**, verify that the correct replication policy is selected.</span></span> <span data-ttu-id="f2767-148">Se você modificar uma política, as alterações serão aplicadas à máquina de replicação e às novas máquinas.</span><span class="sxs-lookup"><span data-stu-id="f2767-148">If you modify a policy, changes will be applied to replicating machine, and to new machines.</span></span>
12. <span data-ttu-id="f2767-149">Habilite **Consistência de várias VMs** se você quiser reunir computadores em um grupo de replicação e especifique um nome para o grupo.</span><span class="sxs-lookup"><span data-stu-id="f2767-149">Enable **Multi-VM consistency** if you want to gather machines into a replication group, and specify a name for the group.</span></span> <span data-ttu-id="f2767-150">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="f2767-150">Then click **OK**.</span></span> <span data-ttu-id="f2767-151">Observe que:</span><span class="sxs-lookup"><span data-stu-id="f2767-151">Note that:</span></span>

    * <span data-ttu-id="f2767-152">Os computadores nos grupos de replicação são replicados em conjunto e têm pontos de recuperação consistentes compartilhados com o aplicativo e com falhas quando executam failover.</span><span class="sxs-lookup"><span data-stu-id="f2767-152">Machines in replication groups replicate together, and have shared crash-consistent and app-consistent recovery points when they fail over.</span></span>
    * <span data-ttu-id="f2767-153">É recomendável que você colete VMs e servidores físicos para que espelhem suas cargas de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f2767-153">We recommend that you gather VMs and physical servers together so that they mirror your workloads.</span></span> <span data-ttu-id="f2767-154">Habilitar a consistência de várias VMs pode afetar o desempenho da carga de trabalho e só deve ser usada se os computadores estão executando a mesma carga de trabalho e precisam de consistência.</span><span class="sxs-lookup"><span data-stu-id="f2767-154">Enabling multi-VM consistency can impact workload performance, and should only be used if machines are running the same workload and you need consistency.</span></span>

    ![Habilitar a replicação](./media/vmware-walkthrough-enable-replication/enable-replication7.png)
13. <span data-ttu-id="f2767-156">Clique em **Habilitar a Replicação**.</span><span class="sxs-lookup"><span data-stu-id="f2767-156">Click **Enable Replication**.</span></span> <span data-ttu-id="f2767-157">Você pode acompanhar o progresso do trabalho **Habilitar Proteção** em **Configurações** > **Trabalhos** > **Trabalhos de Recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="f2767-157">You can track progress of the **Enable Protection** job in **Settings** > **Jobs** > **Site Recovery Jobs**.</span></span> <span data-ttu-id="f2767-158">Após o trabalho de **Finalizar Proteção** ser executado, o computador estará pronto para failover.</span><span class="sxs-lookup"><span data-stu-id="f2767-158">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2767-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2767-159">Next steps</span></span>

<span data-ttu-id="f2767-160">Vá para a [Etapa 12: Executar um failover de teste](vmware-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="f2767-160">Go to [Step 12: Run a test failover](vmware-walkthrough-test-failover.md)</span></span>
