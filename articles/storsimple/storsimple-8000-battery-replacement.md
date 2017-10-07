---
title: bateria aaaReplace no dispositivo do Microsoft Azure StorSimple 8000 series | Microsoft Docs
description: "Descreve como tooremove, substituir e manter o módulo de bateria de backup Olá em seu dispositivo StorSimple."
services: storsimple
documentationcenter: 
author: alkohli
manager: timlt
editor: 
ms.assetid: 
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 06/05/2017
ms.author: alkohli
ms.openlocfilehash: 5ac767807e6c3fd817d8d522629db2aceaac9bdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-hello-backup-battery-module-on-your-storsimple-device"></a><span data-ttu-id="7c71a-103">Substituir o módulo de bateria de backup Olá em seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="7c71a-103">Replace hello backup battery module on your StorSimple device</span></span>

## <a name="overview"></a><span data-ttu-id="7c71a-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="7c71a-104">Overview</span></span>
<span data-ttu-id="7c71a-105">compartimento principal de saudação Power e módulo de resfriamento (PCM) no seu dispositivo StorSimple do Microsoft Azure tem um pacote adicional de bateria.</span><span class="sxs-lookup"><span data-stu-id="7c71a-105">hello primary enclosure Power and Cooling Module (PCM) on your Microsoft Azure StorSimple device has an additional battery pack.</span></span> <span data-ttu-id="7c71a-106">Esse pacote fornece energia para que hello dispositivo StorSimple pode salvar dados caso haja perda de compartimento principal de toohello de alimentação de CA.</span><span class="sxs-lookup"><span data-stu-id="7c71a-106">This pack provides power so that hello StorSimple device can save data if there is loss of AC power toohello primary enclosure.</span></span> <span data-ttu-id="7c71a-107">Esse pacote de bateria é chamado tooas Olá *módulo de bateria de backup*.</span><span class="sxs-lookup"><span data-stu-id="7c71a-107">This battery pack is referred tooas hello *backup battery module*.</span></span> <span data-ttu-id="7c71a-108">módulo de bateria de backup Olá existe somente para o compartimento principal de saudação em seu dispositivo StorSimple (Olá compartimento EBOD não contém um módulo de bateria de backup).</span><span class="sxs-lookup"><span data-stu-id="7c71a-108">hello backup battery module exists only for hello primary enclosure in your StorSimple device (hello EBOD enclosure does not contain a backup battery module).</span></span>

<span data-ttu-id="7c71a-109">Este tutorial explica como:</span><span class="sxs-lookup"><span data-stu-id="7c71a-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="7c71a-110">Remover o módulo de bateria de backup Olá</span><span class="sxs-lookup"><span data-stu-id="7c71a-110">Remove hello backup battery module</span></span>
* <span data-ttu-id="7c71a-111">Instalar um novo módulo de bateria de backup</span><span class="sxs-lookup"><span data-stu-id="7c71a-111">Install a new backup battery module</span></span>
* <span data-ttu-id="7c71a-112">Manter o módulo de bateria de backup Olá</span><span class="sxs-lookup"><span data-stu-id="7c71a-112">Maintain hello backup battery module</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c71a-113">Antes de remover e substituir um módulo de bateria de backup, analisar informações de segurança Olá Olá [substituição de componentes de hardware Introdução tooStorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="7c71a-113">Before removing and replacing a backup battery module, review hello safety information in hello [Introduction tooStorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="remove-hello-backup-battery-module"></a><span data-ttu-id="7c71a-114">Remover o módulo de bateria de backup Olá</span><span class="sxs-lookup"><span data-stu-id="7c71a-114">Remove hello backup battery module</span></span>
<span data-ttu-id="7c71a-115">módulo de bateria de backup Olá para seu dispositivo StorSimple é uma unidade substituível de campo.</span><span class="sxs-lookup"><span data-stu-id="7c71a-115">hello backup battery module for your StorSimple device is a field-replaceable unit.</span></span> <span data-ttu-id="7c71a-116">Antes de ser instalada em Olá PCM, o módulo da bateria Olá deve ser armazenado em sua embalagem original.</span><span class="sxs-lookup"><span data-stu-id="7c71a-116">Before it is installed in hello PCM, hello battery module should be stored in its original packaging.</span></span> <span data-ttu-id="7c71a-117">Execute Olá bateria de backup tooremove Olá etapas a seguir.</span><span class="sxs-lookup"><span data-stu-id="7c71a-117">Perform hello following steps tooremove hello backup battery.</span></span>

