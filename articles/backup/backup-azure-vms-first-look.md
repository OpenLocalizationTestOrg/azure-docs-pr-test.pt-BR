---
title: "Introdução - Fazer backup de VMs do Azure com um cofre de backup | Microsoft Docs"
description: "Use tooback de portal clássico Olá o Cofre de Backup tooa VMs do Azure. Este tutorial explica todas as fases, incluindo criar Cofre de Backup hello, registrar Olá VMs, criar política de backup e executar o trabalho de backup inicial hello."
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
ms.openlocfilehash: 77700e69eab9faccbc7ef923e1eb4e1f97be75d7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="first-look-backing-up-azure-virtual-machines"></a><span data-ttu-id="12c4d-104">Introdução: Fazendo backup de máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="12c4d-104">First look: Backing up Azure virtual machines</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="12c4d-105">Proteger VMs em um cofre de serviços de recuperação</span><span class="sxs-lookup"><span data-stu-id="12c4d-105">Protect VMs with a recovery services vault</span></span>](backup-azure-vms-first-look-arm.md)
> * [<span data-ttu-id="12c4d-106">Proteger as VMs do Azure com um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="12c4d-106">Protect Azure VMs with a backup vault</span></span>](backup-azure-vms-first-look.md)
>
>

<span data-ttu-id="12c4d-107">Este tutorial descreve as etapas de saudação para fazer backup de um cofre de backup tooa máquina virtual do Azure (VM) no Azure.</span><span class="sxs-lookup"><span data-stu-id="12c4d-107">This tutorial takes you through hello steps for backing up an Azure virtual machine (VM) tooa backup vault in Azure.</span></span> <span data-ttu-id="12c4d-108">Este artigo descreve o modelo clássico hello ou modelo de implantação do Service Manager, para fazer backup de máquinas virtuais.</span><span class="sxs-lookup"><span data-stu-id="12c4d-108">This article describes hello classic model or Service Manager deployment model, for backing up VMs.</span></span> <span data-ttu-id="12c4d-109">Olá etapas a seguir se aplicam somente cofres tooBackup criados no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="12c4d-109">hello following steps apply only tooBackup vaults created in hello classic portal.</span></span> <span data-ttu-id="12c4d-110">A Microsoft recomenda usando o modelo do Gerenciador de recursos de saudação para novas implantações.</span><span class="sxs-lookup"><span data-stu-id="12c4d-110">Microsoft recommends using hello Resource Manager model for new deployments.</span></span>

<span data-ttu-id="12c4d-111">Se você estiver interessado em um cofre de serviços de recuperação de tooa VM que pertença tooa grupo de recursos de backup, consulte [primeiro olhar: proteger VMs com um cofre de serviços de recuperação](backup-azure-vms-first-look-arm.md).</span><span class="sxs-lookup"><span data-stu-id="12c4d-111">If you are interested in backing up a VM tooa Recovery Services vault that belongs tooa Resource Group, see [First look: Protect VMs with a recovery services vault](backup-azure-vms-first-look-arm.md).</span></span>

<span data-ttu-id="12c4d-112">toosuccessfully concluir seguinte Olá tutorial, estes pré-requisitos devem existir:</span><span class="sxs-lookup"><span data-stu-id="12c4d-112">toosuccessfully complete hello following tutorial, these prerequisites must exist:</span></span>

