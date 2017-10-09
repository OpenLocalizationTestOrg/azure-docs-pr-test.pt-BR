---
title: "a replicação para máquinas virtuais do Hyper-V replicando tooAzure (sem o System Center VMM) com o Azure Site Recovery aaaEnable | Microsoft Docs"
description: "Resume as etapas de saudação necessário tooenable tooAzure de replicação para máquinas virtuais do Hyper-V usando o serviço do Azure Site Recovery Olá"
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
ms.openlocfilehash: 1589cb7aa1fe954e075cb7bf1f4a4ec199ed3ec7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="step-10-enable-replication-for-hyper-v-vms-replicating-tooazure"></a><span data-ttu-id="83083-103">Etapa 10: Habilitar a replicação para máquinas virtuais do Hyper-V replicando tooAzure</span><span class="sxs-lookup"><span data-stu-id="83083-103">Step 10: Enable replication for Hyper-V VMs replicating tooAzure</span></span>


<span data-ttu-id="83083-104">Este artigo descreve como replicação tooenable para local máquinas virtuais de Hyper-V (não gerenciados pelo System Center VMM) tooAzure, usando Olá [do Azure Site Recovery](site-recovery-overview.md) serviço Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="83083-104">This article describes how tooenable replication for on-premises Hyper-V virtual machines (not managed by System Center VMM) tooAzure, using hello [Azure Site Recovery](site-recovery-overview.md) service in hello Azure portal.</span></span>

