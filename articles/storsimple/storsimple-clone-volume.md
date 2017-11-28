---
title: Clonar o volume StorSimple | Microsoft Docs
description: "Descreve os tipos diferentes de clone e quando usá-los, e explica como você pode usar um conjunto de backups para clonar um volume individual."
services: storsimple
documentationcenter: NA
author: alkohli
manager: carmonm
editor: 
ms.assetid: b5d615f2-02a7-4222-9867-6c0385ce748c
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: 8f1936fac543f559a44ad0f9c35b30d1a92dce68
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-storsimple-manager-service-to-clone-a-volume"></a><span data-ttu-id="39551-103">Usar o serviço StorSimple Manager para clonar um volume</span><span class="sxs-lookup"><span data-stu-id="39551-103">Use the StorSimple Manager service to clone a volume</span></span>
[!INCLUDE [storsimple-version-selector-clone-volume](../../includes/storsimple-version-selector-clone-volume.md)]

## <a name="overview"></a><span data-ttu-id="39551-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="39551-104">Overview</span></span>
<span data-ttu-id="39551-105">A página **Catálogo de Backup** do serviço StorSimple Manager exibe todos os conjuntos de backup criados após a realização de backups manuais ou automatizados.</span><span class="sxs-lookup"><span data-stu-id="39551-105">The StorSimple Manager service **Backup Catalog** page displays all the backup sets that are created when manual or automated backups are taken.</span></span> <span data-ttu-id="39551-106">Você pode usar esta página para listar todos os backups para uma política de backup ou volume, selecionar ou excluir os backups, ou usar um backup para restaurar ou clonar um volume.</span><span class="sxs-lookup"><span data-stu-id="39551-106">You can use this page to list all the backups for a backup policy or a volume, select or delete backups, or use a backup to restore or clone a volume.</span></span>

![Página Catálogo de backup](./media/storsimple-clone-volume/HCS_BackupCatalog.png)  

<span data-ttu-id="39551-108">Este tutorial descreve como você pode usar um conjunto de backups para clonar um volume individual.</span><span class="sxs-lookup"><span data-stu-id="39551-108">This tutorial describes how you can use a backup set to clone an individual volume.</span></span> <span data-ttu-id="39551-109">Ele também explica a diferença entre os clones *transitório* e *permanente*.</span><span class="sxs-lookup"><span data-stu-id="39551-109">It also explains the difference between *transient* and *permanent* clones.</span></span> 

## <a name="create-a-clone-of-a-volume"></a><span data-ttu-id="39551-110">Criar clone de um volume</span><span class="sxs-lookup"><span data-stu-id="39551-110">Create a clone of a volume</span></span>
<span data-ttu-id="39551-111">Você pode criar um clone no mesmo dispositivo, em outro dispositivo ou mesmo em uma máquina virtual usando um instantâneo local ou na nuvem.</span><span class="sxs-lookup"><span data-stu-id="39551-111">You can create a clone on the same device, another device, or even a virtual machine by using a local or a cloud snapshot.</span></span>

#### <a name="to-clone-a-volume"></a><span data-ttu-id="39551-112">Para clonar um volume</span><span class="sxs-lookup"><span data-stu-id="39551-112">To clone a volume</span></span>
1. <span data-ttu-id="39551-113">Na página do serviço Gerenciador StorSimple, clique no **Catálogo de backup** e selecione um conjunto de backups.</span><span class="sxs-lookup"><span data-stu-id="39551-113">On the StorSimple Manager service page, click the **Backup catalog** tab and select a backup set.</span></span>
2. <span data-ttu-id="39551-114">Expanda o conjunto de backups para exibir os volumes associados.</span><span class="sxs-lookup"><span data-stu-id="39551-114">Expand the backup set to view the associated volumes.</span></span> <span data-ttu-id="39551-115">Clique e selecione um volume no conjunto de backups.</span><span class="sxs-lookup"><span data-stu-id="39551-115">Click and select a volume from the backup set.</span></span>
   
     ![Clonar um volume](./media/storsimple-clone-volume/HCS_Clone.png) 
