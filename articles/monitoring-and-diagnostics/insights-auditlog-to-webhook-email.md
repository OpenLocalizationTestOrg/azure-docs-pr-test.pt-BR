---
title: aaaCall um webhook em alertas de Log de atividades do Azure | Microsoft Docs
description: "Serviços de tooother de eventos de log de atividades para ações personalizadas de rota. Por exemplo, envie SMS, registre bugs ou notifique uma equipe por meio do serviço de bate-papo/mensagens."
author: johnkemnetz
manager: orenr
editor: 
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.assetid: 64d333d1-7f37-4a00-9d16-dda6e69a113b
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: johnkem
ms.openlocfilehash: 9017ff3e5165857ec7084a8f07f4123552e55f73
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="call-a-webhook-on-azure-activity-log-alerts"></a>Chamar um webhook em alertas do Log de Atividades do Azure
Webhooks permitir tooroute um Azure alerta sistemas de notificação de tooother para ações de pós-processamento ou personalizados. Você pode usar um webhook em um alerta tooroute-tooservices que enviar SMS, bugs de log, notificar uma equipe por meio de serviços de chat/mensagens ou fazer várias outras ações. Este artigo descreve como tooset toobe um webhook chamado quando um dispara alertas de Log de atividades do Azure. Ele também mostra quais carga Olá Olá HTTP POST tooa webhook parece. Para obter informações sobre a instalação de saudação e esquema de um alerta de métrica do Azure, [consulte esta página em vez disso,](insights-webhooks-alerts.md). Você também pode configurar um email de alerta toosend do Log de atividades quando ativado.

> [!NOTE]
> Este recurso está atualmente em visualização e será removido em algum momento no futuro de saudação.
>
>

