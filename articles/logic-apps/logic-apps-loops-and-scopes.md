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
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="7a320-103">Loops, Escopos e Debatch dos Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="7a320-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="7a320-104">Lógica de aplicativos fornece um número de maneiras toowork com matrizes, coleções, lotes e loops dentro de um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="7a320-104">Logic Apps provides a number of ways toowork with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="7a320-105">Matrizes e loop ForEach</span><span class="sxs-lookup"><span data-stu-id="7a320-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="7a320-106">Lógica de aplicativos permite que você tooloop em um conjunto de dados e executar uma ação para cada item.</span><span class="sxs-lookup"><span data-stu-id="7a320-106">Logic Apps allows you tooloop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="7a320-107">Isso é possível por meio de saudação `foreach` ação.</span><span class="sxs-lookup"><span data-stu-id="7a320-107">This is possible via hello `foreach` action.</span></span>  <span data-ttu-id="7a320-108">No designer de saudação, você pode especificar tooadd um loop for each.</span><span class="sxs-lookup"><span data-stu-id="7a320-108">In hello designer, you can specify tooadd a for each loop.</span></span>  <span data-ttu-id="7a320-109">Depois de selecionar a matriz de saudação que desejar tooiterate sobre, você pode começar a adicionar ações.</span><span class="sxs-lookup"><span data-stu-id="7a320-109">After selecting hello array you wish tooiterate over, you can begin adding actions.</span></span>  <span data-ttu-id="7a320-110">Atualmente você está limitado tooonly uma ação por loop foreach, mas essa restrição será eliminada em hello em semanas.</span><span class="sxs-lookup"><span data-stu-id="7a320-110">Currently you are limited tooonly one action per foreach loop, but this restriction will be lifted in hello coming weeks.</span></span>  <span data-ttu-id="7a320-111">Uma vez em loop hello, você pode começar toospecify o que deve ocorrer a cada valor de matriz de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a320-111">Once within hello loop you can begin toospecify what should occur at each value of hello array.</span></span>

<span data-ttu-id="7a320-112">Se você estiver usando o modo de exibição de código, poderá especificar um loop for each como o abaixo.</span><span class="sxs-lookup"><span data-stu-id="7a320-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="7a320-113">Este é um exemplo de um loop for each que envia um email para cada endereço de email com 'microsoft.com':</span><span class="sxs-lookup"><span data-stu-id="7a320-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

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
  
  <span data-ttu-id="7a320-114">Um `foreach` ação pode iterar em matrizes de too5, linhas, 000.</span><span class="sxs-lookup"><span data-stu-id="7a320-114">A `foreach` action can iterate over arrays up too5,000 rows.</span></span>  <span data-ttu-id="7a320-115">Por padrão, cada iteração será executada paralelamente.</span><span class="sxs-lookup"><span data-stu-id="7a320-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="7a320-116">Loops ForEach sequenciais</span><span class="sxs-lookup"><span data-stu-id="7a320-116">Sequential ForEach loops</span></span>