3. <span data-ttu-id="39551-117">Clique em **Clonar** para começar a clonar o volume selecionado.</span><span class="sxs-lookup"><span data-stu-id="39551-117">Click **Clone** to begin cloning the selected volume.</span></span>
4. <span data-ttu-id="39551-118">No assistente Clonar Volume, em **Especificar nome e local**:</span><span class="sxs-lookup"><span data-stu-id="39551-118">In the Clone Volume wizard, under **Specify name and location**:</span></span>
   
   1. <span data-ttu-id="39551-119">Identificar um dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="39551-119">Identify a target device.</span></span> <span data-ttu-id="39551-120">Esse é o local onde o clone será criado.</span><span class="sxs-lookup"><span data-stu-id="39551-120">This is the location where the clone will be created.</span></span> <span data-ttu-id="39551-121">Você pode escolher o mesmo dispositivo ou especificar outro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="39551-121">You can choose the same device or specify another device.</span></span> <span data-ttu-id="39551-122">Se você escolher um volume associado a outros provedores de serviço de nuvem (não do Azure), a lista suspensa do dispositivo de destino mostrará apenas os dispositivos físicos.</span><span class="sxs-lookup"><span data-stu-id="39551-122">If you choose a volume associated with other cloud service providers (not Azure), the drop-down list for the target device will only show physical devices.</span></span> <span data-ttu-id="39551-123">Não é possível clonar um volume associado a outros provedores de serviço de nuvem em um dispositivo virtual.</span><span class="sxs-lookup"><span data-stu-id="39551-123">You cannot clone a volume associated with other cloud service providers on a virtual device.</span></span>
      
      > [!NOTE]
      > <span data-ttu-id="39551-124">Verifique se a capacidade necessária para o clone é menor que a capacidade disponível no dispositivo de destino.</span><span class="sxs-lookup"><span data-stu-id="39551-124">Make sure that the capacity required for the clone is lower than the capacity available on the target device.</span></span>
      > 
      > 
   2. <span data-ttu-id="39551-125">Especifique um nome de volume exclusivo para o clone.</span><span class="sxs-lookup"><span data-stu-id="39551-125">Specify a unique volume name for your clone.</span></span> <span data-ttu-id="39551-126">O nome deve conter entre 3 e 127 caracteres.</span><span class="sxs-lookup"><span data-stu-id="39551-126">The name must contain between 3 and 127 characters.</span></span>
   3. <span data-ttu-id="39551-127">Clique no ícone de seta </span><span class="sxs-lookup"><span data-stu-id="39551-127">Click the arrow icon</span></span> ![ícone-de-seta](./media/storsimple-clone-volume/HCS_ArrowIcon.png) <span data-ttu-id="39551-129">para continuar para a próxima página.</span><span class="sxs-lookup"><span data-stu-id="39551-129">to proceed to the next page.</span></span>
5. <span data-ttu-id="39551-130">Em **Especificar os hosts que podem usar este volume**:</span><span class="sxs-lookup"><span data-stu-id="39551-130">Under **Specify hosts that can use this volume**:</span></span>
   
   1. <span data-ttu-id="39551-131">Especificar um registro de controle de acesso (ACR) para o clone.</span><span class="sxs-lookup"><span data-stu-id="39551-131">Specify an access control record (ACR) for the clone.</span></span> <span data-ttu-id="39551-132">Você pode adicionar um novo ACR ou escolher na lista existente.</span><span class="sxs-lookup"><span data-stu-id="39551-132">You can add a new ACR or choose from the existing list.</span></span>
   2. <span data-ttu-id="39551-133">Clique no ícone de verificação </span><span class="sxs-lookup"><span data-stu-id="39551-133">Click the check icon</span></span> ![check-icon](./media/storsimple-clone-volume/HCS_CheckIcon.png)<span data-ttu-id="39551-135">para concluir a operação.</span><span class="sxs-lookup"><span data-stu-id="39551-135">to complete the operation.</span></span>
