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
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="6897b-103">APIs REST do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="6897b-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="6897b-104">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="6897b-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="6897b-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="6897b-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="6897b-106">Portal</span><span class="sxs-lookup"><span data-stu-id="6897b-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="6897b-107">API REST</span><span class="sxs-lookup"><span data-stu-id="6897b-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="6897b-108">Atrás de cada chamada tooAzure Gerenciador de recursos, atrás de cada modelo implantado, atrás de cada conta de armazenamento configurada há API RESTful uma ou mais chamadas toohello Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="6897b-108">Behind every call tooAzure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls toohello Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="6897b-109">Este tópico é toothose dedicado APIs e como você pode chamá-las sem usar qualquer SDK em todos os.</span><span class="sxs-lookup"><span data-stu-id="6897b-109">This topic is devoted toothose APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="6897b-110">Essa abordagem é útil se você deseja controle total de solicitações tooAzure ou se hello SDK para seu idioma preferencial não está disponível ou não dá suporte a operações de saudação que é necessário.</span><span class="sxs-lookup"><span data-stu-id="6897b-110">This approach is useful if you want full control of requests tooAzure, or if hello SDK for your preferred language is not available or doesn't support hello operations you need.</span></span>

<span data-ttu-id="6897b-111">Este artigo não passar por todas as APIs que é exposta no Azure, mas em vez disso, usa algumas operações como exemplos de como você conecta toothem.</span><span class="sxs-lookup"><span data-stu-id="6897b-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect toothem.</span></span> <span data-ttu-id="6897b-112">Depois de entender os fundamentos de saudação, você pode ler Olá [Reference à API REST do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) toofind informações detalhadas sobre como o restante Olá toouse Olá APIs.</span><span class="sxs-lookup"><span data-stu-id="6897b-112">After you understand hello basics, you can read hello [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) toofind detailed information on how toouse hello rest of hello APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="6897b-113">Autenticação</span><span class="sxs-lookup"><span data-stu-id="6897b-113">Authentication</span></span>
<span data-ttu-id="6897b-114">A autenticação para o Resource Manager é tratada pelo Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="6897b-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="6897b-115">tooconnect tooany API, você primeiro precisa tooauthenticate com AD do Azure tooreceive um token de autenticação que você pode passar na solicitação tooevery.</span><span class="sxs-lookup"><span data-stu-id="6897b-115">tooconnect tooany API, you first need tooauthenticate with Azure AD tooreceive an authentication token that you can pass on tooevery request.</span></span> <span data-ttu-id="6897b-116">Como estamos descrevendo uma chamada pura diretamente toohello APIs REST, vamos supor que você não deseja tooauthenticate por que está sendo solicitado um nome de usuário e senha.</span><span class="sxs-lookup"><span data-stu-id="6897b-116">As we are describing a pure call directly toohello REST APIs, we assume that you don't want tooauthenticate by being prompted for a username and password.</span></span> <span data-ttu-id="6897b-117">Também supomos que você não está usando mecanismos de autenticação de dois fatores.</span><span class="sxs-lookup"><span data-stu-id="6897b-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="6897b-118">Portanto, criamos o que é chamado de um aplicativo do AD do Azure e uma entidade de serviço são usada toolog no.</span><span class="sxs-lookup"><span data-stu-id="6897b-118">Therefore, we create what is called an Azure AD Application and a service principal that are used toolog in.</span></span> <span data-ttu-id="6897b-119">Lembre-se de que o AD do Azure suporta vários procedimentos de autenticação e todos eles, mas pode ser usado tooretrieve esse token de autenticação que precisamos para solicitações subsequentes de API.</span><span class="sxs-lookup"><span data-stu-id="6897b-119">But remember that Azure AD support several authentication procedures and all of them could be used tooretrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="6897b-120">Siga [Criar aplicativo do Azure AD e Entidade de Serviço](resource-group-create-service-principal-portal.md) para obter etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="6897b-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="6897b-121">Gerando um token de acesso</span><span class="sxs-lookup"><span data-stu-id="6897b-121">Generating an Access Token</span></span>
<span data-ttu-id="6897b-122">Autenticação no AD do Azure é feita ao chamar tooAzure AD, localizado em login.microsoftonline.com. tooauthenticate, você precisa Olá toohave informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="6897b-122">Authentication against Azure AD is done by calling out tooAzure AD, located at login.microsoftonline.com. tooauthenticate, you need toohave hello following information:</span></span>

