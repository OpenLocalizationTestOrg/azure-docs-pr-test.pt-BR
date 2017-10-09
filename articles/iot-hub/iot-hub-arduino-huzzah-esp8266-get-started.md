---
title: "aaaESP8266 toocloud - conectar o difusão HUZZAH ESP8266 tooAzure IoT Hub | Microsoft Docs"
description: "Saiba como toosetup e conecte-se Adafruit difusão HUZZAH ESP8266 tooAzure IoT Hub para ele plataforma de nuvem do Azure toosend dados toohello neste tutorial."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: 
ms.assetid: c505aacf-89a8-40ed-a853-493b75bec524
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/15/2017
ms.author: xshi
ms.openlocfilehash: 44fd47232488948d21c7aa71bdd865397e41e63e
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-tooazure-iot-hub-in-hello-cloud"></a><span data-ttu-id="e30b7-103">Conecte-se Adafruit difusão HUZZAH ESP8266 tooAzure IoT Hub na nuvem Olá</span><span class="sxs-lookup"><span data-stu-id="e30b7-103">Connect Adafruit Feather HUZZAH ESP8266 tooAzure IoT Hub in hello cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexão entre o DHT22, o Feather HUZZAH ESP8266 e o Hub IoT](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="e30b7-105">O que fazer</span><span class="sxs-lookup"><span data-stu-id="e30b7-105">What you do</span></span>


