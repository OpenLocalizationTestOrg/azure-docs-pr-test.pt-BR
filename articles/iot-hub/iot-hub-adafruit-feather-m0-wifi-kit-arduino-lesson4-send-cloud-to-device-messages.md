---
title: "Conectar o Arduino (C) ao IoT do Azure – Lição 4: nuvem para dispositivo | Microsoft Docs"
description: "Um aplicativo de exemplo é executado no Adafruit Feather M0 WiFi e monitora mensagens de entrada de seu Hub IoT. Uma nova tarefa gulp envia mensagens para seu Adafruit Feather M0 WiFi de seu Hub IoT para piscar o LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: controlar led pela web com arduino, controlar led via web com arduino
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: a0bf53fb-29fb-485f-ba4a-6c715057b1a2
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: b4f4c1d86b10b64c104ac812d1f650d723322be8
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="run-a-sample-application-to-receive-cloud-to-device-messages"></a><span data-ttu-id="c3230-105">Executar um aplicativo de exemplo para receber mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="c3230-105">Run a sample application to receive cloud-to-device messages</span></span>
<span data-ttu-id="c3230-106">Neste artigo, você implanta um aplicativo de exemplo na placa Adafruit difusão M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="c3230-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="c3230-107">O aplicativo de exemplo monitora mensagens recebidas do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c3230-107">The sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="c3230-108">Você também executa uma tarefa gulp no computador para enviar mensagens para a placa Arduino de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c3230-108">You also run a gulp task on your computer to send messages to your Arduino board from your IoT hub.</span></span> <span data-ttu-id="c3230-109">Quando o aplicativo de exemplo recebe uma a mensagem, ele pisca o LED.</span><span class="sxs-lookup"><span data-stu-id="c3230-109">When the sample application receives the messages, it blinks the LED.</span></span> <span data-ttu-id="c3230-110">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="c3230-110">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="c3230-111">O que você fará</span><span class="sxs-lookup"><span data-stu-id="c3230-111">What you will do</span></span>
* <span data-ttu-id="c3230-112">Conectar o aplicativo de exemplo ao hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c3230-112">Connect the sample application to your IoT hub.</span></span>
* <span data-ttu-id="c3230-113">Implantar e executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c3230-113">Deploy and run the sample application.</span></span>
* <span data-ttu-id="c3230-114">Envie mensagens do hub IoT para a placa Arduino para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="c3230-114">Send messages from your IoT hub to your Arduino board to blink the LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c3230-115">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c3230-115">What you will learn</span></span>
<span data-ttu-id="c3230-116">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="c3230-116">In this article, you will learn:</span></span>
* <span data-ttu-id="c3230-117">Como monitorar mensagens recebidas do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c3230-117">How to monitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="c3230-118">Agora, você pode enviar mensagens da nuvem para o dispositivo de seu Hub IoT para a placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="c3230-118">How to send cloud-to-device messages from your IoT hub to your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c3230-119">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="c3230-119">What you need</span></span>
* <span data-ttu-id="c3230-120">Sua placa Arduino, configurada para uso.</span><span class="sxs-lookup"><span data-stu-id="c3230-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="c3230-121">Para saber como configurar a placa Arduino Pi, consulte [Configurar seu dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="c3230-121">To learn how to set up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="c3230-122">Um hub IoT criado em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="c3230-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="c3230-123">Para aprender a criar seu Hub IoT, consulte [Criar seu Hub IoT do Azure][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="c3230-123">To learn how to create your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-the-sample-application-to-your-iot-hub"></a><span data-ttu-id="c3230-124">Conectar o aplicativo de exemplo ao Hub IoT</span><span class="sxs-lookup"><span data-stu-id="c3230-124">Connect the sample application to your IoT hub</span></span>

1. <span data-ttu-id="c3230-125">Verifique se você está na pasta de repositório `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="c3230-125">Make sure that you're in the repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="c3230-126">Abra o aplicativo de exemplo no Visual Studio Code, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c3230-126">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="c3230-127">Observe o arquivo `app.ino` na subpasta `app`.</span><span class="sxs-lookup"><span data-stu-id="c3230-127">Notice the `app.ino` file in the `app` subfolder.</span></span> <span data-ttu-id="c3230-128">O arquivo `app.ino` é o arquivo de origem principal que contém o código para monitorar mensagens recebidas do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c3230-128">The `app.ino` file is the key source file that contains the code to monitor incoming messages from the IoT hub.</span></span> <span data-ttu-id="c3230-129">A função `blinkLED` pisca o LED.</span><span class="sxs-lookup"><span data-stu-id="c3230-129">The `blinkLED` function blinks the LED.</span></span>

   ![Estrutura do repositório no aplicativo de exemplo][repo-structure]

2. <span data-ttu-id="c3230-131">Obter a porta serial do dispositivo com a CLI de descoberta de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="c3230-131">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="c3230-132">Você deve ver uma saída semelhante à seguinte e encontrar a porta COM USB para sua placa Arduino:</span><span class="sxs-lookup"><span data-stu-id="c3230-132">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Descoberta de dispositivo][device-discovery]

3. <span data-ttu-id="c3230-134">Abra o arquivo `config.json` na pasta da lição e adicione o valor do número da porta COM encontrado:</span><span class="sxs-lookup"><span data-stu-id="c3230-134">Open the file `config.json` in the lesson folder and input the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="c3230-136">Para a porta COM, na plataforma Windows, ele tem o formato de `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="c3230-136">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="c3230-137">No macOS ou Ubuntu, começará com `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="c3230-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="c3230-138">Inicialize o arquivo de configuração executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c3230-138">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="c3230-139">Faça as seguintes substituições no arquivo `config-arduino.json`:</span><span class="sxs-lookup"><span data-stu-id="c3230-139">Make the following replacements in the `config-arduino.json` file:</span></span>

   <span data-ttu-id="c3230-140">Se você concluiu as etapas em [Criar uma conta de armazenamento e aplicativo de funções do Azure][create-an-azure-function-app-and-storage-account] neste computador, todas as configurações serão herdadas, portanto você poderá ignorar a tarefa de implantar e executar o aplicativo de exemplo.</span><span class="sxs-lookup"><span data-stu-id="c3230-140">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all the configurations are inherited, so you can skip the step to the task of deploying and running the sample application.</span></span> <span data-ttu-id="c3230-141">Se você concluiu as etapas em [Criar uma conta de armazenamento e aplicativo de funções do Azure][create-an-azure-function-app-and-storage-account] em um computador diferente, será necessário substituir os espaços reservados no arquivo `config-arduino.json`.</span><span class="sxs-lookup"><span data-stu-id="c3230-141">If you completed the steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need to replace the placeholders in the `config-arduino.json` file.</span></span> <span data-ttu-id="c3230-142">O arquivo `config-arduino.json` está na subpasta da pasta base.</span><span class="sxs-lookup"><span data-stu-id="c3230-142">The `config-arduino.json` file is in the subfolder of your home folder.</span></span>

   ![Conteúdo do arquivo config-arduino.json][config-arduino-json]

   * <span data-ttu-id="c3230-144">Substitua **[SSID Wi-Fi]** por seu SSID Wi-Fi conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="c3230-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="c3230-145">Substitua **[senha Wi-Fi]** pela senha de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="c3230-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="c3230-146">Remova a cadeia de caracteres se o Wi-Fi não precisar de uma senha.</span><span class="sxs-lookup"><span data-stu-id="c3230-146">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="c3230-147">Substitua **[cadeia de conexão do dispositivo IoT]** pela cadeia de conexão do dispositivo que você obtém executando o comando `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}`.</span><span class="sxs-lookup"><span data-stu-id="c3230-147">Replace **[IoT device connection string]** with the device connection string that you get by running the `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="c3230-148">Substitua **[cadeia de conexão do hub IoT]** pela cadeia de conexão do hub IoT que você obtém executando o comando `az iot hub show-connection-string --name {my hub name}`.</span><span class="sxs-lookup"><span data-stu-id="c3230-148">Replace **[IoT hub connection string]** with the IoT hub connection string that you get by running the `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="c3230-149">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="c3230-149">Deploy and run the sample application</span></span>
<span data-ttu-id="c3230-150">Implante e execute o aplicativo de exemplo na sua placa do Arduino executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c3230-150">Deploy and run the sample application on your Arduino board by running the following commands:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="c3230-151">O comando gulp implanta o aplicativo de exemplo na sua placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="c3230-151">The gulp command deploys the sample application to your Arduino board.</span></span> <span data-ttu-id="c3230-152">Por fim, ele executa o aplicativo na sua placa Arduino e uma tarefa separada no computador host para enviar 20 mensagens de piscar para sua placa Arduino do hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c3230-152">Then, it runs the application on your Arduino board and a separate task on your host computer to send 20 blink messages to your Arduino board from your IoT hub.</span></span>

<span data-ttu-id="c3230-153">Após a execução, o aplicativo de exemplo começa a escutar as mensagens do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="c3230-153">After the sample application runs, it starts listening to messages from your IoT hub.</span></span> <span data-ttu-id="c3230-154">Enquanto isso, a tarefa gulp envia várias mensagens de "piscar" do hub IoT para a sua placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="c3230-154">Meanwhile, the gulp task sends several "blink" messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="c3230-155">Para cada mensagem de piscar que a placa recebe, o aplicativo de exemplo chama a função `blinkLED` para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="c3230-155">For each blink message that the board receives, the sample application calls the `blinkLED` function to blink the LED.</span></span>

<span data-ttu-id="c3230-156">Você deve ver o LED piscar a cada dois segundos, uma vez que a tarefa gulp está enviando 20 mensagens do Hub IoT para sua placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="c3230-156">You should see the LED blink every two seconds as the gulp task sends 20 messages from your IoT hub to your Arduino board.</span></span> <span data-ttu-id="c3230-157">A última é uma mensagem de “parar” que interrompe a execução do aplicativo.</span><span class="sxs-lookup"><span data-stu-id="c3230-157">The last one is a "stop" message that stops the application from running.</span></span>

![Exemplo de aplicativo com o comando gulp e mensagens de piscar][sample-application]

## <a name="summary"></a><span data-ttu-id="c3230-159">Resumo</span><span class="sxs-lookup"><span data-stu-id="c3230-159">Summary</span></span>
<span data-ttu-id="c3230-160">Você enviou com êxito mensagens do hub IoT para sua placa Arduino para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="c3230-160">You’ve successfully sent messages from your IoT hub to your Arduino board to blink the LED.</span></span> <span data-ttu-id="c3230-161">A próxima tarefa é opcional: alterar o comportamento de liga e desliga do LED.</span><span class="sxs-lookup"><span data-stu-id="c3230-161">The next task is optional: change the on and off behavior of the LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3230-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3230-162">Next steps</span></span>
<span data-ttu-id="c3230-163">[Alterar o comportamento de ligar e desligar do LED][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="c3230-163">[Change the on and off behavior of the LED][change-the-on-and-off-led-behavior]</span></span>


<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[create-your-azure-iot-hub]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-prepare-azure-iot-hub.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/repo_structure_arduino.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[create-an-azure-function-app-and-storage-account]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/config-arduino.png
[sample-application]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson4/gulp_blink_arduino.png
[change-the-on-and-off-led-behavior]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson4-change-led-behavior.md