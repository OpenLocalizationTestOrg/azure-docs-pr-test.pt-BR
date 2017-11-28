---
title: "fluxos de trabalho aaaDefine com JSON - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Como as definições de fluxo de trabalho toowrite em JSON para os aplicativos lógicos"
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
ms.openlocfilehash: 0d69d334ecee9c3e7f8684cfde68ef0e85280358
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a><span data-ttu-id="3ae73-103">Criar definições de fluxo de trabalho para aplicativos lógicos usando JSON</span><span class="sxs-lookup"><span data-stu-id="3ae73-103">Create workflow definitions for logic apps using JSON</span></span>

<span data-ttu-id="3ae73-104">Você pode criar definições de fluxo de trabalho para [Aplicativos Lógicos do Azure](logic-apps-what-are-logic-apps.md) com linguagem JSON simples e declarativa.</span><span class="sxs-lookup"><span data-stu-id="3ae73-104">You can create workflow definitions for [Azure Logic Apps](logic-apps-what-are-logic-apps.md) with simple, declarative JSON language.</span></span> <span data-ttu-id="3ae73-105">Se você ainda não fez isso, primeiro examine [como toocreate seu primeiro aplicativo lógica com lógica de aplicativo Designer](logic-apps-create-a-logic-app.md).</span><span class="sxs-lookup"><span data-stu-id="3ae73-105">If you haven't already, first review [how toocreate your first logic app with Logic App Designer](logic-apps-create-a-logic-app.md).</span></span> <span data-ttu-id="3ae73-106">Consulte também Olá [completo referência de linguagem de definição de fluxo de trabalho de saudação](http://aka.ms/logicappsdocs).</span><span class="sxs-lookup"><span data-stu-id="3ae73-106">Also, see hello [full reference for hello Workflow Definition Language](http://aka.ms/logicappsdocs).</span></span>

## <a name="repeat-steps-over-a-list"></a><span data-ttu-id="3ae73-107">Repetir etapas em uma lista</span><span class="sxs-lookup"><span data-stu-id="3ae73-107">Repeat steps over a list</span></span>

<span data-ttu-id="3ae73-108">tooiterate por meio de uma matriz tem too10, 000 itens e executa uma ação para cada item, use Olá [foreach tipo](logic-apps-loops-and-scopes.md).</span><span class="sxs-lookup"><span data-stu-id="3ae73-108">tooiterate through an array that has up too10,000 items and perform an action for each item, use hello [foreach type](logic-apps-loops-and-scopes.md).</span></span>

## <a name="handle-failures-if-something-goes-wrong"></a><span data-ttu-id="3ae73-109">Lidar com falhas se algo der errado</span><span class="sxs-lookup"><span data-stu-id="3ae73-109">Handle failures if something goes wrong</span></span>

<span data-ttu-id="3ae73-110">Normalmente, você deseja tooinclude um *etapa correção* — alguma lógica que executa *se e somente se* um ou mais de suas chamadas falharem.</span><span class="sxs-lookup"><span data-stu-id="3ae73-110">Usually, you want tooinclude a *remediation step* — some logic that executes *if and only if* one or more of your calls fail.</span></span> <span data-ttu-id="3ae73-111">Este exemplo obtém dados de vários locais, mas se Olá chamada falhar, queremos tooPOST uma mensagem em algum lugar pode rastrear essa falha posteriormente:</span><span class="sxs-lookup"><span data-stu-id="3ae73-111">This example gets data from various places, but if hello call fails, we want tooPOST a message somewhere so we can track down that failure later:</span></span>  

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

<span data-ttu-id="3ae73-112">toospecify que `postToErrorMessageQueue` só será executado `readData` tem `Failed`, use Olá `runAfter` propriedade toospecify uma lista de valores possíveis, por exemplo, para que `runAfter` poderia ser `["Succeeded", "Failed"]`.</span><span class="sxs-lookup"><span data-stu-id="3ae73-112">toospecify that `postToErrorMessageQueue` only runs after `readData` has `Failed`, use hello `runAfter` property, for example, toospecify a list of possible values, so that `runAfter` could be `["Succeeded", "Failed"]`.</span></span>

