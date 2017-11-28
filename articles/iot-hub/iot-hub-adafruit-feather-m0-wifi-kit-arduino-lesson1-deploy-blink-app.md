---
title: "Conecte-se Arduino tooAzure IoT - lição 1: implantar o aplicativo | Microsoft Docs"
description: "Clonar um aplicativo de Arduino exemplo hello do GitHub e, em seguida, execute o gulp toodeploy tooyour esse aplicativo Adafruit difusão M0 WiFi. Este aplicativo de exemplo pisca Olá GPIO"
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "projetos led arduino, piscar led arduino, código piscar led arduino, programa de piscar arduino, exemplo de piscar arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: b0a7d076-d580-4686-9f7d-c0712750b615
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 5bf8e4ae88e070aeacf34bfc43b8d2daeeb1a2fa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-deploy-hello-blink-application"></a><span data-ttu-id="3253c-105">Criar e implantar o aplicativo de intermitência hello</span><span class="sxs-lookup"><span data-stu-id="3253c-105">Create and deploy hello blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="3253c-106">O que você fará</span><span class="sxs-lookup"><span data-stu-id="3253c-106">What you will do</span></span>
<span data-ttu-id="3253c-107">Clonar um aplicativo de Arduino exemplo hello do GitHub e use Olá gulp ferramenta toodeploy Olá exemplo aplicativo tooyour Adafruit difusão M0 WiFi Arduino quadro.</span><span class="sxs-lookup"><span data-stu-id="3253c-107">Clone hello sample Arduino application from GitHub, and use hello gulp tool toodeploy hello sample application tooyour Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="3253c-108">Olá exemplo aplicativo pisca Olá GPIO 13 barod LEVOU a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="3253c-108">hello sample application blinks hello GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="3253c-109">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="3253c-109">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="3253c-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="3253c-110">What you will learn</span></span>
* <span data-ttu-id="3253c-111">Como toodeploy e execução Olá aplicativo de exemplo em seu quadro Arduino.</span><span class="sxs-lookup"><span data-stu-id="3253c-111">How toodeploy and run hello sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="3253c-112">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="3253c-112">What you need</span></span>
<span data-ttu-id="3253c-113">Você deve ter concluído Olá seguintes operações com êxito:</span><span class="sxs-lookup"><span data-stu-id="3253c-113">You must have successfully completed hello following operations:</span></span>

