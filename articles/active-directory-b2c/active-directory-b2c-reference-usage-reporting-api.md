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
ms.openlocfilehash: f01f0d1d12464e38f892f1fdd5c7408a3b4cd1aa
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="accessing-usage-reports-in-azure-ad-b2c-via-hello-reporting-api"></a><span data-ttu-id="105a6-103">Acessando os relatórios de uso do Azure AD B2C via Olá API de relatório</span><span class="sxs-lookup"><span data-stu-id="105a6-103">Accessing usage reports in Azure AD B2C via hello reporting API</span></span>

<span data-ttu-id="105a6-104">O Azure AD B2C (Azure Active Directory B2C) fornece autenticação com base na entrada do usuário e na Autenticação Multifator do Azure.</span><span class="sxs-lookup"><span data-stu-id="105a6-104">Azure Active Directory B2C (Azure AD B2C) provides authentication based on user sign-in and Azure Multi-Factor Authentication.</span></span> <span data-ttu-id="105a6-105">A autenticação é fornecida para usuários finais da sua família de aplicativos em provedores de identidade.</span><span class="sxs-lookup"><span data-stu-id="105a6-105">Authentication is provided for end users of your application family across identity providers.</span></span> <span data-ttu-id="105a6-106">Quando você souber o número de saudação de usuários registrados no locatário hello, provedores de saudação usavam tooregister e número de autenticações de saudação por tipo, você pode responder a perguntas como:</span><span class="sxs-lookup"><span data-stu-id="105a6-106">When you know hello number of users registered in hello tenant, hello providers they used tooregister, and hello number of authentications by type, you can answer questions like:</span></span>
* <span data-ttu-id="105a6-107">Quantos usuários de cada tipo de provedor de identidade (por exemplo, uma conta da Microsoft ou LinkedIn) foram registrados no hello últimos 10 dias?</span><span class="sxs-lookup"><span data-stu-id="105a6-107">How many users from each type of identity provider (for example, a Microsoft or LinkedIn account) have registered in hello last 10 days?</span></span>
* <span data-ttu-id="105a6-108">Quantas autenticações usando a autenticação multifator foram concluídos com êxito no Olá no último mês?</span><span class="sxs-lookup"><span data-stu-id="105a6-108">How many authentications using Multi-Factor Authentication have completed successfully in hello last month?</span></span>
* <span data-ttu-id="105a6-109">Quantas autenticações baseadas em início de sessão foram concluídas neste mês?</span><span class="sxs-lookup"><span data-stu-id="105a6-109">How many sign-in-based authentications were completed this month?</span></span> <span data-ttu-id="105a6-110">Por dia?</span><span class="sxs-lookup"><span data-stu-id="105a6-110">Per day?</span></span> <span data-ttu-id="105a6-111">Por aplicativo?</span><span class="sxs-lookup"><span data-stu-id="105a6-111">Per application?</span></span>
* <span data-ttu-id="105a6-112">Como estimar Olá esperado custo mensal da minha atividade de locatário do Azure AD B2C?</span><span class="sxs-lookup"><span data-stu-id="105a6-112">How can I estimate hello expected monthly cost of my Azure AD B2C tenant activity?</span></span>

