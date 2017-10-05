---
title: Fazer backup de VMs do Azure | Microsoft Docs
description: "Descubra, registre e faça backup de máquinas virtuais do Azure em um cofre dos Serviços de Recuperação."
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
ms.openlocfilehash: 40983a3de104238d09b976b5fcf2419da42c1bba
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="back-up-azure-virtual-machines-to-a-recovery-services-vault"></a><span data-ttu-id="a6cc6-104">Fazer backup de máquinas virtuais do Azure em um cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="a6cc6-104">Back up Azure virtual machines to a Recovery Services vault</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="a6cc6-105">Fazer backup de VMs no cofre dos Serviços de Recuperação</span><span class="sxs-lookup"><span data-stu-id="a6cc6-105">Back up VMs to Recovery Services vault</span></span>](backup-azure-arm-vms.md)
> * [<span data-ttu-id="a6cc6-106">Fazer backup de VMs no cofre de Backup</span><span class="sxs-lookup"><span data-stu-id="a6cc6-106">Back up VMs to Backup vault</span></span>](backup-azure-vms.md)
>
>

<span data-ttu-id="a6cc6-107">Este artigo detalha como para fazer backup de VMs do Azure (implantadas pelo Resource Manager ou com a implantação clássica) em um cofre dos Serviços de Recuperação.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-107">This article details how to back up Azure VMs (both Resource Manager-deployed and Classic-deployed) to a Recovery Services vault.</span></span> <span data-ttu-id="a6cc6-108">A maior parte do trabalho para fazer backup de VMs é a preparação.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-108">Most of the work for backing up VMs is the preparation.</span></span> <span data-ttu-id="a6cc6-109">Antes de fazer backup ou proteger uma VM, você deverá atender aos [pré-requisitos](backup-azure-arm-vms-prepare.md) para preparar o ambiente e proteger suas VMs.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-109">Before you can back up or protect a VM, you must complete the [prerequisites](backup-azure-arm-vms-prepare.md) to prepare your environment for protecting your VMs.</span></span> <span data-ttu-id="a6cc6-110">Depois de concluir os pré-requisitos, você pode iniciar a operação de backup para tirar instantâneos da sua VM.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-110">Once you have completed the prerequisites, then you can initiate the backup operation to take snapshots of your VM.</span></span>


[!INCLUDE [learn about backup deployment models](../../includes/backup-deployment-models.md)]

