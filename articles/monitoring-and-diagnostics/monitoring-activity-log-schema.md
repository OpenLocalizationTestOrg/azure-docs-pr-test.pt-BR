---
title: Esquema de evento do Log de atividade de aaaAzure | Microsoft Docs
description: "Entender o esquema de evento Olá para dados emitidas em Olá Log de atividades"
author: johnkemnetz
manager: robb
services: monitoring-and-diagnostics
documentationcenter: monitoring-and-diagnostics
ms.service: monitoring-and-diagnostics
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/20/2017
ms.author: johnkem
ms.openlocfilehash: dfece949a20a4d9b4e8a4d488c1c34842d87d586
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-activity-log-event-schema"></a>Esquema sobre eventos do Log de Atividades do Azure
Olá **o Log de atividades do Azure** é um log que fornece informações sobre quaisquer eventos de nível de assinatura que ocorreram no Azure. Este artigo descreve o esquema de evento Olá por categoria de dados.

## <a name="administrative"></a>Administrativo
Esta categoria contém registro Olá de todos os criar, operações de atualização, exclusão e a ação executada por meio do Gerenciador de recursos. Exemplos de saudação tipos de eventos que você vê nessa categoria incluem "criar a máquina virtual" e "Excluir grupo de segurança de rede" cada ação tomada por um usuário ou aplicativo usando o Gerenciador de recursos é modelado como uma operação em um tipo de recurso específico. Se o tipo de operação de saudação é gravar, Delete ou ação, registros de saudação do início de saudação e o sucesso ou falha da operação são registradas na categoria administrativa hello. categoria administrativa Olá também inclui qualquer controle de acesso baseado em toorole alterações em uma assinatura.

### <a name="sample-event"></a>Evento de exemplo
```json
{
  "authorization": {
    "action": "microsoft.support/supporttickets/write",
    "role": "Subscription Admin",
    "scope": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841"
  },
  "caller": "admin@contoso.com",
  "channels": "Operation",
  "claims": {
    "aud": "https://management.core.windows.net/",
    "iss": "https://sts.windows.net/72f988bf-86f1-41af-91ab-2d7cd011db47/",
    "iat": "1421876371",
    "nbf": "1421876371",
    "exp": "1421880271",
    "ver": "1.0",
    "http://schemas.microsoft.com/identity/claims/tenantid": "1e8d8218-c5e7-4578-9acc-9abbd5d23315 ",
    "http://schemas.microsoft.com/claims/authnmethodsreferences": "pwd",
    "http://schemas.microsoft.com/identity/claims/objectidentifier": "2468adf0-8211-44e3-95xq-85137af64708",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/upn": "admin@contoso.com",
    "puid": "20030000801A118C",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/nameidentifier": "9vckmEGF7zDKk1YzIY8k0t1_EAPaXoeHyPRn6f413zM",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/givenname": "John",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/surname": "Smith",
    "name": "John Smith",
    "groups": "cacfe77c-e058-4712-83qw-f9b08849fd60,7f71d11d-4c41-4b23-99d2-d32ce7aa621c,31522864-0578-4ea0-9gdc-e66cc564d18c",
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/name": " admin@contoso.com",
    "appid": "c44b4083-3bq0-49c1-b47d-974e53cbdf3c",
    "appidacr": "2",
    "http://schemas.microsoft.com/identity/claims/scope": "user_impersonation",
    "http://schemas.microsoft.com/claims/authnclassreference": "1"
  },
  "correlationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "description": "",
  "eventDataId": "44ade6b4-3813-45e6-ae27-7420a95fa2f8",
  "eventName": {
    "value": "EndRequest",
    "localizedValue": "End request"
  },
  "httpRequest": {
    "clientRequestId": "27003b25-91d3-418f-8eb1-29e537dcb249",
    "clientIpAddress": "192.168.35.115",
    "method": "PUT"
  },
  "id": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841/events/44ade6b4-3813-45e6-ae27-7420a95fa2f8/ticks/635574752669792776",
  "level": "Informational",
  "resourceGroupName": "MSSupportGroup",
  "resourceProviderName": {
    "value": "microsoft.support",
    "localizedValue": "microsoft.support"
  },
  "resourceUri": "/subscriptions/s1/resourceGroups/MSSupportGroup/providers/microsoft.support/supporttickets/115012112305841",
  "operationId": "1e121103-0ba6-4300-ac9d-952bb5d0c80f",
  "operationName": {
    "value": "microsoft.support/supporttickets/write",
    "localizedValue": "microsoft.support/supporttickets/write"
  },
  "properties": {
    "statusCode": "Created"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": "Created",
    "localizedValue": "Created (HTTP Status Code: 201)"
  },
  "eventTimestamp": "2015-01-21T22:14:26.9792776Z",
  "submissionTimestamp": "2015-01-21T22:14:39.9936304Z",
  "subscriptionId": "s1"
}
```

