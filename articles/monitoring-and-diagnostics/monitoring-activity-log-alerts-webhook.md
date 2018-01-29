---
title: "Noções básicas sobre o esquema de webhook usado em alertas do log de atividades | Microsoft Docs"
description: "Saiba mais sobre o esquema JSON que é enviado para uma URL de webhook quando um alerta do log de atividades é ativado."
author: johnkemnetz
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
ms.openlocfilehash: 7816efd44c01c3ed60c95d8699042f89cf6de5ec
ms.sourcegitcommit: 9292e15fc80cc9df3e62731bafdcb0bb98c256e1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2018
---
# <a name="webhooks-for-azure-activity-log-alerts"></a>Webhook para alertas de log de atividades do Azure
Como parte da definição de um grupo de ações, você pode configurar pontos de extremidade de webhook para receber notificações de alerta do log de atividades. Os webhooks permitem rotear uma notificação de alerta do Azure para outros sistemas para pós-processamento ou notificações personalizadas. Este artigo mostra a aparência do conteúdo para o HTTP POST para um webhook.

Para saber mais sobre alertas do log de atividades, veja como [Criar alertas do log de atividades do Azure](monitoring-activity-log-alerts.md).

Para saber mais sobre grupos de ações, veja como [criar grupos de ações](monitoring-action-groups.md).

## <a name="authenticate-the-webhook"></a>Autenticar o webhook
Opcionalmente, o webhook pode usar a autorização baseada em token para autenticação. O URI do webhook é salvo com uma ID de token, por exemplo, `https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`.

