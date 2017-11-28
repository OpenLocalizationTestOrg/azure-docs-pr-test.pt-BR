---
title: "Raspberry Pi para nuvem (Node.js) – Conectar o Raspberry Pi ao Hub IoT do Azure | Microsoft Docs"
description: "Neste tutorial, aprenda a configurar e conectar o Raspberry Pi ao Hub IoT do Azure para o Raspberry Pi enviar dados à plataforma de nuvem do Azure."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: raspberry pi azure iot, hub iot raspberry pi, raspberry pi enviar dados para a nuvem, raspberry pi para nuvem
ms.assetid: b0e14bfa-8e64-440a-a6ec-e507ca0f76ba
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 5/27/2017
ms.author: xshi
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: f48c4bd27b1df1d02090ed51172f943e50c76c3e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="connect-raspberry-pi-to-azure-iot-hub-nodejs"></a><span data-ttu-id="042a3-104">Conectar o Raspberry Pi ao Hub IoT do Azure (Node.js)</span><span class="sxs-lookup"><span data-stu-id="042a3-104">Connect Raspberry Pi to Azure IoT Hub (Node.js)</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

<span data-ttu-id="042a3-105">Neste tutorial, você começará aprendendo as noções básicas de como trabalhar com o Raspberry Pi que está executando o Raspbian.</span><span class="sxs-lookup"><span data-stu-id="042a3-105">In this tutorial, you begin by learning the basics of working with Raspberry Pi that's running Raspbian.</span></span> <span data-ttu-id="042a3-106">Em seguida, aprenderá a conectar seus dispositivos diretamente à nuvem usando o [Hub IoT do Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="042a3-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span> <span data-ttu-id="042a3-107">Para obter exemplos do Windows 10 IoT Core, acesse o [Centro de Desenvolvimento do Windows](http://www.windowsondevices.com/).</span><span class="sxs-lookup"><span data-stu-id="042a3-107">For Windows 10 IoT Core samples, go to the [Windows Dev Center](http://www.windowsondevices.com/).</span></span>

<span data-ttu-id="042a3-108">Não tem um dispositivo ainda?</span><span class="sxs-lookup"><span data-stu-id="042a3-108">Don't have a kit yet?</span></span> <span data-ttu-id="042a3-109">Experimente [Simulador online Raspberry Pi](iot-hub-raspberry-pi-web-simulator-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="042a3-109">Try [Raspberry Pi online simulator](iot-hub-raspberry-pi-web-simulator-get-started.md).</span></span> <span data-ttu-id="042a3-110">Ou compre um novo kit de [aqui](https://azure.microsoft.com/develop/iot/starter-kits).</span><span class="sxs-lookup"><span data-stu-id="042a3-110">Or buy a new kit [here](https://azure.microsoft.com/develop/iot/starter-kits).</span></span>


## <a name="what-you-do"></a><span data-ttu-id="042a3-111">O que fazer</span><span class="sxs-lookup"><span data-stu-id="042a3-111">What you do</span></span>

* <span data-ttu-id="042a3-112">Crie um Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="042a3-112">Create an IoT hub.</span></span>
* <span data-ttu-id="042a3-113">Registre um dispositivo para o Pi em seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="042a3-113">Register a device for Pi in your IoT hub.</span></span>
* <span data-ttu-id="042a3-114">Instale o Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="042a3-114">Setup Raspberry Pi.</span></span>
* <span data-ttu-id="042a3-115">Execute um aplicativo de exemplo no Pi para enviar os dados do sensor para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="042a3-115">Run a sample application on Pi to send sensor data to your IoT hub.</span></span>

<span data-ttu-id="042a3-116">Conecte o Raspberry Pi a um Hub IoT criado por você.</span><span class="sxs-lookup"><span data-stu-id="042a3-116">Connect Raspberry Pi to an IoT hub that you create.</span></span> <span data-ttu-id="042a3-117">Em seguida, execute um aplicativo de exemplo no Pi para coletar dados de temperatura e umidade de um sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="042a3-117">Then you run a sample application on Pi to collect temperature and humidity data from a BME280 sensor.</span></span> <span data-ttu-id="042a3-118">Por fim, você envia os dados do sensor para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="042a3-118">Finally, you send the sensor data to your IoT hub.</span></span>

