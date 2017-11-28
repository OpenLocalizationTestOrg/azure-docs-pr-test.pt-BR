---
title: "Habilitar a replicação de VMs Hyper-V que replicam para o Azure (sem o System Center VMM) com o Azure Site Recovery | Microsoft Docs"
description: "Resume as etapas necessárias para habilitar a replicação de VMs Hyper-V para o Azure, usando o serviço Azure Site Recovery"
services: site-recovery
documentationcenter: 
author: rayne-wiselman
manager: carmonm
editor: 
ms.assetid: bd31ef01-69f1-4591-a519-e42510a6e2f4
ms.service: site-recovery
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: storage-backup-recovery
ms.date: 06/21/2017
ms.author: raynew
ms.openlocfilehash: aabe99dbd375b80e4a87ca7a067927008672b4ed
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-to-azure"></a><span data-ttu-id="fcf3a-103">Etapa 10: habilitar replicação para VMs do Hyper-V em replicação para o Azure</span><span class="sxs-lookup"><span data-stu-id="fcf3a-103">Step 10: Enable replication for Hyper-V VMs replicating to Azure</span></span>


<span data-ttu-id="fcf3a-104">Este artigo descreve como habilitar a replicação de máquinas virtuais Hyper-V locais (não gerenciadas pelo System Center VMM) para o Azure, usando o serviço [Azure Site Recovery](site-recovery-overview.md) no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-104">This article describes how to enable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) to Azure, using the [Azure Site Recovery](site-recovery-overview.md) service in the Azure portal.</span></span>