### <a name="property-descriptions"></a>Descrições de propriedade
| Nome do elemento | Descrição |
| --- | --- |
| autorização |Blob de propriedades RBAC do evento hello. Geralmente inclui propriedades de "ação", "função" e "escopo" hello. |
| chamador |Endereço de email do usuário de saudação que executou a operação de hello, declaração UPN ou declaração SPN com base na disponibilidade. |
| canais |Uma saudação valores a seguir: "Admin", "Operação" |
| declarações |token JWT Olá usado pelo Active Directory tooauthenticate Olá usuário ou aplicativo tooperform esta operação no Gerenciador de recursos. |
| correlationId |Normalmente um GUID no formato de cadeia de caracteres de saudação. Os eventos que compartilham um correlationId pertencem toohello mesma ação uber. |
| description |Descrição de texto estático de um evento. |
| eventDataId |Identificador exclusivo de um evento. |
| httpRequest |Blob Olá descrevendo solicitação Http. Geralmente inclui "clientRequestId" Olá, "clientIpAddress" e "método" (método HTTP. Por exemplo, PUT). |
| level |Nível de evento hello. Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado" |
| resourceGroupName |Nome do grupo de recursos de saudação para Olá afetados recursos. |
| resourceProviderName |Nome do provedor de recursos Olá Olá afetado recursos |
| resourceId |Id do recurso da saudação afetados recursos. |
| operationId |Um GUID compartilhado entre eventos Olá correspondentes tooa única operação. |
| operationName |Nome da operação de saudação. |
| propriedades |Conjunto de `<Key, Value>` pares (ou seja, um dicionário) que descreve os detalhes de saudação do evento hello. |
| status |Cadeia de caracteres que descreve o status de saudação da operação de saudação. Alguns valores comuns são: Iniciado, Em Andamento, Êxito, Falha, Ativo, Resolvido. |
| subStatus |Geralmente Olá código de status HTTP da saudação correspondente chamada REST, mas também pode incluir outras cadeias de caracteres que descrevam um substatus, como esses valores comuns: Okey (código de Status HTTP: 200), criado (código de Status HTTP: 201), aceito (código de Status HTTP: 202), nenhum conteúdo (HTTP Código de status: 204), solicitação incorreta (código de Status HTTP: 400), não encontrado (código de Status HTTP: 404), conflito (código de Status HTTP: 409), erro de servidor interno (código de Status HTTP: 500), o Service não está disponível (código de Status HTTP: 503), tempo limite do Gateway (código de Status HTTP: 504). |
| eventTimestamp |Evento Olá correspondente de solicitação de carimbo de hora do evento Olá foi gerado pelo Olá Olá de processamento de serviço do Azure. |
| submissionTimestamp |Carimbo de hora do evento Olá se tornaram disponível para consulta. |
| subscriptionId |ID de Assinatura do Azure. |

## <a name="service-health"></a>Integridade do serviço
Essa categoria contém o registro de saudação de qualquer incidente de integridade do serviço que ocorreram no Azure. Um exemplo de tipo de saudação do evento que você vê nessa categoria é "SQL Azure no Leste dos EUA está passando por tempo de inatividade." Eventos de serviço de integridade são fornecidos em cinco variedades: ação necessária, recuperação assistida, incidente, manutenção, informações ou segurança e só aparecerá se você tiver um recurso na assinatura de saudação que será afetada pelo evento hello.

