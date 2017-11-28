---
title: "Dispositivo SensorTag e Gateway do IoT do Azure - Lição 3: ler mensagens | Microsoft Docs"
description: "Execute um código de exemplo no computador host para ler as mensagens de seu Hub IoT."
services: iot-hub
documentationcenter: 
author: shizn
manager: timtl
tags: 
keywords: "dados na nuvem, coleta de dados de nuvem, serviço de nuvem iot, dados iot"
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
ms.openlocfilehash: 45f3595c4848d5c283cdf95604adf8d2c8d6a809
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="4cda4-104">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="4cda4-104">Read messages from your IoT hub</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="4cda4-105">O que você fará</span><span class="sxs-lookup"><span data-stu-id="4cda4-105">What you will do</span></span>

- <span data-ttu-id="4cda4-106">Execute um código de exemplo no computador host para ler mensagens de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4cda4-106">Run sample code on your host computer to read messages from your IoT hub.</span></span>

<span data-ttu-id="4cda4-107">Se você tiver problemas, procure as soluções na [página de solução de problemas](iot-hub-gateway-kit-c-troubleshooting.md).</span><span class="sxs-lookup"><span data-stu-id="4cda4-107">If you have any problems, look for solutions on the [troubleshooting page](iot-hub-gateway-kit-c-troubleshooting.md).</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="4cda4-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="4cda4-108">What you will learn</span></span>

<span data-ttu-id="4cda4-109">Como usar a ferramenta gulp para ler mensagens de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4cda4-109">How to use the gulp tool to read messages from your IoT hub.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="4cda4-110">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="4cda4-110">What you need</span></span>

- <span data-ttu-id="4cda4-111">O aplicativo de exemplo BLE que você executou com êxito na Lição 3.</span><span class="sxs-lookup"><span data-stu-id="4cda4-111">The BLE sample application that you ran successfully in Lesson 3.</span></span>

## <a name="get-your-iot-hub-and-device-connection-strings"></a><span data-ttu-id="4cda4-112">Obter as cadeias de conexão do dispositivo e do Hub IoT</span><span class="sxs-lookup"><span data-stu-id="4cda4-112">Get your IoT hub and device connection strings</span></span>

<span data-ttu-id="4cda4-113">Essa cadeia de conexão é usada pelo seu dispositivo (SensorTag de TI ou dispositivo simulado) para se conectar ao seu Hub IoT como um dispositivo.</span><span class="sxs-lookup"><span data-stu-id="4cda4-113">The device connection string is used by your device (TI SensorTag or simulated device) to connect to your IoT hub.</span></span> <span data-ttu-id="4cda4-114">A cadeia de conexão do Hub IoT é usada para se conectar ao Registro de identidade em seu Hub IoT para gerenciar os dispositivos que têm permissão para se conectar ao seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4cda4-114">The IoT hub connection string is used to connect to the identity registry in your IoT hub to manage the devices that are allowed to connect to your IoT hub.</span></span>

- <span data-ttu-id="4cda4-115">Listar todos os Hubs IoT no grupo de recursos executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4cda4-115">List all your IoT hubs in your resource group by running the following command:</span></span>

   ```bash
   az iot hub list -g iot-gateway --query [].name
   ```

   <span data-ttu-id="4cda4-116">Use `iot-gateway` como o valor de `{resource group name}` se não tiver alterado o valor.</span><span class="sxs-lookup"><span data-stu-id="4cda4-116">Use `iot-gateway` as the value of `{resource group name}` if you didn't change the value.</span></span>
- <span data-ttu-id="4cda4-117">Obtenha a cadeia de conexão do Hub IoT executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4cda4-117">Get the IoT hub connection string by running the following command:</span></span>

   ```bash
   az iot hub show-connection-string --name {my hub name} -g iot-gateway
   ```

   <span data-ttu-id="4cda4-118">`{my hub name}` é o nome que você especificou na Lição 2.</span><span class="sxs-lookup"><span data-stu-id="4cda4-118">`{my hub name}` is the name that you specified in Lesson 2.</span></span>

## <a name="configure-the-device-connection-for-the-sample-code"></a><span data-ttu-id="4cda4-119">Configurar a conexão do dispositivo para o código de exemplo</span><span class="sxs-lookup"><span data-stu-id="4cda4-119">Configure the device connection for the sample code</span></span>

<span data-ttu-id="4cda4-120">Atualize o arquivo de configuração do dispositivo `config-azure.json` para que você possa ler mensagens de seu Hub IoT no computador host.</span><span class="sxs-lookup"><span data-stu-id="4cda4-120">Update the device configuration file `config-azure.json` so that you can read messages from your IoT hub on your host computer.</span></span> <span data-ttu-id="4cda4-121">Para fazer isso, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="4cda4-121">To do this, follow these steps:</span></span>