<span data-ttu-id="7a320-117">tooenable um tooexecute de loop foreach em sequência, Olá `Sequential` deve ser adicionada a opção de operação.</span><span class="sxs-lookup"><span data-stu-id="7a320-117">tooenable a foreach loop tooexecute sequentially, hello `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="7a320-118">Loop Until</span><span class="sxs-lookup"><span data-stu-id="7a320-118">Until loop</span></span>
  
  <span data-ttu-id="7a320-119">Você pode executar uma ação ou uma série de ações até que uma condição seja atendida.</span><span class="sxs-lookup"><span data-stu-id="7a320-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="7a320-120">Olá cenário mais comum para isso é chamar um ponto de extremidade até obter resposta de saudação que você está procurando.</span><span class="sxs-lookup"><span data-stu-id="7a320-120">hello most common scenario for this is calling an endpoint until you get hello response you are looking for.</span></span>  <span data-ttu-id="7a320-121">No designer de saudação, você pode especificar tooadd um até que o loop.</span><span class="sxs-lookup"><span data-stu-id="7a320-121">In hello designer, you can specify tooadd an until loop.</span></span>  <span data-ttu-id="7a320-122">Depois de adicionar as ações Olá loop, você pode definir a condição de saída de hello, bem como Olá limites do loop.</span><span class="sxs-lookup"><span data-stu-id="7a320-122">After adding actions inside hello loop, you can set hello exit condition, as well as hello loop limits.</span></span>  <span data-ttu-id="7a320-123">Há um atraso de um minuto entre os ciclos de loop.</span><span class="sxs-lookup"><span data-stu-id="7a320-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="7a320-124">Se você estiver usando o modo de exibição de código, poderá especificar um loop unitl como o abaixo.</span><span class="sxs-lookup"><span data-stu-id="7a320-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="7a320-125">Este é um exemplo de como chamar um ponto de extremidade HTTP até que o corpo da resposta Olá tem valor de saudação 'Concluído'.</span><span class="sxs-lookup"><span data-stu-id="7a320-125">This is an example of calling an HTTP endpoint until hello response body has hello value 'Completed'.</span></span>  <span data-ttu-id="7a320-126">Ele será concluído quando a</span><span class="sxs-lookup"><span data-stu-id="7a320-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="7a320-127">Resposta HTTP tiver o status 'Concluído'</span><span class="sxs-lookup"><span data-stu-id="7a320-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="7a320-128">Ele tentou por uma hora</span><span class="sxs-lookup"><span data-stu-id="7a320-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="7a320-129">Ele entrou em loop 100 vezes</span><span class="sxs-lookup"><span data-stu-id="7a320-129">It has looped 100 times</span></span>
  
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
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="7a320-130">SplitOn e debatching</span><span class="sxs-lookup"><span data-stu-id="7a320-130">SplitOn and debatching</span></span>

<span data-ttu-id="7a320-131">Às vezes, um gatilho pode ser uma matriz de itens que você deseja toodebatch e iniciar um fluxo de trabalho por item.</span><span class="sxs-lookup"><span data-stu-id="7a320-131">Sometimes a trigger may receive an array of items that you want toodebatch and start a workflow per item.</span></span>  <span data-ttu-id="7a320-132">Isso pode ser feito por meio de saudação `spliton` comando.</span><span class="sxs-lookup"><span data-stu-id="7a320-132">This can be accomplished via hello `spliton` command.</span></span>  <span data-ttu-id="7a320-133">Por padrão, se o gatilho swagger especificar uma carga que seja uma matriz, um `spliton` será adicionado e iniciará uma execução por item.</span><span class="sxs-lookup"><span data-stu-id="7a320-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="7a320-134">SplitOn só pode ser adicionado tooa gatilho.</span><span class="sxs-lookup"><span data-stu-id="7a320-134">SplitOn can only be added tooa trigger.</span></span>  <span data-ttu-id="7a320-135">Isso pode ser manualmente configurado ou substituído na exibição de código de definição.</span><span class="sxs-lookup"><span data-stu-id="7a320-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="7a320-136">No momento SplitOn pode debatch matrizes de too5, 000 itens.</span><span class="sxs-lookup"><span data-stu-id="7a320-136">Currently SplitOn can debatch arrays up too5,000 items.</span></span>  <span data-ttu-id="7a320-137">Você não pode ter um `spliton` e também implementa o padrão de resposta síncrona de saudação.</span><span class="sxs-lookup"><span data-stu-id="7a320-137">You cannot have a `spliton` and also implement hello synchronous response pattern.</span></span>  <span data-ttu-id="7a320-138">Qualquer fluxo de trabalho chamado que tem um `response` ação além disso muito`spliton` serão executados de forma assíncrona e enviar imediato `202 Accepted` resposta.</span><span class="sxs-lookup"><span data-stu-id="7a320-138">Any workflow called that has a `response` action in addition too`spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="7a320-139">SplitOn pode ser especificado no modo de exibição de código como Olá exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="7a320-139">SplitOn can be specified in code-view as hello following example.</span></span>  <span data-ttu-id="7a320-140">Isso recebe uma matriz de itens e faz debatch em cada linha.</span><span class="sxs-lookup"><span data-stu-id="7a320-140">This receives an array of items and debatches on each row.</span></span>

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

## <a name="scopes"></a><span data-ttu-id="7a320-141">Escopos</span><span class="sxs-lookup"><span data-stu-id="7a320-141">Scopes</span></span>

<span data-ttu-id="7a320-142">É possível toogroup uma série de ações usando um escopo.</span><span class="sxs-lookup"><span data-stu-id="7a320-142">It is possible toogroup a series of actions together using a scope.</span></span>  <span data-ttu-id="7a320-143">Isso é particularmente útil para implementar o tratamento de exceções.</span><span class="sxs-lookup"><span data-stu-id="7a320-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="7a320-144">No designer de saudação, você pode adicionar um novo escopo e começar a adicionar as ações dentro dele.</span><span class="sxs-lookup"><span data-stu-id="7a320-144">In hello designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="7a320-145">Você pode definir escopos na visualização de código como Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="7a320-145">You can define scopes in code-view like hello following:</span></span>


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