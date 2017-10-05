---
title: "Failover do StorSimple e recuperação de desastre para um Dispositivo de Nuvem StorSimple | Microsoft Docs"
description: "Saiba como fazer o failover do seu dispositivo físico StorSimple da série 8000 para um dispositivo de nuvem."
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
ms.openlocfilehash: ec8bebf2854e84a37e84b45564e80fc20b63d8d8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="fail-over-to-your-storsimple-cloud-appliance"></a><span data-ttu-id="cffe6-103">Fazer failover para um Dispositivo de Nuvem StorSimple</span><span class="sxs-lookup"><span data-stu-id="cffe6-103">Fail over to your StorSimple Cloud Appliance</span></span>

## <a name="overview"></a><span data-ttu-id="cffe6-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="cffe6-104">Overview</span></span>

<span data-ttu-id="cffe6-105">Este tutorial descreve as etapas necessárias para fazer failover de um dispositivo físico StorSimple da série 8000 para um Dispositivo de Nuvem StorSimple em caso de desastre.</span><span class="sxs-lookup"><span data-stu-id="cffe6-105">This tutorial describes the steps required to fail over a StorSimple 8000 series physical device to a StorSimple Cloud Appliance if there is a disaster.</span></span> <span data-ttu-id="cffe6-106">O StorSimple usa o recurso de failover de dispositivo para migrar os dados de um dispositivo de origem físico no datacenter para um dispositivo de nuvem em execução no Azure.</span><span class="sxs-lookup"><span data-stu-id="cffe6-106">StorSimple uses the device failover feature to migrate data from a source physical device in the datacenter to a cloud appliance running in Azure.</span></span> <span data-ttu-id="cffe6-107">As diretrizes neste tutorial se aplicam a dispositivos físicos StorSimple da série 8000 e a dispositivos de nuvem que executam versões de software com a Atualização 3 e posterior.</span><span class="sxs-lookup"><span data-stu-id="cffe6-107">The guidance in this tutorial applies to StorSimple 8000 series physical devices and cloud appliances running software versions Update 3 and later.</span></span>

