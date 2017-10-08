---
title: "AAA \"evento de início da tarefa de lote do Azure | Microsoft Docs\""
description: "Referência de evento de início de tarefa de lote."
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
ms.openlocfilehash: 2cb066be1578741125e9081a84a2b7c74dc8356a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="task-start-event"></a>Evento de início da tarefa

 Esse evento é emitido quando uma tarefa tiver sido agendada toostart em um nó de computação pelo Agendador hello. Observe que se a tarefa Olá é repetida ou retirada da fila esse evento será emitido novamente para hello mesma tarefa, mas Olá contagem de repetição e a versão da tarefa de sistema será atualizado adequadamente.


 Olá, exemplo a seguir mostra o corpo de saudação de um evento de início da tarefa.

```
{
    "jobId": "job-0000000001",
    "id": "task-5",
    "taskType": "User",
    "systemTaskVersion": 0,
    "nodeInfo": {
        "poolId": "pool-001",
        "nodeId": "tvm-257509324_1-20160908t162728z"
    },
    "multiInstanceSettings": {
        "numberOfInstances": 1
    },
    "constraints": {
        "maxTaskRetryCount": 2
    },
    "executionInfo": {
        "retryCount": 0
    }
}
```

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|jobId|Cadeia de caracteres|id de saudação do trabalho de saudação que contém a tarefa de saudação.|
|ID|Cadeia de caracteres|id de saudação da tarefa de saudação.|
|taskType|Cadeia de caracteres|tipo de saudação da tarefa de saudação. Pode ser “JobManager” indicando que é uma tarefa do gerenciador de trabalhos ou “Usuário”, indicando que não é uma tarefa do gerenciador de trabalhos.|
|systemTaskVersion|Int32|Este é o contador de repetições interno de saudação em uma tarefa. Internamente, serviço de lote de saudação pode repetir tooaccount uma tarefa para problemas transitórios. Esses problemas podem incluir interno toorecover agendamento erros ou tentativas de nós de computação em um estado inválido.|
|[nodeInfo](#nodeInfo)|Tipo complexo|Contém informações sobre o nó de computação Olá no qual Olá tarefa foi executada.|
|[multiInstanceSettings](#multiInstanceSettings)|Tipo complexo|Especifica que Olá é tarefa várias instâncias que exigem vários nós de computação.  Consulte [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) para obter detalhes.|
|[restrições](#constraints)|Tipo complexo|restrições de execução de saudação que se aplicam a tarefa toothis.|
|[executionInfo](#executionInfo)|Tipo complexo|Contém informações sobre a execução de saudação da tarefa de saudação.|

###  <a name="nodeInfo"></a> nodeInfo

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|poolId|Cadeia de caracteres|id de saudação do pool de saudação em qual Olá tarefa foi executada de.|
|nodeId|Cadeia de caracteres|Olá o id do nó de saudação em qual Olá tarefa foi executada.|

###  <a name="multiInstanceSettings"></a> multiInstanceSettings

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|numberOfInstances|int|número de saudação de nós de computação necessários pela tarefa de saudação.|

###  <a name="constraints"></a> restrições

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|Olá número máximo de vezes Olá tarefa pode ser repetida. Olá serviço de lote repete uma tarefa se seu código de saída é diferente de zero.<br /><br /> Observe que esse valor controla especificamente o número de tentativas de saudação. serviço de lote Olá tentará a tarefa Olá uma vez e pode, em seguida, repita o limite de toothis. Por exemplo, se a contagem de repetição máxima Olá é 3, o lote tenta uma tarefa de backup too4 vezes (uma tentativa inicial e 3 tentativas).<br /><br /> Se a contagem de repetição máxima Olá for 0, Olá serviço de lote não tenta novamente a tarefas.<br /><br /> Se a contagem de repetição máxima Olá é -1, o serviço de lote Olá repete tarefas sem limite.<br /><br /> valor padrão de saudação é 0 (sem repetições).|

###  <a name="executionInfo"></a> executionInfo

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|retryCount|Int32|Olá o número de vezes Olá tarefa foi repetida pelo serviço de lote de saudação. tarefa de saudação será repetida se ele for encerrada com um código de saída diferente de zero, o toohello especificado MaxTaskRetryCount|
