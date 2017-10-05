---
title: "ESP8266 para a nuvem – conectar o Sparkfun ESP8266 Thing Dev ao Hub IoT do Azure | Microsoft Docs"
description: Neste tutorial, aprenda a configurar e conectar Sparkfun ESP8266 Thing Dev para o Hub IoT do Azure para enviar dados para a plataforma de nuvem do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: 587fe292-9602-45b4-95ee-f39bba10e716
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/16/2017
ms.author: xshi
ms.openlocfilehash: 557f0cdf375b345e0dbe0526f5a5bd3c050dec38
ms.sourcegitcommit: 50e23e8d3b1148ae2d36dad3167936b4e52c8a23
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/18/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="ec58c-103">Conectar a Sparkfun ESP8266 Thing Dev ao Hub IoT do Azure na nuvem</span><span class="sxs-lookup"><span data-stu-id="ec58c-103">Connect Sparkfun ESP8266 Thing Dev to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![conexão entre DHT22, a Thing Dev e o Hub IoT](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="ec58c-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="ec58c-105">What you will do</span></span>

<span data-ttu-id="ec58c-106">Conecte a Sparkfun ESP8266 Thing Dev a um Hub IoT que você criará.</span><span class="sxs-lookup"><span data-stu-id="ec58c-106">Connect Sparkfun ESP8266 Thing Dev to an IoT hub you will create.</span></span> <span data-ttu-id="ec58c-107">Execute um aplicativo de exemplo no ESP8266 para coletar dados de temperatura e umidade de um sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="ec58c-107">Then run a sample application on ESP8266 to collect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="ec58c-108">Por fim, envie os dados do sensor para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ec58c-108">Finally, send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="ec58c-109">Se você estiver usando outras placas ESP8266, você ainda pode seguir estas etapas para conectar-se ao seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ec58c-109">If you are using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="ec58c-110">Dependendo da placa ESP8266 que você esteja usando, talvez seja necessário reconfigurar o `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="ec58c-110">Depending on the ESP8266 board you are using, you may need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="ec58c-111">Por exemplo, se você estiver usando a ESP8266 da Al Thinker, poderá alterá-la de `0` para `2`.</span><span class="sxs-lookup"><span data-stu-id="ec58c-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` to `2`.</span></span> <span data-ttu-id="ec58c-112">Ainda não tem um kit?: Clique [aqui](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="ec58c-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="ec58c-113">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="ec58c-113">What you will learn</span></span>

* <span data-ttu-id="ec58c-114">Como criar um Hub IoT e registrar um dispositivo para a Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="ec58c-114">How to create an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="ec58c-115">Como conectar o Thing Dev ao sensor e seu computador.</span><span class="sxs-lookup"><span data-stu-id="ec58c-115">How to connect Thing Dev with the sensor and your computer.</span></span>
* <span data-ttu-id="ec58c-116">Como coletar dados de sensor executando um aplicativo de exemplo no Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="ec58c-116">How to collect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="ec58c-117">Como enviar os dados do sensor para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ec58c-117">How to send the sensor data to your IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="ec58c-118">O que será necessário</span><span class="sxs-lookup"><span data-stu-id="ec58c-118">What you will need</span></span>

![partes necessárias para o tutorial](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="ec58c-120">Para concluir esta operação, você precisará das seguintes partes do seu Kit de início do Thing Dev:</span><span class="sxs-lookup"><span data-stu-id="ec58c-120">To complete this operation, you need the following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="ec58c-121">A placa de desenvolvimento Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="ec58c-121">The Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="ec58c-122">Um cabo Micro USB para USB Tipo A.</span><span class="sxs-lookup"><span data-stu-id="ec58c-122">A Micro USB to Type A USB cable.</span></span>

<span data-ttu-id="ec58c-123">Você também precisa do seguinte para seu ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="ec58c-123">You also need the following for your development environment:</span></span>

* <span data-ttu-id="ec58c-124">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec58c-124">An active Azure subscription.</span></span> <span data-ttu-id="ec58c-125">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ec58c-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="ec58c-126">Mac ou PC que esteja executando o Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ec58c-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="ec58c-127">Rede sem fio à qual a Sparkfun ESP8266 Thing Dev pode se conectar.</span><span class="sxs-lookup"><span data-stu-id="ec58c-127">Wireless network for Sparkfun ESP8266 Thing Dev to connect to.</span></span>
* <span data-ttu-id="ec58c-128">Uma conexão com a Internet para baixar a ferramenta de configuração.</span><span class="sxs-lookup"><span data-stu-id="ec58c-128">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="ec58c-129">[IDE Arduino](https://www.arduino.cc/en/main/software) versão 1.6.8 (ou mais recente), versões anteriores não funcionará com a biblioteca de AzureIoT.</span><span class="sxs-lookup"><span data-stu-id="ec58c-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with the AzureIoT library.</span></span>

<span data-ttu-id="ec58c-130">Os itens a seguir são opcionais, caso você não tenha um sensor.</span><span class="sxs-lookup"><span data-stu-id="ec58c-130">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="ec58c-131">Você também tem a opção de usar dados de sensor simulada.</span><span class="sxs-lookup"><span data-stu-id="ec58c-131">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="ec58c-132">Um sensor de temperatura e umidade Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="ec58c-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="ec58c-133">Uma placa universal.</span><span class="sxs-lookup"><span data-stu-id="ec58c-133">A breadboard.</span></span>
* <span data-ttu-id="ec58c-134">Cabos de jumper de M/M.</span><span class="sxs-lookup"><span data-stu-id="ec58c-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-the-sensor-and-your-computer"></a><span data-ttu-id="ec58c-135">Conecte a ESP8266 Thing Dev ao sensor e seu computador</span><span class="sxs-lookup"><span data-stu-id="ec58c-135">Connect ESP8266 Thing Dev with the sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-esp8266-thing-dev"></a><span data-ttu-id="ec58c-136">Conecte um sensor de temperatura e umidade DHT22 a ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="ec58c-136">Connect a DHT22 temperature and humidity sensor to ESP8266 Thing Dev</span></span>

<span data-ttu-id="ec58c-137">Use os cabos da placa universal e jumper para fazer a conexão da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="ec58c-137">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="ec58c-138">Se você não tiver um sensor, ignore esta seção porque você pode usar dados de sensor simulado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="ec58c-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![referência de conexões](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="ec58c-140">Pinos de sensor, usaremos a ligação a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec58c-140">For sensor pins, we will use the following wiring:</span></span>

| <span data-ttu-id="ec58c-141">Início (Sensor)</span><span class="sxs-lookup"><span data-stu-id="ec58c-141">Start (Sensor)</span></span>           | <span data-ttu-id="ec58c-142">End (quadro)</span><span class="sxs-lookup"><span data-stu-id="ec58c-142">End (Board)</span></span>           | <span data-ttu-id="ec58c-143">Cor de cabo</span><span class="sxs-lookup"><span data-stu-id="ec58c-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="ec58c-144">VDD (Pin 27F)</span><span class="sxs-lookup"><span data-stu-id="ec58c-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="ec58c-145">3V (Pin 8A)</span><span class="sxs-lookup"><span data-stu-id="ec58c-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="ec58c-146">Cabo vermelho</span><span class="sxs-lookup"><span data-stu-id="ec58c-146">Red cable</span></span>     |
| <span data-ttu-id="ec58c-147">DATA (Pin 28F)</span><span class="sxs-lookup"><span data-stu-id="ec58c-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="ec58c-148">GPIO 2 (Pin 9A)</span><span class="sxs-lookup"><span data-stu-id="ec58c-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="ec58c-149">Cabo branco</span><span class="sxs-lookup"><span data-stu-id="ec58c-149">White cable</span></span>    |
| <span data-ttu-id="ec58c-150">GND (Pin 30F)</span><span class="sxs-lookup"><span data-stu-id="ec58c-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="ec58c-151">GND (Pin 7J)</span><span class="sxs-lookup"><span data-stu-id="ec58c-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="ec58c-152">Cabo preto</span><span class="sxs-lookup"><span data-stu-id="ec58c-152">Black cable</span></span>   |


- <span data-ttu-id="ec58c-153">Para obter mais informações, consulte: [Instalação do sensor DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) e [Especificação da Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="ec58c-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="ec58c-154">Agora sua Sparkfun ESP8266 Thing Dev deve estar conectada a um sensor ativo.</span><span class="sxs-lookup"><span data-stu-id="ec58c-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![conectar o dht22 à ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-to-your-computer"></a><span data-ttu-id="ec58c-156">Conectar a Sparkfun ESP8266 Thing Dev ao computador</span><span class="sxs-lookup"><span data-stu-id="ec58c-156">Connect Sparkfun ESP8266 Thing Dev to your computer</span></span>

<span data-ttu-id="ec58c-157">Use o cabo Micro USB para USB tipo A para conectar a Sparkfun ESP8266 Thing Dev a seu computador conforme descrito a seguir.</span><span class="sxs-lookup"><span data-stu-id="ec58c-157">Use the Micro USB to Type A USB cable to connect Sparkfun ESP8266 Thing Dev to your computer as follows.</span></span>

![conectar o feather huzzah ao seu computador](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="ec58c-159">Adicionar permissões de porta serial - somente Ubuntu</span><span class="sxs-lookup"><span data-stu-id="ec58c-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="ec58c-160">Se você usar o Ubuntu, certifique-se de que um usuário normal tenha as permissões para operar na porta USB da Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="ec58c-160">If you use Ubuntu, make sure a normal user has the permissions to operate on the USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="ec58c-161">Para adicionar permissões de porta serial para um usuário normal, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ec58c-161">To add serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="ec58c-162">Execute os seguintes comandos em um terminal:</span><span class="sxs-lookup"><span data-stu-id="ec58c-162">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="ec58c-163">Você recebe uma das seguintes saídas:</span><span class="sxs-lookup"><span data-stu-id="ec58c-163">You get one of the following outputs:</span></span>

   * <span data-ttu-id="ec58c-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="ec58c-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="ec58c-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="ec58c-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="ec58c-166">Na saída, observe `uucp` ou `dialout` que é o nome do proprietário do grupo da porta USB.</span><span class="sxs-lookup"><span data-stu-id="ec58c-166">In the output, notice `uucp` or `dialout` that is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="ec58c-167">Adicione o usuário ao grupo, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ec58c-167">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="ec58c-168">`<group-owner-name>` é o nome de proprietário de grupo que você obteve na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="ec58c-168">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="ec58c-169">`<username>` é o nome de usuário do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ec58c-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="ec58c-170">Faça logoff do Ubuntu e faça logon novamente para que a alteração entre em vigor.</span><span class="sxs-lookup"><span data-stu-id="ec58c-170">Log out Ubuntu and log in it again for the change to take effect.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="ec58c-171">Coletar dados de sensor e enviá-los para o hub IoT</span><span class="sxs-lookup"><span data-stu-id="ec58c-171">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="ec58c-172">Nesta seção, implante e execute um aplicativo de exemplo em Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="ec58c-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="ec58c-173">O aplicativo de exemplo pisca o LED da Sparkfun ESP8266 Thing Dev e envia os dados de temperatura e umidade coletados do sensor DHT22 para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ec58c-173">The sample application blinks the LED on Sparkfun ESP8266 Thing Dev and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="ec58c-174">Obter o aplicativo de exemplo do GitHub</span><span class="sxs-lookup"><span data-stu-id="ec58c-174">Get the sample application from GitHub</span></span>

<span data-ttu-id="ec58c-175">O aplicativo de exemplo está hospedado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="ec58c-175">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="ec58c-176">Clone o repositório de exemplo que contém o aplicativo de exemplo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="ec58c-176">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="ec58c-177">Para clonar o repositório de exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ec58c-177">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="ec58c-178">Abra um prompt de comando ou uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="ec58c-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="ec58c-179">Ir para uma pasta onde você deseja que o aplicativo de exemplo a ser armazenado.</span><span class="sxs-lookup"><span data-stu-id="ec58c-179">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="ec58c-180">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec58c-180">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="ec58c-181">Instale o pacote para a Sparkfun ESP8266 Thing Dev no IDE Arduino:</span><span class="sxs-lookup"><span data-stu-id="ec58c-181">Install the package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="ec58c-182">Abra a pasta onde o aplicativo de exemplo está armazenado.</span><span class="sxs-lookup"><span data-stu-id="ec58c-182">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="ec58c-183">Abra o arquivo app.ino na pasta de aplicativo em Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="ec58c-183">Open the app.ino file in the app folder in Arduino IDE.</span></span>

   ![abrir o aplicativo de exemplo no ide arduino](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="ec58c-185">No IDE Arduino, clique em **arquivo** > **preferências**.</span><span class="sxs-lookup"><span data-stu-id="ec58c-185">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="ec58c-186">No **preferências** caixa de diálogo, clique no ícone ao lado de **URLs adicionais do Gerenciador de placas** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="ec58c-186">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="ec58c-187">Na janela pop-up, insira a URL a seguir e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec58c-187">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![aponte para uma url do pacote no ide arduino](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="ec58c-189">No **preferência** caixa de diálogo, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ec58c-189">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="ec58c-190">Clique em **Ferramentas** > **Placa** > **Gerenciador de Placas** e procure esp8266.</span><span class="sxs-lookup"><span data-stu-id="ec58c-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="ec58c-191">ESP8266 com uma versão 2.2.0 ou posterior deve ser instalado.</span><span class="sxs-lookup"><span data-stu-id="ec58c-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![o pacote de esp8266 está instalado](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="ec58c-193">Clique em **Ferramentas** > **Painel** > **Sparkfun ESP8266 Thing Dev**.</span><span class="sxs-lookup"><span data-stu-id="ec58c-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="ec58c-194">Instalar as bibliotecas necessárias</span><span class="sxs-lookup"><span data-stu-id="ec58c-194">Install necessary libraries</span></span>

1. <span data-ttu-id="ec58c-195">No IDE Arduino, clique em **esboço** > **biblioteca incluem** > **gerenciar bibliotecas**.</span><span class="sxs-lookup"><span data-stu-id="ec58c-195">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="ec58c-196">Procure a seguinte biblioteca nomes individualmente.</span><span class="sxs-lookup"><span data-stu-id="ec58c-196">Search for the following library names one by one.</span></span> <span data-ttu-id="ec58c-197">Para cada biblioteca que você localizar, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="ec58c-197">For each of the library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="ec58c-198">Você não tem um sensor DHT22 real?</span><span class="sxs-lookup"><span data-stu-id="ec58c-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="ec58c-199">O aplicativo de exemplo pode simular a temperatura e umidade dados caso você não tenha um sensor DHT22 real.</span><span class="sxs-lookup"><span data-stu-id="ec58c-199">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="ec58c-200">Para habilitar o aplicativo de exemplo usar dados simulados, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ec58c-200">To enable the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="ec58c-201">Abra o `config.h` arquivo o `app` pasta.</span><span class="sxs-lookup"><span data-stu-id="ec58c-201">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="ec58c-202">Localize a seguinte linha de código e altere o valor de `false` para `true`:</span><span class="sxs-lookup"><span data-stu-id="ec58c-202">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar o aplicativo de exemplo para usar dados simulados](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="ec58c-204">Salvar com `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="ec58c-204">Save with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-sparkfun-esp8266-thing-dev"></a><span data-ttu-id="ec58c-205">Implantar o aplicativo de exemplo para a Sparkfun ESP8266 Thing Dev</span><span class="sxs-lookup"><span data-stu-id="ec58c-205">Deploy the sample application to Sparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="ec58c-206">No IDE Arduino, clique em **Ferramenta** > **Porta** e clique na porta serial para a Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="ec58c-206">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="ec58c-207">Clique em **Esboço** > **Upload** para criar e implantar o aplicativo de exemplo para a Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="ec58c-207">Click **Sketch** > **Upload** to build and deploy the sample application to Sparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="ec58c-208">Se você estiver usando macOS provavelmente você pode ver as seguintes mensagens de erro durante o carregamento.</span><span class="sxs-lookup"><span data-stu-id="ec58c-208">If you are using macOS you could probably see the following messages during uploading.</span></span> <span data-ttu-id="ec58c-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="ec58c-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="ec58c-210">Abra a janela do seu terminal e concluir ações para resolver esse problema abaixo.</span><span class="sxs-lookup"><span data-stu-id="ec58c-210">Please open your ternimal window and finish below actions to solve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="ec58c-211">Inserir suas credenciais</span><span class="sxs-lookup"><span data-stu-id="ec58c-211">Enter your credentials</span></span>

<span data-ttu-id="ec58c-212">Depois que o carregamento for concluído com êxito, siga as etapas para inserir suas credenciais:</span><span class="sxs-lookup"><span data-stu-id="ec58c-212">After the upload completes successfully, follow the steps to enter your credentials:</span></span>

1. <span data-ttu-id="ec58c-213">No IDE Arduino, clique em **ferramentas** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="ec58c-213">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="ec58c-214">Na janela monitor serial, observe as duas listas suspensas no canto inferior direito.</span><span class="sxs-lookup"><span data-stu-id="ec58c-214">In the serial monitor window, notice the two drop-down lists on the bottom right corner.</span></span>
1. <span data-ttu-id="ec58c-215">Selecione **nenhuma final de linha** para obter a lista suspensa à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ec58c-215">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="ec58c-216">Selecione **115200 baud** para obter a lista suspensa à direita.</span><span class="sxs-lookup"><span data-stu-id="ec58c-216">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="ec58c-217">Na caixa de entrada localizada na parte superior da janela do monitor serial, insira as seguintes informações se você for solicitado a fornecê-las e clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="ec58c-217">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="ec58c-218">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="ec58c-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="ec58c-219">Senha de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="ec58c-219">Wi-Fi password</span></span>
   * <span data-ttu-id="ec58c-220">Cadeia de conexão de dispositivo</span><span class="sxs-lookup"><span data-stu-id="ec58c-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="ec58c-221">As informações de credencial são armazenadas no EEPROM da Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="ec58c-221">The credential information is stored in the EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="ec58c-222">Se você clicar no botão Redefinir no painel da Sparkfun ESP8266 Thing Dev, o aplicativo de exemplo pergunta se você deseja apagar as informações.</span><span class="sxs-lookup"><span data-stu-id="ec58c-222">If you click the reset button on the Sparkfun ESP8266 Thing Dev board, the sample application asks you if you want to erase the information.</span></span> <span data-ttu-id="ec58c-223">Digite `Y` para apagar as informações e será solicitado que você forneça as informações novamente.</span><span class="sxs-lookup"><span data-stu-id="ec58c-223">Enter `Y` to have the information erased and you are asked to provide the information again.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="ec58c-224">Verificar se o aplicativo de exemplo está sendo executado com êxito</span><span class="sxs-lookup"><span data-stu-id="ec58c-224">Verify the sample application is running successfully</span></span>

<span data-ttu-id="ec58c-225">Se você vir a seguinte saída da janela serial monitor e o LED piscando na Sparkfun ESP8266 Thing Dev, o aplicativo de exemplo está sendo executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="ec58c-225">If you see the following output from the serial monitor window and the blinking LED on Sparkfun ESP8266 Thing Dev, the sample application is running successfully.</span></span>

![saída final no ide arduino](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="ec58c-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ec58c-227">Next steps</span></span>

<span data-ttu-id="ec58c-228">Você conectou uma Sparkfun ESP8266 Thing Dev ao Hub IoT e enviou os dados capturados pelo sensor ao Hub IoT com êxito.</span><span class="sxs-lookup"><span data-stu-id="ec58c-228">You have successfully connected a Sparkfun ESP8266 Thing Dev to your IoT hub and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
