---
title: ESP8266 para a nuvem - Conectar o Feather HUZZAH ESP8266 ao Hub IoT do Azure | Microsoft Docs
description: Saiba como configurar e conectar Adafruit Feather HUZZAH ESP8266 para Hub IoT do Azure para ele para enviar dados para a plataforma de nuvem do Azure neste tutorial.
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
ms.openlocfilehash: 6a450579c848fe6030a328ddf410f139baae2324
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="connect-adafruit-feather-huzzah-esp8266-to-azure-iot-hub-in-the-cloud"></a><span data-ttu-id="ab834-103">Conectar-se o Adafruit Feather HUZZAH ESP8266 ao Hub IoT do Azure na nuvem</span><span class="sxs-lookup"><span data-stu-id="ab834-103">Connect Adafruit Feather HUZZAH ESP8266 to Azure IoT Hub in the cloud</span></span>

[!INCLUDE [iot-hub-get-started-device-selector](../../includes/iot-hub-get-started-device-selector.md)]

![Conexão entre o DHT22, o Feather HUZZAH ESP8266 e o Hub IoT](media/iot-hub-arduino-huzzah-esp8266-get-started/1_connection-hdt22-feather-huzzah-iot-hub.png)

## <a name="what-you-do"></a><span data-ttu-id="ab834-105">O que fazer</span><span class="sxs-lookup"><span data-stu-id="ab834-105">What you do</span></span>


<span data-ttu-id="ab834-106">Conecte o Adafruit Feather HUZZAH ESP8266 a um Hub IoT criado.</span><span class="sxs-lookup"><span data-stu-id="ab834-106">Connect Adafruit Feather HUZZAH ESP8266 to an IoT hub that you create.</span></span> <span data-ttu-id="ab834-107">Em seguida, você executa um aplicativo de exemplo no ESP8266 para coletar os dados de temperatura e de umidade de um sensor DHT22.</span><span class="sxs-lookup"><span data-stu-id="ab834-107">Then you run a sample application on ESP8266 to collect the temperature and humidity data from a DHT22 sensor.</span></span> <span data-ttu-id="ab834-108">Por fim, você envia os dados do sensor para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ab834-108">Finally, you send the sensor data to your IoT hub.</span></span>

> [!NOTE]
> <span data-ttu-id="ab834-109">Se você estiver usando outras placas ESP8266, ainda poderá seguir estas etapas para conectá-las ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ab834-109">If you're using other ESP8266 boards, you can still follow these steps to connect it to your IoT hub.</span></span> <span data-ttu-id="ab834-110">Dependendo da placa ESP8266 utilizada, talvez seja necessário reconfigurar o `LED_PIN`.</span><span class="sxs-lookup"><span data-stu-id="ab834-110">Depending on the ESP8266 board you're using, you might need to reconfigure the `LED_PIN`.</span></span> <span data-ttu-id="ab834-111">Por exemplo, se você estiver usando ESP8266 da AI-Thinker, poderá alterá-la de `0` para `2`.</span><span class="sxs-lookup"><span data-stu-id="ab834-111">For example, if you're using ESP8266 from AI-Thinker, you might change it from `0` to `2`.</span></span> <span data-ttu-id="ab834-112">Não tem um dispositivo ainda?</span><span class="sxs-lookup"><span data-stu-id="ab834-112">Don't have a kit yet?</span></span> <span data-ttu-id="ab834-113">Obtenha-o no [site do Azure](http://azure.com/iotstarterkits).</span><span class="sxs-lookup"><span data-stu-id="ab834-113">Get it from the [Azure website](http://azure.com/iotstarterkits).</span></span>




## <a name="what-you-learn"></a><span data-ttu-id="ab834-114">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="ab834-114">What you learn</span></span>

