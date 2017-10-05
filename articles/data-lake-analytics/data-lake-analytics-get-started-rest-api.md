---
title: "Introdução ao Data Lake Analytics usando a API REST | Microsoft Docs"
description: "Usar as APIs REST WebHDFS para executar operações no Data Lake Analytics"
services: data-lake-analytics
documentationcenter: 
author: saveenr
manager: saveenr
editor: cgronlun
ms.assetid: 5e133d92-baaa-44c9-890c-ab2d85c91122
ms.service: data-lake-analytics
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 02/03/2017
ms.author: jgao
ms.openlocfilehash: 332d7af2539eea8890745005104ac5b0921c2b7f
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a><span data-ttu-id="ed8a7-103">Introdução ao Azure Data Lake Analytics usando APIs REST</span><span class="sxs-lookup"><span data-stu-id="ed8a7-103">Get started with Azure Data Lake Analytics using REST APIs</span></span>
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

<span data-ttu-id="ed8a7-104">Saiba como usar APIs REST WebHDFS e APIs REST do Data Lake Analytics para gerenciar contas, trabalhos e catálogo do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-104">Learn how to use WebHDFS REST APIs and Data Lake Analytics REST APIs to manage Data Lake Analytics accounts, jobs, and catalog.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="ed8a7-105">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ed8a7-105">Prerequisites</span></span>
* <span data-ttu-id="ed8a7-106">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-106">**An Azure subscription**.</span></span> <span data-ttu-id="ed8a7-107">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-107">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="ed8a7-108">**Criar um aplicativo do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-108">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="ed8a7-109">Você pode usar o aplicativo Azure AD para autenticar o aplicativo Data Lake Analytics com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-109">You use the Azure AD application to authenticate the Data Lake Analytics application with Azure AD.</span></span> <span data-ttu-id="ed8a7-110">Há diferentes abordagens para autenticar com o Azure AD, que são a **autenticação de usuário final** ou a **autenticação serviço a serviço**.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-110">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="ed8a7-111">Para obter instruções e saber mais sobre como autenticar, confira [Autenticar com o Data Lake Analytics usando o Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-111">For instructions and more information on how to authenticate, see [Authenticate with Data Lake Analytics using Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="ed8a7-112">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-112">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="ed8a7-113">Este artigo usa cURL para demonstrar como fazer chamadas à API REST em uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-113">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Analytics account.</span></span>

## <a name="authenticate-with-azure-active-directory"></a><span data-ttu-id="ed8a7-114">Autenticar com o Azure Active Directory</span><span class="sxs-lookup"><span data-stu-id="ed8a7-114">Authenticate with Azure Active Directory</span></span>
<span data-ttu-id="ed8a7-115">Há dois métodos para autenticar com o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-115">There are two methods for authenticating with Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="ed8a7-116">Autenticação do usuário (interativa)</span><span class="sxs-lookup"><span data-stu-id="ed8a7-116">End-user authentication (interactive)</span></span>
<span data-ttu-id="ed8a7-117">Usando esse método, o aplicativo solicita o logon do usuário e todas as operações são executadas no contexto do usuário.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-117">Using this method, application prompts the user to log in and all the operations are performed in the context of the user.</span></span> 

<span data-ttu-id="ed8a7-118">Siga estas etapas para a autenticação interativa:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-118">Follow these steps for interactive authentication:</span></span>

1. <span data-ttu-id="ed8a7-119">Por meio de seu aplicativo, redirecione o usuário para a seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-119">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="ed8a7-120">\<<REDIRECT-URI> precisa ser codificado para uso em uma URL.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-120">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="ed8a7-121">Portanto, para https://localhost, use `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="ed8a7-121">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="ed8a7-122">Para os fins deste tutorial, é possível substituir os valores de espaço reservado na URL acima e colá-los na barra de endereços do navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-122">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="ed8a7-123">Você será redirecionado para autenticar usando seu logon do Azure.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-123">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="ed8a7-124">Depois de fazer logon com êxito, a resposta será exibida na barra de endereços do navegador.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-124">Once you succesfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="ed8a7-125">A resposta estará no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-125">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="ed8a7-126">Capture o código de autorização da resposta.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-126">Capture the authorization code from the response.</span></span> <span data-ttu-id="ed8a7-127">Para este tutorial, é possível copiar o código de autorização da barra de endereços do navegador da Web e passá-lo na solicitação POST para o ponto de extremidade do token, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-127">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="ed8a7-128">Nesse caso, o \<REDIRECT-URI> não precisa ser codificado.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-128">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="ed8a7-129">A resposta é um objeto JSON que contém um token de acesso (por exemplo, `"access_token": "<ACCESS_TOKEN>"`) e um token de atualização (por exemplo, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-129">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="ed8a7-130">Seu aplicativo usa o token de acesso ao acessar o Repositório Azure Data Lake e o token de atualização para obter outro token de acesso quando um token de acesso expira.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-130">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="ed8a7-131">Quando o token de acesso expira, é possível solicitar um novo token de acesso usando o token de atualização, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-131">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="ed8a7-132">Para obter mais informações sobre a autenticação interativa de usuário, confira [Fluxo de concessão de código de autorização](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-132">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="ed8a7-133">Autenticação serviço a serviço (não interativa)</span><span class="sxs-lookup"><span data-stu-id="ed8a7-133">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="ed8a7-134">Usando esse método, o aplicativo fornece suas próprias credenciais para executar as operações.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-134">Using this method, application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="ed8a7-135">Para isso, você deve emitir uma solicitação POST como a mostrada abaixo:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-135">For this, you must issue a POST request like the one shown below:</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="ed8a7-136">A saída dessa solicitação incluirá um token de autorização (indicado por `access-token` na saída abaixo) que você transmitirá posteriormente com as chamadas à API REST.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-136">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="ed8a7-137">Salve esse token de autenticação em um arquivo de texto. Você precisará dele posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-137">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="ed8a7-138">Este artigo usa uma abordagem **não interativa** .</span><span class="sxs-lookup"><span data-stu-id="ed8a7-138">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="ed8a7-139">Para saber mais sobre (chamadas de serviço a serviço) não interativas, confira [Chamadas de serviço a serviço usando credenciais](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-139">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-analytics-account"></a><span data-ttu-id="ed8a7-140">Criar uma conta da Análise Data Lake</span><span class="sxs-lookup"><span data-stu-id="ed8a7-140">Create a Data Lake Analytics account</span></span>
<span data-ttu-id="ed8a7-141">Você deve criar um grupo de Recursos do Azure e uma conta do Data Lake Store para poder criar uma conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-141">You must create an Azure Resource group, and a Data Lake Store account before you can create a Data Lake Analytics account.</span></span>  <span data-ttu-id="ed8a7-142">Veja [Criar uma conta do Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-142">See [Create a Data Lake Store account](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).</span></span>

<span data-ttu-id="ed8a7-143">O seguinte comando Curl mostra como criar uma conta:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-143">The following Curl command shows how to create an account:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

<span data-ttu-id="ed8a7-144">Substitua \<`REDACTED`\> pelo token de autorização, \<`AzureSubscriptionID`\> pela ID de assinatura, \<`AzureResourceGroupName`\> por um nome de Grupo de Recursos do Azure existente e \<`NewAzureDataLakeAnalyticsAccountName`\> por um novo nome de Conta do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-144">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`NewAzureDataLakeAnalyticsAccountName`\> with a new Data Lake Analytics Account name.</span></span> <span data-ttu-id="ed8a7-145">A carga de solicitação para esse comando está contida no arquivo **CreateDatalakeAnalyticsAccountRequest.json** que é fornecido para o parâmetro `-d` acima.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-145">The request payload for this command is contained in the **CreateDatalakeAnalyticsAccountRequest.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="ed8a7-146">O conteúdo do arquivo input.json lembra o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-146">The contents of the input.json file resemble the following:</span></span>

    {  
        "location": "East US 2",  
        "name": "myadla1004",  
        "tags": {},  
        "properties": {  
            "defaultDataLakeStoreAccount": "my1004store",  
            "dataLakeStoreAccounts": [  
                {  
                    "name": "my1004store"  
                }     
            ]
        }  
    }  


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a><span data-ttu-id="ed8a7-147">Listar contas do Data Lake Analytics em uma assinatura</span><span class="sxs-lookup"><span data-stu-id="ed8a7-147">List Data Lake Analytics accounts in a subscription</span></span>
<span data-ttu-id="ed8a7-148">O seguinte comando Curl mostra como listar contas em uma assinatura:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-148">The following Curl command shows how to list accounts in a subscription:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

<span data-ttu-id="ed8a7-149">Substitua \<`REDACTED`\> pelo token de autorização e \<`AzureSubscriptionID`\> por sua ID de assinatura.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-149">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID.</span></span> <span data-ttu-id="ed8a7-150">A saída deverá ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-150">The output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla0831.azuredatalakeanalytics.net",
                "accountId": "21e74660-0941-4880-ae72-b143c2615ea9",
                "creationTime": "2016-09-01T12:49:12.7451428Z",
                "lastModifiedTime": "2016-09-01T12:49:12.7451428Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla0831rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla0831",
            "name": "myadla0831",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            },
            {
            "properties": {
                "provisioningState": "Succeeded",
                "state": "Active",
                "endpoint": "myadla1004.azuredatalakeanalytics.net",
                "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
                "creationTime": "2016-10-04T20:46:42.287147Z",
                "lastModifiedTime": "2016-10-04T20:46:42.287147Z"
            },
            "location": "East US 2",
            "tags": {},
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
            "name": "myadla1004",
            "type": "Microsoft.DataLakeAnalytics/accounts"
            }
        ]
    }

