---
title: "AAA \"evento de conclusão de redimensionamento do pool de lote do Azure | Microsoft Docs\""
description: "Referência de redimensionamento do pool de lote evento inicial."
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
ms.openlocfilehash: dc64711a01aa4cf6192edba1a2c4cad56f953766
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-complete-event"></a>Evento de conclusão de redimensionamento de pool

 Esse evento é emitido na conclusão ou falha de um redimensionamento de pool.

 Olá, exemplo a seguir mostra Olá corpo de um evento completa de redimensionamento do pool para um pool de aumento de tamanho e foi concluída com êxito.

```
{
    "id": "p_1_0_01503750-252d-4e57-bd96-d6aa05601ad8",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 4,
    "targetDedicated": 4,
    "enableAutoScale": false,
    "isAutoPool": false,
    "startTime": "2016-09-09T22:13:06.573Z",
    "endTime": "2016-09-09T22:14:01.727Z",
    "result": "Success",
    "resizeError": "hello operation succeeded"
}
```

|Elemento|Tipo|Observações|
|-------------|----------|-----------|
|ID|Cadeia de caracteres|id de saudação do pool de saudação.|
|nodeDeallocationOption|Cadeia de caracteres|Especifica quando nós podem ser removidos do pool hello, se o tamanho do pool de saudação está diminuindo.<br /><br /> Os valores possíveis são:<br /><br /> **colocar novamente na fila** – Finalize as tarefas em execução e coloque-as novamente na fila. tarefas de saudação serão executadas novamente quando o trabalho de saudação está habilitado. Remova nós assim que tarefas forem terminadas.<br /><br /> **terminar** – Termine as tarefas em execução. tarefas de saudação não serão executado novamente. Remova nós assim que tarefas forem terminadas.<br /><br /> **taskcompletion** – permitir em toocomplete de tarefas em execução no momento. Não agende novas tarefas enquanto aguarda. Remova nós quando todas as tarefas forem concluídas.<br /><br /> **Retaineddata** - permitir executando tarefas toocomplete e esperar até que todas as tarefas tooexpire de períodos de retenção de dados. Não agende novas tarefas enquanto aguarda. Remova nós quando todos os períodos de retenção de tarefa expirem.<br /><br /> valor padrão de saudação é enfileiramento.<br /><br /> Se tamanho de pool hello está aumentando, valor hello está definido muito**inválido**.|
|currentDedicated|Int32|número de saudação de nós de computação atualmente atribuído toohello pool.|
|targetDedicated|Int32|número de saudação de nós de computação que são solicitadas para o pool de saudação.|
|enableAutoScale|Bool|Especifica se o tamanho do pool de saudação ajusta automaticamente ao longo do tempo.|
|isAutoPool|Bool|Especifica se o pool de saudação foi criado por meio do mecanismo de pool automático de um trabalho.|
|startTime|Datetime|tempo de saudação redimensionamento do pool de saudação iniciado.|
|endTime|Datetime|Olá tempo redimensionamento do pool de saudação concluída.|
|resultCode|Cadeia de caracteres|resultado de saudação da saudação redimensionar.|
|resultMessage|Cadeia de caracteres|Erro de redimensionamento Olá inclui detalhes de saudação do resultado hello.<br /><br /> Se Olá redimensionar concluída com êxito-estados de hello a operação foi bem-sucedida.|