## <a name="payload-schema"></a>Esquema de conteúdo
O conteúdo JSON contida na operação POST difere com base no campo de data.context.activityLog.eventSource do conteúdo.

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
    "schemaId": "Microsoft.Insights/activityLogs",
    "data": {
    "status": "Activated",
    "context": {
        "activityLog": {
        "channels": "Admin",
        "correlationId": "bbac944f-ddc0-4b4c-aa85-cc7dc5d5c1a6",
        "description": "Active: Virtual Machines - Australia East",
        "eventSource": "ServiceHealth",
        "eventTimestamp": "2017-10-18T23:49:25.3736084+00:00",
        "eventDataId": "6fa98c0f-334a-b066-1934-1a4b3d929856",
        "level": "Informational",
        "operationName": "Microsoft.ServiceHealth/incident/action",
        "operationId": "bbac944f-ddc0-4b4c-aa85-cc7dc5d5c1a6",
        "properties": {
            "title": "Virtual Machines - Australia East",
            "service": "Virtual Machines",
            "region": "Australia East",
            "communication": "Starting at 02:48 UTC on 18 Oct 2017 you have been identified as a customer using Virtual Machines in Australia East who may receive errors starting Dv2 Promo and DSv2 Promo Virtual Machines which are in a stopped &quot;deallocated&quot; or suspended state. Customers can still provision Dv1 and Dv2 series Virtual Machines or try deploying Virtual Machines in other regions, as a possible workaround. Engineers have identified a possible fix for the underlying cause, and are exploring implementation options. The next update will be provided as events warrant.",
            "incidentType": "Incident",
            "trackingId": "0NIH-U2O",
            "impactStartTime": "2017-10-18T02:48:00.0000000Z",
            "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"Australia East\"}],\"ServiceName\":\"Virtual Machines\"}]",
            "defaultLanguageTitle": "Virtual Machines - Australia East",
            "defaultLanguageContent": "Starting at 02:48 UTC on 18 Oct 2017 you have been identified as a customer using Virtual Machines in Australia East who may receive errors starting Dv2 Promo and DSv2 Promo Virtual Machines which are in a stopped &quot;deallocated&quot; or suspended state. Customers can still provision Dv1 and Dv2 series Virtual Machines or try deploying Virtual Machines in other regions, as a possible workaround. Engineers have identified a possible fix for the underlying cause, and are exploring implementation options. The next update will be provided as events warrant.",
            "stage": "Active",
            "communicationId": "636439673646212912",
            "version": "0.1.1"
        },
        "status": "Active",
        "subscriptionId": "45529734-0ed9-4895-a0df-44b59a5a07f9",
        "submissionTimestamp": "2017-10-18T23:49:28.7864349+00:00"
        }
    },
    "properties": {}
    }
}
```

Para obter detalhes de esquema específico sobre alertas de log de atividades de notificação do serviço integridade, veja [Notificações de integridade do serviço](monitoring-service-notifications.md). Além disso, saiba como [configurar notificações de webhook de integridade do serviço com suas soluções de gerenciamento de problemas existentes](../service-health/service-health-alert-webhook-guide.md).

Para obter detalhes de esquema específico em todos os outros alertas do log de atividades, veja [Visão geral do log de atividades do Azure](monitoring-overview-activity-logs.md).

| Nome do elemento | DESCRIÇÃO |
| --- | --- |
| status |Usado para alertas de métrica. Sempre definido como "ativado" para alertas do log de atividades. |
| context |Contexto do evento. |
| resourceProviderName |O provedor de recursos do recurso afetado. |
| conditionType |Sempre "Evento". |
| Nome |Nome da regra de alerta. |
| ID |ID do recurso do alerta. |
| Descrição |Descrição do alerta definida quando o alerta é criado. |
| subscriptionId |Id de assinatura do Azure. |
| timestamp |Hora quando o evento foi gerado pelo serviço do Azure que processou a solicitação. |
| ResourceId |ID de recurso do recurso afetado. |
| resourceGroupName |Nome do grupo de recursos do recurso afetado. |
| propriedades |Conjunto de pares `<Key, Value>` (ou seja, `Dictionary<String, String>`) que inclui detalhes sobre o evento. |
| evento |Elemento que contém metadados sobre o evento. |
| autorização |As propriedades de Controle de Acesso Baseado em Função do evento. Essas propriedades geralmente incluem a ação, função e escopo. |
| categoria |Categoria do evento. Os valores com suporte são: Administrativo, Alerta, Segurança, ServiceHealth e Recomendação. |
| chamador |Endereço de email do usuário que realizou a operação, declaração UPN ou declaração SPN com base na disponibilidade. Pode ser nulo para determinadas chamadas do sistema. |
| correlationId |Geralmente um GUID no formato de cadeia de caracteres. Eventos com correlationId pertencem à mesma ação maior e geralmente compartilham uma correlationId. |
| eventDescription |Descrição de texto estático do evento. |
| eventDataId |Identificador exclusivo do evento. |
| eventSource |Nome do serviço ou infraestrutura do Azure que gerou o evento. |
| httpRequest |A solicitação geralmente inclui o clientRequestId, clientIpAddress e método HTTP (por exemplo, PUT). |
| level |Um dos seguintes valores: Crítico, Erro, Aviso e Informativo. |
| operationId |Geralmente um GUID compartilhado entre os eventos correspondentes a uma única operação. |
| operationName |Nome da operação. |
| propriedades |Propriedades do evento. |
| status |Cadeia de caracteres. Status da operação. Os valores comuns incluem: Iniciado, Em Andamento, Êxito, Falha, Ativo, Resolvido. |
| subStatus |Geralmente inclui o código de status HTTP da chamada REST correspondente. Também pode incluir outras cadeias de caracteres que descrevam um substatus. Os valores de substatus comuns incluem: OK (Código de Status HTTP: 200), Criado (Código de Status HTTP: 201), Aceito (Código de Status HTTP: 202), Sem Conteúdo (Código de Status HTTP: 204), Solicitação Incorreta (Código de Status HTTP: 400), Não Encontrado (Código de Status HTTP: 404), Conflito (Código de Status HTTP: 409), Erro Interno do Servidor (Código de Status HTTP: 500), Serviço Indisponível (Código de Status HTTP: 503), Tempo Limite do Gateway (Código de Status HTTP: 504). |

## <a name="next-steps"></a>Próximas etapas
* [Leia mais sobre o log de atividades](monitoring-overview-activity-logs.md).
* [Exemplos de scripts da automação do Azure (Runbooks) em alertas do Azure](http://go.microsoft.com/fwlink/?LinkId=627081).
* [Usar aplicativo lógico para enviar um SMS por meio do Twilio de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). Este exemplo serve para alertas de métrica, mas pode ser modificado para funcionar com um alerta do log de atividades.
* [Usar aplicativo lógico para enviar uma mensagem do Slack de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). Este exemplo serve para alertas de métrica, mas pode ser modificado para funcionar com um alerta do log de atividades.
* [Usar aplicativo lógico para enviar uma mensagem a uma fila do Azure de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). Este exemplo serve para alertas de métrica, mas pode ser modificado para funcionar com um alerta do log de atividades.