<span data-ttu-id="83083-105">Postar perguntas e comentários na parte inferior da saudação deste artigo, ou em Olá [Fórum de serviços de recuperação do Azure](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span><span class="sxs-lookup"><span data-stu-id="83083-105">Post comments and questions at hello bottom of this article, or on hello [Azure Recovery Services Forum](https://social.msdn.microsoft.com/forums/azure/home?forum=hypervrecovmgr).</span></span>




## <a name="before-you-start"></a><span data-ttu-id="83083-106">Antes de começar</span><span class="sxs-lookup"><span data-stu-id="83083-106">Before you start</span></span>

<span data-ttu-id="83083-107">Antes de começar, certifique-se de que sua conta de usuário do Azure tem Olá necessário [permissões](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable de replicação de um novo tooAzure de máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="83083-107">Before you start, ensure that your Azure user account has hello required [permissions](site-recovery-role-based-linked-access-control.md#permissions-required-to-enable-replication-for-new-virtual-machines) tooenable replication of a new virtual machine tooAzure.</span></span>

## <a name="exclude-disks-from-replication"></a><span data-ttu-id="83083-108">Excluir discos da replicação</span><span class="sxs-lookup"><span data-stu-id="83083-108">Exclude disks from replication</span></span>

<span data-ttu-id="83083-109">Por padrão, todos os discos em um computador são replicados.</span><span class="sxs-lookup"><span data-stu-id="83083-109">By default all disks on a machine are replicated.</span></span> <span data-ttu-id="83083-110">Você pode excluir discos da replicação.</span><span class="sxs-lookup"><span data-stu-id="83083-110">You can exclude disks from replication.</span></span> <span data-ttu-id="83083-111">Por exemplo, talvez você não queira tooreplicate discos com os dados temporários ou dados que foi atualizada cada vez que uma máquina ou aplicativo reinicia (por exemplo, pagefile.sys ou tempdb do SQL Server).</span><span class="sxs-lookup"><span data-stu-id="83083-111">For example you might not want tooreplicate disks with temporary data, or data that's refreshed each time a machine or application restarts (for example pagefile.sys or SQL Server tempdb).</span></span> [<span data-ttu-id="83083-112">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="83083-112">Learn more</span></span>](site-recovery-exclude-disk.md)


## <a name="replicate-vms"></a><span data-ttu-id="83083-113">Replicar VMs</span><span class="sxs-lookup"><span data-stu-id="83083-113">Replicate VMs</span></span>

<span data-ttu-id="83083-114">Habilite a replicação para VMs conforme demonstrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="83083-114">Enable replication for VMs as follows:</span></span>          

1. <span data-ttu-id="83083-115">Clique em **Replicar aplicativo** > **Origem**.</span><span class="sxs-lookup"><span data-stu-id="83083-115">Click **Replicate application** > **Source**.</span></span> <span data-ttu-id="83083-116">Depois de configurar a replicação para Olá primeira vez, você pode clicar em **+ replicar** tooenable replicação para máquinas adicionais.</span><span class="sxs-lookup"><span data-stu-id="83083-116">After you've set up replication for hello first time, you can click **+Replicate** tooenable replication for additional machines.</span></span>

    ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication.png)
2. <span data-ttu-id="83083-118">Em **fonte**, selecione site Olá Hyper-V.</span><span class="sxs-lookup"><span data-stu-id="83083-118">In **Source**, select hello Hyper-V site.</span></span> <span data-ttu-id="83083-119">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="83083-119">Then click **OK**.</span></span>
3. <span data-ttu-id="83083-120">Em **destino**, selecione a assinatura do cofre hello e Olá failover modelo toouse no Azure (clássico ou o recurso de gerenciamento) após o failover.</span><span class="sxs-lookup"><span data-stu-id="83083-120">In **Target**, select hello vault subscription, and hello failover model you want toouse in Azure (classic or resource management) after failover.</span></span>
4. <span data-ttu-id="83083-121">Selecione a conta de armazenamento de saudação que toouse desejado.</span><span class="sxs-lookup"><span data-stu-id="83083-121">Select hello storage account you want toouse.</span></span> <span data-ttu-id="83083-122">Se você não tiver uma conta que você deseja toouse, você pode [criar um](#set-up-an-azure-storage-account).</span><span class="sxs-lookup"><span data-stu-id="83083-122">If you don't have an account you want toouse, you can [create one](#set-up-an-azure-storage-account).</span></span> <span data-ttu-id="83083-123">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="83083-123">Then click **OK**.</span></span>
5. <span data-ttu-id="83083-124">Selecione Olá toowhich de rede e sub-rede do Azure VMs do Azure se conectará quando eles são criados o failover.</span><span class="sxs-lookup"><span data-stu-id="83083-124">Select hello Azure network and subnet toowhich Azure VMs will connect when they're created failover.</span></span>

    - <span data-ttu-id="83083-125">Selecione tooapply Olá configurações tooall máquinas de rede habilitar para replicação, **configurar agora para os computadores selecionados**.</span><span class="sxs-lookup"><span data-stu-id="83083-125">tooapply hello network settings tooall machines you enable for replication, select **Configure now for selected machines**.</span></span>
    - <span data-ttu-id="83083-126">Selecione **configurar posteriormente** tooselect Olá rede do Azure por máquina.</span><span class="sxs-lookup"><span data-stu-id="83083-126">Select **Configure later** tooselect hello Azure network per machine.</span></span>
    - <span data-ttu-id="83083-127">Se você não tiver uma rede que você deseja toouse, você pode [criar um](#set-up-an-azure-network).</span><span class="sxs-lookup"><span data-stu-id="83083-127">If you don't have a network you want toouse, you can [create one](#set-up-an-azure-network).</span></span> <span data-ttu-id="83083-128">Selecione uma sub-rede, se aplicável.</span><span class="sxs-lookup"><span data-stu-id="83083-128">Select a subnet if applicable.</span></span> <span data-ttu-id="83083-129">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="83083-129">Then click **OK**.</span></span>

   ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication11.png)

6. <span data-ttu-id="83083-131">Em **máquinas virtuais** > **selecionar máquinas virtuais**, clique em e selecione cada máquina que você deseja tooreplicate.</span><span class="sxs-lookup"><span data-stu-id="83083-131">In **Virtual Machines** > **Select virtual machines**, click and select each machine you want tooreplicate.</span></span> <span data-ttu-id="83083-132">Você só pode selecionar computadores para os quais a replicação pode ser habilitada.</span><span class="sxs-lookup"><span data-stu-id="83083-132">You can only select machines for which replication can be enabled.</span></span> <span data-ttu-id="83083-133">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="83083-133">Then click **OK**.</span></span>

    ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication5-for-exclude-disk.png)

7. <span data-ttu-id="83083-135">Em **propriedades** > **configurar propriedades**, selecione o sistema operacional de saudação para VMs Olá selecionado e Olá disco do sistema operacional.</span><span class="sxs-lookup"><span data-stu-id="83083-135">In **Properties** > **Configure properties**, select hello operating system for hello selected VMs, and hello OS disk.</span></span>
8. <span data-ttu-id="83083-136">Verifique se esse nome de VM do Azure hello (nome de destino) está em conformidade com [requisitos da máquina virtual do Azure](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span><span class="sxs-lookup"><span data-stu-id="83083-136">Verify that hello Azure VM name (target name) complies with [Azure virtual machine requirements](site-recovery-support-matrix-to-azure.md#failed-over-azure-vm-requirements).</span></span>
9. <span data-ttu-id="83083-137">Por padrão, todos os discos de saudação da saudação VM são selecionados para replicação.</span><span class="sxs-lookup"><span data-stu-id="83083-137">By default all hello disks of hello VM are selected for replication.</span></span> <span data-ttu-id="83083-138">Limpar discos tooexclude-los.</span><span class="sxs-lookup"><span data-stu-id="83083-138">Clear disks tooexclude them.</span></span>
10. <span data-ttu-id="83083-139">Clique em **Okey** toosave alterações.</span><span class="sxs-lookup"><span data-stu-id="83083-139">Click **OK** toosave changes.</span></span> <span data-ttu-id="83083-140">Você pode definir propriedades adicionais posteriormente.</span><span class="sxs-lookup"><span data-stu-id="83083-140">You can set additional properties later.</span></span>

    ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication6-with-exclude-disk.png)

11. <span data-ttu-id="83083-142">Em **as configurações de replicação** > **definir configurações de replicação**, selecione Olá política de replicação você deseja tooapply para Olá protegido VMs.</span><span class="sxs-lookup"><span data-stu-id="83083-142">In **Replication settings** > **Configure replication settings**, select hello replication policy you want tooapply for hello protected VMs.</span></span> <span data-ttu-id="83083-143">Em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="83083-143">Then click **OK**.</span></span> <span data-ttu-id="83083-144">Você pode modificar a política de replicação de saudação em **políticas de replicação** > nome da política > **editar configurações de**.</span><span class="sxs-lookup"><span data-stu-id="83083-144">You can modify hello replication policy in **Replication policies** > policy-name > **Edit Settings**.</span></span> <span data-ttu-id="83083-145">As alterações aplicadas serão usadas para computadores que já estejam replicando e para novas máquinas.</span><span class="sxs-lookup"><span data-stu-id="83083-145">Changes you apply will be used for machines that are already replicating, and new machines.</span></span>


   ![Habilitar a replicação](./media/hyper-v-site-walkthrough-enable-replication/enable-replication7.png)

<span data-ttu-id="83083-147">Você pode acompanhar o progresso da saudação **Habilitar proteção** trabalho em **trabalhos** > **trabalhos de recuperação de Site**.</span><span class="sxs-lookup"><span data-stu-id="83083-147">You can track progress of hello **Enable Protection** job in **Jobs** > **Site Recovery jobs**.</span></span> <span data-ttu-id="83083-148">Depois de saudação **finalizar proteção** execuções de trabalho máquina hello está pronta para failover.</span><span class="sxs-lookup"><span data-stu-id="83083-148">After hello **Finalize Protection** job runs hello machine is ready for failover.</span></span>


## <a name="next-steps"></a><span data-ttu-id="83083-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="83083-149">Next steps</span></span>


<span data-ttu-id="83083-150">Vá muito[etapa 11: executar um failover de teste](hyper-v-site-walkthrough-test-failover.md)</span><span class="sxs-lookup"><span data-stu-id="83083-150">Go too[Step 11: Run a test failover](hyper-v-site-walkthrough-test-failover.md)</span></span>
