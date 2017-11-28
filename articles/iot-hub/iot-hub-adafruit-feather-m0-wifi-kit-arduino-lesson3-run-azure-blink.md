---
title: "Conectar o Arduino (C) ao IoT do Azure - Lição 3: executar exemplo | Microsoft Docs"
description: Implante e execute um aplicativo de exemplo no Adafruit Feather M0 WiFi que envia mensagens ao Hub IoT e pisca o LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "serviço de nuvem iot, enviar dados para nuvem arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-adafruit-feather-m0-wifi-kit-arduino-get-started
ms.assetid: 92cce319-2b17-4c9b-889d-deac959e3e7c
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 0c17fe74dbd78abca955f7789a1674ed6333367f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="4bc8c-104">Executar um aplicativo de exemplo para enviar mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="4bc8c-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="4bc8c-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="4bc8c-105">What you will do</span></span>
<span data-ttu-id="4bc8c-106">Este artigo mostrará como implantar e executar um aplicativo de exemplo em sua plava Adafruit Feather M0 WiFi Arduino que envia mensagens ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-106">This article will show you how to deploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages to your IoT hub.</span></span>

<span data-ttu-id="4bc8c-107">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="4bc8c-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4bc8c-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="4bc8c-108">What you will learn</span></span>
<span data-ttu-id="4bc8c-109">Você aprenderá a usar a ferramenta gulp para implantar e executar o aplicativo Arduino de exemplo em sua placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-109">You will learn how to use the gulp tool to deploy and run the sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4bc8c-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="4bc8c-110">What you need</span></span>
* <span data-ttu-id="4bc8c-111">Antes de iniciar essa tarefa, você precisa ter concluído com sucesso [Criar um aplicativo de funções e uma conta de armazenamento do Azure para processar e armazenar mensagens do Hub IoT][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="4bc8c-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="4bc8c-112">Obter as cadeias de conexão do dispositivo e do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="4bc8c-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="4bc8c-113">A cadeia de conexão do dispositivo é usada para conectar a placa Arduino ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-113">The device connection string is used to connect your Arduino board to your IoT hub.</span></span> <span data-ttu-id="4bc8c-114">A cadeia de conexão do Hub IoT é usada para conectar o Hub IoT à identidade de dispositivo que representa a placa Arduino no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents your Arduino board in the IoT hub.</span></span>

* <span data-ttu-id="4bc8c-115">Liste todos os Hubs IoT no seu grupo de recursos executando o seguinte comando da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="4bc8c-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="4bc8c-116">Use `iot-sample` como o valor de `{resource group name}` se não tiver alterado o valor.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="4bc8c-117">Obtenha a cadeia de conexão do hub IoT executando o seguinte comando da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="4bc8c-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="4bc8c-118">`{my hub name}` é o nome que você especificou quando criou o Hub IoT e registrou a placa Arduino.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="4bc8c-119">Obtenha a cadeia de conexão do dispositivo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4bc8c-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="4bc8c-120">Use `mym0wifi` como o valor de `{device id}` se não tiver alterado o valor.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-120">Use `mym0wifi` as the value of `{device id}` if you didn't change the value.</span></span>
## <a name="configure-the-device-connection"></a><span data-ttu-id="4bc8c-121">Configurar a conexão do dispositivo</span><span class="sxs-lookup"><span data-stu-id="4bc8c-121">Configure the device connection</span></span>
<span data-ttu-id="4bc8c-122">Para configurar a conexão do dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="4bc8c-122">To configure the device connection, follow these steps:</span></span>

1. <span data-ttu-id="4bc8c-123">Obter a porta serial do dispositivo com a CLI de descoberta de dispositivo:</span><span class="sxs-lookup"><span data-stu-id="4bc8c-123">Obtain the serial port of the device with the device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="4bc8c-124">Você deve ver uma saída semelhante à seguinte e encontrar a porta COM USB para sua placa Arduino:</span><span class="sxs-lookup"><span data-stu-id="4bc8c-124">You should see an output that is similar to the following and find the usb COM port for your Arduino board:</span></span>

   ![Descoberta de dispositivo][device-discovery]

2. <span data-ttu-id="4bc8c-126">Abra o arquivo `config.json` na pasta da lição e adicione o valor do número da porta COM encontrado:</span><span class="sxs-lookup"><span data-stu-id="4bc8c-126">Open the file `config.json` in the lesson folder and add the value of the found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="4bc8c-128">Para a porta COM, na plataforma Windows, ele tem o formato de `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-128">For the COM port, on Windows platform, it has the format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="4bc8c-129">No macOS ou Ubuntu, começa com `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="4bc8c-130">Inicialize o arquivo de configuração executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4bc8c-130">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="4bc8c-131">Abra o arquivo de configuração `config-arduino.json` do dispositivo no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4bc8c-131">Open the device configuration file `config-arduino.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="4bc8c-133">Faça as seguintes substituições no arquivo `config-arduino.json`:</span><span class="sxs-lookup"><span data-stu-id="4bc8c-133">Make the following replacements in the `config-arduino.json` file:</span></span>

   * <span data-ttu-id="4bc8c-134">Substitua **[SSID Wi-Fi]** por seu SSID Wi-Fi conectado à Internet.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected to the Internet.</span></span>
   * <span data-ttu-id="4bc8c-135">Substitua **[senha Wi-Fi]** pela senha de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="4bc8c-136">Remova a cadeia de caracteres se o Wi-Fi não precisar de uma senha.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-136">Remove the string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="4bc8c-137">Substitua **[cadeia de conexão do dispositivo IoT]** pelo `device connection string` que você obteve.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-137">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="4bc8c-138">Substitua **[cadeia de conexão do hub IoT]** pelo `iot hub connection string` que você obteve.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-138">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4bc8c-139">Você não precisa do `azure_storage_connection_string` neste artigo.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="4bc8c-140">Mantenha como está.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-140">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="4bc8c-141">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="4bc8c-141">Deploy and run the sample application</span></span>
<span data-ttu-id="4bc8c-142">Implante e execute o aplicativo de exemplo na sua placa do Arduino executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4bc8c-142">Deploy and run the sample application on your Arduino board by running the following command:</span></span>

```bash
gulp run
# You can monitor the serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="4bc8c-143">A tarefa de gulp padrão executa as tarefas `install-tools` e `run` em sequência.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-143">The default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="4bc8c-144">Quando [implantou o aplicativo de piscar][deployed-the-blink-app], você executou estas tarefas separadamente.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-144">When you [deployed the blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="4bc8c-145">Verificar se o aplicativo de exemplo funciona</span><span class="sxs-lookup"><span data-stu-id="4bc8c-145">Verify that the sample application works</span></span>
<span data-ttu-id="4bc8c-146">Você deve ver o LED do GPIO núm. 0 na placa piscando a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-146">You should see the GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="4bc8c-147">Sempre que o LED pisca, o aplicativo de exemplo envia uma mensagem ao hub IoT e verifica se a mensagem foi enviada com êxito para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-147">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="4bc8c-148">Além disso, cada mensagem recebida pelo Hub IoT é impressa na janela do console.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-148">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="4bc8c-149">O aplicativo de exemplo é encerrado automaticamente após o envio de 20 mensagens.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-149">The sample application terminates automatically after sending 20 messages.</span></span>

![Exemplo de aplicativo com mensagens enviadas e recebidas][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="4bc8c-151">Resumo</span><span class="sxs-lookup"><span data-stu-id="4bc8c-151">Summary</span></span>
<span data-ttu-id="4bc8c-152">Você implantou e executou o novo aplicativo de exemplo de piscar em sua placa Arduino para enviar mensagens do dispositivo para a nuvem para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-152">You've deployed and run the new blink sample application on your Arduino board to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="4bc8c-153">Agora, você monitorara suas mensagens conforme elas são gravadas na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4bc8c-153">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4bc8c-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4bc8c-154">Next steps</span></span>
<span data-ttu-id="4bc8c-155">[Ler mensagens persistentes no Armazenamento do Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="4bc8c-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md