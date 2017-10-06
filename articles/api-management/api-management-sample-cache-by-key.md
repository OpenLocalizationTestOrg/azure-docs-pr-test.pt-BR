---
title: aaaCustom cache no gerenciamento de API do Azure
description: Saiba como toocache itens por chave no gerenciamento de API do Azure
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
ms.openlocfilehash: 681380743c8c96af5d0a8e25948a8c0663e9fd35
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="custom-caching-in-azure-api-management"></a><span data-ttu-id="51cdb-103">Cache personalizado no Gerenciamento de API do Azure</span><span class="sxs-lookup"><span data-stu-id="51cdb-103">Custom caching in Azure API Management</span></span>
<span data-ttu-id="51cdb-104">Serviço de gerenciamento de API do Azure tem suporte interno para [cache de resposta HTTP](api-management-howto-cache.md) usando a URL de recurso hello como chave de saudação.</span><span class="sxs-lookup"><span data-stu-id="51cdb-104">Azure API Management service has built-in support for [HTTP response caching](api-management-howto-cache.md) using hello resource URL as hello key.</span></span> <span data-ttu-id="51cdb-105">Olá chave pode ser modificada por cabeçalhos de solicitação usando Olá `vary-by` propriedades.</span><span class="sxs-lookup"><span data-stu-id="51cdb-105">hello key can be modified by request headers using hello `vary-by` properties.</span></span> <span data-ttu-id="51cdb-106">Isso é útil para armazenar em cache respostas HTTP inteiras (também conhecido como representações), mas às vezes é útil toojust cache uma parte de uma representação.</span><span class="sxs-lookup"><span data-stu-id="51cdb-106">This is useful for caching entire HTTP responses (aka representations), but sometimes it is useful toojust cache a portion of a representation.</span></span> <span data-ttu-id="51cdb-107">Olá novo [valor de pesquisa de cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) e [valor do repositório de cache](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) políticas fornecem a capacidade de saudação toostore e recuperar partes arbitrárias de dados do grupo de definições de política.</span><span class="sxs-lookup"><span data-stu-id="51cdb-107">hello new [cache-lookup-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#GetFromCacheByKey) and [cache-store-value](https://msdn.microsoft.com/library/azure/dn894086.aspx#StoreToCacheByKey) policies provide hello ability toostore and retrieve arbitrary pieces of data from within policy definitions.</span></span> <span data-ttu-id="51cdb-108">Essa capacidade também adiciona valor toohello introduzida anteriormente [solicitação de envio](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) política porque você agora pode armazenar em cache respostas de serviços externos.</span><span class="sxs-lookup"><span data-stu-id="51cdb-108">This ability also adds value toohello previously introduced [send-request](https://msdn.microsoft.com/library/azure/dn894085.aspx#SendRequest) policy because you can now cache responses from external services.</span></span>

## <a name="architecture"></a><span data-ttu-id="51cdb-109">Arquitetura</span><span class="sxs-lookup"><span data-stu-id="51cdb-109">Architecture</span></span>
<span data-ttu-id="51cdb-110">Serviço de gerenciamento de API usa um cache de dados compartilhado por locatário para que, ao dimensionar unidades toomultiple você ainda terá acesso toohello mesmo dados armazenados em cache.</span><span class="sxs-lookup"><span data-stu-id="51cdb-110">API Management service uses a shared per-tenant data cache so that, as you scale up toomultiple units you will still get access toohello same cached data.</span></span> <span data-ttu-id="51cdb-111">No entanto, ao trabalhar com uma implantação de várias regiões são independentes caches dentro de cada uma das regiões de saudação.</span><span class="sxs-lookup"><span data-stu-id="51cdb-111">However, when working with a multi-region deployment there are independent caches within each of hello regions.</span></span> <span data-ttu-id="51cdb-112">Vencimento toothis, é importante toonot tratar cache hello como um repositório de dados, onde é a única fonte Olá de alguma informação.</span><span class="sxs-lookup"><span data-stu-id="51cdb-112">Due toothis, it is important toonot treat hello cache as a data store, where it is hello only source of some piece of information.</span></span> <span data-ttu-id="51cdb-113">Se você fez e posteriormente decidir tootake vantagem da implantação de várias regiões hello, os clientes com usuários que viajam poderão perder acesso toothat armazenado em cache dados.</span><span class="sxs-lookup"><span data-stu-id="51cdb-113">If you did, and later decided tootake advantage of hello multi-region deployment, then customers with users that travel may lose access toothat cached data.</span></span>

## <a name="fragment-caching"></a><span data-ttu-id="51cdb-114">Cache de fragmento</span><span class="sxs-lookup"><span data-stu-id="51cdb-114">Fragment caching</span></span>
<span data-ttu-id="51cdb-115">Há alguns casos onde as respostas que está sendo retornadas contêm uma parte dos dados que são caro toodetermine e ainda permanecem atualizada por um período de tempo razoável.</span><span class="sxs-lookup"><span data-stu-id="51cdb-115">There are certain cases where responses being returned contain some portion of data that is expensive toodetermine and yet remains fresh for a reasonable amount of time.</span></span> <span data-ttu-id="51cdb-116">Por exemplo, considere um serviço criado por uma companhia aérea que fornece informações relacionadas a reservas de voo, status de voo, etc. Se o usuário Olá é membro do programa de pontos de companhias aéreas hello, eles também teriam informações sobre o status atual de tootheir e quilometragem acumulados.</span><span class="sxs-lookup"><span data-stu-id="51cdb-116">As an example, consider a service built by an airline that provides information relating flight reservations, flight status, etc. If hello user is a member of hello airlines points program, they would also have information relating tootheir current status and mileage accumulated.</span></span> <span data-ttu-id="51cdb-117">Essas informações relacionadas ao usuário podem ser armazenadas em um sistema diferente, mas pode ser desejável tooinclude em respostas retornada sobre o status de voo e reservas.</span><span class="sxs-lookup"><span data-stu-id="51cdb-117">This user-related information might be stored in a different system, but it may be desirable tooinclude it in responses returned about flight status and reservations.</span></span> <span data-ttu-id="51cdb-118">Isso pode ser feito usando um processo chamado cache fragmentado.</span><span class="sxs-lookup"><span data-stu-id="51cdb-118">This can be done using a process called fragment caching.</span></span> <span data-ttu-id="51cdb-119">Olá representação primária pode ser retornada do servidor de origem hello usando algum tipo de token tooindicate onde informações relacionadas ao usuário de saudação são toobe inserido.</span><span class="sxs-lookup"><span data-stu-id="51cdb-119">hello primary representation can be returned from hello origin server using some kind of token tooindicate where hello user-related information is toobe inserted.</span></span> 

<span data-ttu-id="51cdb-120">Considere Olá seguindo a resposta JSON de uma API de back-end.</span><span class="sxs-lookup"><span data-stu-id="51cdb-120">Consider hello following JSON response from a backend API.</span></span>

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

<span data-ttu-id="51cdb-121">E o recursos secundário em `/userprofile/{userid}` , semelhante.</span><span class="sxs-lookup"><span data-stu-id="51cdb-121">And secondary resource at `/userprofile/{userid}` that looks like,</span></span>

```json
{ "username" : "Bob Smith", "Status" : "Gold" }
```

<span data-ttu-id="51cdb-122">Ordem toodetermine Olá usuário apropriado informações tooinclude, precisamos tooidentify que o usuário final de saudação.</span><span class="sxs-lookup"><span data-stu-id="51cdb-122">In order toodetermine hello appropriate user information tooinclude, we need tooidentify who hello end user is.</span></span> <span data-ttu-id="51cdb-123">Esse mecanismo é dependente da implementação.</span><span class="sxs-lookup"><span data-stu-id="51cdb-123">This mechanism is implementation dependent.</span></span> <span data-ttu-id="51cdb-124">Por exemplo, estou usando Olá `Subject` de declaração de um `JWT` token.</span><span class="sxs-lookup"><span data-stu-id="51cdb-124">As an example, I am using hello `Subject` claim of a `JWT` token.</span></span> 

```xml
<set-variable
  name="enduserid"
  value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />
```

<span data-ttu-id="51cdb-125">Armazenamos o valor `enduserid` em uma variável de contexto para uso posterior.</span><span class="sxs-lookup"><span data-stu-id="51cdb-125">We store this `enduserid` value in a context variable for later use.</span></span> <span data-ttu-id="51cdb-126">Olá próxima etapa é toodetermine se uma solicitação anterior já recuperar informações de saudação do usuário e armazená-lo em cache hello.</span><span class="sxs-lookup"><span data-stu-id="51cdb-126">hello next step is toodetermine if a previous request has already retrieved hello user information and stored it in hello cache.</span></span> <span data-ttu-id="51cdb-127">Para isso, usamos Olá `cache-lookup-value` política.</span><span class="sxs-lookup"><span data-stu-id="51cdb-127">For this we use hello `cache-lookup-value` policy.</span></span>

```xml
<cache-lookup-value
key="@("userprofile-" + context.Variables["enduserid"])"
variable-name="userprofile" />
```

<span data-ttu-id="51cdb-128">Se não houver nenhuma entrada no cache de saudação que corresponde o valor da chave toohello e não `userprofile` variável de contexto será criado.</span><span class="sxs-lookup"><span data-stu-id="51cdb-128">If there is no entry in hello cache that corresponds toohello key value, then no `userprofile` context variable will be created.</span></span> <span data-ttu-id="51cdb-129">Precisamos verificar o sucesso de saudação da pesquisa hello usando Olá `choose` política de fluxo de controle.</span><span class="sxs-lookup"><span data-stu-id="51cdb-129">We check hello success of hello lookup using hello `choose` control flow policy.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("userprofile"))">
        <!-- If hello userprofile context variable doesn’t exist, make an HTTP request tooretrieve it.  -->
    </when>
