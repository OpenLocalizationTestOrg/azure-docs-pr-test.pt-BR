---
title: "Definir fluxos de trabalho com JSON - Aplicativos Lógicos do Azure | Microsoft Docs"
description: "Como escrever definições de fluxo de trabalho em JSON para aplicativos lógicos"
author: jeffhollan
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: d565873c-6b1b-4057-9250-cf81a96180ae
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 03/29/2017
ms.author: LADocs; jehollan
ms.openlocfilehash: 7f9e5a10066df8a464c285273e77a85c0d562ebb
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="047f7-103">Criar definições de fluxo de trabalho para aplicativos lógicos usando JSON</span><span class="sxs-lookup"><span data-stu-id="047f7-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="047f7-104">Você pode criar definições de fluxo de trabalho para [Aplicativos Lógicos do Azure](logic-apps-what-are-logic-apps.md) com linguagem JSON simples e declarativa.</span><span class="sxs-lookup"><span data-stu-id="047f7-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="047f7-105">Se ainda não fez isso, primeiro examine [como criar seu primeiro aplicativo lógico com o Designer de Aplicativos Lógicos](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="047f7-105">If you haven't already, first review [how to create your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="047f7-106">Confira também a [referência completa da Linguagem de Definição de Fluxo de Trabalho](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="047f7-106">Also, see the [full reference for the Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="047f7-107">Repetir etapas em uma lista</span><span class="sxs-lookup"><span data-stu-id="047f7-107">Repeat steps over a list</span></span>

<span data-ttu-id="047f7-108">Para percorrer uma matriz com até 10.000 itens e executar uma ação para cada item, use o [tipo foreach](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="047f7-108">To iterate through an array that has up to 10,000 items and perform an action for each item, use the [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="047f7-109">Lidar com falhas se algo der errado</span><span class="sxs-lookup"><span data-stu-id="047f7-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="047f7-110">Normalmente, convém incluir uma *etapa de correção*: uma lógica que será executada *somente se* uma ou mais de suas chamadas falharem.</span><span class="sxs-lookup"><span data-stu-id="047f7-110">Usually, you want to include a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="047f7-111">Este exemplo obtém dados de vários locais, mas, se a chamada falhar, queremos POSTAR uma mensagem em algum lugar para podermos acompanhar a falha posteriormente:</span><span class="sxs-lookup"><span data-stu-id="047f7-111">This example gets data from various places, but if the call fails, we want to POST a message somewhere so we can track down that failure later:</span></span>  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "postToErrorMessageQueue": {
      "type": "ApiConnection",
      "inputs": "...",
      "runAfter": {
        "readData": [
          "Failed"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="047f7-112">Para especificar que `postToErrorMessageQueue` só será executado depois que `readData` `Failed`, use a propriedade `runAfter`, por exemplo, para especificar uma lista de valores possíveis, para que `runAfter` possa ser `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="047f7-112">To specify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use the `runAfter` property, for example, to specify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="047f7-113">Por fim, como agora este exemplo trata do erro, não marcamos mais a execução como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="047f7-113">Finally, because this example now handles the error, we no longer mark the run as `Failed`.</span></span> <span data-ttu-id="047f7-114">Como adicionamos a etapa para tratar dessa falha neste exemplo, a execução foi `Succeeded`, embora uma etapa `Failed`.</span><span class="sxs-lookup"><span data-stu-id="047f7-114">Because we added the step for handling this failure in this example, the run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="047f7-115">Executar duas ou mais etapas em paralelo</span><span class="sxs-lookup"><span data-stu-id="047f7-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="047f7-116">Para executar várias ações em paralelo, a propriedade `runAfter` deve ser equivalente em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="047f7-116">To run multiple actions in parallel, the `runAfter` property must be equivalent at runtime.</span></span> 

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {},
  "triggers": {
    "Request": {
      "kind": "http",
      "type": "Request"
    }
  },
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      }
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="047f7-117">Neste exemplo, `branch1` e `branch2` são definidos para execução após `readData`.</span><span class="sxs-lookup"><span data-stu-id="047f7-117">In this example, both `branch1` and `branch2` are set to run after `readData`.</span></span> <span data-ttu-id="047f7-118">Como resultado, ambas as ramificações são executadas em paralelo.</span><span class="sxs-lookup"><span data-stu-id="047f7-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="047f7-119">O carimbo de data/hora de ambas as ramificações é idêntico.</span><span class="sxs-lookup"><span data-stu-id="047f7-119">The timestamp for both branches is identical.</span></span>

![Paralelo](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="047f7-121">Unir duas ramificações paralelas</span><span class="sxs-lookup"><span data-stu-id="047f7-121">Join two parallel branches</span></span>

<span data-ttu-id="047f7-122">Você pode unir duas ações que são definidas para execução em paralelo com a adição de itens para a propriedade `runAfter` do exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="047f7-122">You can join two actions that are set to run in parallel by adding items to the `runAfter` property as in the previous example.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-04-01-preview/workflowdefinition.json#",
  "actions": {
    "readData": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {}
    },
    "branch1": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "branch2": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "readData": [
          "Succeeded"
        ]
      }
    },
    "join": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://myurl"
      },
      "runAfter": {
        "branch1": [
          "Succeeded"
        ],
        "branch2": [
          "Succeeded"
        ]
      }
    }
  },
  "parameters": {},
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "Http",
      "inputs": {
        "schema": {}
      }
    }
  },
  "contentVersion": "1.0.0.0",
  "outputs": {}
}
```

![Paralelo](media/logic-apps-author-definitions/join.png)

## <a name="map-list-items-to-a-different-configuration"></a><span data-ttu-id="047f7-124">Mapear itens de lista para uma configuração diferente</span><span class="sxs-lookup"><span data-stu-id="047f7-124">Map list items to a different configuration</span></span>

<span data-ttu-id="047f7-125">Em seguida, digamos que desejemos obter conteúdo diferente com base no valor de uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="047f7-125">Next, let's say that we want to get different content based on the value of a property.</span></span> <span data-ttu-id="047f7-126">Podemos criar um mapa de valores para destinos, como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="047f7-126">We can create a map of values to destinations as a parameter:</span></span>  

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "specialCategories": {
      "defaultValue": [
        "science",
        "google",
        "microsoft",
        "robots",
        "NSA"
      ],
      "type": "Array"
    },
    "destinationMap": {
      "defaultValue": {
        "science": "http://www.nasa.gov",
        "microsoft": "https://www.microsoft.com/en-us/default.aspx",
        "google": "https://www.google.com",
        "robots": "https://en.wikipedia.org/wiki/Robot",
        "NSA": "https://www.nsa.gov/"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "Request",
      "kind": "http"
    }
  },
  "actions": {
    "getArticles": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "https://ajax.googleapis.com/ajax/services/feed/load?v=1.0&q=http://feeds.wired.com/wired/index"
      }
    },
    "forEachArticle": {
      "type": "foreach",
      "foreach": "@body('getArticles').responseData.feed.entries",
      "actions": {
        "ifGreater": {
          "type": "if",
          "expression": "@greater(length(intersection(item().categories, parameters('specialCategories'))), 0)",
          "actions": {
            "getSpecialPage": {
              "type": "Http",
              "inputs": {
                "method": "GET",
                "uri": "@parameters('destinationMap')[first(intersection(item().categories, parameters('specialCategories')))]"
              }
            }
          }
        }
      },
      "runAfter": {
        "getArticles": [
          "Succeeded"
        ]
      }
    }
  }
}
```

<span data-ttu-id="047f7-127">Nesse caso, primeiro obtemos uma lista de artigos.</span><span class="sxs-lookup"><span data-stu-id="047f7-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="047f7-128">Com base na categoria que foi definida como um parâmetro, a segunda etapa usa um mapa para pesquisar a URL e obter o conteúdo.</span><span class="sxs-lookup"><span data-stu-id="047f7-128">Based on the category that was defined as a parameter, the second step uses a map to look up the URL for getting the content.</span></span>

<span data-ttu-id="047f7-129">Alguns itens a serem observados:</span><span class="sxs-lookup"><span data-stu-id="047f7-129">Some times to note here:</span></span> 

*   <span data-ttu-id="047f7-130">A função [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) verifica se a categoria corresponde a uma das categorias definidas conhecidas.</span><span class="sxs-lookup"><span data-stu-id="047f7-130">The [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether the category matches one of the known defined categories.</span></span>

*   <span data-ttu-id="047f7-131">Depois que obtemos a categoria, podemos extrair o item do mapa usando colchetes: `parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="047f7-131">After we get the category, we can pull the item from the map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="047f7-132">Cadeias de caracteres de processo</span><span class="sxs-lookup"><span data-stu-id="047f7-132">Process strings</span></span>

<span data-ttu-id="047f7-133">Você pode usar várias funções para manipular cadeias de caracteres.</span><span class="sxs-lookup"><span data-stu-id="047f7-133">You can use various functions to manipulate strings.</span></span> <span data-ttu-id="047f7-134">Por exemplo, suponha que haja uma cadeia de caracteres que queremos passar para um sistema, mas não temos certeza sobre a manipulação adequada da codificação de caracteres.</span><span class="sxs-lookup"><span data-stu-id="047f7-134">For example, suppose we have a string that we want to pass to a system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="047f7-135">Uma opção é para codificar essa cadeia de caracteres em formato base64.</span><span class="sxs-lookup"><span data-stu-id="047f7-135">One option is to base64 encode this string.</span></span> <span data-ttu-id="047f7-136">No entanto, para evitar o uso de caracteres de escape em uma URL, vamos substituir alguns caracteres.</span><span class="sxs-lookup"><span data-stu-id="047f7-136">However, to avoid escaping in a URL, we are going to replace a few characters.</span></span> 

<span data-ttu-id="047f7-137">Também queremos uma subcadeia de caracteres do nome do autor da ordem, porque os cinco primeiros caracteres não são usados.</span><span class="sxs-lookup"><span data-stu-id="047f7-137">We also want a substring of the order's name because the first five characters are not used.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1",
        "orderer": "NAME=Contoso"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{replace(replace(base64(substring(parameters('order').orderer,5,sub(length(parameters('order').orderer), 5) )),'+','-') ,'/' ,'_' )}"
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="047f7-138">Trabalhando de dentro para fora:</span><span class="sxs-lookup"><span data-stu-id="047f7-138">Working from inside to outside:</span></span>

1. <span data-ttu-id="047f7-139">Obtenha o [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) para o nome do autor da ordem, para obtermos de volta o número total de caracteres.</span><span class="sxs-lookup"><span data-stu-id="047f7-139">Get the [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for the orderer's name, so we get back the total number of characters.</span></span>

2. <span data-ttu-id="047f7-140">Subtrair 5 porque desejamos uma cadeia de caracteres mais curta.</span><span class="sxs-lookup"><span data-stu-id="047f7-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="047f7-141">Na verdade, colete o [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="047f7-141">Actually, take the [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="047f7-142">Vamos começar no `5` do índice e seguir pelo restante da cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="047f7-142">We start at index `5` and go the remainder of the string.</span></span>

4. <span data-ttu-id="047f7-143">Converter esta subcadeia de caracteres em uma cadeia de caracteres [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64).</span><span class="sxs-lookup"><span data-stu-id="047f7-143">Convert this substring to a [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="047f7-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) todos os `+` caracteres com `-` caracteres.</span><span class="sxs-lookup"><span data-stu-id="047f7-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="047f7-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) todos os `/` caracteres com `_` caracteres.</span><span class="sxs-lookup"><span data-stu-id="047f7-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all the `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="047f7-146">Trabalhar com datas e horas</span><span class="sxs-lookup"><span data-stu-id="047f7-146">Work with Date Times</span></span>

<span data-ttu-id="047f7-147">Valores de Data/Hora podem ser úteis, especialmente quando você estiver tentando extrair dados de uma fonte de dados na qual, naturalmente, não há suporte para *gatilhos*.</span><span class="sxs-lookup"><span data-stu-id="047f7-147">Date Times can be useful, particularly when you are trying to pull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="047f7-148">Você também pode usar Datas e Horas para saber o tempo que as diversas etapas estão levando.</span><span class="sxs-lookup"><span data-stu-id="047f7-148">You can also use Date Times for finding how long various steps are taking.</span></span>

```
{
  "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
  "contentVersion": "1.0.0.0",
  "parameters": {
    "order": {
      "defaultValue": {
        "quantity": 10,
        "id": "myorder1"
      },
      "type": "Object"
    }
  },
  "triggers": {
    "Request": {
      "type": "request",
      "kind": "http"
    }
  },
  "actions": {
    "order": {
      "type": "Http",
      "inputs": {
        "method": "GET",
        "uri": "http://www.example.com/?id=@{parameters('order').id}"
      }
    },
    "ifTimingWarning": {
      "type": "If",
      "expression": "@less(actions('order').startTime,addseconds(utcNow(),-1))",
      "actions": {
        "timingWarning": {
          "type": "Http",
          "inputs": {
            "method": "GET",
            "uri": "http://www.example.com/?recordLongOrderTime=@{parameters('order').id}&currentTime=@{utcNow('r')}"
          }
        }
      },
      "runAfter": {
        "order": [
          "Succeeded"
        ]
      }
    }
  },
  "outputs": {}
}
```

<span data-ttu-id="047f7-149">Neste exemplo, extraímos `startTime` da etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="047f7-149">In this example, we extract the `startTime` from the previous step.</span></span> <span data-ttu-id="047f7-150">Em seguida, obtemos a hora atual e subtraímos um segundo:</span><span class="sxs-lookup"><span data-stu-id="047f7-150">Then we get the current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="047f7-151">Você pode usar outras unidades de tempo, como `minutes` ou `hours`.</span><span class="sxs-lookup"><span data-stu-id="047f7-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="047f7-152">Por fim, podemos comparar esses dois valores.</span><span class="sxs-lookup"><span data-stu-id="047f7-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="047f7-153">Se o primeiro valor for menor que o segundo valor, mais de um segundo terá decorrido desde o primeiro pedido.</span><span class="sxs-lookup"><span data-stu-id="047f7-153">If the first value is less than the second value, then more than one second has passed since the order was first placed.</span></span>

<span data-ttu-id="047f7-154">Para formatar datas, podemos usar formatadores de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="047f7-154">To format dates, we can use string formatters.</span></span> <span data-ttu-id="047f7-155">Por exemplo, para obter RFC1123, usamos [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="047f7-155">For example, to get the RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="047f7-156">Para saber mais sobre a formatação de datas, confira [Linguagem de Definição de Fluxo de Trabalho](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="047f7-156">To learn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="047f7-157">Parâmetros de implantação para ambientes diferentes</span><span class="sxs-lookup"><span data-stu-id="047f7-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="047f7-158">Normalmente, os ciclos de vida de implantação têm um ambiente de desenvolvimento, um ambiente de preparo e um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="047f7-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="047f7-159">Por exemplo, você pode usar a mesma definição em todos esses ambientes, mas usar bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="047f7-159">For example, you might use the same definition in all these environments but use different databases.</span></span> <span data-ttu-id="047f7-160">Do mesmo modo, talvez você queira usar a mesma definição em regiões diferentes para alta disponibilidade, mas deseje que cada instância de Aplicativo lógico se comunique com o banco de dados dessa região.</span><span class="sxs-lookup"><span data-stu-id="047f7-160">Likewise, you might want to use the same definition across different regions for high availability but want each logic app instance to talk to that region's database.</span></span>
<span data-ttu-id="047f7-161">Esse cenário é diferente de obter parâmetros em *tempo de execução* em que, em vez disso, você deve usar a função `trigger()` do exemplo anterior.</span><span class="sxs-lookup"><span data-stu-id="047f7-161">This scenario differs from taking parameters at *runtime* where instead, you should use the `trigger()` function as in the previous example.</span></span>

<span data-ttu-id="047f7-162">Você pode começar com uma definição básica, como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="047f7-162">You can start with a basic definition like this example:</span></span>

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2016-06-01/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "uri": {
            "type": "string"
        }
    },
    "triggers": {
        "request": {
          "type": "request",
          "kind": "http"
        }
    },
    "actions": {
        "readData": {
            "type": "Http",
            "inputs": {
                "method": "GET",
                "uri": "@parameters('uri')"
            }
        }
    },
    "outputs": {}
}
```

<span data-ttu-id="047f7-163">Na verdadeira solicitação `PUT` para Aplicativos Lógicos, você pode fornecer o parâmetro `uri`.</span><span class="sxs-lookup"><span data-stu-id="047f7-163">In the actual `PUT` request for the logic apps, you can provide the parameter `uri`.</span></span> <span data-ttu-id="047f7-164">Como não existe mais um valor padrão, a carga do aplicativo lógico requer este parâmetro:</span><span class="sxs-lookup"><span data-stu-id="047f7-164">Because a default value no longer exists, the logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use the definition from above here
        },
        "parameters": {
            "connection": {
                "value": "https://my.connection.that.is.per.enviornment"
            }
        }
    },
    "location": "westus"
}
``` 

<span data-ttu-id="047f7-165">Em cada ambiente, você pode fornecer um valor diferente para o parâmetro `connection` .</span><span class="sxs-lookup"><span data-stu-id="047f7-165">In each environment, you can provide a different value for the `connection` parameter.</span></span> 

<span data-ttu-id="047f7-166">Para ver todas as opções disponíveis para criar e gerenciar aplicativos lógicos, confira a [documentação da API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="047f7-166">For all the options that you have for creating and managing logic apps, see the [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
