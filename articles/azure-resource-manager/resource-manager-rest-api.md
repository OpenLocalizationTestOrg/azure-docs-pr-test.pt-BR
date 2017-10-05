---
title: APIs REST do Gerenciador de Recursos| Microsoft Docs
description: "Uma visão geral dos exemplos de autenticação e de uso de APIs REST do Gerenciador de Recursos"
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
ms.openlocfilehash: 2f7ba23775545637de865f9ef63680ae22c62164
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="resource-manager-rest-apis"></a><span data-ttu-id="4180a-103">APIs REST do Gerenciador de Recursos</span><span class="sxs-lookup"><span data-stu-id="4180a-103">Resource Manager REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="4180a-104">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="4180a-104">Azure PowerShell</span></span>](powershell-azure-resource-manager.md)
> * [<span data-ttu-id="4180a-105">CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="4180a-105">Azure CLI</span></span>](xplat-cli-azure-resource-manager.md)
> * [<span data-ttu-id="4180a-106">Portal</span><span class="sxs-lookup"><span data-stu-id="4180a-106">Portal</span></span>](resource-group-portal.md) 
> * [<span data-ttu-id="4180a-107">API REST</span><span class="sxs-lookup"><span data-stu-id="4180a-107">REST API</span></span>](resource-manager-rest-api.md)
> 
> 

<span data-ttu-id="4180a-108">Por trás de todas as chamadas ao Azure Resource Manager, de cada modelo implantado e de todas as contas de armazenamento configuradas há uma ou mais chamadas à API RESTful do Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4180a-108">Behind every call to Azure Resource Manager, behind every deployed template, behind every configured storage account there are one or more calls to the Azure Resource Manager's RESTful API.</span></span> <span data-ttu-id="4180a-109">Este tópico é dedicado a essas APIs e como você pode chamá-las sem precisar usar o SDK.</span><span class="sxs-lookup"><span data-stu-id="4180a-109">This topic is devoted to those APIs and how you can call them without using any SDK at all.</span></span> <span data-ttu-id="4180a-110">Essa abordagem pode ser útil se quiser ter controle total sobre todas as solicitações no Azure ou se o SDK para seu idioma não estiver disponível ou não der suporte às operações que você precisa.</span><span class="sxs-lookup"><span data-stu-id="4180a-110">This approach is useful if you want full control of requests to Azure, or if the SDK for your preferred language is not available or doesn't support the operations you need.</span></span>

