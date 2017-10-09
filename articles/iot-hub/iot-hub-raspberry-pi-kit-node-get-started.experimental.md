---
title: aaaRaspberry Pi toocloud (Node. js) - conectar framboesa Pi tooAzure IoT Hub | Microsoft Docs
description: Conecte-se framboesa Pi tooAzure IoT Hub para Pi framboesa toosend dados toohello nuvem do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: Azure iot framboesa pi, framboesa pi iot hub, framboesa pi enviar dados toocloud, framboesa pi toocloud
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.openlocfilehash: 07bc66983c427eab8118be18d91abb25deb03ad3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-raspberry-pi-tooazure-iot-hub-nodejs"></a><span data-ttu-id="9ff88-104">Conecte-se framboesa Pi tooAzure IoT Hub (Node. js)</span><span class="sxs-lookup"><span data-stu-id="9ff88-104">Connect Raspberry Pi tooAzure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="9ff88-105">Neste tutorial, você começar a aprender Noções básicas de saudação do trabalho com Pi framboesa que está executando Raspbian.</span><span class="sxs-lookup"><span data-stu-id="9ff88-105">In this tutorial, you begin by learning hello basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="9ff88-106">Em seguida, você aprenderá como tooseamlessly se conectar a sua nuvem de toohello dispositivos usando [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="9ff88-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="9ff88-107">Para obter exemplos do Windows 10 IoT Core, vá toohello [Centro de desenvolvimento do Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="9ff88-107">For Windows 10 IoT Core samples, go toohello [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="9ff88-108">Não tem um dispositivo ainda?</span><span class="sxs-lookup"><span data-stu-id="9ff88-108">Don't have a kit yet?</span></span> <span data-ttu-id="9ff88-109">Tente Olá [emulador framboesa Pi 3](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span><span class="sxs-lookup"><span data-stu-id="9ff88-109">Try hello [Raspberry Pi 3 emulator](https://blogs.msdn.microsoft.com/iliast/2016/11/10/how-to-emulate-raspberry-pi/).</span></span> <span data-ttu-id="9ff88-110">Ou compre um novo kit de [aqui](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="9ff88-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="9ff88-111">O que fazer</span><span class="sxs-lookup"><span data-stu-id="9ff88-111">What you do</span></span>

* <span data-ttu-id="9ff88-112">Instale o Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="9ff88-112">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="9ff88-113">Crie um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9ff88-113">Create an IoT hub.</span></span>
* <span data-ttu-id="9ff88-114">Registre um dispositivo para o Pi em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="9ff88-114">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="9ff88-115">Execute um aplicativo de exemplo no hub IoT tooyour de dados do Pi toosend sensor.</span><span class="sxs-lookup"><span data-stu-id="9ff88-115">Run a sample application on Pi toosend sensor data tooyour IoT hub.</span></span>

<span data-ttu-id="9ff88-116">Conecte-se o hub IoT do Pi framboesa tooan que você criar.</span><span class="sxs-lookup"><span data-stu-id="9ff88-116">Connect Raspberry Pi tooan IoT hub that you create.</span></span> <span data-ttu-id="9ff88-117">Em seguida, executar um aplicativo de exemplo em dados de temperatura e umidade toocollect Pi a partir de um sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="9ff88-117">Then you run a sample application on Pi toocollect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="9ff88-118">Por fim, você pode enviar hub IoT do hello sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="9ff88-118">Finally, you send hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="9ff88-119">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="9ff88-119">What you learn</span></span>

* <span data-ttu-id="9ff88-120">Como toocreate um hub IoT do Azure e obter sua nova cadeia de caracteres de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="9ff88-120">How toocreate an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="9ff88-121">Como tooconnect Pi com um sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="9ff88-121">How tooconnect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="9ff88-122">Como os dados do sensor toocollect executando um aplicativo de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="9ff88-122">How toocollect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="9ff88-123">Como hub IoT do toosend sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="9ff88-123">How toosend sensor data tooyour IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="9ff88-124">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="9ff88-124">What you need</span></span>

![O que você precisa](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="9ff88-126">Olá framboesa Pi 2 ou 3 de Pi framboesa quadro.</span><span class="sxs-lookup"><span data-stu-id="9ff88-126">hello Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="9ff88-127">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="9ff88-127">An active Azure subscription.</span></span> <span data-ttu-id="9ff88-128">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="9ff88-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="9ff88-129">Um monitor, um USB teclado e mouse que se conectam tooPi.</span><span class="sxs-lookup"><span data-stu-id="9ff88-129">A monitor, a USB keyboard, and mouse that connect tooPi.</span></span>
* <span data-ttu-id="9ff88-130">Um Mac ou PC que esteja executando Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="9ff88-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="9ff88-131">Uma conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="9ff88-131">An Internet connection.</span></span>
* <span data-ttu-id="9ff88-132">Um cartão microSD de 16 GB ou superior.</span><span class="sxs-lookup"><span data-stu-id="9ff88-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="9ff88-133">Um SD USB adaptador ou microSD cartão tooburn Olá imagem do sistema operacional em um cartão microSD de saudação.</span><span class="sxs-lookup"><span data-stu-id="9ff88-133">A USB-SD adapter or microSD card tooburn hello operating system image onto hello microSD card.</span></span>
* <span data-ttu-id="9ff88-134">Fornecer uma potência de 2 amp volt 5 cabo micro-6 pés hello.</span><span class="sxs-lookup"><span data-stu-id="9ff88-134">A 5-volt 2-amp power supply with hello 6-foot micro USB cable.</span></span>

<span data-ttu-id="9ff88-135">Olá itens a seguir é opcional:</span><span class="sxs-lookup"><span data-stu-id="9ff88-135">hello following items are optional:</span></span>

* <span data-ttu-id="9ff88-136">Um sensor de umidade, temperatura e pressão Adafruit BME280 montado.</span><span class="sxs-lookup"><span data-stu-id="9ff88-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="9ff88-137">Uma placa universal.</span><span class="sxs-lookup"><span data-stu-id="9ff88-137">A breadboard.</span></span>
* <span data-ttu-id="9ff88-138">Cabos de jumper fêmea/macho de 15,2 cm.</span><span class="sxs-lookup"><span data-stu-id="9ff88-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="9ff88-139">Um LED de 10 mm difuso.</span><span class="sxs-lookup"><span data-stu-id="9ff88-139">A diffused 10-mm LED.</span></span>

  > [!NOTE] 
  <span data-ttu-id="9ff88-140">Esses itens são opcionais, porque o suporte de exemplo de código Olá simulados dados do sensor.</span><span class="sxs-lookup"><span data-stu-id="9ff88-140">These items are optional because hello code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="9ff88-141">Instalar o Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="9ff88-141">Setup Raspberry Pi</span></span>

### <a name="install-hello-raspbian-operating-system-for-pi"></a><span data-ttu-id="9ff88-142">Instalar o sistema de operacional Raspbian Olá para Pi</span><span class="sxs-lookup"><span data-stu-id="9ff88-142">Install hello Raspbian operating system for Pi</span></span>

<span data-ttu-id="9ff88-143">Prepare um cartão microSD de saudação para a instalação da imagem de Raspbian hello.</span><span class="sxs-lookup"><span data-stu-id="9ff88-143">Prepare hello microSD card for installation of hello Raspbian image.</span></span>

1. <span data-ttu-id="9ff88-144">Baixe o Raspbian.</span><span class="sxs-lookup"><span data-stu-id="9ff88-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="9ff88-145">[Baixar Raspbian Jessie com Pixel](https://www.raspberrypi.org/downloads/raspbian/) (arquivo. zip de saudação).</span><span class="sxs-lookup"><span data-stu-id="9ff88-145">[Download Raspbian Jessie with Pixel](https://www.raspberrypi.org/downloads/raspbian/) (hello .zip file).</span></span>
   1. <span data-ttu-id="9ff88-146">Extrai Olá Raspbian imagem tooa pasta do computador.</span><span class="sxs-lookup"><span data-stu-id="9ff88-146">Extract hello Raspbian image tooa folder on your computer.</span></span>
1. <span data-ttu-id="9ff88-147">Instale Raspbian toohello microSD cartão.</span><span class="sxs-lookup"><span data-stu-id="9ff88-147">Install Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="9ff88-148">[Baixe e instale o utilitário de gravador Olá Etcher SD cartão](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="9ff88-148">[Download and install hello Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="9ff88-149">Execute Etcher e selecione a imagem de Raspbian de saudação extraído na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="9ff88-149">Run Etcher and select hello Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="9ff88-150">Selecione a unidade de cartão microSD hello.</span><span class="sxs-lookup"><span data-stu-id="9ff88-150">Select hello microSD card drive.</span></span> <span data-ttu-id="9ff88-151">Observe que Etcher talvez já selecionou unidade correta hello.</span><span class="sxs-lookup"><span data-stu-id="9ff88-151">Note that Etcher may have already selected hello correct drive.</span></span>
   1. <span data-ttu-id="9ff88-152">Clique em Flash tooinstall Raspbian toohello microSD cartão.</span><span class="sxs-lookup"><span data-stu-id="9ff88-152">Click Flash tooinstall Raspbian toohello microSD card.</span></span>
   1. <span data-ttu-id="9ff88-153">Remova o cartão microSD de saudação do seu computador quando a instalação for concluída.</span><span class="sxs-lookup"><span data-stu-id="9ff88-153">Remove hello microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="9ff88-154">É cartão de microSD tooremove seguro Olá diretamente porque Etcher automaticamente ejeta ou desmonta cartão microSD de saudação após a conclusão.</span><span class="sxs-lookup"><span data-stu-id="9ff88-154">It's safe tooremove hello microSD card directly because Etcher automatically ejects or unmounts hello microSD card upon completion.</span></span>
   1. <span data-ttu-id="9ff88-155">Inserir cartão microSD de saudação Pi.</span><span class="sxs-lookup"><span data-stu-id="9ff88-155">Insert hello microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="9ff88-156">Habilitar SSH e I2C</span><span class="sxs-lookup"><span data-stu-id="9ff88-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="9ff88-157">Conecte-se o monitor de toohello de Pi, teclado e mouse, iniciar Pi e, em seguida, faça logon em Raspbian usando `pi` como nome de usuário hello e `raspberry` como senha hello.</span><span class="sxs-lookup"><span data-stu-id="9ff88-157">Connect Pi toohello monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as hello user name and `raspberry` as hello password.</span></span>
1. <span data-ttu-id="9ff88-158">Clique em Olá ícone framboesa > **preferências** > **framboesa Pi configuração**.</span><span class="sxs-lookup"><span data-stu-id="9ff88-158">Click hello Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![menu de preferências Raspbian Olá](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="9ff88-160">Em Olá **Interfaces** guia, defina **I2C** e **SSH** muito**habilitar**e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="9ff88-160">On hello **Interfaces** tab, set **I2C** and **SSH** too**Enable**, and then click **OK**.</span></span> <span data-ttu-id="9ff88-161">Se você não tiver sensores físicos e deseja que os dados do sensor toouse simulada, esta etapa é opcional.</span><span class="sxs-lookup"><span data-stu-id="9ff88-161">If you don't have physical sensors and want toouse simulated sensor data, this step is optional.</span></span>

   ![Habilitar I2C e SSH no Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="9ff88-163">tooenable SSH e I2C, você pode encontrar mais documentos de referência na [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) e [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="9ff88-163">tooenable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-hello-sensor-toopi"></a><span data-ttu-id="9ff88-164">Conecte-se Olá sensor tooPi</span><span class="sxs-lookup"><span data-stu-id="9ff88-164">Connect hello sensor tooPi</span></span>

<span data-ttu-id="9ff88-165">Use Olá breadboard e jumper fios tooconnect um LED e um tooPi BME280 da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="9ff88-165">Use hello breadboard and jumper wires tooconnect an LED and a BME280 tooPi as follows.</span></span> <span data-ttu-id="9ff88-166">Se você não tiver o sensor hello, ignore esta seção.</span><span class="sxs-lookup"><span data-stu-id="9ff88-166">If you don’t have hello sensor, skip this section.</span></span>

![Olá framboesa Pi e o sensor de conexão](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="9ff88-168">sensor de saudação BME280 pode coletar dados de temperatura e umidade.</span><span class="sxs-lookup"><span data-stu-id="9ff88-168">hello BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="9ff88-169">E Olá LED pisca se houver uma comunicação entre o dispositivo e hello nuvem.</span><span class="sxs-lookup"><span data-stu-id="9ff88-169">And hello LED will blink if there is a communication between device and hello cloud.</span></span> 

<span data-ttu-id="9ff88-170">Pinos do sensor, use Olá fiação a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ff88-170">For sensor pins, use hello following wiring:</span></span>

| <span data-ttu-id="9ff88-171">Início (Sensor e LED)</span><span class="sxs-lookup"><span data-stu-id="9ff88-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="9ff88-172">End (quadro)</span><span class="sxs-lookup"><span data-stu-id="9ff88-172">End (Board)</span></span>            | <span data-ttu-id="9ff88-173">Cor de cabo</span><span class="sxs-lookup"><span data-stu-id="9ff88-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="9ff88-174">VDD (pino 5G)</span><span class="sxs-lookup"><span data-stu-id="9ff88-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="9ff88-175">3,3 v PWR (pino 1)</span><span class="sxs-lookup"><span data-stu-id="9ff88-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="9ff88-176">Cabo branco</span><span class="sxs-lookup"><span data-stu-id="9ff88-176">White cable</span></span>   |
| <span data-ttu-id="9ff88-177">GND (pino 7G)</span><span class="sxs-lookup"><span data-stu-id="9ff88-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="9ff88-178">GND (pino 6)</span><span class="sxs-lookup"><span data-stu-id="9ff88-178">GND (Pin 6)</span></span>            | <span data-ttu-id="9ff88-179">Cabo marrom</span><span class="sxs-lookup"><span data-stu-id="9ff88-179">Brown cable</span></span>   |
| <span data-ttu-id="9ff88-180">SCK (pino 8G)</span><span class="sxs-lookup"><span data-stu-id="9ff88-180">SCK (Pin 8G)</span></span>             | <span data-ttu-id="9ff88-181">I2C1 SDA (pino 3)</span><span class="sxs-lookup"><span data-stu-id="9ff88-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="9ff88-182">Cabo laranja</span><span class="sxs-lookup"><span data-stu-id="9ff88-182">Orange cable</span></span>  |
| <span data-ttu-id="9ff88-183">SDI (pino 10G)</span><span class="sxs-lookup"><span data-stu-id="9ff88-183">SDI (Pin 10G)</span></span>            | <span data-ttu-id="9ff88-184">I2C1 SCL (pino 5)</span><span class="sxs-lookup"><span data-stu-id="9ff88-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="9ff88-185">Cabo vermelho</span><span class="sxs-lookup"><span data-stu-id="9ff88-185">Red cable</span></span>     |
| <span data-ttu-id="9ff88-186">LED VDD (pino 18F)</span><span class="sxs-lookup"><span data-stu-id="9ff88-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="9ff88-187">GPIO 24 (pino 18)</span><span class="sxs-lookup"><span data-stu-id="9ff88-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="9ff88-188">Cabo branco</span><span class="sxs-lookup"><span data-stu-id="9ff88-188">White cable</span></span>   |
| <span data-ttu-id="9ff88-189">LED GND (pino 17F)</span><span class="sxs-lookup"><span data-stu-id="9ff88-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="9ff88-190">GND (pino 20)</span><span class="sxs-lookup"><span data-stu-id="9ff88-190">GND (Pin 20)</span></span>           | <span data-ttu-id="9ff88-191">Cabo preto</span><span class="sxs-lookup"><span data-stu-id="9ff88-191">Black cable</span></span>   |

<span data-ttu-id="9ff88-192">Clique em tooview [framboesa Pi 2 e 3 mapeamentos de Pin](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para referência.</span><span class="sxs-lookup"><span data-stu-id="9ff88-192">Click tooview [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="9ff88-193">Depois de se conectar com êxito BME280 tooyour framboesa Pi, ele deve ser como abaixo de imagem.</span><span class="sxs-lookup"><span data-stu-id="9ff88-193">After you've successfully connected BME280 tooyour Raspberry Pi, it should be like below image.</span></span>

![Pi e BME280 conectados](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-toohello-network"></a><span data-ttu-id="9ff88-195">Conectar a rede de toohello Pi</span><span class="sxs-lookup"><span data-stu-id="9ff88-195">Connect Pi toohello network</span></span>

<span data-ttu-id="9ff88-196">Ative o Pi usando cabo USB da micro hello e fonte de alimentação hello.</span><span class="sxs-lookup"><span data-stu-id="9ff88-196">Turn on Pi by using hello micro USB cable and hello power supply.</span></span> <span data-ttu-id="9ff88-197">Use Olá Ethernet cabo tooconnect Pi tooyour com fio de rede ou siga Olá [instruções de saudação framboesa Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) rede sem fio do tooyour tooconnect Pi.</span><span class="sxs-lookup"><span data-stu-id="9ff88-197">Use hello Ethernet cable tooconnect Pi tooyour wired network or follow hello [instructions from hello Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) tooconnect Pi tooyour wireless network.</span></span> <span data-ttu-id="9ff88-198">Após o Pi rede toohello conectado com êxito, você precisa tootake nota da saudação [endereço IP do seu Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="9ff88-198">After your Pi has been successfully connected toohello network, you need tootake a note of hello [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Rede toowired conectado](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="9ff88-200">Certifique-se de Pi é conectado toohello mesmo de rede do computador.</span><span class="sxs-lookup"><span data-stu-id="9ff88-200">Make sure that Pi is connected toohello same network as your computer.</span></span> <span data-ttu-id="9ff88-201">Por exemplo, se o computador estiver rede sem fio conectada tooa enquanto Pi é conectado tooa rede com fio, talvez você não veja Olá IP endereço na saída de devdisco hello.</span><span class="sxs-lookup"><span data-stu-id="9ff88-201">For example, if your computer is connected tooa wireless network while Pi is connected tooa wired network, you might not see hello IP address in hello devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="9ff88-202">Executar um aplicativo de exemplo no Pi</span><span class="sxs-lookup"><span data-stu-id="9ff88-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-hello-prerequisite-packages"></a><span data-ttu-id="9ff88-203">Clonar um aplicativo de exemplo e instalar pacotes de pré-requisito Olá</span><span class="sxs-lookup"><span data-stu-id="9ff88-203">Clone sample application and install hello prerequisite packages</span></span>

1. <span data-ttu-id="9ff88-204">Use um dos Olá seguir SSH clientes de sua tooyour de tooconnect do computador host framboesa Pi.</span><span class="sxs-lookup"><span data-stu-id="9ff88-204">Use one of hello following SSH clients from your host computer tooconnect tooyour Raspberry Pi.</span></span>
    - <span data-ttu-id="9ff88-205">[PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="9ff88-205">[PuTTY](http://www.putty.org/) for Windows.</span></span> <span data-ttu-id="9ff88-206">Você precisa Olá endereço IP de seu tooconnect Pi-los por meio do SSH.</span><span class="sxs-lookup"><span data-stu-id="9ff88-206">You need hello IP address of your Pi tooconnect it via SSH.</span></span>
    - <span data-ttu-id="9ff88-207">Olá SSH do cliente interno Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="9ff88-207">hello built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="9ff88-208">Você pode precisar executar `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span><span class="sxs-lookup"><span data-stu-id="9ff88-208">You might need run `ssh pi@<ip address of pi>` tooconnect Pi via SSH.</span></span>

   > [!NOTE] 
   <span data-ttu-id="9ff88-209">é o nome de usuário do saudação padrão `pi` , e a senha de saudação é `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="9ff88-209">hello default username is `pi` , and hello password is `raspberry`.</span></span>

1. <span data-ttu-id="9ff88-210">Instale o Node. js e NPM tooyour Pi.</span><span class="sxs-lookup"><span data-stu-id="9ff88-210">Install Node.js and NPM tooyour Pi.</span></span>
   
   <span data-ttu-id="9ff88-211">Primeiro você deve verificar a versão do Node. js com hello comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="9ff88-211">First you should check your Node.js version with hello following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="9ff88-212">Se Olá versão for inferior a 4. x ou não há nenhum Node. js no seu Pi, em seguida, executar Olá tooinstall de comando a seguir ou atualizar Node. js.</span><span class="sxs-lookup"><span data-stu-id="9ff88-212">If hello version is lower than 4.x or there is no Node.js on your Pi, then run hello following command tooinstall or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="9ff88-213">Aplicativo de exemplo hello executando o comando a seguir de saudação do clone:</span><span class="sxs-lookup"><span data-stu-id="9ff88-213">Clone hello sample application by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="9ff88-214">Instale todos os pacotes de saudação comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="9ff88-214">Install all packages by hello following command.</span></span> <span data-ttu-id="9ff88-215">Ele inclui o SDK do dispositivo IoT do Azure, a biblioteca do Sensor BME280 e a biblioteca de fiação do Pi.</span><span class="sxs-lookup"><span data-stu-id="9ff88-215">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="9ff88-216">Pode levar vários toofinish de minutos esse denpening do processo de instalação na sua conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="9ff88-216">It might take several minutes toofinish this installation process denpening on your network connection.</span></span>

### <a name="configure-hello-sample-application"></a><span data-ttu-id="9ff88-217">Configurar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="9ff88-217">Configure hello sample application</span></span>

1. <span data-ttu-id="9ff88-218">Abra o arquivo de configuração de saudação executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ff88-218">Open hello config file by running hello following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Arquivo de configuração](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="9ff88-220">Há dois itens que podem ser configurados nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="9ff88-220">There are two items in this file you can configurate.</span></span> <span data-ttu-id="9ff88-221">Olá primeiro um é `interval`, que define o intervalo de tempo de saudação entre duas mensagens que enviar toocloud.</span><span class="sxs-lookup"><span data-stu-id="9ff88-221">hello first one is `interval`, which defines hello time interval between two messages that send toocloud.</span></span> <span data-ttu-id="9ff88-222">Olá segunda `simulatedData`, que é um valor booleano para se toouse simulados dados do sensor ou não.</span><span class="sxs-lookup"><span data-stu-id="9ff88-222">hello second one `simulatedData`,which is a Boolean value for whether toouse simulated sensor data or not.</span></span>

   <span data-ttu-id="9ff88-223">Se você **não tem o sensor Olá**, defina hello `simulatedData` valor muito`true` aplicativo de exemplo hello toomake criar e usar dados de sensor simulada.</span><span class="sxs-lookup"><span data-stu-id="9ff88-223">If you **don't have hello sensor**, set hello `simulatedData` value too`true` toomake hello sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="9ff88-224">Salve e saia pressionando CTRL+O > ENTER > CTRL+X.</span><span class="sxs-lookup"><span data-stu-id="9ff88-224">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-hello-sample-application"></a><span data-ttu-id="9ff88-225">Executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="9ff88-225">Run hello sample application</span></span>

1. <span data-ttu-id="9ff88-226">Execute o aplicativo de exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="9ff88-226">Run hello sample application by running hello following command:</span></span>

   ```bash
   sudo node index.js '<your Azure IoT hub device connection string>'
   ```

   > [!NOTE] 
   <span data-ttu-id="9ff88-227">Verifique se você copiar e colar cadeia de caracteres de conexão de dispositivo Olá em aspas hello.</span><span class="sxs-lookup"><span data-stu-id="9ff88-227">Make sure you copy-paste hello device connection string into hello single quotes.</span></span>


<span data-ttu-id="9ff88-228">Você verá a seguinte Olá saída mostra Olá sensor dados e hello mensagens enviadas tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9ff88-228">You should see hello following output that shows hello sensor data and hello messages that are sent tooyour IoT hub.</span></span>

![Saída - dados de sensor enviadas do Pi framboesa tooyour hub IoT](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="9ff88-230">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9ff88-230">Next steps</span></span>

<span data-ttu-id="9ff88-231">Executar dados de sensor de toocollect do aplicativo de exemplo e enviá-lo tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="9ff88-231">You’ve run a sample application toocollect sensor data and send it tooyour IoT hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]