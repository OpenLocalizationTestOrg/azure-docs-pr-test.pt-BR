---
title: "aaaStorSimple failover, recuperação de desastres tooa StorSimple Appliance de nuvem | Microsoft Docs"
description: "Saiba como toofail sobre seu tooa de dispositivo físico StorSimple 8000 series nuvem de dispositivo."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 07/03/2017
ms.author: alkohli
ms.openlocfilehash: e8a0bca057024358e3a557fe85a42ddefea36cff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-tooyour-storsimple-cloud-appliance"></a><span data-ttu-id="0a745-103">Failover tooyour StorSimple Appliance de nuvem</span><span class="sxs-lookup"><span data-stu-id="0a745-103">Fail over tooyour StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="0a745-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0a745-104">Overview</span></span>

<span data-ttu-id="0a745-105">Este tutorial descreve Olá etapas necessárias toofail em um tooa de dispositivo físico StorSimple 8000 series StorSimple Appliance de nuvem se houver um desastre.</span><span class="sxs-lookup"><span data-stu-id="0a745-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooa StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="0a745-106">StorSimple usa dados saudação dispositivo failover recurso toomigrate de um dispositivo físico de origem no dispositivo de nuvem Olá datacenter tooa em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="0a745-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooa cloud appliance running in Azure.</span></span> <span data-ttu-id="0a745-107">Guia de saudação neste tutorial se aplica a dispositivos físicos de série tooStorSimple 8000 e soluções de nuvem que executam versões do software Update 3 e posterior.</span><span class="sxs-lookup"><span data-stu-id="0a745-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="0a745-108">toolearn mais informações sobre failover de dispositivo e como ele é usado toorecover de um desastre, ir muito[Failover e recuperação de desastres para dispositivos da série StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="0a745-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="0a745-109">toofail em um dispositivo físico tooanother dispositivo físico StorSimple, ir muito[failover do dispositivo físico do StorSimple tooa](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="0a745-109">toofail over a StorSimple physical device tooanother physical device, go too[Fail over tooa StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="0a745-110">toofail em tooitself um dispositivo, vá muito[failover toohello mesmo dispositivo físico StorSimple](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="0a745-110">toofail over a device tooitself, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="0a745-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0a745-111">Prerequisites</span></span>

- <span data-ttu-id="0a745-112">Certifique-se de ter revisado as considerações de saudação para failover de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0a745-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="0a745-113">Para obter mais informações, vá muito[considerações comuns para failover de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="0a745-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="0a745-114">Você deve ter um Dispositivo de Nuvem StorSimple criado e configurado antes de executar este procedimento.</span><span class="sxs-lookup"><span data-stu-id="0a745-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="0a745-115">Se atualizar 3 versão do software ou posteriormente, considere o uso de um dispositivo de nuvem 8020 para execução Olá DR.</span><span class="sxs-lookup"><span data-stu-id="0a745-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for hello DR.</span></span> <span data-ttu-id="0a745-116">modelo 8020 Olá tem 64 TB e usa o armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="0a745-116">hello 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="0a745-117">Para obter mais informações, vá muito[implantar e gerenciar um dispositivo de nuvem StorSimple](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="0a745-117">For more information, go too[Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-toofail-over-tooa-cloud-appliance"></a><span data-ttu-id="0a745-118">Etapas toofail sobre tooa appliance de nuvem</span><span class="sxs-lookup"><span data-stu-id="0a745-118">Steps toofail over tooa cloud appliance</span></span>

<span data-ttu-id="0a745-119">Execute Olá seguindo as etapas toorestore Olá tooa de destino do dispositivo StorSimple Appliance de nuvem.</span><span class="sxs-lookup"><span data-stu-id="0a745-119">Perform hello following steps toorestore hello device tooa target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="0a745-120">Verifique se o contêiner de volume Olá que desejar toofail pela associou os instantâneos em nuvem.</span><span class="sxs-lookup"><span data-stu-id="0a745-120">Verify that hello volume container you want toofail over has associated cloud snapshots.</span></span> <span data-ttu-id="0a745-121">Para obter mais informações, vá muito[toocreate de serviço do Gerenciador de dispositivos de StorSimple Use backups](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="0a745-121">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="0a745-122">Serviço de Gerenciador de dispositivos de StorSimple tooyour go e clique em **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="0a745-122">Go tooyour StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="0a745-123">Em Olá **dispositivos** folha, vá toohello lista de dispositivos conectados ao seu serviço.</span><span class="sxs-lookup"><span data-stu-id="0a745-123">In hello **Devices** blade, go toohello list of devices connected with your service.</span></span>
    <span data-ttu-id="0a745-124">![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="0a745-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="0a745-125">Selecione e clique no dispositivo de origem.</span><span class="sxs-lookup"><span data-stu-id="0a745-125">Select and click your source device.</span></span> <span data-ttu-id="0a745-126">dispositivo de origem de saudação tem contêineres de volume de saudação que você desejar toofail pela.</span><span class="sxs-lookup"><span data-stu-id="0a745-126">hello source device has hello volume containers that you want toofail over.</span></span> <span data-ttu-id="0a745-127">Vá muito**Configurações > contêineres de Volume**.</span><span class="sxs-lookup"><span data-stu-id="0a745-127">Go too**Settings > Volume Containers**.</span></span>

    ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="0a745-129">Selecione um contêiner de volume que deseja toofail tooanother dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0a745-129">Select a volume container that you would like toofail over tooanother device.</span></span> <span data-ttu-id="0a745-130">Clique em Olá volume contêiner toodisplay Olá lista de volumes neste contêiner.</span><span class="sxs-lookup"><span data-stu-id="0a745-130">Click hello volume container toodisplay hello list of volumes within this container.</span></span> <span data-ttu-id="0a745-131">Selecione um volume, com o botão direito e clique em **colocar Offline** tootake volume de saudação offline.</span><span class="sxs-lookup"><span data-stu-id="0a745-131">Select a volume, right-click, and click **Take Offline** tootake hello volume offline.</span></span>

    ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="0a745-133">Repita esse processo para todos os volumes de saudação no contêiner de volume hello.</span><span class="sxs-lookup"><span data-stu-id="0a745-133">Repeat this process for all hello volumes in hello volume container.</span></span>

     ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="0a745-135">Etapa anterior Olá Repita para todos os contêineres de volume de Olá você gostaria que toofail de dispositivo tooanother.</span><span class="sxs-lookup"><span data-stu-id="0a745-135">Repeat hello previous step for all hello volume containers you would like toofail over tooanother device.</span></span>

7. <span data-ttu-id="0a745-136">Voltar toohello **dispositivos** folha.</span><span class="sxs-lookup"><span data-stu-id="0a745-136">Go back toohello **Devices** blade.</span></span> <span data-ttu-id="0a745-137">Na barra de comandos de saudação, clique em **failover**.</span><span class="sxs-lookup"><span data-stu-id="0a745-137">From hello command bar, click **Fail over**.</span></span>

    ![Clique em Fazer failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="0a745-139">Em Olá **failover** folha, executar Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="0a745-139">In hello **Fail over** blade, perform hello following steps:</span></span>
   
    1. <span data-ttu-id="0a745-140">Clique em **Fonte**.</span><span class="sxs-lookup"><span data-stu-id="0a745-140">Click **Source**.</span></span> <span data-ttu-id="0a745-141">Selecione toofail de contêineres de volume Olá acima.</span><span class="sxs-lookup"><span data-stu-id="0a745-141">Select hello volume containers toofail over.</span></span> <span data-ttu-id="0a745-142">**Olá apenas contêineres de volume com instantâneos de nuvem associados e volumes offline são exibidos.**</span><span class="sxs-lookup"><span data-stu-id="0a745-142">**Only hello volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="0a745-143">![Selecionar fonte](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="0a745-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="0a745-144">Clique em **Destino**.</span><span class="sxs-lookup"><span data-stu-id="0a745-144">Click **Target**.</span></span> <span data-ttu-id="0a745-145">Selecione um dispositivo de destino de nuvem na lista suspensa Olá dos dispositivos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="0a745-145">Select a target cloud appliance from hello dropdown list of available devices.</span></span> <span data-ttu-id="0a745-146">**Somente dispositivos de saudação que tem capacidade suficiente fonte tooaccommodate contêineres de volume são exibidos na lista de saudação.**</span><span class="sxs-lookup"><span data-stu-id="0a745-146">**Only hello devices that have sufficient capacity tooaccommodate source volume containers are displayed in hello list.**</span></span>

        ![Selecionar o destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="0a745-148">Examine as configurações de failover de saudação em **resumo** e selecione Olá caixa de seleção que indica se os volumes de saudação em contêineres de volume selecionados estão offline.</span><span class="sxs-lookup"><span data-stu-id="0a745-148">Review hello failover settings under **Summary** and select hello checkbox indicating that hello volumes in selected volume containers are offline.</span></span> 

        ![Examinar as configurações de failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="0a745-150">Um trabalho de failover é criado.</span><span class="sxs-lookup"><span data-stu-id="0a745-150">A failover job is created.</span></span> <span data-ttu-id="0a745-151">failover de saudação toomonitor de trabalho, clique em notificação de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="0a745-151">toomonitor hello failover job, click hello job notification.</span></span>

    ![Monitorar o trabalho de failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="0a745-153">Após a conclusão do failover Olá, volte toohello **dispositivos** folha.</span><span class="sxs-lookup"><span data-stu-id="0a745-153">After hello failover is completed, go back toohello **Devices** blade.</span></span>

    1. <span data-ttu-id="0a745-154">Selecione o dispositivo de saudação que foi usado como destino Olá Olá failover.</span><span class="sxs-lookup"><span data-stu-id="0a745-154">Select hello device that was used as hello target for hello failover.</span></span>

       ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="0a745-156">Clique em **Contêineres de Volume**.</span><span class="sxs-lookup"><span data-stu-id="0a745-156">Click **Volume Containers**.</span></span> <span data-ttu-id="0a745-157">Todos os contêineres de volume hello, junto com os volumes de saudação do dispositivo antigo do hello, devem ser listados.</span><span class="sxs-lookup"><span data-stu-id="0a745-157">All hello volume containers, along with hello volumes from hello old device, should be listed.</span></span>

       <span data-ttu-id="0a745-158">Se o contêiner de volume de saudação failover foi fixado localmente volumes, os volumes são failover como volumes em camadas.</span><span class="sxs-lookup"><span data-stu-id="0a745-158">If hello volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="0a745-159">Não há suporte para volumes fixados localmente em um Dispositivo de Nuvem StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0a745-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Exibir contêineres de volume de destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="0a745-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0a745-161">Next steps</span></span>

* <span data-ttu-id="0a745-162">Depois de executar um failover, talvez seja necessário muito[desativar ou excluir seu dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="0a745-162">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="0a745-163">Para obter informações sobre como toouse Olá Gerenciador de dispositivos de StorSimple de serviço, visite muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0a745-163">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