6. <span data-ttu-id="39551-136">Um trabalho de clone será iniciado e você será notificado quando o clone for criado com êxito.</span><span class="sxs-lookup"><span data-stu-id="39551-136">A clone job will be initiated and you will be notified when the clone is successfully created.</span></span> <span data-ttu-id="39551-137">Clique em **Exibir Trabalho** para monitorar o trabalho de clone na página **Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="39551-137">Click **View Job** to monitor the clone job on the **Jobs** page.</span></span>
7. <span data-ttu-id="39551-138">Depois do trabalho de clone ser concluído:</span><span class="sxs-lookup"><span data-stu-id="39551-138">After the clone job is completed:</span></span>
   
   1. <span data-ttu-id="39551-139">Vá para a página **Dispositivos** e selecione a guia **Contêineres do Volume**.</span><span class="sxs-lookup"><span data-stu-id="39551-139">Go to the **Devices** page, and select the **Volume Containers** tab.</span></span> 
   2. <span data-ttu-id="39551-140">Selecione o contêiner do volume associado ao volume de origem clonado.</span><span class="sxs-lookup"><span data-stu-id="39551-140">Select the volume container that is associated with the source volume that you cloned.</span></span> <span data-ttu-id="39551-141">Na lista de volumes, você deve ver o clone que acabou de criar.</span><span class="sxs-lookup"><span data-stu-id="39551-141">In the list of volumes, you should see the clone that was just created.</span></span>

> [!NOTE]
> <span data-ttu-id="39551-142">O monitoramento e o backup padrão são desabilitados automaticamente em um volume clonado.</span><span class="sxs-lookup"><span data-stu-id="39551-142">Monitoring and default backup are automatically disabled on a cloned volume.</span></span>
> 
> 

