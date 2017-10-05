---
title: "Políticas entre domínios de Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba mais sobre as políticas entre domínios disponíveis para uso no Gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7689d277-8abe-472a-a78c-e6d4bd43455d
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: ddca9e35b44a21294abbb5eaa4418bcdb85494cf
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="d4989-103">Políticas entre domínios de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="d4989-103">API Management cross domain policies</span></span>
<span data-ttu-id="d4989-104">Este tópico fornece uma referência para as políticas de Gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4989-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="d4989-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="d4989-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="d4989-106"><a name="CrossDomainPolicies"></a> Políticas entre domínios</span><span class="sxs-lookup"><span data-stu-id="d4989-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="d4989-107">[Permitir chamadas entre domínios](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Torna a API acessível por meio de clientes Adobe Flash e Microsoft Silverlight baseados em navegadores.</span><span class="sxs-lookup"><span data-stu-id="d4989-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="d4989-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adicionar suporte de compartilhamento de recursos entre origens (CORS) a uma operação ou a uma API para permitir chamadas entre domínios de clientes baseados em navegadores.</span><span class="sxs-lookup"><span data-stu-id="d4989-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="d4989-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adiciona suporte JSON com preenchimento (JSONP) a uma operação ou a uma API para permitir chamadas entre domínios de clientes JavaScript baseados em navegadores.</span><span class="sxs-lookup"><span data-stu-id="d4989-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="d4989-110"><a name="AllowCrossDomainCalls"></a> Permitir chamadas entre domínios</span><span class="sxs-lookup"><span data-stu-id="d4989-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="d4989-111">Use a política `cross-domain` para tornar a API acessível por clientes baseados em navegadores do Adobe Flash e do Microsoft Silverlight.</span><span class="sxs-lookup"><span data-stu-id="d4989-111">Use the `cross-domain` policy to make the API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d4989-112">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="d4989-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in the Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="d4989-113">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d4989-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="d4989-114">Elementos</span><span class="sxs-lookup"><span data-stu-id="d4989-114">Elements</span></span>  
  
|<span data-ttu-id="d4989-115">Nome</span><span class="sxs-lookup"><span data-stu-id="d4989-115">Name</span></span>|<span data-ttu-id="d4989-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4989-116">Description</span></span>|<span data-ttu-id="d4989-117">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d4989-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d4989-118">cross-domain</span><span class="sxs-lookup"><span data-stu-id="d4989-118">cross-domain</span></span>|<span data-ttu-id="d4989-119">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="d4989-119">Root element.</span></span> <span data-ttu-id="d4989-120">Elementos filho devem estar de acordo com a [Especificação de arquivo de política entre domínios do Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="d4989-120">Child elements must conform to the [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="d4989-121">Sim</span><span class="sxs-lookup"><span data-stu-id="d4989-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d4989-122">Uso</span><span class="sxs-lookup"><span data-stu-id="d4989-122">Usage</span></span>  
 <span data-ttu-id="d4989-123">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4989-123">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d4989-124">**Seções de política:** entrada</span><span class="sxs-lookup"><span data-stu-id="d4989-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d4989-125">**Escopos de política:** global</span><span class="sxs-lookup"><span data-stu-id="d4989-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="d4989-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="d4989-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="d4989-127">A política `cors` adiciona suporte do CORS (compartilhamento de recurso entre origens) a uma operação ou API para permitir chamadas entre domínios de clientes baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="d4989-127">The `cors` policy adds cross-origin resource sharing (CORS) support to an operation or an API to allow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="d4989-128">O CORS permite que um navegador e um servidor interajam e determina e solicitações entre origens específicas devem ou não ser aceitas (por exemplo, chamadas XMLHttpRequests feitas por meio de JavaScript em uma página da Web para outros domínios).</span><span class="sxs-lookup"><span data-stu-id="d4989-128">CORS allows a browser and a server to interact and determine whether or not to allow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page to other domains).</span></span> <span data-ttu-id="d4989-129">Isso permite maior flexibilidade do que permitir somente solicitações com a mesma origem, mas é mais seguro do que permitir todas as solicitações entre origens.</span><span class="sxs-lookup"><span data-stu-id="d4989-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d4989-130">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="d4989-130">Policy statement</span></span>  
  
