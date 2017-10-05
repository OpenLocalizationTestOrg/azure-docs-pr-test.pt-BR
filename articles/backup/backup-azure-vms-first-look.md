---
title: "Introdução - Fazer backup de VMs do Azure com um cofre de backup | Microsoft Docs"
description: "Use o portal clássico para fazer backup de máquinas virtuais do Azure em um cofre de Backup. Este tutorial explica todas as fases, incluindo a criação do cofre de Backup, o registro das máquinas virtuais, a criação da política de backup e a execução do trabalho de backup inicial."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
ms.assetid: 722820dc-b65f-425c-a9e5-c1946e896a87
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/2/2017
ms.author: markgal;
ms.openlocfilehash: fc31d7654e455ec5b4e4bb9af4cf1a166f1661ee
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="72671-104">Introdução: Fazendo backup de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="72671-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="72671-105">Proteger VMs em um cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="72671-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="72671-106">Proteger as VMs do Azure com um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="72671-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="72671-107">Este tutorial explica as etapas para fazer backup de uma VM (máquina virtual) do Azure em um cofre de backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="72671-107">This tutorial takes you through the steps for backing up an Azure virtual machine (VM) to a backup vault in Azure.</span></span> <span data-ttu-id="72671-108">Este artigo descreve o modelo clássico ou o modelo de implantação do Service Manager para fazer backup de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="72671-108">This article describes the classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="72671-109">As etapas a seguir se aplicam somente a cofres de Backup criados no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="72671-109">The following steps apply only to Backup vaults created in the classic portal.</span></span> <span data-ttu-id="72671-110">A Microsoft recomenda usar o modelo do Resource Manager para novas implantações.</span><span class="sxs-lookup"><span data-stu-id="72671-110">Microsoft recommends using the Resource Manager model for new deployments.</span></span>

