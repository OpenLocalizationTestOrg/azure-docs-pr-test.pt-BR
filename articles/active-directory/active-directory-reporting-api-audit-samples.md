---
title: exemplos de API de auditoria de aaaAzure do Active Directory reporting | Microsoft Docs
description: Como tooget iniciada com hello Azure Reporting API do Active Directory
services: active-directory
documentationcenter: 
author: MarkusVi
manager: femila
editor: 
ms.assetid: de8b8ec3-49b3-4aa8-93fb-e38f52c99743
ms.service: active-directory
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 08/02/2017
ms.author: dhanyahk;markvi
ms.reviewer: dhanyahk
ms.openlocfilehash: 6ada8a7184d7baacaba5ba9c1b9130653b1cf7fb
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="azure-active-directory-reporting-audit-api-samples"></a><span data-ttu-id="47cdf-103">Exemplos de API de auditoria de relatórios do Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="47cdf-103">Azure Active Directory reporting audit API samples</span></span>
<span data-ttu-id="47cdf-104">Este tópico faz parte de uma coleção de tópicos sobre Olá Active Directory do Azure API de relatório.</span><span class="sxs-lookup"><span data-stu-id="47cdf-104">This topic is part of a collection of topics about hello Azure Active Directory reporting API.</span></span>  
<span data-ttu-id="47cdf-105">Relatórios de AD do Azure fornece uma API que permite que você tooaccess dados de auditoria usando o código ou ferramentas relacionadas.</span><span class="sxs-lookup"><span data-stu-id="47cdf-105">Azure AD reporting provides you with an API that enables you tooaccess audit data using code or related tools.</span></span>
<span data-ttu-id="47cdf-106">Olá, escopo deste tópico é tooprovide com exemplo de código para hello **audit API**.</span><span class="sxs-lookup"><span data-stu-id="47cdf-106">hello scope of this topic is tooprovide you with sample code for hello **audit API**.</span></span>

<span data-ttu-id="47cdf-107">Consulte:</span><span class="sxs-lookup"><span data-stu-id="47cdf-107">See:</span></span>

