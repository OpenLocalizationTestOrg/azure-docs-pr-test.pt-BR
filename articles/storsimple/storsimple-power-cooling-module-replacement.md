---
title: Substituir um PCM em seu dispositivo StorSimple | Microsoft Docs
description: "Explica como remover e substituir módulo de energia e resfriamento (PCM) em seu dispositivo StorSimple"
services: storsimple
documentationcenter: 
author: alkohli
manager: carmonm
editor: 
ms.assetid: 24a158cb-0b79-4908-bb5a-431e48760f6a
ms.service: storsimple
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: TBD
ms.date: 08/18/2016
ms.author: alkohli
ms.openlocfilehash: 2a956de58b279a013913631a077d7b03c6327f72
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="replace-a-power-and-cooling-module-on-your-storsimple-device"></a><span data-ttu-id="fcf5c-103">Substituir um módulo de energia e resfriamento em seu dispositivo StorSimple</span><span class="sxs-lookup"><span data-stu-id="fcf5c-103">Replace a Power and Cooling Module on your StorSimple device</span></span>
## <a name="overview"></a><span data-ttu-id="fcf5c-104">Visão geral</span><span class="sxs-lookup"><span data-stu-id="fcf5c-104">Overview</span></span>
<span data-ttu-id="fcf5c-105">O módulo de energia e resfriamento (PCM) em seu dispositivo Microsoft Azure StorSimple consiste em uma fonte de alimentação e ventiladores que são controlados por meio de compartimentos primário e EBOD.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-105">The Power and Cooling Module (PCM) in your Microsoft Azure StorSimple device consists of a power supply and cooling fans that are controlled through the primary and EBOD enclosures.</span></span> <span data-ttu-id="fcf5c-106">Há apenas um modelo de PCM que é certificado para cada compartimento.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-106">There is only one model of PCM that is certified for each enclosure.</span></span> <span data-ttu-id="fcf5c-107">O compartimento primário é certificado para um PCM de 764 W e o compartimento EBOD é certificado para um PCM de 580 W.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-107">The primary enclosure is certified for a 764 W PCM and the EBOD enclosure is certified for a 580 W PCM.</span></span> <span data-ttu-id="fcf5c-108">Embora os PCMs do compartimento primário e do compartimento EBOD sejam diferentes, o procedimento de substituição é idêntico.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-108">Although the PCMs for the primary enclosure and the EBOD enclosure are different, the replacement procedure is identical.</span></span>

<span data-ttu-id="fcf5c-109">Este tutorial explica como:</span><span class="sxs-lookup"><span data-stu-id="fcf5c-109">This tutorial explains how to:</span></span>

* <span data-ttu-id="fcf5c-110">Remover um PCM</span><span class="sxs-lookup"><span data-stu-id="fcf5c-110">Remove a PCM</span></span>
* <span data-ttu-id="fcf5c-111">Instalar um PCM de reposição</span><span class="sxs-lookup"><span data-stu-id="fcf5c-111">Install a replacement PCM</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcf5c-112">Antes de remover e substituir um PCM, examine as informações de segurança em [Substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="fcf5c-112">Before removing and replacing a PCM, review the safety information in [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>
> 
> 

## <a name="before-you-replace-a-pcm"></a><span data-ttu-id="fcf5c-113">Antes de substituir um PCM</span><span class="sxs-lookup"><span data-stu-id="fcf5c-113">Before you replace a PCM</span></span>
<span data-ttu-id="fcf5c-114">Esteja ciente das seguintes questões importantes antes de substituir o PCM:</span><span class="sxs-lookup"><span data-stu-id="fcf5c-114">Be aware of the following important issues before you replace your PCM:</span></span>