<span data-ttu-id="4180a-111">Este artigo não abordará todas as APIs expostas no Azure, mas sim usará algumas operações como exemplo de como você pode conectá-las.</span><span class="sxs-lookup"><span data-stu-id="4180a-111">This article does not go through every API that is exposed in Azure, but rather uses some operations as examples of how you connect to them.</span></span> <span data-ttu-id="4180a-112">Se você compreender os fundamentos básicos, poderá ler a [Referência das APIs REST do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/) para encontrar informações detalhadas sobre como usar o restante das APIs.</span><span class="sxs-lookup"><span data-stu-id="4180a-112">After you understand the basics, you can read the [Azure Resource Manager REST API Reference](https://docs.microsoft.com/rest/api/resources/) to find detailed information on how to use the rest of the APIs.</span></span>

## <a name="authentication"></a><span data-ttu-id="4180a-113">Autenticação</span><span class="sxs-lookup"><span data-stu-id="4180a-113">Authentication</span></span>
<span data-ttu-id="4180a-114">A autenticação para o Resource Manager é tratada pelo Azure Active Directory (AD).</span><span class="sxs-lookup"><span data-stu-id="4180a-114">Authentication for Resource Manager is handled by Azure Active Directory (AD).</span></span> <span data-ttu-id="4180a-115">Para se conectar a uma API, você primeiro precisa se autenticar com o Azure AD para receber um token de autenticação que poderá ser passado em cada solicitação.</span><span class="sxs-lookup"><span data-stu-id="4180a-115">To connect to any API, you first need to authenticate with Azure AD to receive an authentication token that you can pass on to every request.</span></span> <span data-ttu-id="4180a-116">Como estamos descrevendo uma chamada simples diretamente para as APIs REST, presumimos que você não deseja autenticar quando um nome de usuário e senha forem solicitados.</span><span class="sxs-lookup"><span data-stu-id="4180a-116">As we are describing a pure call directly to the REST APIs, we assume that you don't want to authenticate by being prompted for a username and password.</span></span> <span data-ttu-id="4180a-117">Também supomos que você não está usando mecanismos de autenticação de dois fatores.</span><span class="sxs-lookup"><span data-stu-id="4180a-117">We also assume you are not using two factor authentication mechanisms.</span></span> <span data-ttu-id="4180a-118">Portanto, criaremos o que chamamos de Aplicativo do Azure AD e uma entidade de serviço que será usada para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="4180a-118">Therefore, we create what is called an Azure AD Application and a service principal that are used to log in.</span></span> <span data-ttu-id="4180a-119">Mas lembre-se de que o Azure AD dá suporte a vários procedimentos de autenticação e todos eles podem ser usados para recuperar esse token de autenticação necessário para solicitações subsequentes de API.</span><span class="sxs-lookup"><span data-stu-id="4180a-119">But remember that Azure AD support several authentication procedures and all of them could be used to retrieve that authentication token that we need for subsequent API requests.</span></span>
<span data-ttu-id="4180a-120">Siga [Criar aplicativo do Azure AD e Entidade de Serviço](resource-group-create-service-principal-portal.md) para obter etapas detalhadas.</span><span class="sxs-lookup"><span data-stu-id="4180a-120">Follow [Create Azure AD Application and Service Principal](resource-group-create-service-principal-portal.md) for step by step instructions.</span></span>

### <a name="generating-an-access-token"></a><span data-ttu-id="4180a-121">Gerando um token de acesso</span><span class="sxs-lookup"><span data-stu-id="4180a-121">Generating an Access Token</span></span>
<span data-ttu-id="4180a-122">A autenticação no Azure AD é feita chamando o Azure AD localizado em login.microsoftonline.com.</span><span class="sxs-lookup"><span data-stu-id="4180a-122">Authentication against Azure AD is done by calling out to Azure AD, located at login.microsoftonline.com.</span></span> <span data-ttu-id="4180a-123">Para autenticar, você precisa ter as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="4180a-123">To authenticate, you need to have the following information:</span></span>

* <span data-ttu-id="4180a-124">A ID do Locatário do Azure AD (o nome deste Azure AD que você está usando para fazer logon, geralmente o mesmo da sua empresa, mas não necessariamente)</span><span class="sxs-lookup"><span data-stu-id="4180a-124">Azure AD Tenant ID (the name of that Azure AD you are using to log in, often the same as your company but not necessary)</span></span>
* <span data-ttu-id="4180a-125">ID do Aplicativo (obtida durante a etapa de criação do aplicativo do Azure AD)</span><span class="sxs-lookup"><span data-stu-id="4180a-125">Application ID (taken during the Azure AD application creation step)</span></span>
* <span data-ttu-id="4180a-126">Senha (que você selecionou ao criar o Aplicativo do Azure AD)</span><span class="sxs-lookup"><span data-stu-id="4180a-126">Password (that you selected while creating the Azure AD Application)</span></span>

<span data-ttu-id="4180a-127">Na solicitação HTTP a seguir, lembre-se de substituir “ID de Locatário do Azure AD”, “ID do Aplicativo” e “Senha” pelos valores corretos.</span><span class="sxs-lookup"><span data-stu-id="4180a-127">In the following HTTP request, make sure to replace "Azure AD Tenant ID", "Application ID" and "Password" with the correct values.</span></span>

<span data-ttu-id="4180a-128">**Solicitação HTTP Genérica:**</span><span class="sxs-lookup"><span data-stu-id="4180a-128">**Generic HTTP Request:**</span></span>

```HTTP
POST /<Azure AD Tenant ID>/oauth2/token?api-version=1.0 HTTP/1.1 HTTP/1.1
Host: login.microsoftonline.com
Cache-Control: no-cache
Content-Type: application/x-www-form-urlencoded

grant_type=client_credentials&resource=https%3A%2F%2Fmanagement.core.windows.net%2F&client_id=<Application ID>&client_secret=<Password>
```

<span data-ttu-id="4180a-129">... resultará (se a autenticação for bem-sucedida) em uma resposta semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="4180a-129">... will (if authentication succeeds) result in a response similar to the following response:</span></span>

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
<span data-ttu-id="4180a-130">(O access_token na resposta acima foi reduzido para elevar a legibilidade)</span><span class="sxs-lookup"><span data-stu-id="4180a-130">(The access_token in the preceding response have been shortened to increase readability)</span></span>

<span data-ttu-id="4180a-131">**Gerando um token de acesso usando Bash:**</span><span class="sxs-lookup"><span data-stu-id="4180a-131">**Generating access token using Bash:**</span></span>

```console
curl -X POST -H "Content-Type: application/x-www-form-urlencoded" -d "grant_type=client_credentials&resource=https://management.core.windows.net/&client_id=<application id>&client_secret=<password you selected for authentication>" https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0
```

<span data-ttu-id="4180a-132">**Gerando um token de acesso usando o PowerShell:**</span><span class="sxs-lookup"><span data-stu-id="4180a-132">**Generating access token using PowerShell:**</span></span>

```powershell
Invoke-RestMethod -Uri https://login.microsoftonline.com/<Azure AD Tenant ID>/oauth2/token?api-version=1.0 -Method Post
 -Body @{"grant_type" = "client_credentials"; "resource" = "https://management.core.windows.net/"; "client_id" = "<application id>"; "client_secret" = "<password you selected for authentication>" }
```

<span data-ttu-id="4180a-133">A resposta contém um token de acesso, informações sobre o tempo de validade desse token e sobre quais recursos podem ser usados com o token.</span><span class="sxs-lookup"><span data-stu-id="4180a-133">The response contains an access token, information about how long that token is valid, and information about what resource you can use that token for.</span></span>
<span data-ttu-id="4180a-134">O token de acesso que você recebeu na chamada HTTP anterior deve ser passado em para todas as solicitações para a API do Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="4180a-134">The access token you received in the previous HTTP call must be passed in for all request to the Resource Manager API.</span></span> <span data-ttu-id="4180a-135">Você pode passá-lo como um valor de cabeçalho denominado “Autorização” com o valor “Portador YOUR_ACCESS_TOKEN”.</span><span class="sxs-lookup"><span data-stu-id="4180a-135">You pass it as a header value named "Authorization" with the value "Bearer YOUR_ACCESS_TOKEN".</span></span> <span data-ttu-id="4180a-136">Observe o espaço entre “Portador” e seu token de acesso.</span><span class="sxs-lookup"><span data-stu-id="4180a-136">Notice the space between "Bearer" and your access token.</span></span>

<span data-ttu-id="4180a-137">Como você pode ver no Resultado HTTP acima, o token é válido por um período durante o qual você deve armazená-lo em cache e reutilizá-lo.</span><span class="sxs-lookup"><span data-stu-id="4180a-137">As you can see from the above HTTP Result, the token is valid for a specific period of time during which you should cache and reuse that same token.</span></span> <span data-ttu-id="4180a-138">Mesmo se fosse possível autenticar no Azure AD para cada chamada à API, isso seria muito ineficiente.</span><span class="sxs-lookup"><span data-stu-id="4180a-138">Even if it is possible to authenticate against Azure AD for each API call, it would be highly inefficient.</span></span>

## <a name="calling-resource-manager-rest-apis"></a><span data-ttu-id="4180a-139">Chamar APIs REST do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4180a-139">Calling Resource Manager REST APIs</span></span>
<span data-ttu-id="4180a-140">Este tópico usa apenas algumas APIs para explicar o uso básico das operações REST.</span><span class="sxs-lookup"><span data-stu-id="4180a-140">This topic only uses a few APIs to explain the basic usage of the REST operations.</span></span> <span data-ttu-id="4180a-141">Para obter informações sobre todas as operações, consulte [Referência das APIs REST do Azure Resource Manager](https://docs.microsoft.com/rest/api/resources/).</span><span class="sxs-lookup"><span data-stu-id="4180a-141">For information about all the operations, see [Azure Resource Manager REST APIs](https://docs.microsoft.com/rest/api/resources/).</span></span>

### <a name="list-all-subscriptions"></a><span data-ttu-id="4180a-142">Listar todas as assinaturas</span><span class="sxs-lookup"><span data-stu-id="4180a-142">List all subscriptions</span></span>
<span data-ttu-id="4180a-143">Listar as assinaturas disponíveis que você pode acessar é uma das operações mais simples de realizar.</span><span class="sxs-lookup"><span data-stu-id="4180a-143">One of the simplest operations you can do is to list the available subscriptions that you can access.</span></span> <span data-ttu-id="4180a-144">Na solicitação a seguir, você pode ver como o token de acesso é passado como um cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="4180a-144">In the following request, you see how the access token is passed in as a header:</span></span>

<span data-ttu-id="4180a-145">(Substitua YOUR_ACCESS_TOKEN por seu Token de Acesso real.)</span><span class="sxs-lookup"><span data-stu-id="4180a-145">(Replace YOUR_ACCESS_TOKEN with your actual Access Token.)</span></span>

```HTTP
GET /subscriptions?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="4180a-146">... e, como resultado, você obterá uma lista de assinaturas que essa entidade de serviço tem permissão para acessar</span><span class="sxs-lookup"><span data-stu-id="4180a-146">... and as a result, you get a list of subscriptions that this service principal is allowed to access</span></span>

<span data-ttu-id="4180a-147">(As IDs de Assinatura abaixo foram reduzidas para facilitar a leitura)</span><span class="sxs-lookup"><span data-stu-id="4180a-147">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="list-all-resource-groups-in-a-specific-subscription"></a><span data-ttu-id="4180a-148">Listar todos os grupos de recursos em uma assinatura específica</span><span class="sxs-lookup"><span data-stu-id="4180a-148">List all resource groups in a specific subscription</span></span>
<span data-ttu-id="4180a-149">Todos os recursos disponíveis com as APIs do Resource Manager estão aninhados dentro de um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4180a-149">All resources available with the Resource Manager APIs are nested inside a resource group.</span></span> <span data-ttu-id="4180a-150">Você pode consultar grupos de recursos existentes do Resource Manager em sua assinatura usando a seguinte solicitação HTTP GET.</span><span class="sxs-lookup"><span data-stu-id="4180a-150">You can query Resource Manager for existing resource groups in your subscription using the following HTTP GET request.</span></span> <span data-ttu-id="4180a-151">Observe como a ID da assinatura é passada como parte da URL dessa vez.</span><span class="sxs-lookup"><span data-stu-id="4180a-151">Notice how the subscription ID is passed in as part of the URL this time.</span></span>

<span data-ttu-id="4180a-152">(Substitua YOUR_ACCESS_TOKEN e SUBSCRIPTION_ID pelo seu token de acesso e ID de assinatura)</span><span class="sxs-lookup"><span data-stu-id="4180a-152">(Replace YOUR_ACCESS_TOKEN and SUBSCRIPTION_ID with your actual access token and subscription ID)</span></span>

```HTTP
GET /subscriptions/SUBSCRIPTION_ID/resourcegroups?api-version=2015-01-01 HTTP/1.1
Host: management.azure.com
Authorization: Bearer YOUR_ACCESS_TOKEN
Content-Type: application/json
```

<span data-ttu-id="4180a-153">A resposta dependerá de você ter ou não grupos de recursos definidos e, se tiver, quantos.</span><span class="sxs-lookup"><span data-stu-id="4180a-153">The response you get depends on whether you have any resource groups defined and if so, how many.</span></span>

<span data-ttu-id="4180a-154">(As IDs de Assinatura abaixo foram reduzidas para facilitar a leitura)</span><span class="sxs-lookup"><span data-stu-id="4180a-154">(Subscription IDs have been shortened for readability)</span></span>

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

### <a name="create-a-resource-group"></a><span data-ttu-id="4180a-155">Criar um grupo de recursos</span><span class="sxs-lookup"><span data-stu-id="4180a-155">Create a resource group</span></span>
<span data-ttu-id="4180a-156">Até agora, consultamos apenas APIs do Resource Manager para obter informações.</span><span class="sxs-lookup"><span data-stu-id="4180a-156">So far, we've only been querying the Resource Manager APIs for information.</span></span> <span data-ttu-id="4180a-157">É hora criamos alguns recursos e vamos começar pelo mais simples de todos, um grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="4180a-157">It's time we create some resources, and let's start by the simplest of them all, a resource group.</span></span> <span data-ttu-id="4180a-158">A solicitação HTTP a seguir cria um grupo de recursos em um região/local de sua escolha e adiciona uma marcação a ele.</span><span class="sxs-lookup"><span data-stu-id="4180a-158">The following HTTP request creates a resource group in a region/location of your choice, and adds a tag to it.</span></span>

<span data-ttu-id="4180a-159">(Substitua YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME pelo Token de Acesso e ID de Assinatura reais e pelo nome do Grupo de Recursos que deseja criar)</span><span class="sxs-lookup"><span data-stu-id="4180a-159">(Replace YOUR_ACCESS_TOKEN, SUBSCRIPTION_ID, RESOURCE_GROUP_NAME with your actual Access Token, Subscription ID and name of the Resource Group you want to create)</span></span>

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

<span data-ttu-id="4180a-160">Se o comando tiver êxito, você receberá uma resposta semelhante à seguinte:</span><span class="sxs-lookup"><span data-stu-id="4180a-160">If successful, you get a response that is similar to the following response:</span></span>

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

<span data-ttu-id="4180a-161">Você criou um grupo de recursos no Azure com êxito.</span><span class="sxs-lookup"><span data-stu-id="4180a-161">You've successfully created a resource group in Azure.</span></span> <span data-ttu-id="4180a-162">Parabéns!</span><span class="sxs-lookup"><span data-stu-id="4180a-162">Congratulations!</span></span>

### <a name="deploy-resources-to-a-resource-group-using-a-resource-manager-template"></a><span data-ttu-id="4180a-163">Implantar recursos em um grupo de recursos usando um Modelo do Resource Manager</span><span class="sxs-lookup"><span data-stu-id="4180a-163">Deploy resources to a resource group using a Resource Manager Template</span></span>
<span data-ttu-id="4180a-164">Com o Resource Manager, você pode implantar os recursos usando modelos.</span><span class="sxs-lookup"><span data-stu-id="4180a-164">With Resource Manager, you can deploy your resources using templates.</span></span> <span data-ttu-id="4180a-165">Um modelo define vários recursos e suas dependências.</span><span class="sxs-lookup"><span data-stu-id="4180a-165">A template defines several resources and their dependencies.</span></span> <span data-ttu-id="4180a-166">Para esta seção, vamos supor que você já esteja familiarizado com Modelos do Resource Manager e mostraremos como fazer uma chamada à API para iniciar uma implantação.</span><span class="sxs-lookup"><span data-stu-id="4180a-166">For this section, we assume you are familiar with Resource Manager templates, and we just show you how to make the API call to start deployment.</span></span> <span data-ttu-id="4180a-167">Para obter mais informações sobre como construir modelos, consulte [Criação de Modelos do Azure Resource Manager](resource-group-authoring-templates.md).</span><span class="sxs-lookup"><span data-stu-id="4180a-167">For more information about constructing templates, see [Authoring Azure Resource Manager templates](resource-group-authoring-templates.md).</span></span>

<span data-ttu-id="4180a-168">A implantação de um modelo de não é muito diferente da ação de chamar outras APIs.</span><span class="sxs-lookup"><span data-stu-id="4180a-168">Deployment of a template doesn't differ much to how you call other APIs.</span></span> <span data-ttu-id="4180a-169">Um aspecto importante é que a implantação de um modelo pode levar muito tempo.</span><span class="sxs-lookup"><span data-stu-id="4180a-169">One important aspect is that deployment of a template can take quite a long time.</span></span> <span data-ttu-id="4180a-170">A chamada à API apenas retorna, cabendo a você como desenvolvedor consultar o status da implantação para saber quando ela foi concluída.</span><span class="sxs-lookup"><span data-stu-id="4180a-170">The API call just returns, and it's up to you as developer to query for status of the deployment to find out when the deployment is done.</span></span> <span data-ttu-id="4180a-171">Para obter mais informações, consulte [Rastrear operações assíncronas de Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="4180a-171">For more information, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>

<span data-ttu-id="4180a-172">Neste exemplo, usaremos um modelo exposto publicamente disponível no [GitHub](https://github.com/Azure/azure-quickstart-templates).</span><span class="sxs-lookup"><span data-stu-id="4180a-172">For this example, we use a publicly exposed template available on [GitHub](https://github.com/Azure/azure-quickstart-templates).</span></span> <span data-ttu-id="4180a-173">O modelo que usamos implanta uma VM Linux para a região Oeste dos EUA.</span><span class="sxs-lookup"><span data-stu-id="4180a-173">The template we use deploys a Linux VM to the West US region.</span></span> <span data-ttu-id="4180a-174">Embora esse exemplo use o modelo disponível em um repositório público como o GitHub, você também pode passar o modelo completo como parte da solicitação.</span><span class="sxs-lookup"><span data-stu-id="4180a-174">Even though this example uses a template available in a public repository like GitHub, you can instead pass the full template as part of the request.</span></span> <span data-ttu-id="4180a-175">Observe que fornecemos valores de parâmetro como parte da solicitação que serão usados dentro do modelo implantado.</span><span class="sxs-lookup"><span data-stu-id="4180a-175">Note that we provide parameter values in the request that are used inside the deployed template.</span></span>

<span data-ttu-id="4180a-176">(Substitua SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD e DNS_NAME_FOR_PUBLIC_IP pelos valores apropriados para sua solicitação)</span><span class="sxs-lookup"><span data-stu-id="4180a-176">(Replace SUBSCRIPTION_ID, RESOURCE_GROUP_NAME, DEPLOYMENT_NAME, YOUR_ACCESS_TOKEN, GLOBALY_UNIQUE_STORAGE_ACCOUNT_NAME, ADMIN_USER_NAME, ADMIN_PASSWORD and DNS_NAME_FOR_PUBLIC_IP to values appropriate for your request)</span></span>

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

<span data-ttu-id="4180a-177">A resposta JSON longa para essa solicitação foi omitida para melhorar a legibilidade deste documento.</span><span class="sxs-lookup"><span data-stu-id="4180a-177">The long JSON response for this request has been omitted to improve readability of this documentation.</span></span> <span data-ttu-id="4180a-178">A resposta contém informações sobre a implantação do modelo que você criou.</span><span class="sxs-lookup"><span data-stu-id="4180a-178">The response contains information about the templated deployment that you created.</span></span>

## <a name="next-steps"></a><span data-ttu-id="4180a-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4180a-179">Next steps</span></span>

- <span data-ttu-id="4180a-180">Para saber mais sobre como lidar com operações assíncronas de REST, confira [Rastrear operações assíncronas do Azure](resource-manager-async-operations.md).</span><span class="sxs-lookup"><span data-stu-id="4180a-180">To learn about handling asynchronous REST operations, see [Track asynchronous Azure operations](resource-manager-async-operations.md).</span></span>
