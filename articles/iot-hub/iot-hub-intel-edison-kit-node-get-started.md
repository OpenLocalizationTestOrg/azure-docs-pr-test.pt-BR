---
title: aaaIntel Edison toocloud (Node. js) - conectar Intel Edison tooAzure IoT Hub | Microsoft Docs
description: Saiba como toosetup e conecte-se a Intel Edison tooAzure IoT Hub para a plataforma de nuvem do Azure Edison Intel toosend dados toohello neste tutorial.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Azure iot intel edison, intel hub iot de edison, intel edison enviar dados toocloud, intel toocloud edison
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: bfc3387efc532b4b83f0626a9cf61d12c2952af2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-intel-edison-tooazure-iot-hub-nodejs"></a><span data-ttu-id="19cdd-104">Conecte-se Intel Edison tooAzure IoT Hub (Node. js)</span><span class="sxs-lookup"><span data-stu-id="19cdd-104">Connect Intel Edison tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="19cdd-105">Neste tutorial, você começar a aprender os fundamentos de saudação do trabalho com Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="19cdd-105">In this tutorial, you begin by learning hello basics of working with Intel Edison.</span></span> <span data-ttu-id="19cdd-106">Em seguida, você aprenderá como tooseamlessly se conectar a sua nuvem de toohello dispositivos usando [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="19cdd-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="19cdd-107">Não tem um dispositivo ainda?</span><span class="sxs-lookup"><span data-stu-id="19cdd-107">Don't have a kit yet?</span></span> <span data-ttu-id="19cdd-108">Comece [aqui](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="19cdd-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="19cdd-109">O que fazer</span><span class="sxs-lookup"><span data-stu-id="19cdd-109">What you do</span></span>

* <span data-ttu-id="19cdd-110">Configure os módulos do Intel Edison e do Grove.</span><span class="sxs-lookup"><span data-stu-id="19cdd-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="19cdd-111">Crie um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="19cdd-111">Create an IoT hub.</span></span>
* <span data-ttu-id="19cdd-112">Registre um dispositivo para o Edison em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="19cdd-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="19cdd-113">Execute um aplicativo de exemplo no hub IoT tooyour de dados do Edison toosend sensor.</span><span class="sxs-lookup"><span data-stu-id="19cdd-113">Run a sample application on Edison toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="19cdd-114">Conecte-se o hub IoT do Intel Edison tooan que você criar.</span><span class="sxs-lookup"><span data-stu-id="19cdd-114">Connect Intel Edison tooan IoT hub that you create.</span></span> <span data-ttu-id="19cdd-115">Em seguida, você executar um aplicativo de exemplo em Edison toocollect temperatura e umidade dados de um sensor de temperatura Grove.</span><span class="sxs-lookup"><span data-stu-id="19cdd-115">Then you run a sample application on Edison toocollect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="19cdd-116">Por fim, você pode enviar hub IoT do hello sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="19cdd-116">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="19cdd-117">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="19cdd-117">What you learn</span></span>

* <span data-ttu-id="19cdd-118">Como toocreate um hub IoT do Azure e obter sua nova cadeia de caracteres de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="19cdd-118">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="19cdd-119">Como tooconnect Edison com um sensor de temperatura Grove.</span><span class="sxs-lookup"><span data-stu-id="19cdd-119">How tooconnect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="19cdd-120">Como os dados do sensor toocollect executando um aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="19cdd-120">How toocollect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="19cdd-121">Como hub IoT do toosend sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="19cdd-121">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="19cdd-122">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="19cdd-122">What you need</span></span>

