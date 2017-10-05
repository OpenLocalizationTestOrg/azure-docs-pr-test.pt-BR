---
title: Intel Edison para nuvem (Node.js) - Conectar o Intel Edison ao Hub IoT do Azure | Microsoft Docs
description: Neste tutorial, aprenda a configurar e conectar o Intel Edison ao Hub IoT do Azure para o Intel Edison enviar dados para a plataforma de nuvem do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: azure iot intel edison, intel edison iot hub, intel edison envia dados para a nuvem, intel edison para nuvem
ms.assetid: a7c9cf2d-c102-41b0-aa45-41285c6877eb
ms.service: iot-hub
ms.devlang: nodejs
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 6/15/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 5a31efba704045196b5563f7bc467c773bea7805
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-intel-edison-to-azure-iot-hub-nodejs"></a><span data-ttu-id="cb056-104">Conectar o Intel Edison ao Hub IoT do Azure (Node.js)</span><span class="sxs-lookup"><span data-stu-id="cb056-104">Connect Intel Edison to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="cb056-105">Neste tutorial, você começa aprendendo as noções básicas de como trabalhar com o Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="cb056-105">In this tutorial, you begin by learning the basics of working with Intel Edison.</span></span> <span data-ttu-id="cb056-106">Em seguida, aprenderá a conectar seus dispositivos diretamente à nuvem usando o [Hub IoT do Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="cb056-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

<span data-ttu-id="cb056-107">Não tem um dispositivo ainda?</span><span class="sxs-lookup"><span data-stu-id="cb056-107">Don't have a kit yet?</span></span> <span data-ttu-id="cb056-108">Comece [aqui](https://azure.microsoft.com/develop/iot/starter-kits)</span><span class="sxs-lookup"><span data-stu-id="cb056-108">Start [here](https://azure.microsoft.com/develop/iot/starter-kits)</span></span>

## <a name="what-you-do"></a><span data-ttu-id="cb056-109">O que fazer</span><span class="sxs-lookup"><span data-stu-id="cb056-109">What you do</span></span>

* <span data-ttu-id="cb056-110">Configure os módulos do Intel Edison e do Grove.</span><span class="sxs-lookup"><span data-stu-id="cb056-110">Setup Intel Edison and and Grove modules.</span></span>
* <span data-ttu-id="cb056-111">Crie um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cb056-111">Create an IoT hub.</span></span>
* <span data-ttu-id="cb056-112">Registre um dispositivo para o Edison em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cb056-112">Register a device for Edison in your IoT hub.</span></span>
* <span data-ttu-id="cb056-113">Execute um aplicativo de exemplo no Edison para enviar os dados do sensor para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cb056-113">Run a sample application on Edison to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="cb056-114">Conecte o Intel Edison a um Hub IoT criado por você.</span><span class="sxs-lookup"><span data-stu-id="cb056-114">Connect Intel Edison to an IoT hub that you create.</span></span> <span data-ttu-id="cb056-115">Em seguida, execute um aplicativo de exemplo no Edison para coletar dados de temperatura e umidade de um sensor de temperatura do Grove.</span><span class="sxs-lookup"><span data-stu-id="cb056-115">Then you run a sample application on Edison to collect temperature and humidity data from a Grove temperature sensor.</span></span> <span data-ttu-id="cb056-116">Por fim, você envia os dados do sensor para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cb056-116">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="cb056-117">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="cb056-117">What you learn</span></span>

* <span data-ttu-id="cb056-118">Como criar um Hub IoT do Azure e obter sua nova cadeia de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cb056-118">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="cb056-119">Como conectar o Edison a um sensor de temperatura do Grove.</span><span class="sxs-lookup"><span data-stu-id="cb056-119">How to connect Edison with a Grove temperature sensor.</span></span>
* <span data-ttu-id="cb056-120">Como coletar dados de sensor executando um aplicativo de exemplo no Edison.</span><span class="sxs-lookup"><span data-stu-id="cb056-120">How to collect sensor data by running a sample application on Edison.</span></span>
* <span data-ttu-id="cb056-121">Como enviar dados de sensor ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cb056-121">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="cb056-122">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="cb056-122">What you need</span></span>