<span data-ttu-id="a6cc6-111">Para obter mais informações, confira os artigos sobre [planejamento da infraestrutura de backup de VM no Azure](backup-azure-vms-introduction.md) e sobre [máquinas virtuais do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/).</span><span class="sxs-lookup"><span data-stu-id="a6cc6-111">For more information, see the articles on [planning your VM backup infrastructure in Azure](backup-azure-vms-introduction.md) and [Azure virtual machines](https://azure.microsoft.com/documentation/services/virtual-machines/).</span></span>

## <a name="triggering-the-backup-job"></a><span data-ttu-id="a6cc6-112">Disparar o trabalho de backup</span><span class="sxs-lookup"><span data-stu-id="a6cc6-112">Triggering the backup job</span></span>
<span data-ttu-id="a6cc6-113">A política de backup associada ao cofre dos Serviços de Recuperação define a frequência e quando a operação de backup é executada.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-113">The backup policy associated with the Recovery Services vault defines how often and when the backup operation runs.</span></span> <span data-ttu-id="a6cc6-114">Por padrão, o primeiro backup agendado é o backup inicial.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-114">By default, the first scheduled backup is the initial backup.</span></span> <span data-ttu-id="a6cc6-115">Até que o backup inicial ocorra, o Status do Último Backup na folha **Trabalhos de Backup** aparece como **Aviso (backup inicial pendente)**.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-115">Until the initial backup occurs, the Last Backup Status on the **Backup Jobs** blade shows as **Warning(initial backup pending)**.</span></span>

![Backup pendente](./media/backup-azure-vms-first-look-arm/initial-backup-not-run.png)

<span data-ttu-id="a6cc6-117">A menos que o backup inicial esteja prestes a começar, é recomendável que você execute **Fazer Backup Agora**.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-117">Unless your initial backup is due to begin soon, it is recommended that you run **Back up Now**.</span></span> <span data-ttu-id="a6cc6-118">O procedimento a seguir começa no painel do cofre.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-118">The following procedure starts from the vault dashboard.</span></span> <span data-ttu-id="a6cc6-119">Esse procedimento serve para executar o trabalho de backup inicial depois de concluir todos os pré-requisitos.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-119">This procedure serves for running the initial backup job after you have completed all prerequisites.</span></span> <span data-ttu-id="a6cc6-120">Se o trabalho de backup inicial já tiver sido executado, esse procedimento não estará disponível.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-120">If the initial backup job has already been run, this procedure is not available.</span></span> <span data-ttu-id="a6cc6-121">A política de backup associada determina o próximo trabalho de backup.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-121">The associated backup policy determines the next backup job.</span></span>  

<span data-ttu-id="a6cc6-122">Para executar o trabalho de backup inicial:</span><span class="sxs-lookup"><span data-stu-id="a6cc6-122">To run the initial backup job:</span></span>

1. <span data-ttu-id="a6cc6-123">No painel do cofre, clique no número em **Itens de Backup**, ou clique no bloco **Itens de Backup**.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-123">On the vault dashboard, click the number under **Backup Items**, or click the **Backup Items** tile.</span></span> <br/><span data-ttu-id="a6cc6-124">
  ![Ícone Configurações](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span><span class="sxs-lookup"><span data-stu-id="a6cc6-124">
![Settings icon](./media/backup-azure-vms-first-look-arm/rs-vault-config-vm-back-up-now-1.png)</span></span>

  <span data-ttu-id="a6cc6-125">A folha **Itens de Backup** será aberta.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-125">The **Backup Items** blade opens.</span></span>

  ![Fazer backup de itens](./media/backup-azure-vms-first-look-arm/back-up-items-list.png)

2. <span data-ttu-id="a6cc6-127">Na folha **Itens de Backup**, selecione o item.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-127">On the **Backup Items** blade, select the item.</span></span>

  ![Ícone Configurações](./media/backup-azure-vms-first-look-arm/back-up-items-list-selected.png)

  <span data-ttu-id="a6cc6-129">A lista **Itens de Backup** será aberta.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-129">The **Backup Items** list opens.</span></span> <br/>

  ![Trabalho de backup iniciado](./media/backup-azure-vms-first-look-arm/backup-items-not-run.png)

3. <span data-ttu-id="a6cc6-131">Na lista **Itens de Backup**, clique nas reticências **...** para abrir o menu de contexto.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-131">On the **Backup Items** list, click the ellipses **...** to open the Context menu.</span></span>

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu.png)

  <span data-ttu-id="a6cc6-133">O menu de contexto é exibido.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-133">The Context menu appears.</span></span>

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu-small.png)

4. <span data-ttu-id="a6cc6-135">No menu de contexto, clique em **Fazer backup agora**.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-135">On the Context menu, click **Backup now**.</span></span>

  ![Menu de contexto](./media/backup-azure-vms-first-look-arm/context-menu-small-backup-now.png)

  <span data-ttu-id="a6cc6-137">A folha Fazer Backup Agora é aberta.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-137">The Backup Now blade opens.</span></span>

  ![mostra a folha Fazer Backup Agora](./media/backup-azure-vms-first-look-arm/backup-now-blade-short.png)

