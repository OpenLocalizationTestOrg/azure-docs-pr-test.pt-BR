---
title: "políticas de gerenciamento de API de cache do aaaAzure | Microsoft Docs"
description: "Saiba mais sobre Olá cache políticas disponíveis para uso no gerenciamento de API do Azure."
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
ms.openlocfilehash: bd6b0721945609b28dbf6e7ef0631979c08c8c65
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-caching-policies"></a><span data-ttu-id="5e3b4-103">Políticas de cache do Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="5e3b4-103">API Management caching policies</span></span>
<span data-ttu-id="5e3b4-104">Este tópico fornece uma referência para Olá políticas de gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="5e3b4-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="5e3b4-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="5e3b4-106"><a name="CachingPolicies"></a> Políticas de cache</span><span class="sxs-lookup"><span data-stu-id="5e3b4-106"><a name="CachingPolicies"></a> Caching policies</span></span>  
  
-   <span data-ttu-id="5e3b4-107">Resposta das políticas de cache</span><span class="sxs-lookup"><span data-stu-id="5e3b4-107">Response caching policies</span></span>  
  
    -   <span data-ttu-id="5e3b4-108">[Obter do cache](api-management-caching-policies.md#GetFromCache): executa a pesquisa em cache e retorna uma resposta válida armazenada em cache quando disponível.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-108">[Get from cache](api-management-caching-policies.md#GetFromCache) - Perform cache look up and return a valid cached responses when available.</span></span>  
  
    -   <span data-ttu-id="5e3b4-109">[Armazenar toocache](api-management-caching-policies.md#StoreToCache) - respostas de Caches de acordo com o toohello configuração de controle de cache especificado.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-109">[Store toocache](api-management-caching-policies.md#StoreToCache) - Caches responses according toohello specified cache control configuration.</span></span>  
  
-   <span data-ttu-id="5e3b4-110">Valor das políticas de cache</span><span class="sxs-lookup"><span data-stu-id="5e3b4-110">Value caching policies</span></span>  
  
    -   <span data-ttu-id="5e3b4-111">[Obter valor do cache](#GetFromCacheByKey) - Recupere um item em cache por chave.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-111">[Get value from cache](#GetFromCacheByKey) - Retrieve a cached item by key.</span></span>  
  
    -   <span data-ttu-id="5e3b4-112">[Armazena o valor em cache](#StoreToCacheByKey) -armazenar um item no cache de saudação por chave.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-112">[Store value in cache](#StoreToCacheByKey) - Store an item in hello cache by key.</span></span>  
  
    -   <span data-ttu-id="5e3b4-113">[Remova o valor do cache](#RemoveCacheByKey) -remover um item no cache de saudação por chave.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-113">[Remove value from cache](#RemoveCacheByKey) - Remove an item in hello cache by key.</span></span>  
  
##  <span data-ttu-id="5e3b4-114"><a name="GetFromCache"></a> Obter do cache</span><span class="sxs-lookup"><span data-stu-id="5e3b4-114"><a name="GetFromCache"></a> Get from cache</span></span>  
 <span data-ttu-id="5e3b4-115">Saudação de uso `cache-lookup` cache da política de tooperform pesquisar e retornar uma resposta válida de cache quando disponível.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-115">Use hello `cache-lookup` policy tooperform cache look up and return a valid cached response when available.</span></span> <span data-ttu-id="5e3b4-116">Esta política deve ser aplicada em casos nos quais o conteúdo da resposta permanece estático por um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-116">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="5e3b4-117">O cache de resposta reduz a largura de banda e requisitos de processamento impostos Olá back-end da web server e reduz a latência percebida pelos consumidores de API.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-117">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5e3b4-118">Essa diretiva deve ter um correspondente [toocache repositório](api-management-caching-policies.md#StoreToCache) política.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-118">This policy must have a corresponding [Store toocache](api-management-caching-policies.md#StoreToCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5e3b4-119">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="5e3b4-119">Policy statement</span></span>  
  
```xml  
<cache-lookup vary-by-developer="true | false" vary-by-developer-groups="true | false" downstream-caching-type="none | private | public" must-revalidate="true | false" allow-private-response-caching="@(expression tooevaluate)">  
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
  
### <a name="examples"></a><span data-ttu-id="5e3b4-120">Exemplos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-120">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="5e3b4-121">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5e3b4-121">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="5e3b4-122">Exemplo usando expressões de política</span><span class="sxs-lookup"><span data-stu-id="5e3b4-122">Example using policy expressions</span></span>  
 <span data-ttu-id="5e3b4-123">Este exemplo mostra como resposta de gerenciamento de API tootooconfigure cache duração que corresponde ao Olá cache de resposta do serviço de back-end Olá conforme especificado pelas Olá feito do serviço `Cache-Control` diretiva.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-123">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="5e3b4-124">Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too25:25.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-124">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="5e3b4-125">Para obter mais informações, veja [Expressões de política](api-management-policy-expressions.md) e [Variável de contexto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="5e3b4-125">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="5e3b4-126">Elementos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-126">Elements</span></span>  
  
|<span data-ttu-id="5e3b4-127">Nome</span><span class="sxs-lookup"><span data-stu-id="5e3b4-127">Name</span></span>|<span data-ttu-id="5e3b4-128">Descrição</span><span class="sxs-lookup"><span data-stu-id="5e3b4-128">Description</span></span>|<span data-ttu-id="5e3b4-129">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5e3b4-129">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5e3b4-130">cache-lookup</span><span class="sxs-lookup"><span data-stu-id="5e3b4-130">cache-lookup</span></span>|<span data-ttu-id="5e3b4-131">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-131">Root element.</span></span>|<span data-ttu-id="5e3b4-132">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-132">Yes</span></span>|  
|<span data-ttu-id="5e3b4-133">vary-by-header</span><span class="sxs-lookup"><span data-stu-id="5e3b4-133">vary-by-header</span></span>|<span data-ttu-id="5e3b4-134">Inicie o cache de respostas por valor de cabeçalho especificado, como Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-134">Start caching responses per value of specified header, such as Accept, Accept-Charset, Accept-Encoding, Accept-Language, Authorization, Expect, From, Host, If-Match.</span></span>|<span data-ttu-id="5e3b4-135">Não</span><span class="sxs-lookup"><span data-stu-id="5e3b4-135">No</span></span>|  
|<span data-ttu-id="5e3b4-136">vary-by-query-parameter</span><span class="sxs-lookup"><span data-stu-id="5e3b4-136">vary-by-query-parameter</span></span>|<span data-ttu-id="5e3b4-137">Inicie o cache de respostas de acordo com o valor dos parâmetros de consulta especificados.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-137">Start caching responses per value of specified query parameters.</span></span> <span data-ttu-id="5e3b4-138">Insira somente um ou múltiplos parâmetros.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-138">Enter a single or multiple parameters.</span></span> <span data-ttu-id="5e3b4-139">Use ponto e vírgula como um separador.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-139">Use semicolon as a separator.</span></span> <span data-ttu-id="5e3b4-140">Se nenhum for especificado, todos os parâmetros de consulta serão usados.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-140">If none are specified, all query parameters are used.</span></span>|<span data-ttu-id="5e3b4-141">Não</span><span class="sxs-lookup"><span data-stu-id="5e3b4-141">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5e3b4-142">Atributos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-142">Attributes</span></span>  
  
|<span data-ttu-id="5e3b4-143">Nome</span><span class="sxs-lookup"><span data-stu-id="5e3b4-143">Name</span></span>|<span data-ttu-id="5e3b4-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="5e3b4-144">Description</span></span>|<span data-ttu-id="5e3b4-145">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5e3b4-145">Required</span></span>|<span data-ttu-id="5e3b4-146">Padrão</span><span class="sxs-lookup"><span data-stu-id="5e3b4-146">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5e3b4-147">allow-private-response-caching</span><span class="sxs-lookup"><span data-stu-id="5e3b4-147">allow-private-response-caching</span></span>|<span data-ttu-id="5e3b4-148">Quando definido muito`true`, permite armazenar em cache de solicitações que contêm um cabeçalho de autorização.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-148">When set too`true`, allows caching of requests that contain an Authorization header.</span></span>|<span data-ttu-id="5e3b4-149">Não</span><span class="sxs-lookup"><span data-stu-id="5e3b4-149">No</span></span>|<span data-ttu-id="5e3b4-150">false</span><span class="sxs-lookup"><span data-stu-id="5e3b4-150">false</span></span>|  
|<span data-ttu-id="5e3b4-151">downstream-caching-type</span><span class="sxs-lookup"><span data-stu-id="5e3b4-151">downstream-caching-type</span></span>|<span data-ttu-id="5e3b4-152">Esse atributo deve ser definido como tooone de saudação valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-152">This attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="5e3b4-153">-   none: o cache downstream não é permitido.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-153">-   none - downstream caching is not allowed.</span></span><br /><span data-ttu-id="5e3b4-154">-   private: o cache downstream privado é permitido.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-154">-   private - downstream private caching is allowed.</span></span><br /><span data-ttu-id="5e3b4-155">-   public: o cache downstream privado e compartilhado é permitido.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-155">-   public - private and shared downstream caching is allowed.</span></span>|<span data-ttu-id="5e3b4-156">Não</span><span class="sxs-lookup"><span data-stu-id="5e3b4-156">No</span></span>|<span data-ttu-id="5e3b4-157">nenhum</span><span class="sxs-lookup"><span data-stu-id="5e3b4-157">none</span></span>|  
|<span data-ttu-id="5e3b4-158">must-revalidate</span><span class="sxs-lookup"><span data-stu-id="5e3b4-158">must-revalidate</span></span>|<span data-ttu-id="5e3b4-159">Quando o cache downstream é habilitado esse atributo ativa ou desativa a saudação `must-revalidate` diretiva de controle de cache em respostas de gateway.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-159">When downstream caching is enabled this attribute turns on or off  hello `must-revalidate` cache control directive in gateway responses.</span></span>|<span data-ttu-id="5e3b4-160">Não</span><span class="sxs-lookup"><span data-stu-id="5e3b4-160">No</span></span>|<span data-ttu-id="5e3b4-161">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="5e3b4-161">true</span></span>|  
|<span data-ttu-id="5e3b4-162">vary-by-developer</span><span class="sxs-lookup"><span data-stu-id="5e3b4-162">vary-by-developer</span></span>|<span data-ttu-id="5e3b4-163">Definir muito`true` respostas toocache por chave de desenvolvedor.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-163">Set too`true` toocache responses per developer key.</span></span>|<span data-ttu-id="5e3b4-164">Não</span><span class="sxs-lookup"><span data-stu-id="5e3b4-164">No</span></span>|<span data-ttu-id="5e3b4-165">false</span><span class="sxs-lookup"><span data-stu-id="5e3b4-165">false</span></span>|  
|<span data-ttu-id="5e3b4-166">vary-by-developer-groups</span><span class="sxs-lookup"><span data-stu-id="5e3b4-166">vary-by-developer-groups</span></span>|<span data-ttu-id="5e3b4-167">Definir muito`true` respostas toocache por função de usuário.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-167">Set too`true` toocache responses per user role.</span></span>|<span data-ttu-id="5e3b4-168">Não</span><span class="sxs-lookup"><span data-stu-id="5e3b4-168">No</span></span>|<span data-ttu-id="5e3b4-169">false</span><span class="sxs-lookup"><span data-stu-id="5e3b4-169">false</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5e3b4-170">Uso</span><span class="sxs-lookup"><span data-stu-id="5e3b4-170">Usage</span></span>  
 <span data-ttu-id="5e3b4-171">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="5e3b4-171">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5e3b4-172">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="5e3b4-172">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="5e3b4-173">**Escopos de política:** API, operação, produto</span><span class="sxs-lookup"><span data-stu-id="5e3b4-173">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="5e3b4-174"><a name="StoreToCache"></a>Repositório toocache</span><span class="sxs-lookup"><span data-stu-id="5e3b4-174"><a name="StoreToCache"></a> Store toocache</span></span>  
 <span data-ttu-id="5e3b4-175">Olá `cache-store` especificado de respostas de caches de política toohello de acordo com as configurações de cache.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-175">hello `cache-store` policy caches responses according toohello specified cache settings.</span></span> <span data-ttu-id="5e3b4-176">Esta política deve ser aplicada em casos nos quais o conteúdo da resposta permanece estático por um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-176">This policy can be applied in cases where response content remains static over a period of time.</span></span> <span data-ttu-id="5e3b4-177">O cache de resposta reduz a largura de banda e requisitos de processamento impostos Olá back-end da web server e reduz a latência percebida pelos consumidores de API.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-177">Response caching reduces bandwidth and processing requirements imposed on hello backend web server and lowers latency perceived by API consumers.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5e3b4-178">Esta política deve ter uma política [Obter do cache](api-management-caching-policies.md#GetFromCache) correspondente.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-178">This policy must have a corresponding [Get from cache](api-management-caching-policies.md#GetFromCache) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5e3b4-179">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="5e3b4-179">Policy statement</span></span>  
  
```xml  
<cache-store duration="seconds" />  
```  
  
### <a name="examples"></a><span data-ttu-id="5e3b4-180">Exemplos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-180">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="5e3b4-181">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5e3b4-181">Example</span></span>  
  
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
  
#### <a name="example-using-policy-expressions"></a><span data-ttu-id="5e3b4-182">Exemplo usando expressões de política</span><span class="sxs-lookup"><span data-stu-id="5e3b4-182">Example using policy expressions</span></span>  
 <span data-ttu-id="5e3b4-183">Este exemplo mostra como resposta de gerenciamento de API tootooconfigure cache duração que corresponde ao Olá cache de resposta do serviço de back-end Olá conforme especificado pelas Olá feito do serviço `Cache-Control` diretiva.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-183">This example shows how tootooconfigure API Management response caching duration that matches hello response caching of hello backend service as specified by hello backed service's `Cache-Control` directive.</span></span> <span data-ttu-id="5e3b4-184">Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too25:25.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-184">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too25:25.</span></span>  
  
```xml  
<!-- hello following cache policy snippets demonstrate how toocontrol API Management reponse cache duration with Cache-Control headers sent by hello backend service. -->  
  
<!-- Copy this snippet into hello inbound section -->  
<cache-lookup vary-by-developer="false" vary-by-developer-groups="false" downstream-caching-type="public" must-revalidate="true" >  
  <vary-by-header>Accept</vary-by-header>  
  <vary-by-header>Accept-Charset</vary-by-header>  
</cache-lookup>  
  
<!-- Copy this snippet into hello outbound section. Note that cache duration is set toohello max-age value provided in hello Cache-Control header received from hello backend service or toohello deafult value of 5 min if none is found  -->  
<cache-store duration="@{  
    var header = context.Response.Headers.GetValueOrDefault("Cache-Control","");  
    var maxAge = Regex.Match(header, @"max-age=(?<maxAge>\d+)").Groups["maxAge"]?.Value;  
    return (!string.IsNullOrEmpty(maxAge))?int.Parse(maxAge):300;  
  }"  
 />  
```  
  
 <span data-ttu-id="5e3b4-185">Para obter mais informações, veja [Expressões de política](api-management-policy-expressions.md) e [Variável de contexto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="5e3b4-185">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="5e3b4-186">Elementos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-186">Elements</span></span>  
  
|<span data-ttu-id="5e3b4-187">Nome</span><span class="sxs-lookup"><span data-stu-id="5e3b4-187">Name</span></span>|<span data-ttu-id="5e3b4-188">Descrição</span><span class="sxs-lookup"><span data-stu-id="5e3b4-188">Description</span></span>|<span data-ttu-id="5e3b4-189">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5e3b4-189">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5e3b4-190">cache-store</span><span class="sxs-lookup"><span data-stu-id="5e3b4-190">cache-store</span></span>|<span data-ttu-id="5e3b4-191">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-191">Root element.</span></span>|<span data-ttu-id="5e3b4-192">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-192">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5e3b4-193">Atributos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-193">Attributes</span></span>  
  
|<span data-ttu-id="5e3b4-194">Nome</span><span class="sxs-lookup"><span data-stu-id="5e3b4-194">Name</span></span>|<span data-ttu-id="5e3b4-195">Descrição</span><span class="sxs-lookup"><span data-stu-id="5e3b4-195">Description</span></span>|<span data-ttu-id="5e3b4-196">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5e3b4-196">Required</span></span>|<span data-ttu-id="5e3b4-197">Padrão</span><span class="sxs-lookup"><span data-stu-id="5e3b4-197">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5e3b4-198">duration</span><span class="sxs-lookup"><span data-stu-id="5e3b4-198">duration</span></span>|<span data-ttu-id="5e3b4-199">Tempo de vida de saudação armazenados em cache as entradas, especificadas em segundos.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-199">Time-to-live of hello cached entries, specified in seconds.</span></span>|<span data-ttu-id="5e3b4-200">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-200">Yes</span></span>|<span data-ttu-id="5e3b4-201">N/D</span><span class="sxs-lookup"><span data-stu-id="5e3b4-201">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5e3b4-202">Uso</span><span class="sxs-lookup"><span data-stu-id="5e3b4-202">Usage</span></span>  
 <span data-ttu-id="5e3b4-203">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="5e3b4-203">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5e3b4-204">**Seções de política:** saída</span><span class="sxs-lookup"><span data-stu-id="5e3b4-204">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="5e3b4-205">**Escopos de política:** API, operação, produto</span><span class="sxs-lookup"><span data-stu-id="5e3b4-205">**Policy scopes:** API, operation, product</span></span>  
  
##  <span data-ttu-id="5e3b4-206"><a name="GetFromCacheByKey"></a> Obter valor do cache</span><span class="sxs-lookup"><span data-stu-id="5e3b4-206"><a name="GetFromCacheByKey"></a> Get value from cache</span></span>  
 <span data-ttu-id="5e3b4-207">Saudação de uso `cache-lookup-value` política tooperform pesquisa de cache por chave e retornam um valor armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-207">Use hello `cache-lookup-value` policy tooperform cache lookup by key and return a cached value.</span></span> <span data-ttu-id="5e3b4-208">chave de saudação pode ter um valor de cadeia de caracteres arbitrária e normalmente é fornecido usando uma expressão de política.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-208">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5e3b4-209">É necessário ter uma política correspondente de [Armazenar valor em cache](#StoreToCacheByKey).</span><span class="sxs-lookup"><span data-stu-id="5e3b4-209">This policy must have a corresponding [Store value in cache](#StoreToCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5e3b4-210">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="5e3b4-210">Policy statement</span></span>  
  
```xml  
<cache-lookup-value key="cache key value"   
    default-value="value toouse if cache lookup resulted in a miss"   
    variable-name="name of a variable looked up value is assigned to" />  
```  
  
### <a name="example"></a><span data-ttu-id="5e3b4-211">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5e3b4-211">Example</span></span>  
 <span data-ttu-id="5e3b4-212">Para saber mais e obter exemplos dessa política, veja [Cache personalizado no Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="5e3b4-212">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-lookup-value  
    key="@("userprofile-" + context.Variables["enduserid"])"    
    variable-name="userprofile" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="5e3b4-213">Elementos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-213">Elements</span></span>  
  
|<span data-ttu-id="5e3b4-214">Nome</span><span class="sxs-lookup"><span data-stu-id="5e3b4-214">Name</span></span>|<span data-ttu-id="5e3b4-215">Descrição</span><span class="sxs-lookup"><span data-stu-id="5e3b4-215">Description</span></span>|<span data-ttu-id="5e3b4-216">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5e3b4-216">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5e3b4-217">cache-lookup-value</span><span class="sxs-lookup"><span data-stu-id="5e3b4-217">cache-lookup-value</span></span>|<span data-ttu-id="5e3b4-218">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-218">Root element.</span></span>|<span data-ttu-id="5e3b4-219">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-219">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5e3b4-220">Atributos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-220">Attributes</span></span>  
  
|<span data-ttu-id="5e3b4-221">Nome</span><span class="sxs-lookup"><span data-stu-id="5e3b4-221">Name</span></span>|<span data-ttu-id="5e3b4-222">Descrição</span><span class="sxs-lookup"><span data-stu-id="5e3b4-222">Description</span></span>|<span data-ttu-id="5e3b4-223">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5e3b4-223">Required</span></span>|<span data-ttu-id="5e3b4-224">Padrão</span><span class="sxs-lookup"><span data-stu-id="5e3b4-224">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5e3b4-225">default-value</span><span class="sxs-lookup"><span data-stu-id="5e3b4-225">default-value</span></span>|<span data-ttu-id="5e3b4-226">Um valor que será atribuído toohello variável se a pesquisa de chave de cache Olá resultou em um erro.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-226">A value that will be assigned toohello variable if hello cache key lookup resulted in a miss.</span></span> <span data-ttu-id="5e3b4-227">Se esse atributo não for especificado, `null` é atribuído.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-227">If this attribute is not specified, `null` is assigned.</span></span>|<span data-ttu-id="5e3b4-228">Não</span><span class="sxs-lookup"><span data-stu-id="5e3b4-228">No</span></span>|`null`|  
|<span data-ttu-id="5e3b4-229">chave</span><span class="sxs-lookup"><span data-stu-id="5e3b4-229">key</span></span>|<span data-ttu-id="5e3b4-230">Toouse de valor de chave na pesquisa de saudação do cache.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-230">Cache key value toouse in hello lookup.</span></span>|<span data-ttu-id="5e3b4-231">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-231">Yes</span></span>|<span data-ttu-id="5e3b4-232">N/D</span><span class="sxs-lookup"><span data-stu-id="5e3b4-232">N/A</span></span>|  
|<span data-ttu-id="5e3b4-233">variable-name</span><span class="sxs-lookup"><span data-stu-id="5e3b4-233">variable-name</span></span>|<span data-ttu-id="5e3b4-234">Nome da saudação [variável de contexto](api-management-policy-expressions.md#ContextVariables) Olá pesquisado o valor será atribuído, se a pesquisa for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-234">Name of hello [context variable](api-management-policy-expressions.md#ContextVariables) hello looked up value will be assigned to, if lookup is successful.</span></span> <span data-ttu-id="5e3b4-235">Se a pesquisa resulta em um erro, variável Olá será atribuído valor Olá Olá `default-value` atributo ou `null`, se hello `default-value` atributo for omitido.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-235">If lookup results in a miss, hello variable will be assigned hello value of hello `default-value` attribute or `null`, if hello `default-value` attribute is omitted.</span></span>|<span data-ttu-id="5e3b4-236">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-236">Yes</span></span>|<span data-ttu-id="5e3b4-237">N/D</span><span class="sxs-lookup"><span data-stu-id="5e3b4-237">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5e3b4-238">Uso</span><span class="sxs-lookup"><span data-stu-id="5e3b4-238">Usage</span></span>  
 <span data-ttu-id="5e3b4-239">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="5e3b4-239">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5e3b4-240">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="5e3b4-240">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="5e3b4-241">**Escopos de política:** global, API, operação, produto</span><span class="sxs-lookup"><span data-stu-id="5e3b4-241">**Policy scopes:** global, API, operation, product</span></span>  
  
##  <span data-ttu-id="5e3b4-242"><a name="StoreToCacheByKey"></a> Armazenar valor em cache</span><span class="sxs-lookup"><span data-stu-id="5e3b4-242"><a name="StoreToCacheByKey"></a> Store value in cache</span></span>  
 <span data-ttu-id="5e3b4-243">Olá `cache-store-value` executa o armazenamento em cache por chave.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-243">hello `cache-store-value` performs cache storage by key.</span></span> <span data-ttu-id="5e3b4-244">chave de saudação pode ter um valor de cadeia de caracteres arbitrária e normalmente é fornecido usando uma expressão de política.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-244">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="5e3b4-245">Esta política deve ter uma política [Obter valor do cache](#GetFromCacheByKey) correspondente.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-245">This policy must have a corresponding [Get value from cache](#GetFromCacheByKey) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="5e3b4-246">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="5e3b4-246">Policy statement</span></span>  
  
```xml  
<cache-store-value key="cache key value" value="value toocache" duration="seconds" />  
```  
  
### <a name="example"></a><span data-ttu-id="5e3b4-247">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5e3b4-247">Example</span></span>  
 <span data-ttu-id="5e3b4-248">Para saber mais e obter exemplos dessa política, veja [Cache personalizado no Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span><span class="sxs-lookup"><span data-stu-id="5e3b4-248">For more information and examples of this policy, see [Custom caching in Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-cache-by-key/).</span></span>  
  
```xml  
<cache-store-value  
    key="@("userprofile-" + context.Variables["enduserid"])"  
    value="@((string)context.Variables["userprofile"])" duration="100000" />  
  
```  
  
### <a name="elements"></a><span data-ttu-id="5e3b4-249">Elementos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-249">Elements</span></span>  
  
|<span data-ttu-id="5e3b4-250">Nome</span><span class="sxs-lookup"><span data-stu-id="5e3b4-250">Name</span></span>|<span data-ttu-id="5e3b4-251">Descrição</span><span class="sxs-lookup"><span data-stu-id="5e3b4-251">Description</span></span>|<span data-ttu-id="5e3b4-252">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5e3b4-252">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5e3b4-253">cache-store-value</span><span class="sxs-lookup"><span data-stu-id="5e3b4-253">cache-store-value</span></span>|<span data-ttu-id="5e3b4-254">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-254">Root element.</span></span>|<span data-ttu-id="5e3b4-255">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-255">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="5e3b4-256">Atributos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-256">Attributes</span></span>  
  
|<span data-ttu-id="5e3b4-257">Nome</span><span class="sxs-lookup"><span data-stu-id="5e3b4-257">Name</span></span>|<span data-ttu-id="5e3b4-258">Descrição</span><span class="sxs-lookup"><span data-stu-id="5e3b4-258">Description</span></span>|<span data-ttu-id="5e3b4-259">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5e3b4-259">Required</span></span>|<span data-ttu-id="5e3b4-260">Padrão</span><span class="sxs-lookup"><span data-stu-id="5e3b4-260">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5e3b4-261">duration</span><span class="sxs-lookup"><span data-stu-id="5e3b4-261">duration</span></span>|<span data-ttu-id="5e3b4-262">Valor serão armazenadas em cache para Olá fornecido valor de duração, especificado em segundos.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-262">Value will be cached for hello provided duration value, specified in seconds.</span></span>|<span data-ttu-id="5e3b4-263">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-263">Yes</span></span>|<span data-ttu-id="5e3b4-264">N/D</span><span class="sxs-lookup"><span data-stu-id="5e3b4-264">N/A</span></span>|  
|<span data-ttu-id="5e3b4-265">chave</span><span class="sxs-lookup"><span data-stu-id="5e3b4-265">key</span></span>|<span data-ttu-id="5e3b4-266">Valor de chave saudação do cache será armazenado em.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-266">Cache key hello value will be stored under.</span></span>|<span data-ttu-id="5e3b4-267">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-267">Yes</span></span>|<span data-ttu-id="5e3b4-268">N/D</span><span class="sxs-lookup"><span data-stu-id="5e3b4-268">N/A</span></span>|  
|<span data-ttu-id="5e3b4-269">valor</span><span class="sxs-lookup"><span data-stu-id="5e3b4-269">value</span></span>|<span data-ttu-id="5e3b4-270">Olá toobe de valor armazenado em cache.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-270">hello value toobe cached.</span></span>|<span data-ttu-id="5e3b4-271">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-271">Yes</span></span>|<span data-ttu-id="5e3b4-272">N/D</span><span class="sxs-lookup"><span data-stu-id="5e3b4-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="5e3b4-273">Uso</span><span class="sxs-lookup"><span data-stu-id="5e3b4-273">Usage</span></span>  
 <span data-ttu-id="5e3b4-274">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="5e3b4-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="5e3b4-275">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="5e3b4-275">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="5e3b4-276">**Escopos de política:** global, API, operação, produto</span><span class="sxs-lookup"><span data-stu-id="5e3b4-276">**Policy scopes:** global, API, operation, product</span></span>  
  
###  <span data-ttu-id="5e3b4-277"><a name="RemoveCacheByKey"></a> Remover valor do cache</span><span class="sxs-lookup"><span data-stu-id="5e3b4-277"><a name="RemoveCacheByKey"></a> Remove value from cache</span></span>  
 <span data-ttu-id="5e3b4-278">Olá `cache-remove-value` exclui um item em cache identificado por sua chave.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-278">hello             `cache-remove-value` deletes a cached item identified by its key.</span></span> <span data-ttu-id="5e3b4-279">chave de saudação pode ter um valor de cadeia de caracteres arbitrária e normalmente é fornecido usando uma expressão de política.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-279">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span>  
  
#### <a name="policy-statement"></a><span data-ttu-id="5e3b4-280">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="5e3b4-280">Policy statement</span></span>  
  
```xml  
  
<cache-remove-value key="cache key value"/>  
  
```  
  
#### <a name="example"></a><span data-ttu-id="5e3b4-281">Exemplo</span><span class="sxs-lookup"><span data-stu-id="5e3b4-281">Example</span></span>  
  
```xml  
  
<cache-remove-value key="@("userprofile-" + context.Variables["enduserid"])"/>  
  
```  
  
#### <a name="elements"></a><span data-ttu-id="5e3b4-282">Elementos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-282">Elements</span></span>  
  
|<span data-ttu-id="5e3b4-283">Nome</span><span class="sxs-lookup"><span data-stu-id="5e3b4-283">Name</span></span>|<span data-ttu-id="5e3b4-284">Descrição</span><span class="sxs-lookup"><span data-stu-id="5e3b4-284">Description</span></span>|<span data-ttu-id="5e3b4-285">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5e3b4-285">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="5e3b4-286">cache-remove-value</span><span class="sxs-lookup"><span data-stu-id="5e3b4-286">cache-remove-value</span></span>|<span data-ttu-id="5e3b4-287">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-287">Root element.</span></span>|<span data-ttu-id="5e3b4-288">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-288">Yes</span></span>|  
  
#### <a name="attributes"></a><span data-ttu-id="5e3b4-289">Atributos</span><span class="sxs-lookup"><span data-stu-id="5e3b4-289">Attributes</span></span>  
  
|<span data-ttu-id="5e3b4-290">Nome</span><span class="sxs-lookup"><span data-stu-id="5e3b4-290">Name</span></span>|<span data-ttu-id="5e3b4-291">Descrição</span><span class="sxs-lookup"><span data-stu-id="5e3b4-291">Description</span></span>|<span data-ttu-id="5e3b4-292">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="5e3b4-292">Required</span></span>|<span data-ttu-id="5e3b4-293">Padrão</span><span class="sxs-lookup"><span data-stu-id="5e3b4-293">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="5e3b4-294">chave</span><span class="sxs-lookup"><span data-stu-id="5e3b4-294">key</span></span>|<span data-ttu-id="5e3b4-295">chave de saudação do hello previamente armazenados em cache toobe valor removido do cache de saudação.</span><span class="sxs-lookup"><span data-stu-id="5e3b4-295">hello key of hello previously cached value toobe removed from hello cache.</span></span>|<span data-ttu-id="5e3b4-296">Sim</span><span class="sxs-lookup"><span data-stu-id="5e3b4-296">Yes</span></span>|<span data-ttu-id="5e3b4-297">N/D</span><span class="sxs-lookup"><span data-stu-id="5e3b4-297">N/A</span></span>|  
  
#### <a name="usage"></a><span data-ttu-id="5e3b4-298">Uso</span><span class="sxs-lookup"><span data-stu-id="5e3b4-298">Usage</span></span>  
 <span data-ttu-id="5e3b4-299">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span><span class="sxs-lookup"><span data-stu-id="5e3b4-299">This policy can be used in hello following policy                    [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and                   [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) .</span></span>  
  
-   <span data-ttu-id="5e3b4-300">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="5e3b4-300">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="5e3b4-301">**Escopos de política:** global, API, operação, produto</span><span class="sxs-lookup"><span data-stu-id="5e3b4-301">**Policy scopes:** global, API, operation, product</span></span>  
  

## <a name="next-steps"></a><span data-ttu-id="5e3b4-302">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5e3b4-302">Next steps</span></span>
<span data-ttu-id="5e3b4-303">Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="5e3b4-303">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  