![O que você precisa](media/iot-hub-intel-edison-kit-node-get-started/0_kit.png)

* <span data-ttu-id="cb056-124">A placa Intel Edison</span><span class="sxs-lookup"><span data-stu-id="cb056-124">The Intel Edison board</span></span>
* <span data-ttu-id="cb056-125">Placa de expansão Arduino</span><span class="sxs-lookup"><span data-stu-id="cb056-125">Arduino expansion board</span></span>
* <span data-ttu-id="cb056-126">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="cb056-126">An active Azure subscription.</span></span> <span data-ttu-id="cb056-127">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="cb056-127">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="cb056-128">Um Mac ou PC que esteja executando Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="cb056-128">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="cb056-129">Uma conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="cb056-129">An Internet connection.</span></span>
* <span data-ttu-id="cb056-130">Um cabo USB do tipo Micro B para Tipo A</span><span class="sxs-lookup"><span data-stu-id="cb056-130">A Micro B to Type A USB cable</span></span>
* <span data-ttu-id="cb056-131">Uma fonte de alimentação CC (corrente contínua).</span><span class="sxs-lookup"><span data-stu-id="cb056-131">A direct current (DC) power supply.</span></span> <span data-ttu-id="cb056-132">A fonte de alimentação deve ser classificada da seguinte maneira:</span><span class="sxs-lookup"><span data-stu-id="cb056-132">Your power supply should be rated as follows:</span></span>
  - <span data-ttu-id="cb056-133">7-15V CC</span><span class="sxs-lookup"><span data-stu-id="cb056-133">7-15V DC</span></span>
  - <span data-ttu-id="cb056-134">Pelo menos 1500 mA</span><span class="sxs-lookup"><span data-stu-id="cb056-134">At least 1500mA</span></span>
  - <span data-ttu-id="cb056-135">O pino central/interno deve ser o polo positivo da fonte de alimentação</span><span class="sxs-lookup"><span data-stu-id="cb056-135">The center/inner pin should be the positive pole of the power supply</span></span>

<span data-ttu-id="cb056-136">Os itens a seguir são opcionais:</span><span class="sxs-lookup"><span data-stu-id="cb056-136">The following items are optional:</span></span>

* <span data-ttu-id="cb056-137">Grove Base Shield V2</span><span class="sxs-lookup"><span data-stu-id="cb056-137">Grove Base Shield V2</span></span>
* <span data-ttu-id="cb056-138">Grove - Sensor de temperatura</span><span class="sxs-lookup"><span data-stu-id="cb056-138">Grove - Temperature Sensor</span></span>
* <span data-ttu-id="cb056-139">Cabo do Grove</span><span class="sxs-lookup"><span data-stu-id="cb056-139">Grove Cable</span></span>
* <span data-ttu-id="cb056-140">As barras separadoras ou parafusos incluídos no pacote, incluindo dois parafusos para fixar o módulo à placa de expansão e quatro conjuntos de parafusos e espaçadores plásticos.</span><span class="sxs-lookup"><span data-stu-id="cb056-140">Any spacer bars or screws included in the packaging, including two screws to fasten the module to the expansion board and four sets of screws and plastic spacers.</span></span>

> [!NOTE] 
<span data-ttu-id="cb056-141">Esses itens são opcionais porque o exemplo de código dá suporte a dados simulados de sensor.</span><span class="sxs-lookup"><span data-stu-id="cb056-141">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-intel-edison"></a><span data-ttu-id="cb056-142">Configurar o Intel Edison</span><span class="sxs-lookup"><span data-stu-id="cb056-142">Setup Intel Edison</span></span>

### <a name="assemble-your-board"></a><span data-ttu-id="cb056-143">Montar sua placa</span><span class="sxs-lookup"><span data-stu-id="cb056-143">Assemble your board</span></span>

