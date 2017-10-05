---
title: "Conectar o Arduino ao IoT do Azure - Lição 1: implantar aplicativo | Microsoft Docs"
description: Clone o aplicativo Arduino de exemplo do GitHub e execute o gulp para implantar esse aplicativo no Adafruit Feather M0 WiFi. Este aplicativo de exemplo pisca o GPIO
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
ms.openlocfilehash: 4431808ac6182d194e841c087c8f89f1a12b1911
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-and-deploy-the-blink-application"></a><span data-ttu-id="38805-105">Criar e implantar o aplicativo de piscar</span><span class="sxs-lookup"><span data-stu-id="38805-105">Create and deploy the blink application</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="38805-106">O que você fará</span><span class="sxs-lookup"><span data-stu-id="38805-106">What you will do</span></span>
<span data-ttu-id="38805-107">Clonar o aplicativo Arduino de exemplo do GitHub e usar a ferramenta gulp para implantar esse aplicativo de exemplo na placa Adafruit Feather M0 WiFi Arduino.</span><span class="sxs-lookup"><span data-stu-id="38805-107">Clone the sample Arduino application from GitHub, and use the gulp tool to deploy the sample application to your Adafruit Feather M0 WiFi Arduino board.</span></span> <span data-ttu-id="38805-108">O aplicativo de exemplo pisca o LED conectado à placa no GPIO núm. 13 a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="38805-108">The sample application blinks the GPIO #13 on-barod LED every two seconds.</span></span>

<span data-ttu-id="38805-109">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting-page].</span><span class="sxs-lookup"><span data-stu-id="38805-109">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting-page].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="38805-110">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="38805-110">What you will learn</span></span>
* <span data-ttu-id="38805-111">Como implantar e executar o aplicativo de exemplo em sua placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="38805-111">How to deploy and run the sample application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="38805-112">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="38805-112">What you need</span></span>
<span data-ttu-id="38805-113">Você deve ter concluído com sucesso as seções a seguir:</span><span class="sxs-lookup"><span data-stu-id="38805-113">You must have successfully completed the following operations:</span></span>

* <span data-ttu-id="38805-114">[Configurar seu dispositivo][configure-your-device]</span><span class="sxs-lookup"><span data-stu-id="38805-114">[Configure your device][configure-your-device]</span></span>
* <span data-ttu-id="38805-115">[Obter as ferramentas][get-the-tools]</span><span class="sxs-lookup"><span data-stu-id="38805-115">[Get the tools][get-the-tools]</span></span>

## <a name="open-the-sample-application"></a><span data-ttu-id="38805-116">Abrir o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="38805-116">Open the sample application</span></span>
<span data-ttu-id="38805-117">Para abrir o aplicativo de exemplo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="38805-117">To open the sample application, follow these steps:</span></span>

1. <span data-ttu-id="38805-118">Clone o repositório de exemplo do GitHub executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="38805-118">Clone the sample repository from GitHub by running the following command:</span></span>

   ```bash
   git clone https://github.com/Azure-Samples/iot-hub-c-feather-m0-getting-started.git
   ```
2. <span data-ttu-id="38805-119">Abra o aplicativo de exemplo no Visual Studio Code, executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="38805-119">Open the sample application in Visual Studio Code by running the following commands:</span></span>

   ```bash
   cd iot-hub-c-feather-m0-getting-started
   cd Lesson1
   code .
   ```

   ![Estrutura do repositório][repo-structure]

<span data-ttu-id="38805-121">O arquivo `app.ino` na subpasta `app` é o arquivo de origem principal que contém o código para controlar o LED.</span><span class="sxs-lookup"><span data-stu-id="38805-121">The `app.ino` file in the `app` subfolder is the key source file that contains the code to control the LED.</span></span>

### <a name="install-application-dependencies"></a><span data-ttu-id="38805-122">Instalar dependências de aplicativos</span><span class="sxs-lookup"><span data-stu-id="38805-122">Install application dependencies</span></span>
<span data-ttu-id="38805-123">Instale as bibliotecas e outros módulos necessários para o aplicativo de exemplo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="38805-123">Install the libraries and other modules you need for the sample application by running the following command:</span></span>

```bash
npm install
```

## <a name="configure-the-device-connection"></a><span data-ttu-id="38805-124">Configurar a conexão do dispositivo</span><span class="sxs-lookup"><span data-stu-id="38805-124">Configure the device connection</span></span>
<span data-ttu-id="38805-125">Para configurar a conexão do dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="38805-125">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="38805-126">Obter a porta serial do dispositivo com a CLI de descoberta de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="38805-126">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="38805-127">Você deve ver uma saída semelhante à seguinte e encontrar a porta COM USB para sua placa Arduino: ![Descoberta de dispositivos][device-discovery]</span><span class="sxs-lookup"><span data-stu-id="38805-127">You should see an output that is similar to the following and find the usb COM port for your Arduino board: ![Device discovery][device-discovery]</span></span>

