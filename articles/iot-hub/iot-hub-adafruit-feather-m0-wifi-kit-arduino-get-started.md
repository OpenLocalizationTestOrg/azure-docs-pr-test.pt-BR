---
title: "M0 toocloud: conectar-se a difusão M0 WiFi tooAzure IoT Hub | Microsoft Docs"
description: "Saiba como tooset up e conectar Adafruit difusão M0 WiFi tooAzure plataforma de nuvem do Azure IoT Hub toosend dados toohello neste tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 51befcdb-332b-416f-a6a1-8aabdb67f283
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 8/16/2017
ms.author: xshi
ms.openlocfilehash: 6aabeb961a50ba5d3934f77eb1ccda4af1bf64c8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-m0-wifi-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="a2e68-103">Conecte-se Adafruit difusão M0 WiFi tooAzure IoT Hub na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="a2e68-103">Connect Adafruit Feather M0 WiFi tooAzure IoT Hub in hello cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexão entre BME280, Feather M0 WiFi e Hub IoT](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="a2e68-105">Neste tutorial, você começar a aprender os fundamentos de saudação do trabalho com seu quadro Arduino.</span><span class="sxs-lookup"><span data-stu-id="a2e68-105">In this tutorial, you begin by learning hello basics of working with your Arduino board.</span></span> <span data-ttu-id="a2e68-106">Em seguida, você aprenderá como tooseamlessly se conectar a sua nuvem de toohello dispositivos usando [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="a2e68-106">You then learn how tooseamlessly connect your devices toohello cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="a2e68-107">O que fazer</span><span class="sxs-lookup"><span data-stu-id="a2e68-107">What you do</span></span>

<span data-ttu-id="a2e68-108">Conecte-se Adafruit difusão M0 WiFi tooan IoT hub que você criar.</span><span class="sxs-lookup"><span data-stu-id="a2e68-108">Connect Adafruit Feather M0 WiFi tooan IoT hub that you create.</span></span> <span data-ttu-id="a2e68-109">Em seguida, execute um aplicativo de exemplo em M0 Wi-Fi toocollect Olá temperatura e umidade dados de um BME280.</span><span class="sxs-lookup"><span data-stu-id="a2e68-109">Then you run a sample application on M0 WiFi toocollect hello temperature and humidity data from a BME280.</span></span> <span data-ttu-id="a2e68-110">Por fim, você pode enviar hub IoT do hello sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="a2e68-110">Finally, you send hello sensor data tooyour IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="a2e68-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="a2e68-111">What you learn</span></span>

* <span data-ttu-id="a2e68-112">Como toocreate um hub IoT e registrar um dispositivo para difusão M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="a2e68-112">How toocreate an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="a2e68-113">Como tooconnect difusão M0 WiFi com sensor hello e seu computador</span><span class="sxs-lookup"><span data-stu-id="a2e68-113">How tooconnect Feather M0 WiFi with hello sensor and your computer</span></span>
* <span data-ttu-id="a2e68-114">Como os dados do sensor toocollect executando um aplicativo de exemplo em difusão M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="a2e68-114">How toocollect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="a2e68-115">Como toosend Olá hub IoT do sensor dados tooyour</span><span class="sxs-lookup"><span data-stu-id="a2e68-115">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a2e68-116">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="a2e68-116">What you need</span></span>

![Partes necessárias para o tutorial Olá](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="a2e68-118">toocomplete essa operação, você precisa Olá seguir partes de seu difusão M0 WiFi Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="a2e68-118">toocomplete this operation, you need hello following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="a2e68-119">Olá difusão M0 WiFi board</span><span class="sxs-lookup"><span data-stu-id="a2e68-119">hello Feather M0 WiFi board</span></span>
* <span data-ttu-id="a2e68-120">Um tooType Micro USB um cabo</span><span class="sxs-lookup"><span data-stu-id="a2e68-120">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="a2e68-121">Você também precisa Olá coisas para seu ambiente de desenvolvimento a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2e68-121">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="a2e68-122">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a2e68-122">An active Azure subscription.</span></span> <span data-ttu-id="a2e68-123">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="a2e68-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="a2e68-124">Um Mac ou PC que esteja executando Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="a2e68-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="a2e68-125">Uma rede sem fio para difusão M0 WiFi tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="a2e68-125">A wireless network for Feather M0 WiFi tooconnect to.</span></span>
* <span data-ttu-id="a2e68-126">Uma ferramenta de configuração do Internet conexão toodownload hello.</span><span class="sxs-lookup"><span data-stu-id="a2e68-126">An Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="a2e68-127">[IDE do Arduino](https://www.arduino.cc/en/main/software) versão 1.6.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a2e68-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="a2e68-128">Versões anteriores não funcionam com a biblioteca do hello Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="a2e68-128">Earlier versions don't work with hello Azure IoT Hub library.</span></span>

<span data-ttu-id="a2e68-129">Se você não tiver um sensor, Olá itens a seguir é opcional.</span><span class="sxs-lookup"><span data-stu-id="a2e68-129">If you don’t have a sensor, hello following items are optional.</span></span> <span data-ttu-id="a2e68-130">Você também tem a opção de saudação do uso de dados de sensor simulada:</span><span class="sxs-lookup"><span data-stu-id="a2e68-130">You also have hello option of using simulated sensor data:</span></span>

* <span data-ttu-id="a2e68-131">Um sensor de temperatura e umidade BME280</span><span class="sxs-lookup"><span data-stu-id="a2e68-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="a2e68-132">Uma placa universal</span><span class="sxs-lookup"><span data-stu-id="a2e68-132">A breadboard</span></span>
* <span data-ttu-id="a2e68-133">Cabos de jumper de M/M</span><span class="sxs-lookup"><span data-stu-id="a2e68-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-hello-sensor-and-your-computer"></a><span data-ttu-id="a2e68-134">Conexão Wi-Fi M0 de difusão com sensor hello e seu computador</span><span class="sxs-lookup"><span data-stu-id="a2e68-134">Connect Feather M0 WiFi with hello sensor and your computer</span></span>
<span data-ttu-id="a2e68-135">Nesta seção, você se conectar a placa de tooyour sensores hello.</span><span class="sxs-lookup"><span data-stu-id="a2e68-135">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="a2e68-136">Em seguida, você conecta o computador tooyour de dispositivo para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="a2e68-136">Then you plug in your device tooyour computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-m0-wifi"></a><span data-ttu-id="a2e68-137">Conecte-se um DHT22 temperatura e umidade sensor tooFeather M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="a2e68-137">Connect a DHT22 temperature and humidity sensor tooFeather M0 WiFi</span></span>

<span data-ttu-id="a2e68-138">Use Olá breadboard e jumper fios toomake Olá conexão.</span><span class="sxs-lookup"><span data-stu-id="a2e68-138">Use hello breadboard and jumper wires toomake hello connection.</span></span> <span data-ttu-id="a2e68-139">Se você não tiver um sensor, ignore esta seção porque você pode usar dados de sensor simulado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="a2e68-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Referência de conexões](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="a2e68-141">Pinos do sensor, use Olá fiação a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2e68-141">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="a2e68-142">Início (sensor)</span><span class="sxs-lookup"><span data-stu-id="a2e68-142">Start (sensor)</span></span>           | <span data-ttu-id="a2e68-143">Fim (placa)</span><span class="sxs-lookup"><span data-stu-id="a2e68-143">End (board)</span></span>            | <span data-ttu-id="a2e68-144">Cor do cabo</span><span class="sxs-lookup"><span data-stu-id="a2e68-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="a2e68-145">VDD (pino 27A)</span><span class="sxs-lookup"><span data-stu-id="a2e68-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="a2e68-146">3V (pino 3A)</span><span class="sxs-lookup"><span data-stu-id="a2e68-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="a2e68-147">Cabo vermelho</span><span class="sxs-lookup"><span data-stu-id="a2e68-147">Red cable</span></span>     |
| <span data-ttu-id="a2e68-148">GND (pino 29A)</span><span class="sxs-lookup"><span data-stu-id="a2e68-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="a2e68-149">GND (pino 6A)</span><span class="sxs-lookup"><span data-stu-id="a2e68-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="a2e68-150">Cabo preto</span><span class="sxs-lookup"><span data-stu-id="a2e68-150">Black cable</span></span>   |
| <span data-ttu-id="a2e68-151">SCK (pino 30A)</span><span class="sxs-lookup"><span data-stu-id="a2e68-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="a2e68-152">SCK (pino 12A)</span><span class="sxs-lookup"><span data-stu-id="a2e68-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="a2e68-153">Cabo amarelo</span><span class="sxs-lookup"><span data-stu-id="a2e68-153">Yellow cable</span></span>  |
| <span data-ttu-id="a2e68-154">SDO (pino 31A)</span><span class="sxs-lookup"><span data-stu-id="a2e68-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="a2e68-155">MI (pino 14A)</span><span class="sxs-lookup"><span data-stu-id="a2e68-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="a2e68-156">Cabo branco</span><span class="sxs-lookup"><span data-stu-id="a2e68-156">White cable</span></span>   |
| <span data-ttu-id="a2e68-157">SDI (pino 32A)</span><span class="sxs-lookup"><span data-stu-id="a2e68-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="a2e68-158">M0 (pino 13A)</span><span class="sxs-lookup"><span data-stu-id="a2e68-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="a2e68-159">Cabo azul</span><span class="sxs-lookup"><span data-stu-id="a2e68-159">Blue cable</span></span>    |
| <span data-ttu-id="a2e68-160">CS (pino 33A)</span><span class="sxs-lookup"><span data-stu-id="a2e68-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="a2e68-161">GPIO 5 (pino 15J)</span><span class="sxs-lookup"><span data-stu-id="a2e68-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="a2e68-162">Cabo laranja</span><span class="sxs-lookup"><span data-stu-id="a2e68-162">Orange cable</span></span>  |

<span data-ttu-id="a2e68-163">Para obter mais informações, consulte [Saídas do sensor de umidade, pressão barométrica e temperatura Adafruit BME280](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) e [Pinagem do Adafruit Feather M0 WiFi](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span><span class="sxs-lookup"><span data-stu-id="a2e68-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="a2e68-164">Agora seu Feather M0 WiFi deve estar conectado a um sensor ativo.</span><span class="sxs-lookup"><span data-stu-id="a2e68-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Conectar o DHT22 ao Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-tooyour-computer"></a><span data-ttu-id="a2e68-166">Conectar o computador de tooyour difusão M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="a2e68-166">Connect Feather M0 WiFi tooyour computer</span></span>

<span data-ttu-id="a2e68-167">Use Olá Micro USB tooType USB um cabo tooconnect difusão M0 WiFi tooyour computador, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="a2e68-167">Use hello Micro USB tooType A USB cable tooconnect Feather M0 WiFi tooyour computer, as shown:</span></span>

![Conectar o computador de tooyour Huzzah de difusão](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="a2e68-169">Adicionar permissões de porta serial (somente Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="a2e68-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="a2e68-170">Se você usar Ubuntu, verifique se que você tem Olá permissões toooperate em Olá USB porta da difusão M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a2e68-170">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="a2e68-171">permissões de porta serial tooadd, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a2e68-171">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="a2e68-172">Em um terminal, execute Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2e68-172">At a terminal, run hello following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="a2e68-173">Você obtém uma saudação saídas a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2e68-173">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="a2e68-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="a2e68-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="a2e68-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="a2e68-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="a2e68-176">Na saída de hello, observe que `uucp` ou `dialout` é o nome de proprietário do grupo de saudação do hello porta USB.</span><span class="sxs-lookup"><span data-stu-id="a2e68-176">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

2. <span data-ttu-id="a2e68-177">tooadd Olá toohello grupo de usuários, execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2e68-177">tooadd hello user toohello group, run hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="a2e68-178">Na etapa anterior de saudação, você obteve o nome do proprietário do grupo Olá `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="a2e68-178">In hello previous step, you obtained hello group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="a2e68-179">Seu nome de usuário do Ubuntu é `<username>`.</span><span class="sxs-lookup"><span data-stu-id="a2e68-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="a2e68-180">Para Olá alteração tooappear, saia do Ubuntu e entrar novamente.</span><span class="sxs-lookup"><span data-stu-id="a2e68-180">For hello change tooappear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="a2e68-181">Coletar dados de sensor e enviá-lo tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="a2e68-181">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="a2e68-182">Nesta seção, você implanta e executa um aplicativo de exemplo no Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="a2e68-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="a2e68-183">aplicativo de exemplo Hello torna Olá intermitência de LED em difusão M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a2e68-183">hello sample application makes hello LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="a2e68-184">Em seguida, envia temperatura hello e umidade os dados coletados de saudação BME280 sensor tooyour hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a2e68-184">It then sends hello temperature and humidity data collected from hello BME280 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github-and-prepare-hello-arduino-ide"></a><span data-ttu-id="a2e68-185">Obter o aplicativo de exemplo hello do GitHub e preparar Olá Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="a2e68-185">Get hello sample application from GitHub and prepare hello Arduino IDE</span></span>

<span data-ttu-id="a2e68-186">aplicativo de exemplo Hello está hospedado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="a2e68-186">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="a2e68-187">Clone o repositório de exemplo hello que contém o aplicativo de exemplo de saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="a2e68-187">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="a2e68-188">repositório de exemplo hello tooclone, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a2e68-188">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="a2e68-189">Abra um prompt de comando ou uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="a2e68-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="a2e68-190">Vá tooa pasta onde você deseja toobe de aplicativo de exemplo hello armazenado.</span><span class="sxs-lookup"><span data-stu-id="a2e68-190">Go tooa folder where you want hello sample application toobe stored.</span></span>
3. <span data-ttu-id="a2e68-191">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a2e68-191">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-hello-package-for-feather-m0-wifi-in-hello-arduino-ide"></a><span data-ttu-id="a2e68-192">Instalar o pacote de saudação para difusão M0 WiFi no hello Arduino IDE</span><span class="sxs-lookup"><span data-stu-id="a2e68-192">Install hello package for Feather M0 WiFi in hello Arduino IDE</span></span>

1. <span data-ttu-id="a2e68-193">Abra a pasta de saudação onde o aplicativo de exemplo hello está armazenado.</span><span class="sxs-lookup"><span data-stu-id="a2e68-193">Open hello folder where hello sample application is stored.</span></span>

2. <span data-ttu-id="a2e68-194">Abra o arquivo de app.ino de saudação na pasta de aplicativo Olá Olá Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="a2e68-194">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Abra o aplicativo de exemplo hello Arduino IDE](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="a2e68-196">Clique em **arquivo** > **preferências** (Windows/Linux) ou **Arduino** > **preferências** (Mac) e copie e Colar vínculo Olá abaixo em Olá **URLs adicionais do Gerenciador de quadros** opção Olá preferências Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="a2e68-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste hello link below into hello **Additional Boards Manager URLs** option in hello Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="a2e68-197">Clique em **ferramentas** > **placa** > **Manager quadros**e, em seguida, instalar Olá `Arduino SAMD Boards` versão `1.6.2` ou posterior.</span><span class="sxs-lookup"><span data-stu-id="a2e68-197">Click **Tools** > **Board** > **Boards Manager**, and then install hello `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="a2e68-198">Em seguida, em Olá mesma janela, instale o `Adafruit SAMD Boards` tooadd definições de arquivos de quadro de saudação do pacote.</span><span class="sxs-lookup"><span data-stu-id="a2e68-198">Then in hello same window, install `Adafruit SAMD Boards` package tooadd hello board file definitions.</span></span>

   ![Olá esp8266 pacote está instalado](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="a2e68-200">Clique em **Ferramentas** > **Placa** > **Adafruit M0 WiFi**.</span><span class="sxs-lookup"><span data-stu-id="a2e68-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="a2e68-201">Instale os drivers (apenas para Windows).</span><span class="sxs-lookup"><span data-stu-id="a2e68-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="a2e68-202">Quando você conecta Wi-Fi M0 de difusão, talvez seja necessário tooinstall um driver.</span><span class="sxs-lookup"><span data-stu-id="a2e68-202">When you plug in Feather M0 WiFi, you might need tooinstall a driver.</span></span> <span data-ttu-id="a2e68-203">Clique em [Olá link para download na página da Web de saudação](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) instalador do driver Olá toodownload.</span><span class="sxs-lookup"><span data-stu-id="a2e68-203">Click [hello download link on hello webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) toodownload hello driver installer.</span></span> <span data-ttu-id="a2e68-204">Siga os drivers de Olá Olá etapas tooinstall desejado.</span><span class="sxs-lookup"><span data-stu-id="a2e68-204">Follow hello steps tooinstall hello drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="a2e68-205">Instalar as bibliotecas necessárias</span><span class="sxs-lookup"><span data-stu-id="a2e68-205">Install necessary libraries</span></span>

1. <span data-ttu-id="a2e68-206">No hello Arduino IDE, clique em **esboço** > **biblioteca incluem** > **gerenciar bibliotecas**.</span><span class="sxs-lookup"><span data-stu-id="a2e68-206">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="a2e68-207">Pesquisar Olá uma nomes de bibliotecas a seguir.</span><span class="sxs-lookup"><span data-stu-id="a2e68-207">Search for hello following library names one by one.</span></span> <span data-ttu-id="a2e68-208">Para cada biblioteca que você localizar, clique em **Instalar**:</span><span class="sxs-lookup"><span data-stu-id="a2e68-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="a2e68-209">Instale o `Adafruit_WINC1500` manualmente.</span><span class="sxs-lookup"><span data-stu-id="a2e68-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="a2e68-210">Vá muito[neste site](https://github.com/adafruit/Adafruit_WINC1500) e clique em **Clone ou download** > **baixar ZIP**.</span><span class="sxs-lookup"><span data-stu-id="a2e68-210">Go too[this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="a2e68-211">Em seu IDE Arduino, acesse muito**esboço** > **biblioteca incluem** > **adicionar. zip biblioteca** e adicione o arquivo zip de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2e68-211">Then in your Arduino IDE, go too**Sketch** > **Include Library** > **Add .zip Library** and add hello zip file.</span></span>

### <a name="use-hello-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="a2e68-212">Use o aplicativo de exemplo hello se você não tiver um sensor BME280 real</span><span class="sxs-lookup"><span data-stu-id="a2e68-212">Use hello sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="a2e68-213">Se você não tiver um sensor BME280 real, o aplicativo de exemplo hello pode simular temperatura e umidade dados.</span><span class="sxs-lookup"><span data-stu-id="a2e68-213">If you don’t have a real BME280 sensor, hello sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="a2e68-214">tooset backup de dados de toouse simulada de aplicativo de exemplo hello, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a2e68-214">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="a2e68-215">Olá abrir `config.h` arquivo hello `app` pasta.</span><span class="sxs-lookup"><span data-stu-id="a2e68-215">Open hello `config.h` file in hello `app` folder.</span></span>

2. <span data-ttu-id="a2e68-216">Localize Olá a seguinte linha de código e altere o valor de saudação de `false` muito`true`:</span><span class="sxs-lookup"><span data-stu-id="a2e68-216">Locate hello following line of code and change hello value from `false` too`true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar dados de toouse simulada de aplicativo de exemplo hello](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="a2e68-218">Salve o arquivo hello com `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="a2e68-218">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-m0-wifi"></a><span data-ttu-id="a2e68-219">Implantar tooFeather de aplicativo de exemplo hello M0 Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="a2e68-219">Deploy hello sample application tooFeather M0 WiFi</span></span>

1. <span data-ttu-id="a2e68-220">No hello Arduino IDE, clique em **ferramenta** > **porta**e, em seguida, clique em porta serial Olá para difusão M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="a2e68-220">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="a2e68-221">Clique em **esboço** > **carregar** toobuild e implantar tooFeather de aplicativo de exemplo hello M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a2e68-221">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="a2e68-222">Introduza as suas credenciais</span><span class="sxs-lookup"><span data-stu-id="a2e68-222">Enter your credentials</span></span>

<span data-ttu-id="a2e68-223">Olá após o carregamento for concluído com êxito, siga estas etapas tooenter suas credenciais:</span><span class="sxs-lookup"><span data-stu-id="a2e68-223">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="a2e68-224">No hello Arduino IDE, clique em **ferramentas** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="a2e68-224">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="a2e68-225">No canto inferior direito de saudação da janela do monitor serial hello, selecione **nenhuma final de linha** na lista suspensa de Olá Olá esquerda.</span><span class="sxs-lookup"><span data-stu-id="a2e68-225">In hello lower-right corner of hello serial monitor window, select **No line ending** in hello drop-down list on hello left.</span></span>
3. <span data-ttu-id="a2e68-226">Selecione **115200 baud** na lista suspensa Olá Olá à direita.</span><span class="sxs-lookup"><span data-stu-id="a2e68-226">Select **115200 baud** in hello drop-down list on hello right.</span></span>
4. <span data-ttu-id="a2e68-227">Na caixa de entrada hello na parte superior do hello, insira Olá informações a seguir se você for solicitado tooprovide e clique em **enviar**:</span><span class="sxs-lookup"><span data-stu-id="a2e68-227">In hello input box at hello top, enter hello following information if you're asked tooprovide it, and click **Send**:</span></span>

   * <span data-ttu-id="a2e68-228">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="a2e68-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="a2e68-229">Senha de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="a2e68-229">Wi-Fi password</span></span>
   * <span data-ttu-id="a2e68-230">Cadeia de conexão de dispositivo</span><span class="sxs-lookup"><span data-stu-id="a2e68-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="a2e68-231">Olá credenciais são armazenadas no hello EEPROM de difusão M0 Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="a2e68-231">hello credential information is stored in hello EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="a2e68-232">Se você clicar em um botão Redefinir Olá Olá difusão M0 WiFi quadro, aplicativo de exemplo hello pergunta se você deseja informações de saudação do tooerase.</span><span class="sxs-lookup"><span data-stu-id="a2e68-232">If you click hello reset button on hello Feather M0 WiFi board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="a2e68-233">Digite `Y` tooerase informações de saudação.</span><span class="sxs-lookup"><span data-stu-id="a2e68-233">Enter `Y` tooerase hello information.</span></span> <span data-ttu-id="a2e68-234">Você será solicitado a informações de saudação tooprovide uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="a2e68-234">You're asked tooprovide hello information a second time.</span></span>

### <a name="verify-that-hello-sample-application-is-running-successfully"></a><span data-ttu-id="a2e68-235">Verifique se que o aplicativo de exemplo hello está sendo executado com êxito</span><span class="sxs-lookup"><span data-stu-id="a2e68-235">Verify that hello sample application is running successfully</span></span>

<span data-ttu-id="a2e68-236">Se você vir seguinte Olá de saída da janela do monitor serial hello e Olá piscando LED em difusão M0 WiFi, o aplicativo de exemplo hello está sendo executado com êxito:</span><span class="sxs-lookup"><span data-stu-id="a2e68-236">If you see hello following output from hello serial monitor window and hello blinking LED on Feather M0 WiFi, hello sample application is running successfully:</span></span>

![Saída final no IDE do Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="a2e68-238">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a2e68-238">Next steps</span></span>

<span data-ttu-id="a2e68-239">Você conectado difusão M0 WiFi tooyour IoT hub e enviados Olá capturado sensor dados tooyour IoT hub com êxito.</span><span class="sxs-lookup"><span data-stu-id="a2e68-239">You have successfully connected Feather M0 WiFi tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

