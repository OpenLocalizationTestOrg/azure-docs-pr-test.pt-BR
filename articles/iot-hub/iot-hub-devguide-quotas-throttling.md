---
title: "as cotas do Azure IoT Hub aaaUnderstand e limitação | Microsoft Docs"
description: "Guia do desenvolvedor - descrição das cotas de saudação que se aplicam a tooIoT Hub e hello esperado comportamento de limitação."
services: iot-hub
documentationcenter: .net
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 425e1b08-8789-4377-85f7-c13131fae4ce
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 06/16/2017
ms.author: dobett
ms.openlocfilehash: 023fa29bfbfb1de35708d6d121a1c56b50adfed9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="reference---iot-hub-quotas-and-throttling"></a>Referência - Cotas e limitação do Hub IoT

## <a name="quotas-and-throttling"></a>Cotas e limitação
Cada assinatura do Azure pode ter no máximo 10 hubs IoT e pelo menos 1 hub Gratuito.

Cada hub IoT é provisionado com um determinado número de unidades em um SKU específico (para obter mais informações, veja [Preços do Hub IoT do Azure][lnk-pricing]). Olá SKU e o número de unidades determinam cota diária máximo de saudação de mensagens que você pode enviar.

Olá SKU também determina Olá limites de IoT Hub impõe em todas as operações de limitação.

## <a name="operation-throttles"></a>Restrições de operação
Aceleradores de operação são os limites de taxa que são aplicados em intervalos de minuto Olá e se destina a tooavoid abuso. IoT Hub tentará tooavoid retornando erros sempre que possível, mas ele começa a retornar exceções se a limitação de saudação for violada por muito tempo.

Olá a seguinte tabela mostra Olá impostas limitações. Valores consulte hub individuais tooan.

| Restrição | Hubs Gratuitos e S1 | Hubs S2 | Hubs S3 | 
| -------- | ------- | ------- | ------- |
| Operações de registro de identidade (criar, recuperar, listar, atualizar, excluir) | 1,67/s/unidade (100/min/unidade) | 1,67/s/unidade (100/min/unidade) | 83,33/s/unidade (5000/min/unidade) |
| Conexões do dispositivo | Máximo de 100/s ou 12/s/unidade <br/> Por exemplo, duas unidades de S1 são 2\*12 = 24/s, mas você tem pelo menos 100/s em suas unidades. Com nove unidades S1 você tem 108/s (9\*12) em suas unidades. | 120/s/unidade | 6000/s/unidade |
| Envios do dispositivo para a nuvem | Máximo de 100/s ou 12/s/unidade <br/> Por exemplo, duas unidades de S1 são 2\*12 = 24/s, mas você tem pelo menos 100/s em suas unidades. Com nove unidades S1 você tem 108/s (9\*12) em suas unidades. | 120/s/unidade | 6000/s/unidade |
| Envios da nuvem para o dispositivo | 1,67/s/unidade (100/min/unidade) | 1,67/s/unidade (100/min/unidade) | 83,33/s/unidade (5000/min/unidade) |
| Recebimentos da nuvem para o dispositivo <br/> (somente quando o dispositivo usar HTTP)| 16,67/s/unidade (1000/min/unidade) | 16,67/s/unidade (1000/min/unidade) | 833,33/s/unidade (50000/min/unidade) |
| Upload de arquivos | 1,67 notificações de carregamento de arquivo/s/unidade (100/min/unidade) | 1,67 notificações de carregamento de arquivo/s/unidade (100/min/unidade) | 83,33 notificações de carregamento de arquivo/s/unidade (5000/min/unidade) |
| Métodos diretos | 20/s/unidade | 60/s/unidade | 3000/s/unidade | 
| Leituras de dispositivo gêmeo | 10/s | Máximo de 10/s ou 1/s/unidade | 50/s/unidade |
| Atualizações de dispositivos gêmeos | 10/s | Máximo de 10/s ou 1/s/unidade | 50/s/unidade |
| Operações de trabalhos <br/> (criar, atualizar, listar, excluir) | 1,67/s/unidade (100/min/unidade) | 1,67/s/unidade (100/min/unidade) | 83,33/s/unidade (5000/min/unidade) |
| Taxa de transferência de operação de trabalhos por dispositivo | 10/s | Máximo de 10/s ou 1/s/unidade | 50/s/unidade |

