---
title: "logs de diagnóstico de barramento de serviço aaaAzure | Microsoft Docs"
description: "Saiba como tooset backup de logs de diagnósticos para o barramento de serviço no Azure."
keywords: 
documentationcenter: .net
services: service-bus-messaging
author: banisadr
manager: timlt
editor: 
ms.assetid: 
ms.service: service-bus-messaging
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: data-services
ms.date: 06/27/2017
ms.author: babanisa;sethm
ms.openlocfilehash: e48d6eaba6e865ae39f5b07ed6cd53d74c92e2ff
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="service-bus-diagnostic-logs"></a>Logs de diagnóstico do Barramento de Serviço

É possível exibir dois tipos de logs para o Barramento de Serviço do Azure:
* **[Logs de atividades](../monitoring-and-diagnostics/monitoring-overview-activity-logs.md)**. Esses logs contém informações sobre as operações executadas em um trabalho. Olá logs são sempre habilitados.
* **[Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md)**. É possível configurar logs de diagnóstico para obter informações mais detalhadas sobre tudo o que acontece em um trabalho. Atividades de cobertura de logs de diagnóstico de tempo de saudação trabalho Olá é criado até que o trabalho de saudação é excluído, incluindo atualizações e as atividades que ocorrem durante a saudação trabalho está em execução.

## <a name="turn-on-diagnostic-logs"></a>Ativar logs de diagnóstico

Os logs de diagnóstico estão desabilitados por padrão. logs de diagnóstico tooenable, execute Olá etapas a seguir:

1.  Em Olá [portal do Azure](https://portal.azure.com), em **monitoramento + gerenciamento**, clique em **logs de diagnóstico**.

    ![Logs de toodiagnostic de navegação de folha](./media/service-bus-diagnostic-logs/image1.png)

2. Clique em recurso Olá desejado toomonitor.  

3.  Clique em **Ativar diagnóstico**.

    ![ativar logs de diagnóstico](./media/service-bus-diagnostic-logs/image2.png)

4.  Para **Status**, clique em **Ativar**.

    ![alterar logs de diagnóstico de status](./media/service-bus-diagnostic-logs/image3.png)

5.  Destino de arquivo do hello conjunto desejado. Por exemplo, uma conta de armazenamento, um Hub de eventos ou análise de logs do Azure.

6.  Salve Olá novas configurações de diagnóstico.

As novas configurações terão efeito em aproximadamente 10 minutos. Depois disso, os logs são exibidos no destino de arquivamento Olá configurado, no hello **logs de diagnóstico** folha.

Para obter mais informações sobre como configurar o diagnóstico, consulte Olá [visão geral dos logs de diagnóstico do Azure](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md).

## <a name="diagnostic-logs-schema"></a>Esquema de logs de diagnóstico

Todos os logs são armazenados no formato JSON (JavaScript Object Notation). Cada entrada tem campos de cadeia de caracteres que usam o formato de saudação descrito na Olá seção a seguir.

## <a name="operational-logs-schema"></a>Esquema de logs operacionais

Registra no hello **OperationalLogs** categoria captura o que acontece durante as operações de barramento de serviço. Especificamente, esses logs capturar o tipo de operação hello, incluindo a criação da fila, os recursos usados e Olá status da operação de saudação.

Cadeias de caracteres do log operacional JSON incluem elementos listados na Olá a tabela a seguir:

Nome | Descrição
------- | -------
ActivityId | ID interna, usada para acompanhamento
EventName | Nome da operação           
resourceId | ID de recurso do Azure Resource Manager
SubscriptionId | ID da assinatura
EventTimeString | Tempo de operação
EventProperties | Propriedades da operação
Status | Status da operação
Chamador | Chamador da operação (portal do Azure ou cliente de gerenciamento)
categoria | OperationalLogs

Este é um exemplo de uma cadeia de caracteres JSON do log operacional:

```json
{
  "ActivityId": "6aa994ac-b56e-4292-8448-0767a5657cc7",
  "EventName": "Create Queue",
  "resourceId": "/SUBSCRIPTIONS/1A2109E3-9DA0-455B-B937-E35E36C1163C/RESOURCEGROUPS/DEFAULT-SERVICEBUS-CENTRALUS/PROVIDERS/MICROSOFT.SERVICEBUS/NAMESPACES/SHOEBOXEHNS-CY4001",
  "SubscriptionId": "1a2109e3-9da0-455b-b937-e35e36c1163c",
  "EventTimeString": "9/28/2016 8:40:06 PM +00:00",
  "EventProperties": "{\"SubscriptionId\":\"1a2109e3-9da0-455b-b937-e35e36c1163c\",\"Namespace\":\"shoeboxehns-cy4001\",\"Via\":\"https://shoeboxehns-cy4001.servicebus.windows.net/f8096791adb448579ee83d30e006a13e/?api-version=2016-07\",\"TrackingId\":\"5ee74c9e-72b5-4e98-97c4-08a62e56e221_G1\"}",
  "Status": "Succeeded",
  "Caller": "ServiceBus Client",
  "category": "OperationalLogs"
}
```

## <a name="next-steps"></a>Próximas etapas

Visite Olá links toolearn mais sobre o barramento de serviço a seguir:

* [Introdução tooService barramento](service-bus-messaging-overview.md)
* [Introdução ao Barramento de Serviço](service-bus-dotnet-get-started-with-queues.md)
