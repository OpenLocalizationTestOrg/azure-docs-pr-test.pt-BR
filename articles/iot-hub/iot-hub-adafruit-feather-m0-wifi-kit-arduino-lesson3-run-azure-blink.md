---
title: "Connect Arduino (C) tooAzure IoT – lição 3: executar o exemplo | Microsoft Docs"
description: "Implantar e executar um aplicativo de exemplo tooAdafruit difusão M0 Wi-Fi que envia o hub de IoT tooyour mensagens e pisca Olá LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "serviço de nuvem de IOT arduino enviar dados toocloud"
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
ms.openlocfilehash: ddca015a3655f8a1a9de2a00e718ec0d28a5affb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="2838c-104">Executar um toosend do aplicativo de exemplo mensagens de dispositivo para nuvem</span><span class="sxs-lookup"><span data-stu-id="2838c-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="2838c-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="2838c-105">What you will do</span></span>
<span data-ttu-id="2838c-106">Este artigo mostra como toodeploy e execute um aplicativo de exemplo no seu Arduino de Wi-Fi Adafruit difusão M0 placa envia mensagens tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2838c-106">This article will show you how toodeploy and run a sample application on your Adafruit Feather M0 WiFi Arduino board that sends messages tooyour IoT hub.</span></span>

<span data-ttu-id="2838c-107">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="2838c-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="2838c-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="2838c-108">What you will learn</span></span>
<span data-ttu-id="2838c-109">Você aprenderá como Olá toouse gulp toodeploy de ferramenta e execute o aplicativo de Arduino exemplo hello em seu quadro Arduino.</span><span class="sxs-lookup"><span data-stu-id="2838c-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Arduino application on your Arduino board.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="2838c-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="2838c-110">What you need</span></span>
* <span data-ttu-id="2838c-111">Antes de começar essa tarefa, você deve concluir com êxito [criar um aplicativo de função do Azure e um armazenamento conta tooprocess e o repositório de IoT hub mensagens][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="2838c-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="2838c-112">Obter as cadeias de conexão do dispositivo e do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="2838c-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="2838c-113">Olá a cadeia de caracteres de conexão de dispositivo é usado tooconnect seu hub de IoT tooyour Arduino quadro.</span><span class="sxs-lookup"><span data-stu-id="2838c-113">hello device connection string is used tooconnect your Arduino board tooyour IoT hub.</span></span> <span data-ttu-id="2838c-114">cadeia de caracteres de conexão do Hello IoT hub é usado tooconnect sua identidade de dispositivo de toohello de hub IoT que representa o Arduino placa no hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="2838c-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents your Arduino board in hello IoT hub.</span></span>

* <span data-ttu-id="2838c-115">Liste todos os seus hubs de IoT em seu grupo de recursos executando Olá após o comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="2838c-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="2838c-116">Use `iot-sample` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="2838c-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="2838c-117">Obter cadeia de caracteres de conexão do hello IoT hub executando Olá após o comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="2838c-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="2838c-118">`{my hub name}`é o nome de saudação que você especificou ao criar o hub IoT e registrado seu quadro Arduino.</span><span class="sxs-lookup"><span data-stu-id="2838c-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered your Arduino board.</span></span>

* <span data-ttu-id="2838c-119">Obter cadeia de caracteres de conexão de dispositivo Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2838c-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id mym0wifi
```

<span data-ttu-id="2838c-120">Use `mym0wifi` como valor de saudação do `{device id}` se você não alterar o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="2838c-120">Use `mym0wifi` as hello value of `{device id}` if you didn't change hello value.</span></span>
## <a name="configure-hello-device-connection"></a><span data-ttu-id="2838c-121">Configurar conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="2838c-121">Configure hello device connection</span></span>
<span data-ttu-id="2838c-122">tooconfigure Olá conexão do dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="2838c-122">tooconfigure hello device connection, follow these steps:</span></span>

1. <span data-ttu-id="2838c-123">Obter a porta serial saudação do dispositivo Olá Olá CLI de descoberta do dispositivo:</span><span class="sxs-lookup"><span data-stu-id="2838c-123">Obtain hello serial port of hello device with hello device discovery cli:</span></span>

   ```bash
   devdisco list --usb
   ```

   <span data-ttu-id="2838c-124">Você deve ver uma saída que é a seguir toohello semelhante e encontrar hello usb porta COM para a sua placa Arduino:</span><span class="sxs-lookup"><span data-stu-id="2838c-124">You should see an output that is similar toohello following and find hello usb COM port for your Arduino board:</span></span>

   ![Descoberta de dispositivo][device-discovery]

2. <span data-ttu-id="2838c-126">Arquivo hello abrir `config.json` em Olá pasta lição e adicionar valor Olá Olá encontrado número da porta COM:</span><span class="sxs-lookup"><span data-stu-id="2838c-126">Open hello file `config.json` in hello lesson folder and add hello value of hello found COM port number:</span></span>

   ```json
   {
       "device_port" : "COM1"
   }
   ```

   ![config.json][config-json]

   > [!NOTE]
   > <span data-ttu-id="2838c-128">Para a porta de saudação COM, na plataforma Windows, tem um formato de Olá `COM1, COM2, ...`.</span><span class="sxs-lookup"><span data-stu-id="2838c-128">For hello COM port, on Windows platform, it has hello format of `COM1, COM2, ...`.</span></span> <span data-ttu-id="2838c-129">No macOS ou Ubuntu, começa com `/dev/`.</span><span class="sxs-lookup"><span data-stu-id="2838c-129">On macOS or Ubuntu, it starts with `/dev/`.</span></span>

3. <span data-ttu-id="2838c-130">Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2838c-130">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   gulp install-tools
   ```
4. <span data-ttu-id="2838c-131">Arquivo de configuração de dispositivo aberto Olá `config-arduino.json` no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2838c-131">Open hello device configuration file `config-arduino.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-arduino.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-arduino.json
   ```

   ![config-arduino.json][config-arduino-json]

5. <span data-ttu-id="2838c-133">Verifique Olá substituições em Olá a seguir `config-arduino.json` arquivo:</span><span class="sxs-lookup"><span data-stu-id="2838c-133">Make hello following replacements in hello `config-arduino.json` file:</span></span>

   * <span data-ttu-id="2838c-134">Substituir **[Wi-Fi SSID]** com o seu SSID de Wi-Fi que conectado toohello da Internet.</span><span class="sxs-lookup"><span data-stu-id="2838c-134">Replace **[Wi-Fi SSID]** with your Wi-Fi SSID that connected toohello Internet.</span></span>
   * <span data-ttu-id="2838c-135">Substitua **[senha Wi-Fi]** pela senha de Wi-Fi.</span><span class="sxs-lookup"><span data-stu-id="2838c-135">Replace **[Wi-Fi password]** with your Wi-Fi password.</span></span> <span data-ttu-id="2838c-136">Remova cadeia de caracteres de saudação se o Wi-Fi não exigir uma senha.</span><span class="sxs-lookup"><span data-stu-id="2838c-136">Remove hello string if your Wi-Fi doesn't require password.</span></span>
   * <span data-ttu-id="2838c-137">Substituir **[cadeia de conexão de dispositivo IoT]** com hello `device connection string` obtidas.</span><span class="sxs-lookup"><span data-stu-id="2838c-137">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="2838c-138">Substituir **[cadeia de conexão de hub IoT]** com hello `iot hub connection string` obtidas.</span><span class="sxs-lookup"><span data-stu-id="2838c-138">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="2838c-139">Você não precisa do `azure_storage_connection_string` neste artigo.</span><span class="sxs-lookup"><span data-stu-id="2838c-139">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="2838c-140">Mantenha como está.</span><span class="sxs-lookup"><span data-stu-id="2838c-140">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="2838c-141">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="2838c-141">Deploy and run hello sample application</span></span>
<span data-ttu-id="2838c-142">Implantar e executar o aplicativo de exemplo hello em seu quadro Arduino executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="2838c-142">Deploy and run hello sample application on your Arduino board by running hello following command:</span></span>

```bash
gulp run
# You can monitor hello serial port by running listen task:
gulp listen

# Or you can combine above two gulp tasks into one:
gulp run --listen
```

> [!NOTE]
> <span data-ttu-id="2838c-143">Olá padrão gulp tarefa é executada `install-tools` e `run` em sequência de tarefas.</span><span class="sxs-lookup"><span data-stu-id="2838c-143">hello default gulp task runs `install-tools` and `run` tasks sequentially.</span></span> <span data-ttu-id="2838c-144">Quando você [implantado Olá intermitência aplicativo][deployed-the-blink-app], você executou estas tarefas separadamente.</span><span class="sxs-lookup"><span data-stu-id="2838c-144">When you [deployed hello blink app][deployed-the-blink-app], you ran these tasks separately.</span></span>

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="2838c-145">Verifique se o aplicativo de exemplo hello funciona</span><span class="sxs-lookup"><span data-stu-id="2838c-145">Verify that hello sample application works</span></span>
<span data-ttu-id="2838c-146">Você deve ver o LED integrado de saudação GPIO #0 piscando cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="2838c-146">You should see hello GPIO #0 on-board LED blinking every two seconds.</span></span> <span data-ttu-id="2838c-147">Sempre Olá LED pisca, o aplicativo de exemplo hello envia um hub de IoT tooyour mensagem e verifica que essa mensagem de saudação enviada com êxito tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="2838c-147">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="2838c-148">Além disso, cada mensagem recebida pelo hub IoT de saudação é impressa na janela de console hello.</span><span class="sxs-lookup"><span data-stu-id="2838c-148">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="2838c-149">aplicativo de exemplo Hello encerra automaticamente após o envio de mensagens de 20.</span><span class="sxs-lookup"><span data-stu-id="2838c-149">hello sample application terminates automatically after sending 20 messages.</span></span>

![Exemplo de aplicativo com mensagens enviadas e recebidas][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="2838c-151">Resumo</span><span class="sxs-lookup"><span data-stu-id="2838c-151">Summary</span></span>
<span data-ttu-id="2838c-152">Você tiver implantado e execute o novo aplicativo de exemplo de intermitência Olá em seu hub IoT Arduino placa toosend mensagens de dispositivo para nuvem tooyour.</span><span class="sxs-lookup"><span data-stu-id="2838c-152">You've deployed and run hello new blink sample application on your Arduino board toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="2838c-153">Agora você monitorar suas mensagens como eles são gravados toohello conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="2838c-153">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="2838c-154">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="2838c-154">Next steps</span></span>
<span data-ttu-id="2838c-155">[Ler mensagens persistentes no Armazenamento do Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="2838c-155">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-deploy-resource-manager-template.md
[device-discovery]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/device_discovery.png
[config-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson1/vscode-config-mac.png
[config-arduino-json]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/config-arduino.png
[deployed-the-blink-app]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson1-deploy-blink-app.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-adafruit-feather-m0-wifi-lessons/lesson3/gulp_run_arduino.png
[read-messages-persisted-in-azure-storage]: iot-hub-adafruit-feather-m0-wifi-kit-arduino-lesson3-read-table-storage.md