É importante tooclarify que Olá *conexões de dispositivo* acelerador controla a taxa de saudação em que novas conexões de dispositivo podem ser estabelecidas com um hub IoT. Olá *conexões de dispositivo* acelerador não controla o número máximo de saudação de dispositivos conectados simultaneamente. limitação de saudação depende de vários Olá unidades que são provisionados para o hub IoT de saudação.

Por exemplo, se você comprar uma única unidade S1, obterá uma restrição de 100 conexões por segundo. Portanto, tooconnect 100.000 dispositivos, levará pelo menos 1000 segundos (aproximadamente 16 minutos). No entanto, você pode conectar ao mesmo tempo todos os seus dispositivos registrados no registro de identidade.

Para uma discussão aprofundada de IoT Hub limitação comportamento, consulte Olá postagem de blog [IoT Hub limitação e][lnk-throttle-blog].

> [!NOTE]
> A qualquer momento, é possível tooincrease cotas ou limites de aceleração aumentando o número de saudação de unidades provisionados em um hub IoT.
> 
> [!IMPORTANT]
> As operações de registro de identidade são destinadas ao uso no tempo de execução em cenários de provisionamento e gerenciamento de dispositivos. Há suporte para leitura ou atualização de grandes números de identidades de dispositivo por meio de [trabalhos de importação e exportação][lnk-importexport].
> 
> 

## <a name="other-limits"></a>Outros limites

IoT Hub impõe outros limites operacionais:

| Operação | Limite |
| --------- | ----- |
| URIs de upload de arquivos | 10000 URIs de SAS podem estar fora de uma conta de armazenamento ao mesmo tempo. <br/> 10 URIs de SAS/dispositivo podem estar fora ao mesmo tempo. |
| Trabalhos | Histórico de trabalho é retido backup too30 dias <br/> O máximo de trabalhos simultâneos é 1 (para Gratuito e S1, 5 (para S2), 10 (para S3). |
| Pontos de extremidade adicionais | Hubs SKU pagos podem ter 10 pontos de extremidade adicionais. Hubs SKU gratuitos podem ter um ponto de extremidade adicional. |
| Regras de roteamento de mensagem | Hubs SKU pagos podem ter 100 regras de roteamento. Hubs SKU gratuitos podem ter cinco regras de roteamento. |
| Mensagens do dispositivo para a nuvem | Tamanho máximo da mensagem 256 KB |
| Mensagens da nuvem para o dispositivo | Tamanho máximo da mensagem 64 KB |
| Mensagens da nuvem para o dispositivo | Máximo de mensagens pendentes para entrega é 50 |

> [!NOTE]
> Olá no momento, o número máximo de dispositivos que você pode se conectar tooa único IoT hub é 500.000. Se você quiser tooincrease esse limite, entre em contato com [Microsoft Support](https://azure.microsoft.com/support/options/).

## <a name="latency"></a>Latência
IoT Hub se esforça tooprovide baixa latência para todas as operações. No entanto, devido a condições de toonetwork e outros fatores imprevisíveis ele não garante uma latência máxima. Ao projetar sua solução, você deve:

* Evite fazer suposições sobre a latência máxima de saudação de qualquer operação de IoT Hub.
* Provisione o hub IoT dispositivos de tooyour mais próximos do hello região do Azure.
* Considere o uso de operações do Azure IoT borda tooperform sensíveis à latência em dispositivo de saudação ou em um dispositivo de gateway toohello fechar.

Várias unidades de Hub IoT afetam limitação, conforme descrito anteriormente, mas não oferecem nenhum benefício de latência nem garantia adicional.
No caso de aumentos inesperados na latência da operação, entre em contato com o [Suporte da Microsoft](https://azure.microsoft.com/support/options/).

## <a name="next-steps"></a>Próximas etapas
Outros tópicos de referência neste Guia do desenvolvedor do Hub IoT incluem:

* [Pontos de extremidade do Hub IoT][lnk-devguide-endpoints]
* [Linguagem de consulta do Hub IoT para dispositivos gêmeos, trabalhos e roteamento de mensagens][lnk-devguide-query]
* [Suporte ao MQTT do Hub IoT][lnk-devguide-mqtt]

[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-throttle-blog]: https://azure.microsoft.com/blog/iot-hub-throttling-and-you/
[lnk-importexport]: iot-hub-devguide-identity-registry.md#import-and-export-device-identities

[lnk-devguide-endpoints]: iot-hub-devguide-endpoints.md
[lnk-devguide-query]: iot-hub-devguide-query-language.md
[lnk-devguide-mqtt]: iot-hub-mqtt-support.md