<span data-ttu-id="fcf3a-105">Poste perguntas e comentários na parte inferior deste artigo ou no [Fórum de Serviços de Recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="fcf3a-105">Post comments and questions at the bottom of this article, or on the [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="fcf3a-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="fcf3a-106">Before you start</span></span>

<span data-ttu-id="fcf3a-107">Antes de começar, verifique se a sua conta de usuário do Azure tem as [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) necessárias para habilitar a replicação de uma nova máquina virtual no Azure.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-107">Before you start, ensure that your Azure user account has the required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) to enable replication of a new virtual machine to Azure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="fcf3a-108">Excluir discos da replicação</span><span class="sxs-lookup"><span data-stu-id="fcf3a-108">Exclude disks from replication</span></span>

<span data-ttu-id="fcf3a-109">Por padrão, todos os discos em um computador são replicados.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="fcf3a-110">Você pode excluir discos da replicação.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-110">You can exclude disks from replication.</span></span> <span data-ttu-id="fcf3a-111">Por exemplo, talvez você não queira replicar discos com dados temporários ou dados atualizados cada vez que um computador ou um aplicativo é reiniciado (por exemplo, pagefile.sys ou SQL Server tempdb).</span><span class="sxs-lookup"><span data-stu-id="fcf3a-111">For example you might not want to replicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="fcf3a-112">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="fcf3a-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="fcf3a-113">Replicar VMs</span><span class="sxs-lookup"><span data-stu-id="fcf3a-113">Replicate VMs</span></span>

<span data-ttu-id="fcf3a-114">Habilite a replicação para VMs conforme demonstrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="fcf3a-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="fcf3a-115">Clique em **Replicar aplicativo** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="fcf3a-116">Depois de configurar a replicação pela primeira vez, você pode clicar em **+Replicar** para habilitar a replicação para outros computadores.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-116">After you've set up replication for the first time, you can click **+Replicate** to enable replication for additional machines.</span></span>

    ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="fcf3a-118">Em **Origem**, selecione o site do Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-118">In **Source**, select the Hyper-V site.</span></span> <span data-ttu-id="fcf3a-119">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-119">Then click **OK**.</span></span>
3. <span data-ttu-id="fcf3a-120">Em **Destino**, selecione a assinatura de cofre e o modelo de failover que você deseja usar no Azure (gerenciamento de recursos ou clássico) após o failover.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-120">In **Target**, select the vault subscription, and the failover model you want to use in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="fcf3a-121">Selecione a conta de armazenamento que você deseja usar.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-121">Select the storage account you want to use.</span></span> <span data-ttu-id="fcf3a-122">Se não tiver uma conta que deseje usar, você poderá [criar uma](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="fcf3a-122">If you don't have an account you want to use, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="fcf3a-123">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-123">Then click **OK**.</span></span>
5. <span data-ttu-id="fcf3a-124">Selecione a rede e a sub-rede do Azure às quais as VMs do Azure se conectarão quando forem criadas após o failover.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-124">Select the Azure network and subnet to which Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="fcf3a-125">Selecione **Configurar agora para computadores selecionados** para aplicar a configuração de rede a todos os computadores habilitados para replicação.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-125">To apply the network settings to all machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="fcf3a-126">Selecione **Configurar mais tarde** para selecionar a rede do Azure por computador.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-126">Select **Configure later** to select the Azure network per machine.</span></span>
    - <span data-ttu-id="fcf3a-127">Se não tiver uma rede que deseje usar, você poderá [criar uma](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="fcf3a-127">If you don't have a network you want to use, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="fcf3a-128">Selecione uma sub-rede, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-128">Select a subnet if applicable.</span></span> <span data-ttu-id="fcf3a-129">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-129">Then click **OK**.</span></span>

   ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="fcf3a-131">Em **Máquinas Virtuais** > **Selecionar máquinas virtuais**, clique e selecione cada máquina que você deseja replicar.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want to replicate.</span></span> <span data-ttu-id="fcf3a-132">Você só pode selecionar computadores para os quais a replicação pode ser habilitada.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="fcf3a-133">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-133">Then click **OK**.</span></span>

    ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="fcf3a-135">Em **Propriedades** > **Configurar propriedades**, selecione o sistema operacional para as VMs selecionadas e o disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-135">In **Properties** > **Configure properties**, select the operating system for the selected VMs, and the OS disk.</span></span>
8. <span data-ttu-id="fcf3a-136">Verifique se o nome da VM do Azure (nome de destino) está em conformidade com os [Requisitos de máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="fcf3a-136">Verify that the Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="fcf3a-137">Por padrão, todos os discos da VM são selecionados para replicação.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-137">By default all the disks of the VM are selected for replication.</span></span> <span data-ttu-id="fcf3a-138">Limpar discos para excluí-los.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-138">Clear disks to exclude them.</span></span>
10. <span data-ttu-id="fcf3a-139">Clique em **OK** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-139">Click **OK** to save changes.</span></span> <span data-ttu-id="fcf3a-140">Você pode definir propriedades adicionais posteriormente.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-140">You can set additional properties later.</span></span>

    ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="fcf3a-142">Em **Configurações de replicação** > **Definir configurações de replicação**, selecione a política de replicação que você deseja aplicar para as VMs protegidas.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-142">In **Replication settings** > **Configure replication settings**, select the replication policy you want to apply for the protected VMs.</span></span> <span data-ttu-id="fcf3a-143">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-143">Then click **OK**.</span></span> <span data-ttu-id="fcf3a-144">É possível modificar a política de replicação em **Políticas de replicação** > nome da política > **Editar Configurações**.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-144">You can modify the replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="fcf3a-145">As alterações aplicadas serão usadas para computadores que já estejam replicando e para novas máquinas.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="fcf3a-147">É possível acompanhar o progresso do trabalho **Habilitar Proteção** em **Trabalhos** > **Trabalhos do Site Recovery**.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-147">You can track progress of the **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="fcf3a-148">Após o trabalho de **Finalizar Proteção** ser executado, o computador estará pronto para failover.</span><span class="sxs-lookup"><span data-stu-id="fcf3a-148">After the **Finalize Protection** job runs the machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="fcf3a-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fcf3a-149">Next steps</span></span>


<span data-ttu-id="fcf3a-150">Acesse a [Etapa 11: Executar um failover de teste](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="fcf3a-150">Go to [Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