1. <span data-ttu-id="4cda4-122">Abra `config-azure.json` no Visual Studio Code executando o seguinte comando em uma janela do console:</span><span class="sxs-lookup"><span data-stu-id="4cda4-122">Open `config-azure.json` in Visual Studio Code by running the following command in a console window:</span></span>

   ```bash
   # For Windows command prompt
   code %USERPROFILE%\.iot-hub-getting-started\config-azure.json
   # For MacOS or Ubuntu
   code ~/.iot-hub-getting-started/config-azure.json
   ```

2. <span data-ttu-id="4cda4-123">Faça as seguintes substituições no arquivo `config-azure.json`:</span><span class="sxs-lookup"><span data-stu-id="4cda4-123">Make the following replacements in the `config-azure.json` file:</span></span>

   ![instantâneo de configuração do Azure](media/iot-hub-gateway-kit-lessons/lesson3/config_azure.png)

   <span data-ttu-id="4cda4-125">Substitua `[IoT hub connection string]` pela cadeia de conexão do Hub IoT obtida.</span><span class="sxs-lookup"><span data-stu-id="4cda4-125">Replace `[IoT hub connection string]` with the IoT hub connection string that you obtained.</span></span>

## <a name="read-messages-from-your-iot-hub"></a><span data-ttu-id="4cda4-126">Ler mensagens de seu Hub IoT</span><span class="sxs-lookup"><span data-stu-id="4cda4-126">Read messages from your IoT hub</span></span>

<span data-ttu-id="4cda4-127">Se você tiver uma SensorTag de TI, certifique-se de já ter ligado a SensorTag.</span><span class="sxs-lookup"><span data-stu-id="4cda4-127">If you have a TI SensorTag, make sure you have already powered on your SensorTag.</span></span> <span data-ttu-id="4cda4-128">Execute o aplicativo de exemplo no gateway e leia as mensagens do Hub IoT por meio do seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="4cda4-128">Run the gateway sample application and read IoT Hub messages by the following command:</span></span>

```bash
gulp run --iot-hub
```

<span data-ttu-id="4cda4-129">O comando executa o aplicativo de exemplo BLE, que lê e empacota dados de temperatura do dispositivo simulado ou SensorTag e envia a mensagem para o Hub IoT a cada 2 segundos.</span><span class="sxs-lookup"><span data-stu-id="4cda4-129">The command runs the BLE sample application that reads and packages temperature data from your SensorTag or simulated device and sends the message to your IoT hub every 2 seconds.</span></span> <span data-ttu-id="4cda4-130">Ele também gera um processo filho para receber a mensagem.</span><span class="sxs-lookup"><span data-stu-id="4cda4-130">It also spawns a child process to receive the message.</span></span>

<span data-ttu-id="4cda4-131">As mensagens que estão sendo enviadas e recebidas são todas exibidas instantaneamente na mesma janela de console no computador host.</span><span class="sxs-lookup"><span data-stu-id="4cda4-131">The messages that are being sent and received are all displayed instantly on the same console window in the host machine.</span></span> <span data-ttu-id="4cda4-132">A instância do aplicativo de exemplo será encerrada automaticamente em 40 segundos.</span><span class="sxs-lookup"><span data-stu-id="4cda4-132">The sample application instance will terminate automatically in 40 seconds.</span></span>

![Aplicativo de exemplo BLE com mensagens enviadas e recebidas](media/iot-hub-gateway-kit-lessons/lesson3/gulp_run_read_hub.png)

## <a name="summary"></a><span data-ttu-id="4cda4-134">Resumo</span><span class="sxs-lookup"><span data-stu-id="4cda4-134">Summary</span></span>

<span data-ttu-id="4cda4-135">Você executou um código de exemplo para ler mensagens de seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="4cda4-135">You've run a sample code to read messages from your IoT hub.</span></span> <span data-ttu-id="4cda4-136">Você está pronto para ler as mensagens que estão armazenadas no seu Armazenamento de Tabelas do Azure.</span><span class="sxs-lookup"><span data-stu-id="4cda4-136">You're ready to read the messages that are stored in your Azure table storage.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4cda4-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4cda4-137">Next steps</span></span>
[<span data-ttu-id="4cda4-138">Criar um aplicativo de funções do Azure e uma conta de armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="4cda4-138">Create an Azure function app and Azure Storage account</span></span>](iot-hub-gateway-kit-c-lesson4-deploy-resource-manager-template.md)


