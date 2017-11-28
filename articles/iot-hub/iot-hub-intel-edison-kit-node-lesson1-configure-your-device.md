---
title: "Conecte-se Edison Intel (nó) tooAzure IoT - lição 1: Configurar dispositivo | Microsoft Docs"
description: Configurar o Intel Edison para o primeiro uso.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "arduino configurado, conecte-se arduino toopc, arduino de instalação, arduino board"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-node-get-started
ms.assetid: 372c9b6d-e701-4ff6-8151-d262aa76aa55
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c0609542a49924c979f71297d808c09acefca0bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="configure-your-intel-edison"></a><span data-ttu-id="3f818-104">Configurar seu Intel Edison</span><span class="sxs-lookup"><span data-stu-id="3f818-104">Configure your Intel Edison</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="3f818-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="3f818-105">What you will do</span></span>
<span data-ttu-id="3f818-106">Configurar Edison Intel para uso pela primeira vez montando o quadro hello, ligar e instalar a configuração ferramenta tooyour desktop SO tooflash firmware de Edison, definir sua senha e conecte-o tooWi-Fi.</span><span class="sxs-lookup"><span data-stu-id="3f818-106">Configure Intel Edison for first-time use by assembling hello board, powering it up and installing configuration tool tooyour desktop OS tooflash Edison's firmware, set its password and connect it tooWi-Fi.</span></span> <span data-ttu-id="3f818-107">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="3f818-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3f818-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="3f818-108">What you will learn</span></span>
<span data-ttu-id="3f818-109">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="3f818-109">In this article, you will learn:</span></span>

* <span data-ttu-id="3f818-110">Como tooassemble Edison placa e ligue-o.</span><span class="sxs-lookup"><span data-stu-id="3f818-110">How tooassemble Edison board and power it up.</span></span>
* <span data-ttu-id="3f818-111">Como o firmware de tooflash Edison, definir senha e conexão Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="3f818-111">How tooflash Edison's firmware, set password and connect Wi-Fi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3f818-112">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="3f818-112">What you need</span></span>
<span data-ttu-id="3f818-113">toocomplete essa operação, você precisa Olá seguir partes de seu Intel Edison Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="3f818-113">toocomplete this operation, you need hello following parts from your Intel Edison Starter Kit:</span></span>

* <span data-ttu-id="3f818-114">Módulo do Intel® Edison</span><span class="sxs-lookup"><span data-stu-id="3f818-114">Intel® Edison module</span></span>
* <span data-ttu-id="3f818-115">Placa de expansão Arduino</span><span class="sxs-lookup"><span data-stu-id="3f818-115">Arduino expansion board</span></span>
* <span data-ttu-id="3f818-116">Qualquer barras espaçador ou parafusos incluídos no pacote hello, incluindo a placa de expansão dois parafusos toofasten Olá módulo toohello e quatro conjuntos de parafusos e espaçadores plásticos.</span><span class="sxs-lookup"><span data-stu-id="3f818-116">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>
* <span data-ttu-id="3f818-117">Um tooType Micro B um cabo</span><span class="sxs-lookup"><span data-stu-id="3f818-117">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="3f818-118">Uma fonte de alimentação CC (corrente contínua).</span><span class="sxs-lookup"><span data-stu-id="3f818-118">A direct current (DC) power supply.</span></span> <span data-ttu-id="3f818-119">A fonte de alimentação deve ser classificada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="3f818-119">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="3f818-120">7-15V CC</span><span class="sxs-lookup"><span data-stu-id="3f818-120">7-15V DC</span></span>
  - <span data-ttu-id="3f818-121">Pelo menos 1500 mA</span><span class="sxs-lookup"><span data-stu-id="3f818-121">At least 1500mA</span></span>
  - <span data-ttu-id="3f818-122">pin do Hello center/interna deve ser Olá positivo polos Olá de fonte de alimentação</span><span class="sxs-lookup"><span data-stu-id="3f818-122">hello center/inner pin should be hello positive pole of hello power supply</span></span>

  ![Coisas em seu Kit de Início](media/iot-hub-intel-edison-lessons/lesson1/kit.png)

