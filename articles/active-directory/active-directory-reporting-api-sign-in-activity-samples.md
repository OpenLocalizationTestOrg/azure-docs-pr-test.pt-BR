---
title: "Exemplos de API de relatório de atividade de entrada do Azure Active Directory | Microsoft Docs"
description: "Como começar a usar a API de relatório do Active Directory do Azure"
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
ms.openlocfilehash: 7fc2b59fe37ed2ffe85925c457300ef8fd83c3c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a><span data-ttu-id="0f716-103">Exemplos de API de relatório de atividade de entrada do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="0f716-103">Azure Active Directory sign-in activity report API samples</span></span>
<span data-ttu-id="0f716-104">Este tópico faz parte de uma coleção de tópicos sobre a API de relatório do Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="0f716-104">This topic is part of a collection of topics about the Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="0f716-105">Os relatórios do Azure AD fornecem uma API que permite a você acessar dados de atividade de entrada usando código ou ferramentas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="0f716-105">Azure AD reporting provides you with an API that enables you to access sign-in activity data using code or related tools.</span></span>  
<span data-ttu-id="0f716-106">O escopo deste tópico é fornecer código de exemplo para a **API de atividade de entrada**.</span><span class="sxs-lookup"><span data-stu-id="0f716-106">The scope of this topic is to provide you with sample code for the **sign-in activity API**.</span></span>

<span data-ttu-id="0f716-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="0f716-107">See:</span></span>

* <span data-ttu-id="0f716-108">[Logs de auditoria](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações conceituais</span><span class="sxs-lookup"><span data-stu-id="0f716-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports)  for more conceptual information</span></span>
* <span data-ttu-id="0f716-109">[Introdução à API de relatório do Azure Active Directory](active-directory-reporting-api-getting-started.md) para saber mais sobre a API de relatório.</span><span class="sxs-lookup"><span data-stu-id="0f716-109">[Getting started with the Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about the reporting API.</span></span>


## <a name="prerequisites"></a><span data-ttu-id="0f716-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="0f716-110">Prerequisites</span></span>
<span data-ttu-id="0f716-111">Antes de usar os exemplos deste tópico, você precisará atender os [pré-requisitos para acessar a API de relatório do Azure AD](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="0f716-111">Before you can use the samples in this topic, you need to complete the [prerequisites to access the Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="powershell-script"></a><span data-ttu-id="0f716-112">Script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="0f716-112">PowerShell script</span></span>
    # This script will require the Web Application and permissions setup in Azure Active Directory
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
        Write-Output "Save the output to a file SigninActivities$i.json"
        Write-Output "---------------------------------------------"
        $myReport.Content | Out-File -FilePath SigninActivities$i.json -Force
        $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
        $i = $i+1
    } while($url -ne $null)

    } else {

        Write-Host "ERROR: No Access Token"
    }




## <a name="executing-the-script"></a><span data-ttu-id="0f716-113">Executando o script</span><span class="sxs-lookup"><span data-stu-id="0f716-113">Executing the script</span></span>
<span data-ttu-id="0f716-114">Quando você terminar de editar o script, execute-o e verifique se os dados esperados do relatório Logs de auditoria são retornados.</span><span class="sxs-lookup"><span data-stu-id="0f716-114">Once you finish editing the script, run it and verify that the expected data from the Audit logs report is returned.</span></span>

<span data-ttu-id="0f716-115">O script retorna a saída do relatório de entradas no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="0f716-115">The script returns output from the sign-in report in JSON format.</span></span> <span data-ttu-id="0f716-116">Ele também cria um arquivo `SigninActivities.json` com a mesma saída.</span><span class="sxs-lookup"><span data-stu-id="0f716-116">It also creates an `SigninActivities.json` file with the same output.</span></span> <span data-ttu-id="0f716-117">Você pode experimentar ao modificar o script para retornar dados de outros relatórios, além de comentar os formatos de saída de que você não precisa.</span><span class="sxs-lookup"><span data-stu-id="0f716-117">You can experiment by modifying the script to return data from other reports, and comment out the output formats that you do not need.</span></span>

## <a name="next-steps"></a><span data-ttu-id="0f716-118">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0f716-118">Next Steps</span></span>
* <span data-ttu-id="0f716-119">Você gostaria de personalizar os exemplos deste tópico?</span><span class="sxs-lookup"><span data-stu-id="0f716-119">Would you like to customize the samples in this topic?</span></span> <span data-ttu-id="0f716-120">Confira a [referência da API de atividade de entrada do Azure Active Directory](active-directory-reporting-api-sign-in-activity-reference.md).</span><span class="sxs-lookup"><span data-stu-id="0f716-120">Check out the [Azure Active Directory sign-in activity API reference](active-directory-reporting-api-sign-in-activity-reference.md).</span></span> 
* <span data-ttu-id="0f716-121">Se você quiser uma visão geral de como usar a API de relatório do Azure Active Directory, confira [Introdução à API de relatório do Azure Active Directory](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="0f716-121">If you want to see a complete overview of using the Azure Active Directory reporting API, see [Getting started with the Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="0f716-122">Se você quiser saber mais sobre os relatórios do Azure Active Directory, confira o [Guia de relatórios do Azure Active Directory](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="0f716-122">If you would like to find out more about Azure Active Directory reporting, see the [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