![O que você precisa](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="19cdd-124">Olá placa Edison Intel</span><span class="sxs-lookup"><span data-stu-id="19cdd-124">hello Intel Edison board</span></span>
* <span data-ttu-id="19cdd-125">Placa de expansão Arduino</span><span class="sxs-lookup"><span data-stu-id="19cdd-125">Arduino expansion board</span></span>
* <span data-ttu-id="19cdd-126">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="19cdd-126">An active Azure subscription.</span></span> <span data-ttu-id="19cdd-127">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="19cdd-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="19cdd-128">Um Mac ou PC que esteja executando Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="19cdd-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="19cdd-129">Uma conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="19cdd-129">An Internet connection.</span></span>
* <span data-ttu-id="19cdd-130">Um tooType Micro B um cabo</span><span class="sxs-lookup"><span data-stu-id="19cdd-130">A Micro B tooType A USB cable</span></span>
* <span data-ttu-id="19cdd-131">Uma fonte de alimentação CC (corrente contínua).</span><span class="sxs-lookup"><span data-stu-id="19cdd-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="19cdd-132">A fonte de alimentação deve ser classificada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="19cdd-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="19cdd-133">7-15V CC</span><span class="sxs-lookup"><span data-stu-id="19cdd-133">7-15V DC</span></span>
  - <span data-ttu-id="19cdd-134">Pelo menos 1500 mA</span><span class="sxs-lookup"><span data-stu-id="19cdd-134">At least 1500mA</span></span>
  - <span data-ttu-id="19cdd-135">pin do Hello center/interna deve ser Olá positivo polos Olá de fonte de alimentação</span><span class="sxs-lookup"><span data-stu-id="19cdd-135">hello center/inner pin should be hello positive pole of hello power supply</span></span>

<span data-ttu-id="19cdd-136">Olá itens a seguir é opcional:</span><span class="sxs-lookup"><span data-stu-id="19cdd-136">hello following items are optional:</span></span>

* <span data-ttu-id="19cdd-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="19cdd-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="19cdd-138">Grove - Sensor de temperatura</span><span class="sxs-lookup"><span data-stu-id="19cdd-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="19cdd-139">Cabo do Grove</span><span class="sxs-lookup"><span data-stu-id="19cdd-139">Grove Cable</span></span>
* <span data-ttu-id="19cdd-140">Qualquer barras espaçador ou parafusos incluídos no pacote hello, incluindo a placa de expansão dois parafusos toofasten Olá módulo toohello e quatro conjuntos de parafusos e espaçadores plásticos.</span><span class="sxs-lookup"><span data-stu-id="19cdd-140">Any spacer bars or screws included in hello packaging, including two screws toofasten hello module toohello expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="19cdd-141">Esses itens são opcionais, porque o suporte de exemplo de código Olá simulados dados do sensor.</span><span class="sxs-lookup"><span data-stu-id="19cdd-141">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="19cdd-142">Configurar o Intel Edison</span><span class="sxs-lookup"><span data-stu-id="19cdd-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="19cdd-143">Montar sua placa</span><span class="sxs-lookup"><span data-stu-id="19cdd-143">Assemble your board</span></span>

<span data-ttu-id="19cdd-144">Esta seção contém etapas tooattach sua placa de expansão Intel® Edison tooyour de módulo.</span><span class="sxs-lookup"><span data-stu-id="19cdd-144">This section contains steps tooattach your Intel® Edison module tooyour expansion board.</span></span>

1. <span data-ttu-id="19cdd-145">Coloque o módulo de Intel® Edison de saudação dentro da estrutura de tópicos Olá branca em seu quadro de expansão, alinhado buracos Olá no módulo Olá com parafusos Olá na placa de expansão de saudação.</span><span class="sxs-lookup"><span data-stu-id="19cdd-145">Place hello Intel® Edison module within hello white outline on your expansion board, lining up hello holes on hello module with hello screws on hello expansion board.</span></span>

2. <span data-ttu-id="19cdd-146">Pressione módulo Olá logo abaixo palavras Olá `What will you make?` até que você se sentir um snapshot.</span><span class="sxs-lookup"><span data-stu-id="19cdd-146">Press down on hello module just below hello words `What will you make?` until you feel a snap.</span></span>

   ![montar a placa 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="19cdd-148">Use Olá dois porcas hexadecimal (incluídos no pacote de saudação) toosecure Olá módulo toohello expansão quadro.</span><span class="sxs-lookup"><span data-stu-id="19cdd-148">Use hello two hex nuts (included in hello package) toosecure hello module toohello expansion board.</span></span>

   ![montar a placa 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="19cdd-150">Insira um parafuso de uma das quatro furos de canto Olá na placa de expansão de saudação.</span><span class="sxs-lookup"><span data-stu-id="19cdd-150">Insert a screw in one of hello four corner holes on hello expansion board.</span></span> <span data-ttu-id="19cdd-151">Gire e reforçar uma espaçadores de plástico Olá branca em parafuso de saudação.</span><span class="sxs-lookup"><span data-stu-id="19cdd-151">Twist and tighten one of hello white plastic spacers onto hello screw.</span></span>

   ![montar a placa 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="19cdd-153">Repita para Olá espaçadores outros três canto.</span><span class="sxs-lookup"><span data-stu-id="19cdd-153">Repeat for hello other three corner spacers.</span></span>

   ![montar a placa 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="19cdd-155">Agora, sua placa está montada.</span><span class="sxs-lookup"><span data-stu-id="19cdd-155">Now your board is assembled.</span></span>

   ![montar a placa](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-hello-grove-base-shield-and-hello-temperature-sensor"></a><span data-ttu-id="19cdd-157">Conecte-se hello Grove base de dados de blindagem e sensor de temperatura Olá</span><span class="sxs-lookup"><span data-stu-id="19cdd-157">Connect hello Grove Base Shield and hello temperature sensor</span></span>

1. <span data-ttu-id="19cdd-158">Coloque Olá Grove base de dados de blindagem na placa tooyour.</span><span class="sxs-lookup"><span data-stu-id="19cdd-158">Place hello Grove Base Shield on tooyour board.</span></span> <span data-ttu-id="19cdd-159">Verifique se todos os pinos estão totalmente conectados à sua placa.</span><span class="sxs-lookup"><span data-stu-id="19cdd-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="19cdd-161">Sensor de temperatura Use Grove cabo tooconnect Grove em Olá Grove base de dados de blindagem **A0** porta.</span><span class="sxs-lookup"><span data-stu-id="19cdd-161">Use Grove Cable tooconnect Grove temperature sensor onto hello Grove Base Shield **A0** port.</span></span>

   ![Conecte-se sensor tootemperature](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Conexão do Edison e do sensor](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="19cdd-164">Agora seu sensor está pronto.</span><span class="sxs-lookup"><span data-stu-id="19cdd-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="19cdd-165">Ligar o Edison</span><span class="sxs-lookup"><span data-stu-id="19cdd-165">Power up Edison</span></span>

1. <span data-ttu-id="19cdd-166">Conecte-se na fonte de alimentação hello.</span><span class="sxs-lookup"><span data-stu-id="19cdd-166">Plug in hello power supply.</span></span>

   ![Conectar à fonte de alimentação](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="19cdd-168">Um LED verde (DS1 em Olá placa de expansão Arduino *) deve acende e permanecer aceso.</span><span class="sxs-lookup"><span data-stu-id="19cdd-168">A green LED(labeled DS1 on hello Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="19cdd-169">Aguarde um minuto para Olá quadro toofinish inicialização.</span><span class="sxs-lookup"><span data-stu-id="19cdd-169">Wait one minute for hello board toofinish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="19cdd-170">Se você não tiver uma fonte de energia do controlador de domínio, você ainda pode placa de saudação de energia por meio de uma porta USB.</span><span class="sxs-lookup"><span data-stu-id="19cdd-170">If you do not have a DC power supply, you can still power hello board through a USB port.</span></span> <span data-ttu-id="19cdd-171">Confira a seção `Connect Edison tooyour computer` para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="19cdd-171">See `Connect Edison tooyour computer` section for details.</span></span> <span data-ttu-id="19cdd-172">Ligar sua placa dessa maneira pode resultar em um comportamento imprevisível da placa, especialmente ao usar Wi-Fi ou motores de acionamento.</span><span class="sxs-lookup"><span data-stu-id="19cdd-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-tooyour-computer"></a><span data-ttu-id="19cdd-173">Conectar o computador de tooyour Edison</span><span class="sxs-lookup"><span data-stu-id="19cdd-173">Connect Edison tooyour computer</span></span>

1. <span data-ttu-id="19cdd-174">Alternar para baixo microcomutador Olá até dois o portas USB micro hello, para que Edison está no modo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="19cdd-174">Toggle down hello microswitch towards hello two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="19cdd-175">Veja [aqui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) as diferenças entre o modo de dispositivo e o modo de host.</span><span class="sxs-lookup"><span data-stu-id="19cdd-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Alternar a saudação microcomutador](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="19cdd-177">Conecte cabo micro Olá Olá superior micro porta.</span><span class="sxs-lookup"><span data-stu-id="19cdd-177">Plug hello micro USB cable into hello top micro USB port.</span></span>

   ![Porta micro USB superior](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="19cdd-179">Plug Olá outra extremidade do cabo USB em seu computador.</span><span class="sxs-lookup"><span data-stu-id="19cdd-179">Plug hello other end of USB cable into your computer.</span></span>

   ![USB do computador](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="19cdd-181">Você saberá que a placa foi inicializada completamente quando o computador montar uma nova unidade (muito semelhante a inserir um cartão SD no computador).</span><span class="sxs-lookup"><span data-stu-id="19cdd-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-hello-configuration-tool"></a><span data-ttu-id="19cdd-182">Baixe e execute a ferramenta de configuração de saudação</span><span class="sxs-lookup"><span data-stu-id="19cdd-182">Download and run hello configuration tool</span></span>
<span data-ttu-id="19cdd-183">Obter a ferramenta de configuração mais recente saudação do [este link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listado em Olá `Installers` título.</span><span class="sxs-lookup"><span data-stu-id="19cdd-183">Get hello latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under hello `Installers` heading.</span></span> <span data-ttu-id="19cdd-184">Execute a ferramenta hello e execute seu na tela instruções, clicar em próximo, quando necessário</span><span class="sxs-lookup"><span data-stu-id="19cdd-184">Execute hello tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="19cdd-185">Atualizar o firmware</span><span class="sxs-lookup"><span data-stu-id="19cdd-185">Flash firmware</span></span>
1. <span data-ttu-id="19cdd-186">Em Olá `Set up options` , clique em `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="19cdd-186">On hello `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="19cdd-187">Selecione Olá tooflash de imagem em seu quadro seguindo um destes procedimentos hello:</span><span class="sxs-lookup"><span data-stu-id="19cdd-187">Select hello image tooflash onto your board by doing one of hello following:</span></span>
   - <span data-ttu-id="19cdd-188">flash e toodownload seu quadro com hello mais recente firmware imagem disponível da Intel, selecione `Download hello latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="19cdd-188">toodownload and flash your board with hello latest firmware image available from Intel, select `Download hello latest image version xxxx`.</span></span>
   - <span data-ttu-id="19cdd-189">tooflash seu quadro com uma imagem que você já tiver salvo em seu computador, selecione `Select hello local image`.</span><span class="sxs-lookup"><span data-stu-id="19cdd-189">tooflash your board with an image you already have saved on your computer, select `Select hello local image`.</span></span> <span data-ttu-id="19cdd-190">Procure tooand Olá selecione imagem tooflash tooyour quadro.</span><span class="sxs-lookup"><span data-stu-id="19cdd-190">Browse tooand select hello image you want tooflash tooyour board.</span></span>
3. <span data-ttu-id="19cdd-191">ferramenta de configuração de saudação tentará tooflash seu quadro.</span><span class="sxs-lookup"><span data-stu-id="19cdd-191">hello setup tool will attempt tooflash your board.</span></span> <span data-ttu-id="19cdd-192">todo o processo de intermitente Olá pode levar too10 minutos.</span><span class="sxs-lookup"><span data-stu-id="19cdd-192">hello entire flashing process may take up too10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="19cdd-193">Definir senha</span><span class="sxs-lookup"><span data-stu-id="19cdd-193">Set password</span></span>
1. <span data-ttu-id="19cdd-194">Em Olá `Set up options` , clique em `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="19cdd-194">On hello `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="19cdd-195">É possível definir um nome personalizado para sua placa Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="19cdd-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="19cdd-196">Isso é opcional.</span><span class="sxs-lookup"><span data-stu-id="19cdd-196">This is optional.</span></span>
3. <span data-ttu-id="19cdd-197">Digite uma senha para a placa e clique em `Set password`.</span><span class="sxs-lookup"><span data-stu-id="19cdd-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="19cdd-198">Marca uma senha hello, que é usada posteriormente.</span><span class="sxs-lookup"><span data-stu-id="19cdd-198">Mark down hello password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="19cdd-199">Conectar ao Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="19cdd-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="19cdd-200">Em Olá `Set up options` , clique em `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="19cdd-200">On hello `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="19cdd-201">Aguarde o minuto tooone como verificações de seu computador para redes Wi-Fi disponíveis.</span><span class="sxs-lookup"><span data-stu-id="19cdd-201">Wait up tooone minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="19cdd-202">De saudação `Detected Networks` lista suspensa, selecione sua rede.</span><span class="sxs-lookup"><span data-stu-id="19cdd-202">From hello `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="19cdd-203">De saudação `Security` lista suspensa, o tipo de segurança da rede Olá select.</span><span class="sxs-lookup"><span data-stu-id="19cdd-203">From hello `Security` drop-down list, select hello network's security type.</span></span>
4. <span data-ttu-id="19cdd-204">Forneça suas informações de logon e senha e clique em `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="19cdd-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="19cdd-205">Marca Olá endereço IP, que é usado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="19cdd-205">Mark down hello IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="19cdd-206">Certifique-se de Edison é conectado toohello mesmo de rede do computador.</span><span class="sxs-lookup"><span data-stu-id="19cdd-206">Make sure that Edison is connected toohello same network as your computer.</span></span> <span data-ttu-id="19cdd-207">O computador se conecta a tooyour Edison usando o endereço IP de saudação.</span><span class="sxs-lookup"><span data-stu-id="19cdd-207">Your computer connects tooyour Edison by using hello IP address.</span></span>

   ![Conecte-se sensor tootemperature](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="19cdd-209">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="19cdd-209">Congratulations!</span></span> <span data-ttu-id="19cdd-210">Você configurou o Edison com êxito.</span><span class="sxs-lookup"><span data-stu-id="19cdd-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="19cdd-211">Executar um exemplo de aplicativo no Intel Edison</span><span class="sxs-lookup"><span data-stu-id="19cdd-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-hello-azure-iot-device-sdk"></a><span data-ttu-id="19cdd-212">Preparar Olá SDK de dispositivo IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="19cdd-212">Prepare hello Azure IoT Device SDK</span></span>

1. <span data-ttu-id="19cdd-213">Use um dos Olá seguir SSH clientes de sua tooyour de tooconnect do computador host Edison Intel.</span><span class="sxs-lookup"><span data-stu-id="19cdd-213">Use one of hello following SSH clients from your host computer tooconnect tooyour Intel Edison.</span></span> <span data-ttu-id="19cdd-214">endereço IP de saudação é da ferramenta de configuração de saudação e senha de saudação é Olá um que você definiu nessa ferramenta.</span><span class="sxs-lookup"><span data-stu-id="19cdd-214">hello IP address is from hello configuration tool and hello password is hello one you've set in that tool.</span></span>
    - <span data-ttu-id="19cdd-215">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="19cdd-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="19cdd-216">Olá SSH do cliente interno Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="19cdd-216">hello built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="19cdd-217">Dispositivo de tooyour do aplicativo cliente do clone Olá exemplo.</span><span class="sxs-lookup"><span data-stu-id="19cdd-217">Clone hello sample client app tooyour device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="19cdd-218">Navegue todos os pacotes de saudação do toohello repositório pasta toorun tooinstall de comando a seguir, pode levar serval toocomplete de minutos.</span><span class="sxs-lookup"><span data-stu-id="19cdd-218">Then navigate toohello repo folder toorun hello following command tooinstall all packages, it may take serval minutes toocomplete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-hello-sample-application"></a><span data-ttu-id="19cdd-219">Configurar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="19cdd-219">Configure and run hello sample application</span></span>

1. <span data-ttu-id="19cdd-220">Abra o arquivo de configuração de saudação executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="19cdd-220">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Arquivo de configuração](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="19cdd-222">Há duas macros que você pode configurar nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="19cdd-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="19cdd-223">Olá primeiro um é `INTERVAL`, que define o intervalo de tempo de saudação entre duas mensagens que enviar toocloud.</span><span class="sxs-lookup"><span data-stu-id="19cdd-223">hello first one is `INTERVAL`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="19cdd-224">Olá segunda `simulatedData`, que é um valor booleano para se toouse simulados dados do sensor ou não.</span><span class="sxs-lookup"><span data-stu-id="19cdd-224">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="19cdd-225">Se você **não tem o sensor Olá**, defina hello `simulatedData` valor muito`true` aplicativo de exemplo hello toomake criar e usar dados de sensor simulada.</span><span class="sxs-lookup"><span data-stu-id="19cdd-225">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="19cdd-226">Salve e saia pressionando CTRL+O > ENTER > CTRL+X.</span><span class="sxs-lookup"><span data-stu-id="19cdd-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="19cdd-227">Execute o aplicativo de exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="19cdd-227">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="19cdd-228">Verifique se você copiar e colar cadeia de caracteres de conexão de dispositivo Olá em aspas hello.</span><span class="sxs-lookup"><span data-stu-id="19cdd-228">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>

<span data-ttu-id="19cdd-229">Você verá a seguinte Olá saída mostra Olá sensor dados e hello mensagens enviadas tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="19cdd-229">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Saída - dados de sensor enviadas do Intel Edison tooyour hub IoT](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="19cdd-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="19cdd-231">Next steps</span></span>

<span data-ttu-id="19cdd-232">Executar dados de sensor de toocollect do aplicativo de exemplo e enviá-lo tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="19cdd-232">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
