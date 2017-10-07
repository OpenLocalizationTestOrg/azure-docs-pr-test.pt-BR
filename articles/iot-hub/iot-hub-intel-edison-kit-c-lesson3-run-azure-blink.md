---
title: "Connect Intel Edison (C) tooAzure IoT – lição 3: enviar mensagens | Microsoft Docs"
description: "Implantar e executar um aplicativo de exemplo tooIntel Edison que envia o hub de IoT tooyour mensagens e pisca Olá LED."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "serviço de nuvem de IOT arduino enviar dados toocloud"
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
ms.openlocfilehash: 83615335027cc792b89d3894578fc3f7a55e5c37
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-a-sample-application-toosend-device-to-cloud-messages"></a><span data-ttu-id="16ee1-104">Executar um toosend do aplicativo de exemplo mensagens de dispositivo para nuvem</span><span class="sxs-lookup"><span data-stu-id="16ee1-104">Run a sample application toosend device-to-cloud messages</span></span>
## <a name="what-you-will-do"></a><span data-ttu-id="16ee1-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="16ee1-105">What you will do</span></span>
<span data-ttu-id="16ee1-106">Este artigo mostra como toodeploy e execute um aplicativo de exemplo no Intel Edison que envia mensagens tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="16ee1-106">This article will show you how toodeploy and run a sample application on Intel Edison that sends messages tooyour IoT hub.</span></span> <span data-ttu-id="16ee1-107">Se você tiver problemas, procure por soluções em Olá [página de solução][troubleshooting].</span><span class="sxs-lookup"><span data-stu-id="16ee1-107">If you have any problems, look for solutions on hello [troubleshooting page][troubleshooting].</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="16ee1-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="16ee1-108">What you will learn</span></span>
<span data-ttu-id="16ee1-109">Você saiba como Olá toouse gulp ferramenta toodeploy e executará o aplicativo de C do exemplo hello em Edison.</span><span class="sxs-lookup"><span data-stu-id="16ee1-109">You will learn how toouse hello gulp tool toodeploy and run hello sample C application on Edison.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="16ee1-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="16ee1-110">What you need</span></span>
* <span data-ttu-id="16ee1-111">Antes de começar essa tarefa, você deve concluir com êxito [criar um aplicativo de função do Azure e um armazenamento conta tooprocess e o repositório de IoT hub mensagens][process-and-store-iot-hub-messages].</span><span class="sxs-lookup"><span data-stu-id="16ee1-111">Before you start this task, you must have successfully completed [Create an Azure function app and a storage account tooprocess and store IoT hub messages][process-and-store-iot-hub-messages].</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="16ee1-112">Obter as cadeias de conexão do dispositivo e do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="16ee1-112">Get your IoT hub and device connection strings</span></span>
<span data-ttu-id="16ee1-113">cadeia de caracteres de conexão de dispositivo Olá é usado tooconnect hub de IoT tooyour Edison.</span><span class="sxs-lookup"><span data-stu-id="16ee1-113">hello device connection string is used tooconnect Edison tooyour IoT hub.</span></span> <span data-ttu-id="16ee1-114">Olá a cadeia de caracteres de conexão de hub IoT é usado tooconnect sua identidade de dispositivo de toohello de hub IoT representando Edison no hub IoT de saudação.</span><span class="sxs-lookup"><span data-stu-id="16ee1-114">hello IoT hub connection string is used tooconnect your IoT hub toohello device identity that represents Edison in hello IoT hub.</span></span>

* <span data-ttu-id="16ee1-115">Liste todos os seus hubs de IoT em seu grupo de recursos executando Olá após o comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="16ee1-115">List all your IoT hubs in your resource group by running hello following Azure CLI command:</span></span>

```bash
az iot hub list -g iot-sample --query [].name
```

<span data-ttu-id="16ee1-116">Use `iot-sample` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="16ee1-116">Use `iot-sample` as hello value of `{resource group name}` if you didn't change hello value.</span></span>

