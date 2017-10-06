---
title: "aaaManage seu catálogo de backup do StorSimple | Microsoft Docs"
description: "Explica como Olá toouse toolist de página do Gerenciador de dispositivos do StorSimple serviço Catálogo de backup, selecione e excluir conjuntos de backup."
services: storsimple
documentationcenter: NA
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/29/2017
ms.author: alkohli
ms.openlocfilehash: e464609e74409a06a198790719abd82ed03c03d9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-storsimple-device-manager-service-toomanage-your-backup-catalog"></a><span data-ttu-id="95497-103">Usar toomanage de serviço do Gerenciador de dispositivos de StorSimple Olá seu catálogo de backup</span><span class="sxs-lookup"><span data-stu-id="95497-103">Use hello StorSimple Device Manager service toomanage your backup catalog</span></span>
## <a name="overview"></a><span data-ttu-id="95497-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="95497-104">Overview</span></span>
<span data-ttu-id="95497-105">saudação de serviço do Gerenciador de dispositivos de StorSimple **catálogo de Backup** folha exibe todos os conjuntos de backup de saudação que são criados quando são realizados backups manuais ou agendados.</span><span class="sxs-lookup"><span data-stu-id="95497-105">hello StorSimple Device Manager service **Backup Catalog** blade displays all hello backup sets that are created when manual or scheduled backups are taken.</span></span> <span data-ttu-id="95497-106">Você pode usar todos os backups de saudação de toolist essa página para uma política de backup ou um volume, selecione ou excluir backups, ou usar um backup toorestore ou clonar um volume.</span><span class="sxs-lookup"><span data-stu-id="95497-106">You can use this page toolist all hello backups for a backup policy or a volume, select or delete backups, or use a backup toorestore or clone a volume.</span></span>

<span data-ttu-id="95497-107">Este tutorial explica como toolist, selecione e exclua um conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-107">This tutorial explains how toolist, select, and delete a backup set.</span></span> <span data-ttu-id="95497-108">toolearn como toorestore seu dispositivo de backup, vá muito[restaurar seu dispositivo de um conjunto de backup](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="95497-108">toolearn how toorestore your device from backup, go too[Restore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span> <span data-ttu-id="95497-109">toolearn como tooclone um volume, ir muito[clonar um volume StorSimple](storsimple-8000-clone-volume-u2.md).</span><span class="sxs-lookup"><span data-stu-id="95497-109">toolearn how tooclone a volume, go too[Clone a StorSimple volume](storsimple-8000-clone-volume-u2.md).</span></span>

![Catálogo de backup](./media/storsimple-8000-manage-backup-catalog/bucatalog.png) 

<span data-ttu-id="95497-111">Olá **catálogo de Backup** folha fornece uma consulta toonarrow sua seleção de conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-111">hello **Backup Catalog** blade provides a query toonarrow your backup set selection.</span></span> <span data-ttu-id="95497-112">Você pode filtrar conjuntos de backup de saudação que são recuperados, com base em Olá parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="95497-112">You can filter hello backup sets that are retrieved, based on hello following parameters:</span></span>

* <span data-ttu-id="95497-113">**Dispositivo** – dispositivo Olá no qual Olá o conjunto de backup foi criado.</span><span class="sxs-lookup"><span data-stu-id="95497-113">**Device** – hello device on which hello backup set was created.</span></span>
* <span data-ttu-id="95497-114">**Política de backup ou Volume** – Olá a política de backup ou volume associado a este conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-114">**Backup policy or Volume** – hello backup policy or volume associated with this backup set.</span></span>
* <span data-ttu-id="95497-115">**De e para** – Olá intervalo de data e hora quando o conjunto de backup Olá foi criado.</span><span class="sxs-lookup"><span data-stu-id="95497-115">**From and To** – hello date and time range when hello backup set was created.</span></span>

<span data-ttu-id="95497-116">Olá conjuntos de backup filtrados são então tabulados com base em Olá seguintes atributos:</span><span class="sxs-lookup"><span data-stu-id="95497-116">hello filtered backup sets are then tabulated based on hello following attributes:</span></span>

