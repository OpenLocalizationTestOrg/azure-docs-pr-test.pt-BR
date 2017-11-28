---
title: "aaaBack o Cofre de backup de tooa implantado clássico máquinas de virtuais do Azure | Microsoft Docs"
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
ms.openlocfilehash: 048e32d9b2bd5bdd7a125225a71a6d805bb4fbd4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-classic-portal"></a><span data-ttu-id="75d9d-104">Fazer backup de máquinas virtuais do Azure (portal clássico)</span><span class="sxs-lookup"><span data-stu-id="75d9d-104">Back up Azure virtual machines (classic portal)</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="75d9d-105">Fazer backup de Cofre de serviços de tooRecovery de VMs</span><span class="sxs-lookup"><span data-stu-id="75d9d-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="75d9d-106">Fazer backup de máquinas virtuais tooBackup cofre</span><span class="sxs-lookup"><span data-stu-id="75d9d-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="75d9d-107">Este artigo fornece procedimentos hello para fazer backup de um cofre de Backup tooa implantado clássico do Azure VM (máquina virtual).</span><span class="sxs-lookup"><span data-stu-id="75d9d-107">This article provides hello procedures for backing up a Classic-deployed Azure virtual machine (VM) tooa Backup vault.</span></span> <span data-ttu-id="75d9d-108">Há algumas tarefas que você precisa tootake aos cuidados de antes de você pode fazer backup de uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="75d9d-108">There are a few tasks you need tootake care of before you can back up an Azure virtual machine.</span></span> <span data-ttu-id="75d9d-109">Se você ainda não tiver feito Olá completa, portanto, [pré-requisitos](backup-azure-vms-prepare.md) tooprepare seu ambiente para fazer backup de suas VMs.</span><span class="sxs-lookup"><span data-stu-id="75d9d-109">If you haven't already done so, complete hello [prerequisites](backup-azure-vms-prepare.md) tooprepare your environment for backing up your VMs.</span></span>

