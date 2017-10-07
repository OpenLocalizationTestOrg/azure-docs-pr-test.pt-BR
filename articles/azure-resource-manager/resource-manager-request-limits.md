---
title: "limites de solicitações do Gerenciador de recursos de aaaAzure | Microsoft Docs"
description: "Descreve como toouse limitação com o Azure Resource Manager solicita quando os limites de assinatura foi atingidos."
services: azure-resource-manager
documentationcenter: na
author: tfitzmac
manager: timlt
editor: tysonn
ms.assetid: e1047233-b8e4-4232-8919-3268d93a3824
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/11/2017
ms.author: tomfitz
ms.openlocfilehash: ea274f3145af36aac753730e1f280d8a8b59c3bf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="throttling-resource-manager-requests"></a>Restrição de solicitações do Resource Manager
Para cada assinatura e de locatário, limites de Gerenciador de recursos too15 de solicitações, 000 por hora de leitura e gravação solicitações too1, 200 por hora. Esses limites se aplicam a instância do Gerenciador de recursos do Azure tooeach; Há várias instâncias em todas as regiões do Azure e do Azure Resource Manager é implantado tooall Azure regiões.  Portanto, na prática, os limites são efetivamente muito maiores do que aqueles listados acima, pois as solicitações do usuário são geralmente atendidas por muitas instâncias diferentes.

Se seu aplicativo ou script atingir esses limites, você precisa toothrottle suas solicitações. Este tópico mostra como Olá toodetermine restantes solicita que você tem antes de atingir o limite de saudação e toorespond quando você atingiu o limite de saudação.

Quando você atingir o limite de saudação, você receberá o código de status HTTP da saudação **muito 429 muitas solicitações**.

número de solicitações de Olá é tooeither no escopo de sua assinatura ou seu locatário. Se você tiver várias, aplicativos simultâneos fazendo solicitações em sua assinatura, Olá solicitações desses aplicativos são adicionados juntos toodetermine número de saudação de solicitações restantes.

Solicitações de assinatura no escopo são aquelas Olá envolvem passando a id de assinatura, como recuperar grupos de recursos de saudação em sua assinatura. Solicitações no escopo do locatário não incluem sua ID de assinatura, assim como a recuperação de locais do Azure válidos.

## <a name="remaining-requests"></a>Solicitações restantes
Você pode determinar o número de saudação de solicitações restantes, examinando os cabeçalhos de resposta. Cada solicitação inclui valores de número de saudação de solicitações de gravação e leitura restante. Olá tabela a seguir descreve cabeçalhos de resposta de saudação, que você pode examinar os valores:

| Cabeçalho de resposta | Descrição |
| --- | --- |
| x-ms-ratelimit-remaining-subscription-reads |Leituras no escopo da assinatura restantes |
| x-ms-ratelimit-remaining-subscription-writes |Gravações no escopo da assinatura restantes |
| x-ms-ratelimit-remaining-tenant-reads |Leituras no escopo do locatário restantes |
| x-ms-ratelimit-remaining-tenant-writes |Gravações no escopo do locatário restantes |
| x-ms-ratelimit-remaining-subscription-resource-requests |Solicitações de tipo de recurso no escopo da assinatura restantes.<br /><br />Esse valor de cabeçalho é retornado somente se um serviço tiver substituído o limite padrão de saudação. Gerenciador de recursos adiciona esse valor em vez da saudação assinatura leituras ou gravações. |
| x-ms-ratelimit-remaining-subscription-resource-entities-read |Solicitações de coletas de tipo de recurso no escopo da assinatura restantes.<br /><br />Esse valor de cabeçalho é retornado somente se um serviço tiver substituído o limite padrão de saudação. Esse valor fornece o número de saudação de coleta de solicitações restantes (recursos de lista). |
| x-ms-ratelimit-remaining-tenant-resource-requests |Solicitações de tipo de recurso no escopo do locatário restantes.<br /><br />Esse cabeçalho é adicionado somente para solicitações no nível de locatário, e somente se um serviço tiver substituído o limite padrão de saudação. Gerenciador de recursos adiciona esse valor em vez da saudação locatário leituras ou gravações. |
| x-ms-ratelimit-remaining-tenant-resource-entities-read |Solicitações de coletas de tipo de recurso no escopo do locatário restantes.<br /><br />Esse cabeçalho é adicionado somente para solicitações no nível de locatário, e somente se um serviço tiver substituído o limite padrão de saudação. |

## <a name="retrieving-hello-header-values"></a>Recuperando valores de cabeçalho Olá
Recuperar esses valores de cabeçalho no seu código ou script não é diferente de recuperar um outro valor de cabeçalho qualquer. 

Por exemplo, em **c#**, recuperar o valor de cabeçalho de saudação de um **HttpWebResponse** objeto chamado **resposta** com hello código a seguir:

```cs
response.Headers.GetValues("x-ms-ratelimit-remaining-subscription-reads").GetValue(0)
```

Em **PowerShell**, recuperar o valor de cabeçalho de saudação de uma operação de Invoke-WebRequest.

```powershell
$r = Invoke-WebRequest -Uri https://management.azure.com/subscriptions/{guid}/resourcegroups?api-version=2016-09-01 -Method GET -Headers $authHeaders
$r.Headers["x-ms-ratelimit-remaining-subscription-reads"]
```

Ou, se quiser toosee Olá restantes solicitações de depuração, você pode fornecer Olá **-Debug** parâmetro em sua **PowerShell** cmdlet.

```powershell
Get-AzureRmResourceGroup -Debug
```

Que retorna vários valores, incluindo o seguinte valor de resposta de saudação:

```powershell
...
DEBUG: ============================ HTTP RESPONSE ============================

Status Code:
OK

Headers:
Pragma                        : no-cache
x-ms-ratelimit-remaining-subscription-reads: 14999
...
```

Em **CLI do Azure**, recuperar o valor do cabeçalho hello usando Olá opção mais detalhada.

```azurecli
azure group list -vv --json
```

Que retorna vários valores, incluindo Olá objeto a seguir:

```azurecli
...
silly: returnObject
{
  "statusCode": 200,
  "header": {
    "cache-control": "no-cache",
    "pragma": "no-cache",
    "content-type": "application/json; charset=utf-8",
    "expires": "-1",
    "x-ms-ratelimit-remaining-subscription-reads": "14998",
    ...
```

## <a name="waiting-before-sending-next-request"></a>Aguardando antes de enviar a próxima solicitação
Quando você atingir o limite de solicitação de Olá, Gerenciador de recursos retorna Olá **429** código de status HTTP e um **Retry-After** valor no cabeçalho de saudação. Olá **Retry-After** valor Especifica o número de saudação de segundos que o aplicativo deve aguardar (ou suspensão) antes de enviar a próxima solicitação de saudação. Se você enviar uma solicitação antes de decorrido o valor de repetição hello, sua solicitação não será processada e será retornado um novo valor de repetição.

## <a name="next-steps"></a>Próximas etapas

* Para obter mais informações sobre limites e cotas, confira [Assinatura do Azure e limite de serviços, cotas e restrições](../azure-subscription-service-limits.md).
* toolearn sobre o tratamento de solicitações REST assíncronas, consulte [controlar operações assíncronas de Azure](resource-manager-async-operations.md).
