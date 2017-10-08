---
title: "Gerenciamento de API de aaaAzure políticas entre domínios | Microsoft Docs"
description: "Saiba mais sobre Olá políticas entre domínios disponíveis para uso no gerenciamento de API do Azure."
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
ms.openlocfilehash: dd5ebfd65b92ebd0c1f589a2bac669a3928d40b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-cross-domain-policies"></a><span data-ttu-id="6f8d6-103">Políticas entre domínios de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="6f8d6-103">API Management cross domain policies</span></span>
<span data-ttu-id="6f8d6-104">Este tópico fornece uma referência para Olá políticas de gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="6f8d6-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="6f8d6-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="6f8d6-106"><a name="CrossDomainPolicies"></a> Políticas entre domínios</span><span class="sxs-lookup"><span data-stu-id="6f8d6-106"><a name="CrossDomainPolicies"></a> Cross domain policies</span></span>  
  
-   <span data-ttu-id="6f8d6-107">[Permitir chamadas entre domínios](api-management-cross-domain-policies.md#AllowCrossDomainCalls) -torna Olá API acessível de clientes baseados em navegador Microsoft Silverlight e Adobe Flash.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-107">[Allow cross-domain calls](api-management-cross-domain-policies.md#AllowCrossDomainCalls) - Makes hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
-   <span data-ttu-id="6f8d6-108">[CORS](api-management-cross-domain-policies.md#CORS) -adiciona o compartilhamento de recursos entre origens (CORS) suporte para a operação de tooan ou chama um API entre tooallow domínios de clientes baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-108">[CORS](api-management-cross-domain-policies.md#CORS) - Adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
-   <span data-ttu-id="6f8d6-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - adiciona JSON com a operação de tooan de suporte de preenchimento (JSONP) ou chama um API entre tooallow domínios de clientes baseados em navegador do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-109">[JSONP](api-management-cross-domain-policies.md#JSONP) - Adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span>  
  
##  <span data-ttu-id="6f8d6-110"><a name="AllowCrossDomainCalls"></a> Permitir chamadas entre domínios</span><span class="sxs-lookup"><span data-stu-id="6f8d6-110"><a name="AllowCrossDomainCalls"></a> Allow cross-domain calls</span></span>  
 <span data-ttu-id="6f8d6-111">Saudação de uso `cross-domain` Olá toomake de política API acessível de clientes baseados em navegador Microsoft Silverlight e Adobe Flash.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-111">Use hello `cross-domain` policy toomake hello API accessible from Adobe Flash and Microsoft Silverlight browser-based clients.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6f8d6-112">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="6f8d6-112">Policy statement</span></span>  
  
```xml  
<cross-domain>  
   <!-Policy configuration is in hello Adobe cross-domain policy file format,   
      see http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html-->  
</cross-domain>  
```  
  
### <a name="example"></a><span data-ttu-id="6f8d6-113">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6f8d6-113">Example</span></span>  
  
```xml  
<cross-domain>  
    <cross-domain-policy>  
        <allow-http-request-headers-from domain='*' headers='*' />  
    </cross-domain-policy>  
</cross-domain>  
```  
  
### <a name="elements"></a><span data-ttu-id="6f8d6-114">Elementos</span><span class="sxs-lookup"><span data-stu-id="6f8d6-114">Elements</span></span>  
  
|<span data-ttu-id="6f8d6-115">Nome</span><span class="sxs-lookup"><span data-stu-id="6f8d6-115">Name</span></span>|<span data-ttu-id="6f8d6-116">Descrição</span><span class="sxs-lookup"><span data-stu-id="6f8d6-116">Description</span></span>|<span data-ttu-id="6f8d6-117">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6f8d6-117">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="6f8d6-118">cross-domain</span><span class="sxs-lookup"><span data-stu-id="6f8d6-118">cross-domain</span></span>|<span data-ttu-id="6f8d6-119">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-119">Root element.</span></span> <span data-ttu-id="6f8d6-120">Elementos filho devem estar de acordo com toohello [especificação de arquivo de política entre domínios do Adobe](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span><span class="sxs-lookup"><span data-stu-id="6f8d6-120">Child elements must conform toohello [Adobe cross-domain policy file specification](http://www.adobe.com/devnet/articles/crossdomain_policy_file_spec.html).</span></span>|<span data-ttu-id="6f8d6-121">Sim</span><span class="sxs-lookup"><span data-stu-id="6f8d6-121">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6f8d6-122">Uso</span><span class="sxs-lookup"><span data-stu-id="6f8d6-122">Usage</span></span>  
 <span data-ttu-id="6f8d6-123">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="6f8d6-123">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6f8d6-124">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="6f8d6-124">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="6f8d6-125">**Escopos de política:** global</span><span class="sxs-lookup"><span data-stu-id="6f8d6-125">**Policy scopes:** global</span></span>  
  
##  <span data-ttu-id="6f8d6-126"><a name="CORS"></a> CORS</span><span class="sxs-lookup"><span data-stu-id="6f8d6-126"><a name="CORS"></a> CORS</span></span>  
 <span data-ttu-id="6f8d6-127">Olá `cors` política adiciona o compartilhamento de recursos entre origens (CORS) suporte para a operação de tooan ou chama um API entre tooallow domínios de clientes baseados em navegador.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-127">hello `cors` policy adds cross-origin resource sharing (CORS) support tooan operation or an API tooallow cross-domain calls from browser-based clients.</span></span>  
  
 <span data-ttu-id="6f8d6-128">CORS permite que um navegador e um servidor toointeract e determinar se as solicitações de tooallow específicas entre origens (ou seja, chamadas XMLHttpRequests feitas do JavaScript em domínios de tooother uma página da web).</span><span class="sxs-lookup"><span data-stu-id="6f8d6-128">CORS allows a browser and a server toointeract and determine whether or not tooallow specific cross-origin requests (i.e. XMLHttpRequests calls made from JavaScript on a web page tooother domains).</span></span> <span data-ttu-id="6f8d6-129">Isso permite maior flexibilidade do que permitir somente solicitações com a mesma origem, mas é mais seguro do que permitir todas as solicitações entre origens.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-129">This allows for more flexibility than only allowing same-origin requests, but is more secure than allowing all cross-origin requests.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6f8d6-130">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="6f8d6-130">Policy statement</span></span>  
  
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
  
### <a name="example"></a><span data-ttu-id="6f8d6-131">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6f8d6-131">Example</span></span>  
 <span data-ttu-id="6f8d6-132">Este exemplo demonstra como solicitar toosupport preliminares, como aquelas com cabeçalhos personalizados ou métodos diferentes de GET e POST.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-132">This example demonstrates how toosupport pre-flight requests, such as those with custom headers or methods other than GET and POST.</span></span> <span data-ttu-id="6f8d6-133">cabeçalhos personalizados toosupport e verbos HTTP adicionais, use Olá `allowed-methods` e `allowed-headers` seções, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-133">toosupport custom headers and additional HTTP verbs, use hello `allowed-methods` and `allowed-headers` sections as shown in hello following example.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="6f8d6-134">Elementos</span><span class="sxs-lookup"><span data-stu-id="6f8d6-134">Elements</span></span>  
  
|<span data-ttu-id="6f8d6-135">Nome</span><span class="sxs-lookup"><span data-stu-id="6f8d6-135">Name</span></span>|<span data-ttu-id="6f8d6-136">Descrição</span><span class="sxs-lookup"><span data-stu-id="6f8d6-136">Description</span></span>|<span data-ttu-id="6f8d6-137">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6f8d6-137">Required</span></span>|<span data-ttu-id="6f8d6-138">Padrão</span><span class="sxs-lookup"><span data-stu-id="6f8d6-138">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6f8d6-139">cors</span><span class="sxs-lookup"><span data-stu-id="6f8d6-139">cors</span></span>|<span data-ttu-id="6f8d6-140">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-140">Root element.</span></span>|<span data-ttu-id="6f8d6-141">Sim</span><span class="sxs-lookup"><span data-stu-id="6f8d6-141">Yes</span></span>|<span data-ttu-id="6f8d6-142">N/D</span><span class="sxs-lookup"><span data-stu-id="6f8d6-142">N/A</span></span>|  
|<span data-ttu-id="6f8d6-143">allowed-origins</span><span class="sxs-lookup"><span data-stu-id="6f8d6-143">allowed-origins</span></span>|<span data-ttu-id="6f8d6-144">Contém `origin` elementos que descrevem a saudação permitida origens para solicitações entre domínios.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-144">Contains `origin` elements that describe hello allowed origins for cross-domain requests.</span></span> <span data-ttu-id="6f8d6-145">`allowed-origins`pode conter um único `origin` elemento especifica `*` tooallow qualquer origem ou de um ou mais `origin` elementos que contêm um URI.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-145">`allowed-origins` can contain either a single `origin` element that specifies `*` tooallow any origin, or one or more `origin` elements that contain a URI.</span></span>|<span data-ttu-id="6f8d6-146">Sim</span><span class="sxs-lookup"><span data-stu-id="6f8d6-146">Yes</span></span>|<span data-ttu-id="6f8d6-147">N/D</span><span class="sxs-lookup"><span data-stu-id="6f8d6-147">N/A</span></span>|  
|<span data-ttu-id="6f8d6-148">origin</span><span class="sxs-lookup"><span data-stu-id="6f8d6-148">origin</span></span>|<span data-ttu-id="6f8d6-149">Olá valor pode ser `*` tooallow todas as origens ou um URI que especifica uma origem única.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-149">hello value can be either `*` tooallow all origins, or a URI that specifies a single origin.</span></span> <span data-ttu-id="6f8d6-150">Olá URI deve incluir um esquema, host e porta.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-150">hello URI must include a scheme, host, and port.</span></span>|<span data-ttu-id="6f8d6-151">Sim</span><span class="sxs-lookup"><span data-stu-id="6f8d6-151">Yes</span></span>|<span data-ttu-id="6f8d6-152">Se a porta de saudação for omitida em um URI, porta 80 é usada para HTTP e é usada a porta 443 para HTTPS.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-152">If hello port is omitted in a URI, port 80 is used for HTTP and port 443 is used for HTTPS.</span></span>|  
|<span data-ttu-id="6f8d6-153">allowed-methods</span><span class="sxs-lookup"><span data-stu-id="6f8d6-153">allowed-methods</span></span>|<span data-ttu-id="6f8d6-154">Esse elemento é necessário se métodos diferentes de GET ou POST forem permitidos.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-154">This element is required if methods other than GET or POST are allowed.</span></span> <span data-ttu-id="6f8d6-155">Contém `method` elementos que especificam a saudação suporte para verbos HTTP.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-155">Contains `method` elements that specify hello supported HTTP verbs.</span></span>|<span data-ttu-id="6f8d6-156">Não</span><span class="sxs-lookup"><span data-stu-id="6f8d6-156">No</span></span>|<span data-ttu-id="6f8d6-157">Se esta seção não estiver presente, GET e POST são compatíveis.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-157">If this section is not present, GET and POST are supported.</span></span>|  
|<span data-ttu-id="6f8d6-158">estático</span><span class="sxs-lookup"><span data-stu-id="6f8d6-158">method</span></span>|<span data-ttu-id="6f8d6-159">Especifica um verbo HTTP.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-159">Specifies an HTTP verb.</span></span>|<span data-ttu-id="6f8d6-160">Pelo menos um `method` elemento é necessário se hello `allowed-methods` seção estiver presente.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-160">At least one `method` element is required if hello `allowed-methods` section is present.</span></span>|<span data-ttu-id="6f8d6-161">N/D</span><span class="sxs-lookup"><span data-stu-id="6f8d6-161">N/A</span></span>|  
|<span data-ttu-id="6f8d6-162">allowed-headers</span><span class="sxs-lookup"><span data-stu-id="6f8d6-162">allowed-headers</span></span>|<span data-ttu-id="6f8d6-163">Esse elemento contém `header` elementos especificando os nomes dos cabeçalhos de saudação que podem ser incluídos na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-163">This element contains `header` elements specifying names of hello headers that can be included in hello request.</span></span>|<span data-ttu-id="6f8d6-164">Não</span><span class="sxs-lookup"><span data-stu-id="6f8d6-164">No</span></span>|<span data-ttu-id="6f8d6-165">N/D</span><span class="sxs-lookup"><span data-stu-id="6f8d6-165">N/A</span></span>|  
|<span data-ttu-id="6f8d6-166">expose-headers</span><span class="sxs-lookup"><span data-stu-id="6f8d6-166">expose-headers</span></span>|<span data-ttu-id="6f8d6-167">Esse elemento contém `header` elementos especificando os nomes dos cabeçalhos de saudação que poderá ser acessados pelo cliente hello.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-167">This element contains `header` elements specifying names of hello headers that will be accessible by hello client.</span></span>|<span data-ttu-id="6f8d6-168">Não</span><span class="sxs-lookup"><span data-stu-id="6f8d6-168">No</span></span>|<span data-ttu-id="6f8d6-169">N/D</span><span class="sxs-lookup"><span data-stu-id="6f8d6-169">N/A</span></span>|  
|<span data-ttu-id="6f8d6-170">cabeçalho</span><span class="sxs-lookup"><span data-stu-id="6f8d6-170">header</span></span>|<span data-ttu-id="6f8d6-171">Especifica um nome de cabeçalho.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-171">Specifies a header name.</span></span>|<span data-ttu-id="6f8d6-172">Pelo menos um `header` elemento é necessário em `allowed-headers` ou `expose-headers` se Olá seção estiver presente.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-172">At least one `header` element is required in `allowed-headers` or `expose-headers` if hello section is present.</span></span>|<span data-ttu-id="6f8d6-173">N/D</span><span class="sxs-lookup"><span data-stu-id="6f8d6-173">N/A</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="6f8d6-174">Atributos</span><span class="sxs-lookup"><span data-stu-id="6f8d6-174">Attributes</span></span>  
  
|<span data-ttu-id="6f8d6-175">Nome</span><span class="sxs-lookup"><span data-stu-id="6f8d6-175">Name</span></span>|<span data-ttu-id="6f8d6-176">Descrição</span><span class="sxs-lookup"><span data-stu-id="6f8d6-176">Description</span></span>|<span data-ttu-id="6f8d6-177">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6f8d6-177">Required</span></span>|<span data-ttu-id="6f8d6-178">Padrão</span><span class="sxs-lookup"><span data-stu-id="6f8d6-178">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6f8d6-179">allow-credentials</span><span class="sxs-lookup"><span data-stu-id="6f8d6-179">allow-credentials</span></span>|<span data-ttu-id="6f8d6-180">Olá `Access-Control-Allow-Credentials` cabeçalho de resposta de simulação hello serão toohello defina o valor desse atributo e afeta as credenciais de toosubmit de capacidade do cliente Olá nas solicitações entre domínios.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-180">hello `Access-Control-Allow-Credentials` header in hello preflight response will be set toohello value of this attribute and affect hello client’s ability toosubmit credentials in cross-domain requests.</span></span>|<span data-ttu-id="6f8d6-181">Não</span><span class="sxs-lookup"><span data-stu-id="6f8d6-181">No</span></span>|<span data-ttu-id="6f8d6-182">false</span><span class="sxs-lookup"><span data-stu-id="6f8d6-182">false</span></span>|  
|<span data-ttu-id="6f8d6-183">preflight-result-max-age</span><span class="sxs-lookup"><span data-stu-id="6f8d6-183">preflight-result-max-age</span></span>|<span data-ttu-id="6f8d6-184">Olá `Access-Control-Max-Age` cabeçalho de resposta de simulação hello serão toohello defina o valor desse atributo e afeta a resposta de simulação do agente do usuário Olá capacidade toocache.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-184">hello `Access-Control-Max-Age` header in hello preflight response will be set toohello value of this attribute and affect hello user agent’s ability toocache pre-flight response.</span></span>|<span data-ttu-id="6f8d6-185">Não</span><span class="sxs-lookup"><span data-stu-id="6f8d6-185">No</span></span>|<span data-ttu-id="6f8d6-186">0</span><span class="sxs-lookup"><span data-stu-id="6f8d6-186">0</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6f8d6-187">Uso</span><span class="sxs-lookup"><span data-stu-id="6f8d6-187">Usage</span></span>  
 <span data-ttu-id="6f8d6-188">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="6f8d6-188">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6f8d6-189">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="6f8d6-189">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="6f8d6-190">**Escopos de política:** API, operação</span><span class="sxs-lookup"><span data-stu-id="6f8d6-190">**Policy scopes:** API, operation</span></span>  
  
##  <span data-ttu-id="6f8d6-191"><a name="JSONP"></a> JSONP</span><span class="sxs-lookup"><span data-stu-id="6f8d6-191"><a name="JSONP"></a> JSONP</span></span>  
 <span data-ttu-id="6f8d6-192">Olá `jsonp` política adiciona JSON com preenchimento de operação de tooan de suporte (JSONP) ou um chamadas à API tooallow entre domínios de clientes baseados em navegador do JavaScript.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-192">hello `jsonp` policy adds JSON with padding (JSONP) support tooan operation or an API tooallow cross-domain calls from JavaScript browser-based clients.</span></span> <span data-ttu-id="6f8d6-193">JSONP é um método usado nos dados de toorequest programas JavaScript de um servidor em um domínio diferente.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-193">JSONP is a method used in JavaScript programs toorequest data from a server in a different domain.</span></span> <span data-ttu-id="6f8d6-194">JSONP ignora a limitação de saudação imposta pela maioria dos navegadores da web onde as páginas de acesso a tooweb devem estar no hello mesmo domínio.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-194">JSONP bypasses hello limitation enforced by most web browsers where access tooweb pages must be in hello same domain.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6f8d6-195">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="6f8d6-195">Policy statement</span></span>  
  
```xml  
<jsonp callback-parameter-name="callback function name" />  
```  
  
### <a name="example"></a><span data-ttu-id="6f8d6-196">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6f8d6-196">Example</span></span>  
  
```xml  
<jsonp callback-parameter-name="cb" />  
```  
  
 <span data-ttu-id="6f8d6-197">Se você chamar o método hello sem parâmetro de retorno de chamada Olá? cb = XXX retornará JSON simples (sem um invólucro de chamada de função).</span><span class="sxs-lookup"><span data-stu-id="6f8d6-197">If you call hello method without hello callback parameter ?cb=XXX it will return plain JSON (without a function call wrapper).</span></span>  
  
 <span data-ttu-id="6f8d6-198">Se você adicionar o parâmetro de retorno de chamada hello `?cb=XXX` ele retornará um resultado JSONP, encapsulamento resultados JSON originais de saudação em torno da função de retorno de chamada hello como`XYZ('<json result goes here>');`</span><span class="sxs-lookup"><span data-stu-id="6f8d6-198">If you add hello callback parameter `?cb=XXX` it will return a JSONP result, wrapping hello original JSON results around hello callback function like `XYZ('<json result goes here>');`</span></span>  
  
### <a name="elements"></a><span data-ttu-id="6f8d6-199">Elementos</span><span class="sxs-lookup"><span data-stu-id="6f8d6-199">Elements</span></span>  
  
|<span data-ttu-id="6f8d6-200">Nome</span><span class="sxs-lookup"><span data-stu-id="6f8d6-200">Name</span></span>|<span data-ttu-id="6f8d6-201">Descrição</span><span class="sxs-lookup"><span data-stu-id="6f8d6-201">Description</span></span>|<span data-ttu-id="6f8d6-202">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6f8d6-202">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="6f8d6-203">jsonp</span><span class="sxs-lookup"><span data-stu-id="6f8d6-203">jsonp</span></span>|<span data-ttu-id="6f8d6-204">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-204">Root element.</span></span>|<span data-ttu-id="6f8d6-205">Sim</span><span class="sxs-lookup"><span data-stu-id="6f8d6-205">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="6f8d6-206">Atributos</span><span class="sxs-lookup"><span data-stu-id="6f8d6-206">Attributes</span></span>  
  
|<span data-ttu-id="6f8d6-207">Nome</span><span class="sxs-lookup"><span data-stu-id="6f8d6-207">Name</span></span>|<span data-ttu-id="6f8d6-208">Descrição</span><span class="sxs-lookup"><span data-stu-id="6f8d6-208">Description</span></span>|<span data-ttu-id="6f8d6-209">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6f8d6-209">Required</span></span>|<span data-ttu-id="6f8d6-210">Padrão</span><span class="sxs-lookup"><span data-stu-id="6f8d6-210">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6f8d6-211">callback-parameter-name</span><span class="sxs-lookup"><span data-stu-id="6f8d6-211">callback-parameter-name</span></span>|<span data-ttu-id="6f8d6-212">Olá chamada de função JavaScript entre domínios prefixado com o nome de domínio totalmente qualificado do hello onde hello função reside.</span><span class="sxs-lookup"><span data-stu-id="6f8d6-212">hello cross-domain JavaScript function call prefixed with hello fully qualified domain name where hello function resides.</span></span>|<span data-ttu-id="6f8d6-213">Sim</span><span class="sxs-lookup"><span data-stu-id="6f8d6-213">Yes</span></span>|<span data-ttu-id="6f8d6-214">N/D</span><span class="sxs-lookup"><span data-stu-id="6f8d6-214">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6f8d6-215">Uso</span><span class="sxs-lookup"><span data-stu-id="6f8d6-215">Usage</span></span>  
 <span data-ttu-id="6f8d6-216">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="6f8d6-216">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6f8d6-217">**Seções de política:** saída</span><span class="sxs-lookup"><span data-stu-id="6f8d6-217">**Policy sections:** outbound</span></span>  
  
-   <span data-ttu-id="6f8d6-218">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="6f8d6-218">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="6f8d6-219">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6f8d6-219">Next steps</span></span>
<span data-ttu-id="6f8d6-220">Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="6f8d6-220">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  