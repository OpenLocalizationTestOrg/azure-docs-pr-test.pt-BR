---
title: "esquemas de controle de aaaX12 para monitoramento de B2B - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Use X12 mensagens de toomonitor B2B esquemas de controle de transações em sua conta de integração do Azure."
author: padmavc
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: a5413f80-eaad-4bcf-b371-2ad0ef629c3d
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/27/2017
ms.author: LADocs; padmavc
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: ed1b338730214dcae12c367ebff025d7122328fe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="start-or-enable-tracking-of-x12-messages-toomonitor-success-errors-and-message-properties"></a>Iniciar ou habilitar o controle de X12 mensagens toomonitor êxito, erros e propriedades de mensagem
Você pode usar esses esquemas de rastreamento X12 no seu toohelp de conta de integração do Azure você monitorar transações entre empresas (B2B):

* Esquema de acompanhamento do conjunto de transações X12
* Esquema de acompanhamento de confirmação do conjunto de transações X12
* Esquema de acompanhamento de intercâmbio X12
* Esquema de acompanhamento de confirmação do intercâmbio X12
* Esquema de acompanhamento de grupo funcional X12
* Esquema de acompanhamento de confirmação do grupo funcional X12

## <a name="x12-transaction-set-tracking-schema"></a>Esquema de acompanhamento do conjunto de transações X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "transactionSetControlNumber": "",
                "CorrelationMessageId": "",
                "messageType": "",
                "isMessageFailed": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "needAk2LoopForValidMessages":  "",
                "segmentsCount": ""
            }
    }
````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| senderPartnerName | Cadeia de caracteres | O nome do parceiro do remetente da mensagem X12. (Opcional) |
| receiverPartnerName | Cadeia de caracteres | O nome do parceiro do destinatário da mensagem X12. (Opcional) |
| senderQualifier | Cadeia de caracteres | Qualificador de parceiro de envio. (Obrigatório) |
| senderIdentifier | Cadeia de caracteres | Identificador de parceiro de envio. (Obrigatório) |
| receiverQualifier | Cadeia de caracteres | Qualificador de parceiro de recebimento. (Obrigatório) |
| receiverIdentifier | Cadeia de caracteres | Identificador de parceiro de recebimento. (Obrigatório) |
| agreementName | Cadeia de caracteres | Nome da saudação X12 mensagens de saudação do contrato toowhich são resolvidas. (Opcional) |
| direction | Enum | Direção de fluxo de mensagens de saudação, receber ou enviar. (Obrigatório) |
| interchangeControlNumber | Cadeia de caracteres | Número de controle de intercâmbio. (Opcional) |
| functionalGroupControlNumber | Cadeia de caracteres | Número de controle funcional. (Opcional) |
| transactionSetControlNumber | Cadeia de caracteres | Número de controle de conjunto de transações. (Opcional) |
| CorrelationMessageId | Cadeia de caracteres | ID de mensagem de correlação. Uma combinação de {AgreementName}{*GroupControlNumber*}{TransactionSetControlNumber}. (Opcional) |
| messageType | Cadeia de caracteres | Tipo de documento ou conjunto de transações. (Opcional) |
| isMessageFailed | Booliano | Se a mensagem de saudação X12 falha. (Obrigatório) |
| isTechnicalAcknowledgmentExpected | Booliano | Se confirmação técnica hello está configurada no contrato Olá X12. (Obrigatório) |
| isFunctionalAcknowledgmentExpected | Booliano | Se confirmação funcional hello está configurada no contrato Olá X12. (Obrigatório) |
| needAk2LoopForValidMessages | Booliano | Se o loop Olá AK2 é necessária para uma mensagem válida. (Obrigatório) |
| segmentsCount | Número inteiro | Número de segmentos no conjunto de transação Olá X12. (Opcional) |

## <a name="x12-transaction-set-acknowledgement-tracking-schema"></a>Esquema de acompanhamento de confirmação do conjunto de transações X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "respondingtransactionSetControlNumber": "",
                "respondingTransactionSetId": "",
                "statusCode": "",
                "processingStatus": "",
                "CorrelationMessageId": ""
                "isMessageFailed": "",
                "ak2Segment": "",
                "ak3Segment": "",
                "ak5Segment": ""
            }
    }