</choose>
```

<span data-ttu-id="51cdb-130">Se hello `userprofile` variável de contexto não existir, então, será contínuo toohave toomake um HTTP solicitação tooretrieve-lo.</span><span class="sxs-lookup"><span data-stu-id="51cdb-130">If hello `userprofile` context variable doesn’t exist, then we are going toohave toomake an HTTP request tooretrieve it.</span></span>

```xml
<send-request
  mode="new"
  response-variable-name="userprofileresponse"
  timeout="10"
  ignore-error="true">

  <!-- Build a URL that points toohello profile for hello current end-user -->
  <set-url>@(new Uri(new Uri("https://apimairlineapi.azurewebsites.net/UserProfile/"),
      (string)context.Variables["enduserid"]).AbsoluteUri)
  </set-url>
  <set-method>GET</set-method>
</send-request>
```

<span data-ttu-id="51cdb-131">Usamos Olá `enduserid` recurso de perfil de usuário tooconstruct Olá URL toohello.</span><span class="sxs-lookup"><span data-stu-id="51cdb-131">We use hello `enduserid` tooconstruct hello URL toohello user profile resource.</span></span> <span data-ttu-id="51cdb-132">Assim que tivermos resposta hello, podemos extrair texto Olá sem resposta hello e armazená-lo novamente em uma variável de contexto.</span><span class="sxs-lookup"><span data-stu-id="51cdb-132">Once we have hello response, we can pull hello body text out of hello response and store it back into a context variable.</span></span>

```xml
<set-variable
    name="userprofile"
    value="@(((IResponse)context.Variables["userprofileresponse"]).Body.As<string>())" />