## <a name="get-information-about-a-data-lake-analytics-account"></a><span data-ttu-id="ed8a7-151">Obter informações sobre uma conta do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ed8a7-151">Get information about a Data Lake Analytics account</span></span>
<span data-ttu-id="ed8a7-152">O seguinte comando Curl mostra como obter as informações da conta:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-152">The following Curl command shows how to get an account information:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

<span data-ttu-id="ed8a7-153">Substitua \<`REDACTED`\> pelo token de autorização, \<`AzureSubscriptionID`\> por sua ID de assinatura, \<`AzureResourceGroupName`\> por um nome de Grupo de Recursos do Azure existente e \<`DataLakeAnalyticsAccountName`\> pelo nome de uma conta existente do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-153">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="ed8a7-154">A saída deverá ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-154">The output is similar to:</span></span>

    {
        "properties": {
            "defaultDataLakeStoreAccount": "my1004store",
            "dataLakeStoreAccounts": [
            {
                "properties": {
                "suffix": "azuredatalakestore.net"
                },
                "name": "my1004store"
            }
            ],
            "provisioningState": "Creating",
            "state": null,
            "endpoint": null,
            "accountId": "3ff9b93b-11c4-43c6-83cc-276292eeb350",
            "creationTime": null,
            "lastModifiedTime": null
        },
        "location": "East US 2",
        "tags": {},
        "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004",
        "name": "myadla1004",
        "type": "Microsoft.DataLakeAnalytics/accounts"
    }

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a><span data-ttu-id="ed8a7-155">Listar Data Lake Stores de uma conta do Data Lake Analytics</span><span class="sxs-lookup"><span data-stu-id="ed8a7-155">List Data Lake Stores of a Data Lake Analytics account</span></span>
<span data-ttu-id="ed8a7-156">O seguinte comando Curl mostra como listar Data Lake Stores de uma conta:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-156">The following Curl command shows how to list Data Lake Stores of an account:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

