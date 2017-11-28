---
title: "grupos de volumes do Gerenciador de instantâneos aaaStorSimple | Microsoft Docs"
description: "Descreve como toouse Olá MMC Gerenciador de instantâneos StorSimple snap-in toocreate e gerenciar grupos de volume."
services: storsimple
documentationcenter: NA
author: SharS
manager: carmonm
editor: 
ms.assetid: 7a232414-6a28-4b81-bd7b-cf61e28b33d7
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: v-sharos
ms.openlocfilehash: f7830b62761db7aa5139456b555b6168fb6a85de
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-storsimple-snapshot-manager-toocreate-and-manage-volume-groups"></a><span data-ttu-id="f2a9a-103">Use o Gerenciador de instantâneos StorSimple toocreate e gerenciar grupos de volume</span><span class="sxs-lookup"><span data-stu-id="f2a9a-103">Use StorSimple Snapshot Manager toocreate and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="f2a9a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="f2a9a-104">Overview</span></span>
<span data-ttu-id="f2a9a-105">Você pode usar o hello **grupos de Volume** nó Olá **escopo** painel tooassign volumes toovolume grupos exibir informações sobre um grupo de volumes, agendar backups e editar grupos de volume.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-105">You can use hello **Volume Groups** node on hello **Scope** pane tooassign volumes toovolume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="f2a9a-106">Grupos de volume são pools de volumes relacionados usados tooensure que os backups sejam consistentes com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-106">Volume groups are pools of related volumes used tooensure that backups are application-consistent.</span></span> <span data-ttu-id="f2a9a-107">Para saber mais, consulte [Volumes e grupos de volumes](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) e [Integração com o Serviço de Cópias de Sombra de Volume do Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="f2a9a-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="f2a9a-108">Todos os volumes em um grupo de volumes devem vir de um único provedor de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="f2a9a-109">Quando você configura grupos de volume, não misture volumes compartilhados de cluster (CSVs) e não CSVs no hello mesmo grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="f2a9a-110">Gerenciador de instantâneos do StorSimple não suporta uma mistura de CSVs e não CSVs no hello mesmo instantâneo.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in hello same snapshot.</span></span>

![Nó Grupos de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="f2a9a-112">**Figura 1: Nó Grupos de Volumes do StorSimple Snapshot Manager**</span><span class="sxs-lookup"><span data-stu-id="f2a9a-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="f2a9a-113">Este tutorial explica como você pode usar o StorSimple Snapshot Manager para:</span><span class="sxs-lookup"><span data-stu-id="f2a9a-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="f2a9a-114">Exibir informações sobre os grupos de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-114">View information about your volume groups</span></span>
* <span data-ttu-id="f2a9a-115">Criar um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-115">Create a volume group</span></span>
* <span data-ttu-id="f2a9a-116">Fazer backup de um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-116">Back up a volume group</span></span>
* <span data-ttu-id="f2a9a-117">Editar um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-117">Edit a volume group</span></span>
* <span data-ttu-id="f2a9a-118">Excluir um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-118">Delete a volume group</span></span>

<span data-ttu-id="f2a9a-119">Todas essas ações também estão disponíveis em Olá **ações** painel.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-119">All of these actions are also available on hello **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="f2a9a-120">Exibir grupos de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-120">View volume groups</span></span>
<span data-ttu-id="f2a9a-121">Se você clicar em Olá **grupos de Volume** nó, Olá **resultados** painel mostra Olá informações sobre cada grupo de volume a seguir, dependendo das seleções de coluna Olá feitas.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-121">If you click hello **Volume Groups** node, hello **Results** pane shows hello following information about each volume group, depending on hello column selections you make.</span></span> <span data-ttu-id="f2a9a-122">(Olá colunas Olá **resultados** painel são configuráveis.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-122">(hello columns in hello **Results** pane are configurable.</span></span> <span data-ttu-id="f2a9a-123">Saudação de atalho **Volumes** nó, selecione **exibição**e, em seguida, selecione **Adicionar/remover colunas**.)</span><span class="sxs-lookup"><span data-stu-id="f2a9a-123">Right-click hello **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="f2a9a-124">Coluna de resultados</span><span class="sxs-lookup"><span data-stu-id="f2a9a-124">Results column</span></span> | <span data-ttu-id="f2a9a-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="f2a9a-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="f2a9a-126">Nome</span><span class="sxs-lookup"><span data-stu-id="f2a9a-126">Name</span></span> |<span data-ttu-id="f2a9a-127">Olá **nome** coluna contém o nome de Olá Olá do grupo de volume.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-127">hello **Name** column contains hello name of hello volume group.</span></span> |
| <span data-ttu-id="f2a9a-128">Aplicativo</span><span class="sxs-lookup"><span data-stu-id="f2a9a-128">Application</span></span> |<span data-ttu-id="f2a9a-129">Olá **aplicativos** coluna mostra o número de saudação de gravadores VSS atualmente instalados e em execução no hello host do Windows.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-129">hello **Applications** column shows hello number of VSS writers currently installed and running on hello Windows host.</span></span> |
| <span data-ttu-id="f2a9a-130">Selecionado</span><span class="sxs-lookup"><span data-stu-id="f2a9a-130">Selected</span></span> |<span data-ttu-id="f2a9a-131">Olá **selecionados** coluna mostra o número de saudação de volumes que estão contidos no grupo de volumes de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-131">hello **Selected** column shows hello number of volumes that are contained in hello volume group.</span></span> <span data-ttu-id="f2a9a-132">Um zero (0) indica que nenhum aplicativo está associado a volumes de saudação no grupo de volumes de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-132">A zero (0) indicates that no application is associated with hello volumes in hello volume group.</span></span> |
| <span data-ttu-id="f2a9a-133">Importado</span><span class="sxs-lookup"><span data-stu-id="f2a9a-133">Imported</span></span> |<span data-ttu-id="f2a9a-134">Olá **importado** coluna mostra o número de saudação de volumes importados.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-134">hello **Imported** column shows hello number of imported volumes.</span></span> <span data-ttu-id="f2a9a-135">Quando definido muito**True**, esta coluna indica que um grupo de volumes foi importado do hello portal do Azure e não foi criado no Gerenciador de instantâneos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-135">When set too**True**, this column indicates that a volume group was imported from hello Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="f2a9a-136">Grupos de volumes do StorSimple Snapshot Manager também são exibidos na Olá **políticas de Backup** guia Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-136">StorSimple Snapshot Manager volume groups are also displayed on hello **Backup Policies** tab in hello Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="f2a9a-137">Criar um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-137">Create a volume group</span></span>
<span data-ttu-id="f2a9a-138">Use Olá seguindo o procedimento toocreate um grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-138">Use hello following procedure toocreate a volume group.</span></span>

#### <a name="toocreate-a-volume-group"></a><span data-ttu-id="f2a9a-139">toocreate um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-139">toocreate a volume group</span></span>
1. <span data-ttu-id="f2a9a-140">Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-140">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="f2a9a-141">Em Olá **escopo** painel, clique com botão direito **grupos de Volume**e, em seguida, clique em **criar grupo de Volume**.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-141">In hello **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![Criar Grupo de Volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="f2a9a-143">Olá **criar um grupo de volumes** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-143">hello **Create a volume group** dialog box appears.</span></span>
   
    ![Criar uma caixa de diálogo de grupo de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="f2a9a-145">Digite hello informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="f2a9a-145">Enter hello following information:</span></span>
   
   1. <span data-ttu-id="f2a9a-146">Em Olá **nome** , digite um nome exclusivo para o novo grupo de volumes hello.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-146">In hello **Name** box, type a unique name for hello new volume group.</span></span>
   2. <span data-ttu-id="f2a9a-147">Em Olá **aplicativos** caixa, selecione os aplicativos associados com volumes de saudação que estará adicionando o grupo de volume toohello.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-147">In hello **Applications** box, select applications associated with hello volumes that you will be adding toohello volume group.</span></span>
      
       <span data-ttu-id="f2a9a-148">Olá **aplicativos** caixa de lista somente os aplicativos que usam volumes do StorSimple e tenham gravadores VSS habilitados para eles.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-148">hello **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="f2a9a-149">Um gravador VSS é habilitado somente se todos os volumes de Olá Olá gravador está ciente de volumes do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-149">A VSS writer is enabled only if all hello volumes that hello writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="f2a9a-150">Se Olá aplicativos caixa estiver vazia, nenhum aplicativo que use volumes do StorSimple do Azure e tem suporte para gravadores VSS está instalado.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-150">If hello Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="f2a9a-151">(Atualmente, o Azure StorSimple dá suporte ao Microsoft Exchange e ao SQL Server.) Para obter mais informações sobre os gravadores VSS, veja [Integração com o Serviço de Cópias de Sombra de Volume do Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="f2a9a-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="f2a9a-152">Se você selecionar um aplicativo, todos os volumes associados a ele serão selecionados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="f2a9a-153">Por outro lado, se você selecionar volumes associados a um aplicativo específico, aplicativo hello é selecionado automaticamente no hello **aplicativos** caixa.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-153">Conversely, if you select volumes associated with a specific application, hello application is automatically selected in hello **Applications** box.</span></span> 
   3. <span data-ttu-id="f2a9a-154">Em Olá **Volumes** , selecione o grupo de volumes do StorSimple volumes tooadd toohello.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-154">In hello **Volumes** box, select StorSimple volumes tooadd toohello volume group.</span></span> 
      
      * <span data-ttu-id="f2a9a-155">É possível incluir volumes com partições simples ou múltiplas.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="f2a9a-156">(Volumes com partições múltiplas podem ser discos dinâmicos ou básicos com várias partições.) Um volume que contém partições múltiplas é tratado como uma única unidade.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="f2a9a-157">Consequentemente, se você adicionar apenas uma saudação partições tooa do grupo de volume, Olá todas as outras partições são toothat adicionado automaticamente o grupo de volumes no hello mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-157">Consequently, if you add only one of hello partitions tooa volume group, all hello other partitions are automatically added toothat volume group at hello same time.</span></span> <span data-ttu-id="f2a9a-158">Depois de adicionar um grupo de volumes tooa vários partição volume, hello volume de múltiplas partições continuará toobe tratado como uma única unidade.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-158">After you add a multiple partition volume tooa volume group, hello multiple partition volume continues toobe treated as a single unit.</span></span>
      * <span data-ttu-id="f2a9a-159">Você pode criar grupos de volume vazio, não atribuindo nenhum toothem de volumes.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-159">You can create empty volume groups by not assigning any volumes toothem.</span></span> 
      * <span data-ttu-id="f2a9a-160">Não misture volumes compartilhados de cluster (CSVs) e não CSVs no hello mesmo grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in hello same volume group.</span></span> <span data-ttu-id="f2a9a-161">Gerenciador de instantâneos do StorSimple não oferece suporte a uma mistura de volumes CSV e Olá de volumes não CSV no mesmo instantâneo.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in hello same snapshot.</span></span>
4. <span data-ttu-id="f2a9a-162">Clique em **Okey** toosave grupo de volumes de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-162">Click **OK** toosave hello volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="f2a9a-163">Fazer backup de um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-163">Back up a volume group</span></span>
<span data-ttu-id="f2a9a-164">Use Olá seguindo o procedimento tooback um grupo de volume.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-164">Use hello following procedure tooback up a volume group.</span></span>

#### <a name="tooback-up-a-volume-group"></a><span data-ttu-id="f2a9a-165">tooback um grupo de volume</span><span class="sxs-lookup"><span data-stu-id="f2a9a-165">tooback up a volume group</span></span>
1. <span data-ttu-id="f2a9a-166">Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-166">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="f2a9a-167">Em Olá **escopo** painel, expanda Olá **grupos de Volume** nó, clique em um nome de grupo de volume e clique **fazer Backup**.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-167">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![Fazer imediatamente o backup do grupo de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="f2a9a-169">Em Olá **fazer Backup** caixa de diálogo, selecione **instantâneo Local** ou **instantâneo em nuvem**e, em seguida, clique em **criar**.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-169">In hello **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![Caixa de diálogo Fazer backup](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="f2a9a-171">tooconfirm Olá backup está em execução, expanda Olá **trabalhos** nó e, em seguida, clique **executando**.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-171">tooconfirm that hello backup is running, expand hello **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="f2a9a-172">Olá backup deve ser listado.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-172">hello backup should be listed.</span></span>
5. <span data-ttu-id="f2a9a-173">Olá tooview concluída de instantâneo, expanda Olá **catálogo de Backup** nó, expanda o nome do grupo de volume hello e, em seguida, clique em **instantâneo Local** ou **instantâneo em nuvem**.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-173">tooview hello completed snapshot, expand hello **Backup Catalog** node, expand hello volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="f2a9a-174">Olá backup será listado se for concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-174">hello backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="f2a9a-175">Editar um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-175">Edit a volume group</span></span>
<span data-ttu-id="f2a9a-176">Use Olá seguindo o procedimento tooedit um grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-176">Use hello following procedure tooedit a volume group.</span></span>

#### <a name="tooedit-a-volume-group"></a><span data-ttu-id="f2a9a-177">tooedit um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-177">tooedit a volume group</span></span>
1. <span data-ttu-id="f2a9a-178">Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-178">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="f2a9a-179">Em Olá **escopo** painel, expanda Olá **grupos de Volume** nó, clique em um nome de grupo de volume e clique **editar**.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-179">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="f2a9a-180">Olá * * criar um grupo de volumes * * caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-180">hello **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="f2a9a-181">Você pode alterar Olá **nome**, **aplicativos**, e **Volumes** entradas.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-181">You can change hello **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="f2a9a-182">Clique em **Okey** toosave suas alterações.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-182">Click **OK** toosave your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="f2a9a-183">Excluir um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-183">Delete a volume group</span></span>
<span data-ttu-id="f2a9a-184">Use Olá seguindo o procedimento toodelete um grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-184">Use hello following procedure toodelete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="f2a9a-185">Isso também exclui todos os backups de saudação associados com o grupo de volumes de saudação.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-185">This also deletes all hello backups associated with hello volume group.</span></span>
> 
> 

#### <a name="toodelete-a-volume-group"></a><span data-ttu-id="f2a9a-186">toodelete um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="f2a9a-186">toodelete a volume group</span></span>
1. <span data-ttu-id="f2a9a-187">Clique em Olá ícone da área de trabalho toostart StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-187">Click hello desktop icon toostart StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="f2a9a-188">Em Olá **escopo** painel, expanda Olá **grupos de Volume** nó, clique em um nome de grupo de volume e clique **excluir**.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-188">In hello **Scope** pane, expand hello **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="f2a9a-189">Olá **excluir grupo de Volume** caixa de diálogo é exibida.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-189">hello **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="f2a9a-190">Tipo **confirmar** Olá caixa de texto e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-190">Type **Confirm** in hello text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="f2a9a-191">grupo de volumes Olá excluído desaparece da lista Olá Olá **resultados** painel e todos os backups que estão associados esse grupo de volume são excluídos do catálogo de backup hello.</span><span class="sxs-lookup"><span data-stu-id="f2a9a-191">hello deleted volume group vanishes from hello list in hello **Results** pane and all backups that are associated with that volume group are deleted from hello backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="f2a9a-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f2a9a-192">Next steps</span></span>
* <span data-ttu-id="f2a9a-193">Saiba como muito[usar o Gerenciador de instantâneos StorSimple tooadminister sua solução StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="f2a9a-193">Learn how too[use StorSimple Snapshot Manager tooadminister your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="f2a9a-194">Saiba como muito[usar o Gerenciador de instantâneos StorSimple toocreate e gerenciar políticas de backup](storsimple-snapshot-manager-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="f2a9a-194">Learn how too[use StorSimple Snapshot Manager toocreate and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