* <span data-ttu-id="6897b-123">ID do locatário do AD do Azure (Olá nome do que você estiver usando toolog no Azure AD, geralmente Olá mesmo que sua empresa, mas não é necessário)</span><span class="sxs-lookup"><span data-stu-id="6897b-123">Azure AD Tenant ID (hello name of that Azure AD you are using toolog in, often hello same as your company but not necessary)</span></span>
* <span data-ttu-id="6897b-124">ID do aplicativo (obtido durante a etapa de criação do aplicativo de saudação do AD do Azure)</span><span class="sxs-lookup"><span data-stu-id="6897b-124">Application ID (taken during hello Azure AD application creation step)</span></span>
* <span data-ttu-id="6897b-125">Senha (que você selecionou ao criar hello aplicativo do Azure AD)</span><span class="sxs-lookup"><span data-stu-id="6897b-125">Password (that you selected while creating hello Azure AD Application)</span></span>

<span data-ttu-id="6897b-126">No hello solicitação HTTP a seguir, verifique se tooreplace "ID de locatário do AD do Azure", "ID do aplicativo" e "Password" com valores corretos hello.</span><span class="sxs-lookup"><span data-stu-id="6897b-126">In hello following HTTP request, make sure tooreplace "Azure AD Tenant ID", "Application ID" and "Password" with hello correct values.</span></span>

<span data-ttu-id="6897b-127">**Solicitação HTTP Genérica:**</span><span class="sxs-lookup"><span data-stu-id="6897b-127">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="6897b-128">... será (se a autenticação for bem-sucedida) resulta em uma toohello semelhante resposta resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="6897b-128">... will (if authentication succeeds) result in a response similar toohello following response:</span></span>

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
<span data-ttu-id="6897b-129">(Olá access_token no hello anterior resposta ter sido reduzido tooincrease legibilidade)</span><span class="sxs-lookup"><span data-stu-id="6897b-129">(hello access_token in hello preceding response have been shortened tooincrease readability)</span></span>

<span data-ttu-id="6897b-130">**Gerando um token de acesso usando Bash:**</span><span class="sxs-lookup"><span data-stu-id="6897b-130">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="6897b-131">**Gerando um token de acesso usando o PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="6897b-131">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="6897b-132">resposta de saudação contém um token de acesso, informações sobre quanto tempo esse token é válido e obter informações sobre quais recursos você pode usar esse token para.</span><span class="sxs-lookup"><span data-stu-id="6897b-132">hello response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="6897b-133">token de acesso de saudação recebida na chamada HTTP anterior Olá deve ser passado em para todos os solicitação toohello API do Gerenciador de recursos.</span><span class="sxs-lookup"><span data-stu-id="6897b-133">hello access token you received in hello previous HTTP call must be passed in for all request toohello Resource Manager API.</span></span> <span data-ttu-id="6897b-134">Você passá-lo como um valor de cabeçalho chamado "Autorização" com o valor de hello "Portador YOUR_ACCESS_TOKEN".</span><span class="sxs-lookup"><span data-stu-id="6897b-134">You pass it as a header value named "Authorization" with hello value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="6897b-135">Observe o espaço de saudação entre "Portador" e o token de acesso.</span><span class="sxs-lookup"><span data-stu-id="6897b-135">Notice hello space between "Bearer" and your access token.</span></span>

