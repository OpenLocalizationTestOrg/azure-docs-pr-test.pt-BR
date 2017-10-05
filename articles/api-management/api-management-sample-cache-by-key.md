---
title: Cache personalizado no Gerenciamento de API do Azure
description: Saiba como armazenar em cache os itens por chave no gerenciamento de API do Azure
services: api-management
documentationcenter: 
author: darrelmiller
manager: erikre
editor: 
ms.assetid: 772bc8dd-5cda-41c4-95bf-b9f6f052bc85
ms.service: api-management
ms.devlang: dotnet
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 12/15/2016
ms.author: apimpm
ms.openlocfilehash: f5d5f44e34fbcd122a10be0ca5b3001760c4c64d
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="90ff5-103">Cache personalizado no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="90ff5-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="90ff5-104">O serviço de gerenciamento de API do Azure tem suporte interno para [Cache de resposta HTTP](api-management-howto-cache.md) usando a URL de recurso como chave.</span><span class="sxs-lookup"><span data-stu-id="90ff5-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using the resource URL as the key.</span></span> <span data-ttu-id="90ff5-105">A chave pode ser modificada por cabeçalhos de solicitação usando as propriedades do `vary-by` .</span><span class="sxs-lookup"><span data-stu-id="90ff5-105">The key can be modified by request headers using the `vary-by` properties.</span></span> <span data-ttu-id="90ff5-106">Isso é útil para armazenar em cache respostas HTTP inteiras (também conhecido como representações), mas às vezes é útil para armazenar apenas uma parte de uma representação.</span><span class="sxs-lookup"><span data-stu-id="90ff5-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful to just cache a portion of a representation.</span></span> <span data-ttu-id="90ff5-107">As novas políticas [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) e [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) fornecem a capacidade de armazenar e recuperar partes arbitrárias de dados de dentro das definições da política.</span><span class="sxs-lookup"><span data-stu-id="90ff5-107">The new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide the ability to store and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="90ff5-108">Essa capacidade também adiciona valor à política anteriormente introduzida [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) porque você agora pode armazenar em cache as respostas de serviços externos.</span><span class="sxs-lookup"><span data-stu-id="90ff5-108">This ability also adds value to the previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="90ff5-109">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="90ff5-109">Architecture</span></span>
<span data-ttu-id="90ff5-110">O serviço de Gerenciamento de API usa um cache de dados compartilhados por locatário para que, à medida que você escalar verticalmente para várias unidades, ainda tenha acesso ao mesmo dados em cache.</span><span class="sxs-lookup"><span data-stu-id="90ff5-110">API Management service uses a shared per-tenant data cache so that, as you scale up to multiple units you will still get access to the same cached data.</span></span> <span data-ttu-id="90ff5-111">No entanto, ao trabalhar com uma implantação de várias regiões, existem caches independentes dentro de cada uma das regiões.</span><span class="sxs-lookup"><span data-stu-id="90ff5-111">However, when working with a multi-region deployment there are independent caches within each of the regions.</span></span> <span data-ttu-id="90ff5-112">Por isso, é importante não tratar o cache como um armazenamento de dados, em que ele é a única fonte de alguma informação.</span><span class="sxs-lookup"><span data-stu-id="90ff5-112">Due to this, it is important to not treat the cache as a data store, where it is the only source of some piece of information.</span></span> <span data-ttu-id="90ff5-113">Se posteriormente você decidir se beneficiar da implantação de várias regiões, clientes com usuários que viajam podem perder o acesso aos dados armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="90ff5-113">If you did, and later decided to take advantage of the multi-region deployment, then customers with users that travel may lose access to that cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="90ff5-114">Cache de fragmento</span><span class="sxs-lookup"><span data-stu-id="90ff5-114">Fragment caching</span></span>
<span data-ttu-id="90ff5-115">Há alguns casos nos quais respostas sendo retornadas contêm uma parte dos dados que é cara de determinar e ainda permanece atualizada por um período razoável.</span><span class="sxs-lookup"><span data-stu-id="90ff5-115">There are certain cases where responses being returned contain some portion of data that is expensive to determine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="90ff5-116">Por exemplo, considere um serviço criado por uma companhia aérea que fornece informações relacionadas a reservas de voo, status de voo, etc. Se o usuário for um membro do programa de pontos da companhia aérea, ele também teria informações relacionadas ao seu status atual e milhas acumuladas.</span><span class="sxs-lookup"><span data-stu-id="90ff5-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If the user is a member of the airlines points program, they would also have information relating to their current status and mileage accumulated.</span></span> <span data-ttu-id="90ff5-117">Essas informações relacionadas ao usuário podem ser armazenadas em um sistema diferente, mas pode ser desejável incluí-las em respostas retornadas sobre reservas e o status de voo.</span><span class="sxs-lookup"><span data-stu-id="90ff5-117">This user-related information might be stored in a different system, but it may be desirable to include it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="90ff5-118">Isso pode ser feito usando um processo chamado cache fragmentado.</span><span class="sxs-lookup"><span data-stu-id="90ff5-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="90ff5-119">A representação principal pode ser retornada do servidor de origem usando algum tipo de token para indicar onde as informações relacionadas ao usuário devem ser inseridas.</span><span class="sxs-lookup"><span data-stu-id="90ff5-119">The primary representation can be returned from the origin server using some kind of token to indicate where the user-related information is to be inserted.</span></span> 

