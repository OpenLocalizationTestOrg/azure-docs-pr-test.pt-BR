---
title: "Connect Arduino (C) tooAzure IoT – lição 4: dispositivos de nuvem | Microsoft Docs"
description: "Um aplicativo de exemplo é executado no Adafruit Feather M0 WiFi e monitora mensagens de entrada de seu Hub IoT. Uma nova tarefa gulp envia mensagens tooAdafruit difusão M0 WiFi do seu Olá de tooblink de hub IoT LED."
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
ms.openlocfilehash: dcddd61ff684f49436103675938d719cb227c409
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-tooreceive-cloud-to-device-messages"></a><span data-ttu-id="36a9e-105">Executar um tooreceive do aplicativo de exemplo mensagens de nuvem para dispositivo</span><span class="sxs-lookup"><span data-stu-id="36a9e-105">Run a sample application tooreceive cloud-to-device messages</span></span>
<span data-ttu-id="36a9e-106">Neste artigo, você implanta um aplicativo de exemplo na placa Adafruit difusão M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="36a9e-106">In this article, you deploy a sample application on your Adafruit Feather M0 WiFi Arduino board.</span></span>

<span data-ttu-id="36a9e-107">aplicativo de exemplo Hello monitora mensagens de entrada de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36a9e-107">hello sample application monitors incoming messages from your IoT hub.</span></span> <span data-ttu-id="36a9e-108">Você também executar uma tarefa de vez em seu tooyour de mensagens do computador toosend Arduino quadro do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36a9e-108">You also run a gulp task on your computer toosend messages tooyour Arduino board from your IoT hub.</span></span> <span data-ttu-id="36a9e-109">Quando o aplicativo de exemplo hello recebe mensagens de saudação, pisca Olá LED.</span><span class="sxs-lookup"><span data-stu-id="36a9e-109">When hello sample application receives hello messages, it blinks hello LED.</span></span> <span data-ttu-id="36a9e-110">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="36a9e-110">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="36a9e-111">O que você fará</span><span class="sxs-lookup"><span data-stu-id="36a9e-111">What you will do</span></span>
* <span data-ttu-id="36a9e-112">Conecte-se o hub IoT do hello exemplo aplicativo tooyour.</span><span class="sxs-lookup"><span data-stu-id="36a9e-112">Connect hello sample application tooyour IoT hub.</span></span>
* <span data-ttu-id="36a9e-113">Implante e execute o aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="36a9e-113">Deploy and run hello sample application.</span></span>
* <span data-ttu-id="36a9e-114">Envie mensagens de seu Olá de quadro tooblink do IoT hub tooyour Arduino LED.</span><span class="sxs-lookup"><span data-stu-id="36a9e-114">Send messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="36a9e-115">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="36a9e-115">What you will learn</span></span>
<span data-ttu-id="36a9e-116">Neste artigo, você aprenderá:</span><span class="sxs-lookup"><span data-stu-id="36a9e-116">In this article, you will learn:</span></span>
* <span data-ttu-id="36a9e-117">Como toomonitor de mensagens de entrada do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36a9e-117">How toomonitor incoming messages from your IoT hub.</span></span>
* <span data-ttu-id="36a9e-118">Como toosend de nuvem para dispositivo mensagens de seu tooyour de hub IoT Arduino quadro.</span><span class="sxs-lookup"><span data-stu-id="36a9e-118">How toosend cloud-to-device messages from your IoT hub tooyour Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="36a9e-119">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="36a9e-119">What you need</span></span>
* <span data-ttu-id="36a9e-120">Sua placa Arduino, configurada para uso.</span><span class="sxs-lookup"><span data-stu-id="36a9e-120">Your Arduino board, set up for use.</span></span> <span data-ttu-id="36a9e-121">toolearn como tooset a placa Arduino, consulte [configurar seu dispositivo][configure-your-device].</span><span class="sxs-lookup"><span data-stu-id="36a9e-121">toolearn how tooset up your Arduino board, see [Configure your device][configure-your-device].</span></span>
* <span data-ttu-id="36a9e-122">Um hub IoT criado em sua assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="36a9e-122">An IoT hub that is created in your Azure subscription.</span></span> <span data-ttu-id="36a9e-123">toolearn como toocreate seu hub IoT, consulte [criar o Azure IoT Hub][create-your-azure-iot-hub].</span><span class="sxs-lookup"><span data-stu-id="36a9e-123">toolearn how toocreate your IoT hub, see [Create your Azure IoT Hub][create-your-azure-iot-hub].</span></span>

## <a name="connect-hello-sample-application-tooyour-iot-hub"></a><span data-ttu-id="36a9e-124">Conecte Olá exemplo aplicativo tooyour IoT hub</span><span class="sxs-lookup"><span data-stu-id="36a9e-124">Connect hello sample application tooyour IoT hub</span></span>