<span data-ttu-id="72671-111">Se você estiver interessado em fazer backup de uma VM em um cofre de Serviços de Recuperação que pertence a um grupo de recursos, confira [Introdução: proteger VMs em um cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="72671-111">If you are interested in backing up a VM to a Recovery Services vault that belongs to a Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="72671-112">Para concluir o tutorial a seguir com êxito, estes pré-requisitos devem existir:</span><span class="sxs-lookup"><span data-stu-id="72671-112">To successfully complete the following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="72671-113">Você criou uma VM em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="72671-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="72671-114">A VM tem conectividade com os endereços IP públicos do Azure.</span><span class="sxs-lookup"><span data-stu-id="72671-114">The VM has connectivity to Azure public IP addresses.</span></span> <span data-ttu-id="72671-115">Para obter informações adicionais, veja [Conectividade de rede](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="72671-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="72671-116">O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="72671-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="72671-117">Este tutorial deve ser usado com máquinas virtuais criadas no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="72671-117">This tutorial is for use with virtual machines created in the classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="72671-118">Criar um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="72671-118">Create a backup vault</span></span>
<span data-ttu-id="72671-119">O cofre de backup é uma entidade que armazena todos os pontos de backups e recuperação que foram criados ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="72671-119">A backup vault is an entity that stores all the backups and recovery points that have been created over time.</span></span> <span data-ttu-id="72671-120">O cofre de backup também contém as políticas de backup que serão aplicadas às máquinas virtuais incluídas no backup.</span><span class="sxs-lookup"><span data-stu-id="72671-120">The backup vault also contains the backup policies that are applied to the virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="72671-121">A partir de março de 2017, você não poderá mais usar o portal clássico para criar os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="72671-121">Starting March 2017, you can no longer use the classic portal to create Backup vaults.</span></span>
> <span data-ttu-id="72671-122">Você pode atualizar os cofres de Backup para cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="72671-122">You can upgrade your Backup vaults to Recovery Services vaults.</span></span> <span data-ttu-id="72671-123">Para obter detalhes, veja o artigo [Atualizar um cofre de Backup para um cofre dos Serviços de Recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="72671-123">For details, see the article [Upgrade a Backup vault to a Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="72671-124">A Microsoft incentiva você a atualizar os cofres de Backup para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="72671-124">Microsoft encourages you to upgrade your Backup vaults to Recovery Services vaults.</span></span><br/> <span data-ttu-id="72671-125">Após 15 de outubro de 2017, você não poderá usar o PowerShell para criar os Cofres do Backup.</span><span class="sxs-lookup"><span data-stu-id="72671-125">After October 15, 2017, you can’t use PowerShell to create Backup vaults.</span></span> <span data-ttu-id="72671-126">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="72671-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="72671-127">Todos os Cofres do Backup restantes serão atualizados automaticamente para os cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="72671-127">All remaining Backup vaults will be automatically upgraded to Recovery Services vaults.</span></span>
>- <span data-ttu-id="72671-128">Você não poderá acessar os dados de backup no portal clássico.</span><span class="sxs-lookup"><span data-stu-id="72671-128">You won't be able to access your backup data in the classic portal.</span></span> <span data-ttu-id="72671-129">Em vez disso, use o portal do Azure para acessar os dados de backup nos cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="72671-129">Instead, use the Azure portal to access your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="72671-130">Descobrir e registrar máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="72671-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="72671-131">Antes de registrar a VM em um cofre, execute o processo de descoberta para identificar novas VMs.</span><span class="sxs-lookup"><span data-stu-id="72671-131">Before registering the VM with a vault, run the discovery process to identify any new VMs.</span></span> <span data-ttu-id="72671-132">Isso retorna uma lista de máquinas virtuais na assinatura, juntamente com informações adicionais, como o nome do serviço de nuvem e a região.</span><span class="sxs-lookup"><span data-stu-id="72671-132">This returns a list of virtual machines in the subscription, along with additional information like the cloud service name and the region.</span></span>

1. <span data-ttu-id="72671-133">Entrar no [portal Clássico do Azure](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="72671-133">Sign in to the [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="72671-134">No portal clássico do Azure, clique em **Serviços de Recuperação** para abrir a lista de cofres dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="72671-134">In the Azure classic portal, click **Recovery Services** to open the list of Recovery Services vaults.</span></span>
    <span data-ttu-id="72671-135">![Selecionar carga de trabalho](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="72671-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="72671-136">Na lista de cofres, escolha o cofre para fazer backup de uma VM.</span><span class="sxs-lookup"><span data-stu-id="72671-136">From the list of vaults, select the vault to back up a VM.</span></span>

    <span data-ttu-id="72671-137">Quando você seleciona o cofre, ele é aberto na página **Início Rápido**</span><span class="sxs-lookup"><span data-stu-id="72671-137">When you select your vault, it opens in the **Quick Start** page</span></span>
4. <span data-ttu-id="72671-138">No menu do cofre, clique em **Itens Registrados**.</span><span class="sxs-lookup"><span data-stu-id="72671-138">From the vault menu, click **Registered Items**.</span></span>

    ![Selecionar carga de trabalho](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="72671-140">No menu **Tipo**, selecione **Máquina Virtual do Azure**.</span><span class="sxs-lookup"><span data-stu-id="72671-140">From the **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Selecionar carga de trabalho](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="72671-142">Clique em **DESCOBRIR** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="72671-142">Click **DISCOVER** at the bottom of the page.</span></span>
    <span data-ttu-id="72671-143">![Botão Descobrir](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="72671-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="72671-144">O processo de descoberta pode ser executado por alguns minutos, enquanto as máquinas virtuais estão sendo tabuladas.</span><span class="sxs-lookup"><span data-stu-id="72671-144">The discovery process may take a few minutes while the virtual machines are being tabulated.</span></span> <span data-ttu-id="72671-145">Há uma notificação na parte inferior da tela que informa você de que o processo está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="72671-145">There is a notification at the bottom of the screen that lets you know that the process is running.</span></span>

    ![Descobrir VMs](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="72671-147">As alterações de notificação quando o processo é concluído.</span><span class="sxs-lookup"><span data-stu-id="72671-147">The notification changes when the process is complete.</span></span>

    ![Descoberta concluída](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="72671-149">Clique em **REGISTRAR** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="72671-149">Click **REGISTER** at the bottom of the page.</span></span>
    <span data-ttu-id="72671-150">![Botão Registrar](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="72671-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="72671-151">No menu de atalho **Registrar Itens** , selecione as máquinas virtuais que você deseja registrar.</span><span class="sxs-lookup"><span data-stu-id="72671-151">In the **Register Items** shortcut menu, select the virtual machines that you want to register.</span></span>

   > [!TIP]
   > <span data-ttu-id="72671-152">Várias máquinas virtuais podem ser registradas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="72671-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="72671-153">Um trabalho é criado para cada máquina virtual selecionada.</span><span class="sxs-lookup"><span data-stu-id="72671-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="72671-154">Clique em **Exibir Trabalho** na notificação para ir para a página **Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="72671-154">Click **View Job** in the notification to go to the **Jobs** page.</span></span>

    ![Registrar trabalho](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="72671-156">A máquina virtual também aparece na lista de itens registrados junto com o status da operação de registro.</span><span class="sxs-lookup"><span data-stu-id="72671-156">The virtual machine also appears in the list of registered items, along with the status of the registration operation.</span></span>

    ![Status de registro 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="72671-158">Quando a operação for concluída, o status será alterado para refletir o estado *registrado* .</span><span class="sxs-lookup"><span data-stu-id="72671-158">When the operation completes, the status changes to reflect the *registered* state.</span></span>

    ![Status de registro 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-the-vm-agent-on-the-virtual-machine"></a><span data-ttu-id="72671-160">Instalar o Agente de VM na máquina virtual</span><span class="sxs-lookup"><span data-stu-id="72671-160">Install the VM Agent on the virtual machine</span></span>
<span data-ttu-id="72671-161">O Agente de VM do Azure deve ser instalado na máquina virtual do Azure para a extensão de Backup funcionar.</span><span class="sxs-lookup"><span data-stu-id="72671-161">The Azure VM Agent must be installed on the Azure virtual machine for the Backup extension to work.</span></span> <span data-ttu-id="72671-162">Se sua VM tiver sido criada da galeria do Azure, o agente de VM já estará presente na VM; você pode pular para [proteção de suas VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="72671-162">If your VM was created from the Azure gallery, the VM Agent is already present on the VM; you can skip to [protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="72671-163">Se sua VM tiver migrado de um datacenter local, a VM provavelmente não terá o agente instalado.</span><span class="sxs-lookup"><span data-stu-id="72671-163">If your VM migrated from an on-premises datacenter, the VM probably does not have the VM Agent installed.</span></span> <span data-ttu-id="72671-164">Você deve instalar o Agente de VM na máquina virtual antes de continuar a proteger a VM.</span><span class="sxs-lookup"><span data-stu-id="72671-164">You must install the VM Agent on the virtual machine before proceeding to protect the VM.</span></span> <span data-ttu-id="72671-165">Para obter etapas detalhadas sobre como instalar o Agente de VM, confira a [seção Agente de VM do artigo Backup de VMs](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="72671-165">For detailed steps on installing the VM Agent, see the [VM Agent section of the Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-the-backup-policy"></a><span data-ttu-id="72671-166">Criar a política de backup</span><span class="sxs-lookup"><span data-stu-id="72671-166">Create the backup policy</span></span>
<span data-ttu-id="72671-167">Antes de disparar o trabalho de backup inicial, defina a agenda de quando os instantâneos de backup serão feitos.</span><span class="sxs-lookup"><span data-stu-id="72671-167">Before you trigger the initial backup job, set the schedule when backup snapshots are taken.</span></span> <span data-ttu-id="72671-168">A agenda de quando os instantâneos de backup são criados e por quanto tempo esses instantâneos serão mantido compõem a política de backup.</span><span class="sxs-lookup"><span data-stu-id="72671-168">The schedule when backup snapshots are taken, and the length of time those snapshots are retained, is the backup policy.</span></span> <span data-ttu-id="72671-169">As informações de retenção se baseiam no esquema de rotação de backup Avô-pai-filho.</span><span class="sxs-lookup"><span data-stu-id="72671-169">The retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="72671-170">Navegue até o cofre de backup, em **Serviços de Recuperação** no Portal Clássico do Azure e clique em **Itens Registrados**.</span><span class="sxs-lookup"><span data-stu-id="72671-170">Navigate to the backup vault under **Recovery Services** in the Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="72671-171">Selecione **Máquina Virtual do Azure** no menu suspenso.</span><span class="sxs-lookup"><span data-stu-id="72671-171">Select **Azure Virtual Machine** from the drop-down menu.</span></span>

    ![Selecionar a carga de trabalho no portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="72671-173">Na parte inferior da página, clique em **PROTEGER** .</span><span class="sxs-lookup"><span data-stu-id="72671-173">Click **PROTECT** at the bottom of the page.</span></span>
    <span data-ttu-id="72671-174">![Clique em Proteger](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="72671-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="72671-175">O **assistente Proteger Itens** é mostrado e lista *apenas* as máquinas virtuais registradas e não protegidas.</span><span class="sxs-lookup"><span data-stu-id="72671-175">The **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Configurar proteção em escala](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="72671-177">Selecione as máquinas virtuais que deseja proteger.</span><span class="sxs-lookup"><span data-stu-id="72671-177">Select the virtual machines that you want to protect.</span></span>

    <span data-ttu-id="72671-178">Se houver duas ou mais máquinas virtuais com o mesmo nome, use o Serviço de Nuvem para distinguir entre elas.</span><span class="sxs-lookup"><span data-stu-id="72671-178">If there are two or more virtual machines with the same name, use the Cloud Service to distinguish between the virtual machines.</span></span>
5. <span data-ttu-id="72671-179">No menu **Configurar proteção** , escolha uma política existente ou crie uma nova política para proteger as máquinas virtuais que você identificou.</span><span class="sxs-lookup"><span data-stu-id="72671-179">On the **Configure protection** menu select an existing policy or create a new policy to protect the virtual machines that you identified.</span></span>

    <span data-ttu-id="72671-180">Os novos cofres de Backup têm uma política padrão associada ao cofre.</span><span class="sxs-lookup"><span data-stu-id="72671-180">New Backup vaults have a default policy associated with the vault.</span></span> <span data-ttu-id="72671-181">Essa política usa um instantâneo diário a cada noite, e o instantâneo diário é mantido por 30 dias.</span><span class="sxs-lookup"><span data-stu-id="72671-181">This policy takes a daily snapshot each evening, and the daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="72671-182">Cada política de backup pode ter várias máquinas virtuais associadas a ela.</span><span class="sxs-lookup"><span data-stu-id="72671-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="72671-183">No entanto, a máquina virtual só pode estar associada a apenas uma política de cada vez.</span><span class="sxs-lookup"><span data-stu-id="72671-183">However, the virtual machine can only be associated with one policy at a time.</span></span>

    ![Proteger com nova política](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="72671-185">Uma política de backup também inclui um esquema de retenção para os backups agendados.</span><span class="sxs-lookup"><span data-stu-id="72671-185">A backup policy includes a retention scheme for the scheduled backups.</span></span> <span data-ttu-id="72671-186">Se você selecionar uma política de backup, não será possível modificar as opções de retenção na próxima etapa.</span><span class="sxs-lookup"><span data-stu-id="72671-186">If you select an existing backup policy, you will be unable to modify the retention options in the next step.</span></span>
   >
   >
6. <span data-ttu-id="72671-187">Em **Intervalo de Retenção** , defina o escopo diário, semanal, mensal e anual para os pontos de backup específicos.</span><span class="sxs-lookup"><span data-stu-id="72671-187">On **Retention Range** define the daily, weekly, monthly, and yearly scope for the specific backup points.</span></span>

    ![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="72671-189">A política de retenção especifica o período de armazenamento de um backup.</span><span class="sxs-lookup"><span data-stu-id="72671-189">Retention policy specifies the length of time for storing a backup.</span></span> <span data-ttu-id="72671-190">Você pode especificar políticas de retenção diferentes com base em quando o backup é feito.</span><span class="sxs-lookup"><span data-stu-id="72671-190">You can specify different retention policies based on when the backup is taken.</span></span>
7. <span data-ttu-id="72671-191">Clique em **Trabalhos** para exibir a lista de trabalhos de **Configurar Proteção**.</span><span class="sxs-lookup"><span data-stu-id="72671-191">Click **Jobs** to view the list of **Configure Protection** jobs.</span></span>

    ![Configurar o trabalho de proteção](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="72671-193">Agora que a política foi estabelecida, vá para a próxima etapa e execute o backup inicial.</span><span class="sxs-lookup"><span data-stu-id="72671-193">Now that you've established the policy, go to the next step and run the initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="72671-194">Backup inicial</span><span class="sxs-lookup"><span data-stu-id="72671-194">Initial backup</span></span>
<span data-ttu-id="72671-195">Após uma máquina virtual ser protegida com uma política, você poderá exibir essa relação na guia **Itens Protegidos** . Até que o backup inicial ocorra, o **Status de Proteção** será mostrado como **Protegido – (backup inicial pendente)**.</span><span class="sxs-lookup"><span data-stu-id="72671-195">Once a virtual machine has been protected with a policy, you can view that relationship on the **Protected Items** tab. Until the initial backup occurs, the **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="72671-196">Por padrão, o primeiro backup agendado é o *backup inicial*.</span><span class="sxs-lookup"><span data-stu-id="72671-196">By default, the first scheduled backup is the *initial backup*.</span></span>

![Backup pendente](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="72671-198">Para começar o backup inicial agora:</span><span class="sxs-lookup"><span data-stu-id="72671-198">To start the initial backup now:</span></span>

1. <span data-ttu-id="72671-199">Na página **Itens Protegidos**, clique em **Fazer Backup Agora** na parte inferior da página.</span><span class="sxs-lookup"><span data-stu-id="72671-199">On the **Protected Items** page, click **Backup Now** at the bottom of the page.</span></span>
    <span data-ttu-id="72671-200">![Ícone de Fazer Backup Agora](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="72671-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="72671-201">O serviço de Backup do Azure cria um trabalho de backup para a operação de backup inicial.</span><span class="sxs-lookup"><span data-stu-id="72671-201">The Azure Backup service creates a backup job for the initial backup operation.</span></span>
2. <span data-ttu-id="72671-202">Clique na guia **Trabalhos** para exibir a lista de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="72671-202">Click the **Jobs** tab to view the list of jobs.</span></span>

    ![Backup em andamento](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="72671-204">Após a conclusão do backup inicial, o status da máquina virtual na guia **Itens Protegidos** é *Protegida*.</span><span class="sxs-lookup"><span data-stu-id="72671-204">When initial backup is complete, the status of the virtual machine in the **Protected Items** tab is *Protected*.</span></span>

    ![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="72671-206">O backup de máquinas virtuais é um processo local.</span><span class="sxs-lookup"><span data-stu-id="72671-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="72671-207">Você não pode fazer backup de máquinas virtuais de uma região em um cofre de backup em outra região.</span><span class="sxs-lookup"><span data-stu-id="72671-207">You cannot back up virtual machines from one region to a backup vault in another region.</span></span> <span data-ttu-id="72671-208">Assim, para todas as regiões do Azure que tenham VMs que precisem de backup, pelo menos um cofre de backup deverá ser criado nessa região.</span><span class="sxs-lookup"><span data-stu-id="72671-208">So, for every Azure region that has VMs that need to be backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="72671-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="72671-209">Next steps</span></span>
<span data-ttu-id="72671-210">Agora que você já fez um backup de uma VM, há várias etapas subsequentes pode poderiam ser interessantes.</span><span class="sxs-lookup"><span data-stu-id="72671-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="72671-211">A etapa mais lógica é se familiarizar com a restauração de dados para uma máquina virtual.</span><span class="sxs-lookup"><span data-stu-id="72671-211">The most logical step is to familiarize yourself with restoring data to a VM.</span></span> <span data-ttu-id="72671-212">No entanto, há tarefas de gerenciamento que o ajudarão a entender como manter os dados seguros e minimizar os custos.</span><span class="sxs-lookup"><span data-stu-id="72671-212">However, there are management tasks that will help you understand how to keep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="72671-213">Gerenciar e monitorar suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="72671-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="72671-214">Restaurar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="72671-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="72671-215">Diretrizes de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="72671-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="72671-216">Perguntas?</span><span class="sxs-lookup"><span data-stu-id="72671-216">Questions?</span></span>
<span data-ttu-id="72671-217">Se você tiver dúvidas ou gostaria de ver algum recurso incluído, [envie-nos seus comentários](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="72671-217">If you have questions, or if there is any feature that you would like to see included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
