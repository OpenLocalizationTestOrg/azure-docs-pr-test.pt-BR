---
title: "esquemas de controle de aaaAS2 para monitoramento de B2B - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Usar AS2 mensagens de toomonitor B2B esquemas de controle de transações em sua conta de integração do Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: f169c411-1bd7-4554-80c1-84351247bf94
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: fe3c5845e2e80160d6857d8c308d836e88af7331
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-as2-messages-and-mdns-toomonitor-success-errors-and-message-properties"></a>Iniciar ou habilitar o rastreamento de mensagens AS2 e MDNs toomonitor êxito, erros e propriedades de mensagem
Você pode usar esses esquemas de rastreamento AS2 no seu toohelp de conta de integração do Azure você monitorar transações entre empresas (B2B):

* Esquema de acompanhamento de mensagens AS2
* Esquema de acompanhamento MDN AS2

## <a name="as2-message-tracking-schema"></a>Esquema de acompanhamento de mensagens AS2
````java

    {
       "agreementProperties": {  
            "senderPartnerName": "",  
            "receiverPartnerName": "",  
            "as2To": "",  
            "as2From": "",  
            "agreementName": ""  
        },  
        "messageProperties": {
            "direction": "",
            "messageId": "",
            "dispositionType": "",
            "fileName": "",
            "isMessageFailed": "",
            "isMessageSigned": "",
            "isMessageEncrypted": "",
            "isMessageCompressed": "",
            "correlationMessageId": "",
            "incomingHeaders": {
            },
            "outgoingHeaders": {
            },
        "isNrrEnabled": "",
        "isMdnExpected": "",
        "mdnType": ""
        }
    }
````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| senderPartnerName | Cadeia de caracteres | O nome do parceiro do remetente da mensagem AS2. (Opcional) |
| receiverPartnerName | Cadeia de caracteres | O nome do parceiro do destinatário da mensagem AS2. (Opcional) |
| as2To | Cadeia de caracteres | Nome do destinatário da mensagem AS2, dos cabeçalhos de saudação de mensagem de saudação AS2. (Obrigatório) |
| as2From | Cadeia de caracteres | Nome do remetente da mensagem AS2, dos cabeçalhos de saudação de mensagem de saudação AS2. (Obrigatório) |
| agreementName | Cadeia de caracteres | Nome de mensagens de saudação do hello AS2 contrato toowhich são resolvidos. (Opcional) |
| direction | Cadeia de caracteres | Direção de fluxo de mensagens de saudação, receber ou enviar. (Obrigatório) |
| messageId | Cadeia de caracteres | ID da mensagem AS2, dos cabeçalhos de saudação de mensagem de saudação AS2 (opcional) |
| dispositionType |Cadeia de caracteres | Valor do tipo de disposição MDN (notificação de disposição de mensagem). (Opcional) |
| fileName | Cadeia de caracteres | Nome do arquivo de cabeçalho de saudação da mensagem de saudação AS2. (Opcional) |
| isMessageFailed |Booliano | Se a mensagem de saudação AS2 falha. (Obrigatório) |
| isMessageSigned | Booliano | Se a mensagem de saudação AS2 foi assinada. (Obrigatório) |
| isMessageEncrypted | Booliano | Se a mensagem de saudação AS2 foi criptografada. (Obrigatório) |
| isMessageCompressed |Booliano | Se a mensagem de saudação AS2 foi compactada. (Obrigatório) |
| correlationMessageId | Cadeia de caracteres | ID da mensagem AS2, mensagens de toocorrelate com MDNs. (Opcional) |
| incomingHeaders |Dicionário de JToken | Detalhes do cabeçalho da mensagem de entrada AS2. (Opcional) |
| outgoingHeaders |Dicionário de JToken | Detalhes do cabeçalho da mensagem de saída AS2. (Opcional) |
| isNrrEnabled | Booliano | Use o valor padrão se o valor de saudação não é conhecido. (Obrigatório) |
| isMdnExpected | Booliano | Use o valor padrão se o valor de saudação não é conhecido. (Obrigatório) |
| mdnType | Enum | Os valores permitidos são **NotConfigured**, **Sync** e **Async**. (Obrigatório) |

## <a name="as2-mdn-tracking-schema"></a>Esquema de acompanhamento MDN AS2
````java

    {
        "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "as2To": "",
                "as2From": "",
                "agreementName": "g"
            },
            "messageProperties": {
                "direction": "",
                "messageId": "",
                "originalMessageId": "",
                "dispositionType": "",
                "isMessageFailed": "",
                "isMessageSigned": "",
                "isNrrEnabled": "",
                "statusCode": "",
                "micVerificationStatus": "",
                "correlationMessageId": "",
                "incomingHeaders": {
                },
                "outgoingHeaders": {
                }
            }
    }
````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| senderPartnerName | Cadeia de caracteres | O nome do parceiro do remetente da mensagem AS2. (Opcional) |
| receiverPartnerName | Cadeia de caracteres | O nome do parceiro do destinatário da mensagem AS2. (Opcional) |
| as2To | Cadeia de caracteres | Nome do parceiro que recebe a mensagem de saudação AS2. (Obrigatório) |
| as2From | Cadeia de caracteres | Nome do parceiro que envia a mensagem de saudação AS2. (Obrigatório) |
| agreementName | Cadeia de caracteres | Nome de mensagens de saudação do hello AS2 contrato toowhich são resolvidos. (Opcional) |
| direction |Cadeia de caracteres | Direção de fluxo de mensagens de saudação, receber ou enviar. (Obrigatório) |
| messageId | Cadeia de caracteres | ID da mensagem AS2. (Opcional) |
| originalMessageId |Cadeia de caracteres | ID da mensagem AS2 original. (Opcional) |
| dispositionType | Cadeia de caracteres | Valor do tipo de disposição MDN. (Opcional) |
| isMessageFailed |Booliano | Se a mensagem de saudação AS2 falha. (Obrigatório) |
| isMessageSigned |Booliano | Se a mensagem de saudação AS2 foi assinada. (Obrigatório) |
| isNrrEnabled | Booliano | Use o valor padrão se o valor de saudação não é conhecido. (Obrigatório) |
| statusCode | Enum | Os valores aceitos são **Accepted**, **Rejected**, **AcceptedWithErrors**. (Obrigatório) |
| micVerificationStatus | Enum | Os valores permitidos são **NotApplicable**, **Succeeded** ou **Failed**. (Obrigatório) |
| correlationMessageId | Cadeia de caracteres | ID de correlação. ID de mensagem de saudação original (Olá ID da mensagem de saudação para o qual MDN é configurada). (Opcional) |
| incomingHeaders | Dicionário de JToken | Indica detalhes do cabeçalho da mensagem de entrada. (Opcional) |
| outgoingHeaders |Dicionário de JToken | Indica detalhes do cabeçalho da mensagem de saída. (Opcional) |

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre Olá [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).    
* Saiba mais sobre o [monitoramento de mensagens de B2B](logic-apps-monitor-b2b-message.md).   
* Saiba mais sobre os esquemas de [acompanhamento personalizado B2B](logic-apps-track-integration-account-custom-tracking-schema.md).   
* Saiba mais sobre os [esquemas de acompanhamento X12](logic-apps-track-integration-account-x12-tracking-schema.md).   
* Saiba mais sobre [acompanhamento de mensagens B2B no portal do Operations Management Suite Olá](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
