---
title: "aaaCustom controle esquemas para B2B monitoramento - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Crie esquemas de acompanhamento personalizado toomonitor B2B mensagens de transações em sua conta de integração do Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 433ae852-a833-44d3-a3c3-14cca33403a2
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 8cf26a43d89f0414a2a8c5ef59d804235afeb5d6
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="enable-tracking-toomonitor-your-complete-workflow-end-to-end"></a>Habilitar o acompanhamento toomonitor seu fluxo de trabalho completo, ponta a ponta
Há um acompanhamento interno que você pode habilitar para diferentes partes do fluxo de trabalho entre empresas, como acompanhamento de mensagens AS2 ou X12. Quando você criar fluxos de trabalho que inclui um lógica de aplicativo, BizTalk Server, SQL Server ou qualquer outra camada, você pode habilitar o controle personalizado que registra eventos de saudação início toohello final do fluxo de trabalho. 

Este tópico fornece código personalizado que você pode usar em camadas Olá fora de seu aplicativo lógico. 

## <a name="custom-tracking-schema"></a>Esquema de controle personalizado
````java

        {
            "sourceType": "",
            "source": {

            "workflow": {
                "systemId": ""
            },
            "runInstance": {
                "runId": ""
            },
            "operation": {
                "operationName": "",
                "repeatItemScopeName": "",
                "repeatItemIndex": "",
                "trackingId": "",
                "correlationId": "",
                "clientRequestId": ""
                }
            },
            "events": [
            {
                "eventLevel": "",
                "eventTime": "",
                "recordType": "",
                "record": {                
                }
            }
         ]
      }

````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| sourceType |   | Tipo de origem Olá executar. Os valores permitidos são **Microsoft.Logic/workflows** e **personalizado**. (Obrigatório) |
| Fonte |   | Se o tipo de origem de saudação é **Microsoft.Logic/workflows**, informações de fonte de saudação precisa toofollow desse esquema. Se o tipo de origem de saudação é **personalizado**, esquema de saudação é um JToken. (Obrigatório) |
| systemId | Cadeia de caracteres | ID do sistema de aplicativo lógico. (Obrigatório) |
| runId | Cadeia de caracteres | ID de execução do aplicativo lógico. (Obrigatório) |
| operationName | Cadeia de caracteres | Nome da operação de saudação (por exemplo, ações ou gatilho). (Obrigatório) |
| repeatItemScopeName | Cadeia de caracteres | Repita o nome do item se ação hello está dentro de um `foreach` / `until` loop. (Obrigatório) |
| repeatItemIndex | Número inteiro | Se a ação hello está dentro de um `foreach` / `until` loop. Indica o índice do item repetido hello. (Obrigatório) |
| trackingId | Cadeia de caracteres | ID de rastreamento, mensagens de saudação do toocorrelate. (Opcional) |
| correlationId | Cadeia de caracteres | ID de correlação, mensagens de saudação do toocorrelate. (Opcional) |
| clientRequestId | Cadeia de caracteres | Cliente pode preenchê-la toocorrelate mensagens. (Opcional) |
| eventLevel |   | Nível de evento hello. (Obrigatório) |
| eventTime |   | Hora do evento hello, no formato AAAA-MM-DDTHH:MM:SS.00000Z do UTC. (Obrigatório) |
| recordType |   | Tipo de registro de controle de saudação. O valor permitido é **personalizado**. (Obrigatório) |
| record |   | Tipo de registro personalizado. O formato permitido é JToken. (Obrigatório) |

## <a name="b2b-protocol-tracking-schemas"></a>Esquemas de acompanhamento do protocolo B2B
Para obter informações sobre esquemas de acompanhamento do protocolo B2B, veja:
* [Esquemas de acompanhamento de AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md)   
* [Esquemas de acompanhamento de X12](logic-apps-track-integration-account-x12-tracking-schema.md)

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre o [monitoramento de mensagens de B2B](logic-apps-monitor-b2b-message.md).   
* Saiba mais sobre [acompanhamento de mensagens B2B no portal do Operations Management Suite Olá](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Saiba mais sobre Olá [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).