#### <a name="tooremove-hello-backup-battery-module"></a><span data-ttu-id="7c71a-118">módulo de bateria de backup Olá tooremove</span><span class="sxs-lookup"><span data-stu-id="7c71a-118">tooremove hello backup battery module</span></span>
1. <span data-ttu-id="7c71a-119">No hello portal do Azure, vá tooyour folha de serviço de Gerenciador de dispositivos do StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7c71a-119">In hello Azure portal, go tooyour StorSimple Device Manager service blade.</span></span> <span data-ttu-id="7c71a-120">Vá muito**dispositivos** e, em seguida, selecione seu dispositivo na lista de saudação de dispositivos.</span><span class="sxs-lookup"><span data-stu-id="7c71a-120">Go too**Devices** and then select your device from hello list of devices.</span></span> <span data-ttu-id="7c71a-121">Navegue muito**Monitor** > **a integridade do Hardware**.</span><span class="sxs-lookup"><span data-stu-id="7c71a-121">Navigate too**Monitor** > **Hardware health**.</span></span> <span data-ttu-id="7c71a-122">Em **componentes compartilhados**, observar Olá status da bateria hello.</span><span class="sxs-lookup"><span data-stu-id="7c71a-122">Under **Shared Components**, look at hello status of hello battery.</span></span>
2. <span data-ttu-id="7c71a-123">Identifica Olá PCM no qual Olá bateria falhou.</span><span class="sxs-lookup"><span data-stu-id="7c71a-123">Identify hello PCM in which hello battery has failed.</span></span> <span data-ttu-id="7c71a-124">A Figura 1 mostra Olá parte posterior do dispositivo do StorSimple hello.</span><span class="sxs-lookup"><span data-stu-id="7c71a-124">Figure 1 shows hello back of hello StorSimple device.</span></span>
   
    ![Backplane dos módulos do compartimento primário do dispositivo](./media/storsimple-battery-replacement/IC740994.png)
   
    <span data-ttu-id="7c71a-126">**Figura 1** Parte traseira do dispositivo primário mostrando os módulos de controlador e PCM</span><span class="sxs-lookup"><span data-stu-id="7c71a-126">**Figure 1** Back of primary device showing PCM and controller modules</span></span>
   
   | <span data-ttu-id="7c71a-127">Rótulo</span><span class="sxs-lookup"><span data-stu-id="7c71a-127">Label</span></span> | <span data-ttu-id="7c71a-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="7c71a-128">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="7c71a-129">1</span><span class="sxs-lookup"><span data-stu-id="7c71a-129">1</span></span> |<span data-ttu-id="7c71a-130">PCM 0</span><span class="sxs-lookup"><span data-stu-id="7c71a-130">PCM 0</span></span> |
   | <span data-ttu-id="7c71a-131">2</span><span class="sxs-lookup"><span data-stu-id="7c71a-131">2</span></span> |<span data-ttu-id="7c71a-132">PCM 1</span><span class="sxs-lookup"><span data-stu-id="7c71a-132">PCM 1</span></span> |
   | <span data-ttu-id="7c71a-133">3</span><span class="sxs-lookup"><span data-stu-id="7c71a-133">3</span></span> |<span data-ttu-id="7c71a-134">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="7c71a-134">Controller 0</span></span> |
   | <span data-ttu-id="7c71a-135">4</span><span class="sxs-lookup"><span data-stu-id="7c71a-135">4</span></span> |<span data-ttu-id="7c71a-136">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="7c71a-136">Controller 1</span></span> |
   
    <span data-ttu-id="7c71a-137">Conforme mostrado pelo número 3 na Figura 2 de hello, Olá monitoramento indicador LED no PCM 0 que corresponde muito**falha de bateria** deve estar aceso.</span><span class="sxs-lookup"><span data-stu-id="7c71a-137">As shown by number 3 in hello Figure 2, hello monitoring indicator LED on PCM 0 that corresponds too**Battery Fault** should be lit.</span></span>
   
    ![Backplane dos LEDs indicadores de monitoramento de PCM do dispositivo](./media/storsimple-battery-replacement/IC740992.png)
   
    <span data-ttu-id="7c71a-139">**Figura 2** saudação do parte posterior do PCM mostrando LEDs indicadores de monitoramento</span><span class="sxs-lookup"><span data-stu-id="7c71a-139">**Figure 2** Back of PCM showing hello monitoring indicator LEDs</span></span>
   
   | <span data-ttu-id="7c71a-140">Rótulo</span><span class="sxs-lookup"><span data-stu-id="7c71a-140">Label</span></span> | <span data-ttu-id="7c71a-141">Descrição</span><span class="sxs-lookup"><span data-stu-id="7c71a-141">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="7c71a-142">1</span><span class="sxs-lookup"><span data-stu-id="7c71a-142">1</span></span> |<span data-ttu-id="7c71a-143">Falha de energia CA</span><span class="sxs-lookup"><span data-stu-id="7c71a-143">AC power failure</span></span> |
   | <span data-ttu-id="7c71a-144">2</span><span class="sxs-lookup"><span data-stu-id="7c71a-144">2</span></span> |<span data-ttu-id="7c71a-145">Falha do ventilador</span><span class="sxs-lookup"><span data-stu-id="7c71a-145">Fan failure</span></span> |
   | <span data-ttu-id="7c71a-146">3</span><span class="sxs-lookup"><span data-stu-id="7c71a-146">3</span></span> |<span data-ttu-id="7c71a-147">Falha de bateria</span><span class="sxs-lookup"><span data-stu-id="7c71a-147">Battery fault</span></span> |
   | <span data-ttu-id="7c71a-148">4</span><span class="sxs-lookup"><span data-stu-id="7c71a-148">4</span></span> |<span data-ttu-id="7c71a-149">PCM OK</span><span class="sxs-lookup"><span data-stu-id="7c71a-149">PCM OK</span></span> |
   | <span data-ttu-id="7c71a-150">5</span><span class="sxs-lookup"><span data-stu-id="7c71a-150">5</span></span> |<span data-ttu-id="7c71a-151">Falha de energia CC</span><span class="sxs-lookup"><span data-stu-id="7c71a-151">DC power failure</span></span> |
   | <span data-ttu-id="7c71a-152">6</span><span class="sxs-lookup"><span data-stu-id="7c71a-152">6</span></span> |<span data-ttu-id="7c71a-153">Bateria íntegra</span><span class="sxs-lookup"><span data-stu-id="7c71a-153">Battery healthy</span></span> |
