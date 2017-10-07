---
title: "monitor e aaaManage backups de máquina virtual do Azure | Microsoft Docs"
description: "Saiba como monitor virtual do Azure e toomanage máquina backups"
services: backup
documentationcenter: 
author: trinadhk
manager: shreeshd
editor: 
ms.assetid: 4372944e-d33a-4f6a-bd5f-d04af2842713
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: trinadhk;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: cb95e0b3760c96f7fd563c42cb4c635553f48957
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-hello-classic-portal"></a><span data-ttu-id="66004-103">Gerenciar trabalhos de Backup do Azure comuns e os alertas de disparador no portal clássico Olá</span><span class="sxs-lookup"><span data-stu-id="66004-103">Manage common Azure Backup jobs and trigger alerts in hello classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="66004-104">Gerenciar backups da VM do Azure</span><span class="sxs-lookup"><span data-stu-id="66004-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="66004-105">Gerenciar backups de VMs clássicas</span><span class="sxs-lookup"><span data-stu-id="66004-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="66004-106">Este artigo fornece informações sobre tarefas comuns de gerenciamento e monitoramento para máquinas virtuais do modelo Clássico protegidas no Azure.</span><span class="sxs-lookup"><span data-stu-id="66004-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="66004-107">O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="66004-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="66004-108">Consulte [preparar seu tooback ambiente backup de máquinas virtuais do Azure](backup-azure-vms-prepare.md) para obter detalhes sobre como trabalhar com implantação clássico VMs de modelo.</span><span class="sxs-lookup"><span data-stu-id="66004-108">See [Prepare your environment tooback up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="66004-109">A partir de março de 2017, você não pode usar os cofres de Backup Olá toocreate portal clássico.</span><span class="sxs-lookup"><span data-stu-id="66004-109">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
>
> <span data-ttu-id="66004-110">Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="66004-110">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="66004-111">Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="66004-111">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="66004-112">A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="66004-112">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="66004-113">Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="66004-113">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="66004-114">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="66004-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="66004-115">Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.</span><span class="sxs-lookup"><span data-stu-id="66004-115">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="66004-116">Você não será capaz de tooaccess os dados de backup no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="66004-116">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="66004-117">Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="66004-117">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="66004-118">Gerenciar máquinas virtuais protegidas</span><span class="sxs-lookup"><span data-stu-id="66004-118">Manage protected virtual machines</span></span>
<span data-ttu-id="66004-119">toomanage máquinas virtuais protegidas:</span><span class="sxs-lookup"><span data-stu-id="66004-119">toomanage protected virtual machines:</span></span>