### <a name="sample-event"></a>Evento de exemplo
```json
{
  "channels": "Admin",
  "correlationId": "c550176b-8f52-4380-bdc5-36c1b59d3a44",
  "description": "Active: Network Infrastructure - UK South",
  "eventDataId": "c5bc4514-6642-2be3-453e-c6a67841b073",
  "eventName": {
      "value": null
  },
  "category": {
      "value": "ServiceHealth",
      "localizedValue": "Service Health"
  },
  "eventTimestamp": "2017-07-20T23:30:14.8022297Z",
  "id": "/subscriptions/mySubscriptionID/events/c5bc4514-6642-2be3-453e-c6a67841b073/ticks/636361902148022297",
  "level": "Warning",
  "operationName": {
      "value": "Microsoft.ServiceHealth/incident/action",
      "localizedValue": "Microsoft.ServiceHealth/incident/action"
  },
  "resourceProviderName": {
      "value": null
  },
  "resourceType": {
      "value": null,
      "localizedValue": ""
  },
  "resourceId": "/subscriptions/mySubscriptionID",
  "status": {
      "value": "Active",
      "localizedValue": "Active"
  },
  "subStatus": {
      "value": null
  },
  "submissionTimestamp": "2017-07-20T23:30:34.7431946Z",
  "subscriptionId": "mySubscriptionID",
  "properties": {
    "title": "Network Infrastructure - UK South",
    "service": "Service Fabric",
    "region": "UK South",
    "communication": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "incidentType": "Incident",
    "trackingId": "NA0F-BJG",
    "impactStartTime": "2017-07-20T21:41:00.0000000Z",
    "impactedServices": "[{\"ImpactedRegions\":[{\"RegionName\":\"UK South\"}],\"ServiceName\":\"Service Fabric\"}]",
    "defaultLanguageTitle": "Network Infrastructure - UK South",
    "defaultLanguageContent": "Starting at approximately 21:41 UTC on 20 Jul 2017, a subset of customers in UK South may experience degraded performance, connectivity drops or timeouts when accessing their Azure resources hosted in this region. Engineers are investigating underlying Network Infrastructure issues in this region. Impacted services may include, but are not limited tooApp Services, Automation, Service Bus, Log Analytics, Key Vault, SQL Database, Service Fabric, Event Hubs, Stream Analytics, Azure Data Movement, API Management, and Azure Search. Multiple engineering teams are engaged in multiple workflows toomitigate hello impact. hello next update will be provided in 60 minutes, or as events warrant.",
    "stage": "Active",
    "communicationId": "636361902146035247",
    "version": "0.1.1"
  }
}
```

### <a name="property-descriptions"></a>Descrições de propriedade
Nome do elemento | Descrição
-------- | -----------
canais | É uma saudação valores a seguir: "Admin", "Operação"
correlationId | É geralmente um GUID no formato de cadeia de caracteres de saudação. Eventos que pertencem a mesma ação uber geralmente compartilham de toohello Olá mesma correlationId.
description | Descrição do evento hello.
eventDataId | Olá identificador exclusivo de um evento.
eventName | título de saudação do evento hello.
level | Nível de evento hello. Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado"
resourceProviderName | Nome do provedor de recursos Olá Olá afetados recursos. Se não for conhecido, será nulo.
resourceType| tipo de saudação do recurso de saudação afetados recursos. Se não for conhecido, será nulo.
subStatus | Geralmente é null para eventos de Integridade do Serviço.
eventTimestamp | Carimbo de hora do evento de log Olá foi gerado e enviado toohello Log de atividades.
submissionTimestamp |   Carimbo de hora do evento Olá foi disponibilizado em Olá Log de atividades.
subscriptionId | Olá assinatura do Azure na qual este evento foi registrado.
status | Cadeia de caracteres que descreve o status de saudação da operação de saudação. Alguns valores comuns são: Ativo, Resolvido.
operationName | Nome da operação de saudação. Normalmente Microsoft.ServiceHealth/incident/action.
categoria | “ServiceHealth”
resourceId | Id do recurso da saudação afetada recurso, se conhecido. Caso contrário, a ID da assinatura é fornecida.
Properties.title | Olá localizado título para essa comunicação. Inglês é o idioma padrão de saudação.
Properties.communication | Olá localizado detalhes de comunicação de saudação com marcação HTML. Inglês é o padrão de saudação.
Properties.incidentType | Possíveis valores: AssistedRecovery, ActionRequired, Information, Incident, Maintenance, Security
Properties.trackingId | Identifica o incidente Olá que esse evento está associado. Use este incidente de tooan relacionados toocorrelate Olá eventos.
Properties.impactedServices | Um blob com caracteres de escape do JSON que descreve os serviços de saudação e regiões que são afetados pelo incidente de saudação. Uma lista de Services, que, individualmente, tem um ServiceName e uma lista de ImpactedRegions, que têm um RegionName.
Properties.defaultLanguageTitle | comunicação de saudação em inglês
Properties.defaultLanguageContent | comunicação de saudação em inglês como marcação html ou como texto sem formatação
Properties.stage | Os possíveis valores para AssistedRecovery, ActionRequired, Information, Incident e Security são Active e Resolved. Para Maintenance, eles são: Active, Planned, InProgress, Canceled, Rescheduled, Resolved, Complete
Properties.communicationId | comunicação Olá esse evento está associado.

