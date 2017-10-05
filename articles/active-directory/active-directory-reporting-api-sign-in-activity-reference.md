---
title: "Referência da API de relatório da atividade de entrada do Azure Active Directory | Microsoft Docs"
description: "Referência para a API de relatório de atividade de entrada do Azure Active Directory"
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
ms.openlocfilehash: d83f1a899ba38dab2c1c1661adede87db6f88c20
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-reference"></a><span data-ttu-id="86168-103">Referência da API de relatório de atividade de entrada do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="86168-103">Azure Active Directory sign-in activity report API reference</span></span>
<span data-ttu-id="86168-104">Este tópico faz parte de uma coleção de tópicos sobre a API de relatório do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="86168-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="86168-105">Os relatórios do Azure AD fornecem uma API que permite a você acessar dados de relatórios de atividade de entrada usando código ou ferramentas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="86168-105">Azure AD reporting provides you with an API that enables you to access sign-in activity report data using code or related tools.</span></span>
<span data-ttu-id="86168-106">O escopo deste tópico é fornecer informações de referência sobre a **API de relatório de atividade de entrada**.</span><span class="sxs-lookup"><span data-stu-id="86168-106">The scope of this topic is to provide you with reference information about the **sign-in activity report API**.</span></span>

<span data-ttu-id="86168-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="86168-107">See:</span></span>