<span data-ttu-id="90ff5-120">Considere a seguinte resposta JSON de uma API de back-end.</span><span class="sxs-lookup"><span data-stu-id="90ff5-120">Consider the following JSON response from a backend API.</span></span>

```json
{
  "airline" : "Air Canada",
  "flightno" : "871",
  "status" : "ontime",
  "gate" : "B40",
  "terminal" : "2A",
  "userprofile" : "$userprofile$"
}  
```

<span data-ttu-id="90ff5-121">E o recursos secundário em `/userprofile/{userid}` , semelhante.</span><span class="sxs-lookup"><span data-stu-id="90ff5-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="90ff5-122">Para determinar as informações de usuário apropriadas a incluir, precisamos identificar quem é o usuário final.</span><span class="sxs-lookup"><span data-stu-id="90ff5-122">In order to determine the appropriate user information to include, we need to identify who the end user is.</span></span> <span data-ttu-id="90ff5-123">Esse mecanismo é dependente da implementação.</span><span class="sxs-lookup"><span data-stu-id="90ff5-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="90ff5-124">Por exemplo, estou usando a declaração `Subject` de um token `JWT`.</span><span class="sxs-lookup"><span data-stu-id="90ff5-124">As an example, I am using the `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="90ff5-125">Armazenamos o valor `enduserid` em uma variável de contexto para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="90ff5-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="90ff5-126">A próxima etapa é determinar se uma solicitação anterior já recuperou as informações do usuário e armazenou-a no cache.</span><span class="sxs-lookup"><span data-stu-id="90ff5-126">The next step is to determine if a previous request has already retrieved the user information and stored it in the cache.</span></span> <span data-ttu-id="90ff5-127">Para fazer isso, usamos a política `cache-lookup-value` .</span><span class="sxs-lookup"><span data-stu-id="90ff5-127">For this we use the `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="90ff5-128">Se não houver nenhuma entrada no cache que corresponda ao valor da chave, então, nenhuma variável de contexto `userprofile` será criada.</span><span class="sxs-lookup"><span data-stu-id="90ff5-128">If there is no entry in the cache that corresponds to the key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="90ff5-129">Podemos verificar o êxito da pesquisa usando a política de fluxo de controle `choose` .</span><span class="sxs-lookup"><span data-stu-id="90ff5-129">We check the success of the lookup using the `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If the userprofile context variable doesn’t exist, make an HTTP request to retrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="90ff5-130">Se a variável de contexto `userprofile` não existir, teremos de fazer uma solicitação HTTP para recuperá-la.</span><span class="sxs-lookup"><span data-stu-id="90ff5-130">If the `userprofile` context variable doesn’t exist, then we are going to have to make an HTTP request to retrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points to the profile for the current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="90ff5-131">Usamos o `enduserid` para construir a URL para o recurso de perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="90ff5-131">We use the `enduserid` to construct the URL to the user profile resource.</span></span> <span data-ttu-id="90ff5-132">Assim que tivermos a resposta, podemos extrair o texto do corpo de resposta e armazená-lo em uma variável de contexto.</span><span class="sxs-lookup"><span data-stu-id="90ff5-132">Once we have the response, we can pull the body text out of the response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="90ff5-133">Para evitar fazer essa solicitação HTTP novamente, quando o mesmo usuário fizer outra solicitação, podemos armazenar o perfil do usuário no cache.</span><span class="sxs-lookup"><span data-stu-id="90ff5-133">To avoid us having to make this HTTP request again, when the same user makes another request, we can store the user profile in the cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="90ff5-134">Armazenamos o valor em cache usando a mesma chave exata com qual tentamos originalmente recuperá-la.</span><span class="sxs-lookup"><span data-stu-id="90ff5-134">We store the value in the cache using the exact same key that we originally attempted to retrieve it with.</span></span> <span data-ttu-id="90ff5-135">A duração que escolhemos para armazenar o valor deve ser baseada na frequência das alterações e no nível de tolerância dos usuários a informações desatualizadas.</span><span class="sxs-lookup"><span data-stu-id="90ff5-135">The duration that we choose to store the value should be based on how often the information changes and how tolerant users are to out of date information.</span></span> 

<span data-ttu-id="90ff5-136">É importante perceber que recuperar do cache ainda é uma solicitação de rede fora do processo e, potencialmente, pode ainda adicionar dezenas de milissegundos à solicitação.</span><span class="sxs-lookup"><span data-stu-id="90ff5-136">It is important to realize that retrieving from the cache is still an out-of-process, network request and potentially can still add tens of milliseconds to the request.</span></span> <span data-ttu-id="90ff5-137">Os benefícios são fornecidos ao determinar que as informações de perfil do usuário demoram muito mais, devido à necessidade de fazer consultas em banco de dados de consultas ou agregar informações de vários back-ends.</span><span class="sxs-lookup"><span data-stu-id="90ff5-137">The benefits come when determining the user profile information takes significantly longer than that due to needing to do database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="90ff5-138">A etapa final do processo é atualizar a resposta retornada com nossas informações de perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="90ff5-138">The final step in the process is to update the returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="90ff5-139">Optei por incluir aspas como parte do token, para que, mesmo que a substituição não ocorra, a resposta seja um JSON válido.</span><span class="sxs-lookup"><span data-stu-id="90ff5-139">I chose to include the quotation marks as part of the token so that even when the replace doesn’t occur, the response was still valid JSON.</span></span> <span data-ttu-id="90ff5-140">Isso era, principalmente, para facilitar a depuração.</span><span class="sxs-lookup"><span data-stu-id="90ff5-140">This was primarily to make debugging easier.</span></span>

<span data-ttu-id="90ff5-141">Depois que você combina todas essas etapas, o resultado final é uma política semelhante à mostrada a seguir.</span><span class="sxs-lookup"><span data-stu-id="90ff5-141">Once you combine all these steps together, the end result is a policy that looks like the following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in the cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in the cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request to get user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points to the profile for the current end-user -->
                    <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),(string)context.Variables["enduserid"]).AbsoluteUri)</set-url>
                    <set-method>GET</set-method>
                </send-request>

                <!-- Store response body in context variable -->
                <set-variable
                  name="userprofile"
                  value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />

                <!-- Store result in cache -->
                <cache-store-value
                  key="@("userprofile-" + context.Variables["enduserid"])"
                  value="@((string)context.Variables["userprofile"])"
                  duration="100000" />
            </when>
        </choose>
        <base />
    </inbound>
    <outbound>
        <!-- Update response body with user profile-->
        <find-and-replace
              from='"$userprofile$"'
              to="@((string)context.Variables["userprofile"])" />
        <base />
    </outbound>
</policies>
```