````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| senderPartnerName | Cadeia de caracteres | O nome do parceiro do remetente da mensagem X12. (Opcional) |
| receiverPartnerName | Cadeia de caracteres | O nome do parceiro do destinatário da mensagem X12. (Opcional) |
| senderQualifier | Cadeia de caracteres | Qualificador de parceiro de envio. (Obrigatório) |
| senderIdentifier | Cadeia de caracteres | Identificador de parceiro de envio. (Obrigatório) |
| receiverQualifier | Cadeia de caracteres | Qualificador de parceiro de recebimento. (Obrigatório) |
| receiverIdentifier | Cadeia de caracteres | Identificador de parceiro de recebimento. (Obrigatório) |
| agreementName | Cadeia de caracteres | Nome da saudação X12 mensagens de saudação do contrato toowhich são resolvidas. (Opcional) |
| direction | Enum | Direção de fluxo de mensagens de saudação, receber ou enviar. (Obrigatório) |
| interchangeControlNumber | Cadeia de caracteres | Número de controle da confirmação funcional Olá de intercâmbio. Valor preenche apenas para o lado de envio de saudação onde recebimento da confirmação funcional para Olá toopartner de mensagens enviadas. (Opcional) |
| functionalGroupControlNumber | Cadeia de caracteres | Número de controle de grupo funcional de confirmação funcional hello. Valor preenche apenas para o lado de envio de saudação onde recebimento da confirmação funcional para Olá toopartner de mensagens enviadas. (Opcional) |
| isaSegment | Cadeia de caracteres | Segmento ISA de mensagem de saudação. Valor preenche apenas para o lado de envio de saudação onde recebimento da confirmação funcional para Olá toopartner de mensagens enviadas. (Opcional) |
| gsSegment | Cadeia de caracteres | Segmento de GS de mensagem de saudação. Valor preenche apenas para o lado de envio de saudação onde recebimento da confirmação funcional para Olá toopartner de mensagens enviadas. (Opcional) |
| respondingfunctionalGroupControlNumber | Cadeia de caracteres | O número de controle de intercâmbio de resposta. (Opcional) |
| respondingFunctionalGroupId | Cadeia de caracteres | Respondendo a ID de grupo funcional, que mapeia tooAK101 na confirmação de saudação. (Opcional) |
| respondingtransactionSetControlNumber | Cadeia de caracteres | Número de controle de conjunto de transações de resposta. (Opcional) |
| respondingTransactionSetId | Cadeia de caracteres | ID, que mapeia tooAK201 na confirmação de saudação do conjunto de transação está respondendo. (Opcional) |
| statusCode | Booliano | O código de status de confirmação do conjunto de transações. (Obrigatório) |
| segmentsCount | Enum | O código de status de confirmação. Os valores aceitos são **Accepted**, **Rejected**, **AcceptedWithErrors**. (Obrigatório) |
| processingStatus | Enum | Status do processamento de confirmação de saudação. Os valores permitidos são **Received**, **Generated**, **Sent**. (Obrigatório) |
| CorrelationMessageId | Cadeia de caracteres | ID de mensagem de correlação. Uma combinação de {AgreementName}{*GroupControlNumber*}{TransactionSetControlNumber}. (Opcional) |
| isMessageFailed | Booliano | Se a mensagem de saudação X12 falha. (Obrigatório) |
| ak2Segment | Cadeia de caracteres | Confirmação de um conjunto de transações em Olá recebeu grupo funcional. (Opcional) |
| ak3Segment | Cadeia de caracteres | Relata erros em um segmento de dados. (Opcional) |
| ak5Segment | Cadeia de caracteres | Informa se a transação Olá definir identificada no segmento Olá AK2 é aceitas ou rejeitada e por quê. (Opcional) |