* <span data-ttu-id="86168-108">[Atividades de entrada](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações conceituais</span><span class="sxs-lookup"><span data-stu-id="86168-108">[Sign-in activities](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="86168-109">[Introdução à API de relatório do Azure Active Directory](active-directory-reporting-api-getting-started.md) para saber mais sobre a API de relatório.</span><span class="sxs-lookup"><span data-stu-id="86168-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="who-can-access-the-api-data"></a><span data-ttu-id="86168-110">Quem pode acessar os dados da API?</span><span class="sxs-lookup"><span data-stu-id="86168-110">Who can access the API data?</span></span>
* <span data-ttu-id="86168-111">Usuários e Entidades de Serviço na função de Administrador de segurança ou Leitor de segurança</span><span class="sxs-lookup"><span data-stu-id="86168-111">Users and Service Principals in the Security Admin or Security Reader role</span></span>
* <span data-ttu-id="86168-112">Administradores globais</span><span class="sxs-lookup"><span data-stu-id="86168-112">Global Admins</span></span>
* <span data-ttu-id="86168-113">Qualquer aplicativo que tenha autorização para acessar a API (a autorização do aplicativo pode ser definida somente com base na permissão de Administrador Global)</span><span class="sxs-lookup"><span data-stu-id="86168-113">Any app that has authorization to access the API (app authorization can be setup only based on Global Admin’s permission)</span></span>

<span data-ttu-id="86168-114">Para configurar o acesso a um aplicativo para acessar as APIs de segurança, como eventos de entrada, use o PowerShell a seguir para adicionar a entidade de serviço de aplicativos à função do Leitor de Segurança</span><span class="sxs-lookup"><span data-stu-id="86168-114">To configure access for an application to access security APIs such as signin events, use the following PowerShell to add the applications Service Principal into the Security Reader role</span></span>

```PowerShell
Connect-MsolService
$servicePrincipal = Get-MsolServicePrincipal -AppPrincipalId "<app client id>"
$role = Get-MsolRole | ? Name -eq "Security Reader"
Add-MsolRoleMember -RoleObjectId $role.ObjectId -RoleMemberType ServicePrincipal -RoleMemberObjectId $servicePrincipal.ObjectId
```

## <a name="prerequisites"></a><span data-ttu-id="86168-115">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="86168-115">Prerequisites</span></span>
<span data-ttu-id="86168-116">Para acessar esse relatório por meio da API de relatórios, você deve ter:</span><span class="sxs-lookup"><span data-stu-id="86168-116">To access this report through the reporting API, you must have:</span></span>

* <span data-ttu-id="86168-117">Um [Azure Active Directory Premium edição P1 ou P2](active-directory-editions.md)</span><span class="sxs-lookup"><span data-stu-id="86168-117">An [Azure Active Directory Premium P1 or P2 edition](active-directory-editions.md)</span></span>
* <span data-ttu-id="86168-118">Concluído os [pré-requisitos para acessar a API de relatório do Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="86168-118">Completed the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span> 

## <a name="accessing-the-api"></a><span data-ttu-id="86168-119">Como acessar a API</span><span class="sxs-lookup"><span data-stu-id="86168-119">Accessing the API</span></span>
<span data-ttu-id="86168-120">Você pode acessar essa API por meio de [Graph Explorer](https://graphexplorer2.cloudapp.net) ou usando programaticamente, por exemplo, o PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86168-120">You can either access this API through the [Graph Explorer](https://graphexplorer2.cloudapp.net) or programmatically using, for example, PowerShell.</span></span> <span data-ttu-id="86168-121">Para o PowerShell interpretar corretamente a sintaxe de filtro OData usada nas chamadas REST Graph do AAD, você deve usar o caractere de acento grave para "escapar" o caractere $.</span><span class="sxs-lookup"><span data-stu-id="86168-121">In order for PowerShell to correctly interpret the OData filter syntax used in AAD Graph REST calls, you must use the backtick (aka: grave accent) character to “escape” the $ character.</span></span> <span data-ttu-id="86168-122">O caractere de acento grave serve como [caractere de escape do PowerShell](https://technet.microsoft.com/library/hh847755.aspx), permitindo que o PowerShell faça uma interpretação literal do caractere $ e evite confundi-lo como um nome de variável do PowerShell (ou seja: $filter).</span><span class="sxs-lookup"><span data-stu-id="86168-122">The backtick character serves as [PowerShell’s escape character](https://technet.microsoft.com/library/hh847755.aspx), allowing PowerShell to do a literal interpretation of the $ character, and avoid confusing it as a PowerShell variable name (ie: $filter).</span></span>

<span data-ttu-id="86168-123">O foco deste tópico é no Graph Explorer.</span><span class="sxs-lookup"><span data-stu-id="86168-123">The focus of this topic is on the Graph Explorer.</span></span> <span data-ttu-id="86168-124">Para obter um exemplo do PowerShell, consulte [scripts do PowerShell](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span><span class="sxs-lookup"><span data-stu-id="86168-124">For a PowerShell example, see this [PowerShell script](active-directory-reporting-api-sign-in-activity-samples.md#powershell-script).</span></span>

## <a name="api-endpoint"></a><span data-ttu-id="86168-125">Ponto de extremidade de API</span><span class="sxs-lookup"><span data-stu-id="86168-125">API Endpoint</span></span>
<span data-ttu-id="86168-126">Você pode acessar essa API usando o seguinte URI de base:</span><span class="sxs-lookup"><span data-stu-id="86168-126">You can access this API using the following base URI:</span></span>  

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta  



<span data-ttu-id="86168-127">Devido ao volume de dados, essa API tem um limite de um milhão de registros retornados.</span><span class="sxs-lookup"><span data-stu-id="86168-127">Due to the volume of data, this API has a limit of one million returned records.</span></span> 

<span data-ttu-id="86168-128">Essa chamada retorna os dados em lotes.</span><span class="sxs-lookup"><span data-stu-id="86168-128">This call returns the data in batches.</span></span> <span data-ttu-id="86168-129">Cada lote tem no máximo 1000 registros.</span><span class="sxs-lookup"><span data-stu-id="86168-129">Each batch has a maximum of 1000 records.</span></span>  
<span data-ttu-id="86168-130">Para obter o próximo lote de registros, use o link Próximo.</span><span class="sxs-lookup"><span data-stu-id="86168-130">To get the next batch of records, use the Next link.</span></span> <span data-ttu-id="86168-131">Obtenha as informações de [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) do primeiro conjunto de registros retornados.</span><span class="sxs-lookup"><span data-stu-id="86168-131">Get the [skiptoken](https://msdn.microsoft.com/library/dd942121.aspx) information from the first set of returned records.</span></span> <span data-ttu-id="86168-132">O token skip estará no final do conjunto de resultados.</span><span class="sxs-lookup"><span data-stu-id="86168-132">The skip token will be at the end of the result set.</span></span>  

    https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&%24skiptoken=-1339686058


## <a name="supported-filters"></a><span data-ttu-id="86168-133">Filtros com suporte</span><span class="sxs-lookup"><span data-stu-id="86168-133">Supported filters</span></span>
<span data-ttu-id="86168-134">Você pode reduzir o número de registros retornados por uma chamada de API na forma de um filtro.</span><span class="sxs-lookup"><span data-stu-id="86168-134">You can narrow down the number of records that are returned by an API call in form of a filter.</span></span>  
<span data-ttu-id="86168-135">Para entrar dados de entrada relacionados à API, os filtros a seguir recebem suporte:</span><span class="sxs-lookup"><span data-stu-id="86168-135">For sign-in API related data, the following filters are supported:</span></span>

* <span data-ttu-id="86168-136">**$top=\<número de registros a serem retornados\>** – para limitar o número de registros retornados.</span><span class="sxs-lookup"><span data-stu-id="86168-136">**$top=\<number of records to be returned\>** - to limit the number of returned records.</span></span> <span data-ttu-id="86168-137">Esta é uma operação cara.</span><span class="sxs-lookup"><span data-stu-id="86168-137">This is an expensive operation.</span></span> <span data-ttu-id="86168-138">Não use esse filtro se você quiser retornar milhares de objetos.</span><span class="sxs-lookup"><span data-stu-id="86168-138">You should not use this filter if you want to return thousands of objects.</span></span>  
* <span data-ttu-id="86168-139">**$filter=\<sua instrução de filtro\>** – para especificar, com base nos campos de filtro com suporte, o tipo de registro com o qual você se preocupa</span><span class="sxs-lookup"><span data-stu-id="86168-139">**$filter=\<your filter statement\>** - to specify, on the basis of supported filter fields, the type of records you care about</span></span>

## <a name="supported-filter-fields-and-operators"></a><span data-ttu-id="86168-140">Campos de filtro e operadores com suporte</span><span class="sxs-lookup"><span data-stu-id="86168-140">Supported filter fields and operators</span></span>
<span data-ttu-id="86168-141">Para especificar o tipo de registro com o qual você se preocupa, compile uma instrução de filtro que possa conter um ou uma combinação dos campos de filtro a seguir:</span><span class="sxs-lookup"><span data-stu-id="86168-141">To specify the type of records you care about, you can build a filter statement that can contain either one or a combination of the following filter fields:</span></span>

* <span data-ttu-id="86168-142">[signinDateTime](#signindatetime) – Define uma data ou intervalo de datas</span><span class="sxs-lookup"><span data-stu-id="86168-142">[signinDateTime](#signindatetime) - defines a date or date range</span></span>
* <span data-ttu-id="86168-143">[userId](#userid) – Define um usuário específico com base na ID do usuário.</span><span class="sxs-lookup"><span data-stu-id="86168-143">[userId](#userid) - defines a specific user based the user's ID.</span></span>
* <span data-ttu-id="86168-144">[userPrincipalName](#userprincipalname) – Define um usuário específico com base no UPN (nome principal do usuário) do usuário</span><span class="sxs-lookup"><span data-stu-id="86168-144">[userPrincipalName](#userprincipalname) - defines a specific user based the user's user principal name (UPN)</span></span>
* <span data-ttu-id="86168-145">[appId](#appid) – Define um aplicativo específico com base na ID do aplicativo</span><span class="sxs-lookup"><span data-stu-id="86168-145">[appId](#appid) - defines a specific app based the app's ID</span></span>
* <span data-ttu-id="86168-146">[appDisplayName](#appdisplayname) – Define um aplicativo específico com base no nome para exibição do aplicativo</span><span class="sxs-lookup"><span data-stu-id="86168-146">[appDisplayName](#appdisplayname) - defines a specific app based the app's display name</span></span>
* <span data-ttu-id="86168-147">[loginStatus](#loginStatus) – Define o status dos logons (sucesso/falha)</span><span class="sxs-lookup"><span data-stu-id="86168-147">[loginStatus](#loginStatus) - defines the status of the logins (success / failure)</span></span>

> [!NOTE]
> <span data-ttu-id="86168-148">Ao usar o Graph Explorer, você precisa usar a capitalização correta para cada letra em seus campos de filtro.</span><span class="sxs-lookup"><span data-stu-id="86168-148">When using Graph Explorer, you the need to use the correct case for each letter is your filter fields.</span></span>
> 
> 

<span data-ttu-id="86168-149">Para restringir o escopo dos dados retornados, você pode compilar combinações dos campos de filtro e filtros com suporte.</span><span class="sxs-lookup"><span data-stu-id="86168-149">To narrow down the scope of the returned data, you can build combinations of the supported filters and filter fields.</span></span> <span data-ttu-id="86168-150">Por exemplo, a instrução a seguir retorna os 10 primeiros registros entre 1º de julho de 2016 e 6 de julho de 2016:</span><span class="sxs-lookup"><span data-stu-id="86168-150">For example, the following statement returns the top 10 records between July 1st 2016 and July 6th 2016:</span></span>

    https://graph.windows.net/contoso.com/activities/signinEvents?api-version=beta&$top=10&$filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T00:00:00Z


- - -
### <a name="signindatetime"></a><span data-ttu-id="86168-151">signinDateTime</span><span class="sxs-lookup"><span data-stu-id="86168-151">signinDateTime</span></span>
<span data-ttu-id="86168-152">**Operadores com suporte**: eq, ge, le, gt, lt</span><span class="sxs-lookup"><span data-stu-id="86168-152">**Supported operators**: eq, ge, le, gt, lt</span></span>

<span data-ttu-id="86168-153">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="86168-153">**Example**:</span></span>

<span data-ttu-id="86168-154">Como usar uma data específica</span><span class="sxs-lookup"><span data-stu-id="86168-154">Using a specific date</span></span>

    $filter=signinDateTime+eq+2016-04-25T23:59:00Z    



<span data-ttu-id="86168-155">Como usar um intervalo de datas</span><span class="sxs-lookup"><span data-stu-id="86168-155">Using a date range</span></span>    

    $filter=signinDateTime+ge+2016-07-01T17:05:21Z+and+signinDateTime+le+2016-07-07T17:05:21Z


<span data-ttu-id="86168-156">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="86168-156">**Notes**:</span></span>

<span data-ttu-id="86168-157">O parâmetro datetime deve estar no formato UTC</span><span class="sxs-lookup"><span data-stu-id="86168-157">The datetime parameter should be in the UTC format</span></span> 

- - -
### <a name="userid"></a><span data-ttu-id="86168-158">userId</span><span class="sxs-lookup"><span data-stu-id="86168-158">userId</span></span>
<span data-ttu-id="86168-159">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="86168-159">**Supported operators**: eq</span></span>

<span data-ttu-id="86168-160">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="86168-160">**Example**:</span></span>

    $filter=userId+eq+’00000000-0000-0000-0000-000000000000’

<span data-ttu-id="86168-161">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="86168-161">**Notes**:</span></span>

<span data-ttu-id="86168-162">O valor de userID é um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="86168-162">The value of userId is a string value</span></span>

- - -
### <a name="userprincipalname"></a><span data-ttu-id="86168-163">userPrincipalName</span><span class="sxs-lookup"><span data-stu-id="86168-163">userPrincipalName</span></span>
<span data-ttu-id="86168-164">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="86168-164">**Supported operators**: eq</span></span>

<span data-ttu-id="86168-165">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="86168-165">**Example**:</span></span>

    $filter=userPrincipalName+eq+'audrey.oliver@wingtiptoysonline.com' 


<span data-ttu-id="86168-166">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="86168-166">**Notes**:</span></span>

<span data-ttu-id="86168-167">O valor de userPrincipalName é um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="86168-167">The value of userPrincipalName is a string value</span></span>

- - -
### <a name="appid"></a><span data-ttu-id="86168-168">appId</span><span class="sxs-lookup"><span data-stu-id="86168-168">appId</span></span>
<span data-ttu-id="86168-169">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="86168-169">**Supported operators**: eq</span></span>

<span data-ttu-id="86168-170">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="86168-170">**Example**:</span></span>

    $filter=appId+eq+’00000000-0000-0000-0000-000000000000’



<span data-ttu-id="86168-171">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="86168-171">**Notes**:</span></span>

<span data-ttu-id="86168-172">O valor de appId é um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="86168-172">The value of appId is a string value</span></span>

- - -
### <a name="appdisplayname"></a><span data-ttu-id="86168-173">appDisplayName</span><span class="sxs-lookup"><span data-stu-id="86168-173">appDisplayName</span></span>
<span data-ttu-id="86168-174">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="86168-174">**Supported operators**: eq</span></span>

<span data-ttu-id="86168-175">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="86168-175">**Example**:</span></span>

    $filter=appDisplayName+eq+'Azure+Portal' 


<span data-ttu-id="86168-176">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="86168-176">**Notes**:</span></span>

<span data-ttu-id="86168-177">O valor de appDisplayName é um valor de cadeia de caracteres</span><span class="sxs-lookup"><span data-stu-id="86168-177">The value of appDisplayName is a string value</span></span>

- - -
### <a name="loginstatus"></a><span data-ttu-id="86168-178">loginStatus</span><span class="sxs-lookup"><span data-stu-id="86168-178">loginStatus</span></span>
<span data-ttu-id="86168-179">**Operadores com suporte**: eq</span><span class="sxs-lookup"><span data-stu-id="86168-179">**Supported operators**: eq</span></span>

<span data-ttu-id="86168-180">**Exemplo**:</span><span class="sxs-lookup"><span data-stu-id="86168-180">**Example**:</span></span>

    $filter=loginStatus+eq+'1'  


<span data-ttu-id="86168-181">**Observações**:</span><span class="sxs-lookup"><span data-stu-id="86168-181">**Notes**:</span></span>

<span data-ttu-id="86168-182">Há duas opções para o loginStatus: 0 – êxito, 1 – Falha</span><span class="sxs-lookup"><span data-stu-id="86168-182">There are two options for the loginStatus: 0 - success, 1 - failure</span></span>

- - -
## <a name="next-steps"></a><span data-ttu-id="86168-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="86168-183">Next steps</span></span>
* <span data-ttu-id="86168-184">Quer ver exemplos para atividades de entrada filtradas?</span><span class="sxs-lookup"><span data-stu-id="86168-184">Do you want to see examples for filtered sign-in activities?</span></span> <span data-ttu-id="86168-185">Confira [Exemplos de API de relatório de atividade de entrada do Azure Active Directory](active-directory-reporting-api-sign-in-activity-samples.md).</span><span class="sxs-lookup"><span data-stu-id="86168-185">Check out the [Azure Active Directory sign-in activity report API samples](active-directory-reporting-api-sign-in-activity-samples.md).</span></span>
* <span data-ttu-id="86168-186">Quer saber mais sobre a API de relatório do Azure AD?</span><span class="sxs-lookup"><span data-stu-id="86168-186">Do you want to know more about the Azure AD reporting API?</span></span> <span data-ttu-id="86168-187">Confira [Introdução à API de relatório do Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="86168-187">See [Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md).</span></span>