* <span data-ttu-id="16ee1-117">Obter cadeia de caracteres de conexão do hello IoT hub executando Olá após o comando CLI do Azure:</span><span class="sxs-lookup"><span data-stu-id="16ee1-117">Get hello IoT hub connection string by running hello following Azure CLI command:</span></span>

```bash
az iot hub show-connection-string --name {my hub name}
```

<span data-ttu-id="16ee1-118">`{my hub name}`é o nome de saudação que você especificou ao criar o hub IoT e registrado Edison.</span><span class="sxs-lookup"><span data-stu-id="16ee1-118">`{my hub name}` is hello name that you specified when you created your IoT hub and registered Edison.</span></span>

* <span data-ttu-id="16ee1-119">Obter cadeia de caracteres de conexão de dispositivo Olá executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="16ee1-119">Get hello device connection string by running hello following command:</span></span>

```bash
az iot device show-connection-string --hub-name {my hub name} --device-id myinteledison
```

<span data-ttu-id="16ee1-120">Use `myinteledison` como valor de saudação do `{device id}` se você não alterar o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="16ee1-120">Use `myinteledison` as hello value of `{device id}` if you didn't change hello value.</span></span>

## <a name="configure-hello-device-connection"></a><span data-ttu-id="16ee1-121">Configurar conexão do dispositivo Olá</span><span class="sxs-lookup"><span data-stu-id="16ee1-121">Configure hello device connection</span></span>
1. <span data-ttu-id="16ee1-122">Inicialize o arquivo de configuração de saudação executando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="16ee1-122">Initialize hello configuration file by running hello following commands:</span></span>

   ```bash
   npm install
   gulp init
   ```
   > [!NOTE]
   > <span data-ttu-id="16ee1-123">Execute **gulp install-tools** e também, se você ainda não fez isso na Lição 1.</span><span class="sxs-lookup"><span data-stu-id="16ee1-123">Run **gulp install-tools** as well, if you haven't done it in Lesson 1.</span></span>

