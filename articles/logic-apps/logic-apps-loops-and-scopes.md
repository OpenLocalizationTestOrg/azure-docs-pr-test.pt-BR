---
title: "Criar loops e escopos ou retirar dados de lote em fluxos de trabalho - Aplicativos Lógicos do Azure | Microsoft Docs"
description: "Criar loops para iterar por meio de dados, as ações de grupo em escopos, ou retirar dados de lote para iniciar mais fluxos de trabalho em Aplicativos Lógicos do Azure."
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
ms.openlocfilehash: 413a2ba9107ca259ed577825bf0a17ff5622f1ac
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="logic-apps-loops-scopes-and-debatching"></a><span data-ttu-id="27fc0-103">Loops, Escopos e Debatch dos Aplicativos Lógicos</span><span class="sxs-lookup"><span data-stu-id="27fc0-103">Logic Apps Loops, Scopes, and Debatching</span></span>
  
<span data-ttu-id="27fc0-104">Os Aplicativos Lógicos fornecem várias maneiras de trabalhar com matrizes, coleções, lotes e loops em um fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="27fc0-104">Logic Apps provides a number of ways to work with arrays, collections, batches, and loops within a workflow.</span></span>
  
## <a name="foreach-loop-and-arrays"></a><span data-ttu-id="27fc0-105">Matrizes e loop ForEach</span><span class="sxs-lookup"><span data-stu-id="27fc0-105">ForEach loop and arrays</span></span>
  
<span data-ttu-id="27fc0-106">Os Aplicativos Lógicos permitem que você faça um loop em um conjunto de dados e execute uma ação para cada item.</span><span class="sxs-lookup"><span data-stu-id="27fc0-106">Logic Apps allows you to loop over a set of data and perform an action for each item.</span></span>  <span data-ttu-id="27fc0-107">Isso é possível por meio da ação `foreach` .</span><span class="sxs-lookup"><span data-stu-id="27fc0-107">This is possible via the `foreach` action.</span></span>  <span data-ttu-id="27fc0-108">No designer, você pode especificar a adição de um loop for each.</span><span class="sxs-lookup"><span data-stu-id="27fc0-108">In the designer, you can specify to add a for each loop.</span></span>  <span data-ttu-id="27fc0-109">Depois de selecionar a matriz em que você deseja iterar, você poderá começar a adicionar ações.</span><span class="sxs-lookup"><span data-stu-id="27fc0-109">After selecting the array you wish to iterate over, you can begin adding actions.</span></span>  <span data-ttu-id="27fc0-110">No momento, você está limitado a apenas uma ação por loop foreach, mas essa restrição será eliminada nas próximas semanas.</span><span class="sxs-lookup"><span data-stu-id="27fc0-110">Currently you are limited to only one action per foreach loop, but this restriction will be lifted in the coming weeks.</span></span>  <span data-ttu-id="27fc0-111">Uma vez no loop, você poderá começar a especificar o que deve ocorrer em cada valor da matriz.</span><span class="sxs-lookup"><span data-stu-id="27fc0-111">Once within the loop you can begin to specify what should occur at each value of the array.</span></span>

<span data-ttu-id="27fc0-112">Se você estiver usando o modo de exibição de código, poderá especificar um loop for each como o abaixo.</span><span class="sxs-lookup"><span data-stu-id="27fc0-112">If using code-view, you can specify a for each loop like below.</span></span>  <span data-ttu-id="27fc0-113">Este é um exemplo de um loop for each que envia um email para cada endereço de email com 'microsoft.com':</span><span class="sxs-lookup"><span data-stu-id="27fc0-113">This is an example of a for each loop that sends an email for each email address that contains 'microsoft.com':</span></span>

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
  
  <span data-ttu-id="27fc0-114">Uma ação `foreach` pode iterar em matrizes até 5.000 linhas.</span><span class="sxs-lookup"><span data-stu-id="27fc0-114">A `foreach` action can iterate over arrays up to 5,000 rows.</span></span>  <span data-ttu-id="27fc0-115">Por padrão, cada iteração será executada paralelamente.</span><span class="sxs-lookup"><span data-stu-id="27fc0-115">Each iteration will execute in parallel by default.</span></span>  

