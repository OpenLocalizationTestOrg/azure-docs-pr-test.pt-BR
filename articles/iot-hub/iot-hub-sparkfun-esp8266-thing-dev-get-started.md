---
title: aaaESP8266 toocloud - tooAzure de conectar o Sparkfun ESP8266 coisa Dev IoT Hub | Microsoft Docs
description: Saiba como toosetup e conecte-se tooAzure Sparkfun ESP8266 coisa Dev IoT Hub para ele plataforma de nuvem do Azure toosend dados toohello neste tutorial.
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
ms.openlocfilehash: 19b249df23b6df516634853521c6d532f51014da
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-sparkfun-esp8266-thing-dev-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="3b32c-103">Conecte-se tooAzure Sparkfun ESP8266 coisa Dev IoT Hub na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="3b32c-103">Connect Sparkfun ESP8266 Thing Dev tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![conexão entre DHT22, a Thing Dev e o Hub IoT](media/iot-hub-sparkfun-thing-dev-get-started/1_connection-hdt22-thing-dev-iot-hub.png)

## <a name="what-you-will-do"></a><span data-ttu-id="3b32c-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="3b32c-105">What you will do</span></span>

<span data-ttu-id="3b32c-106">Conecte-se Sparkfun ESP8266 coisa Dev tooan IoT hub que será criado.</span><span class="sxs-lookup"><span data-stu-id="3b32c-106">Connect Sparkfun ESP8266 Thing Dev tooan IoT hub you will create.</span></span> <span data-ttu-id="3b32c-107">Execute um aplicativo de exemplo em dados de temperatura e umidade toocollect ESP8266 partir de um sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="3b32c-107">Then run a sample application on ESP8266 toocollect temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="3b32c-108">Por fim, envie o hub IoT do hello sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="3b32c-108">Finally, send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="3b32c-109">Se você estiver usando outras placas ESP8266, você ainda pode seguir estas etapas tooconnect-tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="3b32c-109">If you are using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="3b32c-110">Dependendo da placa Olá ESP8266 que está usando, talvez seja necessário Olá tooreconfigure `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="3b32c-110">Depending on hello ESP8266 board you are using, you may need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="3b32c-111">Por exemplo, se você estiver usando ESP8266 do AI Thinker, você pode alterá-la de `0` muito`2`.</span><span class="sxs-lookup"><span data-stu-id="3b32c-111">For example, if you are using ESP8266 from AI-Thinker, you may change it from `0` too`2`.</span></span> <span data-ttu-id="3b32c-112">Ainda não tem um kit?: Clique [aqui](http://azure.com/iotstarterkits)</span><span class="sxs-lookup"><span data-stu-id="3b32c-112">Don't have a kit yet?: Click [here](http://azure.com/iotstarterkits)</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3b32c-113">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="3b32c-113">What you will learn</span></span>

* <span data-ttu-id="3b32c-114">Como toocreate um hub IoT e registrar um dispositivo para propósitos de coisa de dispositivos</span><span class="sxs-lookup"><span data-stu-id="3b32c-114">How toocreate an IoT hub and register a device for Thing Dev.</span></span>
* <span data-ttu-id="3b32c-115">Como tooconnect coisa desenvolvimento com sensor hello e seu computador.</span><span class="sxs-lookup"><span data-stu-id="3b32c-115">How tooconnect Thing Dev with hello sensor and your computer.</span></span>
* <span data-ttu-id="3b32c-116">Como os dados do sensor toocollect executando um aplicativo de exemplo no coisa propósitos de dispositivos</span><span class="sxs-lookup"><span data-stu-id="3b32c-116">How toocollect sensor data by running a sample application on Thing Dev.</span></span>
* <span data-ttu-id="3b32c-117">Como toosend Olá hub IoT do sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="3b32c-117">How toosend hello sensor data tooyour IoT hub.</span></span>

## <a name="what-you-will-need"></a><span data-ttu-id="3b32c-118">O que será necessário</span><span class="sxs-lookup"><span data-stu-id="3b32c-118">What you will need</span></span>

![Partes necessárias para o tutorial Olá](media/iot-hub-sparkfun-thing-dev-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="3b32c-120">toocomplete essa operação, você precisa Olá seguir partes de seu Starter Kit de desenvolvimento de coisa:</span><span class="sxs-lookup"><span data-stu-id="3b32c-120">toocomplete this operation, you need hello following parts from your Thing Dev Starter Kit:</span></span>

* <span data-ttu-id="3b32c-121">Olá Sparkfun ESP8266 coisa Dev quadro.</span><span class="sxs-lookup"><span data-stu-id="3b32c-121">hello Sparkfun ESP8266 Thing Dev board.</span></span>
* <span data-ttu-id="3b32c-122">Cabo USB A um tooType Micro USB.</span><span class="sxs-lookup"><span data-stu-id="3b32c-122">A Micro USB tooType A USB cable.</span></span>

<span data-ttu-id="3b32c-123">Você também precisa seguir Olá para o seu ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="3b32c-123">You also need hello following for your development environment:</span></span>

* <span data-ttu-id="3b32c-124">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="3b32c-124">An active Azure subscription.</span></span> <span data-ttu-id="3b32c-125">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="3b32c-125">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="3b32c-126">Mac ou PC que esteja executando o Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3b32c-126">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="3b32c-127">Rede sem fio para tooconnect Sparkfun ESP8266 coisa desenvolvimento para.</span><span class="sxs-lookup"><span data-stu-id="3b32c-127">Wireless network for Sparkfun ESP8266 Thing Dev tooconnect to.</span></span>
* <span data-ttu-id="3b32c-128">Ferramenta de configuração saudação do toodownload de conexão de Internet.</span><span class="sxs-lookup"><span data-stu-id="3b32c-128">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="3b32c-129">[Arduino IDE](https://www.arduino.cc/en/main/software) versão 1.6.8 (ou mais recente), versões anteriores não funcionarão com a biblioteca de AzureIoT hello.</span><span class="sxs-lookup"><span data-stu-id="3b32c-129">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 (or newer), earlier versions will not work with hello AzureIoT library.</span></span>

<span data-ttu-id="3b32c-130">Olá itens a seguir são opcionais no caso de você não tiver um sensor.</span><span class="sxs-lookup"><span data-stu-id="3b32c-130">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="3b32c-131">Você também tem a opção de saudação do uso de dados de sensor simulada.</span><span class="sxs-lookup"><span data-stu-id="3b32c-131">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="3b32c-132">Um sensor de temperatura e umidade Adafruit DHT22.</span><span class="sxs-lookup"><span data-stu-id="3b32c-132">An Adafruit DHT22 temperature and humidity sensor.</span></span>
* <span data-ttu-id="3b32c-133">Uma placa universal.</span><span class="sxs-lookup"><span data-stu-id="3b32c-133">A breadboard.</span></span>
* <span data-ttu-id="3b32c-134">Cabos de jumper de M/M.</span><span class="sxs-lookup"><span data-stu-id="3b32c-134">M/M jumper wires.</span></span>

[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-esp8266-thing-dev-with-hello-sensor-and-your-computer"></a><span data-ttu-id="3b32c-135">Conecte-se a ESP8266 coisa desenvolvimento com sensor hello e seu computador</span><span class="sxs-lookup"><span data-stu-id="3b32c-135">Connect ESP8266 Thing Dev with hello sensor and your computer</span></span>

### <a name="connect-a-dht22-temperature-and-humidity-sensor-tooesp8266-thing-dev"></a><span data-ttu-id="3b32c-136">Conecte-se de um sensor de temperatura e umidade DHT22 tooESP8266 coisa desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="3b32c-136">Connect a DHT22 temperature and humidity sensor tooESP8266 Thing Dev</span></span>

<span data-ttu-id="3b32c-137">Use Olá breadboard e jumper fios toomake Olá conexão da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="3b32c-137">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="3b32c-138">Se você não tiver um sensor, ignore esta seção porque você pode usar dados de sensor simulado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="3b32c-138">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![referência de conexões](media/iot-hub-sparkfun-thing-dev-get-started/15_connections_on_breadboard.png)

<span data-ttu-id="3b32c-140">Pins de sensor, usaremos Olá fiação a seguir:</span><span class="sxs-lookup"><span data-stu-id="3b32c-140">For sensor pins, we will use hello following wiring:</span></span>

| <span data-ttu-id="3b32c-141">Início (Sensor)</span><span class="sxs-lookup"><span data-stu-id="3b32c-141">Start (Sensor)</span></span>           | <span data-ttu-id="3b32c-142">End (quadro)</span><span class="sxs-lookup"><span data-stu-id="3b32c-142">End (Board)</span></span>           | <span data-ttu-id="3b32c-143">Cor de cabo</span><span class="sxs-lookup"><span data-stu-id="3b32c-143">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="3b32c-144">VDD (Pin 27F)</span><span class="sxs-lookup"><span data-stu-id="3b32c-144">VDD (Pin 27F)</span></span>            | <span data-ttu-id="3b32c-145">3V (Pin 8A)</span><span class="sxs-lookup"><span data-stu-id="3b32c-145">3V (Pin 8A)</span></span>           | <span data-ttu-id="3b32c-146">Cabo vermelho</span><span class="sxs-lookup"><span data-stu-id="3b32c-146">Red cable</span></span>     |
| <span data-ttu-id="3b32c-147">DATA (Pin 28F)</span><span class="sxs-lookup"><span data-stu-id="3b32c-147">DATA (Pin 28F)</span></span>           | <span data-ttu-id="3b32c-148">GPIO 2 (Pin 9A)</span><span class="sxs-lookup"><span data-stu-id="3b32c-148">GPIO 2 (Pin 9A)</span></span>       | <span data-ttu-id="3b32c-149">Cabo branco</span><span class="sxs-lookup"><span data-stu-id="3b32c-149">White cable</span></span>    |
| <span data-ttu-id="3b32c-150">GND (Pin 30F)</span><span class="sxs-lookup"><span data-stu-id="3b32c-150">GND (Pin 30F)</span></span>            | <span data-ttu-id="3b32c-151">GND (Pin 7J)</span><span class="sxs-lookup"><span data-stu-id="3b32c-151">GND (Pin 7J)</span></span>          | <span data-ttu-id="3b32c-152">Cabo preto</span><span class="sxs-lookup"><span data-stu-id="3b32c-152">Black cable</span></span>   |


- <span data-ttu-id="3b32c-153">Para obter mais informações, consulte: [Instalação do sensor DHT22](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) e [Especificação da Sparkfun ESP8266 Thing Dev](https://www.sparkfun.com/products/13711)</span><span class="sxs-lookup"><span data-stu-id="3b32c-153">For more information, see: [DHT22 sensor setup](http://cdn.sparkfun.com/datasheets/Sensors/Weather/RHT03.pdf) and [Sparkfun ESP8266 Thing Dev specification](https://www.sparkfun.com/products/13711)</span></span>

<span data-ttu-id="3b32c-154">Agora sua Sparkfun ESP8266 Thing Dev deve estar conectada a um sensor ativo.</span><span class="sxs-lookup"><span data-stu-id="3b32c-154">Now your Sparkfun ESP8266 Thing Dev should be connected with a working sensor.</span></span>

![conectar o dht22 à ESP8266 Thing Dev](media/iot-hub-sparkfun-thing-dev-get-started/8_connect-dht22-thing-dev.png)

### <a name="connect-sparkfun-esp8266-thing-dev-tooyour-computer"></a><span data-ttu-id="3b32c-156">Conectar o computador de tooyour Sparkfun ESP8266 coisa desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="3b32c-156">Connect Sparkfun ESP8266 Thing Dev tooyour computer</span></span>

<span data-ttu-id="3b32c-157">Use Olá Micro USB tooType USB um cabo tooconnect Sparkfun ESP8266 coisa Dev tooyour computador da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="3b32c-157">Use hello Micro USB tooType A USB cable tooconnect Sparkfun ESP8266 Thing Dev tooyour computer as follows.</span></span>

![conectar difusão huzzah tooyour computador](media/iot-hub-sparkfun-thing-dev-get-started/9_connect-thing-dev-computer.png)

### <a name="add-serial-port-permissions--ubuntu-only"></a><span data-ttu-id="3b32c-159">Adicionar permissões de porta serial - somente Ubuntu</span><span class="sxs-lookup"><span data-stu-id="3b32c-159">Add serial port permissions – Ubuntu only</span></span>

<span data-ttu-id="3b32c-160">Se você usar Ubuntu, certifique-se de que um usuário normal tem Olá permissões toooperate em Olá USB porta de Sparkfun ESP8266 coisa propósitos de dispositivos</span><span class="sxs-lookup"><span data-stu-id="3b32c-160">If you use Ubuntu, make sure a normal user has hello permissions toooperate on hello USB port of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="3b32c-161">permissões de porta serial tooadd para um usuário normal, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3b32c-161">tooadd serial port permissions for a normal user, follow these steps:</span></span>

1. <span data-ttu-id="3b32c-162">Olá executar comandos em um terminal a seguir:</span><span class="sxs-lookup"><span data-stu-id="3b32c-162">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="3b32c-163">Você obtém uma saudação saídas a seguir:</span><span class="sxs-lookup"><span data-stu-id="3b32c-163">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="3b32c-164">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="3b32c-164">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="3b32c-165">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="3b32c-165">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="3b32c-166">Na saída de hello, observe `uucp` ou `dialout` que é Olá grupo nome do proprietário da saudação porta USB.</span><span class="sxs-lookup"><span data-stu-id="3b32c-166">In hello output, notice `uucp` or `dialout` that is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="3b32c-167">Adicione grupo de toohello de usuários de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3b32c-167">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="3b32c-168">`<group-owner-name>`é o nome de proprietário de grupo Olá que você obteve na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="3b32c-168">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="3b32c-169">`<username>` é o nome de usuário do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="3b32c-169">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="3b32c-170">Saia Ubuntu e entre nele novamente para Olá alterar tootake efeito.</span><span class="sxs-lookup"><span data-stu-id="3b32c-170">Log out Ubuntu and log in it again for hello change tootake effect.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="3b32c-171">Coletar dados de sensor e enviá-lo tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="3b32c-171">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="3b32c-172">Nesta seção, implante e execute um aplicativo de exemplo em Sparkfun ESP8266 Thing Dev.</span><span class="sxs-lookup"><span data-stu-id="3b32c-172">In this section, you deploy and run a sample application on Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="3b32c-173">aplicativo de exemplo Hello pisca Olá LED no desenvolvimento de coisa ESP8266 Sparkfun e envia a temperatura hello e umidade os dados coletados de saudação DHT22 sensor tooyour hub IoT.</span><span class="sxs-lookup"><span data-stu-id="3b32c-173">hello sample application blinks hello LED on Sparkfun ESP8266 Thing Dev and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="3b32c-174">Obter o aplicativo de exemplo hello do GitHub</span><span class="sxs-lookup"><span data-stu-id="3b32c-174">Get hello sample application from GitHub</span></span>

<span data-ttu-id="3b32c-175">aplicativo de exemplo Hello está hospedado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="3b32c-175">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="3b32c-176">Clone o repositório de exemplo hello que contém o aplicativo de exemplo de saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="3b32c-176">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="3b32c-177">repositório de exemplo hello tooclone, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3b32c-177">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="3b32c-178">Abra um prompt de comando ou uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="3b32c-178">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="3b32c-179">Vá tooa pasta onde você deseja toobe de aplicativo de exemplo hello armazenado.</span><span class="sxs-lookup"><span data-stu-id="3b32c-179">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="3b32c-180">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3b32c-180">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-SparkFun-ThingDev-client-app.git
   ```

