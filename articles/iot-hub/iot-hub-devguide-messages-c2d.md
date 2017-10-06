---
title: mensagens de aaaUnderstand Azure IoT Hub de nuvem para dispositivo | Microsoft Docs
description: "Guia do desenvolvedor - como toouse nuvem para dispositivo de mensagens com o IoT Hub. Inclui informações sobre o ciclo de vida de mensagem de saudação e opções de configuração."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 05/25/2017
ms.author: dobett
ms.openlocfilehash: 5c747b50163873d823556a8baa769c4b8f7f8c44
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-cloud-to-device-messages-from-iot-hub"></a>Enviar mensagens de nuvem para o dispositivo do Hub IoT

aplicativo de dispositivo de toohello toosend notificações unidirecional de sua solução back-end, enviar mensagens de nuvem para dispositivos do dispositivo IoT hub tooyour. Para uma discussão sobre outras opções de nuvem para o dispositivo com suporte do Hub IoT, consulte [Diretrizes de comunicação de nuvem para o dispositivo][lnk-c2d-guidance].

Você pode enviar mensagens da nuvem para o dispositivo por meio de um ponto de extremidade voltado para o serviço (**/messages/devicebound**). Um dispositivo, em seguida, recebe mensagens de saudação por meio de um ponto de extremidade específico do dispositivo (**/devices/ {deviceId} mensagens/devicebound**).

Cada mensagem de nuvem para dispositivo é destinada a um único dispositivo por configuração Olá **para** propriedade muito**/devices/ {deviceId} mensagens/devicebound**.

Cada fila de dispositivo contém no máximo 50 mensagens da nuvem para o dispositivo. Tentar toosend mais toohello de mensagens mesmo dispositivo resulta em um erro.

## <a name="hello-cloud-to-device-message-lifecycle"></a>Olá do ciclo de vida da mensagem de nuvem para dispositivo

entrega de mensagem at-least-once tooguarantee, IoT Hub mantém as mensagens de nuvem para dispositivo nas filas de cada dispositivo. Dispositivos explicitamente devem reconhecer *conclusão* para o IoT Hub tooremove-los do hello fila. Essa abordagem garante a resiliência contra conectividade e falhas de dispositivo.

Olá diagrama a seguir mostra saudação do ciclo de vida estado gráfico para uma mensagem de nuvem para dispositivo no IoT Hub.

![Ciclo de vida de mensagens da nuvem para o dispositivo][img-lifecycle]

Quando Olá serviço IoT Hub envia uma mensagem tooa dispositivo, como serviço Olá define o estado da mensagem de saudação muito**enfileirado**. Quando um dispositivo se quiser muito*receber* uma mensagem, o IoT Hub *bloqueios* mensagem de saudação (definindo o estado de saudação muito**invisível**), que permite que outros threads em Olá dispositivo toostart recebendo outras mensagens. Quando um thread de dispositivo conclui o processamento de uma mensagem de saudação, ele notifica o IoT Hub por *concluir* mensagem de saudação. IoT Hub, em seguida, define o estado de saudação muito**concluído**.

Um dispositivo também pode escolher:

* *Rejeitar* mensagem de saudação, que faz com que o IoT Hub tooset-toohello **morta** estado. Dispositivos que se conectam por Olá protocolo MQTT não é possível rejeitar mensagens de nuvem para dispositivo.
* *Abandonar* mensagem de saudação, que faz com que o IoT Hub mensagem de saudação tooput novamente na fila de hello, com estado de saudação definido muito**enfileirado**.

Um thread pode falhar tooprocess uma mensagem sem notificar o IoT Hub. Nesse caso, as mensagens automaticamente transição do hello **invisível** toohello back estado **enfileirado** estado após um *tempo limite de visibilidade (ou bloqueio)*. valor padrão Olá esse tempo limite é um minuto.

