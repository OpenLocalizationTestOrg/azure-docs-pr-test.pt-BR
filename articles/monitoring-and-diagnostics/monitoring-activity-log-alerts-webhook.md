---
title: "esquema de webhook Olá aaaUnderstand usada em alertas de log de atividade | Microsoft Docs"
description: "Saiba mais sobre o esquema de saudação do hello JSON que é postada a URL do webhook tooa quando um alerta de log de atividade ativa."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/31/2017
ms.author: johnkem
ms.openlocfilehash: 75562e0589222d3e392ea73eacfd7414a422d115
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="webhooks-for-azure-activity-log-alerts"></a>Webhook para alertas de log de atividades do Azure
Como parte da definição de saudação de um grupo de ação, você pode configurar notificações de alerta de log webhook pontos de extremidade tooreceive atividade. Com webhooks, você pode rotear esses sistemas de tooother notificações para ações de pós-processamento ou personalizados. Este artigo mostra quais carga Olá Olá HTTP POST tooa webhook parece.

Para obter mais informações sobre alertas de log de atividade, consulte como muito[criar alertas de log de atividades do Azure](monitoring-activity-log-alerts.md).

Para obter informações sobre grupos de ação, consulte como muito[criar grupos de ação](monitoring-action-groups.md).

## <a name="authenticate-hello-webhook"></a>Autenticar Olá webhook
Olá webhook pode usar opcionalmente a autorização baseada em token para autenticação. Olá webhook URI é salvo com uma ID de token, por exemplo, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.

## <a name="payload-schema"></a>Esquema de conteúdo
carga JSON Olá contida em Olá operação POST varia com base no campo de data.context.activityLog.eventSource da carga de saudação.

###<a name="common"></a>Comum
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "channels": "Operation",
                "correlationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "eventSource": "Administrative",
                "eventTimestamp": "2017-03-29T15:43:08.0019532+00:00",
                "eventDataId": "8195a56a-85de-4663-943e-1a2bf401ad94",
                "level": "Informational",
                "operationName": "Microsoft.Insights/actionGroups/write",
                "operationId": "6ac88262-43be-4adf-a11c-bd2179852898",
                "status": "Started",
                "subStatus": "",
                "subscriptionId": "52c65f65-0518-4d37-9719-7dbbfc68c57a",
                "submissionTimestamp": "2017-03-29T15:43:20.3863637+00:00",
                ...
            }
        },
        "properties": {}
    }
}
```
###<a name="administrative"></a>Administrativo
```json
{
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "authorization": {
                    "action": "Microsoft.Insights/actionGroups/write",
                    "scope": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions"
                },
                "claims": "{...}",
                "caller": "me@contoso.com",
                "description": "",
                "httpRequest": "{...}",
                "resourceId": "/subscriptions/52c65f65-0518-4d37-9719-7dbbfc68c57b/resourceGroups/CONTOSO-TEST/providers/Microsoft.Insights/actionGroups/IncidentActions",
                "resourceGroupName": "CONTOSO-TEST",
                "resourceProviderName": "Microsoft.Insights",
                "resourceType": "Microsoft.Insights/actionGroups"
            }
        },
        "properties": {}
    }
}

