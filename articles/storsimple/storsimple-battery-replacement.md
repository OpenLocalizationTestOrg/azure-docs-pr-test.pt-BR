---
title: bateria aaaReplace no dispositivo StorSimple do Microsoft Azure | Microsoft Docs
description: "Descreve como tooremove, substituir e manter o módulo de bateria de backup Olá em seu dispositivo StorSimple."
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
ms.openlocfilehash: 542774a5f451ec7ad2bd442f88598df318d8b285
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="228cf-103">Substituir o módulo de bateria de backup Olá em seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="228cf-103">Replace hello backup battery module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="228cf-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="228cf-104">Overview</span></span>
<span data-ttu-id="228cf-105">compartimento principal de saudação Power e módulo de resfriamento (PCM) no seu dispositivo StorSimple do Microsoft Azure tem um pacote adicional de bateria.</span><span class="sxs-lookup"><span data-stu-id="228cf-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="228cf-106">Esse pacote fornece energia para que hello dispositivo StorSimple pode salvar dados caso haja perda de compartimento principal de toohello de alimentação de CA.</span><span class="sxs-lookup"><span data-stu-id="228cf-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="228cf-107">Esse pacote de bateria é chamado tooas Olá *módulo de bateria de backup*.</span><span class="sxs-lookup"><span data-stu-id="228cf-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="228cf-108">módulo de bateria de backup Olá existe somente para o compartimento principal de saudação em seu dispositivo StorSimple (Olá compartimento EBOD não contém um módulo de bateria de backup).</span><span class="sxs-lookup"><span data-stu-id="228cf-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span> 

<span data-ttu-id="228cf-109">Este tutorial explica como:</span><span class="sxs-lookup"><span data-stu-id="228cf-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="228cf-110">Remover o módulo de bateria de backup Olá</span><span class="sxs-lookup"><span data-stu-id="228cf-110">Remove hello backup battery module</span></span> 
* <span data-ttu-id="228cf-111">Instalar um novo módulo de bateria de backup</span><span class="sxs-lookup"><span data-stu-id="228cf-111">Install a new backup battery module</span></span>
* <span data-ttu-id="228cf-112">Manter o módulo de bateria de backup Olá</span><span class="sxs-lookup"><span data-stu-id="228cf-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="228cf-113">Antes de remover e substituir um módulo de bateria de backup, analisar informações de segurança Olá Olá [substituição de componentes de hardware Introdução tooStorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="228cf-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="228cf-114">Remover o módulo de bateria de backup Olá</span><span class="sxs-lookup"><span data-stu-id="228cf-114">Remove hello backup battery module</span></span>
<span data-ttu-id="228cf-115">módulo de bateria de backup Olá para seu dispositivo StorSimple é uma unidade substituível de campo.</span><span class="sxs-lookup"><span data-stu-id="228cf-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="228cf-116">Antes de ser instalada em Olá PCM, o módulo da bateria Olá deve ser armazenado em sua embalagem original.</span><span class="sxs-lookup"><span data-stu-id="228cf-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="228cf-117">Execute Olá bateria de backup tooremove Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="228cf-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="228cf-118">módulo de bateria de backup Olá tooremove</span><span class="sxs-lookup"><span data-stu-id="228cf-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="228cf-119">No hello portal clássico do Azure, vá muito**dispositivos** > **manutenção** > **Status do Hardware**.</span><span class="sxs-lookup"><span data-stu-id="228cf-119">In hello Azure classic portal, go too**Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="228cf-120">Em **componentes compartilhados**, observar Olá status da bateria hello.</span><span class="sxs-lookup"><span data-stu-id="228cf-120">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="228cf-121">Identifica Olá PCM no qual Olá bateria falhou.</span><span class="sxs-lookup"><span data-stu-id="228cf-121">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="228cf-122">A Figura 1 mostra Olá parte posterior do dispositivo do StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="228cf-122">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Backplane dos módulos do compartimento primário do dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="228cf-124">**Figura 1** Parte traseira do dispositivo primário mostrando os módulos de controlador e PCM</span><span class="sxs-lookup"><span data-stu-id="228cf-124">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="228cf-125">Rótulo</span><span class="sxs-lookup"><span data-stu-id="228cf-125">Label</span></span> | <span data-ttu-id="228cf-126">Descrição</span><span class="sxs-lookup"><span data-stu-id="228cf-126">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="228cf-127">1</span><span class="sxs-lookup"><span data-stu-id="228cf-127">1</span></span> |<span data-ttu-id="228cf-128">PCM 0</span><span class="sxs-lookup"><span data-stu-id="228cf-128">PCM 0</span></span> |
   | <span data-ttu-id="228cf-129">2</span><span class="sxs-lookup"><span data-stu-id="228cf-129">2</span></span> |<span data-ttu-id="228cf-130">PCM 1</span><span class="sxs-lookup"><span data-stu-id="228cf-130">PCM 1</span></span> |
   | <span data-ttu-id="228cf-131">3</span><span class="sxs-lookup"><span data-stu-id="228cf-131">3</span></span> |<span data-ttu-id="228cf-132">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="228cf-132">Controller 0</span></span> |
   | <span data-ttu-id="228cf-133">4</span><span class="sxs-lookup"><span data-stu-id="228cf-133">4</span></span> |<span data-ttu-id="228cf-134">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="228cf-134">Controller 1</span></span> |
   
    <span data-ttu-id="228cf-135">Conforme mostrado pelo número 3 na Figura 2 de hello, Olá monitoramento indicador LED no PCM 0 que corresponde muito**falha de bateria** deve estar aceso.</span><span class="sxs-lookup"><span data-stu-id="228cf-135">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Backplane dos LEDs indicadores de monitoramento de PCM do dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="228cf-137">**Figura 2** saudação do parte posterior do PCM mostrando LEDs indicadores de monitoramento</span><span class="sxs-lookup"><span data-stu-id="228cf-137">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="228cf-138">Rótulo</span><span class="sxs-lookup"><span data-stu-id="228cf-138">Label</span></span> | <span data-ttu-id="228cf-139">Descrição</span><span class="sxs-lookup"><span data-stu-id="228cf-139">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="228cf-140">1</span><span class="sxs-lookup"><span data-stu-id="228cf-140">1</span></span> |<span data-ttu-id="228cf-141">Falha de energia CA</span><span class="sxs-lookup"><span data-stu-id="228cf-141">AC power failure</span></span> |
   | <span data-ttu-id="228cf-142">2</span><span class="sxs-lookup"><span data-stu-id="228cf-142">2</span></span> |<span data-ttu-id="228cf-143">Falha do ventilador</span><span class="sxs-lookup"><span data-stu-id="228cf-143">Fan failure</span></span> |
   | <span data-ttu-id="228cf-144">3</span><span class="sxs-lookup"><span data-stu-id="228cf-144">3</span></span> |<span data-ttu-id="228cf-145">Falha de bateria</span><span class="sxs-lookup"><span data-stu-id="228cf-145">Battery fault</span></span> |
   | <span data-ttu-id="228cf-146">4</span><span class="sxs-lookup"><span data-stu-id="228cf-146">4</span></span> |<span data-ttu-id="228cf-147">PCM OK</span><span class="sxs-lookup"><span data-stu-id="228cf-147">PCM OK</span></span> |
   | <span data-ttu-id="228cf-148">5</span><span class="sxs-lookup"><span data-stu-id="228cf-148">5</span></span> |<span data-ttu-id="228cf-149">Falha de energia CC</span><span class="sxs-lookup"><span data-stu-id="228cf-149">DC power failure</span></span> |
   | <span data-ttu-id="228cf-150">6</span><span class="sxs-lookup"><span data-stu-id="228cf-150">6</span></span> |<span data-ttu-id="228cf-151">Bateria íntegra</span><span class="sxs-lookup"><span data-stu-id="228cf-151">Battery healthy</span></span> |