5. <span data-ttu-id="a6cc6-139">Na folha Fazer Backup Agora, clique no ícone de calendário, use o controle de calendário para selecionar o último dia de retenção desse ponto de recuperação e clique em **Fazer Backup**.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-139">On the Backup Now blade, click the calendar icon, use the calendar control to select the last day this recovery point is retained, and click **Backup**.</span></span>

  ![definir o último dia em que o ponto de recuperação de Fazer Backup Agora será retido](./media/backup-azure-vms-first-look-arm/backup-now-blade-calendar.png)

  <span data-ttu-id="a6cc6-141">As notificações de implantação informam que o trabalho de backup foi disparado, e que você pode monitorar o andamento do trabalho na página de Trabalhos de backup.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-141">Deployment notifications let you know the backup job has been triggered, and that you can monitor the progress of the job on the Backup jobs page.</span></span> <span data-ttu-id="a6cc6-142">Dependendo do tamanho da VM, a criação do backup inicial pode demorar um pouco.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-142">Depending on the size of your VM, creating the initial backup may take a while.</span></span>

6. <span data-ttu-id="a6cc6-143">Para exibir ou rastrear o status do backup inicial, no painel do cofre, no bloco **Trabalhos de Backup**, clique em **Em andamento**.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-143">To view or track the status of the initial backup, on the vault dashboard, on the **Backup Jobs** tile click **In progress**.</span></span>

  ![Bloco dos Trabalhos de Backup](./media/backup-azure-vms-first-look-arm/open-backup-jobs-1.png)

  <span data-ttu-id="a6cc6-145">A folha Trabalhos de Backup será aberta.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-145">The Backup Jobs blade opens.</span></span>

  ![Bloco dos Trabalhos de Backup](./media/backup-azure-vms-first-look-arm/backup-jobs-in-jobs-view-1.png)

  <span data-ttu-id="a6cc6-147">Na folha **Trabalhos de backup** , você pode ver o status de todos os trabalhos.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-147">In the **Backup jobs** blade, you can see the status of all jobs.</span></span> <span data-ttu-id="a6cc6-148">Verifique se o trabalho de backup de sua VM ainda está em andamento ou se já foi concluído.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-148">Check if the backup job for your VM is still in progress, or if it has finished.</span></span> <span data-ttu-id="a6cc6-149">Após a conclusão do trabalho de backup, o status será *Concluído*.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-149">When a backup job is finished, the status is *Completed*.</span></span>

  > [!NOTE]
  > <span data-ttu-id="a6cc6-150">Como parte da operação de backup, o serviço de Backup do Azure emite um comando para a extensão de backup em cada VM para limpar todas as gravações e capturar um instantâneo consistente.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-150">As a part of the backup operation, the Azure Backup service issues a command to the backup extension in each VM to flush all writes and take a consistent snapshot.</span></span>
  >
  >

## <a name="troubleshooting-errors"></a><span data-ttu-id="a6cc6-151">Solucionar erros</span><span class="sxs-lookup"><span data-stu-id="a6cc6-151">Troubleshooting errors</span></span>
<span data-ttu-id="a6cc6-152">Se você enfrentar problemas ao copiar a sua máquina virtual, confira o [artigo de solução de problemas de VM](backup-azure-vms-troubleshoot.md) para obter ajuda.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-152">If you run into issues while backing up your virtual machine, see the [VM troubleshooting article](backup-azure-vms-troubleshoot.md) for help.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a6cc6-153">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a6cc6-153">Next steps</span></span>
<span data-ttu-id="a6cc6-154">Agora que você protegeu sua VM, consulte os seguintes artigos para aprender sobre tarefas de gerenciamento de VM e a restauração de VMs.</span><span class="sxs-lookup"><span data-stu-id="a6cc6-154">Now that you have protected your VM, see the following articles to learn about VM management tasks, and how to restore VMs.</span></span>

* [<span data-ttu-id="a6cc6-155">Gerenciar e monitorar suas máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="a6cc6-155">Manage and monitor your virtual machines</span></span>](backup-azure-manage-vms.md)
* [<span data-ttu-id="a6cc6-156">Restaurar máquinas virtuais</span><span class="sxs-lookup"><span data-stu-id="a6cc6-156">Restore virtual machines</span></span>](backup-azure-arm-restore-vms.md)