<span data-ttu-id="6897b-136">Como você pode ver da saudação acima resultado de HTTP, o token de Olá é válido por um período de tempo durante os quais você deve armazenar em cache e reutilizar esse mesmo token específico.</span><span class="sxs-lookup"><span data-stu-id="6897b-136">As you can see from hello above HTTP Result, hello token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="6897b-137">Mesmo se for possível tooauthenticate no AD do Azure para cada chamada de API, poderá ser altamente ineficiente.</span><span class="sxs-lookup"><span data-stu-id="6897b-137">Even if it is possible tooauthenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="6897b-138">Chamar APIs REST do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="6897b-138">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="6897b-139">Este tópico usa apenas algumas APIs tooexplain Olá uso básico de operações de REST hello.</span><span class="sxs-lookup"><span data-stu-id="6897b-139">This topic only uses a few APIs tooexplain hello basic usage of hello REST operations.</span></span> <span data-ttu-id="6897b-140">Para obter informações sobre todas as operações de hello, consulte [APIs de REST do Gerenciador de recursos do Azure](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="6897b-140">For information about all hello operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="6897b-141">Listar todas as assinaturas</span><span class="sxs-lookup"><span data-stu-id="6897b-141">List all subscriptions</span></span>
<span data-ttu-id="6897b-142">Uma das operações mais simples hello, que você pode fazer é toolist Olá assinaturas disponíveis que você pode acessar.</span><span class="sxs-lookup"><span data-stu-id="6897b-142">One of hello simplest operations you can do is toolist hello available subscriptions that you can access.</span></span> <span data-ttu-id="6897b-143">Olá solicitação a seguir, você verá como token de acesso de saudação é passado como um cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="6897b-143">In hello following request, you see how hello access token is passed in as a header:</span></span>

<span data-ttu-id="6897b-144">(Substitua YOUR_ACCESS_TOKEN por seu Token de Acesso real.)</span><span class="sxs-lookup"><span data-stu-id="6897b-144">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="6897b-145">... e como resultado, você obtém uma lista de assinaturas que essa entidade de serviço é permitida tooaccess</span><span class="sxs-lookup"><span data-stu-id="6897b-145">... and as a result, you get a list of subscriptions that this service principal is allowed tooaccess</span></span>

<span data-ttu-id="6897b-146">(As IDs de Assinatura abaixo foram reduzidas para facilitar a leitura)</span><span class="sxs-lookup"><span data-stu-id="6897b-146">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="6897b-147">Listar todos os grupos de recursos em uma assinatura específica</span><span class="sxs-lookup"><span data-stu-id="6897b-147">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="6897b-148">Todos os recursos disponíveis com hello APIs do Gerenciador de recursos são aninhados dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6897b-148">All resources available with hello Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="6897b-149">Você pode consultar o Gerenciador de recursos para grupos de recursos existentes em sua assinatura usando Olá solicitação HTTP GET a seguir.</span><span class="sxs-lookup"><span data-stu-id="6897b-149">You can query Resource Manager for existing resource groups in your subscription using hello following HTTP GET request.</span></span> <span data-ttu-id="6897b-150">Observe como ID de assinatura de saudação é passado como parte da URL Olá neste momento.</span><span class="sxs-lookup"><span data-stu-id="6897b-150">Notice how hello subscription ID is passed in as part of hello URL this time.</span></span>

<span data-ttu-id="6897b-151">(Substitua YOUR_ACCESS_TOKEN e SUBSCRIPTION_ID pelo seu token de acesso e ID de assinatura)</span><span class="sxs-lookup"><span data-stu-id="6897b-151">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="6897b-152">Olá resposta você obter depende se você tiver grupos de recursos definidos e nesse caso, a quantidade.</span><span class="sxs-lookup"><span data-stu-id="6897b-152">hello response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="6897b-153">(As IDs de Assinatura abaixo foram reduzidas para facilitar a leitura)</span><span class="sxs-lookup"><span data-stu-id="6897b-153">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="6897b-154">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="6897b-154">Create a resource group</span></span>
<span data-ttu-id="6897b-155">Até agora, nós já foi consultando apenas Olá APIs do Gerenciador de recursos para obter informações.</span><span class="sxs-lookup"><span data-stu-id="6897b-155">So far, we've only been querying hello Resource Manager APIs for information.</span></span> <span data-ttu-id="6897b-156">É hora de criar alguns recursos e vamos começar hello mais simples de todos eles, um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="6897b-156">It's time we create some resources, and let's start by hello simplest of them all, a resource group.</span></span> <span data-ttu-id="6897b-157">Olá solicitação HTTP a seguir cria um grupo de recursos em um região/local de sua escolha e adiciona uma marca tooit.</span><span class="sxs-lookup"><span data-stu-id="6897b-157">hello following HTTP request creates a resource group in a region/location of your choice, and adds a tag tooit.</span></span>

<span data-ttu-id="6897b-158">(Substitua YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME real Token de acesso, ID da assinatura e nome de grupo de recursos que você deseja toocreate do hello)</span><span class="sxs-lookup"><span data-stu-id="6897b-158">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of hello Resource Group you want toocreate)</span></span>

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

