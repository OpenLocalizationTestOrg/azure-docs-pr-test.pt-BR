---
title: "operações assíncronas aaaAzure | Microsoft Docs"
description: "Descreve como as operações assíncronas tootrack no Azure."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: 
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: b81254196013adf87998eff11a50993efa52d40d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="track-asynchronous-azure-operations"></a>Rastrear operações assíncronas no Azure
Algumas operações REST do Azure executados de forma assíncrona porque a operação de saudação não pode ser concluída rapidamente. Este tópico descreve como o status de saudação tootrack das operações assíncronas por valores retornado na resposta de saudação.  

## <a name="status-codes-for-asynchronous-operations"></a>Códigos de status de operações assíncronas
Uma operação assíncrona inicialmente retorna um dos seguintes códigos de status HTTP:

* 201 (Criado)
* 202 (Aceito) 

Quando a operação de saudação for concluída com êxito, ele retorna um:

* 200 (OK)
* 204 (Sem Conteúdo) 

Consulte toohello [documentação da API REST](/rest/api/) toosee respostas de saudação para operação Olá estão em execução. 

## <a name="monitor-status-of-operation"></a>Monitorar o status da operação
Olá assíncrona REST operações retornar valores de cabeçalho, que você usar toodetermine Olá status de hello a operação. Potencialmente, existem tooexamine do cabeçalho de três valores:

* `Azure-AsyncOperation`-URL para verificar o status de saudação em andamento da operação de saudação. Se a operação retorna esse valor, sempre use o status de saudação do tootrack de TI (em vez de local) da operação de saudação.
* `Location` ‑ A URL para determinar quando uma operação foi concluída. Use esse valor somente quando Azure-AsyncOperation não é retornado.
* `Retry-After`-Olá o número de segundos toowait antes de verificar o status de saudação de operação assíncrona hello.

No entanto, nem toda operação assíncrona retorna todos esses valores. Por exemplo, o valor do cabeçalho tooevaluate hello Azure AsyncOperation talvez seja necessário para uma operação e o valor de cabeçalho de local Olá para outra operação. 

Recuperar valores de cabeçalho hello como recuperaria qualquer valor de cabeçalho de uma solicitação. Por exemplo, no c#, você recuperar valor de cabeçalho de saudação de um `HttpWebResponse` objeto chamado `response` com hello código a seguir:

```cs
response.Headers.GetValues("Azure-AsyncOperation").GetValue(0)
```

## <a name="azure-asyncoperation-request-and-response"></a>Solicitação e resposta de Azure-AsyncOperation

status de saudação de tooget de operação assíncrona do hello, enviar uma URL de toohello solicitação GET no valor do cabeçalho do Azure AsyncOperation.

corpo de Olá de resposta de saudação desta operação contém informações sobre a operação hello. Olá, exemplo a seguir mostra os valores possíveis Olá retornados da operação de saudação:

```json
{
    "id": "{resource path from GET operation}",
    "name": "{operation-id}", 
    "status" : "Succeeded | Failed | Canceled | {resource provider values}", 
    "startTime": "2017-01-06T20:56:36.002812+00:00",
    "endTime": "2017-01-06T20:56:56.002812+00:00",
    "percentComplete": {double between 0 and 100 },
    "properties": {
        /* Specific resource provider values for successful operations */
    },
    "error" : { 
        "code": "{error code}",  
        "message": "{error description}" 
    }
}
```

Somente `status` é retornado para todas as respostas. objeto de erro de saudação é retornado quando o status de saudação é falha ou cancelada. Todos os outros valores são opcionais. Portanto, resposta Olá que recebe pode ser diferente do exemplo hello.

## <a name="provisioningstate-values"></a>Valores de provisioningState

Operações que criam, atualizam ou excluem (PUT, PATCH, DELETE) um recurso geralmente retornam um valor `provisioningState`. Quando uma operação for concluída, um dos três valores a seguir será retornado: 

* Bem-sucedida
* Falha
* Cancelado

Todos os outros valores indicam a operação Olá ainda está em execução. provedor de recursos de saudação pode retornar um valor que indica o estado. Por exemplo, você pode receber **aceito** quando a solicitação de saudação é recebida e em execução.