Uma mensagem pode fazer a transição entre Olá **enfileirado** e **invisível** estados, Olá no máximo, o número de vezes especificado em Olá **máximo de contagem de entrega** propriedade no IoT Hub. Após esse número de transições, IoT Hub define o estado de saudação da mensagem de saudação muito**morta**. Da mesma forma, o IoT Hub define estado saudação de uma mensagem muito**morta** após seu tempo de expiração (consulte [tempo toolive][lnk-ttl]).

Olá [como mensagens de nuvem para dispositivo toosend com o IoT Hub] [ lnk-c2d-tutorial] mostra como as mensagens de nuvem para dispositivo toosend de saudação de nuvem e recebem-los em um dispositivo.

Normalmente, um dispositivo conclui uma mensagem de nuvem para dispositivo quando Olá perda de mensagem de saudação não afeta a lógica do aplicativo hello. Por exemplo, quando dispositivo Olá persistiu conteúdo da mensagem de saudação localmente ou executou com êxito uma operação. mensagem de saudação também pode executar informações temporárias, cuja perda não poderia afetar a funcionalidade de saudação do aplicativo hello. Às vezes, para tarefas de longa execução, você pode concluir a mensagem de saudação do nuvem para dispositivo depois de persistência Olá descrição da tarefa no armazenamento local. Em seguida, você pode notificar Olá solução back-end com uma ou mais mensagens de dispositivo para nuvem em vários estágios do progresso da tarefa de saudação.

## <a name="message-expiration-time-toolive"></a>Expiração da mensagem (tempo toolive)

Todas as mensagens da nuvem para o dispositivo têm um tempo de expiração. Esse tempo é definido pelo serviço de saudação (em Olá **ExpiryTimeUtc** propriedade), ou pelo IoT Hub usando o saudação padrão *tempo toolive* especificado como uma propriedade de IoT Hub. Consulte [Opções de configuração da nuvem para o dispositivo][lnk-c2d-configuration].

Uma vantagem de tootake de maneira comum de expiração da mensagem e evitar o envio de mensagens toodisconnected dispositivos, é tooset valores toolive curto período de tempo. Essa abordagem gera Olá mesmo resultado manter o estado de conexão do dispositivo hello, ao mesmo tempo, sendo mais eficiente. Quando você solicitar confirmações de mensagens, o IoT Hub notifica-o de quais dispositivos estão tooreceive capaz de mensagens e os dispositivos que não estão online ou se houve falha.

## <a name="message-feedback"></a>Comentários da mensagem

Quando você enviar uma mensagem de nuvem para dispositivo, serviço Olá pode solicitar a entrega de saudação comentários de mensagem em relação ao estado final de saudação da mensagem.

| Propriedade Ack | Comportamento |
| ------------ | -------- |
| **positivo** | IoT Hub gera uma mensagem de comentários se e somente se, mensagem de saudação do nuvem para dispositivo atingido Olá **concluído** estado. |
| **negativo** | IoT Hub gera uma mensagem de comentários, e apenas se, mensagem de saudação do nuvem para dispositivo atinge Olá **morta** estado. |
| **completo**     | O Hub IoT gera uma mensagem de comentários em ambos os casos. |

Se **Ack** é **completo**e você não recebe uma mensagem de comentários, o que significa que essa mensagem de saudação do comentários expirou. Olá serviço não é possível saber qual é a mensagem original com toohello. Na prática, um serviço deve garantir que ele possa processar comentários de saudação antes de expirar. tempo máximo de expiração de saudação é dois dias, que permite bastante tempo tooget Olá serviço em execução novamente se ocorrer uma falha.

Como explicado em [Pontos de extremidade][lnk-endpoints], o Hub IoT fornece comentários por meio de um ponto de extremidade voltado para o serviço (**/messages/servicebound/feedback**) como mensagens. Olá semântica para receber comentários Olá mesmo para mensagens de nuvem para dispositivos e ter Olá mesmo [ciclo de vida da mensagem][lnk-lifecycle]. Sempre que possível, comentários de mensagem é colocado em lote em uma única mensagem, com hello formato a seguir:

| Propriedade     | Descrição |
| ------------ | ----------- |
| EnqueuedTime | O carimbo de hora que indica quando a mensagem de saudação foi criada. |
| UserId       | `{iot hub name}` |
| ContentType  | `application/vnd.microsoft.iothub.feedback.json` |

corpo de saudação é uma matriz serializado para JSON de registros, cada um com hello propriedades a seguir:

| Propriedade           | Descrição |
| ------------------ | ----------- |
| EnqueuedTimeUtc    | O carimbo de hora que indica quando o resultado de saudação da mensagem de saudação aconteceu. Olá, por exemplo, o dispositivo foi concluído ou mensagem de saudação expirou. |
| OriginalMessageId  | **MessageId** de toowhich de nuvem para dispositivo mensagem de saudação essas informações de comentários está relacionada. |
| StatusCode         | Cadeia de caracteres obrigatória. Usado em mensagens de comentários geradas pelo Hub IoT. <br/> 'Êxito' <br/> 'Expirado' <br/> 'DeliveryCountExceeded' <br/> 'Rejeitado' <br/> 'Limpo' |
| Descrição        | Valores de cadeia de caracteres para **StatusCode**. |
| deviceId           | **DeviceId** de dispositivo de destino de saudação do toowhich de nuvem para dispositivo mensagem de saudação peça de comentários está relacionada. |
| DeviceGenerationId | **DeviceGenerationId** de dispositivo de destino de saudação do toowhich de nuvem para dispositivo mensagem de saudação peça de comentários está relacionada. |

serviço de saudação deve especificar um **MessageId** para hello nuvem para dispositivo mensagem toocorrelate capaz de toobe seus comentários com mensagem de saudação do original.

Olá, exemplo a seguir mostra Olá corpo de uma mensagem de comentários.

```json
[
  {
    "OriginalMessageId": "0987654321",
    "EnqueuedTimeUtc": "2015-07-28T16:24:48.789Z",
    "StatusCode": 0,
    "Description": "Success",
    "DeviceId": "123",
    "DeviceGenerationId": "abcdefghijklmnopqrstuvwxyz"
  },
  {
    ...
  },
  ...
]
```

## <a name="cloud-to-device-configuration-options"></a>Opções de configuração da nuvem para o dispositivo

Cada hub IoT expõe Olá as opções de configuração para a nuvem para dispositivo de mensagens a seguir:

| Propriedade                  | Descrição | Intervalo e padrão |
| ------------------------- | ----------- | ----------------- |
| defaultTtlAsIso8601       | TTL padrão para mensagens da nuvem para o dispositivo. | Intervalo de ISO_8601 a too2D (mínimo 1 minuto). Padrão: 1 hora. |
| maxDeliveryCount          | Contagem máxima de entrega para filas de nuvem para o dispositivo por dispositivo. | 1 too100. Padrão: 10. |
| feedback.ttlAsIso8601     | Retenção de mensagens informativas do serviço associado. | Intervalo de ISO_8601 a too2D (mínimo 1 minuto). Padrão: 1 hora. |
| feedback.maxDeliveryCount |Contagem máxima de entrega para a fila de comentários. | 1 too100. Padrão: 100. |

Para obter mais informações sobre como tooset essas opções de configuração, consulte [hubs IoT criar][lnk-portal].

## <a name="next-steps"></a>Próximas etapas

Para obter informações sobre SDKs de saudação, você pode usar mensagens de nuvem para dispositivo tooreceive, consulte [SDKs do Azure IoT][lnk-sdks].

tootry limite de recebimento de mensagens de nuvem para dispositivo, consulte Olá [enviar nuvem para dispositivo] [ lnk-c2d-tutorial] tutorial.

[img-lifecycle]: ./media/iot-hub-devguide-messages-c2d/lifecycle.png

[lnk-portal]: iot-hub-create-through-portal.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-endpoints]: iot-hub-devguide-endpoints.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-ttl]: #message-expiration-time-to-live
[lnk-c2d-configuration]: #cloud-to-device-configuration-options
[lnk-lifecycle]: #message-lifecycle
[lnk-c2d-tutorial]: iot-hub-csharp-csharp-c2d.md