<span data-ttu-id="e30b7-106">Conecte-se Adafruit difusão HUZZAH ESP8266 tooan IoT hub que você criar.</span><span class="sxs-lookup"><span data-stu-id="e30b7-106">Connect Adafruit Feather HUZZAH ESP8266 tooan IoT hub that you create.</span></span> <span data-ttu-id="e30b7-107">Em seguida, execute um aplicativo de exemplo no ESP8266 toocollect Olá temperatura e umidade os dados de um sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="e30b7-107">Then you run a sample application on ESP8266 toocollect hello temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="e30b7-108">Por fim, você pode enviar hub IoT do hello sensor dados tooyour.</span><span class="sxs-lookup"><span data-stu-id="e30b7-108">Finally, you send hello sensor data tooyour IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="e30b7-109">Se você estiver usando outras placas ESP8266, você ainda pode seguir estas etapas tooconnect-tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e30b7-109">If you're using other ESP8266 boards, you can still follow these steps tooconnect it tooyour IoT hub.</span></span> <span data-ttu-id="e30b7-110">Dependendo da placa Olá ESP8266 você está usando, talvez seja necessário Olá tooreconfigure `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="e30b7-110">Depending on hello ESP8266 board you're using, you might need tooreconfigure hello `LED_PIN`.</span></span> <span data-ttu-id="e30b7-111">Por exemplo, se você estiver usando ESP8266 do AI Thinker, você pode alterá-la de `0` muito`2`.</span><span class="sxs-lookup"><span data-stu-id="e30b7-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` too`2`.</span></span> <span data-ttu-id="e30b7-112">Não tem um dispositivo ainda?</span><span class="sxs-lookup"><span data-stu-id="e30b7-112">Don't have a kit yet?</span></span> <span data-ttu-id="e30b7-113">Obtê-lo do hello [site do Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="e30b7-113">Get it from hello [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="e30b7-114">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="e30b7-114">What you learn</span></span>

* <span data-ttu-id="e30b7-115">Como toocreate um hub IoT e registrar um dispositivo para difusão HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="e30b7-115">How toocreate an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="e30b7-116">Como tooconnect difusão HUZZAH ESP8266 com sensor hello e seu computador</span><span class="sxs-lookup"><span data-stu-id="e30b7-116">How tooconnect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
* <span data-ttu-id="e30b7-117">Como os dados do sensor toocollect executando um aplicativo de exemplo em difusão HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="e30b7-117">How toocollect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="e30b7-118">Como toosend Olá hub IoT do sensor dados tooyour</span><span class="sxs-lookup"><span data-stu-id="e30b7-118">How toosend hello sensor data tooyour IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="e30b7-119">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="e30b7-119">What you need</span></span>

![Partes necessárias para o tutorial Olá](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="e30b7-121">toocomplete essa operação, você precisa Olá seguir partes de seu difusão HUZZAH ESP8266 Starter Kit:</span><span class="sxs-lookup"><span data-stu-id="e30b7-121">toocomplete this operation, you need hello following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="e30b7-122">Olá difusão HUZZAH ESP8266 board</span><span class="sxs-lookup"><span data-stu-id="e30b7-122">hello Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="e30b7-123">Um tooType Micro USB um cabo</span><span class="sxs-lookup"><span data-stu-id="e30b7-123">A Micro USB tooType A USB cable</span></span>

<span data-ttu-id="e30b7-124">Você também precisa Olá coisas para seu ambiente de desenvolvimento a seguir:</span><span class="sxs-lookup"><span data-stu-id="e30b7-124">You also need hello following things for your development environment:</span></span>

* <span data-ttu-id="e30b7-125">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="e30b7-125">An active Azure subscription.</span></span> <span data-ttu-id="e30b7-126">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="e30b7-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="e30b7-127">Mac ou PC que esteja executando o Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e30b7-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="e30b7-128">Rede sem fio para difusão HUZZAH ESP8266 tooconnect para.</span><span class="sxs-lookup"><span data-stu-id="e30b7-128">Wireless network for Feather HUZZAH ESP8266 tooconnect to.</span></span>
* <span data-ttu-id="e30b7-129">Ferramenta de configuração saudação do toodownload de conexão de Internet.</span><span class="sxs-lookup"><span data-stu-id="e30b7-129">Internet connection toodownload hello configuration tool.</span></span>
* <span data-ttu-id="e30b7-130">[IDE do Arduino](https://www.arduino.cc/en/main/software) versão 1.6.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="e30b7-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="e30b7-131">Versões anteriores não funcionam com a biblioteca de AzureIoT hello.</span><span class="sxs-lookup"><span data-stu-id="e30b7-131">Earlier versions don't work with hello AzureIoT library.</span></span>

<span data-ttu-id="e30b7-132">Olá itens a seguir são opcionais no caso de você não tiver um sensor.</span><span class="sxs-lookup"><span data-stu-id="e30b7-132">hello following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="e30b7-133">Você também tem a opção de saudação do uso de dados de sensor simulada.</span><span class="sxs-lookup"><span data-stu-id="e30b7-133">You also have hello option of using simulated sensor data.</span></span>

* <span data-ttu-id="e30b7-134">Um sensor de temperatura e umidade Adafruit DHT22</span><span class="sxs-lookup"><span data-stu-id="e30b7-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="e30b7-135">Uma placa universal</span><span class="sxs-lookup"><span data-stu-id="e30b7-135">A breadboard</span></span>
* <span data-ttu-id="e30b7-136">Cabos de jumper de M/M</span><span class="sxs-lookup"><span data-stu-id="e30b7-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-hello-sensor-and-your-computer"></a><span data-ttu-id="e30b7-137">Conecte-se a difusão HUZZAH ESP8266 com sensor hello e seu computador</span><span class="sxs-lookup"><span data-stu-id="e30b7-137">Connect Feather HUZZAH ESP8266 with hello sensor and your computer</span></span>
<span data-ttu-id="e30b7-138">Nesta seção, você se conectar a placa de tooyour sensores hello.</span><span class="sxs-lookup"><span data-stu-id="e30b7-138">In this section, you connect hello sensors tooyour board.</span></span> <span data-ttu-id="e30b7-139">Em seguida, você conecta o computador tooyour de dispositivo para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="e30b7-139">Then you plug in your device tooyour computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-toofeather-huzzah-esp8266"></a><span data-ttu-id="e30b7-140">Conecte-se um DHT22 temperatura e umidade sensor tooFeather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="e30b7-140">Connect a DHT22 temperature and humidity sensor tooFeather HUZZAH ESP8266</span></span>

<span data-ttu-id="e30b7-141">Use Olá breadboard e jumper fios toomake Olá conexão da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="e30b7-141">Use hello breadboard and jumper wires toomake hello connection as follows.</span></span> <span data-ttu-id="e30b7-142">Se você não tiver um sensor, ignore esta seção porque você pode usar dados de sensor simulado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="e30b7-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Referência de conexões](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="e30b7-144">Pinos do sensor, use Olá fiação a seguir:</span><span class="sxs-lookup"><span data-stu-id="e30b7-144">For sensor pins, use hello following wiring:</span></span>


| <span data-ttu-id="e30b7-145">Início (Sensor)</span><span class="sxs-lookup"><span data-stu-id="e30b7-145">Start (Sensor)</span></span>           | <span data-ttu-id="e30b7-146">End (quadro)</span><span class="sxs-lookup"><span data-stu-id="e30b7-146">End (Board)</span></span>           | <span data-ttu-id="e30b7-147">Cor de cabo</span><span class="sxs-lookup"><span data-stu-id="e30b7-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="e30b7-148">VDD (Pin 31F)</span><span class="sxs-lookup"><span data-stu-id="e30b7-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="e30b7-149">3V (Fixar 58H)</span><span class="sxs-lookup"><span data-stu-id="e30b7-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="e30b7-150">Cabo vermelho</span><span class="sxs-lookup"><span data-stu-id="e30b7-150">Red cable</span></span>     |
| <span data-ttu-id="e30b7-151">DADOS de (Pin 32F)</span><span class="sxs-lookup"><span data-stu-id="e30b7-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="e30b7-152">GPIO 2 (Pin 46A)</span><span class="sxs-lookup"><span data-stu-id="e30b7-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="e30b7-153">Cabo azul</span><span class="sxs-lookup"><span data-stu-id="e30b7-153">Blue cable</span></span>    |
| <span data-ttu-id="e30b7-154">GND (Pin 34F)</span><span class="sxs-lookup"><span data-stu-id="e30b7-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="e30b7-155">GND (PIn 56I)</span><span class="sxs-lookup"><span data-stu-id="e30b7-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="e30b7-156">Cabo preto</span><span class="sxs-lookup"><span data-stu-id="e30b7-156">Black cable</span></span>   |

<span data-ttu-id="e30b7-157">Para obter mais informações, consulte [Instalação do sensor Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) e [Pinagem do Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="e30b7-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="e30b7-158">Agora seu Feather Huzzah ESP8266 deve estar conectado a um sensor ativo.</span><span class="sxs-lookup"><span data-stu-id="e30b7-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Conectar o DHT22 ao Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-tooyour-computer"></a><span data-ttu-id="e30b7-160">Conectar difusão HUZZAH ESP8266 tooyour computador</span><span class="sxs-lookup"><span data-stu-id="e30b7-160">Connect Feather HUZZAH ESP8266 tooyour computer</span></span>

<span data-ttu-id="e30b7-161">Como mostrado a seguir, use Olá Micro USB tooType USB um cabo tooconnect difusão HUZZAH ESP8266 tooyour computador.</span><span class="sxs-lookup"><span data-stu-id="e30b7-161">As shown next, use hello Micro USB tooType A USB cable tooconnect Feather HUZZAH ESP8266 tooyour computer.</span></span>

![Conectar o computador de tooyour Huzzah de difusão](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="e30b7-163">Adicionar permissões de porta serial (somente Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="e30b7-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="e30b7-164">Se você usar Ubuntu, verifique se que você tem Olá permissões toooperate em Olá USB porta da difusão HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="e30b7-164">If you use Ubuntu, make sure you have hello permissions toooperate on hello USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="e30b7-165">permissões de porta serial tooadd, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e30b7-165">tooadd serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="e30b7-166">Olá executar comandos em um terminal a seguir:</span><span class="sxs-lookup"><span data-stu-id="e30b7-166">Run hello following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="e30b7-167">Você obtém uma saudação saídas a seguir:</span><span class="sxs-lookup"><span data-stu-id="e30b7-167">You get one of hello following outputs:</span></span>

   * <span data-ttu-id="e30b7-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="e30b7-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="e30b7-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="e30b7-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="e30b7-170">Na saída de hello, observe que `uucp` ou `dialout` é o nome de proprietário do grupo de saudação do hello porta USB.</span><span class="sxs-lookup"><span data-stu-id="e30b7-170">In hello output, notice that `uucp` or `dialout` is hello group owner name of hello USB port.</span></span>

1. <span data-ttu-id="e30b7-171">Adicione grupo de toohello de usuários de saudação executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e30b7-171">Add hello user toohello group by running hello following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="e30b7-172">`<group-owner-name>`é o nome de proprietário de grupo Olá que você obteve na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="e30b7-172">`<group-owner-name>` is hello group owner name you obtained in hello previous step.</span></span> <span data-ttu-id="e30b7-173">`<username>` é o nome de usuário do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="e30b7-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="e30b7-174">Saia do Ubuntu e entrar novamente para Olá tooappear de alteração.</span><span class="sxs-lookup"><span data-stu-id="e30b7-174">Sign out of Ubuntu, and then sign in again for hello change tooappear.</span></span>

## <a name="collect-sensor-data-and-send-it-tooyour-iot-hub"></a><span data-ttu-id="e30b7-175">Coletar dados de sensor e enviá-lo tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="e30b7-175">Collect sensor data and send it tooyour IoT hub</span></span>

<span data-ttu-id="e30b7-176">Nesta seção, implante e execute um aplicativo de exemplo em Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="e30b7-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="e30b7-177">aplicativo de exemplo Hello pisca Olá LED em difusão HUZZAH ESP8266 e envia a temperatura hello e umidade os dados coletados de saudação DHT22 sensor tooyour hub IoT.</span><span class="sxs-lookup"><span data-stu-id="e30b7-177">hello sample application blinks hello LED on Feather HUZZAH ESP8266, and sends hello temperature and humidity data collected from hello DHT22 sensor tooyour IoT hub.</span></span>

### <a name="get-hello-sample-application-from-github"></a><span data-ttu-id="e30b7-178">Obter o aplicativo de exemplo hello do GitHub</span><span class="sxs-lookup"><span data-stu-id="e30b7-178">Get hello sample application from GitHub</span></span>

<span data-ttu-id="e30b7-179">aplicativo de exemplo Hello está hospedado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="e30b7-179">hello sample application is hosted on GitHub.</span></span> <span data-ttu-id="e30b7-180">Clone o repositório de exemplo hello que contém o aplicativo de exemplo de saudação do GitHub.</span><span class="sxs-lookup"><span data-stu-id="e30b7-180">Clone hello sample repository that contains hello sample application from GitHub.</span></span> <span data-ttu-id="e30b7-181">repositório de exemplo hello tooclone, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e30b7-181">tooclone hello sample repository, follow these steps:</span></span>

1. <span data-ttu-id="e30b7-182">Abra um prompt de comando ou uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="e30b7-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="e30b7-183">Vá tooa pasta onde você deseja toobe de aplicativo de exemplo hello armazenado.</span><span class="sxs-lookup"><span data-stu-id="e30b7-183">Go tooa folder where you want hello sample application toobe stored.</span></span>
1. <span data-ttu-id="e30b7-184">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="e30b7-184">Run hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="e30b7-185">Instale o pacote de saudação para difusão HUZZAH ESP8266 em Olá Arduino IDE:</span><span class="sxs-lookup"><span data-stu-id="e30b7-185">Install hello package for Feather HUZZAH ESP8266 in hello Arduino IDE:</span></span>

1. <span data-ttu-id="e30b7-186">Abra a pasta de saudação onde o aplicativo de exemplo hello está armazenado.</span><span class="sxs-lookup"><span data-stu-id="e30b7-186">Open hello folder where hello sample application is stored.</span></span>
1. <span data-ttu-id="e30b7-187">Abra o arquivo de app.ino de saudação na pasta de aplicativo Olá Olá Arduino IDE.</span><span class="sxs-lookup"><span data-stu-id="e30b7-187">Open hello app.ino file in hello app folder in hello Arduino IDE.</span></span>

   ![Abra o aplicativo de exemplo hello Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="e30b7-189">No hello Arduino IDE, clique em **arquivo** > **preferências**.</span><span class="sxs-lookup"><span data-stu-id="e30b7-189">In hello Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="e30b7-190">Em Olá **preferências** caixa de diálogo, clique em Olá ícone próximo toohello **URLs adicionais do Gerenciador de quadros** caixa.</span><span class="sxs-lookup"><span data-stu-id="e30b7-190">In hello **Preferences** dialog box, click hello icon next toohello **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="e30b7-191">Na janela pop-up do hello, digite Olá URL a seguir e, em seguida, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="e30b7-191">In hello pop-up window, enter hello following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Url do pacote de ponto tooa Arduino IDE](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="e30b7-193">Em Olá **preferência** caixa de diálogo, clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="e30b7-193">In hello **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="e30b7-194">Clique em **Ferramentas** > **Placa** > **Gerenciador de Placas** e procure esp8266.</span><span class="sxs-lookup"><span data-stu-id="e30b7-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="e30b7-195">O Gerenciador de Placas indica que ESP8266 com uma versão 2.2.0 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="e30b7-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![Olá esp8266 pacote está instalado](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="e30b7-197">Clique em **ferramentas** > **placa** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="e30b7-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="e30b7-198">Instalar as bibliotecas necessárias</span><span class="sxs-lookup"><span data-stu-id="e30b7-198">Install necessary libraries</span></span>

1. <span data-ttu-id="e30b7-199">No hello Arduino IDE, clique em **esboço** > **biblioteca incluem** > **gerenciar bibliotecas**.</span><span class="sxs-lookup"><span data-stu-id="e30b7-199">In hello Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="e30b7-200">Pesquisar Olá uma nomes de bibliotecas a seguir.</span><span class="sxs-lookup"><span data-stu-id="e30b7-200">Search for hello following library names one by one.</span></span> <span data-ttu-id="e30b7-201">Para cada biblioteca que você localizar, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="e30b7-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="e30b7-202">Você não tem um sensor DHT22 real?</span><span class="sxs-lookup"><span data-stu-id="e30b7-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="e30b7-203">aplicativo de exemplo Hello pode simular a temperatura e umidade dados caso você não tenha um sensor DHT22 real.</span><span class="sxs-lookup"><span data-stu-id="e30b7-203">hello sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="e30b7-204">tooset backup de dados de toouse simulada de aplicativo de exemplo hello, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="e30b7-204">tooset up hello sample application toouse simulated data, follow these steps:</span></span>

1. <span data-ttu-id="e30b7-205">Olá abrir `config.h` arquivo hello `app` pasta.</span><span class="sxs-lookup"><span data-stu-id="e30b7-205">Open hello `config.h` file in hello `app` folder.</span></span>
1. <span data-ttu-id="e30b7-206">Localize Olá a seguinte linha de código e altere o valor de saudação de `false` muito`true`:</span><span class="sxs-lookup"><span data-stu-id="e30b7-206">Locate hello following line of code and change hello value from `false` too`true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar dados de toouse simulada de aplicativo de exemplo hello](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="e30b7-208">Salve o arquivo hello com `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="e30b7-208">Save hello file with `Control-s`.</span></span>

### <a name="deploy-hello-sample-application-toofeather-huzzah-esp8266"></a><span data-ttu-id="e30b7-209">Implantar tooFeather de aplicativo de exemplo hello HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="e30b7-209">Deploy hello sample application tooFeather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="e30b7-210">No hello Arduino IDE, clique em **ferramenta** > **porta**e, em seguida, clique em porta serial Olá para difusão HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="e30b7-210">In hello Arduino IDE, click **Tool** > **Port**, and then click hello serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="e30b7-211">Clique em **esboço** > **carregar** toobuild e implantar tooFeather de aplicativo de exemplo hello HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="e30b7-211">Click **Sketch** > **Upload** toobuild and deploy hello sample application tooFeather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="e30b7-212">Inserir suas credenciais</span><span class="sxs-lookup"><span data-stu-id="e30b7-212">Enter your credentials</span></span>

<span data-ttu-id="e30b7-213">Olá após o carregamento for concluído com êxito, siga estas etapas tooenter suas credenciais:</span><span class="sxs-lookup"><span data-stu-id="e30b7-213">After hello upload completes successfully, follow these steps tooenter your credentials:</span></span>

1. <span data-ttu-id="e30b7-214">No hello Arduino IDE, clique em **ferramentas** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="e30b7-214">In hello Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="e30b7-215">Na janela do monitor serial hello, observe Olá dois nas listas suspensas no canto inferior direito de saudação.</span><span class="sxs-lookup"><span data-stu-id="e30b7-215">In hello serial monitor window, notice hello two drop-down lists in hello lower-right corner.</span></span>
1. <span data-ttu-id="e30b7-216">Selecione **nenhuma final de linha** para a lista suspensa da esquerda hello.</span><span class="sxs-lookup"><span data-stu-id="e30b7-216">Select **No line ending** for hello left drop-down list.</span></span>
1. <span data-ttu-id="e30b7-217">Selecione **115200 baud** para a lista suspensa à direita de saudação.</span><span class="sxs-lookup"><span data-stu-id="e30b7-217">Select **115200 baud** for hello right drop-down list.</span></span>
1. <span data-ttu-id="e30b7-218">Na caixa de entrada hello localizada na parte superior de saudação da janela do monitor serial hello, digite Olá informações a seguir se você for solicitado tooprovide-los e, em seguida, clique em **enviar**.</span><span class="sxs-lookup"><span data-stu-id="e30b7-218">In hello input box located at hello top of hello serial monitor window, enter hello following information if you are asked tooprovide them, and then click **Send**.</span></span>
   * <span data-ttu-id="e30b7-219">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="e30b7-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="e30b7-220">Senha de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="e30b7-220">Wi-Fi password</span></span>
   * <span data-ttu-id="e30b7-221">Cadeia de conexão de dispositivo</span><span class="sxs-lookup"><span data-stu-id="e30b7-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="e30b7-222">Olá credenciais são armazenadas no hello EEPROM de difusão HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="e30b7-222">hello credential information is stored in hello EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="e30b7-223">Se você clicar em um botão Redefinir Olá Olá difusão HUZZAH ESP8266 board, aplicativo de exemplo hello pergunta se você deseja informações de saudação do tooerase.</span><span class="sxs-lookup"><span data-stu-id="e30b7-223">If you click hello reset button on hello Feather HUZZAH ESP8266 board, hello sample application asks if you want tooerase hello information.</span></span> <span data-ttu-id="e30b7-224">Digite `Y` toohave informações de saudação apagadas.</span><span class="sxs-lookup"><span data-stu-id="e30b7-224">Enter `Y` toohave hello information erased.</span></span> <span data-ttu-id="e30b7-225">Você será solicitado a informações de saudação tooprovide uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="e30b7-225">You are asked tooprovide hello information a second time.</span></span>

### <a name="verify-hello-sample-application-is-running-successfully"></a><span data-ttu-id="e30b7-226">Verifique se o aplicativo de exemplo hello é executado com êxito</span><span class="sxs-lookup"><span data-stu-id="e30b7-226">Verify hello sample application is running successfully</span></span>

<span data-ttu-id="e30b7-227">Se você vir seguinte Olá saída da janela do monitor serial hello e Olá piscando LED em difusão HUZZAH ESP8266, o aplicativo de exemplo hello está em execução com êxito.</span><span class="sxs-lookup"><span data-stu-id="e30b7-227">If you see hello following output from hello serial monitor window and hello blinking LED on Feather HUZZAH ESP8266, hello sample application is running successfully.</span></span>

![Saída final no IDE do Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="e30b7-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e30b7-229">Next steps</span></span>

<span data-ttu-id="e30b7-230">E com sucesso conectado a um hub de IoT difusão HUZZAH ESP8266 tooyour, enviado Olá capturado sensor dados tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="e30b7-230">You have successfully connected a Feather HUZZAH ESP8266 tooyour IoT hub, and sent hello captured sensor data tooyour IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

