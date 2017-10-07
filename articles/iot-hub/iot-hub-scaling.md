---
title: dimensionamento do Hub IoT de aaaAzure | Microsoft Docs
description: "Como tooscale o toosupport de hub IoT a taxa de transferência de mensagem esperado. Inclui um resumo das opções de fragmentação e taxa de transferência de saudação com suporte para cada camada."
services: iot-hub
documentationcenter: 
author: fsautomata
manager: timlt
editor: 
ms.assetid: e7bd4968-db46-46cf-865d-9c944f683832
ms.service: iot-hub
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 08/25/2017
ms.author: elioda
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 3b8bf6c44631c65b34b69752d9043c21db24bb01
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="scale-your-iot-hub-solution"></a>Escalar sua solução do hub IoT
IoT Hub do Azure pode dar suporte a dispositivos conectados simultaneamente milhões de tooa. Para saber mais, confira [Preço do Hub IoT][lnk-pricing]. Cada unidade do Hub IoT permite uma determinada quantidade de mensagens diárias.

tooproperly dimensionar sua solução, considere o uso do IoT Hub. Em particular, considere a possibilidade de taxa de transferência de pico de saudação necessária para Olá categorias de operações a seguir:

* Mensagens do dispositivo para a nuvem
* Mensagens da nuvem para o dispositivo
* Operações de registro de identidade

Informações de taxa de transferência de toothis adição, consulte [cotas de IoT Hub e limitadores] [ IoT Hub quotas and throttles] e projetar sua solução adequadamente.

## <a name="device-to-cloud-and-cloud-to-device-message-throughput"></a>Taxa de transferência de mensagens do dispositivo para a nuvem e da nuvem para o dispositivo
saudação de melhor forma toosize uma solução de IoT Hub é o tráfego de saudação tooevaluate em uma base por unidade.

As mensagens do dispositivo para a nuvem seguem estas diretrizes de taxa de transferência sustentada.

| Camada | Taxa de transferência sustentada | Taxa de envio sustentada |
| --- | --- | --- |
| S1 |Backup too1111 KB por minuto por unidade<br/>(1,5 GB/dia/unidade) |Média de 278 mensagens/minuto por unidade<br/>(400.000 mensagens/dia por unidade) |
| S2 |Backup too16 MB por minuto por unidade<br/>(22,8 GB/dia/unidade) |Média de 4.167 mensagens/minuto por unidade<br/>(6 milhões de mensagens/dia por unidade) |
| S3 |Backup too814 MB por minuto por unidade<br/>(1144,4 GB/dia/unidade) |Média de 208,333 mensagens/minuto por unidade<br/>(300 milhões de mensagens/dia por unidade) |

## <a name="identity-registry-operation-throughput"></a>Taxa de transferência de operações de registro de identidade
Operações de registro de identidade de IoT Hub não devem toobe operações de tempo de execução, como eles são principalmente provisionamento toodevice relacionado.

Para ver número de pico de desempenho específicos, consulte [Cotas e limites do Hub IoT][IoT Hub quotas and throttles].

## <a name="sharding"></a>Fragmentação
Enquanto um único hub IoT pode dimensionar toomillions de dispositivos, às vezes, sua solução requer características específicas de desempenho que um único hub IoT não pode garantir. Nesse caso, é recomendável que você particione seus dispositivos em vários Hubs IoT. Vários hubs IoT smooth picos de tráfego e obter a taxa de transferência necessária hello ou taxas de operação são necessárias.

## <a name="next-steps"></a>Próximas etapas
toofurther explorar recursos de saudação do IoT Hub, consulte:

* [Guia do desenvolvedor do Hub IoT][lnk-devguide]
* [Simulando um dispositivo com Azure IoT Edge][lnk-iotedge]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[IoT Hub quotas and throttles]: iot-hub-devguide-quotas-throttling.md

[lnk-devguide]: iot-hub-devguide.md
[lnk-iotedge]: iot-hub-linux-iot-edge-simulated-device.md