<span data-ttu-id="cb056-144">Esta seção contém etapas para anexar o módulo Intel® Edison à sua placa de expansão.</span><span class="sxs-lookup"><span data-stu-id="cb056-144">This section contains steps to attach your Intel® Edison module to your expansion board.</span></span>

1. <span data-ttu-id="cb056-145">Coloque o módulo Intel® Edison dentro do contorno branco na placa de expansão, alinhando os orifícios no módulo aos parafusos na placa de expansão.</span><span class="sxs-lookup"><span data-stu-id="cb056-145">Place the Intel® Edison module within the white outline on your expansion board, lining up the holes on the module with the screws on the expansion board.</span></span>

2. <span data-ttu-id="cb056-146">Pressione o módulo logo abaixo das palavras `What will you make?` até sentir um clique.</span><span class="sxs-lookup"><span data-stu-id="cb056-146">Press down on the module just below the words `What will you make?` until you feel a snap.</span></span>

   ![montar a placa 2](media/iot-hub-intel-edison-kit-node-get-started/1_assemble_board2.jpg)

3. <span data-ttu-id="cb056-148">Use as duas porcas sextavadas (incluídas no pacote) para prender o módulo à placa de expansão.</span><span class="sxs-lookup"><span data-stu-id="cb056-148">Use the two hex nuts (included in the package) to secure the module to the expansion board.</span></span>

   ![montar a placa 3](media/iot-hub-intel-edison-kit-node-get-started/2_assemble_board3.jpg)

4. <span data-ttu-id="cb056-150">Insira um parafuso em um dos quatro orifícios nos cantos na placa de expansão.</span><span class="sxs-lookup"><span data-stu-id="cb056-150">Insert a screw in one of the four corner holes on the expansion board.</span></span> <span data-ttu-id="cb056-151">Gire e aperte um dos espaçadores plásticos brancos no parafuso.</span><span class="sxs-lookup"><span data-stu-id="cb056-151">Twist and tighten one of the white plastic spacers onto the screw.</span></span>

   ![montar a placa 4](media/iot-hub-intel-edison-kit-node-get-started/3_assemble_board4.jpg)

5. <span data-ttu-id="cb056-153">Repita para os espaçadores dos outros três cantos.</span><span class="sxs-lookup"><span data-stu-id="cb056-153">Repeat for the other three corner spacers.</span></span>

   ![montar a placa 5](media/iot-hub-intel-edison-kit-node-get-started/4_assemble_board5.jpg)

<span data-ttu-id="cb056-155">Agora, sua placa está montada.</span><span class="sxs-lookup"><span data-stu-id="cb056-155">Now your board is assembled.</span></span>

   ![montar a placa](media/iot-hub-intel-edison-kit-node-get-started/5_assembled_board.jpg)

### <a name="connect-the-grove-base-shield-and-the-temperature-sensor"></a><span data-ttu-id="cb056-157">Conectar o Grove Base Shield e o sensor de temperatura</span><span class="sxs-lookup"><span data-stu-id="cb056-157">Connect the Grove Base Shield and the temperature sensor</span></span>

1. <span data-ttu-id="cb056-158">Coloque o Grove Base Shield em sua placa.</span><span class="sxs-lookup"><span data-stu-id="cb056-158">Place the Grove Base Shield on to your board.</span></span> <span data-ttu-id="cb056-159">Verifique se todos os pinos estão totalmente conectados à sua placa.</span><span class="sxs-lookup"><span data-stu-id="cb056-159">Make sure all pins are tightly plugged into your board.</span></span>
   
   ![Grove Base Shield](media/iot-hub-intel-edison-kit-node-get-started/6_grove_base_sheild.jpg)