<span data-ttu-id="105a6-113">Este artigo se concentra na atividade de toobilling relatórios vinculados, que é baseada no número de saudação de usuários, autenticações de entrada no baseado faturáveis e autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="105a6-113">This article focuses on reports tied toobilling activity, which is based on hello number of users, billable sign-in-based authentications, and multi-factor authentications.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="105a6-114">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="105a6-114">Prerequisites</span></span>
<span data-ttu-id="105a6-115">Antes de começar, você precisa de etapas Olá toocomplete [tooaccess pré-requisitos Olá relatórios do Azure AD APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span><span class="sxs-lookup"><span data-stu-id="105a6-115">Before you get started, you need toocomplete hello steps in [Prerequisites tooaccess hello Azure AD reporting APIs](https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/).</span></span> <span data-ttu-id="105a6-116">Criar um aplicativo, obter um segredo para ele e conceder acesso a ele direitos relatórios tooyour do Azure AD B2C do locatário.</span><span class="sxs-lookup"><span data-stu-id="105a6-116">Create an application, obtain a secret for it, and grant it access rights tooyour Azure AD B2C tenant’s reports.</span></span> <span data-ttu-id="105a6-117">Também são fornecidos aqui os exemplos de *script Bash* e de *script Python*.</span><span class="sxs-lookup"><span data-stu-id="105a6-117">*Bash script* and *Python script* examples are also provided here.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="105a6-118">Script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="105a6-118">PowerShell script</span></span>
<span data-ttu-id="105a6-119">Este script demonstra a criação de saudação de quatro relatórios de uso usando Olá `TimeStamp` parâmetro e hello `ApplicationId` filtro.</span><span class="sxs-lookup"><span data-stu-id="105a6-119">This script demonstrates hello creation of four usage reports by using hello `TimeStamp` parameter and hello `ApplicationId` filter.</span></span>

```powershell
# This script will require hello Web Application and permissions setup in Azure Active Directory

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

    Write-host Data from hello tenantUserCount report
    Write-host ====================================================
     # Returns a JSON document for hello report
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello tenantUserCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/tenantUserCount?%24filter=TimeStamp+gt+2016-10-15&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCountSummary report
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=TimeStamp+gt+2016-09-20+and+TimeStamp+lt+2016-10-03&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cAuthenticationCount report with ApplicationId filter
    Write-host ====================================================
    # Returns a JSON document for hello " " report
        $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cAuthenticationCount?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCountSummary
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with datetime filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCount?%24filter=TimeStamp+gt+2016-09-10+and+TimeStamp+lt+2016-10-04&api-version=beta")
    Write-host $myReport.Content

    Write-host Data from hello b2cMfaRequestCount report with ApplicationId filter
    Write-host ====================================================
    $myReport = (Invoke-WebRequest -Headers $headerParams -Uri "https://graph.windows.net/$tenantdomain/reports/b2cMfaRequestCountSummary?%24filter=ApplicationId+eq+ada78934-a6da-4e69-b816-10de0d79db1d&api-version=beta")
     Write-host $myReport.Content

} else {
    Write-Host "ERROR: No Access Token"
    }
```


## <a name="usage-report-definitions"></a><span data-ttu-id="105a6-120">Definições de relatório de uso</span><span class="sxs-lookup"><span data-stu-id="105a6-120">Usage report definitions</span></span>
* <span data-ttu-id="105a6-121">**tenantUserCount**: Olá número de usuários no locatário Olá por tipo de provedor de identidade por dia em Olá últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="105a6-121">**tenantUserCount**: hello number of users in hello tenant by type of identity provider, per day in hello last 30 days.</span></span> <span data-ttu-id="105a6-122">(Opcionalmente, um `TimeStamp` filtro fornece a contagem de usuários de uma data especificada toohello data atual).</span><span class="sxs-lookup"><span data-stu-id="105a6-122">(Optionally, a `TimeStamp` filter provides user counts from a specified date toohello current date).</span></span> <span data-ttu-id="105a6-123">relatório de saudação fornece:</span><span class="sxs-lookup"><span data-stu-id="105a6-123">hello report provides:</span></span>
  * <span data-ttu-id="105a6-124">**TotalUserCount**: Olá número de todos os objetos de usuário.</span><span class="sxs-lookup"><span data-stu-id="105a6-124">**TotalUserCount**: hello number of all user objects.</span></span>
  * <span data-ttu-id="105a6-125">**OtherUserCount**: Olá o número de usuários do Active Directory do Azure (não o Azure AD B2C usuários).</span><span class="sxs-lookup"><span data-stu-id="105a6-125">**OtherUserCount**: hello number of Azure Active Directory users (not Azure AD B2C users).</span></span>
  * <span data-ttu-id="105a6-126">**LocalUserCount**: Olá número de contas de usuário do Azure AD B2C criadas com locatário de toohello local do Azure AD B2C credenciais.</span><span class="sxs-lookup"><span data-stu-id="105a6-126">**LocalUserCount**: hello number of Azure AD B2C user accounts created with credentials local toohello Azure AD B2C tenant.</span></span>

* <span data-ttu-id="105a6-127">**AlternateIdUserCount**: número de saudação do Azure AD B2C usuários registrados com provedores de identidade externa (por exemplo, Facebook, uma conta da Microsoft ou outro locatário do Active Directory do Azure, também chamado tooas um `OrgId`).</span><span class="sxs-lookup"><span data-stu-id="105a6-127">**AlternateIdUserCount**: hello number of Azure AD B2C users registered with external identity providers (for example, Facebook, a Microsoft account, or another Azure Active Directory tenant, also referred tooas an `OrgId`).</span></span>

* <span data-ttu-id="105a6-128">**b2cAuthenticationCountSummary**: Resumo do número de diário Olá de autenticações faturáveis sobre Olá últimos 30 dias, por dia e o tipo de fluxo de autenticação.</span><span class="sxs-lookup"><span data-stu-id="105a6-128">**b2cAuthenticationCountSummary**: Summary of hello daily number of billable authentications over hello last 30 days, by day and type of authentication flow.</span></span>

* <span data-ttu-id="105a6-129">**b2cAuthenticationCount**: Olá número de autenticações dentro de um período de tempo.</span><span class="sxs-lookup"><span data-stu-id="105a6-129">**b2cAuthenticationCount**: hello number of authentications within a time period.</span></span> <span data-ttu-id="105a6-130">padrão de saudação é hello últimos 30 dias.</span><span class="sxs-lookup"><span data-stu-id="105a6-130">hello default is hello last 30 days.</span></span>  <span data-ttu-id="105a6-131">(Opcional: saudação inicial e final `TimeStamp` parâmetros definem um período de tempo específico.) Olá saída inclui `StartTimeStamp` (data mais antiga de atividade para este Locatário) e `EndTimeStamp` (atualização mais recente).</span><span class="sxs-lookup"><span data-stu-id="105a6-131">(Optional: hello beginning and ending `TimeStamp` parameters define a specific time period.) hello output includes `StartTimeStamp` (earliest date of activity for this tenant) and `EndTimeStamp` (latest update).</span></span>

* <span data-ttu-id="105a6-132">**b2cMfaRequestCountSummary**: Resumo do número de diário de saudação de autenticações de vários fatores, por dia e o tipo (SMS ou voz).</span><span class="sxs-lookup"><span data-stu-id="105a6-132">**b2cMfaRequestCountSummary**: Summary of hello daily number of multi-factor authentications, by day and type (SMS or voice).</span></span>


## <a name="limitations"></a><span data-ttu-id="105a6-133">Limitações</span><span class="sxs-lookup"><span data-stu-id="105a6-133">Limitations</span></span>
<span data-ttu-id="105a6-134">Dados de contagem de usuário são atualizados a cada 24 horas too48.</span><span class="sxs-lookup"><span data-stu-id="105a6-134">User count data is refreshed every 24 too48 hours.</span></span> <span data-ttu-id="105a6-135">As autenticações são atualizadas várias vezes ao dia.</span><span class="sxs-lookup"><span data-stu-id="105a6-135">Authentications are updated several times a day.</span></span> <span data-ttu-id="105a6-136">Ao usar o hello `ApplicationId` filtro, uma resposta de relatório vazio pode ser devida tooone das seguintes condições:</span><span class="sxs-lookup"><span data-stu-id="105a6-136">When using hello `ApplicationId` filter, an empty report response can be due tooone of following conditions:</span></span>
  * <span data-ttu-id="105a6-137">ID do aplicativo Hello não existe no locatário hello.</span><span class="sxs-lookup"><span data-stu-id="105a6-137">hello application ID does not exist in hello tenant.</span></span> <span data-ttu-id="105a6-138">Verifique se que ele está correto.</span><span class="sxs-lookup"><span data-stu-id="105a6-138">Make sure it is correct.</span></span>
  * <span data-ttu-id="105a6-139">ID do aplicativo Hello existe, mas nenhum dado foi encontrado no hello período do relatório.</span><span class="sxs-lookup"><span data-stu-id="105a6-139">hello application ID exists, but no data was found in hello reporting period.</span></span> <span data-ttu-id="105a6-140">Examine seus parâmetros de data/hora.</span><span class="sxs-lookup"><span data-stu-id="105a6-140">Review your date/time parameters.</span></span>


## <a name="next-steps"></a><span data-ttu-id="105a6-141">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="105a6-141">Next steps</span></span>
### <a name="monthly-bill-estimates-for-azure-ad"></a><span data-ttu-id="105a6-142">Estimativas de cobrança mensal do Azure AD</span><span class="sxs-lookup"><span data-stu-id="105a6-142">Monthly bill estimates for Azure AD</span></span>
<span data-ttu-id="105a6-143">Quando combinado com [hello mais atual do Azure AD B2C preços disponíveis](https://azure.microsoft.com/pricing/details/active-directory-b2c/), você pode estimar diários, semana e mensal consumo do Azure.</span><span class="sxs-lookup"><span data-stu-id="105a6-143">When combined with [hello most current Azure AD B2C pricing available](https://azure.microsoft.com/pricing/details/active-directory-b2c/), you can estimate daily, weekly, and monthly Azure consumption.</span></span>  <span data-ttu-id="105a6-144">Uma estimativa é especialmente útil ao planejar alterações no comportamento do locatário que possam afetar o custo geral.</span><span class="sxs-lookup"><span data-stu-id="105a6-144">An estimate is especially useful when you plan for changes in tenant behavior that might impact overall cost.</span></span> <span data-ttu-id="105a6-145">Você pode examinar os custos reais na sua [assinatura vinculada do Azure](active-directory-b2c-how-to-enable-billing.md).</span><span class="sxs-lookup"><span data-stu-id="105a6-145">You can review actual costs in your [linked Azure subscription](active-directory-b2c-how-to-enable-billing.md).</span></span>

### <a name="options-for-other-output-formats"></a><span data-ttu-id="105a6-146">Opções para outros formatos de saída</span><span class="sxs-lookup"><span data-stu-id="105a6-146">Options for other output formats</span></span>
<span data-ttu-id="105a6-147">Olá código a seguir mostra exemplos de enviar a saída tooJSON e uma lista de valores de nome XML:</span><span class="sxs-lookup"><span data-stu-id="105a6-147">hello following code shows examples of sending output tooJSON, a name value list, and XML:</span></span>
```powershell
# toooutput tooJSON use following line in hello PowerShell sample
$myReport.Content | Out-File -FilePath b2cUserJourneySummaryEvents.json -Force

# toooutput hello content tooa name value list
($myReport.Content | ConvertFrom-Json).value | Out-File -FilePath name-your-file.txt -Force

# toooutput hello content in XML use hello following line
(($myReport.Content | ConvertFrom-Json).value | ConvertTo-Xml).InnerXml | Out-File -FilePath name-your-file.xml -Force
```