<span data-ttu-id="3f818-124">Você também precisará de:</span><span class="sxs-lookup"><span data-stu-id="3f818-124">You also need:</span></span>

* <span data-ttu-id="3f818-125">Um computador executando o Windows, Mac ou Linux.</span><span class="sxs-lookup"><span data-stu-id="3f818-125">A computer running Windows, Mac, or Linux.</span></span>
* <span data-ttu-id="3f818-126">Uma conexão sem fio para tooconnect Edison para.</span><span class="sxs-lookup"><span data-stu-id="3f818-126">A wireless connection for Edison tooconnect to.</span></span>
* <span data-ttu-id="3f818-127">Uma ferramenta de configuração de toodownload de conexão de Internet.</span><span class="sxs-lookup"><span data-stu-id="3f818-127">An Internet connection toodownload configuration tool.</span></span>

## <a name="assemble-your-board"></a><span data-ttu-id="3f818-128">Montar sua placa</span><span class="sxs-lookup"><span data-stu-id="3f818-128">Assemble your board</span></span>

<span data-ttu-id="3f818-129">Esta seção contém etapas tooattach sua placa de expansão Intel® Edison tooyour de módulo.</span><span class="sxs-lookup"><span data-stu-id="3f818-129">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="3f818-130">Coloque o módulo de Intel® Edison de saudação dentro da estrutura de tópicos Olá branca em seu quadro de expansão, alinhado buracos Olá no módulo Olá com parafusos Olá na placa de expansão de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f818-130">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="3f818-131">Pressione módulo Olá logo abaixo palavras Olá `What will you make?` até que você se sentir um snapshot.</span><span class="sxs-lookup"><span data-stu-id="3f818-131">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![montar a placa 2](media/iot-hub-intel-edison-lessons/lesson1/assemble_board2.jpg)

3. <span data-ttu-id="3f818-133">Use Olá dois porcas hexadecimal (incluídos no pacote de saudação) toosecure Olá módulo toohello expansão quadro.</span><span class="sxs-lookup"><span data-stu-id="3f818-133">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![montar a placa 3](media/iot-hub-intel-edison-lessons/lesson1/assemble_board3.jpg)

4. <span data-ttu-id="3f818-135">Insira um parafuso de uma das quatro furos de canto Olá na placa de expansão de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f818-135">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="3f818-136">Gire e reforçar uma espaçadores de plástico Olá branca em parafuso de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f818-136">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![montar a placa 4](media/iot-hub-intel-edison-lessons/lesson1/assemble_board4.jpg)

5. <span data-ttu-id="3f818-138">Repita para Olá espaçadores outros três canto.</span><span class="sxs-lookup"><span data-stu-id="3f818-138">Repeat for hello other three corner spacers.</span></span>

   ![montar a placa 5](media/iot-hub-intel-edison-lessons/lesson1/assemble_board5.jpg)

<span data-ttu-id="3f818-140">Agora, sua placa está montada.</span><span class="sxs-lookup"><span data-stu-id="3f818-140">Now your board is assembled.</span></span>

   ![montar a placa](media/iot-hub-intel-edison-lessons/lesson1/assembled_board.jpg)

## <a name="power-up-edison"></a><span data-ttu-id="3f818-142">Ligar o Edison</span><span class="sxs-lookup"><span data-stu-id="3f818-142">Power up Edison</span></span>

1. <span data-ttu-id="3f818-143">Conecte-se na fonte de alimentação hello.</span><span class="sxs-lookup"><span data-stu-id="3f818-143">Plug in hello power supply.</span></span>

   ![Conectar à fonte de alimentação](media/iot-hub-intel-edison-lessons/lesson1/plug_power.jpg)