```

<span data-ttu-id="51cdb-133">tooavoid tenhamos toomake essa solicitação HTTP novamente, ao mesmo usuário hello faz outra solicitação, que pode armazenar Olá perfil de usuário no cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="51cdb-133">tooavoid us having toomake this HTTP request again, when hello same user makes another request, we can store hello user profile in hello cache.</span></span>

```xml
<cache-store-value
    key="@("userprofile-" + context.Variables["enduserid"])"
    value="@((string)context.Variables["userprofile"])" duration="100000" />
```

<span data-ttu-id="51cdb-134">Armazenamos valor Olá no cache de saudação usando Olá exata mesma chave que tentamos originalmente tooretrieve com.</span><span class="sxs-lookup"><span data-stu-id="51cdb-134">We store hello value in hello cache using hello exact same key that we originally attempted tooretrieve it with.</span></span> <span data-ttu-id="51cdb-135">Olá duração, escolhemos o valor de saudação toostore deve ser baseada em frequência hello usuários como tolerante a falhas e alterações de informações são tooout de informações de data.</span><span class="sxs-lookup"><span data-stu-id="51cdb-135">hello duration that we choose toostore hello value should be based on how often hello information changes and how tolerant users are tooout of date information.</span></span> 

<span data-ttu-id="51cdb-136">É importante toorealize que recuperar do cache de saudação ainda é um fora do processo, a solicitação de rede e potencialmente ainda poderá adicionar dezenas de solicitação de toohello milissegundos.</span><span class="sxs-lookup"><span data-stu-id="51cdb-136">It is important toorealize that retrieving from hello cache is still an out-of-process, network request and potentially can still add tens of milliseconds toohello request.</span></span> <span data-ttu-id="51cdb-137">benefícios de saudação vir ao determinar informações de perfil de usuário Olá leva significativamente mais tempo do que o devido a consultas de banco de dados de toodo tooneeding ou agregar informações de vários back-ends.</span><span class="sxs-lookup"><span data-stu-id="51cdb-137">hello benefits come when determining hello user profile information takes significantly longer than that due tooneeding toodo database queries or aggregate information from multiple back-ends.</span></span>

<span data-ttu-id="51cdb-138">Olá, etapa final do processo de saudação é Olá tooupdate retornada uma resposta com nosso informações de perfil do usuário.</span><span class="sxs-lookup"><span data-stu-id="51cdb-138">hello final step in hello process is tooupdate hello returned response with our user profile information.</span></span>

```xml
<!-- Update response body with user profile-->
<find-and-replace
    from='"$userprofile$"'
    to="@((string)context.Variables["userprofile"])" />
