---
title: "preços do Azure IoT Hub aaaUnderstand | Microsoft Docs"
description: "Guia do desenvolvedor ‑ informações sobre como a medição e preço funcionam no Hub IoT, incluindo exemplos funcionais."
services: iot-hub
documentationcenter: 
author: dominicbetts
manager: timlt
editor: 
ms.assetid: 1ac90923-1edf-4134-bbd4-77fee9b68d24
ms.service: iot-hub
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/12/2016
ms.author: elioda
ms.openlocfilehash: e294c0b7f483e042ca3f63e93c14e0c2d773ae7f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-iot-hub-pricing-information"></a>Informações sobre preços do Hub IoT do Azure

[IoT Hub do Azure preços] [ lnk-pricing] fornece informações gerais de saudação em diferentes SKUs e preços para o IoT Hub. Este artigo contém detalhes adicionais sobre como as mensagens de saudação que várias funcionalidades de IoT Hub são monitoradas como pelo IoT Hub.

## <a name="charges-per-operation"></a>Encargos por operação

| Operação | Informações de cobrança | 
| --------- | ------------------- |
| Operações de registro de identidade <br/> (criar, recuperar, listar, atualizar e excluir) | Não será cobrado. |
| Mensagens do dispositivo para a nuvem | As mensagens enviadas com êxito são cobradas em partes de 4 KB na entrada no Hub IoT, por exemplo, uma mensagem de 6 KB é cobrada em 2 mensagens. |
| Mensagens da nuvem para o dispositivo | As mensagens enviadas com êxito são cobradas em partes de 4 KB, por exemplo, uma mensagem de 6 KB é cobrada em 2 mensagens. |
| Carregamentos de arquivos | Transferência de arquivo tooAzure armazenamento não é monitorado pelo IoT Hub. Mensagens de conclusão e inicialização de transferência de arquivo são cobradas como mensagens limitadas com incrementos de 4 KB. Por exemplo, a transferência de um arquivo de 10 MB é cobrado duas mensagens em adição toohello custos de armazenamento do Azure. |
| Métodos diretos | As solicitações de métodos bem-sucedidas são cobradas em partes de 4 KB, as respostas com corpos não vazios são cobradas em 4 KB como mensagens adicionais. Dispositivos de toodisconnected solicitações são cobrados como mensagens em blocos de 4 KB. Por exemplo, um método com um corpo de 6-KB que resulta em uma resposta sem corpo de dispositivo de saudação é cobrada como duas mensagens; um método com um corpo de 6-KB que resulta em uma resposta de 1 KB de dispositivo de saudação é cobrado como duas mensagens de solicitação de hello mais outra mensagem para resposta de saudação. |
| Leituras de dispositivo gêmeo | Duas dispositivo lê de dispositivo de saudação e de volta a solução Olá final é cobrado como mensagens em blocos de 512 bytes. Por exemplo, a leitura de um dispositivo gêmeo de 6 KB é cobrada como 12 mensagens. |
| Atualizações do dispositivo gêmeo (marcas e propriedades) | Atualizações do dispositivo duas do dispositivo hello e Olá são cobradas como mensagens em blocos de 512 bytes. Por exemplo, a leitura de um dispositivo gêmeo de 6 KB é cobrada como 12 mensagens. |
| Consultas de dispositivo gêmeo | Consultas são cobradas como mensagens dependendo do tamanho do resultado da saudação em blocos de 512 bytes. |
| Operações de trabalhos <br/> (criar, atualizar, listar, excluir) | Não será cobrado. |
| Operações de trabalhos por dispositivo | As operações de trabalhos (como atualizações de dispositivos gêmeos e métodos) são cobradas de forma normal. Por exemplo, um trabalho que resulta em 1000 chamadas de método com solicitações de 1 KB e respostas de corpo vazio é cobrado em 1000 mensagens. |

> [!NOTE]
> Todos os tamanhos são computados considerar o tamanho da carga Olá em bytes (quadros de protocolo é ignorado). No caso de mensagens (que têm propriedades e corpo) tamanho Olá é calculado de maneira independente de protocolo, conforme descrito em Olá [IoT Hub guia do desenvolvedor do sistema de mensagens][lnk-message-size].

## <a name="example-1"></a>Exemplo 1

Um dispositivo envia uma mensagem de dispositivo para a nuvem de 1 KB por minuto tooIoT Hub, que é então lidos pelo Azure Stream Analytics. back-end de solução Olá invoca um método (com a carga de 512 bytes) no dispositivo Olá tootrigger cada dez minutos uma ação específica. dispositivo Olá responde toohello método com um resultado de 200 bytes.

dispositivo Olá consome 1 mensagem * 60 minutos * 24 horas = 1440 mensagens por dia para mensagens de saudação do dispositivo para nuvem e 2 solicitação e resposta * 6 vezes por hora * 24 horas = 288 mensagens para métodos hello, para um total de 1728 mensagens por dia.

## <a name="example-2"></a>Exemplo 2:

Um dispositivo envia uma mensagem de 100 KB do dispositivo para a nuvem a cada hora. Ele também atualiza seu dispositivo gêmeo com cargas de 1 KB a cada 4 horas. solução de saudação volta terminar, uma vez por dia, leituras Olá 14 KB dispositivo duas e atualiza com configurações de toochange cargas de 512 bytes.

dispositivo Olá consome 25 mensagens de (100KB / 4KB) * 24 horas para que as mensagens de dispositivo para nuvem, além de 1 mensagem * 6 vezes por dia para atualizações de duas do dispositivo, para um total de 156 mensagens por dia.
Olá back-end solução consome duas de dispositivo (14KB/0,5 KB) de 28 mensagens tooread hello, mais 1 mensagem tooupdate-lo para um total de mensagens de 29.

No total, dispositivo hello e back-end de solução Olá consumir 185 mensagens por dia.


[lnk-pricing]: https://azure.microsoft.com/pricing/details/iot-hub
[lnk-message-size]: iot-hub-devguide-messages-construct.md