* <span data-ttu-id="95497-117">**Nome** – hello nome de política de backup hello ou volumes associados ao conjunto de backup hello.</span><span class="sxs-lookup"><span data-stu-id="95497-117">**Name** – hello name of hello backup policy or volume associated with hello backup set.</span></span>
* <span data-ttu-id="95497-118">**Tamanho** – Olá tamanho real do conjunto de backup hello.</span><span class="sxs-lookup"><span data-stu-id="95497-118">**Size** – hello actual size of hello backup set.</span></span>
* <span data-ttu-id="95497-119">**Criado em** – a data de saudação e a hora quando foram criados backups hello.</span><span class="sxs-lookup"><span data-stu-id="95497-119">**Created On** – hello date and time when hello backups were created.</span></span> 
* <span data-ttu-id="95497-120">**Tipo** – Conjuntos de Backup podem ser instantâneos locais ou instantâneos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="95497-120">**Type** – Backup sets can be local snapshots or cloud snapshots.</span></span> <span data-ttu-id="95497-121">Um instantâneo local é um backup de todos os dados de volume armazenados localmente no dispositivo hello, enquanto um instantâneo de nuvem se refere a toohello backup dos dados de volume que residem na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="95497-121">A local snapshot is a backup of all your volume data stored locally on hello device, whereas a cloud snapshot refers toohello backup of volume data residing in hello cloud.</span></span> <span data-ttu-id="95497-122">Instantâneos locais fornecem acesso mais rápido, enquanto os instantâneos de nuvem são escolhidos para resiliência de dados.</span><span class="sxs-lookup"><span data-stu-id="95497-122">Local snapshots provide faster access, whereas cloud snapshots are chosen for data resiliency.</span></span>
* <span data-ttu-id="95497-123">**Iniciado por** – backups Olá podem ser iniciados automaticamente por uma agenda ou manualmente por um usuário.</span><span class="sxs-lookup"><span data-stu-id="95497-123">**Initiated By** – hello backups can be initiated automatically by a schedule or manually by a user.</span></span> <span data-ttu-id="95497-124">Você pode usar backups de tooschedule uma política de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-124">You can use a backup policy tooschedule backups.</span></span> <span data-ttu-id="95497-125">Como alternativa, você pode usar o hello **fazer backup** tootake opção um backup manual.</span><span class="sxs-lookup"><span data-stu-id="95497-125">Alternatively, you can use hello **Take backup** option tootake a manual backup.</span></span>

## <a name="list-backup-sets-for-a-backup-policy"></a><span data-ttu-id="95497-126">Listar conjuntos de backup para uma política de backup</span><span class="sxs-lookup"><span data-stu-id="95497-126">List backup sets for a backup policy</span></span>
<span data-ttu-id="95497-127">As etapas a seguir Olá completa toolist todos os backups de saudação para uma política de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-127">Complete hello following steps toolist all hello backups for a backup policy.</span></span>

#### <a name="toolist-backup-sets"></a><span data-ttu-id="95497-128">conjuntos de backup toolist</span><span class="sxs-lookup"><span data-stu-id="95497-128">toolist backup sets</span></span>
1. <span data-ttu-id="95497-129">Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **catálogo de Backup**.</span><span class="sxs-lookup"><span data-stu-id="95497-129">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>

2. <span data-ttu-id="95497-130">Filtre seleções de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="95497-130">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="95497-131">Especifique o intervalo de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="95497-131">Specify hello time range.</span></span>
   2. <span data-ttu-id="95497-132">Selecione dispositivo de saudação apropriado.</span><span class="sxs-lookup"><span data-stu-id="95497-132">Select hello appropriate device.</span></span>
   3. <span data-ttu-id="95497-133">Filtrar por **política de Backup** tooview Olá backups de saudação correspondente.</span><span class="sxs-lookup"><span data-stu-id="95497-133">Filter by **Backup policy** tooview hello corresponding hello backups.</span></span>
   3. <span data-ttu-id="95497-134">Na lista suspensa política de backup hello, escolha **todos os** tooview todos Olá backups em Olá selecionado dispositivo.</span><span class="sxs-lookup"><span data-stu-id="95497-134">From hello backup policy dropdown list, choose **All** tooview all hello backups on hello selected device.</span></span>
   4. <span data-ttu-id="95497-135">Clique em **aplicar** tooexecute esta consulta.</span><span class="sxs-lookup"><span data-stu-id="95497-135">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="95497-136">backups Olá associados à política de backup Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-136">hello backups associated with hello selected backup policy should appear in hello list of backup sets.</span></span>

      ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