* <span data-ttu-id="12c4d-113">Você criou uma VM em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="12c4d-113">You have created a VM in your Azure subscription.</span></span>
* <span data-ttu-id="12c4d-114">Olá VM tem endereços IP públicos de tooAzure conectividade.</span><span class="sxs-lookup"><span data-stu-id="12c4d-114">hello VM has connectivity tooAzure public IP addresses.</span></span> <span data-ttu-id="12c4d-115">Para obter informações adicionais, veja [Conectividade de rede](backup-azure-vms-prepare.md#network-connectivity).</span><span class="sxs-lookup"><span data-stu-id="12c4d-115">For additional information, see [Network connectivity](backup-azure-vms-prepare.md#network-connectivity).</span></span>


> [!NOTE]
> <span data-ttu-id="12c4d-116">O Azure tem dois modelos de implantação para criar e trabalhar com recursos: [Gerenciador de Recursos e Clássico](../azure-resource-manager/resource-manager-deployment-model.md).</span><span class="sxs-lookup"><span data-stu-id="12c4d-116">Azure has two deployment models for creating and working with resources: [Resource Manager and Classic](../azure-resource-manager/resource-manager-deployment-model.md).</span></span> <span data-ttu-id="12c4d-117">Este tutorial é para uso com máquinas virtuais criadas no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="12c4d-117">This tutorial is for use with virtual machines created in hello classic portal.</span></span>
>
>

## <a name="create-a-backup-vault"></a><span data-ttu-id="12c4d-118">Criar um cofre de backup</span><span class="sxs-lookup"><span data-stu-id="12c4d-118">Create a backup vault</span></span>
<span data-ttu-id="12c4d-119">Um cofre de backup é uma entidade que armazena todos os backups de saudação e pontos de recuperação que foram criados ao longo do tempo.</span><span class="sxs-lookup"><span data-stu-id="12c4d-119">A backup vault is an entity that stores all hello backups and recovery points that have been created over time.</span></span> <span data-ttu-id="12c4d-120">Cofre de backup Olá também contém Olá as políticas de backup que estão sendo feitas backup de máquinas virtuais toohello aplicado.</span><span class="sxs-lookup"><span data-stu-id="12c4d-120">hello backup vault also contains hello backup policies that are applied toohello virtual machines being backed up.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="12c4d-121">A partir de março de 2017, você não pode usar os cofres de Backup Olá toocreate portal clássico.</span><span class="sxs-lookup"><span data-stu-id="12c4d-121">Starting March 2017, you can no longer use hello classic portal toocreate Backup vaults.</span></span>
> <span data-ttu-id="12c4d-122">Você pode atualizar seu cofres dos serviços de tooRecovery de cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="12c4d-122">You can upgrade your Backup vaults tooRecovery Services vaults.</span></span> <span data-ttu-id="12c4d-123">Para obter detalhes, consulte o artigo Olá [atualizar um tooa de Cofre de Backup Cofre de serviços de recuperação](backup-azure-upgrade-backup-to-recovery-services.md).</span><span class="sxs-lookup"><span data-stu-id="12c4d-123">For details, see hello article [Upgrade a Backup vault tooa Recovery Services vault](backup-azure-upgrade-backup-to-recovery-services.md).</span></span> <span data-ttu-id="12c4d-124">A Microsoft incentiva tooupgrade cofres de serviços tooRecovery os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="12c4d-124">Microsoft encourages you tooupgrade your Backup vaults tooRecovery Services vaults.</span></span><br/> <span data-ttu-id="12c4d-125">Após 15 de outubro de 2017, você não pode usar o PowerShell toocreate os cofres de Backup.</span><span class="sxs-lookup"><span data-stu-id="12c4d-125">After October 15, 2017, you can’t use PowerShell toocreate Backup vaults.</span></span> <span data-ttu-id="12c4d-126">**Em 1º de novembro de 2017**:</span><span class="sxs-lookup"><span data-stu-id="12c4d-126">**By November 1, 2017**:</span></span>
>- <span data-ttu-id="12c4d-127">Todos os cofres de Backup restantes serão automaticamente atualizados tooRecovery cofres de serviços.</span><span class="sxs-lookup"><span data-stu-id="12c4d-127">All remaining Backup vaults will be automatically upgraded tooRecovery Services vaults.</span></span>
>- <span data-ttu-id="12c4d-128">Você não será capaz de tooaccess os dados de backup no portal clássico do hello.</span><span class="sxs-lookup"><span data-stu-id="12c4d-128">You won't be able tooaccess your backup data in hello classic portal.</span></span> <span data-ttu-id="12c4d-129">Em vez disso, use Olá tooaccess portal do Azure os dados de backup em cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="12c4d-129">Instead, use hello Azure portal tooaccess your backup data in Recovery Services vaults.</span></span>
>

## <a name="discover-and-register-azure-virtual-machines"></a><span data-ttu-id="12c4d-130">Descobrir e registrar máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="12c4d-130">Discover and Register Azure virtual machines</span></span>
<span data-ttu-id="12c4d-131">Antes de registrar Olá VM com um cofre, execute tooidentify de processo de descoberta de saudação novas VMs.</span><span class="sxs-lookup"><span data-stu-id="12c4d-131">Before registering hello VM with a vault, run hello discovery process tooidentify any new VMs.</span></span> <span data-ttu-id="12c4d-132">Isso retorna uma lista de máquinas virtuais na assinatura hello, juntamente com informações adicionais, como o nome do serviço de nuvem hello e região hello.</span><span class="sxs-lookup"><span data-stu-id="12c4d-132">This returns a list of virtual machines in hello subscription, along with additional information like hello cloud service name and hello region.</span></span>

1. <span data-ttu-id="12c4d-133">Entrar toohello [portal clássico do Azure](http://manage.windowsazure.com/)</span><span class="sxs-lookup"><span data-stu-id="12c4d-133">Sign in toohello [Azure Classic portal](http://manage.windowsazure.com/)</span></span>
2. <span data-ttu-id="12c4d-134">No portal clássico do Azure do hello, clique em **dos serviços de recuperação** tooopen lista de saudação de cofres de serviços de recuperação.</span><span class="sxs-lookup"><span data-stu-id="12c4d-134">In hello Azure classic portal, click **Recovery Services** tooopen hello list of Recovery Services vaults.</span></span>
    <span data-ttu-id="12c4d-135">![Selecionar carga de trabalho](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span><span class="sxs-lookup"><span data-stu-id="12c4d-135">![Select workload](./media/backup-azure-vms-first-look/recovery-services-icon.png)</span></span>
3. <span data-ttu-id="12c4d-136">Saudação de cofres, selecione lista Olá cofre tooback backup de uma VM.</span><span class="sxs-lookup"><span data-stu-id="12c4d-136">From hello list of vaults, select hello vault tooback up a VM.</span></span>

    <span data-ttu-id="12c4d-137">Quando você seleciona o cofre, ele é aberto no hello **início rápido** página</span><span class="sxs-lookup"><span data-stu-id="12c4d-137">When you select your vault, it opens in hello **Quick Start** page</span></span>
4. <span data-ttu-id="12c4d-138">No menu de cofre hello, clique em **itens registrados**.</span><span class="sxs-lookup"><span data-stu-id="12c4d-138">From hello vault menu, click **Registered Items**.</span></span>

    ![Selecionar carga de trabalho](./media/backup-azure-vms-first-look/configure-registered-items.png)
5. <span data-ttu-id="12c4d-140">De saudação **tipo** menu, selecione **Máquina Virtual do Azure**.</span><span class="sxs-lookup"><span data-stu-id="12c4d-140">From hello **Type** menu, select **Azure Virtual Machine**.</span></span>

    ![Selecionar carga de trabalho](./media/backup-azure-vms/discovery-select-workload.png)
6. <span data-ttu-id="12c4d-142">Clique em **DISCOVER** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="12c4d-142">Click **DISCOVER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="12c4d-143">![Botão Descobrir](./media/backup-azure-vms/discover-button-only.png)</span><span class="sxs-lookup"><span data-stu-id="12c4d-143">![Discover button](./media/backup-azure-vms/discover-button-only.png)</span></span>

    <span data-ttu-id="12c4d-144">o processo de descoberta Olá pode levar alguns minutos enquanto estão sendo tabuladas máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="12c4d-144">hello discovery process may take a few minutes while hello virtual machines are being tabulated.</span></span> <span data-ttu-id="12c4d-145">Há uma notificação na parte inferior da saudação da tela de saudação que permite que você saiba que o processo de hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="12c4d-145">There is a notification at hello bottom of hello screen that lets you know that hello process is running.</span></span>

    ![Descobrir VMs](./media/backup-azure-vms/discovering-vms.png)

    <span data-ttu-id="12c4d-147">Olá notificação muda quando Olá processo for concluído.</span><span class="sxs-lookup"><span data-stu-id="12c4d-147">hello notification changes when hello process is complete.</span></span>

    ![Descoberta concluída](./media/backup-azure-vms-first-look/discovery-complete.png)
7. <span data-ttu-id="12c4d-149">Clique em **registrar** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="12c4d-149">Click **REGISTER** at hello bottom of hello page.</span></span>
    <span data-ttu-id="12c4d-150">![Botão Registrar](./media/backup-azure-vms-first-look/register-icon.png)</span><span class="sxs-lookup"><span data-stu-id="12c4d-150">![Register button](./media/backup-azure-vms-first-look/register-icon.png)</span></span>
8. <span data-ttu-id="12c4d-151">Em Olá **registrar itens** menu de atalho, selecione Olá máquinas de virtuais que você deseja tooregister.</span><span class="sxs-lookup"><span data-stu-id="12c4d-151">In hello **Register Items** shortcut menu, select hello virtual machines that you want tooregister.</span></span>

   > [!TIP]
   > <span data-ttu-id="12c4d-152">Várias máquinas virtuais podem ser registradas ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="12c4d-152">Multiple virtual machines can be registered at one time.</span></span>
   >
   >

    <span data-ttu-id="12c4d-153">Um trabalho é criado para cada máquina virtual selecionada.</span><span class="sxs-lookup"><span data-stu-id="12c4d-153">A job is created for each virtual machine that you've selected.</span></span>
9. <span data-ttu-id="12c4d-154">Clique em **Exibir trabalho** em Olá notificação toogo toohello **trabalhos** página.</span><span class="sxs-lookup"><span data-stu-id="12c4d-154">Click **View Job** in hello notification toogo toohello **Jobs** page.</span></span>

    ![Registrar trabalho](./media/backup-azure-vms/register-create-job.png)

    <span data-ttu-id="12c4d-156">máquina virtual de saudação também aparece na lista de saudação de itens registrados, junto com o status de saudação da operação de registro de saudação.</span><span class="sxs-lookup"><span data-stu-id="12c4d-156">hello virtual machine also appears in hello list of registered items, along with hello status of hello registration operation.</span></span>

    ![Status de registro 1](./media/backup-azure-vms/register-status01.png)

    <span data-ttu-id="12c4d-158">Quando Olá operação for concluída, o status de saudação muda Olá tooreflect *registrado* estado.</span><span class="sxs-lookup"><span data-stu-id="12c4d-158">When hello operation completes, hello status changes tooreflect hello *registered* state.</span></span>

    ![Status de registro 2](./media/backup-azure-vms/register-status02.png)

## <a name="install-hello-vm-agent-on-hello-virtual-machine"></a><span data-ttu-id="12c4d-160">Instalar Olá agente de VM na máquina virtual de saudação</span><span class="sxs-lookup"><span data-stu-id="12c4d-160">Install hello VM Agent on hello virtual machine</span></span>
<span data-ttu-id="12c4d-161">Hello Azure VM Agent deve ser instalado em Olá máquina virtual do Azure para Olá toowork de extensão de Backup.</span><span class="sxs-lookup"><span data-stu-id="12c4d-161">hello Azure VM Agent must be installed on hello Azure virtual machine for hello Backup extension toowork.</span></span> <span data-ttu-id="12c4d-162">Se sua VM foi criada de saudação Galeria do Azure, Olá VM Agent já está presente no hello VM; Você pode ignorar muito[protegendo suas VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span><span class="sxs-lookup"><span data-stu-id="12c4d-162">If your VM was created from hello Azure gallery, hello VM Agent is already present on hello VM; you can skip too[protecting your VMs](backup-azure-vms-first-look.md#create-the-backup-policy).</span></span>

<span data-ttu-id="12c4d-163">Se sua VM migrado de um datacenter local, Olá VM provavelmente não tem Olá que VM Agent instalado.</span><span class="sxs-lookup"><span data-stu-id="12c4d-163">If your VM migrated from an on-premises datacenter, hello VM probably does not have hello VM Agent installed.</span></span> <span data-ttu-id="12c4d-164">Você deve instalar Olá agente de VM na máquina virtual Olá Olá de tooprotect continuar VM.</span><span class="sxs-lookup"><span data-stu-id="12c4d-164">You must install hello VM Agent on hello virtual machine before proceeding tooprotect hello VM.</span></span> <span data-ttu-id="12c4d-165">Para obter etapas detalhadas sobre como instalar hello agente de VM, consulte Olá [seção agente de VM do artigo de VMs de Backup Olá](backup-azure-vms-prepare.md#vm-agent).</span><span class="sxs-lookup"><span data-stu-id="12c4d-165">For detailed steps on installing hello VM Agent, see hello [VM Agent section of hello Backup VMs article](backup-azure-vms-prepare.md#vm-agent).</span></span>

## <a name="create-hello-backup-policy"></a><span data-ttu-id="12c4d-166">Criar política de backup Olá</span><span class="sxs-lookup"><span data-stu-id="12c4d-166">Create hello backup policy</span></span>
<span data-ttu-id="12c4d-167">Antes de disparar o trabalho de backup inicial hello, defina o agendamento de saudação quando os instantâneos de backup são realizados.</span><span class="sxs-lookup"><span data-stu-id="12c4d-167">Before you trigger hello initial backup job, set hello schedule when backup snapshots are taken.</span></span> <span data-ttu-id="12c4d-168">Olá agendar instantâneos de backup são realizados e Olá tempo esses instantâneos são mantidos, é política de backup hello.</span><span class="sxs-lookup"><span data-stu-id="12c4d-168">hello schedule when backup snapshots are taken, and hello length of time those snapshots are retained, is hello backup policy.</span></span> <span data-ttu-id="12c4d-169">informações de retenção Olá baseia-se no esquema de rotação de backup avô-pai-filho.</span><span class="sxs-lookup"><span data-stu-id="12c4d-169">hello retention information is based on Grandfather-father-son backup rotation scheme.</span></span>

1. <span data-ttu-id="12c4d-170">Navegue toohello Cofre de backup em **dos serviços de recuperação** Olá portal clássico do Azure e clique em **itens registrados**.</span><span class="sxs-lookup"><span data-stu-id="12c4d-170">Navigate toohello backup vault under **Recovery Services** in hello Azure Classic portal, and  click **Registered Items**.</span></span>
2. <span data-ttu-id="12c4d-171">Selecione **Máquina Virtual do Azure** do menu suspenso de saudação.</span><span class="sxs-lookup"><span data-stu-id="12c4d-171">Select **Azure Virtual Machine** from hello drop-down menu.</span></span>

    ![Selecionar a carga de trabalho no portal](./media/backup-azure-vms/select-workload.png)
3. <span data-ttu-id="12c4d-173">Clique em **proteger** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="12c4d-173">Click **PROTECT** at hello bottom of hello page.</span></span>
    <span data-ttu-id="12c4d-174">![Clique em Proteger](./media/backup-azure-vms-first-look/protect-icon.png)</span><span class="sxs-lookup"><span data-stu-id="12c4d-174">![Click Protect](./media/backup-azure-vms-first-look/protect-icon.png)</span></span>

    <span data-ttu-id="12c4d-175">Olá **proteger itens assistente** aparece e lista *somente* máquinas virtuais que são registradas e não protegidas.</span><span class="sxs-lookup"><span data-stu-id="12c4d-175">hello **Protect Items wizard** appears and lists *only* virtual machines that are registered and not protected.</span></span>

    ![Configurar proteção em escala](./media/backup-azure-vms/protect-at-scale.png)
4. <span data-ttu-id="12c4d-177">Selecione a saudação de máquinas virtuais que você deseja tooprotect.</span><span class="sxs-lookup"><span data-stu-id="12c4d-177">Select hello virtual machines that you want tooprotect.</span></span>

    <span data-ttu-id="12c4d-178">Se houver dois ou mais máquinas virtuais com hello mesmo nome, use Olá toodistinguish de serviço de nuvem entre máquinas virtuais de saudação.</span><span class="sxs-lookup"><span data-stu-id="12c4d-178">If there are two or more virtual machines with hello same name, use hello Cloud Service toodistinguish between hello virtual machines.</span></span>
5. <span data-ttu-id="12c4d-179">Em Olá **configurar proteção** menu Selecione uma política existente ou crie um novo tooprotect de política máquinas virtuais Olá que você identificou.</span><span class="sxs-lookup"><span data-stu-id="12c4d-179">On hello **Configure protection** menu select an existing policy or create a new policy tooprotect hello virtual machines that you identified.</span></span>

    <span data-ttu-id="12c4d-180">Novos cofres de Backup têm uma política de padrão associada Olá cofre.</span><span class="sxs-lookup"><span data-stu-id="12c4d-180">New Backup vaults have a default policy associated with hello vault.</span></span> <span data-ttu-id="12c4d-181">Esta política usa um diário de instantâneo a cada noite e instantâneo diário Olá é mantido por 30 dias.</span><span class="sxs-lookup"><span data-stu-id="12c4d-181">This policy takes a daily snapshot each evening, and hello daily snapshot is retained for 30 days.</span></span> <span data-ttu-id="12c4d-182">Cada política de backup pode ter várias máquinas virtuais associadas a ela.</span><span class="sxs-lookup"><span data-stu-id="12c4d-182">Each backup policy can have multiple virtual machines associated with it.</span></span> <span data-ttu-id="12c4d-183">No entanto, máquina virtual de saudação só pode ser associada com uma política por vez.</span><span class="sxs-lookup"><span data-stu-id="12c4d-183">However, hello virtual machine can only be associated with one policy at a time.</span></span>

    ![Proteger com nova política](./media/backup-azure-vms/policy-schedule.png)

   > [!NOTE]
   > <span data-ttu-id="12c4d-185">Uma política de backup inclui um esquema de retenção para backups agendado de saudação.</span><span class="sxs-lookup"><span data-stu-id="12c4d-185">A backup policy includes a retention scheme for hello scheduled backups.</span></span> <span data-ttu-id="12c4d-186">Se você selecionar uma política de backup, você será opções de retenção Olá toomodify não é possível na próxima etapa do hello.</span><span class="sxs-lookup"><span data-stu-id="12c4d-186">If you select an existing backup policy, you will be unable toomodify hello retention options in hello next step.</span></span>
   >
   >
6. <span data-ttu-id="12c4d-187">Em **período de retenção** definir Olá escopo diário, semanal, mensal e anual para pontos de backup específico hello.</span><span class="sxs-lookup"><span data-stu-id="12c4d-187">On **Retention Range** define hello daily, weekly, monthly, and yearly scope for hello specific backup points.</span></span>

    ![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/long-term-retention.png)

    <span data-ttu-id="12c4d-189">Política de retenção Especifica Olá período de tempo para armazenar um backup.</span><span class="sxs-lookup"><span data-stu-id="12c4d-189">Retention policy specifies hello length of time for storing a backup.</span></span> <span data-ttu-id="12c4d-190">Você pode especificar diferentes políticas de retenção com base em quando é feito backup hello.</span><span class="sxs-lookup"><span data-stu-id="12c4d-190">You can specify different retention policies based on when hello backup is taken.</span></span>
7. <span data-ttu-id="12c4d-191">Clique em **trabalhos** tooview lista de saudação do **configurar proteção** trabalhos.</span><span class="sxs-lookup"><span data-stu-id="12c4d-191">Click **Jobs** tooview hello list of **Configure Protection** jobs.</span></span>

    ![Configurar o trabalho de proteção](./media/backup-azure-vms/protect-configureprotection.png)

    <span data-ttu-id="12c4d-193">Agora que estabelecida política Olá, vá toohello próxima etapa e executar o backup inicial hello.</span><span class="sxs-lookup"><span data-stu-id="12c4d-193">Now that you've established hello policy, go toohello next step and run hello initial backup.</span></span>

## <a name="initial-backup"></a><span data-ttu-id="12c4d-194">Backup inicial</span><span class="sxs-lookup"><span data-stu-id="12c4d-194">Initial backup</span></span>
<span data-ttu-id="12c4d-195">Depois que uma máquina virtual foi protegida com uma política, você pode exibir esse relacionamento na Olá **itens protegidos** guia. Até que o backup inicial Olá ocorre, hello **Status de proteção** mostra como **protegido - (pendente backup inicial)**.</span><span class="sxs-lookup"><span data-stu-id="12c4d-195">Once a virtual machine has been protected with a policy, you can view that relationship on hello **Protected Items** tab. Until hello initial backup occurs, hello **Protection Status** shows as **Protected - (pending initial backup)**.</span></span> <span data-ttu-id="12c4d-196">Por padrão, o primeiro backup agendado de saudação é Olá *backup inicial*.</span><span class="sxs-lookup"><span data-stu-id="12c4d-196">By default, hello first scheduled backup is hello *initial backup*.</span></span>

![Backup pendente](./media/backup-azure-vms-first-look/protection-pending-border.png)

<span data-ttu-id="12c4d-198">toostart saudação inicial backup agora:</span><span class="sxs-lookup"><span data-stu-id="12c4d-198">toostart hello initial backup now:</span></span>

1. <span data-ttu-id="12c4d-199">Em Olá **itens protegidos** , clique em **Backup agora** final Olá Olá página.</span><span class="sxs-lookup"><span data-stu-id="12c4d-199">On hello **Protected Items** page, click **Backup Now** at hello bottom of hello page.</span></span>
    <span data-ttu-id="12c4d-200">![Ícone de Fazer Backup Agora](./media/backup-azure-vms-first-look/backup-now-icon.png)</span><span class="sxs-lookup"><span data-stu-id="12c4d-200">![Backup Now icon](./media/backup-azure-vms-first-look/backup-now-icon.png)</span></span>

    <span data-ttu-id="12c4d-201">Olá serviço Backup do Azure cria um trabalho de backup para a operação de backup inicial hello.</span><span class="sxs-lookup"><span data-stu-id="12c4d-201">hello Azure Backup service creates a backup job for hello initial backup operation.</span></span>
2. <span data-ttu-id="12c4d-202">Clique em Olá **trabalhos** lista de saudação do guia tooview de trabalhos.</span><span class="sxs-lookup"><span data-stu-id="12c4d-202">Click hello **Jobs** tab tooview hello list of jobs.</span></span>

    ![Backup em andamento](./media/backup-azure-vms-first-look/protect-inprogress.png)

    <span data-ttu-id="12c4d-204">Quando o backup inicial é concluída, o status de saudação de máquina virtual Olá Olá **itens protegidos** guia *protegidos*.</span><span class="sxs-lookup"><span data-stu-id="12c4d-204">When initial backup is complete, hello status of hello virtual machine in hello **Protected Items** tab is *Protected*.</span></span>

    ![O backup da máquina virtual é realizado com ponto de recuperação](./media/backup-azure-vms/protect-backedupvm.png)

   > [!NOTE]
   > <span data-ttu-id="12c4d-206">O backup de máquinas virtuais é um processo local.</span><span class="sxs-lookup"><span data-stu-id="12c4d-206">Backing up virtual machines is a local process.</span></span> <span data-ttu-id="12c4d-207">Você não pode fazer backup de máquinas virtuais de uma região tooa Cofre de backup em outra região.</span><span class="sxs-lookup"><span data-stu-id="12c4d-207">You cannot back up virtual machines from one region tooa backup vault in another region.</span></span> <span data-ttu-id="12c4d-208">Portanto, para cada região do Azure com VMs que precisam de backup de toobe, pelo menos um cofre de backup deve ser criado nessa região.</span><span class="sxs-lookup"><span data-stu-id="12c4d-208">So, for every Azure region that has VMs that need toobe backed up, at least one backup vault must be created in that region.</span></span>
   >
   >

## <a name="next-steps"></a><span data-ttu-id="12c4d-209">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="12c4d-209">Next steps</span></span>
<span data-ttu-id="12c4d-210">Agora que você já fez um backup de uma VM, há várias etapas subsequentes pode poderiam ser interessantes.</span><span class="sxs-lookup"><span data-stu-id="12c4d-210">Now that you have successfully backed up a VM, there are several next steps that could be of interest.</span></span> <span data-ttu-id="12c4d-211">Olá mais lógica etapa é toofamiliarize-se com a restauração de dados tooa VM.</span><span class="sxs-lookup"><span data-stu-id="12c4d-211">hello most logical step is toofamiliarize yourself with restoring data tooa VM.</span></span> <span data-ttu-id="12c4d-212">No entanto, há tarefas de gerenciamento que ajudarão você a entender como tookeep seus dados seguros e minimizar os custos.</span><span class="sxs-lookup"><span data-stu-id="12c4d-212">However, there are management tasks that will help you understand how tookeep your data safe and minimize costs.</span></span>

* [<span data-ttu-id="12c4d-213">Gerenciar e monitorar suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="12c4d-213">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="12c4d-214">Restaurar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="12c4d-214">Restore virtual machines</span></span>](backup-azure-restore-vms.md)
* [<span data-ttu-id="12c4d-215">Diretrizes de solução de problemas</span><span class="sxs-lookup"><span data-stu-id="12c4d-215">Troubleshooting guidance</span></span>](backup-azure-vms-troubleshoot.md)

## <a name="questions"></a><span data-ttu-id="12c4d-216">Perguntas?</span><span class="sxs-lookup"><span data-stu-id="12c4d-216">Questions?</span></span>
<span data-ttu-id="12c4d-217">Se você tiver dúvidas ou se houver qualquer recurso que você gostaria que toosee incluído, [nos enviar comentários](http://aka.ms/azurebackup_feedback).</span><span class="sxs-lookup"><span data-stu-id="12c4d-217">If you have questions, or if there is any feature that you would like toosee included, [send us feedback](http://aka.ms/azurebackup_feedback).</span></span>
