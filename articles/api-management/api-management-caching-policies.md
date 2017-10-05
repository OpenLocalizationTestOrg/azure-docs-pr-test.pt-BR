---
title: "Políticas de cache no Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba mais sobre as políticas de cache disponíveis para uso no Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 8147199c-24d8-439f-b2a9-da28a70a890c
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2a8f012e7e223ef5c1683c8a6c5ecf2f3e96bed8
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="5aa26-103">Políticas de cache do Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="5aa26-103">API Management caching policies</span></span>
<span data-ttu-id="5aa26-104">Este tópico fornece uma referência para as políticas de Gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="5aa26-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="5aa26-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="5aa26-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="5aa26-106"><a name="CachingPolicies"></a> Políticas de cache</span><span class="sxs-lookup"><span data-stu-id="5aa26-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="5aa26-107">Resposta das políticas de cache</span><span class="sxs-lookup"><span data-stu-id="5aa26-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="5aa26-108">[Obter do cache](api-management-caching-policies.md#GetFromCache): executa a pesquisa em cache e retorna uma resposta válida armazenada em cache quando disponível.</span><span class="sxs-lookup"><span data-stu-id="5aa26-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="5aa26-109">[Armazenar em cache](api-management-caching-policies.md#StoreToCache): armazena a resposta em cache de acordo com a configuração de controle de cache especificada.</span><span class="sxs-lookup"><span data-stu-id="5aa26-109">[Store to cache](api-management-caching-policies.md#StoreToCache) - Caches responses according to the specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="5aa26-110">Valor das políticas de cache</span><span class="sxs-lookup"><span data-stu-id="5aa26-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="5aa26-111">[Obter valor do cache](#GetFromCacheByKey) - Recupere um item em cache por chave.</span><span class="sxs-lookup"><span data-stu-id="5aa26-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="5aa26-112">[Armazenar valor em cache](#StoreToCacheByKey) -Armazene um item no cache por chave.</span><span class="sxs-lookup"><span data-stu-id="5aa26-112">[Store value in cache](#StoreToCacheByKey) - Store an item in the cache by key.</span></span>  
  
    -   <span data-ttu-id="5aa26-113">[Remover o valor do cache](#RemoveCacheByKey) - remove um item no cache por chave.</span><span class="sxs-lookup"><span data-stu-id="5aa26-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in the cache by key.</span></span>  
  
##  <span data-ttu-id="5aa26-114"><a name="GetFromCache"></a> Obter do cache</span><span class="sxs-lookup"><span data-stu-id="5aa26-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="5aa26-115">Use a política `cache-lookup` para realizar pesquisas e retornar uma resposta válida em cache quando disponível.</span><span class="sxs-lookup"><span data-stu-id="5aa26-115">Use the `cache-lookup` policy to perform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="5aa26-116">Esta política deve ser aplicada em casos nos quais o conteúdo da resposta permanece estático por um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="5aa26-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="5aa26-117">O cache das respostas reduz os requisitos de largura de banda e processamento exigidos do servidor Web de back-end e reduz a latência percebida pelos consumidores da API.</span><span class="sxs-lookup"><span data-stu-id="5aa26-117">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5aa26-118">É necessário ter uma política correspondente de [Armazenar em cache](api-management-caching-policies.md#StoreToCache).</span><span class="sxs-lookup"><span data-stu-id="5aa26-118">This policy must have a corresponding [Store to cache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5aa26-119">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="5aa26-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression to evaluate)">  
  <vary-by-header>Accept</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Accept-Charset</vary-by-header>  
  <!-- should be present in most cases -->  
  <vary-by-header>Authorization</vary-by-header>  
  <!-- should be present when allow-authorized-response-caching is "true"-->  
  <vary-by-header>header name</vary-by-header>  
  <!-- optional, can repeated several times -->  
  <vary-by-query-parameter>parameter name</vary-by-query-parameter>  
  <!-- optional, can repeated several times -->  
</cache-lookup>  
```  
  
### <a name="examples"></a><span data-ttu-id="5aa26-120">Exemplos</span><span class="sxs-lookup"><span data-stu-id="5aa26-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="5aa26-121">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5aa26-121">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="none" must-revalidate="true">  
            <vary-by-query-parameter>version</vary-by-query-parameter>  
        </cache-lookup>           
    </inbound>  
    <outbound>  
        <cache-store duration="seconds" />  
        <base />          
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="5aa26-122">Exemplo usando expressões de política</span><span class="sxs-lookup"><span data-stu-id="5aa26-122">Example using policy expressions</span></span>  
 <span data-ttu-id="5aa26-123">Este exemplo mostra como configurar a duração do cache de resposta do Gerenciamento de API que corresponde ao cache de resposta do serviço de back-end, conforme especificado pela diretiva `Cache-Control` do serviço de backup.</span><span class="sxs-lookup"><span data-stu-id="5aa26-123">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="5aa26-124">Para ver uma demonstração da configuração e do uso dessa política, veja [Abordagem da Nuvem Episódio 177: Mais Recursos de Gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e avance para 25:25.</span><span class="sxs-lookup"><span data-stu-id="5aa26-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="5aa26-125">Para saber mais, veja [Expressões de política](api-management-policy-expressions.md) e [Variável de contexto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="5aa26-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="5aa26-126">Elementos</span><span class="sxs-lookup"><span data-stu-id="5aa26-126">Elements</span></span>  
  
|<span data-ttu-id="5aa26-127">Nome</span><span class="sxs-lookup"><span data-stu-id="5aa26-127">Name</span></span>|<span data-ttu-id="5aa26-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="5aa26-128">Description</span></span>|<span data-ttu-id="5aa26-129">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5aa26-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5aa26-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="5aa26-130">cache-lookup</span></span>|<span data-ttu-id="5aa26-131">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="5aa26-131">Root element.</span></span>|<span data-ttu-id="5aa26-132">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-132">Yes</span></span>|  
|<span data-ttu-id="5aa26-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="5aa26-133">vary-by-header</span></span>|<span data-ttu-id="5aa26-134">Inicie o cache de respostas por valor de cabeçalho especificado, como Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span><span class="sxs-lookup"><span data-stu-id="5aa26-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="5aa26-135">Não</span><span class="sxs-lookup"><span data-stu-id="5aa26-135">No</span></span>|  
|<span data-ttu-id="5aa26-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="5aa26-136">vary-by-query-parameter</span></span>|<span data-ttu-id="5aa26-137">Inicie o cache de respostas de acordo com o valor dos parâmetros de consulta especificados.</span><span class="sxs-lookup"><span data-stu-id="5aa26-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="5aa26-138">Insira somente um ou múltiplos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="5aa26-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="5aa26-139">Use ponto e vírgula como um separador.</span><span class="sxs-lookup"><span data-stu-id="5aa26-139">Use semicolon as a separator.</span></span> <span data-ttu-id="5aa26-140">Se nenhum for especificado, todos os parâmetros de consulta serão usados.</span><span class="sxs-lookup"><span data-stu-id="5aa26-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="5aa26-141">Não</span><span class="sxs-lookup"><span data-stu-id="5aa26-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5aa26-142">Atributos</span><span class="sxs-lookup"><span data-stu-id="5aa26-142">Attributes</span></span>  
  
|<span data-ttu-id="5aa26-143">Nome</span><span class="sxs-lookup"><span data-stu-id="5aa26-143">Name</span></span>|<span data-ttu-id="5aa26-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="5aa26-144">Description</span></span>|<span data-ttu-id="5aa26-145">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5aa26-145">Required</span></span>|<span data-ttu-id="5aa26-146">Padrão</span><span class="sxs-lookup"><span data-stu-id="5aa26-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5aa26-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="5aa26-147">allow-private-response-caching</span></span>|<span data-ttu-id="5aa26-148">Quando definido como `true`, permite armazenar em cache as solicitações que contêm um cabeçalho Authorization.</span><span class="sxs-lookup"><span data-stu-id="5aa26-148">When set to `true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="5aa26-149">Não</span><span class="sxs-lookup"><span data-stu-id="5aa26-149">No</span></span>|<span data-ttu-id="5aa26-150">false</span><span class="sxs-lookup"><span data-stu-id="5aa26-150">false</span></span>|  
|<span data-ttu-id="5aa26-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="5aa26-151">downstream-caching-type</span></span>|<span data-ttu-id="5aa26-152">Este atributo deve ser definido como um dos valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="5aa26-152">This attribute must be set to one of the following values.</span></span><br /><br /> <span data-ttu-id="5aa26-153">-   none: o cache downstream não é permitido.</span><span class="sxs-lookup"><span data-stu-id="5aa26-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="5aa26-154">-   private: o cache downstream privado é permitido.</span><span class="sxs-lookup"><span data-stu-id="5aa26-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="5aa26-155">-   public: o cache downstream privado e compartilhado é permitido.</span><span class="sxs-lookup"><span data-stu-id="5aa26-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="5aa26-156">Não</span><span class="sxs-lookup"><span data-stu-id="5aa26-156">No</span></span>|<span data-ttu-id="5aa26-157">nenhum</span><span class="sxs-lookup"><span data-stu-id="5aa26-157">none</span></span>|  
|<span data-ttu-id="5aa26-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="5aa26-158">must-revalidate</span></span>|<span data-ttu-id="5aa26-159">Quando o cache downstream está habilitado, este atributo ativa ou desativa a diretiva de controle de cache `must-revalidate` em respostas do gateway.</span><span class="sxs-lookup"><span data-stu-id="5aa26-159">When downstream caching is enabled this attribute turns on or off  the `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="5aa26-160">Não</span><span class="sxs-lookup"><span data-stu-id="5aa26-160">No</span></span>|<span data-ttu-id="5aa26-161">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="5aa26-161">true</span></span>|  
|<span data-ttu-id="5aa26-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="5aa26-162">vary-by-developer</span></span>|<span data-ttu-id="5aa26-163">Definido como `true` para respostas em cache por chave de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="5aa26-163">Set to `true` to cache responses per developer key.</span></span>|<span data-ttu-id="5aa26-164">Não</span><span class="sxs-lookup"><span data-stu-id="5aa26-164">No</span></span>|<span data-ttu-id="5aa26-165">false</span><span class="sxs-lookup"><span data-stu-id="5aa26-165">false</span></span>|  
|<span data-ttu-id="5aa26-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="5aa26-166">vary-by-developer-groups</span></span>|<span data-ttu-id="5aa26-167">Definido como `true` para respostas em cache por função de usuário.</span><span class="sxs-lookup"><span data-stu-id="5aa26-167">Set to `true` to cache responses per user role.</span></span>|<span data-ttu-id="5aa26-168">Não</span><span class="sxs-lookup"><span data-stu-id="5aa26-168">No</span></span>|<span data-ttu-id="5aa26-169">false</span><span class="sxs-lookup"><span data-stu-id="5aa26-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5aa26-170">Uso</span><span class="sxs-lookup"><span data-stu-id="5aa26-170">Usage</span></span>  
 <span data-ttu-id="5aa26-171">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="5aa26-171">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5aa26-172">**Seções de política:** entrada</span><span class="sxs-lookup"><span data-stu-id="5aa26-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="5aa26-173">**Escopos de política:** API, operação, produto</span><span class="sxs-lookup"><span data-stu-id="5aa26-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="5aa26-174"><a name="StoreToCache"></a> Armazenar em cache</span><span class="sxs-lookup"><span data-stu-id="5aa26-174"><a name="StoreToCache"></a> Store to cache</span></span>  
 <span data-ttu-id="5aa26-175">A política `cache-store` armazena as respostas em cache de acordo com a configuração de cache especificada.</span><span class="sxs-lookup"><span data-stu-id="5aa26-175">The `cache-store` policy caches responses according to the specified cache settings.</span></span> <span data-ttu-id="5aa26-176">Esta política deve ser aplicada em casos nos quais o conteúdo da resposta permanece estático por um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="5aa26-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="5aa26-177">O cache das respostas reduz os requisitos de largura de banda e processamento exigidos do servidor Web de back-end e reduz a latência percebida pelos consumidores da API.</span><span class="sxs-lookup"><span data-stu-id="5aa26-177">Response caching reduces bandwidth and processing requirements imposed on the backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5aa26-178">Esta política deve ter uma política [Obter do cache](api-management-caching-policies.md#GetFromCache) correspondente.</span><span class="sxs-lookup"><span data-stu-id="5aa26-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5aa26-179">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="5aa26-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="5aa26-180">Exemplos</span><span class="sxs-lookup"><span data-stu-id="5aa26-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="5aa26-181">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5aa26-181">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
          <cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false">  
                <vary-by-query-parameter>parameter name</vary-by-query-parameter> <!-- optional, can repeated several times -->  
        </cache-lookup>  
    </inbound>  
    <outbound>  
        <base />  
            <cache-store duration="3600" />  
    </outbound>  
</policies>  
```  
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="5aa26-182">Exemplo usando expressões de política</span><span class="sxs-lookup"><span data-stu-id="5aa26-182">Example using policy expressions</span></span>  
 <span data-ttu-id="5aa26-183">Este exemplo mostra como configurar a duração do cache de resposta do Gerenciamento de API que corresponde ao cache de resposta do serviço de back-end, conforme especificado pela diretiva `Cache-Control` do serviço de backup.</span><span class="sxs-lookup"><span data-stu-id="5aa26-183">This example shows how to to configure API Management response caching duration that matches the response caching of the backend service as specified by the backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="5aa26-184">Para ver uma demonstração da configuração e do uso dessa política, veja [Abordagem da Nuvem Episódio 177: Mais Recursos de Gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e avance para 25:25.</span><span class="sxs-lookup"><span data-stu-id="5aa26-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 25:25.</span></span>  
  
```xml  
<!-- The following cache policy snippets demonstrate how to control API Management reponse cache duration with Cache-Control headers sent by the backend service. -->  
  
<!-- Copy this snippet into the inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into the outbound section. Note that cache duration is set to the max-age value provided in the Cache-Control header received from the backend service or to the deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="5aa26-185">Para saber mais, veja [Expressões de política](api-management-policy-expressions.md) e [Variável de contexto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="5aa26-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="5aa26-186">Elementos</span><span class="sxs-lookup"><span data-stu-id="5aa26-186">Elements</span></span>  
  
|<span data-ttu-id="5aa26-187">Nome</span><span class="sxs-lookup"><span data-stu-id="5aa26-187">Name</span></span>|<span data-ttu-id="5aa26-188">Descrição</span><span class="sxs-lookup"><span data-stu-id="5aa26-188">Description</span></span>|<span data-ttu-id="5aa26-189">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5aa26-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5aa26-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="5aa26-190">cache-store</span></span>|<span data-ttu-id="5aa26-191">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="5aa26-191">Root element.</span></span>|<span data-ttu-id="5aa26-192">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5aa26-193">Atributos</span><span class="sxs-lookup"><span data-stu-id="5aa26-193">Attributes</span></span>  
  
|<span data-ttu-id="5aa26-194">Nome</span><span class="sxs-lookup"><span data-stu-id="5aa26-194">Name</span></span>|<span data-ttu-id="5aa26-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="5aa26-195">Description</span></span>|<span data-ttu-id="5aa26-196">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5aa26-196">Required</span></span>|<span data-ttu-id="5aa26-197">Padrão</span><span class="sxs-lookup"><span data-stu-id="5aa26-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5aa26-198">duration</span><span class="sxs-lookup"><span data-stu-id="5aa26-198">duration</span></span>|<span data-ttu-id="5aa26-199">Vida útil das entradas armazenadas em cache, especificada em segundos.</span><span class="sxs-lookup"><span data-stu-id="5aa26-199">Time-to-live of the cached entries, specified in seconds.</span></span>|<span data-ttu-id="5aa26-200">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-200">Yes</span></span>|<span data-ttu-id="5aa26-201">N/D</span><span class="sxs-lookup"><span data-stu-id="5aa26-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5aa26-202">Uso</span><span class="sxs-lookup"><span data-stu-id="5aa26-202">Usage</span></span>  
 <span data-ttu-id="5aa26-203">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="5aa26-203">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5aa26-204">**Seções de política:** saída</span><span class="sxs-lookup"><span data-stu-id="5aa26-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="5aa26-205">**Escopos de política:** API, operação, produto</span><span class="sxs-lookup"><span data-stu-id="5aa26-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="5aa26-206"><a name="GetFromCacheByKey"></a> Obter valor do cache</span><span class="sxs-lookup"><span data-stu-id="5aa26-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="5aa26-207">Use a política `cache-lookup-value` para executar a consulta em cache por chave e retornar um valor armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="5aa26-207">Use the `cache-lookup-value` policy to perform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="5aa26-208">A chave pode ter um valor de cadeia de caracteres arbitrário e geralmente é fornecida usando uma expressão de política.</span><span class="sxs-lookup"><span data-stu-id="5aa26-208">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5aa26-209">É necessário ter uma política correspondente de [Armazenar valor em cache](#StoreToCacheByKey).</span><span class="sxs-lookup"><span data-stu-id="5aa26-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5aa26-210">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="5aa26-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value to use if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="5aa26-211">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5aa26-211">Example</span></span>  
 <span data-ttu-id="5aa26-212">Para saber mais e obter exemplos dessa política, veja [Cache personalizado no Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="5aa26-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="5aa26-213">Elementos</span><span class="sxs-lookup"><span data-stu-id="5aa26-213">Elements</span></span>  
  
|<span data-ttu-id="5aa26-214">Nome</span><span class="sxs-lookup"><span data-stu-id="5aa26-214">Name</span></span>|<span data-ttu-id="5aa26-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="5aa26-215">Description</span></span>|<span data-ttu-id="5aa26-216">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5aa26-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5aa26-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="5aa26-217">cache-lookup-value</span></span>|<span data-ttu-id="5aa26-218">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="5aa26-218">Root element.</span></span>|<span data-ttu-id="5aa26-219">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5aa26-220">Atributos</span><span class="sxs-lookup"><span data-stu-id="5aa26-220">Attributes</span></span>  
  
|<span data-ttu-id="5aa26-221">Nome</span><span class="sxs-lookup"><span data-stu-id="5aa26-221">Name</span></span>|<span data-ttu-id="5aa26-222">Descrição</span><span class="sxs-lookup"><span data-stu-id="5aa26-222">Description</span></span>|<span data-ttu-id="5aa26-223">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5aa26-223">Required</span></span>|<span data-ttu-id="5aa26-224">Padrão</span><span class="sxs-lookup"><span data-stu-id="5aa26-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5aa26-225">default-value</span><span class="sxs-lookup"><span data-stu-id="5aa26-225">default-value</span></span>|<span data-ttu-id="5aa26-226">Um valor que será atribuído à variável se a pesquisa de chave em cache resultou em um erro.</span><span class="sxs-lookup"><span data-stu-id="5aa26-226">A value that will be assigned to the variable if the cache key lookup resulted in a miss.</span></span> <span data-ttu-id="5aa26-227">Se esse atributo não for especificado, `null` é atribuído.</span><span class="sxs-lookup"><span data-stu-id="5aa26-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="5aa26-228">Não</span><span class="sxs-lookup"><span data-stu-id="5aa26-228">No</span></span>|`null`|  
|<span data-ttu-id="5aa26-229">chave</span><span class="sxs-lookup"><span data-stu-id="5aa26-229">key</span></span>|<span data-ttu-id="5aa26-230">Valor de chave de cache a usar na pesquisa.</span><span class="sxs-lookup"><span data-stu-id="5aa26-230">Cache key value to use in the lookup.</span></span>|<span data-ttu-id="5aa26-231">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-231">Yes</span></span>|<span data-ttu-id="5aa26-232">N/D</span><span class="sxs-lookup"><span data-stu-id="5aa26-232">N/A</span></span>|  
|<span data-ttu-id="5aa26-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="5aa26-233">variable-name</span></span>|<span data-ttu-id="5aa26-234">Nome da [variável de contexto](api-management-policy-expressions.md#ContextVariables) a atribuir para o valor pesquisado, se a pesquisa for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="5aa26-234">Name of the [context variable](api-management-policy-expressions.md#ContextVariables) the looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="5aa26-235">Se a pesquisa resulta em um erro, a variável será atribuída o valor do atributo `default-value` ou `null`, se o atributo `default-value` for omitido.</span><span class="sxs-lookup"><span data-stu-id="5aa26-235">If lookup results in a miss, the variable will be assigned the value of the `default-value` attribute or `null`, if the `default-value` attribute is omitted.</span></span>|<span data-ttu-id="5aa26-236">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-236">Yes</span></span>|<span data-ttu-id="5aa26-237">N/D</span><span class="sxs-lookup"><span data-stu-id="5aa26-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5aa26-238">Uso</span><span class="sxs-lookup"><span data-stu-id="5aa26-238">Usage</span></span>  
 <span data-ttu-id="5aa26-239">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="5aa26-239">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5aa26-240">**Seções de política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="5aa26-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="5aa26-241">**Escopos de política:** global, API, operação, produto</span><span class="sxs-lookup"><span data-stu-id="5aa26-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="5aa26-242"><a name="StoreToCacheByKey"></a> Armazenar valor em cache</span><span class="sxs-lookup"><span data-stu-id="5aa26-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="5aa26-243">`cache-store-value` armazena em cache por chave.</span><span class="sxs-lookup"><span data-stu-id="5aa26-243">The `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="5aa26-244">A chave pode ter um valor de cadeia de caracteres arbitrário e geralmente é fornecida usando uma expressão de política.</span><span class="sxs-lookup"><span data-stu-id="5aa26-244">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5aa26-245">Esta política deve ter uma política [Obter valor do cache](#GetFromCacheByKey) correspondente.</span><span class="sxs-lookup"><span data-stu-id="5aa26-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5aa26-246">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="5aa26-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value to cache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="5aa26-247">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5aa26-247">Example</span></span>  
 <span data-ttu-id="5aa26-248">Para saber mais e obter exemplos dessa política, veja [Cache personalizado no Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="5aa26-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="5aa26-249">Elementos</span><span class="sxs-lookup"><span data-stu-id="5aa26-249">Elements</span></span>  
  
|<span data-ttu-id="5aa26-250">Nome</span><span class="sxs-lookup"><span data-stu-id="5aa26-250">Name</span></span>|<span data-ttu-id="5aa26-251">Descrição</span><span class="sxs-lookup"><span data-stu-id="5aa26-251">Description</span></span>|<span data-ttu-id="5aa26-252">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5aa26-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5aa26-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="5aa26-253">cache-store-value</span></span>|<span data-ttu-id="5aa26-254">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="5aa26-254">Root element.</span></span>|<span data-ttu-id="5aa26-255">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5aa26-256">Atributos</span><span class="sxs-lookup"><span data-stu-id="5aa26-256">Attributes</span></span>  
  
|<span data-ttu-id="5aa26-257">Nome</span><span class="sxs-lookup"><span data-stu-id="5aa26-257">Name</span></span>|<span data-ttu-id="5aa26-258">Descrição</span><span class="sxs-lookup"><span data-stu-id="5aa26-258">Description</span></span>|<span data-ttu-id="5aa26-259">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5aa26-259">Required</span></span>|<span data-ttu-id="5aa26-260">Padrão</span><span class="sxs-lookup"><span data-stu-id="5aa26-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5aa26-261">duration</span><span class="sxs-lookup"><span data-stu-id="5aa26-261">duration</span></span>|<span data-ttu-id="5aa26-262">Valor será armazenado em cache para o valor de duração fornecido, especificado em segundos.</span><span class="sxs-lookup"><span data-stu-id="5aa26-262">Value will be cached for the provided duration value, specified in seconds.</span></span>|<span data-ttu-id="5aa26-263">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-263">Yes</span></span>|<span data-ttu-id="5aa26-264">N/D</span><span class="sxs-lookup"><span data-stu-id="5aa26-264">N/A</span></span>|  
|<span data-ttu-id="5aa26-265">chave</span><span class="sxs-lookup"><span data-stu-id="5aa26-265">key</span></span>|<span data-ttu-id="5aa26-266">A chave em cache em que o valor será armazenado.</span><span class="sxs-lookup"><span data-stu-id="5aa26-266">Cache key the value will be stored under.</span></span>|<span data-ttu-id="5aa26-267">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-267">Yes</span></span>|<span data-ttu-id="5aa26-268">N/D</span><span class="sxs-lookup"><span data-stu-id="5aa26-268">N/A</span></span>|  
|<span data-ttu-id="5aa26-269">valor</span><span class="sxs-lookup"><span data-stu-id="5aa26-269">value</span></span>|<span data-ttu-id="5aa26-270">O valor a ser armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="5aa26-270">The value to be cached.</span></span>|<span data-ttu-id="5aa26-271">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-271">Yes</span></span>|<span data-ttu-id="5aa26-272">N/D</span><span class="sxs-lookup"><span data-stu-id="5aa26-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5aa26-273">Uso</span><span class="sxs-lookup"><span data-stu-id="5aa26-273">Usage</span></span>  
 <span data-ttu-id="5aa26-274">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="5aa26-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5aa26-275">**Seções de política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="5aa26-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="5aa26-276">**Escopos de política:** global, API, operação, produto</span><span class="sxs-lookup"><span data-stu-id="5aa26-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="5aa26-277"><a name="RemoveCacheByKey"></a> Remover valor do cache</span><span class="sxs-lookup"><span data-stu-id="5aa26-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="5aa26-278">`cache-remove-value` exclui um item em cache identificado por sua chave.</span><span class="sxs-lookup"><span data-stu-id="5aa26-278">The             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="5aa26-279">A chave pode ter um valor de cadeia de caracteres arbitrário e geralmente é fornecida usando uma expressão de política.</span><span class="sxs-lookup"><span data-stu-id="5aa26-279">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="5aa26-280">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="5aa26-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="5aa26-281">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5aa26-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="5aa26-282">Elementos</span><span class="sxs-lookup"><span data-stu-id="5aa26-282">Elements</span></span>  
  
|<span data-ttu-id="5aa26-283">Nome</span><span class="sxs-lookup"><span data-stu-id="5aa26-283">Name</span></span>|<span data-ttu-id="5aa26-284">Descrição</span><span class="sxs-lookup"><span data-stu-id="5aa26-284">Description</span></span>|<span data-ttu-id="5aa26-285">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5aa26-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5aa26-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="5aa26-286">cache-remove-value</span></span>|<span data-ttu-id="5aa26-287">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="5aa26-287">Root element.</span></span>|<span data-ttu-id="5aa26-288">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="5aa26-289">Atributos</span><span class="sxs-lookup"><span data-stu-id="5aa26-289">Attributes</span></span>  
  
|<span data-ttu-id="5aa26-290">Nome</span><span class="sxs-lookup"><span data-stu-id="5aa26-290">Name</span></span>|<span data-ttu-id="5aa26-291">Descrição</span><span class="sxs-lookup"><span data-stu-id="5aa26-291">Description</span></span>|<span data-ttu-id="5aa26-292">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5aa26-292">Required</span></span>|<span data-ttu-id="5aa26-293">Padrão</span><span class="sxs-lookup"><span data-stu-id="5aa26-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5aa26-294">chave</span><span class="sxs-lookup"><span data-stu-id="5aa26-294">key</span></span>|<span data-ttu-id="5aa26-295">A chave do valor anteriormente armazenado em cache a ser removido do cache.</span><span class="sxs-lookup"><span data-stu-id="5aa26-295">The key of the previously cached value to be removed from the cache.</span></span>|<span data-ttu-id="5aa26-296">Sim</span><span class="sxs-lookup"><span data-stu-id="5aa26-296">Yes</span></span>|<span data-ttu-id="5aa26-297">N/D</span><span class="sxs-lookup"><span data-stu-id="5aa26-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="5aa26-298">Uso</span><span class="sxs-lookup"><span data-stu-id="5aa26-298">Usage</span></span>  
 <span data-ttu-id="5aa26-299">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="5aa26-299">This policy can be used in the following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="5aa26-300">**Seções de política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="5aa26-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="5aa26-301">**Escopos de política:** global, API, operação, produto</span><span class="sxs-lookup"><span data-stu-id="5aa26-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="5aa26-302">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5aa26-302">Next steps</span></span>
<span data-ttu-id="5aa26-303">Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5aa26-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  