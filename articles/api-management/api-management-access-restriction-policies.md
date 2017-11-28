---
title: "políticas de restrição de acesso de gerenciamento de API aaaAzure | Microsoft Docs"
description: "Saiba mais sobre políticas de restrição de acesso de saudação disponíveis para uso no gerenciamento de API do Azure."
services: api-management
documentationcenter: 
author: miaojiang
manager: erikre
editor: 
ms.assetid: 034febe3-465f-4840-9fc6-c448ef520b0f
ms.service: api-management
ms.workload: mobile
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/09/2017
ms.author: apimpm
ms.openlocfilehash: 0ef368c2781d9a5cf9eaaa41a47489c904ed3198
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="e48d9-103">Políticas de restrição de acesso do Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="e48d9-103">API Management access restriction policies</span></span>
<span data-ttu-id="e48d9-104">Este tópico fornece uma referência para Olá políticas de gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="e48d9-104">This topic provides a reference for hello following API Management policies.</span></span> <span data-ttu-id="e48d9-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="e48d9-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="e48d9-106"><a name="AccessRestrictionPolicies"></a> Políticas de restrição de acesso</span><span class="sxs-lookup"><span data-stu-id="e48d9-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="e48d9-107">[Verificar cabeçalho HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) - Impõe a existência e/ou valor de um cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="e48d9-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="e48d9-108">[Limitar a taxa de chamada por assinatura](api-management-access-restriction-policies.md#LimitCallRate) - Previne picos de uso da API limitando a taxa de chamada, baseado em assinatura.</span><span class="sxs-lookup"><span data-stu-id="e48d9-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="e48d9-109">[Limitar a taxa de chamada por chave](#LimitCallRateByKey) - Previne picos de uso da API limitando a taxa de chamada, baseado em chave.</span><span class="sxs-lookup"><span data-stu-id="e48d9-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="e48d9-110">[Restringir IP do autor da chamada](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filtra (permite/recusa) chamadas de endereços IP específicos e/ou intervalos de endereços.</span><span class="sxs-lookup"><span data-stu-id="e48d9-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="e48d9-111">[Definir a cota de uso por assinatura](api-management-access-restriction-policies.md#SetUsageQuota) -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por assinatura.</span><span class="sxs-lookup"><span data-stu-id="e48d9-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="e48d9-112">[Definir a cota de uso pela chave](#SetUsageQuotaByKey) -permite que você tooenforce uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por chave.</span><span class="sxs-lookup"><span data-stu-id="e48d9-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you tooenforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="e48d9-113">[Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) - Impõe a existência e a validade de JWT extraída de um cabeçalho HTTP especificado ou um parâmetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="e48d9-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="e48d9-114"><a name="CheckHTTPHeader"></a> Verificar cabeçalho HTTP</span><span class="sxs-lookup"><span data-stu-id="e48d9-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="e48d9-115">Saudação de uso `check-header` tooenforce de política que uma solicitação tem um cabeçalho HTTP especificado.</span><span class="sxs-lookup"><span data-stu-id="e48d9-115">Use hello `check-header` policy tooenforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="e48d9-116">Opcionalmente, você pode verificar toosee se o cabeçalho de saudação tem um valor específico ou para um intervalo de valores permitidos.</span><span class="sxs-lookup"><span data-stu-id="e48d9-116">You can optionally check toosee if hello header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="e48d9-117">Se Olá verificação falhar, política de saudação termina o processamento da solicitação e retorna Olá HTTP status código e mensagem de erro especificada por política hello.</span><span class="sxs-lookup"><span data-stu-id="e48d9-117">If hello check fails, hello policy terminates request processing and returns hello HTTP status code and error message specified by hello policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e48d9-118">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="e48d9-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="e48d9-119">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e48d9-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="e48d9-120">Elementos</span><span class="sxs-lookup"><span data-stu-id="e48d9-120">Elements</span></span>  
  
|<span data-ttu-id="e48d9-121">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-121">Name</span></span>|<span data-ttu-id="e48d9-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-122">Description</span></span>|<span data-ttu-id="e48d9-123">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e48d9-124">check-header</span><span class="sxs-lookup"><span data-stu-id="e48d9-124">check-header</span></span>|<span data-ttu-id="e48d9-125">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="e48d9-125">Root element.</span></span>|<span data-ttu-id="e48d9-126">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-126">Yes</span></span>|  
|<span data-ttu-id="e48d9-127">valor</span><span class="sxs-lookup"><span data-stu-id="e48d9-127">value</span></span>|<span data-ttu-id="e48d9-128">Valor do cabeçalho HTTP permitido.</span><span class="sxs-lookup"><span data-stu-id="e48d9-128">Allowed HTTP header value.</span></span> <span data-ttu-id="e48d9-129">Quando forem especificados vários elementos de valor, seleção de saudação é considerada um sucesso se qualquer um dos valores de saudação é uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="e48d9-129">When multiple value elements are specified, hello check is considered a success if any one of hello values is a match.</span></span>|<span data-ttu-id="e48d9-130">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e48d9-131">Atributos</span><span class="sxs-lookup"><span data-stu-id="e48d9-131">Attributes</span></span>  
  
|<span data-ttu-id="e48d9-132">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-132">Name</span></span>|<span data-ttu-id="e48d9-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-133">Description</span></span>|<span data-ttu-id="e48d9-134">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-134">Required</span></span>|<span data-ttu-id="e48d9-135">Padrão</span><span class="sxs-lookup"><span data-stu-id="e48d9-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e48d9-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="e48d9-136">failed-check-error-message</span></span>|<span data-ttu-id="e48d9-137">Tooreturn de mensagem de erro no corpo de resposta HTTP de saudação se o cabeçalho de saudação não existe ou tem um valor inválido.</span><span class="sxs-lookup"><span data-stu-id="e48d9-137">Error message tooreturn in hello HTTP response body if hello header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="e48d9-138">Esta mensagem deve conter quaisquer caracteres especiais adequadamente seguidos por caracteres de escape.</span><span class="sxs-lookup"><span data-stu-id="e48d9-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="e48d9-139">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-139">Yes</span></span>|<span data-ttu-id="e48d9-140">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-140">N/A</span></span>|  
|<span data-ttu-id="e48d9-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="e48d9-141">failed-check-httpcode</span></span>|<span data-ttu-id="e48d9-142">Tooreturn do código de HTTP Status se o cabeçalho de saudação não existe ou tem um valor inválido.</span><span class="sxs-lookup"><span data-stu-id="e48d9-142">HTTP Status code tooreturn if hello header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="e48d9-143">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-143">Yes</span></span>|<span data-ttu-id="e48d9-144">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-144">N/A</span></span>|  
|<span data-ttu-id="e48d9-145">header-name</span><span class="sxs-lookup"><span data-stu-id="e48d9-145">header-name</span></span>|<span data-ttu-id="e48d9-146">nome de saudação do hello toocheck do cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="e48d9-146">hello name of hello HTTP Header toocheck.</span></span>|<span data-ttu-id="e48d9-147">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-147">Yes</span></span>|<span data-ttu-id="e48d9-148">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-148">N/A</span></span>|  
|<span data-ttu-id="e48d9-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="e48d9-149">ignore-case</span></span>|<span data-ttu-id="e48d9-150">Pode ser definido tooTrue ou False.</span><span class="sxs-lookup"><span data-stu-id="e48d9-150">Can be set tooTrue or False.</span></span> <span data-ttu-id="e48d9-151">Se o conjunto tooTrue caso é ignorado quando o valor do cabeçalho Olá é comparado com o conjunto de saudação de valores aceitáveis.</span><span class="sxs-lookup"><span data-stu-id="e48d9-151">If set tooTrue case is ignored when hello header value is compared against hello set of acceptable values.</span></span>|<span data-ttu-id="e48d9-152">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-152">Yes</span></span>|<span data-ttu-id="e48d9-153">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e48d9-154">Uso</span><span class="sxs-lookup"><span data-stu-id="e48d9-154">Usage</span></span>  
 <span data-ttu-id="e48d9-155">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e48d9-155">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e48d9-156">**Seções de política:** de entrada, de saída</span><span class="sxs-lookup"><span data-stu-id="e48d9-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="e48d9-157">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="e48d9-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e48d9-158"><a name="LimitCallRate"></a> Limitar a taxa de chamadas por assinatura</span><span class="sxs-lookup"><span data-stu-id="e48d9-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="e48d9-159">Olá `rate-limit` política impede o uso da API picos em uma base por assinatura, limitando Olá chamar tooa taxa especificada número por um período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="e48d9-159">hello `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="e48d9-160">Quando essa política é acionada chamador Olá recebe um `429 Too Many Requests` código de status de resposta.</span><span class="sxs-lookup"><span data-stu-id="e48d9-160">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e48d9-161">Essa política pode ser usada apenas uma vez por cada documento de política.</span><span class="sxs-lookup"><span data-stu-id="e48d9-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="e48d9-162">[Expressões de política](api-management-policy-expressions.md) não pode ser usado em qualquer um dos atributos de política Olá para esta política.</span><span class="sxs-lookup"><span data-stu-id="e48d9-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e48d9-163">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="e48d9-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="e48d9-164">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e48d9-164">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit calls="20" renewal-period="90" />  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="e48d9-165">Elementos</span><span class="sxs-lookup"><span data-stu-id="e48d9-165">Elements</span></span>  
  
|<span data-ttu-id="e48d9-166">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-166">Name</span></span>|<span data-ttu-id="e48d9-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-167">Description</span></span>|<span data-ttu-id="e48d9-168">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e48d9-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="e48d9-169">set-limit</span></span>|<span data-ttu-id="e48d9-170">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="e48d9-170">Root element.</span></span>|<span data-ttu-id="e48d9-171">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-171">Yes</span></span>|  
|<span data-ttu-id="e48d9-172">api</span><span class="sxs-lookup"><span data-stu-id="e48d9-172">api</span></span>|<span data-ttu-id="e48d9-173">Adicione um ou mais desses elementos tooimpose um limite de taxa de chamada nas APIs no produto hello.</span><span class="sxs-lookup"><span data-stu-id="e48d9-173">Add one  or more of these elements tooimpose a call rate limit on APIs within hello product.</span></span> <span data-ttu-id="e48d9-174">Limites de taxa de chamadas à API e ao produto são aplicados de forma independente.</span><span class="sxs-lookup"><span data-stu-id="e48d9-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="e48d9-175">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-175">No</span></span>|  
|<span data-ttu-id="e48d9-176">operation</span><span class="sxs-lookup"><span data-stu-id="e48d9-176">operation</span></span>|<span data-ttu-id="e48d9-177">Adicione um ou mais desses elementos tooimpose um limite de taxa de chamada nas operações em uma API.</span><span class="sxs-lookup"><span data-stu-id="e48d9-177">Add one  or more of these elements tooimpose a call rate limit on operations within an API.</span></span> <span data-ttu-id="e48d9-178">Limites de taxa de chamadas à API, operação e produto são aplicados de forma independente.</span><span class="sxs-lookup"><span data-stu-id="e48d9-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="e48d9-179">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e48d9-180">Atributos</span><span class="sxs-lookup"><span data-stu-id="e48d9-180">Attributes</span></span>  
  
|<span data-ttu-id="e48d9-181">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-181">Name</span></span>|<span data-ttu-id="e48d9-182">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-182">Description</span></span>|<span data-ttu-id="e48d9-183">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-183">Required</span></span>|<span data-ttu-id="e48d9-184">Padrão</span><span class="sxs-lookup"><span data-stu-id="e48d9-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e48d9-185">name</span><span class="sxs-lookup"><span data-stu-id="e48d9-185">name</span></span>|<span data-ttu-id="e48d9-186">nome de Olá do hello API para o limite de taxa que tooapply Olá.</span><span class="sxs-lookup"><span data-stu-id="e48d9-186">hello name of hello API for which tooapply hello rate limit.</span></span>|<span data-ttu-id="e48d9-187">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-187">Yes</span></span>|<span data-ttu-id="e48d9-188">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-188">N/A</span></span>|  
|<span data-ttu-id="e48d9-189">chamadas</span><span class="sxs-lookup"><span data-stu-id="e48d9-189">calls</span></span>|<span data-ttu-id="e48d9-190">Olá número total máximo de chamadas permitidas durante o intervalo de tempo de saudação especificado no hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e48d9-190">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e48d9-191">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-191">Yes</span></span>|<span data-ttu-id="e48d9-192">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-192">N/A</span></span>|  
|<span data-ttu-id="e48d9-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="e48d9-193">renewal-period</span></span>|<span data-ttu-id="e48d9-194">saudação do período de tempo em segundos após o qual hello cota é redefinida.</span><span class="sxs-lookup"><span data-stu-id="e48d9-194">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="e48d9-195">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-195">Yes</span></span>|<span data-ttu-id="e48d9-196">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e48d9-197">Uso</span><span class="sxs-lookup"><span data-stu-id="e48d9-197">Usage</span></span>  
 <span data-ttu-id="e48d9-198">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e48d9-198">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e48d9-199">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="e48d9-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e48d9-200">**Escopos de política:** produto</span><span class="sxs-lookup"><span data-stu-id="e48d9-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="e48d9-201"><a name="LimitCallRateByKey"></a> Limitar a taxa de chamadas por chave</span><span class="sxs-lookup"><span data-stu-id="e48d9-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="e48d9-202">Olá `rate-limit-by-key` política impede o uso da API picos em uma base por chave limitando Olá chamar tooa taxa especificada número por um período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="e48d9-202">hello `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting hello call rate tooa specified number per a specified time period.</span></span> <span data-ttu-id="e48d9-203">chave de saudação pode ter um valor de cadeia de caracteres arbitrária e normalmente é fornecido usando uma expressão de política.</span><span class="sxs-lookup"><span data-stu-id="e48d9-203">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="e48d9-204">Condição de incremento opcional pode ser adicionada toospecify as solicitações que devem ser contadas até o limite de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-204">Optional increment condition can be added toospecify which requests should be counted towards hello limit.</span></span> <span data-ttu-id="e48d9-205">Quando essa política é acionada chamador Olá recebe um `429 Too Many Requests` código de status de resposta.</span><span class="sxs-lookup"><span data-stu-id="e48d9-205">When this policy is triggered hello caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="e48d9-206">Para obter mais informações e exemplos dessa política, consulte [Limitação de solicitação avançada com o Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="e48d9-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e48d9-207">Essa política pode ser usada apenas uma vez por cada documento de política.</span><span class="sxs-lookup"><span data-stu-id="e48d9-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e48d9-208">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="e48d9-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="e48d9-209">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e48d9-209">Example</span></span>  
 <span data-ttu-id="e48d9-210">Em Olá exemplo a seguir, o limite de taxa de saudação é codificado por endereço IP do chamador Olá.</span><span class="sxs-lookup"><span data-stu-id="e48d9-210">In hello following example, hello rate limit is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <rate-limit-by-key  calls="10"  
              renewal-period="60"  
              increment-condition="@(context.Response.StatusCode == 200)"  
              counter-key="@(context.Request.IpAddress)"/>  
    </inbound>  
    <outbound>  
        <base />          
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="e48d9-211">Elementos</span><span class="sxs-lookup"><span data-stu-id="e48d9-211">Elements</span></span>  
  
|<span data-ttu-id="e48d9-212">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-212">Name</span></span>|<span data-ttu-id="e48d9-213">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-213">Description</span></span>|<span data-ttu-id="e48d9-214">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e48d9-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="e48d9-215">set-limit</span></span>|<span data-ttu-id="e48d9-216">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="e48d9-216">Root element.</span></span>|<span data-ttu-id="e48d9-217">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e48d9-218">Atributos</span><span class="sxs-lookup"><span data-stu-id="e48d9-218">Attributes</span></span>  
  
|<span data-ttu-id="e48d9-219">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-219">Name</span></span>|<span data-ttu-id="e48d9-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-220">Description</span></span>|<span data-ttu-id="e48d9-221">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-221">Required</span></span>|<span data-ttu-id="e48d9-222">Padrão</span><span class="sxs-lookup"><span data-stu-id="e48d9-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e48d9-223">chamadas</span><span class="sxs-lookup"><span data-stu-id="e48d9-223">calls</span></span>|<span data-ttu-id="e48d9-224">Olá número total máximo de chamadas permitidas durante o intervalo de tempo de saudação especificado no hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e48d9-224">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e48d9-225">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-225">Yes</span></span>|<span data-ttu-id="e48d9-226">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-226">N/A</span></span>|  
|<span data-ttu-id="e48d9-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="e48d9-227">counter-key</span></span>|<span data-ttu-id="e48d9-228">Olá toouse chave para política de limite de taxa de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-228">hello key toouse for hello rate limit policy.</span></span>|<span data-ttu-id="e48d9-229">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-229">Yes</span></span>|<span data-ttu-id="e48d9-230">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-230">N/A</span></span>|  
|<span data-ttu-id="e48d9-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="e48d9-231">increment-condition</span></span>|<span data-ttu-id="e48d9-232">expressão booleana Hello, especificando se a solicitação Olá deve ser contabilizada em direção a cota de saudação (`true`).</span><span class="sxs-lookup"><span data-stu-id="e48d9-232">hello boolean expression specifying if hello request should be counted towards hello quota (`true`).</span></span>|<span data-ttu-id="e48d9-233">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-233">No</span></span>|<span data-ttu-id="e48d9-234">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-234">N/A</span></span>|  
|<span data-ttu-id="e48d9-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="e48d9-235">renewal-period</span></span>|<span data-ttu-id="e48d9-236">saudação do período de tempo em segundos após o qual hello cota é redefinida.</span><span class="sxs-lookup"><span data-stu-id="e48d9-236">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="e48d9-237">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-237">Yes</span></span>|<span data-ttu-id="e48d9-238">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e48d9-239">Uso</span><span class="sxs-lookup"><span data-stu-id="e48d9-239">Usage</span></span>  
 <span data-ttu-id="e48d9-240">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e48d9-240">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e48d9-241">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="e48d9-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e48d9-242">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="e48d9-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e48d9-243"><a name="RestrictCallerIPs"></a> Restringir IPs do chamador</span><span class="sxs-lookup"><span data-stu-id="e48d9-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="e48d9-244">Olá `ip-filter` política filtros de chamadas (permite/recusa) de endereços IP específicos e/ou intervalos de endereços.</span><span class="sxs-lookup"><span data-stu-id="e48d9-244">hello `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e48d9-245">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="e48d9-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="e48d9-246">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e48d9-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="e48d9-247">Elementos</span><span class="sxs-lookup"><span data-stu-id="e48d9-247">Elements</span></span>  
  
|<span data-ttu-id="e48d9-248">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-248">Name</span></span>|<span data-ttu-id="e48d9-249">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-249">Description</span></span>|<span data-ttu-id="e48d9-250">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e48d9-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="e48d9-251">ip-filter</span></span>|<span data-ttu-id="e48d9-252">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="e48d9-252">Root element.</span></span>|<span data-ttu-id="e48d9-253">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-253">Yes</span></span>|  
|<span data-ttu-id="e48d9-254">endereço</span><span class="sxs-lookup"><span data-stu-id="e48d9-254">address</span></span>|<span data-ttu-id="e48d9-255">Especifica um único endereço IP no qual toofilter.</span><span class="sxs-lookup"><span data-stu-id="e48d9-255">Specifies a single IP address on which toofilter.</span></span>|<span data-ttu-id="e48d9-256">Pelo menos um elemento `address` ou `address-range` é necessário.</span><span class="sxs-lookup"><span data-stu-id="e48d9-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="e48d9-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="e48d9-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="e48d9-258">Especifica um intervalo de endereços IP no qual toofilter.</span><span class="sxs-lookup"><span data-stu-id="e48d9-258">Specifies a range of IP address on which toofilter.</span></span>|<span data-ttu-id="e48d9-259">Pelo menos um elemento `address` ou `address-range` é necessário.</span><span class="sxs-lookup"><span data-stu-id="e48d9-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e48d9-260">Atributos</span><span class="sxs-lookup"><span data-stu-id="e48d9-260">Attributes</span></span>  
  
|<span data-ttu-id="e48d9-261">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-261">Name</span></span>|<span data-ttu-id="e48d9-262">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-262">Description</span></span>|<span data-ttu-id="e48d9-263">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-263">Required</span></span>|<span data-ttu-id="e48d9-264">Padrão</span><span class="sxs-lookup"><span data-stu-id="e48d9-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e48d9-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="e48d9-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="e48d9-266">Um intervalo de IP endereços tooallow ou negar acesso.</span><span class="sxs-lookup"><span data-stu-id="e48d9-266">A range of IP addresses tooallow or deny access for.</span></span>|<span data-ttu-id="e48d9-267">Necessário quando hello `address-range` elemento é usado.</span><span class="sxs-lookup"><span data-stu-id="e48d9-267">Required when hello `address-range` element is used.</span></span>|<span data-ttu-id="e48d9-268">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-268">N/A</span></span>|  
|<span data-ttu-id="e48d9-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="e48d9-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="e48d9-270">Especifica se chamadas devem ser permitidas ou não para Olá especificado intervalos e endereços IP.</span><span class="sxs-lookup"><span data-stu-id="e48d9-270">Specifies whether calls should be allowed or not for hello specified IP addresses and ranges.</span></span>|<span data-ttu-id="e48d9-271">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-271">Yes</span></span>|<span data-ttu-id="e48d9-272">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e48d9-273">Uso</span><span class="sxs-lookup"><span data-stu-id="e48d9-273">Usage</span></span>  
 <span data-ttu-id="e48d9-274">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e48d9-274">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e48d9-275">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="e48d9-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e48d9-276">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="e48d9-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e48d9-277"><a name="SetUsageQuota"></a> Definir a cota de uso por assinatura</span><span class="sxs-lookup"><span data-stu-id="e48d9-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="e48d9-278">Olá `quota` política impõe uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por assinatura.</span><span class="sxs-lookup"><span data-stu-id="e48d9-278">hello `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e48d9-279">Essa política pode ser usada apenas uma vez por cada documento de política.</span><span class="sxs-lookup"><span data-stu-id="e48d9-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="e48d9-280">[Expressões de política](api-management-policy-expressions.md) não pode ser usado em qualquer um dos atributos de política Olá para esta política.</span><span class="sxs-lookup"><span data-stu-id="e48d9-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e48d9-281">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="e48d9-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="e48d9-282">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e48d9-282">Example</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota calls="10000" bandwidth="40000" renewal-period="3600" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="e48d9-283">Elementos</span><span class="sxs-lookup"><span data-stu-id="e48d9-283">Elements</span></span>  
  
|<span data-ttu-id="e48d9-284">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-284">Name</span></span>|<span data-ttu-id="e48d9-285">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-285">Description</span></span>|<span data-ttu-id="e48d9-286">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e48d9-287">quota</span><span class="sxs-lookup"><span data-stu-id="e48d9-287">quota</span></span>|<span data-ttu-id="e48d9-288">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="e48d9-288">Root element.</span></span>|<span data-ttu-id="e48d9-289">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-289">Yes</span></span>|  
|<span data-ttu-id="e48d9-290">api</span><span class="sxs-lookup"><span data-stu-id="e48d9-290">api</span></span>|<span data-ttu-id="e48d9-291">Adicione um ou mais desses elementos tooimpose uma cota nas APIs no produto hello.</span><span class="sxs-lookup"><span data-stu-id="e48d9-291">Add one  or more of these elements tooimpose a quota on APIs within hello product.</span></span> <span data-ttu-id="e48d9-292">Cotas de API e produto são aplicadas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="e48d9-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="e48d9-293">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-293">No</span></span>|  
|<span data-ttu-id="e48d9-294">operation</span><span class="sxs-lookup"><span data-stu-id="e48d9-294">operation</span></span>|<span data-ttu-id="e48d9-295">Adicione um ou mais desses elementos tooimpose uma cota nas operações em uma API.</span><span class="sxs-lookup"><span data-stu-id="e48d9-295">Add one  or more of these elements tooimpose a quota on operations within an API.</span></span> <span data-ttu-id="e48d9-296">Cotas de operações, APIs e produtos são aplicadas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="e48d9-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="e48d9-297">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e48d9-298">Atributos</span><span class="sxs-lookup"><span data-stu-id="e48d9-298">Attributes</span></span>  
  
|<span data-ttu-id="e48d9-299">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-299">Name</span></span>|<span data-ttu-id="e48d9-300">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-300">Description</span></span>|<span data-ttu-id="e48d9-301">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-301">Required</span></span>|<span data-ttu-id="e48d9-302">Padrão</span><span class="sxs-lookup"><span data-stu-id="e48d9-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e48d9-303">name</span><span class="sxs-lookup"><span data-stu-id="e48d9-303">name</span></span>|<span data-ttu-id="e48d9-304">nome de saudação do hello API ou operação para o qual Olá cota se aplica.</span><span class="sxs-lookup"><span data-stu-id="e48d9-304">hello name of hello API or operation for which hello quota applies.</span></span>|<span data-ttu-id="e48d9-305">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-305">Yes</span></span>|<span data-ttu-id="e48d9-306">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-306">N/A</span></span>|  
|<span data-ttu-id="e48d9-307">largura de banda</span><span class="sxs-lookup"><span data-stu-id="e48d9-307">bandwidth</span></span>|<span data-ttu-id="e48d9-308">Olá número máximo total de quilobytes permitidos durante o intervalo de tempo de saudação especificado no hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e48d9-308">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e48d9-309">`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="e48d9-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e48d9-310">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-310">N/A</span></span>|  
|<span data-ttu-id="e48d9-311">chamadas</span><span class="sxs-lookup"><span data-stu-id="e48d9-311">calls</span></span>|<span data-ttu-id="e48d9-312">Olá número total máximo de chamadas permitidas durante o intervalo de tempo de saudação especificado no hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e48d9-312">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e48d9-313">`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="e48d9-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e48d9-314">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-314">N/A</span></span>|  
|<span data-ttu-id="e48d9-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="e48d9-315">renewal-period</span></span>|<span data-ttu-id="e48d9-316">saudação do período de tempo em segundos após o qual hello cota é redefinida.</span><span class="sxs-lookup"><span data-stu-id="e48d9-316">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="e48d9-317">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-317">Yes</span></span>|<span data-ttu-id="e48d9-318">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e48d9-319">Uso</span><span class="sxs-lookup"><span data-stu-id="e48d9-319">Usage</span></span>  
 <span data-ttu-id="e48d9-320">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e48d9-320">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e48d9-321">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="e48d9-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e48d9-322">**Escopos de política:** produto</span><span class="sxs-lookup"><span data-stu-id="e48d9-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="e48d9-323"><a name="SetUsageQuotaByKey"></a> Definir uma cota de uso por chave</span><span class="sxs-lookup"><span data-stu-id="e48d9-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="e48d9-324">Olá `quota-by-key` política impõe uma vida útil ou renovável chamada volume e/ou a largura de banda de cota, em uma base por chave.</span><span class="sxs-lookup"><span data-stu-id="e48d9-324">hello `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="e48d9-325">chave de saudação pode ter um valor de cadeia de caracteres arbitrária e normalmente é fornecido usando uma expressão de política.</span><span class="sxs-lookup"><span data-stu-id="e48d9-325">hello key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="e48d9-326">Condição de incremento opcional pode ser adicionada toospecify as solicitações que devem ser contadas em direção a cota de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-326">Optional increment condition can be added toospecify which requests should be counted towards hello quota.</span></span>  
  
 <span data-ttu-id="e48d9-327">Para obter mais informações e exemplos dessa política, consulte [Limitação de solicitação avançada com o Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="e48d9-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e48d9-328">Essa política pode ser usada apenas uma vez por cada documento de política.</span><span class="sxs-lookup"><span data-stu-id="e48d9-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="e48d9-329">[Expressões de política](api-management-policy-expressions.md) não pode ser usado em qualquer um dos atributos de política Olá para esta política.</span><span class="sxs-lookup"><span data-stu-id="e48d9-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of hello policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e48d9-330">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="e48d9-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="e48d9-331">Exemplo</span><span class="sxs-lookup"><span data-stu-id="e48d9-331">Example</span></span>  
 <span data-ttu-id="e48d9-332">Em Olá exemplo a seguir, cota Olá é inserida pelo endereço IP do chamador hello.</span><span class="sxs-lookup"><span data-stu-id="e48d9-332">In hello following example, hello quota is keyed by hello caller IP address.</span></span>  
  
```xml  
<policies>  
    <inbound>  
        <base />  
        <quota-by-key calls="10000" bandwidth="40000" renewal-period="3600"  
                      increment-condition="@(context.Response.StatusCode >= 200 && context.Response.StatusCode < 400)"  
                      counter-key="@(context.Request.IpAddress)" />  
    </inbound>  
    <outbound>  
        <base />  
    </outbound>  
</policies>  
```  
  
### <a name="elements"></a><span data-ttu-id="e48d9-333">Elementos</span><span class="sxs-lookup"><span data-stu-id="e48d9-333">Elements</span></span>  
  
|<span data-ttu-id="e48d9-334">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-334">Name</span></span>|<span data-ttu-id="e48d9-335">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-335">Description</span></span>|<span data-ttu-id="e48d9-336">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="e48d9-337">quota</span><span class="sxs-lookup"><span data-stu-id="e48d9-337">quota</span></span>|<span data-ttu-id="e48d9-338">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="e48d9-338">Root element.</span></span>|<span data-ttu-id="e48d9-339">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e48d9-340">Atributos</span><span class="sxs-lookup"><span data-stu-id="e48d9-340">Attributes</span></span>  
  
|<span data-ttu-id="e48d9-341">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-341">Name</span></span>|<span data-ttu-id="e48d9-342">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-342">Description</span></span>|<span data-ttu-id="e48d9-343">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-343">Required</span></span>|<span data-ttu-id="e48d9-344">Padrão</span><span class="sxs-lookup"><span data-stu-id="e48d9-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e48d9-345">largura de banda</span><span class="sxs-lookup"><span data-stu-id="e48d9-345">bandwidth</span></span>|<span data-ttu-id="e48d9-346">Olá número máximo total de quilobytes permitidos durante o intervalo de tempo de saudação especificado no hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e48d9-346">hello maximum total number of kilobytes allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e48d9-347">`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="e48d9-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e48d9-348">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-348">N/A</span></span>|  
|<span data-ttu-id="e48d9-349">chamadas</span><span class="sxs-lookup"><span data-stu-id="e48d9-349">calls</span></span>|<span data-ttu-id="e48d9-350">Olá número total máximo de chamadas permitidas durante o intervalo de tempo de saudação especificado no hello `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="e48d9-350">hello maximum total number of calls allowed during hello time interval specified in hello `renewal-period`.</span></span>|<span data-ttu-id="e48d9-351">`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="e48d9-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="e48d9-352">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-352">N/A</span></span>|  
|<span data-ttu-id="e48d9-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="e48d9-353">counter-key</span></span>|<span data-ttu-id="e48d9-354">Olá toouse chave para a política de cota de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-354">hello key toouse for hello quota policy.</span></span>|<span data-ttu-id="e48d9-355">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-355">Yes</span></span>|<span data-ttu-id="e48d9-356">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-356">N/A</span></span>|  
|<span data-ttu-id="e48d9-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="e48d9-357">increment-condition</span></span>|<span data-ttu-id="e48d9-358">expressão booleana Hello, especificando se a solicitação Olá deve ser contabilizada em direção a cota de saudação (`true`)</span><span class="sxs-lookup"><span data-stu-id="e48d9-358">hello boolean expression specifying if hello request should be counted towards hello quota (`true`)</span></span>|<span data-ttu-id="e48d9-359">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-359">No</span></span>|<span data-ttu-id="e48d9-360">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-360">N/A</span></span>|  
|<span data-ttu-id="e48d9-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="e48d9-361">renewal-period</span></span>|<span data-ttu-id="e48d9-362">saudação do período de tempo em segundos após o qual hello cota é redefinida.</span><span class="sxs-lookup"><span data-stu-id="e48d9-362">hello time period in seconds after which hello quota resets.</span></span>|<span data-ttu-id="e48d9-363">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-363">Yes</span></span>|<span data-ttu-id="e48d9-364">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e48d9-365">Uso</span><span class="sxs-lookup"><span data-stu-id="e48d9-365">Usage</span></span>  
 <span data-ttu-id="e48d9-366">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e48d9-366">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e48d9-367">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="e48d9-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e48d9-368">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="e48d9-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="e48d9-369"><a name="ValidateJWT"></a> Validar JWT</span><span class="sxs-lookup"><span data-stu-id="e48d9-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="e48d9-370">Olá `validate-jwt` política impõe a existência e a validade de um JWT extraído de um determinado cabeçalho HTTP ou um parâmetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="e48d9-370">hello `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="e48d9-371">Olá `validate-jwt` política requer que Olá `exp` declaração registrada é incluído (s) no token JWT hello, a menos que `require-expiration-time` atributo for especificado e definido muito`false`.</span><span class="sxs-lookup"><span data-stu-id="e48d9-371">hello `validate-jwt` policy requires that hello `exp` registered claim is inlcuded in hello JWT token, unless `require-expiration-time` attribute is specified and set too`false`.</span></span>  
> <span data-ttu-id="e48d9-372">Olá `validate-jwt` diretiva dá suporte a algoritmos de assinatura HS256 e RS256.</span><span class="sxs-lookup"><span data-stu-id="e48d9-372">hello `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="e48d9-373">Para HS256 chave Olá deve ser fornecido embutido na política de saudação no formulário do hello codificado na base64.</span><span class="sxs-lookup"><span data-stu-id="e48d9-373">For HS256 hello key must be provided inline within hello policy in hello base64 encoded form.</span></span> <span data-ttu-id="e48d9-374">RS256 chave Olá tem toobe fornecer por meio de um ponto de extremidade de configuração do Open ID.</span><span class="sxs-lookup"><span data-stu-id="e48d9-374">For RS256 hello key has toobe provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="e48d9-375">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="e48d9-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing hello token (use query-parameter-name attribute if hello token is passed in hello URL)"   
    failed-validation-httpcode="http status code tooreturn on failure"   
    failed-validation-error-message="error message tooreturn on failure"   
    require-expiration-time="true|false"
    require-scheme="scheme"
    require-signed-tokens="true|false"   
    clock-skew="allowed clock skew in seconds">  
  <issuer-signing-keys>  
    <key>base64 encoded signing key</key>  
    <!-- if there are multiple keys, then add additional key elements -->  
  </issuer-signing-keys>  
  <audiences>  
    <audience>audience string</audience>  
    <!-- if there are multiple possible audiences, then add additional audience elements -->  
  </audiences>  
  <issuers>  
    <issuer>issuer string</issuer>  
    <!-- if there are multiple possible issuers, then add additional issuer elements -->  
  </issuers>  
  <required-claims>  
    <claim name="name of hello claim as it appears in hello token" match="all|any">  
      <value>claim value as it is expected tooappear in hello token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of hello configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="e48d9-376">Exemplos</span><span class="sxs-lookup"><span data-stu-id="e48d9-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="e48d9-377">Validação de token de Serviços Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="e48d9-377">Azure Mobile Services token validation</span></span>  
  
```xml  
<validate-jwt header-name="x-zumo-auth" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Supplied access token is invalid.">  
    <issuers>  
        <issuer>urn:microsoft:windows-azure:zumo</issuer>  
    </issuers>  
    <audiences>  
        <audience>Facebook</audience>  
    </audiences>  
    <issuer-signing-keys>  
        <zumo-master-key id="0">insert key here</zumo-master-key>  
    </issuer-signing-keys>  
</validate-jwt>  
```  
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="e48d9-378">Validação de token do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="e48d9-378">Azure Active Directory token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/contoso.onmicrosoft.com/.well-known/openid-configuration" />  
    <audiences>
        <audience>25eef6e4-c905-4a07-8eb4-0d08d5df8b3f</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="e48d9-379">Validação de token do Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="e48d9-379">Azure Active Directory B2C token validation</span></span>  
  
```xml  
<validate-jwt header-name="Authorization" failed-validation-httpcode="401" failed-validation-error-message="Unauthorized. Access token is missing or invalid.">  
    <openid-config url="https://login.microsoftonline.com/tfp/contoso.onmicrosoft.com/b2c_1_signin/v2.0/.well-known/openid-configuration" />
    <audiences>
        <audience>d313c4e4-de5f-4197-9470-e509a2f0b806</audience>
    </audiences>
    <required-claims>  
        <claim name="id" match="all">  
            <value>insert claim here</value>  
        </claim>  
    </required-claims>  
</validate-jwt>  
```  
  
#### <a name="authorize-access-toooperations-based-on-token-claims"></a><span data-ttu-id="e48d9-380">Autorizar toooperations de acesso baseado em declarações de token</span><span class="sxs-lookup"><span data-stu-id="e48d9-380">Authorize access toooperations based on token claims</span></span>  
 <span data-ttu-id="e48d9-381">Este exemplo mostra como Olá toouse [validar JWT](api-management-access-restriction-policies.md#ValidateJWT) política toopre-autorizar toooperations de acesso baseado em declarações de token.</span><span class="sxs-lookup"><span data-stu-id="e48d9-381">This example shows how toouse hello [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy toopre-authorize access toooperations based on token claims.</span></span> <span data-ttu-id="e48d9-382">Para ver uma demonstração de como configurar e usar essa política, consulte [nuvem abrangem episódio 177: mais recursos de gerenciamento de API com Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) e Avançar too13:50.</span><span class="sxs-lookup"><span data-stu-id="e48d9-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward too13:50.</span></span> <span data-ttu-id="e48d9-383">Avanço too15:00 toosee políticas de saudação configuradas no editor de diretiva de saudação e, em seguida, too18:50 para ver uma demonstração de como chamar uma operação do portal do desenvolvedor do hello com e sem Olá necessário token de autorização.</span><span class="sxs-lookup"><span data-stu-id="e48d9-383">Fast forward too15:00 toosee hello policies configured in hello policy editor and then too18:50 for a demonstration of calling an operation from hello developer portal both with and without hello required authorization token.</span></span>  
  
```xml  
<!-- Copy hello following snippet into hello inbound section at hello api (or higher) level toopre-authorize access toooperations based on token claims -->  
<set-variable name="signingKey" value="insert signing key here" />  
<choose>  
  <when condition="@(context.Request.Method.Equals("patch",StringComparison.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="edit">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <when condition="@(new [] {"post", "put"}.Contains(context.Request.Method,StringComparer.OrdinalIgnoreCase))">  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
      <required-claims>  
        <claim name="create">  
          <value>true</value>  
        </claim>  
      </required-claims>  
    </validate-jwt>  
  </when>  
  <otherwise>  
    <validate-jwt header-name="Authorization">  
      <issuer-signing-keys>  
        <key>@((string)context.Variables["signingKey"])</key>  
      </issuer-signing-keys>  
    </validate-jwt>  
  </otherwise>  
</choose>  
```  
  
### <a name="elements"></a><span data-ttu-id="e48d9-384">Elementos</span><span class="sxs-lookup"><span data-stu-id="e48d9-384">Elements</span></span>  
  
|<span data-ttu-id="e48d9-385">Elemento</span><span class="sxs-lookup"><span data-stu-id="e48d9-385">Element</span></span>|<span data-ttu-id="e48d9-386">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-386">Description</span></span>|<span data-ttu-id="e48d9-387">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="e48d9-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="e48d9-388">validate-jwt</span></span>|<span data-ttu-id="e48d9-389">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="e48d9-389">Root element.</span></span>|<span data-ttu-id="e48d9-390">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-390">Yes</span></span>|  
|<span data-ttu-id="e48d9-391">públicos-alvo</span><span class="sxs-lookup"><span data-stu-id="e48d9-391">audiences</span></span>|<span data-ttu-id="e48d9-392">Contém uma lista de declarações de público aceitáveis que podem estar presentes no token de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-392">Contains a list of acceptable audience claims that can be present on hello token.</span></span> <span data-ttu-id="e48d9-393">Se vários valores de público-alvo estiverem presentes, cada valor será tentado até que todos sejam esgotados (nesse caso, a validação falhará) ou até obter êxito.</span><span class="sxs-lookup"><span data-stu-id="e48d9-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="e48d9-394">Pelo menos um público-alvo deve ser especificado.</span><span class="sxs-lookup"><span data-stu-id="e48d9-394">At least one audience must be specified.</span></span>|<span data-ttu-id="e48d9-395">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-395">No</span></span>|  
|<span data-ttu-id="e48d9-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="e48d9-396">issuer-signing-keys</span></span>|<span data-ttu-id="e48d9-397">Uma lista de segurança codificada em Base64 chaves usadas toovalidate assinado tokens.</span><span class="sxs-lookup"><span data-stu-id="e48d9-397">A list of Base64-encoded security keys used toovalidate signed tokens.</span></span> <span data-ttu-id="e48d9-398">Se várias chaves de segurança estiverem presentes, cada chave será tentada até que todas sejam esgotadas (nesse caso, a validação falhará) ou até obter êxito (útil para substituição de token).</span><span class="sxs-lookup"><span data-stu-id="e48d9-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="e48d9-399">Elementos chave têm um recurso opcional `id` toomatch atributo usado contra `kid` de declaração.</span><span class="sxs-lookup"><span data-stu-id="e48d9-399">Key elements have an optional `id` attribute used toomatch against `kid` claim.</span></span>|<span data-ttu-id="e48d9-400">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-400">No</span></span>|  
|<span data-ttu-id="e48d9-401">emissores</span><span class="sxs-lookup"><span data-stu-id="e48d9-401">issuers</span></span>|<span data-ttu-id="e48d9-402">Uma lista de entidades aceitáveis que emitiu o token de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-402">A list of acceptable principals that issued hello token.</span></span> <span data-ttu-id="e48d9-403">Se vários valores de emissor estiverem presentes, cada valor será tentado até que todos sejam esgotados (nesse caso, a validação falhará) ou até obter êxito.</span><span class="sxs-lookup"><span data-stu-id="e48d9-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="e48d9-404">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-404">No</span></span>|  
|<span data-ttu-id="e48d9-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="e48d9-405">openid-config</span></span>|<span data-ttu-id="e48d9-406">elemento de saudação usado para especificar um compatível com Open ID configuração ponto de extremidade do qual as chaves e o emissor de assinatura pode ser obtido.</span><span class="sxs-lookup"><span data-stu-id="e48d9-406">hello element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="e48d9-407">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-407">No</span></span>|  
|<span data-ttu-id="e48d9-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="e48d9-408">required-claims</span></span>|<span data-ttu-id="e48d9-409">Contém uma lista de declarações esperadas toobe presente no token Olá para ele toobe considerado válido.</span><span class="sxs-lookup"><span data-stu-id="e48d9-409">Contains a list of claims expected toobe present on hello token for it toobe considered valid.</span></span> <span data-ttu-id="e48d9-410">Olá quando `match` atributo está definido muito`all` cada valor de declaração na diretiva Olá deve estar presente no token Olá para toosucceed de validação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-410">When hello `match` attribute is set too`all` every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="e48d9-411">Olá quando `match` atributo está definido muito`any` pelo menos uma declaração deve estar presente no token Olá para toosucceed de validação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-411">When hello `match` attribute is set too`any` at least one claim must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="e48d9-412">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-412">No</span></span>|  
|<span data-ttu-id="e48d9-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="e48d9-413">zumo-master-key</span></span>|<span data-ttu-id="e48d9-414">Chave mestra para tokens emitidos pelos Serviços Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="e48d9-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="e48d9-415">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="e48d9-416">Atributos</span><span class="sxs-lookup"><span data-stu-id="e48d9-416">Attributes</span></span>  
  
|<span data-ttu-id="e48d9-417">Nome</span><span class="sxs-lookup"><span data-stu-id="e48d9-417">Name</span></span>|<span data-ttu-id="e48d9-418">Descrição</span><span class="sxs-lookup"><span data-stu-id="e48d9-418">Description</span></span>|<span data-ttu-id="e48d9-419">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="e48d9-419">Required</span></span>|<span data-ttu-id="e48d9-420">Padrão</span><span class="sxs-lookup"><span data-stu-id="e48d9-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="e48d9-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="e48d9-421">clock-skew</span></span>|<span data-ttu-id="e48d9-422">Período de tempo.</span><span class="sxs-lookup"><span data-stu-id="e48d9-422">Timespan.</span></span> <span data-ttu-id="e48d9-423">Fornece alguma reserva pequena no caso de declaração de expiração do token hello está presente no token hello e passou Olá atual data / hora.</span><span class="sxs-lookup"><span data-stu-id="e48d9-423">Provides some small leeway in case hello token's expiration claim is present in hello token and is past hello current date / time.</span></span>|<span data-ttu-id="e48d9-424">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-424">No</span></span>|<span data-ttu-id="e48d9-425">0 segundos</span><span class="sxs-lookup"><span data-stu-id="e48d9-425">0 seconds</span></span>|  
|<span data-ttu-id="e48d9-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="e48d9-426">failed-validation-error-message</span></span>|<span data-ttu-id="e48d9-427">Tooreturn de mensagem de erro no corpo de resposta HTTP de saudação se Olá JWT não passar na validação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-427">Error message tooreturn in hello HTTP response body if hello JWT does not pass validation.</span></span> <span data-ttu-id="e48d9-428">Esta mensagem deve conter quaisquer caracteres especiais adequadamente seguidos por caracteres de escape.</span><span class="sxs-lookup"><span data-stu-id="e48d9-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="e48d9-429">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-429">No</span></span>|<span data-ttu-id="e48d9-430">A mensagem de erro padrão depende do problema de validação, por exemplo, "O JWT não está presente."</span><span class="sxs-lookup"><span data-stu-id="e48d9-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="e48d9-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="e48d9-431">failed-validation-httpcode</span></span>|<span data-ttu-id="e48d9-432">Tooreturn do código de HTTP Status se Olá JWT não passa na validação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-432">HTTP Status code tooreturn if hello JWT doesn't pass validation.</span></span>|<span data-ttu-id="e48d9-433">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-433">No</span></span>|<span data-ttu-id="e48d9-434">401</span><span class="sxs-lookup"><span data-stu-id="e48d9-434">401</span></span>|  
|<span data-ttu-id="e48d9-435">header-name</span><span class="sxs-lookup"><span data-stu-id="e48d9-435">header-name</span></span>|<span data-ttu-id="e48d9-436">nome de saudação do cabeçalho de saudação HTTP contém Olá token.</span><span class="sxs-lookup"><span data-stu-id="e48d9-436">hello name of hello HTTP header holding hello token.</span></span>|<span data-ttu-id="e48d9-437">`header-name` ou `query-paremeter-name` deve ser especificado; mas não ambos.</span><span class="sxs-lookup"><span data-stu-id="e48d9-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="e48d9-438">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-438">N/A</span></span>|  
|<span data-ttu-id="e48d9-439">ID</span><span class="sxs-lookup"><span data-stu-id="e48d9-439">id</span></span>|<span data-ttu-id="e48d9-440">Olá `id` atributo Olá `key` elemento permite toospecify Olá cadeia de caracteres será comparada à `kid` toofind de token (se houver) Olá out Olá toouse de chave apropriado para a validação de assinatura de declaração.</span><span class="sxs-lookup"><span data-stu-id="e48d9-440">hello `id` attribute on hello `key` element allows you toospecify hello string that will be matched against `kid` claim in hello token (if present) toofind out hello appropriate key toouse for signature validation.</span></span>|<span data-ttu-id="e48d9-441">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-441">No</span></span>|<span data-ttu-id="e48d9-442">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-442">N/A</span></span>|  
|<span data-ttu-id="e48d9-443">match</span><span class="sxs-lookup"><span data-stu-id="e48d9-443">match</span></span>|<span data-ttu-id="e48d9-444">Olá `match` atributo Olá `claim` elemento Especifica se cada valor de declaração na diretiva Olá deve estar presente no token Olá para toosucceed de validação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-444">hello `match` attribute on hello `claim` element specifies whether every claim value in hello policy must be present in hello token for validation toosucceed.</span></span> <span data-ttu-id="e48d9-445">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="e48d9-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="e48d9-446">-                          `all`-cada valor de declaração na diretiva Olá deve estar presente no token Olá para toosucceed de validação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-446">-                          `all` - every claim value in hello policy must be present in hello token for validation toosucceed.</span></span><br /><br /> <span data-ttu-id="e48d9-447">-                          `any`-pelo menos uma declaração de valor deve estar presente no token Olá para toosucceed de validação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-447">-                          `any` - at least one claim value must be present in hello token for validation toosucceed.</span></span>|<span data-ttu-id="e48d9-448">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-448">No</span></span>|<span data-ttu-id="e48d9-449">tudo</span><span class="sxs-lookup"><span data-stu-id="e48d9-449">all</span></span>|  
|<span data-ttu-id="e48d9-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="e48d9-450">query-paremeter-name</span></span>|<span data-ttu-id="e48d9-451">nome de Olá Olá Olá do parâmetro de consulta contém o token de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-451">hello name of hello hello query parameter holding hello token.</span></span>|<span data-ttu-id="e48d9-452">`header-name` ou `query-paremeter-name` deve ser especificado; mas não ambos.</span><span class="sxs-lookup"><span data-stu-id="e48d9-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="e48d9-453">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-453">N/A</span></span>|  
|<span data-ttu-id="e48d9-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="e48d9-454">require-expiration-time</span></span>|<span data-ttu-id="e48d9-455">Booliano.</span><span class="sxs-lookup"><span data-stu-id="e48d9-455">Boolean.</span></span> <span data-ttu-id="e48d9-456">Especifica se uma declaração de expiração é necessária no token de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-456">Specifies whether an expiration claim is required in hello token.</span></span>|<span data-ttu-id="e48d9-457">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-457">No</span></span>|<span data-ttu-id="e48d9-458">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="e48d9-458">true</span></span>|
|<span data-ttu-id="e48d9-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="e48d9-459">require-scheme</span></span>|<span data-ttu-id="e48d9-460">Olá, por exemplo, o nome do esquema de token Olá, "Portador".</span><span class="sxs-lookup"><span data-stu-id="e48d9-460">hello name of hello token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="e48d9-461">Quando esse atributo é definido, política de saudação garantirá que especificado o esquema está presente no valor do cabeçalho de autorização de saudação.</span><span class="sxs-lookup"><span data-stu-id="e48d9-461">When this attribute is set, hello policy will ensure that specified scheme is present in hello Authorization header value.</span></span>|<span data-ttu-id="e48d9-462">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-462">No</span></span>|<span data-ttu-id="e48d9-463">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-463">N/A</span></span>|
|<span data-ttu-id="e48d9-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="e48d9-464">require-signed-tokens</span></span>|<span data-ttu-id="e48d9-465">Booliano.</span><span class="sxs-lookup"><span data-stu-id="e48d9-465">Boolean.</span></span> <span data-ttu-id="e48d9-466">Especifica se um token é necessário toobe assinado.</span><span class="sxs-lookup"><span data-stu-id="e48d9-466">Specifies whether a token is required toobe signed.</span></span>|<span data-ttu-id="e48d9-467">Não</span><span class="sxs-lookup"><span data-stu-id="e48d9-467">No</span></span>|<span data-ttu-id="e48d9-468">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="e48d9-468">true</span></span>|  
|<span data-ttu-id="e48d9-469">url</span><span class="sxs-lookup"><span data-stu-id="e48d9-469">url</span></span>|<span data-ttu-id="e48d9-470">URL ponto de extremidade de configuração de Open ID da qual é possível obter os metadados de configuração de Open ID.</span><span class="sxs-lookup"><span data-stu-id="e48d9-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="e48d9-471">Active Directory do Azure use Olá URL a seguir: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituindo o nome do locatário de diretório, por exemplo, `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="e48d9-471">For Azure Active Directory use hello following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="e48d9-472">Sim</span><span class="sxs-lookup"><span data-stu-id="e48d9-472">Yes</span></span>|<span data-ttu-id="e48d9-473">N/D</span><span class="sxs-lookup"><span data-stu-id="e48d9-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="e48d9-474">Uso</span><span class="sxs-lookup"><span data-stu-id="e48d9-474">Usage</span></span>  
 <span data-ttu-id="e48d9-475">Essa política pode ser usada em Olá após diretiva [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span><span class="sxs-lookup"><span data-stu-id="e48d9-475">This policy can be used in hello following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="e48d9-476">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="e48d9-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="e48d9-477">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="e48d9-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="e48d9-478">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="e48d9-478">Next steps</span></span>
<span data-ttu-id="e48d9-479">Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="e48d9-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
