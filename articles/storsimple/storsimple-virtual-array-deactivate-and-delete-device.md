---
title: aaaDeactivate e excluir uma matriz do Microsoft Azure StorSimple Virtual | Microsoft Docs
description: "Descreve como o dispositivo StorSimple tooremove do serviço primeiro desativá-lo e, em seguida, excluí-lo."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: a929f5bc-03e2-4b01-b925-973db236f19f
ms.service: storsimple
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 11/21/2016
ms.author: alkohli
ms.openlocfilehash: b1f3ddb5822d19965739777e238af19b507df984
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="deactivate-and-delete-a-storsimple-virtual-array"></a><span data-ttu-id="9e2c9-103">Desativar e excluir uma Matriz Virtual StorSimple</span><span class="sxs-lookup"><span data-stu-id="9e2c9-103">Deactivate and delete a StorSimple Virtual Array</span></span>

## <a name="overview"></a><span data-ttu-id="9e2c9-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="9e2c9-104">Overview</span></span>

<span data-ttu-id="9e2c9-105">Quando você desativa uma matriz Virtual StorSimple, você interromper a conexão de saudação entre Olá dispositivo e o serviço de Gerenciador de dispositivos do StorSimple correspondente Olá.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-105">When you deactivate a StorSimple Virtual Array, you break hello connection between hello device and hello corresponding StorSimple Device Manager service.</span></span> <span data-ttu-id="9e2c9-106">Este tutorial explica como:</span><span class="sxs-lookup"><span data-stu-id="9e2c9-106">This tutorial explains how to:</span></span>

* <span data-ttu-id="9e2c9-107">Desativar um dispositivo</span><span class="sxs-lookup"><span data-stu-id="9e2c9-107">Deactivate a device</span></span> 
* <span data-ttu-id="9e2c9-108">Excluir um dispositivo desativado</span><span class="sxs-lookup"><span data-stu-id="9e2c9-108">Delete a deactivated device</span></span>

<span data-ttu-id="9e2c9-109">informações de Olá neste artigo aplicam-se somente a matrizes Virtual tooStorSimple.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-109">hello information in this article applies tooStorSimple Virtual Arrays only.</span></span> <span data-ttu-id="9e2c9-110">Para obter informações sobre a 8000 série, vá toohow muito[desativar ou excluir um dispositivo](storsimple-deactivate-and-delete-device.md).</span><span class="sxs-lookup"><span data-stu-id="9e2c9-110">For information on 8000 series, go toohow too[deactivate or delete a device](storsimple-deactivate-and-delete-device.md).</span></span>

## <a name="when-toodeactivate"></a><span data-ttu-id="9e2c9-111">Quando toodeactivate?</span><span class="sxs-lookup"><span data-stu-id="9e2c9-111">When toodeactivate?</span></span>

<span data-ttu-id="9e2c9-112">A desativação é uma operação PERMANENTE e não pode ser desfeita.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-112">Deactivation is a PERMANENT operation and cannot be undone.</span></span> <span data-ttu-id="9e2c9-113">Você não pode registrar um dispositivo desativado com hello serviço do Gerenciador de dispositivos de StorSimple novamente.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-113">You cannot register a deactivated device with hello StorSimple Device Manager service again.</span></span> <span data-ttu-id="9e2c9-114">Você pode precisar toodeactivate e excluir uma matriz Virtual do StorSimple no hello os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="9e2c9-114">You may need toodeactivate and delete a StorSimple Virtual Array in hello following scenarios:</span></span>