<span data-ttu-id="3ae73-113">Por fim, porque este exemplo agora manipula erros hello, nós não marcar Olá executar como `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3ae73-113">Finally, because this example now handles hello error, we no longer mark hello run as `Failed`.</span></span> <span data-ttu-id="3ae73-114">Como adicionamos etapa Olá para lidar com essa falha neste exemplo, Olá executar tem `Succeeded` Embora uma etapa `Failed`.</span><span class="sxs-lookup"><span data-stu-id="3ae73-114">Because we added hello step for handling this failure in this example, hello run has `Succeeded` although one step `Failed`.</span></span>

## <a name="execute-two-or-more-steps-in-parallel"></a><span data-ttu-id="3ae73-115">Executar duas ou mais etapas em paralelo</span><span class="sxs-lookup"><span data-stu-id="3ae73-115">Execute two or more steps in parallel</span></span>

<span data-ttu-id="3ae73-116">toorun várias ações em paralelo, Olá `runAfter` propriedade deve ser equivalente em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="3ae73-116">toorun multiple actions in parallel, hello `runAfter` property must be equivalent at runtime.</span></span> 

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

<span data-ttu-id="3ae73-117">Neste exemplo, ambos `branch1` e `branch2` são definidos toorun após `readData`.</span><span class="sxs-lookup"><span data-stu-id="3ae73-117">In this example, both `branch1` and `branch2` are set toorun after `readData`.</span></span> <span data-ttu-id="3ae73-118">Como resultado, ambas as ramificações são executadas em paralelo.</span><span class="sxs-lookup"><span data-stu-id="3ae73-118">As a result, both branches run in parallel.</span></span> <span data-ttu-id="3ae73-119">saudação de carimbo de hora para ambas as ramificações é idêntico.</span><span class="sxs-lookup"><span data-stu-id="3ae73-119">hello timestamp for both branches is identical.</span></span>

![Paralelo](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a><span data-ttu-id="3ae73-121">Unir duas ramificações paralelas</span><span class="sxs-lookup"><span data-stu-id="3ae73-121">Join two parallel branches</span></span>

<span data-ttu-id="3ae73-122">Você pode unir duas ações definidas toorun em paralelo com a adição de itens toohello `runAfter` propriedade como no exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ae73-122">You can join two actions that are set toorun in parallel by adding items toohello `runAfter` property as in hello previous example.</span></span>

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

## <a name="map-list-items-tooa-different-configuration"></a><span data-ttu-id="3ae73-124">Mapear configuração diferente da lista de itens tooa</span><span class="sxs-lookup"><span data-stu-id="3ae73-124">Map list items tooa different configuration</span></span>

<span data-ttu-id="3ae73-125">Em seguida, vamos supor que queremos tooget conteúdo diferente com base no valor de saudação de uma propriedade.</span><span class="sxs-lookup"><span data-stu-id="3ae73-125">Next, let's say that we want tooget different content based on hello value of a property.</span></span> <span data-ttu-id="3ae73-126">Podemos criar um mapa de valores toodestinations como um parâmetro:</span><span class="sxs-lookup"><span data-stu-id="3ae73-126">We can create a map of values toodestinations as a parameter:</span></span>  

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

<span data-ttu-id="3ae73-127">Nesse caso, primeiro obtemos uma lista de artigos.</span><span class="sxs-lookup"><span data-stu-id="3ae73-127">In this case, we first get a list of articles.</span></span> <span data-ttu-id="3ae73-128">Segunda etapa de saudação com base na categoria de saudação que foi definida como um parâmetro, usa toolook um mapa Olá URL para obter conteúdo de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ae73-128">Based on hello category that was defined as a parameter, hello second step uses a map toolook up hello URL for getting hello content.</span></span>

<span data-ttu-id="3ae73-129">Algumas vezes toonote aqui:</span><span class="sxs-lookup"><span data-stu-id="3ae73-129">Some times toonote here:</span></span> 

*   <span data-ttu-id="3ae73-130">Olá [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) função verifica se categoria Olá corresponde a um dos Olá conhecido categorias definidas.</span><span class="sxs-lookup"><span data-stu-id="3ae73-130">hello [`intersection()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) function checks whether hello category matches one of hello known defined categories.</span></span>

*   <span data-ttu-id="3ae73-131">Depois de recebermos categoria Olá, é possível efetuar pull item de saudação do mapa de saudação usando colchetes:`parameters[...]`</span><span class="sxs-lookup"><span data-stu-id="3ae73-131">After we get hello category, we can pull hello item from hello map using square brackets: `parameters[...]`</span></span>

## <a name="process-strings"></a><span data-ttu-id="3ae73-132">Cadeias de caracteres de processo</span><span class="sxs-lookup"><span data-stu-id="3ae73-132">Process strings</span></span>

