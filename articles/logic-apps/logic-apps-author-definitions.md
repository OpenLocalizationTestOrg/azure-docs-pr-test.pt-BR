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
# <a name="create-workflow-definitions-for-logic-apps-using-json"></a>Criar definições de fluxo de trabalho para aplicativos lógicos usando JSON

Você pode criar definições de fluxo de trabalho para [Aplicativos Lógicos do Azure](logic-apps-what-are-logic-apps.md) com linguagem JSON simples e declarativa. Se você ainda não fez isso, primeiro examine [como toocreate seu primeiro aplicativo lógica com lógica de aplicativo Designer](logic-apps-create-a-logic-app.md). Consulte também Olá [completo referência de linguagem de definição de fluxo de trabalho de saudação](http://aka.ms/logicappsdocs).

## <a name="repeat-steps-over-a-list"></a>Repetir etapas em uma lista

tooiterate por meio de uma matriz tem too10, 000 itens e executa uma ação para cada item, use Olá [foreach tipo](logic-apps-loops-and-scopes.md).

## <a name="handle-failures-if-something-goes-wrong"></a>Lidar com falhas se algo der errado

Normalmente, você deseja tooinclude um *etapa correção* — alguma lógica que executa *se e somente se* um ou mais de suas chamadas falharem. Este exemplo obtém dados de vários locais, mas se Olá chamada falhar, queremos tooPOST uma mensagem em algum lugar pode rastrear essa falha posteriormente:  

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

toospecify que `postToErrorMessageQueue` só será executado `readData` tem `Failed`, use Olá `runAfter` propriedade toospecify uma lista de valores possíveis, por exemplo, para que `runAfter` poderia ser `["Succeeded", "Failed"]`.

Por fim, porque este exemplo agora manipula erros hello, nós não marcar Olá executar como `Failed`. Como adicionamos etapa Olá para lidar com essa falha neste exemplo, Olá executar tem `Succeeded` Embora uma etapa `Failed`.

## <a name="execute-two-or-more-steps-in-parallel"></a>Executar duas ou mais etapas em paralelo

toorun várias ações em paralelo, Olá `runAfter` propriedade deve ser equivalente em tempo de execução. 

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

Neste exemplo, ambos `branch1` e `branch2` são definidos toorun após `readData`. Como resultado, ambas as ramificações são executadas em paralelo. saudação de carimbo de hora para ambas as ramificações é idêntico.

![Paralelo](media/logic-apps-author-definitions/parallel.png)

## <a name="join-two-parallel-branches"></a>Unir duas ramificações paralelas

Você pode unir duas ações definidas toorun em paralelo com a adição de itens toohello `runAfter` propriedade como no exemplo anterior de saudação.

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

## <a name="map-list-items-tooa-different-configuration"></a>Mapear configuração diferente da lista de itens tooa

Em seguida, vamos supor que queremos tooget conteúdo diferente com base no valor de saudação de uma propriedade. Podemos criar um mapa de valores toodestinations como um parâmetro:  

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

Nesse caso, primeiro obtemos uma lista de artigos. Segunda etapa de saudação com base na categoria de saudação que foi definida como um parâmetro, usa toolook um mapa Olá URL para obter conteúdo de saudação.

Algumas vezes toonote aqui: 

*   Olá [ `intersection()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#intersection) função verifica se categoria Olá corresponde a um dos Olá conhecido categorias definidas.

*   Depois de recebermos categoria Olá, é possível efetuar pull item de saudação do mapa de saudação usando colchetes:`parameters[...]`

## <a name="process-strings"></a>Cadeias de caracteres de processo

Você pode usar várias cadeias de caracteres de toomanipulate de funções. Por exemplo, suponha que temos uma cadeia de caracteres que desejamos toopass tooa sistema, mas não tem certeza sobre a manipulação adequada de codificação de caracteres. Uma opção é toobase64 codifique essa cadeia de caracteres. No entanto, tooavoid saída em uma URL, vamos tooreplace alguns caracteres. 

Também gostaríamos de subcadeia de caracteres do nome da ordem hello como primeiros cinco caracteres de saudação não são usados.

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

Trabalho de dentro de toooutside:

1. Obter Olá [ `length()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#length) nome do hello autor da ordem, portanto obtemos número total de saudação de caracteres.

2. Subtrair 5 porque desejamos uma cadeia de caracteres mais curta.

3. Na verdade, fazer Olá [ `substring()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#substring). Vamos começar no índice `5` e vá Olá restante da cadeia de caracteres de saudação.

4. Converter esta tooa subcadeia de caracteres [ `base64()` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#base64) cadeia de caracteres.

5. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)saudação de todos os `+` caracteres com `-` caracteres.

6. [`replace()`](https://msdn.microsoft.com/library/azure/mt643789.aspx#replace)saudação de todos os `/` caracteres com `_` caracteres.

## <a name="work-with-date-times"></a>Trabalhar com datas e horas

Datas podem ser úteis, especialmente quando você está tentando toopull dados de uma fonte de dados que não oferece suporte naturalmente *gatilhos*. Você também pode usar Datas e Horas para saber o tempo que as diversas etapas estão levando.

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

Neste exemplo, podemos extrair Olá `startTime` da etapa anterior hello. Em seguida, podemos obter Olá a hora atual e subtrair um segundo:

[`addseconds(..., -1)`](https://msdn.microsoft.com/library/azure/mt643789.aspx#addseconds) 

Você pode usar outras unidades de tempo, como `minutes` ou `hours`. Por fim, podemos comparar esses dois valores. Se o primeiro valor de saudação é menor que o valor de segundo hello, em seguida, mais de um segundo decorrido desde Olá primeiro pedido.

datas de tooformat, podemos usar formatadores de cadeia de caracteres. Por exemplo, tooget Olá RFC1123, usamos [ `utcnow('r')` ](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow). toolearn sobre a formatação de data, consulte [linguagem de definição de fluxo de trabalho](https://msdn.microsoft.com/library/azure/mt643789.aspx#utcnow).

## <a name="deployment-parameters-for-different-environments"></a>Parâmetros de implantação para ambientes diferentes

Normalmente, os ciclos de vida de implantação têm um ambiente de desenvolvimento, um ambiente de preparo e um ambiente de produção. Por exemplo, você pode usar Olá a mesma definição em todos esses ambientes, mas usar bancos de dados diferentes. Da mesma forma, você poderá toouse Olá a mesma definição em regiões diferentes para alta disponibilidade, mas deseja o banco de dados de cada lógica aplicativo instância tootalk toothat da região.
Neste cenário é diferente de pegar parâmetros em *tempo de execução* onde em vez disso, você deve usar Olá `trigger()` funcionar como no exemplo anterior de saudação.

Você pode começar com uma definição básica, como neste exemplo:

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

Em Olá real `PUT` solicitar para aplicativos de lógica de saudação, você pode fornecer o parâmetro hello `uri`. Como um valor padrão não existe, carga de aplicativo hello lógica requer esse parâmetro:

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

Em cada ambiente, você pode fornecer um valor diferente para Olá `connection` parâmetro. 

Para todos os hello opções que você tem para criar e gerenciar aplicativos lógicos, consulte Olá [documentação da API REST](https://msdn.microsoft.com/library/azure/mt643787.aspx). 