* <span data-ttu-id="9e2c9-115">**Failover planejado** : seu dispositivo está online e planejar toofail em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-115">**Planned failover** : Your device is online and you plan toofail over your device.</span></span> <span data-ttu-id="9e2c9-116">Se você estiver planejando tooupgrade tooa maior do dispositivo, talvez seja necessário toofail em seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-116">If you are planning tooupgrade tooa larger device, you may need toofail over your device.</span></span> <span data-ttu-id="9e2c9-117">Depois que propriedade Olá dos dados é transferida e Olá failover estiver concluído, o dispositivo de origem Olá é excluído automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-117">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="9e2c9-118">**Failover não planejado** : seu dispositivo está offline e precisar de toofail dispositivo hello.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-118">**Unplanned failover** : Your device is offline and you need toofail over hello device.</span></span> <span data-ttu-id="9e2c9-119">Esta situação pode ocorrer durante um desastre quando houver uma interrupção no datacenter hello e seu dispositivo primário está inativo.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-119">This scenario may occur during a disaster when there is an outage in hello datacenter and your primary device is down.</span></span> <span data-ttu-id="9e2c9-120">Planejar toofail sobre Olá dispositivo tooa secundário dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-120">You plan toofail over hello device tooa secondary device.</span></span> <span data-ttu-id="9e2c9-121">Depois que propriedade Olá dos dados é transferida e Olá failover estiver concluído, o dispositivo de origem Olá é excluído automaticamente.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-121">After hello data ownership is transferred and hello failover is complete, hello source device is automatically deleted.</span></span>
* <span data-ttu-id="9e2c9-122">**Encerrar** : toodecommission Olá dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-122">**Decommission** : You want toodecommission hello device.</span></span> <span data-ttu-id="9e2c9-123">Isso exige que você toofirst desativar dispositivo hello e, em seguida, excluí-lo.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-123">This requires you toofirst deactivate hello device and then delete it.</span></span> <span data-ttu-id="9e2c9-124">Ao desativar um dispositivo, não é mais possível acessar os dados que foram armazenados localmente.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-124">When you deactivate a device, you can no longer access any data that is stored locally.</span></span> <span data-ttu-id="9e2c9-125">Você pode apenas acesso e recupere Olá os dados armazenados na nuvem hello.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-125">You can only access and recover hello data stored in hello cloud.</span></span> <span data-ttu-id="9e2c9-126">Se você planejar os dados do dispositivo Olá tookeep após a desativação, você deve executar um instantâneo de nuvem de todos os dados antes de desativar um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-126">If you plan tookeep hello device data after deactivation, then you should take a cloud snapshot of all your data before you deactivate a device.</span></span> <span data-ttu-id="9e2c9-127">Esse instantâneo de nuvem permite que você toorecover todos Olá dados em um estágio posterior.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-127">This cloud snapshot allows you toorecover all hello data at a later stage.</span></span>

## <a name="deactivate-a-device"></a><span data-ttu-id="9e2c9-128">Desativar um dispositivo</span><span class="sxs-lookup"><span data-stu-id="9e2c9-128">Deactivate a device</span></span>

<span data-ttu-id="9e2c9-129">toodeactivate seu dispositivo, execute Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-129">toodeactivate your device, perform hello following steps.</span></span>

#### <a name="toodeactivate-hello-device"></a><span data-ttu-id="9e2c9-130">dispositivo de saudação toodeactivate</span><span class="sxs-lookup"><span data-stu-id="9e2c9-130">toodeactivate hello device</span></span>

1. <span data-ttu-id="9e2c9-131">No seu serviço, vá muito**gerenciamento > dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-131">In your service, go too**Management > Devices**.</span></span> <span data-ttu-id="9e2c9-132">Em Olá **dispositivos** folha, clique em e dispositivo Olá selecione que você deseja toodeactivate.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-132">In hello **Devices** blade, click and select hello device that you wish toodeactivate.</span></span>
   
    ![Selecione o dispositivo toodeactivate](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete7.png)
2. <span data-ttu-id="9e2c9-134">No seu **painel dispositivo** folha, clique em **... Mais** e selecione lista de saudação **desativar**.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-134">In your **Device dashboard** blade, click **… More** and from hello list, select **Deactivate**.</span></span>
   
    ![Clique em desativar](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete8.png)
3. <span data-ttu-id="9e2c9-136">Em Olá **desativar** folha, nome do tipo de dispositivo hello e clique **desativar**.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-136">In hello **Deactivate** blade, type hello device name and then click **Deactivate**.</span></span> 
   
    ![Confirme desativar](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete1.png)
   
    <span data-ttu-id="9e2c9-138">Olá desativar o início do processo e leva toocomplete de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-138">hello deactivate process starts and takes a few minutes toocomplete.</span></span>
   
    ![Desativação em andamento](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete2.png)
4. <span data-ttu-id="9e2c9-140">Após a desativação Olá lista de atualizações de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-140">After deactivation, hello list of devices refreshes.</span></span>
   
    ![Desativação concluída](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete3.png)
   
    <span data-ttu-id="9e2c9-142">Agora você pode excluir este dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-142">You can now delete this device.</span></span>

## <a name="delete-hello-device"></a><span data-ttu-id="9e2c9-143">Excluir dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="9e2c9-143">Delete hello device</span></span>

