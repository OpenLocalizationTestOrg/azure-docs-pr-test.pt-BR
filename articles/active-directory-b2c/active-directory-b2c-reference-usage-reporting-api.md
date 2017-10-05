---
title: "Azure Active Directory B2C: definições e exemplos de API de relatório de uso | Microsoft Docs"
description: "Guia e exemplos de como obter relatórios sobre usuários de locatário, autenticações e autenticações multifator do Azure AD B2C"
services: active-directory-b2c
documentationcenter: dev-center-name
author: rojasja
manager: mbaldwin
ms.service: active-directory-b2c
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/04/2017
ms.author: joroja
ms.openlocfilehash: 52180b760046d273c5a75720df0a73532d0343ad
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-the-reporting-api"></a><span data-ttu-id="7ac1f-103">Acessando os relatórios de uso do Azure AD B2C por meio da API de geração de relatórios</span><span class="sxs-lookup"><span data-stu-id="7ac1f-103">Accessing usage reports in Azure AD B2C via the reporting API</span></span>

<span data-ttu-id="7ac1f-104">O Azure AD B2C (Azure Active Directory B2C) fornece autenticação com base na entrada do usuário e na Autenticação Multifator do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="7ac1f-105">A autenticação é fornecida para usuários finais da sua família de aplicativos em provedores de identidade.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="7ac1f-106">Quando você sabe o número de usuários registrados no locatário, os provedores que eles usaram para registrar-se e o número de autenticações por tipo, você pode responder a perguntas como:</span><span class="sxs-lookup"><span data-stu-id="7ac1f-106">When you know the number of users registered in the tenant, the providers they used to register, and the number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="7ac1f-107">Quantos usuários de cada tipo de provedor de identidade (por exemplo, uma conta da Microsoft ou do LinkedIn) se registraram nos últimos 10 dias?</span><span class="sxs-lookup"><span data-stu-id="7ac1f-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in the last 10 days?</span></span>
* <span data-ttu-id="7ac1f-108">Quantas autenticações usando a Autenticação Multifator foram concluídas com êxito no último mês?</span><span class="sxs-lookup"><span data-stu-id="7ac1f-108">How many authentications using Multi-Factor Authentication have completed successfully in the last month?</span></span>
* <span data-ttu-id="7ac1f-109">Quantas autenticações baseadas em início de sessão foram concluídas neste mês?</span><span class="sxs-lookup"><span data-stu-id="7ac1f-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="7ac1f-110">Por dia?</span><span class="sxs-lookup"><span data-stu-id="7ac1f-110">Per day?</span></span> <span data-ttu-id="7ac1f-111">Por aplicativo?</span><span class="sxs-lookup"><span data-stu-id="7ac1f-111">Per application?</span></span>
* <span data-ttu-id="7ac1f-112">Como posso estimar o custo mensal esperado da minha atividade de locatário do Azure AD B2C?</span><span class="sxs-lookup"><span data-stu-id="7ac1f-112">How can I estimate the expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="7ac1f-113">Este artigo se concentra em relatórios ligados à atividade de cobrança, que é baseada no número de usuários, nas autenticações faturáveis baseadas em início de sessão e nas autenticações multifator.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-113">This article focuses on reports tied to billing activity, which is based on the number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="7ac1f-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="7ac1f-114">Prerequisites</span></span>
<span data-ttu-id="7ac1f-115">Antes de começar, você precisa concluir as etapas em [Pré-requisitos para acessar as APIs de relatório do Azure AD](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="7ac1f-115">Before you get started, you need to complete the steps in [Prerequisites to access the Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="7ac1f-116">Criar um aplicativo, obter um segredo para ele e conceder acesso direitos para relatórios do locatário B2C do AD do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-116">Create an application, obtain a secret for it, and grant it access rights to your Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="7ac1f-117">Também são fornecidos aqui os exemplos de *script Bash* e de *script Python*.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="7ac1f-118">Script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ac1f-118">PowerShell script</span></span>
<span data-ttu-id="7ac1f-119">Este script demonstra a criação de quatro relatórios de uso por meio do parâmetro `TimeStamp` e do filtro `ApplicationId`.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-119">This script demonstrates the creation of four usage reports by using the `TimeStamp` parameter and the `ApplicationId` filter.</span></span>

```powershell
# This script will require the Web Application and permissions setup in Azure Active Directory

# Constants
$ClientID      = "your-client-application-id-here"  
$ClientSecret  = "your-client-application-secret-here"
$loginURL      = "https://login.microsoftonline.com"
$tenantdomain  = "your-b2c-tenant-domain.onmicrosoft.com"  
# Get an Oauth 2 access token based on client id, secret and tenant domain
$body          = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
$oauth         = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body
if ($oauth.access_token -ne $null) {
    $headerParams  = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    Write-host Data from the tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for the report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for the " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from the b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="7ac1f-120">Definições de relatório de uso</span><span class="sxs-lookup"><span data-stu-id="7ac1f-120">Usage report definitions</span></span>
* <span data-ttu-id="7ac1f-121">**tenantUserCount**: o número de usuários no locatário por tipo de provedor de identidade, por dia, nos últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-121">**tenantUserCount**: The number of users in the tenant by type of identity provider, per day in the last 30 days.</span></span> <span data-ttu-id="7ac1f-122">(opcionalmente, um filtro `TimeStamp` fornece contas de usuário de uma data especificada até a data atual).</span><span class="sxs-lookup"><span data-stu-id="7ac1f-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date to the current date).</span></span> <span data-ttu-id="7ac1f-123">O relatório fornece:</span><span class="sxs-lookup"><span data-stu-id="7ac1f-123">The report provides:</span></span>
  * <span data-ttu-id="7ac1f-124">**TotalUserCount**: o número de todos os objetos de usuário.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-124">**TotalUserCount**: The number of all user objects.</span></span>
  * <span data-ttu-id="7ac1f-125">**OtherUserCount**: o número de usuários do Azure Active Directory (não os usuários do Azure AD B2C).</span><span class="sxs-lookup"><span data-stu-id="7ac1f-125">**OtherUserCount**: The number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="7ac1f-126">**LocalUserCount**: o número de contas de usuário do Azure AD B2C criadas com credenciais locais ao locatário do Azure AD B2C.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-126">**LocalUserCount**: The number of Azure AD B2C user accounts created with credentials local to the Azure AD B2C tenant.</span></span>

* <span data-ttu-id="7ac1f-127">**AlternateIdUserCount**: o número de usuários do Azure AD B2C registrados com provedores de identidade externa (por exemplo, Facebook, uma conta da Microsoft ou outro locatário do Azure Active Directory, também conhecido como uma `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="7ac1f-127">**AlternateIdUserCount**: The number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred to as an `OrgId`).</span></span>

* <span data-ttu-id="7ac1f-128">**b2cAuthenticationCountSummary**: resumo do número diário de autenticações faturáveis nos últimos 30 dias, por dia e tipo de fluxo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-128">**b2cAuthenticationCountSummary**: Summary of the daily number of billable authentications over the last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="7ac1f-129">**b2cAuthenticationCount**: o número de autenticações em um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-129">**b2cAuthenticationCount**: The number of authentications within a time period.</span></span> <span data-ttu-id="7ac1f-130">O padrão é nos últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-130">The default is the last 30 days.</span></span>  <span data-ttu-id="7ac1f-131">(Opcional: os parâmetros `TimeStamp` inicial e final definem um período de tempo específico). A saída inclui `StartTimeStamp` (data mais antiga de atividade para este locatário) e `EndTimeStamp` (atualização mais recente).</span><span class="sxs-lookup"><span data-stu-id="7ac1f-131">(Optional: The beginning and ending `TimeStamp` parameters define a specific time period.) The output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="7ac1f-132">**b2cMfaRequestCountSummary**: resumo do número diário de autenticações multifator, por dia e por tipo (SMS ou voz).</span><span class="sxs-lookup"><span data-stu-id="7ac1f-132">**b2cMfaRequestCountSummary**: Summary of the daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="7ac1f-133">Limitações</span><span class="sxs-lookup"><span data-stu-id="7ac1f-133">Limitations</span></span>
<span data-ttu-id="7ac1f-134">Dados de contagem de usuário são atualizados a cada 24 a 48 horas.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-134">User count data is refreshed every 24 to 48 hours.</span></span> <span data-ttu-id="7ac1f-135">As autenticações são atualizadas várias vezes ao dia.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="7ac1f-136">Ao usar o filtro `ApplicationId`, uma resposta de relatório em branco poderá ser devida a uma das seguintes condições:</span><span class="sxs-lookup"><span data-stu-id="7ac1f-136">When using the `ApplicationId` filter, an empty report response can be due to one of following conditions:</span></span>
  * <span data-ttu-id="7ac1f-137">A ID do aplicativo não existe no locatário.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-137">The application ID does not exist in the tenant.</span></span> <span data-ttu-id="7ac1f-138">Verifique se que ele está correto.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="7ac1f-139">A ID do aplicativo existe, mas não foi encontrado nenhum dado no período do relatório.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-139">The application ID exists, but no data was found in the reporting period.</span></span> <span data-ttu-id="7ac1f-140">Examine seus parâmetros de data/hora.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="7ac1f-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7ac1f-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="7ac1f-142">Estimativas de cobrança mensal do Azure AD</span><span class="sxs-lookup"><span data-stu-id="7ac1f-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="7ac1f-143">Quando combinado com [a mais atual do Azure AD B2C preços disponíveis](https://azure.microsoft.com/pricing/details/active-directory-b2c/), você pode estimar diários, semana e mensal de consumo do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-143">When combined with [the most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="7ac1f-144">Uma estimativa é especialmente útil ao planejar alterações no comportamento do locatário que possam afetar o custo geral.</span><span class="sxs-lookup"><span data-stu-id="7ac1f-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="7ac1f-145">Você pode examinar os custos reais na sua [assinatura vinculada do Azure](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="7ac1f-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="7ac1f-146">Opções para outros formatos de saída</span><span class="sxs-lookup"><span data-stu-id="7ac1f-146">Options for other output formats</span></span>
<span data-ttu-id="7ac1f-147">O código a seguir mostra exemplos do envio da saída para JSON, para uma lista de nome-valor e para XML:</span><span class="sxs-lookup"><span data-stu-id="7ac1f-147">The following code shows examples of sending output to JSON, a name value list, and XML:</span></span>
```powershell
# to output to JSON use following line in the PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# to output the content to a name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# to output the content in XML use the following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