<span data-ttu-id="39551-143">Um clone criado dessa maneira é um clone transitório.</span><span class="sxs-lookup"><span data-stu-id="39551-143">A clone that is created this way is a transient clone.</span></span> <span data-ttu-id="39551-144">Para obter mais informações sobre os tipos de clone, consulte [Clones transitórios versus permanentes](#transient-vs-permanent-clones).</span><span class="sxs-lookup"><span data-stu-id="39551-144">For more information about clone types, see [Transient vs. permanent clones](#transient-vs-permanent-clones).</span></span>

<span data-ttu-id="39551-145">O clone é agora um volume normal e qualquer operação que é possível em um volume estará disponível para o clone.</span><span class="sxs-lookup"><span data-stu-id="39551-145">This clone is now a regular volume, and any operation that is possible on a volume will be available for the clone.</span></span> <span data-ttu-id="39551-146">Você precisará configurar este volume para qualquer backup.</span><span class="sxs-lookup"><span data-stu-id="39551-146">You will need to configure this volume for any backups.</span></span>

## <a name="transient-vs-permanent-clones"></a><span data-ttu-id="39551-147">Clones transitórios versus permanentes</span><span class="sxs-lookup"><span data-stu-id="39551-147">Transient vs. permanent clones</span></span>
<span data-ttu-id="39551-148">Os clones transitórios e permanentes são criados apenas quando a clonagem está sendo realizada para um dispositivo diferente.</span><span class="sxs-lookup"><span data-stu-id="39551-148">Transient and permanent clones are created only when you are cloning on to a different device.</span></span> <span data-ttu-id="39551-149">Você pode clonar um volume específico por meio de um conjunto de backups para um dispositivo diferente.</span><span class="sxs-lookup"><span data-stu-id="39551-149">You can clone a specific volume from a backup set to a different device.</span></span> <span data-ttu-id="39551-150">Um clone criado dessa maneira é um clone *transitório* .</span><span class="sxs-lookup"><span data-stu-id="39551-150">A clone created in this way is a *transient* clone.</span></span> <span data-ttu-id="39551-151">O clone transitório terá referências para o volume original e usará esse volume para ler durante a gravação local.</span><span class="sxs-lookup"><span data-stu-id="39551-151">The transient clone will have references to the original volume and will use that volume to read while writing locally.</span></span> 

<span data-ttu-id="39551-152">Depois de fazer um instantâneo de nuvem de um clone transitório, o clone resultante será um clone *permanente* .</span><span class="sxs-lookup"><span data-stu-id="39551-152">After you take a cloud snapshot of a transient clone, the resulting clone will be a *permanent* clone.</span></span> <span data-ttu-id="39551-153">O clone permanente é independente e não tem nenhuma referência para o volume original do qual foi clonado.</span><span class="sxs-lookup"><span data-stu-id="39551-153">The permanent clone is independent and doesn’t have any references to the original volume that it was cloned from.</span></span>  

## <a name="scenarios-for-transient-and-permanent-clones"></a><span data-ttu-id="39551-154">Cenários para os clones transitórios e permanentes</span><span class="sxs-lookup"><span data-stu-id="39551-154">Scenarios for transient and permanent clones</span></span>
<span data-ttu-id="39551-155">As seções a seguir descrevem as situações de exemplo nas quais os clones transitórios e permanentes podem ser usados.</span><span class="sxs-lookup"><span data-stu-id="39551-155">The following sections describe example situations in which transient and permanent clones can be used.</span></span>

### <a name="item-level-recovery-with-a-transient-clone"></a><span data-ttu-id="39551-156">Recuperação ao nível do item com um clone transitório</span><span class="sxs-lookup"><span data-stu-id="39551-156">Item-level recovery with a transient clone</span></span>
<span data-ttu-id="39551-157">Você precisa recuperar um arquivo de apresentação do Microsoft PowerPoint com um ano.</span><span class="sxs-lookup"><span data-stu-id="39551-157">You need to recover a one-year-old Microsoft PowerPoint presentation file.</span></span> <span data-ttu-id="39551-158">O administrador de TI identifica o backup específico desse intervalo de tempo, em seguida, filtra o volume.</span><span class="sxs-lookup"><span data-stu-id="39551-158">Your IT administrator identifies the specific backup from that time frame, and then filters the volume.</span></span> <span data-ttu-id="39551-159">Então, o administrador clona o volume, localiza o arquivo que você está procurando e fornece a você.</span><span class="sxs-lookup"><span data-stu-id="39551-159">The administrator then clones the volume, locates the file that you are looking for, and provides it to you.</span></span> <span data-ttu-id="39551-160">Nesse cenário, é usado um clone transitório.</span><span class="sxs-lookup"><span data-stu-id="39551-160">In this scenario, a transient clone is used.</span></span> 

<span data-ttu-id="39551-161">![Vídeo disponível](./media/storsimple-clone-volume/Video_icon.png) **Vídeo disponível**</span><span class="sxs-lookup"><span data-stu-id="39551-161">![Video available](./media/storsimple-clone-volume/Video_icon.png) **Video available**</span></span>

<span data-ttu-id="39551-162">Para assistir a um vídeo que demonstra como você pode usar os recursos de clonagem e restauração no StorSimple para recuperar arquivos excluídos, clique [aqui](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span><span class="sxs-lookup"><span data-stu-id="39551-162">To watch a video that demonstrates how you can use the clone and restore features in StorSimple to recover deleted files, click [here](https://azure.microsoft.com/documentation/videos/storsimple-recover-deleted-files-with-storsimple/).</span></span>

### <a name="testing-in-the-production-environment-with-a-permanent-clone"></a><span data-ttu-id="39551-163">Testando no ambiente de produção com um clone permanente</span><span class="sxs-lookup"><span data-stu-id="39551-163">Testing in the production environment with a permanent clone</span></span>
<span data-ttu-id="39551-164">Você precisa verificar um bug de teste no ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="39551-164">You need to verify a testing bug in the production environment.</span></span> <span data-ttu-id="39551-165">Você cria um clone do volume no ambiente de produção fazendo um instantâneo da nuvem desse clone.</span><span class="sxs-lookup"><span data-stu-id="39551-165">You create a clone of the volume in the production environment by taking a cloud snapshot of this clone.</span></span> <span data-ttu-id="39551-166">O volume clonado agora é independente.</span><span class="sxs-lookup"><span data-stu-id="39551-166">The cloned volume is now independent.</span></span> <span data-ttu-id="39551-167">Nesse cenário, é usado um clone permanente.</span><span class="sxs-lookup"><span data-stu-id="39551-167">In this scenario, a permanent clone is used.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39551-168">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="39551-168">Next steps</span></span>
* <span data-ttu-id="39551-169">Saiba como [restaurar um volume StorSimple a partir de um conjunto de backups](storsimple-restore-from-backup-set.md).</span><span class="sxs-lookup"><span data-stu-id="39551-169">Learn how to [restore a StorSimple volume from a backup set](storsimple-restore-from-backup-set.md).</span></span>
* <span data-ttu-id="39551-170">Saiba como [usar o serviço StorSimple Manager para administrar seu dispositivo StorSimple](storsimple-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="39551-170">Learn how to [use the StorSimple Manager service to administer your StorSimple device](storsimple-manager-service-administration.md).</span></span>