```xml  
<cors allow-credentials="false|true">  
    <allowed-origins>  
        <origin>origin uri</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="number of seconds">  
        <method>http verb</method>  
    </allowed-methods>  
    <allowed-headers>  
        <header>header name</header>  
    </allowed-headers>  
    <expose-headers>  
        <header>header name</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="example"></a><span data-ttu-id="d4989-131">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d4989-131">Example</span></span>  
 <span data-ttu-id="d4989-132">Este exemplo demonstra como dar suporte a solicitações preliminares, como as com cabeçalhos personalizados ou métodos diferentes de GET e POST.</span><span class="sxs-lookup"><span data-stu-id="d4989-132">This example demonstrates how to support pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="d4989-133">Para oferecer suporte a cabeçalhos personalizados e verbos HTTP adicionais, use as seções `allowed-methods` e `allowed-headers` conforme mostrado no exemplo a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4989-133">To support custom headers and additional HTTP verbs, use the `allowed-methods` and `allowed-headers` sections as shown in the following example.</span></span>  
  
```xml  
<cors allow-credentials="true">  
    <allowed-origins>  
        <!-- Localhost useful for development -->  
        <origin>http://localhost:8080/</origin>  
        <origin>http://example.com/</origin>  
    </allowed-origins>  
    <allowed-methods preflight-result-max-age="300">  
        <method>GET</method>  
        <method>POST</method>  
        <method>PATCH</method>  
        <method>DELETE</method>  
    </allowed-methods>  
    <allowed-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
        <header>x-zumo-version</header>  
        <header>x-zumo-auth</header>  
        <header>content-type</header>  
        <header>accept</header>  
    </allowed-headers>  
    <expose-headers>  
        <!-- Examples below show Azure Mobile Services headers -->  
        <header>x-zumo-installation-id</header>  
        <header>x-zumo-application</header>  
    </expose-headers>  
