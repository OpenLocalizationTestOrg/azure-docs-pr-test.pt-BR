---
title: "Eventos de início de tarefa em lote do Azure | Microsoft Docs"
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
ms.openlocfilehash: c47ab36c99dddd46a14c15018a2a46bf7f873ffa
ms.sourcegitcommit: 6699c77dcbd5f8a1a2f21fba3d0a0005ac9ed6b7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/11/2017
---
# <a name="task-start-event"></a>Evento de início da tarefa

 Esse evento é emitido quando uma tarefa é agendada para iniciar em um nó de computação pelo agendador. Observe que, se a tarefa for repetida ou colocada novamente na fila, esse evento será emitido novamente para a mesma tarefa, mas a contagem de repetição e versão de tarefa do sistema serão atualizadas adequadamente.


 O exemplo a seguir mostra o corpo de um evento de início da tarefa.

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
|jobId|Cadeia de caracteres|A ID do trabalho que contém a tarefa.|
|ID|Cadeia de caracteres|A ID da tarefa.|
|taskType|Cadeia de caracteres|O tipo de tarefa. Pode ser “JobManager” indicando que é uma tarefa do gerenciador de trabalhos ou “Usuário”, indicando que não é uma tarefa do gerenciador de trabalhos.|
|systemTaskVersion|Int32|Esse é o contador interno de repetição de uma tarefa. Internamente, o serviço em lotes pode repetir uma tarefa para contabilizar problemas transitórios. Esses problemas podem incluir erros internos de agendamento ou tentativa de recuperar nós de computação em estado inválido.|
|[nodeInfo](#nodeInfo)|Tipo complexo|Contém informações sobre o nó de computação em que a tarefa é executada.|
|[multiInstanceSettings](#multiInstanceSettings)|Tipo complexo|Especifica que a tarefa é uma tarefa com várias instâncias que precisa de vários nós de computação.  Consulte [multiInstanceSettings](https://docs.microsoft.com/rest/api/batchservice/get-information-about-a-task) para obter detalhes.|
|[restrições](#constraints)|Tipo complexo|As restrições de execução aplicáveis a essa tarefa.|
|[executionInfo](#executionInfo)|Tipo complexo|Contém informações sobre a execução da tarefa.|

###  <a name="nodeInfo"></a> nodeInfo

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|poolId|Cadeia de caracteres|A ID do pool em que a tarefa foi executada.|
|nodeId|Cadeia de caracteres|A ID do nó em que a tarefa foi executada.|

###  <a name="multiInstanceSettings"></a> multiInstanceSettings

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|numberOfInstances|int|O número de nós de computação que a tarefa precisa.|

###  <a name="constraints"></a> restrições

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|maxTaskRetryCount|Int32|O número máximo de vezes que a tarefa pode ser repetida. O serviço em lotes repetirá uma tarefa se seu código de saída for diferente de zero.<br /><br /> Observe que esse valor controla especificamente o número de tentativas. O serviço em lotes tentará a tarefa uma vez e, em seguida, pode tentar novamente até esse limite. Por exemplo, se a contagem máxima de repetição for 3, o lote tentará uma tarefa até 4 vezes (uma tentativa inicial e 3 repetições).<br /><br /> Se a contagem máxima de repetição for 0, o serviço em lote não tentará repetir a tarefas.<br /><br /> Se a contagem máxima de repetição for -1, o serviço em lotes repetirá as tarefas ilimitadamente.<br /><br /> O valor padrão é 0 (sem novas tentativas).|

###  <a name="executionInfo"></a> executionInfo

|Nome do elemento|Tipo|Observações|
|------------------|----------|-----------|
|retryCount|Int32|O número de vezes que a tarefa foi repetida pelo serviço em lotes. A tarefa será repetida se a saída tiver um código de saída diferente de zero, até a MaxTaskRetryCount especificada|
