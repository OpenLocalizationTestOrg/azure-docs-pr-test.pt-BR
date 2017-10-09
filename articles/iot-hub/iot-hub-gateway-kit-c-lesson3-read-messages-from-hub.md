---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 3: ler mensagens | Microsoft Docs"
description: "Execute um código de exemplo em suas mensagens de saudação do tooread de computador host do seu hub IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados em nuvem hello, coleta de dados de nuvem, o serviço de nuvem iot, iot dados"
ROBOTS: NOINDEX
redirect_url: /azure/iot-hub/iot-hub-gateway-kit-c-lesson1-set-up-nuc
ms.assetid: cc88be24-b5c0-4ef2-ba21-4e8f77f3e167
ms.service: iot-hub
ms.devlang: c
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 3/21/2017
ms.author: xshi
ms.openlocfilehash: d3ffbe2e83f9d61c0088b8876a7f0eea62c1fbe1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="044d3-104">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="044d3-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="044d3-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="044d3-105">What you will do</span></span>

- <span data-ttu-id="044d3-106">Execute código de exemplo no host do seu computador tooread mensagens de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="044d3-106">Run sample code on your host computer tooread messages from your IoT hub.</span></span>

<span data-ttu-id="044d3-107">Se você tiver problemas, procure por soluções em Olá [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="044d3-107">If you have any problems, look for solutions on hello [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="044d3-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="044d3-108">What you will learn</span></span>

<span data-ttu-id="044d3-109">Como Olá toouse gulp mensagens de tooread ferramenta do seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="044d3-109">How toouse hello gulp tool tooread messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="044d3-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="044d3-110">What you need</span></span>

- <span data-ttu-id="044d3-111">saudação do aplicativo de exemplo Bilitar que foi executado com êxito na lição 3.</span><span class="sxs-lookup"><span data-stu-id="044d3-111">hello BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="044d3-112">Obter as cadeias de conexão do dispositivo e do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="044d3-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="044d3-113">cadeia de caracteres de conexão de dispositivo Olá é usada pelo seu hub IoT de tooyour de tooconnect de dispositivo (SensorTag de TI ou dispositivo simulado).</span><span class="sxs-lookup"><span data-stu-id="044d3-113">hello device connection string is used by your device (TI SensorTag or simulated device) tooconnect tooyour IoT hub.</span></span> <span data-ttu-id="044d3-114">Olá cadeia de caracteres de conexão de hub IoT é um registro de identidade toohello tooconnect usados em dispositivos IoT hub toomanage Olá que são permitidas tooconnect tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="044d3-114">hello IoT hub connection string is used tooconnect toohello identity registry in your IoT hub toomanage hello devices that are allowed tooconnect tooyour IoT hub.</span></span>

- <span data-ttu-id="044d3-115">Liste todos os seus hubs de IoT em seu grupo de recursos executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="044d3-115">List all your IoT hubs in your resource group by running hello following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="044d3-116">Use `iot-gateway` como valor de saudação do `{resource group name}` se você não alterar o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="044d3-116">Use `iot-gateway` as hello value of `{resource group name}` if you didn't change hello value.</span></span>
- <span data-ttu-id="044d3-117">Obter cadeia de caracteres de conexão do hello IoT hub executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="044d3-117">Get hello IoT hub connection string by running hello following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="044d3-118">`{my hub name}`é o nome de saudação que você especificou na lição 2.</span><span class="sxs-lookup"><span data-stu-id="044d3-118">`{my hub name}` is hello name that you specified in Lesson 2.</span></span>

## <a name="configure-hello-device-connection-for-hello-sample-code"></a><span data-ttu-id="044d3-119">Configurar conexão do dispositivo Olá para o código de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="044d3-119">Configure hello device connection for hello sample code</span></span>

<span data-ttu-id="044d3-120">Arquivo de configuração de dispositivo de saudação atualização `config-azure.json` para que você pode ler mensagens de seu hub IoT no computador host.</span><span class="sxs-lookup"><span data-stu-id="044d3-120">Update hello device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="044d3-121">toodo isso, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="044d3-121">toodo this, follow these steps:</span></span>

1. <span data-ttu-id="044d3-122">Abra `config-azure.json` no código do Visual Studio executando Olá comando na janela do console a seguir:</span><span class="sxs-lookup"><span data-stu-id="044d3-122">Open `config-azure.json` in Visual Studio Code by running hello following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="044d3-123">Verifique Olá substituições em Olá a seguir `config-azure.json` arquivo:</span><span class="sxs-lookup"><span data-stu-id="044d3-123">Make hello following replacements in hello `config-azure.json` file:</span></span>

   ![instantâneo de configuração do Azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="044d3-125">Substituir `[IoT hub connection string]` com hello cadeia de conexão do hub IoT obtida.</span><span class="sxs-lookup"><span data-stu-id="044d3-125">Replace `[IoT hub connection string]` with hello IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="044d3-126">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="044d3-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="044d3-127">Se você tiver uma SensorTag de TI, certifique-se de já ter ligado a SensorTag.</span><span class="sxs-lookup"><span data-stu-id="044d3-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="044d3-128">Executar o aplicativo de exemplo hello gateway e leia o IoT Hub mensagens por Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="044d3-128">Run hello gateway sample application and read IoT Hub messages by hello following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="044d3-129">comando Olá executa Olá Bilitar exemplo de aplicativo que lê dados de temperatura do dispositivo simulado ou SensorTag de pacotes e envia hub IoT do hello mensagem tooyour a cada 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="044d3-129">hello command runs hello BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends hello message tooyour IoT hub every 2 seconds.</span></span> <span data-ttu-id="044d3-130">Ela também gera uma mensagem de saudação do tooreceive de processo filho.</span><span class="sxs-lookup"><span data-stu-id="044d3-130">It also spawns a child process tooreceive hello message.</span></span>

<span data-ttu-id="044d3-131">mensagens de saudação que estão sendo enviadas e recebidos são todos Olá exibidos imediatamente na mesma janela do console Olá computador host.</span><span class="sxs-lookup"><span data-stu-id="044d3-131">hello messages that are being sent and received are all displayed instantly on hello same console window in hello host machine.</span></span> <span data-ttu-id="044d3-132">instância de aplicativo de exemplo Hello será encerrado automaticamente em 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="044d3-132">hello sample application instance will terminate automatically in 40 seconds.</span></span>

![Aplicativo de exemplo BLE com mensagens enviadas e recebidas](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="044d3-134">Resumo</span><span class="sxs-lookup"><span data-stu-id="044d3-134">Summary</span></span>

<span data-ttu-id="044d3-135">Executar um tooread de código de exemplo mensagens de seu hub IoT.</span><span class="sxs-lookup"><span data-stu-id="044d3-135">You've run a sample code tooread messages from your IoT hub.</span></span> <span data-ttu-id="044d3-136">Você está pronto tooread mensagens de saudação que são armazenadas no seu armazenamento de tabela do Azure.</span><span class="sxs-lookup"><span data-stu-id="044d3-136">You're ready tooread hello messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="044d3-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="044d3-137">Next steps</span></span>
[<span data-ttu-id="044d3-138">Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="044d3-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


