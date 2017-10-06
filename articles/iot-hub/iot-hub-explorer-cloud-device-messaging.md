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
# <a name="use-iothub-explorer-toosend-and-receive-messages-between-your-device-and-iot-hub"></a>Use o Gerenciador de Hub IOT toosend e receber mensagens entre o dispositivo e o IoT Hub

![Diagrama de ponta a ponta](media/iot-hub-get-started-e2e-diagram/2.png)

[!INCLUDE [iot-hub-get-started-note](../../includes/iot-hub-get-started-note.md)]

O [iothub-explorer](https://github.com/azure/iothub-explorer) tem alguns comandos que facilitam o gerenciamento do Hub IoT. Este tutorial se concentra em como toouse explorer hub IOT toosend e receber mensagens entre o dispositivo e o hub IoT.

## <a name="what-you-will-learn"></a>O que você aprenderá

Você aprenderá como toouse mensagens de dispositivo para a nuvem do Gerenciador de Hub IOT toomonitor e toosend nuvem para dispositivo. Mensagens de dispositivo para nuvem podem ser dados de sensor que seu dispositivo coleta e, em seguida, envia tooyour IoT hub. Mensagens de nuvem para dispositivo podem ser comandos que o hub IoT envia tooyour dispositivo tooblink um LED que é o tooyour conectado.

## <a name="what-you-will-do"></a>O que você fará

- Use as mensagens do Gerenciador de Hub IOT toomonitor dispositivo para nuvem.
- Use as mensagens do Gerenciador de Hub IOT toosend nuvem para dispositivo.

## <a name="what-you-need"></a>O que você precisa

- Tutorial [configurar seu dispositivo](iot-hub-raspberry-pi-kit-node-get-started.md) concluída que abrange Olá requisitos a seguir:
  - Uma assinatura ativa do Azure.
  - Um hub IoT do Azure em sua assinatura.
  - Um aplicativo cliente que envia o hub do mensagens tooyour IoT do Azure.
- iothub-explorer. ([Instalar o iothub-explorer](https://github.com/azure/iothub-explorer))

## <a name="monitor-device-to-cloud-messages"></a>Monitorar mensagens do dispositivo para a nuvem

toomonitor mensagens que são enviadas de seu hub IoT de tooyour de dispositivo, siga estas etapas:

1. Abra uma janela do console.
1. Execute Olá comando a seguir:

   ```bash
   iothub-explorer monitor-events <device-id> --login "<IoTHubConnectionString>"
   ```

   > [!Note]
   > Obtenha `<device-id>` e `<IoTHubConnectionString>` do seu Hub IoT. Verifique se você acabou de tutorial anterior hello. Ou você pode tentar toouse `iothub-explorer monitor-events <device-id> --login "HostName=<my-hub>.azure-devices.net;SharedAccessKeyName=<my-policy>;SharedAccessKey=<my-policy-key>"` se você tiver `HostName`, `SharedAccessKeyName` e `SharedAccessKey`.

## <a name="send-cloud-to-device-messages"></a>Envie mensagens da nuvem para o dispositivo

toosend uma mensagem do dispositivo IoT hub tooyour, siga estas etapas:

1. Abra uma janela do console.
1. Inicie uma sessão em seu hub IoT executando Olá comando a seguir:

   ```bash
   iothub-explorer login `<IoTHubConnectionString>`
   ```

1. Envie um dispositivo de tooyour mensagem executando Olá comando a seguir:

   ```bash
   iothub-explorer send <device-id> <message>
   ```

comando Olá pisca Olá LED dispositivo conectado tooyour e envia o dispositivo de tooyour de mensagem de saudação.

> [!Note]
> Não é necessário para Olá dispositivo toosend um hub de IoT ack separado comando tooyour voltar ao receber a mensagem de saudação.

## <a name="next-steps"></a>Próximas etapas

Você aprendeu como dispositivo para nuvem toomonitor mensagens e enviar mensagens de nuvem para dispositivo entre o dispositivo IoT e o Azure IoT Hub.

[!INCLUDE [iot-hub-get-started-next-steps](../../includes/iot-hub-get-started-next-steps.md)]
