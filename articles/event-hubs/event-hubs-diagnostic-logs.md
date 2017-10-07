---
title: "logs de diagnóstico de Hubs de eventos aaaAzure | Microsoft Docs"
description: "Saiba como tooset backup de logs de diagnósticos para os hubs de eventos no Azure."
keywords: 
documentationcenter: 
services: event-hubs
author: banisadr
manager: 
editor: 
ms.assetid: 
ms.service: event-hubs
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: sethm;babanisa
ms.openlocfilehash: d2054e2e444e715e5077fe2608fe1e009e6c1d84
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="event-hubs-diagnostic-logs"></a>Logs de diagnóstico dos Hubs de Eventos

É possível exibir dois tipos de logs para os Hubs de Eventos do Azure:
* **[Logs de atividades](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Esses logs contém informações sobre as operações executadas em um trabalho. Olá logs são sempre habilitados.
* **[Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. É possível configurar logs de diagnóstico para ter uma visão mais detalhada de tudo o que acontece com um trabalho. Atividades de cobertura de logs de diagnóstico de tempo de saudação trabalho Olá é criado até que o trabalho de saudação é excluído, incluindo atualizações e as atividades que ocorrem durante a saudação trabalho está em execução.

## <a name="turn-on-diagnostic-logs"></a>Ativar logs de diagnóstico
Os logs de diagnóstico estão desabilitados por padrão. logs de diagnóstico tooenable:

1.  Em Olá [portal do Azure](https://portal.azure.com), em **monitoramento + gerenciamento**, clique em **logs de diagnóstico**.

    ![Logs de toodiagnostic de navegação de folha](./media/event-hubs-diagnostic-logs/image1.png)

2.  Clique em recurso Olá desejado toomonitor.

3.  Clique em **Ativar diagnóstico**.

    ![Ativar logs de diagnóstico](./media/event-hubs-diagnostic-logs/image2.png)

4.  Para **Status**, clique em **Ativar**.

    ![Alterar o status de saudação de logs de diagnóstico](./media/event-hubs-diagnostic-logs/image3.png)

5.  Destino de arquivo do hello conjunto desejado. Por exemplo, uma conta de armazenamento, um hub de eventos ou análise de logs do Azure.

6.  Salve Olá novas configurações de diagnóstico.

As novas configurações terão efeito em aproximadamente 10 minutos. Depois disso, os logs são exibidos no destino de arquivamento Olá configurado, no hello **logs de diagnóstico** folha.

Para obter mais informações sobre como configurar o diagnóstico, consulte Olá [visão geral dos logs de diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-categories"></a>Categorias dos logs de diagnóstico
Os Hubs de Eventos capturam os logs de diagnóstico de duas categorias:

* **ArchiveLogs**: logs relacionados a arquivos de Hubs tooEvent, especificamente, registra erros de tooarchive relacionados.
* **OperationalLogs**: informações sobre o que está acontecendo durante as operações de Hubs de eventos, especificamente, Olá o tipo de operação, incluindo a criação do hub de eventos, os recursos usados e Olá status da operação de saudação.

## <a name="diagnostic-logs-schema"></a>Esquema de logs de diagnóstico
Todos os logs são armazenados no formato JSON (JavaScript Object Notation). Cada entrada tem campos de cadeia de caracteres que usam o formato de saudação descrito nas seções a seguir de saudação.

### <a name="archive-logs-schema"></a>Esquema dos logs de arquivo morto

Cadeias de caracteres JSON do arquivo log incluem elementos listados na Olá a tabela a seguir:

Nome | Descrição
------- | -------
TaskName | Descrição da tarefa de saudação que falhou.
ActivityId | ID interna, usada para acompanhamento.
trackingId | ID interna, usada para acompanhamento.
resourceId | ID do Recurso do Azure Resource Manager.
eventHub | Nome completo do hub de eventos (inclui o nome do namespace).
partitionId | Partição do Hub de Eventos usada para gravação.
archiveStep | ArchiveFlushWriter
startTime | Hora de início da falha.
failures | Número de vezes que a falha ocorreu.
durationInSeconds | Duração da falha.
Message | Mensagem de erro.
categoria | ArchiveLogs

Olá código a seguir é um exemplo de um cadeia de caracteres JSON do log de arquivo:

```json
{
     "TaskName": "EventHubArchiveUserError",
     "ActivityId": "21b89a0b-8095-471a-9db8-d151d74ecf26",
     "trackingId": "21b89a0b-8095-471a-9db8-d151d74ecf26_B7",
     "resourceId": "/SUBSCRIPTIONS/854D368F-1828-428F-8F3C-F2AFFA9B2F7D/RESOURCEGROUPS/DEFAULT-EVENTHUB-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/FBETTATI-OPERA-EVENTHUB",
     "eventHub": "fbettati-opera-eventhub:eventhub:eh123~32766",
     "partitionId": "1",
     "archiveStep": "ArchiveFlushWriter",
     "startTime": "9/22/2016 5:11:21 AM",
     "failures": 3,
     "durationInSeconds": 360,
     "message": "Microsoft.WindowsAzure.Storage.StorageException: hello remote server returned an error: (404) Not Found. ---> System.Net.WebException: hello remote server returned an error: (404) Not Found.\r\n   at Microsoft.WindowsAzure.Storage.Shared.Protocol.HttpResponseParsers.ProcessExpectedStatusCodeNoException[T](HttpStatusCode expectedStatusCode, HttpStatusCode actualStatusCode, T retVal, StorageCommandBase`1 cmd, Exception ex)\r\n   at Microsoft.WindowsAzure.Storage.Blob.CloudBlockBlob.<PutBlockImpl>b__3e(RESTCommand`1 cmd, HttpWebResponse resp, Exception ex, OperationContext ctx)\r\n   at Microsoft.WindowsAzure.Storage.Core.Executor.Executor.EndGetResponse[T](IAsyncResult getResponseResult)\r\n   --- End of inner exception stack trace ---\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.StorageAsyncResult`1.End()\r\n   at Microsoft.WindowsAzure.Storage.Core.Util.AsyncExtensions.<>c__DisplayClass4.<CreateCallbackVoid>b__3(IAsyncResult ar)\r\n--- End of stack trace from previous location where exception was thrown ---\r\n   at System.",
     "category": "ArchiveLogs"
}
```

### <a name="operational-logs-schema"></a>Esquema de logs operacionais

Cadeias de caracteres do log operacional JSON incluem elementos listados na Olá a tabela a seguir:

Nome | Descrição
------- | -------
ActivityId | ID interna, usadas tootrack finalidade.
EventName | Nome da operação.  
resourceId | ID do Recurso do Azure Resource Manager.
SubscriptionId | ID da assinatura.
EventTimeString | Tempo da operação.
EventProperties | Propriedades da operação.
Status | Status da operação.
Chamador | Chamador da operação (Portal do Azure ou cliente de gerenciamento).
categoria | OperationalLogs

Olá código a seguir é um exemplo de uma cadeia de caracteres do log operacional JSON:

```json
Example:
{
     "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
     "EventName": "Create EventHub",
     "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.EVENTHUB/NAMESPACES/SHOEBOXEHNS-CY4001",
     "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
     "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
     "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
     "Status": "Succeeded",
     "Caller": "ServiceBus Client",
     "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Próximas etapas
* [Introdução tooEvent Hubs](event-hubs-what-is-event-hubs.md)
* [Visão geral de API de Hubs de Eventos](event-hubs-api-overview.md)
* [Introdução aos Hubs de Evento](event-hubs-csharp-ephcs-getstarted.md)
