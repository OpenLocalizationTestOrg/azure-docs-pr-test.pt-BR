---
title: "aaaAzure comunicação de IoT Hub protocolos e portas | Microsoft Docs"
description: "Guia do desenvolvedor - descreve os protocolos de comunicação Olá com suporte para comunicações de dispositivo para nuvem e nuvem para dispositivo e números de porta de saudação que devem ser abertos."
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
ms.openlocfilehash: 31cb948f1d30edd87edb13ad0dd859c02bcc3239
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# Referência – escolha um protocolo de comunicação

IoT Hub permite que dispositivos toouse [MQTT][lnk-mqtt], MQTT por meio de WebSockets, [AMQP][lnk-amqp], protocolos de AMQP sobre HTTP e WebSockets do lado do dispositivo comunicações. Para saber mais sobre como esses protocolos dão suporte a recursos específicos do Hub IoT, confira [Orientação sobre comunicações de dispositivo para a nuvem][lnk-d2c-guidance] e [Orientação sobre comunicações de dispositivo para a nuvem][lnk-c2d-guidance].

Olá tabela a seguir fornece recomendações de alto nível Olá para sua opção de protocolo:

| Protocolo | Quando você deve escolher este protocolo |
| --- | --- |
| MQTT <br> MQTT sobre WebSocket |Usar vários dispositivos (cada um com suas próprias credenciais por dispositivo) em todos os dispositivos que não exigem tooconnect sobre Olá mesma conexão de TLS. |
| AMQP <br> AMQP sobre WebSocket |Usar no campo e nuvem gateways tootake aproveitar multiplexação em todos os dispositivos de conexão. |
| HTTP |Use para dispositivos que não dão suporte a outros protocolos. |

Considere Olá pontos a seguir quando você escolhe o protocolo para as comunicações do lado do dispositivo:

* **Padrão da nuvem para o dispositivo**. HTTP não tem um envio de servidor de tooimplement de maneira eficiente. Assim, ao usar HTTP, os dispositivos sondam o Hub IoT em busca de mensagens da nuvem para o dispositivo. Essa abordagem é ineficiente para dispositivo hello e IoT Hub. De acordo com as diretrizes atuais de HTTP, cada dispositivo deve sondar mensagens a cada 25 minutos ou mais. Em Olá outro lado, MQTT e AMQP oferecem suporte ao envio de servidor ao receber mensagens de nuvem para dispositivo. Elas permitem imediatos envios de mensagens de dispositivo do IoT Hub toohello. Se a latência de entrega for uma preocupação, MQTT ou AMQP são Olá melhor protocolos toouse. Para dispositivos conectados raramente, o HTTP funciona também.
* **Gateways de campo**. Ao usar MQTT e HTTP, você não pode se conectar a vários dispositivos (cada um com suas próprias credenciais por dispositivo) usando Olá a mesma conexão de TLS. Assim, para [campo cenários de gateway][lnk-azure-gateway-guidance], esses protocolos estão abaixo do ideal porque eles exigem uma conexão TLS entre o gateway de campo hello e IoT Hub para cada gateway do dispositivo conectado toohello campo.
* **Dispositivos com poucos recursos**. Olá MQTT e bibliotecas de HTTP têm um espaço menor de bibliotecas do AMQP hello. Dessa forma, se hello dispositivo limitou os recursos (por exemplo, menor que 1 MB de RAM), esses protocolos podem ser Olá única implementação de protocolo disponível.
* **Percurso da rede**. protocolo AMQP padrão de saudação usa a porta 5671, enquanto MQTT escuta na porta 8883, que pode causar problemas em redes de protocolos HTTP toonon fechado. MQTT por meio de WebSockets, AMQP sobre HTTP e WebSockets estão disponível toobe usada neste cenário.
* **Tamanho da carga**. O MQTT e o AMQP são protocolos binários, que resultam em cargas mais compactas que o HTTP.

> [!WARNING]
> Ao usar o HTTP, cada dispositivo deverá sondar se há mensagens da nuvem para o dispositivo a cada 25 minutos ou mais. No entanto, durante o desenvolvimento, é aceitável toopoll com mais frequência do que a cada 25 minutos.

## Números de porta

Os dispositivos podem se comunicar com o Hub IoT no Azure usando uma variedade de protocolos. Normalmente, escolha de saudação do protocolo é orientada por requisitos específicos de saudação de solução de saudação. Olá tabela a seguir lista portas de saída de hello devem estar abertas para um dispositivo toobe capaz de toouse um protocolo específico:

| Protocolo | Porta |
| --- | --- |
| MQTT |8883 |
| MQTT sobre WebSockets |443 |
| AMQP |5671 |
| AMQP sobre WebSockets |443 |
| HTTP |443 |

Depois de criar um hub IoT em uma região do Azure, hello mantém de hub IoT Olá mesmo endereço IP para o tempo de vida de saudação do hub IoT. No entanto, toomaintain qualidade de serviço, se o Microsoft move a unidade de escala diferentes Olá IoT hub tooa, em seguida, ele recebe um novo endereço IP.


## Próximas etapas

toolearn mais sobre como o IoT Hub implementa o protocolo MQTT hello, consulte [comunicação com o hub IoT usando o protocolo MQTT Olá][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