3. <span data-ttu-id="228cf-152">Olá tooremove PCM com uma bateria com falha, execute as etapas de saudação em [remover um PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="228cf-152">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="228cf-153">Olá PCM removido, comparação de precisão e bateria Olá girar módulo tratar para cima, conforme indicado na figura a seguir de saudação e levante-o backup de bateria de saudação tooremove.</span><span class="sxs-lookup"><span data-stu-id="228cf-153">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Removendo bateria do PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="228cf-155">**Figura 3** removendo bateria de saudação do hello PCM</span><span class="sxs-lookup"><span data-stu-id="228cf-155">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="228cf-156">Coloque o módulo de saudação no pacote da unidade substituível em campo hello.</span><span class="sxs-lookup"><span data-stu-id="228cf-156">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="228cf-157">Retorne Olá tooMicrosoft de unidade defeituosa para serviços e reparos adequados.</span><span class="sxs-lookup"><span data-stu-id="228cf-157">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="228cf-158">Instalar um novo módulo de bateria de backup</span><span class="sxs-lookup"><span data-stu-id="228cf-158">Install a new backup battery module</span></span>
<span data-ttu-id="228cf-159">Execute Olá seguindo o módulo de bateria de substituição etapas tooinstall Olá no hello PCM no compartimento primário de saudação do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="228cf-159">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="228cf-160">módulo de bateria Olá tooinstall</span><span class="sxs-lookup"><span data-stu-id="228cf-160">tooinstall hello battery module</span></span>
1. <span data-ttu-id="228cf-161">Coloque o módulo de bateria de backup de saudação na orientação correta de saudação no hello PCM.</span><span class="sxs-lookup"><span data-stu-id="228cf-161">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="228cf-162">Pressione para baixo o módulo da bateria Olá lidar com todas as conector de Olá Olá maneira tooseat.</span><span class="sxs-lookup"><span data-stu-id="228cf-162">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="228cf-163">Substituir Olá PCM no compartimento primário Olá seguindo as diretrizes Olá [substituir de energia e resfriamento módulo em seu dispositivo StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="228cf-163">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="228cf-164">Após a conclusão da substituição hello, vá muito**dispositivos** > **manutenção** > **Status de Hardware** no hello portal clássico do Azure.</span><span class="sxs-lookup"><span data-stu-id="228cf-164">After hello replacement is complete, go too**Devices** > **Maintenance** > **Hardware Status** in hello Azure classic portal.</span></span> <span data-ttu-id="228cf-165">Verificar o status da saudação do hello bateria toomake-se de que a instalação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="228cf-165">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="228cf-166">Um status verde indica que a bateria hello está íntegra.</span><span class="sxs-lookup"><span data-stu-id="228cf-166">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="228cf-167">Manter o módulo de bateria de backup Olá</span><span class="sxs-lookup"><span data-stu-id="228cf-167">Maintain hello backup battery module</span></span>
<span data-ttu-id="228cf-168">Em seu dispositivo StorSimple, o módulo de bateria de backup Olá fornece controlador toohello de energia durante um evento de perda de energia.</span><span class="sxs-lookup"><span data-stu-id="228cf-168">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="228cf-169">Ele permite Olá StorSimple dispositivo toosave dados críticos anterior tooshutting para baixo de forma controlada.</span><span class="sxs-lookup"><span data-stu-id="228cf-169">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="228cf-170">Com duas baterias completamente no hello PCMs, sistema Olá pode lidar com dois eventos consecutivos de perda.</span><span class="sxs-lookup"><span data-stu-id="228cf-170">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="228cf-171">No portal clássico do Azure do hello, Olá **Status do Hardware** em Olá **manutenção** página indica se a bateria hello está funcionando corretamente ou Olá fim da vida está se aproximando.</span><span class="sxs-lookup"><span data-stu-id="228cf-171">In hello Azure classic portal, hello **Hardware Status** on hello **Maintenance** page indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="228cf-172">status da bateria Olá é indicado por **bateria no PCM 0** ou **bateria no PCM 1** em **componentes compartilhados**.</span><span class="sxs-lookup"><span data-stu-id="228cf-172">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="228cf-173">Essa página mostrará um estado **DEGRADADO** quando próximo do fim da vida útil e **FALHA** quando atingir o fim da vida útil.</span><span class="sxs-lookup"><span data-stu-id="228cf-173">This page will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span> 

> [!NOTE]
> <span data-ttu-id="228cf-174">Olá bateria pode relatar **falha** quando ele precisa apenas toobe cobrado.</span><span class="sxs-lookup"><span data-stu-id="228cf-174">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>
> 
> 

<span data-ttu-id="228cf-175">Se hello **DEGRADADO** estado é exibido, é recomendável Olá curso de ação a seguir:</span><span class="sxs-lookup"><span data-stu-id="228cf-175">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="228cf-176">sistema Olá pode encontraram uma perda de energia recentes ou baterias Olá podem ser passando por manutenção periódica.</span><span class="sxs-lookup"><span data-stu-id="228cf-176">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="228cf-177">Observe o sistema Olá para 12 horas antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="228cf-177">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="228cf-178">Se o estado de saudação ainda **DEGRADADO** após 12 horas de energia de tooAC de conexão contínua com hello controladores e execução, de PCMs, em seguida, Olá bateria precisa toobe substituído.</span><span class="sxs-lookup"><span data-stu-id="228cf-178">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="228cf-179">Por favor [Contate o Suporte da Microsoft](storsimple-contact-microsoft-support.md) para obter um módulo de bateria de backup de reposição.</span><span class="sxs-lookup"><span data-stu-id="228cf-179">Please [contact Microsoft Support](storsimple-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="228cf-180">Se o estado da saudação se tornará Okey após 12 horas, Olá bateria está operacional e somente é necessário um custo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="228cf-180">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="228cf-181">Se não houve uma perda associada alternada e hello PCM está ligada e conectado tooAC power, bateria Olá precisa toobe substituído.</span><span class="sxs-lookup"><span data-stu-id="228cf-181">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="228cf-182">[Entre em contato com o Microsoft Support](storsimple-contact-microsoft-support.md) tooorder uma substituição de módulo de bateria de backup.</span><span class="sxs-lookup"><span data-stu-id="228cf-182">[Contact Microsoft Support](storsimple-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="228cf-183">Descarte Olá Falha na bateria de acordo com as normas regionais e toonational.</span><span class="sxs-lookup"><span data-stu-id="228cf-183">Dispose of hello failed battery according toonational and regional regulations.</span></span> 
> 
> 

## <a name="next-steps"></a><span data-ttu-id="228cf-184">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="228cf-184">Next steps</span></span>
<span data-ttu-id="228cf-185">Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="228cf-185">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