## <a name="what-you-learn"></a><span data-ttu-id="042a3-119">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="042a3-119">What you learn</span></span>

* <span data-ttu-id="042a3-120">Como criar um Hub IoT do Azure e obter sua nova cadeia de conexão do dispositivo.</span><span class="sxs-lookup"><span data-stu-id="042a3-120">How to create an Azure IoT hub and get your new device connection string.</span></span>
* <span data-ttu-id="042a3-121">Como conectar o Pi a um sensor BME280.</span><span class="sxs-lookup"><span data-stu-id="042a3-121">How to connect Pi with a BME280 sensor.</span></span>
* <span data-ttu-id="042a3-122">Como coletar dados de sensor executando um aplicativo de exemplo no Pi.</span><span class="sxs-lookup"><span data-stu-id="042a3-122">How to collect sensor data by running a sample application on Pi.</span></span>
* <span data-ttu-id="042a3-123">Como enviar dados de sensor ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="042a3-123">How to send sensor data to your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="042a3-124">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="042a3-124">What you need</span></span>

![O que você precisa](media/iot-hub-raspberry-pi-kit-node-get-started/0_starter_kit.jpg)

* <span data-ttu-id="042a3-126">Da placa do Raspberry Pi 2 ou do Raspberry Pi 3.</span><span class="sxs-lookup"><span data-stu-id="042a3-126">The Raspberry Pi 2 or Raspberry Pi 3 board.</span></span>
* <span data-ttu-id="042a3-127">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="042a3-127">An active Azure subscription.</span></span> <span data-ttu-id="042a3-128">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="042a3-128">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="042a3-129">Um monitor, um teclado USB e mouse que se conectam ao Pi.</span><span class="sxs-lookup"><span data-stu-id="042a3-129">A monitor, a USB keyboard, and mouse that connect to Pi.</span></span>
* <span data-ttu-id="042a3-130">Um Mac ou PC que esteja executando Windows ou Linux.</span><span class="sxs-lookup"><span data-stu-id="042a3-130">A Mac or a PC that is running Windows or Linux.</span></span>
* <span data-ttu-id="042a3-131">Uma conexão com a Internet.</span><span class="sxs-lookup"><span data-stu-id="042a3-131">An Internet connection.</span></span>
* <span data-ttu-id="042a3-132">Um cartão microSD de 16 GB ou superior.</span><span class="sxs-lookup"><span data-stu-id="042a3-132">A 16 GB or above microSD card.</span></span>
* <span data-ttu-id="042a3-133">Um adaptador USB-SD ou um cartão microSD para gravar a imagem do sistema operacional no cartão microSD.</span><span class="sxs-lookup"><span data-stu-id="042a3-133">A USB-SD adapter or microSD card to burn the operating system image onto the microSD card.</span></span>
* <span data-ttu-id="042a3-134">Uma fonte de alimentação de 5 volts e 2 amperes com o cabo micro USB de 2,7 metros.</span><span class="sxs-lookup"><span data-stu-id="042a3-134">A 5-volt 2-amp power supply with the 6-foot micro USB cable.</span></span>

<span data-ttu-id="042a3-135">Os itens a seguir são opcionais:</span><span class="sxs-lookup"><span data-stu-id="042a3-135">The following items are optional:</span></span>

* <span data-ttu-id="042a3-136">Um sensor de umidade, temperatura e pressão Adafruit BME280 montado.</span><span class="sxs-lookup"><span data-stu-id="042a3-136">An assembled Adafruit BME280 temperature, pressure, and humidity sensor.</span></span>
* <span data-ttu-id="042a3-137">Uma placa universal.</span><span class="sxs-lookup"><span data-stu-id="042a3-137">A breadboard.</span></span>
* <span data-ttu-id="042a3-138">Cabos de jumper fêmea/macho de 15,2 cm.</span><span class="sxs-lookup"><span data-stu-id="042a3-138">6 F/M jumper wires.</span></span>
* <span data-ttu-id="042a3-139">Um LED de 10 mm difuso.</span><span class="sxs-lookup"><span data-stu-id="042a3-139">A diffused 10-mm LED.</span></span>


