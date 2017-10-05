---
title: "Portas e protocolos de comunicação do Hub IoT do Azure | Microsoft Docs"
description: "Guia do desenvolvedor – descreve os protocolos de comunicação com suporte para comunicações de dispositivo para a nuvem e da nuvem para dispositivos e os números de porta que devem ser abertos."
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
ms.openlocfilehash: 98004a48734e33f85eebf8f6213d9f0751dea843
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# Referência – escolha um protocolo de comunicação

O Hub IoT permite que os dispositivos usem protocolos [MQTT][lnk-mqtt], MQTT sobre WebSockets, [AMQP][lnk-amqp], AMQP sobre WebSockets e HTTP para comunicação do lado do dispositivo. Para saber mais sobre como esses protocolos dão suporte a recursos específicos do Hub IoT, confira [Orientação sobre comunicações de dispositivo para a nuvem][lnk-d2c-guidance] e [Orientação sobre comunicações de dispositivo para a nuvem][lnk-c2d-guidance].

A tabela a seguir fornece as recomendações de alto nível para sua escolha de protocolo:

| Protocolo | Quando você deve escolher este protocolo |
| --- | --- |
| MQTT <br> MQTT sobre WebSocket |Use em todos os dispositivos que não exigem conectar vários dispositivos (cada um com suas próprias credenciais por dispositivo) sobre a mesma conexão TLS. |
| AMQP <br> AMQP sobre WebSocket |Use em gateways de campo e de nuvem para tirar proveito da multiplexação de conexão entre dispositivos. |
| HTTP |Use para dispositivos que não dão suporte a outros protocolos. |

Considere os seguintes pontos ao escolher seu protocolo de comunicação do lado do dispositivo:

* **Padrão da nuvem para o dispositivo**. O HTTP não tem uma maneira eficiente de implementar o envio do servidor. Assim, ao usar HTTP, os dispositivos sondam o Hub IoT em busca de mensagens da nuvem para o dispositivo. Essa abordagem é ineficiente para o dispositivo e para o Hub IoT. De acordo com as diretrizes atuais de HTTP, cada dispositivo deve sondar mensagens a cada 25 minutos ou mais. Por outro lado, o MQTT e o AMQP dão suporte ao envio por push do servidor quando recebem mensagens de nuvem para o dispositivo. Eles permitem envios por push imediatos de mensagens do Hub IoT para o dispositivo. Se a latência de entrega for uma preocupação, o MQTT ou AMQP serão as melhores opções de protocolo. Para dispositivos conectados raramente, o HTTP funciona também.
* **Gateways de campo**. Ao usar MQTT e HTTP, você não pode conectar vários dispositivos (cada um com suas próprias credenciais por dispositivo) usando a mesma conexão TLS. Assim, para [Cenários de gateway de campo][lnk-azure-gateway-guidance], esses protocolos ficam abaixo do ideal, pois exigem uma conexão TLS entre o gateway de campo e o Hub IoT para cada dispositivo conectado ao gateway de campo.
* **Dispositivos com poucos recursos**. As bibliotecas de MQTT e HTTP têm uma superfície menor do que as bibliotecas de AMQP. Dessa forma, caso o dispositivo tenha recursos limitados (por exemplo, menos de 1 MB de RAM), esses protocolos poderão ser a única implementação de protocolo disponível.
* **Percurso da rede**. O protocolo AMQP padrão usa a porta 5671, enquanto o MQTT escuta na porta 8883, o que pode causar problemas em redes que estão fechadas para protocolos não HTTP. MQTT sobre WebSockets, AMQP sobre WebSockets e HTTP estão disponíveis para serem usados nesse cenário.
* **Tamanho da carga**. O MQTT e o AMQP são protocolos binários, que resultam em cargas mais compactas que o HTTP.

> [!WARNING]
> Ao usar o HTTP, cada dispositivo deverá sondar se há mensagens da nuvem para o dispositivo a cada 25 minutos ou mais. No entanto, durante o desenvolvimento, é aceitável sondar com mais frequência do que a cada 25 minutos.

## Números de porta

Os dispositivos podem se comunicar com o Hub IoT no Azure usando uma variedade de protocolos. Normalmente, a opção de protocolo é orientada por requisitos específicos da solução. A tabela a seguir lista as portas de saída que devem ser abertas para um dispositivo para poder usar um protocolo específico:

| Protocolo | Porta |
| --- | --- |
| MQTT |8883 |
| MQTT sobre WebSockets |443 |
| AMQP |5671 |
| AMQP sobre WebSockets |443 |
| HTTP |443 |

Depois de criar um Hub IoT em uma região do Azure, o hub manterá o mesmo endereço IP durante a vida útil desse Hub IoT. No entanto, para manter a qualidade do serviço, se a Microsoft mover o Hub IoT para uma unidade de escala diferente, ele receberá um novo endereço IP.


## Próximas etapas

Para saber mais sobre como o Hub IoT implementa o protocolo MQTT, confira [Comunicação com o hub IoT usando o protocolo MQTT][lnk-mqtt-support].

[lnk-d2c-guidance]: iot-hub-devguide-d2c-guidance.md
[lnk-c2d-guidance]: iot-hub-devguide-c2d-guidance.md
[lnk-mqtt-support]: iot-hub-mqtt-support.md
[lnk-amqp]: http://docs.oasis-open.org/amqp/core/v1.0/os/amqp-core-complete-v1.0-os.pdf
[lnk-mqtt]: http://docs.oasis-open.org/mqtt/mqtt/v3.1.1/mqtt-v3.1.1.pdf
[lnk-azure-gateway-guidance]: iot-hub-devguide-endpoints.md#field-gateways
