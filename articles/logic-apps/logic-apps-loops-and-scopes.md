---
title: "aaaCreate loops e os escopos ou debatch dados em fluxos de trabalho - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Criar loops tooiterate pelos dados, agrupar ações em escopos, ou debatch toostart dados mais fluxos de trabalho em aplicativos do Azure lógica."
services: logic-apps
documentationcenter: .net,nodejs,java
author: jeffhollan
manager: anneta
editor: 
ms.assetid: 75b52eeb-23a7-47dd-a42f-1351c6dfebdc
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/29/2016
ms.author: LADocs; jehollan
ms.openlocfilehash: e612ec2e83541f028916a07bf12c44e7b1f57ad1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a>Loops, Escopos e Debatch dos Aplicativos Lógicos
  
Lógica de aplicativos fornece um número de maneiras toowork com matrizes, coleções, lotes e loops dentro de um fluxo de trabalho.
  
## <a name="foreach-loop-and-arrays"></a>Matrizes e loop ForEach
  
Lógica de aplicativos permite que você tooloop em um conjunto de dados e executar uma ação para cada item.  Isso é possível por meio de saudação `foreach` ação.  No designer de saudação, você pode especificar tooadd um loop for each.  Depois de selecionar a matriz de saudação que desejar tooiterate sobre, você pode começar a adicionar ações.  Atualmente você está limitado tooonly uma ação por loop foreach, mas essa restrição será eliminada em hello em semanas.  Uma vez em loop hello, você pode começar toospecify o que deve ocorrer a cada valor de matriz de saudação.

Se você estiver usando o modo de exibição de código, poderá especificar um loop for each como o abaixo.  Este é um exemplo de um loop for each que envia um email para cada endereço de email com 'microsoft.com':

``` json
{
    "email_filter": {
        "type": "query",
        "inputs": {
            "from": "@triggerBody()['emails']",
            "where": "@contains(item()['email'], 'microsoft.com')"
        }
    },
    "forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "actions": {
            "send_email": {
                "type": "ApiConnection",
                "inputs": {
                "body": {
                    "to": "@item()",
                    "from": "me@contoso.com",
                    "message": "Hello, thank you for ordering"
                },
                "host": {
                    "connection": {
                        "id": "@parameters('$connections')['office365']['connection']['id']"
                    }
                },
                }
            }
        },
        "runAfter":{
            "email_filter": [ "Succeeded" ]
        }
    }
}
```
  
  Um `foreach` ação pode iterar em matrizes de too5, linhas, 000.  Por padrão, cada iteração será executada paralelamente.  

### <a name="sequential-foreach-loops"></a>Loops ForEach sequenciais

tooenable um tooexecute de loop foreach em sequência, Olá `Sequential` deve ser adicionada a opção de operação.

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a>Loop Until
  
  Você pode executar uma ação ou uma série de ações até que uma condição seja atendida.  Olá cenário mais comum para isso é chamar um ponto de extremidade até obter resposta de saudação que você está procurando.  No designer de saudação, você pode especificar tooadd um até que o loop.  Depois de adicionar as ações Olá loop, você pode definir a condição de saída de hello, bem como Olá limites do loop.  Há um atraso de um minuto entre os ciclos de loop.
  
  Se você estiver usando o modo de exibição de código, poderá especificar um loop unitl como o abaixo.  Este é um exemplo de como chamar um ponto de extremidade HTTP até que o corpo da resposta Olá tem valor de saudação 'Concluído'.  Ele será concluído quando a 
  
  * Resposta HTTP tiver o status 'Concluído'
  * Ele tentou por uma hora
  * Ele entrou em loop 100 vezes
  
  ``` json
  {
      "until_successful":{
        "type": "until",
        "expression": "@equals(actions('http')['status'], 'Completed')",
        "limit": {
            "count": 100,
            "timeout": "PT1H"
        },
        "actions": {
            "create_resource": {
                "type": "http",
                "inputs": {
                    "url": "http://provisionRseource.com",
                    "body": {
                        "resourceId": "@triggerBody()"
                    }
                }
            }
        }
      }
  }
  ```
  
## <a name="spliton-and-debatching"></a>SplitOn e debatching

Às vezes, um gatilho pode ser uma matriz de itens que você deseja toodebatch e iniciar um fluxo de trabalho por item.  Isso pode ser feito por meio de saudação `spliton` comando.  Por padrão, se o gatilho swagger especificar uma carga que seja uma matriz, um `spliton` será adicionado e iniciará uma execução por item.  SplitOn só pode ser adicionado tooa gatilho.  Isso pode ser manualmente configurado ou substituído na exibição de código de definição.  No momento SplitOn pode debatch matrizes de too5, 000 itens.  Você não pode ter um `spliton` e também implementa o padrão de resposta síncrona de saudação.  Qualquer fluxo de trabalho chamado que tem um `response` ação além disso muito`spliton` serão executados de forma assíncrona e enviar imediato `202 Accepted` resposta.  

SplitOn pode ser especificado no modo de exibição de código como Olá exemplo a seguir.  Isso recebe uma matriz de itens e faz debatch em cada linha.

```
{
    "myDebatchTrigger": {
        "type": "Http",
        "inputs": {
            "url": "http://getNewCustomers",
        },
        "recurrence": {
            "frequencey": "Second",
            "interval": 15
        },
        "spliton": "@triggerBody()['rows']"
    }
}
```

## <a name="scopes"></a>Escopos

É possível toogroup uma série de ações usando um escopo.  Isso é particularmente útil para implementar o tratamento de exceções.  No designer de saudação, você pode adicionar um novo escopo e começar a adicionar as ações dentro dele.  Você pode definir escopos na visualização de código como Olá a seguir:


```
{
    "myScope": {
        "type": "scope",
        "actions": {
            "call_bing": {
                "type": "http",
                "inputs": {
                    "url": "http://www.bing.com"
                }
            }
        }
    }
}
```