<span data-ttu-id="ed8a7-157">Substitua \<`REDACTED`\> pelo token de autorização, \<`AzureSubscriptionID`\> por sua ID de assinatura, \<`AzureResourceGroupName`\> por um nome de Grupo de Recursos do Azure existente e \<`DataLakeAnalyticsAccountName`\> pelo nome de uma conta existente do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-157">Replace \<`REDACTED`\> with the authorization token, \<`AzureSubscriptionID`\> with your subscription ID, \<`AzureResourceGroupName`\> with an existing Azure Resource Group name, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="ed8a7-158">A saída deverá ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-158">The output is similar to:</span></span>

    {
        "value": [
            {
            "properties": {
                "suffix": "azuredatalakestore.net"
            },
            "id": "/subscriptions/65a1016d-0f67-45d2-b838-b8f373d6d52e/resourceGroups/myadla1004rg/providers/Microsoft.DataLakeAnalytics/accounts/myadla1004/dataLakeStoreAccounts/my1004store",
            "name": "my1004store",
            "type": "Microsoft.DataLakeAnalytics/accounts/dataLakeStoreAccounts"
            }
        ]
    }

## <a name="submit-u-sql-jobs"></a><span data-ttu-id="ed8a7-159">Enviar trabalhos de U-SQL</span><span class="sxs-lookup"><span data-stu-id="ed8a7-159">Submit U-SQL jobs</span></span>
<span data-ttu-id="ed8a7-160">O seguinte comando Curl mostra como enviar um trabalho de U-SQL:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-160">The following Curl command shows how to submit a U-SQL job:</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

