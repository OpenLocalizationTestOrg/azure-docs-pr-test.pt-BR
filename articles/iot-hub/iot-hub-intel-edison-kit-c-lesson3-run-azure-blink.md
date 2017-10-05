---
title: "Conectar o Intel Edison (C) ao IoT do Azure - Lição 3: enviar mensagens| Microsoft Docs"
description: Implante e execute um aplicativo de exemplo para o Intel Edison que envia mensagens ao seu Hub IoT e pisque o LED.
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "serviço de nuvem iot, enviar dados para nuvem arduino"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-intel-edison-kit-c-get-started
ms.assetid: 12672b64-795a-4dfc-86fd-df53ed3eeef7
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d104618ebb37a19c83f161beceb5c71bc89bbb56
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="run-a-sample-application-to-send-device-to-cloud-messages"></a><span data-ttu-id="4626d-104">Executar um aplicativo de exemplo para enviar mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="4626d-104">Run a sample application to send device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="4626d-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="4626d-105">What you will do</span></span>
<span data-ttu-id="4626d-106">Esse artigo mostrará como implantar e executar um aplicativo de exemplo no Intel Edison que envia mensagens ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4626d-106">This article will show you how to deploy and run a sample application on Intel Edison that sends messages to your IoT hub.</span></span> <span data-ttu-id="4626d-107">Se você tiver problemas, procure por soluções na [página de solução de problemas][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="4626d-107">If you have any problems, look for solutions on the [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4626d-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="4626d-108">What you will learn</span></span>
<span data-ttu-id="4626d-109">Você aprenderá a usar a ferramenta gulp para implantar e executar o aplicativo de exemplo C no Edison.</span><span class="sxs-lookup"><span data-stu-id="4626d-109">You will learn how to use the gulp tool to deploy and run the sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4626d-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="4626d-110">What you need</span></span>
* <span data-ttu-id="4626d-111">Antes de iniciar essa tarefa, você precisa ter concluído com sucesso [Criar um aplicativo de funções e uma conta de armazenamento do Azure para processar e armazenar mensagens do Hub IoT][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="4626d-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account to process and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="4626d-112">Obter as cadeias de conexão do dispositivo e do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="4626d-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="4626d-113">A cadeia de conexão do dispositivo é usada para conectar o Edison ao Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4626d-113">The device connection string is used to connect Edison to your IoT hub.</span></span> <span data-ttu-id="4626d-114">A cadeia de conexão do Hub IoT é usada para conectar o Hub IoT à identidade de dispositivo que representa o Edison no Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4626d-114">The IoT hub connection string is used to connect your IoT hub to the device identity that represents Edison in the IoT hub.</span></span>

* <span data-ttu-id="4626d-115">Liste todos os Hubs IoT no seu grupo de recursos executando o seguinte comando da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="4626d-115">List all your IoT hubs in your resource group by running the following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="4626d-116">Use `iot-sample` como o valor de `{resource group name}` se não tiver alterado o valor.</span><span class="sxs-lookup"><span data-stu-id="4626d-116">Use `iot-sample` as the value of `{resource group name}` if you didn't change the value.</span></span>

* <span data-ttu-id="4626d-117">Obtenha a cadeia de conexão do hub IoT executando o seguinte comando da CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="4626d-117">Get the IoT hub connection string by running the following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="4626d-118">`{my hub name}` é o nome que você especificou quando criou o Hub IoT e registrou o Edison.</span><span class="sxs-lookup"><span data-stu-id="4626d-118">`{my hub name}` is the name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="4626d-119">Obtenha a cadeia de conexão do dispositivo executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4626d-119">Get the device connection string by running the following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="4626d-120">Use `myinteledison` como o valor de `{device id}` se não tiver alterado o valor.</span><span class="sxs-lookup"><span data-stu-id="4626d-120">Use `myinteledison` as the value of `{device id}` if you didn't change the value.</span></span>

## <a name="configure-the-device-connection"></a><span data-ttu-id="4626d-121">Configurar a conexão do dispositivo</span><span class="sxs-lookup"><span data-stu-id="4626d-121">Configure the device connection</span></span>
1. <span data-ttu-id="4626d-122">Inicialize o arquivo de configuração executando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="4626d-122">Initialize the configuration file by running the following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > <span data-ttu-id="4626d-123">Execute **gulp install-tools** e também, se você ainda não fez isso na Lição 1.</span><span class="sxs-lookup"><span data-stu-id="4626d-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="4626d-124">Abra o arquivo de configuração `config-edison.json` do dispositivo no Visual Studio Code executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4626d-124">Open the device configuration file `config-edison.json` in Visual Studio Code by running the following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. <span data-ttu-id="4626d-126">Faça as seguintes substituições no arquivo `config-edison.json`:</span><span class="sxs-lookup"><span data-stu-id="4626d-126">Make the following replacements in the `config-edison.json` file:</span></span>

   * <span data-ttu-id="4626d-127">Substitua **[nome de host ou endereço IP do dispositivo]** pelo endereço IP do dispositivo que você marcou quando configurou seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4626d-127">Replace **[device hostname or IP address]** with the device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="4626d-128">Substitua **[cadeia de conexão do dispositivo IoT]** pelo `device connection string` que você obteve.</span><span class="sxs-lookup"><span data-stu-id="4626d-128">Replace **[IoT device connection string]** with the `device connection string` you obtained.</span></span>
   * <span data-ttu-id="4626d-129">Substitua **[cadeia de conexão do hub IoT]** pelo `iot hub connection string` que você obteve.</span><span class="sxs-lookup"><span data-stu-id="4626d-129">Replace **[IoT hub connection string]** with the `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="4626d-130">Você não precisa do `azure_storage_connection_string` neste artigo.</span><span class="sxs-lookup"><span data-stu-id="4626d-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="4626d-131">Mantenha como está.</span><span class="sxs-lookup"><span data-stu-id="4626d-131">Keep it as is.</span></span>

## <a name="deploy-and-run-the-sample-application"></a><span data-ttu-id="4626d-132">Implantar e executar o aplicativo de exemplo</span><span class="sxs-lookup"><span data-stu-id="4626d-132">Deploy and run the sample application</span></span>
<span data-ttu-id="4626d-133">Implante e execute o aplicativo de exemplo no Edison executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4626d-133">Deploy and run the sample application on Edison by running the following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-the-sample-application-works"></a><span data-ttu-id="4626d-134">Verificar se o aplicativo de exemplo funciona</span><span class="sxs-lookup"><span data-stu-id="4626d-134">Verify that the sample application works</span></span>
<span data-ttu-id="4626d-135">Você deve ver o LED que está conectado ao Edison piscar a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="4626d-135">You should see the LED that is connected to Edison blinking every two seconds.</span></span> <span data-ttu-id="4626d-136">Sempre que o LED pisca, o aplicativo de exemplo envia uma mensagem ao hub IoT e verifica se a mensagem foi enviada com êxito para o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4626d-136">Every time the LED blinks, the sample application sends a message to your IoT hub and verifies that the message has been successfully sent to your IoT hub.</span></span> <span data-ttu-id="4626d-137">Além disso, cada mensagem recebida pelo Hub IoT é impressa na janela do console.</span><span class="sxs-lookup"><span data-stu-id="4626d-137">In addition, each message received by the IoT hub is printed in the console window.</span></span> <span data-ttu-id="4626d-138">O aplicativo de exemplo é encerrado automaticamente após o envio de 20 mensagens.</span><span class="sxs-lookup"><span data-stu-id="4626d-138">The sample application terminates automatically after sending 20 messages.</span></span>

![Exemplo de aplicativo com mensagens enviadas e recebidas][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="4626d-140">Resumo</span><span class="sxs-lookup"><span data-stu-id="4626d-140">Summary</span></span>
<span data-ttu-id="4626d-141">Você implantou e executou o novo aplicativo de exemplo de piscar no Edison para enviar mensagens do dispositivo para a nuvem para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4626d-141">You've deployed and run the new blink sample application on Edison to send device-to-cloud messages to your IoT hub.</span></span> <span data-ttu-id="4626d-142">Agora, você monitorara suas mensagens conforme elas são gravadas na conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="4626d-142">You now monitor your messages as they are written to the storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4626d-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4626d-143">Next steps</span></span>
<span data-ttu-id="4626d-144">[Ler mensagens persistentes no Armazenamento do Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="4626d-144">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md