<span data-ttu-id="3b32c-181">Instale o pacote de saudação para Sparkfun ESP8266 coisa Dev no Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="3b32c-181">Install hello package for Sparkfun ESP8266 Thing Dev in Arduino IDE:</span></span>

1. <span data-ttu-id="3b32c-182">Abra a pasta de saudação onde o aplicativo de exemplo hello está armazenado.</span><span class="sxs-lookup"><span data-stu-id="3b32c-182">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="3b32c-183">Abra o arquivo de app.ino de saudação na pasta do aplicativo hello Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="3b32c-183">Open hello app.ino file in hello app folder in Arduino IDE.</span></span>

   ![Abra o aplicativo de exemplo hello no ide arduino](media/iot-hub-sparkfun-thing-dev-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="3b32c-185">No hello Arduino IDE, clique em **arquivo** > **preferências**.</span><span class="sxs-lookup"><span data-stu-id="3b32c-185">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="3b32c-186">Em Olá **preferências** caixa de diálogo, clique em Olá ícone próximo toohello **URLs adicionais do Gerenciador de quadros** caixa de texto.</span><span class="sxs-lookup"><span data-stu-id="3b32c-186">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** text box.</span></span>
1. <span data-ttu-id="3b32c-187">Na janela pop-up do hello, digite Olá URL a seguir e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="3b32c-187">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![url do pacote de ponto tooa arduino IDE](media/iot-hub-sparkfun-thing-dev-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="3b32c-189">Em Olá **preferência** caixa de diálogo, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="3b32c-189">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="3b32c-190">Clique em **Ferramentas** > **Placa** > **Gerenciador de Placas** e procure esp8266.</span><span class="sxs-lookup"><span data-stu-id="3b32c-190">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>
   <span data-ttu-id="3b32c-191">ESP8266 com uma versão 2.2.0 ou posterior deve ser instalado.</span><span class="sxs-lookup"><span data-stu-id="3b32c-191">ESP8266 with a version of 2.2.0 or later should be installed.</span></span>

   ![Olá esp8266 pacote está instalado](media/iot-hub-sparkfun-thing-dev-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="3b32c-193">Clique em **Ferramentas** > **Painel** > **Sparkfun ESP8266 Thing Dev**.</span><span class="sxs-lookup"><span data-stu-id="3b32c-193">Click **Tools** > **Board** > **Sparkfun ESP8266 Thing Dev**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="3b32c-194">Instalar as bibliotecas necessárias</span><span class="sxs-lookup"><span data-stu-id="3b32c-194">Install necessary libraries</span></span>

1. <span data-ttu-id="3b32c-195">No hello Arduino IDE, clique em **esboço** > **biblioteca incluem** > **gerenciar bibliotecas**.</span><span class="sxs-lookup"><span data-stu-id="3b32c-195">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="3b32c-196">Pesquisar Olá uma nomes de bibliotecas a seguir.</span><span class="sxs-lookup"><span data-stu-id="3b32c-196">Search for hello following library names one by one.</span></span> <span data-ttu-id="3b32c-197">Para cada biblioteca Olá você localizar, clique em **instalar**.</span><span class="sxs-lookup"><span data-stu-id="3b32c-197">For each of hello library you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="3b32c-198">Você não tem um sensor DHT22 real?</span><span class="sxs-lookup"><span data-stu-id="3b32c-198">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="3b32c-199">aplicativo de exemplo Hello pode simular a temperatura e umidade dados caso você não tenha um sensor DHT22 real.</span><span class="sxs-lookup"><span data-stu-id="3b32c-199">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="3b32c-200">dados de toouse simulada do aplicativo de exemplo de hello tooenable, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3b32c-200">tooenable hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="3b32c-201">Olá abrir `config.h` arquivo hello `app` pasta.</span><span class="sxs-lookup"><span data-stu-id="3b32c-201">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="3b32c-202">Localize Olá a seguinte linha de código e altere o valor de saudação de `false` muito`true`:</span><span class="sxs-lookup"><span data-stu-id="3b32c-202">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar dados de toouse simulada de aplicativo de exemplo hello](media/iot-hub-sparkfun-thing-dev-get-started/13_arduino-ide-configure-app-use-simulated-data.png)
   
1. <span data-ttu-id="3b32c-204">Salvar com `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="3b32c-204">Save with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toosparkfun-esp8266-thing-dev"></a><span data-ttu-id="3b32c-205">Implantar tooSparkfun de aplicativo de exemplo hello ESP8266 coisa desenvolvimento</span><span class="sxs-lookup"><span data-stu-id="3b32c-205">Deploy hello sample application tooSparkfun ESP8266 Thing Dev</span></span>

1. <span data-ttu-id="3b32c-206">No hello Arduino IDE, clique em **ferramenta** > **porta**e, em seguida, clique em porta serial Olá para propósitos de dispositivos Sparkfun ESP8266 coisa</span><span class="sxs-lookup"><span data-stu-id="3b32c-206">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Sparkfun ESP8266 Thing Dev.</span></span>
1. <span data-ttu-id="3b32c-207">Clique em **esboço** > **carregar** toobuild e implantar tooSparkfun de aplicativo de exemplo hello propósitos de dispositivos ESP8266 coisa</span><span class="sxs-lookup"><span data-stu-id="3b32c-207">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooSparkfun ESP8266 Thing Dev.</span></span>

> [!Note]
> <span data-ttu-id="3b32c-208">Se você estiver usando macOS provavelmente você pode ver Olá mensagens a seguir durante o carregamento.</span><span class="sxs-lookup"><span data-stu-id="3b32c-208">If you are using macOS you could probably see hello following messages during uploading.</span></span> <span data-ttu-id="3b32c-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span><span class="sxs-lookup"><span data-stu-id="3b32c-209">`warning: espcomm_sync failed`,`error: espcomm_open failed`.</span></span> <span data-ttu-id="3b32c-210">Abra a janela ternimal e concluir abaixo ações toosolve esse problema.</span><span class="sxs-lookup"><span data-stu-id="3b32c-210">Please open your ternimal window and finish below actions toosolve this issue.</span></span>
> ```bash
> cd /System/Library/Extensions/IOUSBFamily.kext/Contents/PlugIns
> sudo mv AppleUSBFTDI.kext AppleUSBFTDI.disabled
> sudo touch /System/Library/Extensions
> ```

### <a name="enter-your-credentials"></a><span data-ttu-id="3b32c-211">Inserir suas credenciais</span><span class="sxs-lookup"><span data-stu-id="3b32c-211">Enter your credentials</span></span>

<span data-ttu-id="3b32c-212">Olá após o carregamento for concluído com êxito, execute Olá etapas tooenter suas credenciais:</span><span class="sxs-lookup"><span data-stu-id="3b32c-212">After hello upload completes successfully, follow hello steps tooenter your credentials:</span></span>

1. <span data-ttu-id="3b32c-213">No hello Arduino IDE, clique em **ferramentas** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="3b32c-213">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="3b32c-214">Na janela do monitor serial hello, observe Olá dois nas listas suspensas no hello canto inferior direito.</span><span class="sxs-lookup"><span data-stu-id="3b32c-214">In hello serial monitor window, notice hello two drop-down lists on hello bottom right corner.</span></span>
1. <span data-ttu-id="3b32c-215">Selecione **nenhuma final de linha** para a lista suspensa da esquerda hello.</span><span class="sxs-lookup"><span data-stu-id="3b32c-215">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="3b32c-216">Selecione **115200 baud** para a lista suspensa à direita de saudação.</span><span class="sxs-lookup"><span data-stu-id="3b32c-216">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="3b32c-217">Na caixa de entrada hello localizada na parte superior de saudação da janela do monitor serial hello, digite Olá informações a seguir se você for solicitado tooprovide-los e, em seguida, clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="3b32c-217">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="3b32c-218">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="3b32c-218">Wi-Fi SSID</span></span>
   * <span data-ttu-id="3b32c-219">Senha de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="3b32c-219">Wi-Fi password</span></span>
   * <span data-ttu-id="3b32c-220">Cadeia de conexão de dispositivo</span><span class="sxs-lookup"><span data-stu-id="3b32c-220">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="3b32c-221">Olá credenciais são armazenadas no hello EEPROM de Sparkfun ESP8266 coisa propósitos de dispositivos</span><span class="sxs-lookup"><span data-stu-id="3b32c-221">hello credential information is stored in hello EEPROM of Sparkfun ESP8266 Thing Dev.</span></span> <span data-ttu-id="3b32c-222">Se você clicar em um botão redefinição Olá Olá placa Sparkfun ESP8266 coisa Dev, aplicativo de exemplo hello pergunta se você deseja informações de saudação do tooerase.</span><span class="sxs-lookup"><span data-stu-id="3b32c-222">If you click hello reset button on hello Sparkfun ESP8266 Thing Dev board, hello sample application asks you if you want tooerase hello information.</span></span> <span data-ttu-id="3b32c-223">Digite `Y` toohave informações de saudação apagados e você será solicitado tooprovide informações de saudação novamente.</span><span class="sxs-lookup"><span data-stu-id="3b32c-223">Enter `Y` toohave hello information erased and you are asked tooprovide hello information again.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="3b32c-224">Verifique se o aplicativo de exemplo hello é executado com êxito</span><span class="sxs-lookup"><span data-stu-id="3b32c-224">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="3b32c-225">Se você vir seguinte Olá saída da janela do monitor serial hello e Olá piscando LED no desenvolvimento de coisa ESP8266 Sparkfun, o aplicativo de exemplo hello está em execução com êxito.</span><span class="sxs-lookup"><span data-stu-id="3b32c-225">If you see hello following output from hello serial monitor window and hello blinking LED on Sparkfun ESP8266 Thing Dev, hello sample application is running successfully.</span></span>

![saída final no ide arduino](media/iot-hub-sparkfun-thing-dev-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="3b32c-227">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3b32c-227">Next steps</span></span>

<span data-ttu-id="3b32c-228">Você conectado a um hub de IoT tooyour Sparkfun ESP8266 coisa desenvolvimento e enviados Olá capturado sensor dados tooyour IoT hub com êxito.</span><span class="sxs-lookup"><span data-stu-id="3b32c-228">You have successfully connected a Sparkfun ESP8266 Thing Dev tooyour IoT hub and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
