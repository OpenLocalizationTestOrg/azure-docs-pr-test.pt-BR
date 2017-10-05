---
title: "Gerenciar e monitorar backups de máquinas virtuais do Azure | Microsoft Docs"
description: "Saiba como gerenciar e monitorar backups de uma máquina virtual do Azure"
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
ms.openlocfilehash: d876bb1759600fa29a26730bfa8b4ec19db1e442
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="manage-common-azure-backup-jobs-and-trigger-alerts-in-the-classic-portal"></a><span data-ttu-id="60870-103">Gerenciar trabalhos comuns do Backup do Azure e disparar alertas no portal clássico</span><span class="sxs-lookup"><span data-stu-id="60870-103">Manage common Azure Backup jobs and trigger alerts in the classic portal</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="60870-104">Gerenciar backups da VM do Azure</span><span class="sxs-lookup"><span data-stu-id="60870-104">Manage Azure VM backups</span></span>](backup-azure-manage-vms.md)
> * [<span data-ttu-id="60870-105">Gerenciar backups de VMs clássicas</span><span class="sxs-lookup"><span data-stu-id="60870-105">Manage Classic VM backups</span></span>](backup-azure-manage-vms-classic.md)
>
>

<span data-ttu-id="60870-106">Este artigo fornece informações sobre tarefas comuns de gerenciamento e monitoramento para máquinas virtuais do modelo Clássico protegidas no Azure.</span><span class="sxs-lookup"><span data-stu-id="60870-106">This article provides information about common management and monitoring tasks for Classic-model virtual machines protected in Azure.</span></span>  

