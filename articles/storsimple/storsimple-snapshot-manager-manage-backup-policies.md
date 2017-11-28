---
title: "políticas de backup de instantâneo Manager aaaStorSimple | Microsoft Docs"
description: "Descreve como toouse Olá MMC Gerenciador de instantâneos StorSimple snap-in toocreate e gerenciar políticas de backup Olá que controlam os backups agendados."
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
ms.openlocfilehash: c2ae75a8d0568090add6018da18de73eb56e6590
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-backup-policies"></a><span data-ttu-id="574ad-103">Use o Gerenciador de instantâneos StorSimple toocreate e gerenciar políticas de backup</span><span class="sxs-lookup"><span data-stu-id="574ad-103">Use StorSimple Snapshot Manager toocreate and manage backup policies</span></span>
## <a name="overview"></a><span data-ttu-id="574ad-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="574ad-104">Overview</span></span>
<span data-ttu-id="574ad-105">Uma política de backup cria uma agenda de backup de dados de volume localmente ou na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="574ad-105">A backup policy creates a schedule for backing up volume data locally or in hello cloud.</span></span> <span data-ttu-id="574ad-106">Quando cria uma política de backup, você também pode especificar uma política de retenção.</span><span class="sxs-lookup"><span data-stu-id="574ad-106">When you create a backup policy, you can also specify a retention policy.</span></span> <span data-ttu-id="574ad-107">(Você pode manter no máximo 64 instantâneos). Para obter mais informações sobre políticas de backup, consulte [Tipos de Backup](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) na [StorSimple série 8000: uma solução de nuvem híbrida](storsimple-overview.md).</span><span class="sxs-lookup"><span data-stu-id="574ad-107">(You can retain a maximum of 64 snapshots.) For more information about backup policies, see [Backup types](storsimple-what-is-snapshot-manager.md#backup-types-and-backup-policies) in [StorSimple 8000 series: a hybrid cloud solution](storsimple-overview.md).</span></span>

<span data-ttu-id="574ad-108">Este tutorial explica como:</span><span class="sxs-lookup"><span data-stu-id="574ad-108">This tutorial explains how to:</span></span>

* <span data-ttu-id="574ad-109">Criar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="574ad-109">Create a backup policy</span></span>
* <span data-ttu-id="574ad-110">Editar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="574ad-110">Edit a backup policy</span></span>
* <span data-ttu-id="574ad-111">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="574ad-111">Delete a backup policy</span></span>

## <a name="create-a-backup-policy"></a><span data-ttu-id="574ad-112">Criar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="574ad-112">Create a backup policy</span></span>
<span data-ttu-id="574ad-113">Use Olá seguindo o procedimento toocreate uma nova política de backup.</span><span class="sxs-lookup"><span data-stu-id="574ad-113">Use hello following procedure toocreate a new backup policy.</span></span>

#### <a name="toocreate-a-backup-policy"></a><span data-ttu-id="574ad-114">toocreate uma política de backup</span><span class="sxs-lookup"><span data-stu-id="574ad-114">toocreate a backup policy</span></span>
1. <span data-ttu-id="574ad-115">Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="574ad-115">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="574ad-116">Em Olá **escopo** painel, clique com botão direito **políticas de Backup**e clique em **Criar política de Backup**.</span><span class="sxs-lookup"><span data-stu-id="574ad-116">In hello **Scope** pane, right-click **Backup Policies**, and click **Create Backup Policy**.</span></span>

    ![Criar uma política de backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_BU_policy.png)

    <span data-ttu-id="574ad-118">Olá **criar uma política de** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="574ad-118">hello **Create a Policy** dialog box appears.</span></span>

    ![Criar uma Política - guia Geral](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_general.png)
3. <span data-ttu-id="574ad-120">Em Olá **geral** guia, Olá completa informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="574ad-120">On hello **General** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="574ad-121">Em Olá **nome** caixa de texto, digite um nome para a política de saudação.</span><span class="sxs-lookup"><span data-stu-id="574ad-121">In hello **Name** text box, type a name for hello policy.</span></span>
   2. <span data-ttu-id="574ad-122">Em Olá **grupo de volumes** caixa de texto, digite o nome de Olá Olá do grupo de volume associado à política de saudação.</span><span class="sxs-lookup"><span data-stu-id="574ad-122">In hello **Volume group** text box, type hello name of hello volume group associated with hello policy.</span></span>
   3. <span data-ttu-id="574ad-123">Selecione **Instantâneo Local** ou **Instantâneo em Nuvem**.</span><span class="sxs-lookup"><span data-stu-id="574ad-123">Select either **Local Snapshot** or **Cloud Snapshot**.</span></span>
   4. <span data-ttu-id="574ad-124">Selecione o número de saudação do tooretain de instantâneos.</span><span class="sxs-lookup"><span data-stu-id="574ad-124">Select hello number of snapshots tooretain.</span></span> <span data-ttu-id="574ad-125">Se você selecionar **todos os**, 64 instantâneos serão retidos (máximo de saudação).</span><span class="sxs-lookup"><span data-stu-id="574ad-125">If you select **All**, 64 snapshots will be retained (hello maximum).</span></span>
4. <span data-ttu-id="574ad-126">Clique em Olá **agenda** guia.</span><span class="sxs-lookup"><span data-stu-id="574ad-126">Click hello **Schedule** tab.</span></span>

    ![Criar uma política - guia Agenda](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Create_policy_schedule.png)
5. <span data-ttu-id="574ad-128">Em Olá **agenda** guia, Olá completa informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="574ad-128">On hello **Schedule** tab, complete hello following information:</span></span>

   1. <span data-ttu-id="574ad-129">Clique em Olá **habilitar** próximo backup de caixa de seleção tooschedule hello.</span><span class="sxs-lookup"><span data-stu-id="574ad-129">Click hello **Enable** check box tooschedule hello next backup.</span></span>
   2. <span data-ttu-id="574ad-130">Nas **Configurações**, selecione **Uma vez**, **Diariamente**, **Semanalmente** ou **Mensalmente**.</span><span class="sxs-lookup"><span data-stu-id="574ad-130">Under **Settings**, select **One time**, **Daily**, **Weekly**, or **Monthly**.</span></span>
   3. <span data-ttu-id="574ad-131">Em Olá **iniciar** caixa de texto, clique o ícone de calendário hello e selecione uma data de início.</span><span class="sxs-lookup"><span data-stu-id="574ad-131">In hello **Start** text box, click hello calendar icon and select a start date.</span></span>
   4. <span data-ttu-id="574ad-132">Em **Configurações Avançadas**, você pode definir cronogramas opcionais de repetição e uma data de término.</span><span class="sxs-lookup"><span data-stu-id="574ad-132">Under **Advanced Settings**, you can set optional repeat schedules and an end date.</span></span>
   5. <span data-ttu-id="574ad-133">Clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="574ad-133">Click **OK**.</span></span>

<span data-ttu-id="574ad-134">Depois de criar uma política de backup, Olá informações a seguir aparece no hello **resultados** painel:</span><span class="sxs-lookup"><span data-stu-id="574ad-134">After you create a backup policy, hello following information appears in hello **Results** pane:</span></span>

* <span data-ttu-id="574ad-135">**Nome** – hello nome da política de backup.</span><span class="sxs-lookup"><span data-stu-id="574ad-135">**Name** – hello name of backup policy.</span></span>
* <span data-ttu-id="574ad-136">**Tipo** – instantâneo local ou instantâneo de nuvem.</span><span class="sxs-lookup"><span data-stu-id="574ad-136">**Type** – local snapshot or cloud snapshot.</span></span>
* <span data-ttu-id="574ad-137">**Grupo de volume** – hello associado à política de saudação do grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="574ad-137">**Volume Group** – hello volume group associated with hello policy.</span></span>
* <span data-ttu-id="574ad-138">**Retenção** – hello número de instantâneos retidos; Olá máximo é 64.</span><span class="sxs-lookup"><span data-stu-id="574ad-138">**Retention** – hello number of snapshots retained; hello maximum is 64.</span></span>
* <span data-ttu-id="574ad-139">**Criada** – data de saudação que esta política foi criada.</span><span class="sxs-lookup"><span data-stu-id="574ad-139">**Created** – hello date that this policy was created.</span></span>
* <span data-ttu-id="574ad-140">**Habilitado** – se a política de saudação está atualmente em vigor: **True** indica que ele está em vigor; **False** indica que ele não está em vigor.</span><span class="sxs-lookup"><span data-stu-id="574ad-140">**Enabled** – whether hello policy is currently in effect: **True** indicates that it is in effect; **False** indicates that it is not in effect.</span></span>

## <a name="edit-a-backup-policy"></a><span data-ttu-id="574ad-141">Editar uma política de backup</span><span class="sxs-lookup"><span data-stu-id="574ad-141">Edit a backup policy</span></span>
<span data-ttu-id="574ad-142">Use Olá seguindo o procedimento tooedit uma política de backup existente.</span><span class="sxs-lookup"><span data-stu-id="574ad-142">Use hello following procedure tooedit an existing backup policy.</span></span>

#### <a name="tooedit-a-backup-policy"></a><span data-ttu-id="574ad-143">tooedit uma política de backup</span><span class="sxs-lookup"><span data-stu-id="574ad-143">tooedit a backup policy</span></span>
1. <span data-ttu-id="574ad-144">Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="574ad-144">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="574ad-145">Em Olá **escopo** painel, clique em Olá **políticas de Backup** nó.</span><span class="sxs-lookup"><span data-stu-id="574ad-145">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="574ad-146">Todas as políticas de backup Olá aparecem no hello **resultados** painel.</span><span class="sxs-lookup"><span data-stu-id="574ad-146">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="574ad-147">Clique com botão direito política Olá que você deseja tooedit e, em seguida, clique em **editar**.</span><span class="sxs-lookup"><span data-stu-id="574ad-147">Right-click hello policy that you want tooedit, and then click **Edit**.</span></span>

    ![Editar uma política de backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Edit_BU_policy.png)
4. <span data-ttu-id="574ad-149">Olá quando **criar uma política de** janela for exibida, insira suas alterações e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="574ad-149">When hello **Create a Policy** window appears, enter your changes, and then click **OK**.</span></span>

## <a name="delete-a-backup-policy"></a><span data-ttu-id="574ad-150">Excluir uma política de backup</span><span class="sxs-lookup"><span data-stu-id="574ad-150">Delete a backup policy</span></span>
<span data-ttu-id="574ad-151">Use Olá seguindo o procedimento toodelete uma política de backup.</span><span class="sxs-lookup"><span data-stu-id="574ad-151">Use hello following procedure toodelete a backup policy.</span></span>

#### <a name="toodelete-a-backup-policy"></a><span data-ttu-id="574ad-152">toodelete uma política de backup</span><span class="sxs-lookup"><span data-stu-id="574ad-152">toodelete a backup policy</span></span>
1. <span data-ttu-id="574ad-153">Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="574ad-153">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="574ad-154">Em Olá **escopo** painel, clique em Olá **políticas de Backup** nó.</span><span class="sxs-lookup"><span data-stu-id="574ad-154">In hello **Scope** pane, click hello **Backup Policies** node.</span></span> <span data-ttu-id="574ad-155">Todas as políticas de backup Olá aparecem no hello **resultados** painel.</span><span class="sxs-lookup"><span data-stu-id="574ad-155">All hello backup policies appear in hello **Results** pane.</span></span>
3. <span data-ttu-id="574ad-156">Clique com botão direito a política de backup Olá que você deseja toodelete e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="574ad-156">Right-click hello backup policy that you want toodelete, and then click **Delete**.</span></span>
4. <span data-ttu-id="574ad-157">Quando aparece a mensagem de confirmação de saudação, clique em **Sim**.</span><span class="sxs-lookup"><span data-stu-id="574ad-157">When hello confirmation message appears, click **Yes**.</span></span>

    ![Excluir confirmação da política de backup](./media/storsimple-snapshot-manager-manage-backup-policies/HCS_SSM_Delete_BU_policy.png)

## <a name="next-steps"></a><span data-ttu-id="574ad-159">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="574ad-159">Next steps</span></span>
* <span data-ttu-id="574ad-160">Saiba como muito[usar o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="574ad-160">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="574ad-161">Saiba como muito[usar Gerenciador de instantâneos StorSimple tooview e gerenciar trabalhos de backup](storsimple-snapshot-manager-manage-backup-jobs.md).</span><span class="sxs-lookup"><span data-stu-id="574ad-161">Learn how too[use StorSimple Snapshot Manager tooview and manage backup jobs](storsimple-snapshot-manager-manage-backup-jobs.md).</span></span>