</cors>  
```  
  
### <a name="elements"></a><span data-ttu-id="d4989-134">Elementos</span><span class="sxs-lookup"><span data-stu-id="d4989-134">Elements</span></span>  
  
|<span data-ttu-id="d4989-135">Nome</span><span class="sxs-lookup"><span data-stu-id="d4989-135">Name</span></span>|<span data-ttu-id="d4989-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4989-136">Description</span></span>|<span data-ttu-id="d4989-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d4989-137">Required</span></span>|<span data-ttu-id="d4989-138">Padrão</span><span class="sxs-lookup"><span data-stu-id="d4989-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d4989-139">cors</span><span class="sxs-lookup"><span data-stu-id="d4989-139">cors</span></span>|<span data-ttu-id="d4989-140">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="d4989-140">Root element.</span></span>|<span data-ttu-id="d4989-141">Sim</span><span class="sxs-lookup"><span data-stu-id="d4989-141">Yes</span></span>|<span data-ttu-id="d4989-142">N/D</span><span class="sxs-lookup"><span data-stu-id="d4989-142">N/A</span></span>|  
|<span data-ttu-id="d4989-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="d4989-143">allowed-origins</span></span>|<span data-ttu-id="d4989-144">Contém elementos `origin` que descrevem as origens permitidas para solicitações entre domínios.</span><span class="sxs-lookup"><span data-stu-id="d4989-144">Contains `origin` elements that describe the allowed origins for cross-domain requests.</span></span> <span data-ttu-id="d4989-145">`allowed-origins` pode conter um único elemento `origin` que especifica `*` para permitir qualquer origem, ou um ou mais elementos `origin` que contêm uma URI.</span><span class="sxs-lookup"><span data-stu-id="d4989-145">`allowed-origins` can contain either a single `origin` element that specifies `*` to allow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="d4989-146">Sim</span><span class="sxs-lookup"><span data-stu-id="d4989-146">Yes</span></span>|<span data-ttu-id="d4989-147">N/D</span><span class="sxs-lookup"><span data-stu-id="d4989-147">N/A</span></span>|  
|<span data-ttu-id="d4989-148">origin</span><span class="sxs-lookup"><span data-stu-id="d4989-148">origin</span></span>|<span data-ttu-id="d4989-149">O valor pode ser `*` para permitir todas as origens ou um URI que especifica uma origem única.</span><span class="sxs-lookup"><span data-stu-id="d4989-149">The value can be either `*` to allow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="d4989-150">O URI deve incluir um esquema, um host e uma porta.</span><span class="sxs-lookup"><span data-stu-id="d4989-150">The URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="d4989-151">Sim</span><span class="sxs-lookup"><span data-stu-id="d4989-151">Yes</span></span>|<span data-ttu-id="d4989-152">Se a porta for omitida em um URI, a porta 80 é usada para HTTP e a porta 443 é usada para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="d4989-152">If the port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="d4989-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="d4989-153">allowed-methods</span></span>|<span data-ttu-id="d4989-154">Esse elemento é necessário se métodos diferentes de GET ou POST forem permitidos.</span><span class="sxs-lookup"><span data-stu-id="d4989-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="d4989-155">Contém elementos `method` que especificam os verbos HTTP compatíveis.</span><span class="sxs-lookup"><span data-stu-id="d4989-155">Contains `method` elements that specify the supported HTTP verbs.</span></span>|<span data-ttu-id="d4989-156">Não</span><span class="sxs-lookup"><span data-stu-id="d4989-156">No</span></span>|<span data-ttu-id="d4989-157">Se esta seção não estiver presente, GET e POST são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="d4989-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="d4989-158">estático</span><span class="sxs-lookup"><span data-stu-id="d4989-158">method</span></span>|<span data-ttu-id="d4989-159">Especifica um verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="d4989-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="d4989-160">Pelo menos um elemento `method` é necessário se a seção `allowed-methods` estiver presente.</span><span class="sxs-lookup"><span data-stu-id="d4989-160">At least one `method` element is required if the `allowed-methods` section is present.</span></span>|<span data-ttu-id="d4989-161">N/D</span><span class="sxs-lookup"><span data-stu-id="d4989-161">N/A</span></span>|  
|<span data-ttu-id="d4989-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="d4989-162">allowed-headers</span></span>|<span data-ttu-id="d4989-163">Esse elemento contém elementos `header` que especificam os nomes dos cabeçalhos que podem ser incluídos na solicitação.</span><span class="sxs-lookup"><span data-stu-id="d4989-163">This element contains `header` elements specifying names of the headers that can be included in the request.</span></span>|<span data-ttu-id="d4989-164">Não</span><span class="sxs-lookup"><span data-stu-id="d4989-164">No</span></span>|<span data-ttu-id="d4989-165">N/D</span><span class="sxs-lookup"><span data-stu-id="d4989-165">N/A</span></span>|  
|<span data-ttu-id="d4989-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="d4989-166">expose-headers</span></span>|<span data-ttu-id="d4989-167">Esse elemento contém elementos `header` que especificam os nomes dos cabeçalhos que ficarão acessíveis para o cliente.</span><span class="sxs-lookup"><span data-stu-id="d4989-167">This element contains `header` elements specifying names of the headers that will be accessible by the client.</span></span>|<span data-ttu-id="d4989-168">Não</span><span class="sxs-lookup"><span data-stu-id="d4989-168">No</span></span>|<span data-ttu-id="d4989-169">N/D</span><span class="sxs-lookup"><span data-stu-id="d4989-169">N/A</span></span>|  
|<span data-ttu-id="d4989-170">cabeçalho</span><span class="sxs-lookup"><span data-stu-id="d4989-170">header</span></span>|<span data-ttu-id="d4989-171">Especifica um nome de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="d4989-171">Specifies a header name.</span></span>|<span data-ttu-id="d4989-172">Pelo menos um elemento `header` é necessário em `allowed-headers` ou `expose-headers` se a seção estiver presente.</span><span class="sxs-lookup"><span data-stu-id="d4989-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if the section is present.</span></span>|<span data-ttu-id="d4989-173">N/D</span><span class="sxs-lookup"><span data-stu-id="d4989-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d4989-174">Atributos</span><span class="sxs-lookup"><span data-stu-id="d4989-174">Attributes</span></span>  
  
|<span data-ttu-id="d4989-175">Nome</span><span class="sxs-lookup"><span data-stu-id="d4989-175">Name</span></span>|<span data-ttu-id="d4989-176">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4989-176">Description</span></span>|<span data-ttu-id="d4989-177">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d4989-177">Required</span></span>|<span data-ttu-id="d4989-178">Padrão</span><span class="sxs-lookup"><span data-stu-id="d4989-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d4989-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="d4989-179">allow-credentials</span></span>|<span data-ttu-id="d4989-180">O cabeçalho `Access-Control-Allow-Credentials` na resposta preliminar será definido com o valor desse atributo e afetará a capacidade do cliente para enviar credenciais nas solicitações entre domínios.</span><span class="sxs-lookup"><span data-stu-id="d4989-180">The `Access-Control-Allow-Credentials` header in the preflight response will be set to the value of this attribute and affect the client’s ability to submit credentials in cross-domain requests.</span></span>|<span data-ttu-id="d4989-181">Não</span><span class="sxs-lookup"><span data-stu-id="d4989-181">No</span></span>|<span data-ttu-id="d4989-182">false</span><span class="sxs-lookup"><span data-stu-id="d4989-182">false</span></span>|  
|<span data-ttu-id="d4989-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="d4989-183">preflight-result-max-age</span></span>|<span data-ttu-id="d4989-184">O cabeçalho `Access-Control-Max-Age` na resposta preliminar será definido com o valor desse atributo e afetará a capacidade do agente do usuário para colocar em cache a resposta preliminar.</span><span class="sxs-lookup"><span data-stu-id="d4989-184">The `Access-Control-Max-Age` header in the preflight response will be set to the value of this attribute and affect the user agent’s ability to cache pre-flight response.</span></span>|<span data-ttu-id="d4989-185">Não</span><span class="sxs-lookup"><span data-stu-id="d4989-185">No</span></span>|<span data-ttu-id="d4989-186">0</span><span class="sxs-lookup"><span data-stu-id="d4989-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d4989-187">Uso</span><span class="sxs-lookup"><span data-stu-id="d4989-187">Usage</span></span>  
 <span data-ttu-id="d4989-188">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4989-188">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d4989-189">**Seções de política:** entrada</span><span class="sxs-lookup"><span data-stu-id="d4989-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="d4989-190">**Escopos de política:** API, operação</span><span class="sxs-lookup"><span data-stu-id="d4989-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="d4989-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="d4989-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="d4989-192">A política `jsonp` adiciona suporte a JSONP com padding (JSONP) a uma operação ou API para permitir chamadas entre domínios de clientes JavaScript baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="d4989-192">The `jsonp` policy adds JSON with padding (JSONP) support to an operation or an API to allow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="d4989-193">O JSONP é um método usado em programas JavaScript para solicitar dados de um servidor em um domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="d4989-193">JSONP is a method used in JavaScript programs to request data from a server in a different domain.</span></span> <span data-ttu-id="d4989-194">O JSONP ignora a limitação aplicada pela maioria dos navegadores da Web quando o acesso às páginas da Web precisa ser do mesmo domínio.</span><span class="sxs-lookup"><span data-stu-id="d4989-194">JSONP bypasses the limitation enforced by most web browsers where access to web pages must be in the same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="d4989-195">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="d4989-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="d4989-196">Exemplo</span><span class="sxs-lookup"><span data-stu-id="d4989-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="d4989-197">Se você chamar o método sem o parâmetro de retorno de chamada ?cb=XXX, será retornado o JSON simples (sem um wrapper de chamada de função).</span><span class="sxs-lookup"><span data-stu-id="d4989-197">If you call the method without the callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="d4989-198">Se você adicionar o parâmetro de retorno de chamada `?cb=XXX`, será retornado um resultado JSONP, dispondo os resultados JSON originais em torno da função de retorno de chamada como `XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="d4989-198">If you add the callback parameter `?cb=XXX` it will return a JSONP result, wrapping the original JSON results around the callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="d4989-199">Elementos</span><span class="sxs-lookup"><span data-stu-id="d4989-199">Elements</span></span>  
  
