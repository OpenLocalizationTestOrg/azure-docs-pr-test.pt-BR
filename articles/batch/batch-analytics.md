---
title: "aaaAzure análise de lote | Microsoft Docs"
description: "Referência para análise de lote do Azure."
services: batch
author: tamram
manager: timlt
ms.assetid: 
ms.service: batch
ms.devlang: multiple
ms.topic: article
ms.tgt_pltfrm: vm-windows
ms.workload: big-compute
ms.date: 04/20/2017
ms.author: tamram
ms.openlocfilehash: 462fbad1ac522b485ae18c1e8891b9d2cabd45e0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="batch-analytics"></a>Análise de lote
tópicos de saudação na análise do lote contêm informações de referência para eventos de saudação e alertas disponíveis para os recursos de serviço de lote.

Consulte [Registro em log de diagnóstico de Lote do Azure](https://azure.microsoft.com/documentation/articles/batch-diagnostics/) para obter mais informações sobre como habilitar e consumir logs de diagnóstico de lote.

## <a name="diagnostic-logs"></a>Logs de diagnóstico

Olá serviço de lote do Azure emite Olá eventos de log de diagnóstico a seguir durante a vida útil de saudação de determinados recursos de lote.

**Eventos do Log de Serviço**
* [Criação de pool](batch-pool-create-event.md)
* [Início de exclusão de pool](batch-pool-delete-start-event.md)
* [Conclusão da exclusão de pool](batch-pool-delete-complete-event.md)
* [Início de redimensionamento de pool](batch-pool-resize-start-event.md)
* [Conclusão de redimensionamento de pool](batch-pool-resize-complete-event.md)
* [Início da tarefa](batch-task-start-event.md)
* [Conclusão da tarefa](batch-task-complete-event.md)
* [Falha da tarefa](batch-task-fail-event.md)