1. <span data-ttu-id="36a9e-125">Certifique-se de que você está na pasta do repositório de saudação `iot-hub-c-feather-m0-getting-started`.</span><span class="sxs-lookup"><span data-stu-id="36a9e-125">Make sure that you're in hello repo folder `iot-hub-c-feather-m0-getting-started`.</span></span>

   <span data-ttu-id="36a9e-126">Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="36a9e-126">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd Lesson4
   code .
   ```

   <span data-ttu-id="36a9e-127">Saudação de aviso `app.ino` arquivo hello `app` subpasta.</span><span class="sxs-lookup"><span data-stu-id="36a9e-127">Notice hello `app.ino` file in hello `app` subfolder.</span></span> <span data-ttu-id="36a9e-128">Olá `app.ino` é arquivo de origem da chave de saudação que contém Olá código toomonitor mensagens de entrada de hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="36a9e-128">hello `app.ino` file is hello key source file that contains hello code toomonitor incoming messages from hello IoT hub.</span></span> <span data-ttu-id="36a9e-129">Olá `blinkLED` função pisca Olá LED.</span><span class="sxs-lookup"><span data-stu-id="36a9e-129">hello `blinkLED` function blinks hello LED.</span></span>

   ![Estrutura do repositório no aplicativo de exemplo hello][repo-structure]

2. <span data-ttu-id="36a9e-131">Obter a porta serial saudação do dispositivo Olá Olá CLI de descoberta do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="36a9e-131">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="36a9e-132">Você deve ver uma saída que é a seguir toohello semelhante e encontrar hello usb porta COM para a sua placa Arduino:</span><span class="sxs-lookup"><span data-stu-id="36a9e-132">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Descoberta de dispositivo][device-discovery]

3. <span data-ttu-id="36a9e-134">Arquivo hello abrir `config.json` na pasta de lição do hello e o valor de entrada hello da saudação encontrada número da porta COM:</span><span class="sxs-lookup"><span data-stu-id="36a9e-134">Open hello file `config.json` in hello lesson folder and input hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="36a9e-136">Para a porta de saudação COM, na plataforma Windows, tem um formato de Olá `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="36a9e-136">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="36a9e-137">No macOS ou Ubuntu, começará com `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="36a9e-137">On macOS or Ubuntu, it will start with `/dev/`.</span></span>

4. <span data-ttu-id="36a9e-138">Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="36a9e-138">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   # For Windows command prompt
   npm install
   gulp init
   gulp install-tools
   ```

5. <span data-ttu-id="36a9e-139">Verifique Olá substituições em Olá a seguir `config-arduino.json` arquivo:</span><span class="sxs-lookup"><span data-stu-id="36a9e-139">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   <span data-ttu-id="36a9e-140">Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure] [ create-an-azure-function-app-and-storage-account] neste computador, todas as configurações de saudação são herdadas, portanto você pode ignorar a tarefa de toohello Olá etapa de implantação e executando o aplicativo de exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="36a9e-140">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on this computer, all hello configurations are inherited, so you can skip hello step toohello task of deploying and running hello sample application.</span></span> <span data-ttu-id="36a9e-141">Se você concluiu as etapas de saudação em [criar uma conta de armazenamento e o aplicativo de função do Azure] [ create-an-azure-function-app-and-storage-account] em um computador diferente, você precisa espaços reservados Olá tooreplace Olá `config-arduino.json` arquivo.</span><span class="sxs-lookup"><span data-stu-id="36a9e-141">If you completed hello steps in [Create an Azure function app and storage account][create-an-azure-function-app-and-storage-account] on a different computer, you need tooreplace hello placeholders in hello `config-arduino.json` file.</span></span> <span data-ttu-id="36a9e-142">Olá `config-arduino.json` arquivo está na subpasta de saudação da sua pasta base.</span><span class="sxs-lookup"><span data-stu-id="36a9e-142">hello `config-arduino.json` file is in hello subfolder of your home folder.</span></span>

   ![Conteúdo do arquivo de configuração arduino.json Olá][config-arduino-json]

   * <span data-ttu-id="36a9e-144">Substituir **[Wi-Fi SSID]** com o seu SSID de Wi-Fi que conectado toohello da Internet.</span><span class="sxs-lookup"><span data-stu-id="36a9e-144">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="36a9e-145">Substitua **[senha Wi-Fi]** pela senha de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="36a9e-145">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="36a9e-146">Remova cadeia de caracteres de saudação se o Wi-Fi não exigir uma senha.</span><span class="sxs-lookup"><span data-stu-id="36a9e-146">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="36a9e-147">Substituir **[cadeia de conexão de dispositivo IoT]** com cadeia de conexão do dispositivo Olá obter executando Olá `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` comando.</span><span class="sxs-lookup"><span data-stu-id="36a9e-147">Replace **[IoT device connection string]** with hello device connection string that you get by running hello `az iot device show-connection-string --hub-name {my hub name} --device-id {device id}` command.</span></span>
   * <span data-ttu-id="36a9e-148">Substituir **[cadeia de conexão de hub IoT]** com hello cadeia de conexão de hub IoT que você obtém executando Olá `az iot hub show-connection-string --name {my hub name}` comando.</span><span class="sxs-lookup"><span data-stu-id="36a9e-148">Replace **[IoT hub connection string]** with hello IoT hub connection string that you get by running hello `az iot hub show-connection-string --name {my hub name}` command.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="36a9e-149">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="36a9e-149">Deploy and run hello sample application</span></span>
