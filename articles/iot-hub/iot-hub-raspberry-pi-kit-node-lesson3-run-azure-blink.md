---
title: "Conectar o Raspberry Pi (Nó) ao IoT do Azure - Lição 3: executar exemplo | Microsoft Docs"
description: Implante e execute um aplicativo de exemplo para o Raspberry Pi 3 que envie mensagens ao seu Hub IoT e pisque o LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: pi de nuvem do led de piscar, led de piscar da nuvem
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-raspberry-pi-kit-node-get-started
ms.assetid: 427d8e5e-8af8-4249-8607-44edc90a4972
ms.service: iot-hub
ms.devlang: node
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 1c03283ee276a954f822d6eca5f0a3d5f93ec64b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="088ce-104">Executar um aplicativo de exemplo para enviar mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="088ce-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="088ce-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="088ce-105">What you will do</span></span>
<span data-ttu-id="088ce-106">Esse artigo mostrará como implantar e executar um aplicativo de exemplo para seu Raspberry Pi 3 que envie mensagens ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="088ce-106">This article will show you how to deploy and run a sample application on Raspberry Pi 3 that sends messages to your IoT hub.</span></span> <span data-ttu-id="088ce-107">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="088ce-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-raspberry-pi-kit-node-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="088ce-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="088ce-108">What you will learn</span></span>
<span data-ttu-id="088ce-109">Você aprenderá como usar a ferramenta gulp para implantar e executar o aplicativo de exemplo Node.js no Pi.</span><span class="sxs-lookup"><span data-stu-id="088ce-109">You will learn how to use the gulp tool to deploy and run the sample Node.js application on Pi.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="088ce-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="088ce-110">What you need</span></span>
* <span data-ttu-id="088ce-111">Antes de iniciar essa tarefa, você deve ter concluído com sucesso [Criar um aplicativo de funções do Azure e uma conta de armazenamento para processar e armazenar mensagens do Hub IoT](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span><span class="sxs-lookup"><span data-stu-id="088ce-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages](iot-hub-raspberry-pi-kit-node-lesson3-deploy-resource-manager-template.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="088ce-112">Obter as cadeias de conexão do dispositivo e do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="088ce-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="088ce-113">A cadeia de conexão do dispositivo é usada pelo seu Pi para conectar ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="088ce-113">The device connection string is used by your Pi to connect to your IoT hub.</span></span> <span data-ttu-id="088ce-114">A cadeia de conexão do Hub IoT é usada para se conectar ao Registro de identidade em seu Hub IoT para gerenciar os dispositivos que têm permissão para se conectar ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="088ce-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span> 

* <span data-ttu-id="088ce-115">Liste todos os Hubs IoT no seu grupo de recursos executando o seguinte comando da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="088ce-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="088ce-116">Use `iot-sample` como o valor de `{resource group name}` se não tiver alterado o valor.</span><span class="sxs-lookup"><span data-stu-id="088ce-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="088ce-117">Obtenha a cadeia de conexão do hub IoT executando o seguinte comando da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="088ce-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name} -g iot-sample
```

<span data-ttu-id="088ce-118">`{my hub name}` é o nome que você especificou quando criou o Hub IoT e registrou o Pi.</span><span class="sxs-lookup"><span data-stu-id="088ce-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Pi.</span></span>

* <span data-ttu-id="088ce-119">Obtenha a cadeia de conexão do dispositivo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="088ce-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myraspberrypi -g iot-sample
```

<span data-ttu-id="088ce-120">Use `myraspberrypi` como o valor de `{device id}` se não tiver alterado o valor.</span><span class="sxs-lookup"><span data-stu-id="088ce-120">Use `myraspberrypi` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="088ce-121">Configurar a conexão do dispositivo</span><span class="sxs-lookup"><span data-stu-id="088ce-121">Configure the device connection</span></span>
1. <span data-ttu-id="088ce-122">Inicialize o arquivo de configuração executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="088ce-122">Initialize the configuration file by running the following commands:</span></span>
   
   ```bash
   npm install
   gulp init
   ```
2. <span data-ttu-id="088ce-123">Abra o arquivo de configuração `config-raspberrypi.json` do dispositivo no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="088ce-123">Open the device configuration file `config-raspberrypi.json` in Visual Studio Code by running the following command:</span></span>
   
   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-raspberrypi.json
  
   # For macOS or Ubuntu
   code ~/.iot-hub-getting-started/config-raspberrypi.json
   ```
  
   ![config.json](media/iot-hub-raspberry-pi-lessons/lesson3/config.png)
3. <span data-ttu-id="088ce-125">Faça as seguintes substituições no arquivo `config-raspberrypi.json`:</span><span class="sxs-lookup"><span data-stu-id="088ce-125">Make the following replacements in the `config-raspberrypi.json` file:</span></span>
   
   * <span data-ttu-id="088ce-126">Substitua **[nome do host ou endereço IP do dispositivo]** pelo endereço IP ou o nome de host do dispositivo que você obteve de `device-discovery-cli` ou pelo valor herdado quando você configurou o seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="088ce-126">Replace **[device hostname or IP address]** with the device IP address or host name you got from `device-discovery-cli` or with the value inherited when you configured your device.</span></span>
   * <span data-ttu-id="088ce-127">Substitua **[cadeia de conexão do dispositivo IoT]** pelo `device connection string` que você obteve.</span><span class="sxs-lookup"><span data-stu-id="088ce-127">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="088ce-128">Substitua **[cadeia de conexão do hub IoT]** pelo `iot hub connection string` que você obteve.</span><span class="sxs-lookup"><span data-stu-id="088ce-128">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

<span data-ttu-id="088ce-129">Atualize o arquivo `config-raspberrypi.json` para que você possa implantar o aplicativo de exemplo de seu computador.</span><span class="sxs-lookup"><span data-stu-id="088ce-129">Update the `config-raspberrypi.json` file so that you can deploy the sample application from your computer.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="088ce-130">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="088ce-130">Deploy and run the sample application</span></span>
<span data-ttu-id="088ce-131">Implante e execute o aplicativo de exemplo no Pi executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="088ce-131">Deploy and run the sample application on Pi by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="088ce-132">Verificar se o aplicativo de exemplo funciona</span><span class="sxs-lookup"><span data-stu-id="088ce-132">Verify that the sample application works</span></span>
<span data-ttu-id="088ce-133">Você deve ver o LED que está conectado ao Pi piscar a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="088ce-133">You should see the LED that is connected to Pi blinking every two seconds.</span></span> <span data-ttu-id="088ce-134">Sempre que o LED pisca, o aplicativo de exemplo envia uma mensagem ao hub IoT e verifica se a mensagem foi enviada com êxito para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="088ce-134">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="088ce-135">Além disso, cada mensagem recebida pelo Hub IoT é impressa na janela do console.</span><span class="sxs-lookup"><span data-stu-id="088ce-135">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="088ce-136">O aplicativo de exemplo é encerrado automaticamente após o envio de 20 mensagens.</span><span class="sxs-lookup"><span data-stu-id="088ce-136">The sample application terminates automatically after sending 20 messages.</span></span>

![Exemplo de aplicativo com mensagens enviadas e recebidas](media/iot-hub-raspberry-pi-lessons/lesson3/gulp_run.png)

## <a name="summary"></a><span data-ttu-id="088ce-138">Resumo</span><span class="sxs-lookup"><span data-stu-id="088ce-138">Summary</span></span>
<span data-ttu-id="088ce-139">Você implantou e executou o novo aplicativo de exemplo de piscar no Pi para enviar mensagens do dispositivo para a nuvem para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="088ce-139">You've deployed and run the new blink sample application on Pi to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="088ce-140">Você pode monitorar suas mensagens conforme elas são gravadas na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="088ce-140">You can now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="088ce-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="088ce-141">Next steps</span></span>
[<span data-ttu-id="088ce-142">Ler mensagens mantidas no Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="088ce-142">Read messages persisted in Azure Storage</span></span>](iot-hub-raspberry-pi-kit-node-lesson3-read-table-storage.md)

