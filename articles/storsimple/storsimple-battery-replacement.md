---
title: Substituir a bateria em um dispositivo Microsoft Azure StorSimple | Microsoft Docs
description: "Descreve como remover, substituir e realizar manutenção no módulo de bateria de backup do dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 3c8a6654-4826-4883-aad8-75f332347c53
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/17/2016
ms.author: alkohli
ms.openlocfilehash: f8b89b3f6851ec9ee0570f551b5407419fdba2d6
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-the-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="8269d-103">Substitua o módulo de bateria de backup no dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="8269d-103">Replace the backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="8269d-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="8269d-104">Overview</span></span>
<span data-ttu-id="8269d-105">O módulo de energia e refrigeração (PCM) do compartimento primário no dispositivo Microsoft Azure StorSimple tem um pacote de bateria adicional.</span><span class="sxs-lookup"><span data-stu-id="8269d-105">The primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="8269d-106">Esse pacote fornece energia para que o dispositivo StorSimple possa salvar dados caso haja perda de energia CA no compartimento primário.</span><span class="sxs-lookup"><span data-stu-id="8269d-106">This pack provides power so that the StorSimple device can save data if there is loss of AC power to the primary enclosure.</span></span> <span data-ttu-id="8269d-107">Esse pacote de bateria é conhecido como *módulo de bateria de backup*.</span><span class="sxs-lookup"><span data-stu-id="8269d-107">This battery pack is referred to as the *backup battery module*.</span></span> <span data-ttu-id="8269d-108">O módulo de bateria de backup existe somente para o compartimento primário em seu dispositivo StorSimple (o compartimento EBOD não contém um módulo de bateria de backup).</span><span class="sxs-lookup"><span data-stu-id="8269d-108">The backup battery module exists only for the primary enclosure in your StorSimple device (the EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="8269d-109">Este tutorial explica como:</span><span class="sxs-lookup"><span data-stu-id="8269d-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="8269d-110">Remover o módulo de bateria de backup</span><span class="sxs-lookup"><span data-stu-id="8269d-110">Remove the backup battery module</span></span> 
* <span data-ttu-id="8269d-111">Instalar um novo módulo de bateria de backup</span><span class="sxs-lookup"><span data-stu-id="8269d-111">Install a new backup battery module</span></span>
* <span data-ttu-id="8269d-112">Realizar manutenção no módulo de bateria de backup</span><span class="sxs-lookup"><span data-stu-id="8269d-112">Maintain the backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8269d-113">Antes de remover e de substituir um módulo de bateria de backup, examine as informações de segurança em [Introdução à substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="8269d-113">Before removing and replacing a backup battery module, review the safety information in the [Introduction to StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-the-backup-battery-module"></a><span data-ttu-id="8269d-114">Remover o módulo de bateria de backup</span><span class="sxs-lookup"><span data-stu-id="8269d-114">Remove the backup battery module</span></span>
<span data-ttu-id="8269d-115">O módulo de bateria de backup de seu dispositivo StorSimple é uma unidade substituível no local.</span><span class="sxs-lookup"><span data-stu-id="8269d-115">The backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="8269d-116">Antes de ser instalado no PCM, o módulo de bateria deve ser armazenado em seu pacote original.</span><span class="sxs-lookup"><span data-stu-id="8269d-116">Before it is installed in the PCM, the battery module should be stored in its original packaging.</span></span> <span data-ttu-id="8269d-117">Execute as etapas a seguir para remover a bateria de backup.</span><span class="sxs-lookup"><span data-stu-id="8269d-117">Perform the following steps to remove the backup battery.</span></span>

#### <a name="to-remove-the-backup-battery-module"></a><span data-ttu-id="8269d-118">Para remover o módulo de bateria de backup</span><span class="sxs-lookup"><span data-stu-id="8269d-118">To remove the backup battery module</span></span>
1. <span data-ttu-id="8269d-119">No portal clássico do Azure, vá até **Dispositivos** > **Manutenção** > **Status de Hardware**.</span><span class="sxs-lookup"><span data-stu-id="8269d-119">In the Azure classic portal, go to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="8269d-120">Em **Componentes compartilhados**, observe o status da bateria.</span><span class="sxs-lookup"><span data-stu-id="8269d-120">Under **Shared Components**, look at the status of the battery.</span></span>
2. <span data-ttu-id="8269d-121">Identifique o PCM no qual a bateria falhou.</span><span class="sxs-lookup"><span data-stu-id="8269d-121">Identify the PCM in which the battery has failed.</span></span> <span data-ttu-id="8269d-122">A Figura 1 mostra a parte traseira do dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8269d-122">Figure 1 shows the back of the StorSimple device.</span></span>
   
    ![Backplane dos módulos do compartimento primário do dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="8269d-124">**Figura 1** Parte traseira do dispositivo primário mostrando os módulos de controlador e PCM</span><span class="sxs-lookup"><span data-stu-id="8269d-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="8269d-125">Rótulo</span><span class="sxs-lookup"><span data-stu-id="8269d-125">Label</span></span> | <span data-ttu-id="8269d-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="8269d-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="8269d-127">1</span><span class="sxs-lookup"><span data-stu-id="8269d-127">1</span></span> |<span data-ttu-id="8269d-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="8269d-128">PCM 0</span></span> |
   | <span data-ttu-id="8269d-129">2</span><span class="sxs-lookup"><span data-stu-id="8269d-129">2</span></span> |<span data-ttu-id="8269d-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="8269d-130">PCM 1</span></span> |
   | <span data-ttu-id="8269d-131">3</span><span class="sxs-lookup"><span data-stu-id="8269d-131">3</span></span> |<span data-ttu-id="8269d-132">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="8269d-132">Controller 0</span></span> |
   | <span data-ttu-id="8269d-133">4</span><span class="sxs-lookup"><span data-stu-id="8269d-133">4</span></span> |<span data-ttu-id="8269d-134">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="8269d-134">Controller 1</span></span> |
   
    <span data-ttu-id="8269d-135">Conforme mostrado pelo número 3 na Figura 2, o LED indicador de monitoramento no PCM 0 que corresponde à **Falha de bateria** deve estar aceso.</span><span class="sxs-lookup"><span data-stu-id="8269d-135">As shown by number 3 in the Figure 2, the monitoring indicator LED on PCM 0 that corresponds to **Battery Fault** should be lit.</span></span>
   
    ![Backplane dos LEDs indicadores de monitoramento de PCM do dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="8269d-137">**Figura 2** Parte traseira do PCM mostrando os LEDs indicadores de monitoramento</span><span class="sxs-lookup"><span data-stu-id="8269d-137">**Figure 2** Back of PCM showing the monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="8269d-138">Rótulo</span><span class="sxs-lookup"><span data-stu-id="8269d-138">Label</span></span> | <span data-ttu-id="8269d-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="8269d-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="8269d-140">1</span><span class="sxs-lookup"><span data-stu-id="8269d-140">1</span></span> |<span data-ttu-id="8269d-141">Falha de energia CA</span><span class="sxs-lookup"><span data-stu-id="8269d-141">AC power failure</span></span> |
   | <span data-ttu-id="8269d-142">2</span><span class="sxs-lookup"><span data-stu-id="8269d-142">2</span></span> |<span data-ttu-id="8269d-143">Falha do ventilador</span><span class="sxs-lookup"><span data-stu-id="8269d-143">Fan failure</span></span> |
   | <span data-ttu-id="8269d-144">3</span><span class="sxs-lookup"><span data-stu-id="8269d-144">3</span></span> |<span data-ttu-id="8269d-145">Falha de bateria</span><span class="sxs-lookup"><span data-stu-id="8269d-145">Battery fault</span></span> |
   | <span data-ttu-id="8269d-146">4</span><span class="sxs-lookup"><span data-stu-id="8269d-146">4</span></span> |<span data-ttu-id="8269d-147">PCM OK</span><span class="sxs-lookup"><span data-stu-id="8269d-147">PCM OK</span></span> |
   | <span data-ttu-id="8269d-148">5</span><span class="sxs-lookup"><span data-stu-id="8269d-148">5</span></span> |<span data-ttu-id="8269d-149">Falha de energia CC</span><span class="sxs-lookup"><span data-stu-id="8269d-149">DC power failure</span></span> |
   | <span data-ttu-id="8269d-150">6</span><span class="sxs-lookup"><span data-stu-id="8269d-150">6</span></span> |<span data-ttu-id="8269d-151">Bateria íntegra</span><span class="sxs-lookup"><span data-stu-id="8269d-151">Battery healthy</span></span> |
3. <span data-ttu-id="8269d-152">Para remover o PCM com uma bateria com falha, siga as etapas em [Remover um PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="8269d-152">To remove the PCM with a failed battery, follow the steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="8269d-153">Com o PCM removido, levante e gire a alça do módulo da bateria para cima, conforme indicado na figura a seguir, e puxe-a para remover a bateria.</span><span class="sxs-lookup"><span data-stu-id="8269d-153">With the PCM removed, lift and rotate the battery module handle upward as indicated in the following figure, and pull it up to remove the battery.</span></span>
   
    ![Removendo bateria do PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="8269d-155">**Figura 3** Remoção da bateria do PCM</span><span class="sxs-lookup"><span data-stu-id="8269d-155">**Figure 3** Removing the battery from the PCM</span></span>
5. <span data-ttu-id="8269d-156">Coloque o módulo na embalagem da unidade substituível no local.</span><span class="sxs-lookup"><span data-stu-id="8269d-156">Place the module in the field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="8269d-157">Devolva a unidade com defeito à Microsoft para que a manutenção e o manuseio adequados sejam realizados.</span><span class="sxs-lookup"><span data-stu-id="8269d-157">Return the defective unit to Microsoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="8269d-158">Instalar um novo módulo de bateria de backup</span><span class="sxs-lookup"><span data-stu-id="8269d-158">Install a new backup battery module</span></span>
<span data-ttu-id="8269d-159">Execute as etapas a seguir para instalar o módulo de bateria de reposição no PCM no compartimento primário do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="8269d-159">Perform the following steps to install the replacement battery module in the PCM in the primary enclosure of your StorSimple device.</span></span>

#### <a name="to-install-the-battery-module"></a><span data-ttu-id="8269d-160">Para instalar o módulo de bateria</span><span class="sxs-lookup"><span data-stu-id="8269d-160">To install the battery module</span></span>
1. <span data-ttu-id="8269d-161">Coloque o módulo de bateria de backup na direção correta no PCM.</span><span class="sxs-lookup"><span data-stu-id="8269d-161">Place the backup battery module in the proper orientation in the PCM.</span></span>
2. <span data-ttu-id="8269d-162">Pressione para baixo a alça do módulo da bateria até o conector no banco</span><span class="sxs-lookup"><span data-stu-id="8269d-162">Press down the battery module handle all the way to seat the connector.</span></span>
3. <span data-ttu-id="8269d-163">Substitua o PCM no compartimento primário, seguindo as orientações em [Substituir um módulo de energia e refrigeração no seu dispositivo StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="8269d-163">Replace the PCM in the primary enclosure by following the guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="8269d-164">Após a substituição ser concluída, vá até **Dispositivos** > **Manutenção** > **Status de Hardware** no portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="8269d-164">After the replacement is complete, go to **Devices** > **Maintenance** > **Hardware Status** in the Azure classic portal.</span></span> <span data-ttu-id="8269d-165">Verifique o status da bateria para se certificar de que a instalação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="8269d-165">Verify the status of the battery to make sure that the installation was successful.</span></span> <span data-ttu-id="8269d-166">Um status verde indica que a bateria está íntegra.</span><span class="sxs-lookup"><span data-stu-id="8269d-166">A green status indicates that the battery is healthy.</span></span>

## <a name="maintain-the-backup-battery-module"></a><span data-ttu-id="8269d-167">Realizar manutenção no módulo de bateria de backup</span><span class="sxs-lookup"><span data-stu-id="8269d-167">Maintain the backup battery module</span></span>
<span data-ttu-id="8269d-168">No seu dispositivo StorSimple, o módulo de bateria de backup fornece energia ao controlador durante um evento de perda de energia.</span><span class="sxs-lookup"><span data-stu-id="8269d-168">In your StorSimple device, the backup battery module provides power to the controller during a power loss event.</span></span> <span data-ttu-id="8269d-169">Ele permite que o dispositivo StorSimple salve dados críticos antes de encerrar de maneira controlada.</span><span class="sxs-lookup"><span data-stu-id="8269d-169">It allows the StorSimple device to save critical data prior to shutting down in a controlled manner.</span></span> <span data-ttu-id="8269d-170">Com duas baterias completamente carregadas nos PCMs, o sistema pode manipular dois eventos consecutivos de perda.</span><span class="sxs-lookup"><span data-stu-id="8269d-170">With two fully charged batteries in the PCMs, the system can handle two consecutive loss events.</span></span>

<span data-ttu-id="8269d-171">No Portal clássico do Azure, o **Status de Hardware** na página **Manutenção** indica se a bateria está com defeito ou se está próxima do fim da vida útil.</span><span class="sxs-lookup"><span data-stu-id="8269d-171">In the Azure classic portal, the **Hardware Status** on the **Maintenance** page indicates whether the battery is malfunctioning or the end-of-life is approaching.</span></span> <span data-ttu-id="8269d-172">O status da bateria é indicado por **Bateria no PCM 0** ou **Bateria no PCM 1** em **Componentes compartilhados**.</span><span class="sxs-lookup"><span data-stu-id="8269d-172">The battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="8269d-173">Essa página mostrará um estado **DEGRADADO** quando próximo do fim da vida útil e **FALHA** quando atingir o fim da vida útil.</span><span class="sxs-lookup"><span data-stu-id="8269d-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="8269d-174">A bateria pode relatar **FALHA** quando precisar apenas ser carregada.</span><span class="sxs-lookup"><span data-stu-id="8269d-174">The battery can report **FAILED** when it simply needs to be charged.</span></span>
> 
> 

<span data-ttu-id="8269d-175">Se o estado **DEGRADADO** for exibido, recomendamos o seguinte curso de ação:</span><span class="sxs-lookup"><span data-stu-id="8269d-175">If the **DEGRADED** state appears, we recommend the following course of action:</span></span>

* <span data-ttu-id="8269d-176">O sistema pode ter tido uma perda de energia recente ou as baterias podem estar passando por manutenção periódica.</span><span class="sxs-lookup"><span data-stu-id="8269d-176">The system may have experienced a recent power loss or the batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="8269d-177">Observe o sistema por 12 horas antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="8269d-177">Observe the system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="8269d-178">Se o estado ainda estiver **DEGRADADO** após 12 horas de conexão contínua à energia CA com os controladores e os PCMs em execução, então a bateria precisará ser substituída.</span><span class="sxs-lookup"><span data-stu-id="8269d-178">If the state is still **DEGRADED** after 12 hours of continuous connection to AC power with the controllers and PCMs running, then the battery needs to be replaced.</span></span> <span data-ttu-id="8269d-179">Por favor [Contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md) para obter um módulo de bateria de backup de reposição.</span><span class="sxs-lookup"><span data-stu-id="8269d-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="8269d-180">Se o estado estiver OK após 12 horas, a bateria está operacional e precisava apenas de uma carga de manutenção.</span><span class="sxs-lookup"><span data-stu-id="8269d-180">If the state becomes OK after 12 hours, the battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="8269d-181">Se não houve uma perda associada à energia AC e o PCM está ligado e conectado à corrente alternada, a bateria precisa ser substituído.</span><span class="sxs-lookup"><span data-stu-id="8269d-181">If there has not been an associated loss of AC power and the PCM is turned on and connected to AC power, the battery needs to be replaced.</span></span> <span data-ttu-id="8269d-182">[Contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md) para solicitar um módulo de bateria de reposição.</span><span class="sxs-lookup"><span data-stu-id="8269d-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) to order a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8269d-183">Descarte a bateria com falha de acordo com as regulamentações nacionais e regionais.</span><span class="sxs-lookup"><span data-stu-id="8269d-183">Dispose of the failed battery according to national and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8269d-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8269d-184">Next steps</span></span>
<span data-ttu-id="8269d-185">Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="8269d-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