> [!NOTE] 
<span data-ttu-id="042a3-140">Esses itens são opcionais porque o exemplo de código dá suporte a dados simulados de sensor.</span><span class="sxs-lookup"><span data-stu-id="042a3-140">These items are optional because the code sample support simulated sensor data.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="setup-raspberry-pi"></a><span data-ttu-id="042a3-141">Instalar o Raspberry Pi</span><span class="sxs-lookup"><span data-stu-id="042a3-141">Setup Raspberry Pi</span></span>

### <a name="install-the-raspbian-operating-system-for-pi"></a><span data-ttu-id="042a3-142">Instalar o sistema operacional Raspbian para o Pi</span><span class="sxs-lookup"><span data-stu-id="042a3-142">Install the Raspbian operating system for Pi</span></span>

<span data-ttu-id="042a3-143">Preparar o cartão microSD para instalação da imagem do Raspbian.</span><span class="sxs-lookup"><span data-stu-id="042a3-143">Prepare the microSD card for installation of the Raspbian image.</span></span>

1. <span data-ttu-id="042a3-144">Baixe o Raspbian.</span><span class="sxs-lookup"><span data-stu-id="042a3-144">Download Raspbian.</span></span>
   1. <span data-ttu-id="042a3-145">[Baixe o Raspbian Jessie com área de trabalho](https://www.raspberrypi.org/downloads/raspbian/) (o arquivo .zip).</span><span class="sxs-lookup"><span data-stu-id="042a3-145">[Download Raspbian Jessie with Desktop](https://www.raspberrypi.org/downloads/raspbian/) (the .zip file).</span></span>
   1. <span data-ttu-id="042a3-146">Extraia a imagem do Raspbian em uma pasta no computador.</span><span class="sxs-lookup"><span data-stu-id="042a3-146">Extract the Raspbian image to a folder on your computer.</span></span>
1. <span data-ttu-id="042a3-147">Instale o Raspbian no cartão microSD.</span><span class="sxs-lookup"><span data-stu-id="042a3-147">Install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="042a3-148">[Baixe e instale o utilitário gravador de cartão SD Etcher](https://etcher.io/).</span><span class="sxs-lookup"><span data-stu-id="042a3-148">[Download and install the Etcher SD card burner utility](https://etcher.io/).</span></span>
   1. <span data-ttu-id="042a3-149">Execute o Etcher e selecione a imagem do Raspbian extraída na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="042a3-149">Run Etcher and select the Raspbian image that you extracted in step 1.</span></span>
   1. <span data-ttu-id="042a3-150">Selecione a unidade de cartão microSD.</span><span class="sxs-lookup"><span data-stu-id="042a3-150">Select the microSD card drive.</span></span> <span data-ttu-id="042a3-151">Observação que o Etcher talvez já tenha selecionado a unidade correta.</span><span class="sxs-lookup"><span data-stu-id="042a3-151">Note that Etcher may have already selected the correct drive.</span></span>
   1. <span data-ttu-id="042a3-152">Clique em Flash para instalar o Raspbian no cartão microSD.</span><span class="sxs-lookup"><span data-stu-id="042a3-152">Click Flash to install Raspbian to the microSD card.</span></span>
   1. <span data-ttu-id="042a3-153">Remova o cartão microSD do computador após a conclusão.</span><span class="sxs-lookup"><span data-stu-id="042a3-153">Remove the microSD card from your computer when installation is complete.</span></span> <span data-ttu-id="042a3-154">É seguro remover o cartão microSD diretamente porque o Etcher ejeta ou desmonta automaticamente o cartão microSD após a conclusão.</span><span class="sxs-lookup"><span data-stu-id="042a3-154">It's safe to remove the microSD card directly because Etcher automatically ejects or unmounts the microSD card upon completion.</span></span>
   1. <span data-ttu-id="042a3-155">Insira o cartão microSD no Pi.</span><span class="sxs-lookup"><span data-stu-id="042a3-155">Insert the microSD card into Pi.</span></span>

### <a name="enable-ssh-and-i2c"></a><span data-ttu-id="042a3-156">Habilitar SSH e I2C</span><span class="sxs-lookup"><span data-stu-id="042a3-156">Enable SSH and I2C</span></span>

1. <span data-ttu-id="042a3-157">Conecte o Pi ao monitor, ao teclado e ao mouse, inicie o Pi e, em seguida, faça logon no Raspbian usando `pi` como o nome de usuário e `raspberry` como a senha.</span><span class="sxs-lookup"><span data-stu-id="042a3-157">Connect Pi to the monitor, keyboard and mouse, start Pi and then log in Raspbian by using `pi` as the user name and `raspberry` as the password.</span></span>
1. <span data-ttu-id="042a3-158">Clique no ícone do Raspberry > **Preferências** > **Configuração do Raspberry Pi**.</span><span class="sxs-lookup"><span data-stu-id="042a3-158">Click the Raspberry icon > **Preferences** > **Raspberry Pi Configuration**.</span></span>

   ![O menu de Preferências do Raspbian](media/iot-hub-raspberry-pi-kit-node-get-started/1_raspbian-preferences-menu.png)

1. <span data-ttu-id="042a3-160">Na guia **Interfaces**, defina **I2C** e **SSH** como **Habilitar** e, em seguida, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="042a3-160">On the **Interfaces** tab, set **I2C** and **SSH** to **Enable**, and then click **OK**.</span></span> <span data-ttu-id="042a3-161">Se você não tiver sensores físicos e quiser usar dados de sensor simulados, esta etapa será opcional.</span><span class="sxs-lookup"><span data-stu-id="042a3-161">If you don't have physical sensors and want to use simulated sensor data, this step is optional.</span></span>

   ![Habilitar I2C e SSH no Raspberry Pi](media/iot-hub-raspberry-pi-kit-node-get-started/2_enable-i2c-ssh-on-raspberry-pi.png)

> [!NOTE] 
<span data-ttu-id="042a3-163">Para habilitar o SSH e o I2C, você pode encontrar mais documentos de referência em [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) e [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span><span class="sxs-lookup"><span data-stu-id="042a3-163">To enable SSH and I2C, you can find more reference documents on [raspberrypi.org](https://www.raspberrypi.org/documentation/remote-access/ssh/) and [Adafruit.com](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-4-gpio-setup/configuring-i2c).</span></span>

### <a name="connect-the-sensor-to-pi"></a><span data-ttu-id="042a3-164">Conectar o sensor ao Pi</span><span class="sxs-lookup"><span data-stu-id="042a3-164">Connect the sensor to Pi</span></span>

<span data-ttu-id="042a3-165">Use a placa universal e os cabos de jumper para conectar um LED e um BME280 ao Pi, da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="042a3-165">Use the breadboard and jumper wires to connect an LED and a BME280 to Pi as follows.</span></span> <span data-ttu-id="042a3-166">Se você não tiver o sensor, [ignore esta seção](#connect-pi-to-the-network).</span><span class="sxs-lookup"><span data-stu-id="042a3-166">If you don’t have the sensor, [skip this section](#connect-pi-to-the-network).</span></span>

![A conexão do Raspberry Pi e do sensor](media/iot-hub-raspberry-pi-kit-node-get-started/3_raspberry-pi-sensor-connection.png)

<span data-ttu-id="042a3-168">O sensor BME280 pode coletar dados de temperatura e umidade.</span><span class="sxs-lookup"><span data-stu-id="042a3-168">The BME280 sensor can collect temperature and humidity data.</span></span> <span data-ttu-id="042a3-169">E o LED piscará se houver uma comunicação entre o dispositivo e a nuvem.</span><span class="sxs-lookup"><span data-stu-id="042a3-169">And the LED will blink if there is a communication between device and the cloud.</span></span> 

<span data-ttu-id="042a3-170">Use a seguinte fiação para os pinos do sensor:</span><span class="sxs-lookup"><span data-stu-id="042a3-170">For sensor pins, use the following wiring:</span></span>

| <span data-ttu-id="042a3-171">Início (Sensor e LED)</span><span class="sxs-lookup"><span data-stu-id="042a3-171">Start (Sensor & LED)</span></span>     | <span data-ttu-id="042a3-172">End (quadro)</span><span class="sxs-lookup"><span data-stu-id="042a3-172">End (Board)</span></span>            | <span data-ttu-id="042a3-173">Cor de cabo</span><span class="sxs-lookup"><span data-stu-id="042a3-173">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="042a3-174">VDD (pino 5G)</span><span class="sxs-lookup"><span data-stu-id="042a3-174">VDD (Pin 5G)</span></span>             | <span data-ttu-id="042a3-175">3,3 v PWR (pino 1)</span><span class="sxs-lookup"><span data-stu-id="042a3-175">3.3V PWR (Pin 1)</span></span>       | <span data-ttu-id="042a3-176">Cabo branco</span><span class="sxs-lookup"><span data-stu-id="042a3-176">White cable</span></span>   |
| <span data-ttu-id="042a3-177">GND (pino 7G)</span><span class="sxs-lookup"><span data-stu-id="042a3-177">GND (Pin 7G)</span></span>             | <span data-ttu-id="042a3-178">GND (pino 6)</span><span class="sxs-lookup"><span data-stu-id="042a3-178">GND (Pin 6)</span></span>            | <span data-ttu-id="042a3-179">Cabo marrom</span><span class="sxs-lookup"><span data-stu-id="042a3-179">Brown cable</span></span>   |
| <span data-ttu-id="042a3-180">SDI (pino 10G)</span><span class="sxs-lookup"><span data-stu-id="042a3-180">SDI (Pin 10G)</span></span>            | <span data-ttu-id="042a3-181">I2C1 SDA (pino 3)</span><span class="sxs-lookup"><span data-stu-id="042a3-181">I2C1 SDA (Pin 3)</span></span>       | <span data-ttu-id="042a3-182">Cabo vermelho</span><span class="sxs-lookup"><span data-stu-id="042a3-182">Red cable</span></span>     |
| <span data-ttu-id="042a3-183">SCK (pino 8G)</span><span class="sxs-lookup"><span data-stu-id="042a3-183">SCK (Pin 8G)</span></span>             | <span data-ttu-id="042a3-184">I2C1 SCL (pino 5)</span><span class="sxs-lookup"><span data-stu-id="042a3-184">I2C1 SCL (Pin 5)</span></span>       | <span data-ttu-id="042a3-185">Cabo laranja</span><span class="sxs-lookup"><span data-stu-id="042a3-185">Orange cable</span></span>  |
| <span data-ttu-id="042a3-186">LED VDD (pino 18F)</span><span class="sxs-lookup"><span data-stu-id="042a3-186">LED VDD (Pin 18F)</span></span>        | <span data-ttu-id="042a3-187">GPIO 24 (pino 18)</span><span class="sxs-lookup"><span data-stu-id="042a3-187">GPIO 24 (Pin 18)</span></span>       | <span data-ttu-id="042a3-188">Cabo branco</span><span class="sxs-lookup"><span data-stu-id="042a3-188">White cable</span></span>   |
| <span data-ttu-id="042a3-189">LED GND (pino 17F)</span><span class="sxs-lookup"><span data-stu-id="042a3-189">LED GND (Pin 17F)</span></span>        | <span data-ttu-id="042a3-190">GND (pino 20)</span><span class="sxs-lookup"><span data-stu-id="042a3-190">GND (Pin 20)</span></span>           | <span data-ttu-id="042a3-191">Cabo preto</span><span class="sxs-lookup"><span data-stu-id="042a3-191">Black cable</span></span>   |

<span data-ttu-id="042a3-192">Clique para exibir os [mapeamentos de pinos do Raspberry Pi 2 e 3](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) para referência.</span><span class="sxs-lookup"><span data-stu-id="042a3-192">Click to view [Raspberry Pi 2 & 3 Pin mappings](https://developer.microsoft.com/windows/iot/docs/pinmappingsrpi) for your reference.</span></span>

<span data-ttu-id="042a3-193">Depois de conectar com êxito o BME280 ao Raspberry Pi, ele deve ficar semelhante à imagem abaixo.</span><span class="sxs-lookup"><span data-stu-id="042a3-193">After you've successfully connected BME280 to your Raspberry Pi, it should be like below image.</span></span>

![Pi e BME280 conectados](media/iot-hub-raspberry-pi-kit-node-get-started/4_connected-pi.jpg)

### <a name="connect-pi-to-the-network"></a><span data-ttu-id="042a3-195">Conectar Pi à rede</span><span class="sxs-lookup"><span data-stu-id="042a3-195">Connect Pi to the network</span></span>

<span data-ttu-id="042a3-196">Ligue o Pi usando o cabo micro USB e a fonte de alimentação.</span><span class="sxs-lookup"><span data-stu-id="042a3-196">Turn on Pi by using the micro USB cable and the power supply.</span></span> <span data-ttu-id="042a3-197">Use o cabo Ethernet para conectar o Pi à sua rede com fio ou siga as [instruções da Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) para conectar o Pi à sua rede sem fio.</span><span class="sxs-lookup"><span data-stu-id="042a3-197">Use the Ethernet cable to connect Pi to your wired network or follow the [instructions from the Raspberry Pi Foundation](https://www.raspberrypi.org/learning/software-guide/wifi/) to connect Pi to your wireless network.</span></span> <span data-ttu-id="042a3-198">Depois que o Pi tiver se conectado com êxito à rede, você precisará observar o [endereço IP do Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span><span class="sxs-lookup"><span data-stu-id="042a3-198">After your Pi has been successfully connected to the network, you need to take a note of the [IP address of your Pi](https://learn.adafruit.com/adafruits-raspberry-pi-lesson-3-network-setup/finding-your-pis-ip-address).</span></span>

![Conectado à rede com fio](media/iot-hub-raspberry-pi-kit-node-get-started/5_power-on-pi.jpg)

> [!NOTE]
> <span data-ttu-id="042a3-200">Verifique se o Pi está conectado à mesma rede que o computador.</span><span class="sxs-lookup"><span data-stu-id="042a3-200">Make sure that Pi is connected to the same network as your computer.</span></span> <span data-ttu-id="042a3-201">Por exemplo, se o computador estiver conectado a uma rede sem fio enquanto o Pi estiver conectado a uma rede com fio, talvez você não veja o endereço IP na saída devdisco.</span><span class="sxs-lookup"><span data-stu-id="042a3-201">For example, if your computer is connected to a wireless network while Pi is connected to a wired network, you might not see the IP address in the devdisco output.</span></span>

## <a name="run-a-sample-application-on-pi"></a><span data-ttu-id="042a3-202">Executar um aplicativo de exemplo no Pi</span><span class="sxs-lookup"><span data-stu-id="042a3-202">Run a sample application on Pi</span></span>

### <a name="clone-sample-application-and-install-the-prerequisite-packages"></a><span data-ttu-id="042a3-203">Clonar o aplicativo de exemplo e instalar os pacotes de pré-requisito</span><span class="sxs-lookup"><span data-stu-id="042a3-203">Clone sample application and install the prerequisite packages</span></span>

1. <span data-ttu-id="042a3-204">Use um dos seguintes clientes SSH do seu computador host para se conectar ao Raspberry Pi.</span><span class="sxs-lookup"><span data-stu-id="042a3-204">Use one of the following SSH clients from your host computer to connect to your Raspberry Pi.</span></span>
   
   <span data-ttu-id="042a3-205">**Usuários do Windows**</span><span class="sxs-lookup"><span data-stu-id="042a3-205">**Windows Users**</span></span>
   1. <span data-ttu-id="042a3-206">Baixe e instale o [PuTTY](http://www.putty.org/) para Windows.</span><span class="sxs-lookup"><span data-stu-id="042a3-206">Download and install [PuTTY](http://www.putty.org/) for Windows.</span></span> 
   1. <span data-ttu-id="042a3-207">Copie o endereço IP do seu Pi para a seção Nome do host (ou Endereço IP) e selecione SSH como o tipo de conexão.</span><span class="sxs-lookup"><span data-stu-id="042a3-207">Copy the IP address of your Pi into the Host name (or IP address) section and select SSH as the connection type.</span></span>
   
   ![PuTTy](media/iot-hub-raspberry-pi-kit-node-get-started/7_putty-windows.png)
   
   <span data-ttu-id="042a3-209">**Usuários de Mac e do Ubuntu**</span><span class="sxs-lookup"><span data-stu-id="042a3-209">**Mac and Ubuntu Users**</span></span>
   
   <span data-ttu-id="042a3-210">Use o cliente SSH interno no Ubuntu ou macOS.</span><span class="sxs-lookup"><span data-stu-id="042a3-210">Use the built-in SSH client on Ubuntu or macOS.</span></span> <span data-ttu-id="042a3-211">Talvez você precise executar `ssh pi@<ip address of pi>` para conectar o Pi via SSH.</span><span class="sxs-lookup"><span data-stu-id="042a3-211">You might need to run `ssh pi@<ip address of pi>` to connect Pi via SSH.</span></span>
   > [!NOTE] 
   <span data-ttu-id="042a3-212">O nome de usuário padrão é `pi` e a senha é `raspberry`.</span><span class="sxs-lookup"><span data-stu-id="042a3-212">The default username is `pi` , and the password is `raspberry`.</span></span>

1. <span data-ttu-id="042a3-213">Instale o Node.js e o NPM em seu Pi.</span><span class="sxs-lookup"><span data-stu-id="042a3-213">Install Node.js and NPM to your Pi.</span></span>
   
   <span data-ttu-id="042a3-214">Primeiro você deve verificar a versão do Node.js com o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="042a3-214">First you should check your Node.js version with the following command.</span></span> 
   
   ```bash
   node -v
   ```

   <span data-ttu-id="042a3-215">Se a versão for inferior a 4.x ou não existir nenhum Node.js no seu Pi, execute o comando a seguir para instalar ou atualizar o Node.js.</span><span class="sxs-lookup"><span data-stu-id="042a3-215">If the version is lower than 4.x or there is no Node.js on your Pi, then run the following command to install or update Node.js.</span></span>

   ```bash
   curl -sL http://deb.nodesource.com/setup_4.x | sudo -E bash
   sudo apt-get -y install nodejs
   ```

1. <span data-ttu-id="042a3-216">Clone o aplicativo de exemplo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="042a3-216">Clone the sample application by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-node-raspberrypi-client-app
   ```

1. <span data-ttu-id="042a3-217">Instale todos os pacotes com o comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="042a3-217">Install all packages by the following command.</span></span> <span data-ttu-id="042a3-218">Ele inclui o SDK do dispositivo IoT do Azure, a biblioteca do Sensor BME280 e a biblioteca de fiação do Pi.</span><span class="sxs-lookup"><span data-stu-id="042a3-218">It includes Azure IoT device SDK, BME280 Sensor library and Wiring Pi library.</span></span>

   ```bash
   cd iot-hub-node-raspberrypi-client-app
   sudo npm install
   ```
   > [!NOTE] 
   <span data-ttu-id="042a3-219">O processo de instalação poderá levar alguns minutos para ser concluído, dependendo da sua conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="042a3-219">It might take several minutes to finish this installation process depending on your network connection.</span></span>

### <a name="configure-the-sample-application"></a><span data-ttu-id="042a3-220">Configurar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="042a3-220">Configure the sample application</span></span>

1. <span data-ttu-id="042a3-221">Abra o arquivo de configuração executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="042a3-221">Open the config file by running the following commands:</span></span>

   ```bash
   nano config.json
   ```

   ![Arquivo de configuração](media/iot-hub-raspberry-pi-kit-node-get-started/6_config-file.png)

   <span data-ttu-id="042a3-223">Há dois itens que podem ser configurados nesse arquivo.</span><span class="sxs-lookup"><span data-stu-id="042a3-223">There are two items in this file you can configurate.</span></span> <span data-ttu-id="042a3-224">A primeira é a `interval`, que define o intervalo de tempo (em milissegundos) entre duas mensagens que são enviadas para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="042a3-224">The first one is `interval`, which defines the time interval (in milliseconds) between two messages that send to cloud.</span></span> <span data-ttu-id="042a3-225">O segundo, o `simulatedData`, é um valor booliano para definir se os dados simulados de sensor serão usados ou não.</span><span class="sxs-lookup"><span data-stu-id="042a3-225">The second one `simulatedData`,which is a Boolean value for whether to use simulated sensor data or not.</span></span>

   <span data-ttu-id="042a3-226">Se você **não tiver o sensor**, defina o valor `simulatedData` como `true` para fazer com que o aplicativo de exemplo crie e use dados simulados de sensor.</span><span class="sxs-lookup"><span data-stu-id="042a3-226">If you **don't have the sensor**, set the `simulatedData` value to `true` to make the sample application create and use simulated sensor data.</span></span>

1. <span data-ttu-id="042a3-227">Salve e saia pressionando CTRL+O > ENTER > CTRL+X.</span><span class="sxs-lookup"><span data-stu-id="042a3-227">Save and exit by pressing Control-O > Enter > Control-X.</span></span>

### <a name="run-the-sample-application"></a><span data-ttu-id="042a3-228">Executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="042a3-228">Run the sample application</span></span>

<span data-ttu-id="042a3-229">Execute o aplicativo de exemplo com seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="042a3-229">Run the sample application by running the following command:</span></span>

   ```bash
   sudo node index.js '<YOUR AZURE IOT HUB DEVICE CONNECTION STRING>'
   ```

   > [!NOTE] 
   <span data-ttu-id="042a3-230">Verifique se você copiou e colou a cadeia de conexão do dispositivo em aspas simples.</span><span class="sxs-lookup"><span data-stu-id="042a3-230">Make sure you copy-paste the device connection string into the single quotes.</span></span>


<span data-ttu-id="042a3-231">Você deverá ver a seguinte saída, mostrando os dados do sensor e as mensagens que são enviadas ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="042a3-231">You should see the following output that shows the sensor data and the messages that are sent to your IoT hub.</span></span>

![Saída – dados de sensor enviados do Raspberry Pi para o seu Hub IoT](media/iot-hub-raspberry-pi-kit-node-get-started/8_run-output.png)

## <a name="next-steps"></a><span data-ttu-id="042a3-233">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="042a3-233">Next steps</span></span>

<span data-ttu-id="042a3-234">Você executou um aplicativo de exemplo para coletar dados de sensor e enviá-los ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="042a3-234">You’ve run a sample application to collect sensor data and send it to your IoT hub.</span></span> <span data-ttu-id="042a3-235">Para ver as mensagens que o seu Raspberry Pi enviou ao seu Hub IoT ou enviar mensagens para o Raspberry Pi em uma interface de linha de comando, consulte o [tutorial Gerenciar mensagens em dispositivo de nuvem com o gerenciador de Hubs IoT](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span><span class="sxs-lookup"><span data-stu-id="042a3-235">To see the messages that your Raspberry Pi has sent to your IoT hub or send messages to your Raspberry Pi in a command line interface, see the [Manage cloud device messaging with iothub-explorer tutorial](https://docs.microsoft.com/en-gb/azure/iot-hub/iot-hub-explorer-cloud-device-messaging).</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
