---
title: "aaaBack backup de máquinas virtuais do Azure | Microsoft Docs"
description: "Descobrir, registrar e fazer backup de Cofre de serviços de recuperação de tooa de máquinas virtuais do Azure."
services: backup
documentationcenter: 
author: markgalioto
manager: carmonm
editor: 
keywords: "backup de máquinas virtuais; fazer backup de máquina virtual, backup e recuperação de desastres; backup de vm arm"
ms.assetid: 5c68481d-7be3-4e68-b87c-0961c267053e
ms.service: backup
ms.workload: storage-backup-recovery
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 8/15/2017
ms.author: trinadhk;jimpark;markgal;
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: a204a42726450a7fd89b5563a786b5070578b113
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="back-up-azure-virtual-machines-tooa-recovery-services-vault"></a><span data-ttu-id="aec36-104">Fazer backup de máquinas virtuais do Azure cofre dos serviços de recuperação de tooa</span><span class="sxs-lookup"><span data-stu-id="aec36-104">Back up Azure virtual machines tooa Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="aec36-105">Fazer backup de Cofre de serviços de tooRecovery de VMs</span><span class="sxs-lookup"><span data-stu-id="aec36-105">Back up VMs tooRecovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="aec36-106">Fazer backup de máquinas virtuais tooBackup cofre</span><span class="sxs-lookup"><span data-stu-id="aec36-106">Back up VMs tooBackup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="aec36-107">Este artigo fornece detalhes sobre como tooback backup de máquinas virtuais do Azure (Gerenciador de recursos implantados e implantado clássico) tooa serviços de recuperação do cofre.</span><span class="sxs-lookup"><span data-stu-id="aec36-107">This article details how tooback up Azure VMs (both Resource Manager-deployed and Classic-deployed) tooa Recovery Services vault.</span></span> <span data-ttu-id="aec36-108">A maioria do trabalho hello para fazer backup de máquinas virtuais é preparação hello.</span><span class="sxs-lookup"><span data-stu-id="aec36-108">Most of hello work for backing up VMs is hello preparation.</span></span> <span data-ttu-id="aec36-109">Antes de fazer backup ou proteger uma máquina virtual, você deve concluir Olá [pré-requisitos](backup-azure-arm-vms-prepare.md) tooprepare seu ambiente para proteger suas VMs.</span><span class="sxs-lookup"><span data-stu-id="aec36-109">Before you can back up or protect a VM, you must complete hello [prerequisites](backup-azure-arm-vms-prepare.md) tooprepare your environment for protecting your VMs.</span></span> <span data-ttu-id="aec36-110">Depois de concluir os pré-requisitos de saudação, você pode iniciar instantâneos de tootake Olá operação de backup da VM.</span><span class="sxs-lookup"><span data-stu-id="aec36-110">Once you have completed hello prerequisites, then you can initiate hello backup operation tootake snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="aec36-111">Para obter mais informações, consulte os artigos de saudação em [Planejando sua infra-estrutura de backup de VM no Azure](backup-azure-vms-introduction.md) e [máquinas virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="aec36-111">For more information, see hello articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-hello-backup-job"></a><span data-ttu-id="aec36-112">Disparo do trabalho de backup Olá</span><span class="sxs-lookup"><span data-stu-id="aec36-112">Triggering hello backup job</span></span>
<span data-ttu-id="aec36-113">política de backup Olá associada Olá que Cofre de serviços de recuperação define a frequência e quando a operação de backup Olá é executado.</span><span class="sxs-lookup"><span data-stu-id="aec36-113">hello backup policy associated with hello Recovery Services vault defines how often and when hello backup operation runs.</span></span> <span data-ttu-id="aec36-114">Por padrão, o primeiro backup agendado de saudação é backup inicial hello.</span><span class="sxs-lookup"><span data-stu-id="aec36-114">By default, hello first scheduled backup is hello initial backup.</span></span> <span data-ttu-id="aec36-115">Até que ocorra o backup inicial hello, Olá Status do último Backup em Olá **trabalhos de Backup** folha mostra como **aviso (backup inicial pendente)**.</span><span class="sxs-lookup"><span data-stu-id="aec36-115">Until hello initial backup occurs, hello Last Backup Status on hello **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Backup pendente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="aec36-117">A menos que o backup inicial está vencido toobegin em breve, é recomendável que você execute **backup agora**.</span><span class="sxs-lookup"><span data-stu-id="aec36-117">Unless your initial backup is due toobegin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="aec36-118">Olá procedimento a seguir inicia no painel do Cofre de saudação.</span><span class="sxs-lookup"><span data-stu-id="aec36-118">hello following procedure starts from hello vault dashboard.</span></span> <span data-ttu-id="aec36-119">Esse procedimento serve para executar o trabalho de backup inicial Olá depois de concluir todos os pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="aec36-119">This procedure serves for running hello initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="aec36-120">Se o trabalho de backup inicial Olá já foi executado, esse procedimento não está disponível.</span><span class="sxs-lookup"><span data-stu-id="aec36-120">If hello initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="aec36-121">Olá, política de backup associada determina próximo trabalho de backup hello.</span><span class="sxs-lookup"><span data-stu-id="aec36-121">hello associated backup policy determines hello next backup job.</span></span>  

<span data-ttu-id="aec36-122">toorun saudação inicial trabalho de backup:</span><span class="sxs-lookup"><span data-stu-id="aec36-122">toorun hello initial backup job:</span></span>

1. <span data-ttu-id="aec36-123">No painel do cofre hello, clique em número de saudação em **itens de Backup**, ou clique em Olá **itens de Backup** lado a lado.</span><span class="sxs-lookup"><span data-stu-id="aec36-123">On hello vault dashboard, click hello number under **Backup Items**, or click hello **Backup Items** tile.</span></span> <br/><span data-ttu-id="aec36-124">
  ![Ícone Configurações](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="aec36-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="aec36-125">Olá **itens de Backup** folha é aberta.</span><span class="sxs-lookup"><span data-stu-id="aec36-125">hello **Backup Items** blade opens.</span></span>

  ![Fazer backup de itens](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="aec36-127">Em Olá **itens de Backup** folha, item Olá select.</span><span class="sxs-lookup"><span data-stu-id="aec36-127">On hello **Backup Items** blade, select hello item.</span></span>

  ![Ícone Configurações](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="aec36-129">Olá **itens de Backup** lista é aberta.</span><span class="sxs-lookup"><span data-stu-id="aec36-129">hello **Backup Items** list opens.</span></span> <br/>

  ![Trabalho de backup iniciado](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="aec36-131">Em Olá **itens de Backup** lista, clique nas reticências de saudação **...**  tooopen menu de contexto de saudação.</span><span class="sxs-lookup"><span data-stu-id="aec36-131">On hello **Backup Items** list, click hello ellipses **...** tooopen hello Context menu.</span></span>

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="aec36-133">menu de contexto de saudação aparece.</span><span class="sxs-lookup"><span data-stu-id="aec36-133">hello Context menu appears.</span></span>

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="aec36-135">No menu de contexto de saudação, clique em **Backup agora**.</span><span class="sxs-lookup"><span data-stu-id="aec36-135">On hello Context menu, click **Backup now**.</span></span>

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="aec36-137">Fazer Backup agora folha Olá é aberto.</span><span class="sxs-lookup"><span data-stu-id="aec36-137">hello Backup Now blade opens.</span></span>

  ![mostra o Backup agora folha Olá](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="aec36-139">Olá Backup agora folha, clique no ícone de calendário hello, use Olá calendário controle tooselect Olá último dia deste ponto de recuperação é mantido e clique em **Backup**.</span><span class="sxs-lookup"><span data-stu-id="aec36-139">On hello Backup Now blade, click hello calendar icon, use hello calendar control tooselect hello last day this recovery point is retained, and click **Backup**.</span></span>

  ![conjunto Olá último dia Olá Backup agora o ponto de recuperação será mantido](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="aec36-141">Notificações de implantação informar o trabalho de backup Olá foi disparado, e que você pode monitorar o progresso de saudação do trabalho de saudação na página de trabalhos de Backup hello.</span><span class="sxs-lookup"><span data-stu-id="aec36-141">Deployment notifications let you know hello backup job has been triggered, and that you can monitor hello progress of hello job on hello Backup jobs page.</span></span> <span data-ttu-id="aec36-142">Dependendo do tamanho de saudação da VM, criar backup de saudação inicial pode demorar um pouco.</span><span class="sxs-lookup"><span data-stu-id="aec36-142">Depending on hello size of your VM, creating hello initial backup may take a while.</span></span>

6. <span data-ttu-id="aec36-143">status de saudação tooview ou rastrear do backup inicial hello, no painel do cofre hello, em Olá **trabalhos de Backup** bloco clique **em andamento**.</span><span class="sxs-lookup"><span data-stu-id="aec36-143">tooview or track hello status of hello initial backup, on hello vault dashboard, on hello **Backup Jobs** tile click **In progress**.</span></span>

  ![Bloco dos Trabalhos de Backup](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="aec36-145">Abre a folha de trabalhos de Backup de saudação.</span><span class="sxs-lookup"><span data-stu-id="aec36-145">hello Backup Jobs blade opens.</span></span>

  ![Bloco dos Trabalhos de Backup](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="aec36-147">Em Olá **trabalhos de Backup** folha, você pode ver o status de saudação de todos os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="aec36-147">In hello **Backup jobs** blade, you can see hello status of all jobs.</span></span> <span data-ttu-id="aec36-148">Verifique se o trabalho de backup Olá para sua VM ainda está em andamento ou se ele tiver sido concluída.</span><span class="sxs-lookup"><span data-stu-id="aec36-148">Check if hello backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="aec36-149">Quando um trabalho de backup for concluído, o status de saudação é *concluído*.</span><span class="sxs-lookup"><span data-stu-id="aec36-149">When a backup job is finished, hello status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="aec36-150">Como parte da operação de backup hello, Olá serviço Backup do Azure emite uma extensão de backup de toohello do comando em cada tooflush VM todas as gravações e tirar um instantâneo consistente.</span><span class="sxs-lookup"><span data-stu-id="aec36-150">As a part of hello backup operation, hello Azure Backup service issues a command toohello backup extension in each VM tooflush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="aec36-151">Solucionar erros</span><span class="sxs-lookup"><span data-stu-id="aec36-151">Troubleshooting errors</span></span>
<span data-ttu-id="aec36-152">Se você tiver problemas durante a cópia sua máquina virtual, consulte Olá [artigo de solução de problemas de VM](backup-azure-vms-troubleshoot.md) para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="aec36-152">If you run into issues while backing up your virtual machine, see hello [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="aec36-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aec36-153">Next steps</span></span>
<span data-ttu-id="aec36-154">Agora que você protegeu sua VM, consulte Olá toolearn artigos sobre tarefas de gerenciamento de VM, a seguir e como toorestore VMs.</span><span class="sxs-lookup"><span data-stu-id="aec36-154">Now that you have protected your VM, see hello following articles toolearn about VM management tasks, and how toorestore VMs.</span></span>

* [<span data-ttu-id="aec36-155">Gerenciar e monitorar suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="aec36-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="aec36-156">Restaurar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="aec36-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