```

<span data-ttu-id="51cdb-139">Escolhi tooinclude Olá aspas como parte do token Olá para que, mesmo quando não ocorre Olá replace, resposta Olá era JSON ainda é válido.</span><span class="sxs-lookup"><span data-stu-id="51cdb-139">I chose tooinclude hello quotation marks as part of hello token so that even when hello replace doesn’t occur, hello response was still valid JSON.</span></span> <span data-ttu-id="51cdb-140">Isso foi principalmente toomake depuração mais fácil.</span><span class="sxs-lookup"><span data-stu-id="51cdb-140">This was primarily toomake debugging easier.</span></span>

<span data-ttu-id="51cdb-141">Depois que você pode combinar todas essas etapas juntas, o resultado de final de saudação é uma política que se parece com hello seguindo um.</span><span class="sxs-lookup"><span data-stu-id="51cdb-141">Once you combine all these steps together, hello end result is a policy that looks like hello following one.</span></span>

```xml
<policies>
    <inbound>
        <!-- How you determine user identity is application dependent -->
        <set-variable
          name="enduserid"
          value="@(context.Request.Headers.GetValueOrDefault("Authorization","").Split(' ')[1].AsJwt()?.Subject)" />

        <!--Look for userprofile for this user in hello cache -->
        <cache-lookup-value
          key="@("userprofile-" + context.Variables["enduserid"])"
          variable-name="userprofile" />

        <!-- If we don’t find it in hello cache, make a request for it and store it -->
        <choose>
            <when condition="@(!context.Variables.ContainsKey("userprofile"))">
                <!-- Make HTTP request tooget user profile -->
                <send-request
                  mode="new"
                  response-variable-name="userprofileresponse"
                  timeout="10"
                  ignore-error="true">

                   <!-- Build a URL that points toohello profile for hello current end-user -->
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

