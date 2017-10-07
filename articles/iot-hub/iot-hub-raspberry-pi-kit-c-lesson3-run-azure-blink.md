---
title: "Connect Raspberry PI (C) tooAzure IoT – lição 3: executar o exemplo | Microsoft Docs"
description: "Implantar e executar um aplicativo de exemplo tooRaspberry Pi 3 que envia o hub de IoT tooyour mensagens e pisca Olá LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: pi de nuvem do led de piscar, led de piscar da nuvem
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-c-get-started
ms.assetid: e38df29f-f77f-435f-9add-46814297564f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: c484beb2e2d3a3cf19f071f2ba87b9a4fe41c1fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="c3ca9-104">Executar um toosend do aplicativo de exemplo mensagens de dispositivo para nuvem</span><span class="sxs-lookup"><span data-stu-id="c3ca9-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="c3ca9-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="c3ca9-105">What you will do</span></span>
<span data-ttu-id="c3ca9-106">Este artigo mostra como toodeploy e execute um aplicativo de exemplo no framboesa Pi 3 que envia mensagens tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-106">This article will show you how toodeploy and run a sample application on Raspberry Pi 3 that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="c3ca9-107">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="c3ca9-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-raspberry-pi-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="c3ca9-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="c3ca9-108">What you will learn</span></span>
<span data-ttu-id="c3ca9-109">Você aprenderá como Olá toouse gulp toodeploy de ferramenta e execute o aplicativo de Node.js do exemplo hello em Pi.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-109">You will learn how toouse hello gulp tool toodeploy and run hello sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="c3ca9-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="c3ca9-110">What you need</span></span>
* <span data-ttu-id="c3ca9-111">Antes de começar essa tarefa, você deve concluir com êxito [criar um aplicativo de função do Azure e um armazenamento conta tooprocess e o repositório de IoT hub mensagens](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="c3ca9-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages](iot-hub-raspberry-pi-kit-c-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="c3ca9-112">Obter as cadeias de conexão do dispositivo e do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="c3ca9-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="c3ca9-113">cadeia de caracteres de conexão de dispositivo Olá é usada pelo seu hub IoT de tooyour de tooconnect de Pi.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-113">hello device connection string is used by your Pi tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="c3ca9-114">Olá cadeia de caracteres de conexão de hub IoT é um registro de identidade toohello tooconnect usados em dispositivos IoT hub toomanage Olá que são permitidas tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span> 

* <span data-ttu-id="c3ca9-115">Liste todos os seus hubs de IoT em seu grupo de recursos executando Olá após o comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="c3ca9-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="c3ca9-116">Use `iot-sample` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="c3ca9-117">Obter cadeia de caracteres de conexão do hello IoT hub executando Olá após o comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="c3ca9-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="c3ca9-118">`{my hub name}`é o nome de saudação que você especificou ao criar o hub IoT e registrado Pi.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="c3ca9-119">Obter cadeia de caracteres de conexão de dispositivo Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3ca9-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="c3ca9-120">Use `myraspberrypi` como valor de saudação do `{device id}` se você não alterar o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-120">Use `myraspberrypi` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="c3ca9-121">Configurar conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="c3ca9-121">Configure hello device connection</span></span>
1. <span data-ttu-id="c3ca9-122">Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3ca9-122">Initialize hello configuration file by running hello following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```

> [!NOTE]
> <span data-ttu-id="c3ca9-123">Execute **gulp install-tools** e também, se você ainda não fez isso na Lição 1.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="c3ca9-124">Arquivo de configuração de dispositivo aberto Olá `config-raspberrypi.json` no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3ca9-124">Open hello device configuration file `config-raspberrypi.json` in Visual Studio Code by running hello following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
   
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
   
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="c3ca9-126">Verifique Olá substituições em Olá a seguir `config-raspberrypi.json` arquivo:</span><span class="sxs-lookup"><span data-stu-id="c3ca9-126">Make hello following replacements in hello `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="c3ca9-127">Substituir **[nome de host do dispositivo ou endereço IP]** com o nome de host ou endereço IP de dispositivo do hello você obteve `device-discovery-cli` ou com valor de saudação herdadas quando você configurou seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-127">Replace **[device hostname or IP address]** with hello device IP address or host name you got from `device-discovery-cli` or with hello value inherited when you configured your device.</span></span>
   * <span data-ttu-id="c3ca9-128">Substituir **[cadeia de conexão de dispositivo IoT]** com hello `device connection string` obtidas.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="c3ca9-129">Substituir **[cadeia de conexão de hub IoT]** com hello `iot hub connection string` obtidas.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

> [!NOTE]
> <span data-ttu-id="c3ca9-130">Você não precisa do `azure_storage_connection_string` neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="c3ca9-131">Mantenha como está.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-131">Keep it as is.</span></span>

<span data-ttu-id="c3ca9-132">Saudação de atualização `config-raspberrypi.json` arquivos de forma que você pode implantar o aplicativo de exemplo hello do seu computador.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-132">Update hello `config-raspberrypi.json` file so that you can deploy hello sample application from your computer.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="c3ca9-133">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="c3ca9-133">Deploy and run hello sample application</span></span>
<span data-ttu-id="c3ca9-134">Implantar e executar o aplicativo de exemplo hello em Pi executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="c3ca9-134">Deploy and run hello sample application on Pi by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="c3ca9-135">Verifique se o aplicativo de exemplo hello funciona</span><span class="sxs-lookup"><span data-stu-id="c3ca9-135">Verify that hello sample application works</span></span>
<span data-ttu-id="c3ca9-136">Você deve ver Olá LED que está conectada tooPi piscando a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-136">You should see hello LED that is connected tooPi blinking every two seconds.</span></span> <span data-ttu-id="c3ca9-137">Sempre Olá LED pisca, o aplicativo de exemplo hello envia um hub de IoT tooyour mensagem e verifica que essa mensagem de saudação enviada com êxito tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-137">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="c3ca9-138">Além disso, cada mensagem recebida pelo hub IoT de saudação é impressa na janela de console hello.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-138">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="c3ca9-139">aplicativo de exemplo Hello encerra automaticamente após o envio de mensagens de 20.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-139">hello sample application terminates automatically after sending 20 messages.</span></span>

![Exemplo de aplicativo com mensagens enviadas e recebidas](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run_c.png)

## <a name="summary"></a><span data-ttu-id="c3ca9-141">Resumo</span><span class="sxs-lookup"><span data-stu-id="c3ca9-141">Summary</span></span>
<span data-ttu-id="c3ca9-142">Você tiver implantado e executar o novo aplicativo de exemplo de intermitência Olá no hub IoT do Pi toosend mensagens de dispositivo para nuvem tooyour.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-142">You've deployed and run hello new blink sample application on Pi toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="c3ca9-143">Agora você monitorar suas mensagens como eles são gravados toohello conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c3ca9-143">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3ca9-144">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c3ca9-144">Next steps</span></span>
[<span data-ttu-id="c3ca9-145">Ler mensagens mantidas no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="c3ca9-145">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-c-lesson3-read-table-storage.md)

