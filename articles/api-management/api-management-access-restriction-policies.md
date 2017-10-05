---
title: "Políticas de restrição de acesso do Gerenciamento de API do Azure | Microsoft Docs"
description: "Saiba mais sobre as políticas de restrição de acesso disponíveis para uso no Gerenciamento de API do Azure."
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
ms.openlocfilehash: 4c9991baf3fbcf3b8ea01f8dd573e2336db88b68
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="api-management-access-restriction-policies"></a><span data-ttu-id="6ed10-103">Políticas de restrição de acesso do Gerenciamento de API</span><span class="sxs-lookup"><span data-stu-id="6ed10-103">API Management access restriction policies</span></span>
<span data-ttu-id="6ed10-104">Este tópico fornece uma referência para as políticas de Gerenciamento de API a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ed10-104">This topic provides a reference for the following API Management policies.</span></span> <span data-ttu-id="6ed10-105">Para obter mais informações sobre como adicionar e configurar políticas, consulte [Políticas de Gerenciamento de API](http://go.microsoft.com/fwlink/?LinkID=398186).</span><span class="sxs-lookup"><span data-stu-id="6ed10-105">For information on adding and configuring policies, see [Policies in API Management](http://go.microsoft.com/fwlink/?LinkID=398186).</span></span>  
  
##  <span data-ttu-id="6ed10-106"><a name="AccessRestrictionPolicies"></a> Políticas de restrição de acesso</span><span class="sxs-lookup"><span data-stu-id="6ed10-106"><a name="AccessRestrictionPolicies"></a> Access restriction policies</span></span>  
  
