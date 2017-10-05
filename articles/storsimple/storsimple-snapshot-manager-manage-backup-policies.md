---
title: "Políticas de backup do StorSimple Snapshot Manager | Microsoft Docs"
description: "Descreve como usar o snap-in StorSimple Snapshot Manager MMC para criar e gerenciar as políticas de backup que controlam os backups agendados."
services: storsimple
documentationcenter: NA
author: SharS
manager: timlt
editor: 
ms.assetid: 04415d0b-42f0-4737-8afa-257fb2dbe5d0
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: 218c89e403673c16c72da95aa2c1d685bbed5a86
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-backup-policies"></a><span data-ttu-id="91d05-103">Usar o StorSimple Snapshot Manager para criar e gerenciar políticas de backup</span><span class="sxs-lookup"><span data-stu-id="91d05-103">Use StorSimple Snapshot Manager to create and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="91d05-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="91d05-104">Overview</span></span>
<span data-ttu-id="91d05-105">Uma política de backup cria um cronograma para o backup de dados de volumes localmente ou na nuvem.</span><span class="sxs-lookup"><span data-stu-id="91d05-105">A backup policy creates a schedule for backing up volume data locally or in the cloud.</span></span> <span data-ttu-id="91d05-106">Quando cria uma política de backup, você também pode especificar uma política de retenção.</span><span class="sxs-lookup"><span data-stu-id="91d05-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="91d05-107">(Você pode manter no máximo 64 instantâneos). Para obter mais informações sobre políticas de backup, consulte [Tipos de Backup](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) na [StorSimple série 8000: uma solução de nuvem híbrida](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="91d05-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="91d05-108">Este tutorial explica como:</span><span class="sxs-lookup"><span data-stu-id="91d05-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="91d05-109">Criar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="91d05-109">Create a backup policy</span></span>
* <span data-ttu-id="91d05-110">Editar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="91d05-110">Edit a backup policy</span></span>
* <span data-ttu-id="91d05-111">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="91d05-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="91d05-112">Criar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="91d05-112">Create a backup policy</span></span>
<span data-ttu-id="91d05-113">Use o procedimento a seguir para criar uma nova política de backup.</span><span class="sxs-lookup"><span data-stu-id="91d05-113">Use the following procedure to create a new backup policy.</span></span>