<span data-ttu-id="ed8a7-161">Substitua \<`REDACTED`\> pelo token de autorização e \<`DataLakeAnalyticsAccountName`\> pelo nome de uma conta existente do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-161">Replace \<`REDACTED`\> with the authorization token, \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> <span data-ttu-id="ed8a7-162">A carga de solicitação para esse comando está contida no arquivo **SubmitADLAJob.json** fornecido para o parâmetro `-d` acima.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-162">The request payload for this command is contained in the **SubmitADLAJob.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="ed8a7-163">O conteúdo do arquivo input.json lembra o seguinte:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-163">The contents of the input.json file resemble the following:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "properties": {
            "type": "USql",
            "script": "@searchlog =\n    EXTRACT UserId          int,\n            Start           DateTime,\n            Region          string,\n            Query          
        string,\n            Duration        int?,\n            Urls            string,\n            ClickedUrls     string\n    FROM \"/Samples/Data/SearchLog.tsv\"\n    US
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    TO \"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

<span data-ttu-id="ed8a7-164">A saída deverá ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-164">The output is similar to:</span></span>

    {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "myadl@SPI",
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "2016-10-05T13:54:59.9871859+00:00",
        "state": "Compiling",
        "result": "Succeeded",
        "stateAuditRecords": [
            {
            "newState": "New",
            "timeStamp": "2016-10-05T13:54:59.9871859+00:00",
            "details": "userName:myadl@SPI;submitMachine:N/A"
            }
        ],
        "properties": {
            "owner": "myadl@SPI",
            "resources": [],
            "runtimeVersion": "default",
            "rootProcessNodeId": "00000000-0000-0000-0000-000000000000",
            "algebraFilePath": "adl://myadls0831.azuredatalakestore.net/system/jobservice/jobs/Usql/2016/10/05/13/54/8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a/algebra.xml",
            "compileMode": "Semantic",
            "errorSource": "Unknown",
            "totalCompilationTime": "PT0S",
            "totalPausedTime": "PT0S",
            "totalQueuedTime": "PT0S",
            "totalRunningTime": "PT0S",
            "type": "USql"
        }
    }


## <a name="list-u-sql-jobs"></a><span data-ttu-id="ed8a7-165">Listar trabalhos de U-SQL</span><span class="sxs-lookup"><span data-stu-id="ed8a7-165">List U-SQL jobs</span></span>
<span data-ttu-id="ed8a7-166">O seguinte comando Curl mostra como listar trabalhos U-SQL:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-166">The following Curl command shows how to list U-SQL jobs:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

<span data-ttu-id="ed8a7-167">Substitua \<`REDACTED`\> pelo token de autorização e \<`DataLakeAnalyticsAccountName`\> pelo nome de uma conta existente do Data Lake Analytics.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-167">Replace \<`REDACTED`\> with the authorization token, and \<`DataLakeAnalyticsAccountName`\> with the name of an existing Data Lake Analytics Account.</span></span> 

