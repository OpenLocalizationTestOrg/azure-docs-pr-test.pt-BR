---
title: "relatório de atividade aaaAzure sign-in do Active Directory referência de API | Microsoft Docs"
description: "Referência para o relatório de atividade de saudação do Active Directory do Azure entrar API"
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: ddcd9ae0-f6b7-4f13-a5e1-6cbf51a25634
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 8123f308a291503f2c61ac5de26696806c6402ba
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="813a6-103">Referência da API de relatório de atividade de entrada do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="813a6-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="813a6-104">Este tópico faz parte de uma coleção de tópicos sobre Olá Active Directory do Azure API de relatório.</span><span class="sxs-lookup"><span data-stu-id="813a6-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="813a6-105">Relatórios de AD do Azure fornece uma API que permite que você tooaccess dados de relatório de atividade de entrada usando o código ou ferramentas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="813a6-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="813a6-106">escopo de saudação deste tópico é tooprovide você com informações de referência sobre Olá **API de relatório de atividade de entrada**.</span><span class="sxs-lookup"><span data-stu-id="813a6-106">hello scope of this topic is tooprovide you with reference information about hello **sign-in activity report API**.</span></span>

<span data-ttu-id="813a6-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="813a6-107">See:</span></span>

* <span data-ttu-id="813a6-108">[Atividades de entrada](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações conceituais</span><span class="sxs-lookup"><span data-stu-id="813a6-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="813a6-109">[Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) para obter mais informações sobre Olá API de relatório.</span><span class="sxs-lookup"><span data-stu-id="813a6-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="who-can-access-hello-api-data"></a><span data-ttu-id="813a6-110">Quem pode acessar dados de API Olá?</span><span class="sxs-lookup"><span data-stu-id="813a6-110">Who can access hello API data?</span></span>
* <span data-ttu-id="813a6-111">Os usuários e entidades de serviço na função de administrador de segurança ou segurança leitor Olá</span><span class="sxs-lookup"><span data-stu-id="813a6-111">Users and Service Principals in hello Security Admin or Security Reader role</span></span>
* <span data-ttu-id="813a6-112">Administradores globais</span><span class="sxs-lookup"><span data-stu-id="813a6-112">Global Admins</span></span>
* <span data-ttu-id="813a6-113">Qualquer aplicativo que tenha autorização tooaccess Olá API (o autorização de aplicativo pode ser configurado somente com base na permissão do Administrador Global)</span><span class="sxs-lookup"><span data-stu-id="813a6-113">Any app that has authorization tooaccess hello API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="813a6-114">acesso de tooconfigure para um aplicativo tooaccess segurança APIs como eventos de entrada, Olá use aplicativos de saudação do PowerShell tooadd entidade de serviço a seguir à função de leitor de segurança Olá</span><span class="sxs-lookup"><span data-stu-id="813a6-114">tooconfigure access for an application tooaccess security APIs such as signin events, use hello following PowerShell tooadd hello applications Service Principal into hello Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="813a6-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="813a6-115">Prerequisites</span></span>
<span data-ttu-id="813a6-116">Esse relatório por meio de tooaccess Olá API de relatório, você deve ter:</span><span class="sxs-lookup"><span data-stu-id="813a6-116">tooaccess this report through hello reporting API, you must have:</span></span>

* <span data-ttu-id="813a6-117">Um [Azure Active Directory Premium edição P1 ou P2](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="813a6-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="813a6-118">Olá concluído [pré-requisitos tooaccess Olá AD do Azure reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="813a6-118">Completed hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-hello-api"></a><span data-ttu-id="813a6-119">Acessando a API de saudação</span><span class="sxs-lookup"><span data-stu-id="813a6-119">Accessing hello API</span></span>
<span data-ttu-id="813a6-120">É possível acessar essa API por meio de saudação [Gerenciador de gráficos](https://graphexplorer2.cloudapp.net) ou programaticamente, usando, por exemplo, do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="813a6-120">You can either access this API through hello [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="813a6-121">Para toocorrectly PowerShell interpretar a sintaxe de filtro OData Olá usada nas chamadas AAD Graph REST, você deve usar Olá acento (também conhecido como: acento grave) caractere muito "caractere de escape" hello $.</span><span class="sxs-lookup"><span data-stu-id="813a6-121">In order for PowerShell toocorrectly interpret hello OData filter syntax used in AAD Graph REST calls, you must use hello backtick (aka: grave accent) character too“escape” hello $ character.</span></span> <span data-ttu-id="813a6-122">caractere de acento grave Olá serve como [caractere de escape do PowerShell](https://technet.microsoft.com/library/hh847755.aspx), permitindo que o PowerShell toodo uma interpretação de literal de caractere de $ hello e evitar confundi-lo como um nome de variável do PowerShell (ou seja: $filter).</span><span class="sxs-lookup"><span data-stu-id="813a6-122">hello backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell toodo a literal interpretation of hello $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="813a6-123">Olá foco deste tópico é Olá Gerenciador de gráficos.</span><span class="sxs-lookup"><span data-stu-id="813a6-123">hello focus of this topic is on hello Graph Explorer.</span></span> <span data-ttu-id="813a6-124">Para obter um exemplo do PowerShell, consulte [scripts do PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="813a6-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="813a6-125">Ponto de extremidade de API</span><span class="sxs-lookup"><span data-stu-id="813a6-125">API Endpoint</span></span>
<span data-ttu-id="813a6-126">Você pode acessar essa API usando Olá URI de base a seguir:</span><span class="sxs-lookup"><span data-stu-id="813a6-126">You can access this API using hello following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="813a6-127">Devido a toohello o volume de dados, essa API tem um limite de um milhão de registros retornados.</span><span class="sxs-lookup"><span data-stu-id="813a6-127">Due toohello volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="813a6-128">Essa chamada retorna dados saudação em lotes.</span><span class="sxs-lookup"><span data-stu-id="813a6-128">This call returns hello data in batches.</span></span> <span data-ttu-id="813a6-129">Cada lote tem no máximo 1000 registros.</span><span class="sxs-lookup"><span data-stu-id="813a6-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="813a6-130">tooget Olá próximo lote de registros, use Olá próximo link.</span><span class="sxs-lookup"><span data-stu-id="813a6-130">tooget hello next batch of records, use hello Next link.</span></span> <span data-ttu-id="813a6-131">Obter Olá [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) informações do primeiro conjunto de registros retornados de saudação.</span><span class="sxs-lookup"><span data-stu-id="813a6-131">Get hello [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from hello first set of returned records.</span></span> <span data-ttu-id="813a6-132">símbolo de salto Olá será final Olá Olá do conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="813a6-132">hello skip token will be at hello end of hello result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="813a6-133">Filtros com suporte</span><span class="sxs-lookup"><span data-stu-id="813a6-133">Supported filters</span></span>
<span data-ttu-id="813a6-134">Você pode reduzir o número de saudação de registros que são retornados por uma API chamada na forma de um filtro.</span><span class="sxs-lookup"><span data-stu-id="813a6-134">You can narrow down hello number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="813a6-135">Para entrar API dados relacionados, Olá filtros a seguir têm suporte:</span><span class="sxs-lookup"><span data-stu-id="813a6-135">For sign-in API related data, hello following filters are supported:</span></span>

* <span data-ttu-id="813a6-136">**$top =\<retornado do número de registros toobe\>**  -número de saudação toolimit de registros retornados.</span><span class="sxs-lookup"><span data-stu-id="813a6-136">**$top=\<number of records toobe returned\>** - toolimit hello number of returned records.</span></span> <span data-ttu-id="813a6-137">Esta é uma operação cara.</span><span class="sxs-lookup"><span data-stu-id="813a6-137">This is an expensive operation.</span></span> <span data-ttu-id="813a6-138">Você não deve usar esse filtro se quiser tooreturn milhares de objetos.</span><span class="sxs-lookup"><span data-stu-id="813a6-138">You should not use this filter if you want tooreturn thousands of objects.</span></span>  
* <span data-ttu-id="813a6-139">**$filter =\<sua instrução de filtro\>**  -toospecify, cada saudação de campos de filtro com suporte, tipo de saudação de registros que importam</span><span class="sxs-lookup"><span data-stu-id="813a6-139">**$filter=\<your filter statement\>** - toospecify, on hello basis of supported filter fields, hello type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="813a6-140">Campos de filtro e operadores com suporte</span><span class="sxs-lookup"><span data-stu-id="813a6-140">Supported filter fields and operators</span></span>
<span data-ttu-id="813a6-141">tipo de saudação toospecify de registros importantes para você, você pode criar uma instrução de filtro que pode conter um ou uma combinação de saudação campos de filtro a seguir:</span><span class="sxs-lookup"><span data-stu-id="813a6-141">toospecify hello type of records you care about, you can build a filter statement that can contain either one or a combination of hello following filter fields:</span></span>

* <span data-ttu-id="813a6-142">[signinDateTime](#signindatetime) – Define uma data ou intervalo de datas</span><span class="sxs-lookup"><span data-stu-id="813a6-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="813a6-143">[userId](#userid) -define a ID. do usuário de saudação um usuário específico com base</span><span class="sxs-lookup"><span data-stu-id="813a6-143">[userId](#userid) - defines a specific user based hello user's ID.</span></span>
* <span data-ttu-id="813a6-144">[userPrincipalName](#userprincipalname) -define o nome principal do usuário de saudação um usuário específico com base em usuário (UPN)</span><span class="sxs-lookup"><span data-stu-id="813a6-144">[userPrincipalName](#userprincipalname) - defines a specific user based hello user's user principal name (UPN)</span></span>
* <span data-ttu-id="813a6-145">[appId](#appid) -define a ID do aplicativo hello um aplicativo específico com base em</span><span class="sxs-lookup"><span data-stu-id="813a6-145">[appId](#appid) - defines a specific app based hello app's ID</span></span>
* <span data-ttu-id="813a6-146">[appDisplayName](#appdisplayname) -define o nome para exibição do aplicativo hello um aplicativo específico com base em</span><span class="sxs-lookup"><span data-stu-id="813a6-146">[appDisplayName](#appdisplayname) - defines a specific app based hello app's display name</span></span>
* <span data-ttu-id="813a6-147">[status de logon](#loginStatus) -define o status de saudação de logons de saudação (êxito / falha)</span><span class="sxs-lookup"><span data-stu-id="813a6-147">[loginStatus](#loginStatus) - defines hello status of hello logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="813a6-148">Ao usar o Gerenciador de gráficos, você Olá necessário toouse Olá correto para cada letra é seus campos de filtro.</span><span class="sxs-lookup"><span data-stu-id="813a6-148">When using Graph Explorer, you hello need toouse hello correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="813a6-149">toonarrow escopo de saudação da saudação retornada dados, você pode criar combinações de filtros de saudação com suporte e os campos de filtro.</span><span class="sxs-lookup"><span data-stu-id="813a6-149">toonarrow down hello scope of hello returned data, you can build combinations of hello supported filters and filter fields.</span></span> <span data-ttu-id="813a6-150">Por exemplo, hello instrução a seguir retorna Olá top 10 registros entre 1º de julho de 2016 e 6 de julho de 2016:</span><span class="sxs-lookup"><span data-stu-id="813a6-150">For example, hello following statement returns hello top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="813a6-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="813a6-151">signinDateTime</span></span>
<span data-ttu-id="813a6-152">**Operadores com suporte**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="813a6-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="813a6-153">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="813a6-153">**Example**:</span></span>

<span data-ttu-id="813a6-154">Como usar uma data específica</span><span class="sxs-lookup"><span data-stu-id="813a6-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="813a6-155">Como usar um intervalo de datas</span><span class="sxs-lookup"><span data-stu-id="813a6-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="813a6-156">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="813a6-156">**Notes**:</span></span>

<span data-ttu-id="813a6-157">Olá datetime deveria estar no formato UTC de saudação</span><span class="sxs-lookup"><span data-stu-id="813a6-157">hello datetime parameter should be in hello UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="813a6-158">userId</span><span class="sxs-lookup"><span data-stu-id="813a6-158">userId</span></span>
<span data-ttu-id="813a6-159">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="813a6-159">**Supported operators**: eq</span></span>

<span data-ttu-id="813a6-160">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="813a6-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="813a6-161">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="813a6-161">**Notes**:</span></span>

<span data-ttu-id="813a6-162">valor de saudação do userId é um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="813a6-162">hello value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="813a6-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="813a6-163">userPrincipalName</span></span>
<span data-ttu-id="813a6-164">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="813a6-164">**Supported operators**: eq</span></span>

<span data-ttu-id="813a6-165">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="813a6-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="813a6-166">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="813a6-166">**Notes**:</span></span>

<span data-ttu-id="813a6-167">valor de saudação do userPrincipalName é um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="813a6-167">hello value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="813a6-168">appId</span><span class="sxs-lookup"><span data-stu-id="813a6-168">appId</span></span>
<span data-ttu-id="813a6-169">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="813a6-169">**Supported operators**: eq</span></span>

<span data-ttu-id="813a6-170">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="813a6-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="813a6-171">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="813a6-171">**Notes**:</span></span>

<span data-ttu-id="813a6-172">valor de saudação do appId é um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="813a6-172">hello value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="813a6-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="813a6-173">appDisplayName</span></span>
<span data-ttu-id="813a6-174">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="813a6-174">**Supported operators**: eq</span></span>

<span data-ttu-id="813a6-175">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="813a6-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="813a6-176">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="813a6-176">**Notes**:</span></span>

<span data-ttu-id="813a6-177">valor de saudação do appDisplayName é um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="813a6-177">hello value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="813a6-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="813a6-178">loginStatus</span></span>
<span data-ttu-id="813a6-179">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="813a6-179">**Supported operators**: eq</span></span>

<span data-ttu-id="813a6-180">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="813a6-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="813a6-181">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="813a6-181">**Notes**:</span></span>

<span data-ttu-id="813a6-182">Há duas opções para o status de logon Olá: 0 - êxito, 1 - Falha</span><span class="sxs-lookup"><span data-stu-id="813a6-182">There are two options for hello loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="813a6-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="813a6-183">Next steps</span></span>
* <span data-ttu-id="813a6-184">Você deseja toosee exemplos para atividades filtradas entrar?</span><span class="sxs-lookup"><span data-stu-id="813a6-184">Do you want toosee examples for filtered sign-in activities?</span></span> <span data-ttu-id="813a6-185">Check-out Olá [exemplos de API de relatório de atividade de entrada do Active Directory do Azure](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="813a6-185">Check out hello [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="813a6-186">Você deseja tooknow mais sobre a API de relatório de saudação do AD do Azure?</span><span class="sxs-lookup"><span data-stu-id="813a6-186">Do you want tooknow more about hello Azure AD reporting API?</span></span> <span data-ttu-id="813a6-187">Consulte [Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="813a6-187">See [Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

