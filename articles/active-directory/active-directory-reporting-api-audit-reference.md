---
title: "auditoria de Active Directory aaaAzure Referência de API | Microsoft Docs"
description: Como tooget iniciada com hello API de auditoria do Active Directory do Azure
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
ms.openlocfilehash: 5f33b62ede9be445f35704739e328580dc454368
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-audit-api-reference"></a><span data-ttu-id="96082-103">Referência à API de auditoria do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="96082-103">Azure Active Directory audit API reference</span></span>
<span data-ttu-id="96082-104">Este tópico faz parte de uma coleção de tópicos sobre Olá Active Directory do Azure API de relatório.</span><span class="sxs-lookup"><span data-stu-id="96082-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="96082-105">Relatórios de AD do Azure fornece uma API que permite que você tooaccess dados de auditoria usando o código ou ferramentas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="96082-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="96082-106">escopo de saudação deste tópico é tooprovide você com informações de referência sobre Olá **audit API**.</span><span class="sxs-lookup"><span data-stu-id="96082-106">hello scope of this topic is tooprovide you with reference information about hello **audit API**.</span></span>

<span data-ttu-id="96082-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="96082-107">See:</span></span>

* <span data-ttu-id="96082-108">[Logs de auditoria](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações conceituais</span><span class="sxs-lookup"><span data-stu-id="96082-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>

* <span data-ttu-id="96082-109">[Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) para obter mais informações sobre Olá API de relatório.</span><span class="sxs-lookup"><span data-stu-id="96082-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


<span data-ttu-id="96082-110">Para:</span><span class="sxs-lookup"><span data-stu-id="96082-110">For:</span></span>

- <span data-ttu-id="96082-111">Perguntas frequentes, leia nossas [Perguntas Frequentes](active-directory-reporting-faq.md)</span><span class="sxs-lookup"><span data-stu-id="96082-111">Frequently asked questions, read our [FAQ](active-directory-reporting-faq.md)</span></span> 

- <span data-ttu-id="96082-112">Solucionar problemas, [registre um tíquete de suporte](active-directory-troubleshooting-support-howto.md)</span><span class="sxs-lookup"><span data-stu-id="96082-112">Issues, please [file a support ticket](active-directory-troubleshooting-support-howto.md)</span></span> 


## <a name="who-can-access-hello-data"></a><span data-ttu-id="96082-113">Quem pode acessar dados Olá?</span><span class="sxs-lookup"><span data-stu-id="96082-113">Who can access hello data?</span></span>
* <span data-ttu-id="96082-114">Usuários na função de administrador de segurança ou segurança leitor Olá</span><span class="sxs-lookup"><span data-stu-id="96082-114">Users in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="96082-115">Administradores globais</span><span class="sxs-lookup"><span data-stu-id="96082-115">Global Admins</span></span>
* <span data-ttu-id="96082-116">Qualquer aplicativo que tenha autorização tooaccess Olá API (o autorização de aplicativo pode ser configurado somente com base na permissão do Administrador Global)</span><span class="sxs-lookup"><span data-stu-id="96082-116">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

## <a name="prerequisites"></a><span data-ttu-id="96082-117">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="96082-117">Prerequisites</span></span>
<span data-ttu-id="96082-118">Em ordem tooaccess esse relatório por meio de Olá API de relatório, você deve ter:</span><span class="sxs-lookup"><span data-stu-id="96082-118">In order tooaccess this report through hello Reporting API, you must have:</span></span>

* <span data-ttu-id="96082-119">Um [Azure Active Directory gratuito ou uma edição melhor](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="96082-119">An [Azure Active Directory Free or better edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="96082-120">Olá concluído [pré-requisitos tooaccess Olá AD do Azure reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="96082-120">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="96082-121">Acessando a API de saudação</span><span class="sxs-lookup"><span data-stu-id="96082-121">Accessing hello API</span></span>
<span data-ttu-id="96082-122">É possível acessar essa API por meio de saudação [Gerenciador de gráficos](https://graphexplorer2.cloudapp.net) ou programaticamente, usando, por exemplo, do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="96082-122">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="96082-123">Para toocorrectly PowerShell interpretar a sintaxe de filtro OData Olá usada nas chamadas AAD Graph REST, você deve usar Olá acento (também conhecido como: acento grave) caractere muito "caractere de escape" hello $.</span><span class="sxs-lookup"><span data-stu-id="96082-123">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="96082-124">caractere de acento grave Olá serve como [caractere de escape do PowerShell](https://technet.microsoft.com/library/hh847755.aspx), permitindo que o PowerShell toodo uma interpretação de literal de caractere de $ hello e evitar confundi-lo como um nome de variável do PowerShell (ou seja: $filter).</span><span class="sxs-lookup"><span data-stu-id="96082-124">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="96082-125">Olá foco deste tópico é Olá Gerenciador de gráficos.</span><span class="sxs-lookup"><span data-stu-id="96082-125">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="96082-126">Para obter um exemplo do PowerShell, consulte [scripts do PowerShell](active-directory-reporting-api-audit-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="96082-126">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-audit-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="96082-127">Ponto de extremidade de API</span><span class="sxs-lookup"><span data-stu-id="96082-127">API Endpoint</span></span>
<span data-ttu-id="96082-128">Você pode acessar essa API usando Olá URI a seguir:</span><span class="sxs-lookup"><span data-stu-id="96082-128">You can access this API using hello following URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta

<span data-ttu-id="96082-129">Não há nenhum limite no número de saudação de registros retornados pela API de auditoria de saudação do AD do Azure (usando a paginação do OData).</span><span class="sxs-lookup"><span data-stu-id="96082-129">There is no limit on hello number of records returned by hello Azure AD audit API (using OData pagination).</span></span>
<span data-ttu-id="96082-130">Para conhecer os limites de retenção em dados de relatório, confira [Políticas de retenção de relatório](active-directory-reporting-retention.md).</span><span class="sxs-lookup"><span data-stu-id="96082-130">For retention limits on reporting data, check out [Reporting Retention Policies](active-directory-reporting-retention.md).</span></span>

<span data-ttu-id="96082-131">Essa chamada retorna dados saudação em lotes.</span><span class="sxs-lookup"><span data-stu-id="96082-131">This call returns hello data in batches.</span></span> <span data-ttu-id="96082-132">Cada lote tem no máximo 1000 registros.</span><span class="sxs-lookup"><span data-stu-id="96082-132">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="96082-133">tooget Olá próximo lote de registros, use Olá próximo link.</span><span class="sxs-lookup"><span data-stu-id="96082-133">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="96082-134">Obter informações de token Skip de saudação do primeiro conjunto de registros retornados de saudação.</span><span class="sxs-lookup"><span data-stu-id="96082-134">Get hello skiptoken information from hello first set of returned records.</span></span> <span data-ttu-id="96082-135">símbolo de salto Olá será final Olá Olá do conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="96082-135">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/contoso.com/activities/audit?api-version=beta&%24skiptoken=-1339686058




## <a name="supported-filters"></a><span data-ttu-id="96082-136">Filtros com suporte</span><span class="sxs-lookup"><span data-stu-id="96082-136">Supported filters</span></span>
<span data-ttu-id="96082-137">Você pode reduzir o número de saudação de registros que são retornados por uma API chamada na forma de um filtro.</span><span class="sxs-lookup"><span data-stu-id="96082-137">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="96082-138">Para entrar API dados relacionados, Olá filtros a seguir têm suporte:</span><span class="sxs-lookup"><span data-stu-id="96082-138">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="96082-139">**$top =\<retornado do número de registros toobe\>**  -número de saudação toolimit de registros retornados.</span><span class="sxs-lookup"><span data-stu-id="96082-139">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="96082-140">Esta é uma operação cara.</span><span class="sxs-lookup"><span data-stu-id="96082-140">This is an expensive operation.</span></span> <span data-ttu-id="96082-141">Você não deve usar esse filtro se quiser tooreturn milhares de objetos.</span><span class="sxs-lookup"><span data-stu-id="96082-141">You should not use this filter if you want tooreturn thousands of objects.</span></span>     
* <span data-ttu-id="96082-142">**$filter =\<sua instrução de filtro\>**  -toospecify, cada saudação de campos de filtro com suporte, tipo de saudação de registros que importam</span><span class="sxs-lookup"><span data-stu-id="96082-142">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="96082-143">Campos de filtro e operadores com suporte</span><span class="sxs-lookup"><span data-stu-id="96082-143">Supported filter fields and operators</span></span>
<span data-ttu-id="96082-144">tipo de saudação toospecify de registros importantes para você, você pode criar uma instrução de filtro que pode conter um ou uma combinação de saudação campos de filtro a seguir:</span><span class="sxs-lookup"><span data-stu-id="96082-144">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="96082-145">[activityDate](#activitydate) – define uma data ou intervalo de datas</span><span class="sxs-lookup"><span data-stu-id="96082-145">[activityDate](#activitydate)  - defines a date or date range</span></span>
* <span data-ttu-id="96082-146">[categoria](#category) -define a categoria Olá deseja toofilter no.</span><span class="sxs-lookup"><span data-stu-id="96082-146">[category](#category) - defines hello category you want toofilter on.</span></span>
* <span data-ttu-id="96082-147">[activityStatus](#activitystatus) -define o status de saudação de uma atividade</span><span class="sxs-lookup"><span data-stu-id="96082-147">[activityStatus](#activitystatus) - defines hello status of an activity</span></span>
* <span data-ttu-id="96082-148">[activityType](#activitytype) -define o tipo de saudação de uma atividade</span><span class="sxs-lookup"><span data-stu-id="96082-148">[activityType](#activitytype)  - defines hello type of an activity</span></span>
* <span data-ttu-id="96082-149">[atividade](#activity) -define atividade hello como cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="96082-149">[activity](#activity) - defines hello activity as string</span></span>  
* <span data-ttu-id="96082-150">[nome do ator](#actorname) -define ator Olá na forma de nome do ator Olá</span><span class="sxs-lookup"><span data-stu-id="96082-150">[actor/name](#actorname) -   defines hello actor in form of hello actor's name</span></span>
* <span data-ttu-id="96082-151">[ator/objectid](#actorobjectid) -define ator Olá na forma de ID do ator Olá</span><span class="sxs-lookup"><span data-stu-id="96082-151">[actor/objectid](#actorobjectid) - defines hello actor in form of hello actor's ID</span></span>   
* <span data-ttu-id="96082-152">[ator/upn](#actorupn) -define ator Olá no formulário princípio do ator Olá nome de usuário (UPN)</span><span class="sxs-lookup"><span data-stu-id="96082-152">[actor/upn](#actorupn)  - defines hello actor in form of hello actor's user principle name (UPN)</span></span> 
* <span data-ttu-id="96082-153">[nome do destino](#targetname) -define o destino de saudação na forma de nome do ator Olá</span><span class="sxs-lookup"><span data-stu-id="96082-153">[target/name](#targetname)  - defines hello target in form of hello actor's name</span></span>
* <span data-ttu-id="96082-154">[destino/objectid](#targetobjectid) -define o destino de saudação na forma de ID do destino Olá</span><span class="sxs-lookup"><span data-stu-id="96082-154">[target/objectid](#targetobjectid) - defines hello target in form of hello target's ID</span></span>  
* <span data-ttu-id="96082-155">[destino/upn](#targetupn) -define ator Olá no formulário princípio do ator Olá nome de usuário (UPN)</span><span class="sxs-lookup"><span data-stu-id="96082-155">[target/upn](#targetupn) - defines hello actor in form of hello actor's user principle name (UPN)</span></span>   

- - -
### <a name="activitydate"></a><span data-ttu-id="96082-156">activityDate</span><span class="sxs-lookup"><span data-stu-id="96082-156">activityDate</span></span>
<span data-ttu-id="96082-157">**Operadores com suporte**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="96082-157">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="96082-158">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="96082-158">**Example**:</span></span>

    $filter=tdomain + 'activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago    

<span data-ttu-id="96082-159">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="96082-159">**Notes**:</span></span>

<span data-ttu-id="96082-160">datetime deve estar no formato UTC</span><span class="sxs-lookup"><span data-stu-id="96082-160">datetime should be in UTC format</span></span>

- - -
### <a name="category"></a><span data-ttu-id="96082-161">categoria</span><span class="sxs-lookup"><span data-stu-id="96082-161">category</span></span>

<span data-ttu-id="96082-162">**Valores com suporte**:</span><span class="sxs-lookup"><span data-stu-id="96082-162">**Supported values**:</span></span>

| <span data-ttu-id="96082-163">Categoria</span><span class="sxs-lookup"><span data-stu-id="96082-163">Category</span></span>                         | <span data-ttu-id="96082-164">Valor</span><span class="sxs-lookup"><span data-stu-id="96082-164">Value</span></span>     |
| :--                              | ---       |
| <span data-ttu-id="96082-165">Diretório principal</span><span class="sxs-lookup"><span data-stu-id="96082-165">Core Directory</span></span>                   | <span data-ttu-id="96082-166">Diretório</span><span class="sxs-lookup"><span data-stu-id="96082-166">Directory</span></span> |
| <span data-ttu-id="96082-167">Gerenciamento de senhas de auto-atendimento</span><span class="sxs-lookup"><span data-stu-id="96082-167">Self-service Password Management</span></span> | <span data-ttu-id="96082-168">SSPR</span><span class="sxs-lookup"><span data-stu-id="96082-168">SSPR</span></span>      |
| <span data-ttu-id="96082-169">Gerenciamento de grupos de autoatendimento</span><span class="sxs-lookup"><span data-stu-id="96082-169">Self-service Group Management</span></span>    | <span data-ttu-id="96082-170">SSGM</span><span class="sxs-lookup"><span data-stu-id="96082-170">SSGM</span></span>      |
| <span data-ttu-id="96082-171">Provisionamento de conta de usuário</span><span class="sxs-lookup"><span data-stu-id="96082-171">Account Provisioning</span></span>             | <span data-ttu-id="96082-172">Sincronizar</span><span class="sxs-lookup"><span data-stu-id="96082-172">Sync</span></span>      |
| <span data-ttu-id="96082-173">Substituição de senha automática</span><span class="sxs-lookup"><span data-stu-id="96082-173">Automated Password Rollover</span></span>      | <span data-ttu-id="96082-174">Substituição de senha automática</span><span class="sxs-lookup"><span data-stu-id="96082-174">Automated Password Rollover</span></span> |
| <span data-ttu-id="96082-175">Identity Protection</span><span class="sxs-lookup"><span data-stu-id="96082-175">Identity Protection</span></span>              | <span data-ttu-id="96082-176">IdentityProtection</span><span class="sxs-lookup"><span data-stu-id="96082-176">IdentityProtection</span></span> |
| <span data-ttu-id="96082-177">Usuários Convidados</span><span class="sxs-lookup"><span data-stu-id="96082-177">Invited Users</span></span>                    | <span data-ttu-id="96082-178">Usuários Convidados</span><span class="sxs-lookup"><span data-stu-id="96082-178">Invited Users</span></span> |
| <span data-ttu-id="96082-179">Serviço MIM</span><span class="sxs-lookup"><span data-stu-id="96082-179">MIM Service</span></span>                      | <span data-ttu-id="96082-180">Serviço MIM</span><span class="sxs-lookup"><span data-stu-id="96082-180">MIM Service</span></span> |



<span data-ttu-id="96082-181">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="96082-181">**Supported operators**: eq</span></span>

<span data-ttu-id="96082-182">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="96082-182">**Example**:</span></span>

    $filter=category eq 'SSPR'
- - -
### <a name="activitystatus"></a><span data-ttu-id="96082-183">activityStatus</span><span class="sxs-lookup"><span data-stu-id="96082-183">activityStatus</span></span>

<span data-ttu-id="96082-184">**Valores com suporte**:</span><span class="sxs-lookup"><span data-stu-id="96082-184">**Supported values**:</span></span>

| <span data-ttu-id="96082-185">Status da Atividade</span><span class="sxs-lookup"><span data-stu-id="96082-185">Activity Status</span></span> | <span data-ttu-id="96082-186">Valor</span><span class="sxs-lookup"><span data-stu-id="96082-186">Value</span></span> |
| :--             | ---   |
| <span data-ttu-id="96082-187">Sucesso</span><span class="sxs-lookup"><span data-stu-id="96082-187">Success</span></span>         | <span data-ttu-id="96082-188">0</span><span class="sxs-lookup"><span data-stu-id="96082-188">0</span></span>     |
| <span data-ttu-id="96082-189">Failure</span><span class="sxs-lookup"><span data-stu-id="96082-189">Failure</span></span>         | <span data-ttu-id="96082-190">- 1</span><span class="sxs-lookup"><span data-stu-id="96082-190">- 1</span></span>   |

<span data-ttu-id="96082-191">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="96082-191">**Supported operators**: eq</span></span>

<span data-ttu-id="96082-192">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="96082-192">**Example**:</span></span>

    $filter=activityStatus eq -1    

---
### <a name="activitytype"></a><span data-ttu-id="96082-193">activityType</span><span class="sxs-lookup"><span data-stu-id="96082-193">activityType</span></span>
<span data-ttu-id="96082-194">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="96082-194">**Supported operators**: eq</span></span>

<span data-ttu-id="96082-195">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="96082-195">**Example**:</span></span>

    $filter=activityType eq 'User'    

<span data-ttu-id="96082-196">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="96082-196">**Notes**:</span></span>

<span data-ttu-id="96082-197">diferencia maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="96082-197">case-sensitive</span></span>

- - -
### <a name="activity"></a><span data-ttu-id="96082-198">activity</span><span class="sxs-lookup"><span data-stu-id="96082-198">activity</span></span>
<span data-ttu-id="96082-199">**Suporte para operadores**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="96082-199">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="96082-200">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="96082-200">**Example**:</span></span>

    $filter=activity eq 'Add application' or contains(activity, 'Application') or startsWith(activity, 'Add')    

<span data-ttu-id="96082-201">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="96082-201">**Notes**:</span></span>

<span data-ttu-id="96082-202">diferencia maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="96082-202">case-sensitive</span></span>

- - -
### <a name="actorname"></a><span data-ttu-id="96082-203">actor/name</span><span class="sxs-lookup"><span data-stu-id="96082-203">actor/name</span></span>
<span data-ttu-id="96082-204">**Suporte para operadores**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="96082-204">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="96082-205">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="96082-205">**Example**:</span></span>

    $filter=actor/name eq 'test' or contains(actor/name, 'test') or startswith(actor/name, 'test')    

<span data-ttu-id="96082-206">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="96082-206">**Notes**:</span></span>

<span data-ttu-id="96082-207">não diferenciam maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="96082-207">case-insensitive</span></span>

- - -
### <a name="actorobjectid"></a><span data-ttu-id="96082-208">actor/objectid</span><span class="sxs-lookup"><span data-stu-id="96082-208">actor/objectId</span></span>
<span data-ttu-id="96082-209">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="96082-209">**Supported operators**: eq</span></span>

<span data-ttu-id="96082-210">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="96082-210">**Example**:</span></span>

    $filter=actor/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba'    


- - -
### <a name="targetname"></a><span data-ttu-id="96082-211">target/name</span><span class="sxs-lookup"><span data-stu-id="96082-211">target/name</span></span>
<span data-ttu-id="96082-212">**Suporte para operadores**: eq, contains, startsWith</span><span class="sxs-lookup"><span data-stu-id="96082-212">**Supported operators**: eq, contains, startsWith</span></span>

<span data-ttu-id="96082-213">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="96082-213">**Example**:</span></span>

    $filter=targets/any(t: t/name eq 'some name')    

<span data-ttu-id="96082-214">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="96082-214">**Notes**:</span></span>

<span data-ttu-id="96082-215">não diferenciam maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="96082-215">Case-insensitive</span></span>

- - -
### <a name="targetupn"></a><span data-ttu-id="96082-216">target/upn</span><span class="sxs-lookup"><span data-stu-id="96082-216">target/upn</span></span>
<span data-ttu-id="96082-217">**Suporte para operadores**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="96082-217">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="96082-218">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="96082-218">**Example**:</span></span>

    $filter=targets/any(t: startswith(t/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity/userPrincipalName,'abc'))    

<span data-ttu-id="96082-219">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="96082-219">**Notes**:</span></span>

* <span data-ttu-id="96082-220">não diferenciam maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="96082-220">Case-insensitive</span></span>
* <span data-ttu-id="96082-221">Você precisará tooadd Olá completo namespace ao consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span><span class="sxs-lookup"><span data-stu-id="96082-221">You need tooadd hello full namespace when querying  Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.TargetResourceUserEntity</span></span>

- - -
### <a name="targetobjectid"></a><span data-ttu-id="96082-222">target/objectid</span><span class="sxs-lookup"><span data-stu-id="96082-222">target/objectId</span></span>
<span data-ttu-id="96082-223">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="96082-223">**Supported operators**: eq</span></span>

<span data-ttu-id="96082-224">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="96082-224">**Example**:</span></span>

    $filter=targets/any(t: t/objectId eq 'e8096343-86a2-4384-b43a-ebfdb17600ba')    

- - -
### <a name="actorupn"></a><span data-ttu-id="96082-225">ator/upn</span><span class="sxs-lookup"><span data-stu-id="96082-225">actor/upn</span></span>
<span data-ttu-id="96082-226">**Suporte para operadores**: eq, startsWith</span><span class="sxs-lookup"><span data-stu-id="96082-226">**Supported operators**: eq, startsWith</span></span>

<span data-ttu-id="96082-227">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="96082-227">**Example**:</span></span>

    $filter=startswith(actor/Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity/userPrincipalName,'abc')    

<span data-ttu-id="96082-228">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="96082-228">**Notes**:</span></span>

* <span data-ttu-id="96082-229">não diferenciam maiúsculas de minúsculas</span><span class="sxs-lookup"><span data-stu-id="96082-229">Case-insensitive</span></span> 
* <span data-ttu-id="96082-230">Você precisará tooadd Olá completo namespace ao consultar Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span><span class="sxs-lookup"><span data-stu-id="96082-230">You need tooadd hello full namespace when querying Microsoft.ActiveDirectory.DataService.PublicApi.Model.Reporting.AuditLog.ActorUserEntity</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="96082-231">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="96082-231">Next Steps</span></span>
* <span data-ttu-id="96082-232">Você deseja toosee exemplos para atividades de sistema filtrado?</span><span class="sxs-lookup"><span data-stu-id="96082-232">Do you want toosee examples for filtered system activities?</span></span> <span data-ttu-id="96082-233">Check-out Olá [exemplos de API de auditoria do Active Directory do Azure](active-directory-reporting-api-audit-samples.md).</span><span class="sxs-lookup"><span data-stu-id="96082-233">Check out hello [Azure Active Directory audit API samples](active-directory-reporting-api-audit-samples.md).</span></span>
* <span data-ttu-id="96082-234">Você deseja tooknow mais sobre a API de relatório de saudação do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="96082-234">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="96082-235">Consulte [Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="96082-235">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