## <a name="alert"></a>Alerta
Essa categoria contém o registro de saudação de todas as ativações de alertas do Azure. Um exemplo desse tipo de saudação do evento que você vê nessa categoria é "% da CPU em myVM 80 para hello nos últimos 5 minutos." Uma variedade de sistemas do Azure têm um conceito de alerta – você pode definir uma regra de algum tipo e receber uma notificação quando as condições corresponderem a essa regra. Cada vez que um tipo de alerta com suporte do Azure 'ativa,' ou condições hello são atendido toogenerate uma notificação, um registro de ativação de saudação também é enviada por push toothis categoria de saudação Log de atividades.

### <a name="sample-event"></a>Evento de exemplo

```json
{
  "caller": "Microsoft.Insights/alertRules",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/alertRules"
  },
  "correlationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "description": "'Disk read LessThan 100000 ([Count]) in hello last 5 minutes' has been resolved for CloudService: myResourceGroup/Production/Event.BackgroundJobsWorker.razzle (myResourceGroup)",
  "eventDataId": "149d4baf-53dc-4cf4-9e29-17de37405cd9",
  "eventName": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "category": {
    "value": "Alert",
    "localizedValue": "Alert"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle/events/149d4baf-53dc-4cf4-9e29-17de37405cd9/ticks/636362258535221920",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "Microsoft.ClassicCompute",
    "localizedValue": "Microsoft.ClassicCompute"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/Event.BackgroundJobsWorker.razzle",
  "resourceType": {
    "value": "Microsoft.ClassicCompute/domainNames/slots/roles",
    "localizedValue": "Microsoft.ClassicCompute/domainNames/slots/roles"
  },
  "operationId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert/incidents/L3N1YnNjcmlwdGlvbnMvZGY2MDJjOWMtN2FhMC00MDdkLWE2ZmItZWIyMGM4YmQxMTkyL3Jlc291cmNlR3JvdXBzL0NzbUV2ZW50RE9HRk9PRC1XZXN0VVMvcHJvdmlkZXJzL21pY3Jvc29mdC5pbnNpZ2h0cy9hbGVydHJ1bGVzL215YWxlcnQwNjM2MzYyMjU4NTM1MjIxOTIw",
  "operationName": {
    "value": "Microsoft.Insights/AlertRules/Resolved/Action",
    "localizedValue": "Microsoft.Insights/AlertRules/Resolved/Action"
  },
  "properties": {
    "RuleUri": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/alertrules/myalert",
    "RuleName": "myalert",
    "RuleDescription": "",
    "Threshold": "100000",
    "WindowSizeInMinutes": "5",
    "Aggregation": "Average",
    "Operator": "LessThan",
    "MetricName": "Disk read",
    "MetricUnit": "Count"
  },
  "status": {
    "value": "Resolved",
    "localizedValue": "Resolved"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T09:24:13.522192Z",
  "submissionTimestamp": "2017-07-21T09:24:15.6578651Z",
  "subscriptionId": "mySubscriptionID"
}
```

### <a name="property-descriptions"></a>Descrições de propriedade
| Nome do elemento | Descrição |
| --- | --- |
| chamador | Always Microsoft.Insights/alertRules |
| canais | Sempre "Administrador, Operação" |
| declarações | Blob JSON com as tipo hello SPN (nome principal do serviço) ou de recurso, do mecanismo de alerta de saudação. |
| correlationId | Um GUID no formato de cadeia de caracteres de saudação. |
| description |Descrição de alerta de evento Olá texto estático. |
| eventDataId |Identificador exclusivo do evento de alerta de saudação. |
| level |Nível de evento hello. Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado" |
| resourceGroupName |Nome do grupo de recursos de saudação para Olá afetados recurso se ele é um alerta de métrica. Para outros tipos de alerta, esse é o nome de Olá Olá do grupo de recursos que contém o alerta de saudação em si. |
| resourceProviderName |Nome do provedor de recursos Olá Olá afetados recurso se ele é um alerta de métrica. Para outros tipos de alerta, este é o nome de saudação do provedor de recursos de saudação para alerta Olá em si. |
| resourceId | Nome da ID de recurso Olá para Olá afetados recurso se ele é um alerta de métrica. Para outros tipos de alerta, isso é o ID de recurso de saudação do recurso de alerta de saudação em si. |
| operationId |Um GUID compartilhado entre eventos Olá correspondentes tooa única operação. |
| operationName |Nome da operação de saudação. |
| propriedades |Conjunto de `<Key, Value>` pares (ou seja, um dicionário) que descreve os detalhes de saudação do evento hello. |
| status |Cadeia de caracteres que descreve o status de saudação da operação de saudação. Alguns valores comuns são: Iniciado, Em Andamento, Êxito, Falha, Ativo, Resolvido. |
| subStatus | Geralmente é null para alertas. |
| eventTimestamp |Evento Olá correspondente de solicitação de carimbo de hora do evento Olá foi gerado pelo Olá Olá de processamento de serviço do Azure. |
| submissionTimestamp |Carimbo de hora do evento Olá se tornaram disponível para consulta. |
| subscriptionId |ID de Assinatura do Azure. |