## <a name="select-a-backup-set"></a><span data-ttu-id="95497-138">Selecione um conjunto de backup</span><span class="sxs-lookup"><span data-stu-id="95497-138">Select a backup set</span></span>
<span data-ttu-id="95497-139">Olá completa tooselect as etapas a seguir um backup definido para uma política de backup ou volume.</span><span class="sxs-lookup"><span data-stu-id="95497-139">Complete hello following steps tooselect a backup set for a volume or backup policy.</span></span>

#### <a name="tooselect-a-backup-set"></a><span data-ttu-id="95497-140">tooselect um conjunto de backup</span><span class="sxs-lookup"><span data-stu-id="95497-140">tooselect a backup set</span></span>
1. <span data-ttu-id="95497-141">Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **catálogo de Backup**.</span><span class="sxs-lookup"><span data-stu-id="95497-141">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="95497-142">Filtre seleções de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="95497-142">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="95497-143">Especifique o intervalo de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="95497-143">Specify hello time range.</span></span> 
   2. <span data-ttu-id="95497-144">Selecione dispositivo de saudação apropriado.</span><span class="sxs-lookup"><span data-stu-id="95497-144">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="95497-145">Filtrar por política de backup ou volume para backup de saudação que você deseja tooselect.</span><span class="sxs-lookup"><span data-stu-id="95497-145">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="95497-146">Clique em **aplicar** tooexecute esta consulta.</span><span class="sxs-lookup"><span data-stu-id="95497-146">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="95497-147">Hello backups associados à política de backup ou volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-147">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="95497-149">Selecione e expanda um conjunto de backups.</span><span class="sxs-lookup"><span data-stu-id="95497-149">Select and expand a backup set.</span></span> <span data-ttu-id="95497-150">Agora você pode ver os conjuntos de backup Olá divididos por volumes Olá que ele contém.</span><span class="sxs-lookup"><span data-stu-id="95497-150">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="95497-151">Olá **restaurar** e **excluir** opções estão disponíveis por meio do menu de contexto (direito) Olá Olá conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-151">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="95497-152">Você pode executar qualquer uma dessas ações no conjunto de backup de saudação que você selecionou.</span><span class="sxs-lookup"><span data-stu-id="95497-152">You can perform either of these actions on hello backup set that you selected.</span></span>

    ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog2.png)

## <a name="delete-a-backup-set"></a><span data-ttu-id="95497-154">Excluir um conjunto de backups</span><span class="sxs-lookup"><span data-stu-id="95497-154">Delete a backup set</span></span>
<span data-ttu-id="95497-155">Exclua um backup quando você não deseja mais dados de saudação tooretain associados a ele.</span><span class="sxs-lookup"><span data-stu-id="95497-155">Delete a backup when you no longer wish tooretain hello data associated with it.</span></span> <span data-ttu-id="95497-156">Execute Olá seguindo as etapas toodelete um conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-156">Perform hello following steps toodelete a backup set.</span></span>

#### <a name="toodelete-a-backup-set"></a><span data-ttu-id="95497-157">toodelete um conjunto de backup</span><span class="sxs-lookup"><span data-stu-id="95497-157">toodelete a backup set</span></span>
 <span data-ttu-id="95497-158">Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **catálogo de Backup**.</span><span class="sxs-lookup"><span data-stu-id="95497-158">Go tooyour StorSimple Device Manager service and click **Backup catalog**.</span></span>