<span data-ttu-id="cffe6-108">Para saber mais sobre o failover de dispositivo e como ele é usado para recuperação de um desastre, acesse [Failover e recuperação de desastre para dispositivos StorSimple da série 8000](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-108">To learn more about device failover and how it is used to recover from a disaster, go to [Failover and disaster recovery for StorSimple 8000 series devices](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

<span data-ttu-id="cffe6-109">Para fazer failover de um dispositivo físico StorSimple para outro, acesse [Fazer failover para um dispositivo físico StorSimple](storsimple-8000-device-failover-physical-device.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-109">To fail over a StorSimple physical device to another physical device, go to [Fail over to a StorSimple physical device](storsimple-8000-device-failover-physical-device.md).</span></span> <span data-ttu-id="cffe6-110">Para fazer failover de um dispositivo para ele mesmo, acesse [Fazer failover para o mesmo dispositivo físico StorSimple](storsimple-8000-device-failover-same-device.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-110">To fail over a device to itself, go to [Fail over to the same StorSimple physical device](storsimple-8000-device-failover-same-device.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="cffe6-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="cffe6-111">Prerequisites</span></span>

- <span data-ttu-id="cffe6-112">Não deixe de revisar as considerações de failover de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cffe6-112">Ensure that you have reviewed the considerations for device failover.</span></span> <span data-ttu-id="cffe6-113">Para obter mais informações, acesse [Considerações comuns para failover de dispositivo](storsimple-8000-device-failover-disaster-recovery.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-113">For more information, go to [Common considerations for device failover](storsimple-8000-device-failover-disaster-recovery.md).</span></span>

- <span data-ttu-id="cffe6-114">Você deve ter um Dispositivo de Nuvem StorSimple criado e configurado antes de executar este procedimento.</span><span class="sxs-lookup"><span data-stu-id="cffe6-114">You must have a StorSimple Cloud Appliance created and configured before running this procedure.</span></span> <span data-ttu-id="cffe6-115">Se estiver executando a versão de software com a Atualização 3 ou posterior, considere usar um dispositivo de nuvem 8020 para a recuperação de desastre.</span><span class="sxs-lookup"><span data-stu-id="cffe6-115">If running   Update 3 software version or later, consider using an 8020 cloud appliance for the DR.</span></span> <span data-ttu-id="cffe6-116">O modelo 8020 tem 64 TB e usa o Armazenamento Premium.</span><span class="sxs-lookup"><span data-stu-id="cffe6-116">The 8020 model has 64 TB and uses Premium Storage.</span></span> <span data-ttu-id="cffe6-117">Para obter mais informações, acesse [Implantar e gerenciar um Dispositivo de Nuvem StorSimple](storsimple-8000-cloud-appliance-u2.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-117">For more information, go to [Deploy and manage a StorSimple Cloud Appliance](storsimple-8000-cloud-appliance-u2.md).</span></span>

## <a name="steps-to-fail-over-to-a-cloud-appliance"></a><span data-ttu-id="cffe6-118">Etapas para fazer failover para um dispositivo de nuvem</span><span class="sxs-lookup"><span data-stu-id="cffe6-118">Steps to fail over to a cloud appliance</span></span>

<span data-ttu-id="cffe6-119">Execute as etapas a seguir para restaurar o dispositivo para um Dispositivo de Nuvem StorSimple de destino.</span><span class="sxs-lookup"><span data-stu-id="cffe6-119">Perform the following steps to restore the device to a target StorSimple Cloud Appliance.</span></span>

1.  <span data-ttu-id="cffe6-120">Verifique se o contêiner de volume para o qual você deseja fazer o failover associou instantâneos de nuvem.</span><span class="sxs-lookup"><span data-stu-id="cffe6-120">Verify that the volume container you want to fail over has associated cloud snapshots.</span></span> <span data-ttu-id="cffe6-121">Para saber mais, acesse [Usar o serviço do Gerenciador de Dispositivos do StorSimple para criar backups](storsimple-8000-manage-backup-policies-u2.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-121">For more information, go to [Use StorSimple Device Manager service to create backups](storsimple-8000-manage-backup-policies-u2.md).</span></span>
2. <span data-ttu-id="cffe6-122">Acesse o serviço Gerenciador de Dispositivo StorSimple e clique em **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="cffe6-122">Go to your StorSimple Device Manager service and click **Devices**.</span></span> <span data-ttu-id="cffe6-123">Na folha **Dispositivos**, vá até a lista de dispositivos conectados ao seu serviço.</span><span class="sxs-lookup"><span data-stu-id="cffe6-123">In the **Devices** blade, go to the list of devices connected with your service.</span></span>
    <span data-ttu-id="cffe6-124">![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span><span class="sxs-lookup"><span data-stu-id="cffe6-124">![Select device](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev1.png)</span></span>
3. <span data-ttu-id="cffe6-125">Selecione e clique no dispositivo de origem.</span><span class="sxs-lookup"><span data-stu-id="cffe6-125">Select and click your source device.</span></span> <span data-ttu-id="cffe6-126">O dispositivo de origem tem os contêineres de volume para os quais você deseja fazer failover.</span><span class="sxs-lookup"><span data-stu-id="cffe6-126">The source device has the volume containers that you want to fail over.</span></span> <span data-ttu-id="cffe6-127">Acesse **Configurações > Contêineres de Volume**.</span><span class="sxs-lookup"><span data-stu-id="cffe6-127">Go to **Settings > Volume Containers**.</span></span>

    ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev2.png)
    
4. <span data-ttu-id="cffe6-129">Selecione um contêiner de volume para o qual você gostaria de fazer failover para outro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cffe6-129">Select a volume container that you would like to fail over to another device.</span></span> <span data-ttu-id="cffe6-130">Clique no contêiner de volume para exibir a lista de volumes neste contêiner.</span><span class="sxs-lookup"><span data-stu-id="cffe6-130">Click the volume container to display the list of volumes within this container.</span></span> <span data-ttu-id="cffe6-131">Selecione um volume, clique com o botão direito em **Deixar Offline** para deixar o volume offline.</span><span class="sxs-lookup"><span data-stu-id="cffe6-131">Select a volume, right-click, and click **Take Offline** to take the volume offline.</span></span>

    ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev5.png)

5. <span data-ttu-id="cffe6-133">Repita esse processo para todos os volumes no contêiner de volume.</span><span class="sxs-lookup"><span data-stu-id="cffe6-133">Repeat this process for all the volumes in the volume container.</span></span>

     ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev7.png)

6. <span data-ttu-id="cffe6-135">Repita a etapa anterior para todos os contêineres de volume para os quais você gostaria de fazer o failover para outro dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cffe6-135">Repeat the previous step for all the volume containers you would like to fail over to another device.</span></span>

7. <span data-ttu-id="cffe6-136">Retorne para a folha **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="cffe6-136">Go back to the **Devices** blade.</span></span> <span data-ttu-id="cffe6-137">Na barra de comandos, clique em **Fazer failover**.</span><span class="sxs-lookup"><span data-stu-id="cffe6-137">From the command bar, click **Fail over**.</span></span>

    ![Clique em Fazer failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev8.png)
8. <span data-ttu-id="cffe6-139">Na folha **Fazer failover**, execute as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="cffe6-139">In the **Fail over** blade, perform the following steps:</span></span>
   
    1. <span data-ttu-id="cffe6-140">Clique em **Fonte**.</span><span class="sxs-lookup"><span data-stu-id="cffe6-140">Click **Source**.</span></span> <span data-ttu-id="cffe6-141">Selecione os contêineres de volume que passarão por failover.</span><span class="sxs-lookup"><span data-stu-id="cffe6-141">Select the volume containers to fail over.</span></span> <span data-ttu-id="cffe6-142">**São exibidos apenas os contêineres de volume com instantâneos de nuvem e volumes offline associados.**</span><span class="sxs-lookup"><span data-stu-id="cffe6-142">**Only the volume containers with associated cloud snapshots and offline volumes are displayed.**</span></span>
        <span data-ttu-id="cffe6-143">![Selecionar fonte](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span><span class="sxs-lookup"><span data-stu-id="cffe6-143">![Select source](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev11.png)</span></span>
    2. <span data-ttu-id="cffe6-144">Clique em **Destino**.</span><span class="sxs-lookup"><span data-stu-id="cffe6-144">Click **Target**.</span></span> <span data-ttu-id="cffe6-145">Selecione um dispositivo de nuvem de destino na lista suspensa de dispositivos disponíveis.</span><span class="sxs-lookup"><span data-stu-id="cffe6-145">Select a target cloud appliance from the dropdown list of available devices.</span></span> <span data-ttu-id="cffe6-146">**Somente os dispositivos que têm capacidade suficiente para acomodar os contêineres de volume de origem são exibidos na lista.**</span><span class="sxs-lookup"><span data-stu-id="cffe6-146">**Only the devices that have sufficient capacity to accommodate source volume containers are displayed in the list.**</span></span>

        ![Selecionar o destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev12.png)

    3. <span data-ttu-id="cffe6-148">Revise as configurações de failover em **Resumo** e marque a caixa de seleção que indica se os volumes nos contêineres de volume selecionados estão offline.</span><span class="sxs-lookup"><span data-stu-id="cffe6-148">Review the failover settings under **Summary** and select the checkbox indicating that the volumes in selected volume containers are offline.</span></span> 

        ![Examinar as configurações de failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-cloud-dev13.png)

9. <span data-ttu-id="cffe6-150">Um trabalho de failover é criado.</span><span class="sxs-lookup"><span data-stu-id="cffe6-150">A failover job is created.</span></span> <span data-ttu-id="cffe6-151">Para monitorar o trabalho de failover, clique na notificação do trabalho.</span><span class="sxs-lookup"><span data-stu-id="cffe6-151">To monitor the failover job, click the job notification.</span></span>

    ![Monitorar o trabalho de failover](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev13.png)

10. <span data-ttu-id="cffe6-153">Após a conclusão do failover, volte para a folha **Dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="cffe6-153">After the failover is completed, go back to the **Devices** blade.</span></span>

    1. <span data-ttu-id="cffe6-154">Selecione o dispositivo que foi usado como destino para o failover.</span><span class="sxs-lookup"><span data-stu-id="cffe6-154">Select the device that was used as the target for the failover.</span></span>

       ![Selecionar dispositivo](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev14.png)

    2. <span data-ttu-id="cffe6-156">Clique em **Contêineres de Volume**.</span><span class="sxs-lookup"><span data-stu-id="cffe6-156">Click **Volume Containers**.</span></span> <span data-ttu-id="cffe6-157">Todos os contêineres de volume, juntamente com os volumes do antigo dispositivo devem ser listados.</span><span class="sxs-lookup"><span data-stu-id="cffe6-157">All the volume containers, along with the volumes from the old device, should be listed.</span></span>

       <span data-ttu-id="cffe6-158">Se o contêiner de volume que passou por failover tem volumes fixados localmente, tais volumes passam por failover como volumes em camadas.</span><span class="sxs-lookup"><span data-stu-id="cffe6-158">If the volume container that you failed over has locally pinned volumes, those volumes are failed over as tiered volumes.</span></span> <span data-ttu-id="cffe6-159">Não há suporte para volumes fixados localmente em um Dispositivo de Nuvem StorSimple.</span><span class="sxs-lookup"><span data-stu-id="cffe6-159">Locally pinned volumes are not supported on a StorSimple Cloud Appliance.</span></span>

       ![Exibir contêineres de volume de destino](./media/storsimple-8000-device-failover-disaster-recovery/failover-phy-dev17.png)


## <a name="next-steps"></a><span data-ttu-id="cffe6-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cffe6-161">Next steps</span></span>

* <span data-ttu-id="cffe6-162">Depois de realizar um failover, talvez seja necessário [desativar ou excluir seu dispositivo StorSimple](storsimple-8000-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-162">After you have performed a failover, you may need to [deactivate or delete your StorSimple device](storsimple-8000-deactivate-and-delete-device.md).</span></span>

* <span data-ttu-id="cffe6-163">Para obter informações sobre como usar o serviço do Gerenciador de Dispositivos do StorSimple, acesse [Usar o serviço do Gerenciador de Dispositivos do StorSimple para administrar seu dispositivo StorSimple](storsimple-8000-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="cffe6-163">For information about how to use the StorSimple Device Manager service, go to [Use the StorSimple Device Manager service to administer your StorSimple device](storsimple-8000-manager-service-administration.md).</span></span>

