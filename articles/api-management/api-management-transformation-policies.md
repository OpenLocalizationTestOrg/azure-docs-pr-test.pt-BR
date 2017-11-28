---
title: "políticas de transformação do gerenciamento de API aaaAzure | Microsoft Docs"
description: "Saiba mais sobre políticas de transformação de saudação disponíveis para uso no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 7406a8ce-5f9c-4fae-9b0f-e574befb2ee9
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 2891cc52d0017b717b3c12a98bc4941b5fd7ea78
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-transformation-policies"></a><span data-ttu-id="fcd71-103">Políticas de transformação de Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="fcd71-103">API Management transformation policies</span></span>
<span data-ttu-id="fcd71-104">Este tópico fornece uma referência para Olá políticas de gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="fcd71-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="fcd71-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="fcd71-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="fcd71-106"><a name="TransformationPolicies"></a> Políticas de transformação</span><span class="sxs-lookup"><span data-stu-id="fcd71-106"><a name="TransformationPolicies"></a> Transformation policies</span></span>  
  
-   <span data-ttu-id="fcd71-107">[Converter JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - converte solicitação ou o corpo da resposta de JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="fcd71-107">[Convert JSON tooXML](api-management-transformation-policies.md#ConvertJSONtoXML) - Converts request or response body from JSON tooXML.</span></span>  
  
-   <span data-ttu-id="fcd71-108">[Converter XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - converte solicitação ou o corpo da resposta de XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="fcd71-108">[Convert XML tooJSON](api-management-transformation-policies.md#ConvertXMLtoJSON) - Converts request or response body from XML tooJSON.</span></span>  
  
-   <span data-ttu-id="fcd71-109">[Localizar e substituir cadeia no corpo](api-management-transformation-policies.md#Findandreplacestringinbody) - Encontra uma subcadeia de uma solicitação ou resposta e a substitui por outra subcadeia.</span><span class="sxs-lookup"><span data-stu-id="fcd71-109">[Find and replace string in body](api-management-transformation-policies.md#Findandreplacestringinbody) - Finds a request or response substring and replaces it with a different substring.</span></span>  
  
-   <span data-ttu-id="fcd71-110">[Mascarar URLs no conteúdo](api-management-transformation-policies.md#MaskURLSContent) -regrava (mascara) links na resposta de saudação do corpo para que eles apontem toohello o link equivalente através do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-110">[Mask URLs in content](api-management-transformation-policies.md#MaskURLSContent) - Re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span>  
  
-   <span data-ttu-id="fcd71-111">[Configurar o serviço de back-end](api-management-transformation-policies.md#SetBackendService) -altera o serviço de back-end Olá para uma solicitação de entrada.</span><span class="sxs-lookup"><span data-stu-id="fcd71-111">[Set backend service](api-management-transformation-policies.md#SetBackendService) - Changes hello backend service for an incoming request.</span></span>  
  
-   <span data-ttu-id="fcd71-112">[Definir corpo](api-management-transformation-policies.md#SetBody) -define o corpo da mensagem de saudação para solicitações de entrada e saídas.</span><span class="sxs-lookup"><span data-stu-id="fcd71-112">[Set body](api-management-transformation-policies.md#SetBody) - Sets hello message body for incoming and outgoing requests.</span></span>  
  
-   <span data-ttu-id="fcd71-113">[Definir cabeçalho HTTP](api-management-transformation-policies.md#SetHTTPheader) - atribui um cabeçalho de solicitação e/ou resposta do valor tooan existente ou adiciona um novo cabeçalho de solicitação de e/ou resposta.</span><span class="sxs-lookup"><span data-stu-id="fcd71-113">[Set HTTP header](api-management-transformation-policies.md#SetHTTPheader) - Assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
-   <span data-ttu-id="fcd71-114">[Definir parâmetro de cadeia de consulta](api-management-transformation-policies.md#SetQueryStringParameter) - Adiciona, substitui o valor ou exclui parâmetros de cadeias de consulta de solicitação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-114">[Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) - Adds, replaces value of, or deletes request query string parameter.</span></span>  
  
-   <span data-ttu-id="fcd71-115">[Regravar URL](api-management-transformation-policies.md#RewriteURL) -converte uma URL de solicitação de forma pública formulário toohello esperada pelo serviço da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-115">[Rewrite URL](api-management-transformation-policies.md#RewriteURL) - Converts a request URL from its public form toohello form expected by hello web service.</span></span>  
  
-   <span data-ttu-id="fcd71-116">[Transformar XML usando um XSLT](api-management-transformation-policies.md#XSLTransform) -aplica-se um tooXML de transformação XSL no corpo de solicitação ou resposta hello.</span><span class="sxs-lookup"><span data-stu-id="fcd71-116">[Transform XML using an XSLT](api-management-transformation-policies.md#XSLTransform) - Applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
##  <span data-ttu-id="fcd71-117"><a name="ConvertJSONtoXML"></a>Converter JSON tooXML</span><span class="sxs-lookup"><span data-stu-id="fcd71-117"><a name="ConvertJSONtoXML"></a> Convert JSON tooXML</span></span>  
 <span data-ttu-id="fcd71-118">Olá `json-to-xml` política converte um corpo de resposta ou solicitação de JSON tooXML.</span><span class="sxs-lookup"><span data-stu-id="fcd71-118">hello `json-to-xml` policy converts a request or response body from JSON tooXML.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="fcd71-119">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="fcd71-119">Policy statement</span></span>  
  
```xml  
<json-to-xml apply="always | content-type-json" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="fcd71-120">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fcd71-120">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <json-to-xml apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="fcd71-121">Elementos</span><span class="sxs-lookup"><span data-stu-id="fcd71-121">Elements</span></span>  
  
|<span data-ttu-id="fcd71-122">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-122">Name</span></span>|<span data-ttu-id="fcd71-123">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-123">Description</span></span>|<span data-ttu-id="fcd71-124">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-124">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fcd71-125">json-to-xml</span><span class="sxs-lookup"><span data-stu-id="fcd71-125">json-to-xml</span></span>|<span data-ttu-id="fcd71-126">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="fcd71-126">Root element.</span></span>|<span data-ttu-id="fcd71-127">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-127">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="fcd71-128">Atributos</span><span class="sxs-lookup"><span data-stu-id="fcd71-128">Attributes</span></span>  
  
|<span data-ttu-id="fcd71-129">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-129">Name</span></span>|<span data-ttu-id="fcd71-130">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-130">Description</span></span>|<span data-ttu-id="fcd71-131">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-131">Required</span></span>|<span data-ttu-id="fcd71-132">Padrão</span><span class="sxs-lookup"><span data-stu-id="fcd71-132">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="fcd71-133">aplicar</span><span class="sxs-lookup"><span data-stu-id="fcd71-133">apply</span></span>|<span data-ttu-id="fcd71-134">atributo Olá deve ser definido como tooone de saudação valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="fcd71-134">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="fcd71-135">–  always – sempre aplicar conversão.</span><span class="sxs-lookup"><span data-stu-id="fcd71-135">-   always - always apply conversion.</span></span><br /><span data-ttu-id="fcd71-136">–  content-type-json – converter somente se o cabeçalho Content-Type da resposta indica a presença de JSON.</span><span class="sxs-lookup"><span data-stu-id="fcd71-136">-   content-type-json - convert only if response Content-Type header indicates presence of JSON.</span></span>|<span data-ttu-id="fcd71-137">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-137">Yes</span></span>|<span data-ttu-id="fcd71-138">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-138">N/A</span></span>|  
|<span data-ttu-id="fcd71-139">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="fcd71-139">consider-accept-header</span></span>|<span data-ttu-id="fcd71-140">atributo Olá deve ser definido como tooone de saudação valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="fcd71-140">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="fcd71-141">–  true – aplica conversão se JSON é solicitado no cabeçalho Accept da solicitação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-141">-   true - apply conversion if JSON is requested in request Accept header.</span></span><br /><span data-ttu-id="fcd71-142">–  false – sempre aplicar conversão.</span><span class="sxs-lookup"><span data-stu-id="fcd71-142">-   false -always apply conversion.</span></span>|<span data-ttu-id="fcd71-143">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-143">No</span></span>|<span data-ttu-id="fcd71-144">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="fcd71-144">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="fcd71-145">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd71-145">Usage</span></span>  
 <span data-ttu-id="fcd71-146">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fcd71-146">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fcd71-147">**Seções de política:** de entrada, de saída, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="fcd71-147">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="fcd71-148">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="fcd71-148">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="fcd71-149"><a name="ConvertXMLtoJSON"></a>Converter XML tooJSON</span><span class="sxs-lookup"><span data-stu-id="fcd71-149"><a name="ConvertXMLtoJSON"></a> Convert XML tooJSON</span></span>  
 <span data-ttu-id="fcd71-150">Olá `xml-to-json` política converte um corpo de resposta ou solicitação de XML tooJSON.</span><span class="sxs-lookup"><span data-stu-id="fcd71-150">hello `xml-to-json` policy converts a request or response body from XML tooJSON.</span></span> <span data-ttu-id="fcd71-151">Esta política pode ser usado toomodernize APIs com base em serviços da web de back-end XML apenas.</span><span class="sxs-lookup"><span data-stu-id="fcd71-151">This policy can be used toomodernize APIs based on XML-only backend web services.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="fcd71-152">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="fcd71-152">Policy statement</span></span>  
  
```xml  
<xml-to-json kind="javascript-friendly | direct" apply="always | content-type-xml" consider-accept-header="true | false"/>  
```  
  
### <a name="example"></a><span data-ttu-id="fcd71-153">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fcd71-153">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
        <xml-to-json kind="direct" apply="always" consider-accept-header="false" />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="fcd71-154">Elementos</span><span class="sxs-lookup"><span data-stu-id="fcd71-154">Elements</span></span>  
  
|<span data-ttu-id="fcd71-155">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-155">Name</span></span>|<span data-ttu-id="fcd71-156">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-156">Description</span></span>|<span data-ttu-id="fcd71-157">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-157">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fcd71-158">xml-to-json</span><span class="sxs-lookup"><span data-stu-id="fcd71-158">xml-to-json</span></span>|<span data-ttu-id="fcd71-159">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="fcd71-159">Root element.</span></span>|<span data-ttu-id="fcd71-160">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-160">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="fcd71-161">Atributos</span><span class="sxs-lookup"><span data-stu-id="fcd71-161">Attributes</span></span>  
  
|<span data-ttu-id="fcd71-162">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-162">Name</span></span>|<span data-ttu-id="fcd71-163">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-163">Description</span></span>|<span data-ttu-id="fcd71-164">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-164">Required</span></span>|<span data-ttu-id="fcd71-165">Padrão</span><span class="sxs-lookup"><span data-stu-id="fcd71-165">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="fcd71-166">kind</span><span class="sxs-lookup"><span data-stu-id="fcd71-166">kind</span></span>|<span data-ttu-id="fcd71-167">atributo Olá deve ser definido como tooone de saudação valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="fcd71-167">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="fcd71-168">Olá-javascript friendly – converter JSON tem um desenvolvedores tooJavaScript amigável do formulário.</span><span class="sxs-lookup"><span data-stu-id="fcd71-168">-   javascript-friendly - hello converted JSON has a form friendly tooJavaScript developers.</span></span><br /><span data-ttu-id="fcd71-169">-direta - Olá JSON convertido reflete a estrutura do documento do XML de original hello.</span><span class="sxs-lookup"><span data-stu-id="fcd71-169">-   direct - hello converted JSON reflects hello original XML document's structure.</span></span>|<span data-ttu-id="fcd71-170">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-170">Yes</span></span>|<span data-ttu-id="fcd71-171">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-171">N/A</span></span>|  
|<span data-ttu-id="fcd71-172">aplicar</span><span class="sxs-lookup"><span data-stu-id="fcd71-172">apply</span></span>|<span data-ttu-id="fcd71-173">atributo Olá deve ser definido como tooone de saudação valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="fcd71-173">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="fcd71-174">– always – converter sempre.</span><span class="sxs-lookup"><span data-stu-id="fcd71-174">-   always - convert always.</span></span><br /><span data-ttu-id="fcd71-175">–  content-type-xml – converter somente se o cabeçalho Content-Type da resposta indica a presença de XML.</span><span class="sxs-lookup"><span data-stu-id="fcd71-175">-   content-type-xml - convert only if response Content-Type header indicates presence of XML.</span></span>|<span data-ttu-id="fcd71-176">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-176">Yes</span></span>|<span data-ttu-id="fcd71-177">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-177">N/A</span></span>|  
|<span data-ttu-id="fcd71-178">consider-accept-header</span><span class="sxs-lookup"><span data-stu-id="fcd71-178">consider-accept-header</span></span>|<span data-ttu-id="fcd71-179">atributo Olá deve ser definido como tooone de saudação valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="fcd71-179">hello attribute must be set tooone of hello following values.</span></span><br /><br /> <span data-ttu-id="fcd71-180">–  true – aplica conversão se XML é solicitado no cabeçalho Accept da solicitação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-180">-   true - apply conversion if XML is requested in request Accept header.</span></span><br /><span data-ttu-id="fcd71-181">–  false – sempre aplicar conversão.</span><span class="sxs-lookup"><span data-stu-id="fcd71-181">-   false -always apply conversion.</span></span>|<span data-ttu-id="fcd71-182">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-182">No</span></span>|<span data-ttu-id="fcd71-183">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="fcd71-183">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="fcd71-184">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd71-184">Usage</span></span>  
 <span data-ttu-id="fcd71-185">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fcd71-185">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fcd71-186">**Seções de política:** de entrada, de saída, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="fcd71-186">**Policy sections:** inbound, outbound, on-error</span></span>  
  
-   <span data-ttu-id="fcd71-187">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="fcd71-187">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="fcd71-188"><a name="Findandreplacestringinbody"></a> Localizar e substituir cadeia de caracteres no corpo</span><span class="sxs-lookup"><span data-stu-id="fcd71-188"><a name="Findandreplacestringinbody"></a> Find and replace string in body</span></span>  
 <span data-ttu-id="fcd71-189">Olá `find-and-replace` política localiza uma subcadeia de caracteres de solicitação ou resposta e a substitui por uma subcadeia de caracteres diferente.</span><span class="sxs-lookup"><span data-stu-id="fcd71-189">hello `find-and-replace` policy finds a request or response substring and replaces it with a different substring.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="fcd71-190">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="fcd71-190">Policy statement</span></span>  
  
```xml  
<find-and-replace from="what tooreplace" to="replacement" />  
```  
  
### <a name="example"></a><span data-ttu-id="fcd71-191">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fcd71-191">Example</span></span>  
  
```xml  
<find-and-replace from="notebook" to="laptop" />  
```  
  
### <a name="elements"></a><span data-ttu-id="fcd71-192">Elementos</span><span class="sxs-lookup"><span data-stu-id="fcd71-192">Elements</span></span>  
  
|<span data-ttu-id="fcd71-193">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-193">Name</span></span>|<span data-ttu-id="fcd71-194">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-194">Description</span></span>|<span data-ttu-id="fcd71-195">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-195">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fcd71-196">find-and-replace</span><span class="sxs-lookup"><span data-stu-id="fcd71-196">find-and-replace</span></span>|<span data-ttu-id="fcd71-197">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="fcd71-197">Root element.</span></span>|<span data-ttu-id="fcd71-198">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-198">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="fcd71-199">Atributos</span><span class="sxs-lookup"><span data-stu-id="fcd71-199">Attributes</span></span>  
  
|<span data-ttu-id="fcd71-200">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-200">Name</span></span>|<span data-ttu-id="fcd71-201">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-201">Description</span></span>|<span data-ttu-id="fcd71-202">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-202">Required</span></span>|<span data-ttu-id="fcd71-203">Padrão</span><span class="sxs-lookup"><span data-stu-id="fcd71-203">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="fcd71-204">Da</span><span class="sxs-lookup"><span data-stu-id="fcd71-204">from</span></span>|<span data-ttu-id="fcd71-205">Olá toosearch de cadeia de caracteres para.</span><span class="sxs-lookup"><span data-stu-id="fcd71-205">hello string toosearch for.</span></span>|<span data-ttu-id="fcd71-206">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-206">Yes</span></span>|<span data-ttu-id="fcd71-207">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-207">N/A</span></span>|  
|<span data-ttu-id="fcd71-208">para</span><span class="sxs-lookup"><span data-stu-id="fcd71-208">to</span></span>|<span data-ttu-id="fcd71-209">cadeia de caracteres de substituição de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-209">hello replacement string.</span></span> <span data-ttu-id="fcd71-210">Especifique uma substituição cadeia de caracteres tooremove Olá pesquisa sequência de tamanho zero.</span><span class="sxs-lookup"><span data-stu-id="fcd71-210">Specify a zero length replacement string tooremove hello search string.</span></span>|<span data-ttu-id="fcd71-211">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-211">Yes</span></span>|<span data-ttu-id="fcd71-212">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-212">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="fcd71-213">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd71-213">Usage</span></span>  
 <span data-ttu-id="fcd71-214">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fcd71-214">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fcd71-215">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="fcd71-215">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="fcd71-216">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="fcd71-216">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="fcd71-217"><a name="MaskURLSContent"></a> Mascarar URLs no conteúdo</span><span class="sxs-lookup"><span data-stu-id="fcd71-217"><a name="MaskURLSContent"></a> Mask URLs in content</span></span>  
 <span data-ttu-id="fcd71-218">Olá `redirect-content-urls` política regrava (mascara) links no corpo de resposta Olá para que eles apontem toohello o link equivalente através do gateway de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-218">hello `redirect-content-urls` policy re-writes (masks) links in hello response body so that they point toohello equivalent link via hello gateway.</span></span> <span data-ttu-id="fcd71-219">Use em toomake links corpo de resposta do hello seção saída toore gravação-los toohello de ponto de gateway.</span><span class="sxs-lookup"><span data-stu-id="fcd71-219">Use in hello outbound section toore-write response body links toomake them point toohello gateway.</span></span> <span data-ttu-id="fcd71-220">Uso em Olá seção para um efeito oposto de entrada.</span><span class="sxs-lookup"><span data-stu-id="fcd71-220">Use in hello inbound section for an opposite effect.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="fcd71-221">Essa política não altera nenhum valor de cabeçalho como cabeçalhos `Location`.</span><span class="sxs-lookup"><span data-stu-id="fcd71-221">This policy does not change any header values such as `Location` headers.</span></span> <span data-ttu-id="fcd71-222">valores de cabeçalho toochange, use Olá [cabeçalho do conjunto](api-management-transformation-policies.md#SetHTTPheader) política.</span><span class="sxs-lookup"><span data-stu-id="fcd71-222">toochange header values, use hello [set-header](api-management-transformation-policies.md#SetHTTPheader) policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="fcd71-223">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="fcd71-223">Policy statement</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="example"></a><span data-ttu-id="fcd71-224">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fcd71-224">Example</span></span>  
  
```xml  
<redirect-content-urls />  
```  
  
### <a name="elements"></a><span data-ttu-id="fcd71-225">Elementos</span><span class="sxs-lookup"><span data-stu-id="fcd71-225">Elements</span></span>  
  
|<span data-ttu-id="fcd71-226">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-226">Name</span></span>|<span data-ttu-id="fcd71-227">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-227">Description</span></span>|<span data-ttu-id="fcd71-228">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-228">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fcd71-229">redirect-content-urls</span><span class="sxs-lookup"><span data-stu-id="fcd71-229">redirect-content-urls</span></span>|<span data-ttu-id="fcd71-230">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="fcd71-230">Root element.</span></span>|<span data-ttu-id="fcd71-231">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-231">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="fcd71-232">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd71-232">Usage</span></span>  
 <span data-ttu-id="fcd71-233">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fcd71-233">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fcd71-234">**Seções de política:** de entrada, de saída</span><span class="sxs-lookup"><span data-stu-id="fcd71-234">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="fcd71-235">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="fcd71-235">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="fcd71-236"><a name="SetBackendService"></a> Definir o serviço de back-end</span><span class="sxs-lookup"><span data-stu-id="fcd71-236"><a name="SetBackendService"></a> Set backend service</span></span>  
 <span data-ttu-id="fcd71-237">Saudação de uso `set-backend-service` política tooredirect uma entrada de solicitação back-end diferente de tooa de Olá especificado nas configurações de saudação API para essa operação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-237">Use hello `set-backend-service` policy tooredirect an incoming request tooa different backend than hello one specified in hello API settings for that operation.</span></span> <span data-ttu-id="fcd71-238">Essa política altera back-end Olá URL base do serviço de toohello solicitação de entrada hello especificada na política de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-238">This policy changes hello backend service base URL of hello incoming request toohello one specified in hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="fcd71-239">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="fcd71-239">Policy statement</span></span>  
  
```xml  
<set-backend-service base-url="base URL of hello backend service" />  
```  
  
### <a name="example"></a><span data-ttu-id="fcd71-240">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fcd71-240">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <choose>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2013-05")">  
                <set-backend-service base-url="http://contoso.com/api/8.2/" />  
            </when>  
            <when condition="@(context.Request.Url.Query.GetValueOrDefault("version") == "2014-03")">  
                <set-backend-service base-url="http://contoso.com/api/9.1/" />  
            </when>  
        </choose>  
        <base />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="fcd71-241">Em Olá Este exemplo Definir política de serviço de back-end roteia solicitações com base no valor de versão Olá passado no serviço de back-end diferente de tooa Olá consulta cadeia de caracteres que Olá Olá especificado em uma API.</span><span class="sxs-lookup"><span data-stu-id="fcd71-241">In this example hello set backend service policy routes requests based on hello version value passed in hello query string tooa different backend service than hello one specified in hello API.</span></span>
  
<span data-ttu-id="fcd71-242">Inicialmente hello URL base do serviço de back-end é derivada de configurações de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-242">Initially hello backend service base URL is derived from hello API settings.</span></span> <span data-ttu-id="fcd71-243">Olá para a URL de solicitação `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` se torna `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` onde `http://contoso.com/api/10.4/` é a URL do serviço de back-end de saudação especificado nas configurações de API de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-243">So hello request URL `https://contoso.azure-api.net/api/partners/15?version=2013-05&subscription-key=abcdef` becomes `http://contoso.com/api/10.4/partners/15?version=2013-05&subscription-key=abcdef` where `http://contoso.com/api/10.4/` is hello backend service URL specified in hello API settings.</span></span>  
  
<span data-ttu-id="fcd71-244">Olá quando [< escolha\> ](api-management-advanced-policies.md#choose) declaração da política é aplicada Olá URL de base do serviço de back-end pode alterar novamente muito`http://contoso.com/api/8.2` ou `http://contoso.com/api/9.1`, dependendo do valor de saudação do parâmetro de consulta de solicitação de versão de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-244">When hello [<choose\>](api-management-advanced-policies.md#choose) policy statement is applied hello backend service base URL may change again either too`http://contoso.com/api/8.2` or `http://contoso.com/api/9.1`, depending on hello value of hello version request query parameter.</span></span> <span data-ttu-id="fcd71-245">Por exemplo, se hello valor é `"2013-15"` solicitação final de saudação URL será `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span><span class="sxs-lookup"><span data-stu-id="fcd71-245">For example, if hello value is `"2013-15"` hello final request URL becomes `http://contoso.com/api/8.2/partners/15?version=2013-05&subscription-key=abcdef`.</span></span>  
  
<span data-ttu-id="fcd71-246">Se outra transformação de solicitação de saudação será desejado, [políticas de transformação](api-management-transformation-policies.md#TransformationPolicies) pode ser usado.</span><span class="sxs-lookup"><span data-stu-id="fcd71-246">If further transformation of hello request is desired, other [Transformation policies](api-management-transformation-policies.md#TransformationPolicies) can be used.</span></span> <span data-ttu-id="fcd71-247">Por exemplo, tooremove Olá versão consulta parâmetro agora que hello solicitação está sendo roteada back-end específico de versão de tooa, hello [definir parâmetro de cadeia de caracteres de consulta](api-management-transformation-policies.md#SetQueryStringParameter) política pode ser o atributo de versão agora redundante Olá tooremove usado.</span><span class="sxs-lookup"><span data-stu-id="fcd71-247">For example, tooremove hello version query parameter now that hello request is being routed tooa version specific backend, hello  [Set query string parameter](api-management-transformation-policies.md#SetQueryStringParameter) policy can be used tooremove hello now redundant version attribute.</span></span>  
  
### <a name="example"></a><span data-ttu-id="fcd71-248">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fcd71-248">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <set-backend-service backend-id="my-sf-service" sf-partition-key="@(context.Request.Url.Query.GetValueOrDefault("userId","")" sf-replica-type="primary" /> 
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
<span data-ttu-id="fcd71-249">Neste exemplo hello política rotas Olá solicitação tooa serviço malha back-end, usando a cadeia de caracteres de consulta de userId hello como chave de partição hello e usando Olá réplica primária de partição hello.</span><span class="sxs-lookup"><span data-stu-id="fcd71-249">In this example hello policy routes hello request tooa service fabric backend, using hello userId query string as hello partition key and using hello primary replica of hello partition.</span></span>  

### <a name="elements"></a><span data-ttu-id="fcd71-250">Elementos</span><span class="sxs-lookup"><span data-stu-id="fcd71-250">Elements</span></span>  
  
|<span data-ttu-id="fcd71-251">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-251">Name</span></span>|<span data-ttu-id="fcd71-252">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-252">Description</span></span>|<span data-ttu-id="fcd71-253">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-253">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fcd71-254">set-backend-service</span><span class="sxs-lookup"><span data-stu-id="fcd71-254">set-backend-service</span></span>|<span data-ttu-id="fcd71-255">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="fcd71-255">Root element.</span></span>|<span data-ttu-id="fcd71-256">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-256">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="fcd71-257">Atributos</span><span class="sxs-lookup"><span data-stu-id="fcd71-257">Attributes</span></span>  
  
|<span data-ttu-id="fcd71-258">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-258">Name</span></span>|<span data-ttu-id="fcd71-259">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-259">Description</span></span>|<span data-ttu-id="fcd71-260">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-260">Required</span></span>|<span data-ttu-id="fcd71-261">Padrão</span><span class="sxs-lookup"><span data-stu-id="fcd71-261">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="fcd71-262">base-url</span><span class="sxs-lookup"><span data-stu-id="fcd71-262">base-url</span></span>|<span data-ttu-id="fcd71-263">Nova URL base do serviço de back-end.</span><span class="sxs-lookup"><span data-stu-id="fcd71-263">New backend service base URL.</span></span>|<span data-ttu-id="fcd71-264">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-264">No</span></span>|<span data-ttu-id="fcd71-265">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-265">N/A</span></span>|  
|<span data-ttu-id="fcd71-266">backend-id</span><span class="sxs-lookup"><span data-stu-id="fcd71-266">backend-id</span></span>|<span data-ttu-id="fcd71-267">Identificador da saudação tooroute de back-end para.</span><span class="sxs-lookup"><span data-stu-id="fcd71-267">Identifier of hello backend tooroute to.</span></span>|<span data-ttu-id="fcd71-268">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-268">No</span></span>|<span data-ttu-id="fcd71-269">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-269">N/A</span></span>|  
|<span data-ttu-id="fcd71-270">sf-partition-key</span><span class="sxs-lookup"><span data-stu-id="fcd71-270">sf-partition-key</span></span>|<span data-ttu-id="fcd71-271">Só aplicável quando o hello back-end é um serviço de malha do serviço e é especificado usando 'id de back-end'.</span><span class="sxs-lookup"><span data-stu-id="fcd71-271">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="fcd71-272">Usado tooresolve uma partição específica do serviço de resolução de nome de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-272">Used tooresolve a specific partition from hello name resolution service.</span></span>|<span data-ttu-id="fcd71-273">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-273">No</span></span>|<span data-ttu-id="fcd71-274">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-274">N/A</span></span>|  
|<span data-ttu-id="fcd71-275">sf-replica-type</span><span class="sxs-lookup"><span data-stu-id="fcd71-275">sf-replica-type</span></span>|<span data-ttu-id="fcd71-276">Só aplicável quando o hello back-end é um serviço de malha do serviço e é especificado usando 'id de back-end'.</span><span class="sxs-lookup"><span data-stu-id="fcd71-276">Only applicable when hello backend is a Service Fabric service and is specified using 'backend-id'.</span></span> <span data-ttu-id="fcd71-277">Controla se a solicitação de saudação deve ir toohello a réplica primária ou secundária de uma partição.</span><span class="sxs-lookup"><span data-stu-id="fcd71-277">Controls if hello request should go toohello primary or secondary replica of a partition.</span></span> |<span data-ttu-id="fcd71-278">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-278">No</span></span>|<span data-ttu-id="fcd71-279">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-279">N/A</span></span>|    
|<span data-ttu-id="fcd71-280">sf-resolve-condition</span><span class="sxs-lookup"><span data-stu-id="fcd71-280">sf-resolve-condition</span></span>|<span data-ttu-id="fcd71-281">Só é aplicável quando Olá back-end é um serviço de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="fcd71-281">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="fcd71-282">Identificação de condição se Olá chamar back-end de malha tooService tem toobe repetida com nova resolução.</span><span class="sxs-lookup"><span data-stu-id="fcd71-282">Condition identifying if hello call tooService Fabric backend has toobe repeated with new resolution.</span></span>|<span data-ttu-id="fcd71-283">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-283">No</span></span>|<span data-ttu-id="fcd71-284">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-284">N/A</span></span>|    
|<span data-ttu-id="fcd71-285">sf-service-instance-name</span><span class="sxs-lookup"><span data-stu-id="fcd71-285">sf-service-instance-name</span></span>|<span data-ttu-id="fcd71-286">Só é aplicável quando Olá back-end é um serviço de malha do serviço.</span><span class="sxs-lookup"><span data-stu-id="fcd71-286">Only applicable when hello backend is a Service Fabric service.</span></span> <span data-ttu-id="fcd71-287">Permite que toochange instâncias de serviço em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="fcd71-287">Allows toochange service instances at runtime.</span></span> |<span data-ttu-id="fcd71-288">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-288">No</span></span>|<span data-ttu-id="fcd71-289">N/D </span><span class="sxs-lookup"><span data-stu-id="fcd71-289">N/A</span></span>|    

### <a name="usage"></a><span data-ttu-id="fcd71-290">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd71-290">Usage</span></span>  
 <span data-ttu-id="fcd71-291">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fcd71-291">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fcd71-292">**Seções de política:** de entrada, back-end</span><span class="sxs-lookup"><span data-stu-id="fcd71-292">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="fcd71-293">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="fcd71-293">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="fcd71-294"><a name="SetBody"></a> Definir corpo</span><span class="sxs-lookup"><span data-stu-id="fcd71-294"><a name="SetBody"></a> Set body</span></span>  
 <span data-ttu-id="fcd71-295">Saudação de uso `set-body` corpo da mensagem de saudação política tooset para solicitações de entrada e saídas.</span><span class="sxs-lookup"><span data-stu-id="fcd71-295">Use hello `set-body` policy tooset hello message body for incoming and outgoing requests.</span></span> <span data-ttu-id="fcd71-296">tooaccess Olá corpo de mensagem, você pode usar o hello `context.Request.Body` propriedade ou hello `context.Response.Body`, dependendo se a política de saudação está em Olá seção de entrada ou saída.</span><span class="sxs-lookup"><span data-stu-id="fcd71-296">tooaccess hello message body you can use hello `context.Request.Body` property or hello `context.Response.Body`, depending on whether hello policy is in hello inbound or outbound section.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="fcd71-297">Observe que, por padrão, quando você acessar Olá corpo de mensagem usando `context.Request.Body` ou `context.Response.Body`, mensagem original de saudação do corpo é perdido e deve ser definido, retornando o corpo de saudação volta na expressão de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-297">Note that by default when you access hello message body using `context.Request.Body` or `context.Response.Body`, hello original message body is lost and must be set by returning hello body back in hello expression.</span></span> <span data-ttu-id="fcd71-298">corpo da saudação toopreserve conteúdo, defina Olá `preserveContent` parâmetro muito`true` ao acessar a mensagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-298">toopreserve hello body content, set hello `preserveContent` parameter too`true` when accessing hello message.</span></span> <span data-ttu-id="fcd71-299">Se `preserveContent` está definido muito`true` e um corpo diferente é retornado pela expressão hello, Olá retornado corpo é usado.</span><span class="sxs-lookup"><span data-stu-id="fcd71-299">If `preserveContent` is set too`true` and a different body is returned by hello expression, hello returned body is used.</span></span>  
>   
>  <span data-ttu-id="fcd71-300">Observação Olá considerações a seguir ao usar o hello `set-body` política.</span><span class="sxs-lookup"><span data-stu-id="fcd71-300">Please note hello following considerations when using hello `set-body` policy.</span></span>  
>   
>  -   <span data-ttu-id="fcd71-301">Se você estiver usando Olá `set-body` tooreturn política um corpo de novo ou atualizado não é necessário tooset `preserveContent` muito`true` porque você está fornecendo um novo conteúdo de corpo Olá explicitamente.</span><span class="sxs-lookup"><span data-stu-id="fcd71-301">If you are using hello `set-body` policy tooreturn a new or updated body you don't need tooset `preserveContent` too`true` because you are explicitly supplying hello new body contents.</span></span>  
> -   <span data-ttu-id="fcd71-302">Preservar o conteúdo de saudação de uma resposta no pipeline de entrada hello não faz sentido, porque não há nenhuma resposta ainda.</span><span class="sxs-lookup"><span data-stu-id="fcd71-302">Preserving hello content of a response in hello inbound pipeline doesn't make sense because there is no response yet.</span></span>  
> -   <span data-ttu-id="fcd71-303">Preservar o conteúdo de saudação de uma solicitação no pipeline de saída Olá não faz sentido porque Olá solicitação já foi enviada toohello back-end neste momento.</span><span class="sxs-lookup"><span data-stu-id="fcd71-303">Preserving hello content of a request in hello outbound pipeline doesn't make sense because hello request has already been sent toohello backend at this point.</span></span>  
> -   <span data-ttu-id="fcd71-304">Se essa política é usada quando não há nenhum corpo da mensagem, por exemplo em um GET de entrada, uma exceção é lançada.</span><span class="sxs-lookup"><span data-stu-id="fcd71-304">If this policy is used when there is no message body, for example in an inbound GET, an exception is thrown.</span></span>  
  
 <span data-ttu-id="fcd71-305">Para obter mais informações, consulte Olá `context.Request.Body`, `context.Response.Body`e hello `IMessage` seções Olá [variável de contexto](api-management-policy-expressions.md#ContextVariables) tabela.</span><span class="sxs-lookup"><span data-stu-id="fcd71-305">For more information, see hello `context.Request.Body`, `context.Response.Body`, and hello `IMessage` sections in hello [Context variable](api-management-policy-expressions.md#ContextVariables) table.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="fcd71-306">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="fcd71-306">Policy statement</span></span>  
  
```xml  
<set-body>new body value as text</set-body>  
```  
  
### <a name="examples"></a><span data-ttu-id="fcd71-307">Exemplos</span><span class="sxs-lookup"><span data-stu-id="fcd71-307">Examples</span></span>  
  
#### <a name="literal-text-example"></a><span data-ttu-id="fcd71-308">Exemplo de texto literal</span><span class="sxs-lookup"><span data-stu-id="fcd71-308">Literal text example</span></span>  
  
```xml  
<set-body>Hello world!</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-string-note-that-we-are-preserving-hello-original-request-body-so-that-we-can-access-it-later-in-hello-pipeline"></a><span data-ttu-id="fcd71-309">Por exemplo, acessando o corpo de saudação como uma cadeia de caracteres.</span><span class="sxs-lookup"><span data-stu-id="fcd71-309">Example accessing hello body as a string.</span></span> <span data-ttu-id="fcd71-310">Observe que estamos são preservando corpo da solicitação original Olá para que podemos pode acessá-lo mais tarde no pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-310">Note that we are preserving hello original request body so that we can access it later in hello pipeline.</span></span>
  
```xml  
<set-body>  
@{   
    string inBody = context.Request.Body.As<string>(preserveContent: true);   
    if (inBody[0] =='c') {   
        inBody[0] = 'm';   
    }   
    return inBody;   
}  
</set-body>  
```  
  
#### <a name="example-accessing-hello-body-as-a-jobject-note-that-since-we-are-not-reserving-hello-original-request-body-accesing-it-later-in-hello-pipeline-will-result-in-an-exception"></a><span data-ttu-id="fcd71-311">Por exemplo, acessando o corpo da saudação como um JObject.</span><span class="sxs-lookup"><span data-stu-id="fcd71-311">Example accessing hello body as a JObject.</span></span> <span data-ttu-id="fcd71-312">Observe que, desde que não são reservar o corpo da solicitação original hello, acessar posteriormente no pipeline de saudação resultará em uma exceção.</span><span class="sxs-lookup"><span data-stu-id="fcd71-312">Note that since we are not reserving hello original request body, accesing it later in hello pipeline will result in an exception.</span></span>  
  
```xml  
<set-body>   
@{   
    JObject inBody = context.Request.Body.As<JObject>();   
    if (inBody.attribute == <tag>) {   
        inBody[0] = 'm';   
    }   
    return inBody.ToString();   
}   
</set-body>  
  
```  
  
#### <a name="filter-response-based-on-product"></a><span data-ttu-id="fcd71-313">Resposta de filtro com base no produto</span><span class="sxs-lookup"><span data-stu-id="fcd71-313">Filter response based on product</span></span>  
 <span data-ttu-id="fcd71-314">Este exemplo mostra como tooperform a filtragem de conteúdo removendo elementos de dados de resposta de saudação foi recebida do serviço de back-end Olá Olá `Starter` produto.</span><span class="sxs-lookup"><span data-stu-id="fcd71-314">This example shows how tooperform content filtering by removing data elements from hello response received from hello backend service when using hello `Starter` product.</span></span> <span data-ttu-id="fcd71-315">Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too34:30.</span><span class="sxs-lookup"><span data-stu-id="fcd71-315">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too34:30.</span></span> <span data-ttu-id="fcd71-316">Iniciar em 31:50 toosee uma visão geral de [Olá escuro API de previsão Sky](https://developer.forecast.io/) usado para esta demonstração.</span><span class="sxs-lookup"><span data-stu-id="fcd71-316">Start  at 31:50 toosee an overview of [hello Dark Sky Forecast API](https://developer.forecast.io/) used for this demo.</span></span>  
  
```xml  
<!-- Copy this snippet into hello outbound section tooremove a number of data elements from hello response received from hello backend service based on hello name of hello api product -->  
<choose>  
  <when condition="@(context.Response.StatusCode == 200 && context.Product.Name.Equals("Starter"))">  
    <set-body>@{  
        var response = context.Response.Body.As<JObject>();  
        foreach (var key in new [] {"minutely", "hourly", "daily", "flags"}) {  
          response.Property (key).Remove ();  
        }  
        return response.ToString();  
      }  
    </set-body>  
  </when>  
</choose>  
```  

### <a name="using-liquid-templates-with-set-body"></a><span data-ttu-id="fcd71-317">Usando modelos Líquidos com o corpo definido</span><span class="sxs-lookup"><span data-stu-id="fcd71-317">Using Liquid templates with set body</span></span> 
<span data-ttu-id="fcd71-318">Olá `set-body` política pode ser configurado toouse Olá [líquido](https://shopify.github.io/liquid/basics/introduction/) corpo da saudação tootransfom modelagem idioma de uma solicitação ou resposta.</span><span class="sxs-lookup"><span data-stu-id="fcd71-318">hello `set-body` policy can be configured toouse hello [Liquid](https://shopify.github.io/liquid/basics/introduction/) templating language tootransfom hello body of a request or response.</span></span> <span data-ttu-id="fcd71-319">Isso pode ser muito eficaz se você precisar de formato de saudação de reformatação toocompletely da mensagem.</span><span class="sxs-lookup"><span data-stu-id="fcd71-319">This can be very effective if you need toocompletely reshape hello format of your message.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcd71-320">Olá implementação de líquido usado em Olá `set-body` a política é configurada no 'modo de C# '.</span><span class="sxs-lookup"><span data-stu-id="fcd71-320">hello implementation of Liquid used in hello `set-body` policy is configured in 'C# mode'.</span></span> <span data-ttu-id="fcd71-321">Isso é particularmente importante ao executar ações como filtragem.</span><span class="sxs-lookup"><span data-stu-id="fcd71-321">This is particularly important when doing things such as filtering.</span></span> <span data-ttu-id="fcd71-322">Por exemplo, usando um filtro de data requer o uso de saudação do Pascal maiusculas e minúsculas e c#, por exemplo, formatação de data:</span><span class="sxs-lookup"><span data-stu-id="fcd71-322">As an example, using a date filter requires hello use of Pascal casing and C# date formatting e.g.:</span></span>
>
> <span data-ttu-id="fcd71-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span><span class="sxs-lookup"><span data-stu-id="fcd71-323">{{body.foo.startDateTime| Date:"yyyyMMddTHH:mm:ddZ"}}</span></span>

> [!IMPORTANT]
> <span data-ttu-id="fcd71-324">Em ordem toocorrectly bind tooan corpo XML usando o modelo líquidos hello, use um `set-header` política tooset Content-Type tooeither aplicativo/xml, texto/xml (ou qualquer tipo que terminam com + xml); para um corpo JSON, ele deve ser aplicativo/json, texto/json (ou final de qualquer tipo com + json).</span><span class="sxs-lookup"><span data-stu-id="fcd71-324">In order toocorrectly bind tooan XML body using hello Liquid template, use a `set-header` policy tooset Content-Type tooeither application/xml, text/xml (or any type ending with +xml); for a JSON body, it must be application/json, text/json (or any type ending with +json).</span></span>

#### <a name="convert-json-toosoap-using-a-liquid-template"></a><span data-ttu-id="fcd71-325">Converter JSON tooSOAP usando um modelo líquido</span><span class="sxs-lookup"><span data-stu-id="fcd71-325">Convert JSON tooSOAP using a Liquid template</span></span>
```xml
<set-body template="liquid">
    <soap:Envelope xmlns="http://tempuri.org/" xmlns:soap="http://schemas.xmlsoap.org/soap/envelope/">
        <soap:Body>
            <GetOpenOrders>
                <cust>{{body.getOpenOrders.cust}}</cust>
            </GetOpenOrders>
        </soap:Body>
    </soap:Envelope>
</set-body>
```

#### <a name="tranform-json-using-a-liquid-template"></a><span data-ttu-id="fcd71-326">Transformar JSON usando um modelo Líquido</span><span class="sxs-lookup"><span data-stu-id="fcd71-326">Tranform JSON using a Liquid template</span></span>
```xml
{
"order": {
    "id": "{{body.customer.purchase.identifier}}",
    "summary": "{{body.customer.purchase.orderShortDesc}}"
    }
}
```

### <a name="elements"></a><span data-ttu-id="fcd71-327">Elementos</span><span class="sxs-lookup"><span data-stu-id="fcd71-327">Elements</span></span>  
  
|<span data-ttu-id="fcd71-328">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-328">Name</span></span>|<span data-ttu-id="fcd71-329">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-329">Description</span></span>|<span data-ttu-id="fcd71-330">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-330">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fcd71-331">set-body</span><span class="sxs-lookup"><span data-stu-id="fcd71-331">set-body</span></span>|<span data-ttu-id="fcd71-332">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="fcd71-332">Root element.</span></span> <span data-ttu-id="fcd71-333">Contém o texto de saudação ou expressões que retornam um corpo.</span><span class="sxs-lookup"><span data-stu-id="fcd71-333">Contains hello body text or an expressions that returns a body.</span></span>|<span data-ttu-id="fcd71-334">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-334">Yes</span></span>|  

### <a name="properties"></a><span data-ttu-id="fcd71-335">Propriedades</span><span class="sxs-lookup"><span data-stu-id="fcd71-335">Properties</span></span>  
  
|<span data-ttu-id="fcd71-336">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-336">Name</span></span>|<span data-ttu-id="fcd71-337">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-337">Description</span></span>|<span data-ttu-id="fcd71-338">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-338">Required</span></span>|<span data-ttu-id="fcd71-339">Padrão</span><span class="sxs-lookup"><span data-stu-id="fcd71-339">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="fcd71-340">template</span><span class="sxs-lookup"><span data-stu-id="fcd71-340">template</span></span>|<span data-ttu-id="fcd71-341">Modo de modelagem do hello toochange usado Olá definir corpo política executará.</span><span class="sxs-lookup"><span data-stu-id="fcd71-341">Used toochange hello templating mode that hello set body policy will run in.</span></span> <span data-ttu-id="fcd71-342">Atualmente, o valor de saudação só tem suportada é:</span><span class="sxs-lookup"><span data-stu-id="fcd71-342">Currently hello only supported value is:</span></span><br /><br /><span data-ttu-id="fcd71-343">Olá - líquido - definir corpo política usará o mecanismo de modelagem líquidos Olá</span><span class="sxs-lookup"><span data-stu-id="fcd71-343">- liquid - hello set body policy will use hello liquid templating engine</span></span> |<span data-ttu-id="fcd71-344">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-344">No</span></span>|<span data-ttu-id="fcd71-345">liquid</span><span class="sxs-lookup"><span data-stu-id="fcd71-345">liquid</span></span>|  

<span data-ttu-id="fcd71-346">Para acessar informações sobre Olá solicitação e resposta, modelo líquidos Olá pode vincular o objeto de contexto tooa com hello propriedades a seguir:</span><span class="sxs-lookup"><span data-stu-id="fcd71-346">For accessing information about hello request and response, hello Liquid template can bind tooa context object with hello following properties:</span></span> <br />
<pre>context.
    Request.
        Url
        Method
        OriginalMethod
        OriginalUrl
        IpAddress
        MatchedParameters
        HasBody
        ClientCertificates
        Headers

    Response.
        StatusCode
        Method
        Headers
Url.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString

OriginalUrl.
    Scheme
    Host
    Port
    Path
    Query
    QueryString
    ToUri
    ToString
</pre>



### <a name="usage"></a><span data-ttu-id="fcd71-347">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd71-347">Usage</span></span>  
 <span data-ttu-id="fcd71-348">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fcd71-348">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fcd71-349">**Seções de política:** entrada, saída, back-end</span><span class="sxs-lookup"><span data-stu-id="fcd71-349">**Policy sections:** inbound, outbound, backend</span></span>  
  
-   <span data-ttu-id="fcd71-350">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="fcd71-350">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="fcd71-351"><a name="SetHTTPheader"></a> Definir cabeçalho HTTP</span><span class="sxs-lookup"><span data-stu-id="fcd71-351"><a name="SetHTTPheader"></a> Set HTTP header</span></span>  
 <span data-ttu-id="fcd71-352">Olá `set-header` política atribui um cabeçalho de solicitação e/ou resposta do valor tooan existente ou adiciona um novo cabeçalho de solicitação de e/ou resposta.</span><span class="sxs-lookup"><span data-stu-id="fcd71-352">hello `set-header` policy assigns a value tooan existing response and/or request header or adds a new response and/or request header.</span></span>  
  
 <span data-ttu-id="fcd71-353">Insere uma lista de cabeçalhos HTTP em uma mensagem HTTP.</span><span class="sxs-lookup"><span data-stu-id="fcd71-353">Inserts a list of HTTP headers into an HTTP message.</span></span> <span data-ttu-id="fcd71-354">Quando colocada em um pipeline de entrada, essa política define os cabeçalhos HTTP Olá para solicitação hello está sendo passado toohello serviço de destino.</span><span class="sxs-lookup"><span data-stu-id="fcd71-354">When placed in an inbound pipeline, this policy sets hello HTTP headers for hello request being passed toohello target service.</span></span> <span data-ttu-id="fcd71-355">Quando colocada em um pipeline de saída, essa política define os cabeçalhos HTTP Olá para resposta de hello está sendo enviada cliente toohello do gateway.</span><span class="sxs-lookup"><span data-stu-id="fcd71-355">When placed in an outbound pipeline, this policy sets hello HTTP headers for hello response being sent toohello gateway’s client.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="fcd71-356">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="fcd71-356">Policy statement</span></span>  
  
```xml  
<set-header name="header name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple headers with hello same name add additional value elements-->  
</set-header>  
```  
  
### <a name="examples"></a><span data-ttu-id="fcd71-357">Exemplos</span><span class="sxs-lookup"><span data-stu-id="fcd71-357">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="fcd71-358">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fcd71-358">Example</span></span>  
  
```xml  
<set-header name="some header name" exists-action="override">  
    <value>20</value>   
</set-header>  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="fcd71-359">Encaminhar o serviço de back-end de toohello de informações de contexto</span><span class="sxs-lookup"><span data-stu-id="fcd71-359">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="fcd71-360">Este exemplo mostra como a diretiva tooapply Olá API nível toosupply serviço de back-end de toohello de informações de contexto.</span><span class="sxs-lookup"><span data-stu-id="fcd71-360">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="fcd71-361">Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too10:30.</span><span class="sxs-lookup"><span data-stu-id="fcd71-361">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="fcd71-362">Em 12:10, há uma demonstração de como chamar uma operação no portal do desenvolvedor Olá onde você pode ver a política de saudação no trabalho.</span><span class="sxs-lookup"><span data-stu-id="fcd71-362">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward some context information, user id and hello region hello gateway is hosted in, toohello backend service for logging or evaluation -->  
<set-header name="x-request-context-data" exists-action="override">  
  <value>@(context.User.Id)</value>  
  <value>@(context.Deployment.Region)</value>  
</set-header>  
```  
  
 <span data-ttu-id="fcd71-363">Para obter mais informações, veja [Expressões de política](api-management-policy-expressions.md) e [Variável de contexto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="fcd71-363">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="fcd71-364">Elementos</span><span class="sxs-lookup"><span data-stu-id="fcd71-364">Elements</span></span>  
  
|<span data-ttu-id="fcd71-365">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-365">Name</span></span>|<span data-ttu-id="fcd71-366">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-366">Description</span></span>|<span data-ttu-id="fcd71-367">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-367">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fcd71-368">set-header</span><span class="sxs-lookup"><span data-stu-id="fcd71-368">set-header</span></span>|<span data-ttu-id="fcd71-369">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="fcd71-369">Root element.</span></span>|<span data-ttu-id="fcd71-370">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-370">Yes</span></span>|  
|<span data-ttu-id="fcd71-371">valor</span><span class="sxs-lookup"><span data-stu-id="fcd71-371">value</span></span>|<span data-ttu-id="fcd71-372">Especifica o valor de saudação do hello cabeçalho toobe conjunto.</span><span class="sxs-lookup"><span data-stu-id="fcd71-372">Specifies hello value of hello header toobe set.</span></span> <span data-ttu-id="fcd71-373">Para vários cabeçalhos com hello mesmo nome adicionar adicional `value` elementos.</span><span class="sxs-lookup"><span data-stu-id="fcd71-373">For multiple headers with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="fcd71-374">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-374">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="fcd71-375">Propriedades</span><span class="sxs-lookup"><span data-stu-id="fcd71-375">Properties</span></span>  
  
|<span data-ttu-id="fcd71-376">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-376">Name</span></span>|<span data-ttu-id="fcd71-377">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-377">Description</span></span>|<span data-ttu-id="fcd71-378">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-378">Required</span></span>|<span data-ttu-id="fcd71-379">Padrão</span><span class="sxs-lookup"><span data-stu-id="fcd71-379">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="fcd71-380">exists-action</span><span class="sxs-lookup"><span data-stu-id="fcd71-380">exists-action</span></span>|<span data-ttu-id="fcd71-381">Especifica qual ação tootake quando Olá cabeçalho já está especificado.</span><span class="sxs-lookup"><span data-stu-id="fcd71-381">Specifies what action tootake when hello header is already specified.</span></span> <span data-ttu-id="fcd71-382">Esse atributo deve ter uma saudação valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="fcd71-382">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="fcd71-383">-valor de substituição - substitui saudação do cabeçalho existente hello.</span><span class="sxs-lookup"><span data-stu-id="fcd71-383">-   override - replaces hello value of hello existing header.</span></span><br /><span data-ttu-id="fcd71-384">-Ignorar - não substitui o valor do cabeçalho existente hello.</span><span class="sxs-lookup"><span data-stu-id="fcd71-384">-   skip - does not replace hello existing header value.</span></span><br /><span data-ttu-id="fcd71-385">-Acrescentar - acrescenta Olá valor toohello valor do cabeçalho existente.</span><span class="sxs-lookup"><span data-stu-id="fcd71-385">-   append - appends hello value toohello existing header value.</span></span><br /><span data-ttu-id="fcd71-386">-delete - remove o cabeçalho de saudação da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-386">-   delete - removes hello header from hello request.</span></span><br /><br /> <span data-ttu-id="fcd71-387">Quando definido muito`override` alistando várias entradas com hello mesmo nome resultados no cabeçalho Olá sendo conjunto acordo tooall entradas (que serão listadas várias vezes); somente os valores listados serão definidos no resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-387">When set too`override` enlisting multiple entries with hello same name results in hello header being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="fcd71-388">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-388">No</span></span>|<span data-ttu-id="fcd71-389">override</span><span class="sxs-lookup"><span data-stu-id="fcd71-389">override</span></span>|  
|<span data-ttu-id="fcd71-390">name</span><span class="sxs-lookup"><span data-stu-id="fcd71-390">name</span></span>|<span data-ttu-id="fcd71-391">Especifica o nome do conjunto de toobe do cabeçalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-391">Specifies name of hello header toobe set.</span></span>|<span data-ttu-id="fcd71-392">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-392">Yes</span></span>|<span data-ttu-id="fcd71-393">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-393">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="fcd71-394">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd71-394">Usage</span></span>  
 <span data-ttu-id="fcd71-395">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fcd71-395">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fcd71-396">**Seções da política:** entrada, saída, back-end, em caso de erro</span><span class="sxs-lookup"><span data-stu-id="fcd71-396">**Policy sections:** inbound, outbound, backend, on-error</span></span>  
  
-   <span data-ttu-id="fcd71-397">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="fcd71-397">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="fcd71-398"><a name="SetQueryStringParameter"></a> Definir parâmetro de cadeia de consulta</span><span class="sxs-lookup"><span data-stu-id="fcd71-398"><a name="SetQueryStringParameter"></a> Set query string parameter</span></span>  
 <span data-ttu-id="fcd71-399">Olá `set-query-parameter` política adiciona, substitui o valor, ou parâmetro de cadeia de caracteres de consulta de solicitação de exclusões.</span><span class="sxs-lookup"><span data-stu-id="fcd71-399">hello `set-query-parameter` policy adds, replaces value of, or deletes request query string parameter.</span></span> <span data-ttu-id="fcd71-400">Pode ser usado toopass parâmetros de consulta esperados pelo serviço de back-end de saudação que são opcionais ou nunca estão presentes na solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-400">Can be used toopass query parameters expected by hello backend service which are optional or never present in hello request.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="fcd71-401">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="fcd71-401">Policy statement</span></span>  
  
```xml  
<set-query-parameter name="param name" exists-action="override | skip | append | delete">  
    <value>value</value> <!--for multiple parameters with hello same name add additional value elements-->  
</set-query-parameter>  
```  
  
### <a name="examples"></a><span data-ttu-id="fcd71-402">Exemplos</span><span class="sxs-lookup"><span data-stu-id="fcd71-402">Examples</span></span>  
  
#### <a name="example"></a><span data-ttu-id="fcd71-403">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fcd71-403">Example</span></span>  
  
```xml  
  
<set-query-parameter>  
  <parameter name="api-key" exists-action="skip">  
    <value>12345678901</value>  
  </parameter>  
  <!-- for multiple parameters with hello same name add additional value elements -->  
</set-query-parameter>  
  
```  
  
#### <a name="forward-context-information-toohello-backend-service"></a><span data-ttu-id="fcd71-404">Encaminhar o serviço de back-end de toohello de informações de contexto</span><span class="sxs-lookup"><span data-stu-id="fcd71-404">Forward context information toohello backend service</span></span>  
 <span data-ttu-id="fcd71-405">Este exemplo mostra como a diretiva tooapply Olá API nível toosupply serviço de back-end de toohello de informações de contexto.</span><span class="sxs-lookup"><span data-stu-id="fcd71-405">This example shows how tooapply policy at hello API level toosupply context information toohello backend service.</span></span> <span data-ttu-id="fcd71-406">Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too10:30.</span><span class="sxs-lookup"><span data-stu-id="fcd71-406">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too10:30.</span></span> <span data-ttu-id="fcd71-407">Em 12:10, há uma demonstração de como chamar uma operação no portal do desenvolvedor Olá onde você pode ver a política de saudação no trabalho.</span><span class="sxs-lookup"><span data-stu-id="fcd71-407">At 12:10 there is a demo of calling an operation in hello developer portal where you can see hello policy at work.</span></span>  
  
```xml  
<!-- Copy this snippet into hello inbound element tooforward a piece of context, product name in this example, toohello backend service for logging or evaluation -->  
<set-query-parameter name="x-product-name" exists-action="override">  
  <value>@(context.Product.Name)</value>  
</set-query-parameter>  
  
```  
  
 <span data-ttu-id="fcd71-408">Para obter mais informações, veja [Expressões de política](api-management-policy-expressions.md) e [Variável de contexto](api-management-policy-expressions.md#ContextVariables).</span><span class="sxs-lookup"><span data-stu-id="fcd71-408">For more information, see [Policy expressions](api-management-policy-expressions.md) and [Context variable](api-management-policy-expressions.md#ContextVariables).</span></span>  
  
### <a name="elements"></a><span data-ttu-id="fcd71-409">Elementos</span><span class="sxs-lookup"><span data-stu-id="fcd71-409">Elements</span></span>  
  
|<span data-ttu-id="fcd71-410">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-410">Name</span></span>|<span data-ttu-id="fcd71-411">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-411">Description</span></span>|<span data-ttu-id="fcd71-412">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-412">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fcd71-413">set-query-parameter</span><span class="sxs-lookup"><span data-stu-id="fcd71-413">set-query-parameter</span></span>|<span data-ttu-id="fcd71-414">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="fcd71-414">Root element.</span></span>|<span data-ttu-id="fcd71-415">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-415">Yes</span></span>|  
|<span data-ttu-id="fcd71-416">valor</span><span class="sxs-lookup"><span data-stu-id="fcd71-416">value</span></span>|<span data-ttu-id="fcd71-417">Especifica o valor de Olá Olá parâmetro toobe do conjunto de consulta.</span><span class="sxs-lookup"><span data-stu-id="fcd71-417">Specifies hello value of hello query parameter toobe set.</span></span> <span data-ttu-id="fcd71-418">Para vários parâmetros de consulta com hello mesmo nome adicionar adicional `value` elementos.</span><span class="sxs-lookup"><span data-stu-id="fcd71-418">For multiple query parameters with hello same name add additional `value` elements.</span></span>|<span data-ttu-id="fcd71-419">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-419">Yes</span></span>|  
  
### <a name="properties"></a><span data-ttu-id="fcd71-420">Propriedades</span><span class="sxs-lookup"><span data-stu-id="fcd71-420">Properties</span></span>  
  
|<span data-ttu-id="fcd71-421">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-421">Name</span></span>|<span data-ttu-id="fcd71-422">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-422">Description</span></span>|<span data-ttu-id="fcd71-423">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-423">Required</span></span>|<span data-ttu-id="fcd71-424">Padrão</span><span class="sxs-lookup"><span data-stu-id="fcd71-424">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="fcd71-425">exists-action</span><span class="sxs-lookup"><span data-stu-id="fcd71-425">exists-action</span></span>|<span data-ttu-id="fcd71-426">Especifica qual ação tootake quando o parâmetro de consulta Olá já está especificado.</span><span class="sxs-lookup"><span data-stu-id="fcd71-426">Specifies what action tootake when hello query parameter is already specified.</span></span> <span data-ttu-id="fcd71-427">Esse atributo deve ter uma saudação valores a seguir.</span><span class="sxs-lookup"><span data-stu-id="fcd71-427">This attribute must have one of hello following values.</span></span><br /><br /> <span data-ttu-id="fcd71-428">-Substitua - substitui Olá valor de parâmetro de saudação existente.</span><span class="sxs-lookup"><span data-stu-id="fcd71-428">-   override - replaces hello value of hello existing parameter.</span></span><br /><span data-ttu-id="fcd71-429">-Ignorar - não substitui o valor de parâmetro de consulta existente hello.</span><span class="sxs-lookup"><span data-stu-id="fcd71-429">-   skip - does not replace hello existing query parameter value.</span></span><br /><span data-ttu-id="fcd71-430">-Acrescentar - acrescenta o valor de parâmetro do hello valor toohello existente consulta.</span><span class="sxs-lookup"><span data-stu-id="fcd71-430">-   append - appends hello value toohello existing query parameter value.</span></span><br /><span data-ttu-id="fcd71-431">-delete - remove o parâmetro de consulta de saudação da solicitação de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-431">-   delete - removes hello query parameter from hello request.</span></span><br /><br /> <span data-ttu-id="fcd71-432">Quando definido muito`override` alistando várias entradas com hello mesmo nome resultados no parâmetro de consulta Olá sendo conjunto acordo tooall entradas (que serão listadas várias vezes); somente os valores listados serão definidos no resultado de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-432">When set too`override` enlisting multiple entries with hello same name results in hello query parameter being set according tooall entries (which will be listed multiple times); only listed values will be set in hello result.</span></span>|<span data-ttu-id="fcd71-433">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-433">No</span></span>|<span data-ttu-id="fcd71-434">override</span><span class="sxs-lookup"><span data-stu-id="fcd71-434">override</span></span>|  
|<span data-ttu-id="fcd71-435">name</span><span class="sxs-lookup"><span data-stu-id="fcd71-435">name</span></span>|<span data-ttu-id="fcd71-436">Especifica o nome do conjunto de toobe do parâmetro de consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-436">Specifies name of hello query parameter toobe set.</span></span>|<span data-ttu-id="fcd71-437">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-437">Yes</span></span>|<span data-ttu-id="fcd71-438">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-438">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="fcd71-439">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd71-439">Usage</span></span>  
 <span data-ttu-id="fcd71-440">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fcd71-440">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fcd71-441">**Seções de política:** de entrada, back-end</span><span class="sxs-lookup"><span data-stu-id="fcd71-441">**Policy sections:** inbound, backend</span></span>  
  
-   <span data-ttu-id="fcd71-442">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="fcd71-442">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="fcd71-443"><a name="RewriteURL"></a> Reescrever URL</span><span class="sxs-lookup"><span data-stu-id="fcd71-443"><a name="RewriteURL"></a> Rewrite URL</span></span>  
 <span data-ttu-id="fcd71-444">Olá `rewrite-uri` política converte uma URL de solicitação de forma pública formulário toohello esperada pelo serviço da web de hello, conforme mostrado no exemplo a seguir de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-444">hello `rewrite-uri` policy converts a request URL from its public form toohello form expected by hello web service, as shown in hello following example.</span></span>  
  
-   <span data-ttu-id="fcd71-445">URL pública – `http://api.example.com/storenumber/ordernumber`</span><span class="sxs-lookup"><span data-stu-id="fcd71-445">Public URL - `http://api.example.com/storenumber/ordernumber`</span></span>  
  
-   <span data-ttu-id="fcd71-446">URL de Solicitação – `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span><span class="sxs-lookup"><span data-stu-id="fcd71-446">Request URL - `http://api.example.com/v2/US/hardware/storenumber&ordernumber?City&State`</span></span>  
  
 <span data-ttu-id="fcd71-447">Essa política pode ser usada quando uma URL humana e/ou navegador amigável deve ser transformada em formato de URL de saudação esperado pelo serviço da web de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-447">This policy can be used when a human and/or browser-friendly URL should be transformed into hello URL format expected by hello web service.</span></span> <span data-ttu-id="fcd71-448">Essa política só precisa toobe aplicada ao expor um formato de URL alternativo, como URLs limpas, URLs RESTful, URLs amigáveis ou URLs de SEO amigável que sejam URLs puramente estruturais que não contêm uma cadeia de caracteres de consulta e contêm apenas o caminho de saudação de saudação recurso (após o esquema de saudação e da autoridade de saudação).</span><span class="sxs-lookup"><span data-stu-id="fcd71-448">This policy only needs toobe applied when exposing an alternative URL format, such as clean URLs, RESTful URLs, user-friendly URLs or SEO-friendly URLs that are purely structural URLs that do not contain a query string and instead contain only hello path of hello resource (after hello scheme and hello authority).</span></span> <span data-ttu-id="fcd71-449">Frequentemente, isso é feito para fins estéticos, de usabilidade ou de otimização do mecanismo de pesquisa (SEO).</span><span class="sxs-lookup"><span data-stu-id="fcd71-449">This is often done for aesthetic, usability, or search engine optimization (SEO) purposes.</span></span>  
  
> [!NOTE]
>  <span data-ttu-id="fcd71-450">Você só pode adicionar parâmetros de cadeia de caracteres de consulta usando a política de saudação.</span><span class="sxs-lookup"><span data-stu-id="fcd71-450">You can only add query string parameters using hello policy.</span></span> <span data-ttu-id="fcd71-451">Não é possível adicionar parâmetros de caminho de modelo extra na Olá regravar URL.</span><span class="sxs-lookup"><span data-stu-id="fcd71-451">You cannot add extra template path parameters in hello rewrite URL.</span></span>  

### <a name="policy-statement"></a><span data-ttu-id="fcd71-452">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="fcd71-452">Policy statement</span></span>  
  
```xml  
<rewrite-uri template="uri template" copy-unmatched-params="true | false" />  
```  
  
### <a name="example"></a><span data-ttu-id="fcd71-453">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fcd71-453">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/v2/US/hardware/{storenumber}&{ordernumber}?City=city&State=state" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put?c=d -->
```  
```xml
<!-- Assuming incoming request is /get?a=b&c=d and operation template is set too/get?a={b} -->
<policies>  
    <inbound>  
        <base />  
        <rewrite-uri template="/put" copy-unmatched-params="false" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
<!-- Resulting URL will be /put -->
```

### <a name="elements"></a><span data-ttu-id="fcd71-454">Elementos</span><span class="sxs-lookup"><span data-stu-id="fcd71-454">Elements</span></span>  
  
|<span data-ttu-id="fcd71-455">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-455">Name</span></span>|<span data-ttu-id="fcd71-456">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-456">Description</span></span>|<span data-ttu-id="fcd71-457">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-457">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fcd71-458">rewrite-uri</span><span class="sxs-lookup"><span data-stu-id="fcd71-458">rewrite-uri</span></span>|<span data-ttu-id="fcd71-459">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="fcd71-459">Root element.</span></span>|<span data-ttu-id="fcd71-460">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-460">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="fcd71-461">Atributos</span><span class="sxs-lookup"><span data-stu-id="fcd71-461">Attributes</span></span>  
  
|<span data-ttu-id="fcd71-462">Atributo</span><span class="sxs-lookup"><span data-stu-id="fcd71-462">Attribute</span></span>|<span data-ttu-id="fcd71-463">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-463">Description</span></span>|<span data-ttu-id="fcd71-464">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-464">Required</span></span>|<span data-ttu-id="fcd71-465">Padrão</span><span class="sxs-lookup"><span data-stu-id="fcd71-465">Default</span></span>|  
|---------------|-----------------|--------------|-------------|  
|<span data-ttu-id="fcd71-466">template</span><span class="sxs-lookup"><span data-stu-id="fcd71-466">template</span></span>|<span data-ttu-id="fcd71-467">Olá o URL do serviço web real com quaisquer parâmetros de cadeia de caracteres de consulta.</span><span class="sxs-lookup"><span data-stu-id="fcd71-467">hello actual web service URL with any query string parameters.</span></span> <span data-ttu-id="fcd71-468">Ao usar expressões, o valor de inteiro Olá deve ser uma expressão.</span><span class="sxs-lookup"><span data-stu-id="fcd71-468">When using expressions, hello whole value must be an expression.</span></span>|<span data-ttu-id="fcd71-469">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-469">Yes</span></span>|<span data-ttu-id="fcd71-470">N/D</span><span class="sxs-lookup"><span data-stu-id="fcd71-470">N/A</span></span>|  
|<span data-ttu-id="fcd71-471">copy-unmatched-params</span><span class="sxs-lookup"><span data-stu-id="fcd71-471">copy-unmatched-params</span></span>|<span data-ttu-id="fcd71-472">Especifica se os parâmetros de consulta na solicitação de entrada de saudação não está presente no modelo de URL original Olá são adicionados toohello URL definido pelo Olá grave novamente o modelo</span><span class="sxs-lookup"><span data-stu-id="fcd71-472">Specifies whether query parameters in hello incoming request not present in hello original URL template are added toohello URL defined by hello re-write template</span></span>|<span data-ttu-id="fcd71-473">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-473">No</span></span>|<span data-ttu-id="fcd71-474">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="fcd71-474">true</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="fcd71-475">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd71-475">Usage</span></span>  
 <span data-ttu-id="fcd71-476">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fcd71-476">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fcd71-477">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="fcd71-477">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="fcd71-478">**Escopos de política:** produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="fcd71-478">**Policy scopes:** product, API, operation</span></span>  
  
##  <span data-ttu-id="fcd71-479"><a name="XSLTransform"></a> Transformar XML usando um XSLT</span><span class="sxs-lookup"><span data-stu-id="fcd71-479"><a name="XSLTransform"></a> Transform XML using an XSLT</span></span>  
 <span data-ttu-id="fcd71-480">Olá `Transform XML using an XSLT` política se aplica a um tooXML de transformação XSL no corpo de solicitação ou resposta hello.</span><span class="sxs-lookup"><span data-stu-id="fcd71-480">hello `Transform XML using an XSLT` policy applies an XSL transformation tooXML in hello request or response body.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="fcd71-481">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="fcd71-481">Policy statement</span></span>  
  
```xml  
<xsl-transform>  
    <parameter name="User-Agent">@(context.Request.Headers.GetValueOrDefault("User-Agent","non-specified"))</parameter>  
    <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
        <xsl:output method="xml" indent="yes" />  
        <xsl:param name="User-Agent" />  
        <xsl:template match="* | @* | node()">  
            <xsl:copy>  
                <xsl:if test="self::* and not(parent::*)">  
                    <xsl:attribute name="User-Agent">  
                        <xsl:value-of select="$User-Agent" />  
                    </xsl:attribute>  
                </xsl:if>  
                <xsl:apply-templates select="* | @* | node()" />  
            </xsl:copy>  
        </xsl:template>  
    </xsl:stylesheet>  
  </xsl-transform>  
```  
  
### <a name="example"></a><span data-ttu-id="fcd71-482">Exemplo</span><span class="sxs-lookup"><span data-stu-id="fcd71-482">Example</span></span>  
  
```xml  
<policies>  
  <inbound>  
      <base />  
  </inbound>  
  <outbound>  
      <base />  
      <xsl-transform>  
        <xsl:stylesheet version="1.0" xmlns:xsl="http://www.w3.org/1999/XSL/Transform">  
            <xsl:output omit-xml-declaration="yes" method="xml" indent="yes" />  
            <!-- Copy all nodes directly-->  
            <xsl:template match="node()| @*|*">  
                <xsl:copy>  
                    <xsl:apply-templates select="@* | node()|*" />  
                </xsl:copy>  
            </xsl:template>  
        </xsl:stylesheet>  
    </xsl-transform>  
  </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="fcd71-483">Elementos</span><span class="sxs-lookup"><span data-stu-id="fcd71-483">Elements</span></span>  
  
|<span data-ttu-id="fcd71-484">Nome</span><span class="sxs-lookup"><span data-stu-id="fcd71-484">Name</span></span>|<span data-ttu-id="fcd71-485">Descrição</span><span class="sxs-lookup"><span data-stu-id="fcd71-485">Description</span></span>|<span data-ttu-id="fcd71-486">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="fcd71-486">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="fcd71-487">xsl-transform</span><span class="sxs-lookup"><span data-stu-id="fcd71-487">xsl-transform</span></span>|<span data-ttu-id="fcd71-488">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="fcd71-488">Root element.</span></span>|<span data-ttu-id="fcd71-489">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-489">Yes</span></span>|  
|<span data-ttu-id="fcd71-490">parâmetro</span><span class="sxs-lookup"><span data-stu-id="fcd71-490">parameter</span></span>|<span data-ttu-id="fcd71-491">Variáveis usadas toodefine usadas na transformação de saudação</span><span class="sxs-lookup"><span data-stu-id="fcd71-491">Used toodefine variables used in hello transform</span></span>|<span data-ttu-id="fcd71-492">Não</span><span class="sxs-lookup"><span data-stu-id="fcd71-492">No</span></span>|  
|<span data-ttu-id="fcd71-493">xsl:stylesheet</span><span class="sxs-lookup"><span data-stu-id="fcd71-493">xsl:stylesheet</span></span>|<span data-ttu-id="fcd71-494">Elemento de folha de estilos de raiz.</span><span class="sxs-lookup"><span data-stu-id="fcd71-494">Root stylesheet element.</span></span> <span data-ttu-id="fcd71-495">Todos os elementos e atributos definidos no seguem o padrão de saudação [especificação XSLT](http://www.w3.org/TR/xslt)</span><span class="sxs-lookup"><span data-stu-id="fcd71-495">All elements and attributes defined within follow hello standard [XSLT specification](http://www.w3.org/TR/xslt)</span></span>|<span data-ttu-id="fcd71-496">Sim</span><span class="sxs-lookup"><span data-stu-id="fcd71-496">Yes</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="fcd71-497">Uso</span><span class="sxs-lookup"><span data-stu-id="fcd71-497">Usage</span></span>  
 <span data-ttu-id="fcd71-498">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="fcd71-498">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="fcd71-499">**Seções de política:** de entrada, de saída</span><span class="sxs-lookup"><span data-stu-id="fcd71-499">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="fcd71-500">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="fcd71-500">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="fcd71-501">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="fcd71-501">Next steps</span></span>
<span data-ttu-id="fcd71-502">Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="fcd71-502">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