<span data-ttu-id="9e2c9-144">Um dispositivo tem toodelete desativadas do primeiro toobe-lo.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-144">A device has toobe first deactivated toodelete it.</span></span> <span data-ttu-id="9e2c9-145">Excluir um dispositivo remove da lista de saudação de dispositivos conectados toohello serviço.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-145">Deleting a device removes it from hello list of devices connected toohello service.</span></span> <span data-ttu-id="9e2c9-146">serviço Hello, em seguida, não poderá mais gerenciar dispositivo Olá excluído.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-146">hello service can then no longer manage hello deleted device.</span></span> <span data-ttu-id="9e2c9-147">No entanto, dados de saudação associados ao dispositivo Olá permanecem na nuvem de saudação.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-147">hello data associated with hello device however remains in hello cloud.</span></span> <span data-ttu-id="9e2c9-148">Esses dados acumulam encargos.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-148">This data then accrues charges.</span></span>

<span data-ttu-id="9e2c9-149">dispositivo de saudação toodelete, executar Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-149">toodelete hello device, perform hello following steps.</span></span>

#### <a name="toodelete-hello-device"></a><span data-ttu-id="9e2c9-150">dispositivo de saudação toodelete</span><span class="sxs-lookup"><span data-stu-id="9e2c9-150">toodelete hello device</span></span>

1. <span data-ttu-id="9e2c9-151">No Gerenciador de dispositivos seu StorSimple, ir muito**gerenciamento > dispositivos**.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-151">In your StorSimple Device Manager, go too**Management > Devices**.</span></span> <span data-ttu-id="9e2c9-152">Em Olá **dispositivos** folha, selecione um dispositivo desativado que você deseja toodelete.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-152">In hello **Devices** blade, select a deactivated device that you wish toodelete.</span></span>
2. <span data-ttu-id="9e2c9-153">Em Olá **painel dispositivo** folha, clique em **... Mais** e, em seguida, clique em **excluir**.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-153">In hello **Device dashboard** blade, click **… More** and then click **Delete**.</span></span>
   
   ![Selecione o dispositivo toodelete](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete4.png)
3. <span data-ttu-id="9e2c9-155">Em Olá **excluir** folha, digite o nome de saudação de sua exclusão do dispositivo tooconfirm hello e clique **excluir**.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-155">In hello **Delete** blade, type hello name of your device tooconfirm hello deletion and then click **Delete**.</span></span> <span data-ttu-id="9e2c9-156">Excluindo dispositivos de saudação não exclui dados de nuvem Olá associados Olá dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-156">Deleting hello device does not delete hello cloud data associated with hello device.</span></span> 
   
   ![Confirmar exclusão](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete5.png) 
4. <span data-ttu-id="9e2c9-158">exclusão de saudação é iniciado e leva toocomplete de alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-158">hello deletion starts and takes a few minutes toocomplete.</span></span>
   
   ![Exclusão em andamento](./media/storsimple-virtual-array-deactivate-and-delete-device/deactivate-delete6.png)
   
    <span data-ttu-id="9e2c9-160">Depois que o dispositivo de saudação é excluído, você pode exibir a lista de saudação atualizada de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="9e2c9-160">After hello device is deleted, you can view hello updated list of devices.</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e2c9-161">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e2c9-161">Next steps</span></span>

* <span data-ttu-id="9e2c9-162">Para obter informações sobre como toofail, ir muito[Failover e recuperação de desastres de sua matriz Virtual StorSimple](storsimple-virtual-array-failover-dr.md).</span><span class="sxs-lookup"><span data-stu-id="9e2c9-162">For information on how toofail over, go too[Failover and disaster recovery of your StorSimple Virtual Array](storsimple-virtual-array-failover-dr.md).</span></span>

* <span data-ttu-id="9e2c9-163">toolearn mais sobre como Olá toouse serviço do Gerenciador de dispositivos de StorSimple, ir muito[Use Olá tooadminister de serviço do Gerenciador de dispositivos de StorSimple sua matriz Virtual StorSimple](storsimple-virtual-array-manager-service-administration.md).</span><span class="sxs-lookup"><span data-stu-id="9e2c9-163">toolearn more about how toouse hello StorSimple Device Manager service, go too[Use hello StorSimple Device Manager service tooadminister your StorSimple Virtual Array](storsimple-virtual-array-manager-service-administration.md).</span></span> 