1. <span data-ttu-id="66004-120">tooview e gerenciar as configurações de backup para uma máquina virtual, clique em Olá **itens protegidos** guia.</span><span class="sxs-lookup"><span data-stu-id="66004-120">tooview and manage backup settings for a virtual machine click hello **Protected Items** tab.</span></span>
2. <span data-ttu-id="66004-121">Clique no nome de saudação de uma saudação do item protegido toosee **detalhes de Backup** guia, que mostra informações sobre o último backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="66004-121">Click on hello name of a protected item toosee hello **Backup Details** tab, which shows you information about hello last backup.</span></span>

    ![Backup de máquinas virtuais](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="66004-123">tooview e gerenciar configurações de política de backup para uma máquina virtual, clique em Olá **políticas** guia.</span><span class="sxs-lookup"><span data-stu-id="66004-123">tooview and manage backup policy settings for a virtual machine click hello **Policies** tab.</span></span>

    ![Política de máquina virtual](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="66004-125">Olá **políticas de Backup** guia mostra Olá política existente.</span><span class="sxs-lookup"><span data-stu-id="66004-125">hello **Backup Policies** tab shows you hello existing policy.</span></span> <span data-ttu-id="66004-126">Você pode modificar conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="66004-126">You can modify as needed.</span></span> <span data-ttu-id="66004-127">Se você precisar de uma nova política de toocreate clique **criar** em Olá **políticas** página.</span><span class="sxs-lookup"><span data-stu-id="66004-127">If you need toocreate a new policy click **Create** on hello **Policies** page.</span></span> <span data-ttu-id="66004-128">Observe que se você quiser tooremove uma política de ele não deve ter todas as máquinas virtuais associadas a ele.</span><span class="sxs-lookup"><span data-stu-id="66004-128">Note that if you want tooremove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Política de máquina virtual](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="66004-130">Você pode obter mais informações sobre ações ou status para uma máquina virtual em Olá **trabalhos** página.</span><span class="sxs-lookup"><span data-stu-id="66004-130">You can get more information about actions or status for a virtual machine on hello **Jobs** page.</span></span> <span data-ttu-id="66004-131">Clique em um trabalho em Olá lista tooget mais detalhes, ou filtre os trabalhos para uma máquina virtual específica.</span><span class="sxs-lookup"><span data-stu-id="66004-131">Click a job in hello list tooget more details, or filter jobs for a specific virtual machine.</span></span>

    ![Trabalhos](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="66004-133">Backup sob demanda de uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="66004-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="66004-134">Você pode obter um backup sob demanda de uma máquina virtual quando ela estiver configurada para proteção.</span><span class="sxs-lookup"><span data-stu-id="66004-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="66004-135">Se o backup de saudação inicial está pendente para a máquina virtual de hello, backup sob demanda criará uma cópia completa da máquina virtual de saudação no cofre de backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="66004-135">If hello initial backup is pending for hello virtual machine, on-demand backup will create a full copy of hello virtual machine in Azure backup vault.</span></span> <span data-ttu-id="66004-136">Se o primeiro backup for concluído, será backup sob demanda somente alterações de envio do backup anterior de backup tooAzure cofre ou seja, ele é sempre incremental.</span><span class="sxs-lookup"><span data-stu-id="66004-136">If first backup is completed, on-demand backup will only send changes from previous backup tooAzure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="66004-137">Período de retenção de um backup sob demanda é definir o valor de tooretention especificado para retenção diária na política de backup correspondente toohello VM.</span><span class="sxs-lookup"><span data-stu-id="66004-137">Retention range of an on-demand backup is set tooretention value specified for Daily retention in backup policy corresponding toohello VM.</span></span>  
>
>

<span data-ttu-id="66004-138">backup tootake uma demanda de uma máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="66004-138">tootake an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="66004-139">Navegue toohello **itens protegidos** página e selecione **Máquina Virtual do Azure** como **tipo** (se ainda não estiver selecionado) e clique em **selecione**botão.</span><span class="sxs-lookup"><span data-stu-id="66004-139">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![Tipo de VM](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="66004-141">Selecionar máquina virtual de saudação na qual você deseja tootake uma demanda backup e clique em **Backup agora** botão final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="66004-141">Select hello virtual machine on which you want tootake an on-demand backup and click on **Backup Now** button at hello bottom of hello page.</span></span>

    ![Fazer backup agora](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="66004-143">Isso criará um trabalho de backup na máquina virtual de saudação selecionada.</span><span class="sxs-lookup"><span data-stu-id="66004-143">This will create a backup job on hello selected virtual machine.</span></span> <span data-ttu-id="66004-144">Período de retenção de ponto de recuperação criado por esse trabalho será o mesmo que a especificada na política de saudação associada à máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="66004-144">Retention range of recovery point created through this job will be same as that specified in hello policy associated with hello virtual machine.</span></span>

    ![Criando um trabalho de backup](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="66004-146">política de saudação tooview associada a uma máquina virtual, detalhada para baixo em máquina virtual no hello **itens protegidos** guia de política de toobackup vá e página.</span><span class="sxs-lookup"><span data-stu-id="66004-146">tooview hello policy associated with a virtual machine, drill down into virtual machine in hello **Protected Items** page and go toobackup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="66004-147">Quando o trabalho de saudação é criado, você pode clicar em **Exibir trabalho** botão torrada Olá barra toosee trabalho correspondente do hello na página de trabalhos de saudação.</span><span class="sxs-lookup"><span data-stu-id="66004-147">Once hello job is created, you can click on **View job** button in hello toast bar toosee hello corresponding job in hello jobs page.</span></span>

    ![Trabalho de backup criado](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="66004-149">Após a conclusão bem-sucedida do trabalho hello, um ponto de recuperação será criado que você pode usar toorestore Olá VM.</span><span class="sxs-lookup"><span data-stu-id="66004-149">After successful completion of hello job, a recovery point will be created which you can use toorestore hello virtual machine.</span></span> <span data-ttu-id="66004-150">Isso também será incrementado valor de coluna de ponto de recuperação Olá por 1 na **itens protegidos** página.</span><span class="sxs-lookup"><span data-stu-id="66004-150">This will also increment hello recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="66004-151">Interromper a proteção de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="66004-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="66004-152">Você pode escolher toostop futuros backups saudação de uma máquina virtual com hello as opções a seguir:</span><span class="sxs-lookup"><span data-stu-id="66004-152">You can choose toostop hello future backups of a virtual machine with hello following options:</span></span>

* <span data-ttu-id="66004-153">Reter dados de backup associados à máquina virtual no cofre de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="66004-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="66004-154">Excluir dados de backup associados à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="66004-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="66004-155">Se você tiver selecionado dados de backup tooretain associados à máquina virtual, você pode usar a máquina virtual do hello dados de backup toorestore Olá.</span><span class="sxs-lookup"><span data-stu-id="66004-155">If you have selected tooretain backup data associated with virtual machine, you can use hello backup data toorestore hello virtual machine.</span></span> <span data-ttu-id="66004-156">Para obter detalhes de preço dessas máquinas virtuais, clique [aqui](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="66004-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="66004-157">proteção de tooStop para uma máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="66004-157">tooStop protection for a virtual machine:</span></span>

1. <span data-ttu-id="66004-158">Navegue muito**itens protegidos** página e selecione **máquina virtual do Azure** como tipo de filtro da saudação (se ainda não estiver selecionado) e clique em **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="66004-158">Navigate too**Protected Items** page and select **Azure virtual machine** as hello filter type (if not already selected) and click on **Select** button.</span></span>

    ![Tipo de VM](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="66004-160">Selecione a máquina virtual de saudação e clique em **parar proteção** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="66004-160">Select hello virtual machine and click on **Stop Protection** at hello bottom of hello page.</span></span>

    ![Parar a proteção](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="66004-162">Por padrão, Backup do Azure não excluir os dados de backup Olá associados à máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="66004-162">By default, Azure Backup doesn’t delete hello backup data associated with hello virtual machine.</span></span>

    ![Confirmar a interrupção da proteção](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="66004-164">Se você quiser toodelete dados de backup, marque a caixa de seleção de saudação.</span><span class="sxs-lookup"><span data-stu-id="66004-164">If you want toodelete backup data, select hello check box.</span></span>

    ![Caixa de seleção](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="66004-166">Selecione um motivo para interromper o backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="66004-166">Please select a reason for stopping hello backup.</span></span> <span data-ttu-id="66004-167">Enquanto isso é opcional, fornecer um motivo ajuda toowork de Backup do Azure nos comentários de saudação e priorizar os cenários de cliente Olá.</span><span class="sxs-lookup"><span data-stu-id="66004-167">While this is optional, providing a reason will help Azure Backup toowork on hello feedback and prioritize hello customer scenarios.</span></span>
4. <span data-ttu-id="66004-168">Clique em **enviar** saudação do botão toosubmit **interromper a proteção** trabalho.</span><span class="sxs-lookup"><span data-stu-id="66004-168">Click on **Submit** button toosubmit hello **Stop protection** job.</span></span> <span data-ttu-id="66004-169">Clique em **Exibir trabalho** toosee Olá trabalho Olá correspondente em **trabalhos** página.</span><span class="sxs-lookup"><span data-stu-id="66004-169">Click on **View Job** toosee hello corresponding hello job in **Jobs** page.</span></span>

    ![Parar a proteção](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="66004-171">Se você não selecionou **excluir os dados de backup associados** opção durante **parar proteção** proteção Assistente e, em seguida, após a conclusão do trabalho, status muda muito**proteção interrompida**.</span><span class="sxs-lookup"><span data-stu-id="66004-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes too**Protection Stopped**.</span></span> <span data-ttu-id="66004-172">dados de saudação permanecem com o Azure Backup até que sejam excluídas explicitamente.</span><span class="sxs-lookup"><span data-stu-id="66004-172">hello data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="66004-173">Você sempre pode excluir dados saudação, selecionando a máquina virtual de saudação no hello **itens protegidos** página e clicando em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="66004-173">You can always delete hello data by selecting hello virtual machine in hello **Protected Items** page and clicking **Delete**.</span></span>

    ![Proteção interrompida](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="66004-175">Se você tiver selecionado Olá **excluir os dados de backup associados** opção, hello máquina virtual não fará parte dos Olá **itens protegidos** página.</span><span class="sxs-lookup"><span data-stu-id="66004-175">If you have selected hello **Delete associated backup data** option, hello virtual machine won’t be part of hello **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="66004-176">Proteger novamente a Máquina virtual</span><span class="sxs-lookup"><span data-stu-id="66004-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="66004-177">Se você não selecionou Olá **excluir dados de backup associados** opção **parar proteção**, proteger máquina virtual de saudação novamente seguindo Olá etapas semelhantes toobacking backup registrado virtual máquinas.</span><span class="sxs-lookup"><span data-stu-id="66004-177">If you have not selected hello **Delete associate backup data** option in **Stop Protection**, you can re-protect hello virtual machine by following hello steps similar toobacking up registered virtual machines.</span></span> <span data-ttu-id="66004-178">Depois de protegido, esta máquina virtual terá proteção do backup de dados retidos toostop anterior e pontos de recuperação criado após protege novamente.</span><span class="sxs-lookup"><span data-stu-id="66004-178">Once protected, this virtual machine will have backup data retained prior toostop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="66004-179">Depois de proteger novamente, o status de proteção da máquina de virtual Olá será alterado muito**protegidos** se houver pontos de recuperação anterior muito**parar proteção**.</span><span class="sxs-lookup"><span data-stu-id="66004-179">After re-protect, hello virtual machine’s protection status will be changed too**Protected** if there are recovery points prior too**Stop Protection**.</span></span>

  ![Máquina virtual protegida novamente](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="66004-181">Ao proteger novamente a máquina virtual de hello, você pode escolher uma regra diferente que a política de saudação com a qual a máquina virtual foi inicialmente protegida.</span><span class="sxs-lookup"><span data-stu-id="66004-181">When re-protecting hello virtual machine, you can choose a different policy than hello policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="66004-182">Cancelar o registro das máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="66004-182">Unregister virtual machines</span></span>
<span data-ttu-id="66004-183">Se você desejar tooremove Olá máquina de virtual do Cofre de backup hello:</span><span class="sxs-lookup"><span data-stu-id="66004-183">If you want tooremove hello virtual machine from hello backup vault:</span></span>

1. <span data-ttu-id="66004-184">Clique em Olá **UNREGISTER** botão final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="66004-184">Click on hello **UNREGISTER** button at hello bottom of hello page.</span></span>

    ![Desabilitar a proteção](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="66004-186">Uma notificação do sistema será exibido na parte inferior da saudação da tela hello solicitando a confirmação.</span><span class="sxs-lookup"><span data-stu-id="66004-186">A toast notification will appear at hello bottom of hello screen requesting confirmation.</span></span> <span data-ttu-id="66004-187">Clique em **Sim** toocontinue.</span><span class="sxs-lookup"><span data-stu-id="66004-187">Click **YES** toocontinue.</span></span>

    ![Desabilitar a proteção](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="66004-189">Excluir dados de backup</span><span class="sxs-lookup"><span data-stu-id="66004-189">Delete Backup data</span></span>
<span data-ttu-id="66004-190">Você pode excluir os dados de backup Olá associados a uma máquina virtual, ou:</span><span class="sxs-lookup"><span data-stu-id="66004-190">You can delete hello backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="66004-191">Durante a interrupção do trabalho da proteção</span><span class="sxs-lookup"><span data-stu-id="66004-191">During Stop Protection Job</span></span>
* <span data-ttu-id="66004-192">Após uma interrupção no trabalho de proteção ser concluída em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="66004-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="66004-193">toodelete dados de backup em uma máquina virtual, que está na saudação *proteção interrompida* estado após a conclusão bem-sucedida de um **parar Backup** trabalho:</span><span class="sxs-lookup"><span data-stu-id="66004-193">toodelete backup data on a virtual machine, which is in hello *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="66004-194">Navegue toohello **itens protegidos** página e selecione **Máquina Virtual do Azure** como *tipo* e clique em Olá **selecione** botão.</span><span class="sxs-lookup"><span data-stu-id="66004-194">Navigate toohello **Protected Items** page and select **Azure Virtual Machine** as *type* and click hello **Select** button.</span></span>

    ![Tipo de VM](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="66004-196">Selecione a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="66004-196">Select hello virtual machine.</span></span> <span data-ttu-id="66004-197">máquina virtual de saudação estará em **proteção interrompida** estado.</span><span class="sxs-lookup"><span data-stu-id="66004-197">hello virtual machine will be in **Protection Stopped** state.</span></span>

    ![Proteção interrompida](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="66004-199">Clique em Olá **excluir** botão final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="66004-199">Click hello **DELETE** button at hello bottom of hello page.</span></span>

    ![Excluir backup](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="66004-201">Em Olá **excluir dados de backup** assistente, selecione um motivo para a exclusão de dados de backup (recomendados) e clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="66004-201">In hello **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![Excluir dados de backup](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="66004-203">Isso criará um trabalho toodelete backup de dados de máquina virtual selecionada.</span><span class="sxs-lookup"><span data-stu-id="66004-203">This will create a job toodelete backup data of selected virtual machine.</span></span> <span data-ttu-id="66004-204">Clique em **Exibir trabalho** toosee o trabalho correspondente na página trabalhos.</span><span class="sxs-lookup"><span data-stu-id="66004-204">Click **View job** toosee corresponding job in Jobs page.</span></span>

    ![Exclusão de dados bem-sucedida](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="66004-206">Após a conclusão do trabalho hello, Olá entrada de máquina virtual de toohello correspondente será removida do **itens protegidos** página.</span><span class="sxs-lookup"><span data-stu-id="66004-206">Once hello job is completed, hello entry corresponding toohello virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="66004-207">Painel</span><span class="sxs-lookup"><span data-stu-id="66004-207">Dashboard</span></span>
<span data-ttu-id="66004-208">Em Olá **painel** página você pode examinar informações sobre máquinas virtuais do Azure, armazenamento e trabalhos associados a eles no hello últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="66004-208">On hello **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in hello last 24 hours.</span></span> <span data-ttu-id="66004-209">Você pode exibir o status de backup e quaisquer erros de backup associados.</span><span class="sxs-lookup"><span data-stu-id="66004-209">You can view backup status and any associated backup errors.</span></span>

![Painel](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="66004-211">Os valores no painel de saudação são atualizados uma vez a cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="66004-211">Values in hello dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="66004-212">Operações de auditoria</span><span class="sxs-lookup"><span data-stu-id="66004-212">Auditing Operations</span></span>
<span data-ttu-id="66004-213">O backup do Azure fornece análise de hello "logs de operação" das operações de backup disparados por cliente Olá tornando fácil toosee exatamente quais operações de gerenciamento foram realizadas no cofre de backup hello.</span><span class="sxs-lookup"><span data-stu-id="66004-213">Azure backup provides review of hello "operation logs" of backup operations triggered by hello customer making it easy toosee exactly what management operations were performed on hello backup vault.</span></span> <span data-ttu-id="66004-214">Logs de operações habilitar post-mortem grande e suporte para operações de backup de saudação de auditoria.</span><span class="sxs-lookup"><span data-stu-id="66004-214">Operations logs enable great post-mortem and audit support for hello backup operations.</span></span>

<span data-ttu-id="66004-215">Olá operações a seguir é registrada nos logs de operação:</span><span class="sxs-lookup"><span data-stu-id="66004-215">hello following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="66004-216">Registrar</span><span class="sxs-lookup"><span data-stu-id="66004-216">Register</span></span>
* <span data-ttu-id="66004-217">Cancelar o registro </span><span class="sxs-lookup"><span data-stu-id="66004-217">Unregister</span></span>
* <span data-ttu-id="66004-218">Configurar a proteção</span><span class="sxs-lookup"><span data-stu-id="66004-218">Configure protection</span></span>
* <span data-ttu-id="66004-219">Backup (tanto as agendadas quanto as sob demanda por meio do BackupNow)</span><span class="sxs-lookup"><span data-stu-id="66004-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="66004-220">Restaurar</span><span class="sxs-lookup"><span data-stu-id="66004-220">Restore</span></span>
* <span data-ttu-id="66004-221">Parar a proteção</span><span class="sxs-lookup"><span data-stu-id="66004-221">Stop protection</span></span>
* <span data-ttu-id="66004-222">Excluir dados de backup</span><span class="sxs-lookup"><span data-stu-id="66004-222">Delete backup data</span></span>
* <span data-ttu-id="66004-223">Adicionar política</span><span class="sxs-lookup"><span data-stu-id="66004-223">Add policy</span></span>
* <span data-ttu-id="66004-224">Excluir política</span><span class="sxs-lookup"><span data-stu-id="66004-224">Delete policy</span></span>
* <span data-ttu-id="66004-225">Atualizar política</span><span class="sxs-lookup"><span data-stu-id="66004-225">Update policy</span></span>
* <span data-ttu-id="66004-226">Cancelar trabalho</span><span class="sxs-lookup"><span data-stu-id="66004-226">Cancel job</span></span>

<span data-ttu-id="66004-227">Cofre de backup correspondente tooa logs da operação de tooview:</span><span class="sxs-lookup"><span data-stu-id="66004-227">tooview operation logs corresponding tooa backup vault:</span></span>

1. <span data-ttu-id="66004-228">Navegue muito**serviços de gerenciamento de** no portal do Azure e, em seguida, clique em Olá **Logs de operação** guia.</span><span class="sxs-lookup"><span data-stu-id="66004-228">Navigate too**Management services** in Azure portal, and then click hello **Operation Logs** tab.</span></span>

    ![Logs de operação](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="66004-230">Em filtros de saudação, selecione **Backup** como *tipo* e especifique o nome do Cofre de backup Olá na *nome do serviço* e clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="66004-230">In hello filters, select **Backup** as *Type* and specify hello backup vault name in *service name* and click on **Submit**.</span></span>

    ![Filtro de logs de operação](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="66004-232">Nos logs de operações de saudação, selecione qualquer operação e clique em **detalhes** toosee detalhes de operação tooan correspondente.</span><span class="sxs-lookup"><span data-stu-id="66004-232">In hello operations logs, select any operation and click  **Details** toosee details corresponding tooan operation.</span></span>

    ![Detalhes de busca de logs de operação](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="66004-234">Olá **Assistente detalhes** contém informações sobre a operação Olá disparada, o Id de recurso em que essa operação é disparada e hora de início da operação de saudação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="66004-234">hello **Details wizard** contains information about hello operation triggered, job Id, resource on which this operation is triggered, and start time of hello operation.</span></span>

    ![Detalhes da Operação](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="66004-236">Notificações de alerta</span><span class="sxs-lookup"><span data-stu-id="66004-236">Alert notifications</span></span>
<span data-ttu-id="66004-237">Você pode obter notificações de alerta personalizadas para trabalhos de saudação no portal.</span><span class="sxs-lookup"><span data-stu-id="66004-237">You can get custom alert notifications for hello jobs in portal.</span></span> <span data-ttu-id="66004-238">Isso é possível ao definir regras de alerta do PowerShell baseadas em eventos de logs operacionais.</span><span class="sxs-lookup"><span data-stu-id="66004-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="66004-239">É recomendável usar o *PowerShell versão 1.3.0 ou superior*.</span><span class="sxs-lookup"><span data-stu-id="66004-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="66004-240">toodefine tooalert uma notificação personalizada para falhas de backup, um comando de exemplo será semelhante:</span><span class="sxs-lookup"><span data-stu-id="66004-240">toodefine a custom notification tooalert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="66004-241">**ResourceId**: você pode obter isso no pop-up Logs de Operações, conforme descrito na seção acima.</span><span class="sxs-lookup"><span data-stu-id="66004-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="66004-242">ResourceUri na janela pop-up de detalhes de uma operação é Olá ResourceId toobe fornecido para este cmdlet.</span><span class="sxs-lookup"><span data-stu-id="66004-242">ResourceUri in details popup window of an operation is hello ResourceId toobe supplied for this cmdlet.</span></span>

<span data-ttu-id="66004-243">**OperationName**: esse será o formato de saudação "Microsoft.Backup/backupvault/<EventName>" onde EventName um de registrar, cancelar registro, ConfigureProtection, Backup, restauração, StopProtection, DeleteBackupData, CreateProtectionPolicy, DeleteProtectionPolicy, UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="66004-243">**OperationName**: This will be of hello format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="66004-244">**Status**: os valores com suporte são Started, Succeeded e Failed.</span><span class="sxs-lookup"><span data-stu-id="66004-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="66004-245">**ResourceGroup**: grupo de recursos do recurso de saudação no qual a operação é disparada.</span><span class="sxs-lookup"><span data-stu-id="66004-245">**ResourceGroup**:ResourceGroup of hello resource on which operation is triggered.</span></span> <span data-ttu-id="66004-246">Você pode obter isso do valor ResourceId.</span><span class="sxs-lookup"><span data-stu-id="66004-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="66004-247">Valor entre campos */resourceGroups/* e */providers/* em ResourceId valor é o valor de saudação para o grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="66004-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is hello value for ResourceGroup.</span></span>

<span data-ttu-id="66004-248">**Nome**: nome da regra de alerta de saudação.</span><span class="sxs-lookup"><span data-stu-id="66004-248">**Name**: Name of hello Alert Rule.</span></span>

<span data-ttu-id="66004-249">**CustomEmail**: especificar Olá email personalizado endereço toowhich deseja toosend notificação de alerta</span><span class="sxs-lookup"><span data-stu-id="66004-249">**CustomEmail**: Specify hello custom email address toowhich you want toosend alert notification</span></span>

<span data-ttu-id="66004-250">**SendToServiceOwners**: essa opção envia os administradores tooall de notificação de alerta e os coadministradores de assinatura de saudação.</span><span class="sxs-lookup"><span data-stu-id="66004-250">**SendToServiceOwners**: This option sends alert notification tooall administrators and co-administrators of hello subscription.</span></span> <span data-ttu-id="66004-251">Pode ser usado no cmdlet **New-AzureRmAlertRuleEmail**</span><span class="sxs-lookup"><span data-stu-id="66004-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="66004-252">Limitações sobre alertas</span><span class="sxs-lookup"><span data-stu-id="66004-252">Limitations on Alerts</span></span>
<span data-ttu-id="66004-253">Alertas baseados em eventos estão sujeito toohello seguintes limitações:</span><span class="sxs-lookup"><span data-stu-id="66004-253">Event-based alerts are subjected toohello following limitations:</span></span>

1. <span data-ttu-id="66004-254">Os alertas são disparados em todas as máquinas virtuais no cofre de backup hello.</span><span class="sxs-lookup"><span data-stu-id="66004-254">Alerts are triggered on all virtual machines in hello backup vault.</span></span> <span data-ttu-id="66004-255">Você não é possível personalizá-lo tooget alertas para um conjunto específico de máquinas virtuais em um cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="66004-255">You cannot customize it tooget alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="66004-256">Esse recurso está em Preview.</span><span class="sxs-lookup"><span data-stu-id="66004-256">This feature is in Preview.</span></span> [<span data-ttu-id="66004-257">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="66004-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="66004-258">Você receberá alertas de “alerts-noreply@mail.windowsazure.com”.</span><span class="sxs-lookup"><span data-stu-id="66004-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="66004-259">Atualmente você não pode modificar o remetente do email hello.</span><span class="sxs-lookup"><span data-stu-id="66004-259">Currently you can't modify hello email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="66004-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="66004-260">Next steps</span></span>
* [<span data-ttu-id="66004-261">Restaurar máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="66004-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
