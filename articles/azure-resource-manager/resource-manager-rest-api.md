---
title: REST APIs do Gerenciador de aaaResource | Microsoft Docs
description: "Uma visão geral do hello autenticação de APIs de REST do Gerenciador de recursos e exemplos de uso"
services: azure-resource-manager
documentationcenter: na
author: navalev
manager: timlt
editor: 
ms.assetid: e8d7a1d2-1e82-4212-8288-8697341408c5
ms.service: azure-resource-manager
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 01/13/2017
ms.author: navale;tomfitz;
ms.openlocfilehash: 3ccc3575c5e06c41f2fdc5317711980fc6a2f649
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="resource-manager-rest-apis"></a>APIs REST do Gerenciador de Recursos
> [!div class="op_single_selector"]
> * [PowerShell do Azure](powershell-azure-resource-manager.md)
> * [CLI do Azure](xplat-cli-azure-resource-manager.md)
> * [Portal](resource-group-portal.md) 
> * [API REST](resource-manager-rest-api.md)
> 
> 

Atrás de cada chamada tooAzure Gerenciador de recursos, atrás de cada modelo implantado, atrás de cada conta de armazenamento configurada há API RESTful uma ou mais chamadas toohello Azure Resource Manager. Este tópico é toothose dedicado APIs e como você pode chamá-las sem usar qualquer SDK em todos os. Essa abordagem é útil se você deseja controle total de solicitações tooAzure ou se hello SDK para seu idioma preferencial não está disponível ou não dá suporte a operações de saudação que é necessário.

Este artigo não passar por todas as APIs que é exposta no Azure, mas em vez disso, usa algumas operações como exemplos de como você conecta toothem. Depois de entender os fundamentos de saudação, você pode ler Olá [Reference à API REST do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) toofind informações detalhadas sobre como o restante Olá toouse Olá APIs.

## <a name="authentication"></a>Autenticação
A autenticação para o Resource Manager é tratada pelo Azure Active Directory (AD). tooconnect tooany API, você primeiro precisa tooauthenticate com AD do Azure tooreceive um token de autenticação que você pode passar na solicitação tooevery. Como estamos descrevendo uma chamada pura diretamente toohello APIs REST, vamos supor que você não deseja tooauthenticate por que está sendo solicitado um nome de usuário e senha. Também supomos que você não está usando mecanismos de autenticação de dois fatores. Portanto, criamos o que é chamado de um aplicativo do AD do Azure e uma entidade de serviço são usada toolog no. Lembre-se de que o AD do Azure suporta vários procedimentos de autenticação e todos eles, mas pode ser usado tooretrieve esse token de autenticação que precisamos para solicitações subsequentes de API.
Siga [Criar aplicativo do Azure AD e Entidade de Serviço](resource-group-create-service-principal-portal.md) para obter etapas detalhadas.

### <a name="generating-an-access-token"></a>Gerando um token de acesso
Autenticação no AD do Azure é feita ao chamar tooAzure AD, localizado em login.microsoftonline.com. tooauthenticate, você precisa Olá toohave informações a seguir:

* ID do locatário do AD do Azure (Olá nome do que você estiver usando toolog no Azure AD, geralmente Olá mesmo que sua empresa, mas não é necessário)
* ID do aplicativo (obtido durante a etapa de criação do aplicativo de saudação do AD do Azure)
* Senha (que você selecionou ao criar hello aplicativo do Azure AD)

No hello solicitação HTTP a seguir, verifique se tooreplace "ID de locatário do AD do Azure", "ID do aplicativo" e "Password" com valores corretos hello.

**Solicitação HTTP Genérica:**

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

... será (se a autenticação for bem-sucedida) resulta em uma toohello semelhante resposta resposta a seguir:

```json
{
  "token_type": "Bearer",
  "expires_in": "3600",
  "expires_on": "1448199959",
  "not_before": "1448196059",
  "resource": "https://management.core.windows.net/",
  "access_token": "eyJ0eXAiOiJKV1QiLCJhb...86U3JI_0InPUk_lZqWvKiEWsayA"
}
```
(Olá access_token no hello anterior resposta ter sido reduzido tooincrease legibilidade)

**Gerando um token de acesso usando Bash:**

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

**Gerando um token de acesso usando o PowerShell:**

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

resposta de saudação contém um token de acesso, informações sobre quanto tempo esse token é válido e obter informações sobre quais recursos você pode usar esse token para.
token de acesso de saudação recebida na chamada HTTP anterior Olá deve ser passado em para todos os solicitação toohello API do Gerenciador de recursos. Você passá-lo como um valor de cabeçalho chamado "Autorização" com o valor de hello "Portador YOUR_ACCESS_TOKEN". Observe o espaço de saudação entre "Portador" e o token de acesso.

Como você pode ver da saudação acima resultado de HTTP, o token de Olá é válido por um período de tempo durante os quais você deve armazenar em cache e reutilizar esse mesmo token específico. Mesmo se for possível tooauthenticate no AD do Azure para cada chamada de API, poderá ser altamente ineficiente.