> [!NOTE]
> <span data-ttu-id="60870-107">O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="60870-107">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="60870-108">Consulte [Preparar seu ambiente para fazer backup de máquinas virtuais do Azure](backup-azure-vms-prepare.md) para obter detalhes sobre como trabalhar com VMs do modelo de implantação Clássico.</span><span class="sxs-lookup"><span data-stu-id="60870-108">See [Prepare your environment to back up Azure virtual machines](backup-azure-vms-prepare.md) for details on working with Classic deployment model VMs.</span></span>
>
> [!IMPORTANT]
><span data-ttu-id="60870-109">A partir de março de 2017, você não poderá mais usar o portal clássico para criar os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="60870-109">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
>
> <span data-ttu-id="60870-110">Agora você pode atualizar os cofres de Backup para cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="60870-110">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="60870-111">Para obter detalhes, veja o artigo [Atualizar um cofre de Backup para um cofre dos Serviços de Recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="60870-111">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="60870-112">A Microsoft incentiva você a atualizar os cofres de Backup para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="60870-112">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="60870-113">Após 15 de outubro de 2017, você não poderá usar o PowerShell para criar os Cofres do Backup.</span><span class="sxs-lookup"><span data-stu-id="60870-113">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="60870-114">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="60870-114">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="60870-115">Todos os Cofres do Backup restantes serão atualizados automaticamente para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="60870-115">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="60870-116">Você não poderá acessar os dados de backup no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="60870-116">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="60870-117">Em vez disso, use o portal do Azure para acessar os dados de backup nos cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="60870-117">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>

## <a name="manage-protected-virtual-machines"></a><span data-ttu-id="60870-118">Gerenciar máquinas virtuais protegidas</span><span class="sxs-lookup"><span data-stu-id="60870-118">Manage protected virtual machines</span></span>
<span data-ttu-id="60870-119">Para gerenciar máquinas virtuais protegidas:</span><span class="sxs-lookup"><span data-stu-id="60870-119">To manage protected virtual machines:</span></span>

1. <span data-ttu-id="60870-120">Para exibir e gerenciar as configurações de backup de uma máquina virtual, clique na guia **Itens Protegidos** .</span><span class="sxs-lookup"><span data-stu-id="60870-120">To view and manage backup settings for a virtual machine click the **Protected Items** tab.</span></span>
2. <span data-ttu-id="60870-121">Clique no nome de um item protegido para ver a guia **Detalhes de Backup** , que mostra informações sobre o último backup.</span><span class="sxs-lookup"><span data-stu-id="60870-121">Click on the name of a protected item to see the **Backup Details** tab, which shows you information about the last backup.</span></span>

    ![Backup de máquinas virtuais](./media/backup-azure-manage-vms/backup-vmdetails.png)
3. <span data-ttu-id="60870-123">Para exibir e gerenciar as configurações de política de backup de uma máquina virtual, clique na guia **Políticas** .</span><span class="sxs-lookup"><span data-stu-id="60870-123">To view and manage backup policy settings for a virtual machine click the **Policies** tab.</span></span>

    ![Política de máquina virtual](./media/backup-azure-manage-vms/manage-policy-settings.png)

    <span data-ttu-id="60870-125">A guia **Políticas de Backup** exibe a política existente.</span><span class="sxs-lookup"><span data-stu-id="60870-125">The **Backup Policies** tab shows you the existing policy.</span></span> <span data-ttu-id="60870-126">Você pode modificar conforme necessário.</span><span class="sxs-lookup"><span data-stu-id="60870-126">You can modify as needed.</span></span> <span data-ttu-id="60870-127">Se você precisar criar uma nova política, clique em **Criar** na página **Políticas**.</span><span class="sxs-lookup"><span data-stu-id="60870-127">If you need to create a new policy click **Create** on the **Policies** page.</span></span> <span data-ttu-id="60870-128">Se você quiser remover uma política, ela não deve ter nenhuma máquina virtual associada a ela.</span><span class="sxs-lookup"><span data-stu-id="60870-128">Note that if you want to remove a policy it shouldn't have any virtual machines associated with it.</span></span>

    ![Política de máquina virtual](./media/backup-azure-manage-vms/backup-vmpolicy.png)
4. <span data-ttu-id="60870-130">Você pode obter mais informações sobre ações ou status de uma máquina virtual na página **Trabalhos** .</span><span class="sxs-lookup"><span data-stu-id="60870-130">You can get more information about actions or status for a virtual machine on the **Jobs** page.</span></span> <span data-ttu-id="60870-131">Clique em um trabalho na lista para obter mais detalhes ou filtrar trabalhos para uma máquina virtual específica.</span><span class="sxs-lookup"><span data-stu-id="60870-131">Click a job in the list to get more details, or filter jobs for a specific virtual machine.</span></span>

    ![Trabalhos](./media/backup-azure-manage-vms/backup-job.png)

## <a name="on-demand-backup-of-a-virtual-machine"></a><span data-ttu-id="60870-133">Backup sob demanda de uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="60870-133">On-demand backup of a virtual machine</span></span>
<span data-ttu-id="60870-134">Você pode obter um backup sob demanda de uma máquina virtual quando ela estiver configurada para proteção.</span><span class="sxs-lookup"><span data-stu-id="60870-134">You can take an on-demand backup of a virtual machine once it is configured for protection.</span></span> <span data-ttu-id="60870-135">Se o backup inicial estiver pendente para a máquina virtual, o backup sob demanda criará uma cópia completa da máquina virtual no cofre de backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="60870-135">If the initial backup is pending for the virtual machine, on-demand backup will create a full copy of the virtual machine in Azure backup vault.</span></span> <span data-ttu-id="60870-136">Se o primeiro backup for concluído, o backup sob demanda enviará apenas as alterações de backup anterior para o cofre de backup do Azure, ou seja, sempre é incremental.</span><span class="sxs-lookup"><span data-stu-id="60870-136">If first backup is completed, on-demand backup will only send changes from previous backup to Azure backup vault i.e. it is always incremental.</span></span>

> [!NOTE]
> <span data-ttu-id="60870-137">O período de retenção de um backup sob demanda é definido como o valor de retenção especificado para retenção diária na política de backup correspondente à VM.</span><span class="sxs-lookup"><span data-stu-id="60870-137">Retention range of an on-demand backup is set to retention value specified for Daily retention in backup policy corresponding to the VM.</span></span>  
>
>

<span data-ttu-id="60870-138">Para fazer backup sob demanda de uma máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="60870-138">To take an on-demand backup of a virtual machine:</span></span>

1. <span data-ttu-id="60870-139">Navegue até a página **Itens Protegidos** e selecione **Máquina Virtual do Azure** como **Tipo** (se ainda não estiver selecionada) e clique no botão **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="60870-139">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as **Type** (if not already selected) and click on **Select** button.</span></span>

    ![Tipo de VM](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="60870-141">Selecione a máquina virtual na qual você deseja fazer um backup sob demanda e clique no botão **Backup agora** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="60870-141">Select the virtual machine on which you want to take an on-demand backup and click on **Backup Now** button at the bottom of the page.</span></span>

    ![Fazer backup agora](./media/backup-azure-manage-vms/backup-now.png)

    <span data-ttu-id="60870-143">Isso criará um trabalho de backup na máquina virtual selecionada.</span><span class="sxs-lookup"><span data-stu-id="60870-143">This will create a backup job on the selected virtual machine.</span></span> <span data-ttu-id="60870-144">O período de retenção do ponto de recuperação criado por esse trabalho será o mesmo que o especificado na política associada à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60870-144">Retention range of recovery point created through this job will be same as that specified in the policy associated with the virtual machine.</span></span>

    ![Criando um trabalho de backup](./media/backup-azure-manage-vms/creating-job.png)

   > [!NOTE]
   > <span data-ttu-id="60870-146">Para exibir a política associada a uma máquina virtual, faça uma busca detalhada na máquina virtual na página **Itens protegidos** e vá para a guia da política de backup.</span><span class="sxs-lookup"><span data-stu-id="60870-146">To view the policy associated with a virtual machine, drill down into virtual machine in the **Protected Items** page and go to backup policy tab.</span></span>
   >
   >
3. <span data-ttu-id="60870-147">Depois que o trabalho é criado, você pode clicar no botão **Exibir trabalho** na barra de notificação do sistema para ver o trabalho correspondente na página de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="60870-147">Once the job is created, you can click on **View job** button in the toast bar to see the corresponding job in the jobs page.</span></span>

    ![Trabalho de backup criado](./media/backup-azure-manage-vms/created-job.png)
4. <span data-ttu-id="60870-149">Depois da conclusão bem-sucedida do trabalho, um ponto de recuperação será criado, o qual você poderá usar para restaurar a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60870-149">After successful completion of the job, a recovery point will be created which you can use to restore the virtual machine.</span></span> <span data-ttu-id="60870-150">Isso também incrementará o valor da coluna do ponto de recuperação em 1 na página **Itens protegidos** .</span><span class="sxs-lookup"><span data-stu-id="60870-150">This will also increment the recovery point column value by 1 in **Protected Items** page.</span></span>

## <a name="stop-protecting-virtual-machines"></a><span data-ttu-id="60870-151">Interromper a proteção de máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="60870-151">Stop protecting virtual machines</span></span>
<span data-ttu-id="60870-152">Você pode optar por parar os futuros backups de uma máquina virtual com as seguintes opções:</span><span class="sxs-lookup"><span data-stu-id="60870-152">You can choose to stop the future backups of a virtual machine with the following options:</span></span>

* <span data-ttu-id="60870-153">Reter dados de backup associados à máquina virtual no cofre de Backup do Azure</span><span class="sxs-lookup"><span data-stu-id="60870-153">Retain backup data associated with virtual machine in Azure Backup vault</span></span>
* <span data-ttu-id="60870-154">Excluir dados de backup associados à máquina virtual</span><span class="sxs-lookup"><span data-stu-id="60870-154">Delete backup data associated with virtual machine</span></span>

<span data-ttu-id="60870-155">Se você tiver optado por reter dados de backup associados à máquina virtual, você pode usar os dados de backup para restaurá-la.</span><span class="sxs-lookup"><span data-stu-id="60870-155">If you have selected to retain backup data associated with virtual machine, you can use the backup data to restore the virtual machine.</span></span> <span data-ttu-id="60870-156">Para obter detalhes de preço dessas máquinas virtuais, clique [aqui](https://azure.microsoft.com/pricing/details/backup/).</span><span class="sxs-lookup"><span data-stu-id="60870-156">For pricing details for such virtual machines, click [here](https://azure.microsoft.com/pricing/details/backup/).</span></span>

<span data-ttu-id="60870-157">Para interromper a proteção para uma máquina virtual:</span><span class="sxs-lookup"><span data-stu-id="60870-157">To Stop protection for a virtual machine:</span></span>

1. <span data-ttu-id="60870-158">Navegue até a página **Itens Protegidos**, selecione **Máquina virtual do Azure** como o tipo de filtro (se ainda não estiver selecionada) e clique no botão **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="60870-158">Navigate to **Protected Items** page and select **Azure virtual machine** as the filter type (if not already selected) and click on **Select** button.</span></span>

    ![Tipo de VM](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="60870-160">Selecione a máquina virtual e clique em **Parar proteção** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="60870-160">Select the virtual machine and click on **Stop Protection** at the bottom of the page.</span></span>

    ![Parar proteção](./media/backup-azure-manage-vms/stop-protection.png)
3. <span data-ttu-id="60870-162">Por padrão, o Backup do Azure não exclui os dados de backup associados à máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60870-162">By default, Azure Backup doesn’t delete the backup data associated with the virtual machine.</span></span>

    ![Confirmar a interrupção da proteção](./media/backup-azure-manage-vms/confirm-stop-protection.png)

    <span data-ttu-id="60870-164">Se você deseja excluir os dados de backup, marque a caixa de seleção.</span><span class="sxs-lookup"><span data-stu-id="60870-164">If you want to delete backup data, select the check box.</span></span>

    ![Caixa de seleção](./media/backup-azure-manage-vms/checkbox.png)

    <span data-ttu-id="60870-166">Selecione um motivo para interromper o backup.</span><span class="sxs-lookup"><span data-stu-id="60870-166">Please select a reason for stopping the backup.</span></span> <span data-ttu-id="60870-167">Embora seja opcional, fornecer um motivo ajudará o Backup do Azure a trabalhar com os comentários e priorizar os cenários do cliente.</span><span class="sxs-lookup"><span data-stu-id="60870-167">While this is optional, providing a reason will help Azure Backup to work on the feedback and prioritize the customer scenarios.</span></span>
4. <span data-ttu-id="60870-168">Clique no botão **Enviar** para enviar o trabalho **Interromper proteção**.</span><span class="sxs-lookup"><span data-stu-id="60870-168">Click on **Submit** button to submit the **Stop protection** job.</span></span> <span data-ttu-id="60870-169">Clique em **Exibir trabalho** para ver o trabalho correspondente na página **Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="60870-169">Click on **View Job** to see the corresponding the job in **Jobs** page.</span></span>

    ![Parar a proteção](./media/backup-azure-manage-vms/stop-protect-success.png)

    <span data-ttu-id="60870-171">Se você não selecionou a opção **Excluir dados de backup associados** durante o assistente **Parar proteção**, poste a conclusão do trabalho, as alterações de status de proteção para **Proteção interrompida**.</span><span class="sxs-lookup"><span data-stu-id="60870-171">If you have not selected **Delete associated backup data** option during **Stop Protection** wizard, then post job completion, protection status changes to **Protection Stopped**.</span></span> <span data-ttu-id="60870-172">Os dados permanecem com o Backup do Azure até que sejam explicitamente excluídos.</span><span class="sxs-lookup"><span data-stu-id="60870-172">The data remains with Azure Backup until it is explicitly deleted.</span></span> <span data-ttu-id="60870-173">Você sempre pode excluir os dados selecionando a máquina virtual na página **Itens protegidos** e clicando em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="60870-173">You can always delete the data by selecting the virtual machine in the **Protected Items** page and clicking **Delete**.</span></span>

    ![Proteção interrompida](./media/backup-azure-manage-vms/protection-stopped-status.png)

    <span data-ttu-id="60870-175">Se você tiver selecionado a opção **Excluir dados de backup associados**, a máquina virtual não fará parte da página **Itens Protegidos**.</span><span class="sxs-lookup"><span data-stu-id="60870-175">If you have selected the **Delete associated backup data** option, the virtual machine won’t be part of the **Protected Items** page.</span></span>

## <a name="re-protect-virtual-machine"></a><span data-ttu-id="60870-176">Proteger novamente a Máquina virtual</span><span class="sxs-lookup"><span data-stu-id="60870-176">Re-protect Virtual machine</span></span>
<span data-ttu-id="60870-177">Se você não selecionou a opção **Excluir dados de backup associados** em **Parar proteção**, pode proteger novamente a máquina virtual seguindo as etapas semelhantes para fazer backup de máquinas virtuais registradas.</span><span class="sxs-lookup"><span data-stu-id="60870-177">If you have not selected the **Delete associate backup data** option in **Stop Protection**, you can re-protect the virtual machine by following the steps similar to backing up registered virtual machines.</span></span> <span data-ttu-id="60870-178">Depois de protegida, essa máquina virtual terá os dados de backup retidos antes da interrupção da proteção e os pontos de recuperação serão criados após a nova proteção.</span><span class="sxs-lookup"><span data-stu-id="60870-178">Once protected, this virtual machine will have backup data retained prior to stop protection and recovery points created after re-protect.</span></span>

<span data-ttu-id="60870-179">Após proteger novamente, o status de proteção da máquina virtual será alterado para **Protegido** se houver pontos de recuperação anteriores a **Parar proteção**.</span><span class="sxs-lookup"><span data-stu-id="60870-179">After re-protect, the virtual machine’s protection status will be changed to **Protected** if there are recovery points prior to **Stop Protection**.</span></span>

  ![Máquina virtual protegida novamente](./media/backup-azure-manage-vms/reprotected-status.png)

> [!NOTE]
> <span data-ttu-id="60870-181">Ao proteger novamente a máquina virtual, você pode escolher uma política diferente da política com a qual a máquina virtual foi inicialmente protegida.</span><span class="sxs-lookup"><span data-stu-id="60870-181">When re-protecting the virtual machine, you can choose a different policy than the policy with which virtual machine was protected initially.</span></span>
>
>

## <a name="unregister-virtual-machines"></a><span data-ttu-id="60870-182">Cancelar o registro das máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="60870-182">Unregister virtual machines</span></span>
<span data-ttu-id="60870-183">Se você quiser remover a máquina virtual do cofre de backup:</span><span class="sxs-lookup"><span data-stu-id="60870-183">If you want to remove the virtual machine from the backup vault:</span></span>

1. <span data-ttu-id="60870-184">Clique no botão **CANCELAR REGISTRO** , na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="60870-184">Click on the **UNREGISTER** button at the bottom of the page.</span></span>

    ![Desabilitar a proteção](./media/backup-azure-manage-vms/unregister-button.png)

    <span data-ttu-id="60870-186">Uma notificação do sistema será exibida na parte inferior da tela solicitando confirmação.</span><span class="sxs-lookup"><span data-stu-id="60870-186">A toast notification will appear at the bottom of the screen requesting confirmation.</span></span> <span data-ttu-id="60870-187">Clique em **SIM** para continuar.</span><span class="sxs-lookup"><span data-stu-id="60870-187">Click **YES** to continue.</span></span>

    ![Desabilitar a proteção](./media/backup-azure-manage-vms/confirm-unregister.png)

## <a name="delete-backup-data"></a><span data-ttu-id="60870-189">Excluir dados de backup</span><span class="sxs-lookup"><span data-stu-id="60870-189">Delete Backup data</span></span>
<span data-ttu-id="60870-190">Você pode excluir os dados de backup associados a uma máquina virtual, ou:</span><span class="sxs-lookup"><span data-stu-id="60870-190">You can delete the backup data associated with a virtual machine, either:</span></span>

* <span data-ttu-id="60870-191">Durante a interrupção do trabalho da proteção</span><span class="sxs-lookup"><span data-stu-id="60870-191">During Stop Protection Job</span></span>
* <span data-ttu-id="60870-192">Após uma interrupção no trabalho de proteção ser concluída em uma máquina virtual</span><span class="sxs-lookup"><span data-stu-id="60870-192">After a stop protection job is completed on a virtual machine</span></span>

<span data-ttu-id="60870-193">Para excluir dados de backup em uma máquina virtual, que está no estado *Proteção Interrompida* , poste a conclusão bem-sucedida do trabalho em **Parar Backup** :</span><span class="sxs-lookup"><span data-stu-id="60870-193">To delete backup data on a virtual machine, which is in the *Protection Stopped* state post successful completion of a **Stop Backup** job:</span></span>

1. <span data-ttu-id="60870-194">Navegue até a página **Itens Protegidos** e selecione **Máquina Virtual do Azure** como o *tipo* e clique no botão **Selecionar**.</span><span class="sxs-lookup"><span data-stu-id="60870-194">Navigate to the **Protected Items** page and select **Azure Virtual Machine** as *type* and click the **Select** button.</span></span>

    ![Tipo de VM](./media/backup-azure-manage-vms/vm-type.png)
2. <span data-ttu-id="60870-196">Selecione a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="60870-196">Select the virtual machine.</span></span> <span data-ttu-id="60870-197">A máquina virtual estará no estado **Proteção interrompida** .</span><span class="sxs-lookup"><span data-stu-id="60870-197">The virtual machine will be in **Protection Stopped** state.</span></span>

    ![Proteção interrompida](./media/backup-azure-manage-vms/protection-stopped-b.png)
3. <span data-ttu-id="60870-199">Clique no botão **EXCLUIR** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="60870-199">Click the **DELETE** button at the bottom of the page.</span></span>

    ![Excluir backup](./media/backup-azure-manage-vms/delete-backup.png)
4. <span data-ttu-id="60870-201">No assistente **Excluir dados de backup**, selecione um motivo para a exclusão de dados de backup (altamente recomendado) e clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="60870-201">In the **Delete backup data** wizard, select a reason for deleting backup data (highly recommended) and click **Submit**.</span></span>

    ![Excluir dados de backup](./media/backup-azure-manage-vms/delete-backup-data.png)
5. <span data-ttu-id="60870-203">Isso criará um trabalho para excluir os dados de backup da máquina virtual selecionada.</span><span class="sxs-lookup"><span data-stu-id="60870-203">This will create a job to delete backup data of selected virtual machine.</span></span> <span data-ttu-id="60870-204">Clique em **Exibir trabalho** para ver o trabalho correspondente na página Trabalhos.</span><span class="sxs-lookup"><span data-stu-id="60870-204">Click **View job** to see corresponding job in Jobs page.</span></span>

    ![Exclusão de dados bem-sucedida](./media/backup-azure-manage-vms/delete-data-success.png)

    <span data-ttu-id="60870-206">Depois que o trabalho for concluído, a entrada correspondente à máquina virtual será removida da página **Itens protegidos** .</span><span class="sxs-lookup"><span data-stu-id="60870-206">Once the job is completed, the entry corresponding to the virtual machine will be removed from **Protected items** page.</span></span>

## <a name="dashboard"></a><span data-ttu-id="60870-207">Painel</span><span class="sxs-lookup"><span data-stu-id="60870-207">Dashboard</span></span>
<span data-ttu-id="60870-208">Na página **Painel** , você pode examinar informações sobre máquinas virtuais do Azure, seu armazenamento e os trabalhos associados a elas nas últimas 24 horas.</span><span class="sxs-lookup"><span data-stu-id="60870-208">On the **Dashboard** page you can review information about Azure virtual machines, their storage, and jobs associated with them in the last 24 hours.</span></span> <span data-ttu-id="60870-209">Você pode exibir o status de backup e quaisquer erros de backup associados.</span><span class="sxs-lookup"><span data-stu-id="60870-209">You can view backup status and any associated backup errors.</span></span>

![Painel](./media/backup-azure-manage-vms/dashboard-protectedvms.png)

> [!NOTE]
> <span data-ttu-id="60870-211">Os valores no painel são atualizados a cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="60870-211">Values in the dashboard are refreshed once every 24 hours.</span></span>
>
>

## <a name="auditing-operations"></a><span data-ttu-id="60870-212">Operações de auditoria</span><span class="sxs-lookup"><span data-stu-id="60870-212">Auditing Operations</span></span>
<span data-ttu-id="60870-213">O backup do Azure oferece análise dos “logs de operação” das operações de backup disparadas pelo cliente que facilita ver exatamente quais operações de gerenciamento foram realizadas no cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="60870-213">Azure backup provides review of the "operation logs" of backup operations triggered by the customer making it easy to see exactly what management operations were performed on the backup vault.</span></span> <span data-ttu-id="60870-214">Os logs de operações permitem um ótimo suporte a auditoria e análise posterior das operações de backup.</span><span class="sxs-lookup"><span data-stu-id="60870-214">Operations logs enable great post-mortem and audit support for the backup operations.</span></span>

<span data-ttu-id="60870-215">As seguintes operações são registradas nos logs de operação:</span><span class="sxs-lookup"><span data-stu-id="60870-215">The following operations are logged in Operation logs:</span></span>

* <span data-ttu-id="60870-216">Registrar</span><span class="sxs-lookup"><span data-stu-id="60870-216">Register</span></span>
* <span data-ttu-id="60870-217">Cancelar o registro </span><span class="sxs-lookup"><span data-stu-id="60870-217">Unregister</span></span>
* <span data-ttu-id="60870-218">Configurar a proteção</span><span class="sxs-lookup"><span data-stu-id="60870-218">Configure protection</span></span>
* <span data-ttu-id="60870-219">Backup (tanto as agendadas quanto as sob demanda por meio do BackupNow)</span><span class="sxs-lookup"><span data-stu-id="60870-219">Backup ( Both scheduled as well as on-demand backup through BackupNow)</span></span>
* <span data-ttu-id="60870-220">Restaurar</span><span class="sxs-lookup"><span data-stu-id="60870-220">Restore</span></span>
* <span data-ttu-id="60870-221">Parar a proteção</span><span class="sxs-lookup"><span data-stu-id="60870-221">Stop protection</span></span>
* <span data-ttu-id="60870-222">Excluir dados de backup</span><span class="sxs-lookup"><span data-stu-id="60870-222">Delete backup data</span></span>
* <span data-ttu-id="60870-223">Adicionar política</span><span class="sxs-lookup"><span data-stu-id="60870-223">Add policy</span></span>
* <span data-ttu-id="60870-224">Excluir política</span><span class="sxs-lookup"><span data-stu-id="60870-224">Delete policy</span></span>
* <span data-ttu-id="60870-225">Atualizar política</span><span class="sxs-lookup"><span data-stu-id="60870-225">Update policy</span></span>
* <span data-ttu-id="60870-226">Cancelar trabalho</span><span class="sxs-lookup"><span data-stu-id="60870-226">Cancel job</span></span>

<span data-ttu-id="60870-227">Para exibir logs de operação correspondentes a um cofre de backup:</span><span class="sxs-lookup"><span data-stu-id="60870-227">To view operation logs corresponding to a backup vault:</span></span>

1. <span data-ttu-id="60870-228">Navegue até **Serviços de gerenciamento** no portal do Azure e clique na guia **Logs de Operação**.</span><span class="sxs-lookup"><span data-stu-id="60870-228">Navigate to **Management services** in Azure portal, and then click the **Operation Logs** tab.</span></span>

    ![Logs de operação](./media/backup-azure-manage-vms/ops-logs.png)
2. <span data-ttu-id="60870-230">Em filtros, selecione **Backup** como *Tipo*, especifique o nome do cofre de backup em *nome do serviço* e clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="60870-230">In the filters, select **Backup** as *Type* and specify the backup vault name in *service name* and click on **Submit**.</span></span>

    ![Filtro de logs de operação](./media/backup-azure-manage-vms/ops-logs-filter.png)
3. <span data-ttu-id="60870-232">Nos logs de operações, selecione qualquer operação e clique em **Detalhes** para ver os detalhes correspondentes a uma operação.</span><span class="sxs-lookup"><span data-stu-id="60870-232">In the operations logs, select any operation and click  **Details** to see details corresponding to an operation.</span></span>

    ![Detalhes de busca de logs de operação](./media/backup-azure-manage-vms/ops-logs-details.png)

    <span data-ttu-id="60870-234">O **Assistente de detalhes** contém informações sobre a operação disparada, a Id do trabalho, o recurso em que essa operação é disparada e a hora de início da operação.</span><span class="sxs-lookup"><span data-stu-id="60870-234">The **Details wizard** contains information about the operation triggered, job Id, resource on which this operation is triggered, and start time of the operation.</span></span>

    ![Detalhes da Operação](./media/backup-azure-manage-vms/ops-logs-details-window.png)

## <a name="alert-notifications"></a><span data-ttu-id="60870-236">Notificações de alerta</span><span class="sxs-lookup"><span data-stu-id="60870-236">Alert notifications</span></span>
<span data-ttu-id="60870-237">Você pode obter notificações de alerta personalizadas para os trabalhos no portal.</span><span class="sxs-lookup"><span data-stu-id="60870-237">You can get custom alert notifications for the jobs in portal.</span></span> <span data-ttu-id="60870-238">Isso é possível ao definir regras de alerta do PowerShell baseadas em eventos de logs operacionais.</span><span class="sxs-lookup"><span data-stu-id="60870-238">This is achieved by defining PowerShell-based alert rules on operational logs events.</span></span> <span data-ttu-id="60870-239">É recomendável usar o *PowerShell versão 1.3.0 ou superior*.</span><span class="sxs-lookup"><span data-stu-id="60870-239">We recommend using *PowerShell version 1.3.0 or above*.</span></span>

<span data-ttu-id="60870-240">Para definir uma notificação personalizada para o alerta de falhas de backup, um comando de exemplo terá a seguinte aparência:</span><span class="sxs-lookup"><span data-stu-id="60870-240">To define a custom notification to alert for backup failures, a sample command will look like:</span></span>

```
PS C:\> $actionEmail = New-AzureRmAlertRuleEmail -CustomEmail contoso@microsoft.com
PS C:\> Add-AzureRmLogAlertRule -Name backupFailedAlert -Location "East US" -ResourceGroup RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US -OperationName Microsoft.Backup/backupVault/Backup -Status Failed -TargetResourceId /subscriptions/86eeac34-eth9a-4de3-84db-7a27d121967e/resourceGroups/RecoveryServices-DP2RCXUGWS3MLJF4LKPI3A3OMJ2DI4SRJK6HIJH22HFIHZVVELRQ-East-US/providers/microsoft.backupbvtd2/BackupVault/trinadhVault -Actions $actionEmail
```

<span data-ttu-id="60870-241">**ResourceId**: você pode obter isso no pop-up Logs de Operações, conforme descrito na seção acima.</span><span class="sxs-lookup"><span data-stu-id="60870-241">**ResourceId**: You can get this from Operations Logs popup as described in above section.</span></span> <span data-ttu-id="60870-242">O ResourceUri na janela pop-up de detalhes de uma operação é a ResourceId a ser fornecida para esse cmdlet.</span><span class="sxs-lookup"><span data-stu-id="60870-242">ResourceUri in details popup window of an operation is the ResourceId to be supplied for this cmdlet.</span></span>

<span data-ttu-id="60870-243">**OperationName**: terá o formato "Microsoft.Backup/backupvault/<EventName> em que NomeDoEvento é uma das seguintes opções: Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span><span class="sxs-lookup"><span data-stu-id="60870-243">**OperationName**: This will be of the format "Microsoft.Backup/backupvault/<EventName>" where EventName is one of Register,Unregister,ConfigureProtection,Backup,Restore,StopProtection,DeleteBackupData,CreateProtectionPolicy,DeleteProtectionPolicy,UpdateProtectionPolicy</span></span>

<span data-ttu-id="60870-244">**Status**: os valores com suporte são Started, Succeeded e Failed.</span><span class="sxs-lookup"><span data-stu-id="60870-244">**Status**: Supported values are- Started, Succeeded and Failed.</span></span>

<span data-ttu-id="60870-245">**ResourceGroup**: ResourceGroup do recurso em que a operação é disparada.</span><span class="sxs-lookup"><span data-stu-id="60870-245">**ResourceGroup**:ResourceGroup of the resource on which operation is triggered.</span></span> <span data-ttu-id="60870-246">Você pode obter isso do valor ResourceId.</span><span class="sxs-lookup"><span data-stu-id="60870-246">You can obtain this from ResourceId value.</span></span> <span data-ttu-id="60870-247">O valor entre os campos */resourceGroups/* e */providers/* em um valor ResourceId é o valor para ResourceGroup.</span><span class="sxs-lookup"><span data-stu-id="60870-247">Value between fields */resourceGroups/* and */providers/* in ResourceId value is the value for ResourceGroup.</span></span>

<span data-ttu-id="60870-248">**Name**: nome da regra de alerta.</span><span class="sxs-lookup"><span data-stu-id="60870-248">**Name**: Name of the Alert Rule.</span></span>

<span data-ttu-id="60870-249">**CustomEmail**: especifica o endereço de email personalizado para o qual você deseja enviar a notificação de alerta</span><span class="sxs-lookup"><span data-stu-id="60870-249">**CustomEmail**: Specify the custom email address to which you want to send alert notification</span></span>

<span data-ttu-id="60870-250">**SendToServiceOwners**: essa opção envia a notificação de alerta para todos os administradores e coadministradores da assinatura.</span><span class="sxs-lookup"><span data-stu-id="60870-250">**SendToServiceOwners**: This option sends alert notification to all administrators and co-administrators of the subscription.</span></span> <span data-ttu-id="60870-251">Pode ser usado no cmdlet **New-AzureRmAlertRuleEmail**</span><span class="sxs-lookup"><span data-stu-id="60870-251">It can be used in **New-AzureRmAlertRuleEmail** cmdlet</span></span>

### <a name="limitations-on-alerts"></a><span data-ttu-id="60870-252">Limitações sobre alertas</span><span class="sxs-lookup"><span data-stu-id="60870-252">Limitations on Alerts</span></span>
<span data-ttu-id="60870-253">Os alertas baseados em eventos estão sujeitos às seguintes limitações:</span><span class="sxs-lookup"><span data-stu-id="60870-253">Event-based alerts are subjected to the following limitations:</span></span>

1. <span data-ttu-id="60870-254">Os alertas são disparados em todas as máquinas virtuais no cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="60870-254">Alerts are triggered on all virtual machines in the backup vault.</span></span> <span data-ttu-id="60870-255">Você não pode personalizá-lo para obter alertas de um conjunto específico de máquinas virtuais em um cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="60870-255">You cannot customize it to get alerts for specific set of virtual machines in a backup vault.</span></span>
2. <span data-ttu-id="60870-256">Esse recurso está em Preview.</span><span class="sxs-lookup"><span data-stu-id="60870-256">This feature is in Preview.</span></span> [<span data-ttu-id="60870-257">Saiba mais</span><span class="sxs-lookup"><span data-stu-id="60870-257">Learn more</span></span>](../monitoring-and-diagnostics/insights-powershell-samples.md#create-metric-alerts)
3. <span data-ttu-id="60870-258">Você receberá alertas de “alerts-noreply@mail.windowsazure.com”.</span><span class="sxs-lookup"><span data-stu-id="60870-258">You will receive alerts from "alerts-noreply@mail.windowsazure.com".</span></span> <span data-ttu-id="60870-259">No momento, você não pode modificar o remetente do email.</span><span class="sxs-lookup"><span data-stu-id="60870-259">Currently you can't modify the email sender.</span></span>

## <a name="next-steps"></a><span data-ttu-id="60870-260">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="60870-260">Next steps</span></span>
* [<span data-ttu-id="60870-261">Restaurar máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="60870-261">Restore Azure VMs</span></span>](backup-azure-restore-vms.md)
