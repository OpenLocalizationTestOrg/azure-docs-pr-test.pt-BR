---
title: Gerenciar sistema de mensagens de dispositivos de nuvem do Hub IoT do Azure com o iothub-explorer | Microsoft Docs
description: Saiba como usar a ferramenta iothub-explorer da CLI para monitorar mensagens do dispositivo para a nuvem (D2C) e enviar mensagens da nuvem para o dispositivo (C2D) no Hub IoT do Azure.
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: iothub explorer, sistema de mensagens de dispositivo de nuvem, nuvem ao dispositivo do Hub IoT, sistema de mensagens da nuvem para o dispositivo
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 30151b7bdc544bc36e959cc3528d37897198fc7e
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-iothub-explorer-to-send-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="a5d3e-104">Use o iothub-explorer para enviar e receber mensagens entre o dispositivo e o Hub IoT</span><span class="sxs-lookup"><span data-stu-id="a5d3e-104">Use iothub-explorer to send and receive messages between your device and IoT Hub</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="a5d3e-106">O [iothub-explorer](https://github.com/azure/iothub-explorer) tem alguns comandos que facilitam o gerenciamento do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="a5d3e-107">Este tutorial se concentra em como usar o iothub-explorer para enviar e receber mensagens entre o dispositivo e o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-107">This tutorial focuses on how to use iothub-explorer to send and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="a5d3e-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="a5d3e-108">What you will learn</span></span>

<span data-ttu-id="a5d3e-109">Saiba como usar o iothub-explorer para monitorar mensagens do dispositivo para a nuvem e enviar mensagens da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-109">You learn how to use iothub-explorer to monitor device-to-cloud messages and to send cloud-to-device messages.</span></span> <span data-ttu-id="a5d3e-110">Mensagens do dispositivo para a nuvem podem ser dados de sensor que o dispositivo coleta e envia para o Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-110">Device-to-cloud messages could be sensor data that your device collects and then sends to your IoT hub.</span></span> <span data-ttu-id="a5d3e-111">Mensagens da nuvem para o dispositivo podem ser comandos que o Hub IoT envia para o dispositivo para que um LED conectado a ele pisque.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-111">Cloud-to-device messages could be commands that your IoT hub sends to your device to blink an LED that is connected to your device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="a5d3e-112">O que você fará</span><span class="sxs-lookup"><span data-stu-id="a5d3e-112">What you will do</span></span>

- <span data-ttu-id="a5d3e-113">Use o iothub-explorer para monitorar mensagens do dispositivo para a nuvem.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-113">Use iothub-explorer to monitor device-to-cloud messages.</span></span>
- <span data-ttu-id="a5d3e-114">Use o iothub-explorer para enviar mensagens da nuvem para o dispositivo.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-114">Use iothub-explorer to send cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="a5d3e-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="a5d3e-115">What you need</span></span>

- <span data-ttu-id="a5d3e-116">Tutorial [Configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluído que aborda os seguintes requisitos:</span><span class="sxs-lookup"><span data-stu-id="a5d3e-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers the following requirements:</span></span>
  - <span data-ttu-id="a5d3e-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="a5d3e-118">Um hub IoT do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="a5d3e-119">O aplicativo cliente que envia mensagens para o Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-119">A client application that sends messages to your Azure IoT hub.</span></span>
- <span data-ttu-id="a5d3e-120">iothub-explorer.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-120">iothub-explorer.</span></span> <span data-ttu-id="a5d3e-121">([Instalar o iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="a5d3e-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="a5d3e-122">Monitorar mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="a5d3e-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="a5d3e-123">Para monitorar as mensagens enviadas do seu dispositivo ao seu Hub IoT, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a5d3e-123">To monitor messages that are sent from your device to your IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="a5d3e-124">Abra uma janela do console.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-124">Open a console window.</span></span>
1. <span data-ttu-id="a5d3e-125">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="a5d3e-125">Run the following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="a5d3e-126">Obtenha `<device-id>` e `<IoTHubConnectionString>` do seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="a5d3e-127">Certifique-se de ter concluído o tutorial anterior.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-127">Make sure you've finished the previous tutorial.</span></span> <span data-ttu-id="a5d3e-128">Ou então, você pode tentar usar `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` se você tiver `HostName`, `SharedAccessKeyName` e `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-128">Or you can try to use `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="a5d3e-129">Envie mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="a5d3e-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="a5d3e-130">Para enviar uma mensagem do Hub IoT para o dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="a5d3e-130">To send a message from your IoT hub to your device, follow these steps:</span></span>

1. <span data-ttu-id="a5d3e-131">Abra uma janela do console.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-131">Open a console window.</span></span>
1. <span data-ttu-id="a5d3e-132">Inicie uma sessão no Hub IoT, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a5d3e-132">Start a session on your IoT hub by running the following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="a5d3e-133">Envie uma mensagem para o dispositivo, executando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a5d3e-133">Send a message to your device by running the following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="a5d3e-134">O comando envia a mensagem ao dispositivo e pisca o LED conectado a ele.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-134">The command blinks the LED that is connected to your device and sends the message to your device.</span></span>

> [!Note]
> <span data-ttu-id="a5d3e-135">Não é necessário que o dispositivo envie um comando de confirmação separado para o Hub IoT ao receber a mensagem.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-135">There is no need for the device to send a separate ack command back to your IoT hub upon receiving the message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a5d3e-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a5d3e-136">Next steps</span></span>

<span data-ttu-id="a5d3e-137">Você aprendeu como monitorar mensagens do dispositivo para a nuvem e enviar mensagens da nuvem para o dispositivo entre o dispositivo IoT e o Hub IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="a5d3e-137">You’ve learned how to monitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
