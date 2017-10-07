---
title: mensagens de Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor – Mensagens do dispositivo para a nuvem e da nuvem para o dispositivo com o Hub IoT. Inclui informações sobre formatos de mensagem e protocolos de comunicação com suporte."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 3fc5f1a3-3711-4611-9897-d4db079b4250
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: a610741e23e243f392f1c042f9ab4a00d42f734f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="device-to-cloud-and-cloud-to-device-messaging-with-iot-hub"></a>Mensagens de dispositivo para nuvem e nuvem para dispositivo com o Hub IoT

Use IoT Hub mensagens toocommunicate com seus dispositivos por:

* Enviar [dispositivo para nuvem] [ lnk-d2c] mensagens de sua solução de tooyour dispositivos back-end.
* Enviar [nuvem para dispositivo] [ lnk-c2d] mensagens de volta a solução Olá terminar tooyour dispositivos.

Propriedades de núcleo da funcionalidade de mensagens de IoT Hub são confiabilidade hello e durabilidade de mensagens. Essas propriedades permitem conectividade de toointermittent resiliência no lado do dispositivo de saudação e tooload picos em processamento no lado da nuvem de saudação de eventos. O Hub IoT implementa *pelo menos uma vez* as garantias de entrega de mensagens do dispositivo para a nuvem e da nuvem para o dispositivo.

Para recursos de toohello uma introdução de IoT Hub, consulte os artigos de saudação [Azure e Internet das coisas] [ lnk-azure-iot] e [visão geral da saudação serviço Azure IoT Hub] [lnk-iot-hub-overview].

## <a name="when-toouse-iot-hub-messaging"></a>Quando mensagens de Hub IoT toouse

Use mensagens de dispositivo para nuvem para enviar telemetria de série de tempo e alertas do seu aplicativo de dispositivo e de nuvem para dispositivo para o aplicativo de dispositivo tooyour notificações unidirecional.

* Consulte também[orientação de comunicação do dispositivo para nuvem] [ lnk-d2c-guidance] se em dúvida entre usar mensagens de dispositivo para nuvem, propriedades relatadas ou carregamento de arquivo.
* Consulte também[orientação de comunicação de nuvem para dispositivo] [ lnk-c2d-guidance] se em dúvida entre o uso diretos métodos, propriedades desejadas ou mensagens de nuvem para dispositivo.

## <a name="next-steps"></a>Próximas etapas

* Saiba mais sobre [mensagens de dispositivo para a nuvem][lnk-d2c] do Hub IoT.
* Saiba mais sobre [mensagens da nuvem para dispositivos][lnk-c2d] do Hub IoT.

[lnk-azure-iot]: iot-hub-what-is-azure-iot.md
[lnk-iot-hub-overview]: iot-hub-what-is-iot-hub.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md