<span data-ttu-id="90ff5-142">Essa abordagem de cache é usada principalmente em sites da Web em que o HTML é composto no lado do servidor para que possa ser renderizado como uma única página.</span><span class="sxs-lookup"><span data-stu-id="90ff5-142">This caching approach is primarily used in web sites where HTML is composed on the server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="90ff5-143">No entanto, ela também pode ser útil em APIs em que os clientes não podem realizar cache HTTP de cliente ou é desejável não colocar a responsabilidade no cliente.</span><span class="sxs-lookup"><span data-stu-id="90ff5-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not to put that responsibility on the client.</span></span>

<span data-ttu-id="90ff5-144">Esse tipo de cache de fragmento também pode ser feito nos servidores back-end da Web, usando um servidor de cache Redis, no entanto, o uso do serviço de gerenciamento de API para realizar esse trabalho é útil quando os fragmentos em cache são provenientes de back-ends diferentes das respostas principais.</span><span class="sxs-lookup"><span data-stu-id="90ff5-144">This same kind of fragment caching can also be done on the backend web servers using a Redis caching server, however, using the API Management service to perform this work is useful when the cached fragments are coming from different back-ends than the primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="90ff5-145">Controle de versão transparente</span><span class="sxs-lookup"><span data-stu-id="90ff5-145">Transparent versioning</span></span>
<span data-ttu-id="90ff5-146">É uma prática comum para várias versões de implementação diferentes de uma API, ter suporte a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="90ff5-146">It is common practice for multiple different implementation versions of an API to be supported at any one time.</span></span> <span data-ttu-id="90ff5-147">Isso, talvez, é para dar suporte a ambientes diferentes, como desenvolvimento, teste, produção, etc., ou pode dar suporte a versões mais antigas da API e dar tempo aos consumidores da API para migrarem para versões mais recentes.</span><span class="sxs-lookup"><span data-stu-id="90ff5-147">This is perhaps to support different environments, like dev, test, production, etc, or it may be to support older versions of the API to give time for API consumers to migrate to newer versions.</span></span> 