* <span data-ttu-id="3253c-114">[Configurar seu dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="3253c-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="3253c-115">[Obter ferramentas Olá][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="3253c-115">[Get hello tools][get-the-tools]</span></span>

## <a name="open-hello-sample-application"></a><span data-ttu-id="3253c-116">Aplicativo de exemplo hello aberto</span><span class="sxs-lookup"><span data-stu-id="3253c-116">Open hello sample application</span></span>
<span data-ttu-id="3253c-117">Olá tooopen aplicativo de exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3253c-117">tooopen hello sample application, follow these steps:</span></span>

1. <span data-ttu-id="3253c-118">Clone o repositório de exemplo de saudação do GitHub executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3253c-118">Clone hello sample repository from GitHub by running hello following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="3253c-119">Abra o aplicativo de exemplo hello no código do Visual Studio executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="3253c-119">Open hello sample application in Visual Studio Code by running hello following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Estrutura do repositório][repo-structure]

<span data-ttu-id="3253c-121">Olá `app.ino` arquivo hello `app` subpasta é o arquivo de origem da chave de saudação que contém Olá código toocontrol Olá LED.</span><span class="sxs-lookup"><span data-stu-id="3253c-121">hello `app.ino` file in hello `app` subfolder is hello key source file that contains hello code toocontrol hello LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="3253c-122">Instalar dependências de aplicativos</span><span class="sxs-lookup"><span data-stu-id="3253c-122">Install application dependencies</span></span>
<span data-ttu-id="3253c-123">Instale bibliotecas de saudação e outros módulos, que é necessário para o aplicativo de exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3253c-123">Install hello libraries and other modules you need for hello sample application by running hello following command:</span></span>

```bash
npm install
```

## <a name="configure-hello-device-connection"></a><span data-ttu-id="3253c-124">Configurar conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="3253c-124">Configure hello device connection</span></span>
<span data-ttu-id="3253c-125">tooconfigure Olá conexão do dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="3253c-125">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="3253c-126">Obter a porta serial saudação do dispositivo Olá Olá CLI de descoberta do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="3253c-126">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="3253c-127">Você deve ver uma saída que é a seguir toohello semelhante e encontrar a porta COM hello usb para a sua placa Arduino: ![a descoberta de dispositivos][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="3253c-127">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="3253c-128">Arquivo hello abrir `config.json` em Olá pasta lição e adicionar valor Olá Olá encontrado número da porta COM:</span><span class="sxs-lookup"><span data-stu-id="3253c-128">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > <span data-ttu-id="3253c-130">Para a porta de saudação COM, na plataforma Windows, tem um formato de Olá `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="3253c-130">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="3253c-131">No macOS ou Ubuntu, começa com `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="3253c-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="3253c-132">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="3253c-132">Deploy and run hello sample application</span></span>
### <a name="install-hello-required-tools-for-your-arduino-board"></a><span data-ttu-id="3253c-133">Instalar as ferramentas de saudação necessários para seu quadro Arduino</span><span class="sxs-lookup"><span data-stu-id="3253c-133">Install hello required tools for your Arduino board</span></span>

<span data-ttu-id="3253c-134">Instale o hello Azure IoT Hub SDK para seu quadro Arduino executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3253c-134">Install hello Azure IoT Hub SDK for your Arduino board by running hello following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="3253c-135">Essa tarefa pode levar um longo tempo toocomplete, dependendo de sua conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="3253c-135">This task might take a long time toocomplete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="3253c-136">Saia do hello executando a instância de Arduino IDE quando você executar tarefas de gulp: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="3253c-136">Please exit hello running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-hello-sample-app"></a><span data-ttu-id="3253c-137">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="3253c-137">Deploy and run hello sample app</span></span>
<span data-ttu-id="3253c-138">Implantar e executar o aplicativo de exemplo hello executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="3253c-138">Deploy and run hello sample application by running hello following command:</span></span>

```bash
gulp run

# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-hello-app-works"></a><span data-ttu-id="3253c-139">Verifique se Olá aplicativo funciona</span><span class="sxs-lookup"><span data-stu-id="3253c-139">Verify hello app works</span></span>
<span data-ttu-id="3253c-140">Se você não vir Olá LED piscando, consulte Olá [guia de solução de problemas] [ troubleshooting-page] para problemas de toocommon de soluções.</span><span class="sxs-lookup"><span data-stu-id="3253c-140">If you don’t see hello LED blinking, see hello [troubleshooting guide][troubleshooting-page] for solutions toocommon problems.</span></span>

![LED piscando][led-blinking]

## <a name="summary"></a><span data-ttu-id="3253c-142">Resumo</span><span class="sxs-lookup"><span data-stu-id="3253c-142">Summary</span></span>
<span data-ttu-id="3253c-143">Instalar Olá necessárias ferramentas toowork com seu quadro Arduino e implantado uma saudação de quadro tooblink do exemplo aplicativo tooyour Arduino LED.</span><span class="sxs-lookup"><span data-stu-id="3253c-143">You've installed hello required tools toowork with your Arduino board and deployed a sample application tooyour Arduino board tooblink hello LED.</span></span> <span data-ttu-id="3253c-144">Você pode criar, implantar e executar outro aplicativo de exemplo que se conecta a seu quadro de Arduino tooAzure toosend de IoT Hub e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="3253c-144">You can now create, deploy, and run another sample application that connects your Arduino board tooAzure IoT Hub toosend and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="3253c-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3253c-145">Next steps</span></span>
<span data-ttu-id="3253c-146">[Obter Olá ferramentas do Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="3253c-146">[Get hello Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md