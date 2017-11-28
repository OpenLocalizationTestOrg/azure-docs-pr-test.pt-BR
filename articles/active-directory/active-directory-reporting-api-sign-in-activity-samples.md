---
title: "exemplos de API de relatório de atividade de aaaAzure sign-in do Active Directory | Microsoft Docs"
description: Como tooget iniciada com hello Azure Reporting API do Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: c41c1489-726b-4d3f-81d6-83beb932df9c
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 07/15/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: d4fbbea95fe0b52828673b997681ae37481e21bc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="0715d-103">Exemplos de API de relatório de atividade de entrada do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0715d-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="0715d-104">Este tópico faz parte de uma coleção de tópicos sobre Olá Active Directory do Azure API de relatório.</span><span class="sxs-lookup"><span data-stu-id="0715d-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="0715d-105">Relatórios de AD do Azure fornece uma API que permite que você tooaccess dados de atividade de entrada usando o código ou ferramentas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="0715d-105">Azure AD reporting provides you with an API that enables you tooaccess sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="0715d-106">Olá, escopo deste tópico é tooprovide com exemplo de código para hello **API de atividade de entrada**.</span><span class="sxs-lookup"><span data-stu-id="0715d-106">hello scope of this topic is tooprovide you with sample code for hello **sign-in activity API**.</span></span>

<span data-ttu-id="0715d-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="0715d-107">See:</span></span>

* <span data-ttu-id="0715d-108">[Logs de auditoria](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações conceituais</span><span class="sxs-lookup"><span data-stu-id="0715d-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="0715d-109">[Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) para obter mais informações sobre Olá API de relatório.</span><span class="sxs-lookup"><span data-stu-id="0715d-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0715d-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0715d-110">Prerequisites</span></span>
<span data-ttu-id="0715d-111">Antes de você pode usar os exemplos de saudação neste tópico, é necessário Olá toocomplete [pré-requisitos tooaccess Olá AD do Azure reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="0715d-111">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="0715d-112">Script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="0715d-112">PowerShell script</span></span>
    # This script will require hello Web Application and permissions setup in Azure Active Directory
    $ClientID       = "<clientId>"             # Should be a ~35 character string insert your info here
    $ClientSecret   = "<clientSecret>"         # Should be a ~44 character string insert your info here
    $loginURL       = "https://login.microsoftonline.com/"
    $tenantdomain   = "<tenantDomain>"
    $ daterange            # For example, contoso.onmicrosoft.com

    $7daysago = "{0:s}" -f (get-date).AddDays(-7) + "Z"
    # or, AddMinutes(-5)

    Write-Output $7daysago

    # Get an Oauth 2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}

    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    if ($oauth.access_token -ne $null) {
    $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}

    $url = "https://graph.windows.net/$tenantdomain/activities/signinEvents?api-version=beta&`$filter=signinDateTime ge $7daysago"

    $i=0

    Do{
        Write-Output "Fetching data using Uri: $url"
        $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
        Write-Output "Save hello output tooa file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-hello-script"></a><span data-ttu-id="0715d-113">Executando o script hello</span><span class="sxs-lookup"><span data-stu-id="0715d-113">Executing hello script</span></span>
<span data-ttu-id="0715d-114">Uma vez você terminar de editar o script hello, executá-lo e verifique se que esse Olá esperado de dados de relatório de logs de auditoria de saudação são retornados.</span><span class="sxs-lookup"><span data-stu-id="0715d-114">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="0715d-115">script Hello retorna a saída do relatório entrada hello no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0715d-115">hello script returns output from hello sign-in report in JSON format.</span></span> <span data-ttu-id="0715d-116">Ele também cria um `SigninActivities.json` arquivo com hello mesma saída.</span><span class="sxs-lookup"><span data-stu-id="0715d-116">It also creates an `SigninActivities.json` file with hello same output.</span></span> <span data-ttu-id="0715d-117">Você pode experimentar, modificando Olá script tooreturn dados de outros relatórios e comente Olá formatos de saída não é necessário.</span><span class="sxs-lookup"><span data-stu-id="0715d-117">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0715d-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0715d-118">Next Steps</span></span>
* <span data-ttu-id="0715d-119">Você gostaria que toocustomize exemplos Olá neste tópico?</span><span class="sxs-lookup"><span data-stu-id="0715d-119">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="0715d-120">Check-out Olá [atividade de entrada do Active Directory do Azure referência da API](active-directory-reporting-api-sign-in-activity-reference.md).</span><span class="sxs-lookup"><span data-stu-id="0715d-120">Check out hello [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="0715d-121">Se você quiser uma visão geral completa do uso de toosee Olá do Active Directory do Azure API de relatório, consulte [guia de Introdução ao Olá do Active Directory do Azure API de relatório](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="0715d-121">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="0715d-122">Se você quiser toofind mais informações sobre os relatórios do Active Directory do Azure, consulte Olá [do Azure Active Directory Reporting guia](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="0715d-122">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

