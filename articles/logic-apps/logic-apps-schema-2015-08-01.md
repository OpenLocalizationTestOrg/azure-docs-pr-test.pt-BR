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
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="ec1f5-103">Atualizações de esquema para Aplicativos Lógicos do Azure - visualização de 1º de junho de 2015</span><span class="sxs-lookup"><span data-stu-id="ec1f5-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="ec1f5-104">Esse novo esquema e a API de versão para os aplicativos lógicos do Azure inclui aprimoramentos importantes que tornam os aplicativos lógicos mais toouse mais fácil e confiável:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier toouse:</span></span>

*   <span data-ttu-id="ec1f5-105">Olá **APIApp** tipo de ação é atualizada tooa novo [ **APIConnection** ](#api-connections) tipo de ação.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-105">hello **APIApp** action type is updated tooa new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="ec1f5-106">**Repita** é renomeado muito[**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="ec1f5-106">**Repeat** is renamed too[**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="ec1f5-107">Olá [ **ouvinte HTTP** API App](#http-listener) não é mais necessário.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-107">hello [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="ec1f5-108">A ação de chamar fluxos de trabalho secundários usa um [novo esquema](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="ec1f5-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-tooapi-connections"></a><span data-ttu-id="ec1f5-109">Mover tooAPI conexões</span><span class="sxs-lookup"><span data-stu-id="ec1f5-109">Move tooAPI connections</span></span>

<span data-ttu-id="ec1f5-110">Olá maior alteração é que você não tem mais toodeploy aplicativos de API em sua assinatura do Azure, você pode usar as APIs.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-110">hello biggest change is that you no longer have toodeploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="ec1f5-111">Aqui estão Olá maneiras que você pode usar APIs:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-111">Here are hello ways that you can use APIs:</span></span>

* <span data-ttu-id="ec1f5-112">APIs gerenciadas</span><span class="sxs-lookup"><span data-stu-id="ec1f5-112">Managed APIs</span></span>
* <span data-ttu-id="ec1f5-113">Suas APIs Web personalizadas</span><span class="sxs-lookup"><span data-stu-id="ec1f5-113">Your custom Web APIs</span></span>

<span data-ttu-id="ec1f5-114">Cada modo é tratado de forma ligeiramente diferente, pois seu gerenciamento e modelos de hospedagem são diferentes.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="ec1f5-115">Uma vantagem desse modelo é que você não está restrita tooresources que são implantados no seu grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-115">One advantage of this model is you're no longer constrained tooresources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="ec1f5-116">APIs gerenciadas</span><span class="sxs-lookup"><span data-stu-id="ec1f5-116">Managed APIs</span></span>

<span data-ttu-id="ec1f5-117">A Microsoft gerencia algumas APIs em seu nome, por exemplo o Office 365, Salesforce, Twitter e FTP.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="ec1f5-118">Algumas dessas APIs gerenciadas como o Bing Translate podem ser usadas como estão, enquanto outras exigem configuração.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="ec1f5-119">Essa configuração é denominada *conexão*.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="ec1f5-120">Por exemplo, quando você usa o Office 365, deve criar uma conexão que contém o token de entrada do Office 365.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="ec1f5-121">Esse token é armazenado e atualizado para que seu aplicativo lógico sempre possa chamar hello API do Office 365 com segurança.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-121">This token is securely stored and refreshed so that your logic app can always call hello Office 365 API.</span></span> <span data-ttu-id="ec1f5-122">Como alternativa, se desejar que o servidor SQL ou FTP tooyour tooconnect, você deve criar uma conexão com a cadeia de caracteres de conexão de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-122">Alternatively, if you want tooconnect tooyour SQL or FTP server, you must create a connection that has hello connection string.</span></span> 

<span data-ttu-id="ec1f5-123">Nessa definição, essas ações são denominadas `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="ec1f5-124">Aqui está um exemplo de uma conexão que chama o Office 365 toosend um email:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-124">Here is an example of a connection that calls Office 365 toosend an email:</span></span>

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

<span data-ttu-id="ec1f5-125">Olá `host` objeto é parte de entradas conexões tooAPI exclusivo, e contém dois partes: `api` e `connection`.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-125">hello `host` object is portion of inputs that is unique tooAPI connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="ec1f5-126">Olá `api` tem tempo de execução de saudação URL de onde que API não gerenciada está hospedado.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-126">hello `api` has hello runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="ec1f5-127">Você pode ver todos os Olá disponíveis APIs gerenciadas chamando `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-127">You can see all hello available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="ec1f5-128">Quando você usa uma API, Olá API poderá ou não ter qualquer *parâmetros de conexão* definido.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-128">When you use an API, hello API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="ec1f5-129">Se não Olá API, nenhum *conexão* é necessária.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-129">If hello API doesn't, no *connection* is required.</span></span> <span data-ttu-id="ec1f5-130">Se Olá API, você deve criar uma conexão.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-130">If hello API does, you must create a connection.</span></span> <span data-ttu-id="ec1f5-131">conexão Olá criado tem o nome de saudação que você escolher.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-131">hello created connection has hello name that you choose.</span></span> <span data-ttu-id="ec1f5-132">Você fazer referência a nome de saudação em hello `connection` objeto dentro de saudação `host` objeto.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-132">You then reference hello name in hello `connection` object inside hello `host` object.</span></span> <span data-ttu-id="ec1f5-133">uma conexão em um grupo de recursos, chamada de toocreate:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-133">toocreate a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="ec1f5-134">Com hello corpo a seguir:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-134">With hello following body:</span></span>

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

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="ec1f5-135">Implantar APIs gerenciadas em um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="ec1f5-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="ec1f5-136">Você pode criar um aplicativo completo em um modelo do Azure Resource Manager, desde que ele não exija entrada interativa.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="ec1f5-137">Se a entrada é necessária, você pode configurar tudo com o modelo do Azure Resource Manager hello, mas você ainda possui toovisit Olá tooauthorize portal Olá conexões.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-137">If sign-in is required, you can set up everything with hello Azure Resource Manager template, but you still have toovisit hello portal tooauthorize hello connections.</span></span> 

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

<span data-ttu-id="ec1f5-138">Você pode ver neste exemplo conexões Olá são apenas recursos que moram em seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-138">You can see in this example that hello connections are just resources that live in your resource group.</span></span> <span data-ttu-id="ec1f5-139">Eles fazem referência tooyou disponível de APIs de Olá gerenciado na sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-139">They reference hello managed APIs available tooyou in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="ec1f5-140">Suas APIs Web personalizadas</span><span class="sxs-lookup"><span data-stu-id="ec1f5-140">Your custom Web APIs</span></span>

<span data-ttu-id="ec1f5-141">Se você usar suas próprias APIs, aqueles não gerenciados pela Microsoft, use internas Olá **HTTP** ação toocall-los.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-141">If you use your own APIs, not Microsoft-managed ones, use hello built-in **HTTP** action toocall them.</span></span> <span data-ttu-id="ec1f5-142">Para uma experiência ideal, você deve expor um ponto de extremidade do Swagger para sua API.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="ec1f5-143">Esse ponto de extremidade permite que entradas de Olá Olá lógica aplicativo Designer toorender e saídas para a sua API.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-143">This endpoint enables hello Logic App Designer toorender hello inputs and outputs for your API.</span></span> <span data-ttu-id="ec1f5-144">Sem Swagger, designer de saudação só pode mostrar Olá entradas e saídas como objetos JSON opacos.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-144">Without Swagger, hello designer can only show hello inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="ec1f5-145">Aqui está uma saudação de mostrando exemplo novo `metadata.apiDefinitionUrl` propriedade:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-145">Here is an example showing hello new `metadata.apiDefinitionUrl` property:</span></span>

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

<span data-ttu-id="ec1f5-146">Se você hospedar sua API da Web no serviço de aplicativo do Azure, a API da Web é automaticamente aparece na lista de saudação de ações disponíveis no designer de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-146">If you host your Web API on Azure App Service, your Web API automatically appears in hello list of actions available in hello designer.</span></span> <span data-ttu-id="ec1f5-147">Caso contrário, o que toopaste diretamente na URL de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-147">If not, you have toopaste in hello URL directly.</span></span> <span data-ttu-id="ec1f5-148">ponto de extremidade de Swagger Olá deve ser não autenticado toobe utilizável em Olá Designer de lógica do aplicativo, embora você pode proteger a saudação própria API com qualquer métodos que oferece suporte a Swagger.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-148">hello Swagger endpoint must be unauthenticated toobe usable in hello Logic App Designer, although you can secure hello API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="ec1f5-149">Chamar aplicativos de API implantados com 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="ec1f5-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="ec1f5-150">Se você tiver implantado uma API App, você pode chamar o aplicativo hello com hello **HTTP** ação.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-150">If you previously deployed an API App, you can call hello app with hello **HTTP** action.</span></span>

<span data-ttu-id="ec1f5-151">Por exemplo, se você usar arquivos de toolist Dropbox, seu **2014-12-01-preview** definição de versão de esquema pode encontrar algo como:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-151">For example, if you use Dropbox toolist files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

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

<span data-ttu-id="ec1f5-152">Você pode construir a ação de HTTP equivalente hello como neste exemplo, enquanto a seção parâmetros Olá Olá definição de lógica de aplicativo permanece inalterada:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-152">You can construct hello equivalent HTTP action like this example, while hello parameters section of hello Logic app definition remains unchanged:</span></span>

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

<span data-ttu-id="ec1f5-153">Percorra essas propriedades, uma por vez:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="ec1f5-154">Propriedade da ação</span><span class="sxs-lookup"><span data-stu-id="ec1f5-154">Action property</span></span> | <span data-ttu-id="ec1f5-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="ec1f5-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="ec1f5-156">`Http` em vez de `APIapp`</span><span class="sxs-lookup"><span data-stu-id="ec1f5-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="ec1f5-157">toouse esta ação na Olá lógica de aplicativo Designer, incluem hello metadados ponto de extremidade, que é construído a partir de:`{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="ec1f5-157">toouse this action in hello Logic App Designer, include hello metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of hello api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="ec1f5-158">Construído com base em: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="ec1f5-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of hello api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="ec1f5-159">Sempre `POST`</span><span class="sxs-lookup"><span data-stu-id="ec1f5-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="ec1f5-160">Parâmetros do aplicativo toohello idênticos API</span><span class="sxs-lookup"><span data-stu-id="ec1f5-160">Identical toohello API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="ec1f5-161">Toohello idêntico autenticação API App</span><span class="sxs-lookup"><span data-stu-id="ec1f5-161">Identical toohello API App authentication</span></span> |

<span data-ttu-id="ec1f5-162">Essa abordagem deve funcionar para todas as ações de Aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="ec1f5-163">No entanto, lembre-se de que esses aplicativos de API anterior não têm mais suporte.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="ec1f5-164">Portanto você deve mover tooone de saudação duas outras opções anteriores, uma API gerenciada ou hospedando sua API da Web personalizado.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-164">So you should move tooone of hello two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-tooforeach"></a><span data-ttu-id="ec1f5-165">Renomeado 'Repetir' too'foreach'</span><span class="sxs-lookup"><span data-stu-id="ec1f5-165">Renamed 'repeat' too'foreach'</span></span>

<span data-ttu-id="ec1f5-166">Para a versão de esquema anterior hello, recebemos muito comentários dos clientes que **Repita** foi confuso e não capturar corretamente que **Repita** foi realmente um loop for each.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-166">For hello previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="ec1f5-167">Como resultado, podemos renomeou `repeat` muito`foreach`.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-167">As a result, we have renamed `repeat` too`foreach`.</span></span> <span data-ttu-id="ec1f5-168">Por exemplo, anteriormente você escreveria:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-168">For example, previously you would write:</span></span>

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

<span data-ttu-id="ec1f5-169">Agora você escreveria:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-169">Now you would write:</span></span>

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

<span data-ttu-id="ec1f5-170">Olá função `@repeatItem()` foi item atual do hello tooreference usadas anteriormente que está sendo iterado.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-170">hello function `@repeatItem()` was previously used tooreference hello current item being iterated over.</span></span> <span data-ttu-id="ec1f5-171">Essa função foi simplificada muito`@item()`.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-171">This function is now simplified too`@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="ec1f5-172">Saídas de referência de 'foreach'</span><span class="sxs-lookup"><span data-stu-id="ec1f5-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="ec1f5-173">Para simplificar, Olá saídas de `foreach` ações não são encapsuladas em um objeto chamado `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-173">For simplification, hello outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="ec1f5-174">Enquanto Olá saídas de saudação anterior `repeat` exemplo foram:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-174">While hello outputs from hello previous `repeat` example were:</span></span>

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

<span data-ttu-id="ec1f5-175">Agora, essas saídas são:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-175">Now these outputs are:</span></span>

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

<span data-ttu-id="ec1f5-176">Anteriormente, tooget toohello corpo de ação de saudação ao fazer referência a essas saídas:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-176">Previously, tooget toohello body of hello action when referencing these outputs:</span></span>

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

<span data-ttu-id="ec1f5-177">Agora você pode fazer:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-177">Now you can do instead:</span></span>

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

<span data-ttu-id="ec1f5-178">Com essas alterações, Olá funções `@repeatItem()`, `@repeatBody()`, e `@repeatOutputs()` são removidos.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-178">With these changes, hello functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="ec1f5-179">Ouvinte HTTP nativo:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-179">Native HTTP listener</span></span>

<span data-ttu-id="ec1f5-180">Olá ouvinte HTTP recursos agora são incorporados no.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-180">hello HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="ec1f5-181">Portanto, você não precisa toodeploy um aplicativo de API do ouvinte HTTP.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-181">So you no longer need toodeploy an HTTP Listener API App.</span></span> <span data-ttu-id="ec1f5-182">Consulte [Olá detalhes completos sobre como toomake seu aqui pode ser chamado de ponto de extremidade de aplicativo lógica](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="ec1f5-182">See [hello full details for how toomake your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="ec1f5-183">Com essas alterações, removemos Olá `@accessKeys()` função, que são substituídos pelo Olá `@listCallbackURL()` função para obter o ponto de extremidade hello quando necessário.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-183">With these changes, we removed hello `@accessKeys()` function, which we replaced with hello `@listCallbackURL()` function for getting hello endpoint when necessary.</span></span> <span data-ttu-id="ec1f5-184">Além disso, agora você deve definir pelo menos um gatilho em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="ec1f5-185">Se você quiser muito`/run` Olá fluxo de trabalho, você deve ter uma esses disparadores: `manual`, `apiConnectionWebhook`, ou `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-185">If you want too`/run` hello workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="ec1f5-186">Chamar fluxos de trabalho secundários</span><span class="sxs-lookup"><span data-stu-id="ec1f5-186">Call child workflows</span></span>

<span data-ttu-id="ec1f5-187">Anteriormente, chamar fluxos de trabalho filho necessário passar o fluxo de trabalho toohello, obter token de acesso de saudação e colando Olá token na definição de aplicativo de lógica de saudação onde você deseja toocall fluxo de trabalho filho.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-187">Previously, calling child workflows required going toohello workflow, getting hello access token, and pasting hello token in hello logic app definition where you want toocall that child workflow.</span></span> <span data-ttu-id="ec1f5-188">Com o novo esquema de hello, mecanismo gera automaticamente um SAS em tempo de execução para os aplicativos lógicos Olá Olá fluxo de trabalho filho para que você não tem muito colar informações secretas na definição de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-188">With hello new schema, hello Logic Apps engine automatically generates a SAS at runtime for hello child workflow so you don't have too paste any secrets into hello definition.</span></span> <span data-ttu-id="ec1f5-189">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="ec1f5-189">Here is an example:</span></span>

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

<span data-ttu-id="ec1f5-190">Uma melhoria de segundo é que nós estamos fornecendo filho Olá a solicitação de entrada do toohello de acesso total de fluxos de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-190">A second improvement is we are giving hello child workflows full access toohello incoming request.</span></span> <span data-ttu-id="ec1f5-191">Isso significa que você pode passar parâmetros de saudação *consultas* seção e em Olá *cabeçalhos* objeto e que você pode definir totalmente Olá corpo inteiro.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-191">That means that you can pass parameters in hello *queries* section and in hello *headers* object and that you can fully define hello entire body.</span></span>

<span data-ttu-id="ec1f5-192">Por fim, há as alterações necessárias toohello filho fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-192">Finally, there are required changes toohello child workflow.</span></span> <span data-ttu-id="ec1f5-193">Enquanto você poderia chamar anteriormente um fluxo de trabalho filho diretamente, agora você deve definir um ponto de extremidade do disparador no fluxo de trabalho Olá para Olá pai toocall.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in hello workflow for hello parent toocall.</span></span> <span data-ttu-id="ec1f5-194">Em geral, você adicionaria um gatilho que tenha `manual` digite e, em seguida, usar esse gatilho na definição do pai de saudação.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in hello parent definition.</span></span> <span data-ttu-id="ec1f5-195">Saudação de Observação `host` propriedade especificamente tem um `triggerName` porque você sempre deve especificar o gatilho está chamando.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-195">Note hello `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="ec1f5-196">Outras alterações</span><span class="sxs-lookup"><span data-stu-id="ec1f5-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="ec1f5-197">Nova propriedade ‘queries’</span><span class="sxs-lookup"><span data-stu-id="ec1f5-197">New 'queries' property</span></span>

<span data-ttu-id="ec1f5-198">Todos os tipos de ação oferecem suporte a uma nova entrada denominada `queries`.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="ec1f5-199">Essa entrada pode ser um objeto estruturado, em vez de ter a cadeia de caracteres de saudação tooassemble manualmente.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-199">This input can be a structured object, rather than you having tooassemble hello string by hand.</span></span>

### <a name="renamed-parse-function-toojson"></a><span data-ttu-id="ec1f5-200">Renomeado too'json() de função 'Parse' '</span><span class="sxs-lookup"><span data-stu-id="ec1f5-200">Renamed 'parse()' function too'json()'</span></span>

<span data-ttu-id="ec1f5-201">Estamos adicionando tipos de conteúdo mais rápido, para que tenhamos renomeado Olá `parse()` função muito`json()`.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-201">We are adding more content types soon, so we renamed hello `parse()` function too`json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="ec1f5-202">Em breve: APIs de Integração Corporativa</span><span class="sxs-lookup"><span data-stu-id="ec1f5-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="ec1f5-203">Não temos versões gerenciadas ainda do hello APIs de integração do Enterprise, como AS2.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-203">We don't have managed versions yet of hello Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="ec1f5-204">Enquanto isso, você pode usar seu APIs existentes do BizTalk implantados por meio de saudação ação HTTP.</span><span class="sxs-lookup"><span data-stu-id="ec1f5-204">Meanwhile, you can use your existing deployed BizTalk APIs through hello HTTP action.</span></span> <span data-ttu-id="ec1f5-205">Para obter detalhes, consulte "Usando seus aplicativos de API já implantados" em Olá [roteiro de integração](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="ec1f5-205">For details, see "Using your already deployed API apps" in hello [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
