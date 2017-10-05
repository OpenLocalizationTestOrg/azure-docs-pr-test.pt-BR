---
title: "Referência à API de auditoria do Azure Active Directory | Microsoft Docs"
description: "Como começar a usar a API de auditoria do Azure Active Directory"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: 44e46be8-09e5-4981-be2b-d474aaa92792
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/05/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 573e940c5390e7b990d889681eb37b73c5b253d9
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="1eec7-103">Referência à API de auditoria do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="1eec7-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="1eec7-104">Este tópico faz parte de uma coleção de tópicos sobre a API de relatório do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="1eec7-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="1eec7-105">Os relatórios do Azure AD fornecem uma API que permite a você acessar dados de auditoria usando código ou ferramentas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="1eec7-105">Azure AD reporting provides you with an API that enables you to access audit data using code or related tools.</span></span>
<span data-ttu-id="1eec7-106">O escopo deste tópico é fornecer informações de referência sobre a **API de auditoria**.</span><span class="sxs-lookup"><span data-stu-id="1eec7-106">The scope of this topic is to provide you with reference information about the **audit API**.</span></span>

<span data-ttu-id="1eec7-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="1eec7-107">See:</span></span>

* <span data-ttu-id="1eec7-108">[Logs de auditoria](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações conceituais</span><span class="sxs-lookup"><span data-stu-id="1eec7-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="1eec7-109">[Introdução à API de relatório do Azure Active Directory](active-directory-reporting-api-getting-started.md) para saber mais sobre a API de relatório.</span><span class="sxs-lookup"><span data-stu-id="1eec7-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


<span data-ttu-id="1eec7-110">Para:</span><span class="sxs-lookup"><span data-stu-id="1eec7-110">For:</span></span>

- <span data-ttu-id="1eec7-111">Perguntas frequentes, leia nossas [Perguntas Frequentes](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="1eec7-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="1eec7-112">Solucionar problemas, [registre um tíquete de suporte](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="1eec7-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-the-data"></a><span data-ttu-id="1eec7-113">Quem pode acessar os dados?</span><span class="sxs-lookup"><span data-stu-id="1eec7-113">Who can access the data?</span></span>
* <span data-ttu-id="1eec7-114">Usuários na função de Administrador de segurança ou Leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="1eec7-114">Users in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="1eec7-115">Administradores globais</span><span class="sxs-lookup"><span data-stu-id="1eec7-115">Global Admins</span></span>
* <span data-ttu-id="1eec7-116">Qualquer aplicativo que tenha autorização para acessar a API (a autorização do aplicativo pode ser definida somente com base na permissão de Administrador Global)</span><span class="sxs-lookup"><span data-stu-id="1eec7-116">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1eec7-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1eec7-117">Prerequisites</span></span>
<span data-ttu-id="1eec7-118">Para acessar esse relatório por meio da API de relatórios, você deve ter:</span><span class="sxs-lookup"><span data-stu-id="1eec7-118">In order to access this report through the Reporting API, you must have:</span></span>

* <span data-ttu-id="1eec7-119">Um [Azure Active Directory gratuito ou uma edição melhor](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="1eec7-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="1eec7-120">Concluído os [pré-requisitos para acessar a API de relatório do Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="1eec7-120">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="1eec7-121">Como acessar a API</span><span class="sxs-lookup"><span data-stu-id="1eec7-121">Accessing the API</span></span>
<span data-ttu-id="1eec7-122">Você pode acessar essa API por meio de [Graph Explorer](https://graphexplorer2.cloudapp.net) ou usando programaticamente, por exemplo, o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="1eec7-122">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="1eec7-123">Para o PowerShell interpretar corretamente a sintaxe de filtro OData usada nas chamadas REST Graph do AAD, você deve usar o caractere de acento grave para "escapar" o caractere $.</span><span class="sxs-lookup"><span data-stu-id="1eec7-123">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="1eec7-124">O caractere de acento grave serve como [caractere de escape do PowerShell](https://technet.microsoft.com/library/hh847755.aspx), permitindo que o PowerShell faça uma interpretação literal do caractere $ e evite confundi-lo como um nome de variável do PowerShell (ou seja: $filter).</span><span class="sxs-lookup"><span data-stu-id="1eec7-124">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="1eec7-125">O foco deste tópico é no Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="1eec7-125">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="1eec7-126">Para obter um exemplo do PowerShell, consulte [scripts do PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="1eec7-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="1eec7-127">Ponto de extremidade de API</span><span class="sxs-lookup"><span data-stu-id="1eec7-127">API Endpoint</span></span>
<span data-ttu-id="1eec7-128">Você pode acessar essa API usando o seguinte URI:</span><span class="sxs-lookup"><span data-stu-id="1eec7-128">You can access this API using the following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="1eec7-129">Não há qualquer limite para o número de registros retornados pela API de auditoria do Azure AD (usando a paginação de OData).</span><span class="sxs-lookup"><span data-stu-id="1eec7-129">There is no limit on the number of records returned by the Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="1eec7-130">Para conhecer os limites de retenção em dados de relatório, confira [Políticas de retenção de relatório](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="1eec7-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="1eec7-131">Essa chamada retorna os dados em lotes.</span><span class="sxs-lookup"><span data-stu-id="1eec7-131">This call returns the data in batches.</span></span> <span data-ttu-id="1eec7-132">Cada lote tem no máximo 1000 registros.</span><span class="sxs-lookup"><span data-stu-id="1eec7-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="1eec7-133">Para obter o próximo lote de registros, use o link Próximo.</span><span class="sxs-lookup"><span data-stu-id="1eec7-133">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="1eec7-134">Obtenha as informações de skiptoken do primeiro conjunto de registros retornados.</span><span class="sxs-lookup"><span data-stu-id="1eec7-134">Get the skiptoken information from the first set of returned records.</span></span> <span data-ttu-id="1eec7-135">O token skip estará no final do conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="1eec7-135">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="1eec7-136">Filtros com suporte</span><span class="sxs-lookup"><span data-stu-id="1eec7-136">Supported filters</span></span>
<span data-ttu-id="1eec7-137">Você pode reduzir o número de registros retornados por uma chamada de API na forma de um filtro.</span><span class="sxs-lookup"><span data-stu-id="1eec7-137">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="1eec7-138">Para entrar dados de entrada relacionados à API, os filtros a seguir recebem suporte:</span><span class="sxs-lookup"><span data-stu-id="1eec7-138">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="1eec7-139">**$top=\<número de registros a serem retornados\>** – para limitar o número de registros retornados.</span><span class="sxs-lookup"><span data-stu-id="1eec7-139">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="1eec7-140">Esta é uma operação cara.</span><span class="sxs-lookup"><span data-stu-id="1eec7-140">This is an expensive operation.</span></span> <span data-ttu-id="1eec7-141">Não use esse filtro se você quiser retornar milhares de objetos.</span><span class="sxs-lookup"><span data-stu-id="1eec7-141">You should not use this filter if you want to return thousands of objects.</span></span>     
* <span data-ttu-id="1eec7-142">**$filter=\<sua instrução de filtro\>** – para especificar, com base nos campos de filtro com suporte, o tipo de registro com o qual você se preocupa</span><span class="sxs-lookup"><span data-stu-id="1eec7-142">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="1eec7-143">Campos de filtro e operadores com suporte</span><span class="sxs-lookup"><span data-stu-id="1eec7-143">Supported filter fields and operators</span></span>
<span data-ttu-id="1eec7-144">Para especificar o tipo de registro com o qual você se preocupa, compile uma instrução de filtro que possa conter um ou uma combinação dos campos de filtro a seguir:</span><span class="sxs-lookup"><span data-stu-id="1eec7-144">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="1eec7-145">[activityDate](#activitydate) – define uma data ou intervalo de datas</span><span class="sxs-lookup"><span data-stu-id="1eec7-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="1eec7-146">[categoria](#category) – define a categoria pela qual você deseja filtrar.</span><span class="sxs-lookup"><span data-stu-id="1eec7-146">[category](#category) - defines the category you want to filter on.</span></span>
* <span data-ttu-id="1eec7-147">[activityStatus](#activitystatus) – define o status de uma atividade</span><span class="sxs-lookup"><span data-stu-id="1eec7-147">[activityStatus](#activitystatus) - defines the status of an activity</span></span>
* <span data-ttu-id="1eec7-148">[activityType](#activitytype) – define o tipo de uma atividade</span><span class="sxs-lookup"><span data-stu-id="1eec7-148">[activityType](#activitytype)  - defines the type of an activity</span></span>
* <span data-ttu-id="1eec7-149">[activity](#activity) – Define a atividade como uma cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="1eec7-149">[activity](#activity) - defines the activity as string</span></span>  
* <span data-ttu-id="1eec7-150">[actor/name](#actorname) – define o ator na forma de nome do ator</span><span class="sxs-lookup"><span data-stu-id="1eec7-150">[actor/name](#actorname) -   defines the actor in form of the actor's name</span></span>
* <span data-ttu-id="1eec7-151">[actor/objectid](#actorobjectid) – Define o ator na forma da ID do ator</span><span class="sxs-lookup"><span data-stu-id="1eec7-151">[actor/objectid](#actorobjectid) - defines the actor in form of the actor's ID</span></span>   
* <span data-ttu-id="1eec7-152">[ator/upn](#actorupn) – define o ator na forma de nome UPN do ator</span><span class="sxs-lookup"><span data-stu-id="1eec7-152">[actor/upn](#actorupn)  - defines the actor in form of the actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="1eec7-153">[target/name](#targetname) – define o destino na forma de nome do ator</span><span class="sxs-lookup"><span data-stu-id="1eec7-153">[target/name](#targetname)  - defines the target in form of the actor's name</span></span>
* <span data-ttu-id="1eec7-154">[target/objectid](#targetobjectid) – Define o destino na forma de ID do destino</span><span class="sxs-lookup"><span data-stu-id="1eec7-154">[target/objectid](#targetobjectid) - defines the target in form of the target's ID</span></span>  
* <span data-ttu-id="1eec7-155">[target/upn](#targetupn) – Define o ator na forma de UPN (nome principal de usuário) do ator</span><span class="sxs-lookup"><span data-stu-id="1eec7-155">[target/upn](#targetupn) - defines the actor in form of the actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="1eec7-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="1eec7-156">activityDate</span></span>
<span data-ttu-id="1eec7-157">**Operadores com suporte**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="1eec7-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="1eec7-158">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="1eec7-159">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-159">**Notes**:</span></span>

<span data-ttu-id="1eec7-160">datetime deve estar no formato UTC</span><span class="sxs-lookup"><span data-stu-id="1eec7-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="1eec7-161">categoria</span><span class="sxs-lookup"><span data-stu-id="1eec7-161">category</span></span>

<span data-ttu-id="1eec7-162">**Valores com suporte**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-162">**Supported values**:</span></span>

| <span data-ttu-id="1eec7-163">Categoria</span><span class="sxs-lookup"><span data-stu-id="1eec7-163">Category</span></span>                         | <span data-ttu-id="1eec7-164">Valor</span><span class="sxs-lookup"><span data-stu-id="1eec7-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="1eec7-165">Diretório principal</span><span class="sxs-lookup"><span data-stu-id="1eec7-165">Core Directory</span></span>                   | <span data-ttu-id="1eec7-166">Diretório</span><span class="sxs-lookup"><span data-stu-id="1eec7-166">Directory</span></span> |
| <span data-ttu-id="1eec7-167">Gerenciamento de senhas de auto-atendimento</span><span class="sxs-lookup"><span data-stu-id="1eec7-167">Self-service Password Management</span></span> | <span data-ttu-id="1eec7-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="1eec7-168">SSPR</span></span>      |
| <span data-ttu-id="1eec7-169">Gerenciamento de grupos de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="1eec7-169">Self-service Group Management</span></span>    | <span data-ttu-id="1eec7-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="1eec7-170">SSGM</span></span>      |
| <span data-ttu-id="1eec7-171">Provisionamento de conta de usuário</span><span class="sxs-lookup"><span data-stu-id="1eec7-171">Account Provisioning</span></span>             | <span data-ttu-id="1eec7-172">Sincronizar</span><span class="sxs-lookup"><span data-stu-id="1eec7-172">Sync</span></span>      |
| <span data-ttu-id="1eec7-173">Substituição de senha automática</span><span class="sxs-lookup"><span data-stu-id="1eec7-173">Automated Password Rollover</span></span>      | <span data-ttu-id="1eec7-174">Substituição de senha automática</span><span class="sxs-lookup"><span data-stu-id="1eec7-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="1eec7-175">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="1eec7-175">Identity Protection</span></span>              | <span data-ttu-id="1eec7-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="1eec7-176">IdentityProtection</span></span> |
| <span data-ttu-id="1eec7-177">Usuários Convidados</span><span class="sxs-lookup"><span data-stu-id="1eec7-177">Invited Users</span></span>                    | <span data-ttu-id="1eec7-178">Usuários Convidados</span><span class="sxs-lookup"><span data-stu-id="1eec7-178">Invited Users</span></span> |
| <span data-ttu-id="1eec7-179">Serviço MIM</span><span class="sxs-lookup"><span data-stu-id="1eec7-179">MIM Service</span></span>                      | <span data-ttu-id="1eec7-180">Serviço MIM</span><span class="sxs-lookup"><span data-stu-id="1eec7-180">MIM Service</span></span> |



<span data-ttu-id="1eec7-181">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="1eec7-181">**Supported operators**: eq</span></span>

<span data-ttu-id="1eec7-182">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="1eec7-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="1eec7-183">activityStatus</span></span>

<span data-ttu-id="1eec7-184">**Valores com suporte**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-184">**Supported values**:</span></span>

| <span data-ttu-id="1eec7-185">Status da Atividade</span><span class="sxs-lookup"><span data-stu-id="1eec7-185">Activity Status</span></span> | <span data-ttu-id="1eec7-186">Valor</span><span class="sxs-lookup"><span data-stu-id="1eec7-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="1eec7-187">Sucesso</span><span class="sxs-lookup"><span data-stu-id="1eec7-187">Success</span></span>         | <span data-ttu-id="1eec7-188">0</span><span class="sxs-lookup"><span data-stu-id="1eec7-188">0</span></span>     |
| <span data-ttu-id="1eec7-189">Failure</span><span class="sxs-lookup"><span data-stu-id="1eec7-189">Failure</span></span>         | <span data-ttu-id="1eec7-190">- 1</span><span class="sxs-lookup"><span data-stu-id="1eec7-190">- 1</span></span>   |

<span data-ttu-id="1eec7-191">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="1eec7-191">**Supported operators**: eq</span></span>

<span data-ttu-id="1eec7-192">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="1eec7-193">activityType</span><span class="sxs-lookup"><span data-stu-id="1eec7-193">activityType</span></span>
<span data-ttu-id="1eec7-194">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="1eec7-194">**Supported operators**: eq</span></span>

<span data-ttu-id="1eec7-195">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="1eec7-196">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-196">**Notes**:</span></span>

<span data-ttu-id="1eec7-197">diferencia maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="1eec7-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="1eec7-198">activity</span><span class="sxs-lookup"><span data-stu-id="1eec7-198">activity</span></span>
<span data-ttu-id="1eec7-199">**Suporte para operadores**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="1eec7-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="1eec7-200">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="1eec7-201">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-201">**Notes**:</span></span>

<span data-ttu-id="1eec7-202">diferencia maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="1eec7-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="1eec7-203">actor/name</span><span class="sxs-lookup"><span data-stu-id="1eec7-203">actor/name</span></span>
<span data-ttu-id="1eec7-204">**Suporte para operadores**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="1eec7-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="1eec7-205">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="1eec7-206">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-206">**Notes**:</span></span>

<span data-ttu-id="1eec7-207">não diferenciam maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="1eec7-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="1eec7-208">actor/objectid</span><span class="sxs-lookup"><span data-stu-id="1eec7-208">actor/objectId</span></span>
<span data-ttu-id="1eec7-209">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="1eec7-209">**Supported operators**: eq</span></span>

<span data-ttu-id="1eec7-210">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="1eec7-211">target/name</span><span class="sxs-lookup"><span data-stu-id="1eec7-211">target/name</span></span>
<span data-ttu-id="1eec7-212">**Suporte para operadores**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="1eec7-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="1eec7-213">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="1eec7-214">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-214">**Notes**:</span></span>

<span data-ttu-id="1eec7-215">não diferenciam maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="1eec7-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="1eec7-216">target/upn</span><span class="sxs-lookup"><span data-stu-id="1eec7-216">target/upn</span></span>
<span data-ttu-id="1eec7-217">**Suporte para operadores**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="1eec7-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="1eec7-218">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="1eec7-219">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-219">**Notes**:</span></span>

* <span data-ttu-id="1eec7-220">Não diferenciam maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="1eec7-220">Case-insensitive</span></span>
* <span data-ttu-id="1eec7-221">Você precisa adicionar o namespace completo ao consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="1eec7-221">You need to add the full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="1eec7-222">target/objectid</span><span class="sxs-lookup"><span data-stu-id="1eec7-222">target/objectId</span></span>
<span data-ttu-id="1eec7-223">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="1eec7-223">**Supported operators**: eq</span></span>

<span data-ttu-id="1eec7-224">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="1eec7-225">ator/upn</span><span class="sxs-lookup"><span data-stu-id="1eec7-225">actor/upn</span></span>
<span data-ttu-id="1eec7-226">**Suporte para operadores**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="1eec7-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="1eec7-227">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="1eec7-228">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="1eec7-228">**Notes**:</span></span>

* <span data-ttu-id="1eec7-229">não diferenciam maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="1eec7-229">Case-insensitive</span></span> 
* <span data-ttu-id="1eec7-230">Você precisa adicionar o namespace completo ao consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="1eec7-230">You need to add the full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="1eec7-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1eec7-231">Next Steps</span></span>
* <span data-ttu-id="1eec7-232">Quer ver exemplos para atividades do sistema filtradas?</span><span class="sxs-lookup"><span data-stu-id="1eec7-232">Do you want to see examples for filtered system activities?</span></span> <span data-ttu-id="1eec7-233">Confira os [exemplos de API de auditoria do Azure Active Directory](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="1eec7-233">Check out the [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="1eec7-234">Quer saber mais sobre a API de relatório do Azure AD?</span><span class="sxs-lookup"><span data-stu-id="1eec7-234">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="1eec7-235">Confira [Introdução à API de relatório do Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="1eec7-235">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