Você pode configurar um alerta de Log de atividades usando Olá [Cmdlets do PowerShell do Azure](insights-powershell-samples.md#create-metric-alerts), [CLI de plataforma cruzada](insights-cli-samples.md#work-with-alerts), ou [API REST do Azure Monitor](https://msdn.microsoft.com/library/azure/dn933805.aspx). No momento, você não pode definir um usando Olá portal do Azure.

## <a name="authenticating-hello-webhook"></a>Autenticando Olá webhook
Olá webhook pode autenticar usando um destes métodos:

1. **Autorização baseada em token** -Olá webhook URI é salvo com uma ID de token, por exemplo,`https://mysamplealert/webcallback?tokenid=sometokenid&someparameter=somevalue`
2. **Básicas de autorização** -Olá webhook URI é salvo com um nome de usuário e senha, por exemplo,`https://userid:password@mysamplealert/webcallback?someparamater=somevalue&foo=bar`

## <a name="payload-schema"></a>Esquema de conteúdo
Olá operação POST contém Olá carga JSON e o esquema para alertas todas baseadas no Log de atividades a seguir. Esse esquema é semelhante toohello um usado por alertas com base em métrica.

```
{
        "status": "Activated",
        "context": {
                "resourceProviderName": "Microsoft.Web",
                "event": {
                        "$type": "Microsoft.WindowsAzure.Management.Monitoring.Automation.Notifications.GenericNotifications.Datacontracts.InstanceEventContext, Microsoft.WindowsAzure.Management.Mon.Automation",
                        "authorization": {
                                "action": "Microsoft.Web/sites/start/action",
                                "scope": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest"
                        },
                        "eventDataId": "327caaca-08d7-41b1-86d8-27d0a7adb92d",
                        "category": "Administrative",
                        "caller": "myname@mycompany.com",
                        "httpRequest": {
                                "clientRequestId": "f58cead8-c9ed-43af-8710-55e64def208d",
                                "clientIpAddress": "104.43.166.155",
                                "method": "POST"
                        },
                        "status": "Succeeded",
                        "subStatus": "OK",
                        "level": "Informational",
                        "correlationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "eventDescription": "",
                        "operationName": "Microsoft.Web/sites/start/action",
                        "operationId": "4a40beaa-6a63-4d92-85c4-923a25abb590",
                        "properties": {
                                "$type": "Microsoft.WindowsAzure.Management.Common.Storage.CasePreservedDictionary, Microsoft.WindowsAzure.Management.Common.Storage",
                                "statusCode": "OK",
                                "serviceRequestId": "f7716681-496a-4f5c-8d14-d564bcf54714"
                        }
                },
                "timestamp": "Friday, March 11, 2016 9:13:23 PM",
                "id": "/subscriptions/s1/resourceGroups/rg1/providers/microsoft.insights/alertrules/alertonevent2",
                "name": "alertonevent2",
                "description": "test alert on event start",
                "conditionType": "Event",
                "subscriptionId": "s1",
                "resourceId": "/subscriptions/s1/resourcegroups/rg1/providers/Microsoft.Web/sites/leoalerttest",
                "resourceGroupName": "rg1"
        },
        "properties": {
                "key1": "value1",
                "key2": "value2"
        }
}
```

| Nome do elemento | Descrição |
| --- | --- |
| status |Usado para alertas de métrica. Sempre defina muito "ativado" para alertas de Log de atividades. |
| context |Contexto do evento hello. |
| resourceProviderName |provedor de recursos de saudação do hello afetados recursos. |
| conditionType |Sempre "Evento". |
| name |Nome da regra de alerta de saudação. |
| ID |ID do recurso de alerta de saudação. |
| description |Descrição do alerta conforme definido durante a criação de alerta de saudação. |
| subscriptionId |ID de assinatura do Azure. |
| timestamp |Hora na qual Olá evento foi gerado pelo saudação do serviço do Azure que processa Olá solicitação. |
| resourceId |ID do recurso da saudação afetados recursos. |
| resourceGroupName |Nome do grupo de recursos de saudação para Olá afetado recursos |
| propriedades |Conjunto de `<Key, Value>` pares (ou seja, `Dictionary<String, String>`) que inclui detalhes sobre o evento hello. |
| evento |Elemento que contém metadados sobre o evento hello. |
| autorização |propriedades RBAC saudação do evento hello. Isso geralmente inclui hello "ação", "função" hello "escopo e." |
| categoria |Categoria de evento de saudação. Os valores com suporte são: Administrativo, Alerta, Segurança, ServiceHealth, Recomendação. |
| chamador |Endereço de email do usuário de saudação que realizou a operação hello, declaração UPN ou declaração SPN com base na disponibilidade. Pode ser nulo para determinadas chamadas do sistema. |
| correlationId |Geralmente um GUID no formato de cadeia de caracteres. Os eventos com correlationId pertencem toohello mesma ação maior e geralmente compartilham um correlationId. |
| eventDescription |Descrição de evento Olá texto estático. |
| eventDataId |Identificador exclusivo do evento hello. |
| eventSource |Nome do hello infraestrutura ou serviço do Azure que o evento Olá gerado. |
| httpRequest |Geralmente inclui "clientRequestId" Olá, "clientIpAddress" e "método" (método HTTP, como PUT). |
| level |Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado". |
| operationId |Normalmente um GUID compartilhado entre eventos Olá correspondente toosingle operação. |
| operationName |Nome da operação de saudação. |
| propriedades |Propriedades de evento de saudação. |
| status |Cadeia de caracteres. Status da operação de saudação. Os valores comuns incluem: "Iniciado", "Em Andamento", "Êxito", "Falha", "Ativo", "Resolvido". |
| subStatus |Geralmente inclui o código de status HTTP saudação da chamada REST correspondente de saudação. Também pode incluir outras cadeias de caracteres que descrevam um substatus. Os valores de substatus comuns incluem: OK (Código de Status HTTP: 200), Criado (Código de Status HTTP: 201), Aceito (Código de Status HTTP: 202), Sem Conteúdo (Código de Status HTTP: 204), Solicitação Incorreta (Código de Status HTTP: 400), Não Encontrado (Código de Status HTTP: 404), Conflito (Código de Status HTTP: 409), Erro Interno do Servidor (Código de Status HTTP: 500), Serviço Indisponível (Código de Status HTTP: 503), Tempo Limite do Gateway (Código de Status HTTP: 504) |

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre Olá Log de atividades](monitoring-overview-activity-logs.md)
* [Exemplos de scripts da Automação do Azure (Runbooks) em alertas do Azure](http://go.microsoft.com/fwlink/?LinkId=627081)
* [Use o aplicativo lógico toosend um SMS por meio do Twilio em um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-text-message-with-logic-app). Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta do Log de atividades.
* [Use o aplicativo lógico toosend uma mensagem de margem de atraso de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-slack-with-logic-app). Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta do Log de atividades.
* [Use o aplicativo lógico toosend tooan uma mensagem fila do Azure de um alerta do Azure](https://github.com/Azure/azure-quickstart-templates/tree/master/201-alert-to-queue-with-logic-app). Este exemplo é para alertas de métrica, mas pode ser modificado toowork com um alerta do Log de atividades.
