---
title: dispositivo de nuvem do Azure IoT Hub aaaManage mensagens com o Gerenciador de Hub IOT | Microsoft Docs
description: "Saiba como toouse Olá mensagens do Gerenciador de Hub IOT CLI ferramenta toomonitor dispositivo toocloud (D2C) e enviar mensagens de toodevice (C2D) de nuvem no Azure IoT Hub."
services: iot-hub
documentationcenter: 
author: shizn
manager: timlt
tags: 
keywords: Gerenciador de Hub IOT, dispositivos de nuvem do sistema de mensagens, toodevice de nuvem do hub iot, toodevice mensagens de nuvem
ms.assetid: 04521658-35d3-4503-ae48-51d6ad3c62cc
ms.service: iot-hub
ms.devlang: arduino
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: xshi
ms.openlocfilehash: 741383b5631714cc2fef3309541fd2117aa7824c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a><span data-ttu-id="81b6d-104">Use o Gerenciador de Hub IOT toosend e receber mensagens entre o dispositivo e o IoT Hub</span><span class="sxs-lookup"><span data-stu-id="81b6d-104">Use iothub-explorer toosend and receive messages between your device and IoT Hub</span></span>

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

<span data-ttu-id="81b6d-106">O [iothub-explorer](https://github.com/azure/iothub-explorer) tem alguns comandos que facilitam o gerenciamento do Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="81b6d-106">[iothub-explorer](https://github.com/azure/iothub-explorer) has a handful of commands that makes IoT Hub management easier.</span></span> <span data-ttu-id="81b6d-107">Este tutorial se concentra em como toouse explorer hub IOT toosend e receber mensagens entre o dispositivo e o hub IoT.</span><span class="sxs-lookup"><span data-stu-id="81b6d-107">This tutorial focuses on how toouse iothub-explorer toosend and receive messages between your device and your IoT hub.</span></span>

## <a name="what-you-will-learn"></a><span data-ttu-id="81b6d-108">O que você aprenderá</span><span class="sxs-lookup"><span data-stu-id="81b6d-108">What you will learn</span></span>

<span data-ttu-id="81b6d-109">Você aprenderá como toouse mensagens de dispositivo para a nuvem do Gerenciador de Hub IOT toomonitor e toosend nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="81b6d-109">You learn how toouse iothub-explorer toomonitor device-to-cloud messages and toosend cloud-to-device messages.</span></span> <span data-ttu-id="81b6d-110">Mensagens de dispositivo para nuvem podem ser dados de sensor que seu dispositivo coleta e, em seguida, envia tooyour IoT hub.</span><span class="sxs-lookup"><span data-stu-id="81b6d-110">Device-to-cloud messages could be sensor data that your device collects and then sends tooyour IoT hub.</span></span> <span data-ttu-id="81b6d-111">Mensagens de nuvem para dispositivo podem ser comandos que o hub IoT envia tooyour dispositivo tooblink um LED que é o tooyour conectado.</span><span class="sxs-lookup"><span data-stu-id="81b6d-111">Cloud-to-device messages could be commands that your IoT hub sends tooyour device tooblink an LED that is connected tooyour device.</span></span>

## <a name="what-you-will-do"></a><span data-ttu-id="81b6d-112">O que você fará</span><span class="sxs-lookup"><span data-stu-id="81b6d-112">What you will do</span></span>

- <span data-ttu-id="81b6d-113">Use as mensagens do Gerenciador de Hub IOT toomonitor dispositivo para nuvem.</span><span class="sxs-lookup"><span data-stu-id="81b6d-113">Use iothub-explorer toomonitor device-to-cloud messages.</span></span>
- <span data-ttu-id="81b6d-114">Use as mensagens do Gerenciador de Hub IOT toosend nuvem para dispositivo.</span><span class="sxs-lookup"><span data-stu-id="81b6d-114">Use iothub-explorer toosend cloud-to-device messages.</span></span>

## <a name="what-you-need"></a><span data-ttu-id="81b6d-115">O que você precisa</span><span class="sxs-lookup"><span data-stu-id="81b6d-115">What you need</span></span>

- <span data-ttu-id="81b6d-116">Tutorial [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluída que abrange Olá requisitos a seguir:</span><span class="sxs-lookup"><span data-stu-id="81b6d-116">Tutorial [Setup your device](iot-hub-raspberry-pi-kit-node-get-started.md) completed which covers hello following requirements:</span></span>
  - <span data-ttu-id="81b6d-117">Uma assinatura ativa do Azure.</span><span class="sxs-lookup"><span data-stu-id="81b6d-117">An active Azure subscription.</span></span>
  - <span data-ttu-id="81b6d-118">Um hub IoT do Azure em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="81b6d-118">An Azure IoT hub under your subscription.</span></span>
  - <span data-ttu-id="81b6d-119">Um aplicativo cliente que envia o hub do mensagens tooyour IoT do Azure.</span><span class="sxs-lookup"><span data-stu-id="81b6d-119">A client application that sends messages tooyour Azure IoT hub.</span></span>
- <span data-ttu-id="81b6d-120">iothub-explorer.</span><span class="sxs-lookup"><span data-stu-id="81b6d-120">iothub-explorer.</span></span> <span data-ttu-id="81b6d-121">([Instalar o iothub-explorer](https://github.com/azure/iothub-explorer))</span><span class="sxs-lookup"><span data-stu-id="81b6d-121">([Install iothub-explorer](https://github.com/azure/iothub-explorer))</span></span>

## <a name="monitor-device-to-cloud-messages"></a><span data-ttu-id="81b6d-122">Monitorar mensagens do dispositivo para a nuvem</span><span class="sxs-lookup"><span data-stu-id="81b6d-122">Monitor device-to-cloud messages</span></span>

<span data-ttu-id="81b6d-123">toomonitor mensagens que são enviadas de seu hub IoT de tooyour de dispositivo, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="81b6d-123">toomonitor messages that are sent from your device tooyour IoT hub, follow these steps:</span></span>

1. <span data-ttu-id="81b6d-124">Abra uma janela do console.</span><span class="sxs-lookup"><span data-stu-id="81b6d-124">Open a console window.</span></span>
1. <span data-ttu-id="81b6d-125">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="81b6d-125">Run hello following command:</span></span>

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > <span data-ttu-id="81b6d-126">Obtenha `<device-id>` e `<IoTHubConnectionString>` do seu Hub IoT.</span><span class="sxs-lookup"><span data-stu-id="81b6d-126">Get `<device-id>` and `<IoTHubConnectionString>` from your IoT hub.</span></span> <span data-ttu-id="81b6d-127">Verifique se você acabou de tutorial anterior hello.</span><span class="sxs-lookup"><span data-stu-id="81b6d-127">Make sure you've finished hello previous tutorial.</span></span> <span data-ttu-id="81b6d-128">Ou você pode tentar toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` se você tiver `HostName`, `SharedAccessKeyName` e `SharedAccessKey`.</span><span class="sxs-lookup"><span data-stu-id="81b6d-128">Or you can try toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` if you have `HostName`, `SharedAccessKeyName` and `SharedAccessKey`.</span></span>

## <a name="send-cloud-to-device-messages"></a><span data-ttu-id="81b6d-129">Envie mensagens da nuvem para o dispositivo</span><span class="sxs-lookup"><span data-stu-id="81b6d-129">Send cloud-to-device messages</span></span>

<span data-ttu-id="81b6d-130">toosend uma mensagem do dispositivo IoT hub tooyour, siga estas etapas:</span><span class="sxs-lookup"><span data-stu-id="81b6d-130">toosend a message from your IoT hub tooyour device, follow these steps:</span></span>

1. <span data-ttu-id="81b6d-131">Abra uma janela do console.</span><span class="sxs-lookup"><span data-stu-id="81b6d-131">Open a console window.</span></span>
1. <span data-ttu-id="81b6d-132">Inicie uma sessão em seu hub IoT executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="81b6d-132">Start a session on your IoT hub by running hello following command:</span></span>

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. <span data-ttu-id="81b6d-133">Envie um dispositivo de tooyour mensagem executando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="81b6d-133">Send a message tooyour device by running hello following command:</span></span>

   ```bash
   iothub-explorer send <device-id> <message>
   ```

<span data-ttu-id="81b6d-134">comando Olá pisca Olá LED dispositivo conectado tooyour e envia o dispositivo de tooyour de mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="81b6d-134">hello command blinks hello LED that is connected tooyour device and sends hello message tooyour device.</span></span>

> [!Note]
> <span data-ttu-id="81b6d-135">Não é necessário para Olá dispositivo toosend um hub de IoT ack separado comando tooyour voltar ao receber a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="81b6d-135">There is no need for hello device toosend a separate ack command back tooyour IoT hub upon receiving hello message.</span></span>

## <a name="next-steps"></a><span data-ttu-id="81b6d-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="81b6d-136">Next steps</span></span>

<span data-ttu-id="81b6d-137">Você aprendeu como dispositivo para nuvem toomonitor mensagens e enviar mensagens de nuvem para dispositivo entre o dispositivo IoT e o Azure IoT Hub.</span><span class="sxs-lookup"><span data-stu-id="81b6d-137">You’ve learned how toomonitor device-to-cloud messages and send cloud-to-device messages between your IoT device and Azure IoT Hub.</span></span>

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
