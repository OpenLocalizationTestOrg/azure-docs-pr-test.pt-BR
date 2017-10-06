---
title: aaaCompare Azure IoT Hub tooAzure Hubs de eventos | Microsoft Docs
description: "Uma comparação de saudação IoT Hub e serviços do Azure de Hubs de evento realce as diferenças funcionais e casos de uso. comparação de saudação inclui os protocolos suportados, gerenciamento de dispositivos, monitoramento, e carregamento de arquivo."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: aeddea62-8302-48e2-9aad-c5a0e5f5abe9
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/24/2017
ms.author: elioda
ms.openlocfilehash: e5f546b54e29860498d540abfc86a41c4662c0df
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="comparison-of-azure-iot-hub-and-azure-event-hubs"></a>Comparação do Hub IoT do Azure e Hubs de Eventos do Azure
Um dos casos de uso principal de saudação de IoT Hub é toogather telemetria dos dispositivos. Por esse motivo, o IoT Hub é geralmente comparado muito[Hubs de eventos do Azure][Azure Event Hubs]. Como o IoT Hub, Hubs de eventos é um serviço que permite que eventos e telemetria de processamento de eventos toohello nuvem em grande escala, com baixa latência e alta confiabilidade.

No entanto, os serviços de saudação tem muitas diferenças, que são detalhadas no Olá a tabela a seguir:

| Área | Hub IoT | Hubs de Eventos |
| --- | --- | --- |
| Padrões de comunicação | Permite [comunicação do dispositivo com a nuvem][lnk-d2c-guidance] (mensagens, carregamentos de arquivos e propriedades reportadas) e [comunicação da nuvem com o dispositivo][lnk-c2d-guidance] (métodos diretos, propriedades desejadas, mensagens). |Permite somente a entrada de eventos (geralmente considerada para cenários do dispositivo para a nuvem). |
| Informações de estado do dispositivo | [Dispositivos gêmeos][lnk-twins] podem armazenar e consultar informações de estado do dispositivo. | Nenhuma informação de estado do dispositivo pode ser armazenada. |
| Suporte ao protocolo de dispositivo |Dá suporte a MQTT, MQTT por WebSockets, AMQP, AMQP por WebSockets e HTTP. Além disso, o IoT Hub funciona com hello [gateway de protocolo do Azure IoT][lnk-azure-protocol-gateway], um protocolos personalizados do protocolo personalizável gateway implementação toosupport. |Compatível com AMQP, AMQP sobre WebSockets e HTTP. |
| Segurança |Fornece identidade por dispositivo e controle de acesso revogável. Consulte Olá [seção segurança do hello guia do desenvolvedor de IoT Hub]. |Fornece [políticas de acesso compartilhado][Event Hubs - security] em todos os Hubs de Eventos, com suporte limitado à revogação usando [políticas do editor][Event Hubs publisher policies]. Soluções de IoT geralmente são credenciais tooimplement necessária uma solução personalizada toosupport por dispositivo e medidas antifalsificação. |
| Monitoramento de operações |Permite IoT soluções toosubscribe tooa rico conjunto de eventos de conectividade e gerenciamento de identidade de dispositivo, como erros de autenticação de dispositivo individual, limitação e exceções de formato incorreto. Esses eventos permitem que você tooquickly identificar problemas de conectividade no nível do dispositivo individual hello. |Expõe apenas as métricas de agregação. |
| Escala |É otimizado toosupport milhões de dispositivos conectados simultaneamente. |Medidores Olá conexões conforme [cotas de Hubs de eventos do Azure][Azure Event Hubs quotas]. Em Olá outro lado, os Hubs de eventos permite que você toospecify partição de saudação para cada mensagem enviada. |
| SDKs de dispositivo |Fornece [dispositivo SDKs] [ Azure IoT SDKs] para uma grande variedade de plataformas e idiomas em adição toodirect MQTT, AMQP e APIs do HTTP. |Há suporte para .NET, Java e C em adição tooAMQP e interfaces de envio HTTP. |
| Upload de arquivos |Permite que os arquivos de tooupload do IoT soluções de nuvem de toohello de dispositivos. Inclui um ponto de extremidade de notificação de arquivo para a integração de fluxo de trabalho e uma categoria de monitoramento de operações para o suporte à depuração. | Sem suporte. |
| Toomultiple pontos de extremidade de mensagens de rota | Backup too10 há suporte para pontos de extremidade personalizados. As regras determinam como as mensagens são roteadas toocustom pontos de extremidade. Para saber mais, confira [Enviar e receber mensagens com o Hub IoT][lnk-devguide-messaging]. | Requer um código adicional toobe criado e hospedado para distribuição de mensagem. |

Em resumo, mesmo se Olá caso de uso único é ingresso de telemetria do dispositivo para nuvem, o IoT Hub fornece um serviço que foi projetado para conectividade de dispositivo IoT. Ela continua propostas de valor tooexpand Olá para esses cenários com recursos específicos de IoT. Hubs de eventos destina-se a entrada de evento em grande escala, no contexto de saudação de cenários de datacenter inter e dentro do próprio datacenter.

Não é incomum toouse IoT Hub e Hubs de eventos de Olá mesma solução. IoT Hub trata a comunicação de dispositivo para nuvem hello e Hubs de eventos trata a entrada de evento do estágio posterior em mecanismos de processamento em tempo real.

### <a name="next-steps"></a>Próximas etapas
toolearn mais sobre como planejar sua implantação do IoT Hub, consulte [dimensionamento, alta disponibilidade e recuperação de desastres][lnk-scaling].

toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]
* [Simulando um dispositivo com IoT Edge][lnk-iotedge]

[lnk-twins]: iot-hub-devguide-device-twins.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md

[Azure Event Hubs]: ../event-hubs/event-hubs-what-is-event-hubs.md
[seção segurança do hello guia do desenvolvedor de IoT Hub]: iot-hub-devguide-security.md
[Event Hubs - security]: ../event-hubs/event-hubs-authentication-and-security-model-overview.md
[Event Hubs publisher policies]: ../event-hubs/event-hubs-features.md#event-publishers
[Azure Event Hubs quotas]: ../event-hubs/event-hubs-quotas.md
[Azure IoT SDKs]: https://github.com/Azure/azure-iot-sdks
[lnk-azure-protocol-gateway]: iot-hub-protocol-gateway.md

[lnk-scaling]: iot-hub-scaling.md
[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
[lnk-devguide-messaging]: iot-hub-devguide-messaging.md
