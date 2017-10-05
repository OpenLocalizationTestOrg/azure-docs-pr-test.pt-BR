---
title: "M0 para a nuvem – conectar o Feather M0 WiFi ao Hub IoT do Azure | Microsoft Docs"
description: "Saiba como configurar e conectar o Adafruit Feather M0 WiFi ao Hub IoT do Azure para enviar dados à plataforma de nuvem do Azure neste tutorial."
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
ms.openlocfilehash: 0dcf6b46a4c6c743c713d24ce7844e801b278dcf
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-adafruit-feather-m0-wifi-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="f48fa-103">Conectar o Adafruit Feather M0 WiFi ao Hub IoT do Azure na nuvem</span><span class="sxs-lookup"><span data-stu-id="f48fa-103">Connect Adafruit Feather M0 WiFi to Azure IoT Hub in the cloud</span></span>
[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexão entre BME280, Feather M0 WiFi e Hub IoT](media/iot-hub-adafruit-feather-m0-wifi-get-started/1_connection-m0-feather-m0-iot-hub.png)

<span data-ttu-id="f48fa-105">Neste tutorial, você começa aprendendo as noções básicas de como trabalhar com sua placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="f48fa-105">In this tutorial, you begin by learning the basics of working with your Arduino board.</span></span> <span data-ttu-id="f48fa-106">Em seguida, aprenderá a conectar seus dispositivos diretamente à nuvem usando o [Hub IoT do Azure](iot-hub-what-is-iot-hub.md).</span><span class="sxs-lookup"><span data-stu-id="f48fa-106">You then learn how to seamlessly connect your devices to the cloud by using [Azure IoT Hub](iot-hub-what-is-iot-hub.md).</span></span>

## <a name="what-you-do"></a><span data-ttu-id="f48fa-107">O que fazer</span><span class="sxs-lookup"><span data-stu-id="f48fa-107">What you do</span></span>

<span data-ttu-id="f48fa-108">Conecte o Adafruit Feather M0 WiFi a um Hub IoT criado por você.</span><span class="sxs-lookup"><span data-stu-id="f48fa-108">Connect Adafruit Feather M0 WiFi to an IoT hub that you create.</span></span> <span data-ttu-id="f48fa-109">Em seguida, você executa um aplicativo de exemplo no M0 WiFi para coletar dados de temperatura e umidade de um BME280.</span><span class="sxs-lookup"><span data-stu-id="f48fa-109">Then you run a sample application on M0 WiFi to collect the temperature and humidity data from a BME280.</span></span> <span data-ttu-id="f48fa-110">Por fim, você envia os dados do sensor para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f48fa-110">Finally, you send the sensor data to your IoT hub.</span></span>


## <a name="what-you-learn"></a><span data-ttu-id="f48fa-111">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="f48fa-111">What you learn</span></span>

* <span data-ttu-id="f48fa-112">Como criar um Hub IoT e registrar um dispositivo para o Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="f48fa-112">How to create an IoT hub and register a device for Feather M0 WiFi</span></span>
* <span data-ttu-id="f48fa-113">Como conectar o Feather M0 WiFi ao sensor e ao seu computador</span><span class="sxs-lookup"><span data-stu-id="f48fa-113">How to connect Feather M0 WiFi with the sensor and your computer</span></span>
* <span data-ttu-id="f48fa-114">Como coletar dados de sensor executando um aplicativo de exemplo no Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="f48fa-114">How to collect sensor data by running a sample application on Feather M0 WiFi</span></span>
* <span data-ttu-id="f48fa-115">Como enviar os dados do sensor para o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="f48fa-115">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="f48fa-116">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="f48fa-116">What you need</span></span>