3. <span data-ttu-id="7c71a-154">Olá tooremove PCM com uma bateria com falha, execute as etapas de saudação em [remover um PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span><span class="sxs-lookup"><span data-stu-id="7c71a-154">tooremove hello PCM with a failed battery, follow hello steps in [Remove a PCM](storsimple-power-cooling-module-replacement.md#remove-a-pcm).</span></span>
4. <span data-ttu-id="7c71a-155">Olá PCM removido, comparação de precisão e bateria Olá girar módulo tratar para cima, conforme indicado na figura a seguir de saudação e levante-o backup de bateria de saudação tooremove.</span><span class="sxs-lookup"><span data-stu-id="7c71a-155">With hello PCM removed, lift and rotate hello battery module handle upward as indicated in hello following figure, and pull it up tooremove hello battery.</span></span>
   
    ![Removendo bateria do PCM](./media/storsimple-battery-replacement/IC741019.png)
   
    <span data-ttu-id="7c71a-157">**Figura 3** removendo bateria de saudação do hello PCM</span><span class="sxs-lookup"><span data-stu-id="7c71a-157">**Figure 3** Removing hello battery from hello PCM</span></span>
5. <span data-ttu-id="7c71a-158">Coloque o módulo de saudação no pacote da unidade substituível em campo hello.</span><span class="sxs-lookup"><span data-stu-id="7c71a-158">Place hello module in hello field-replaceable unit packaging.</span></span>
6. <span data-ttu-id="7c71a-159">Retorne Olá tooMicrosoft de unidade defeituosa para serviços e reparos adequados.</span><span class="sxs-lookup"><span data-stu-id="7c71a-159">Return hello defective unit tooMicrosoft for proper servicing and handling.</span></span>

## <a name="install-a-new-backup-battery-module"></a><span data-ttu-id="7c71a-160">Instalar um novo módulo de bateria de backup</span><span class="sxs-lookup"><span data-stu-id="7c71a-160">Install a new backup battery module</span></span>
<span data-ttu-id="7c71a-161">Execute Olá seguindo o módulo de bateria de substituição etapas tooinstall Olá no hello PCM no compartimento primário de saudação do seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="7c71a-161">Perform hello following steps tooinstall hello replacement battery module in hello PCM in hello primary enclosure of your StorSimple device.</span></span>

#### <a name="tooinstall-hello-battery-module"></a><span data-ttu-id="7c71a-162">módulo de bateria Olá tooinstall</span><span class="sxs-lookup"><span data-stu-id="7c71a-162">tooinstall hello battery module</span></span>
1. <span data-ttu-id="7c71a-163">Coloque o módulo de bateria de backup de saudação na orientação correta de saudação no hello PCM.</span><span class="sxs-lookup"><span data-stu-id="7c71a-163">Place hello backup battery module in hello proper orientation in hello PCM.</span></span>
2. <span data-ttu-id="7c71a-164">Pressione para baixo o módulo da bateria Olá lidar com todas as conector de Olá Olá maneira tooseat.</span><span class="sxs-lookup"><span data-stu-id="7c71a-164">Press down hello battery module handle all hello way tooseat hello connector.</span></span>
3. <span data-ttu-id="7c71a-165">Substituir Olá PCM no compartimento primário Olá seguindo as diretrizes Olá [substituir de energia e resfriamento módulo em seu dispositivo StorSimple](storsimple-power-cooling-module-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="7c71a-165">Replace hello PCM in hello primary enclosure by following hello guidelines in [Replace a Power and Cooling Module on your StorSimple device](storsimple-power-cooling-module-replacement.md).</span></span>
4. <span data-ttu-id="7c71a-166">Após a conclusão da substituição hello, vá tooyour dispositivo e muito**Monitor** > **a integridade do Hardware** no hello portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="7c71a-166">After hello replacement is complete, go tooyour device and then go too**Monitor** > **Hardware health** in hello Azure portal.</span></span> <span data-ttu-id="7c71a-167">Verificar o status da saudação do hello bateria toomake-se de que a instalação de saudação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="7c71a-167">Verify hello status of hello battery toomake sure that hello installation was successful.</span></span> <span data-ttu-id="7c71a-168">Um status verde indica que a bateria hello está íntegra.</span><span class="sxs-lookup"><span data-stu-id="7c71a-168">A green status indicates that hello battery is healthy.</span></span>

## <a name="maintain-hello-backup-battery-module"></a><span data-ttu-id="7c71a-169">Manter o módulo de bateria de backup Olá</span><span class="sxs-lookup"><span data-stu-id="7c71a-169">Maintain hello backup battery module</span></span>
<span data-ttu-id="7c71a-170">Em seu dispositivo StorSimple, o módulo de bateria de backup Olá fornece controlador toohello de energia durante um evento de perda de energia.</span><span class="sxs-lookup"><span data-stu-id="7c71a-170">In your StorSimple device, hello backup battery module provides power toohello controller during a power loss event.</span></span> <span data-ttu-id="7c71a-171">Ele permite Olá StorSimple dispositivo toosave dados críticos anterior tooshutting para baixo de forma controlada.</span><span class="sxs-lookup"><span data-stu-id="7c71a-171">It allows hello StorSimple device toosave critical data prior tooshutting down in a controlled manner.</span></span> <span data-ttu-id="7c71a-172">Com duas baterias completamente no hello PCMs, sistema Olá pode lidar com dois eventos consecutivos de perda.</span><span class="sxs-lookup"><span data-stu-id="7c71a-172">With two fully charged batteries in hello PCMs, hello system can handle two consecutive loss events.</span></span>

<span data-ttu-id="7c71a-173">No portal do Azure de Olá, Olá **a integridade do Hardware** em Olá **Monitor** folha indica se a bateria hello está funcionando corretamente ou Olá fim da vida está se aproximando.</span><span class="sxs-lookup"><span data-stu-id="7c71a-173">In hello Azure portal, hello **Hardware health** under hello **Monitor** blade indicates whether hello battery is malfunctioning or hello end-of-life is approaching.</span></span> <span data-ttu-id="7c71a-174">status da bateria Olá é indicado por **bateria no PCM 0** ou **bateria no PCM 1** em **componentes compartilhados**.</span><span class="sxs-lookup"><span data-stu-id="7c71a-174">hello battery status is indicated by **Battery in PCM 0** or **Battery in PCM 1** under **Shared Components**.</span></span> <span data-ttu-id="7c71a-175">Essa folha mostrará um estado **DEGRADADO** quando ela estiver próxima do fim do tempo de vida e **FALHA** quando atingir o fim do tempo de vida.</span><span class="sxs-lookup"><span data-stu-id="7c71a-175">This blade will show a **DEGRADED** state for end-of-life approaching, and **FAILED** for end-of-life reached.</span></span>

> [!NOTE]
> <span data-ttu-id="7c71a-176">Olá bateria pode relatar **falha** quando ele precisa apenas toobe cobrado.</span><span class="sxs-lookup"><span data-stu-id="7c71a-176">hello battery can report **FAILED** when it simply needs toobe charged.</span></span>


<span data-ttu-id="7c71a-177">Se hello **DEGRADADO** estado é exibido, é recomendável Olá curso de ação a seguir:</span><span class="sxs-lookup"><span data-stu-id="7c71a-177">If hello **DEGRADED** state appears, we recommend hello following course of action:</span></span>

* <span data-ttu-id="7c71a-178">sistema Olá pode encontraram uma perda de energia recentes ou baterias Olá podem ser passando por manutenção periódica.</span><span class="sxs-lookup"><span data-stu-id="7c71a-178">hello system may have experienced a recent power loss or hello batteries may be undergoing periodic maintenance.</span></span> <span data-ttu-id="7c71a-179">Observe o sistema Olá para 12 horas antes de continuar.</span><span class="sxs-lookup"><span data-stu-id="7c71a-179">Observe hello system for 12 hours before proceeding.</span></span>
  
  * <span data-ttu-id="7c71a-180">Se o estado de saudação ainda **DEGRADADO** após 12 horas de energia de tooAC de conexão contínua com hello controladores e execução, de PCMs, em seguida, Olá bateria precisa toobe substituído.</span><span class="sxs-lookup"><span data-stu-id="7c71a-180">If hello state is still **DEGRADED** after 12 hours of continuous connection tooAC power with hello controllers and PCMs running, then hello battery needs toobe replaced.</span></span> <span data-ttu-id="7c71a-181">Por favor [Contate o Suporte da Microsoft](storsimple-8000-contact-microsoft-support.md) para obter um módulo de bateria de backup de reposição.</span><span class="sxs-lookup"><span data-stu-id="7c71a-181">Please [contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) for a replacement backup battery module.</span></span>
  * <span data-ttu-id="7c71a-182">Se o estado da saudação se tornará Okey após 12 horas, Olá bateria está operacional e somente é necessário um custo de manutenção.</span><span class="sxs-lookup"><span data-stu-id="7c71a-182">If hello state becomes OK after 12 hours, hello battery is operational, and it only needed a maintenance charge.</span></span>
* <span data-ttu-id="7c71a-183">Se não houve uma perda associada alternada e hello PCM está ligada e conectado tooAC power, bateria Olá precisa toobe substituído.</span><span class="sxs-lookup"><span data-stu-id="7c71a-183">If there has not been an associated loss of AC power and hello PCM is turned on and connected tooAC power, hello battery needs toobe replaced.</span></span> <span data-ttu-id="7c71a-184">[Entre em contato com o Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder uma substituição de módulo de bateria de backup.</span><span class="sxs-lookup"><span data-stu-id="7c71a-184">[Contact Microsoft Support](storsimple-8000-contact-microsoft-support.md) tooorder a replacement backup battery module.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7c71a-185">Descarte Olá Falha na bateria de acordo com as normas regionais e toonational.</span><span class="sxs-lookup"><span data-stu-id="7c71a-185">Dispose of hello failed battery according toonational and regional regulations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7c71a-186">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7c71a-186">Next steps</span></span>
<span data-ttu-id="7c71a-187">Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="7c71a-187">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

