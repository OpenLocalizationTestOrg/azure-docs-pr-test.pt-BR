---
title: "Atualizações de esquema 1 de agosto de 2015 preview - Aplicativo Lógico do Azure | Microsoft Docs"
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
ms.openlocfilehash: 35d7a56d5607dcc18a4407c65b92962d3d0dcd1d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="schema-updates-for-azure-logic-apps---august-1-2015-preview"></a><span data-ttu-id="95068-103">Atualizações de esquema para Aplicativos Lógicos do Azure - visualização de 1º de junho de 2015</span><span class="sxs-lookup"><span data-stu-id="95068-103">Schema updates for Azure Logic Apps - August 1, 2015 preview</span></span>

<span data-ttu-id="95068-104">Esse novo esquema e a versão da API para Aplicativos Lógicos do Azure incluem os principais aprimoramentos que tornam a lógica de aplicativos mais confiável e fácil de usar:</span><span class="sxs-lookup"><span data-stu-id="95068-104">This new schema and API version for Azure Logic Apps includes key improvements that make logic apps more reliable and easier to use:</span></span>

*   <span data-ttu-id="95068-105">O tipo de ação **APIApp** é atualizado para um novo tipo de ação [**APIConnection**](#api-connections).</span><span class="sxs-lookup"><span data-stu-id="95068-105">The **APIApp** action type is updated to a new [**APIConnection**](#api-connections) action type.</span></span>
*   <span data-ttu-id="95068-106">**Repeat** é renomeado para [**Foreach**](#foreach).</span><span class="sxs-lookup"><span data-stu-id="95068-106">**Repeat** is renamed to [**Foreach**](#foreach).</span></span>
*   <span data-ttu-id="95068-107">O [**aplicativo de API** Ouvinte HTTP](#http-listener) não é mais necessário.</span><span class="sxs-lookup"><span data-stu-id="95068-107">The [**HTTP Listener** API App](#http-listener) is no longer required.</span></span>
*   <span data-ttu-id="95068-108">A ação de chamar fluxos de trabalho secundários usa um [novo esquema](#child-workflows).</span><span class="sxs-lookup"><span data-stu-id="95068-108">Calling child workflows uses a [new schema](#child-workflows).</span></span>

<a name="api-connections"></a>
## <a name="move-to-api-connections"></a><span data-ttu-id="95068-109">Mover para conexões de API</span><span class="sxs-lookup"><span data-stu-id="95068-109">Move to API connections</span></span>

<span data-ttu-id="95068-110">A maior mudança é que você não precisa mais implantar Aplicativos de API em sua Assinatura do Azure para que você possa usar as APIs.</span><span class="sxs-lookup"><span data-stu-id="95068-110">The biggest change is that you no longer have to deploy API Apps into your Azure subscription so you can use APIs.</span></span> <span data-ttu-id="95068-111">Estas são as maneiras como você pode usar APIs:</span><span class="sxs-lookup"><span data-stu-id="95068-111">Here are the ways that you can use APIs:</span></span>

* <span data-ttu-id="95068-112">APIs gerenciadas</span><span class="sxs-lookup"><span data-stu-id="95068-112">Managed APIs</span></span>
* <span data-ttu-id="95068-113">Suas APIs Web personalizadas</span><span class="sxs-lookup"><span data-stu-id="95068-113">Your custom Web APIs</span></span>

<span data-ttu-id="95068-114">Cada modo é tratado de forma ligeiramente diferente, pois seu gerenciamento e modelos de hospedagem são diferentes.</span><span class="sxs-lookup"><span data-stu-id="95068-114">Each way is handled slightly differently because their management and hosting models are different.</span></span> <span data-ttu-id="95068-115">Uma vantagem desse modelo é que você não fica restrito aos recursos que são implantados em seu grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="95068-115">One advantage of this model is you're no longer constrained to resources that are deployed in your Azure resource group.</span></span> 

### <a name="managed-apis"></a><span data-ttu-id="95068-116">APIs gerenciadas</span><span class="sxs-lookup"><span data-stu-id="95068-116">Managed APIs</span></span>

<span data-ttu-id="95068-117">A Microsoft gerencia algumas APIs em seu nome, por exemplo o Office 365, Salesforce, Twitter e FTP.</span><span class="sxs-lookup"><span data-stu-id="95068-117">Microsoft manages some APIs on your behalf, such as Office 365, Salesforce, Twitter, and FTP.</span></span> <span data-ttu-id="95068-118">Algumas dessas APIs gerenciadas como o Bing Translate podem ser usadas como estão, enquanto outras exigem configuração.</span><span class="sxs-lookup"><span data-stu-id="95068-118">You can use some managed APIs as-is, such as Bing Translate, while others require configuration.</span></span> <span data-ttu-id="95068-119">Essa configuração é denominada *conexão*.</span><span class="sxs-lookup"><span data-stu-id="95068-119">This configuration is called a *connection*.</span></span>

<span data-ttu-id="95068-120">Por exemplo, quando você usa o Office 365, deve criar uma conexão que contém o token de entrada do Office 365.</span><span class="sxs-lookup"><span data-stu-id="95068-120">For example, when you use Office 365, you must create a connection that contains your Office 365 sign-in token.</span></span> <span data-ttu-id="95068-121">Esse token é armazenado e atualizado com segurança para que seu aplicativo lógico sempre possa chamar a API do Office 365.</span><span class="sxs-lookup"><span data-stu-id="95068-121">This token is securely stored and refreshed so that your logic app can always call the Office 365 API.</span></span> <span data-ttu-id="95068-122">Como alternativa, se você quiser se conectar ao seu servidor SQL ou FTP, será necessário criar uma conexão que tenha cadeia de conexão.</span><span class="sxs-lookup"><span data-stu-id="95068-122">Alternatively, if you want to connect to your SQL or FTP server, you must create a connection that has the connection string.</span></span> 

<span data-ttu-id="95068-123">Nessa definição, essas ações são denominadas `APIConnection`.</span><span class="sxs-lookup"><span data-stu-id="95068-123">In this definition, these actions are called `APIConnection`.</span></span> <span data-ttu-id="95068-124">Veja um exemplo de uma conexão que chama o Office 365 para enviar um email:</span><span class="sxs-lookup"><span data-stu-id="95068-124">Here is an example of a connection that calls Office 365 to send an email:</span></span>

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

<span data-ttu-id="95068-125">O objeto `host` é uma fração das entradas que é exclusiva para conexões de API e contém duas partes: `api` e `connection`.</span><span class="sxs-lookup"><span data-stu-id="95068-125">The `host` object is portion of inputs that is unique to API connections, and contains tow parts: `api` and `connection`.</span></span>

<span data-ttu-id="95068-126">`api` tem a URL de execução de onde a API gerenciada está hospedada.</span><span class="sxs-lookup"><span data-stu-id="95068-126">The `api` has the runtime URL of where that managed API is hosted.</span></span> <span data-ttu-id="95068-127">Você pode ver todas as APIs gerenciadas disponíveis chamando `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span><span class="sxs-lookup"><span data-stu-id="95068-127">You can see all the available managed APIs by calling `GET https://management.azure.com/subscriptions/{subid}/providers/Microsoft.Web/managedApis/?api-version=2015-08-01-preview`.</span></span>

<span data-ttu-id="95068-128">Quando você usa uma API, existe a possibilidade de ela não ter nenhum *parâmetro de conexão* definido ou de ter algum.</span><span class="sxs-lookup"><span data-stu-id="95068-128">When you use an API, the API might or might not have any *connection parameters* defined.</span></span> <span data-ttu-id="95068-129">Se a API não tiver, nenhuma *conexão* será necessária.</span><span class="sxs-lookup"><span data-stu-id="95068-129">If the API doesn't, no *connection* is required.</span></span> <span data-ttu-id="95068-130">Se a API tiver, você deverá criar uma conexão.</span><span class="sxs-lookup"><span data-stu-id="95068-130">If the API does, you must create a connection.</span></span> <span data-ttu-id="95068-131">A conexão criada com o nome que você escolher.</span><span class="sxs-lookup"><span data-stu-id="95068-131">The created connection has the name that you choose.</span></span> <span data-ttu-id="95068-132">Você faz então referência ao nome no objeto `connection` dentro do objeto `host`.</span><span class="sxs-lookup"><span data-stu-id="95068-132">You then reference the name in the `connection` object inside the `host` object.</span></span> <span data-ttu-id="95068-133">Para criar uma conexão em um grupo de recursos, chame:</span><span class="sxs-lookup"><span data-stu-id="95068-133">To create a connection in a resource group, call:</span></span>

```
PUT https://management.azure.com/subscriptions/{subid}/resourceGroups/{rgname}/providers/Microsoft.Web/connections/{name}?api-version=2015-08-01-preview
```

<span data-ttu-id="95068-134">Com o seguinte corpo:</span><span class="sxs-lookup"><span data-stu-id="95068-134">With the following body:</span></span>

```
{
  "properties": {
    "api": {
      "id": "/subscriptions/{subid}/providers/Microsoft.Web/managedApis/azureblob"
    },
    "parameterValues": {
        "accountName": "{The name of the storage account -- the set of parameters is different for each API}"
    }
  },
  "location": "{Logic app's location}"
}
```

### <a name="deploy-managed-apis-in-an-azure-resource-manager-template"></a><span data-ttu-id="95068-135">Implantar APIs gerenciadas em um modelo do Azure Resource Manager</span><span class="sxs-lookup"><span data-stu-id="95068-135">Deploy managed APIs in an Azure Resource Manager template</span></span>

<span data-ttu-id="95068-136">Você pode criar um aplicativo completo em um modelo do Azure Resource Manager, desde que ele não exija entrada interativa.</span><span class="sxs-lookup"><span data-stu-id="95068-136">You can create a full application in an Azure Resource Manager template as long as interactive sign-in isn't required.</span></span>
<span data-ttu-id="95068-137">Se for necessário entrar, você poderá configurar tudo com o modelo do Azure Resource Manager, mas ainda precisará visitar o portal a fim de autorizar as conexões.</span><span class="sxs-lookup"><span data-stu-id="95068-137">If sign-in is required, you can set up everything with the Azure Resource Manager template, but you still have to visit the portal to authorize the connections.</span></span> 

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

<span data-ttu-id="95068-138">Você pode ver neste exemplo que as conexões são apenas recursos que residem em seu grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="95068-138">You can see in this example that the connections are just resources that live in your resource group.</span></span> <span data-ttu-id="95068-139">Elas fazem referência às APIs gerenciadas disponíveis em sua assinatura.</span><span class="sxs-lookup"><span data-stu-id="95068-139">They reference the managed APIs available to you in your subscription.</span></span>

### <a name="your-custom-web-apis"></a><span data-ttu-id="95068-140">Suas APIs Web personalizadas</span><span class="sxs-lookup"><span data-stu-id="95068-140">Your custom Web APIs</span></span>

<span data-ttu-id="95068-141">Se você usar suas próprias APIs, aqueles não gerenciados pela Microsoft, usar interno **HTTP** ação chamá-los.</span><span class="sxs-lookup"><span data-stu-id="95068-141">If you use your own APIs, not Microsoft-managed ones, use the built-in **HTTP** action to call them.</span></span> <span data-ttu-id="95068-142">Para uma experiência ideal, você deve expor um ponto de extremidade do Swagger para sua API.</span><span class="sxs-lookup"><span data-stu-id="95068-142">For an ideal experience, you should expose a Swagger endpoint for your API.</span></span> <span data-ttu-id="95068-143">Esse ponto de extremidade permite que o Designer de Aplicativos Lógicos renderize as entradas e saídas de sua API.</span><span class="sxs-lookup"><span data-stu-id="95068-143">This endpoint enables the Logic App Designer to render the inputs and outputs for your API.</span></span> <span data-ttu-id="95068-144">Sem o Swagger, o designer só poderá mostrar as entradas e saídas como objetos JSON opacos.</span><span class="sxs-lookup"><span data-stu-id="95068-144">Without Swagger, the designer can only show the inputs and outputs as opaque JSON objects.</span></span>

<span data-ttu-id="95068-145">Veja um exemplo que mostra a nova propriedade `metadata.apiDefinitionUrl` :</span><span class="sxs-lookup"><span data-stu-id="95068-145">Here is an example showing the new `metadata.apiDefinitionUrl` property:</span></span>

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

<span data-ttu-id="95068-146">Se você hospedar sua API Web no Serviço de Aplicativo do Azure, ela aparecerá automaticamente na lista de ações disponíveis no designer.</span><span class="sxs-lookup"><span data-stu-id="95068-146">If you host your Web API on Azure App Service, your Web API automatically appears in the list of actions available in the designer.</span></span> <span data-ttu-id="95068-147">Caso você não faça isso, será necessário colar a URL diretamente.</span><span class="sxs-lookup"><span data-stu-id="95068-147">If not, you have to paste in the URL directly.</span></span> <span data-ttu-id="95068-148">O ponto de extremidade do Swagger não deve ser autenticado para que possa ser usado dentro do Designer de Aplicativos Lógicos, embora você possa proteger a API com quaisquer métodos com suporte no Swagger.</span><span class="sxs-lookup"><span data-stu-id="95068-148">The Swagger endpoint must be unauthenticated to be usable in the Logic App Designer, although you can secure the API itself with whatever methods that Swagger supports.</span></span>

### <a name="call-deployed-api-apps-with-2015-08-01-preview"></a><span data-ttu-id="95068-149">Chamar aplicativos de API implantados com 2015-08-01-preview</span><span class="sxs-lookup"><span data-stu-id="95068-149">Call deployed API apps with 2015-08-01-preview</span></span>

<span data-ttu-id="95068-150">Se você tiver implantado um Aplicativo de API, chame-o por meio da ação **HTTP** .</span><span class="sxs-lookup"><span data-stu-id="95068-150">If you previously deployed an API App, you can call the app with the **HTTP** action.</span></span>

<span data-ttu-id="95068-151">Por exemplo, se você usar o Dropbox para listar os arquivos, poderá ter algo assim em sua definição da versão do esquema **2014-12-01-preview**:</span><span class="sxs-lookup"><span data-stu-id="95068-151">For example, if you use Dropbox to list files, your **2014-12-01-preview** schema version definition might have something like:</span></span>

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

<span data-ttu-id="95068-152">Você pode construir a ação HTTP como neste exemplo enquanto a seção de parâmetros da definição do Aplicativo lógico permanece inalterada:</span><span class="sxs-lookup"><span data-stu-id="95068-152">You can construct the equivalent HTTP action like this example, while the parameters section of the Logic app definition remains unchanged:</span></span>

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

<span data-ttu-id="95068-153">Percorra essas propriedades, uma por vez:</span><span class="sxs-lookup"><span data-stu-id="95068-153">Walking through these properties one-by-one:</span></span>

| <span data-ttu-id="95068-154">Propriedade da ação</span><span class="sxs-lookup"><span data-stu-id="95068-154">Action property</span></span> | <span data-ttu-id="95068-155">Descrição</span><span class="sxs-lookup"><span data-stu-id="95068-155">Description</span></span> |
| --- | --- |
| `type` |<span data-ttu-id="95068-156">`Http` em vez de `APIapp`</span><span class="sxs-lookup"><span data-stu-id="95068-156">`Http` instead of `APIapp`</span></span> |
| `metadata.apiDefinitionUrl` |<span data-ttu-id="95068-157">Para usar essa ação no Designer de Aplicativos Lógicos, inclua o ponto de extremidade de metadados que é construído com base em: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span><span class="sxs-lookup"><span data-stu-id="95068-157">To use this action in the Logic App Designer, include the metadata endpoint, which is constructed from: `{api app host.gateway}/api/service/apidef/{last segment of the api app host.id}/?api-version=2015-01-14&format=swagger-2.0-standard`</span></span> |
| `inputs.uri` |<span data-ttu-id="95068-158">Construído com base em: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span><span class="sxs-lookup"><span data-stu-id="95068-158">Constructed from: `{api app host.gateway}/api/service/invoke/{last segment of the api app host.id}/{api app operation}?api-version=2015-01-14`</span></span> |
| `inputs.method` |<span data-ttu-id="95068-159">Sempre `POST`</span><span class="sxs-lookup"><span data-stu-id="95068-159">Always `POST`</span></span> |
| `inputs.body` |<span data-ttu-id="95068-160">Idêntico aos parâmetros do Aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="95068-160">Identical to the API App parameters</span></span> |
| `inputs.authentication` |<span data-ttu-id="95068-161">Idêntico à autenticação do aplicativo de API</span><span class="sxs-lookup"><span data-stu-id="95068-161">Identical to the API App authentication</span></span> |

<span data-ttu-id="95068-162">Essa abordagem deve funcionar para todas as ações de Aplicativo de API.</span><span class="sxs-lookup"><span data-stu-id="95068-162">This approach should work for all API App actions.</span></span> <span data-ttu-id="95068-163">No entanto, lembre-se de que esses aplicativos de API anterior não têm mais suporte.</span><span class="sxs-lookup"><span data-stu-id="95068-163">However, remember that these previous API Apps are no longer supported.</span></span> <span data-ttu-id="95068-164">Portanto, você deve mover para uma das duas outras opções anteriores, uma API gerenciada ou hospedagem sua API da Web personalizado.</span><span class="sxs-lookup"><span data-stu-id="95068-164">So you should move to one of the two other previous options, a managed API or hosting your custom Web API.</span></span>

<a name="foreach"></a>
## <a name="renamed-repeat-to-foreach"></a><span data-ttu-id="95068-165">'repeat' renomeado para 'foreach'</span><span class="sxs-lookup"><span data-stu-id="95068-165">Renamed 'repeat' to 'foreach'</span></span>

<span data-ttu-id="95068-166">Recebemos muitos comentários de clientes na versão anterior do esquema informando que **Repeat** era confuso e não capturava corretamente que **Repeat** era, na verdade, um loop for each.</span><span class="sxs-lookup"><span data-stu-id="95068-166">For the previous schema version, we received much customer feedback that **Repeat** was confusing and didn't properly capture that **Repeat** was really a for-each loop.</span></span> <span data-ttu-id="95068-167">Como resultado, nós renomeamos `repeat` como `foreach`.</span><span class="sxs-lookup"><span data-stu-id="95068-167">As a result, we have renamed `repeat` to `foreach`.</span></span> <span data-ttu-id="95068-168">Por exemplo, anteriormente você escreveria:</span><span class="sxs-lookup"><span data-stu-id="95068-168">For example, previously you would write:</span></span>

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

<span data-ttu-id="95068-169">Agora você escreveria:</span><span class="sxs-lookup"><span data-stu-id="95068-169">Now you would write:</span></span>

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

<span data-ttu-id="95068-170">Anteriormente, a função `@repeatItem()` era usada para fazer referência ao item atual sendo iterado.</span><span class="sxs-lookup"><span data-stu-id="95068-170">The function `@repeatItem()` was previously used to reference the current item being iterated over.</span></span> <span data-ttu-id="95068-171">Essa função foi agora simplificada para `@item()`.</span><span class="sxs-lookup"><span data-stu-id="95068-171">This function is now simplified to `@item()`.</span></span> 

### <a name="reference-outputs-from-foreach"></a><span data-ttu-id="95068-172">Saídas de referência de 'foreach'</span><span class="sxs-lookup"><span data-stu-id="95068-172">Reference outputs from 'foreach'</span></span>

<span data-ttu-id="95068-173">Para simplificar, as saídas de ações do `foreach` não são encapsuladas em um objeto chamado `repeatItems`.</span><span class="sxs-lookup"><span data-stu-id="95068-173">For simplification, the outputs from `foreach` actions are not wrapped in an object called `repeatItems`.</span></span> <span data-ttu-id="95068-174">Embora as saídas do exemplo anterior de `repeat` tenham sido:</span><span class="sxs-lookup"><span data-stu-id="95068-174">While the outputs from the previous `repeat` example were:</span></span>

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

<span data-ttu-id="95068-175">Agora, essas saídas são:</span><span class="sxs-lookup"><span data-stu-id="95068-175">Now these outputs are:</span></span>

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

<span data-ttu-id="95068-176">Anteriormente, para chegar ao corpo da ação ao fazer referência a essas saídas:</span><span class="sxs-lookup"><span data-stu-id="95068-176">Previously, to get to the body of the action when referencing these outputs:</span></span>

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

<span data-ttu-id="95068-177">Agora você pode fazer:</span><span class="sxs-lookup"><span data-stu-id="95068-177">Now you can do instead:</span></span>

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

<span data-ttu-id="95068-178">Com essas alterações, as funções `@repeatItem()`, `@repeatBody()` e `@repeatOutputs()` foram removidas.</span><span class="sxs-lookup"><span data-stu-id="95068-178">With these changes, the functions `@repeatItem()`, `@repeatBody()`, and `@repeatOutputs()` are removed.</span></span>

<a name="http-listener"></a>
## <a name="native-http-listener"></a><span data-ttu-id="95068-179">Ouvinte HTTP nativo:</span><span class="sxs-lookup"><span data-stu-id="95068-179">Native HTTP listener</span></span>

<span data-ttu-id="95068-180">Os recursos de Ouvinte HTTP agora são internos.</span><span class="sxs-lookup"><span data-stu-id="95068-180">The HTTP Listener capabilities are now built in.</span></span> <span data-ttu-id="95068-181">Portanto, você não precisa mais implantar um Aplicativo de API do Ouvinte HTTP.</span><span class="sxs-lookup"><span data-stu-id="95068-181">So you no longer need to deploy an HTTP Listener API App.</span></span> <span data-ttu-id="95068-182">Veja [os detalhes completos de como fazer com que seu ponto de extremidade do aplicativo lógico seja chamado aqui](../logic-apps/logic-apps-http-endpoint.md).</span><span class="sxs-lookup"><span data-stu-id="95068-182">See [the full details for how to make your Logic app endpoint callable here](../logic-apps/logic-apps-http-endpoint.md).</span></span> 

<span data-ttu-id="95068-183">Com essas alterações, removemos o `@accessKeys()` função, que são substituídos com o `@listCallbackURL()` função para obter o ponto de extremidade quando necessário.</span><span class="sxs-lookup"><span data-stu-id="95068-183">With these changes, we removed the `@accessKeys()` function, which we replaced with the `@listCallbackURL()` function for getting the endpoint when necessary.</span></span> <span data-ttu-id="95068-184">Além disso, agora você deve definir pelo menos um gatilho em seu aplicativo lógico.</span><span class="sxs-lookup"><span data-stu-id="95068-184">Also, you must now define at least one trigger in your logic app.</span></span> <span data-ttu-id="95068-185">Se você quiser `/run` o fluxo de trabalho, deverá ter um dos gatilhos a seguir: `manual`, `apiConnectionWebhook` ou `httpWebhook`.</span><span class="sxs-lookup"><span data-stu-id="95068-185">If you want to `/run` the workflow, you must have one of these triggers: `manual`, `apiConnectionWebhook`, or `httpWebhook`.</span></span>

<a name="child-workflows"></a>
## <a name="call-child-workflows"></a><span data-ttu-id="95068-186">Chamar fluxos de trabalho secundários</span><span class="sxs-lookup"><span data-stu-id="95068-186">Call child workflows</span></span>

<span data-ttu-id="95068-187">Anteriormente, chamar os fluxos de trabalho secundários exigia ir para esse fluxo de trabalho, obter o token de acesso e colar o token na definição do aplicativo lógico no qual você deseja chamar o fluxo de trabalho secundário.</span><span class="sxs-lookup"><span data-stu-id="95068-187">Previously, calling child workflows required going to the workflow, getting the access token, and pasting the token in the logic app definition where you want to call that child workflow.</span></span> <span data-ttu-id="95068-188">Com o novo esquema, o mecanismo de Aplicativos Lógicos gera automaticamente um SAS em tempo de execução para fluxo de trabalho filho para que você não precise colar informações secretas na definição.</span><span class="sxs-lookup"><span data-stu-id="95068-188">With the new schema, the Logic Apps engine automatically generates a SAS at runtime for the child workflow so you don't have to paste any secrets into the definition.</span></span> <span data-ttu-id="95068-189">Aqui está um exemplo:</span><span class="sxs-lookup"><span data-stu-id="95068-189">Here is an example:</span></span>

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

<span data-ttu-id="95068-190">Um segundo aprimoramento é que demos aos fluxos de trabalho filho acesso completo à solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="95068-190">A second improvement is we are giving the child workflows full access to the incoming request.</span></span> <span data-ttu-id="95068-191">Isso significa que você pode passar parâmetros na seção *consultas* e no objeto *cabeçalhos*, e que pode definir completamente o corpo.</span><span class="sxs-lookup"><span data-stu-id="95068-191">That means that you can pass parameters in the *queries* section and in the *headers* object and that you can fully define the entire body.</span></span>

<span data-ttu-id="95068-192">Por fim, há alterações necessárias no fluxo de trabalho secundário.</span><span class="sxs-lookup"><span data-stu-id="95068-192">Finally, there are required changes to the child workflow.</span></span> <span data-ttu-id="95068-193">Enquanto antes você podia chamar um fluxo de trabalho filho diretamente, agora você precisa definir um ponto de extremidade de gatilho no fluxo de trabalho para o pai chamar.</span><span class="sxs-lookup"><span data-stu-id="95068-193">While you could previously call a child workflow directly, now you must define a trigger endpoint in the workflow for the parent to call.</span></span> <span data-ttu-id="95068-194">Em geral, você adicionaria um disparador que possui `manual` digite e, em seguida, usar esse gatilho na definição do pai.</span><span class="sxs-lookup"><span data-stu-id="95068-194">Generally, you would add a trigger that has `manual` type, and then use that trigger in the parent definition.</span></span> <span data-ttu-id="95068-195">Observe que a propriedade `host`, especificamente, tem um `triggerName`, pois você sempre deve especificar qual gatilho está invocando.</span><span class="sxs-lookup"><span data-stu-id="95068-195">Note the `host` property specifically has a `triggerName` because you must always specify which trigger you are invoking.</span></span>

## <a name="other-changes"></a><span data-ttu-id="95068-196">Outras alterações</span><span class="sxs-lookup"><span data-stu-id="95068-196">Other changes</span></span>

### <a name="new-queries-property"></a><span data-ttu-id="95068-197">Nova propriedade ‘queries’</span><span class="sxs-lookup"><span data-stu-id="95068-197">New 'queries' property</span></span>

<span data-ttu-id="95068-198">Todos os tipos de ação oferecem suporte a uma nova entrada denominada `queries`.</span><span class="sxs-lookup"><span data-stu-id="95068-198">All action types now support a new input called `queries`.</span></span> <span data-ttu-id="95068-199">Essa entrada pode ser um objeto estruturado em vez de precisar montar a cadeia de caracteres manualmente.</span><span class="sxs-lookup"><span data-stu-id="95068-199">This input can be a structured object, rather than you having to assemble the string by hand.</span></span>

### <a name="renamed-parse-function-to-json"></a><span data-ttu-id="95068-200">Função 'parse()' renomeada para 'json()'</span><span class="sxs-lookup"><span data-stu-id="95068-200">Renamed 'parse()' function to 'json()'</span></span>

<span data-ttu-id="95068-201">Adicionaremos mais tipos de conteúdo em breve e, portanto, renomeamos a função `parse()` para `json()`.</span><span class="sxs-lookup"><span data-stu-id="95068-201">We are adding more content types soon, so we renamed the `parse()` function to `json()`.</span></span>

## <a name="coming-soon-enterprise-integration-apis"></a><span data-ttu-id="95068-202">Em breve: APIs de Integração Corporativa</span><span class="sxs-lookup"><span data-stu-id="95068-202">Coming soon: Enterprise Integration APIs</span></span>

<span data-ttu-id="95068-203">Não temos versões gerenciadas ainda das APIs de integração do Enterprise, como o AS2.</span><span class="sxs-lookup"><span data-stu-id="95068-203">We don't have managed versions yet of the Enterprise Integration APIs, like AS2.</span></span> <span data-ttu-id="95068-204">Enquanto isso, você pode usar suas APIs do BizTalk implantadas existentes por meio da ação de HTTP.</span><span class="sxs-lookup"><span data-stu-id="95068-204">Meanwhile, you can use your existing deployed BizTalk APIs through the HTTP action.</span></span> <span data-ttu-id="95068-205">Para obter detalhes, veja "Uso dos seus aplicativos de API já implantados" no [roteiro de integração](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span><span class="sxs-lookup"><span data-stu-id="95068-205">For details, see "Using your already deployed API apps" in the [integration roadmap](http://www.zdnet.com/article/microsoft-outlines-its-cloud-and-server-integration-roadmap-for-2016/).</span></span> 