<span data-ttu-id="90ff5-148">Uma abordagem para lidar com isso, em vez de exigir que os desenvolvedores de cliente alterem as URLs de `/v1/customers` para `/v2/customers`, é armazenar dados de perfil do consumidor, cuja versão da API eles desejam usar e chamar a URL de back-end apropriada.</span><span class="sxs-lookup"><span data-stu-id="90ff5-148">One approach to handling this instead of requiring client developers to change the URLs from `/v1/customers` to `/v2/customers` is to store in the consumer’s profile data which version of the API they currently wish to use and call the appropriate backend URL.</span></span> <span data-ttu-id="90ff5-149">Para determinar a URL correta de back-end para chamar determinado cliente, é necessário consultar alguns dados de configuração.</span><span class="sxs-lookup"><span data-stu-id="90ff5-149">In order to determine the correct backend URL to call for a particular client, it is necessary to query some configuration data.</span></span> <span data-ttu-id="90ff5-150">Ao armazenar em cache esses dados de configuração, podemos minimizar a degradação do desempenho ao fazer essa pesquisa.</span><span class="sxs-lookup"><span data-stu-id="90ff5-150">By caching this configuration data, we can minimize the performance penalty of doing this lookup.</span></span>

<span data-ttu-id="90ff5-151">A primeira etapa é determinar o identificador usado para configurar a versão desejada.</span><span class="sxs-lookup"><span data-stu-id="90ff5-151">The first step is to determine the identifier used to configure the desired version.</span></span> <span data-ttu-id="90ff5-152">Neste exemplo, optei por associar a versão à chave de assinatura do produto.</span><span class="sxs-lookup"><span data-stu-id="90ff5-152">In this example, I chose to associate the version to the product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="90ff5-153">Em seguida, fazemos uma pesquisa no cache para ver se já recuperamos a versão de cliente desejada.</span><span class="sxs-lookup"><span data-stu-id="90ff5-153">We then do a cache lookup to see if we already have retrieved the desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="90ff5-154">Em seguida, verificamos se não a encontramos no cache.</span><span class="sxs-lookup"><span data-stu-id="90ff5-154">Then we check to see if we did not find it in the cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="90ff5-155">Se não, nós a recuperamos.</span><span class="sxs-lookup"><span data-stu-id="90ff5-155">If we didn’t then we go and retrieve it.</span></span>

```xml
<send-request
    mode="new"
    response-variable-name="clientconfiguresponse"
    timeout="10"
    ignore-error="true">
            <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
            <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="90ff5-156">Extraia o texto do corpo de resposta da resposta.</span><span class="sxs-lookup"><span data-stu-id="90ff5-156">Extract the response body text from the response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="90ff5-157">Armazene-o no cache para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="90ff5-157">Store it back in the cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="90ff5-158">E, finalmente, atualize a URL do back-end para selecionar a versão de serviço desejada pelo cliente.</span><span class="sxs-lookup"><span data-stu-id="90ff5-158">And finally update the back-end URL to select the version of the service desired by the client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="90ff5-159">A política completa é conforme segue.</span><span class="sxs-lookup"><span data-stu-id="90ff5-159">The completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in the cache, make a request for it and store it -->
    <choose>
        <when condition="@(!context.Variables.ContainsKey("clientversion"))">
            <send-request mode="new" response-variable-name="clientconfiguresponse" timeout="10" ignore-error="true">
                <set-url>@(new Uri(new Uri(context.Api.ServiceUrl.ToString() + "api/ClientConfig/"),(string)context.Variables["clientid"]).AbsoluteUri)</set-url>
                <set-method>GET</set-method>
            </send-request>
            <!-- Store response body in context variable -->
            <set-variable name="clientversion" value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
            <!-- Store result in cache -->
            <cache-store-value key="@("clientversion-" + context.Variables["clientid"])" value="@((string)context.Variables["clientversion"])" duration="100000" />
        </when>
    </choose>
    <set-backend-service base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
</inbound>
```

