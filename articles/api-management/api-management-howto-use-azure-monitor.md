---
title: aaaMonitor gerenciamento de API com o Monitor do Azure | Microsoft Docs
description: "Saiba como toomonitor gerenciamento do Azure API de serviço usando o Monitor do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 2fa193cd-ea71-4b33-a5ca-1f55e5351e23
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/23/2017
ms.author: apimpm
ms.openlocfilehash: 5012d8ed57ea4f94ea6bc1b7c4e1102516ec4414
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="monitor-api-management-with-azure-monitor"></a>Monitorar o Gerenciamento de API com o Azure Monitor
O Azure Monitor é um serviço do Azure que fornece uma única fonte para monitorar todos os recursos do Azure. Monitor do Azure, você pode visualizar, consultar, encaminhar, arquivar e executar ações nas métricas de saudação e logs vindos de recursos do Azure, como gerenciamento de API. 

Olá seguindo o vídeo mostra como toomonitor gerenciamento de API usando o Monitor do Azure. Para obter mais informações sobre o Azure Monitor, consulte [Introdução ao Azure Monitor]. 


> [!VIDEO https://channel9.msdn.com/Blogs/AzureApiMgmt/Monitor-API-Management-with-Azure-Monitor/player]
>
>
 
## <a name="metrics"></a>Métricas
Gerenciamento de API atualmente emite cinco métricas e estamos planejando tooadd mais no hello futuras. Essas métricas são emitidas a cada minuto, fornecendo próximo visibilidade em tempo real de estado de saudação e a integridade de suas APIs. A seguir está um resumo das métricas de saudação:
* Total de solicitações de Gateway: o número de saudação da API de solicitações no período de saudação. 
* Solicitações bem sucedidas de Gateway: número de saudação de solicitações de API que recebeu os códigos de resposta HTTP bem-sucedida incluindo 304, 307 e nada menor que 301 (por exemplo, 200). 
* Falha nas solicitações de Gateway: o número de saudação de solicitações de API que recebeu os códigos de resposta HTTP incorretos incluindo 400 e tudo o que é maior que 500.
* Solicitações não autorizadas de Gateway: número de saudação de solicitações de API que recebeu os códigos de resposta HTTP como 401, 403 e 429. 
* Outras solicitações de Gateway: número de saudação de solicitações de API que recebeu os códigos de resposta HTTP que não pertencem tooany de saudação anterior categorias (por exemplo, 418).

É possível acessar as métricas em seu serviço de Gerenciamento de API ou acessar as métricas de todos os seus recursos do Azure no Azure Monitor. métricas de tooview em seu serviço de gerenciamento de API:
1. Olá Abrir portal do Azure.
2. Serviço de gerenciamento de API de tooyour go.
3. Clique em **Métricas**.

![Folha de métricas][metrics-blade]

Para obter mais informações sobre como toouse métricas, consulte [visão geral das métricas].

## <a name="activity-logs"></a>Logs de atividade
Logs de atividade fornecem informações sobre operações de saudação que foram executadas em seus serviços de gerenciamento de API. Anteriormente eles eram conhecidos como "logs de auditoria" ou "logs operacionais". Usando logs de atividade, você pode determinar hello ", que e quando" para qualquer gravação as operações executadas em seus serviços de gerenciamento de API (PUT, POST, DELETE). 

> [!NOTE]
> Logs de atividade não incluem operações de leitura (GET) ou as operações executadas no hello Portal clássico do publicador ou usando Olá APIs de gerenciamento original.

É possível acessar os logs de atividades em seu serviço de Gerenciamento de API ou acessar logs de todos os seus recursos do Azure no Azure Monitor. logs de atividades de tooview em seu serviço de gerenciamento de API:
1. Olá Abrir portal do Azure.
2. Serviço de gerenciamento de API de tooyour go.
3. Clique em **Log de atividades**.

![Folha Logs de atividade][activity-logs-blade]

Para obter mais informações sobre como toouse métricas, consulte [visão geral dos Logs de atividade].

## <a name="alerts"></a>Alertas
Você pode configurar alertas de tooreceive com base nas métricas e registros de atividades. Monitor do Azure permite que você tooconfigure uma saudação de alerta toodo após quando ele dispara:

* Enviar uma notificação por email
* Chamar um webhook
* Invocar um aplicativo lógico do Azure

É possível configurar regras de alerta em seu serviço de Gerenciamento de API ou no Azure Monitor. tooconfigure-los no gerenciamento de API: 
1. Olá Abrir portal do Azure.
2. Serviço de gerenciamento de API de tooyour go.
3. Clique em **Regras de alerta**.

![Folha Regras de alerta][alert-rules-blade]

Para obter mais informações sobre o uso de alertas, consulte [Overview of Alerts (Visão geral dos Alertas)].

## <a name="diagnostic-logs"></a>Logs de Diagnóstico
Os logs de diagnóstico fornecem informações avançadas sobre operações e erros importantes para auditoria, bem como para fins de solução de problemas. Os logs de diagnóstico são diferentes dos logs de atividades. Logs de atividade fornecem informações sobre operações de saudação que foram executadas em recursos do Azure. Os Logs de Diagnóstico fornecem informações em operações que o recurso realizou por conta própria.

Gerenciamento de API no momento fornece diagnósticos de solicitação de logs (lotes por hora) sobre API individual com cada entrada tendo Olá estrutura a seguir:

```
{
    "Tenant": "",
      "DeploymentName": "",
      "time": "",
      "resourceId": "",
      "category": "GatewayLogs",
      "operationName": "Microsoft.ApiManagement/GatewayLogs",
      "durationMs": ,
      "Level": ,
      "properties": "{
          "ApiId": "",
          "OperationId": "",
          "ProductId": "",
          "SubscriptionId": "",
          "Method": "",
          "Url": "",
          "RequestSize": ,
          "ServiceTime": "",
          "BackendMethod": "",
          "BackendUrl": "",
          "BackendResponseCode": ,
          "ResponseCode": ,
          "ResponseSize": ,
          "Cache": "",
          "UserId"
      }"
 }
```

É possível acessar os logs de diagnóstico em seu serviço de Gerenciamento de API ou acessar logs de todos os seus recursos do Azure no Azure Monitor. logs de diagnóstico tooview em seu serviço de gerenciamento de API:
1. Olá Abrir portal do Azure.
2. Serviço de gerenciamento de API de tooyour go.
3. Clique em **Log de diagnóstico**.

![Folha Logs de Diagnóstico][diagnostic-logs-blade]

Para obter mais informações sobre como toouse métricas, consulte [visão geral dos Logs de diagnóstico].

## <a name="next-step"></a>Próxima etapa

* [Introdução ao Azure Monitor]
* [visão geral das métricas]
* [visão geral dos Logs de atividade]
* [visão geral dos Logs de diagnóstico]
* [Overview of Alerts (Visão geral dos Alertas)]

[Introdução ao Azure Monitor]: ../monitoring-and-diagnostics/monitoring-get-started.md
[visão geral das métricas]: ../monitoring-and-diagnostics/monitoring-overview-metrics.md
[visão geral dos Logs de atividade]: ../monitoring-and-diagnostics/monitoring-overview-activity-logs.md
[visão geral dos Logs de diagnóstico]: ../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md
[Overview of Alerts (Visão geral dos Alertas)]: ../monitoring-and-diagnostics/insights-alerts-portal.md



[metrics-blade]: ./media/api-management-azure-monitor/api-management-metrics-blade.png
[activity-logs-blade]: ./media/api-management-azure-monitor/api-management-activity-logs-blade.png
[alert-rules-blade]: ./media/api-management-azure-monitor/api-management-alert-rules-blade.png
[diagnostic-logs-blade]: ./media/api-management-azure-monitor/api-management-diagnostic-logs-blade.png