2. <span data-ttu-id="16ee1-124">Arquivo de configuração de dispositivo aberto Olá `config-edison.json` no código do Visual Studio executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="16ee1-124">Open hello device configuration file `config-edison.json` in Visual Studio Code by running hello following command:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-edison.json

   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-edison.json
   ```

   ![config.json](media/iot-hub-intel-edison-lessons/lesson3/config.png)

3. <span data-ttu-id="16ee1-126">Verifique Olá substituições em Olá a seguir `config-edison.json` arquivo:</span><span class="sxs-lookup"><span data-stu-id="16ee1-126">Make hello following replacements in hello `config-edison.json` file:</span></span>

   * <span data-ttu-id="16ee1-127">Substituir **[nome de host do dispositivo ou endereço IP]** com endereço IP do dispositivo Olá marcado para baixo, quando você configurou seu dispositivo.</span><span class="sxs-lookup"><span data-stu-id="16ee1-127">Replace **[device hostname or IP address]** with hello device IP address you marked down when you configured your device.</span></span>
   * <span data-ttu-id="16ee1-128">Substituir **[cadeia de conexão de dispositivo IoT]** com hello `device connection string` obtidas.</span><span class="sxs-lookup"><span data-stu-id="16ee1-128">Replace **[IoT device connection string]** with hello `device connection string` you obtained.</span></span>
   * <span data-ttu-id="16ee1-129">Substituir **[cadeia de conexão de hub IoT]** com hello `iot hub connection string` obtidas.</span><span class="sxs-lookup"><span data-stu-id="16ee1-129">Replace **[IoT hub connection string]** with hello `iot hub connection string` you obtained.</span></span>

   > [!NOTE]
   > <span data-ttu-id="16ee1-130">Você não precisa do `azure_storage_connection_string` neste artigo.</span><span class="sxs-lookup"><span data-stu-id="16ee1-130">You don't need `azure_storage_connection_string` in this article.</span></span> <span data-ttu-id="16ee1-131">Mantenha como está.</span><span class="sxs-lookup"><span data-stu-id="16ee1-131">Keep it as is.</span></span>

## <a name="deploy-and-run-hello-sample-application"></a><span data-ttu-id="16ee1-132">Implantar e executar o aplicativo de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="16ee1-132">Deploy and run hello sample application</span></span>
<span data-ttu-id="16ee1-133">Implantar e executar o aplicativo de exemplo hello Edison executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="16ee1-133">Deploy and run hello sample application on Edison by running hello following command:</span></span>

```bash
gulp deploy && gulp run
```

## <a name="verify-that-hello-sample-application-works"></a><span data-ttu-id="16ee1-134">Verifique se o aplicativo de exemplo hello funciona</span><span class="sxs-lookup"><span data-stu-id="16ee1-134">Verify that hello sample application works</span></span>
<span data-ttu-id="16ee1-135">Você deve ver Olá LED que está conectada tooEdison piscando a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="16ee1-135">You should see hello LED that is connected tooEdison blinking every two seconds.</span></span> <span data-ttu-id="16ee1-136">Sempre Olá LED pisca, o aplicativo de exemplo hello envia um hub de IoT tooyour mensagem e verifica que essa mensagem de saudação enviada com êxito tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="16ee1-136">Every time hello LED blinks, hello sample application sends a message tooyour IoT hub and verifies that hello message has been successfully sent tooyour IoT hub.</span></span> <span data-ttu-id="16ee1-137">Além disso, cada mensagem recebida pelo hub IoT de saudação é impressa na janela de console hello.</span><span class="sxs-lookup"><span data-stu-id="16ee1-137">In addition, each message received by hello IoT hub is printed in hello console window.</span></span> <span data-ttu-id="16ee1-138">aplicativo de exemplo Hello encerra automaticamente após o envio de mensagens de 20.</span><span class="sxs-lookup"><span data-stu-id="16ee1-138">hello sample application terminates automatically after sending 20 messages.</span></span>

![Exemplo de aplicativo com mensagens enviadas e recebidas][sample-application-with-sent-and-received-messages]

## <a name="summary"></a><span data-ttu-id="16ee1-140">Resumo</span><span class="sxs-lookup"><span data-stu-id="16ee1-140">Summary</span></span>
<span data-ttu-id="16ee1-141">Você tiver implantado e execute o novo aplicativo de exemplo de intermitência Olá em Edison hub IoT do toosend mensagens de dispositivo para nuvem tooyour.</span><span class="sxs-lookup"><span data-stu-id="16ee1-141">You've deployed and run hello new blink sample application on Edison toosend device-to-cloud messages tooyour IoT hub.</span></span> <span data-ttu-id="16ee1-142">Agora você monitorar suas mensagens como eles são gravados toohello conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="16ee1-142">You now monitor your messages as they are written toohello storage account.</span></span>

## <a name="next-steps"></a><span data-ttu-id="16ee1-143">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="16ee1-143">Next steps</span></span>
<span data-ttu-id="16ee1-144">[Ler mensagens persistentes no Armazenamento do Azure][read-messages-persisted-in-azure-storage]</span><span class="sxs-lookup"><span data-stu-id="16ee1-144">[Read messages persisted in Azure Storage][read-messages-persisted-in-azure-storage]</span></span>
<!-- Images and links -->

[troubleshooting]: iot-hub-intel-edison-kit-c-troubleshooting.md
[process-and-store-iot-hub-messages]: iot-hub-intel-edison-kit-c-lesson3-deploy-resource-manager-template.md
[sample-application-with-sent-and-received-messages]: media/iot-hub-intel-edison-lessons/lesson3/gulp_run_c.png
[read-messages-persisted-in-azure-storage]: iot-hub-intel-edison-kit-c-lesson3-read-table-storage.md