#### <a name="to-create-a-backup-policy"></a><span data-ttu-id="91d05-114">Para criar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="91d05-114">To create a backup policy</span></span>
1. <span data-ttu-id="91d05-115">Clique no ícone da área de trabalho para iniciar o StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="91d05-115">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="91d05-116">No painel **Escopo**, clique com o botão direito em **Políticas de Backup** e clique em **Criar Política de Backup**.</span><span class="sxs-lookup"><span data-stu-id="91d05-116">In the **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Criar uma política de backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="91d05-118">A caixa de diálogo **Criar uma Política** é exibida.</span><span class="sxs-lookup"><span data-stu-id="91d05-118">The **Create a Policy** dialog box appears.</span></span>

    ![Criar uma Política - guia Geral](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="91d05-120">Na guia **Geral** , preencha as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="91d05-120">On the **General** tab, complete the following information:</span></span>

   1. <span data-ttu-id="91d05-121">Na caixa de texto **Nome** , digite um nome para a política.</span><span class="sxs-lookup"><span data-stu-id="91d05-121">In the **Name** text box, type a name for the policy.</span></span>
   2. <span data-ttu-id="91d05-122">Na caixa de texto **Grupo de Volumes** , digite o nome do grupo de volumes associado à política.</span><span class="sxs-lookup"><span data-stu-id="91d05-122">In the **Volume group** text box, type the name of the volume group associated with the policy.</span></span>
   3. <span data-ttu-id="91d05-123">Selecione **Instantâneo Local** ou **Instantâneo em Nuvem**.</span><span class="sxs-lookup"><span data-stu-id="91d05-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="91d05-124">Selecione o número de instantâneos a serem retidos.</span><span class="sxs-lookup"><span data-stu-id="91d05-124">Select the number of snapshots to retain.</span></span> <span data-ttu-id="91d05-125">Se você selecionar **Todos**, 64 instantâneos serão retidos (máximo).</span><span class="sxs-lookup"><span data-stu-id="91d05-125">If you select **All**, 64 snapshots will be retained (the maximum).</span></span>
4. <span data-ttu-id="91d05-126">Clique na guia **Agenda** .</span><span class="sxs-lookup"><span data-stu-id="91d05-126">Click the **Schedule** tab.</span></span>

    ![Criar uma política - guia Agenda](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="91d05-128">Na guia **Agenda** , preencha as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="91d05-128">On the **Schedule** tab, complete the following information:</span></span>

   1. <span data-ttu-id="91d05-129">Marque a caixa de seleção **Habilitar** para agendar o próximo backup.</span><span class="sxs-lookup"><span data-stu-id="91d05-129">Click the **Enable** check box to schedule the next backup.</span></span>
   2. <span data-ttu-id="91d05-130">Nas **Configurações**, selecione **Uma vez**, **Diariamente**, **Semanalmente** ou **Mensalmente**.</span><span class="sxs-lookup"><span data-stu-id="91d05-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="91d05-131">Na caixa de texto **Iniciar** , clique no ícone de calendário e selecione uma data de início.</span><span class="sxs-lookup"><span data-stu-id="91d05-131">In the **Start** text box, click the calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="91d05-132">Em **Configurações Avançadas**, você pode definir cronogramas opcionais de repetição e uma data de término.</span><span class="sxs-lookup"><span data-stu-id="91d05-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="91d05-133">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="91d05-133">Click **OK**.</span></span>

<span data-ttu-id="91d05-134">Após você criar uma política de backup, as seguintes informações aparecem no painel **Resultados** :</span><span class="sxs-lookup"><span data-stu-id="91d05-134">After you create a backup policy, the following information appears in the **Results** pane:</span></span>

* <span data-ttu-id="91d05-135">**Nome** – o nome da política de backup.</span><span class="sxs-lookup"><span data-stu-id="91d05-135">**Name** – the name of backup policy.</span></span>
* <span data-ttu-id="91d05-136">**Tipo** – instantâneo local ou instantâneo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="91d05-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="91d05-137">**Grupo de Volumes** – o grupo de volumes associado à política.</span><span class="sxs-lookup"><span data-stu-id="91d05-137">**Volume Group** – the volume group associated with the policy.</span></span>
* <span data-ttu-id="91d05-138">**Retenção** – o número de instantâneos retidos; o máximo é 64.</span><span class="sxs-lookup"><span data-stu-id="91d05-138">**Retention** – the number of snapshots retained; the maximum is 64.</span></span>
* <span data-ttu-id="91d05-139">**Criado** – a data em que esta política foi criada.</span><span class="sxs-lookup"><span data-stu-id="91d05-139">**Created** – the date that this policy was created.</span></span>
* <span data-ttu-id="91d05-140">**Habilitado** – se a política está em vigor: **Verdadeiro** indica que está em vigor; **Falso** indica que não está.</span><span class="sxs-lookup"><span data-stu-id="91d05-140">**Enabled** – whether the policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="91d05-141">Editar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="91d05-141">Edit a backup policy</span></span>
<span data-ttu-id="91d05-142">Use o procedimento a seguir para editar uma política de backup existente.</span><span class="sxs-lookup"><span data-stu-id="91d05-142">Use the following procedure to edit an existing backup policy.</span></span>

#### <a name="to-edit-a-backup-policy"></a><span data-ttu-id="91d05-143">Para editar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="91d05-143">To edit a backup policy</span></span>
1. <span data-ttu-id="91d05-144">Clique no ícone da área de trabalho para iniciar o StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="91d05-144">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="91d05-145">No painel **Escopo**, clique no nó **Políticas de Backup**.</span><span class="sxs-lookup"><span data-stu-id="91d05-145">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="91d05-146">Todas as políticas de backup aparecem no painel **Resultados** .</span><span class="sxs-lookup"><span data-stu-id="91d05-146">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="91d05-147">Clique com o botão direito na política que você deseja editar e clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="91d05-147">Right-click the policy that you want to edit, and then click **Edit**.</span></span>

    ![Editar uma política de backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="91d05-149">Quando a janela **Criar uma Política** for exibida, insira suas alterações e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="91d05-149">When the **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="91d05-150">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="91d05-150">Delete a backup policy</span></span>
<span data-ttu-id="91d05-151">Use o procedimento a seguir para excluir uma política de backup.</span><span class="sxs-lookup"><span data-stu-id="91d05-151">Use the following procedure to delete a backup policy.</span></span>

#### <a name="to-delete-a-backup-policy"></a><span data-ttu-id="91d05-152">Para excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="91d05-152">To delete a backup policy</span></span>
1. <span data-ttu-id="91d05-153">Clique no ícone da área de trabalho para iniciar o StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="91d05-153">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="91d05-154">No painel **Escopo**, clique no nó **Políticas de Backup**.</span><span class="sxs-lookup"><span data-stu-id="91d05-154">In the **Scope** pane, click the **Backup Policies** node.</span></span> <span data-ttu-id="91d05-155">Todas as políticas de backup aparecem no painel **Resultados** .</span><span class="sxs-lookup"><span data-stu-id="91d05-155">All the backup policies appear in the **Results** pane.</span></span>
3. <span data-ttu-id="91d05-156">Clique com o botão direito do mouse na política de backup que você deseja excluir e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="91d05-156">Right-click the backup policy that you want to delete, and then click **Delete**.</span></span>
4. <span data-ttu-id="91d05-157">Quando a mensagem de confirmação aparecer, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="91d05-157">When the confirmation message appears, click **Yes**.</span></span>

    ![Excluir confirmação da política de backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="91d05-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="91d05-159">Next steps</span></span>
* <span data-ttu-id="91d05-160">Saiba como [usar o StorSimple Snapshot Manager para administrar sua solução do StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="91d05-160">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="91d05-161">Saiba como [Usar o StorSimple Snapshot Manager para exibir e gerenciar trabalhos de backup](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="91d05-161">Learn how to [use StorSimple Snapshot Manager to view and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