<span data-ttu-id="51cdb-142">Essa abordagem de cache é usada principalmente em sites da web onde o HTML é composto no lado do servidor de saudação para que ele pode ser renderizado como uma única página.</span><span class="sxs-lookup"><span data-stu-id="51cdb-142">This caching approach is primarily used in web sites where HTML is composed on hello server side so that it can be rendered as a single page.</span></span> <span data-ttu-id="51cdb-143">No entanto, ele também pode ser útil para onde os clientes não é possível executar o cliente de APIs do lado do cache de HTTP ou é desejável não tooput essa responsabilidade no cliente de saudação.</span><span class="sxs-lookup"><span data-stu-id="51cdb-143">However, it can also be useful in APIs where clients cannot do client side HTTP caching or it is desirable not tooput that responsibility on hello client.</span></span>

<span data-ttu-id="51cdb-144">Esse tipo de cache de fragmento também pode ser feito nos servidores de web de back-end hello usando um servidor de cache de Redis, no entanto, usar tooperform de serviço de gerenciamento de API Olá esse trabalho é útil quando fragmentos Olá armazenados em cache são provenientes de back-ends diferentes que Olá respostas primárias.</span><span class="sxs-lookup"><span data-stu-id="51cdb-144">This same kind of fragment caching can also be done on hello backend web servers using a Redis caching server, however, using hello API Management service tooperform this work is useful when hello cached fragments are coming from different back-ends than hello primary responses.</span></span>

## <a name="transparent-versioning"></a><span data-ttu-id="51cdb-145">Controle de versão transparente</span><span class="sxs-lookup"><span data-stu-id="51cdb-145">Transparent versioning</span></span>
<span data-ttu-id="51cdb-146">É uma prática comum para várias versões diferentes de implementação de um toobe de API com suporte a qualquer momento.</span><span class="sxs-lookup"><span data-stu-id="51cdb-146">It is common practice for multiple different implementation versions of an API toobe supported at any one time.</span></span> <span data-ttu-id="51cdb-147">Essa é talvez toosupport diferentes ambientes, como desenvolvimento, teste, produção, etc., ou pode ser toosupport de versões mais antigas de tempo de toogive Olá API para as versões de API consumidores toomigrate toonewer.</span><span class="sxs-lookup"><span data-stu-id="51cdb-147">This is perhaps toosupport different environments, like dev, test, production, etc, or it may be toosupport older versions of hello API toogive time for API consumers toomigrate toonewer versions.</span></span> 

<span data-ttu-id="51cdb-148">Uma abordagem toohandling em vez de exigir saudação do cliente desenvolvedores toochange URLs de `/v1/customers` muito`/v2/customers` é toostore nos dados de perfil do consumidor Olá qual versão de API do hello eles atualmente deseja toouse e chamar hello URL de back-end.</span><span class="sxs-lookup"><span data-stu-id="51cdb-148">One approach toohandling this instead of requiring client developers toochange hello URLs from `/v1/customers` too`/v2/customers` is toostore in hello consumer’s profile data which version of hello API they currently wish toouse and call hello appropriate backend URL.</span></span> <span data-ttu-id="51cdb-149">Em ordem toodetermine Olá correto de back-end URL toocall para um determinado cliente, é necessário tooquery alguns dados de configuração.</span><span class="sxs-lookup"><span data-stu-id="51cdb-149">In order toodetermine hello correct backend URL toocall for a particular client, it is necessary tooquery some configuration data.</span></span> <span data-ttu-id="51cdb-150">Armazenando em cache esses dados de configuração, é possível minimizar penalidade de desempenho de saudação de fazer essa pesquisa.</span><span class="sxs-lookup"><span data-stu-id="51cdb-150">By caching this configuration data, we can minimize hello performance penalty of doing this lookup.</span></span>