2. <span data-ttu-id="95497-159">Filtre seleções de saudação da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="95497-159">Filter hello selections as follows:</span></span>
   
   1. <span data-ttu-id="95497-160">Especifique o intervalo de tempo de saudação.</span><span class="sxs-lookup"><span data-stu-id="95497-160">Specify hello time range.</span></span> 
   2. <span data-ttu-id="95497-161">Selecione dispositivo de saudação apropriado.</span><span class="sxs-lookup"><span data-stu-id="95497-161">Select hello appropriate device.</span></span> 
   3. <span data-ttu-id="95497-162">Filtrar por política de backup ou volume para backup de saudação que você deseja tooselect.</span><span class="sxs-lookup"><span data-stu-id="95497-162">Filter by volume or backup policy for hello backup that you wish tooselect.</span></span>
   4. <span data-ttu-id="95497-163">Clique em **aplicar** tooexecute esta consulta.</span><span class="sxs-lookup"><span data-stu-id="95497-163">Click **Apply** tooexecute this query.</span></span>
      
      <span data-ttu-id="95497-164">Hello backups associados à política de backup ou volume Olá selecionado devem aparecer na lista de saudação de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-164">hello backups associated with hello selected volume or backup policy should appear in hello list of backup sets.</span></span>

      ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog1.png)

3. <span data-ttu-id="95497-166">Selecione e expanda um conjunto de backups.</span><span class="sxs-lookup"><span data-stu-id="95497-166">Select and expand a backup set.</span></span> <span data-ttu-id="95497-167">Agora você pode ver os conjuntos de backup Olá divididos por volumes Olá que ele contém.</span><span class="sxs-lookup"><span data-stu-id="95497-167">You can now see hello backup sets broken down by hello volumes that it contains.</span></span> <span data-ttu-id="95497-168">Olá **restaurar** e **excluir** opções estão disponíveis por meio do menu de contexto (direito) Olá Olá conjunto de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-168">hello **Restore** and **Delete** options are available via hello context menu (right-click) for hello backup set.</span></span> <span data-ttu-id="95497-169">Conjunto de backup Olá selecionado e Olá no menu de contexto, selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="95497-169">Right-click hello selected backup set and from hello context menu, select **Delete**.</span></span>

    ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog3.png)

4. <span data-ttu-id="95497-171">Quando solicitado para confirmação, examine informações Olá exibido e clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="95497-171">When prompted for confirmation, review hello displayed information and click **Delete**.</span></span> <span data-ttu-id="95497-172">backup de saudação selecionado será excluído permanentemente.</span><span class="sxs-lookup"><span data-stu-id="95497-172">hello selected backup is deleted permanently.</span></span>

    ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog4.png)  

5. <span data-ttu-id="95497-174">Você será notificado quando Olá exclusão está em andamento e quando ele foi concluído com êxito.</span><span class="sxs-lookup"><span data-stu-id="95497-174">You will be notified when hello deletion is in progress and when it has successfully finished.</span></span> <span data-ttu-id="95497-175">Após a exclusão hello, atualize a consulta de saudação nesta página.</span><span class="sxs-lookup"><span data-stu-id="95497-175">After hello deletion is done, refresh hello query on this page.</span></span> <span data-ttu-id="95497-176">Não, o conjunto de backup Olá excluída aparecerá na lista de saudação de conjuntos de backup.</span><span class="sxs-lookup"><span data-stu-id="95497-176">hello deleted backup set will no longer appear in hello list of backup sets.</span></span>

    ![Vá toobackup catálogo](./media/storsimple-8000-manage-backup-catalog/bucatalog7.png)

## <a name="next-steps"></a><span data-ttu-id="95497-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="95497-178">Next steps</span></span>
* <span data-ttu-id="95497-179">Saiba como muito[use Olá toorestore do catálogo de backup de seu dispositivo de um conjunto de backup](storsimple-8000-restore-from-backup-set-u2.md).</span><span class="sxs-lookup"><span data-stu-id="95497-179">Learn how too[use hello backup catalog toorestore your device from a backup set](storsimple-8000-restore-from-backup-set-u2.md).</span></span>
* <span data-ttu-id="95497-180">Saiba como muito[use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="95497-180">Learn how too[use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