### <a name="sequential-foreach-loops"></a><span data-ttu-id="27fc0-116">Loops ForEach sequenciais</span><span class="sxs-lookup"><span data-stu-id="27fc0-116">Sequential ForEach loops</span></span>

<span data-ttu-id="27fc0-117">Para habilitar um loop foreach para ser executado sequencialmente, a opção de operação `Sequential` deve ser adicionada.</span><span class="sxs-lookup"><span data-stu-id="27fc0-117">To enable a foreach loop to execute sequentially, the `Sequential` operation option should be added.</span></span>

``` json
"forEach_email": {
        "type": "foreach",
        "foreach": "@body('email_filter')",
        "operationOptions": "Sequential",
        "..."
}
```
  
## <a name="until-loop"></a><span data-ttu-id="27fc0-118">Loop Until</span><span class="sxs-lookup"><span data-stu-id="27fc0-118">Until loop</span></span>
  
  <span data-ttu-id="27fc0-119">Você pode executar uma ação ou uma série de ações até que uma condição seja atendida.</span><span class="sxs-lookup"><span data-stu-id="27fc0-119">You can perform an action or series of actions until a condition is met.</span></span>  <span data-ttu-id="27fc0-120">O cenário mais comum para isso é chamar um ponto de extremidade até você chegar à resposta que está procurando.</span><span class="sxs-lookup"><span data-stu-id="27fc0-120">The most common scenario for this is calling an endpoint until you get the response you are looking for.</span></span>  <span data-ttu-id="27fc0-121">No designer, você pode especificar a adição de um loop until.</span><span class="sxs-lookup"><span data-stu-id="27fc0-121">In the designer, you can specify to add an until loop.</span></span>  <span data-ttu-id="27fc0-122">Depois de adicionar ações dentro do loop, você poderá definir a condição de saída, bem como os limites do loop.</span><span class="sxs-lookup"><span data-stu-id="27fc0-122">After adding actions inside the loop, you can set the exit condition, as well as the loop limits.</span></span>  <span data-ttu-id="27fc0-123">Há um atraso de um minuto entre os ciclos de loop.</span><span class="sxs-lookup"><span data-stu-id="27fc0-123">There is a 1 minute delay between loop cycles.</span></span>
  
  <span data-ttu-id="27fc0-124">Se você estiver usando o modo de exibição de código, poderá especificar um loop unitl como o abaixo.</span><span class="sxs-lookup"><span data-stu-id="27fc0-124">If using code-view, you can specify an until loop like below.</span></span>  <span data-ttu-id="27fc0-125">Este é um exemplo de chamada a um ponto de extremidade HTTP até que o corpo da resposta tenha o valor 'Concluído'.</span><span class="sxs-lookup"><span data-stu-id="27fc0-125">This is an example of calling an HTTP endpoint until the response body has the value 'Completed'.</span></span>  <span data-ttu-id="27fc0-126">Ele será concluído quando a</span><span class="sxs-lookup"><span data-stu-id="27fc0-126">It will complete when either</span></span> 
  
  * <span data-ttu-id="27fc0-127">Resposta HTTP tiver o status 'Concluído'</span><span class="sxs-lookup"><span data-stu-id="27fc0-127">HTTP Response has status of 'Completed'</span></span>
  * <span data-ttu-id="27fc0-128">Ele tentou por uma hora</span><span class="sxs-lookup"><span data-stu-id="27fc0-128">It has tried for 1 hour</span></span>
  * <span data-ttu-id="27fc0-129">Ele entrou em loop 100 vezes</span><span class="sxs-lookup"><span data-stu-id="27fc0-129">It has looped 100 times</span></span>
  
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
  
## <a name="spliton-and-debatching"></a><span data-ttu-id="27fc0-130">SplitOn e debatching</span><span class="sxs-lookup"><span data-stu-id="27fc0-130">SplitOn and debatching</span></span>

