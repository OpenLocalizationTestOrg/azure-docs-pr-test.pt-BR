---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 3: ler mensagens | Microsoft Docs"
description: "Execute um código de exemplo em suas mensagens de saudação do tooread de computador host do seu hub IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados em nuvem hello, coleta de dados de nuvem, o serviço de nuvem iot, iot dados"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: 5a6ec9c1-d83c-41c1-beaf-7c0d3395d77f
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: 540575724bb5cdac4db581a226d8a02a59004d8c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="fa6a8-104">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="fa6a8-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="fa6a8-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="fa6a8-105">What you will do</span></span>

- <span data-ttu-id="fa6a8-106">Execute código de exemplo no host do seu computador tooread mensagens de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="fa6a8-107">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="fa6a8-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="fa6a8-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="fa6a8-108">What you will learn</span></span>

<span data-ttu-id="fa6a8-109">Como Olá toouse gulp mensagens de tooread ferramenta do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="fa6a8-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="fa6a8-110">What you need</span></span>

- <span data-ttu-id="fa6a8-111">exemplo de dispositivo simulado Olá [configurar e executar uma nuvem de dispositivo simulado carregar o aplicativo de exemplo](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="fa6a8-111">hello simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="fa6a8-112">Obter as cadeias de conexão do dispositivo e do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="fa6a8-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="fa6a8-113">cadeia de caracteres de conexão de dispositivo Olá é usada pelo seu hub do dispositivo simulado tooconnect tooyour IoT.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-113">hello device connection string is used by your simulated device tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="fa6a8-114">Olá cadeia de caracteres de conexão de hub IoT é um registro de identidade toohello tooconnect usados em dispositivos IoT hub toomanage Olá que são permitidas tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="fa6a8-115">Liste todos os seus hubs de IoT em seu grupo de recursos executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa6a8-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="fa6a8-116">Use `iot-gateway` como valor de saudação do `{resource group name}` se você não alterá-lo.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="fa6a8-117">Obter cadeia de caracteres de conexão do hello IoT hub executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa6a8-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="fa6a8-118">`{my hub name}`é o nome de saudação que você especificou na lição 2.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="fa6a8-119">Configurar conexão do dispositivo Olá para o código de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="fa6a8-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="fa6a8-120">Atualizar IoT hub e dispositivo configurações de conexão em `config-azure.json` executando Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa6a8-120">Update IoT hub and device connection configurations in `config-azure.json` by performing hello following steps:</span></span>

1. <span data-ttu-id="fa6a8-121">Abra `config-azure.json` no código do Visual Studio executando Olá comando na janela do console a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa6a8-121">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="fa6a8-122">Verifique Olá substituições em Olá a seguir `config-azure.json` arquivo:</span><span class="sxs-lookup"><span data-stu-id="fa6a8-122">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![instantâneo de configuração do Azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="fa6a8-124">Substituir `[IoT hub connection string]` com hello cadeia de caracteres de conexão de hub IoT.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-124">Replace `[IoT hub connection string]` with hello IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="fa6a8-125">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="fa6a8-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="fa6a8-126">Executar aplicativo de exemplo do dispositivo Olá simulado e ler mensagens de IoT Hub por Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="fa6a8-126">Run hello simulated device sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="fa6a8-127">comando Olá executa o aplicativo hello que envia hub de IoT tooyour mensagens a cada 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-127">hello command runs hello application that sends messages tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="fa6a8-128">Ela também gera uma mensagem de saudação do tooreceive de processo filho.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-128">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="fa6a8-129">mensagens de saudação que estão sendo enviadas e recebidos são todos Olá exibidos imediatamente na mesma janela do console Olá computador host.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-129">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="fa6a8-130">aplicativo Hello será encerrado em 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-130">hello application will exit in 40 seconds.</span></span>

![O aplicativo de exemplo simulado com mensagens enviadas e recebidas](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="fa6a8-132">Resumo</span><span class="sxs-lookup"><span data-stu-id="fa6a8-132">Summary</span></span>

<span data-ttu-id="fa6a8-133">Executar tooyour IoT hub de saudação exemplo aplicativo toosend dados com êxito com o dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-133">You've successfully run hello sample application toosend data tooyour IoT hub with simulated device.</span></span> <span data-ttu-id="fa6a8-134">Você leu também mensagens de saudação que enviaram tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="fa6a8-134">You've also read hello messages that have been sent tooyour IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="fa6a8-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fa6a8-135">Next steps</span></span>
[<span data-ttu-id="fa6a8-136">Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="fa6a8-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


