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
# <a name="azure-active-directory-sign-in-activity-report-api-samples"></a>Exemplos de API de relatório de atividade de entrada do Azure Active Directory
Este tópico faz parte de uma coleção de tópicos sobre Olá Active Directory do Azure API de relatório.  
Relatórios de AD do Azure fornece uma API que permite que você tooaccess dados de atividade de entrada usando o código ou ferramentas relacionadas.  
Olá, escopo deste tópico é tooprovide com exemplo de código para hello **API de atividade de entrada**.

Consulte:

* [Logs de auditoria](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações conceituais
* [Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) para obter mais informações sobre Olá API de relatório.


## <a name="prerequisites"></a>Pré-requisitos
Antes de você pode usar os exemplos de saudação neste tópico, é necessário Olá toocomplete [pré-requisitos tooaccess Olá AD do Azure reporting API](active-directory-reporting-api-prerequisites.md).  

## <a name="powershell-script"></a>Script do PowerShell
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




## <a name="executing-hello-script"></a>Executando o script hello
Uma vez você terminar de editar o script hello, executá-lo e verifique se que esse Olá esperado de dados de relatório de logs de auditoria de saudação são retornados.

script Hello retorna a saída do relatório entrada hello no formato JSON. Ele também cria um `SigninActivities.json` arquivo com hello mesma saída. Você pode experimentar, modificando Olá script tooreturn dados de outros relatórios e comente Olá formatos de saída não é necessário.

## <a name="next-steps"></a>Próximas etapas
* Você gostaria que toocustomize exemplos Olá neste tópico? Check-out Olá [atividade de entrada do Active Directory do Azure referência da API](active-directory-reporting-api-sign-in-activity-reference.md). 
* Se você quiser uma visão geral completa do uso de toosee Olá do Active Directory do Azure API de relatório, consulte [guia de Introdução ao Olá do Active Directory do Azure API de relatório](active-directory-reporting-api-getting-started.md).
* Se você quiser toofind mais informações sobre os relatórios do Active Directory do Azure, consulte Olá [do Azure Active Directory Reporting guia](active-directory-reporting-guide.md).  