* <span data-ttu-id="ab834-115">Como criar um Hub IoT e registrar um dispositivo no Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="ab834-115">How to create an IoT hub and register a device for Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="ab834-116">Como conectar o Feather HUZZAH ESP8266 ao sensor e ao computador</span><span class="sxs-lookup"><span data-stu-id="ab834-116">How to connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
* <span data-ttu-id="ab834-117">Como coletar dados do sensor executando um aplicativo de exemplo no Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="ab834-117">How to collect sensor data by running a sample application on Feather HUZZAH ESP8266</span></span>
* <span data-ttu-id="ab834-118">Como enviar os dados do sensor para o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="ab834-118">How to send the sensor data to your IoT hub</span></span>

## <a name="what-you-need"></a><span data-ttu-id="ab834-119">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="ab834-119">What you need</span></span>

![Partes necessárias para o tutorial](media/iot-hub-arduino-huzzah-esp8266-get-started/2_parts-needed-for-the-tutorial.png)

<span data-ttu-id="ab834-121">Para concluir esta operação, você precisará das seguintes partes do seu Kit de Início do Feather HUZZAH ESP8266:</span><span class="sxs-lookup"><span data-stu-id="ab834-121">To complete this operation, you need the following parts from your Feather HUZZAH ESP8266 Starter Kit:</span></span>

* <span data-ttu-id="ab834-122">A placa Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="ab834-122">The Feather HUZZAH ESP8266 board</span></span>
* <span data-ttu-id="ab834-123">Um cabo Micro USB para USB Tipo A</span><span class="sxs-lookup"><span data-stu-id="ab834-123">A Micro USB to Type A USB cable</span></span>

<span data-ttu-id="ab834-124">Você também precisa destes itens para seu ambiente de desenvolvimento:</span><span class="sxs-lookup"><span data-stu-id="ab834-124">You also need the following things for your development environment:</span></span>

