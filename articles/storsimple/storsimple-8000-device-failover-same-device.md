---
title: "Failover e recuperação de desastre do StorSimple para dispositivos da série 8000 | Microsoft Docs"
description: Saiba como fazer failover de seu dispositivo StorSimple para o mesmo dispositivo.
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
ms.openlocfilehash: acc8929dc3476e9590e8e4d9526b38b7c0719570
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-your-storsimple-physical-device-to-same-device"></a><span data-ttu-id="ae029-103">Fazer failover de seu dispositivo físico StorSimple para o próprio dispositivo</span><span class="sxs-lookup"><span data-stu-id="ae029-103">Fail over your StorSimple physical device to same device</span></span>

## <a name="overview"></a><span data-ttu-id="ae029-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="ae029-104">Overview</span></span>

<span data-ttu-id="ae029-105">Este tutorial descreve as etapas necessárias para fazer failover de um dispositivo StorSimple da série 8000 para o próprio dispositivo em caso de desastre.</span><span class="sxs-lookup"><span data-stu-id="ae029-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to itself if there is a disaster.</span></span> <span data-ttu-id="ae029-106">O StorSimple usa o recurso de failover de dispositivo para migrar os dados de um dispositivo de origem físico no datacenter para outro dispositivo físico.</span><span class="sxs-lookup"><span data-stu-id="ae029-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to another physical device.</span></span> <span data-ttu-id="ae029-107">As diretrizes neste tutorial se aplicam a dispositivos físicos StorSimple da série 8000 que executam versões de software com Atualização 3 e posterior.</span><span class="sxs-lookup"><span data-stu-id="ae029-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices running software versions Update 3 and later.</span></span>