2. <span data-ttu-id="cb056-161">Use o Cabo do Grove para conectar o sensor de temperatura do Grove à porta **A0** do Grove Base Shield.</span><span class="sxs-lookup"><span data-stu-id="cb056-161">Use Grove Cable to connect Grove temperature sensor onto the Grove Base Shield **A0** port.</span></span>

   ![Conectar ao sensor de temperatura](media/iot-hub-intel-edison-kit-node-get-started/7_temperature_sensor.jpg)

   ![Conexão do Edison e do sensor](media/iot-hub-intel-edison-kit-node-get-started/16_edion_sensor.png)

<span data-ttu-id="cb056-164">Agora seu sensor está pronto.</span><span class="sxs-lookup"><span data-stu-id="cb056-164">Now your sensor is ready.</span></span>

### <a name="power-up-edison"></a><span data-ttu-id="cb056-165">Ligar o Edison</span><span class="sxs-lookup"><span data-stu-id="cb056-165">Power up Edison</span></span>

1. <span data-ttu-id="cb056-166">Conecte à fonte de alimentação.</span><span class="sxs-lookup"><span data-stu-id="cb056-166">Plug in the power supply.</span></span>

   ![Conectar à fonte de alimentação](media/iot-hub-intel-edison-kit-node-get-started/8_plug_power.jpg)

2. <span data-ttu-id="cb056-168">Um LED verde (rotulado como DS1 na placa de expansão Arduino*) deve acender e permanecer aceso.</span><span class="sxs-lookup"><span data-stu-id="cb056-168">A green LED(labeled DS1 on the Arduino* expansion board) should light up and stay lit.</span></span>

3. <span data-ttu-id="cb056-169">Aguarde um minuto para a placa concluir a inicialização.</span><span class="sxs-lookup"><span data-stu-id="cb056-169">Wait one minute for the board to finish booting up.</span></span>

   > [!NOTE]
   > <span data-ttu-id="cb056-170">Se não tiver uma fonte de alimentação CC, você ainda poderá ligar a placa usando uma porta USB.</span><span class="sxs-lookup"><span data-stu-id="cb056-170">If you do not have a DC power supply, you can still power the board through a USB port.</span></span> <span data-ttu-id="cb056-171">Confira a seção `Connect Edison to your computer` para obter detalhes.</span><span class="sxs-lookup"><span data-stu-id="cb056-171">See `Connect Edison to your computer` section for details.</span></span> <span data-ttu-id="cb056-172">Ligar sua placa dessa maneira pode resultar em um comportamento imprevisível da placa, especialmente ao usar Wi-Fi ou motores de acionamento.</span><span class="sxs-lookup"><span data-stu-id="cb056-172">Powering your board in this fashion may result in unpredictable behavior from your board, especially when using Wi-Fi or driving motors.</span></span>

### <a name="connect-edison-to-your-computer"></a><span data-ttu-id="cb056-173">Conectar o Edison ao computador</span><span class="sxs-lookup"><span data-stu-id="cb056-173">Connect Edison to your computer</span></span>

1. <span data-ttu-id="cb056-174">Mude a posição do microcomutador para baixo, na direção das duas portas micro USB, para que o Edison fique no modo de dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cb056-174">Toggle down the microswitch towards the two micro USB ports, so that Edison is in device mode.</span></span> <span data-ttu-id="cb056-175">Veja [aqui](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode) as diferenças entre o modo de dispositivo e o modo de host.</span><span class="sxs-lookup"><span data-stu-id="cb056-175">For differences between device mode and host mode, please reference [here](https://software.intel.com/en-us/node/628233#usb-device-mode-vs-usb-host-mode).</span></span>

   ![Mudar a posição do microcomutador para baixo](media/iot-hub-intel-edison-kit-node-get-started/9_toggle_down_microswitch.jpg)

2. <span data-ttu-id="cb056-177">Conecte o cabo micro USB à porta micro USB superior.</span><span class="sxs-lookup"><span data-stu-id="cb056-177">Plug the micro USB cable into the top micro USB port.</span></span>

   ![Porta micro USB superior](media/iot-hub-intel-edison-kit-node-get-started/10_top_usbport.jpg)