* <span data-ttu-id="ab834-125">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="ab834-125">An active Azure subscription.</span></span> <span data-ttu-id="ab834-126">Se não tiver uma conta do Azure, [crie uma conta de avaliação gratuita do Azure](https://azure.microsoft.com/free/) em apenas alguns minutos.</span><span class="sxs-lookup"><span data-stu-id="ab834-126">If you don't have an Azure account, [create a free Azure trial account](https://azure.microsoft.com/free/) in just a few minutes.</span></span>
* <span data-ttu-id="ab834-127">Mac ou PC que esteja executando o Windows ou Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ab834-127">Mac or PC that is running Windows or Ubuntu.</span></span>
* <span data-ttu-id="ab834-128">Rede sem fio à qual Feather HUZZAH ESP8266 deve se conectar.</span><span class="sxs-lookup"><span data-stu-id="ab834-128">Wireless network for Feather HUZZAH ESP8266 to connect to.</span></span>
* <span data-ttu-id="ab834-129">Uma conexão com a Internet para baixar a ferramenta de configuração.</span><span class="sxs-lookup"><span data-stu-id="ab834-129">Internet connection to download the configuration tool.</span></span>
* <span data-ttu-id="ab834-130">[IDE do Arduino](https://www.arduino.cc/en/main/software) versão 1.6.8 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="ab834-130">[Arduino IDE](https://www.arduino.cc/en/main/software) version 1.6.8 or later.</span></span> <span data-ttu-id="ab834-131">As versões anteriores não funcionam com a biblioteca do AzureIoT.</span><span class="sxs-lookup"><span data-stu-id="ab834-131">Earlier versions don't work with the AzureIoT library.</span></span>

<span data-ttu-id="ab834-132">Os itens a seguir são opcionais, caso você não tenha um sensor.</span><span class="sxs-lookup"><span data-stu-id="ab834-132">The following items are optional in case you don’t have a sensor.</span></span> <span data-ttu-id="ab834-133">Você também tem a opção de usar dados de sensor simulada.</span><span class="sxs-lookup"><span data-stu-id="ab834-133">You also have the option of using simulated sensor data.</span></span>

* <span data-ttu-id="ab834-134">Um sensor de temperatura e umidade Adafruit DHT22</span><span class="sxs-lookup"><span data-stu-id="ab834-134">An Adafruit DHT22 temperature and humidity sensor</span></span>
* <span data-ttu-id="ab834-135">Uma placa universal</span><span class="sxs-lookup"><span data-stu-id="ab834-135">A breadboard</span></span>
* <span data-ttu-id="ab834-136">Cabos de jumper de M/M</span><span class="sxs-lookup"><span data-stu-id="ab834-136">M/M jumper wires</span></span>


[!INCLUDE [iot-hub-get-started-create-hub-and-device](../../includes/iot-hub-get-started-create-hub-and-device.md)]

## <a name="connect-feather-huzzah-esp8266-with-the-sensor-and-your-computer"></a><span data-ttu-id="ab834-137">Difusão HUZZAH ESP8266 de conexão com o sensor e seu computador</span><span class="sxs-lookup"><span data-stu-id="ab834-137">Connect Feather HUZZAH ESP8266 with the sensor and your computer</span></span>
<span data-ttu-id="ab834-138">Nesta seção, você conecta os sensores à sua placa.</span><span class="sxs-lookup"><span data-stu-id="ab834-138">In this section, you connect the sensors to your board.</span></span> <span data-ttu-id="ab834-139">Em seguida, você conecta o dispositivo ao computador para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="ab834-139">Then you plug in your device to your computer for further use.</span></span>
### <a name="connect-a-dht22-temperature-and-humidity-sensor-to-feather-huzzah-esp8266"></a><span data-ttu-id="ab834-140">Conecte um sensor de temperatura e umidade DHT22 a Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="ab834-140">Connect a DHT22 temperature and humidity sensor to Feather HUZZAH ESP8266</span></span>

<span data-ttu-id="ab834-141">Use os cabos da placa universal e jumper para fazer a conexão da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="ab834-141">Use the breadboard and jumper wires to make the connection as follows.</span></span> <span data-ttu-id="ab834-142">Se você não tiver um sensor, ignore esta seção porque você pode usar dados de sensor simulado em vez disso.</span><span class="sxs-lookup"><span data-stu-id="ab834-142">If you don’t have a sensor, skip this section because you can use simulated sensor data instead.</span></span>

![Referência de conexões](media/iot-hub-arduino-huzzah-esp8266-get-started/15_connections_on_breadboard.png)


<span data-ttu-id="ab834-144">Para os pinos do sensor, use a seguinte fiação:</span><span class="sxs-lookup"><span data-stu-id="ab834-144">For sensor pins, use the following wiring:</span></span>


| <span data-ttu-id="ab834-145">Início (Sensor)</span><span class="sxs-lookup"><span data-stu-id="ab834-145">Start (Sensor)</span></span>           | <span data-ttu-id="ab834-146">End (quadro)</span><span class="sxs-lookup"><span data-stu-id="ab834-146">End (Board)</span></span>           | <span data-ttu-id="ab834-147">Cor de cabo</span><span class="sxs-lookup"><span data-stu-id="ab834-147">Cable Color</span></span>   |
| -----------------------  | ---------------------- | ------------: |
| <span data-ttu-id="ab834-148">VDD (Pin 31F)</span><span class="sxs-lookup"><span data-stu-id="ab834-148">VDD (Pin 31F)</span></span>            | <span data-ttu-id="ab834-149">3V (Fixar 58H)</span><span class="sxs-lookup"><span data-stu-id="ab834-149">3V (Pin 58H)</span></span>           | <span data-ttu-id="ab834-150">Cabo vermelho</span><span class="sxs-lookup"><span data-stu-id="ab834-150">Red cable</span></span>     |
| <span data-ttu-id="ab834-151">DADOS de (Pin 32F)</span><span class="sxs-lookup"><span data-stu-id="ab834-151">DATA (Pin 32F)</span></span>           | <span data-ttu-id="ab834-152">GPIO 2 (Pin 46A)</span><span class="sxs-lookup"><span data-stu-id="ab834-152">GPIO 2 (Pin 46A)</span></span>       | <span data-ttu-id="ab834-153">Cabo azul</span><span class="sxs-lookup"><span data-stu-id="ab834-153">Blue cable</span></span>    |
| <span data-ttu-id="ab834-154">GND (Pin 34F)</span><span class="sxs-lookup"><span data-stu-id="ab834-154">GND (Pin 34F)</span></span>            | <span data-ttu-id="ab834-155">GND (PIn 56I)</span><span class="sxs-lookup"><span data-stu-id="ab834-155">GND (PIn 56I)</span></span>          | <span data-ttu-id="ab834-156">Cabo preto</span><span class="sxs-lookup"><span data-stu-id="ab834-156">Black cable</span></span>   |

<span data-ttu-id="ab834-157">Para obter mais informações, consulte [Instalação do sensor Adafruit DHT22](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) e [Pinagem do Adafruit Feather HUZZAH Esp8266](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span><span class="sxs-lookup"><span data-stu-id="ab834-157">For more information, see [Adafruit DHT22 sensor setup](https://learn.adafruit.com/dht/connecting-to-a-dhtxx-sensor) and [Adafruit Feather HUZZAH Esp8266 Pinouts](https://learn.adafruit.com/adafruit-feather-huzzah-esp8266/using-arduino-ide?view=all#pinouts).</span></span>



<span data-ttu-id="ab834-158">Agora seu Feather Huzzah ESP8266 deve estar conectado a um sensor ativo.</span><span class="sxs-lookup"><span data-stu-id="ab834-158">Now your Feather Huzzah ESP8266 should be connected with a working sensor.</span></span>

![Conectar o DHT22 ao Feather Huzzah](media/iot-hub-arduino-huzzah-esp8266-get-started/8_connect-dht22-feather-huzzah.png)

### <a name="connect-feather-huzzah-esp8266-to-your-computer"></a><span data-ttu-id="ab834-160">Conectar o Feather HUZZAH ESP8266 ao seu computador</span><span class="sxs-lookup"><span data-stu-id="ab834-160">Connect Feather HUZZAH ESP8266 to your computer</span></span>

<span data-ttu-id="ab834-161">Como mostrado a seguir, use o cabo Micro USB para USB Tipo A para conectar o Feather HUZZAH ESP8266 ao computador.</span><span class="sxs-lookup"><span data-stu-id="ab834-161">As shown next, use the Micro USB to Type A USB cable to connect Feather HUZZAH ESP8266 to your computer.</span></span>

![Conectar o Feather Huzzah ao computador](media/iot-hub-arduino-huzzah-esp8266-get-started/9_connect-feather-huzzah-computer.png)

### <a name="add-serial-port-permissions-ubuntu-only"></a><span data-ttu-id="ab834-163">Adicionar permissões de porta serial (somente Ubuntu)</span><span class="sxs-lookup"><span data-stu-id="ab834-163">Add serial port permissions (Ubuntu only)</span></span>


<span data-ttu-id="ab834-164">Se você usar o Ubuntu, verifique se tem as permissões para operar na porta USB do Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="ab834-164">If you use Ubuntu, make sure you have the permissions to operate on the USB port of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="ab834-165">Para adicionar permissões de porta serial, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ab834-165">To add serial port permissions, follow these steps:</span></span>


1. <span data-ttu-id="ab834-166">Execute os seguintes comandos em um terminal:</span><span class="sxs-lookup"><span data-stu-id="ab834-166">Run the following commands at a terminal:</span></span>

   ```bash
   ls -l /dev/ttyUSB*
   ls -l /dev/ttyACM*
   ```

   <span data-ttu-id="ab834-167">Você recebe uma das seguintes saídas:</span><span class="sxs-lookup"><span data-stu-id="ab834-167">You get one of the following outputs:</span></span>

   * <span data-ttu-id="ab834-168">crw-rw---- 1 root uucp xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="ab834-168">crw-rw---- 1 root uucp xxxxxxxx</span></span>
   * <span data-ttu-id="ab834-169">crw-rw---- 1 root dialout xxxxxxxx</span><span class="sxs-lookup"><span data-stu-id="ab834-169">crw-rw---- 1 root dialout xxxxxxxx</span></span>

   <span data-ttu-id="ab834-170">Na saída, observe se `uucp` ou `dialout` é o nome do proprietário do grupo da porta USB.</span><span class="sxs-lookup"><span data-stu-id="ab834-170">In the output, notice that `uucp` or `dialout` is the group owner name of the USB port.</span></span>

1. <span data-ttu-id="ab834-171">Adicione o usuário ao grupo, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="ab834-171">Add the user to the group by running the following command:</span></span>

   ```bash
   sudo usermod -a -G <group-owner-name> <username>
   ```

   <span data-ttu-id="ab834-172">`<group-owner-name>` é o nome de proprietário de grupo que você obteve na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="ab834-172">`<group-owner-name>` is the group owner name you obtained in the previous step.</span></span> <span data-ttu-id="ab834-173">`<username>` é o nome de usuário do Ubuntu.</span><span class="sxs-lookup"><span data-stu-id="ab834-173">`<username>` is your Ubuntu user name.</span></span>

1. <span data-ttu-id="ab834-174">Saia do Ubuntu e entre novamente para que a alteração seja exibida.</span><span class="sxs-lookup"><span data-stu-id="ab834-174">Sign out of Ubuntu, and then sign in again for the change to appear.</span></span>

## <a name="collect-sensor-data-and-send-it-to-your-iot-hub"></a><span data-ttu-id="ab834-175">Coletar dados de sensor e enviá-los para o hub IoT</span><span class="sxs-lookup"><span data-stu-id="ab834-175">Collect sensor data and send it to your IoT hub</span></span>

<span data-ttu-id="ab834-176">Nesta seção, implante e execute um aplicativo de exemplo em Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="ab834-176">In this section, you deploy and run a sample application on Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="ab834-177">O aplicativo de exemplo pisca o LED do Feather HUZZAH ESP8266 e envia os dados de temperatura e umidade coletados do sensor DHT22 para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="ab834-177">The sample application blinks the LED on Feather HUZZAH ESP8266, and sends the temperature and humidity data collected from the DHT22 sensor to your IoT hub.</span></span>

### <a name="get-the-sample-application-from-github"></a><span data-ttu-id="ab834-178">Obter o aplicativo de exemplo do GitHub</span><span class="sxs-lookup"><span data-stu-id="ab834-178">Get the sample application from GitHub</span></span>

<span data-ttu-id="ab834-179">O aplicativo de exemplo está hospedado no GitHub.</span><span class="sxs-lookup"><span data-stu-id="ab834-179">The sample application is hosted on GitHub.</span></span> <span data-ttu-id="ab834-180">Clone o repositório de exemplo que contém o aplicativo de exemplo do GitHub.</span><span class="sxs-lookup"><span data-stu-id="ab834-180">Clone the sample repository that contains the sample application from GitHub.</span></span> <span data-ttu-id="ab834-181">Para clonar o repositório de exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ab834-181">To clone the sample repository, follow these steps:</span></span>

1. <span data-ttu-id="ab834-182">Abra um prompt de comando ou uma janela de terminal.</span><span class="sxs-lookup"><span data-stu-id="ab834-182">Open a command prompt or a terminal window.</span></span>
1. <span data-ttu-id="ab834-183">Ir para uma pasta onde você deseja que o aplicativo de exemplo a ser armazenado.</span><span class="sxs-lookup"><span data-stu-id="ab834-183">Go to a folder where you want the sample application to be stored.</span></span>
1. <span data-ttu-id="ab834-184">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="ab834-184">Run the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-feather-huzzah-client-app.git
   ```

<span data-ttu-id="ab834-185">Instale o pacote do Feather HUZZAH ESP8266 no IDE do Arduino:</span><span class="sxs-lookup"><span data-stu-id="ab834-185">Install the package for Feather HUZZAH ESP8266 in the Arduino IDE:</span></span>

1. <span data-ttu-id="ab834-186">Abra a pasta onde o aplicativo de exemplo está armazenado.</span><span class="sxs-lookup"><span data-stu-id="ab834-186">Open the folder where the sample application is stored.</span></span>
1. <span data-ttu-id="ab834-187">Abra o arquivo app.ino na pasta do aplicativo no IDE do Arduino.</span><span class="sxs-lookup"><span data-stu-id="ab834-187">Open the app.ino file in the app folder in the Arduino IDE.</span></span>

   ![Abrir o aplicativo de exemplo no IDE do Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/10_arduino-ide-open-sample-app.png)

1. <span data-ttu-id="ab834-189">No IDE Arduino, clique em **arquivo** > **preferências**.</span><span class="sxs-lookup"><span data-stu-id="ab834-189">In the Arduino IDE, click **File** > **Preferences**.</span></span>
1. <span data-ttu-id="ab834-190">Na caixa de diálogo **Preferências**, clique no ícone ao lado da caixa **URLs Adicionais do Gerenciador de Placas**.</span><span class="sxs-lookup"><span data-stu-id="ab834-190">In the **Preferences** dialog box, click the icon next to the **Additional Boards Manager URLs** box.</span></span>
1. <span data-ttu-id="ab834-191">Na janela pop-up, insira a URL a seguir e clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab834-191">In the pop-up window, enter the following URL, and then click **OK**.</span></span>

   `http://arduino.esp8266.com/stable/package_esp8266com_index.json`

   ![Apontar para uma URL do pacote no IDE do Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/11_arduino-ide-package-url.png)

1. <span data-ttu-id="ab834-193">No **preferência** caixa de diálogo, clique em **OK**.</span><span class="sxs-lookup"><span data-stu-id="ab834-193">In the **Preference** dialog box, click **OK**.</span></span>
1. <span data-ttu-id="ab834-194">Clique em **Ferramentas** > **Placa** > **Gerenciador de Placas** e procure esp8266.</span><span class="sxs-lookup"><span data-stu-id="ab834-194">Click **Tools** > **Board** > **Boards Manager**, and then search for esp8266.</span></span>

   <span data-ttu-id="ab834-195">O Gerenciador de Placas indica que ESP8266 com uma versão 2.2.0 ou posterior está instalado.</span><span class="sxs-lookup"><span data-stu-id="ab834-195">Boards Manager indicates that ESP8266 with a version of 2.2.0 or later is installed.</span></span>

   ![O pacote do esp8266 é instalado](media/iot-hub-arduino-huzzah-esp8266-get-started/12_arduino-ide-esp8266-installed.png)

1. <span data-ttu-id="ab834-197">Clique em **ferramentas** > **placa** > **Adafruit HUZZAH ESP8266**.</span><span class="sxs-lookup"><span data-stu-id="ab834-197">Click **Tools** > **Board** > **Adafruit HUZZAH ESP8266**.</span></span>

### <a name="install-necessary-libraries"></a><span data-ttu-id="ab834-198">Instalar as bibliotecas necessárias</span><span class="sxs-lookup"><span data-stu-id="ab834-198">Install necessary libraries</span></span>

1. <span data-ttu-id="ab834-199">No IDE Arduino, clique em **esboço** > **biblioteca incluem** > **gerenciar bibliotecas**.</span><span class="sxs-lookup"><span data-stu-id="ab834-199">In the Arduino IDE, click **Sketch** > **Include Library** > **Manage Libraries**.</span></span>
1. <span data-ttu-id="ab834-200">Procure a seguinte biblioteca nomes individualmente.</span><span class="sxs-lookup"><span data-stu-id="ab834-200">Search for the following library names one by one.</span></span> <span data-ttu-id="ab834-201">Para cada biblioteca que você localizar, clique em **Instalar**.</span><span class="sxs-lookup"><span data-stu-id="ab834-201">For each  library that you find, click **Install**.</span></span>
   * `AzureIoTHub`
   * `AzureIoTUtility`
   * `AzureIoTProtocol_MQTT`
   * `ArduinoJson`
   * `DHT sensor library`
   * `Adafruit Unified Sensor`

### <a name="dont-have-a-real-dht22-sensor"></a><span data-ttu-id="ab834-202">Você não tem um sensor DHT22 real?</span><span class="sxs-lookup"><span data-stu-id="ab834-202">Don’t have a real DHT22 sensor?</span></span>

<span data-ttu-id="ab834-203">O aplicativo de exemplo pode simular a temperatura e umidade dados caso você não tenha um sensor DHT22 real.</span><span class="sxs-lookup"><span data-stu-id="ab834-203">The sample application can simulate temperature and humidity data in case you don’t have a real DHT22 sensor.</span></span> <span data-ttu-id="ab834-204">Para configurar o aplicativo de exemplo para usar dados simulados, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="ab834-204">To set up the sample application to use simulated data, follow these steps:</span></span>

1. <span data-ttu-id="ab834-205">Abra o `config.h` arquivo o `app` pasta.</span><span class="sxs-lookup"><span data-stu-id="ab834-205">Open the `config.h` file in the `app` folder.</span></span>
1. <span data-ttu-id="ab834-206">Localize a seguinte linha de código e altere o valor de `false` para `true`:</span><span class="sxs-lookup"><span data-stu-id="ab834-206">Locate the following line of code and change the value from `false` to `true`:</span></span>
   ```c
   define SIMULATED_DATA true
   ```
   ![Configurar o aplicativo de exemplo para usar dados simulados](media/iot-hub-arduino-huzzah-esp8266-get-started/13_arduino-ide-configure-app-use-simulated-data.png)

1. <span data-ttu-id="ab834-208">Salve o arquivo com `Control-s`.</span><span class="sxs-lookup"><span data-stu-id="ab834-208">Save the file with `Control-s`.</span></span>

### <a name="deploy-the-sample-application-to-feather-huzzah-esp8266"></a><span data-ttu-id="ab834-209">Implantar o aplicativo de exemplo para Feather HUZZAH ESP8266</span><span class="sxs-lookup"><span data-stu-id="ab834-209">Deploy the sample application to Feather HUZZAH ESP8266</span></span>

1. <span data-ttu-id="ab834-210">No IDE Arduino, clique em **Ferramenta** > **Porta** e clique na porta serial para Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="ab834-210">In the Arduino IDE, click **Tool** > **Port**, and then click the serial port for Feather HUZZAH ESP8266.</span></span>
1. <span data-ttu-id="ab834-211">Clique em **esboço** > **carregar** para criar e implantar o aplicativo de exemplo para Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="ab834-211">Click **Sketch** > **Upload** to build and deploy the sample application to Feather HUZZAH ESP8266.</span></span>

### <a name="enter-your-credentials"></a><span data-ttu-id="ab834-212">Inserir suas credenciais</span><span class="sxs-lookup"><span data-stu-id="ab834-212">Enter your credentials</span></span>

<span data-ttu-id="ab834-213">Depois que o upload for concluído com êxito, siga estas etapas para inserir suas credenciais:</span><span class="sxs-lookup"><span data-stu-id="ab834-213">After the upload completes successfully, follow these steps to enter your credentials:</span></span>

1. <span data-ttu-id="ab834-214">No IDE Arduino, clique em **ferramentas** > **Serial Monitor**.</span><span class="sxs-lookup"><span data-stu-id="ab834-214">In the Arduino IDE, click **Tools** > **Serial Monitor**.</span></span>
1. <span data-ttu-id="ab834-215">Na janela do monitor serial, observe as duas listas suspensas no canto inferior direito.</span><span class="sxs-lookup"><span data-stu-id="ab834-215">In the serial monitor window, notice the two drop-down lists in the lower-right corner.</span></span>
1. <span data-ttu-id="ab834-216">Selecione **nenhuma final de linha** para obter a lista suspensa à esquerda.</span><span class="sxs-lookup"><span data-stu-id="ab834-216">Select **No line ending** for the left drop-down list.</span></span>
1. <span data-ttu-id="ab834-217">Selecione **115200 baud** para obter a lista suspensa à direita.</span><span class="sxs-lookup"><span data-stu-id="ab834-217">Select **115200 baud** for the right drop-down list.</span></span>
1. <span data-ttu-id="ab834-218">Na caixa de entrada localizada na parte superior da janela do monitor serial, insira as seguintes informações se você for solicitado a fornecê-las e clique em **Enviar**.</span><span class="sxs-lookup"><span data-stu-id="ab834-218">In the input box located at the top of the serial monitor window, enter the following information if you are asked to provide them, and then click **Send**.</span></span>
   * <span data-ttu-id="ab834-219">SSID Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="ab834-219">Wi-Fi SSID</span></span>
   * <span data-ttu-id="ab834-220">Senha de Wi-Fi</span><span class="sxs-lookup"><span data-stu-id="ab834-220">Wi-Fi password</span></span>
   * <span data-ttu-id="ab834-221">Cadeia de conexão de dispositivo</span><span class="sxs-lookup"><span data-stu-id="ab834-221">Device connection string</span></span>

> [!Note]
> <span data-ttu-id="ab834-222">As informações de credencial são armazenadas no EEPROM do Feather HUZZAH ESP8266.</span><span class="sxs-lookup"><span data-stu-id="ab834-222">The credential information is stored in the EEPROM of Feather HUZZAH ESP8266.</span></span> <span data-ttu-id="ab834-223">Se você clicar no botão Redefinir da placa Feather HUZZAH ESP8266, o aplicativo de exemplo perguntará se você deseja apagar as informações.</span><span class="sxs-lookup"><span data-stu-id="ab834-223">If you click the reset button on the Feather HUZZAH ESP8266 board, the sample application asks if you want to erase the information.</span></span> <span data-ttu-id="ab834-224">Insira `Y` para apagar as informações.</span><span class="sxs-lookup"><span data-stu-id="ab834-224">Enter `Y` to have the information erased.</span></span> <span data-ttu-id="ab834-225">Você será solicitado a fornecer as informações uma segunda vez.</span><span class="sxs-lookup"><span data-stu-id="ab834-225">You are asked to provide the information a second time.</span></span>

### <a name="verify-the-sample-application-is-running-successfully"></a><span data-ttu-id="ab834-226">Verificar se o aplicativo de exemplo está sendo executado com êxito</span><span class="sxs-lookup"><span data-stu-id="ab834-226">Verify the sample application is running successfully</span></span>

<span data-ttu-id="ab834-227">Se você vir a seguinte saída da janela serial monitor e o LED piscando no Feather HUZZAH ESP8266, o aplicativo de exemplo está sendo executado com êxito.</span><span class="sxs-lookup"><span data-stu-id="ab834-227">If you see the following output from the serial monitor window and the blinking LED on Feather HUZZAH ESP8266, the sample application is running successfully.</span></span>

![Saída final no IDE do Arduino](media/iot-hub-arduino-huzzah-esp8266-get-started/14_arduino-ide-final-output.png)

## <a name="next-steps"></a><span data-ttu-id="ab834-229">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ab834-229">Next steps</span></span>

<span data-ttu-id="ab834-230">Você conectou um Feather HUZZAH ESP8266 ao Hub IoT e enviou os dados capturados do sensor para o Hub IoT com êxito.</span><span class="sxs-lookup"><span data-stu-id="ab834-230">You have successfully connected a Feather HUZZAH ESP8266 to your IoT hub, and sent the captured sensor data to your IoT hub.</span></span> 

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]