2. <span data-ttu-id="3f818-145">Um LED verde (DS1 em Olá placa de expansão Arduino *) deve acende e permanecer aceso.</span><span class="sxs-lookup"><span data-stu-id="3f818-145">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="3f818-146">Aguarde um minuto para Olá quadro toofinish inicialização.</span><span class="sxs-lookup"><span data-stu-id="3f818-146">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="3f818-147">Se você não tiver uma fonte de energia do controlador de domínio, você ainda pode placa de saudação de energia por meio de uma porta USB.</span><span class="sxs-lookup"><span data-stu-id="3f818-147">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="3f818-148">Confira a seção `Connect Edison tooyour computer` para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="3f818-148">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="3f818-149">Ligar sua placa dessa maneira pode resultar em um comportamento imprevisível da placa, especialmente ao usar Wi-Fi ou motores de acionamento.</span><span class="sxs-lookup"><span data-stu-id="3f818-149">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

## <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="3f818-150">Conectar o computador de tooyour Edison</span><span class="sxs-lookup"><span data-stu-id="3f818-150">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="3f818-151">Alternar para baixo microcomutador Olá até dois o portas USB micro hello, para que Edison está no modo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="3f818-151">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="3f818-152">Veja [aqui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) as diferenças entre o modo de dispositivo e o modo de host.</span><span class="sxs-lookup"><span data-stu-id="3f818-152">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Alternar a saudação microcomutador](media/iot-hub-intel-edison-lessons/lesson1/toggle_down_microswitch.jpg)

2. <span data-ttu-id="3f818-154">Conecte cabo micro Olá Olá superior micro porta.</span><span class="sxs-lookup"><span data-stu-id="3f818-154">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Porta micro USB superior](media/iot-hub-intel-edison-lessons/lesson1/top_usbport.jpg)

3. <span data-ttu-id="3f818-156">Plug Olá outra extremidade do cabo USB em seu computador.</span><span class="sxs-lookup"><span data-stu-id="3f818-156">Plug hello other end of USB cable into your computer.</span></span>

   ![USB do computador](media/iot-hub-intel-edison-lessons/lesson1/computer_usb.jpg)

