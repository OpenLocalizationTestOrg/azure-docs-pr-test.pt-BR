---
title: "Fazer backup de máquinas de virtuais do Azure implantadas com o modelo clássico em um cofre de backup | Microsoft Docs"
description: "Descubra suas máquinas virtuais, registre-as e faça backup delas com estes procedimentos para o backup de máquina virtual do Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "backup de máquinas virtuais; fazer backup de máquina virtual, backup e recuperação de desastre; backup de vm"
ms.assetid: c0ab5469-65fd-4af5-ae9b-f5d183f82ce8
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/02/2017
ms.author: markgal;trinadhk;
ms.openlocfilehash: e1da8bce96078a43c656f84005cefc8bbe81c9e3
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="8b92c-104">Fazer backup de máquinas virtuais do Azure (portal clássico)</span><span class="sxs-lookup"><span data-stu-id="8b92c-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="8b92c-105">Fazer backup de VMs no cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="8b92c-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="8b92c-106">Fazer backup de VMs no cofre de Backup</span><span class="sxs-lookup"><span data-stu-id="8b92c-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="8b92c-107">Este artigo mostra os procedimentos para fazer backup de uma VM (máquina virtual) do Azure com implantação clássica em um cofre de Backup.</span><span class="sxs-lookup"><span data-stu-id="8b92c-107">This article provides the procedures for backing up a Classic-deployed Azure virtual machine (VM) to a Backup vault.</span></span> <span data-ttu-id="8b92c-108">Há algumas tarefas que você precisa fazer antes de poder fazer backup de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b92c-108">There are a few tasks you need to take care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="8b92c-109">Se ainda não tiver feito isto, conclua os [pré-requisitos](backup-azure-vms-prepare.md) para preparar o ambiente para o backup de VMs.</span><span class="sxs-lookup"><span data-stu-id="8b92c-109">If you haven't already done so, complete the [prerequisites](backup-azure-vms-prepare.md) to prepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="8b92c-110">Para obter informações adicionais, confira os artigos em [planejamento da infraestrutura de backup de VM no Azure](backup-azure-vms-introduction.md) e em [máquinas virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="8b92c-110">For additional information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="8b92c-111">O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="8b92c-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="8b92c-112">Um cofre de Backup só pode proteger VMs com implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="8b92c-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="8b92c-113">Você não pode proteger VMs implantadas pelo Resource Manager com um cofre de Backup.</span><span class="sxs-lookup"><span data-stu-id="8b92c-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="8b92c-114">Confira [Fazer backup de VMs no cofre dos Serviços de Recuperação](backup-azure-arm-vms.md) para obter detalhes sobre como trabalhar com cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="8b92c-114">See [Back up VMs to Recovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="8b92c-115">Fazer o backup de máquinas virtuais do Azure envolve três etapas principais:</span><span class="sxs-lookup"><span data-stu-id="8b92c-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Três etapas para fazer o backup de uma VM de IaaS do Azure](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="8b92c-117">O backup de máquinas virtuais é um processo local.</span><span class="sxs-lookup"><span data-stu-id="8b92c-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="8b92c-118">Não é possível fazer backup de máquinas virtuais de uma região em um cofre de backup em outra região.</span><span class="sxs-lookup"><span data-stu-id="8b92c-118">You cannot back up virtual machines in one region to a backup vault in another region.</span></span> <span data-ttu-id="8b92c-119">Portanto, você deve criar um cofre de backup em cada região do Azure na qual existam VMs das quais serão feitos backups.</span><span class="sxs-lookup"><span data-stu-id="8b92c-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="8b92c-120">A partir de março de 2017, você não poderá mais usar o portal clássico para criar os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="8b92c-120">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="8b92c-121">Agora você pode atualizar os cofres de Backup para cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="8b92c-121">You can now upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="8b92c-122">Para obter detalhes, veja o artigo [Atualizar um cofre de Backup para um cofre dos Serviços de Recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="8b92c-122">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="8b92c-123">A Microsoft incentiva você a atualizar os cofres de Backup para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="8b92c-123">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="8b92c-124">Após 15 de outubro de 2017, você não poderá usar o PowerShell para criar os Cofres do Backup.</span><span class="sxs-lookup"><span data-stu-id="8b92c-124">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="8b92c-125">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="8b92c-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="8b92c-126">Todos os Cofres do Backup restantes serão atualizados automaticamente para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="8b92c-126">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="8b92c-127">Você não poderá acessar os dados de backup no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="8b92c-127">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="8b92c-128">Em vez disso, use o portal do Azure para acessar os dados de backup nos cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="8b92c-128">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="8b92c-129">Etapa 1 - Descobrir máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="8b92c-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="8b92c-130">Para garantir que qualquer VM (máquina virtual) nova adicionada à assinatura seja identificada antes do registro, execute o processo de descoberta.</span><span class="sxs-lookup"><span data-stu-id="8b92c-130">To ensure any new virtual machines (VMs) added to the subscription are identified before registering, run the discovery process.</span></span> <span data-ttu-id="8b92c-131">O processo consulta o Azure quanto à lista de máquinas virtuais na assinatura, juntamente com informações adicionais, como o nome do serviço de nuvem e a região.</span><span class="sxs-lookup"><span data-stu-id="8b92c-131">The process queries Azure for the list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="8b92c-132">Entrar no [portal clássico](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="8b92c-132">Sign in to the [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="8b92c-133">Na lista de serviços do Azure, clique em **Serviços de Recuperação** para abrir a lista de cofres de Backup e Recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="8b92c-133">In the list of Azure services, click **Recovery Services** to open the list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="8b92c-134">![Abrir listas de cofres](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="8b92c-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="8b92c-135">Na lista de cofres de Backup, escolha o cofre para fazer backup de uma VM.</span><span class="sxs-lookup"><span data-stu-id="8b92c-135">In the list of Backup vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="8b92c-136">Se for um novo cofre, o portal abrirá na página **Início Rápido** .</span><span class="sxs-lookup"><span data-stu-id="8b92c-136">If this is a new vault the portal opens to the **Quick Start** page.</span></span>

    ![Abrir o menu Itens registrados](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="8b92c-138">Se o cofre tiver sido configurado anteriormente, o portal abrirá no menu usado mais recentemente.</span><span class="sxs-lookup"><span data-stu-id="8b92c-138">If the vault has previously been configured, the portal opens to the most recently used menu.</span></span>
4. <span data-ttu-id="8b92c-139">No menu do cofre (na parte superior da página), clique em **Itens Registrados**.</span><span class="sxs-lookup"><span data-stu-id="8b92c-139">From the vault menu (at the top of the page), click **Registered Items**.</span></span>

    ![Abrir o menu Itens registrados](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="8b92c-141">No menu **Tipo**, selecione **Máquina Virtual do Azure**.</span><span class="sxs-lookup"><span data-stu-id="8b92c-141">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Selecionar carga de trabalho](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="8b92c-143">Clique em **DESCOBRIR** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="8b92c-143">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="8b92c-144">![Botão Descobrir](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="8b92c-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="8b92c-145">O processo de descoberta pode ser executado por alguns minutos, enquanto as máquinas virtuais estão sendo tabuladas.</span><span class="sxs-lookup"><span data-stu-id="8b92c-145">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="8b92c-146">Há uma notificação na parte inferior da tela que informa você de que o processo está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="8b92c-146">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![Descobrir VMs](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="8b92c-148">As alterações de notificação quando o processo é concluído.</span><span class="sxs-lookup"><span data-stu-id="8b92c-148">The notification changes when the process is complete.</span></span> <span data-ttu-id="8b92c-149">Se o processo de descoberta não tiver localizado as máquinas virtuais, primeiro verifique se as VMs existem mesmo.</span><span class="sxs-lookup"><span data-stu-id="8b92c-149">If the discovery process did not find the virtual machines, first ensure the VMs exist.</span></span> <span data-ttu-id="8b92c-150">Se existirem, garanta que as VMs estejam na mesma região que o cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="8b92c-150">If the VMs exist, ensure the VMs are in the same region as the backup vault.</span></span> <span data-ttu-id="8b92c-151">Se existirem e estiverem na mesma região, verifique se as VMs já não estão registradas em um cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="8b92c-151">If the VMs exist and are in the same region, ensure the VMs are not already registered to a backup vault.</span></span> <span data-ttu-id="8b92c-152">Se uma VM estiver atribuída a um cofre de backup, ela não estará disponível para ser atribuída a outros cofres de backup.</span><span class="sxs-lookup"><span data-stu-id="8b92c-152">If a VM is assigned to a backup vault it is not available to be assigned to other backup vaults.</span></span>

    ![Descoberta concluída](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="8b92c-154">Depois de descobrir os novos itens, vá para a Etapa 2 e registre suas VMs.</span><span class="sxs-lookup"><span data-stu-id="8b92c-154">Once you have discovered the new items, go to Step 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="8b92c-155">Etapa 2 - Registrar as máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="8b92c-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="8b92c-156">Você registra uma máquina virtual do Azure para associá-la ao serviço Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b92c-156">You register an Azure virtual machine to associate it with the Azure Backup service.</span></span> <span data-ttu-id="8b92c-157">Normalmente, é uma atividade realizada uma única vez.</span><span class="sxs-lookup"><span data-stu-id="8b92c-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="8b92c-158">Navegue até o cofre de backup em **Serviços de Recuperação** no portal do Azure e clique em **Itens Registrados**.</span><span class="sxs-lookup"><span data-stu-id="8b92c-158">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="8b92c-159">Selecione **Máquina Virtual do Azure** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="8b92c-159">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Selecionar carga de trabalho](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="8b92c-161">Clique em **REGISTRAR** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="8b92c-161">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="8b92c-162">![Botão Registrar](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="8b92c-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="8b92c-163">No menu de atalho **Registrar Itens** , selecione as máquinas virtuais que você deseja registrar.</span><span class="sxs-lookup"><span data-stu-id="8b92c-163">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span> <span data-ttu-id="8b92c-164">Se houver duas ou mais máquinas virtuais com o mesmo nome, use o serviço de nuvem para fazer a distinção entre elas.</span><span class="sxs-lookup"><span data-stu-id="8b92c-164">If there are two or more virtual machines with the same name, use the cloud service to distinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="8b92c-165">Várias máquinas virtuais podem ser registradas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="8b92c-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="8b92c-166">Um trabalho é criado para cada máquina virtual selecionada.</span><span class="sxs-lookup"><span data-stu-id="8b92c-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="8b92c-167">Clique em **Exibir Trabalho** na notificação para ir para a página **Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="8b92c-167">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Registrar trabalho](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="8b92c-169">A máquina virtual também aparece na lista de itens registrados junto com o status da operação de registro.</span><span class="sxs-lookup"><span data-stu-id="8b92c-169">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Status de registro 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="8b92c-171">Quando a operação for concluída, o status será alterado para refletir o estado *registrado* .</span><span class="sxs-lookup"><span data-stu-id="8b92c-171">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Status de registro 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="8b92c-173">Etapa 3 - Proteger máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="8b92c-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="8b92c-174">Agora você pode configurar uma política de backup e de retenção para a máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="8b92c-174">Now you can set up a backup and retention policy for the virtual machine.</span></span> <span data-ttu-id="8b92c-175">Várias máquinas virtuais podem ser protegidas usando uma única ação de proteção.</span><span class="sxs-lookup"><span data-stu-id="8b92c-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="8b92c-176">Os cofres do Backup do Azure criados depois de maio de 2015 poderão vir com uma política padrão interna ao cofre.</span><span class="sxs-lookup"><span data-stu-id="8b92c-176">Azure Backup vaults created after May 2015 come with a default policy built into the vault.</span></span> <span data-ttu-id="8b92c-177">Essa política padrão é fornecida com uma retenção padrão de 30 dias e agendamento de backup de uma vez por dia.</span><span class="sxs-lookup"><span data-stu-id="8b92c-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="8b92c-178">Navegue até o cofre de backup em **Serviços de Recuperação** no portal do Azure e clique em **Itens Registrados**.</span><span class="sxs-lookup"><span data-stu-id="8b92c-178">Navigate to the backup vault under **Recovery Services** in the Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="8b92c-179">Selecione **Máquina Virtual do Azure** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="8b92c-179">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Selecionar a carga de trabalho no portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="8b92c-181">Na parte inferior da página, clique em **PROTEGER** .</span><span class="sxs-lookup"><span data-stu-id="8b92c-181">Click **PROTECT** at the bottom of the page.</span></span>

    <span data-ttu-id="8b92c-182">O **assistente Proteger Itens** é exibido.</span><span class="sxs-lookup"><span data-stu-id="8b92c-182">The **Protect Items wizard** appears.</span></span> <span data-ttu-id="8b92c-183">Esse assistente lista apenas as máquinas virtuais registradas e não protegidas.</span><span class="sxs-lookup"><span data-stu-id="8b92c-183">The wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="8b92c-184">Selecione as máquinas virtuais que deseja proteger.</span><span class="sxs-lookup"><span data-stu-id="8b92c-184">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="8b92c-185">Se houver duas ou mais máquinas virtuais com o mesmo nome, use o serviço de nuvem para distinguir entre elas.</span><span class="sxs-lookup"><span data-stu-id="8b92c-185">If there are two or more virtual machines with the same name, use the cloud service to distinguish between the virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="8b92c-186">Você pode proteger várias máquinas virtuais de uma só vez.</span><span class="sxs-lookup"><span data-stu-id="8b92c-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Configurar proteção em escala](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="8b92c-188">Escolha um **agendamento de backup** para fazer o backup das máquinas virtuais que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="8b92c-188">Choose a **backup schedule** to back up the virtual machines that you've selected.</span></span> <span data-ttu-id="8b92c-189">Escolha um conjunto existente de políticas ou defina um novo.</span><span class="sxs-lookup"><span data-stu-id="8b92c-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="8b92c-190">Cada política de backup pode ter várias máquinas virtuais associadas a ela.</span><span class="sxs-lookup"><span data-stu-id="8b92c-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="8b92c-191">No entanto, a máquina virtual só pode estar associada a apenas uma política em um determinado ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="8b92c-191">However, the virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Proteger com nova política](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="8b92c-193">Uma política de backup também inclui um esquema de retenção para os backups agendados.</span><span class="sxs-lookup"><span data-stu-id="8b92c-193">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="8b92c-194">Se você selecionar uma política de backup existente, não será possível modificar as opções de retenção na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="8b92c-194">If you select an existing backup policy, you cannot modify the retention options in the next step.</span></span>
   >
   >

5. <span data-ttu-id="8b92c-195">Escolha um **intervalo de retenção** a ser associado aos backups.</span><span class="sxs-lookup"><span data-stu-id="8b92c-195">Choose a **retention range** to associate with the backups.</span></span>

    ![Proteger com retenção flexível](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="8b92c-197">A política de retenção especifica o período de armazenamento de um backup.</span><span class="sxs-lookup"><span data-stu-id="8b92c-197">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="8b92c-198">Você pode especificar políticas de retenção diferentes com base em quando o backup é feito.</span><span class="sxs-lookup"><span data-stu-id="8b92c-198">You can specify different retention policies based on when the backup is taken.</span></span> <span data-ttu-id="8b92c-199">Por exemplo, um ponto de backup feito diariamente (que funciona como um ponto de recuperação operacional) pode ser preservado durante 90 dias.</span><span class="sxs-lookup"><span data-stu-id="8b92c-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="8b92c-200">Em comparação, um ponto de backup feito no final de cada trimestre (para fins de auditoria) precisará ser preservado por muitos meses ou anos.</span><span class="sxs-lookup"><span data-stu-id="8b92c-200">In comparison, a backup point taken at the end of each quarter (for audit purposes) may need to be preserved for many months or years.</span></span>

    ![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="8b92c-202">Nesta imagem de exemplo:</span><span class="sxs-lookup"><span data-stu-id="8b92c-202">In this example image:</span></span>

   * <span data-ttu-id="8b92c-203">**Política de retenção diária**: os backups diários são armazenados por 30 dias.</span><span class="sxs-lookup"><span data-stu-id="8b92c-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="8b92c-204">**Política de retenção semanal**: os backups feitos todas as semanas aos domingos serão preservados por 104 semanas.</span><span class="sxs-lookup"><span data-stu-id="8b92c-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="8b92c-205">**Política de retenção mensal**: os backups feitos no último domingo de cada mês serão preservados por 120 meses.</span><span class="sxs-lookup"><span data-stu-id="8b92c-205">**Monthly retention policy**: Backups taken on the last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="8b92c-206">**Política de retenção anual**: os backups feitos no primeiro domingo de cada janeiro serão preservados por 99 anos.</span><span class="sxs-lookup"><span data-stu-id="8b92c-206">**Yearly retention policy**: Backups taken on the first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="8b92c-207">Um trabalho é criado para configurar a política de proteção e associar as máquinas virtuais a essa política para cada máquina virtual selecionada.</span><span class="sxs-lookup"><span data-stu-id="8b92c-207">A job is created to configure the protection policy and associate the virtual machines to that policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="8b92c-208">Para exibir a lista de trabalhos de **Configurar Proteção**, no menu dos cofres, clique em **Trabalhos** e selecione **Configurar Proteção** no filtro **Operação**.</span><span class="sxs-lookup"><span data-stu-id="8b92c-208">To view the list of **Configure Protection** jobs, from the vaults menu, click **Jobs** and select **Configure Protection** from the **Operation** filter.</span></span>

    ![Configurar o trabalho de proteção](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="8b92c-210">Backup inicial</span><span class="sxs-lookup"><span data-stu-id="8b92c-210">Initial backup</span></span>
<span data-ttu-id="8b92c-211">Uma vez protegida com uma política, a máquina virtual será exibida na guia **Itens Protegidos** com o status *Protegida (pendente de backup inicial)*.</span><span class="sxs-lookup"><span data-stu-id="8b92c-211">Once the virtual machine is protected with a policy, it shows up under the **Protected Items** tab with the status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="8b92c-212">Por padrão, o primeiro backup agendado é o *backup inicial*.</span><span class="sxs-lookup"><span data-stu-id="8b92c-212">By default, the first scheduled backup is the *initial backup*.</span></span>

<span data-ttu-id="8b92c-213">Para disparar o backup inicial imediatamente após a configuração de proteção:</span><span class="sxs-lookup"><span data-stu-id="8b92c-213">To trigger the initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="8b92c-214">Na parte inferior da página **Itens Protegidos**, clique em **Fazer Backup Agora**.</span><span class="sxs-lookup"><span data-stu-id="8b92c-214">At the bottom of the **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="8b92c-215">O serviço de Backup do Azure cria um trabalho de backup para a operação de backup inicial.</span><span class="sxs-lookup"><span data-stu-id="8b92c-215">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="8b92c-216">Clique na guia **Trabalhos** para exibir a lista de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="8b92c-216">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Backup em andamento](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="8b92c-218">Durante a operação de backup, o serviço de Backup do Azure emite um comando para a extensão de backup em cada máquina virtual a fim de limpar todos os trabalhos de gravação e capturar um instantâneo consistente.</span><span class="sxs-lookup"><span data-stu-id="8b92c-218">During the backup operation, the Azure Backup service issues a command to the backup extension in each virtual machine to flush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="8b92c-219">Quando o backup inicial terminar, o status da máquina virtual na guia **Itens Protegidos** será *Protegido*.</span><span class="sxs-lookup"><span data-stu-id="8b92c-219">When the initial backup finishes, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="8b92c-221">Exibindo detalhes e status do backup</span><span class="sxs-lookup"><span data-stu-id="8b92c-221">Viewing backup status and details</span></span>
<span data-ttu-id="8b92c-222">Depois de protegido, a contagem de máquina virtual também aumenta no resumo da página **Painel** .</span><span class="sxs-lookup"><span data-stu-id="8b92c-222">Once protected, the virtual machine count also increases in the **Dashboard** page summary.</span></span> <span data-ttu-id="8b92c-223">A página **Painel** também mostra o número de trabalhos das últimas 24 horas que foram *bem-sucedidos*, que *falharam* e que estão *em andamento*.</span><span class="sxs-lookup"><span data-stu-id="8b92c-223">The **Dashboard** page also shows the number of jobs from the last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="8b92c-224">Na página **Trabalhos**, use os menus **Status**, **Operação** ou **De** e **Para** a fim de filtrar os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="8b92c-224">On the **Jobs** page, use the **Status**, **Operation**, or **From** and **To** menus to filter the jobs.</span></span>

![Status do backup na página Painel](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="8b92c-226">Os valores no painel são atualizados a cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="8b92c-226">Values in the dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="8b92c-227">Solucionar erros</span><span class="sxs-lookup"><span data-stu-id="8b92c-227">Troubleshooting errors</span></span>
<span data-ttu-id="8b92c-228">Se você enfrentar problemas durante o backup da sua máquina virtual, examine o [artigo sobre solução de problemas de VM](backup-azure-vms-troubleshoot.md) para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="8b92c-228">If you run into issues while backing up your virtual machine, look at the [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b92c-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b92c-229">Next steps</span></span>
* [<span data-ttu-id="8b92c-230">Gerenciar e monitorar suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8b92c-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="8b92c-231">Restaurar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="8b92c-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