* <span data-ttu-id="fcf5c-115">Se a fonte de alimentação do PCM falhar, deixe o módulo com defeito instalado, mas remova o cabo de alimentação.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-115">If the power supply of the PCM fails, leave the faulty module installed, but remove the power cord.</span></span> <span data-ttu-id="fcf5c-116">O ventilador continuará a receber energia do compartimento e continuará a fornecer resfriamento adequado.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-116">The fan will continue to receive power from the enclosure and continue to provide proper cooling.</span></span> <span data-ttu-id="fcf5c-117">Se o ventilador falhar, o PCM precisa ser trocado imediatamente.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-117">If the fan fails, the PCM needs to be replaced immediately.</span></span>
* <span data-ttu-id="fcf5c-118">Antes de remover o PCM, desconecte o PCM desativando o interruptor principal (se houver) ou removendo fisicamente o cabo de alimentação.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-118">Before removing the PCM, disconnect the power from the PCM by turning off the main switch (where present) or by physically removing the power cord.</span></span> <span data-ttu-id="fcf5c-119">Isso avisa o sistema que um desligamento da energia é iminente.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-119">This provides a warning to your system that a power shutdown is imminent.</span></span>
* <span data-ttu-id="fcf5c-120">Certifique-se de que outros PCM estejam funcionando para que o sistema continue em operação antes de substituir o PCM defeituoso.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-120">Make sure that the other PCM is functional for continued system operation before replacing the faulty PCM.</span></span> <span data-ttu-id="fcf5c-121">Um PCM defeituoso deve ser substituído por um PCM totalmente operacional assim que possível.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-121">A faulty PCM must be replaced by a fully operational PCM as soon as possible.</span></span>
* <span data-ttu-id="fcf5c-122">A substituição do módulo PCM leva apenas alguns minutos para ser concluída, mas precisa ser concluída em até 10 minutos após remover o PCM com falha para evitar superaquecimento.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-122">PCM module replacement takes only few minutes to complete, but it must be completed within 10 minutes of removing the failed PCM to prevent overheating.</span></span>
* <span data-ttu-id="fcf5c-123">Observe que os módulos de substituição PCM de 764 W enviados da fábrica não contêm o módulo de bateria de backup.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-123">Note that the replacement 764 W PCM modules shipped from the factory do not contain the backup battery module.</span></span> <span data-ttu-id="fcf5c-124">Você precisará remover a bateria do seu PCM com falha e, então, inseri-la no módulo de substituição antes de executar a substituição.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-124">You will need to remove the battery from your faulty PCM and then insert it into the replacement module prior to performing the replacement.</span></span> <span data-ttu-id="fcf5c-125">Para obter mais informações, confira como [remover e inserir um módulo de bateria de backup](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="fcf5c-125">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

## <a name="remove-a-pcm"></a><span data-ttu-id="fcf5c-126">Remover um PCM</span><span class="sxs-lookup"><span data-stu-id="fcf5c-126">Remove a PCM</span></span>
<span data-ttu-id="fcf5c-127">Siga estas instruções quando estiver pronto para remover um módulo de energia e resfriamento (PCM) do dispositivo Microsoft Azure StorSimple.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-127">Follow these instructions when you are ready to remove a Power and Cooling Module (PCM) from your Microsoft Azure StorSimple device.</span></span>

> [!NOTE]
> <span data-ttu-id="fcf5c-128">Antes de remover o PCM, verifique se você tem uma peça de reposição correta (764 W para o compartimento primário ou 580 W para o compartimento EBOD).</span><span class="sxs-lookup"><span data-stu-id="fcf5c-128">Before you remove your PCM, verify that you have a correct replacement (764 W for the primary enclosure or 580 W for the EBOD enclosure).</span></span>
> 
> 

#### <a name="to-remove-a-pcm"></a><span data-ttu-id="fcf5c-129">Para remover um PCM</span><span class="sxs-lookup"><span data-stu-id="fcf5c-129">To remove a PCM</span></span>
1. <span data-ttu-id="fcf5c-130">No Portal clássico do Azure, clique em **Dispositivos** > **Manutenção** > **Status de Hardware**.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-130">In the Azure classic portal, click **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="fcf5c-131">Verifique o status dos componentes do PCM em **Componentes compartilhados** para identificar qual PCM falhou:</span><span class="sxs-lookup"><span data-stu-id="fcf5c-131">Check the status of the PCM components under **Shared Components** to identify which PCM has failed:</span></span>
   
   * <span data-ttu-id="fcf5c-132">Se uma fonte de alimentação no PCM 0 tiver falhado, o status da **Fonte de Alimentação no PCM 0** ficará vermelho.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-132">If a power supply in PCM 0 has failed, the status of **Power Supply in PCM 0** will be red.</span></span>
   * <span data-ttu-id="fcf5c-133">Se uma fonte de alimentação no PCM 1 tiver falhado, o status da **Fonte de Alimentação no PCM 1** ficará vermelho.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-133">If a power supply in PCM 1 has failed, the status of **Power Supply in PCM 1** will be red.</span></span>
   * <span data-ttu-id="fcf5c-134">Se houve falha no ventilador do PCM 1, o status do **Resfriamento 0 do PCM 0** ou do **Resfriamento 1 do PCM 0** ficará vermelho.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-134">If the fan in PCM 1 has failed, the status of either **Cooling 0 for PCM 0** or **Cooling 1 for PCM 0** will be red.</span></span>
2. <span data-ttu-id="fcf5c-135">Localize o PCM com falha na parte traseira do compartimento primário.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-135">Locate the failed PCM on the back of the primary enclosure.</span></span> <span data-ttu-id="fcf5c-136">Se você estiver executando um modelo 8600, identifique o compartimento primário examinando o número de identificação da unidade do sistema no display de LED do painel frontal.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-136">If you are running an 8600 model, identify the primary enclosure by looking at the System Unit Identification Number shown on the front panel LED display.</span></span> <span data-ttu-id="fcf5c-137">A ID de unidade padrão exibida no compartimento primário é **00**, enquanto que a ID de unidade padrão exibida no compartimento EBOD é **01**.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-137">The default Unit ID displayed on the primary enclosure is **00**, whereas the default Unit ID displayed on the EBOD enclosure is **01**.</span></span> <span data-ttu-id="fcf5c-138">O diagrama e a tabela a seguir explicam o painel frontal do display de LED.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-138">The following diagram and table explain the front panel of the LED display.</span></span>
   
    ![ID do sistema na no painel de operações frontal](./media/storsimple-power-cooling-module-replacement/IC740991.png)
   
     <span data-ttu-id="fcf5c-140">**Figura 1** Parte frontal do dispositivo</span><span class="sxs-lookup"><span data-stu-id="fcf5c-140">**Figure 1** Front panel of the device</span></span>  
   
   | <span data-ttu-id="fcf5c-141">Rótulo</span><span class="sxs-lookup"><span data-stu-id="fcf5c-141">Label</span></span> | <span data-ttu-id="fcf5c-142">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcf5c-142">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="fcf5c-143">1</span><span class="sxs-lookup"><span data-stu-id="fcf5c-143">1</span></span> |<span data-ttu-id="fcf5c-144">Botão silenciar</span><span class="sxs-lookup"><span data-stu-id="fcf5c-144">Mute button</span></span> |
   | <span data-ttu-id="fcf5c-145">2</span><span class="sxs-lookup"><span data-stu-id="fcf5c-145">2</span></span> |<span data-ttu-id="fcf5c-146">Energia do sistema</span><span class="sxs-lookup"><span data-stu-id="fcf5c-146">System power</span></span> |
   | <span data-ttu-id="fcf5c-147">3</span><span class="sxs-lookup"><span data-stu-id="fcf5c-147">3</span></span> |<span data-ttu-id="fcf5c-148">Falha do módulo</span><span class="sxs-lookup"><span data-stu-id="fcf5c-148">Module fault</span></span> |
   | <span data-ttu-id="fcf5c-149">4</span><span class="sxs-lookup"><span data-stu-id="fcf5c-149">4</span></span> |<span data-ttu-id="fcf5c-150">Falha lógica</span><span class="sxs-lookup"><span data-stu-id="fcf5c-150">Logical fault</span></span> |
   | <span data-ttu-id="fcf5c-151">5</span><span class="sxs-lookup"><span data-stu-id="fcf5c-151">5</span></span> |<span data-ttu-id="fcf5c-152">Exibição da ID da unidade</span><span class="sxs-lookup"><span data-stu-id="fcf5c-152">Unit ID display</span></span> |
3. <span data-ttu-id="fcf5c-153">Os LEDs indicadores de monitoramento na parte traseira do compartimento primário também podem ser usado para identificar o PCM defeituoso.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-153">The monitoring indicator LEDs in the back of the primary enclosure can also be used to identify the faulty PCM.</span></span> <span data-ttu-id="fcf5c-154">Consulte o diagrama e a tabela a seguir para entender como usar os LEDs para localizar o PCM defeituoso.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-154">See the following diagram and table to understand how to use the LEDs to locate the faulty PCM.</span></span> <span data-ttu-id="fcf5c-155">Por exemplo, se o LED correspondente à **Falha do Ventilador** estiver aceso, houve falha no ventilador.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-155">For example, if the LED corresponding to the **Fan Fail** is lit, the fan has failed.</span></span> <span data-ttu-id="fcf5c-156">Da mesma forma, se o LED correspondente à **Falha de CA** estiver aceso, a fonte de alimentação falhou.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-156">Likewise, if the LED corresponding to **AC Fail** is lit, the power supply has failed.</span></span> 
   
    ![Backplane dos LEDs indicadores de monitoramento de PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740992.png)
   
     <span data-ttu-id="fcf5c-158">**Figura 2** Parte posterior do PCM com LEDs indicadores</span><span class="sxs-lookup"><span data-stu-id="fcf5c-158">**Figure 2** Back of PCM with indicator LEDs</span></span>
   
   | <span data-ttu-id="fcf5c-159">Rótulo</span><span class="sxs-lookup"><span data-stu-id="fcf5c-159">Label</span></span> | <span data-ttu-id="fcf5c-160">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcf5c-160">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="fcf5c-161">1</span><span class="sxs-lookup"><span data-stu-id="fcf5c-161">1</span></span> |<span data-ttu-id="fcf5c-162">Falha de energia CA</span><span class="sxs-lookup"><span data-stu-id="fcf5c-162">AC power failure</span></span> |
   | <span data-ttu-id="fcf5c-163">2</span><span class="sxs-lookup"><span data-stu-id="fcf5c-163">2</span></span> |<span data-ttu-id="fcf5c-164">Falha do ventilador</span><span class="sxs-lookup"><span data-stu-id="fcf5c-164">Fan failure</span></span> |
   | <span data-ttu-id="fcf5c-165">3</span><span class="sxs-lookup"><span data-stu-id="fcf5c-165">3</span></span> |<span data-ttu-id="fcf5c-166">Falha de bateria</span><span class="sxs-lookup"><span data-stu-id="fcf5c-166">Battery fault</span></span> |
   | <span data-ttu-id="fcf5c-167">4</span><span class="sxs-lookup"><span data-stu-id="fcf5c-167">4</span></span> |<span data-ttu-id="fcf5c-168">PCM OK</span><span class="sxs-lookup"><span data-stu-id="fcf5c-168">PCM OK</span></span> |
   | <span data-ttu-id="fcf5c-169">5</span><span class="sxs-lookup"><span data-stu-id="fcf5c-169">5</span></span> |<span data-ttu-id="fcf5c-170">Falha de energia CC</span><span class="sxs-lookup"><span data-stu-id="fcf5c-170">DC power failure</span></span> |
   | <span data-ttu-id="fcf5c-171">6</span><span class="sxs-lookup"><span data-stu-id="fcf5c-171">6</span></span> |<span data-ttu-id="fcf5c-172">Bateria íntegra</span><span class="sxs-lookup"><span data-stu-id="fcf5c-172">Battery healthy</span></span> |
4. <span data-ttu-id="fcf5c-173">Consulte o diagrama a seguir da parte traseira do dispositivo StorSimple para localizar o módulo de PCM com falha.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-173">Refer to the following diagram of the back of the StorSimple device to locate the failed PCM module.</span></span> <span data-ttu-id="fcf5c-174">PCM 0 está à esquerda e PCM 1 está à direita.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-174">PCM 0 is on the left and PCM 1 is on the right.</span></span> <span data-ttu-id="fcf5c-175">A tabela a seguir explica os módulos.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-175">The table that follows explains the modules.</span></span>
   
     ![Backplane dos módulos do compartimento primário do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740994.png)
   
     <span data-ttu-id="fcf5c-177">**Figura 3** Parte traseira do dispositivo com módulos de plug-in</span><span class="sxs-lookup"><span data-stu-id="fcf5c-177">**Figure 3** Back of device with plug-in modules</span></span> 
   
   | <span data-ttu-id="fcf5c-178">Rótulo</span><span class="sxs-lookup"><span data-stu-id="fcf5c-178">Label</span></span> | <span data-ttu-id="fcf5c-179">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcf5c-179">Description</span></span> |
   |:--- |:--- |
   | <span data-ttu-id="fcf5c-180">1</span><span class="sxs-lookup"><span data-stu-id="fcf5c-180">1</span></span> |<span data-ttu-id="fcf5c-181">PCM 0</span><span class="sxs-lookup"><span data-stu-id="fcf5c-181">PCM 0</span></span> |
   | <span data-ttu-id="fcf5c-182">2</span><span class="sxs-lookup"><span data-stu-id="fcf5c-182">2</span></span> |<span data-ttu-id="fcf5c-183">PCM 1</span><span class="sxs-lookup"><span data-stu-id="fcf5c-183">PCM 1</span></span> |
   | <span data-ttu-id="fcf5c-184">3</span><span class="sxs-lookup"><span data-stu-id="fcf5c-184">3</span></span> |<span data-ttu-id="fcf5c-185">Controlador 0</span><span class="sxs-lookup"><span data-stu-id="fcf5c-185">Controller 0</span></span> |
   | <span data-ttu-id="fcf5c-186">4</span><span class="sxs-lookup"><span data-stu-id="fcf5c-186">4</span></span> |<span data-ttu-id="fcf5c-187">Controlador 1</span><span class="sxs-lookup"><span data-stu-id="fcf5c-187">Controller 1</span></span> |
5. <span data-ttu-id="fcf5c-188">Desative o PCM defeituoso e desconecte o cabo da fonte de alimentação.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-188">Turn off the faulty PCM and disconnect the power supply cord.</span></span> <span data-ttu-id="fcf5c-189">Agora você pode remover o PCM.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-189">You can now remove the PCM.</span></span>
6. <span data-ttu-id="fcf5c-190">Segure a trava e o lado da alça do PCM entre o polegar e o dedo indicador e aperte-os para abrir a alça.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-190">Grasp the latch and the side of the PCM handle between your thumb and forefinger, and squeeze them together to open the handle.</span></span>
   
    ![Abrindo a alça do PCM](./media/storsimple-power-cooling-module-replacement/IC740995.png)
   
    <span data-ttu-id="fcf5c-192">**Figura 4** Abertura da alça do PCM</span><span class="sxs-lookup"><span data-stu-id="fcf5c-192">**Figure 4** Opening the PCM handle</span></span>
7. <span data-ttu-id="fcf5c-193">Segure a alça e remova o PCM.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-193">Grip the handle and remove the PCM.</span></span>
   
    ![Removendo o PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740996.png)
   
    <span data-ttu-id="fcf5c-195">**Figura 5** Removendo o PCM</span><span class="sxs-lookup"><span data-stu-id="fcf5c-195">**Figure 5** Removing the PCM</span></span>

## <a name="install-a-replacement-pcm"></a><span data-ttu-id="fcf5c-196">Instalar um PCM de reposição</span><span class="sxs-lookup"><span data-stu-id="fcf5c-196">Install a replacement PCM</span></span>
<span data-ttu-id="fcf5c-197">Siga estas instruções para instalar um PCM em seu dispositivo StorSimple.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-197">Follow these instructions to install a PCM in your StorSimple device.</span></span> <span data-ttu-id="fcf5c-198">Certifique-se de que você inseriu o módulo de bateria de backup antes de instalar o PCM de substituição (aplicável somente aos PCMs de 764 W).</span><span class="sxs-lookup"><span data-stu-id="fcf5c-198">Ensure that you have inserted the backup battery module prior to installing the replacement PCM (applies to 764 W PCMs only).</span></span> <span data-ttu-id="fcf5c-199">Para obter mais informações, confira como [remover e inserir um módulo de bateria de backup](storsimple-battery-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="fcf5c-199">For more information, see how to [remove and insert a backup battery module](storsimple-battery-replacement.md).</span></span>

#### <a name="to-install-a-pcm"></a><span data-ttu-id="fcf5c-200">Para instalar um PCM</span><span class="sxs-lookup"><span data-stu-id="fcf5c-200">To install a PCM</span></span>
1. <span data-ttu-id="fcf5c-201">Verifique se possui a peça de reposição do PCM para esse compartimento.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-201">Verify that you have the correct replacement PCM for this enclosure.</span></span> <span data-ttu-id="fcf5c-202">O compartimento primário necessita de um PCM de 764 W e o compartimento EBOD necessita de um PCM de 580 W.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-202">The primary enclosure needs a 764 W PCM and the EBOD enclosure needs a 580 W PCM.</span></span> <span data-ttu-id="fcf5c-203">Você não deve tentar usar o PCM de 580 W no compartimento primário nem o PCM de 764 W no compartimento EBOD.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-203">You should not attempt to use the 580 W PCM in the Primary enclosure, or the 764 W PCM in the EBOD enclosure.</span></span> <span data-ttu-id="fcf5c-204">A imagem a seguir mostra onde identificar essas informações na etiqueta do PCM.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-204">The following image shows where to identify this information on the label that is affixed to the PCM.</span></span>
   
    ![Etiqueta do PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740973.png)
   
    <span data-ttu-id="fcf5c-206">**Figura 6** Etiqueta do PCM</span><span class="sxs-lookup"><span data-stu-id="fcf5c-206">**Figure 6** PCM label</span></span>
2. <span data-ttu-id="fcf5c-207">Verifique se há danos no compartimento, prestando muita atenção aos conectores.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-207">Check for damage to the enclosure, paying particular attention to the connectors.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="fcf5c-208">**Não instale o módulo se algum pino do conector estiver torto.**</span><span class="sxs-lookup"><span data-stu-id="fcf5c-208">**Do not install the module if any connector pins are bent.**</span></span>
   > 
   > 
3. <span data-ttu-id="fcf5c-209">Com a alça do PCM na posição aberta, deslize o módulo para dentro do compartimento.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-209">With the PCM handle in the open position, slide the module into the enclosure.</span></span>
   
    ![Instalando o PCM do dispositivo](./media/storsimple-power-cooling-module-replacement/IC740975.png)
   
    <span data-ttu-id="fcf5c-211">**Figura 7** Instalando o PCM</span><span class="sxs-lookup"><span data-stu-id="fcf5c-211">**Figure 7** Installing the PCM</span></span>
4. <span data-ttu-id="fcf5c-212">Feche manualmente a alça do PCM.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-212">Manually close the PCM handle.</span></span> <span data-ttu-id="fcf5c-213">Você deve ouvir um clique ao encaixar a trava da alça.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-213">You should hear a click as the handle latch engages.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="fcf5c-214">Para garantir que os pinos do conector tenham encaixado, com cuidado, puxe a alça sem soltar a trava.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-214">To ensure that the connector pins have engaged, you can gently tug on the handle without releasing the latch.</span></span> <span data-ttu-id="fcf5c-215">Se o PCM deslizar, isso significa que a trava foi fechada antes que os conectores encaixassem.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-215">If the PCM slides out, it implies that the latch was closed before the connectors engaged.</span></span>
   > 
   > 
5. <span data-ttu-id="fcf5c-216">Conecte os cabos de energia na fonte de alimentação e no PCM.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-216">Connect the power cables to the power source and to the PCM.</span></span>
6. <span data-ttu-id="fcf5c-217">Proteja os ganchos de alívio de tensão.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-217">Secure the strain relief bales.</span></span> 
7. <span data-ttu-id="fcf5c-218">Ligue o PCM.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-218">Turn on the PCM.</span></span>
8. <span data-ttu-id="fcf5c-219">Verifique se a substituição foi bem-sucedida: no Portal clássico do Azure do seu serviço StorSimple Manager, navegue até **Dispositivos** > **Manutenção** > **Status de Hardware**.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-219">Verify that the replacement was successful: in the Azure classic portal of your StorSimple Manager service, navigate to **Devices** > **Maintenance** > **Hardware Status**.</span></span> <span data-ttu-id="fcf5c-220">Em **Componentes Compartilhados**, o status do PCM deverá estar verde.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-220">Under **Shared Components**, the status of the PCM should be green.</span></span> 
   
   > [!NOTE]
   > <span data-ttu-id="fcf5c-221">Pode levar alguns minutos até que o PCM de reposição esteja completamente inicializado.</span><span class="sxs-lookup"><span data-stu-id="fcf5c-221">It may take a few minutes for the replacement PCM to completely initialize.</span></span>
   > 
   > 

## <a name="next-steps"></a><span data-ttu-id="fcf5c-222">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fcf5c-222">Next steps</span></span>
<span data-ttu-id="fcf5c-223">Saiba mais sobre [substituição de componentes de hardware do StorSimple](storsimple-hardware-component-replacement.md).</span><span class="sxs-lookup"><span data-stu-id="fcf5c-223">Learn more about [StorSimple hardware component replacement](storsimple-hardware-component-replacement.md).</span></span>

