---
title: "Dispositivo simulado e Gateway do IoT do Azure - Lição 3: ler mensagens | Microsoft Docs"
description: "Execute um código de exemplo no computador host para ler as mensagens de seu Hub IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados na nuvem, coleta de dados de nuvem, serviço de nuvem iot, dados iot"
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
ms.openlocfilehash: 9fbf7958e2437d274f2692dbc235ac8147bdfa63
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="88573-104">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="88573-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="88573-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="88573-105">What you will do</span></span>

- <span data-ttu-id="88573-106">Execute um código de exemplo no computador host para ler mensagens de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="88573-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="88573-107">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="88573-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-sim-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="88573-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="88573-108">What you will learn</span></span>

<span data-ttu-id="88573-109">Como usar a ferramenta gulp para ler mensagens de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="88573-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="88573-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="88573-110">What you need</span></span>

- <span data-ttu-id="88573-111">O exemplo de dispositivo simulado em [Configurar e executar um aplicativo de exemplo de upload de nuvem de dispositivo simulado](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span><span class="sxs-lookup"><span data-stu-id="88573-111">The simulated device sample in [Configure and run a simulated device cloud upload sample application](iot-hub-gateway-kit-c-sim-lesson3-configure-simulated-device-app.md).</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="88573-112">Obter as cadeias de conexão do dispositivo e do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="88573-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="88573-113">A cadeia de conexão do dispositivo é usada pelo seu dispositivo simulado para conectar ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="88573-113">The device connection string is used by your simulated device to connect to your IoT hub.</span></span> <span data-ttu-id="88573-114">A cadeia de conexão do Hub IoT é usada para se conectar ao Registro de identidade em seu Hub IoT para gerenciar os dispositivos que têm permissão para se conectar ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="88573-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="88573-115">Listar todos os Hubs IoT no grupo de recursos executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="88573-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="88573-116">Use `iot-gateway` como o valor de `{resource group name}` se você não o tiver alterado.</span><span class="sxs-lookup"><span data-stu-id="88573-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change it.</span></span>
- <span data-ttu-id="88573-117">Obtenha a cadeia de conexão do Hub IoT executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="88573-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="88573-118">`{my hub name}` é o nome que você especificou na Lição 2.</span><span class="sxs-lookup"><span data-stu-id="88573-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="88573-119">Configurar a conexão do dispositivo para o código de exemplo</span><span class="sxs-lookup"><span data-stu-id="88573-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="88573-120">Atualizar configurações de Hub IoT e de conexão do dispositivo em `config-azure.json` executando as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="88573-120">Update IoT hub and device connection configurations in `config-azure.json` by performing the following steps:</span></span>

1. <span data-ttu-id="88573-121">Abra `config-azure.json` no Visual Studio Code executando o seguinte comando em uma janela do console:</span><span class="sxs-lookup"><span data-stu-id="88573-121">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="88573-122">Faça as seguintes substituições no arquivo `config-azure.json`:</span><span class="sxs-lookup"><span data-stu-id="88573-122">Make the following replacements in the `config-azure.json` file:</span></span>

   ![instantâneo de configuração do Azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="88573-124">Substitua `[IoT hub connection string]` pela cadeia de conexão do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="88573-124">Replace `[IoT hub connection string]` with the IoT hub connection string.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="88573-125">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="88573-125">Read messages from your IoT hub</span></span>

<span data-ttu-id="88573-126">Execute o aplicativo de exemplo de dispositivo simulado e leia as mensagens do Hub IoT por meio do seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="88573-126">Run the simulated device sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="88573-127">O comando executa o aplicativo que envia mensagens ao Hub IoT a cada dois segundos.</span><span class="sxs-lookup"><span data-stu-id="88573-127">The command runs the application that sends messages to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="88573-128">Ele também gera um processo filho para receber a mensagem.</span><span class="sxs-lookup"><span data-stu-id="88573-128">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="88573-129">As mensagens que estão sendo enviadas e recebidas são todas exibidas instantaneamente na mesma janela de console no computador host.</span><span class="sxs-lookup"><span data-stu-id="88573-129">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="88573-130">O aplicativo será encerrado em 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="88573-130">The application will exit in 40 seconds.</span></span>

![O aplicativo de exemplo simulado com mensagens enviadas e recebidas](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub_simudev.png)

## <a name="summary"></a><span data-ttu-id="88573-132">Resumo</span><span class="sxs-lookup"><span data-stu-id="88573-132">Summary</span></span>

<span data-ttu-id="88573-133">Você executou com êxito o aplicativo de exemplo para enviar dados para o Hub IoT com o dispositivo simulado.</span><span class="sxs-lookup"><span data-stu-id="88573-133">You've successfully run the sample application to send data to your IoT hub with simulated device.</span></span> <span data-ttu-id="88573-134">Você também leu as mensagens que foram enviadas para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="88573-134">You've also read the messages that have been sent to your IoT hub.</span></span>

## <a name="next-steps"></a><span data-ttu-id="88573-135">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="88573-135">Next steps</span></span>
[<span data-ttu-id="88573-136">Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="88573-136">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-sim-lesson4-deploy-resource-manager-template.md)


