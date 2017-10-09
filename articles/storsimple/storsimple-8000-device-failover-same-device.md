---
title: "aaaStorSimple failover, recuperação de desastres para dispositivos da 8000 série | Microsoft Docs"
description: Saiba como toofail sobre seu toohello de dispositivo StorSimple mesmo dispositivo.
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
ms.date: 06/23/2017
ms.author: alkohli
ms.openlocfilehash: b0b4216c7af6745ff68b85ca3d655691b43b4334
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="fail-over-your-storsimple-physical-device-toosame-device"></a><span data-ttu-id="0feeb-103">O failover de seu dispositivo de toosame do dispositivo físico StorSimple</span><span class="sxs-lookup"><span data-stu-id="0feeb-103">Fail over your StorSimple physical device toosame device</span></span>

## <a name="overview"></a><span data-ttu-id="0feeb-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="0feeb-104">Overview</span></span>

<span data-ttu-id="0feeb-105">Este tutorial descreve Olá etapas necessárias toofail em um tooitself de dispositivo físico StorSimple 8000 series se houver um desastre.</span><span class="sxs-lookup"><span data-stu-id="0feeb-105">This tutorial describes hello steps required toofail over a StorSimple 8000 series physical device tooitself if there is a disaster.</span></span> <span data-ttu-id="0feeb-106">StorSimple usa dados saudação dispositivo failover recurso toomigrate de um dispositivo físico de origem no dispositivo físico da saudação datacenter tooanother.</span><span class="sxs-lookup"><span data-stu-id="0feeb-106">StorSimple uses hello device failover feature toomigrate data from a source physical device in hello datacenter tooanother physical device.</span></span> <span data-ttu-id="0feeb-107">Guia de saudação neste tutorial se aplica a dispositivos físicos de série tooStorSimple 8000 que executam versões do software Update 3 e posterior.</span><span class="sxs-lookup"><span data-stu-id="0feeb-107">hello guidance in this tutorial applies tooStorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="0feeb-108">toolearn mais informações sobre failover de dispositivo e como ele é usado toorecover de um desastre, ir muito[Failover e recuperação de desastres para dispositivos da série StorSimple 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="0feeb-108">toolearn more about device failover and how it is used toorecover from a disaster, go too[Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="0feeb-109">toofail em um dispositivo físico do tooanother de dispositivo físico, vá muito[failover toohello mesmo dispositivo físico StorSimple](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="0feeb-109">toofail over a physical device tooanother physical device, go too[Fail over toohello same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="0feeb-110">toofail em um dispositivo físico de StorSimple tooa StorSimple Appliance de nuvem, ir muito[failover tooa StorSimple Appliance de nuvem](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="0feeb-110">toofail over a StorSimple physical device tooa StorSimple Cloud Appliance, go too[Fail over tooa StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0feeb-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0feeb-111">Prerequisites</span></span>

- <span data-ttu-id="0feeb-112">Certifique-se de ter revisado as considerações de saudação para failover de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0feeb-112">Ensure that you have reviewed hello considerations for device failover.</span></span> <span data-ttu-id="0feeb-113">Para obter mais informações, vá muito[considerações comuns para failover de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="0feeb-113">For more information, go too[Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-toofail-over-toohello-same-device"></a><span data-ttu-id="0feeb-114">Etapas toofail sobre toohello mesmo dispositivo</span><span class="sxs-lookup"><span data-stu-id="0feeb-114">Steps toofail over toohello same device</span></span>

<span data-ttu-id="0feeb-115">Executar Olá etapas a seguir se precisar de toofail toohello mesmo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0feeb-115">Perform hello following steps if you need toofail over toohello same device.</span></span>

1. <span data-ttu-id="0feeb-116">Tire instantâneos em nuvem de todos os volumes de saudação em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0feeb-116">Take cloud snapshots of all hello volumes in your device.</span></span> <span data-ttu-id="0feeb-117">Para obter mais informações, vá muito[toocreate de serviço do Gerenciador de dispositivos de StorSimple Use backups](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="0feeb-117">For more information, go too[Use StorSimple Device Manager service toocreate backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="0feeb-118">Redefina o dispositivo toofactory padrão.</span><span class="sxs-lookup"><span data-stu-id="0feeb-118">Reset your device toofactory defaults.</span></span> <span data-ttu-id="0feeb-119">Siga Olá detalhadas instruções [como configurações de padrão tooreset um toofactory de dispositivo StorSimple](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="0feeb-119">Follow hello detailed instructions in [how tooreset a StorSimple device toofactory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="0feeb-120">Serviço de Gerenciador de dispositivos de StorSimple toohello go e, em seguida, selecione **dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="0feeb-120">Go toohello StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="0feeb-121">Em Olá **dispositivos** folha, dispositivo antigo Olá deve aparecer como **Offline**.</span><span class="sxs-lookup"><span data-stu-id="0feeb-121">In hello **Devices** blade, hello old device should show as **Offline**.</span></span>

    ![Dispositivo de origem offline](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="0feeb-123">Configure o seu dispositivo e registre-o novamente no serviço do Gerenciador de Dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="0feeb-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="0feeb-124">Olá dispositivo registrado recentemente deve aparecer como **pronto tooset backup**.</span><span class="sxs-lookup"><span data-stu-id="0feeb-124">hello newly registered device should show as **Ready tooset up**.</span></span> <span data-ttu-id="0feeb-125">nome do dispositivo Olá para o novo dispositivo de saudação é hello igual ao dispositivo antigo Olá mas anexado com um numeral tooindicate dispositivo Olá era redefinição toofactory padrão e registrados novamente.</span><span class="sxs-lookup"><span data-stu-id="0feeb-125">hello device name for hello new device is hello same as hello old device but appended with a numeral tooindicate that hello device was reset toofactory default and registered again.</span></span>

    ![Dispositivo registrado recentemente a tooset pronto para cima](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="0feeb-127">Para o novo dispositivo de hello, conclua a configuração de dispositivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="0feeb-127">For hello new device, complete hello device setup.</span></span> <span data-ttu-id="0feeb-128">Para obter mais informações, vá muito[etapa 4: concluir a configuração mínima do dispositivo](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="0feeb-128">For more information, go too[Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="0feeb-129">Em Olá **dispositivos** folha, status de saudação do dispositivo Olá muda muito**Online**.</span><span class="sxs-lookup"><span data-stu-id="0feeb-129">On hello **Devices** blade, hello status of hello device changes too**Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="0feeb-130">**Concluir a configuração mínima de saudação pela primeira vez ou a recuperação de desastres pode falhar.**</span><span class="sxs-lookup"><span data-stu-id="0feeb-130">**Complete hello minimum configuration first, or your DR may fail.**</span></span>

    ![Dispositivo recém-registrado online](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="0feeb-132">Selecione o dispositivo antigo da saudação (status offline) e na barra de comandos de saudação, clique em **failover**.</span><span class="sxs-lookup"><span data-stu-id="0feeb-132">Select hello old device (status offline) and from hello command bar, click **Fail over**.</span></span> <span data-ttu-id="0feeb-133">Em Olá **failover** folha, selecione antigo dispositivo como origem de saudação e especifique o dispositivo de destino hello como Olá dispositivo registrado recentemente.</span><span class="sxs-lookup"><span data-stu-id="0feeb-133">In hello **Fail over** blade, select old device as hello source and specify hello target device as hello newly registered device.</span></span>

    ![Resumo de failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="0feeb-135">Para obter instruções detalhadas, consulte muito[failover de dispositivo físico tooanother](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="0feeb-135">For detailed instructions, refer too[Fail over tooanother physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="0feeb-136">Um trabalho de restauração do dispositivo é criado que você pode monitorar de saudação **trabalhos** folha.</span><span class="sxs-lookup"><span data-stu-id="0feeb-136">A device restore job is created that you can monitor from hello **Jobs** blade.</span></span>

8. <span data-ttu-id="0feeb-137">Depois que o trabalho de saudação for concluída com êxito, acessar o novo dispositivo de saudação e navegar toohello **contêineres de Volume** folha.</span><span class="sxs-lookup"><span data-stu-id="0feeb-137">After hello job has successfully completed, access hello new device and navigate toohello **Volume containers** blade.</span></span> <span data-ttu-id="0feeb-138">Verifique se todos os contêineres de volume de saudação do dispositivo antigo Olá foram migradas toohello novo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="0feeb-138">Verify that all hello volume containers from hello old device have migrated toohello new device.</span></span>

   ![Contêineres de volume migrados](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="0feeb-140">Após a conclusão do failover hello, você pode desativar e excluir dispositivo antigo saudação do portal de saudação.</span><span class="sxs-lookup"><span data-stu-id="0feeb-140">After hello failover is complete, you can deactivate and delete hello old device from hello portal.</span></span> <span data-ttu-id="0feeb-141">Selecione Olá antigo dispositivo (offline), com o botão direito e, em seguida, selecione **desativar**.</span><span class="sxs-lookup"><span data-stu-id="0feeb-141">Select hello old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="0feeb-142">Depois que o dispositivo hello está desativado, status de saudação do dispositivo Olá é atualizado.</span><span class="sxs-lookup"><span data-stu-id="0feeb-142">After hello device is deactivated, hello status of hello device is updated.</span></span>

     ![Dispositivo de origem desativado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="0feeb-144">Selecione Olá desativado dispositivo, com o botão direito e selecione **excluir**.</span><span class="sxs-lookup"><span data-stu-id="0feeb-144">Select hello deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="0feeb-145">Isso exclui o dispositivo Olá da lista de saudação de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="0feeb-145">This deletes hello device from hello list of devices.</span></span>

    ![Dispositivo de origem excluído](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="0feeb-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0feeb-147">Next steps</span></span>

* <span data-ttu-id="0feeb-148">Depois de executar um failover, talvez seja necessário muito[desativar ou excluir seu dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="0feeb-148">After you have performed a failover, you may need too[deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="0feeb-149">Para obter informações sobre como toouse Olá Gerenciador de dispositivos de StorSimple de serviço, visite muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="0feeb-149">For information about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

