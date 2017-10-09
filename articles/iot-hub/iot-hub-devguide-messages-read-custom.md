---
title: pontos de extremidade personalizados do Azure IoT Hub aaaUnderstand | Microsoft Docs
description: Guia do desenvolvedor - usando roteamento regras tooroute pontos de extremidade de toocustom de mensagens de dispositivo para a nuvem.
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
ms.openlocfilehash: daa9cfb35d0853e316bbf469b034d4dadbd4e85d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-message-routes-and-custom-endpoints-for-device-to-cloud-messages"></a>Usar rotas de mensagens e pontos de extremidade personalizados para mensagens de dispositivo para a nuvem

IoT Hub permite tooroute [mensagens de dispositivo para nuvem] [ lnk-device-to-cloud] tooIoT Hub voltados para o serviço de pontos de extremidade com base nas propriedades da mensagem. Mensagens de onde eles precisarem toogo sem Olá roteamento dê regras Olá toosend flexibilidade necessário para mensagens de tooprocess serviços adicionais ou código adicional toowrite. Cada regra de roteamento que você configurou tem Olá propriedades a seguir:

| Propriedade      | Descrição |
| ------------- | ----------- |
| **Nome**      | Olá nome exclusivo que identifica a regra de saudação. |
| **Fonte**    | origem de saudação do dados saudação fluxo toobe tratado. Por exemplo, telemetria do dispositivo. |
| **Condição** | expressão de consulta Olá para regra de roteamento de saudação que é executada em cabeçalhos e corpo de mensagem de saudação e usados toodetermine seja uma correspondência para o ponto de extremidade de saudação. Para obter mais informações sobre como construir uma condição de rota, consulte Olá [referência - linguagem de consulta para trabalhos e twins dispositivo][lnk-devguide-query-language]. |
| **Ponto de extremidade**  | nome de saudação do ponto de extremidade Olá onde o IoT Hub envia mensagens que correspondem à condição de saudação. Pontos de extremidade devem estar no hello mesma região que o hub IoT de hello, caso contrário, você pode ser cobrado para grava entre regiões. |

Uma única mensagem pode coincidir com a condição de saudação em várias regras de roteamento, caso o IoT Hub oferece Olá mensagem toohello ponto de extremidade associado a cada regra correspondente. IoT Hub automaticamente também elimina a duplicação de entrega de mensagens, para se corresponder a uma mensagem de várias regras que tenham Olá mesmo destino, ela é apenas gravada toothat destino uma vez.

Um hub IoT tem um [ponto de extremidade interno][lnk-built-in] padrão. Você pode criar pontos de extremidade personalizados tooroute mensagens tooby vinculação outros serviços em seu hub de toohello de assinatura. O Hub IoT atualmente dá suporte aos Hubs de Eventos, filas do Barramento de Serviço e tópicos do Barramento de Serviço como pontos de extremidade personalizados.

> [!WARNING]
> As filas e os tópicos do Barramento de Serviço com **Sessões** ou **Detecção de Duplicidades** habilitadas não têm suporte como pontos de extremidade personalizados.

Para obter mais informações sobre a criação de pontos de extremidade personalizados no Hub IoT, consulte [Pontos de extremidade do Hub IoT][lnk-devguide-endpoints].

Para saber mais sobre a leitura de pontos de extremidade personalizados, confira:

* Leitura de [Hubs de Eventos][lnk-getstarted-eh].
* Leitura de [filas do Barramento de Serviço][lnk-getstarted-queue].
* Leitura de [tópicos do Barramento de Serviço][lnk-getstarted-topic].

### <a name="next-steps"></a>Próximas etapas

Para saber mais sobre pontos de extremidade do Hub IoT, confira [Pontos de extremidade do Hub IoT][lnk-devguide-endpoints].

Para obter mais informações sobre a linguagem de consulta Olá você pode usar regras de roteamento de toodefine, consulte [linguagem de consulta de IoT Hub para twins do dispositivo, trabalhos e roteamento de mensagens][lnk-devguide-query-language].

Olá [mensagens de dispositivo para nuvem processo IoT Hub usando rotas] [ lnk-d2c-tutorial] tutorial mostra como regras de roteamento de toouse e pontos de extremidade personalizados.

[lnk-built-in]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-to-cloud]: iot-hub-devguide-messages-d2c.md
[lnk-devguide-query-language]: iot-hub-devguide-query-language.md
[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
[lnk-getstarted-eh]: ../event-hubs/event-hubs-csharp-ephcs-getstarted.md
[lnk-getstarted-queue]: ../service-bus-messaging/service-bus-dotnet-get-started-with-queues.md
[lnk-getstarted-topic]: ../service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions.md