<span data-ttu-id="36a9e-150">Implantar e executar o aplicativo de exemplo hello em seu quadro Arduino executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="36a9e-150">Deploy and run hello sample application on your Arduino board by running hello following commands:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

<span data-ttu-id="36a9e-151">comando de gulp Olá implanta quadro do hello exemplo aplicativo tooyour Arduino.</span><span class="sxs-lookup"><span data-stu-id="36a9e-151">hello gulp command deploys hello sample application tooyour Arduino board.</span></span> <span data-ttu-id="36a9e-152">Em seguida, ele é executado aplicativo hello em seu quadro Arduino e uma tarefa separada em seu host placa Arduino tooyour de mensagens do computador toosend 20 intermitência de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36a9e-152">Then, it runs hello application on your Arduino board and a separate task on your host computer toosend 20 blink messages tooyour Arduino board from your IoT hub.</span></span>

<span data-ttu-id="36a9e-153">Depois que o aplicativo de exemplo hello é executado, ele inicia a escuta toomessages do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="36a9e-153">After hello sample application runs, it starts listening toomessages from your IoT hub.</span></span> <span data-ttu-id="36a9e-154">Enquanto isso, a tarefa de gulp de saudação envia várias mensagens de "intermitência" de seu tooyour de hub IoT Arduino quadro.</span><span class="sxs-lookup"><span data-stu-id="36a9e-154">Meanwhile, hello gulp task sends several "blink" messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="36a9e-155">Para cada mensagem de intermitência Olá placa recebe, o aplicativo de exemplo hello chama Olá `blinkLED` Olá tooblink de função LED.</span><span class="sxs-lookup"><span data-stu-id="36a9e-155">For each blink message that hello board receives, hello sample application calls hello `blinkLED` function tooblink hello LED.</span></span>

<span data-ttu-id="36a9e-156">Você deve ver Olá LED piscar a cada dois segundos como tarefa de gulp Olá envia 20 mensagens da sua tooyour de hub IoT Arduino quadro.</span><span class="sxs-lookup"><span data-stu-id="36a9e-156">You should see hello LED blink every two seconds as hello gulp task sends 20 messages from your IoT hub tooyour Arduino board.</span></span> <span data-ttu-id="36a9e-157">Hello última um é uma mensagem "stop" que interrompe a execução do aplicativo hello.</span><span class="sxs-lookup"><span data-stu-id="36a9e-157">hello last one is a "stop" message that stops hello application from running.</span></span>

![Exemplo de aplicativo com o comando gulp e mensagens de piscar][sample-application]

## <a name="summary"></a><span data-ttu-id="36a9e-159">Resumo</span><span class="sxs-lookup"><span data-stu-id="36a9e-159">Summary</span></span>
<span data-ttu-id="36a9e-160">Você enviou com êxito as mensagens de seu Olá de quadro tooblink do IoT hub tooyour Arduino LED.</span><span class="sxs-lookup"><span data-stu-id="36a9e-160">You’ve successfully sent messages from your IoT hub tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="36a9e-161">Olá próxima tarefa é opcional: altere Olá ativa e desativa o comportamento de saudação LED.</span><span class="sxs-lookup"><span data-stu-id="36a9e-161">hello next task is optional: change hello on and off behavior of hello LED.</span></span>

## <a name="next-steps"></a><span data-ttu-id="36a9e-162">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="36a9e-162">Next steps</span></span>
<span data-ttu-id="36a9e-163">[Alterar Olá ativa e desativa o comportamento de saudação LED][change-the-on-and-off-led-behavior]</span><span class="sxs-lookup"><span data-stu-id="36a9e-163">[Change hello on and off behavior of hello LED][change-the-on-and-off-led-behavior]</span></span>


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