<span data-ttu-id="3ae73-133">Você pode usar várias cadeias de caracteres de toomanipulate de funções.</span><span class="sxs-lookup"><span data-stu-id="3ae73-133">You can use various functions toomanipulate strings.</span></span> <span data-ttu-id="3ae73-134">Por exemplo, suponha que temos uma cadeia de caracteres que desejamos toopass tooa sistema, mas não tem certeza sobre a manipulação adequada de codificação de caracteres.</span><span class="sxs-lookup"><span data-stu-id="3ae73-134">For example, suppose we have a string that we want toopass tooa system, but we aren't confident about proper handling for character encoding.</span></span> <span data-ttu-id="3ae73-135">Uma opção é toobase64 codifique essa cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="3ae73-135">One option is toobase64 encode this string.</span></span> <span data-ttu-id="3ae73-136">No entanto, tooavoid saída em uma URL, vamos tooreplace alguns caracteres.</span><span class="sxs-lookup"><span data-stu-id="3ae73-136">However, tooavoid escaping in a URL, we are going tooreplace a few characters.</span></span> 

<span data-ttu-id="3ae73-137">Também gostaríamos de subcadeia de caracteres do nome da ordem hello como primeiros cinco caracteres de saudação não são usados.</span><span class="sxs-lookup"><span data-stu-id="3ae73-137">We also want a substring of hello order's name because hello first five characters are not used.</span></span>

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

<span data-ttu-id="3ae73-138">Trabalho de dentro de toooutside:</span><span class="sxs-lookup"><span data-stu-id="3ae73-138">Working from inside toooutside:</span></span>

1. <span data-ttu-id="3ae73-139">Obter Olá [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) nome do hello autor da ordem, portanto obtemos número total de saudação de caracteres.</span><span class="sxs-lookup"><span data-stu-id="3ae73-139">Get hello [`length()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) for hello orderer's name, so we get back hello total number of characters.</span></span>

2. <span data-ttu-id="3ae73-140">Subtrair 5 porque desejamos uma cadeia de caracteres mais curta.</span><span class="sxs-lookup"><span data-stu-id="3ae73-140">Subtract 5 because we want a shorter string.</span></span>

3. <span data-ttu-id="3ae73-141">Na verdade, fazer Olá [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span><span class="sxs-lookup"><span data-stu-id="3ae73-141">Actually, take hello [`substring()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring).</span></span> <span data-ttu-id="3ae73-142">Vamos começar no índice `5` e vá Olá restante da cadeia de caracteres de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ae73-142">We start at index `5` and go hello remainder of hello string.</span></span>