### <a name="properties-field-per-alert-type"></a>Campo de propriedades por tipo de alerta
campo de propriedades Olá conterá valores diferentes dependendo da fonte de saudação do alerta de evento hello. Dois provedores de alerta de evento comuns são alertas do Log de Atividades e de métrica.

#### <a name="properties-for-activity-log-alerts"></a>Propriedades de alertas do Log de Atividades
| Nome do elemento | Descrição |
| --- | --- |
| properties.subscriptionId | ID de assinatura de saudação do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado. |
| properties.eventDataId | Olá evento ID de dados de evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado. |
| properties.resourceGroup | grupo de recursos de saudação do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado. |
| properties.resourceId | ID do recurso de saudação do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado. |
| properties.eventTimestamp | Olá carimbo de hora de eventos do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado. |
| properties.operationName | nome da operação de saudação do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado. |
| properties.status | status de saudação do evento de log de atividade de saudação que causou este toobe de regra de alerta do log de atividade ativado.|

#### <a name="properties-for-metric-alerts"></a>Propriedades de alertas de métrica
| Nome do elemento | Descrição |
| --- | --- |
| properties.RuleUri | ID do recurso de saudação métrica regra de alerta em si. |
| properties.RuleName | nome de saudação da regra de alerta métrica hello. |
| properties.RuleDescription | Descrição de saudação da regra de alerta métrica hello (conforme definido na regra de alerta de saudação). |
| properties.Threshold | valor de limite de saudação usado na avaliação de saudação da regra de alerta métrica hello. |
| properties.WindowSizeInMinutes | tamanho da janela Olá usado na avaliação de saudação da regra de alerta métrica hello. |
| properties.Aggregation | tipo de agregação Olá definido na regra de alerta métrica hello. |
| properties.Operator | operador condicional Olá usada na avaliação de saudação da regra de alerta métrica hello. |
| properties.MetricName | nome da métrica Olá da métrica de saudação usada na avaliação de saudação da regra de alerta métrica hello. |
| properties.MetricUnit | unidade de métrica Olá para métrica de saudação usada na avaliação de saudação da regra de alerta métrica Olá. |

## <a name="autoscale"></a>Autoscale
Esta categoria contém registro Olá de qualquer operação de toohello relacionados de eventos do mecanismo de dimensionamento automático de saudação com base em quaisquer configurações de dimensionamento automático que você definiu na sua assinatura. Um exemplo desse tipo de saudação do evento que você vê nessa categoria é "Escala de dimensionamento automático das ações de falha". Usar o dimensionamento automático, você pode automaticamente expansão ou escala em Olá o número de instâncias em um tipo de recurso com suporte com base na hora do dia e/ou carregar dados (métricas) usando uma configuração de AutoEscala. Quando Olá condições tooscale para cima ou para baixo, Olá início e foi bem-sucedida ou eventos com falha serão registrados nessa categoria.