## <a name="x12-interchange-tracking-schema"></a>Esquema de acompanhamento de intercâmbio X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "isa09": "",
                "isa10": "",
                "isa11": "",
                "isa12": "",
                "isa14": "",
                "isa15": "",
                "isa16": ""
            }
    }
````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| senderPartnerName | Cadeia de caracteres | O nome do parceiro do remetente da mensagem X12. (Opcional) |
| receiverPartnerName | Cadeia de caracteres | O nome do parceiro do destinatário da mensagem X12. (Opcional) |
| senderQualifier | Cadeia de caracteres | Qualificador de parceiro de envio. (Obrigatório) |
| senderIdentifier | Cadeia de caracteres | Identificador de parceiro de envio. (Obrigatório) |
| receiverQualifier | Cadeia de caracteres | Qualificador de parceiro de recebimento. (Obrigatório) |
| receiverIdentifier | Cadeia de caracteres | Identificador de parceiro de recebimento. (Obrigatório) |
| agreementName | Cadeia de caracteres | Nome da saudação X12 mensagens de saudação do contrato toowhich são resolvidas. (Opcional) |
| direction | Enum | Direção de fluxo de mensagens de saudação, receber ou enviar. (Obrigatório) |
| interchangeControlNumber | Cadeia de caracteres | Número de controle de intercâmbio. (Opcional) |
| isaSegment | Cadeia de caracteres | Segmento ISA de mensagem. (Opcional) |
| isTechnicalAcknowledgmentExpected | Booliano | Se confirmação técnica hello está configurada no contrato Olá X12. (Obrigatório) |
| isMessageFailed | Booliano | Se a mensagem de saudação X12 falha. (Obrigatório) |
| isa09 | Cadeia de caracteres | A data de intercâmbio do documento X12. (Opcional) |
| isa10 | Cadeia de caracteres | A hora de intercâmbio do documento X12. (Opcional) |
| isa11 | Cadeia de caracteres | O identificador de Padrões de Controle de intercâmbio X12. (Opcional) |
| isa12 | Cadeia de caracteres | O número de versão de controle de intercâmbio X12. (Opcional) |
| isa14 | Cadeia de caracteres | A confirmação do X12 é solicitada. (Opcional) |
| isa15 | Cadeia de caracteres | O indicador de teste ou produção. (Opcional) |
| isa16 | Cadeia de caracteres | Separador de elementos. (Opcional) |

## <a name="x12-interchange-acknowledgement-tracking-schema"></a>Esquema de acompanhamento de confirmação do intercâmbio X12
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "isaSegment": "",
                "respondingInterchangeControlNumber": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ta102": "",
                "ta103": "",
                "ta105": ""
            }
    }
````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| senderPartnerName | Cadeia de caracteres | O nome do parceiro do remetente da mensagem X12. (Opcional) |
| receiverPartnerName | Cadeia de caracteres | O nome do parceiro do destinatário da mensagem X12. (Opcional) |
| senderQualifier | Cadeia de caracteres | Qualificador de parceiro de envio. (Obrigatório) |
| senderIdentifier | Cadeia de caracteres | Identificador de parceiro de envio. (Obrigatório) |
| receiverQualifier | Cadeia de caracteres | Qualificador de parceiro de recebimento. (Obrigatório) |
| receiverIdentifier | Cadeia de caracteres | Identificador de parceiro de recebimento. (Obrigatório) |
| agreementName | Cadeia de caracteres | Nome da saudação X12 mensagens de saudação do contrato toowhich são resolvidas. (Opcional) |
| direction | Enum | Direção de fluxo de mensagens de saudação, receber ou enviar. (Obrigatório) |
| interchangeControlNumber | Cadeia de caracteres | Número de controle da confirmação técnica de saudação recebidos de parceiros de intercâmbio. (Opcional) |
| isaSegment | Cadeia de caracteres | Segmento ISA para confirmação técnica de saudação recebidos de parceiros. (Opcional) |
| respondingInterchangeControlNumber |Cadeia de caracteres | Número de controle para confirmação técnica de saudação recebidos de parceiros de intercâmbio. (Opcional) |
| isMessageFailed | Booliano | Se a mensagem de saudação X12 falha. (Obrigatório) |
| statusCode | Enum | O código de status de confirmação do intercâmbio. Os valores aceitos são **Accepted**, **Rejected**, **AcceptedWithErrors**. (Obrigatório) |
| processingStatus | Enum | Status de confirmação. Os valores permitidos são **Received**, **Generated**, **Sent**. (Obrigatório) |
| ta102 | Cadeia de caracteres | Data do intercâmbio. (Opcional) |
| ta103 | Cadeia de caracteres | Hora do intercâmbio. (Opcional) |
| ta105 | Cadeia de caracteres | Código de observação de intercâmbio. (Opcional) |