4. <span data-ttu-id="3f818-158">Você saberá que a placa foi inicializada completamente quando o computador montar uma nova unidade (muito semelhante a inserir um cartão SD no computador).</span><span class="sxs-lookup"><span data-stu-id="3f818-158">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="3f818-159">Baixe e execute a ferramenta de configuração de saudação</span><span class="sxs-lookup"><span data-stu-id="3f818-159">Download and run hello configuration tool</span></span>
<span data-ttu-id="3f818-160">Obter a ferramenta de configuração mais recente saudação do [este link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listado em Olá `Installers` título.</span><span class="sxs-lookup"><span data-stu-id="3f818-160">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="3f818-161">Execute a ferramenta hello e execute seu na tela instruções, clicar em próximo, quando necessário</span><span class="sxs-lookup"><span data-stu-id="3f818-161">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="3f818-162">Atualizar o firmware</span><span class="sxs-lookup"><span data-stu-id="3f818-162">Flash firmware</span></span>
1. <span data-ttu-id="3f818-163">Em Olá `Set up options` , clique em `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="3f818-163">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="3f818-164">Selecione Olá tooflash de imagem em seu quadro seguindo um destes procedimentos hello:</span><span class="sxs-lookup"><span data-stu-id="3f818-164">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="3f818-165">flash e toodownload seu quadro com hello mais recente firmware imagem disponível da Intel, selecione `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="3f818-165">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="3f818-166">tooflash seu quadro com uma imagem que você já tiver salvo em seu computador, selecione `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="3f818-166">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="3f818-167">Procure tooand Olá selecione imagem tooflash tooyour quadro.</span><span class="sxs-lookup"><span data-stu-id="3f818-167">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="3f818-168">ferramenta de configuração de saudação tentará tooflash seu quadro.</span><span class="sxs-lookup"><span data-stu-id="3f818-168">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="3f818-169">todo o processo de intermitente Olá pode levar too10 minutos.</span><span class="sxs-lookup"><span data-stu-id="3f818-169">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="3f818-170">Definir senha</span><span class="sxs-lookup"><span data-stu-id="3f818-170">Set password</span></span>
1. <span data-ttu-id="3f818-171">Em Olá `Set up options` , clique em `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="3f818-171">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="3f818-172">É possível definir um nome personalizado para sua placa Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="3f818-172">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="3f818-173">Isso é opcional.</span><span class="sxs-lookup"><span data-stu-id="3f818-173">This is optional.</span></span>
3. <span data-ttu-id="3f818-174">Digite uma senha para a placa e clique em `Set password`.</span><span class="sxs-lookup"><span data-stu-id="3f818-174">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="3f818-175">Marca uma senha hello, que é usada posteriormente.</span><span class="sxs-lookup"><span data-stu-id="3f818-175">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="3f818-176">Conectar ao Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="3f818-176">Connect Wi-Fi</span></span>
1. <span data-ttu-id="3f818-177">Em Olá `Set up options` , clique em `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="3f818-177">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="3f818-178">Aguarde o minuto tooone como verificações de seu computador para redes Wi-Fi disponíveis.</span><span class="sxs-lookup"><span data-stu-id="3f818-178">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="3f818-179">De saudação `Detected Networks` lista suspensa, selecione sua rede.</span><span class="sxs-lookup"><span data-stu-id="3f818-179">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="3f818-180">De saudação `Security` lista suspensa, o tipo de segurança da rede Olá select.</span><span class="sxs-lookup"><span data-stu-id="3f818-180">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="3f818-181">Forneça suas informações de logon e senha e clique em `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="3f818-181">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="3f818-182">Marca Olá endereço IP, que é usado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="3f818-182">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="3f818-183">Certifique-se de Edison é conectado toohello mesmo de rede do computador.</span><span class="sxs-lookup"><span data-stu-id="3f818-183">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="3f818-184">O computador se conecta a tooyour Edison usando o endereço IP de saudação.</span><span class="sxs-lookup"><span data-stu-id="3f818-184">Your computer connects tooyour Edison by using hello IP address.</span></span>

<span data-ttu-id="3f818-185">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="3f818-185">Congratulations!</span></span> <span data-ttu-id="3f818-186">Você configurou o Edison com êxito.</span><span class="sxs-lookup"><span data-stu-id="3f818-186">You've successfully configured Edison.</span></span>

## <a name="summary"></a><span data-ttu-id="3f818-187">Resumo</span><span class="sxs-lookup"><span data-stu-id="3f818-187">Summary</span></span>
<span data-ttu-id="3f818-188">Neste artigo, você aprendeu como tooassemble Olá placa Edison, flash sua senha de configuração, o firmware e conectá-lo tooWi-Fi usando a ferramenta de configuração.</span><span class="sxs-lookup"><span data-stu-id="3f818-188">In this article, you’ve learned how tooassemble hello Edison board, flash its firmware, setup password and connect it tooWi-Fi by using configuration tool.</span></span> <span data-ttu-id="3f818-189">Observe que Olá que LED ainda não ativado.</span><span class="sxs-lookup"><span data-stu-id="3f818-189">Note that hello LED doesn't yet light up.</span></span> <span data-ttu-id="3f818-190">Olá próxima tarefa é o software em preparação para a execução de um aplicativo de exemplo no Edison e ferramentas necessárias de saudação tooinstall.</span><span class="sxs-lookup"><span data-stu-id="3f818-190">hello next task is tooinstall hello necessary tools and software in preparation for running a sample application on Edison.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3f818-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3f818-191">Next steps</span></span>
<span data-ttu-id="3f818-192">[Obter ferramentas Olá][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="3f818-192">[Get hello tools][get-the-tools]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-node-troubleshooting.md
[get-the-tools]: iot-hub-intel-edison-kit-node-lesson1-get-the-tools-win32.md