## <a name="calling-resource-manager-rest-apis"></a>Chamar APIs REST do Resource Manager
Este tópico usa apenas algumas APIs tooexplain Olá uso básico de operações de REST hello. Para obter informações sobre todas as operações de hello, consulte [APIs de REST do Gerenciador de recursos do Azure](https://docs.microsoft.com/rest/api/resources/).

### <a name="list-all-subscriptions"></a>Listar todas as assinaturas
Uma das operações mais simples hello, que você pode fazer é toolist Olá assinaturas disponíveis que você pode acessar. Olá solicitação a seguir, você verá como token de acesso de saudação é passado como um cabeçalho:

(Substitua YOUR_ACCESS_TOKEN por seu Token de Acesso real.)

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

... e como resultado, você obtém uma lista de assinaturas que essa entidade de serviço é permitida tooaccess

(As IDs de Assinatura abaixo foram reduzidas para facilitar a leitura)

```json
{
  "value": [
    {
      "id": "/subscriptions/3a8555...555995",
      "subscriptionId": "3a8555...555995",
      "displayName": "Azure Subscription",
      "state": "Enabled",
      "subscriptionPolicies": {
        "locationPlacementId": "Internal_2014-09-01",
        "quotaId": "Internal_2014-09-01"
      }
    }
  ]
}
```

### <a name="list-all-resource-groups-in-a-specific-subscription"></a>Listar todos os grupos de recursos em uma assinatura específica
Todos os recursos disponíveis com hello APIs do Gerenciador de recursos são aninhados dentro de um grupo de recursos. Você pode consultar o Gerenciador de recursos para grupos de recursos existentes em sua assinatura usando Olá solicitação HTTP GET a seguir. Observe como ID de assinatura de saudação é passado como parte da URL Olá neste momento.

(Substitua YOUR_ACCESS_TOKEN e SUBSCRIPTION_ID pelo seu token de acesso e ID de assinatura)

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

Olá resposta você obter depende se você tiver grupos de recursos definidos e nesse caso, a quantidade.

(As IDs de Assinatura abaixo foram reduzidas para facilitar a leitura)

```json
{
    "value": [
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/myfirstresourcegroup",
            "name": "myfirstresourcegroup",
            "location": "eastus",
            "properties": {
                "provisioningState": "Succeeded"
            }
        },
        {
            "id": "/subscriptions/3a8555...555995/resourceGroups/mysecondresourcegroup",
            "name": "mysecondresourcegroup",
            "location": "northeurope",
            "tags": {
                "tagname1": "My first tag"
            },
            "properties": {
                "provisioningState": "Succeeded"
            }
        }
    ]
}
```

### <a name="create-a-resource-group"></a>Criar um grupo de recursos
Até agora, nós já foi consultando apenas Olá APIs do Gerenciador de recursos para obter informações. É hora de criar alguns recursos e vamos começar hello mais simples de todos eles, um grupo de recursos. Olá solicitação HTTP a seguir cria um grupo de recursos em um região/local de sua escolha e adiciona uma marca tooit.

(Substitua YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME real Token de acesso, ID da assinatura e nome de grupo de recursos que você deseja toocreate do hello)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  }
}
```

Se for bem-sucedido, você receberá uma resposta semelhante toohello resposta a seguir:

```json
{
  "id": "/subscriptions/3a8555...555995/resourceGroups/RESOURCE_GROUP_NAME",
  "name": "RESOURCE_GROUP_NAME",
  "location": "northeurope",
  "tags": {
    "tagname1": "test-tag"
  },
  "properties": {
    "provisioningState": "Succeeded"
  }
}
```

Você criou um grupo de recursos no Azure com êxito. Parabéns!

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a>Implantar grupo de recursos tooa de recursos usando um modelo do Gerenciador de recursos
Com o Resource Manager, você pode implantar os recursos usando modelos. Um modelo define vários recursos e suas dependências. Para essa seção, vamos supor estiver familiarizado com modelos do Gerenciador de recursos, e apenas exibir como toomake Olá API chamar toostart implantação. Para obter mais informações sobre como construir modelos, consulte [Criação de Modelos do Azure Resource Manager](resource-group-authoring-templates.md).

Implantação de um modelo não diferem muito toohow chamar outras APIs. Um aspecto importante é que a implantação de um modelo pode levar muito tempo. chamada Hello API retorna apenas e é o tooyou como desenvolvedor tooquery status da saudação implantação toofind out quando Olá implantação é feita. Para obter mais informações, consulte [Rastrear operações assíncronas de Azure](resource-manager-async-operations.md).

Neste exemplo, usaremos um modelo exposto publicamente disponível no [GitHub](https://github.com/Azure/azure-quickstart-templates). modelo de saudação que usamos implanta uma região do VM Linux toohello Oeste dos EUA. Embora esse exemplo usa um modelo disponível em um repositório público como GitHub, você pode passar em vez disso, modelo completo hello como parte da solicitação de saudação. Observe que podemos fornecer valores de parâmetro na solicitação de saudação que são utilizados em Olá implantados modelo.

(Substitua SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD e DNS_NAME_FOR_PUBLIC_IP toovalues apropriado para a sua solicitação)

```HTTP
PUT /subscriptions/SUBSCRIPTION_ID/resourcegroups/RESOURCE_GROUP_NAME/providers/microsoft.resources/deployments/DEPLOYMENT_NAME?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json

{
  "properties": {
    "templateLink": {
      "uri": "https://raw.githubusercontent.com/Azure/azure-quickstart-templates/master/101-simple-linux-vm/azuredeploy.json",
      "contentVersion": "1.0.0.0",
    },
    "mode": "Incremental",
    "parameters": {
        "newStorageAccountName": {
          "value": "GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME"
        },
        "adminUsername": {
          "value": "ADMIN_USER_NAME"
        },
        "adminPassword": {
          "value": "ADMIN_PASSWORD"
        },
        "dnsNameForPublicIP": {
          "value": "DNS_NAME_FOR_PUBLIC_IP"
        },
        "ubuntuOSVersion": {
          "value": "15.04"
        }
    }
  }
}
```

resposta JSON longa Olá para esta solicitação foi omitido tooimprove legibilidade desta documentação. resposta de saudação contém informações sobre a implantação de modelo de saudação que você criou.

## <a name="next-steps"></a>Próximas etapas

- toolearn sobre como lidar com operações assíncronas de REST, consulte [controlar operações assíncronas de Azure](resource-manager-async-operations.md).