<span data-ttu-id="90ff5-160">Habilitar consumidores da API a controlar, de forma transparente, qual versão de back-end está sendo acessado por clientes sem a necessidade de atualizar e reimplantar clientes é uma solução elegante que resolve muitas preocupações de controle de versão de API.</span><span class="sxs-lookup"><span data-stu-id="90ff5-160">Enabling API consumers to transparently control which backend version is being accessed by clients without having to update and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="90ff5-161">Isolamento de locatário</span><span class="sxs-lookup"><span data-stu-id="90ff5-161">Tenant Isolation</span></span>
<span data-ttu-id="90ff5-162">Em implantações maiores, de vários locatários, algumas empresas criar grupos separados de locatários em implantações distintas do hardware de back-end.</span><span class="sxs-lookup"><span data-stu-id="90ff5-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="90ff5-163">Isso minimiza o número de clientes afetados por um problema de hardware no back-end.</span><span class="sxs-lookup"><span data-stu-id="90ff5-163">This minimizes the number of customers who are impacted by a hardware issue on the backend.</span></span> <span data-ttu-id="90ff5-164">Também permite que novas versões de software sejam implementadas em estágios.</span><span class="sxs-lookup"><span data-stu-id="90ff5-164">It also enables new software versions to be rolled out in stages.</span></span> <span data-ttu-id="90ff5-165">O ideal é que essa arquitetura de back-end seja transparente para os consumidores de API.</span><span class="sxs-lookup"><span data-stu-id="90ff5-165">Ideally this backend architecture should be transparent to API consumers.</span></span> <span data-ttu-id="90ff5-166">Isso pode ser obtido de forma semelhante ao controle de versão transparente porque baseia-se na mesma técnica de manipular a URL do back-end usando o estado de configuração por chave de API.</span><span class="sxs-lookup"><span data-stu-id="90ff5-166">This can be achieved in a similar way to transparent versioning because it is based on the same technique of manipulating the backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="90ff5-167">Em vez de retornar uma versão de preferência da API para cada chave de assinatura, você retornará um identificador que relaciona um locatário ao grupo de hardware atribuído.</span><span class="sxs-lookup"><span data-stu-id="90ff5-167">Instead of returning a preferred version of the API for each subscription key, you would return an identifier that relates a tenant to the assigned hardware group.</span></span> <span data-ttu-id="90ff5-168">Esse identificador pode ser usado para construir a URL de back-end apropriada.</span><span class="sxs-lookup"><span data-stu-id="90ff5-168">That identifier can be used to construct the appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="90ff5-169">Resumo</span><span class="sxs-lookup"><span data-stu-id="90ff5-169">Summary</span></span>
<span data-ttu-id="90ff5-170">A liberdade de usar o cache de gerenciamento de API do Azure para armazenar qualquer tipo de dados permite acesso eficiente aos dados de configuração que podem afetar a maneira pela qual uma solicitação de entrada é processada.</span><span class="sxs-lookup"><span data-stu-id="90ff5-170">The freedom to use the Azure API management cache for storing any kind of data enables efficient access to configuration data that can affect the way an inbound request is processed.</span></span> <span data-ttu-id="90ff5-171">Ele também pode ser usado para armazenar fragmentos de dados que podem aumentar as respostas retornadas de uma API de back-end.</span><span class="sxs-lookup"><span data-stu-id="90ff5-171">It can also be used to store data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="90ff5-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="90ff5-172">Next steps</span></span>
<span data-ttu-id="90ff5-173">Envie-nos seus comentários no thread de discussão para este tópico, se houver outros cenários que essas políticas habilitaram para você, ou se houver cenários que você gostaria de ter, mas não sente que é possível no momento.</span><span class="sxs-lookup"><span data-stu-id="90ff5-173">Please give us your feedback in the Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like to achieve but do not feel are currently possible.</span></span>