|<span data-ttu-id="d4989-200">Nome</span><span class="sxs-lookup"><span data-stu-id="d4989-200">Name</span></span>|<span data-ttu-id="d4989-201">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4989-201">Description</span></span>|<span data-ttu-id="d4989-202">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d4989-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="d4989-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="d4989-203">jsonp</span></span>|<span data-ttu-id="d4989-204">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="d4989-204">Root element.</span></span>|<span data-ttu-id="d4989-205">Sim</span><span class="sxs-lookup"><span data-stu-id="d4989-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="d4989-206">Atributos</span><span class="sxs-lookup"><span data-stu-id="d4989-206">Attributes</span></span>  
  
|<span data-ttu-id="d4989-207">Nome</span><span class="sxs-lookup"><span data-stu-id="d4989-207">Name</span></span>|<span data-ttu-id="d4989-208">Descrição</span><span class="sxs-lookup"><span data-stu-id="d4989-208">Description</span></span>|<span data-ttu-id="d4989-209">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="d4989-209">Required</span></span>|<span data-ttu-id="d4989-210">Padrão</span><span class="sxs-lookup"><span data-stu-id="d4989-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="d4989-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="d4989-211">callback-parameter-name</span></span>|<span data-ttu-id="d4989-212">A chamada da função JavaScript entre domínios, prefixada com o nome do domínio onde a função reside totalmente qualificado.</span><span class="sxs-lookup"><span data-stu-id="d4989-212">The cross-domain JavaScript function call prefixed with the fully qualified domain name where the function resides.</span></span>|<span data-ttu-id="d4989-213">Sim</span><span class="sxs-lookup"><span data-stu-id="d4989-213">Yes</span></span>|<span data-ttu-id="d4989-214">N/D</span><span class="sxs-lookup"><span data-stu-id="d4989-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="d4989-215">Uso</span><span class="sxs-lookup"><span data-stu-id="d4989-215">Usage</span></span>  
 <span data-ttu-id="d4989-216">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="d4989-216">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="d4989-217">**Seções de política:** saída</span><span class="sxs-lookup"><span data-stu-id="d4989-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="d4989-218">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="d4989-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="d4989-219">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="d4989-219">Next steps</span></span>
<span data-ttu-id="d4989-220">Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="d4989-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  