## <a name="x12-functional-group-tracking-schema"></a>Esquema de acompanhamento de grupo funcional X12
````java

    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "gsSegment": "",
                "isTechnicalAcknowledgmentExpected": "",
                "isFunctionalAcknowledgmentExpected": "",
                "isMessageFailed": "",
                "gs01": "",
                "gs02": "",
                "gs03": "",
                "gs04": "",
                "gs05": "",
                "gs07": "",
                "gs08": ""
            }
    }
````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| senderPartnerName | Cadeia de caracteres | O nome do parceiro do remetente da mensagem X12. (Opcional) |
| receiverPartnerName | Cadeia de caracteres | O nome do parceiro do destinatário da mensagem X12. (Opcional) |
| senderQualifier | Cadeia de caracteres | Qualificador de parceiro de envio. (Obrigatório) |
| senderIdentifier | Cadeia de caracteres | Identificador de parceiro de envio. (Obrigatório) |
| receiverQualifier | Cadeia de caracteres | Qualificador de parceiro de recebimento. (Obrigatório) |
| receiverIdentifier | Cadeia de caracteres | Identificador de parceiro de recebimento. (Obrigatório) |
| agreementName | Cadeia de caracteres | Nome da saudação X12 mensagens de saudação do contrato toowhich são resolvidas. (Opcional) |
| direction | Enum | Direção de fluxo de mensagens de saudação, receber ou enviar. (Obrigatório) |
| interchangeControlNumber | Cadeia de caracteres | Número de controle de intercâmbio. (Opcional) |
| functionalGroupControlNumber | Cadeia de caracteres | Número de controle funcional. (Opcional) |
| gsSegment | Cadeia de caracteres | Segmento GS de mensagem. (Opcional) |
| isTechnicalAcknowledgmentExpected | Booliano | Se confirmação técnica hello está configurada no contrato Olá X12. (Obrigatório) |
| isFunctionalAcknowledgmentExpected | Booliano | Se confirmação funcional hello está configurada no contrato Olá X12. (Obrigatório) |
| isMessageFailed | Booliano | Se a mensagem de saudação X12 falha. (Obrigatório)|
| gs01 | Cadeia de caracteres | O código do identificador funcional. (Opcional) |
| gs02 | Cadeia de caracteres | O código do remetente do aplicativo. (Opcional) |
| gs03 | Cadeia de caracteres | O código do receptor do aplicativo. (Opcional) |
| gs04 | Cadeia de caracteres | Data de grupo funcional. (Opcional) |
| gs05 | Cadeia de caracteres | Hora de grupo funcional. (Opcional) |
| gs07 | Cadeia de caracteres | Código da agência responsável. (Opcional) |
| gs08 | Cadeia de caracteres | Código de identificador de versão/lançamento/setor. (Opcional) |

## <a name="x12-functional-group-acknowledgement-tracking-schema"></a>Esquema de acompanhamento de confirmação do grupo funcional X12
````java
    {
            "agreementProperties": {
                "senderPartnerName": "",
                "receiverPartnerName": "",
                "senderQualifier": "",
                "senderIdentifier": "",
                "receiverQualifier": "",
                "receiverIdentifier": "",
                "agreementName": ""
            },
            "messageProperties": {
                "direction": "",
                "interchangeControlNumber": "",
                "functionalGroupControlNumber": "",
                "isaSegment": "",
                "gsSegment": "",
                "respondingfunctionalGroupControlNumber": "",
                "respondingFunctionalGroupId": "",
                "isMessageFailed": "",
                "statusCode": "",
                "processingStatus": "",
                "ak903": "",
                "ak904": "",
                "ak9Segment": ""
            }
    }
