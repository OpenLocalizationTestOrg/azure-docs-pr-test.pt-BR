---
title: mensagens de dispositivo para a nuvem de Azure IoT Hub aaaUnderstand | Microsoft Docs
description: "Guia do desenvolvedor - como toouse dispositivo para a nuvem com o IoT Hub de mensagens. Inclui informações sobre o envio de dados de telemetria e não telemtry e usando o roteamento de mensagens toodeliver."
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
ms.openlocfilehash: 07dc8a6be747365c7efbc528ab2762b0d9790758
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="send-device-to-cloud-messages-tooiot-hub"></a>Enviar mensagens de dispositivo para nuvem tooIoT Hub

Telemetria de série temporal toosend e alertas de seu dispositivos tooyour solução back-end, enviar mensagens de dispositivo para a nuvem de hub IoT de tooyour de dispositivo. Para ver uma discussão sobre outras opções de dispositivo para a nuvem com suporte no Hub IoT, confira [Orientação sobre comunicações de dispositivo para a nuvem][lnk-d2c-guidance].

Você envia mensagens do dispositivo para a nuvem por meio de um ponto de extremidade voltado para o dispositivo (**/devices/{deviceId}/messages/events**). Regras de roteamento e rotear o tooone mensagens de pontos de extremidade de serviço voltados Olá em seu hub IoT. Regras de roteamento usam cabeçalhos de saudação e corpo de mensagens de saudação do dispositivo para a nuvem que passam por seu hub toodetermine onde tooroute-los. Por padrão, as mensagens são roteadas toohello internos voltados para o serviço endpoint (**mensagens de eventos**), que é compatível com [Hubs de eventos][lnk-event-hubs]. Portanto, você pode usar o padrão [integração com Hubs de evento e SDKs] [ lnk-compatible-endpoint] tooreceive mensagens de dispositivo para nuvem em sua solução de back-end.

O Hub IoT implementa mensagens de dispositivo para nuvem usando um padrão de sistema de mensagens de streaming. Mensagens de dispositivo para a nuvem do IoT Hub são mais [Hubs de eventos] [ lnk-event-hubs] *eventos* que [Service Bus] [ lnk-servicebus] *mensagens* que há um grande volume de eventos que passam pelo serviço de saudação que pode ser lido por vários leitores.

Mensagens com o IoT Hub dispositivo para nuvem tem Olá características a seguir:

* Mensagens de dispositivo para nuvem são duráveis e mantidas no padrão de um hub IoT **mensagens de eventos** ponto de extremidade para o tooseven dias.
* Mensagens de dispositivo para nuvem podem ter no máximo 256 KB e podem ser agrupadas em lotes toooptimize envia. Os lotes podem ter no máximo 256 KB.
* Conforme explicado em Olá [tooIoT de acesso de controle Hub] [ lnk-devguide-security] seção, o IoT Hub habilita o controle de acesso e autenticação por dispositivo.
* IoT Hub permite toocreate too10 pontos de extremidade personalizado. As mensagens são entregues toohello pontos de extremidade com base nas rotas configuradas em seu hub IoT. Para saber mais, confira [Regras de direcionamento](#routing-rules).
* O Hub IoT habilita milhões de dispositivos conectados simultaneamente (confira [Cotas e limitação][lnk-quotas]).
* O Hub IoT não permite o particionamento arbitrário. As mensagens do dispositivo para a nuvem são particionadas com base em sua **deviceId**de origem.

Para obter mais informações sobre as diferenças de saudação entre Olá IoT Hub e os serviços de Hubs de eventos, consulte [comparação de IoT Hub do Azure e Hubs de eventos do Azure][lnk-comparison].

## <a name="send-non-telemetry-traffic"></a>Enviar tráfego sem telemetria

Geralmente, os dispositivos além de pontos de dados de tootelemetry, enviam mensagens e solicitações que exigem tratamento no back-end de solução hello e execução separado. Por exemplo, alertas críticos que devem disparar uma ação específica em Olá back-end. Você pode escrever facilmente um [regra de roteamento] [ lnk-devguide-custom] toosend esses tipos de ponto de extremidade de mensagens tooan dedicado tootheir processamento com base em qualquer um cabeçalho de mensagem de saudação ou um valor no corpo da mensagem de saudação.

Para obter mais informações sobre Olá melhor maneira tooprocess nesse tipo de mensagem, consulte Olá [Tutorial: como tooprocess mensagens de dispositivo para a nuvem de IoT Hub] [ lnk-d2c-tutorial] tutorial.

## <a name="route-device-to-cloud-messages"></a>Encaminhar mensagens do dispositivo para a nuvem

Você tem duas opções para aplicativos de back-end do roteamento mensagens de dispositivo para nuvem tooyour:

* Usar Olá interno [ponto de extremidade compatível com o evento Hub] [ lnk-compatible-endpoint] tooenable aplicativos de back-end tooread Olá dispositivo para nuvem as mensagens recebidas pelo hub hello. toolearn sobre ponto de extremidade Olá de interno compatível Hub de eventos, consulte [ler mensagens de dispositivo para a nuvem de ponto de extremidade internos Olá][lnk-devguide-builtin].
* Use o roteamento regras toosend mensagens toocustom pontos de extremidade em seu hub IoT. Pontos de extremidade personalizados permitem que as mensagens de dispositivo para nuvem tooread aplicativos de back-end usando Hubs de eventos, filas de barramento de serviço ou tópicos do barramento de serviço. toolearn sobre pontos de extremidade personalizados e roteamentos, consulte [usar pontos de extremidade personalizados e regras de roteamento para mensagens de dispositivo para nuvem][lnk-devguide-custom].

## <a name="anti-spoofing-properties"></a>Propriedades antifalsificação

dispositivo tooavoid falsificação em mensagens de dispositivo para nuvem, o IoT Hub carimbos todas as mensagens com hello propriedades a seguir:

* **ConnectionDeviceId**
* **ConnectionDeviceGenerationId**
* **ConnectionAuthMethod**

Olá primeiro dois contêm Olá **deviceId** e **generationId** de saudação provenientes do dispositivo, como por [propriedades de identidade de dispositivo][lnk-device-properties].

Olá **ConnectionAuthMethod** propriedade contém um objeto JSON serializado, com hello propriedades a seguir:

```json
{
  "scope": "{ hub | device}",
  "type": "{ symkey | sas}",
  "issuer": "iothub"
}
```

## <a name="next-steps"></a>Próximas etapas

Para obter informações sobre SDKs de saudação, você pode usar mensagens de dispositivo para nuvem toosend, consulte [SDKs do Azure IoT][lnk-sdks].

Olá [começar] [ lnk-get-started] tutoriais mostram como dispositivo para nuvem toosend mensagens de dispositivos simulados e físicos. Para obter mais detalhes, consulte Olá [mensagens de dispositivo para nuvem processo IoT Hub usando rotas] [ lnk-d2c-tutorial] tutorial.

[lnk-devguide-builtin]: iot-hub-devguide-messages-read-builtin.md
[lnk-devguide-custom]: iot-hub-devguide-messages-read-custom.md
[lnk-comparison]: iot-hub-compare-event-hubs.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-get-started]: iot-hub-get-started.md

[lnk-event-hubs]: http://azure.microsoft.com/documentation/services/event-hubs/
[lnk-servicebus]: http://azure.microsoft.com/documentation/services/service-bus/
[lnk-quotas]: iot-hub-devguide-quotas-throttling.md
[lnk-sdks]: iot-hub-devguide-sdks.md
[lnk-compatible-endpoint]: iot-hub-devguide-messages-read-builtin.md
[lnk-device-properties]: iot-hub-devguide-identity-registry.md#device-identity-properties
[lnk-devguide-security]: iot-hub-devguide-security.md
[lnk-d2c-tutorial]: iot-hub-csharp-csharp-process-d2c.md