<span data-ttu-id="51cdb-151">Olá primeira etapa é o identificador de saudação toodetermine usado versão desejada do tooconfigure hello.</span><span class="sxs-lookup"><span data-stu-id="51cdb-151">hello first step is toodetermine hello identifier used tooconfigure hello desired version.</span></span> <span data-ttu-id="51cdb-152">Neste exemplo, escolhi chave de assinatura de produto tooassociate Olá versão toohello.</span><span class="sxs-lookup"><span data-stu-id="51cdb-152">In this example, I chose tooassociate hello version toohello product subscription key.</span></span> 

```xml
<set-variable name="clientid" value="@(context.Subscription.Key)" />
```

<span data-ttu-id="51cdb-153">Em seguida, fazemos uma toosee de pesquisa do cache se já recuperamos versão de cliente desejado de saudação.</span><span class="sxs-lookup"><span data-stu-id="51cdb-153">We then do a cache lookup toosee if we already have retrieved hello desired client version.</span></span>

```xml
<cache-lookup-value
key="@("clientversion-" + context.Variables["clientid"])"
variable-name="clientversion" />
```

<span data-ttu-id="51cdb-154">Em seguida, marcamos toosee se não foi encontrada-la no cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="51cdb-154">Then we check toosee if we did not find it in hello cache.</span></span>

```xml
<choose>
    <when condition="@(!context.Variables.ContainsKey("clientversion"))">
```

<span data-ttu-id="51cdb-155">Se não, nós a recuperamos.</span><span class="sxs-lookup"><span data-stu-id="51cdb-155">If we didn’t then we go and retrieve it.</span></span>

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

<span data-ttu-id="51cdb-156">Extrai o texto do corpo de resposta de saudação da resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="51cdb-156">Extract hello response body text from hello response.</span></span>

```xml
<set-variable
      name="clientversion"
      value="@(((IResponse)context.Variables["clientconfiguresponse"]).Body.As<string>())" />
```

<span data-ttu-id="51cdb-157">Armazená-lo novamente no cache de saudação para uso futuro.</span><span class="sxs-lookup"><span data-stu-id="51cdb-157">Store it back in hello cache for future use.</span></span>

```xml
<cache-store-value
      key="@("clientversion-" + context.Variables["clientid"])"
      value="@((string)context.Variables["clientversion"])"
      duration="100000" />
```

<span data-ttu-id="51cdb-158">E finalmente Olá back-end URL tooselect Olá versão da atualização do serviço de saudação desejado pelo cliente hello.</span><span class="sxs-lookup"><span data-stu-id="51cdb-158">And finally update hello back-end URL tooselect hello version of hello service desired by hello client.</span></span>

```xml
<set-backend-service
      base-url="@(context.Api.ServiceUrl.ToString() + "api/" + (string)context.Variables["clientversion"] + "/")" />
```

<span data-ttu-id="51cdb-159">Olá completamente política é da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="51cdb-159">hello completely policy is as follows.</span></span>