* <span data-ttu-id="47cdf-108">[Logs de auditoria](active-directory-reporting-azure-portal.md#activity-reports) para obter mais informações conceituais</span><span class="sxs-lookup"><span data-stu-id="47cdf-108">[Audit logs](active-directory-reporting-azure-portal.md#activity-reports) for more conceptual information</span></span>
* <span data-ttu-id="47cdf-109">[Introdução à saudação do Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) para obter mais informações sobre Olá API de relatório.</span><span class="sxs-lookup"><span data-stu-id="47cdf-109">[Getting started with hello Azure Active Directory Reporting API](active-directory-reporting-api-getting-started.md) for more information about hello reporting API.</span></span>

<span data-ttu-id="47cdf-110">Para dúvidas, problemas ou comentários, entre em contato com a [Ajuda de relatório do AAD](mailto:aadreportinghelp@microsoft.com).</span><span class="sxs-lookup"><span data-stu-id="47cdf-110">For questions, issues or feedback, please contact [AAD Reporting Help](mailto:aadreportinghelp@microsoft.com).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="47cdf-111">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="47cdf-111">Prerequisites</span></span>
<span data-ttu-id="47cdf-112">Antes de você pode usar os exemplos de saudação neste tópico, é necessário Olá toocomplete [pré-requisitos tooaccess Olá AD do Azure reporting API](active-directory-reporting-api-prerequisites.md).</span><span class="sxs-lookup"><span data-stu-id="47cdf-112">Before you can use hello samples in this topic, you need toocomplete hello [prerequisites tooaccess hello Azure AD reporting API](active-directory-reporting-api-prerequisites.md).</span></span>  

## <a name="known-issue"></a><span data-ttu-id="47cdf-113">Problema conhecido</span><span class="sxs-lookup"><span data-stu-id="47cdf-113">Known issue</span></span>
<span data-ttu-id="47cdf-114">Autenticação do aplicativo não funcionará se o seu locatário estiver na região da Europa de saudação.</span><span class="sxs-lookup"><span data-stu-id="47cdf-114">App Auth will not work if your tenant is in hello EU region.</span></span> <span data-ttu-id="47cdf-115">Use autenticação de usuário para acessar Olá API de auditoria para solucionar esse problema até que podemos corrigir o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="47cdf-115">Please use User Auth for accessing hello Audit API as a workaround until we fix hello issue.</span></span> 

## <a name="powershell-script"></a><span data-ttu-id="47cdf-116">Script do PowerShell</span><span class="sxs-lookup"><span data-stu-id="47cdf-116">PowerShell script</span></span>
    # This script will require registration of a Web Application in Azure Active Directory (see https://azure.microsoft.com/documentation/articles/active-directory-reporting-api-getting-started/)

    # Constants
    $ClientID       = "your-client-application-id-here"       # Insert your application's Client ID, a Globally Unique ID (registered by Global Admin)
    $ClientSecret   = "your-client-application-secret-here"   # Insert your application's Client Key/Secret string
    $loginURL       = "https://login.microsoftonline.com"     # AAD Instance; for example https://login.microsoftonline.com
    $tenantdomain   = "your-tenant-domain.onmicrosoft.com"    # AAD Tenant; for example, contoso.onmicrosoft.com
    $resource       = "https://graph.windows.net"             # Azure AD Graph API resource URI
    $7daysago       = "{0:s}" -f (get-date).AddDays(-7) + "Z" # Use 'AddMinutes(-5)' toodecrement minutes, for example
    Write-Output "Searching for events starting $7daysago"

    # Create HTTP header, get an OAuth2 access token based on client id, secret and tenant domain
    $body       = @{grant_type="client_credentials";resource=$resource;client_id=$ClientID;client_secret=$ClientSecret}
    $oauth      = Invoke-RestMethod -Method Post -Uri $loginURL/$tenantdomain/oauth2/token?api-version=1.0 -Body $body

    # Parse audit report items, save output toofile(s): auditX.json, where X = 0 thru n for number of nextLink pages
    if ($oauth.access_token -ne $null) {   
        $i=0
        $headerParams = @{'Authorization'="$($oauth.token_type) $($oauth.access_token)"}
        $url = 'https://graph.windows.net/' + $tenantdomain + '/activities/audit?api-version=beta&`$filter=activityDate gt ' + $7daysago

        # loop through each query page (1 through n)
        Do{
            # display each event on hello console window
            Write-Output "Fetching data using Uri: $url"
            $myReport = (Invoke-WebRequest -UseBasicParsing -Headers $headerParams -Uri $url)
            foreach ($event in ($myReport.Content | ConvertFrom-Json).value) {
                Write-Output ($event | ConvertTo-Json)
            }

            # save hello query page tooan output file
            Write-Output "Save hello output tooa file audit$i.json"
            $myReport.Content | Out-File -FilePath audit$i.json -Force
            $url = ($myReport.Content | ConvertFrom-Json).'@odata.nextLink'
            $i = $i+1
        } while($url -ne $null)
    } else {
        Write-Host "ERROR: No Access Token"
        }

    Write-Host "Press any key toocontinue ..."
    $x = $host.UI.RawUI.ReadKey("NoEcho,IncludeKeyDown")


### <a name="executing-hello-powershell-script"></a><span data-ttu-id="47cdf-117">Executar script do PowerShell Olá</span><span class="sxs-lookup"><span data-stu-id="47cdf-117">Executing hello PowerShell script</span></span>
<span data-ttu-id="47cdf-118">Uma vez você terminar de editar o script hello, executá-lo e verifique se que esse Olá esperado de dados de relatório de logs de auditoria de saudação são retornados.</span><span class="sxs-lookup"><span data-stu-id="47cdf-118">Once you finish editing hello script, run it and verify that hello expected data from hello Audit logs report is returned.</span></span>

<span data-ttu-id="47cdf-119">script Hello retorna a saída do relatório de auditoria Olá no formato JSON.</span><span class="sxs-lookup"><span data-stu-id="47cdf-119">hello script returns output from hello audit report in JSON format.</span></span> <span data-ttu-id="47cdf-120">Ele também cria um `audit.json` arquivo com hello mesma saída.</span><span class="sxs-lookup"><span data-stu-id="47cdf-120">It also creates an `audit.json` file with hello same output.</span></span> <span data-ttu-id="47cdf-121">Você pode experimentar, modificando Olá script tooreturn dados de outros relatórios e comente Olá formatos de saída não é necessário.</span><span class="sxs-lookup"><span data-stu-id="47cdf-121">You can experiment by modifying hello script tooreturn data from other reports, and comment out hello output formats that you do not need.</span></span>

## <a name="bash-script"></a><span data-ttu-id="47cdf-122">Script Bash</span><span class="sxs-lookup"><span data-stu-id="47cdf-122">Bash script</span></span>
    #!/bin/bash

    # Author: Ken Hoff (kenhoff@microsoft.com)
    # Date: 2015.08.20
    # NOTE: This script requires jq (https://stedolan.github.io/jq/)

    CLIENT_ID="your-application-client-id-here"         # Should be a ~35 character string insert your info here
    CLIENT_SECRET="your-application-client-secret-here" # Should be a ~44 character string insert your info here
    LOGIN_URL="https://login.microsoftonline.com"
    TENANT_DOMAIN="your-directory-name-here.onmicrosoft.com"    # For example, contoso.onmicrosoft.com

    TOKEN_INFO=$(curl -s --data-urlencode "grant_type=client_credentials" --data-urlencode "client_id=$CLIENT_ID" --data-urlencode "client_secret=$CLIENT_SECRET" "$LOGIN_URL/$TENANT_DOMAIN/oauth2/token?api-version=1.0")

    TOKEN_TYPE=$(echo $TOKEN_INFO | ./jq-win64.exe -r '.token_type')
    ACCESS_TOKEN=$(echo $TOKEN_INFO | ./jq-win64.exe -r '.access_token')

    # get yesterday's date

    YESTERDAY=$(date --date='1 day ago' +'%Y-%m-%d')

    URL="https://graph.windows.net/$TENANT_DOMAIN/activities/audit?api-version=beta&$filter=activityDate%20gt%20$YESTERDAY"


    REPORT=$(curl -s --header "Authorization: $TOKEN_TYPE $ACCESS_TOKEN" $URL)

    echo $REPORT | ./jq-win64.exe -r '.value' | ./jq-win64.exe -r ".[]"

## <a name="python-script"></a><span data-ttu-id="47cdf-123">Script Python</span><span class="sxs-lookup"><span data-stu-id="47cdf-123">Python script</span></span>
    # Author: Michael McLaughlin (michmcla@microsoft.com)
    # Date: January 20, 2016
    # This requires hello Python Requests module: http://docs.python-requests.org

    import requests
    import datetime
    import sys

    client_id = 'your-application-client-id-here'
    client_secret = 'your-application-client-secret-here'
    login_url = 'https://login.microsoftonline.com/'
    tenant_domain = 'your-directory-name-here.onmicrosoft.com'

    # Get an OAuth access token
    bodyvals = {'client_id': client_id,
                'client_secret': client_secret,
                'grant_type': 'client_credentials'}

    request_url = login_url + tenant_domain + '/oauth2/token?api-version=1.0'
    token_response = requests.post(request_url, data=bodyvals)

    access_token = token_response.json().get('access_token')
    token_type = token_response.json().get('token_type')

    if access_token is None or token_type is None:
        print "ERROR: Couldn't get access token"
        sys.exit(1)

    # Use hello access token toomake hello API request
    yesterday = datetime.date.strftime(datetime.date.today() - datetime.timedelta(days=1), '%Y-%m-%d')

    header_params = {'Authorization': token_type + ' ' + access_token}
    request_string = 'https://graph.windows.net/' + tenant_domain + 'activities/audit?api-version=beta&$filter=activityDate%20gt%20' + yesterday   
    response = requests.get(request_string, headers = header_params)

    if response.status_code is 200:
        print response.content
    else:
        print 'ERROR: API request failed'





## <a name="next-steps"></a><span data-ttu-id="47cdf-124">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="47cdf-124">Next steps</span></span>
* <span data-ttu-id="47cdf-125">Você gostaria que toocustomize exemplos Olá neste tópico?</span><span class="sxs-lookup"><span data-stu-id="47cdf-125">Would you like toocustomize hello samples in this topic?</span></span> <span data-ttu-id="47cdf-126">Check-out Olá [auditoria do Active Directory do Azure referência da API](active-directory-reporting-api-audit-reference.md).</span><span class="sxs-lookup"><span data-stu-id="47cdf-126">Check out hello [Azure Active Directory audit API reference](active-directory-reporting-api-audit-reference.md).</span></span> 
* <span data-ttu-id="47cdf-127">Se você quiser uma visão geral completa do uso de toosee Olá do Active Directory do Azure API de relatório, consulte [guia de Introdução ao Olá do Active Directory do Azure API de relatório](active-directory-reporting-api-getting-started.md).</span><span class="sxs-lookup"><span data-stu-id="47cdf-127">If you want toosee a complete overview of using hello Azure Active Directory reporting API, see [Getting started with hello Azure Active Directory reporting API](active-directory-reporting-api-getting-started.md).</span></span>
* <span data-ttu-id="47cdf-128">Se você quiser toofind mais informações sobre os relatórios do Active Directory do Azure, consulte Olá [do Azure Active Directory Reporting guia](active-directory-reporting-guide.md).</span><span class="sxs-lookup"><span data-stu-id="47cdf-128">If you would like toofind out more about Azure Active Directory reporting, see hello [Azure Active Directory Reporting Guide](active-directory-reporting-guide.md).</span></span>  

