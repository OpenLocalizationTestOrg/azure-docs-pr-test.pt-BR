---
title: "aaaSchema atualizações 1 de agosto de 2015 preview - os aplicativos lógicos do Azure | Microsoft Docs"
description: "Criar definições de JSON para Aplicativos Lógicos do Azure com a versão de esquema 2015-08-01-preview"
author: stepsic-microsoft-com
manager: anneta
editor: 
services: logic-apps
documentationcenter: 
ms.assetid: 0d03a4d4-e8a8-4c81-aed5-bfd2a28c7f0c
ms.service: logic-apps
ms.workload: integration
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.custom: H1Hack27Feb2017
ms.date: 05/31/2016
ms.author: LADocs; stepsic
ms.openlocfilehash: 950cd18a27aa1859c4f0b6116de3fb8699d746c4
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a>Atualizações de esquema para Aplicativos Lógicos do Azure - visualização de 1º de junho de 2015

Esse novo esquema e a API de versão para os aplicativos lógicos do Azure inclui aprimoramentos importantes que tornam os aplicativos lógicos mais toouse mais fácil e confiável:

*   Olá **APIApp** tipo de ação é atualizada tooa novo [ **APIConnection** ](#api-connections) tipo de ação.
*   **Repita** é renomeado muito[**Foreach**](#foreach).
*   Olá [ **ouvinte HTTP** API App](#http-listener) não é mais necessário.
*   A ação de chamar fluxos de trabalho secundários usa um [novo esquema](#child-workflows).

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a>Mover tooAPI conexões

Olá maior alteração é que você não tem mais toodeploy aplicativos de API em sua assinatura do Azure, você pode usar as APIs. Aqui estão Olá maneiras que você pode usar APIs:

* APIs gerenciadas
* Suas APIs Web personalizadas

Cada modo é tratado de forma ligeiramente diferente, pois seu gerenciamento e modelos de hospedagem são diferentes. Uma vantagem desse modelo é que você não está restrita tooresources que são implantados no seu grupo de recursos do Azure. 

### <a name="managed-apis"></a>APIs gerenciadas

A Microsoft gerencia algumas APIs em seu nome, por exemplo o Office 365, Salesforce, Twitter e FTP. Algumas dessas APIs gerenciadas como o Bing Translate podem ser usadas como estão, enquanto outras exigem configuração. Essa configuração é denominada *conexão*.

Por exemplo, quando você usa o Office 365, deve criar uma conexão que contém o token de entrada do Office 365. Esse token é armazenado e atualizado para que seu aplicativo lógico sempre possa chamar hello API do Office 365 com segurança. Como alternativa, se desejar que o servidor SQL ou FTP tooyour tooconnect, você deve criar uma conexão com a cadeia de caracteres de conexão de saudação. 

Nessa definição, essas ações são denominadas `APIConnection`. Aqui está um exemplo de uma conexão que chama o Office 365 toosend um email:

```
{
    "actions": {
        "Send_Email": {
            "type": "ApiConnection",
            "inputs": {
                "host": {
                    "api": {
                        "runtimeUrl": "https://msmanaged-na.azure-apim.net/apim/office365"
                    },
                    "connection": {
                        "name": "@parameters('$connections')['shared_office365']['connectionId']"
                    }
                },
                "method": "post",
                "body": {
                    "Subject": "Reminder",
                    "Body": "Don't forget!",
                    "To": "me@contoso.com"
                },
                "path": "/Mail"
            }
        }
    }
}
```

Olá `host` objeto é parte de entradas conexões tooAPI exclusivo, e contém dois partes: `api` e `connection`.

Olá `api` tem tempo de execução de saudação URL de onde que API não gerenciada está hospedado. Você pode ver todos os Olá disponíveis APIs gerenciadas chamando `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.

Quando você usa uma API, Olá API poderá ou não ter qualquer *parâmetros de conexão* definido. Se não Olá API, nenhum *conexão* é necessária. Se Olá API, você deve criar uma conexão. conexão Olá criado tem o nome de saudação que você escolher. Você fazer referência a nome de saudação em hello `connection` objeto dentro de saudação `host` objeto. uma conexão em um grupo de recursos, chamada de toocreate:

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

Com hello corpo a seguir:

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{hello name of hello storage account -- hello set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a>Implantar APIs gerenciadas em um modelo do Azure Resource Manager

Você pode criar um aplicativo completo em um modelo do Azure Resource Manager, desde que ele não exija entrada interativa.
Se a entrada é necessária, você pode configurar tudo com o modelo do Azure Resource Manager hello, mas você ainda possui toovisit Olá tooauthorize portal Olá conexões. 

```
    "resources": [{
        "apiVersion": "2015-08-01-preview",
        "name": "azureblob",
        "type": "Microsoft.Web/connections",
        "location": "[resourceGroup().location]",
        "properties": {
            "api": {
                "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
            },
            "parameterValues": {
                "accountName": "[parameters('storageAccountName')]",
                "accessKey": "[parameters('storageAccountKey')]"
            }
        }
    }, {
        "type": "Microsoft.Logic/workflows",
        "apiVersion": "2015-08-01-preview",
        "name": "[parameters('logicAppName')]",
        "location": "[resourceGroup().location]",
        "dependsOn": ["[resourceId('Microsoft.Web/connections', 'azureblob')]"
        ],
        "properties": {
            "sku": {
                "name": "[parameters('sku')]",
                "plan": {
                    "id": "[concat(resourceGroup().id, '/providers/Microsoft.Web/serverfarms/',parameters('svcPlanName'))]"
                }
            },
            "definition": {
                "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2015-08-01-preview/workflowdefinition.json#",
                "actions": {
                    "Create_file": {
                        "type": "apiconnection",
                        "inputs": {
                            "host": {
                                "api": {
                                    "runtimeUrl": "https://logic-apis-westus.azure-apim.net/apim/azureblob"
                                },
                                "connection": {
                                    "name": "@parameters('$connections')['azureblob']['connectionId']"
                                }
                            },
                            "method": "post",
                            "queries": {
                                "folderPath": "[concat('/', parameters('containerName'))]",
                                "name": "helloworld.txt"
                            },
                            "body": "@decodeDataUri('data:, Hello+world!')",
                            "path": "/datasets/default/files"
                        },
                        "conditions": []
                    }
                },
                "contentVersion": "1.0.0.0",
                "outputs": {},
                "parameters": {
                    "$connections": {
                        "defaultValue": {},
                        "type": "Object"
                    }
                },
                "triggers": {
                    "recurrence": {
                        "type": "Recurrence",
                        "recurrence": {
                            "frequency": "Day",
                            "interval": 1
                        }
                    }
                }
            },
            "parameters": {
                "$connections": {
                    "value": {
                        "azureblob": {
                            "connectionId": "[concat(resourceGroup().id,'/providers/Microsoft.Web/connections/azureblob')]",
                            "connectionName": "azureblob",
                            "id": "[concat(subscription().id,'/providers/Microsoft.Web/locations/westus/managedApis/azureblob')]"
                        }

                    }
                }
            }
        }
    }]
```

Você pode ver neste exemplo conexões Olá são apenas recursos que moram em seu grupo de recursos. Eles fazem referência tooyou disponível de APIs de Olá gerenciado na sua assinatura.

### <a name="your-custom-web-apis"></a>Suas APIs Web personalizadas

Se você usar suas próprias APIs, aqueles não gerenciados pela Microsoft, use internas Olá **HTTP** ação toocall-los. Para uma experiência ideal, você deve expor um ponto de extremidade do Swagger para sua API. Esse ponto de extremidade permite que entradas de Olá Olá lógica aplicativo Designer toorender e saídas para a sua API. Sem Swagger, designer de saudação só pode mostrar Olá entradas e saídas como objetos JSON opacos.

Aqui está uma saudação de mostrando exemplo novo `metadata.apiDefinitionUrl` propriedade:

```
{
   "actions": {
        "mycustomAPI": {
            "type": "http",
            "metadata": {
              "apiDefinitionUrl": "https://mysite.azurewebsites.net/api/apidef/"  
            },
            "inputs": {
                "uri": "https://mysite.azurewebsites.net/api/getsomedata",
                "method": "GET"
            }
        }
    }
}
```

Se você hospedar sua API da Web no serviço de aplicativo do Azure, a API da Web é automaticamente aparece na lista de saudação de ações disponíveis no designer de saudação. Caso contrário, o que toopaste diretamente na URL de saudação. ponto de extremidade de Swagger Olá deve ser não autenticado toobe utilizável em Olá Designer de lógica do aplicativo, embora você pode proteger a saudação própria API com qualquer métodos que oferece suporte a Swagger.

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a>Chamar aplicativos de API implantados com 2015-08-01-preview

Se você tiver implantado uma API App, você pode chamar o aplicativo hello com hello **HTTP** ação.

Por exemplo, se você usar arquivos de toolist Dropbox, seu **2014-12-01-preview** definição de versão de esquema pode encontrar algo como:

```
{
    "$schema": "https://schema.management.azure.com/providers/Microsoft.Logic/schemas/2014-12-01-preview/workflowdefinition.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token": {
            "defaultValue": "eyJ0eX...wCn90",
            "type": "String",
            "metadata": {
                "token": {
                    "name": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token"
                }
            }
        }
    },
    "actions": {
        "dropboxconnector": {
            "type": "ApiApp",
            "inputs": {
                "apiVersion": "2015-01-14",
                "host": {
                    "id": "/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector",
                    "gateway": "https://avdemo.azurewebsites.net"
                },
                "operation": "ListFiles",
                "parameters": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

Você pode construir a ação de HTTP equivalente hello como neste exemplo, enquanto a seção parâmetros Olá Olá definição de lógica de aplicativo permanece inalterada:

```
{
    "actions": {
        "dropboxconnector": {
            "type": "Http",
            "metadata": {
              "apiDefinitionUrl": "https://avdemo.azurewebsites.net/api/service/apidef/dropboxconnector/?api-version=2015-01-14&format=swagger-2.0-standard"  
            },
            "inputs": {
                "uri": "https://avdemo.azurewebsites.net/api/service/invoke/dropboxconnector/ListFiles?api-version=2015-01-14",
                "method": "POST",
                "body": {
                    "FolderPath": "/myfolder"
                },
                "authentication": {
                    "type": "Raw",
                    "scheme": "Zumo",
                    "parameter": "@parameters('/subscriptions/423db32d-...-b59f14c962f1/resourcegroups/avdemo/providers/Microsoft.AppService/apiapps/dropboxconnector/token')"
                }
            }
        }
    }
}
```

Percorra essas propriedades, uma por vez:

| Propriedade da ação | Descrição |
| --- | --- |
| `type` |`Http` em vez de `APIapp` |
| `metadata.apiDefinitionUrl` |toouse esta ação na Olá lógica de aplicativo Designer, incluem hello metadados ponto de extremidade, que é construído a partir de:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard` |
| `inputs.uri` |Construído com base em: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14` |
| `inputs.method` |Sempre `POST` |
| `inputs.body` |Parâmetros do aplicativo toohello idênticos API |
| `inputs.authentication` |Toohello idêntico autenticação API App |

Essa abordagem deve funcionar para todas as ações de Aplicativo de API. No entanto, lembre-se de que esses aplicativos de API anterior não têm mais suporte. Portanto você deve mover tooone de saudação duas outras opções anteriores, uma API gerenciada ou hospedando sua API da Web personalizado.

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a>Renomeado 'Repetir' too'foreach'

Para a versão de esquema anterior hello, recebemos muito comentários dos clientes que **Repita** foi confuso e não capturar corretamente que **Repita** foi realmente um loop for each. Como resultado, podemos renomeou `repeat` muito`foreach`. Por exemplo, anteriormente você escreveria:

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "repeat": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{repeatItem()}"
            }
        }
    }
}
```

Agora você escreveria:

```
{
    "actions": {
        "pingBing": {
            "type": "Http",
            "foreach": "@range(0,2)",
            "inputs": {
                "method": "GET",
                "uri": "https://www.bing.com/search?q=@{item()}"
            }
        }
    }
}
```

Olá função `@repeatItem()` foi item atual do hello tooreference usadas anteriormente que está sendo iterado. Essa função foi simplificada muito`@item()`. 

### <a name="reference-outputs-from-foreach"></a>Saídas de referência de 'foreach'

Para simplificar, Olá saídas de `foreach` ações não são encapsuladas em um objeto chamado `repeatItems`. Enquanto Olá saídas de saudação anterior `repeat` exemplo foram:

```
{
    "repeatItems": [
        {
            "name": "pingBing",
            "inputs": {
                "uri": "https://www.bing.com/search?q=0",
                "method": "GET"
            },
            "outputs": {
                "headers": { },
                "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
            }
            "status": "Succeeded"
        }
    ]
}
```

Agora, essas saídas são:

```
[
    {
        "name": "pingBing",
        "inputs": {
            "uri": "https://www.bing.com/search?q=0",
            "method": "GET"
        },
        "outputs": {
            "headers": { },
            "body": "<!DOCTYPE html><html lang=\"en\" xml:lang=\"en\" xmlns=\"http://www.w3.org/1999/xhtml\" xmlns:Web=\"http://schemas.live.com/Web/\">...</html>"
        }
        "status": "Succeeded"
    }
]
```

Anteriormente, tooget toohello corpo de ação de saudação ao fazer referência a essas saídas:

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "repeat": "@outputs('pingBing').repeatItems",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@repeatItem().outputs.body"
            }
        }
    }
}
```

Agora você pode fazer:

```
{
    "actions": {
        "secondAction": {
            "type": "Http",
            "foreach": "@outputs('pingBing')",
            "inputs": {
                "method": "POST",
                "uri": "http://www.example.com",
                "body": "@item().outputs.body"
            }
        }
    }
}
```

Com essas alterações, Olá funções `@repeatItem()`, `@repeatBody()`, e `@repeatOutputs()` são removidos.

<a name="http-listener"></a>
## <a name="native-http-listener"></a>Ouvinte HTTP nativo:

Olá ouvinte HTTP recursos agora são incorporados no. Portanto, você não precisa toodeploy um aplicativo de API do ouvinte HTTP. Consulte [Olá detalhes completos sobre como toomake seu aqui pode ser chamado de ponto de extremidade de aplicativo lógica](../logic-apps/logic-apps-http-endpoint.md). 

Com essas alterações, removemos Olá `@accessKeys()` função, que são substituídos pelo Olá `@listCallbackURL()` função para obter o ponto de extremidade hello quando necessário. Além disso, agora você deve definir pelo menos um gatilho em seu aplicativo lógico. Se você quiser muito`/run` Olá fluxo de trabalho, você deve ter uma esses disparadores: `manual`, `apiConnectionWebhook`, ou `httpWebhook`.

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a>Chamar fluxos de trabalho secundários

Anteriormente, chamar fluxos de trabalho filho necessário passar o fluxo de trabalho toohello, obter token de acesso de saudação e colando Olá token na definição de aplicativo de lógica de saudação onde você deseja toocall fluxo de trabalho filho. Com o novo esquema de hello, mecanismo gera automaticamente um SAS em tempo de execução para os aplicativos lógicos Olá Olá fluxo de trabalho filho para que você não tem muito colar informações secretas na definição de saudação. Aqui está um exemplo:

```
"mynestedwf": {
    "type": "workflow",
    "inputs": {
        "host": {
            "id": "/subscriptions/xxxxyyyyzzz/resourceGroups/rg001/providers/Microsoft.Logic/mywf001",
            "triggerName": "myendpointtrigger"
        },
        "queries": {
            "extrafield": "specialValue"
        },
        "headers": {
            "x-ms-date": "@utcnow()",
            "Content-type": "application/json"
        },
        "body": {
            "contentFieldOne": "value100",
            "anotherField": 10.001
        }
    },
    "conditions": []
}
```

Uma melhoria de segundo é que nós estamos fornecendo filho Olá a solicitação de entrada do toohello de acesso total de fluxos de trabalho. Isso significa que você pode passar parâmetros de saudação *consultas* seção e em Olá *cabeçalhos* objeto e que você pode definir totalmente Olá corpo inteiro.

Por fim, há as alterações necessárias toohello filho fluxo de trabalho. Enquanto você poderia chamar anteriormente um fluxo de trabalho filho diretamente, agora você deve definir um ponto de extremidade do disparador no fluxo de trabalho Olá para Olá pai toocall. Em geral, você adicionaria um gatilho que tenha `manual` digite e, em seguida, usar esse gatilho na definição do pai de saudação. Saudação de Observação `host` propriedade especificamente tem um `triggerName` porque você sempre deve especificar o gatilho está chamando.

## <a name="other-changes"></a>Outras alterações

### <a name="new-queries-property"></a>Nova propriedade ‘queries’

Todos os tipos de ação oferecem suporte a uma nova entrada denominada `queries`. Essa entrada pode ser um objeto estruturado, em vez de ter a cadeia de caracteres de saudação tooassemble manualmente.

### <a name="renamed-parse-function-toojson"></a>Renomeado too'json() de função 'Parse' '

Estamos adicionando tipos de conteúdo mais rápido, para que tenhamos renomeado Olá `parse()` função muito`json()`.

## <a name="coming-soon-enterprise-integration-apis"></a>Em breve: APIs de Integração Corporativa

Não temos versões gerenciadas ainda do hello APIs de integração do Enterprise, como AS2. Enquanto isso, você pode usar seu APIs existentes do BizTalk implantados por meio de saudação ação HTTP. Para obter detalhes, consulte "Usando seus aplicativos de API já implantados" em Olá [roteiro de integração](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/). 