![Partes necessárias para o tutorial](media/iot-hub-adafruit-feather-m0-wifi-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="f48fa-118">Para concluir esta operação, você precisará das seguintes partes do seu Kit de Início do Feather M0 WiFi:</span><span class="sxs-lookup"><span data-stu-id="f48fa-118">To complete this operation, you need the following parts from your Feather M0 WiFi Starter Kit:</span></span>

* <span data-ttu-id="f48fa-119">A placa Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="f48fa-119">The Feather M0 WiFi board</span></span>
* <span data-ttu-id="f48fa-120">Um cabo Micro USB para USB Tipo A</span><span class="sxs-lookup"><span data-stu-id="f48fa-120">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="f48fa-121">Você também precisa destes itens para seu ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="f48fa-121">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="f48fa-122">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="f48fa-122">An active Azure subscription.</span></span> <span data-ttu-id="f48fa-123">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="f48fa-123">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="f48fa-124">Um Mac ou PC que esteja executando Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="f48fa-124">A Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="f48fa-125">Uma rede sem fio à qual o Feather M0 WiFi deve se conectar.</span><span class="sxs-lookup"><span data-stu-id="f48fa-125">A wireless network for Feather M0 WiFi to connect to.</span></span>
* <span data-ttu-id="f48fa-126">Uma conexão com a Internet para baixar a ferramenta de configuração.</span><span class="sxs-lookup"><span data-stu-id="f48fa-126">An Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="f48fa-127">[IDE do Arduino](https://www.arduino.cc/en/main/software) versão 1.6.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f48fa-127">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="f48fa-128">Versões anteriores não funcionam com a biblioteca do Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="f48fa-128">Earlier versions don't work with the Azure IoT Hub library.</span></span>

<span data-ttu-id="f48fa-129">Se você não tiver um sensor, os itens a seguir serão opcionais.</span><span class="sxs-lookup"><span data-stu-id="f48fa-129">If you don’t have a sensor, the following items are optional.</span></span> <span data-ttu-id="f48fa-130">Você também tem a opção de usar dados de sensor simulados:</span><span class="sxs-lookup"><span data-stu-id="f48fa-130">You also have the option of using simulated sensor data:</span></span>

* <span data-ttu-id="f48fa-131">Um sensor de temperatura e umidade BME280</span><span class="sxs-lookup"><span data-stu-id="f48fa-131">A BME280 temperature and humidity sensor</span></span>
* <span data-ttu-id="f48fa-132">Uma placa universal</span><span class="sxs-lookup"><span data-stu-id="f48fa-132">A breadboard</span></span>
* <span data-ttu-id="f48fa-133">Cabos de jumper macho/macho</span><span class="sxs-lookup"><span data-stu-id="f48fa-133">M/M jumper wires</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-m0-wifi-with-the-sensor-and-your-computer"></a><span data-ttu-id="f48fa-134">Conectar o Feather M0 WiFi ao sensor e ao seu computador</span><span class="sxs-lookup"><span data-stu-id="f48fa-134">Connect Feather M0 WiFi with the sensor and your computer</span></span>
<span data-ttu-id="f48fa-135">Nesta seção, você conecta os sensores à sua placa.</span><span class="sxs-lookup"><span data-stu-id="f48fa-135">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="f48fa-136">Em seguida, você conecta o dispositivo ao seu computador para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="f48fa-136">Then you plug in your device to your computer for further use.</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-m0-wifi"></a><span data-ttu-id="f48fa-137">Conectar um sensor de temperatura e umidade DHT22 ao Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="f48fa-137">Connect a DHT22 temperature and humidity sensor to Feather M0 WiFi</span></span>

<span data-ttu-id="f48fa-138">Use os cabos da placa universal e jumper para fazer a conexão.</span><span class="sxs-lookup"><span data-stu-id="f48fa-138">Use the breadboard and jumper wires to make the connection.</span></span> <span data-ttu-id="f48fa-139">Se você não tiver um sensor, ignore esta seção porque você pode usar dados de sensor simulado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="f48fa-139">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Referência de conexões](media/iot-hub-adafruit-feather-m0-wifi-get-started/3_connections_on_breadboard.png)


<span data-ttu-id="f48fa-141">Use a seguinte fiação para os pinos do sensor:</span><span class="sxs-lookup"><span data-stu-id="f48fa-141">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="f48fa-142">Início (sensor)</span><span class="sxs-lookup"><span data-stu-id="f48fa-142">Start (sensor)</span></span>           | <span data-ttu-id="f48fa-143">Fim (placa)</span><span class="sxs-lookup"><span data-stu-id="f48fa-143">End (board)</span></span>            | <span data-ttu-id="f48fa-144">Cor do cabo</span><span class="sxs-lookup"><span data-stu-id="f48fa-144">Cable color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="f48fa-145">VDD (pino 27A)</span><span class="sxs-lookup"><span data-stu-id="f48fa-145">VDD (Pin 27A)</span></span>            | <span data-ttu-id="f48fa-146">3V (pino 3A)</span><span class="sxs-lookup"><span data-stu-id="f48fa-146">3V (Pin 3A)</span></span>            | <span data-ttu-id="f48fa-147">Cabo vermelho</span><span class="sxs-lookup"><span data-stu-id="f48fa-147">Red cable</span></span>     |
| <span data-ttu-id="f48fa-148">GND (pino 29A)</span><span class="sxs-lookup"><span data-stu-id="f48fa-148">GND (Pin 29A)</span></span>            | <span data-ttu-id="f48fa-149">GND (pino 6A)</span><span class="sxs-lookup"><span data-stu-id="f48fa-149">GND (Pin 6A)</span></span>           | <span data-ttu-id="f48fa-150">Cabo preto</span><span class="sxs-lookup"><span data-stu-id="f48fa-150">Black cable</span></span>   |
| <span data-ttu-id="f48fa-151">SCK (pino 30A)</span><span class="sxs-lookup"><span data-stu-id="f48fa-151">SCK (Pin 30A)</span></span>            | <span data-ttu-id="f48fa-152">SCK (pino 12A)</span><span class="sxs-lookup"><span data-stu-id="f48fa-152">SCK (Pin 12A)</span></span>          | <span data-ttu-id="f48fa-153">Cabo amarelo</span><span class="sxs-lookup"><span data-stu-id="f48fa-153">Yellow cable</span></span>  |
| <span data-ttu-id="f48fa-154">SDO (pino 31A)</span><span class="sxs-lookup"><span data-stu-id="f48fa-154">SDO (Pin 31A)</span></span>            | <span data-ttu-id="f48fa-155">MI (pino 14A)</span><span class="sxs-lookup"><span data-stu-id="f48fa-155">MI (Pin 14A)</span></span>           | <span data-ttu-id="f48fa-156">Cabo branco</span><span class="sxs-lookup"><span data-stu-id="f48fa-156">White cable</span></span>   |
| <span data-ttu-id="f48fa-157">SDI (pino 32A)</span><span class="sxs-lookup"><span data-stu-id="f48fa-157">SDI (Pin 32A)</span></span>            | <span data-ttu-id="f48fa-158">M0 (pino 13A)</span><span class="sxs-lookup"><span data-stu-id="f48fa-158">M0 (Pin 13A)</span></span>           | <span data-ttu-id="f48fa-159">Cabo azul</span><span class="sxs-lookup"><span data-stu-id="f48fa-159">Blue cable</span></span>    |
| <span data-ttu-id="f48fa-160">CS (pino 33A)</span><span class="sxs-lookup"><span data-stu-id="f48fa-160">CS (Pin 33A)</span></span>             | <span data-ttu-id="f48fa-161">GPIO 5 (pino 15J)</span><span class="sxs-lookup"><span data-stu-id="f48fa-161">GPIO 5 (Pin 15J)</span></span>       | <span data-ttu-id="f48fa-162">Cabo laranja</span><span class="sxs-lookup"><span data-stu-id="f48fa-162">Orange cable</span></span>  |

<span data-ttu-id="f48fa-163">Para obter mais informações, consulte [Saídas do sensor de umidade, pressão barométrica e temperatura Adafruit BME280](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) e [Pinagem do Adafruit Feather M0 WiFi](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span><span class="sxs-lookup"><span data-stu-id="f48fa-163">For more information, see [Adafruit BME280 Humidity + Barometric Pressure + Temperature Sensor Breakout](https://learn.adafruit.com/adafruit-bme280-humidity-barometric-pressure-temperature-sensor-breakout/wiring-and-test?view=all) and [Adafruit Feather M0 WiFi pinouts](https://learn.adafruit.com/adafruit-feather-m0-wifi-atwinc1500/pinouts).</span></span>



<span data-ttu-id="f48fa-164">Agora seu Feather M0 WiFi deve estar conectado a um sensor ativo.</span><span class="sxs-lookup"><span data-stu-id="f48fa-164">Now your Feather M0 WiFi should be connected with a working sensor.</span></span>

![Conectar o DHT22 com o Feather Huzzah](media/iot-hub-adafruit-feather-m0-wifi-get-started/4_connect-bme280-feather-m0-wifi.png)

### <a name="connect-feather-m0-wifi-to-your-computer"></a><span data-ttu-id="f48fa-166">Conectar o Feather M0 WiFi ao seu computador</span><span class="sxs-lookup"><span data-stu-id="f48fa-166">Connect Feather M0 WiFi to your computer</span></span>

<span data-ttu-id="f48fa-167">Conforme mostrado a seguir, use o cabo Micro USB para USB Tipo A para conectar o Feather M0 WiFi ao seu computador, conforme mostrado:</span><span class="sxs-lookup"><span data-stu-id="f48fa-167">Use the Micro USB to Type A USB cable to connect Feather M0 WiFi to your computer, as shown:</span></span>

![Conectar o Feather Huzzah ao seu computador](media/iot-hub-adafruit-feather-m0-wifi-get-started/5_connect-feather-m0-wifi-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="f48fa-169">Adicionar permissões de porta serial (somente Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="f48fa-169">Add serial port permissions (Ubuntu only)</span></span>

<span data-ttu-id="f48fa-170">Se você usa o Ubuntu, verifique se tem as permissões para operar na porta USB do Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="f48fa-170">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather M0 WiFi.</span></span> <span data-ttu-id="f48fa-171">Para adicionar permissões de porta serial, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="f48fa-171">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="f48fa-172">Em um terminal, execute os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="f48fa-172">At a terminal, run the following commands:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="f48fa-173">Você recebe uma das seguintes saídas:</span><span class="sxs-lookup"><span data-stu-id="f48fa-173">You get one of the following outputs:</span></span>

   * <span data-ttu-id="f48fa-174">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="f48fa-174">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="f48fa-175">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="f48fa-175">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="f48fa-176">Na saída, observe se `uucp` ou `dialout` é o nome do proprietário do grupo da porta USB.</span><span class="sxs-lookup"><span data-stu-id="f48fa-176">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

2. <span data-ttu-id="f48fa-177">Para adicionar o usuário ao grupo, execute o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="f48fa-177">To add the user to the group, run the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="f48fa-178">Na etapa anterior, você obteve o nome de proprietário do grupo `<group-owner-name>`.</span><span class="sxs-lookup"><span data-stu-id="f48fa-178">In the previous step, you obtained the group owner name `<group-owner-name>`.</span></span> <span data-ttu-id="f48fa-179">Seu nome de usuário do Ubuntu é `<username>`.</span><span class="sxs-lookup"><span data-stu-id="f48fa-179">Your Ubuntu user name is `<username>`.</span></span>

3. <span data-ttu-id="f48fa-180">Saia do Ubuntu e entre novamente para que a alteração seja exibida.</span><span class="sxs-lookup"><span data-stu-id="f48fa-180">For the change to appear, sign out of Ubuntu and then sign in again.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="f48fa-181">Coletar dados de sensor e enviá-los para o hub IoT</span><span class="sxs-lookup"><span data-stu-id="f48fa-181">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="f48fa-182">Nesta seção, você implanta e executa um aplicativo de exemplo no Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="f48fa-182">In this section, you deploy and run a sample application on Feather M0 WiFi.</span></span> <span data-ttu-id="f48fa-183">O aplicativo de exemplo faz o LED piscar no Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="f48fa-183">The sample application makes the LED blink on Feather M0 WiFi.</span></span> <span data-ttu-id="f48fa-184">Em seguida, ele envia os dados de temperatura e umidade coletados do sensor BME280 para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="f48fa-184">It then sends the temperature and humidity data collected from the BME280 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github-and-prepare-the-arduino-ide"></a><span data-ttu-id="f48fa-185">Obtenha o aplicativo de exemplo do GitHub e prepare o IDE do Arduino</span><span class="sxs-lookup"><span data-stu-id="f48fa-185">Get the sample application from GitHub and prepare the Arduino IDE</span></span>

<span data-ttu-id="f48fa-186">O aplicativo de exemplo está hospedado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="f48fa-186">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="f48fa-187">Clone o repositório de exemplo que contém o aplicativo de exemplo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="f48fa-187">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="f48fa-188">Para clonar o repositório de exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="f48fa-188">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="f48fa-189">Abra um prompt de comando ou uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="f48fa-189">Open a command prompt or a terminal window.</span></span>

2. <span data-ttu-id="f48fa-190">Ir para uma pasta onde você deseja que o aplicativo de exemplo a ser armazenado.</span><span class="sxs-lookup"><span data-stu-id="f48fa-190">Go to a folder where you want the sample application to be stored.</span></span>
3. <span data-ttu-id="f48fa-191">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f48fa-191">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-Feather-M0-WiFi-client-app.git
   ```

### <a name="install-the-package-for-feather-m0-wifi-in-the-arduino-ide"></a><span data-ttu-id="f48fa-192">Instale o pacote para o Feather M0 WiFi no IDE do Arduino</span><span class="sxs-lookup"><span data-stu-id="f48fa-192">Install the package for Feather M0 WiFi in the Arduino IDE</span></span>

1. <span data-ttu-id="f48fa-193">Abra a pasta onde o aplicativo de exemplo está armazenado.</span><span class="sxs-lookup"><span data-stu-id="f48fa-193">Open the folder where the sample application is stored.</span></span>

2. <span data-ttu-id="f48fa-194">Abra o arquivo app.ino na pasta do aplicativo no IDE do Arduino.</span><span class="sxs-lookup"><span data-stu-id="f48fa-194">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Abrir o aplicativo de exemplo no IDE do Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/6_arduino-ide-open-sample-app.png)


1. <span data-ttu-id="f48fa-196">Clique em **Arquivo** > **Preferências** (Windows/Linux) ou **Arduino** > **Preferências** (Mac) e copie e cole o link abaixo para na opção **URLs adicionais do Gerenciador de Placas** nas preferências do IDE do Arduino.</span><span class="sxs-lookup"><span data-stu-id="f48fa-196">Click **File** > **Preferences** (Windows/Linux) or **Arduino** > **Preferences** (Mac) and copy and paste the link below into the **Additional Boards Manager URLs** option in the Arduino IDE preferences.</span></span>
   
   ```
   https://adafruit.github.io/arduino-board-index/package_adafruit_index.json, https://adafruit.github.io/arduino-board-index/package_adafruit_index.json
   ```

1. <span data-ttu-id="f48fa-197">Clique em **Ferramentas** > **Placa** > **Gerenciador de Placas** e, em seguida, instale o `Arduino SAMD Boards` versão `1.6.2` ou posterior.</span><span class="sxs-lookup"><span data-stu-id="f48fa-197">Click **Tools** > **Board** > **Boards Manager**, and then install the `Arduino SAMD Boards` version `1.6.2` or later.</span></span> 

1. <span data-ttu-id="f48fa-198">Em seguida, na mesma janela, instale o pacote `Adafruit SAMD Boards` para adicionar as definições do arquivo de placa.</span><span class="sxs-lookup"><span data-stu-id="f48fa-198">Then in the same window, install `Adafruit SAMD Boards` package to add the board file definitions.</span></span>

   ![O pacote esp8266 está instalado](media/iot-hub-adafruit-feather-m0-wifi-get-started/7_arduino-ide-package-url.png)

4. <span data-ttu-id="f48fa-200">Clique em **Ferramentas** > **Placa** > **Adafruit M0 WiFi**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-200">Click **Tools** > **Board** > **Adafruit M0 WiFi**.</span></span>

5. <span data-ttu-id="f48fa-201">Instale os drivers (apenas para Windows).</span><span class="sxs-lookup"><span data-stu-id="f48fa-201">Install drivers (for Windows only).</span></span> <span data-ttu-id="f48fa-202">Quando você conecta o Feather M0 Wi-Fi, pode precisar instalar um driver.</span><span class="sxs-lookup"><span data-stu-id="f48fa-202">When you plug in Feather M0 WiFi, you might need to install a driver.</span></span> <span data-ttu-id="f48fa-203">Clique no [link de download na página da Web](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) para baixar o instalador do driver.</span><span class="sxs-lookup"><span data-stu-id="f48fa-203">Click [the download link on the webpage](https://github.com/adafruit/Adafruit_Windows_Drivers/releases/download/1.1/adafruit_drivers.exe) to download the driver installer.</span></span> <span data-ttu-id="f48fa-204">Siga as etapas para instalar os drivers que deseja.</span><span class="sxs-lookup"><span data-stu-id="f48fa-204">Follow the steps to install the drivers you want.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="f48fa-205">Instalar as bibliotecas necessárias</span><span class="sxs-lookup"><span data-stu-id="f48fa-205">Install necessary libraries</span></span>

1. <span data-ttu-id="f48fa-206">No IDE Arduino, clique em **esboço** > **biblioteca incluem** > **gerenciar bibliotecas**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-206">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>

2. <span data-ttu-id="f48fa-207">Procure a seguinte biblioteca nomes individualmente.</span><span class="sxs-lookup"><span data-stu-id="f48fa-207">Search for the following library names one by one.</span></span> <span data-ttu-id="f48fa-208">Para cada biblioteca que você localizar, clique em **Instalar**:</span><span class="sxs-lookup"><span data-stu-id="f48fa-208">For each library that you find, click **Install**:</span></span>

   * `RTCZero`
   * `NTPClient`
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_HTTP`
   * `ArduinoJson`
   * `Adafruit BME280 Library`
   * `Adafruit Unified Sensor`

3. <span data-ttu-id="f48fa-209">Instale o `Adafruit_WINC1500` manualmente.</span><span class="sxs-lookup"><span data-stu-id="f48fa-209">Manually install `Adafruit_WINC1500`.</span></span> <span data-ttu-id="f48fa-210">Vá para [este site](https://github.com/adafruit/Adafruit_WINC1500) e clique em **Clonar ou baixar** > **Baixar ZIP**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-210">Go to [this website](https://github.com/adafruit/Adafruit_WINC1500) and click **Clone or download** > **Download ZIP**.</span></span> <span data-ttu-id="f48fa-211">Em seguida, no IDE do Arduino, acesse **Esboço** > **Incluir Biblioteca** > **Adicionar Biblioteca .zip** e adicione o arquivo zip.</span><span class="sxs-lookup"><span data-stu-id="f48fa-211">Then in your Arduino IDE, go to **Sketch** > **Include Library** > **Add .zip Library** and add the zip file.</span></span>

### <a name="use-the-sample-application-if-you-dont-have-a-real-bme280-sensor"></a><span data-ttu-id="f48fa-212">Use o aplicativo de exemplo se você não tiver um sensor BME280 real</span><span class="sxs-lookup"><span data-stu-id="f48fa-212">Use the sample application if you don’t have a real BME280 sensor</span></span>

<span data-ttu-id="f48fa-213">Caso você não tenha um sensor BME280 real, o aplicativo de exemplo poderá simular os dados de temperatura e umidade.</span><span class="sxs-lookup"><span data-stu-id="f48fa-213">If you don’t have a real BME280 sensor, the sample application can simulate temperature and humidity data.</span></span> <span data-ttu-id="f48fa-214">Para configurar o aplicativo de exemplo para usar dados simulados, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="f48fa-214">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="f48fa-215">Abra o `config.h` arquivo o `app` pasta.</span><span class="sxs-lookup"><span data-stu-id="f48fa-215">Open the `config.h` file in the `app` folder.</span></span>

2. <span data-ttu-id="f48fa-216">Localize a seguinte linha de código e altere o valor de `false` para `true`:</span><span class="sxs-lookup"><span data-stu-id="f48fa-216">Locate the following line of code and change the value from `false` to `true`:</span></span>

   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar o aplicativo de exemplo para usar dados simulados](media/iot-hub-adafruit-feather-m0-wifi-get-started/8_arduino-ide-configure-app-use-simulated-data.png)

3. <span data-ttu-id="f48fa-218">Salve o arquivo com `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="f48fa-218">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-m0-wifi"></a><span data-ttu-id="f48fa-219">Implantar o aplicativo de exemplo para o Feather M0 WiFi</span><span class="sxs-lookup"><span data-stu-id="f48fa-219">Deploy the sample application to Feather M0 WiFi</span></span>

1. <span data-ttu-id="f48fa-220">No IDE do Arduino, clique em **Ferramenta** > **Porta** e clique na porta serial do Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="f48fa-220">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather M0 WiFi.</span></span>

2. <span data-ttu-id="f48fa-221">Clique em **Esboço** > **Carregar** para criar e implantar o aplicativo de exemplo do Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="f48fa-221">Click **Sketch** > **Upload** to build and deploy the sample application to Feather M0 WiFi.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="f48fa-222">Inserir suas credenciais</span><span class="sxs-lookup"><span data-stu-id="f48fa-222">Enter your credentials</span></span>

<span data-ttu-id="f48fa-223">Depois que o upload for concluído com êxito, siga estas etapas para inserir suas credenciais:</span><span class="sxs-lookup"><span data-stu-id="f48fa-223">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="f48fa-224">No IDE Arduino, clique em **ferramentas** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="f48fa-224">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>

2. <span data-ttu-id="f48fa-225">No canto inferior direito da janela do monitor serial, selecione **Nenhum final de linha** na lista suspensa à esquerda.</span><span class="sxs-lookup"><span data-stu-id="f48fa-225">In the lower-right corner of the serial monitor window, select **No line ending** in the drop-down list on the left.</span></span>
3. <span data-ttu-id="f48fa-226">Selecione **115200 baud** na lista suspensa à direita.</span><span class="sxs-lookup"><span data-stu-id="f48fa-226">Select **115200 baud** in the drop-down list on the right.</span></span>
4. <span data-ttu-id="f48fa-227">Na caixa de entrada na parte superior, insira as seguintes informações se você for solicitado a fornecê-las e, em seguida, clique em **Enviar**:</span><span class="sxs-lookup"><span data-stu-id="f48fa-227">In the input box at the top, enter the following information if you're asked to provide it, and click **Send**:</span></span>

   * <span data-ttu-id="f48fa-228">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="f48fa-228">Wi-Fi SSID</span></span>
   * <span data-ttu-id="f48fa-229">Senha de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="f48fa-229">Wi-Fi password</span></span>
   * <span data-ttu-id="f48fa-230">Cadeia de conexão de dispositivo</span><span class="sxs-lookup"><span data-stu-id="f48fa-230">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="f48fa-231">As informações de credencial são armazenadas na EEPROM do Feather M0 WiFi.</span><span class="sxs-lookup"><span data-stu-id="f48fa-231">The credential information is stored in the EEPROM of Feather M0 WiFi.</span></span> <span data-ttu-id="f48fa-232">Se você clicar no botão de redefinir na placa do Feather M0 WiFi, o aplicativo de exemplo perguntará se você deseja apagar as informações.</span><span class="sxs-lookup"><span data-stu-id="f48fa-232">If you click the reset button on the Feather M0 WiFi board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="f48fa-233">Digite `Y` para apagar as informações.</span><span class="sxs-lookup"><span data-stu-id="f48fa-233">Enter `Y` to erase the information.</span></span> <span data-ttu-id="f48fa-234">Você é solicitado a fornecer as informações uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="f48fa-234">You're asked to provide the information a second time.</span></span>

### <a name="verify-that-the-sample-application-is-running-successfully"></a><span data-ttu-id="f48fa-235">Verifique se o aplicativo de exemplo está sendo executado com êxito</span><span class="sxs-lookup"><span data-stu-id="f48fa-235">Verify that the sample application is running successfully</span></span>

<span data-ttu-id="f48fa-236">Caso você veja a seguinte saída na janela do monitor serial e o LED piscando no Feather M0 WiFi, o aplicativo de exemplo estará sendo executado com êxito:</span><span class="sxs-lookup"><span data-stu-id="f48fa-236">If you see the following output from the serial monitor window and the blinking LED on Feather M0 WiFi, the sample application is running successfully:</span></span>

![Saída final no IDE do Arduino](media/iot-hub-adafruit-feather-m0-wifi-get-started/9_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="f48fa-238">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f48fa-238">Next steps</span></span>

<span data-ttu-id="f48fa-239">Você conectou um Feather M0 WiFi ao hub IoT e enviou os dados capturados pelo sensor para o hub IoT com sucesso.</span><span class="sxs-lookup"><span data-stu-id="f48fa-239">You have successfully connected Feather M0 WiFi to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