<span data-ttu-id="6897b-159">Se for bem-sucedido, você receberá uma resposta semelhante toohello resposta a seguir:</span><span class="sxs-lookup"><span data-stu-id="6897b-159">If successful, you get a response that is similar toohello following response:</span></span>

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

<span data-ttu-id="6897b-160">Você criou um grupo de recursos no Azure com êxito.</span><span class="sxs-lookup"><span data-stu-id="6897b-160">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="6897b-161">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="6897b-161">Congratulations!</span></span>

### <a name="deploy-resources-tooa-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="6897b-162">Implantar grupo de recursos tooa de recursos usando um modelo do Gerenciador de recursos</span><span class="sxs-lookup"><span data-stu-id="6897b-162">Deploy resources tooa resource group using a Resource Manager Template</span></span>
<span data-ttu-id="6897b-163">Com o Resource Manager, você pode implantar os recursos usando modelos.</span><span class="sxs-lookup"><span data-stu-id="6897b-163">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="6897b-164">Um modelo define vários recursos e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="6897b-164">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="6897b-165">Para essa seção, vamos supor estiver familiarizado com modelos do Gerenciador de recursos, e apenas exibir como toomake Olá API chamar toostart implantação.</span><span class="sxs-lookup"><span data-stu-id="6897b-165">For this section, we assume you are familiar with Resource Manager templates, and we just show you how toomake hello API call toostart deployment.</span></span> <span data-ttu-id="6897b-166">Para obter mais informações sobre como construir modelos, consulte [Criação de Modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="6897b-166">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="6897b-167">Implantação de um modelo não diferem muito toohow chamar outras APIs.</span><span class="sxs-lookup"><span data-stu-id="6897b-167">Deployment of a template doesn't differ much toohow you call other APIs.</span></span> <span data-ttu-id="6897b-168">Um aspecto importante é que a implantação de um modelo pode levar muito tempo.</span><span class="sxs-lookup"><span data-stu-id="6897b-168">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="6897b-169">chamada Hello API retorna apenas e é o tooyou como desenvolvedor tooquery status da saudação implantação toofind out quando Olá implantação é feita.</span><span class="sxs-lookup"><span data-stu-id="6897b-169">hello API call just returns, and it's up tooyou as developer tooquery for status of hello deployment toofind out when hello deployment is done.</span></span> <span data-ttu-id="6897b-170">Para obter mais informações, consulte [Rastrear operações assíncronas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="6897b-170">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="6897b-171">Neste exemplo, usaremos um modelo exposto publicamente disponível no [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="6897b-171">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="6897b-172">modelo de saudação que usamos implanta uma região do VM Linux toohello Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="6897b-172">hello template we use deploys a Linux VM toohello West US region.</span></span> <span data-ttu-id="6897b-173">Embora esse exemplo usa um modelo disponível em um repositório público como GitHub, você pode passar em vez disso, modelo completo hello como parte da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6897b-173">Even though this example uses a template available in a public repository like GitHub, you can instead pass hello full template as part of hello request.</span></span> <span data-ttu-id="6897b-174">Observe que podemos fornecer valores de parâmetro na solicitação de saudação que são utilizados em Olá implantados modelo.</span><span class="sxs-lookup"><span data-stu-id="6897b-174">Note that we provide parameter values in hello request that are used inside hello deployed template.</span></span>

<span data-ttu-id="6897b-175">(Substitua SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD e DNS_NAME_FOR_PUBLIC_IP toovalues apropriado para a sua solicitação)</span><span class="sxs-lookup"><span data-stu-id="6897b-175">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP toovalues appropriate for your request)</span></span>

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

<span data-ttu-id="6897b-176">resposta JSON longa Olá para esta solicitação foi omitido tooimprove legibilidade desta documentação.</span><span class="sxs-lookup"><span data-stu-id="6897b-176">hello long JSON response for this request has been omitted tooimprove readability of this documentation.</span></span> <span data-ttu-id="6897b-177">resposta de saudação contém informações sobre a implantação de modelo de saudação que você criou.</span><span class="sxs-lookup"><span data-stu-id="6897b-177">hello response contains information about hello templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="6897b-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6897b-178">Next steps</span></span>

- <span data-ttu-id="6897b-179">toolearn sobre como lidar com operações assíncronas de REST, consulte [controlar operações assíncronas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="6897b-179">toolearn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
