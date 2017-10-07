---
title: formato de mensagem do Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor - formato de saudação descreve e conteúdo esperado das mensagens de IoT Hub."
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
ms.openlocfilehash: 3b1567e47bc32f70c0c252996648c4035ae81243
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-and-read-iot-hub-messages"></a>Criar e ler mensagens do Hub IoT

toosupport interoperabilidade perfeita entre protocolos, o IoT Hub define um formato de mensagem comum para todos os protocolos voltados para o dispositivo. Este formato de mensagem é utilizado para as mensagens [do dispositivo para a nuvem][lnk-d2c] e [nuvem para o dispositivo][lnk-c2d]. Uma [mensagem do Hub IoT][lnk-messaging] consiste de:

* Um conjunto de *propriedades do sistema*. Propriedades que o Hub IoT interpreta ou define. Esse conjunto é predeterminado.
* Um conjunto de *propriedades do aplicativo*. Um dicionário de propriedades de cadeia de caracteres que o aplicativo hello pode definir e acesso, sem a necessidade de corpo de mensagem de saudação do toodeserialize. O Hub IoT nunca modifica essas propriedades.
* Um corpo de binário opaco.

Valores e nomes de propriedade podem conter somente caracteres alfanuméricos ASCII, mais ``{'!', '#', '$', '%, '&', "'", '*', '*', '+', '-', '.', '^', '_', '`', '|', '~'}`` quando você:

* Envie mensagens de dispositivo para nuvem usando o protocolo HTTP de saudação.
* Enviar mensagens da nuvem para o dispositivo.

Para obter mais informações sobre como tooencode e decodificar mensagens enviadas usando protocolos diferentes, consulte [SDKs do Azure IoT][lnk-sdks].

Olá a tabela a seguir lista o conjunto de saudação de propriedades do sistema em mensagens de IoT Hub.

| Propriedade | Descrição |
| --- | --- |
| MessageId |Um identificador definível pelo usuário para a mensagem de saudação usada por padrões de solicitação-resposta. Formato: Uma diferencia maiusculas de minúsculas (a too128 caracteres) cadeia de caracteres ASCII de 7 bits alfanuméricos + `{'-', ':',’.', '+', '%', '_', '#', '*', '?', '!', '(', ')', ',', '=', '@', ';', '$', '''}`. |
| Número de sequência |Um número (exclusivo por dispositivo de fila) atribuído por mensagem de nuvem para dispositivo do IoT Hub tooeach. |
| muito|Um destino especificado em mensagens [Da nuvem para o dispositivo][lnk-c2d]. |
| ExpiryTimeUtc |Data e hora de expiração da mensagem. |
| EnqueuedTime |Data e hora Olá [nuvem para dispositivo] [ lnk-c2d] mensagem foi recebida pelo IoT Hub. |
| CorrelationId |Uma propriedade de cadeia de caracteres em uma mensagem de resposta que geralmente contém Olá MessageId da solicitação hello, nos padrões de solicitação-resposta. |
| UserId |Uma ID usada toospecify origem de saudação de mensagens. Quando as mensagens são geradas pelo IoT Hub, ele é definido muito`{iot hub name}`. |
| Ack |Um gerador de mensagem de comentários. Esta propriedade é usada em mensagens, mensagens de nuvem para dispositivo toorequest Hub IoT toogenerate comentários como resultado de consumo de saudação de mensagem de saudação pelo dispositivo de saudação. Os valores possíveis: **nenhum** (padrão): nenhuma mensagem de comentários é gerada, **positivo**: receber uma mensagem de comentários se a mensagem de saudação foi concluída, **negativo**: receber um mensagem de comentários se a mensagem de saudação expirou (ou contagem máxima de entrega foi atingida) sem que está sendo concluída pelo dispositivo hello, ou **completo**: positivos e negativos. Para saber mais, consulte [Comentários sobre a mensagem][lnk-feedback]. |
| ConnectionDeviceId |Uma ID definida pelo Hub IoT em mensagens do dispositivo para a nuvem. Ele contém Olá **deviceId** do dispositivo Olá que enviou a mensagem de saudação. |
| ConnectionDeviceGenerationId |Uma ID definida pelo Hub IoT em mensagens do dispositivo para a nuvem. Contém Olá **generationId** (como por [propriedades de identidade de dispositivo][lnk-device-properties]) do dispositivo de saudação que enviou a mensagem de saudação. |
| ConnectionAuthMethod |Um método de autenticação definido pelo Hub IoT em mensagens do dispositivo para a nuvem. Esta propriedade contém informações sobre dispositivo Olá autenticação método usado tooauthenticate Olá enviar mensagem de saudação. Para obter mais informações, consulte [dispositivo toocloud antifalsificação][lnk-antispoofing]. |

## <a name="message-size"></a>Tamanho da mensagem

IoT Hub mede o tamanho da mensagem de forma independente de protocolo, considerando a carga real de saudação somente. tamanho de Olá em bytes é calculado como a soma de saudação do seguinte hello:

* tamanho do corpo da saudação em bytes.
* tamanho de saudação em bytes de todos os valores hello das propriedades do sistema de mensagem de saudação.
* tamanho de saudação em bytes de todos os nomes de propriedade do usuário e valores.

Valores e nomes de propriedade são caracteres tooASCII limitado, então comprimento Olá de cadeias de caracteres de saudação é igual ao tamanho de saudação em bytes.

## <a name="next-steps"></a>Próximas etapas

Para obter informações sobre limites de tamanho de mensagem no Hub IoT, consulte [cotas do Hub IoT e limitação][lnk-quotas].

toolearn como toocreate e ler mensagens de Hub IoT em várias linguagens de programação, consulte Olá [começar] [ lnk-get-started] tutoriais.

[lnk-messaging]: iot-hub-devguide-messaging.md
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-get-started]: iot-hub-get-started.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-c2d]: iot-hub-devguide-messages-c2d.md
[lnk-d2c]: iot-hub-devguide-messages-d2c.md
[lnk-feedback]: iot-hub-devguide-messages-c2d.md#message-feedback
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-antispoofing]: iot-hub-devguide-messages-d2c.md#anti-spoofing-properties