2. <span data-ttu-id="38805-128">Abra o arquivo `config.json` na pasta da lição e adicione o valor do número da porta COM encontrado:</span><span class="sxs-lookup"><span data-stu-id="38805-128">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```
   ![config.json][config-json]
   > [!NOTE]
   > <span data-ttu-id="38805-130">Para a porta COM, na plataforma Windows, ele tem o formato de `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="38805-130">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="38805-131">No macOS ou Ubuntu, começa com `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="38805-131">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="38805-132">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="38805-132">Deploy and run the sample application</span></span>
### <a name="install-the-required-tools-for-your-arduino-board"></a><span data-ttu-id="38805-133">Instalar as ferramentas necessárias para sua placa Arduino</span><span class="sxs-lookup"><span data-stu-id="38805-133">Install the required tools for your Arduino board</span></span>

<span data-ttu-id="38805-134">Instale o SDK do Hub IoT do Azure na placa Arduino executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="38805-134">Install the Azure IoT Hub SDK for your Arduino board by running the following command:</span></span>

```bash
gulp install-tools
```

<span data-ttu-id="38805-135">Essa tarefa pode levar muito tempo para ser concluída, dependendo da sua conexão de rede.</span><span class="sxs-lookup"><span data-stu-id="38805-135">This task might take a long time to complete, depending on your network connection.</span></span>

> [!NOTE]
> <span data-ttu-id="38805-136">Saia da instância em execução do IDE do Arduino ao executar tarefas gulp: `install-tools`, `run`.</span><span class="sxs-lookup"><span data-stu-id="38805-136">Please exit the running Arduino IDE instance when running gulp tasks: `install-tools`, `run`.</span></span>

### <a name="deploy-and-run-the-sample-app"></a><span data-ttu-id="38805-137">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="38805-137">Deploy and run the sample app</span></span>
<span data-ttu-id="38805-138">Implantar e executar o aplicativo de exemplo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="38805-138">Deploy and run the sample application by running the following command:</span></span>

```bash
gulp run

# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

### <a name="verify-the-app-works"></a><span data-ttu-id="38805-139">Verificar se o aplicativo funciona</span><span class="sxs-lookup"><span data-stu-id="38805-139">Verify the app works</span></span>
<span data-ttu-id="38805-140">Se você não vir o LED piscar, consulte o [guia de solução de problemas][troubleshooting-page] para ver soluções de problemas comuns.</span><span class="sxs-lookup"><span data-stu-id="38805-140">If you don’t see the LED blinking, see the [troubleshooting guide][troubleshooting-page] for solutions to common problems.</span></span>

![LED piscando][led-blinking]

## <a name="summary"></a><span data-ttu-id="38805-142">Resumo</span><span class="sxs-lookup"><span data-stu-id="38805-142">Summary</span></span>
<span data-ttu-id="38805-143">Você instalou as ferramentas necessárias para trabalhar com a placa Arduino e implantou um aplicativo de exemplo para a placa Arduino para piscar o LED.</span><span class="sxs-lookup"><span data-stu-id="38805-143">You've installed the required tools to work with your Arduino board and deployed a sample application to your Arduino board to blink the LED.</span></span> <span data-ttu-id="38805-144">Agora, você pode criar, implantar e executar outro aplicativo de exemplo que conecta sua placa Arduino ao Hub IoT do Azure para enviar e receber mensagens.</span><span class="sxs-lookup"><span data-stu-id="38805-144">You can now create, deploy, and run another sample application that connects your Arduino board to Azure IoT Hub to send and receive messages.</span></span>

## <a name="next-steps"></a><span data-ttu-id="38805-145">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="38805-145">Next steps</span></span>
<span data-ttu-id="38805-146">[Obter as ferramentas do Azure][get-the-azure-tools]</span><span class="sxs-lookup"><span data-stu-id="38805-146">[Get the Azure tools][get-the-azure-tools]</span></span>

<!-- Images and links -->

[troubleshooting-page]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[configure-your-device]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-configure-your-device.md
[get-the-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-get-the-tools-win32.md
[repo-structure]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-blink-arduino-mac.png
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[led-blinking]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/led_blinking.png
[get-the-azure-tools]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson2-get-azure-tools-win32.md