3. <span data-ttu-id="cb056-179">Conecte a outra extremidade do cabo USB ao computador.</span><span class="sxs-lookup"><span data-stu-id="cb056-179">Plug the other end of USB cable into your computer.</span></span>

   ![USB do computador](media/iot-hub-intel-edison-kit-node-get-started/11_computer_usb.jpg)

4. <span data-ttu-id="cb056-181">Você saberá que a placa foi inicializada completamente quando o computador montar uma nova unidade (muito semelhante a inserir um cartão SD no computador).</span><span class="sxs-lookup"><span data-stu-id="cb056-181">You will know that your board is fully initialized when your computer mounts a new drive (much like inserting a SD card into your computer).</span></span>

## <a name="download-and-run-the-configuration-tool"></a><span data-ttu-id="cb056-182">Baixe e execute a ferramenta de configuração</span><span class="sxs-lookup"><span data-stu-id="cb056-182">Download and run the configuration tool</span></span>
<span data-ttu-id="cb056-183">Obtenha a ferramenta de configuração mais recente [deste link](https://software.intel.com/en-us/iot/hardware/edison/downloads), listada sob o título `Installers`.</span><span class="sxs-lookup"><span data-stu-id="cb056-183">Get the latest configuration tool from [this link](https://software.intel.com/en-us/iot/hardware/edison/downloads) listed under the `Installers` heading.</span></span> <span data-ttu-id="cb056-184">Execute a ferramenta e siga as instruções na tela, clicando em Avançar quando necessário</span><span class="sxs-lookup"><span data-stu-id="cb056-184">Execute the tool and follow its on-screen instructions, clicking Next where needed</span></span>

### <a name="flash-firmware"></a><span data-ttu-id="cb056-185">Atualizar o firmware</span><span class="sxs-lookup"><span data-stu-id="cb056-185">Flash firmware</span></span>
1. <span data-ttu-id="cb056-186">Na página `Set up options`, clique em `Flash Firmware`.</span><span class="sxs-lookup"><span data-stu-id="cb056-186">On the `Set up options` page, click `Flash Firmware`.</span></span>
2. <span data-ttu-id="cb056-187">Selecione a imagem para atualizar sua placa seguindo um destes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="cb056-187">Select the image to flash onto your board by doing one of the following:</span></span>
   - <span data-ttu-id="cb056-188">Para baixar e atualizar sua placa com a imagem de firmware mais recente disponível da Intel, selecione `Download the latest image version xxxx`.</span><span class="sxs-lookup"><span data-stu-id="cb056-188">To download and flash your board with the latest firmware image available from Intel, select `Download the latest image version xxxx`.</span></span>
   - <span data-ttu-id="cb056-189">Para atualizar sua placa com uma imagem que você já salvou no computador, selecione `Select the local image`.</span><span class="sxs-lookup"><span data-stu-id="cb056-189">To flash your board with an image you already have saved on your computer, select `Select the local image`.</span></span> <span data-ttu-id="cb056-190">Navegue e selecione a imagem com que você quer atualizar a placa.</span><span class="sxs-lookup"><span data-stu-id="cb056-190">Browse to and select the image you want to flash to your board.</span></span>
3. <span data-ttu-id="cb056-191">A ferramenta de configuração tentará atualizar a placa.</span><span class="sxs-lookup"><span data-stu-id="cb056-191">The setup tool will attempt to flash your board.</span></span> <span data-ttu-id="cb056-192">Todo o processo de atualização pode levar até 10 minutos.</span><span class="sxs-lookup"><span data-stu-id="cb056-192">The entire flashing process may take up to 10 minutes.</span></span>

### <a name="set-password"></a><span data-ttu-id="cb056-193">Definir senha</span><span class="sxs-lookup"><span data-stu-id="cb056-193">Set password</span></span>
1. <span data-ttu-id="cb056-194">Na página `Set up options`, clique em `Enable Security`.</span><span class="sxs-lookup"><span data-stu-id="cb056-194">On the `Set up options` page, click `Enable Security`.</span></span>
2. <span data-ttu-id="cb056-195">É possível definir um nome personalizado para sua placa Intel® Edison.</span><span class="sxs-lookup"><span data-stu-id="cb056-195">You can set a custom name for your Intel® Edison board.</span></span> <span data-ttu-id="cb056-196">Isso é opcional.</span><span class="sxs-lookup"><span data-stu-id="cb056-196">This is optional.</span></span>
3. <span data-ttu-id="cb056-197">Digite uma senha para a placa e clique em `Set password`.</span><span class="sxs-lookup"><span data-stu-id="cb056-197">Type a password for your board, then click `Set password`.</span></span>
4. <span data-ttu-id="cb056-198">Marque a senha, que será usada mais tarde.</span><span class="sxs-lookup"><span data-stu-id="cb056-198">Mark down the password, which is used later.</span></span>

### <a name="connect-wi-fi"></a><span data-ttu-id="cb056-199">Conectar ao Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="cb056-199">Connect Wi-Fi</span></span>
1. <span data-ttu-id="cb056-200">Na página `Set up options`, clique em `Connect Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="cb056-200">On the `Set up options` page, click `Connect Wi-Fi`.</span></span> <span data-ttu-id="cb056-201">Aguarde até um minuto para que seu computador identifique as redes Wi-Fi disponíveis.</span><span class="sxs-lookup"><span data-stu-id="cb056-201">Wait up to one minute as your computer scans for available Wi-Fi networks.</span></span>
2. <span data-ttu-id="cb056-202">Na lista suspensa `Detected Networks`, selecione a rede.</span><span class="sxs-lookup"><span data-stu-id="cb056-202">From the `Detected Networks` drop-down list, select your network.</span></span>
3. <span data-ttu-id="cb056-203">Na lista suspensa `Security`, selecione o tipo de segurança da rede.</span><span class="sxs-lookup"><span data-stu-id="cb056-203">From the `Security` drop-down list, select the network's security type.</span></span>
4. <span data-ttu-id="cb056-204">Forneça suas informações de logon e senha e clique em `Configure Wi-Fi`.</span><span class="sxs-lookup"><span data-stu-id="cb056-204">Provide your login and password information, then click `Configure Wi-Fi`.</span></span>
5. <span data-ttu-id="cb056-205">Marque o endereço IP, que será usado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="cb056-205">Mark down the IP address, which is used later.</span></span>

> [!NOTE]
> <span data-ttu-id="cb056-206">Verifique se o Edison está conectado à mesma rede que o computador.</span><span class="sxs-lookup"><span data-stu-id="cb056-206">Make sure that Edison is connected to the same network as your computer.</span></span> <span data-ttu-id="cb056-207">Seu computador se conecta ao Edison usando o endereço IP.</span><span class="sxs-lookup"><span data-stu-id="cb056-207">Your computer connects to your Edison by using the IP address.</span></span>

   ![Conectar ao sensor de temperatura](media/iot-hub-intel-edison-kit-node-get-started/12_configuration_tool.png)

<span data-ttu-id="cb056-209">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="cb056-209">Congratulations!</span></span> <span data-ttu-id="cb056-210">Você configurou o Edison com êxito.</span><span class="sxs-lookup"><span data-stu-id="cb056-210">You've successfully configured Edison.</span></span>

## <a name="run-a-sample-application-on-intel-edison"></a><span data-ttu-id="cb056-211">Executar um exemplo de aplicativo no Intel Edison</span><span class="sxs-lookup"><span data-stu-id="cb056-211">Run a sample application on Intel Edison</span></span>

### <a name="prepare-the-azure-iot-device-sdk"></a><span data-ttu-id="cb056-212">Preparar o SDK do dispositivo IoT do Azure</span><span class="sxs-lookup"><span data-stu-id="cb056-212">Prepare the Azure IoT Device SDK</span></span>

1. <span data-ttu-id="cb056-213">Use um dos seguintes clientes SSH do seu computador host para se conectar ao Intel Edison.</span><span class="sxs-lookup"><span data-stu-id="cb056-213">Use one of the following SSH clients from your host computer to connect to your Intel Edison.</span></span> <span data-ttu-id="cb056-214">O endereço IP é da ferramenta de configuração, e a senha é aquela que você definiu na ferramenta.</span><span class="sxs-lookup"><span data-stu-id="cb056-214">The IP address is from the configuration tool and the password is the one you've set in that tool.</span></span>
    - <span data-ttu-id="cb056-215">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="cb056-215">[PuTTY](http://www.putty.org/) for Windows.</span></span>
    - <span data-ttu-id="cb056-216">O cliente SSH interno no Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="cb056-216">The built-in SSH client on Ubuntu or macOS.</span></span>

2. <span data-ttu-id="cb056-217">Clone o exemplo de aplicativo cliente com seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="cb056-217">Clone the sample client app to your device.</span></span> 
   
   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-intel-edison-client-app
   ```

3. <span data-ttu-id="cb056-218">Em seguida, navegue até a pasta do repositório para executar o comando a seguir para instalar todos os pacotes. Isso levará alguns minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="cb056-218">Then navigate to the repo folder to run the following command to install all packages, it may take serval minutes to complete.</span></span>
   
   ```bash
   cd iot-hub-node-intel-edison-client-app
   npm install
   ```


### <a name="configure-and-run-the-sample-application"></a><span data-ttu-id="cb056-219">Configurar e executar um aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="cb056-219">Configure and run the sample application</span></span>

1. <span data-ttu-id="cb056-220">Abra o arquivo de configuração executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="cb056-220">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Arquivo de configuração](media/iot-hub-intel-edison-kit-node-get-started/13_configure_file.png)

   <span data-ttu-id="cb056-222">Há duas macros que você pode configurar nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="cb056-222">There are two macros in this file you can configurate.</span></span> <span data-ttu-id="cb056-223">A primeira é a `INTERVAL`, que define o intervalo de tempo entre duas mensagens que são enviadas para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="cb056-223">The first one is `INTERVAL`, which defines the time interval between two messages that send to cloud.</span></span> <span data-ttu-id="cb056-224">O segundo, o `simulatedData`, é um valor booliano para definir se os dados simulados de sensor serão usados ou não.</span><span class="sxs-lookup"><span data-stu-id="cb056-224">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="cb056-225">Se você **não tiver o sensor**, defina o valor `simulatedData` como `true` para fazer com que o aplicativo de exemplo crie e use dados simulados de sensor.</span><span class="sxs-lookup"><span data-stu-id="cb056-225">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="cb056-226">Salve e saia pressionando CTRL+O > ENTER > CTRL+X.</span><span class="sxs-lookup"><span data-stu-id="cb056-226">Save and exit by pressing Control-O > Enter > Control-X.</span></span>


1. <span data-ttu-id="cb056-227">Execute o aplicativo de exemplo com seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="cb056-227">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="cb056-228">Verifique se você copiou e colou a cadeia de conexão do dispositivo em aspas simples.</span><span class="sxs-lookup"><span data-stu-id="cb056-228">Make sure you copy-paste the device connection string into the single quotes.</span></span>

<span data-ttu-id="cb056-229">Você deverá ver a seguinte saída, mostrando os dados do sensor e as mensagens que são enviadas ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cb056-229">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Saída – dados de sensor enviados do Intel Edison para o seu Hub IoT](media/iot-hub-intel-edison-kit-node-get-started/15_message_sent.png)

## <a name="next-steps"></a><span data-ttu-id="cb056-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="cb056-231">Next steps</span></span>

<span data-ttu-id="cb056-232">Você executou um aplicativo de exemplo para coletar dados de sensor e enviá-los ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="cb056-232">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
