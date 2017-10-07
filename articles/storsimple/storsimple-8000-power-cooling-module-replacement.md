---
title: "aaaReplace um PCM do dispositivo da série StorSimple 8000 | Microsoft Docs"
description: "Explica como tooremove e substituir Olá energia e o módulo de resfriamento (PCM) no seu dispositivo StorSimple"
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
ms.date: 06/02/2017
ms.author: alkohli
ms.openlocfilehash: 474fd09787c5361a81efda4de74356027ac60f47
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="456aa-103">Substituir um módulo de energia e resfriamento em seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="456aa-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="456aa-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="456aa-104">Overview</span></span>
<span data-ttu-id="456aa-105">Olá Power e módulo de resfriamento (PCM) no seu dispositivo StorSimple do Microsoft Azure consiste em uma fonte de alimentação e ventiladores de resfriamento que são controladas pela hello primário e compartimentos EBOD.</span><span class="sxs-lookup"><span data-stu-id="456aa-105">hello Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through hello primary and EBOD enclosures.</span></span> <span data-ttu-id="456aa-106">Há apenas um modelo de PCM que é certificado para cada compartimento.</span><span class="sxs-lookup"><span data-stu-id="456aa-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="456aa-107">compartimento principal Olá é certificado para um PCM de 764 W e compartimento do EBOD Olá é certificado para um PCM de 580 W.</span><span class="sxs-lookup"><span data-stu-id="456aa-107">hello primary enclosure is certified for a 764 W PCM and hello EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="456aa-108">Embora hello PCMs para o compartimento principal hello e compartimento do EBOD Olá forem diferentes, o procedimento de substituição de saudação é idêntico.</span><span class="sxs-lookup"><span data-stu-id="456aa-108">Although hello PCMs for hello primary enclosure and hello EBOD enclosure are different, hello replacement procedure is identical.</span></span>

<span data-ttu-id="456aa-109">Este tutorial explica como:</span><span class="sxs-lookup"><span data-stu-id="456aa-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="456aa-110">Remover um PCM</span><span class="sxs-lookup"><span data-stu-id="456aa-110">Remove a PCM</span></span>
* <span data-ttu-id="456aa-111">Instalar um PCM de reposição</span><span class="sxs-lookup"><span data-stu-id="456aa-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="456aa-112">Antes de remover e substituir um PCM, revise as informações de segurança de saudação em [substituição de componentes de hardware do StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="456aa-112">Before removing and replacing a PCM, review hello safety information in [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>


## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="456aa-113">Antes de substituir um PCM</span><span class="sxs-lookup"><span data-stu-id="456aa-113">Before you replace a PCM</span></span>
<span data-ttu-id="456aa-114">Esteja ciente das questões importantes a seguir antes de substituir o PCM de saudação:</span><span class="sxs-lookup"><span data-stu-id="456aa-114">Be aware of hello following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="456aa-115">Se a fonte de alimentação de saudação do hello PCM falhar, mantenha Olá módulo com falha instalado, mas remova o cabo de alimentação Olá.</span><span class="sxs-lookup"><span data-stu-id="456aa-115">If hello power supply of hello PCM fails, leave hello faulty module installed, but remove hello power cord.</span></span> <span data-ttu-id="456aa-116">ventilador Olá continuará tooreceive energia do compartimento hello e continuar tooprovide o resfriamento apropriado.</span><span class="sxs-lookup"><span data-stu-id="456aa-116">hello fan will continue tooreceive power from hello enclosure and continue tooprovide proper cooling.</span></span> <span data-ttu-id="456aa-117">Se Olá ventilador falhar, Olá PCM deve toobe substituído imediatamente.</span><span class="sxs-lookup"><span data-stu-id="456aa-117">If hello fan fails, hello PCM needs toobe replaced immediately.</span></span>
* <span data-ttu-id="456aa-118">Antes de remover Olá PCM, desconecte Olá Olá PCM desligando o interruptor principal hello (se houver) ou removendo fisicamente o cabo de alimentação hello.</span><span class="sxs-lookup"><span data-stu-id="456aa-118">Before removing hello PCM, disconnect hello power from hello PCM by turning off hello main switch (where present) or by physically removing hello power cord.</span></span> <span data-ttu-id="456aa-119">Isso fornece um sistema de tooyour de aviso que a energia será desligada iminente.</span><span class="sxs-lookup"><span data-stu-id="456aa-119">This provides a warning tooyour system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="456aa-120">Certifique-se que Olá para que outro PCM está funcionando continua operação do sistema antes de substituir Olá PCM com falha.</span><span class="sxs-lookup"><span data-stu-id="456aa-120">Make sure that hello other PCM is functional for continued system operation before replacing hello faulty PCM.</span></span> <span data-ttu-id="456aa-121">Um PCM defeituoso deve ser substituído por um PCM totalmente operacional assim que possível.</span><span class="sxs-lookup"><span data-stu-id="456aa-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="456aa-122">Substituição do módulo PCM leva apenas alguns toocomplete de minutos, mas ela deve ser concluída em 10 minutos da remoção Olá falhado PCM tooprevent superaquecimento.</span><span class="sxs-lookup"><span data-stu-id="456aa-122">PCM module replacement takes only few minutes toocomplete, but it must be completed within 10 minutes of removing hello failed PCM tooprevent overheating.</span></span>
* <span data-ttu-id="456aa-123">Note que Olá substituição 764 W PCM módulos enviados da fábrica de saudação não contém o módulo de bateria de backup hello.</span><span class="sxs-lookup"><span data-stu-id="456aa-123">Note that hello replacement 764 W PCM modules shipped from hello factory do not contain hello backup battery module.</span></span> <span data-ttu-id="456aa-124">Será necessário tooremove bateria de saudação do seu PCM com falha e, em seguida, inseri-lo em substituição do módulo anterior tooperforming saudação do hello substituição.</span><span class="sxs-lookup"><span data-stu-id="456aa-124">You will need tooremove hello battery from your faulty PCM and then insert it into hello replacement module prior tooperforming hello replacement.</span></span> <span data-ttu-id="456aa-125">Para obter mais informações, consulte como muito[remover e inserir um módulo de bateria de backup](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="456aa-125">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="456aa-126">Remover um PCM</span><span class="sxs-lookup"><span data-stu-id="456aa-126">Remove a PCM</span></span>
<span data-ttu-id="456aa-127">Siga estas instruções quando estiver pronto tooremove uma potência e o módulo de resfriamento (PCM) do seu dispositivo StorSimple do Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="456aa-127">Follow these instructions when you are ready tooremove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="456aa-128">Antes de remover o PCM, verifique se você tem uma substituição correta (764 W para o compartimento principal Olá) ou 580 W para Olá compartimento EBOD.</span><span class="sxs-lookup"><span data-stu-id="456aa-128">Before you remove your PCM, verify that you have a correct replacement (764 W for hello primary enclosure or 580 W for hello EBOD enclosure).</span></span>

#### <a name="tooremove-a-pcm"></a><span data-ttu-id="456aa-129">tooremove um PCM</span><span class="sxs-lookup"><span data-stu-id="456aa-129">tooremove a PCM</span></span>
1. <span data-ttu-id="456aa-130">No portal clássico do Azure do hello, clique em **Configurações > Monitor > integridade do Hardware**.</span><span class="sxs-lookup"><span data-stu-id="456aa-130">In hello Azure classic portal, click **Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="456aa-131">Verificar o status de saudação de componentes PCM Olá em **componentes compartilhados** tooidentify qual PCM falhou:</span><span class="sxs-lookup"><span data-stu-id="456aa-131">Check hello status of hello PCM components under **Shared components** tooidentify which PCM has failed:</span></span>
   
   * <span data-ttu-id="456aa-132">Se uma fonte de alimentação no PCM 0 falhou, Olá status de **fonte de alimentação no PCM 0** será vermelho.</span><span class="sxs-lookup"><span data-stu-id="456aa-132">If a power supply in PCM 0 has failed, hello status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="456aa-133">Se uma fonte de alimentação no PCM 1 tiver falhado, Olá status de **fonte de alimentação no PCM 1** será vermelho.</span><span class="sxs-lookup"><span data-stu-id="456aa-133">If a power supply in PCM 1 has failed, hello status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="456aa-134">Se o ventilador Olá no PCM 1 tiver falhado, Olá status de **resfriamento 0 para o PCM 0** ou **resfriamento 1 para o PCM 0** será vermelho.</span><span class="sxs-lookup"><span data-stu-id="456aa-134">If hello fan in PCM 1 has failed, hello status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="456aa-135">Localize Olá PCM com falha em Olá fazer do compartimento primário hello.</span><span class="sxs-lookup"><span data-stu-id="456aa-135">Locate hello failed PCM on hello back of hello primary enclosure.</span></span> <span data-ttu-id="456aa-136">Se você estiver executando um modelo 8600, identificar compartimento principal Olá examinando Olá número de identificação da unidade de sistema mostradas na exibição de LED do painel frontal Olá.</span><span class="sxs-lookup"><span data-stu-id="456aa-136">If you are running an 8600 model, identify hello primary enclosure by looking at hello System Unit Identification Number shown on hello front panel LED display.</span></span> <span data-ttu-id="456aa-137">Olá padrão é a ID de unidade exibida no compartimento primário Olá **00**, enquanto o saudação padrão ID de unidade exibida no compartimento EBOD de saudação é **01**.</span><span class="sxs-lookup"><span data-stu-id="456aa-137">hello default Unit ID displayed on hello primary enclosure is **00**, whereas hello default Unit ID displayed on hello EBOD enclosure is **01**.</span></span> <span data-ttu-id="456aa-138">Olá seguinte diagrama e tabela explicam painel frontal de saudação da exibição Olá LED.</span><span class="sxs-lookup"><span data-stu-id="456aa-138">hello following diagram and table explain hello front panel of hello LED display.</span></span>
   
    ![ID do sistema na no painel de operações frontal](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="456aa-140">**Figura 1** painel frontal do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="456aa-140">**Figure 1** Front panel of hello device</span></span>  
   
   | <span data-ttu-id="456aa-141">Rótulo</span><span class="sxs-lookup"><span data-stu-id="456aa-141">Label</span></span> | <span data-ttu-id="456aa-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="456aa-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="456aa-143">1</span><span class="sxs-lookup"><span data-stu-id="456aa-143">1</span></span> |<span data-ttu-id="456aa-144">Botão silenciar</span><span class="sxs-lookup"><span data-stu-id="456aa-144">Mute button</span></span> |
   | <span data-ttu-id="456aa-145">2</span><span class="sxs-lookup"><span data-stu-id="456aa-145">2</span></span> |<span data-ttu-id="456aa-146">Energia do sistema</span><span class="sxs-lookup"><span data-stu-id="456aa-146">System power</span></span> |
   | <span data-ttu-id="456aa-147">3</span><span class="sxs-lookup"><span data-stu-id="456aa-147">3</span></span> |<span data-ttu-id="456aa-148">Falha do módulo</span><span class="sxs-lookup"><span data-stu-id="456aa-148">Module fault</span></span> |
   | <span data-ttu-id="456aa-149">4</span><span class="sxs-lookup"><span data-stu-id="456aa-149">4</span></span> |<span data-ttu-id="456aa-150">Falha lógica</span><span class="sxs-lookup"><span data-stu-id="456aa-150">Logical fault</span></span> |
   | <span data-ttu-id="456aa-151">5</span><span class="sxs-lookup"><span data-stu-id="456aa-151">5</span></span> |<span data-ttu-id="456aa-152">Exibição da ID da unidade</span><span class="sxs-lookup"><span data-stu-id="456aa-152">Unit ID display</span></span> |
3. <span data-ttu-id="456aa-153">Olá LEDs indicadores no hello parte traseira do compartimento principal Olá de monitoramento também pode ser usado tooidentify Olá PCM com falha.</span><span class="sxs-lookup"><span data-stu-id="456aa-153">hello monitoring indicator LEDs in hello back of hello primary enclosure can also be used tooidentify hello faulty PCM.</span></span> <span data-ttu-id="456aa-154">Consulte Olá seguinte diagrama e tabela toounderstand como toouse Olá LEDs toolocate Olá PCM com falha.</span><span class="sxs-lookup"><span data-stu-id="456aa-154">See hello following diagram and table toounderstand how toouse hello LEDs toolocate hello faulty PCM.</span></span> <span data-ttu-id="456aa-155">Por exemplo, se hello LED correspondente toohello **falha do ventilador** estiver aceso, Olá ventilador falhou.</span><span class="sxs-lookup"><span data-stu-id="456aa-155">For example, if hello LED corresponding toohello **Fan Fail** is lit, hello fan has failed.</span></span> <span data-ttu-id="456aa-156">Da mesma forma, se hello LED correspondente muito**falha de CA** estiver aceso, Olá alimentação falhou.</span><span class="sxs-lookup"><span data-stu-id="456aa-156">Likewise, if hello LED corresponding too**AC Fail** is lit, hello power supply has failed.</span></span> 
   
    ![Backplane dos LEDs indicadores de monitoramento de PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="456aa-158">**Figura 2** Parte posterior do PCM com LEDs indicadores</span><span class="sxs-lookup"><span data-stu-id="456aa-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="456aa-159">Rótulo</span><span class="sxs-lookup"><span data-stu-id="456aa-159">Label</span></span> | <span data-ttu-id="456aa-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="456aa-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="456aa-161">1</span><span class="sxs-lookup"><span data-stu-id="456aa-161">1</span></span> |<span data-ttu-id="456aa-162">Falha de energia CA</span><span class="sxs-lookup"><span data-stu-id="456aa-162">AC power failure</span></span> |
   | <span data-ttu-id="456aa-163">2</span><span class="sxs-lookup"><span data-stu-id="456aa-163">2</span></span> |<span data-ttu-id="456aa-164">Falha do ventilador</span><span class="sxs-lookup"><span data-stu-id="456aa-164">Fan failure</span></span> |
   | <span data-ttu-id="456aa-165">3</span><span class="sxs-lookup"><span data-stu-id="456aa-165">3</span></span> |<span data-ttu-id="456aa-166">Falha de bateria</span><span class="sxs-lookup"><span data-stu-id="456aa-166">Battery fault</span></span> |
   | <span data-ttu-id="456aa-167">4</span><span class="sxs-lookup"><span data-stu-id="456aa-167">4</span></span> |<span data-ttu-id="456aa-168">PCM OK</span><span class="sxs-lookup"><span data-stu-id="456aa-168">PCM OK</span></span> |
   | <span data-ttu-id="456aa-169">5</span><span class="sxs-lookup"><span data-stu-id="456aa-169">5</span></span> |<span data-ttu-id="456aa-170">Falha de energia CC</span><span class="sxs-lookup"><span data-stu-id="456aa-170">DC power failure</span></span> |
   | <span data-ttu-id="456aa-171">6</span><span class="sxs-lookup"><span data-stu-id="456aa-171">6</span></span> |<span data-ttu-id="456aa-172">Bateria íntegra</span><span class="sxs-lookup"><span data-stu-id="456aa-172">Battery healthy</span></span> |
4. <span data-ttu-id="456aa-173">Consulte toohello diagrama de saudação parte posterior do módulo do PCM Olá StorSimple dispositivo toolocate Olá falhado a seguir.</span><span class="sxs-lookup"><span data-stu-id="456aa-173">Refer toohello following diagram of hello back of hello StorSimple device toolocate hello failed PCM module.</span></span> <span data-ttu-id="456aa-174">PCM 0 está Olá esquerda e PCM 1 está saudação à direita.</span><span class="sxs-lookup"><span data-stu-id="456aa-174">PCM 0 is on hello left and PCM 1 is on hello right.</span></span> <span data-ttu-id="456aa-175">tabela Olá a seguir explica módulos hello.</span><span class="sxs-lookup"><span data-stu-id="456aa-175">hello table that follows explains hello modules.</span></span>
   
     ![Backplane dos módulos do compartimento primário do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="456aa-177">**Figura 3** Parte traseira do dispositivo com módulos de plug-in</span><span class="sxs-lookup"><span data-stu-id="456aa-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="456aa-178">Rótulo</span><span class="sxs-lookup"><span data-stu-id="456aa-178">Label</span></span> | <span data-ttu-id="456aa-179">Descrição</span><span class="sxs-lookup"><span data-stu-id="456aa-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="456aa-180">1</span><span class="sxs-lookup"><span data-stu-id="456aa-180">1</span></span> |<span data-ttu-id="456aa-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="456aa-181">PCM 0</span></span> |
   | <span data-ttu-id="456aa-182">2</span><span class="sxs-lookup"><span data-stu-id="456aa-182">2</span></span> |<span data-ttu-id="456aa-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="456aa-183">PCM 1</span></span> |
   | <span data-ttu-id="456aa-184">3</span><span class="sxs-lookup"><span data-stu-id="456aa-184">3</span></span> |<span data-ttu-id="456aa-185">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="456aa-185">Controller 0</span></span> |
   | <span data-ttu-id="456aa-186">4</span><span class="sxs-lookup"><span data-stu-id="456aa-186">4</span></span> |<span data-ttu-id="456aa-187">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="456aa-187">Controller 1</span></span> |
5. <span data-ttu-id="456aa-188">Ativar logoff Olá PCM com falha e desconecte o cabo da fonte de alimentação hello.</span><span class="sxs-lookup"><span data-stu-id="456aa-188">Turn off hello faulty PCM and disconnect hello power supply cord.</span></span> <span data-ttu-id="456aa-189">Agora você pode remover Olá PCM.</span><span class="sxs-lookup"><span data-stu-id="456aa-189">You can now remove hello PCM.</span></span>
6. <span data-ttu-id="456aa-190">Segure a trava hello e Olá da saudação PCM tratar entre o polegar e o dedo indicador e pressione-as alça de saudação tooopen juntos.</span><span class="sxs-lookup"><span data-stu-id="456aa-190">Grasp hello latch and hello side of hello PCM handle between your thumb and forefinger, and squeeze them together tooopen hello handle.</span></span>
   
    ![Abrindo a alça do PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="456aa-192">**Figura 4** tratar Olá abertura PCM</span><span class="sxs-lookup"><span data-stu-id="456aa-192">**Figure 4** Opening hello PCM handle</span></span>
7. <span data-ttu-id="456aa-193">Segure a alça de saudação e remova Olá PCM.</span><span class="sxs-lookup"><span data-stu-id="456aa-193">Grip hello handle and remove hello PCM.</span></span>
   
    ![Removendo o PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="456aa-195">**Figura 5** Olá removendo PCM</span><span class="sxs-lookup"><span data-stu-id="456aa-195">**Figure 5** Removing hello PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="456aa-196">Instalar um PCM de reposição</span><span class="sxs-lookup"><span data-stu-id="456aa-196">Install a replacement PCM</span></span>
<span data-ttu-id="456aa-197">Siga essas instruções tooinstall um PCM no seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="456aa-197">Follow these instructions tooinstall a PCM in your StorSimple device.</span></span> <span data-ttu-id="456aa-198">Certifique-se de que você inseriu Olá bateria de backup anteriores tooinstalling Olá substituição do módulo de PCM (aplica-se too764 PCMs W).</span><span class="sxs-lookup"><span data-stu-id="456aa-198">Ensure that you have inserted hello backup battery module prior tooinstalling hello replacement PCM (applies too764 W PCMs only).</span></span> <span data-ttu-id="456aa-199">Para obter mais informações, consulte como muito[remover e inserir um módulo de bateria de backup](storsimple-8000-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="456aa-199">For more information, see how too[remove and insert a backup battery module](storsimple-8000-battery-replacement.md).</span></span>

#### <a name="tooinstall-a-pcm"></a><span data-ttu-id="456aa-200">tooinstall um PCM</span><span class="sxs-lookup"><span data-stu-id="456aa-200">tooinstall a PCM</span></span>
1. <span data-ttu-id="456aa-201">Verifique se você tem Olá PCM de substituição correto para esse compartimento.</span><span class="sxs-lookup"><span data-stu-id="456aa-201">Verify that you have hello correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="456aa-202">compartimento principal Olá precisa de um PCM de 764 W e Olá compartimento EBOD precisa de um PCM de 580 W.</span><span class="sxs-lookup"><span data-stu-id="456aa-202">hello primary enclosure needs a 764 W PCM and hello EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="456aa-203">Não tente toouse Olá PCM de 580 W no compartimento primário hello, ou Olá PCM de 764 W em Olá compartimento EBOD.</span><span class="sxs-lookup"><span data-stu-id="456aa-203">You should not attempt toouse hello 580 W PCM in hello Primary enclosure, or hello 764 W PCM in hello EBOD enclosure.</span></span> <span data-ttu-id="456aa-204">Olá a imagem a seguir mostra onde tooidentify essas informações em Olá rótulo que é afixada toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="456aa-204">hello following image shows where tooidentify this information on hello label that is affixed toohello PCM.</span></span>
   
    ![Etiqueta do PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="456aa-206">**Figura 6** Etiqueta do PCM</span><span class="sxs-lookup"><span data-stu-id="456aa-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="456aa-207">Verifique se há compartimento de toohello dano, prestando atenção especial toohello conectores.</span><span class="sxs-lookup"><span data-stu-id="456aa-207">Check for damage toohello enclosure, paying particular attention toohello connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="456aa-208">**Não instale o módulo de saudação se os pinos do conector estiver torto.**</span><span class="sxs-lookup"><span data-stu-id="456aa-208">**Do not install hello module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="456aa-209">Com hello PCM manipular Olá abra posição, módulo de saudação do slide para compartimento de saudação.</span><span class="sxs-lookup"><span data-stu-id="456aa-209">With hello PCM handle in hello open position, slide hello module into hello enclosure.</span></span>
   
    ![Instalando o PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="456aa-211">**Figura 7** Olá instalando PCM</span><span class="sxs-lookup"><span data-stu-id="456aa-211">**Figure 7** Installing hello PCM</span></span>
4. <span data-ttu-id="456aa-212">Feche manualmente a alça do PCM hello.</span><span class="sxs-lookup"><span data-stu-id="456aa-212">Manually close hello PCM handle.</span></span> <span data-ttu-id="456aa-213">Você ouvirá um clique quando Olá trava da alça encaixar.</span><span class="sxs-lookup"><span data-stu-id="456aa-213">You should hear a click as hello handle latch engages.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="456aa-214">tooensure que Olá pinos do conector estão encaixados, puxe levemente no identificador de saudação sem soltar a trava hello.</span><span class="sxs-lookup"><span data-stu-id="456aa-214">tooensure that hello connector pins have engaged, you can gently tug on hello handle without releasing hello latch.</span></span> <span data-ttu-id="456aa-215">Se Olá PCM Deslizar para fora, significa que Olá trava fechou antes do conectores Olá envolvido.</span><span class="sxs-lookup"><span data-stu-id="456aa-215">If hello PCM slides out, it implies that hello latch was closed before hello connectors engaged.</span></span>
   
5. <span data-ttu-id="456aa-216">Conecte a fonte de alimentação Olá power cabos toohello e toohello PCM.</span><span class="sxs-lookup"><span data-stu-id="456aa-216">Connect hello power cables toohello power source and toohello PCM.</span></span>
6. <span data-ttu-id="456aa-217">Proteja a tensão Olá alívio de tensão.</span><span class="sxs-lookup"><span data-stu-id="456aa-217">Secure hello strain relief bales.</span></span>
7. <span data-ttu-id="456aa-218">Ative Olá PCM.</span><span class="sxs-lookup"><span data-stu-id="456aa-218">Turn on hello PCM.</span></span>
8. <span data-ttu-id="456aa-219">Verificar se a substituição de saudação foi bem-sucedida: no hello portal do Azure do seu serviço de Gerenciador de dispositivos de StorSimple, navegue tooyour dispositivo e, em seguida, muito**Configurações > Monitor > integridade do Hardware**.</span><span class="sxs-lookup"><span data-stu-id="456aa-219">Verify that hello replacement was successful: in hello Azure portal of your StorSimple Device Manager service, navigate tooyour device and then too**Settings > Monitor > Hardware health**.</span></span> <span data-ttu-id="456aa-220">Em Olá **componentes compartilhados**, status de saudação do hello PCM deve estar verde.</span><span class="sxs-lookup"><span data-stu-id="456aa-220">Under hello **Shared components**, hello status of hello PCM should be green.</span></span>
   
   > [!NOTE]
   > <span data-ttu-id="456aa-221">Ele pode levar alguns minutos para inicializar de toocompletely PCM de substituição de saudação.</span><span class="sxs-lookup"><span data-stu-id="456aa-221">It may take a few minutes for hello replacement PCM toocompletely initialize.</span></span>

## <a name="next-steps"></a><span data-ttu-id="456aa-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="456aa-222">Next steps</span></span>
<span data-ttu-id="456aa-223">Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-8000-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="456aa-223">Learn more about [StorSimple hardware component replacement](storsimple-8000-hardware-component-replacement.md).</span></span>

