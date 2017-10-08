---
title: AAA "evento inicial de redimensionamento do pool de lote do Azure | Microsoft Docs"
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
ms.openlocfilehash: 2ca2a4f1195c3f785ae5b051b63340f70eecbc22
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="pool-resize-start-event"></a>Evento inicial de redimensionamento de pool

 Esse evento é emitido quando um redimensionamento de pool é iniciado. Como o redimensionamento do pool de saudação é um evento assíncrono, você pode esperar um toobe de evento de conclusão de redimensionamento pool emitido depois que a operação de redimensionamento Olá for concluída.

 redimensiona Olá mostra Olá corpo de um evento de início de redimensionamento do pool para um pool de redimensionamento de 0 nós too2 com um manual de exemplo a seguir.

```
{
    "poolId": "myPool1",
    "nodeDeallocationOption": "invalid",
    "currentDedicated": 0,
    "targetDedicated": 2,
    "enableAutoScale": false,
    "isAutoPool": false
}
```

|Elemento|Tipo|Observações|
|-------------|----------|-----------|
|poolId|Cadeia de caracteres|id de saudação do pool de saudação.|
|nodeDeallocationOption|Cadeia de caracteres|Especifica quando nós podem ser removidos do pool hello, se o tamanho do pool de saudação está diminuindo.<br /><br /> Os valores possíveis são:<br /><br /> **colocar novamente na fila** – Finalize as tarefas em execução e coloque-as novamente na fila. tarefas de saudação serão executadas novamente quando o trabalho de saudação está habilitado. Remova nós assim que tarefas forem terminadas.<br /><br /> **terminar** – Termine as tarefas em execução. tarefas de saudação não serão executado novamente. Remova nós assim que tarefas forem terminadas.<br /><br /> **taskcompletion** – permitir em toocomplete de tarefas em execução no momento. Não agende novas tarefas enquanto aguarda. Remova nós quando todas as tarefas forem concluídas.<br /><br /> **Retaineddata** - permitir executando tarefas toocomplete e esperar até que todas as tarefas tooexpire de períodos de retenção de dados. Não agende novas tarefas enquanto aguarda. Remova nós quando todos os períodos de retenção de tarefa expirem.<br /><br /> valor padrão de saudação é enfileiramento.<br /><br /> Se tamanho de pool hello está aumentando, valor hello está definido muito**inválido**.|
|currentDedicated|Int32|número de saudação de nós de computação atualmente atribuído toohello pool.|
|targetDedicated|Int32|número de saudação de nós de computação que são solicitadas para o pool de saudação.|
|enableAutoScale|Bool|Especifica se o tamanho do pool de saudação ajusta automaticamente ao longo do tempo.|
|isAutoPool|Bool|Especifica se o pool de saudação foi criado por meio do mecanismo de pool automático de um trabalho.|
