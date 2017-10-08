---
title: "aaaEnable log de diagnóstico para eventos de lote - Azure | Microsoft Docs"
description: "Registre e analisar eventos de log de diagnóstico para recursos de conta do Lote do Azure, como pools e tarefas."
services: batch
documentationcenter: 
author: tamram
manager: timlt
editor: 
ms.assetid: e14e611d-12cd-4671-91dc-bc506dc853e5
ms.service: batch
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: multiple
ms.workload: big-compute
ms.date: 05/22/2017
ms.author: tamram
ms.custom: H1Hack27Feb2017
ms.openlocfilehash: 9d03303a3e857e9303f40cc6de5c32b5a51d8f8a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="log-events-for-diagnostic-evaluation-and-monitoring-of-batch-solutions"></a>Eventos de log para avaliação de diagnóstico e monitoramento de soluções do Lote

Assim como acontece com muitos serviços do Azure, Olá serviço de lote emite eventos de log para certos recursos durante Olá tempo de vida do recurso de saudação. Você pode habilitar eventos de toorecord de logs de diagnóstico do Azure Batch para recursos, como tarefas e pools e, em seguida, usar os logs de saudação para avaliação de diagnóstica e monitoramento. Eventos como criação de pool, exclusão de pool, início da tarefa, conclusão de tarefa e outros são incluídos nos logs de diagnóstico do Lote.

> [!NOTE]
> Este artigo descreve os eventos de registro em log para os próprios recursos de conta do Lote, e não para os dados de saída de trabalhos e tarefas. Para obter detalhes sobre como armazenar dados de saída de saudação de seus trabalhos e tarefas, consulte [saída de trabalhos e tarefas de lote do Azure persistem](batch-task-output.md).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
* [Conta do Lote do Azure](batch-account-create-portal.md)
* [Conta do Armazenamento do Azure](../storage/common/storage-create-storage-account.md#create-a-storage-account)
  
  logs de diagnóstico toopersist em lotes, você deve criar uma conta de armazenamento do Azure em que o Azure armazenará Olá logs. Especifique a conta de Armazenamento quando você [Habilitar o registro em log de diagnóstico](#enable-diagnostic-logging) para sua conta do Lote. Olá conta de armazenamento especificada quando você habilita a coleta de log não é Olá mesmo como uma saudação do armazenamento vinculado conta referida tooin [pacotes de aplicativos](batch-application-packages.md) e [persistência de saída da tarefa](batch-task-output.md) artigos.
  
  > [!WARNING]
  > Você está **cobrado** para dados de saudação armazenados em sua conta de armazenamento do Azure. Isso inclui logs de diagnóstico Olá discutido neste artigo. Lembre-se disso ao projetar sua [política de retenção de log](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md).
  > 
  > 

## <a name="enable-diagnostic-logging"></a>Habilitar registro em log de diagnóstico
O registro em log de diagnóstico não está habilitado por padrão para sua conta do Lote. Você deve habilitar explicitamente o log de diagnóstico para cada conta de lote que você deseja toomonitor:

[Como tooenable coleta de Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md#how-to-enable-collection-of-resource-diagnostic-logs)

É recomendável que você leia Olá completo [visão geral do Azure Logs de diagnóstico](../monitoring-and-diagnostics/monitoring-overview-of-diagnostic-logs.md) artigo toogain entender não apenas como tooenable log, mas Olá log categorias suportados pelo Olá vários serviços do Azure. Por exemplo, atualmente o Lote do Azure oferece suporte a uma categoria de log: **Logs de Serviço**.

## <a name="service-logs"></a>Logs de serviço
Logs de serviço de lote do Azure contêm os eventos emitidos pelo serviço de lote do Azure Olá durante o tempo de vida de saudação de um recurso de lote como uma tarefa ou um pool. Cada evento emitido pelo lote é armazenado no hello especificado conta de armazenamento no formato JSON. Por exemplo, este é o corpo de saudação de uma amostra de **criação do pool de evento**:

```json
{
    "poolId": "myPool1",
    "displayName": "Production Pool",
    "vmSize": "Small",
    "cloudServiceConfiguration": {
        "osFamily": "4",
        "targetOsVersion": "*"
    },
    "networkConfiguration": {
        "subnetId": " "
    },
    "resizeTimeout": "300000",
    "targetDedicatedComputeNodes": 2,
    "maxTasksPerNode": 1,
    "vmFillType": "Spread",
    "enableAutoscale": false,
    "enableInterNodeCommunication": false,
    "isAutoPool": false
}
```

Cada corpo de evento reside em um. JSON arquivo hello especificou a conta de armazenamento do Azure. Se você quiser tooaccess Olá logs diretamente, poderá Olá tooreview [esquema dos Logs de diagnóstico na conta de armazenamento Olá](../monitoring-and-diagnostics/monitoring-archive-diagnostic-logs.md#schema-of-diagnostic-logs-in-the-storage-account).

## <a name="service-log-events"></a>Eventos do Log de Serviço
Olá serviço em lotes atualmente emite Olá eventos de Log do serviço a seguir. Essa lista pode não ser completa, pois outros eventos podem ter sido adicionados desde a última atualização deste artigo.

| **Eventos do Log de Serviço** |
| --- |
| [Criação de pool][pool_create] |
| [Início de exclusão de pool][pool_delete_start] |
| [Conclusão de exclusão de pool][pool_delete_complete] |
| [Início de redimensionamento de pool][pool_resize_start] |
| [Conclusão de redimensionamento de pool][pool_resize_complete] |
| [Início de tarefa][task_start] |
| [Conclusão de tarefa][task_complete] |
| [Falha de tarefa][task_fail] |

## <a name="next-steps"></a>Próximas etapas
Eventos de log de diagnóstico de toostoring de adição em uma conta de armazenamento do Azure, você também pode transmitir tooan de eventos de Log do serviço de lote [Hub de eventos do Azure](../event-hubs/event-hubs-what-is-event-hubs.md)e enviá-los muito[Azure Log Analytics](../log-analytics/log-analytics-overview.md).

* [Fluxo de Logs de diagnóstico do Azure tooEvent Hubs](../monitoring-and-diagnostics/monitoring-stream-diagnostic-logs-to-event-hubs.md)
  
  Serviço de entrada de dados altamente escalonável do lote eventos de diagnóstico toohello, Hubs de eventos de fluxo. Os Hubs de Eventos podem incluir milhões de eventos por segundo, os quais você pode transformar e armazenar usando qualquer provedor de análise em tempo real.
* [Analisar logs de diagnóstico do Azure usando o Log Analytics](../log-analytics/log-analytics-azure-storage.md)
  
  Envie seu tooLog logs de diagnóstico análise onde analisá-los no portal do Operations Management Suite (OMS) hello ou exportá-los para análise no Power BI ou Excel.

[pool_create]: https://msdn.microsoft.com/library/azure/mt743615.aspx
[pool_delete_start]: https://msdn.microsoft.com/library/azure/mt743610.aspx
[pool_delete_complete]: https://msdn.microsoft.com/library/azure/mt743618.aspx
[pool_resize_start]: https://msdn.microsoft.com/library/azure/mt743609.aspx
[pool_resize_complete]: https://msdn.microsoft.com/library/azure/mt743608.aspx
[task_start]: https://msdn.microsoft.com/library/azure/mt743616.aspx
[task_complete]: https://msdn.microsoft.com/library/azure/mt743612.aspx
[task_fail]: https://msdn.microsoft.com/library/azure/mt743607.aspx