## <a name="example-requests-and-responses"></a>Exemplo de solicitações e respostas

### <a name="start-virtual-machine-202-with-azure-asyncoperation"></a>Iniciar a máquina virtual (202 com Azure-AsyncOperation)
Este exemplo mostra como toodetermine Olá status de **iniciar** operação para máquinas virtuais. solicitação de saudação inicial está em Olá formato a seguir:

```HTTP
POST 
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Compute/virtualMachines/{vm-name}/start?api-version=2016-03-30
```

Ele retorna um código de status 202. Entre os valores de cabeçalho hello, consulte:

```HTTP
Azure-AsyncOperation : https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

status de saudação toocheck da operação assíncrona do hello, enviar outra solicitação toothat URL.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Compute/locations/{region}/operations/{operation-id}?api-version=2016-03-30
```

corpo da resposta Olá contém status de saudação da operação de saudação:

```json
{
  "startTime": "2017-01-06T18:58:24.7596323+00:00",
  "status": "InProgress",
  "name": "9a062a88-e463-4697-bef2-fe039df73a02"
}
```

### <a name="deploy-resources-201-with-azure-asyncoperation"></a>Implantar recursos (201 com Azure-AsyncOperation)

Este exemplo mostra como toodetermine Olá status de **implantações** operação para implantar recursos tooAzure. solicitação de saudação inicial está em Olá formato a seguir:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/microsoft.resources/deployments/{deployment-name}?api-version=2016-09-01
```

Ele retorna um código de status 201. saudação de corpo de resposta de saudação inclui:

```json
"provisioningState":"Accepted",
```

Entre os valores de cabeçalho hello, consulte:

```HTTP
Azure-AsyncOperation: https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

status de saudação toocheck da operação assíncrona do hello, enviar outra solicitação toothat URL.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/resourcegroups/{resource-group}/providers/Microsoft.Resources/deployments/{deployment-name}/operationStatuses/{operation-id}?api-version=2016-09-01
```

corpo da resposta Olá contém status de saudação da operação de saudação:

```json
{"status":"Running"}
```

Quando Olá implantação for concluída, a resposta de saudação contém:

```json
{"status":"Succeeded"}
```

### <a name="create-storage-account-202-with-location-and-retry-after"></a>Criar conta de armazenamento (202 com Location e Retry-After)

Este exemplo mostra como toodetermine Olá status de saudação **criar** operação para contas de armazenamento. solicitação de saudação inicial está em Olá formato a seguir:

```HTTP
PUT
https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group}/providers/Microsoft.Storage/storageAccounts/{storage-name}?api-version=2016-01-01
```

E o corpo da solicitação Olá contém propriedades da conta de armazenamento hello:

```json
{ "location": "South Central US", "properties": {}, "sku": { "name": "Standard_LRS" }, "kind": "Storage" }
```

Ele retorna um código de status 202. Entre os valores de cabeçalho hello, você verá Olá dois valores a seguir:

```HTTP
Location: https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
Retry-After: 17
```

Depois de aguardar por número de segundos especificado em Retry-After, verifique o status de saudação de operação assíncrona Olá enviando outra solicitação toothat URL.

```HTTP
GET 
https://management.azure.com/subscriptions/{subscription-id}/providers/Microsoft.Storage/operations/{operation-id}?monitor=true&api-version=2016-01-01
```

Se a solicitação Olá ainda está em execução, você receberá um código de status 202. Se a solicitação de saudação for concluída, a receber um código de status 200 e corpo de saudação da resposta Olá contém propriedades de Olá Olá da conta de armazenamento que foi criado.

## <a name="next-steps"></a>Próximas etapas

* Para ver a documentação sobre cada operação REST, consulte [Documentação da API REST](/rest/api/).
* Para obter informações sobre o gerenciamento de recursos por meio de saudação REST API do Gerenciador de recursos, consulte [hello usando REST API do Gerenciador de recursos](resource-manager-rest-api.md).
* Para obter informações sobre a implantação de modelos por meio de saudação REST API do Gerenciador de recursos, consulte [implantar recursos com modelos do Gerenciador de recursos e a API de REST do Gerenciador de recursos](resource-group-template-deploy-rest.md).