-   <span data-ttu-id="6ed10-107">[Verificar cabeçalho HTTP](api-management-access-restriction-policies.md#CheckHTTPHeader) - Impõe a existência e/ou valor de um cabeçalho HTTP.</span><span class="sxs-lookup"><span data-stu-id="6ed10-107">[Check HTTP header](api-management-access-restriction-policies.md#CheckHTTPHeader) - Enforces existence and/or value of a HTTP Header.</span></span>  
  
-   <span data-ttu-id="6ed10-108">[Limitar a taxa de chamada por assinatura](api-management-access-restriction-policies.md#LimitCallRate) - Previne picos de uso da API limitando a taxa de chamada, baseado em assinatura.</span><span class="sxs-lookup"><span data-stu-id="6ed10-108">[Limit call rate by subscription](api-management-access-restriction-policies.md#LimitCallRate) - Prevents API usage spikes by limiting call rate, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="6ed10-109">[Limitar a taxa de chamada por chave](#LimitCallRateByKey) - Previne picos de uso da API limitando a taxa de chamada, baseado em chave.</span><span class="sxs-lookup"><span data-stu-id="6ed10-109">[Limit call rate by key](#LimitCallRateByKey) - Prevents API usage spikes by limiting call rate, on a per key basis.</span></span>  
  
-   <span data-ttu-id="6ed10-110">[Restringir IP do autor da chamada](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filtra (permite/recusa) chamadas de endereços IP específicos e/ou intervalos de endereços.</span><span class="sxs-lookup"><span data-stu-id="6ed10-110">[Restrict caller IPs](api-management-access-restriction-policies.md#RestrictCallerIPs) - Filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
-   <span data-ttu-id="6ed10-111">[Definir a cota de uso por assinatura](api-management-access-restriction-policies.md#SetUsageQuota) - Permite que você aplique uma cota renovável ou permanente de volume de chamada e/ou largura de banda, baseado em assinatura.</span><span class="sxs-lookup"><span data-stu-id="6ed10-111">[Set usage quota by subscription](api-management-access-restriction-policies.md#SetUsageQuota) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
-   <span data-ttu-id="6ed10-112">[Definir a cota de uso por chave](#SetUsageQuotaByKey) - Permite que você aplique uma cota renovável ou permanente de volume de chamada e/ou largura de banda, baseado em chave.</span><span class="sxs-lookup"><span data-stu-id="6ed10-112">[Set usage quota by key](#SetUsageQuotaByKey) - Allows you to enforce a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span>  
  
-   <span data-ttu-id="6ed10-113">[Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) - Impõe a existência e a validade de JWT extraída de um cabeçalho HTTP especificado ou um parâmetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="6ed10-113">[Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) - Enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
##  <span data-ttu-id="6ed10-114"><a name="CheckHTTPHeader"></a> Verificar cabeçalho HTTP</span><span class="sxs-lookup"><span data-stu-id="6ed10-114"><a name="CheckHTTPHeader"></a> Check HTTP header</span></span>  
 <span data-ttu-id="6ed10-115">Use a política `check-header` para impor que uma solicitação tem um cabeçalho HTTP especificado.</span><span class="sxs-lookup"><span data-stu-id="6ed10-115">Use the `check-header` policy to enforce that a request has a specified HTTP header.</span></span> <span data-ttu-id="6ed10-116">Você pode, opcionalmente, verificar se o cabeçalho tem um valor específico ou procurar um intervalo de valores permitidos.</span><span class="sxs-lookup"><span data-stu-id="6ed10-116">You can optionally check to see if the header has a specific value or check for a range of allowed values.</span></span> <span data-ttu-id="6ed10-117">Se a verificação falhar, a política encerrará o processamento da solicitação e retornará a mensagem de erro e código de status HTTP especificada pela política.</span><span class="sxs-lookup"><span data-stu-id="6ed10-117">If the check fails, the policy terminates request processing and returns the HTTP status code and error message specified by the policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6ed10-118">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="6ed10-118">Policy statement</span></span>  
  
```xml  
<check-header name="header name" failed-check-httpcode="code" failed-check-error-message="message" ignore-case="True">  
    <value>Value1</value>  
    <value>Value2</value>  
</check-header>  
```  
  
### <a name="example"></a><span data-ttu-id="6ed10-119">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6ed10-119">Example</span></span>  
  
```xml  
<check-header name="Authorization" failed-check-httpcode="401" failed-check-error-message="Not authorized" ignore-case="false">  
    <value>f6dc69a089844cf6b2019bae6d36fac8</value>  
</check-header>  
```  
  
### <a name="elements"></a><span data-ttu-id="6ed10-120">Elementos</span><span class="sxs-lookup"><span data-stu-id="6ed10-120">Elements</span></span>  
  
|<span data-ttu-id="6ed10-121">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-121">Name</span></span>|<span data-ttu-id="6ed10-122">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-122">Description</span></span>|<span data-ttu-id="6ed10-123">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-123">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="6ed10-124">check-header</span><span class="sxs-lookup"><span data-stu-id="6ed10-124">check-header</span></span>|<span data-ttu-id="6ed10-125">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="6ed10-125">Root element.</span></span>|<span data-ttu-id="6ed10-126">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-126">Yes</span></span>|  
|<span data-ttu-id="6ed10-127">valor</span><span class="sxs-lookup"><span data-stu-id="6ed10-127">value</span></span>|<span data-ttu-id="6ed10-128">Valor do cabeçalho HTTP permitido.</span><span class="sxs-lookup"><span data-stu-id="6ed10-128">Allowed HTTP header value.</span></span> <span data-ttu-id="6ed10-129">Quando vários elementos de valor são especificados, a verificação é considerada um sucesso se qualquer um dos valores é uma correspondência.</span><span class="sxs-lookup"><span data-stu-id="6ed10-129">When multiple value elements are specified, the check is considered a success if any one of the values is a match.</span></span>|<span data-ttu-id="6ed10-130">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-130">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="6ed10-131">Atributos</span><span class="sxs-lookup"><span data-stu-id="6ed10-131">Attributes</span></span>  
  
|<span data-ttu-id="6ed10-132">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-132">Name</span></span>|<span data-ttu-id="6ed10-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-133">Description</span></span>|<span data-ttu-id="6ed10-134">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-134">Required</span></span>|<span data-ttu-id="6ed10-135">Padrão</span><span class="sxs-lookup"><span data-stu-id="6ed10-135">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6ed10-136">failed-check-error-message</span><span class="sxs-lookup"><span data-stu-id="6ed10-136">failed-check-error-message</span></span>|<span data-ttu-id="6ed10-137">A mensagem de erro para retornar no corpo da resposta HTTP se o cabeçalho não existe ou tem um valor inválido.</span><span class="sxs-lookup"><span data-stu-id="6ed10-137">Error message to return in the HTTP response body if the header doesn't exist or has an invalid value.</span></span> <span data-ttu-id="6ed10-138">Esta mensagem deve conter quaisquer caracteres especiais adequadamente seguidos por caracteres de escape.</span><span class="sxs-lookup"><span data-stu-id="6ed10-138">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="6ed10-139">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-139">Yes</span></span>|<span data-ttu-id="6ed10-140">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-140">N/A</span></span>|  
|<span data-ttu-id="6ed10-141">failed-check-httpcode</span><span class="sxs-lookup"><span data-stu-id="6ed10-141">failed-check-httpcode</span></span>|<span data-ttu-id="6ed10-142">O código de status HTTP para retornar se o cabeçalho não existir ou tiver um valor inválido.</span><span class="sxs-lookup"><span data-stu-id="6ed10-142">HTTP Status code to return if the header doesn't exist or has an invalid value.</span></span>|<span data-ttu-id="6ed10-143">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-143">Yes</span></span>|<span data-ttu-id="6ed10-144">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-144">N/A</span></span>|  
|<span data-ttu-id="6ed10-145">header-name</span><span class="sxs-lookup"><span data-stu-id="6ed10-145">header-name</span></span>|<span data-ttu-id="6ed10-146">O nome do cabeçalho HTTP para verificar.</span><span class="sxs-lookup"><span data-stu-id="6ed10-146">The name of the HTTP Header to check.</span></span>|<span data-ttu-id="6ed10-147">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-147">Yes</span></span>|<span data-ttu-id="6ed10-148">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-148">N/A</span></span>|  
|<span data-ttu-id="6ed10-149">ignore-case</span><span class="sxs-lookup"><span data-stu-id="6ed10-149">ignore-case</span></span>|<span data-ttu-id="6ed10-150">Pode ser definido como True ou False.</span><span class="sxs-lookup"><span data-stu-id="6ed10-150">Can be set to True or False.</span></span> <span data-ttu-id="6ed10-151">Se definido como True, maiúsculas e minúsculas são ignoradas quando o valor do cabeçalho é comparado com o conjunto de valores aceitáveis.</span><span class="sxs-lookup"><span data-stu-id="6ed10-151">If set to True case is ignored when the header value is compared against the set of acceptable values.</span></span>|<span data-ttu-id="6ed10-152">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-152">Yes</span></span>|<span data-ttu-id="6ed10-153">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-153">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6ed10-154">Uso</span><span class="sxs-lookup"><span data-stu-id="6ed10-154">Usage</span></span>  
 <span data-ttu-id="6ed10-155">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ed10-155">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6ed10-156">**Seções de política:** de entrada, de saída</span><span class="sxs-lookup"><span data-stu-id="6ed10-156">**Policy sections:** inbound, outbound</span></span>  
  
-   <span data-ttu-id="6ed10-157">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="6ed10-157">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="6ed10-158"><a name="LimitCallRate"></a> Limitar a taxa de chamadas por assinatura</span><span class="sxs-lookup"><span data-stu-id="6ed10-158"><a name="LimitCallRate"></a> Limit call rate by subscription</span></span>  
 <span data-ttu-id="6ed10-159">A política `rate-limit` impede picos de uso da API para cada assinatura, limitando a taxa de chamadas para um número especificado por um período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="6ed10-159">The `rate-limit` policy prevents API usage spikes on a per subscription basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="6ed10-160">Quando essa política é disparada, o chamador recebe um código de status de resposta `429 Too Many Requests`.</span><span class="sxs-lookup"><span data-stu-id="6ed10-160">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="6ed10-161">Essa política pode ser usada apenas uma vez por cada documento de política.</span><span class="sxs-lookup"><span data-stu-id="6ed10-161">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="6ed10-162">As [expressões de política](api-management-policy-expressions.md) não podem ser usadas em nenhum dos atributos de política para essa política.</span><span class="sxs-lookup"><span data-stu-id="6ed10-162">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6ed10-163">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="6ed10-163">Policy statement</span></span>  
  
```xml  
<rate-limit calls="number" renewal-period="seconds">  
    <api name="name" calls="number" renewal-period="seconds">  
        <operation name="name" calls="number" renewal-period="seconds" />  
    </api>  
</rate-limit>  
```  
  
### <a name="example"></a><span data-ttu-id="6ed10-164">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6ed10-164">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="6ed10-165">Elementos</span><span class="sxs-lookup"><span data-stu-id="6ed10-165">Elements</span></span>  
  
|<span data-ttu-id="6ed10-166">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-166">Name</span></span>|<span data-ttu-id="6ed10-167">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-167">Description</span></span>|<span data-ttu-id="6ed10-168">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-168">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="6ed10-169">set-limit</span><span class="sxs-lookup"><span data-stu-id="6ed10-169">set-limit</span></span>|<span data-ttu-id="6ed10-170">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="6ed10-170">Root element.</span></span>|<span data-ttu-id="6ed10-171">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-171">Yes</span></span>|  
|<span data-ttu-id="6ed10-172">api</span><span class="sxs-lookup"><span data-stu-id="6ed10-172">api</span></span>|<span data-ttu-id="6ed10-173">Adicione um ou mais desses elementos para impor um limite de taxa de chamadas para as APIs dentro do produto.</span><span class="sxs-lookup"><span data-stu-id="6ed10-173">Add one  or more of these elements to impose a call rate limit on APIs within the product.</span></span> <span data-ttu-id="6ed10-174">Limites de taxa de chamadas à API e ao produto são aplicados de forma independente.</span><span class="sxs-lookup"><span data-stu-id="6ed10-174">Product and API call rate limits are applied independently.</span></span>|<span data-ttu-id="6ed10-175">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-175">No</span></span>|  
|<span data-ttu-id="6ed10-176">operation</span><span class="sxs-lookup"><span data-stu-id="6ed10-176">operation</span></span>|<span data-ttu-id="6ed10-177">Adicione um ou mais desses elementos para impor um limite de taxa de chamadas para as operações dentro de uma API.</span><span class="sxs-lookup"><span data-stu-id="6ed10-177">Add one  or more of these elements to impose a call rate limit on operations within an API.</span></span> <span data-ttu-id="6ed10-178">Limites de taxa de chamadas à API, operação e produto são aplicados de forma independente.</span><span class="sxs-lookup"><span data-stu-id="6ed10-178">Product, API, and operation call rate limits are applied independently.</span></span>|<span data-ttu-id="6ed10-179">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-179">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="6ed10-180">Atributos</span><span class="sxs-lookup"><span data-stu-id="6ed10-180">Attributes</span></span>  
  
|<span data-ttu-id="6ed10-181">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-181">Name</span></span>|<span data-ttu-id="6ed10-182">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-182">Description</span></span>|<span data-ttu-id="6ed10-183">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-183">Required</span></span>|<span data-ttu-id="6ed10-184">Padrão</span><span class="sxs-lookup"><span data-stu-id="6ed10-184">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6ed10-185">name</span><span class="sxs-lookup"><span data-stu-id="6ed10-185">name</span></span>|<span data-ttu-id="6ed10-186">O nome da API para a qual aplicar o limite de taxa.</span><span class="sxs-lookup"><span data-stu-id="6ed10-186">The name of the API for which to apply the rate limit.</span></span>|<span data-ttu-id="6ed10-187">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-187">Yes</span></span>|<span data-ttu-id="6ed10-188">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-188">N/A</span></span>|  
|<span data-ttu-id="6ed10-189">chamadas</span><span class="sxs-lookup"><span data-stu-id="6ed10-189">calls</span></span>|<span data-ttu-id="6ed10-190">O número total máximo de chamadas permitidas durante o intervalo de tempo especificado no `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="6ed10-190">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="6ed10-191">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-191">Yes</span></span>|<span data-ttu-id="6ed10-192">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-192">N/A</span></span>|  
|<span data-ttu-id="6ed10-193">renewal-period</span><span class="sxs-lookup"><span data-stu-id="6ed10-193">renewal-period</span></span>|<span data-ttu-id="6ed10-194">O período de tempo, em segundos, durante o qual uma cota reinicia.</span><span class="sxs-lookup"><span data-stu-id="6ed10-194">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="6ed10-195">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-195">Yes</span></span>|<span data-ttu-id="6ed10-196">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-196">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6ed10-197">Uso</span><span class="sxs-lookup"><span data-stu-id="6ed10-197">Usage</span></span>  
 <span data-ttu-id="6ed10-198">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ed10-198">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6ed10-199">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="6ed10-199">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="6ed10-200">**Escopos de política:** produto</span><span class="sxs-lookup"><span data-stu-id="6ed10-200">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="6ed10-201"><a name="LimitCallRateByKey"></a> Limitar a taxa de chamadas por chave</span><span class="sxs-lookup"><span data-stu-id="6ed10-201"><a name="LimitCallRateByKey"></a> Limit call rate by key</span></span>  
 <span data-ttu-id="6ed10-202">A política `rate-limit-by-key` impede picos de uso da API para cada chave, limitando a taxa de chamadas para um número especificado por um período de tempo especificado.</span><span class="sxs-lookup"><span data-stu-id="6ed10-202">The `rate-limit-by-key` policy prevents API usage spikes on a per key basis by limiting the call rate to a specified number per a specified time period.</span></span> <span data-ttu-id="6ed10-203">A chave pode ter um valor de cadeia de caracteres arbitrária e geralmente é fornecida usando uma expressão de política.</span><span class="sxs-lookup"><span data-stu-id="6ed10-203">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="6ed10-204">A condição de incremento opcional pode ser adicionada para especificar quais solicitações devem ser contadas para obtenção do limite.</span><span class="sxs-lookup"><span data-stu-id="6ed10-204">Optional increment condition can be added to specify which requests should be counted towards the limit.</span></span> <span data-ttu-id="6ed10-205">Quando essa política é disparada, o chamador recebe um código de status de resposta `429 Too Many Requests`.</span><span class="sxs-lookup"><span data-stu-id="6ed10-205">When this policy is triggered the caller receives a `429 Too Many Requests` response status code.</span></span>  
  
 <span data-ttu-id="6ed10-206">Para obter mais informações e exemplos dessa política, consulte [Limitação de solicitação avançada com o Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="6ed10-206">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="6ed10-207">Essa política pode ser usada apenas uma vez por cada documento de política.</span><span class="sxs-lookup"><span data-stu-id="6ed10-207">This policy can be used only once per policy document.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6ed10-208">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="6ed10-208">Policy statement</span></span>  
  
```xml  
<rate-limit-by-key calls="number"  
                   renewal-period="seconds"   
                   increment-condition="condition"   
                   counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="6ed10-209">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6ed10-209">Example</span></span>  
 <span data-ttu-id="6ed10-210">No exemplo a seguir, o limite de taxa é codificado pelo endereço IP do chamador.</span><span class="sxs-lookup"><span data-stu-id="6ed10-210">In the following example, the rate limit is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="6ed10-211">Elementos</span><span class="sxs-lookup"><span data-stu-id="6ed10-211">Elements</span></span>  
  
|<span data-ttu-id="6ed10-212">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-212">Name</span></span>|<span data-ttu-id="6ed10-213">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-213">Description</span></span>|<span data-ttu-id="6ed10-214">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-214">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="6ed10-215">set-limit</span><span class="sxs-lookup"><span data-stu-id="6ed10-215">set-limit</span></span>|<span data-ttu-id="6ed10-216">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="6ed10-216">Root element.</span></span>|<span data-ttu-id="6ed10-217">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-217">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="6ed10-218">Atributos</span><span class="sxs-lookup"><span data-stu-id="6ed10-218">Attributes</span></span>  
  
|<span data-ttu-id="6ed10-219">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-219">Name</span></span>|<span data-ttu-id="6ed10-220">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-220">Description</span></span>|<span data-ttu-id="6ed10-221">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-221">Required</span></span>|<span data-ttu-id="6ed10-222">Padrão</span><span class="sxs-lookup"><span data-stu-id="6ed10-222">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6ed10-223">chamadas</span><span class="sxs-lookup"><span data-stu-id="6ed10-223">calls</span></span>|<span data-ttu-id="6ed10-224">O número total máximo de chamadas permitidas durante o intervalo de tempo especificado no `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="6ed10-224">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="6ed10-225">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-225">Yes</span></span>|<span data-ttu-id="6ed10-226">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-226">N/A</span></span>|  
|<span data-ttu-id="6ed10-227">counter-key</span><span class="sxs-lookup"><span data-stu-id="6ed10-227">counter-key</span></span>|<span data-ttu-id="6ed10-228">A chave a ser usada para a política de limite de taxa.</span><span class="sxs-lookup"><span data-stu-id="6ed10-228">The key to use for the rate limit policy.</span></span>|<span data-ttu-id="6ed10-229">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-229">Yes</span></span>|<span data-ttu-id="6ed10-230">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-230">N/A</span></span>|  
|<span data-ttu-id="6ed10-231">increment-condition</span><span class="sxs-lookup"><span data-stu-id="6ed10-231">increment-condition</span></span>|<span data-ttu-id="6ed10-232">A expressão booliana que especifica se a solicitação deve ser contabilizada para a cota (`true`).</span><span class="sxs-lookup"><span data-stu-id="6ed10-232">The boolean expression specifying if the request should be counted towards the quota (`true`).</span></span>|<span data-ttu-id="6ed10-233">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-233">No</span></span>|<span data-ttu-id="6ed10-234">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-234">N/A</span></span>|  
|<span data-ttu-id="6ed10-235">renewal-period</span><span class="sxs-lookup"><span data-stu-id="6ed10-235">renewal-period</span></span>|<span data-ttu-id="6ed10-236">O período de tempo, em segundos, durante o qual uma cota reinicia.</span><span class="sxs-lookup"><span data-stu-id="6ed10-236">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="6ed10-237">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-237">Yes</span></span>|<span data-ttu-id="6ed10-238">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-238">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6ed10-239">Uso</span><span class="sxs-lookup"><span data-stu-id="6ed10-239">Usage</span></span>  
 <span data-ttu-id="6ed10-240">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ed10-240">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6ed10-241">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="6ed10-241">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="6ed10-242">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="6ed10-242">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="6ed10-243"><a name="RestrictCallerIPs"></a> Restringir IPs do chamador</span><span class="sxs-lookup"><span data-stu-id="6ed10-243"><a name="RestrictCallerIPs"></a> Restrict caller IPs</span></span>  
 <span data-ttu-id="6ed10-244">A política `ip-filter` filtra (permite/recusa) chamadas de endereços IP específicos e/ou intervalos de endereços.</span><span class="sxs-lookup"><span data-stu-id="6ed10-244">The `ip-filter` policy filters (allows/denies) calls from specific IP addresses and/or address ranges.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6ed10-245">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="6ed10-245">Policy statement</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="example"></a><span data-ttu-id="6ed10-246">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6ed10-246">Example</span></span>  
  
```xml  
<ip-filter action="allow | forbid">  
    <address>address</address>  
    <address-range from="address" to="address" />  
</ip-filter>  
```  
  
### <a name="elements"></a><span data-ttu-id="6ed10-247">Elementos</span><span class="sxs-lookup"><span data-stu-id="6ed10-247">Elements</span></span>  
  
|<span data-ttu-id="6ed10-248">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-248">Name</span></span>|<span data-ttu-id="6ed10-249">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-249">Description</span></span>|<span data-ttu-id="6ed10-250">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-250">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="6ed10-251">ip-filter</span><span class="sxs-lookup"><span data-stu-id="6ed10-251">ip-filter</span></span>|<span data-ttu-id="6ed10-252">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="6ed10-252">Root element.</span></span>|<span data-ttu-id="6ed10-253">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-253">Yes</span></span>|  
|<span data-ttu-id="6ed10-254">endereço</span><span class="sxs-lookup"><span data-stu-id="6ed10-254">address</span></span>|<span data-ttu-id="6ed10-255">Especifica um único endereço IP no qual filtrar.</span><span class="sxs-lookup"><span data-stu-id="6ed10-255">Specifies a single IP address on which to filter.</span></span>|<span data-ttu-id="6ed10-256">Pelo menos um elemento `address` ou `address-range` é necessário.</span><span class="sxs-lookup"><span data-stu-id="6ed10-256">At least one `address` or `address-range` element is required.</span></span>|  
|<span data-ttu-id="6ed10-257">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="6ed10-257">address-range from="address" to="address"</span></span>|<span data-ttu-id="6ed10-258">Especifica um intervalo de endereços IP nos quais filtrar.</span><span class="sxs-lookup"><span data-stu-id="6ed10-258">Specifies a range of IP address on which to filter.</span></span>|<span data-ttu-id="6ed10-259">Pelo menos um elemento `address` ou `address-range` é necessário.</span><span class="sxs-lookup"><span data-stu-id="6ed10-259">At least one `address` or `address-range` element is required.</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="6ed10-260">Atributos</span><span class="sxs-lookup"><span data-stu-id="6ed10-260">Attributes</span></span>  
  
|<span data-ttu-id="6ed10-261">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-261">Name</span></span>|<span data-ttu-id="6ed10-262">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-262">Description</span></span>|<span data-ttu-id="6ed10-263">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-263">Required</span></span>|<span data-ttu-id="6ed10-264">Padrão</span><span class="sxs-lookup"><span data-stu-id="6ed10-264">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6ed10-265">address-range from="address" to="address"</span><span class="sxs-lookup"><span data-stu-id="6ed10-265">address-range from="address" to="address"</span></span>|<span data-ttu-id="6ed10-266">Um intervalo de endereços IP aos quais o acesso será permitido ou negado.</span><span class="sxs-lookup"><span data-stu-id="6ed10-266">A range of IP addresses to allow or deny access for.</span></span>|<span data-ttu-id="6ed10-267">Necessário quando o elemento `address-range` é usado.</span><span class="sxs-lookup"><span data-stu-id="6ed10-267">Required when the `address-range` element is used.</span></span>|<span data-ttu-id="6ed10-268">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-268">N/A</span></span>|  
|<span data-ttu-id="6ed10-269">ip-filter action="allow &#124; forbid"</span><span class="sxs-lookup"><span data-stu-id="6ed10-269">ip-filter action="allow &#124; forbid"</span></span>|<span data-ttu-id="6ed10-270">Especifica se chamadas para os endereços IP e intervalos de endereços IP especificados devem ou não ser permitidas.</span><span class="sxs-lookup"><span data-stu-id="6ed10-270">Specifies whether calls should be allowed or not for the specified IP addresses and ranges.</span></span>|<span data-ttu-id="6ed10-271">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-271">Yes</span></span>|<span data-ttu-id="6ed10-272">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-272">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6ed10-273">Uso</span><span class="sxs-lookup"><span data-stu-id="6ed10-273">Usage</span></span>  
 <span data-ttu-id="6ed10-274">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ed10-274">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6ed10-275">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="6ed10-275">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="6ed10-276">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="6ed10-276">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="6ed10-277"><a name="SetUsageQuota"></a> Definir a cota de uso por assinatura</span><span class="sxs-lookup"><span data-stu-id="6ed10-277"><a name="SetUsageQuota"></a> Set usage quota by subscription</span></span>  
 <span data-ttu-id="6ed10-278">A política `quota` impõe uma cota renovável ou de tempo de vida de volume de chamadas e/ou largura de banda, para cada assinatura.</span><span class="sxs-lookup"><span data-stu-id="6ed10-278">The `quota` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per subscription basis.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="6ed10-279">Essa política pode ser usada apenas uma vez por cada documento de política.</span><span class="sxs-lookup"><span data-stu-id="6ed10-279">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="6ed10-280">As [expressões de política](api-management-policy-expressions.md) não podem ser usadas em nenhum dos atributos de política para essa política.</span><span class="sxs-lookup"><span data-stu-id="6ed10-280">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6ed10-281">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="6ed10-281">Policy statement</span></span>  
  
```xml  
<quota calls="number" bandwidth="kilobytes" renewal-period="seconds">  
    <api name="name" calls="number" bandwidth="kilobytes">  
        <operation name="name" calls="number" bandwidth="kilobytes" />  
    </api>  
</quota>  
```  
  
### <a name="example"></a><span data-ttu-id="6ed10-282">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6ed10-282">Example</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="6ed10-283">Elementos</span><span class="sxs-lookup"><span data-stu-id="6ed10-283">Elements</span></span>  
  
|<span data-ttu-id="6ed10-284">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-284">Name</span></span>|<span data-ttu-id="6ed10-285">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-285">Description</span></span>|<span data-ttu-id="6ed10-286">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-286">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="6ed10-287">quota</span><span class="sxs-lookup"><span data-stu-id="6ed10-287">quota</span></span>|<span data-ttu-id="6ed10-288">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="6ed10-288">Root element.</span></span>|<span data-ttu-id="6ed10-289">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-289">Yes</span></span>|  
|<span data-ttu-id="6ed10-290">api</span><span class="sxs-lookup"><span data-stu-id="6ed10-290">api</span></span>|<span data-ttu-id="6ed10-291">Adicione um ou mais desses elementos para impor uma cota para as APIs dentro do produto.</span><span class="sxs-lookup"><span data-stu-id="6ed10-291">Add one  or more of these elements to impose a quota on APIs within the product.</span></span> <span data-ttu-id="6ed10-292">Cotas de API e produto são aplicadas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="6ed10-292">Product and API quotas are applied independently.</span></span>|<span data-ttu-id="6ed10-293">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-293">No</span></span>|  
|<span data-ttu-id="6ed10-294">operation</span><span class="sxs-lookup"><span data-stu-id="6ed10-294">operation</span></span>|<span data-ttu-id="6ed10-295">Adicione um ou mais desses elementos para impor uma cota para as operações dentro de uma API.</span><span class="sxs-lookup"><span data-stu-id="6ed10-295">Add one  or more of these elements to impose a quota on operations within an API.</span></span> <span data-ttu-id="6ed10-296">Cotas de operações, APIs e produtos são aplicadas de forma independente.</span><span class="sxs-lookup"><span data-stu-id="6ed10-296">Product, API, and operation quotas are applied independently.</span></span>|<span data-ttu-id="6ed10-297">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-297">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="6ed10-298">Atributos</span><span class="sxs-lookup"><span data-stu-id="6ed10-298">Attributes</span></span>  
  
|<span data-ttu-id="6ed10-299">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-299">Name</span></span>|<span data-ttu-id="6ed10-300">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-300">Description</span></span>|<span data-ttu-id="6ed10-301">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-301">Required</span></span>|<span data-ttu-id="6ed10-302">Padrão</span><span class="sxs-lookup"><span data-stu-id="6ed10-302">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6ed10-303">name</span><span class="sxs-lookup"><span data-stu-id="6ed10-303">name</span></span>|<span data-ttu-id="6ed10-304">O nome da API ou operação à qual a cota se aplica.</span><span class="sxs-lookup"><span data-stu-id="6ed10-304">The name of the API or operation for which the quota applies.</span></span>|<span data-ttu-id="6ed10-305">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-305">Yes</span></span>|<span data-ttu-id="6ed10-306">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-306">N/A</span></span>|  
|<span data-ttu-id="6ed10-307">largura de banda</span><span class="sxs-lookup"><span data-stu-id="6ed10-307">bandwidth</span></span>|<span data-ttu-id="6ed10-308">O número total máximo de kilobytes permitidos durante o intervalo de tempo especificado no `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="6ed10-308">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="6ed10-309">`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="6ed10-309">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="6ed10-310">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-310">N/A</span></span>|  
|<span data-ttu-id="6ed10-311">chamadas</span><span class="sxs-lookup"><span data-stu-id="6ed10-311">calls</span></span>|<span data-ttu-id="6ed10-312">O número total máximo de chamadas permitidas durante o intervalo de tempo especificado no `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="6ed10-312">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="6ed10-313">`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="6ed10-313">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="6ed10-314">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-314">N/A</span></span>|  
|<span data-ttu-id="6ed10-315">renewal-period</span><span class="sxs-lookup"><span data-stu-id="6ed10-315">renewal-period</span></span>|<span data-ttu-id="6ed10-316">O período de tempo, em segundos, durante o qual uma cota reinicia.</span><span class="sxs-lookup"><span data-stu-id="6ed10-316">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="6ed10-317">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-317">Yes</span></span>|<span data-ttu-id="6ed10-318">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-318">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6ed10-319">Uso</span><span class="sxs-lookup"><span data-stu-id="6ed10-319">Usage</span></span>  
 <span data-ttu-id="6ed10-320">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ed10-320">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6ed10-321">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="6ed10-321">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="6ed10-322">**Escopos de política:** produto</span><span class="sxs-lookup"><span data-stu-id="6ed10-322">**Policy scopes:** product</span></span>  
  
##  <span data-ttu-id="6ed10-323"><a name="SetUsageQuotaByKey"></a> Definir uma cota de uso por chave</span><span class="sxs-lookup"><span data-stu-id="6ed10-323"><a name="SetUsageQuotaByKey"></a> Set usage quota by key</span></span>  
 <span data-ttu-id="6ed10-324">A política `quota-by-key` impõe uma cota renovável ou de tempo de vida de volume de chamadas e/ou largura de banda, para cada chave.</span><span class="sxs-lookup"><span data-stu-id="6ed10-324">The `quota-by-key` policy enforces a renewable or lifetime call volume and/or bandwidth quota, on a per key basis.</span></span> <span data-ttu-id="6ed10-325">A chave pode ter um valor de cadeia de caracteres arbitrária e geralmente é fornecida usando uma expressão de política.</span><span class="sxs-lookup"><span data-stu-id="6ed10-325">The key can have an arbitrary string value and is typically provided using a policy expression.</span></span> <span data-ttu-id="6ed10-326">A condição de incremento opcional pode ser adicionada para especificar quais solicitações devem ser contadas para obtenção da cota.</span><span class="sxs-lookup"><span data-stu-id="6ed10-326">Optional increment condition can be added to specify which requests should be counted towards the quota.</span></span>  
  
 <span data-ttu-id="6ed10-327">Para obter mais informações e exemplos dessa política, consulte [Limitação de solicitação avançada com o Gerenciamento de API do Azure](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span><span class="sxs-lookup"><span data-stu-id="6ed10-327">For more information and examples of this policy, see [Advanced request throttling with Azure API Management](https://azure.microsoft.com/documentation/articles/api-management-sample-flexible-throttling/).</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="6ed10-328">Essa política pode ser usada apenas uma vez por cada documento de política.</span><span class="sxs-lookup"><span data-stu-id="6ed10-328">This policy can be used only once per policy document.</span></span>  
>   
>  <span data-ttu-id="6ed10-329">As [expressões de política](api-management-policy-expressions.md) não podem ser usadas em nenhum dos atributos de política para essa política.</span><span class="sxs-lookup"><span data-stu-id="6ed10-329">[Policy expressions](api-management-policy-expressions.md) cannot be used in any of the policy attributes for this policy.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6ed10-330">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="6ed10-330">Policy statement</span></span>  
  
```xml  
<quota-by-key calls="number"   
              bandwidth="kilobytes"   
              renewal-period="seconds"  
              increment-condition="condition"   
              counter-key="key value" />  
  
```  
  
### <a name="example"></a><span data-ttu-id="6ed10-331">Exemplo</span><span class="sxs-lookup"><span data-stu-id="6ed10-331">Example</span></span>  
 <span data-ttu-id="6ed10-332">No exemplo a seguir, a cota é codificada pelo endereço IP do chamador.</span><span class="sxs-lookup"><span data-stu-id="6ed10-332">In the following example, the quota is keyed by the caller IP address.</span></span>  
  
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
  
### <a name="elements"></a><span data-ttu-id="6ed10-333">Elementos</span><span class="sxs-lookup"><span data-stu-id="6ed10-333">Elements</span></span>  
  
|<span data-ttu-id="6ed10-334">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-334">Name</span></span>|<span data-ttu-id="6ed10-335">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-335">Description</span></span>|<span data-ttu-id="6ed10-336">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-336">Required</span></span>|  
|----------|-----------------|--------------|  
|<span data-ttu-id="6ed10-337">quota</span><span class="sxs-lookup"><span data-stu-id="6ed10-337">quota</span></span>|<span data-ttu-id="6ed10-338">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="6ed10-338">Root element.</span></span>|<span data-ttu-id="6ed10-339">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-339">Yes</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="6ed10-340">Atributos</span><span class="sxs-lookup"><span data-stu-id="6ed10-340">Attributes</span></span>  
  
|<span data-ttu-id="6ed10-341">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-341">Name</span></span>|<span data-ttu-id="6ed10-342">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-342">Description</span></span>|<span data-ttu-id="6ed10-343">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-343">Required</span></span>|<span data-ttu-id="6ed10-344">Padrão</span><span class="sxs-lookup"><span data-stu-id="6ed10-344">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6ed10-345">largura de banda</span><span class="sxs-lookup"><span data-stu-id="6ed10-345">bandwidth</span></span>|<span data-ttu-id="6ed10-346">O número total máximo de kilobytes permitidos durante o intervalo de tempo especificado no `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="6ed10-346">The maximum total number of kilobytes allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="6ed10-347">`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="6ed10-347">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="6ed10-348">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-348">N/A</span></span>|  
|<span data-ttu-id="6ed10-349">chamadas</span><span class="sxs-lookup"><span data-stu-id="6ed10-349">calls</span></span>|<span data-ttu-id="6ed10-350">O número total máximo de chamadas permitidas durante o intervalo de tempo especificado no `renewal-period`.</span><span class="sxs-lookup"><span data-stu-id="6ed10-350">The maximum total number of calls allowed during the time interval specified in the `renewal-period`.</span></span>|<span data-ttu-id="6ed10-351">`calls` ou `bandwidth` ou ainda ambos juntos devem ser especificados.</span><span class="sxs-lookup"><span data-stu-id="6ed10-351">Either `calls`, `bandwidth`, or both together must be specified.</span></span>|<span data-ttu-id="6ed10-352">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-352">N/A</span></span>|  
|<span data-ttu-id="6ed10-353">counter-key</span><span class="sxs-lookup"><span data-stu-id="6ed10-353">counter-key</span></span>|<span data-ttu-id="6ed10-354">A chave a ser usada para a política de cota.</span><span class="sxs-lookup"><span data-stu-id="6ed10-354">The key to use for the quota policy.</span></span>|<span data-ttu-id="6ed10-355">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-355">Yes</span></span>|<span data-ttu-id="6ed10-356">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-356">N/A</span></span>|  
|<span data-ttu-id="6ed10-357">increment-condition</span><span class="sxs-lookup"><span data-stu-id="6ed10-357">increment-condition</span></span>|<span data-ttu-id="6ed10-358">A expressão booliana que especifica se a solicitação deve ser contabilizada para a cota (`true`)</span><span class="sxs-lookup"><span data-stu-id="6ed10-358">The boolean expression specifying if the request should be counted towards the quota (`true`)</span></span>|<span data-ttu-id="6ed10-359">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-359">No</span></span>|<span data-ttu-id="6ed10-360">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-360">N/A</span></span>|  
|<span data-ttu-id="6ed10-361">renewal-period</span><span class="sxs-lookup"><span data-stu-id="6ed10-361">renewal-period</span></span>|<span data-ttu-id="6ed10-362">O período de tempo, em segundos, durante o qual uma cota reinicia.</span><span class="sxs-lookup"><span data-stu-id="6ed10-362">The time period in seconds after which the quota resets.</span></span>|<span data-ttu-id="6ed10-363">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-363">Yes</span></span>|<span data-ttu-id="6ed10-364">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-364">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6ed10-365">Uso</span><span class="sxs-lookup"><span data-stu-id="6ed10-365">Usage</span></span>  
 <span data-ttu-id="6ed10-366">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ed10-366">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6ed10-367">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="6ed10-367">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="6ed10-368">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="6ed10-368">**Policy scopes:** global, product, API, operation</span></span>  
  
##  <span data-ttu-id="6ed10-369"><a name="ValidateJWT"></a> Validar JWT</span><span class="sxs-lookup"><span data-stu-id="6ed10-369"><a name="ValidateJWT"></a> Validate JWT</span></span>  
 <span data-ttu-id="6ed10-370">A política `validate-jwt` impõe a existência e a validade de um JWT extraído de um Cabeçalho HTTP ou um parâmetro de consulta especificado.</span><span class="sxs-lookup"><span data-stu-id="6ed10-370">The `validate-jwt` policy enforces existence and validity of a JWT extracted from either a specified HTTP Header or a specified query parameter.</span></span>  
  
> [!IMPORTANT]
>  <span data-ttu-id="6ed10-371">A política `validate-jwt` requer que a declaração registrada `exp` seja incluída no token JWT, a menos que o atributo `require-expiration-time` seja especificado e definido como `false`.</span><span class="sxs-lookup"><span data-stu-id="6ed10-371">The `validate-jwt` policy requires that the `exp` registered claim is inlcuded in the JWT token, unless `require-expiration-time` attribute is specified and set to `false`.</span></span>  
> <span data-ttu-id="6ed10-372">A política `validate-jwt` dá suporte aos algoritmos de assinatura HS256 e RS256.</span><span class="sxs-lookup"><span data-stu-id="6ed10-372">The `validate-jwt` policy supports HS256 and RS256 signing algorithms.</span></span> <span data-ttu-id="6ed10-373">Para HS256, a chave deve ser fornecida embutida na política no formato codificado em base64.</span><span class="sxs-lookup"><span data-stu-id="6ed10-373">For HS256 the key must be provided inline within the policy in the base64 encoded form.</span></span> <span data-ttu-id="6ed10-374">Para RS256, a chave deve ser fornecida por meio de um ponto de extremidade de configuração de Open ID.</span><span class="sxs-lookup"><span data-stu-id="6ed10-374">For RS256 the key has to be provide via an Open ID configuration endpoint.</span></span>  
  
### <a name="policy-statement"></a><span data-ttu-id="6ed10-375">Declaração de política</span><span class="sxs-lookup"><span data-stu-id="6ed10-375">Policy statement</span></span>  
  
```xml  
<validate-jwt   
    header-name="name of http header containing the token (use query-parameter-name attribute if the token is passed in the URL)"   
    failed-validation-httpcode="http status code to return on failure"   
    failed-validation-error-message="error message to return on failure"   
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
    <claim name="name of the claim as it appears in the token" match="all|any">  
      <value>claim value as it is expected to appear in the token</value>  
      <!-- if there is more than one allowed values, then add additional value elements -->  
    </claim>  
    <!-- if there are multiple possible allowed values, then add additional value elements -->  
  </required-claims>  
  <openid-config url="full URL of the configuration endpoint, e.g. https://login.constoso.com/openid-configuration" />  
  <zumo-master-key id="key identifier">key value</zumo-master-key>  
</validate-jwt>  
  
```  
  
### <a name="examples"></a><span data-ttu-id="6ed10-376">Exemplos</span><span class="sxs-lookup"><span data-stu-id="6ed10-376">Examples</span></span>  
  
#### <a name="azure-mobile-services-token-validation"></a><span data-ttu-id="6ed10-377">Validação de token de Serviços Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="6ed10-377">Azure Mobile Services token validation</span></span>  
  
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
  
#### <a name="azure-active-directory-token-validation"></a><span data-ttu-id="6ed10-378">Validação de token do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="6ed10-378">Azure Active Directory token validation</span></span>  
  
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

  
#### <a name="azure-active-directory-b2c-token-validation"></a><span data-ttu-id="6ed10-379">Validação de token do Azure Active Directory B2C</span><span class="sxs-lookup"><span data-stu-id="6ed10-379">Azure Active Directory B2C token validation</span></span>  
  
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
  
#### <a name="authorize-access-to-operations-based-on-token-claims"></a><span data-ttu-id="6ed10-380">Autorizar o acesso para operações baseadas em declarações de token</span><span class="sxs-lookup"><span data-stu-id="6ed10-380">Authorize access to operations based on token claims</span></span>  
 <span data-ttu-id="6ed10-381">Este exemplo mostra como usar a política [Validar JWT](api-management-access-restriction-policies.md#ValidateJWT) para pré-autorizar o acesso a operações baseadas em declarações de token.</span><span class="sxs-lookup"><span data-stu-id="6ed10-381">This example shows how to use the [Validate JWT](api-management-access-restriction-policies.md#ValidateJWT) policy to pre-authorize access to operations based on token claims.</span></span> <span data-ttu-id="6ed10-382">Para ver uma demonstração da configuração e do uso dessa política, consulte [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) (Abordagem da Nuvem Episódio 177: Mais Recursos de Gerenciamento de API com Vlad Vinogradsky) e avance para 13:50.</span><span class="sxs-lookup"><span data-stu-id="6ed10-382">For a demonstration of configuring and using this policy, see [Cloud Cover Episode 177: More API Management Features with Vlad Vinogradsky](https://azure.microsoft.com/documentation/videos/episode-177-more-api-management-features-with-vlad-vinogradsky/) and fast-forward to 13:50.</span></span> <span data-ttu-id="6ed10-383">Avance para 15:00 para ver as diretivas configuradas no editor de diretiva e, em seguida, 18:50 para uma demonstração de como chamar uma operação do portal do desenvolvedor com e sem o token de autorização necessário.</span><span class="sxs-lookup"><span data-stu-id="6ed10-383">Fast forward to 15:00 to see the policies configured in the policy editor and then to 18:50 for a demonstration of calling an operation from the developer portal both with and without the required authorization token.</span></span>  
  
```xml  
<!-- Copy the following snippet into the inbound section at the api (or higher) level to pre-authorize access to operations based on token claims -->  
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
  
### <a name="elements"></a><span data-ttu-id="6ed10-384">Elementos</span><span class="sxs-lookup"><span data-stu-id="6ed10-384">Elements</span></span>  
  
|<span data-ttu-id="6ed10-385">Elemento</span><span class="sxs-lookup"><span data-stu-id="6ed10-385">Element</span></span>|<span data-ttu-id="6ed10-386">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-386">Description</span></span>|<span data-ttu-id="6ed10-387">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-387">Required</span></span>|  
|-------------|-----------------|--------------|  
|<span data-ttu-id="6ed10-388">validate-jwt</span><span class="sxs-lookup"><span data-stu-id="6ed10-388">validate-jwt</span></span>|<span data-ttu-id="6ed10-389">Elemento raiz.</span><span class="sxs-lookup"><span data-stu-id="6ed10-389">Root element.</span></span>|<span data-ttu-id="6ed10-390">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-390">Yes</span></span>|  
|<span data-ttu-id="6ed10-391">públicos-alvo</span><span class="sxs-lookup"><span data-stu-id="6ed10-391">audiences</span></span>|<span data-ttu-id="6ed10-392">Contém uma lista de declarações de público-alvo aceitáveis que podem estar presentes no token.</span><span class="sxs-lookup"><span data-stu-id="6ed10-392">Contains a list of acceptable audience claims that can be present on the token.</span></span> <span data-ttu-id="6ed10-393">Se vários valores de público-alvo estiverem presentes, cada valor será tentado até que todos sejam esgotados (nesse caso, a validação falhará) ou até obter êxito.</span><span class="sxs-lookup"><span data-stu-id="6ed10-393">If multiple audience values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span> <span data-ttu-id="6ed10-394">Pelo menos um público-alvo deve ser especificado.</span><span class="sxs-lookup"><span data-stu-id="6ed10-394">At least one audience must be specified.</span></span>|<span data-ttu-id="6ed10-395">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-395">No</span></span>|  
|<span data-ttu-id="6ed10-396">issuer-signing-keys</span><span class="sxs-lookup"><span data-stu-id="6ed10-396">issuer-signing-keys</span></span>|<span data-ttu-id="6ed10-397">Uma lista de chaves de segurança codificadas em Base64 usadas para validar tokens assinados.</span><span class="sxs-lookup"><span data-stu-id="6ed10-397">A list of Base64-encoded security keys used to validate signed tokens.</span></span> <span data-ttu-id="6ed10-398">Se várias chaves de segurança estiverem presentes, cada chave será tentada até que todas sejam esgotadas (nesse caso, a validação falhará) ou até obter êxito (útil para substituição de token).</span><span class="sxs-lookup"><span data-stu-id="6ed10-398">If multiple security keys are present, then each key is tried until either all are exhausted (in which case validation fails) or until one succeeds (useful for token rollover).</span></span> <span data-ttu-id="6ed10-399">Elementos-chave têm um atributo `id` opcional usado para correspondência com a declaração `kid`.</span><span class="sxs-lookup"><span data-stu-id="6ed10-399">Key elements have an optional `id` attribute used to match against `kid` claim.</span></span>|<span data-ttu-id="6ed10-400">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-400">No</span></span>|  
|<span data-ttu-id="6ed10-401">emissores</span><span class="sxs-lookup"><span data-stu-id="6ed10-401">issuers</span></span>|<span data-ttu-id="6ed10-402">Uma lista de entidades aceitáveis que emitiram o token.</span><span class="sxs-lookup"><span data-stu-id="6ed10-402">A list of acceptable principals that issued the token.</span></span> <span data-ttu-id="6ed10-403">Se vários valores de emissor estiverem presentes, cada valor será tentado até que todos sejam esgotados (nesse caso, a validação falhará) ou até obter êxito.</span><span class="sxs-lookup"><span data-stu-id="6ed10-403">If multiple issuer values are present, then each value is tried until either all are exhausted (in which case validation fails) or until one succeeds.</span></span>|<span data-ttu-id="6ed10-404">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-404">No</span></span>|  
|<span data-ttu-id="6ed10-405">openid-config</span><span class="sxs-lookup"><span data-stu-id="6ed10-405">openid-config</span></span>|<span data-ttu-id="6ed10-406">O elemento usado para especificar um ponto de extremidade de configuração de Open ID em conformidade do qual chaves de assinatura e emissor podem ser obtidos.</span><span class="sxs-lookup"><span data-stu-id="6ed10-406">The element used for specifying a compliant Open ID configuration endpoint from which signing keys and issuer can be obtained.</span></span>|<span data-ttu-id="6ed10-407">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-407">No</span></span>|  
|<span data-ttu-id="6ed10-408">required-claims</span><span class="sxs-lookup"><span data-stu-id="6ed10-408">required-claims</span></span>|<span data-ttu-id="6ed10-409">Contém uma lista de declarações cuja presença é esperada no token para que ele possa ser considerado válido.</span><span class="sxs-lookup"><span data-stu-id="6ed10-409">Contains a list of claims expected to be present on the token for it to be considered valid.</span></span> <span data-ttu-id="6ed10-410">Quando o atributo `match` é definido como `all`, cada valor de declaração na política deve estar presente no token para que a validação seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="6ed10-410">When the `match` attribute is set to `all` every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="6ed10-411">Quando o atributo `match` é definido como `any`, pelo menos uma declaração deve estar presente no token para que a validação seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="6ed10-411">When the `match` attribute is set to `any` at least one claim must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="6ed10-412">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-412">No</span></span>|  
|<span data-ttu-id="6ed10-413">zumo-master-key</span><span class="sxs-lookup"><span data-stu-id="6ed10-413">zumo-master-key</span></span>|<span data-ttu-id="6ed10-414">Chave mestra para tokens emitidos pelos Serviços Móveis do Azure</span><span class="sxs-lookup"><span data-stu-id="6ed10-414">Master key for tokens issued by Azure Mobile Services</span></span>|<span data-ttu-id="6ed10-415">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-415">No</span></span>|  
  
### <a name="attributes"></a><span data-ttu-id="6ed10-416">Atributos</span><span class="sxs-lookup"><span data-stu-id="6ed10-416">Attributes</span></span>  
  
|<span data-ttu-id="6ed10-417">Nome</span><span class="sxs-lookup"><span data-stu-id="6ed10-417">Name</span></span>|<span data-ttu-id="6ed10-418">Descrição</span><span class="sxs-lookup"><span data-stu-id="6ed10-418">Description</span></span>|<span data-ttu-id="6ed10-419">Obrigatório</span><span class="sxs-lookup"><span data-stu-id="6ed10-419">Required</span></span>|<span data-ttu-id="6ed10-420">Padrão</span><span class="sxs-lookup"><span data-stu-id="6ed10-420">Default</span></span>|  
|----------|-----------------|--------------|-------------|  
|<span data-ttu-id="6ed10-421">clock-skew</span><span class="sxs-lookup"><span data-stu-id="6ed10-421">clock-skew</span></span>|<span data-ttu-id="6ed10-422">Período de tempo.</span><span class="sxs-lookup"><span data-stu-id="6ed10-422">Timespan.</span></span> <span data-ttu-id="6ed10-423">Fornece alguma pequena reserva caso a declaração de expiração do token esteja presente no token e seja após a data/hora atual.</span><span class="sxs-lookup"><span data-stu-id="6ed10-423">Provides some small leeway in case the token's expiration claim is present in the token and is past the current date / time.</span></span>|<span data-ttu-id="6ed10-424">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-424">No</span></span>|<span data-ttu-id="6ed10-425">0 segundos</span><span class="sxs-lookup"><span data-stu-id="6ed10-425">0 seconds</span></span>|  
|<span data-ttu-id="6ed10-426">failed-validation-error-message</span><span class="sxs-lookup"><span data-stu-id="6ed10-426">failed-validation-error-message</span></span>|<span data-ttu-id="6ed10-427">Mensagem de erro para retornar no corpo da resposta HTTP se o JWT não passar na validação.</span><span class="sxs-lookup"><span data-stu-id="6ed10-427">Error message to return in the HTTP response body if the JWT does not pass validation.</span></span> <span data-ttu-id="6ed10-428">Esta mensagem deve conter quaisquer caracteres especiais adequadamente seguidos por caracteres de escape.</span><span class="sxs-lookup"><span data-stu-id="6ed10-428">This message must have any special characters properly escaped.</span></span>|<span data-ttu-id="6ed10-429">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-429">No</span></span>|<span data-ttu-id="6ed10-430">A mensagem de erro padrão depende do problema de validação, por exemplo, "O JWT não está presente."</span><span class="sxs-lookup"><span data-stu-id="6ed10-430">Default error message depends on validation issue, for example "JWT not present."</span></span>|  
|<span data-ttu-id="6ed10-431">failed-validation-httpcode</span><span class="sxs-lookup"><span data-stu-id="6ed10-431">failed-validation-httpcode</span></span>|<span data-ttu-id="6ed10-432">O código de status HTTP para retornar se o JWT não passar na validação.</span><span class="sxs-lookup"><span data-stu-id="6ed10-432">HTTP Status code to return if the JWT doesn't pass validation.</span></span>|<span data-ttu-id="6ed10-433">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-433">No</span></span>|<span data-ttu-id="6ed10-434">401</span><span class="sxs-lookup"><span data-stu-id="6ed10-434">401</span></span>|  
|<span data-ttu-id="6ed10-435">header-name</span><span class="sxs-lookup"><span data-stu-id="6ed10-435">header-name</span></span>|<span data-ttu-id="6ed10-436">O nome do cabeçalho HTTP contendo o token.</span><span class="sxs-lookup"><span data-stu-id="6ed10-436">The name of the HTTP header holding the token.</span></span>|<span data-ttu-id="6ed10-437">`header-name` ou `query-paremeter-name` deve ser especificado; mas não ambos.</span><span class="sxs-lookup"><span data-stu-id="6ed10-437">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="6ed10-438">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-438">N/A</span></span>|  
|<span data-ttu-id="6ed10-439">ID</span><span class="sxs-lookup"><span data-stu-id="6ed10-439">id</span></span>|<span data-ttu-id="6ed10-440">O atributo `id` no elemento `key` permite que você especifique a cadeia de caracteres cuja correspondência será verificada em relação à declaração `kid` no token (se presente) para descobrir a chave apropriada a ser usada para validação de assinatura.</span><span class="sxs-lookup"><span data-stu-id="6ed10-440">The `id` attribute on the `key` element allows you to specify the string that will be matched against `kid` claim in the token (if present) to find out the appropriate key to use for signature validation.</span></span>|<span data-ttu-id="6ed10-441">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-441">No</span></span>|<span data-ttu-id="6ed10-442">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-442">N/A</span></span>|  
|<span data-ttu-id="6ed10-443">match</span><span class="sxs-lookup"><span data-stu-id="6ed10-443">match</span></span>|<span data-ttu-id="6ed10-444">O atributo `match` no elemento `claim` especifica se todos os valores de declaração na política devem estar presentes no token para que a validação seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="6ed10-444">The `match` attribute on the `claim` element specifies whether every claim value in the policy must be present in the token for validation to succeed.</span></span> <span data-ttu-id="6ed10-445">Os valores possíveis são:</span><span class="sxs-lookup"><span data-stu-id="6ed10-445">Possible values are:</span></span><br /><br /> <span data-ttu-id="6ed10-446">-                          `all` – todos os valores de declaração na política devem estar presentes no token para que a validação seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="6ed10-446">-                          `all` - every claim value in the policy must be present in the token for validation to succeed.</span></span><br /><br /> <span data-ttu-id="6ed10-447">-                          `any` – pelo menos um valor de declaração na política deve estar presente no token para que a validação seja bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="6ed10-447">-                          `any` - at least one claim value must be present in the token for validation to succeed.</span></span>|<span data-ttu-id="6ed10-448">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-448">No</span></span>|<span data-ttu-id="6ed10-449">tudo</span><span class="sxs-lookup"><span data-stu-id="6ed10-449">all</span></span>|  
|<span data-ttu-id="6ed10-450">query-paremeter-name</span><span class="sxs-lookup"><span data-stu-id="6ed10-450">query-paremeter-name</span></span>|<span data-ttu-id="6ed10-451">O nome do parâmetro de consulta que contém o token.</span><span class="sxs-lookup"><span data-stu-id="6ed10-451">The name of the the query parameter holding the token.</span></span>|<span data-ttu-id="6ed10-452">`header-name` ou `query-paremeter-name` deve ser especificado; mas não ambos.</span><span class="sxs-lookup"><span data-stu-id="6ed10-452">Either `header-name` or `query-paremeter-name` must be specified; but not both.</span></span>|<span data-ttu-id="6ed10-453">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-453">N/A</span></span>|  
|<span data-ttu-id="6ed10-454">require-expiration-time</span><span class="sxs-lookup"><span data-stu-id="6ed10-454">require-expiration-time</span></span>|<span data-ttu-id="6ed10-455">Booliano.</span><span class="sxs-lookup"><span data-stu-id="6ed10-455">Boolean.</span></span> <span data-ttu-id="6ed10-456">Especifica se uma declaração de expiração é necessária no token.</span><span class="sxs-lookup"><span data-stu-id="6ed10-456">Specifies whether an expiration claim is required in the token.</span></span>|<span data-ttu-id="6ed10-457">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-457">No</span></span>|<span data-ttu-id="6ed10-458">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6ed10-458">true</span></span>|
|<span data-ttu-id="6ed10-459">require-scheme</span><span class="sxs-lookup"><span data-stu-id="6ed10-459">require-scheme</span></span>|<span data-ttu-id="6ed10-460">O nome do esquema do token, por exemplo, "Portador".</span><span class="sxs-lookup"><span data-stu-id="6ed10-460">The name of the token scheme, e.g. "Bearer".</span></span> <span data-ttu-id="6ed10-461">Quando esse atributo for definido, a política garantirá que o esquema especificado esteja presente no valor do cabeçalho de Autorização.</span><span class="sxs-lookup"><span data-stu-id="6ed10-461">When this attribute is set, the policy will ensure that specified scheme is present in the Authorization header value.</span></span>|<span data-ttu-id="6ed10-462">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-462">No</span></span>|<span data-ttu-id="6ed10-463">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-463">N/A</span></span>|
|<span data-ttu-id="6ed10-464">require-signed-tokens</span><span class="sxs-lookup"><span data-stu-id="6ed10-464">require-signed-tokens</span></span>|<span data-ttu-id="6ed10-465">Booliano.</span><span class="sxs-lookup"><span data-stu-id="6ed10-465">Boolean.</span></span> <span data-ttu-id="6ed10-466">Especifica se é necessário que um determinado token seja assinado.</span><span class="sxs-lookup"><span data-stu-id="6ed10-466">Specifies whether a token is required to be signed.</span></span>|<span data-ttu-id="6ed10-467">Não</span><span class="sxs-lookup"><span data-stu-id="6ed10-467">No</span></span>|<span data-ttu-id="6ed10-468">verdadeiro</span><span class="sxs-lookup"><span data-stu-id="6ed10-468">true</span></span>|  
|<span data-ttu-id="6ed10-469">url</span><span class="sxs-lookup"><span data-stu-id="6ed10-469">url</span></span>|<span data-ttu-id="6ed10-470">URL ponto de extremidade de configuração de Open ID da qual é possível obter os metadados de configuração de Open ID.</span><span class="sxs-lookup"><span data-stu-id="6ed10-470">Open ID configuration endpoint URL from where Open ID configuration metadata can be obtained.</span></span> <span data-ttu-id="6ed10-471">Para o Azure Active Directory, use a seguinte URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituindo o seu nome de locatário do diretório, por exemplo, `contoso.onmicrosoft.com`.</span><span class="sxs-lookup"><span data-stu-id="6ed10-471">For Azure Active Directory use the following URL: `https://login.microsoftonline.com/{tenant-name}/.well-known/openid-configuration` substituting your directory tenant name, e.g. `contoso.onmicrosoft.com`.</span></span>|<span data-ttu-id="6ed10-472">Sim</span><span class="sxs-lookup"><span data-stu-id="6ed10-472">Yes</span></span>|<span data-ttu-id="6ed10-473">N/D</span><span class="sxs-lookup"><span data-stu-id="6ed10-473">N/A</span></span>|  
  
### <a name="usage"></a><span data-ttu-id="6ed10-474">Uso</span><span class="sxs-lookup"><span data-stu-id="6ed10-474">Usage</span></span>  
 <span data-ttu-id="6ed10-475">Essa política pode ser usada nas [seções](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) e nos [escopos](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes) da política a seguir.</span><span class="sxs-lookup"><span data-stu-id="6ed10-475">This policy can be used in the following policy [sections](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#sections) and [scopes](http://azure.microsoft.com/documentation/articles/api-management-howto-policies/#scopes).</span></span>  
  
-   <span data-ttu-id="6ed10-476">**Seções de política:** de entrada</span><span class="sxs-lookup"><span data-stu-id="6ed10-476">**Policy sections:** inbound</span></span>  
  
-   <span data-ttu-id="6ed10-477">**Escopos de política:** global, produto, API, operação</span><span class="sxs-lookup"><span data-stu-id="6ed10-477">**Policy scopes:** global, product, API, operation</span></span>  
  
## <a name="next-steps"></a><span data-ttu-id="6ed10-478">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="6ed10-478">Next steps</span></span>
<span data-ttu-id="6ed10-479">Para saber mais sobre como trabalhar com políticas, veja [Políticas em Gerenciamento de API](api-management-howto-policies.md).</span><span class="sxs-lookup"><span data-stu-id="6ed10-479">For more information working with policies, see [Policies in API Management](api-management-howto-policies.md).</span></span>  