<span data-ttu-id="ed8a7-168">A saída deverá ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-168">The output is similar to:</span></span>

    {
    "value": [
        {
        "jobId": "65cf1691-9dbe-43cd-90ed-1cafbfb406fb",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someone@microsoft.com",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:46:53 GMT",
        "startTime": "Wed, 05 Oct 2016 13:47:33 GMT",
        "endTime": "Wed, 05 Oct 2016 13:48:07 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        },
        {
        "jobId": "8f8ebf8c-4b63-428a-ab46-a03d2cc5b65a",
        "name": "convertTSVtoCSV",
        "type": "USql",
        "submitter": "someoneadl@SPI",
        "account": null,
        "degreeOfParallelism": 1,
        "priority": 1000,
        "submitTime": "Wed, 05 Oct 2016 13:54:59 GMT",
        "startTime": "Wed, 05 Oct 2016 13:55:43 GMT",
        "endTime": "Wed, 05 Oct 2016 13:56:11 GMT",
        "state": "Ended",
        "result": "Succeeded",
        "errorMessage": null,
        "storageAccounts": null,
        "stateAuditRecords": null,
        "logFilePatterns": null,
        "properties": null
        }
    ],
    "nextLink": null,
    "count": null
    }


## <a name="get-catalog-items"></a><span data-ttu-id="ed8a7-169">Obter itens do catálogo</span><span class="sxs-lookup"><span data-stu-id="ed8a7-169">Get catalog items</span></span>
<span data-ttu-id="ed8a7-170">O seguinte comando Curl mostra como obter os bancos de dados do catálogo:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-170">The following Curl command shows how to get the databases from the catalog:</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

<span data-ttu-id="ed8a7-171">A saída deverá ser semelhante a:</span><span class="sxs-lookup"><span data-stu-id="ed8a7-171">The output is similar to:</span></span>

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a><span data-ttu-id="ed8a7-172">Consulte também</span><span class="sxs-lookup"><span data-stu-id="ed8a7-172">See also</span></span>
* <span data-ttu-id="ed8a7-173">Para ver uma consulta mais complexa, consulte [Analisar logs de site usando a Análise Data Lake do Azure](data-lake-analytics-analyze-weblogs.md).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-173">To see a more complex query, see [Analyze Website logs using Azure Data Lake Analytics](data-lake-analytics-analyze-weblogs.md).</span></span>
* <span data-ttu-id="ed8a7-174">Para começar a desenvolver aplicativos U-SQL, consulte [Desenvolver scripts U-SQL usando as Ferramentas do Data Lake para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-174">To get started developing U-SQL applications, see [Develop U-SQL scripts using Data Lake Tools for Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).</span></span>
* <span data-ttu-id="ed8a7-175">Para aprender a usar o U-SQL, veja [Introdução à linguagem U-SQL da Análise do Azure Data Lake](data-lake-analytics-u-sql-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-175">To learn U-SQL, see [Get started with Azure Data Lake Analytics U-SQL language](data-lake-analytics-u-sql-get-started.md).</span></span>
* <span data-ttu-id="ed8a7-176">Para obter as tarefas de gerenciamento, confira [Gerenciar o Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-manage-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-176">For management tasks, see [Manage Azure Data Lake Analytics using Azure portal](data-lake-analytics-manage-use-portal.md).</span></span>
* <span data-ttu-id="ed8a7-177">Para obter uma visão geral da Análise do Data Lake, veja [Visão geral da Análise do Azure Data Lake](data-lake-analytics-overview.md).</span><span class="sxs-lookup"><span data-stu-id="ed8a7-177">To get an overview of Data Lake Analytics, see [Azure Data Lake Analytics overview](data-lake-analytics-overview.md).</span></span>
* <span data-ttu-id="ed8a7-178">Para ver o mesmo tutorial usando outras ferramentas, clique nos seletores de guias na parte superior da página.</span><span class="sxs-lookup"><span data-stu-id="ed8a7-178">To see the same tutorial using other tools, click the tab selectors on the top of the page.</span></span>