<span data-ttu-id="75d9d-110">Para obter mais informações, consulte os artigos de saudação em [Planejando sua infra-estrutura de backup de VM no Azure](backup-azure-vms-introduction.md) e [máquinas virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="75d9d-110">For additional information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

> [!NOTE]
> <span data-ttu-id="75d9d-111">O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="75d9d-111">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="75d9d-112">Um cofre de Backup só pode proteger VMs com implantação clássica.</span><span class="sxs-lookup"><span data-stu-id="75d9d-112">A Backup vault can only protect Classic-deployed VMs.</span></span> <span data-ttu-id="75d9d-113">Você não pode proteger VMs implantadas pelo Resource Manager com um cofre de Backup.</span><span class="sxs-lookup"><span data-stu-id="75d9d-113">You cannot protect Resource Manager-deployed VMs with a Backup vault.</span></span> <span data-ttu-id="75d9d-114">Consulte [VMs tooRecovery serviços Cofre de backup](backup-azure-arm-vms.md) para obter detalhes sobre como trabalhar com serviços de recuperação os cofres.</span><span class="sxs-lookup"><span data-stu-id="75d9d-114">See [Back up VMs tooRecovery Services vault](backup-azure-arm-vms.md) for details on working with Recovery Services vaults.</span></span>
>
>

<span data-ttu-id="75d9d-115">Fazer o backup de máquinas virtuais do Azure envolve três etapas principais:</span><span class="sxs-lookup"><span data-stu-id="75d9d-115">Backing up Azure virtual machines involves three key steps:</span></span>

![Três etapas tooback a uma máquina virtual IaaS do Azure](./media/backup-azure-vms/3-steps-for-backup.png)

> [!NOTE]
> <span data-ttu-id="75d9d-117">O backup de máquinas virtuais é um processo local.</span><span class="sxs-lookup"><span data-stu-id="75d9d-117">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="75d9d-118">Você não pode fazer backup de máquinas virtuais em uma região tooa Cofre de backup em outra região.</span><span class="sxs-lookup"><span data-stu-id="75d9d-118">You cannot back up virtual machines in one region tooa backup vault in another region.</span></span> <span data-ttu-id="75d9d-119">Portanto, você deve criar um cofre de backup em cada região do Azure na qual existam VMs das quais serão feitos backups.</span><span class="sxs-lookup"><span data-stu-id="75d9d-119">So, you must create a backup vault in each Azure region, where there are VMs that will be backed up.</span></span>
>
> [!IMPORTANT]
> <span data-ttu-id="75d9d-120">A partir de março de 2017, você não pode usar os cofres de Backup Olá toocreate portal clássico.</span><span class="sxs-lookup"><span data-stu-id="75d9d-120">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="75d9d-121">Agora você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="75d9d-121">You can now upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="75d9d-122">Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="75d9d-122">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="75d9d-123">A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="75d9d-123">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="75d9d-124">Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="75d9d-124">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="75d9d-125">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="75d9d-125">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="75d9d-126">Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.</span><span class="sxs-lookup"><span data-stu-id="75d9d-126">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="75d9d-127">Você não será capaz de tooaccess os dados de backup no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="75d9d-127">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="75d9d-128">Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="75d9d-128">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="step-1---discover-azure-virtual-machines"></a><span data-ttu-id="75d9d-129">Etapa 1 - Descobrir máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="75d9d-129">Step 1 - Discover Azure virtual machines</span></span>
<span data-ttu-id="75d9d-130">tooensure qualquer nova assinatura adicionado toohello máquinas virtuais (VMs) são identificados antes de registrar, executar o processo de descoberta de saudação.</span><span class="sxs-lookup"><span data-stu-id="75d9d-130">tooensure any new virtual machines (VMs) added toohello subscription are identified before registering, run hello discovery process.</span></span> <span data-ttu-id="75d9d-131">Olá processar consultas do Azure para obter lista de saudação de máquinas virtuais na assinatura hello, juntamente com informações adicionais, como nome de serviço de nuvem hello e região Olá.</span><span class="sxs-lookup"><span data-stu-id="75d9d-131">hello process queries Azure for hello list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="75d9d-132">Entrar toohello [portal clássico](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="75d9d-132">Sign in toohello [Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="75d9d-133">Na lista de saudação de serviços do Azure, clique em **dos serviços de recuperação** tooopen lista de saudação de cofres de Backup e recuperação de Site.</span><span class="sxs-lookup"><span data-stu-id="75d9d-133">In hello list of Azure services, click **Recovery Services** tooopen hello list of Backup and Site Recovery vaults.</span></span>
    <span data-ttu-id="75d9d-134">![Abrir listas de cofres](./media/backup-azure-vms/choose-vault-list.png)</span><span class="sxs-lookup"><span data-stu-id="75d9d-134">![Open vault list](./media/backup-azure-vms/choose-vault-list.png)</span></span>
3. <span data-ttu-id="75d9d-135">Na lista de saudação de cofres de Backup, selecione Olá cofre tooback backup de uma VM.</span><span class="sxs-lookup"><span data-stu-id="75d9d-135">In hello list of Backup vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="75d9d-136">Se esse for um novo portal de saudação do cofre abre toohello **início rápido** página.</span><span class="sxs-lookup"><span data-stu-id="75d9d-136">If this is a new vault hello portal opens toohello **Quick Start** page.</span></span>

    ![Abrir o menu Itens registrados](./media/backup-azure-vms/vault-quick-start.png)

    <span data-ttu-id="75d9d-138">Se o cofre Olá tenha sido previamente configurada, o portal de saudação abre o menu de toohello usado mais recentemente.</span><span class="sxs-lookup"><span data-stu-id="75d9d-138">If hello vault has previously been configured, hello portal opens toohello most recently used menu.</span></span>
4. <span data-ttu-id="75d9d-139">No menu de cofre hello (na parte superior de saudação da página de saudação), clique em **itens registrados**.</span><span class="sxs-lookup"><span data-stu-id="75d9d-139">From hello vault menu (at hello top of hello page), click **Registered Items**.</span></span>

    ![Abrir o menu Itens registrados](./media/backup-azure-vms/vault-menu.png)
5. <span data-ttu-id="75d9d-141">De saudação **tipo** menu, selecione **Máquina Virtual do Azure**.</span><span class="sxs-lookup"><span data-stu-id="75d9d-141">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Selecionar carga de trabalho](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="75d9d-143">Clique em **DISCOVER** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="75d9d-143">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="75d9d-144">![Botão Descobrir](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="75d9d-144">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="75d9d-145">o processo de descoberta Olá pode levar alguns minutos enquanto estão sendo tabuladas máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="75d9d-145">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="75d9d-146">Há uma notificação na parte inferior da saudação da tela de saudação que permite que você saiba que o processo de hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="75d9d-146">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Descobrir VMs](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="75d9d-148">Olá notificação muda quando Olá processo for concluído.</span><span class="sxs-lookup"><span data-stu-id="75d9d-148">hello notification changes when hello process is complete.</span></span> <span data-ttu-id="75d9d-149">Se o processo de descoberta de saudação não localizou máquinas virtuais de hello, primeiro verifique Olá VMs.</span><span class="sxs-lookup"><span data-stu-id="75d9d-149">If hello discovery process did not find hello virtual machines, first ensure hello VMs exist.</span></span> <span data-ttu-id="75d9d-150">Se houver VMs hello, certifique-se de Olá VMs estão em Olá mesmo região Olá Cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="75d9d-150">If hello VMs exist, ensure hello VMs are in hello same region as hello backup vault.</span></span> <span data-ttu-id="75d9d-151">Se as VMs de saudação existem e estão em Olá mesma região, certifique-se de que VMs Olá ainda não estiverem registrados tooa Cofre de backup.</span><span class="sxs-lookup"><span data-stu-id="75d9d-151">If hello VMs exist and are in hello same region, ensure hello VMs are not already registered tooa backup vault.</span></span> <span data-ttu-id="75d9d-152">Se uma VM for atribuído tooa Cofre de backup não é disponível toobe atribuído tooother cofres de backup.</span><span class="sxs-lookup"><span data-stu-id="75d9d-152">If a VM is assigned tooa backup vault it is not available toobe assigned tooother backup vaults.</span></span>

    ![Descoberta concluída](./media/backup-azure-vms/discovery-complete.png)

    <span data-ttu-id="75d9d-154">Depois que você descobriu novos itens de hello, vá tooStep 2 e registrar suas VMs.</span><span class="sxs-lookup"><span data-stu-id="75d9d-154">Once you have discovered hello new items, go tooStep 2 and register your VMs.</span></span>

## <a name="step-2---register-azure-virtual-machines"></a><span data-ttu-id="75d9d-155">Etapa 2 - Registrar as máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="75d9d-155">Step 2 - Register Azure virtual machines</span></span>
<span data-ttu-id="75d9d-156">Registrar tooassociate uma máquina virtual do Azure com hello serviço Backup do Azure.</span><span class="sxs-lookup"><span data-stu-id="75d9d-156">You register an Azure virtual machine tooassociate it with hello Azure Backup service.</span></span> <span data-ttu-id="75d9d-157">Normalmente, é uma atividade realizada uma única vez.</span><span class="sxs-lookup"><span data-stu-id="75d9d-157">This is typically a one-time activity.</span></span>

1. <span data-ttu-id="75d9d-158">Navegue toohello Cofre de backup em **dos serviços de recuperação** Olá portal do Azure e, em seguida, clique em **itens registrados**.</span><span class="sxs-lookup"><span data-stu-id="75d9d-158">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="75d9d-159">Selecione **Máquina Virtual do Azure** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="75d9d-159">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Selecionar carga de trabalho](./media/backup-azure-vms/discovery-select-workload.png)
3. <span data-ttu-id="75d9d-161">Clique em **registrar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="75d9d-161">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="75d9d-162">![Botão Registrar](./media/backup-azure-vms/register-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="75d9d-162">![Register button](./media/backup-azure-vms/register-button-only.png)</span></span>
4. <span data-ttu-id="75d9d-163">Em Olá **registrar itens** menu de atalho, selecione Olá máquinas de virtuais que você deseja tooregister.</span><span class="sxs-lookup"><span data-stu-id="75d9d-163">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span> <span data-ttu-id="75d9d-164">Se houver dois ou mais máquinas virtuais com hello mesmo nome, use toodistinguish de serviço de nuvem Olá entre eles.</span><span class="sxs-lookup"><span data-stu-id="75d9d-164">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between them.</span></span>

   > [!TIP]
   > <span data-ttu-id="75d9d-165">Várias máquinas virtuais podem ser registradas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="75d9d-165">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="75d9d-166">Um trabalho é criado para cada máquina virtual selecionada.</span><span class="sxs-lookup"><span data-stu-id="75d9d-166">A job is created for each virtual machine that you've selected.</span></span>
5. <span data-ttu-id="75d9d-167">Clique em **Exibir trabalho** em Olá notificação toogo toohello **trabalhos** página.</span><span class="sxs-lookup"><span data-stu-id="75d9d-167">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Registrar trabalho](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="75d9d-169">máquina virtual de saudação também aparece na lista de saudação de itens registrados, junto com o status de saudação da operação de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="75d9d-169">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Status de registro 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="75d9d-171">Quando Olá operação for concluída, o status de saudação muda Olá tooreflect *registrado* estado.</span><span class="sxs-lookup"><span data-stu-id="75d9d-171">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Status de registro 2](./media/backup-azure-vms/register-status02.png)

## <a name="step-3---protect-azure-virtual-machines"></a><span data-ttu-id="75d9d-173">Etapa 3 - Proteger máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="75d9d-173">Step 3 - Protect Azure virtual machines</span></span>
<span data-ttu-id="75d9d-174">Agora você pode configurar uma política de backup e retenção para a máquina virtual de saudação.</span><span class="sxs-lookup"><span data-stu-id="75d9d-174">Now you can set up a backup and retention policy for hello virtual machine.</span></span> <span data-ttu-id="75d9d-175">Várias máquinas virtuais podem ser protegidas usando uma única ação de proteção.</span><span class="sxs-lookup"><span data-stu-id="75d9d-175">Multiple virtual machines can be protected by using a single protect action.</span></span>

<span data-ttu-id="75d9d-176">Os cofres de Backup do Azure criados depois de maio de 2015 vem com uma política padrão incorporados cofre hello.</span><span class="sxs-lookup"><span data-stu-id="75d9d-176">Azure Backup vaults created after May 2015 come with a default policy built into hello vault.</span></span> <span data-ttu-id="75d9d-177">Essa política padrão é fornecida com uma retenção padrão de 30 dias e agendamento de backup de uma vez por dia.</span><span class="sxs-lookup"><span data-stu-id="75d9d-177">This default policy comes with a default retention of 30 days and a once-daily backup schedule.</span></span>

1. <span data-ttu-id="75d9d-178">Navegue toohello Cofre de backup em **dos serviços de recuperação** Olá portal do Azure e, em seguida, clique em **itens registrados**.</span><span class="sxs-lookup"><span data-stu-id="75d9d-178">Navigate toohello backup vault under **Recovery Services** in hello Azure portal, and then click **Registered Items**.</span></span>
2. <span data-ttu-id="75d9d-179">Selecione **Máquina Virtual do Azure** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="75d9d-179">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Selecionar a carga de trabalho no portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="75d9d-181">Clique em **proteger** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="75d9d-181">Click **PROTECT** at hello bottom of hello page.</span></span>

    <span data-ttu-id="75d9d-182">Olá **proteger itens assistente** é exibida.</span><span class="sxs-lookup"><span data-stu-id="75d9d-182">hello **Protect Items wizard** appears.</span></span> <span data-ttu-id="75d9d-183">Assistente de saudação lista apenas máquinas virtuais que são registradas e não protegidas.</span><span class="sxs-lookup"><span data-stu-id="75d9d-183">hello wizard only lists virtual machines that are registered and not protected.</span></span> <span data-ttu-id="75d9d-184">Selecione a saudação de máquinas virtuais que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="75d9d-184">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="75d9d-185">Se houver dois ou mais máquinas virtuais com hello mesmo nome, use toodistinguish de serviço de nuvem Olá entre máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="75d9d-185">If there are two or more virtual machines with hello same name, use hello cloud service toodistinguish between hello virtual machines.</span></span>

   > [!TIP]
   > <span data-ttu-id="75d9d-186">Você pode proteger várias máquinas virtuais de uma só vez.</span><span class="sxs-lookup"><span data-stu-id="75d9d-186">You can protect multiple virtual machines at one time.</span></span>
   >
   >

    ![Configurar proteção em escala](./media/backup-azure-vms/protect-at-scale.png)

4. <span data-ttu-id="75d9d-188">Escolha um **agendamento de backup** tooback backup de máquinas virtuais Olá que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="75d9d-188">Choose a **backup schedule** tooback up hello virtual machines that you've selected.</span></span> <span data-ttu-id="75d9d-189">Escolha um conjunto existente de políticas ou defina um novo.</span><span class="sxs-lookup"><span data-stu-id="75d9d-189">You can pick from an existing set of policies or define a new one.</span></span>

    <span data-ttu-id="75d9d-190">Cada política de backup pode ter várias máquinas virtuais associadas a ela.</span><span class="sxs-lookup"><span data-stu-id="75d9d-190">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="75d9d-191">No entanto, máquina virtual de saudação só pode ser associada com uma política em qualquer ponto no tempo.</span><span class="sxs-lookup"><span data-stu-id="75d9d-191">However, hello virtual machine can only be associated with one policy at any given point in time.</span></span>

    ![Proteger com nova política](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="75d9d-193">Uma política de backup inclui um esquema de retenção para backups agendado de saudação.</span><span class="sxs-lookup"><span data-stu-id="75d9d-193">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="75d9d-194">Se você selecionar uma política de backup existente, você não pode modificar as opções de retenção de saudação na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="75d9d-194">If you select an existing backup policy, you cannot modify hello retention options in hello next step.</span></span>
   >
   >

5. <span data-ttu-id="75d9d-195">Escolha um **período de retenção** tooassociate com backups de saudação.</span><span class="sxs-lookup"><span data-stu-id="75d9d-195">Choose a **retention range** tooassociate with hello backups.</span></span>

    ![Proteger com retenção flexível](./media/backup-azure-vms/policy-retention.png)

    <span data-ttu-id="75d9d-197">Política de retenção Especifica Olá período de tempo para armazenar um backup.</span><span class="sxs-lookup"><span data-stu-id="75d9d-197">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="75d9d-198">Você pode especificar diferentes políticas de retenção com base em quando é feito backup hello.</span><span class="sxs-lookup"><span data-stu-id="75d9d-198">You can specify different retention policies based on when hello backup is taken.</span></span> <span data-ttu-id="75d9d-199">Por exemplo, um ponto de backup feito diariamente (que funciona como um ponto de recuperação operacional) pode ser preservado durante 90 dias.</span><span class="sxs-lookup"><span data-stu-id="75d9d-199">For example, a backup point taken daily (which serves as an operational recovery point) might be preserved for 90 days.</span></span> <span data-ttu-id="75d9d-200">Em comparação, um ponto de backup feito no final de saudação de cada trimestre (para fins de auditoria) talvez seja necessário toobe preservado para muitos meses ou anos.</span><span class="sxs-lookup"><span data-stu-id="75d9d-200">In comparison, a backup point taken at hello end of each quarter (for audit purposes) may need toobe preserved for many months or years.</span></span>

    ![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="75d9d-202">Nesta imagem de exemplo:</span><span class="sxs-lookup"><span data-stu-id="75d9d-202">In this example image:</span></span>

   * <span data-ttu-id="75d9d-203">**Política de retenção diária**: os backups diários são armazenados por 30 dias.</span><span class="sxs-lookup"><span data-stu-id="75d9d-203">**Daily retention policy**: Backups taken daily are stored for 30 days.</span></span>
   * <span data-ttu-id="75d9d-204">**Política de retenção semanal**: os backups feitos todas as semanas aos domingos serão preservados por 104 semanas.</span><span class="sxs-lookup"><span data-stu-id="75d9d-204">**Weekly retention policy**: Backups taken every week on Sunday are preserved for 104 weeks.</span></span>
   * <span data-ttu-id="75d9d-205">**Política de retenção mensal**: Backups feitos em Olá último domingo de cada mês são preservados para 120 meses.</span><span class="sxs-lookup"><span data-stu-id="75d9d-205">**Monthly retention policy**: Backups taken on hello last Sunday of each month are preserved for 120 months.</span></span>
   * <span data-ttu-id="75d9d-206">**Política de retenção anual**: Backups feitos em Olá primeiro domingo de cada janeiro são preservados para 99 anos.</span><span class="sxs-lookup"><span data-stu-id="75d9d-206">**Yearly retention policy**: Backups taken on hello first Sunday of every January are preserved for 99 years.</span></span>

     <span data-ttu-id="75d9d-207">Um trabalho é criado a política de proteção tooconfigure hello e associar a política de toothat Olá máquinas virtuais para cada máquina virtual que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="75d9d-207">A job is created tooconfigure hello protection policy and associate hello virtual machines toothat policy for each virtual machine that you've selected.</span></span>
6. <span data-ttu-id="75d9d-208">lista de saudação tooview de **configurar proteção** trabalhos, no menu de cofres hello, clique em **trabalhos** e selecione **configurar proteção** de saudação **operação**  filtro.</span><span class="sxs-lookup"><span data-stu-id="75d9d-208">tooview hello list of **Configure Protection** jobs, from hello vaults menu, click **Jobs** and select **Configure Protection** from hello **Operation** filter.</span></span>

    ![Configurar o trabalho de proteção](./media/backup-azure-vms/protect-configureprotection.png)

## <a name="initial-backup"></a><span data-ttu-id="75d9d-210">Backup inicial</span><span class="sxs-lookup"><span data-stu-id="75d9d-210">Initial backup</span></span>
<span data-ttu-id="75d9d-211">Depois que a máquina virtual de saudação é protegida com uma política, ele é exibido em Olá **itens protegidos** guia com o status de saudação do *protegido - (pendente backup inicial)*.</span><span class="sxs-lookup"><span data-stu-id="75d9d-211">Once hello virtual machine is protected with a policy, it shows up under hello **Protected Items** tab with hello status of *Protected - (pending initial backup)*.</span></span> <span data-ttu-id="75d9d-212">Por padrão, o primeiro backup agendado de saudação é Olá *backup inicial*.</span><span class="sxs-lookup"><span data-stu-id="75d9d-212">By default, hello first scheduled backup is hello *initial backup*.</span></span>

<span data-ttu-id="75d9d-213">backup inicial de saudação de tootrigger imediatamente após a configuração de proteção:</span><span class="sxs-lookup"><span data-stu-id="75d9d-213">tootrigger hello initial backup immediately after configuring protection:</span></span>

1. <span data-ttu-id="75d9d-214">Na parte inferior de saudação do hello **itens protegidos** , clique em **Backup agora**.</span><span class="sxs-lookup"><span data-stu-id="75d9d-214">At hello bottom of hello **Protected Items** page, click **Backup Now**.</span></span>

    <span data-ttu-id="75d9d-215">Olá serviço Backup do Azure cria um trabalho de backup para a operação de backup inicial hello.</span><span class="sxs-lookup"><span data-stu-id="75d9d-215">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="75d9d-216">Clique em Olá **trabalhos** lista de saudação do guia tooview de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="75d9d-216">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Backup em andamento](./media/backup-azure-vms/protect-inprogress.png)

> [!NOTE]
> <span data-ttu-id="75d9d-218">Durante a operação de backup Olá Olá serviço Backup do Azure emite uma extensão de backup comando toohello em tooflush cada máquina virtual, todos os trabalhos de gravação e tirar um instantâneo consistente.</span><span class="sxs-lookup"><span data-stu-id="75d9d-218">During hello backup operation, hello Azure Backup service issues a command toohello backup extension in each virtual machine tooflush all write jobs and take a consistent snapshot.</span></span>
>
>

<span data-ttu-id="75d9d-219">Quando saudação inicial conclusão do backup, status de saudação da máquina virtual Olá Olá **itens protegidos** guia *protegidos*.</span><span class="sxs-lookup"><span data-stu-id="75d9d-219">When hello initial backup finishes, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/protect-backedupvm.png)

## <a name="viewing-backup-status-and-details"></a><span data-ttu-id="75d9d-221">Exibindo detalhes e status do backup</span><span class="sxs-lookup"><span data-stu-id="75d9d-221">Viewing backup status and details</span></span>
<span data-ttu-id="75d9d-222">Depois de protegido, contagem de máquina virtual Olá também aumenta em Olá **painel** página resumida.</span><span class="sxs-lookup"><span data-stu-id="75d9d-222">Once protected, hello virtual machine count also increases in hello **Dashboard** page summary.</span></span> <span data-ttu-id="75d9d-223">Olá **painel** página também mostra o número de saudação de trabalhos de saudação últimas 24 horas que foram *bem-sucedida*, ter *falha*e são *em andamento*.</span><span class="sxs-lookup"><span data-stu-id="75d9d-223">hello **Dashboard** page also shows hello number of jobs from hello last 24 hours that were *successful*, have *failed*, and are *in progress*.</span></span> <span data-ttu-id="75d9d-224">Em Olá **trabalhos** página, use Olá **Status**, **operação**, ou **de** e **para** toofilter menus trabalhos de saudação.</span><span class="sxs-lookup"><span data-stu-id="75d9d-224">On hello **Jobs** page, use hello **Status**, **Operation**, or **From** and **To** menus toofilter hello jobs.</span></span>

![Status do backup na página Painel](./media/backup-azure-vms/dashboard-protectedvms.png)

<span data-ttu-id="75d9d-226">Os valores no painel de saudação são atualizados uma vez a cada 24 horas.</span><span class="sxs-lookup"><span data-stu-id="75d9d-226">Values in hello dashboard are refreshed once every 24 hours.</span></span>

## <a name="troubleshooting-errors"></a><span data-ttu-id="75d9d-227">Solucionar erros</span><span class="sxs-lookup"><span data-stu-id="75d9d-227">Troubleshooting errors</span></span>
<span data-ttu-id="75d9d-228">Se você tiver problemas durante a cópia sua máquina virtual, examine a saudação [artigo de solução de problemas de VM](backup-azure-vms-troubleshoot.md) para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="75d9d-228">If you run into issues while backing up your virtual machine, look at hello [VM     troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="75d9d-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="75d9d-229">Next steps</span></span>
* [<span data-ttu-id="75d9d-230">Gerenciar e monitorar suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="75d9d-230">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="75d9d-231">Restaurar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="75d9d-231">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