<span data-ttu-id="27fc0-131">Às vezes, um gatilho pode receber uma matriz de itens nos quais deseja fazer debatch e iniciar um fluxo de trabalho por item.</span><span class="sxs-lookup"><span data-stu-id="27fc0-131">Sometimes a trigger may receive an array of items that you want to debatch and start a workflow per item.</span></span>  <span data-ttu-id="27fc0-132">Isso pode ser feito por meio do comando `spliton` .</span><span class="sxs-lookup"><span data-stu-id="27fc0-132">This can be accomplished via the `spliton` command.</span></span>  <span data-ttu-id="27fc0-133">Por padrão, se o gatilho swagger especificar uma carga que seja uma matriz, um `spliton` será adicionado e iniciará uma execução por item.</span><span class="sxs-lookup"><span data-stu-id="27fc0-133">By default, if your trigger swagger specifies a payload that is an array, a `spliton` will be added and start a run per item.</span></span>  <span data-ttu-id="27fc0-134">SplitOn só pode ser adicionado a um gatilho.</span><span class="sxs-lookup"><span data-stu-id="27fc0-134">SplitOn can only be added to a trigger.</span></span>  <span data-ttu-id="27fc0-135">Isso pode ser manualmente configurado ou substituído na exibição de código de definição.</span><span class="sxs-lookup"><span data-stu-id="27fc0-135">This can be manually configured or overridden in definition code-view.</span></span>  <span data-ttu-id="27fc0-136">Atualmente, o SplitOn pode fazer debatch em matrizes de até 5.000 itens.</span><span class="sxs-lookup"><span data-stu-id="27fc0-136">Currently SplitOn can debatch arrays up to 5,000 items.</span></span>  <span data-ttu-id="27fc0-137">Você não pode ter um `spliton` e também implementar o padrão de resposta síncrona.</span><span class="sxs-lookup"><span data-stu-id="27fc0-137">You cannot have a `spliton` and also implement the synchronous response pattern.</span></span>  <span data-ttu-id="27fc0-138">Qualquer fluxo de trabalho chamado com uma ação `response` além de `spliton` será executado de forma assíncrona e enviará uma resposta `202 Accepted` imediata.</span><span class="sxs-lookup"><span data-stu-id="27fc0-138">Any workflow called that has a `response` action in addition to `spliton` will run asynchronously and send an immediate `202 Accepted` response.</span></span>  

<span data-ttu-id="27fc0-139">SplitOn pode ser especificado no modo de exibição de código como o exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="27fc0-139">SplitOn can be specified in code-view as the following example.</span></span>  <span data-ttu-id="27fc0-140">Isso recebe uma matriz de itens e faz debatch em cada linha.</span><span class="sxs-lookup"><span data-stu-id="27fc0-140">This receives an array of items and debatches on each row.</span></span>

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

## <a name="scopes"></a><span data-ttu-id="27fc0-141">Escopos</span><span class="sxs-lookup"><span data-stu-id="27fc0-141">Scopes</span></span>

<span data-ttu-id="27fc0-142">É possível agrupar uma série de ações usando um escopo.</span><span class="sxs-lookup"><span data-stu-id="27fc0-142">It is possible to group a series of actions together using a scope.</span></span>  <span data-ttu-id="27fc0-143">Isso é particularmente útil para implementar o tratamento de exceções.</span><span class="sxs-lookup"><span data-stu-id="27fc0-143">This is particularly useful for implementing exception handling.</span></span>  <span data-ttu-id="27fc0-144">No designer, você pode adicionar um novo escopo e começar a adicionar ações dentro dele.</span><span class="sxs-lookup"><span data-stu-id="27fc0-144">In the designer you can add a new scope, and begin adding any actions inside of it.</span></span>  <span data-ttu-id="27fc0-145">É possível definir escopos no modo de exibição de código semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="27fc0-145">You can define scopes in code-view like the following:</span></span>


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