<span data-ttu-id="ae029-108">Para saber mais sobre o failover de dispositivo e como ele é usado para recuperação de um desastre, acesse [Failover e recuperação de desastre para dispositivos StorSimple da série 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="ae029-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="ae029-109">Para fazer failover de um dispositivo físico para outro, acesse [Fazer failover para o mesmo dispositivo físico StorSimple](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="ae029-109">To fail over a physical device to another physical device, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="ae029-110">Para fazer failover de um dispositivo físico StorSimple para um Dispositivo de Nuvem StorSimple, acesse [Fazer failover para um Dispositivo de Nuvem StorSimple](storsimple-8000-device-failover-cloud-appliance.md).</span><span class="sxs-lookup"><span data-stu-id="ae029-110">To fail over a StorSimple physical device to a StorSimple Cloud Appliance, go to [Fail over to a StorSimple Cloud Appliance](storsimple-8000-device-failover-cloud-appliance.md).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="ae029-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ae029-111">Prerequisites</span></span>

- <span data-ttu-id="ae029-112">Não deixe de revisar as considerações de failover de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ae029-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="ae029-113">Para obter mais informações, acesse [Considerações comuns para failover de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="ae029-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>


## <a name="steps-to-fail-over-to-the-same-device"></a><span data-ttu-id="ae029-114">Etapas para fazer failover para o mesmo dispositivo</span><span class="sxs-lookup"><span data-stu-id="ae029-114">Steps to fail over to the same device</span></span>

<span data-ttu-id="ae029-115">Execute as etapas a seguir se precisar fazer failover para o mesmo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ae029-115">Perform the following steps if you need to fail over to the same device.</span></span>

1. <span data-ttu-id="ae029-116">Tirar instantâneos de nuvem de todos os volumes em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ae029-116">Take cloud snapshots of all the volumes in your device.</span></span> <span data-ttu-id="ae029-117">Para saber mais, acesse [Usar o serviço do Gerenciador de Dispositivos do StorSimple para criar backups](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="ae029-117">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="ae029-118">Redefina o dispositivo para os padrões de fábrica.</span><span class="sxs-lookup"><span data-stu-id="ae029-118">Reset your device to factory defaults.</span></span> <span data-ttu-id="ae029-119">Siga as instruções detalhadas em [como redefinir um dispositivo StorSimple para as configurações padrões de fábrica](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span><span class="sxs-lookup"><span data-stu-id="ae029-119">Follow the detailed instructions in [how to reset a StorSimple device to factory default settings](storsimple-8000-manage-device-controller.md#reset-the-device-to-factory-default-settings).</span></span>
3. <span data-ttu-id="ae029-120">Acesse o serviço do Gerenciador de Dispositivos do StorSimple Device e clique em **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="ae029-120">Go to the StorSimple Device Manager service and then select **Devices**.</span></span> <span data-ttu-id="ae029-121">Na folha **Dispositivos**, o antigo dispositivo deverá aparecer como **Offline**.</span><span class="sxs-lookup"><span data-stu-id="ae029-121">In the **Devices** blade, the old device should show as **Offline**.</span></span>

    ![Dispositivo de origem offline](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev2.png)

4. <span data-ttu-id="ae029-123">Configure o seu dispositivo e registre-o novamente no serviço do Gerenciador de Dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="ae029-123">Configure your device and register it again with your StorSimple Device Manager service.</span></span> <span data-ttu-id="ae029-124">Os dispositivos recém-registrados devem aparecer como **Pronto para ser configurado**.</span><span class="sxs-lookup"><span data-stu-id="ae029-124">The newly registered device should show as **Ready to set up**.</span></span> <span data-ttu-id="ae029-125">O nome do novo dispositivo é o mesmo que o do dispositivo antigo, porém acrescido com um número para indicar que o dispositivo foi redefinido para o padrão de fábrica e registrado novamente.</span><span class="sxs-lookup"><span data-stu-id="ae029-125">The device name for the new device is the same as the old device but appended with a numeral to indicate that the device was reset to factory default and registered again.</span></span>

    ![Dispositivo recém-registrado pronto para ser configurado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev3.png)
5. <span data-ttu-id="ae029-127">Conclua a configuração do novo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ae029-127">For the new device, complete the device setup.</span></span> <span data-ttu-id="ae029-128">Para obter mais informações, acesse [Etapa 4: concluir a configuração mínima de dispositivo](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span><span class="sxs-lookup"><span data-stu-id="ae029-128">For more information, go to [Step 4: Complete minimum device setup](storsimple-8000-deployment-walkthrough-u2.md#step-4-complete-minimum-device-setup).</span></span> <span data-ttu-id="ae029-129">Na folha **Dispositivos**, o status do dispositivo muda para **Online**.</span><span class="sxs-lookup"><span data-stu-id="ae029-129">On the **Devices** blade, the status of the device changes to **Online**.</span></span>

   > [!IMPORTANT]
   > <span data-ttu-id="ae029-130">**Conclua primeiramente a configuração mínima, caso contrário a recuperação de desastre pode falhar.**</span><span class="sxs-lookup"><span data-stu-id="ae029-130">**Complete the minimum configuration first, or your DR may fail.**</span></span>

    ![Dispositivo recém-registrado online](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev7.png)

6. <span data-ttu-id="ae029-132">Selecione o dispositivo antigo (status offline) e, na barra de comandos, clique em **Fazer failover**.</span><span class="sxs-lookup"><span data-stu-id="ae029-132">Select the old device (status offline) and from the command bar, click **Fail over**.</span></span> <span data-ttu-id="ae029-133">Na folha **Fazer failover**, selecione o dispositivo antigo como a origem e especifique o dispositivo de destino como o dispositivo recém-registrado.</span><span class="sxs-lookup"><span data-stu-id="ae029-133">In the **Fail over** blade, select old device as the source and specify the target device as the newly registered device.</span></span>

    ![Resumo de failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev11.png)

    <span data-ttu-id="ae029-135">Para obter instruções detalhadas, consulte [Failover para outro dispositivo físico](#fail-over-to-another-physical-device).</span><span class="sxs-lookup"><span data-stu-id="ae029-135">For detailed instructions, refer to [Fail over to another physical device](#fail-over-to-another-physical-device).</span></span>

7. <span data-ttu-id="ae029-136">É criado um trabalho de restauração de dispositivo para que você possa monitorar na folha **Trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="ae029-136">A device restore job is created that you can monitor from the **Jobs** blade.</span></span>

8. <span data-ttu-id="ae029-137">Depois que o trabalho for concluído com êxito, acesse o novo dispositivo e navegue para a folha **Contêineres de volume**.</span><span class="sxs-lookup"><span data-stu-id="ae029-137">After the job has successfully completed, access the new device and navigate to the **Volume containers** blade.</span></span> <span data-ttu-id="ae029-138">Verifique se todos os contêineres de volume do antigo dispositivo foram migrados para o novo dispositivo.</span><span class="sxs-lookup"><span data-stu-id="ae029-138">Verify that all the volume containers from the old device have migrated to the new device.</span></span>

   ![Contêineres de volume migrados](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev13.png)

9. <span data-ttu-id="ae029-140">Após a conclusão do failover, você pode desativar e excluir o antigo dispositivo do portal.</span><span class="sxs-lookup"><span data-stu-id="ae029-140">After the failover is complete, you can deactivate and delete the old device from the portal.</span></span> <span data-ttu-id="ae029-141">Selecione o antigo dispositivo (offline), clique com o botão direito do mouse e selecione **Desativar**.</span><span class="sxs-lookup"><span data-stu-id="ae029-141">Select the old device (offline), right-click, and then select **Deactivate**.</span></span> <span data-ttu-id="ae029-142">Depois que o dispositivo for desativado, seu status será atualizado.</span><span class="sxs-lookup"><span data-stu-id="ae029-142">After the device is deactivated, the status of the device is updated.</span></span>

     ![Dispositivo de origem desativado](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev14.png)

10. <span data-ttu-id="ae029-144">Selecione o dispositivo desativado, clique com o botão direito do mouse e selecione **Excluir**.</span><span class="sxs-lookup"><span data-stu-id="ae029-144">Select the deactivated device, right-click, and then select **Delete**.</span></span> <span data-ttu-id="ae029-145">Isso exclui o dispositivo da lista de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="ae029-145">This deletes the device from the list of devices.</span></span>

    ![Dispositivo de origem excluído](./media/storsimple-8000-device-failover-disaster-recovery/failover-single-dev15.png)



## <a name="next-steps"></a><span data-ttu-id="ae029-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ae029-147">Next steps</span></span>

* <span data-ttu-id="ae029-148">Depois de realizar um failover, talvez seja necessário [desativar ou excluir seu dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="ae029-148">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>
* <span data-ttu-id="ae029-149">Para obter informações sobre como usar o serviço do Gerenciador de Dispositivos do StorSimple, acesse [Usar o serviço do Gerenciador de Dispositivos do StorSimple para administrar seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="ae029-149">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