```
###<a name="servicehealth"></a>ServiceHealth
```json
{
    "schemaId": "unknown",
    "data": {
        "status": "Activated",
        "context": {
            "activityLog": {
                "properties": {
                    "title": "...",
                    "service": "...",
                    "region": "...",
                    "communication": "...",
                    "incidentType": "Incident",
                    "trackingId": "...",
                    "groupId": "...",
                    "impactStartTime": "3/29/2017 3:43:21 PM",
                    "impactMitigationTime": "3/29/2017 3:43:21 PM",
                    "eventCreationTime": "3/29/2017 3:43:21 PM",
                    "impactedServices": "[{...}]",
                    "defaultLanguageTitle": "...",
                    "defaultLanguageContent": "...",
                    "stage": "Active",
                    "communicationId": "...",
                    "version": "0.1"
                }
            }
        },
        "properties": {}
    }
}
```

Para obter detalhes de esquema específico sobre alertas de log de atividades de notificação do serviço integridade, veja [Notificações de integridade do serviço](monitoring-service-notifications.md).

Para obter detalhes de esquema específico em todos os outros alertas do log de atividade, consulte [visão geral do log de atividades do Azure Olá](monitoring-overview-activity-logs.md).

| Nome do elemento | Descrição |
| --- | --- |
| status |Usado para alertas de métrica. Sempre defina muito "ativado" para alertas de log de atividade. |
| context |Contexto do evento hello. |
| resourceProviderName |provedor de recursos de saudação do hello afetados recursos. |
| conditionType |Sempre "Evento". |
| name |Nome da regra de alerta de saudação. |
| ID |ID do recurso de alerta de saudação. |
| description |Descrição do alerta definida quando o alerta de saudação é criado. |
| subscriptionId |Id de assinatura do Azure. |
| timestamp |Hora na qual Olá evento foi gerado pelo saudação do serviço do Azure que processa Olá solicitação. |
| resourceId |ID do recurso da saudação afetados recursos. |
| resourceGroupName |Nome do grupo de recursos de saudação para Olá afetados recursos. |
| propriedades |Conjunto de `<Key, Value>` pares (ou seja, `Dictionary<String, String>`) que inclui detalhes sobre o evento hello. |
| evento |Elemento que contém metadados sobre o evento hello. |
| autorização |Propriedades de controle de acesso baseado em função Hello de evento hello. Geralmente, essas propriedades incluem hello ação, função hello e escopo de saudação. |
| categoria |Categoria de evento de saudação. Os valores com suporte são: Administrativo, Alerta, Segurança, ServiceHealth e Recomendação. |
| chamador |Endereço de email do usuário de saudação que realizou a operação hello, declaração UPN ou declaração SPN com base na disponibilidade. Pode ser nulo para determinadas chamadas do sistema. |
| correlationId |Geralmente um GUID no formato de cadeia de caracteres. Os eventos com correlationId pertencem toohello mesma ação maior e geralmente compartilham um correlationId. |
| eventDescription |Descrição de evento Olá texto estático. |
| eventDataId |Identificador exclusivo do evento hello. |
| eventSource |Nome do hello infraestrutura ou serviço do Azure que o evento Olá gerado. |
| httpRequest |Olá solicitação geralmente inclui Olá clientRequestId, clientIpAddress e método HTTP (por exemplo, colocar). |
| level |Uma saudação valores a seguir: crítico, erro, aviso, informativo e detalhado. |
| operationId |Normalmente um GUID compartilhado entre eventos Olá correspondente toosingle operação. |
| operationName |Nome da operação de saudação. |
| propriedades |Propriedades de evento de saudação. |
| status |Cadeia de caracteres. Status da operação de saudação. Os valores comuns incluem: Iniciado, Em Andamento, Êxito, Falha, Ativo, Resolvido. |
| subStatus |Geralmente inclui o código de status HTTP saudação da chamada REST correspondente de saudação. Também pode incluir outras cadeias de caracteres que descrevam um substatus. Os valores de substatus comuns incluem: OK (Código de Status HTTP: 200), Criado (Código de Status HTTP: 201), Aceito (Código de Status HTTP: 202), Sem Conteúdo (Código de Status HTTP: 204), Solicitação Incorreta (Código de Status HTTP: 400), Não Encontrado (Código de Status HTTP: 404), Conflito (Código de Status HTTP: 409), Erro Interno do Servidor (Código de Status HTTP: 500), Serviço Indisponível (Código de Status HTTP: 503), Tempo Limite do Gateway (Código de Status HTTP: 504). |

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre o log de atividades de saudação](monitoring-overview-activity-logs.md).
* [Exemplos de scripts da automação do Azure (Runbooks) em alertas do Azure](http://go.microsoft.com/fwlink/?LinkId=627081).
* [Usar um toosend de aplicativo um SMS por meio do Twilio lógica de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta de log de atividade.
* [Use um aplicativo de lógica toosend uma mensagem de margem de atraso de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta de log de atividade.
* [Usar um toosend do aplicativo de lógica de fila tooan uma mensagem do Azure de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta de log de atividade.