````

| Propriedade | Tipo | Descrição |
| --- | --- | --- |
| senderPartnerName | Cadeia de caracteres | O nome do parceiro do remetente da mensagem X12. (Opcional) |
| receiverPartnerName | Cadeia de caracteres | O nome do parceiro do destinatário da mensagem X12. (Opcional) |
| senderQualifier | Cadeia de caracteres | Qualificador de parceiro de envio. (Obrigatório) |
| senderIdentifier | Cadeia de caracteres | Identificador de parceiro de envio. (Obrigatório) |
| receiverQualifier | Cadeia de caracteres | Qualificador de parceiro de recebimento. (Obrigatório) |
| receiverIdentifier | Cadeia de caracteres | Identificador de parceiro de recebimento. (Obrigatório) |
| agreementName | Cadeia de caracteres | Nome da saudação X12 mensagens de saudação do contrato toowhich são resolvidas. (Opcional) |
| direction | Enum | Direção de fluxo de mensagens de saudação, receber ou enviar. (Obrigatório) |
| interchangeControlNumber | Cadeia de caracteres | Número de controle de intercâmbio, que preenche para o lado de envio de saudação quando uma confirmação técnica é recebida de parceiros. (Opcional) |
| functionalGroupControlNumber | Cadeia de caracteres | Número de controle de grupo funcional de confirmação técnica hello, que preenche para Olá lado de envio quando uma confirmação técnica é recebida de parceiros. (Opcional) |
| isaSegment | Cadeia de caracteres | O mesmo que o número de controle de intercâmbio, só é populado em casos específicos. (Opcional) |
| gsSegment | Cadeia de caracteres | O mesmo que o número de controle de grupo funcional, só é populado em casos específicos. (Opcional) |
| respondingfunctionalGroupControlNumber | Cadeia de caracteres | Número de controle de grupo funcional original de saudação. (Opcional) |
| respondingFunctionalGroupId | Cadeia de caracteres | Mapeia tooAK101 na ID de grupo funcional de confirmação do hello. (Opcional) |
| isMessageFailed | Booliano | Se a mensagem de saudação X12 falha. (Obrigatório) |
| statusCode | Enum | O código de status de confirmação. Os valores aceitos são **Accepted**, **Rejected**, **AcceptedWithErrors**. (Obrigatório) |
| processingStatus | Enum | Status do processamento de confirmação de saudação. Os valores permitidos são **Received**, **Generated**, **Sent**. (Obrigatório) |
| ak903 | Cadeia de caracteres | Número de conjuntos de transação recebidos. (Opcional) |
| ak904 | Cadeia de caracteres | Número de conjuntos de transações aceitas em grupo funcional de saudação identificado. (Opcional) |
| ak9Segment | Cadeia de caracteres | Se o grupo funcional de saudação identificado no segmento Olá AK1 é aceitas ou rejeitado e por quê. (Opcional) |

## <a name="next-steps"></a>Próximas etapas
* Saiba mais sobre o [monitoramento de mensagens de B2B](logic-apps-monitor-b2b-message.md).
* Saiba mais sobre os [esquemas de acompanhamento AS2](../logic-apps/logic-apps-track-integration-account-as2-tracking-schemas.md).
* Saiba mais sobre os esquemas de [acompanhamento personalizado B2B](../logic-apps/logic-apps-track-integration-account-custom-tracking-schema.md).
* Saiba mais sobre [acompanhamento de mensagens B2B no portal do Operations Management Suite Olá](../logic-apps/logic-apps-track-b2b-messages-omsportal.md).
* Saiba mais sobre Olá [Enterprise Integration Pack](../logic-apps/logic-apps-enterprise-integration-overview.md).  
