---
title: Grupos de volume do StorSimple Snapshot Manager | Microsoft Docs
description: Descreve como usar o snap-in StorSimple Snapshot Manager MMC para criar e gerenciar grupos de volumes.
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
ms.openlocfilehash: 6067a88cd42d29c3d2f4b74580095424de77561e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-storsimple-snapshot-manager-to-create-and-manage-volume-groups"></a><span data-ttu-id="2f716-103">Usar o StorSimple Snapshot Manager para criar e gerenciar grupos de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-103">Use StorSimple Snapshot Manager to create and manage volume groups</span></span>
## <a name="overview"></a><span data-ttu-id="2f716-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="2f716-104">Overview</span></span>
<span data-ttu-id="2f716-105">Você pode usar o nó **Grupos de Volume** no painel **Escopo** para atribuir volumes a grupos de volumes, exibir informações sobre um grupo de volumes, agendar backups e editar grupos de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-105">You can use the **Volume Groups** node on the **Scope** pane to assign volumes to volume groups, view information about a volume group, schedule backups, and edit volume groups.</span></span>

<span data-ttu-id="2f716-106">Grupos de volumes são conjuntos de volumes relacionados usados para garantir que os backups sejam consistentes com o aplicativo.</span><span class="sxs-lookup"><span data-stu-id="2f716-106">Volume groups are pools of related volumes used to ensure that backups are application-consistent.</span></span> <span data-ttu-id="2f716-107">Para saber mais, consulte [Volumes e grupos de volumes](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) e [Integração com o Serviço de Cópias de Sombra de Volume do Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="2f716-107">For more information, see [Volumes and volume groups](storsimple-what-is-snapshot-manager.md#volumes-and-volume-groups) and [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="2f716-108">Todos os volumes em um grupo de volumes devem vir de um único provedor de serviço de nuvem.</span><span class="sxs-lookup"><span data-stu-id="2f716-108">All volumes in a volume group must come from a single cloud service provider.</span></span>
> * <span data-ttu-id="2f716-109">Quando configurar grupos de volumes, não misture volumes compartilhados de cluster (CSVs) e volumes não CSV no mesmo grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-109">When you configure volume groups, do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="2f716-110">O StorSimple Snapshot Manager não dá suporte a uma combinação de CSVs e não CSVs no mesmo instantâneo.</span><span class="sxs-lookup"><span data-stu-id="2f716-110">StorSimple Snapshot Manager does not support a mix of CSVs and non-CSVs in the same snapshot.</span></span>

![Nó Grupos de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Volume_groups.png)

<span data-ttu-id="2f716-112">**Figura 1: Nó Grupos de Volumes do StorSimple Snapshot Manager**</span><span class="sxs-lookup"><span data-stu-id="2f716-112">**Figure 1: StorSimple Snapshot Manager Volume Groups node**</span></span> 

<span data-ttu-id="2f716-113">Este tutorial explica como você pode usar o StorSimple Snapshot Manager para:</span><span class="sxs-lookup"><span data-stu-id="2f716-113">This tutorial explains how you can use StorSimple Snapshot Manager to:</span></span>

* <span data-ttu-id="2f716-114">Exibir informações sobre os grupos de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-114">View information about your volume groups</span></span>
* <span data-ttu-id="2f716-115">Criar um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-115">Create a volume group</span></span>
* <span data-ttu-id="2f716-116">Fazer backup de um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-116">Back up a volume group</span></span>
* <span data-ttu-id="2f716-117">Editar um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-117">Edit a volume group</span></span>
* <span data-ttu-id="2f716-118">Excluir um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-118">Delete a volume group</span></span>

<span data-ttu-id="2f716-119">Todas essas ações também estão disponíveis no painel **Ações** .</span><span class="sxs-lookup"><span data-stu-id="2f716-119">All of these actions are also available on the **Actions** pane.</span></span>

## <a name="view-volume-groups"></a><span data-ttu-id="2f716-120">Exibir grupos de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-120">View volume groups</span></span>
<span data-ttu-id="2f716-121">Se você clicar no nó **Grupos de Volumes**, o painel **Resultados** mostrará as informações a seguir sobre cada grupo de volumes, dependendo das colunas selecionadas.</span><span class="sxs-lookup"><span data-stu-id="2f716-121">If you click the **Volume Groups** node, the **Results** pane shows the following information about each volume group, depending on the column selections you make.</span></span> <span data-ttu-id="2f716-122">(As colunas no painel **Resultados** são configuráveis.</span><span class="sxs-lookup"><span data-stu-id="2f716-122">(The columns in the **Results** pane are configurable.</span></span> <span data-ttu-id="2f716-123">Clique com o botão direito do mouse no nó **Volumes**, selecione **Exibir** e selecione **Adicionar/Remover Colunas**.)</span><span class="sxs-lookup"><span data-stu-id="2f716-123">Right-click the **Volumes** node, select **View**, and then select **Add/Remove Columns**.)</span></span>

| <span data-ttu-id="2f716-124">Coluna de resultados</span><span class="sxs-lookup"><span data-stu-id="2f716-124">Results column</span></span> | <span data-ttu-id="2f716-125">Descrição</span><span class="sxs-lookup"><span data-stu-id="2f716-125">Description</span></span> |
|:--- |:--- |
| <span data-ttu-id="2f716-126">Nome</span><span class="sxs-lookup"><span data-stu-id="2f716-126">Name</span></span> |<span data-ttu-id="2f716-127">A coluna **Nome** contém o nome do grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-127">The **Name** column contains the name of the volume group.</span></span> |
| <span data-ttu-id="2f716-128">Aplicativo</span><span class="sxs-lookup"><span data-stu-id="2f716-128">Application</span></span> |<span data-ttu-id="2f716-129">A coluna **Aplicativos** mostra o número de gravadores VSS atualmente instalados e em execução no host do Windows.</span><span class="sxs-lookup"><span data-stu-id="2f716-129">The **Applications** column shows the number of VSS writers currently installed and running on the Windows host.</span></span> |
| <span data-ttu-id="2f716-130">Selecionado</span><span class="sxs-lookup"><span data-stu-id="2f716-130">Selected</span></span> |<span data-ttu-id="2f716-131">A coluna **Selecionados** mostra o número de volumes contidos no grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-131">The **Selected** column shows the number of volumes that are contained in the volume group.</span></span> <span data-ttu-id="2f716-132">Um zero (0) indica que nenhum aplicativo está associado aos volumes no grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-132">A zero (0) indicates that no application is associated with the volumes in the volume group.</span></span> |
| <span data-ttu-id="2f716-133">Importado</span><span class="sxs-lookup"><span data-stu-id="2f716-133">Imported</span></span> |<span data-ttu-id="2f716-134">A coluna **Importados** mostra o número de volumes importados.</span><span class="sxs-lookup"><span data-stu-id="2f716-134">The **Imported** column shows the number of imported volumes.</span></span> <span data-ttu-id="2f716-135">Quando definida como **True**, essa coluna indica que um grupo de volumes foi importado do portal do Azure e não foi criado no StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="2f716-135">When set to **True**, this column indicates that a volume group was imported from the Azure portal and was not created in StorSimple Snapshot Manager.</span></span> |

> [!NOTE]
> <span data-ttu-id="2f716-136">Os grupos de volumes do StorSimple Snapshot Manager também são exibidos na guia **Políticas de Backup** no portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="2f716-136">StorSimple Snapshot Manager volume groups are also displayed on the **Backup Policies** tab in the Azure portal.</span></span>
> 
> 

## <a name="create-a-volume-group"></a><span data-ttu-id="2f716-137">Criar um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-137">Create a volume group</span></span>
<span data-ttu-id="2f716-138">Use o procedimento a seguir para criar um grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-138">Use the following procedure to create a volume group.</span></span>

#### <a name="to-create-a-volume-group"></a><span data-ttu-id="2f716-139">Para criar um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-139">To create a volume group</span></span>
1. <span data-ttu-id="2f716-140">Clique no ícone da área de trabalho para iniciar o StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="2f716-140">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2f716-141">No painel **Escopo**, clique com o botão direito do mouse em **Grupos de Volume** e clique em **Criar Grupo de Volumes**.</span><span class="sxs-lookup"><span data-stu-id="2f716-141">In the **Scope** pane, right-click **Volume Groups**, and then click **Create Volume Group**.</span></span>
   
    ![Criar Grupo de Volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Create_volume_group.png)
   
    <span data-ttu-id="2f716-143">A caixa de diálogo **Criar um grupo de volumes** é exibida.</span><span class="sxs-lookup"><span data-stu-id="2f716-143">The **Create a volume group** dialog box appears.</span></span>
   
    ![Criar uma caixa de diálogo de grupo de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_CreateVolumeGroup_dialog.png)
3. <span data-ttu-id="2f716-145">Insira as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="2f716-145">Enter the following information:</span></span>
   
   1. <span data-ttu-id="2f716-146">Na caixa **Nome** , digite um nome exclusivo para o novo grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-146">In the **Name** box, type a unique name for the new volume group.</span></span>
   2. <span data-ttu-id="2f716-147">Na caixa **Aplicativos** , selecione os aplicativos associados aos volumes que você adicionará ao grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-147">In the **Applications** box, select applications associated with the volumes that you will be adding to the volume group.</span></span>
      
       <span data-ttu-id="2f716-148">A caixa **Aplicativos** lista apenas os aplicativos que usam volumes do StorSimple e que contêm gravadores VSS habilitados.</span><span class="sxs-lookup"><span data-stu-id="2f716-148">The **Applications** box lists only those applications that use StorSimple volumes and have VSS writers enabled for them.</span></span> <span data-ttu-id="2f716-149">Um gravador VSS será habilitado apenas se todos os volumes de que ele estiver ciente forem volumes do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="2f716-149">A VSS writer is enabled only if all the volumes that the writer is aware of are StorSimple volumes.</span></span> <span data-ttu-id="2f716-150">Se a caixa Aplicativos estiver vazia, nenhum aplicativo que usa volumes do Azure StorSimple e oferece suporte a gravadores VSS está instalado.</span><span class="sxs-lookup"><span data-stu-id="2f716-150">If the Applications box is empty, then no applications that use Azure StorSimple volumes and have supported VSS writers are installed.</span></span> <span data-ttu-id="2f716-151">(Atualmente, o Azure StorSimple dá suporte ao Microsoft Exchange e ao SQL Server.) Para obter mais informações sobre os gravadores VSS, veja [Integração com o Serviço de Cópias de Sombra de Volume do Windows](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span><span class="sxs-lookup"><span data-stu-id="2f716-151">(Currently, Azure StorSimple supports Microsoft Exchange and SQL Server.) For more information about VSS writers, see [Integration with Windows Volume Shadow Copy Service](storsimple-what-is-snapshot-manager.md#integration-with-windows-volume-shadow-copy-service).</span></span>
      
       <span data-ttu-id="2f716-152">Se você selecionar um aplicativo, todos os volumes associados a ele serão selecionados automaticamente.</span><span class="sxs-lookup"><span data-stu-id="2f716-152">If you select an application, all volumes associated with it are automatically selected.</span></span> <span data-ttu-id="2f716-153">Por outro lado, se você selecionar volumes associados a um aplicativo específico, o aplicativo será selecionado automaticamente na caixa **Aplicativos** .</span><span class="sxs-lookup"><span data-stu-id="2f716-153">Conversely, if you select volumes associated with a specific application, the application is automatically selected in the **Applications** box.</span></span> 
   3. <span data-ttu-id="2f716-154">Na caixa **Volumes** , selecione os volumes do StorSimple a serem adicionados ao grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-154">In the **Volumes** box, select StorSimple volumes to add to the volume group.</span></span> 
      
      * <span data-ttu-id="2f716-155">É possível incluir volumes com partições simples ou múltiplas.</span><span class="sxs-lookup"><span data-stu-id="2f716-155">You can include volumes with single or multiple partitions.</span></span> <span data-ttu-id="2f716-156">(Volumes com partições múltiplas podem ser discos dinâmicos ou básicos com várias partições.) Um volume que contém partições múltiplas é tratado como uma única unidade.</span><span class="sxs-lookup"><span data-stu-id="2f716-156">(Multiple partition volumes can be dynamic disks or basic disks with multiple partitions.) A volume that contains multiple partitions is treated as a single unit.</span></span> <span data-ttu-id="2f716-157">Consequentemente, se você adicionar apenas uma das partições a um grupo de volumes, todas as outras partições serão adicionadas automaticamente ao grupo de volumes ao mesmo tempo.</span><span class="sxs-lookup"><span data-stu-id="2f716-157">Consequently, if you add only one of the partitions to a volume group, all the other partitions are automatically added to that volume group at the same time.</span></span> <span data-ttu-id="2f716-158">Após você adicionar um volume com partições múltiplas a um grupo de volumes, o volume com partições múltiplas continuará sendo tratado como uma única unidade.</span><span class="sxs-lookup"><span data-stu-id="2f716-158">After you add a multiple partition volume to a volume group, the multiple partition volume continues to be treated as a single unit.</span></span>
      * <span data-ttu-id="2f716-159">Você pode criar grupos de volumes vazios não atribuindo nenhum volume a eles.</span><span class="sxs-lookup"><span data-stu-id="2f716-159">You can create empty volume groups by not assigning any volumes to them.</span></span> 
      * <span data-ttu-id="2f716-160">Não misture volumes compartilhados de cluster (CSVs) e volumes não CSV no mesmo grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-160">Do not mix cluster-shared volumes (CSVs) and non-CSVs in the same volume group.</span></span> <span data-ttu-id="2f716-161">O StorSimple Snapshot Manager não dá suporte a uma combinação de volumes CSV e não CSV no mesmo instantâneo.</span><span class="sxs-lookup"><span data-stu-id="2f716-161">StorSimple Snapshot Manager does not support a mix of CSV volumes and non-CSV volumes in the same snapshot.</span></span>
4. <span data-ttu-id="2f716-162">Clique em **OK** para salvar o grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-162">Click **OK** to save the volume group.</span></span>

## <a name="back-up-a-volume-group"></a><span data-ttu-id="2f716-163">Fazer backup de um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-163">Back up a volume group</span></span>
<span data-ttu-id="2f716-164">Use o procedimento a seguir para fazer backup de um grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-164">Use the following procedure to back up a volume group.</span></span>

#### <a name="to-back-up-a-volume-group"></a><span data-ttu-id="2f716-165">Para fazer backup de um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-165">To back up a volume group</span></span>
1. <span data-ttu-id="2f716-166">Clique no ícone da área de trabalho para iniciar o StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="2f716-166">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2f716-167">No painel **Escopo**, expanda o nó **Grupos de Volumes**, clique com o botão direito do mouse no nome de um grupo de volumes e clique em **Fazer Backup**.</span><span class="sxs-lookup"><span data-stu-id="2f716-167">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Take Backup**.</span></span>
   
    ![Fazer imediatamente o backup do grupo de volumes](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_Take_backup.png)
3. <span data-ttu-id="2f716-169">Na caixa de diálogo **Fazer Backup**, selecione **Instantâneo Local** ou **Instantâneo em Nuvem** e clique em **Criar**.</span><span class="sxs-lookup"><span data-stu-id="2f716-169">In the **Take Backup** dialog box, select **Local Snapshot** or **Cloud Snapshot**, and then click **Create**.</span></span>
   
    ![Caixa de diálogo Fazer backup](./media/storsimple-snapshot-manager-manage-volume-groups/HCS_SSM_TakeBackup_dialog.png)
4. <span data-ttu-id="2f716-171">Para confirmar que o backup está em execução, expanda o nó **Trabalhos** e clique em **Em execução**.</span><span class="sxs-lookup"><span data-stu-id="2f716-171">To confirm that the backup is running, expand the **Jobs** node, and then click **Running**.</span></span> <span data-ttu-id="2f716-172">O backup deve estar listado.</span><span class="sxs-lookup"><span data-stu-id="2f716-172">The backup should be listed.</span></span>
5. <span data-ttu-id="2f716-173">Para exibir o instantâneo concluído, expanda o nó **Catálogo de Backup**, expanda o nome do grupo de volumes e clique em **Instantâneo Local** ou em **Instantâneo em Nuvem**.</span><span class="sxs-lookup"><span data-stu-id="2f716-173">To view the completed snapshot, expand the **Backup Catalog** node, expand the volume group name, and then click **Local Snapshot** or **Cloud Snapshot**.</span></span> <span data-ttu-id="2f716-174">O backup será listado se tiver sido concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="2f716-174">The backup will be listed if it finished successfully.</span></span>

## <a name="edit-a-volume-group"></a><span data-ttu-id="2f716-175">Editar um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-175">Edit a volume group</span></span>
<span data-ttu-id="2f716-176">Use o procedimento a seguir para editar um grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-176">Use the following procedure to edit a volume group.</span></span>

#### <a name="to-edit-a-volume-group"></a><span data-ttu-id="2f716-177">Para editar um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-177">To edit a volume group</span></span>
1. <span data-ttu-id="2f716-178">Clique no ícone da área de trabalho para iniciar o StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="2f716-178">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2f716-179">No painel **Escopo**, expanda o nó **Grupos de Volumes**, clique com o botão direito do mouse no nome de um grupo de volumes e clique em **Editar**.</span><span class="sxs-lookup"><span data-stu-id="2f716-179">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Edit**.</span></span>
3. <span data-ttu-id="2f716-180">A caixa de diálogo **Criar um grupo de volumes** é exibida.</span><span class="sxs-lookup"><span data-stu-id="2f716-180">The **Create a volume group **dialog box appears.</span></span> <span data-ttu-id="2f716-181">Você pode alterar as entradas **Nome**, **Aplicativos** e **Volumes**.</span><span class="sxs-lookup"><span data-stu-id="2f716-181">You can change the **Name**, **Applications**, and **Volumes** entries.</span></span>
4. <span data-ttu-id="2f716-182">Clique em **OK** para salvar as alterações.</span><span class="sxs-lookup"><span data-stu-id="2f716-182">Click **OK** to save your changes.</span></span>

## <a name="delete-a-volume-group"></a><span data-ttu-id="2f716-183">Excluir um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-183">Delete a volume group</span></span>
<span data-ttu-id="2f716-184">Use o procedimento a seguir para excluir um grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-184">Use the following procedure to delete a volume group.</span></span> 

> [!WARNING]
> <span data-ttu-id="2f716-185">Isso também exclui todos os backups associados ao grupo de volumes.</span><span class="sxs-lookup"><span data-stu-id="2f716-185">This also deletes all the backups associated with the volume group.</span></span>
> 
> 

#### <a name="to-delete-a-volume-group"></a><span data-ttu-id="2f716-186">Para excluir um grupo de volumes</span><span class="sxs-lookup"><span data-stu-id="2f716-186">To delete a volume group</span></span>
1. <span data-ttu-id="2f716-187">Clique no ícone da área de trabalho para iniciar o StorSimple Snapshot Manager.</span><span class="sxs-lookup"><span data-stu-id="2f716-187">Click the desktop icon to start StorSimple Snapshot Manager.</span></span>
2. <span data-ttu-id="2f716-188">No painel **Escopo**, expanda o nó **Grupos de Volumes**, clique com o botão direito do mouse no nome de um grupo de volumes e clique em **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="2f716-188">In the **Scope** pane, expand the **Volume Groups** node, right-click a volume group name, and then click **Delete**.</span></span>
3. <span data-ttu-id="2f716-189">A caixa de diálogo **Excluir Grupo de Volumes** é exibida.</span><span class="sxs-lookup"><span data-stu-id="2f716-189">The **Delete Volume Group** dialog box appears.</span></span> <span data-ttu-id="2f716-190">Digite **Confirmar** na caixa de texto e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="2f716-190">Type **Confirm** in the text box, and then click **OK**.</span></span>
   
    <span data-ttu-id="2f716-191">O grupo de volumes excluído desaparece da lista no painel **Resultados** e todos os backups associados ao grupo de volumes são excluídos do catálogo de backups.</span><span class="sxs-lookup"><span data-stu-id="2f716-191">The deleted volume group vanishes from the list in the **Results** pane and all backups that are associated with that volume group are deleted from the backup catalog.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2f716-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2f716-192">Next steps</span></span>
* <span data-ttu-id="2f716-193">Saiba como [usar o StorSimple Snapshot Manager para administrar sua solução do StorSimple](storsimple-snapshot-manager-admin.md).</span><span class="sxs-lookup"><span data-stu-id="2f716-193">Learn how to [use StorSimple Snapshot Manager to administer your StorSimple solution](storsimple-snapshot-manager-admin.md).</span></span>
* <span data-ttu-id="2f716-194">Saiba como [usar o StorSimple Snapshot Manager para criar e gerenciar políticas de backup](storsimple-snapshot-manager-manage-backup-policies.md).</span><span class="sxs-lookup"><span data-stu-id="2f716-194">Learn how to [use StorSimple Snapshot Manager to create and manage backup policies](storsimple-snapshot-manager-manage-backup-policies.md).</span></span>