4. <span data-ttu-id="3ae73-143">Converter esta tooa subcadeia de caracteres [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="3ae73-143">Convert this substring tooa [`base64()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) string.</span></span>

5. <span data-ttu-id="3ae73-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)saudação de todos os `+` caracteres com `-` caracteres.</span><span class="sxs-lookup"><span data-stu-id="3ae73-144">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `+` characters with `-` characters.</span></span>

6. <span data-ttu-id="3ae73-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)saudação de todos os `/` caracteres com `_` caracteres.</span><span class="sxs-lookup"><span data-stu-id="3ae73-145">[`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace) all hello `/` characters with `_` characters.</span></span>

## <a name="work-with-date-times"></a><span data-ttu-id="3ae73-146">Trabalhar com datas e horas</span><span class="sxs-lookup"><span data-stu-id="3ae73-146">Work with Date Times</span></span>

<span data-ttu-id="3ae73-147">Datas podem ser úteis, especialmente quando você está tentando toopull dados de uma fonte de dados que não oferece suporte naturalmente *gatilhos*.</span><span class="sxs-lookup"><span data-stu-id="3ae73-147">Date Times can be useful, particularly when you are trying toopull data from a data source that doesn't naturally support *triggers*.</span></span> <span data-ttu-id="3ae73-148">Você também pode usar Datas e Horas para saber o tempo que as diversas etapas estão levando.</span><span class="sxs-lookup"><span data-stu-id="3ae73-148">You can also use Date Times for finding how long various steps are taking.</span></span>

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

<span data-ttu-id="3ae73-149">Neste exemplo, podemos extrair Olá `startTime` da etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="3ae73-149">In this example, we extract hello `startTime` from hello previous step.</span></span> <span data-ttu-id="3ae73-150">Em seguida, podemos obter Olá a hora atual e subtrair um segundo:</span><span class="sxs-lookup"><span data-stu-id="3ae73-150">Then we get hello current time, and subtract one second:</span></span>

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

<span data-ttu-id="3ae73-151">Você pode usar outras unidades de tempo, como `minutes` ou `hours`.</span><span class="sxs-lookup"><span data-stu-id="3ae73-151">You can use other units of time, like `minutes` or `hours`.</span></span> <span data-ttu-id="3ae73-152">Por fim, podemos comparar esses dois valores.</span><span class="sxs-lookup"><span data-stu-id="3ae73-152">Finally, we can compare these two values.</span></span> <span data-ttu-id="3ae73-153">Se o primeiro valor de saudação é menor que o valor de segundo hello, em seguida, mais de um segundo decorrido desde Olá primeiro pedido.</span><span class="sxs-lookup"><span data-stu-id="3ae73-153">If hello first value is less than hello second value, then more than one second has passed since hello order was first placed.</span></span>

<span data-ttu-id="3ae73-154">datas de tooformat, podemos usar formatadores de cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="3ae73-154">tooformat dates, we can use string formatters.</span></span> <span data-ttu-id="3ae73-155">Por exemplo, tooget Olá RFC1123, usamos [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="3ae73-155">For example, tooget hello RFC1123, we use [`utcnow('r')`](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span> <span data-ttu-id="3ae73-156">toolearn sobre a formatação de data, consulte [linguagem de definição de fluxo de trabalho](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span><span class="sxs-lookup"><span data-stu-id="3ae73-156">toolearn about date formatting, see [Workflow Definition Language](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).</span></span>

## <a name="deployment-parameters-for-different-environments"></a><span data-ttu-id="3ae73-157">Parâmetros de implantação para ambientes diferentes</span><span class="sxs-lookup"><span data-stu-id="3ae73-157">Deployment parameters for different environments</span></span>

<span data-ttu-id="3ae73-158">Normalmente, os ciclos de vida de implantação têm um ambiente de desenvolvimento, um ambiente de preparo e um ambiente de produção.</span><span class="sxs-lookup"><span data-stu-id="3ae73-158">Commonly, deployment lifecycles have a development environment, a staging environment, and a production environment.</span></span> <span data-ttu-id="3ae73-159">Por exemplo, você pode usar Olá a mesma definição em todos esses ambientes, mas usar bancos de dados diferentes.</span><span class="sxs-lookup"><span data-stu-id="3ae73-159">For example, you might use hello same definition in all these environments but use different databases.</span></span> <span data-ttu-id="3ae73-160">Da mesma forma, você poderá toouse Olá a mesma definição em regiões diferentes para alta disponibilidade, mas deseja o banco de dados de cada lógica aplicativo instância tootalk toothat da região.</span><span class="sxs-lookup"><span data-stu-id="3ae73-160">Likewise, you might want toouse hello same definition across different regions for high availability but want each logic app instance tootalk toothat region's database.</span></span>
<span data-ttu-id="3ae73-161">Neste cenário é diferente de pegar parâmetros em *tempo de execução* onde em vez disso, você deve usar Olá `trigger()` funcionar como no exemplo anterior de saudação.</span><span class="sxs-lookup"><span data-stu-id="3ae73-161">This scenario differs from taking parameters at *runtime* where instead, you should use hello `trigger()` function as in hello previous example.</span></span>

<span data-ttu-id="3ae73-162">Você pode começar com uma definição básica, como neste exemplo:</span><span class="sxs-lookup"><span data-stu-id="3ae73-162">You can start with a basic definition like this example:</span></span>

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

<span data-ttu-id="3ae73-163">Em Olá real `PUT` solicitar para aplicativos de lógica de saudação, você pode fornecer o parâmetro hello `uri`.</span><span class="sxs-lookup"><span data-stu-id="3ae73-163">In hello actual `PUT` request for hello logic apps, you can provide hello parameter `uri`.</span></span> <span data-ttu-id="3ae73-164">Como um valor padrão não existe, carga de aplicativo hello lógica requer esse parâmetro:</span><span class="sxs-lookup"><span data-stu-id="3ae73-164">Because a default value no longer exists, hello logic app payload requires this parameter:</span></span>

```
{
    "properties": {},
        "definition": {
          // Use hello definition from above here
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

<span data-ttu-id="3ae73-165">Em cada ambiente, você pode fornecer um valor diferente para Olá `connection` parâmetro.</span><span class="sxs-lookup"><span data-stu-id="3ae73-165">In each environment, you can provide a different value for hello `connection` parameter.</span></span> 

<span data-ttu-id="3ae73-166">Para todos os hello opções que você tem para criar e gerenciar aplicativos lógicos, consulte Olá [documentação da API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span><span class="sxs-lookup"><span data-stu-id="3ae73-166">For all hello options that you have for creating and managing logic apps, see hello [REST API documentation](https://msdn.microsoft.com/library/azure/mt643787.aspx).</span></span> 