```xml
<inbound>
    <base />
    <set-variable name="clientid" value="@(context.Subscription.Key)" />
    <cache-lookup-value key="@("clientversion-" + context.Variables["clientid"])" variable-name="clientversion" />

    <!-- If we don’t find it in hello cache, make a request for it and store it -->
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

<span data-ttu-id="51cdb-160">Ativando o controle de tootransparently consumidores de API qual versão de back-end está sendo acessado por clientes sem ter que clientes tooupdate e a reimplantação é uma solução elegante que resolve muitos problemas de controle de versão de API.</span><span class="sxs-lookup"><span data-stu-id="51cdb-160">Enabling API consumers tootransparently control which backend version is being accessed by clients without having tooupdate and redeploy clients is a elegant solution that addresses many API versioning concerns.</span></span>

## <a name="tenant-isolation"></a><span data-ttu-id="51cdb-161">Isolamento de locatário</span><span class="sxs-lookup"><span data-stu-id="51cdb-161">Tenant Isolation</span></span>
<span data-ttu-id="51cdb-162">Em implantações maiores, de vários locatários, algumas empresas criar grupos separados de locatários em implantações distintas do hardware de back-end.</span><span class="sxs-lookup"><span data-stu-id="51cdb-162">In larger, multi-tenant deployments some companies create separate groups of tenants on distinct deployments of backend hardware.</span></span> <span data-ttu-id="51cdb-163">Isso minimiza o número de saudação de clientes que são afetados por um problema de hardware em Olá back-end.</span><span class="sxs-lookup"><span data-stu-id="51cdb-163">This minimizes hello number of customers who are impacted by a hardware issue on hello backend.</span></span> <span data-ttu-id="51cdb-164">Ele também permite que o novo toobe de versões de software distribuído em estágios.</span><span class="sxs-lookup"><span data-stu-id="51cdb-164">It also enables new software versions toobe rolled out in stages.</span></span> <span data-ttu-id="51cdb-165">O ideal é essa arquitetura de back-end deve ser consumidores tooAPI transparente.</span><span class="sxs-lookup"><span data-stu-id="51cdb-165">Ideally this backend architecture should be transparent tooAPI consumers.</span></span> <span data-ttu-id="51cdb-166">Isso pode ser obtido de um controle de versão de tootransparent de maneira semelhante, porque ela é baseada no hello mesma técnica de manipulação de URL de back-end hello usando o estado de configuração por chave de API.</span><span class="sxs-lookup"><span data-stu-id="51cdb-166">This can be achieved in a similar way tootransparent versioning because it is based on hello same technique of manipulating hello backend URL using configuration state per API key.</span></span>  

<span data-ttu-id="51cdb-167">Em vez de retornar uma versão preferencial do hello API para cada chave de assinatura, você retornará um identificador que está relacionada a um grupo de hardware do locatário toohello atribuído.</span><span class="sxs-lookup"><span data-stu-id="51cdb-167">Instead of returning a preferred version of hello API for each subscription key, you would return an identifier that relates a tenant toohello assigned hardware group.</span></span> <span data-ttu-id="51cdb-168">Esse identificador pode ser usado tooconstruct Olá back-end apropriado URL.</span><span class="sxs-lookup"><span data-stu-id="51cdb-168">That identifier can be used tooconstruct hello appropriate backend URL.</span></span>

## <a name="summary"></a><span data-ttu-id="51cdb-169">Resumo</span><span class="sxs-lookup"><span data-stu-id="51cdb-169">Summary</span></span>
<span data-ttu-id="51cdb-170">saudação de toouse Olá liberdade cache de gerenciamento de API do Azure para armazenar qualquer tipo de dados permite que os dados de tooconfiguration acesso eficiente que podem afetar a maneira de saudação que uma solicitação de entrada é processada.</span><span class="sxs-lookup"><span data-stu-id="51cdb-170">hello freedom toouse hello Azure API management cache for storing any kind of data enables efficient access tooconfiguration data that can affect hello way an inbound request is processed.</span></span> <span data-ttu-id="51cdb-171">Ele também pode ser usado toostore os fragmentos de dados que podem aumentar respostas, retornadas de uma API de back-end.</span><span class="sxs-lookup"><span data-stu-id="51cdb-171">It can also be used toostore data fragments that can augment responses, returned from a backend API.</span></span>

## <a name="next-steps"></a><span data-ttu-id="51cdb-172">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="51cdb-172">Next steps</span></span>
<span data-ttu-id="51cdb-173">. Forneça seus comentários no hello threads do Disqus para este tópico se há outros cenários que essas políticas tem habilitado para você, ou se há cenários você gostaria que tooachieve, mas não se sinta são possíveis no momento.</span><span class="sxs-lookup"><span data-stu-id="51cdb-173">Please give us your feedback in hello Disqus thread for this topic if there are other scenarios that these policies have enabled for you, or if there are scenarios you would like tooachieve but do not feel are currently possible.</span></span>