### <a name="sample-event"></a>Evento de exemplo
```json
{
  "caller": "Microsoft.Insights/autoscaleSettings",
  "channels": "Admin, Operation",
  "claims": {
    "http://schemas.xmlsoap.org/ws/2005/05/identity/claims/spn": "Microsoft.Insights/autoscaleSettings"
  },
  "correlationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
  "eventDataId": "a5b92075-1de9-42f1-b52e-6f3e4945a7c7",
  "eventName": {
    "value": "AutoscaleAction",
    "localizedValue": "AutoscaleAction"
  },
  "category": {
    "value": "Autoscale",
    "localizedValue": "Autoscale"
  },
  "id": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup/events/a5b92075-1de9-42f1-b52e-6f3e4945a7c7/ticks/636361956518681572",
  "level": "Informational",
  "resourceGroupName": "myResourceGroup",
  "resourceProviderName": {
    "value": "microsoft.insights",
    "localizedValue": "microsoft.insights"
  },
  "resourceId": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/microsoft.insights/autoscalesettings/myResourceGroup-Production-myResource-myResourceGroup",
  "resourceType": {
    "value": "microsoft.insights/autoscalesettings",
    "localizedValue": "microsoft.insights/autoscalesettings"
  },
  "operationId": "fc6a7ff5-ff68-4bb7-81b4-3629212d03d0",
  "operationName": {
    "value": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action",
    "localizedValue": "Microsoft.Insights/AutoscaleSettings/Scaledown/Action"
  },
  "properties": {
    "Description": "hello autoscale engine attempting tooscale resource '/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource' from 3 instances count too2 instances count.",
    "ResourceName": "/subscriptions/mySubscriptionID/resourceGroups/myResourceGroup/providers/Microsoft.ClassicCompute/domainNames/myResourceGroup/slots/Production/roles/myResource",
    "OldInstancesCount": "3",
    "NewInstancesCount": "2",
    "LastScaleActionTime": "Fri, 21 Jul 2017 01:00:51 GMT"
  },
  "status": {
    "value": "Succeeded",
    "localizedValue": "Succeeded"
  },
  "subStatus": {
    "value": null
  },
  "eventTimestamp": "2017-07-21T01:00:51.8681572Z",
  "submissionTimestamp": "2017-07-21T01:00:52.3008754Z",
  "subscriptionId": "mySubscriptionID"
}

```

### <a name="property-descriptions"></a>Descrições de propriedade
| Nome do elemento | Descrição |
| --- | --- |
| chamador | Always Microsoft.Insights/autoscaleSettings |
| canais | Sempre "Administrador, Operação" |
| declarações | Blob JSON com tipo de recurso ou o SPN (nome principal do serviço), do mecanismo de dimensionamento automático de saudação do hello. |
| correlationId | Um GUID no formato de cadeia de caracteres de saudação. |
| description |Descrição de texto estático do evento de dimensionamento automático de saudação. |
| eventDataId |Identificador exclusivo do evento de dimensionamento automático hello. |
| level |Nível de evento hello. Uma saudação valores a seguir: "Crítico", "Error", "Aviso", "Informativo" e "Detalhado" |
| resourceGroupName |Nome do grupo de recursos de saudação para configuração de dimensionamento automático de saudação. |
| resourceProviderName |Nome do provedor de recursos de saudação para configuração de dimensionamento automático hello. |
| resourceId |Id do recurso de configuração de dimensionamento automático hello. |
| operationId |Um GUID compartilhado entre eventos Olá correspondentes tooa única operação. |
| operationName |Nome da operação de saudação. |
| propriedades |Conjunto de `<Key, Value>` pares (ou seja, um dicionário) que descreve os detalhes de saudação do evento hello. |
| properties.Description | Descrição detalhada do qual o mecanismo de dimensionamento automático Olá estava fazendo. |
| properties.ResourceName | ID do recurso da saudação afetado recursos (Olá recursos no qual Olá ação de escala estava sendo executada) |
| properties.OldInstancesCount | número de saudação de instâncias antes da ação de dimensionamento automático hello está em vigor. |
| properties.NewInstancesCount | número de saudação de instâncias após a ação de dimensionamento automático hello está em vigor. |
| properties.LastScaleActionTime | Olá carimbo de hora de quando a ação de dimensionamento automático Olá ocorreu. |
| status |Cadeia de caracteres que descreve o status de saudação da operação de saudação. Alguns valores comuns são: Iniciado, Em Andamento, Êxito, Falha, Ativo, Resolvido. |
| subStatus | Geralmente é null para dimensionamento automático. |
| eventTimestamp |Evento Olá correspondente de solicitação de carimbo de hora do evento Olá foi gerado pelo Olá Olá de processamento de serviço do Azure. |
| submissionTimestamp |Carimbo de hora do evento Olá se tornaram disponível para consulta. |
| subscriptionId |ID de Assinatura do Azure. |

## <a name="next-steps"></a>Próximas etapas
* [Saiba mais sobre hello (anteriormente conhecida como Logs de auditoria) do Log de atividades](monitoring-overview-activity-logs.md)
* [Fluxo de tooEvent de Log de atividades do Azure Olá Hubs](monitoring-stream-activity-logs-event-hubs.md)
