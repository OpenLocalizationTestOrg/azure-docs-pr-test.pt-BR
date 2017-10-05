---
title: "Use a API REST para introdução ao Data Lake Store | Microsoft Docs"
description: "Usar as APIs REST WebHDFS para executar operações no Repositório Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 57ac6501-cb71-4f75-82c2-acc07c562889
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 04/21/2017
ms.author: nitinme
ms.openlocfilehash: dc2c8f58e0a2faf1b00f4903148328a5141a8637
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="c0aca-103">Introdução ao Repositório Azure Data Lake usando APIs REST</span><span class="sxs-lookup"><span data-stu-id="c0aca-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="c0aca-104">Portal</span><span class="sxs-lookup"><span data-stu-id="c0aca-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="c0aca-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="c0aca-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="c0aca-106">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="c0aca-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="c0aca-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="c0aca-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="c0aca-108">API REST</span><span class="sxs-lookup"><span data-stu-id="c0aca-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="c0aca-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="c0aca-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="c0aca-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="c0aca-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="c0aca-111">Python</span><span class="sxs-lookup"><span data-stu-id="c0aca-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="c0aca-112">Neste artigo, você aprenderá a usar as APIs REST WebHDFS e as APIs REST do Repositório Data Lake para executar o gerenciamento de contas e as operações de sistema de arquivos no Repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c0aca-112">In this article, you will learn how to use WebHDFS REST APIs and Data Lake Store REST APIs to perform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="c0aca-113">O Repositório Azure Data Lake expõe suas próprias APIs REST para operações de gerenciamento de conta.</span><span class="sxs-lookup"><span data-stu-id="c0aca-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="c0aca-114">No entanto, como o Repositório Data Lake é compatível com o ecossistema HDFS e Hadoop, ele oferece suporte usando as APIs REST WebHDFS para operações do sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="c0aca-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="c0aca-115">Para obter informações detalhadas sobre o suporte à API REST para o Repositório Data Lake, consulte [Referência da API REST do Repositório Azure Data Lake](https://msdn.microsoft.com/library/mt693424.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0aca-115">For detailed information on the REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="c0aca-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c0aca-116">Prerequisites</span></span>
* <span data-ttu-id="c0aca-117">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="c0aca-117">**An Azure subscription**.</span></span> <span data-ttu-id="c0aca-118">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="c0aca-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="c0aca-119">**Criar um aplicativo do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="c0aca-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="c0aca-120">Você pode usar o aplicativo Azure AD para autenticar o aplicativo Data Lake Store com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="c0aca-120">You use the Azure AD application to authenticate the Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="c0aca-121">Há diferentes abordagens para autenticar com o Azure AD, que são a **autenticação de usuário final** ou a **autenticação serviço a serviço**.</span><span class="sxs-lookup"><span data-stu-id="c0aca-121">There are different approaches to authenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="c0aca-122">Para obter instruções e saber mais sobre como se autenticar, veja [Autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [Autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="c0aca-122">For instructions and more information on how to authenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="c0aca-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="c0aca-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="c0aca-124">Este artigo usa cURL para demonstrar como fazer chamadas à API REST em uma conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c0aca-124">This article uses cURL to demonstrate how to make REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="c0aca-125">Como faço para me autenticar usando o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="c0aca-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="c0aca-126">Você pode usar duas abordagens para se autenticar usando o Azure Active Directory.</span><span class="sxs-lookup"><span data-stu-id="c0aca-126">You can use two approaches to authenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="c0aca-127">Autenticação do usuário (interativa)</span><span class="sxs-lookup"><span data-stu-id="c0aca-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="c0aca-128">Nesse cenário, o aplicativo solicita o logon do usuário e todas as operações são executadas no contexto do usuário.</span><span class="sxs-lookup"><span data-stu-id="c0aca-128">In this scenario, the application prompts the user to log in and all the operations are performed in the context of the user.</span></span> <span data-ttu-id="c0aca-129">Realize as seguintes etapas para a autenticação interativa.</span><span class="sxs-lookup"><span data-stu-id="c0aca-129">Perform the following steps for interactive authentication.</span></span>

1. <span data-ttu-id="c0aca-130">Por meio de seu aplicativo, redirecione o usuário para a seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="c0aca-130">Through your application, redirect the user to the following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="c0aca-131">\<<REDIRECT-URI> precisa ser codificado para uso em uma URL.</span><span class="sxs-lookup"><span data-stu-id="c0aca-131">\<REDIRECT-URI> needs to be encoded for use in a URL.</span></span> <span data-ttu-id="c0aca-132">Portanto, para https://localhost, use `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="c0aca-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="c0aca-133">Para os fins deste tutorial, é possível substituir os valores de espaço reservado na URL acima e colá-los na barra de endereços do navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="c0aca-133">For the purpose of this tutorial, you can replace the placeholder values in the URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="c0aca-134">Você será redirecionado para autenticar usando seu logon do Azure.</span><span class="sxs-lookup"><span data-stu-id="c0aca-134">You will be redirected to authenticate using your Azure login.</span></span> <span data-ttu-id="c0aca-135">Depois de fazer logon com êxito, a resposta será exibida na barra de endereços do navegador.</span><span class="sxs-lookup"><span data-stu-id="c0aca-135">Once you successfully log in, the response is displayed in the browser's address bar.</span></span> <span data-ttu-id="c0aca-136">A resposta estará no seguinte formato:</span><span class="sxs-lookup"><span data-stu-id="c0aca-136">The response will be in the following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="c0aca-137">Capture o código de autorização da resposta.</span><span class="sxs-lookup"><span data-stu-id="c0aca-137">Capture the authorization code from the response.</span></span> <span data-ttu-id="c0aca-138">Para este tutorial, é possível copiar o código de autorização da barra de endereços do navegador da Web e passá-lo na solicitação POST para o ponto de extremidade do token, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="c0aca-138">For this tutorial, you can copy the authorization code from the address bar of the web browser and pass it in the POST request to the token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="c0aca-139">Nesse caso, o \<REDIRECT-URI> não precisa ser codificado.</span><span class="sxs-lookup"><span data-stu-id="c0aca-139">In this case, the \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="c0aca-140">A resposta é um objeto JSON que contém um token de acesso (por exemplo, `"access_token": "<ACCESS_TOKEN>"`) e um token de atualização (por exemplo, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="c0aca-140">The response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="c0aca-141">Seu aplicativo usa o token de acesso ao acessar o Repositório Azure Data Lake e o token de atualização para obter outro token de acesso quando um token de acesso expira.</span><span class="sxs-lookup"><span data-stu-id="c0aca-141">Your application uses the access token when accessing Azure Data Lake Store and the refresh token to get another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="c0aca-142">Quando o token de acesso expira, é possível solicitar um novo token de acesso usando o token de atualização, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="c0aca-142">When the access token expires, you can request a new access token using the refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="c0aca-143">Para obter mais informações sobre a autenticação interativa de usuário, confira [Fluxo de concessão de código de autorização](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0aca-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="c0aca-144">Autenticação serviço a serviço (não interativa)</span><span class="sxs-lookup"><span data-stu-id="c0aca-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="c0aca-145">Nesse cenário, o aplicativo fornece suas próprias credenciais para executar as operações.</span><span class="sxs-lookup"><span data-stu-id="c0aca-145">In this scenario, the the application provides its own credentials to perform the operations.</span></span> <span data-ttu-id="c0aca-146">Para isso, você deve emitir uma solicitação POST como a mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="c0aca-146">For this, you must issue a POST request like the one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="c0aca-147">A saída dessa solicitação incluirá um token de autorização (indicado por `access-token` na saída abaixo) que você transmitirá posteriormente com as chamadas à API REST.</span><span class="sxs-lookup"><span data-stu-id="c0aca-147">The output of this request will include an authorization token (denoted by `access-token` in the output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="c0aca-148">Salve esse token de autenticação em um arquivo de texto. Você precisará dele posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="c0aca-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="c0aca-149">Este artigo usa uma abordagem **não interativa** .</span><span class="sxs-lookup"><span data-stu-id="c0aca-149">This article uses the **non-interactive** approach.</span></span> <span data-ttu-id="c0aca-150">Para saber mais sobre (chamadas de serviço a serviço) não interativas, confira [Chamadas de serviço a serviço usando credenciais](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0aca-150">For more information on non-interactive (service-to-service calls), see [Service to service calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="c0aca-151">Criar uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="c0aca-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="c0aca-152">Essa operação se baseia na chamada à API REST definida [aqui](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0aca-152">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="c0aca-153">Use o comando cURL a seguir.</span><span class="sxs-lookup"><span data-stu-id="c0aca-153">Use the following cURL command.</span></span> <span data-ttu-id="c0aca-154">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c0aca-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="c0aca-155">No comando acima, substitua \<`REDACTED`\> pelo token de autorização recuperado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c0aca-155">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="c0aca-156">A carga de solicitação para esse comando está contida no arquivo **input.json** fornecido para o parâmetro `-d` acima.</span><span class="sxs-lookup"><span data-stu-id="c0aca-156">The request payload for this command is contained in the **input.json** file that is provided for the `-d` parameter above.</span></span> <span data-ttu-id="c0aca-157">O conteúdo do arquivo input.json lembra o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c0aca-157">The contents of the input.json file resemble the following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="c0aca-158">Criar pastas na conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="c0aca-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="c0aca-159">Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="c0aca-159">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="c0aca-160">Use o comando cURL a seguir.</span><span class="sxs-lookup"><span data-stu-id="c0aca-160">Use the following cURL command.</span></span> <span data-ttu-id="c0aca-161">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c0aca-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="c0aca-162">No comando acima, substitua \<`REDACTED`\> pelo token de autorização recuperado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c0aca-162">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span> <span data-ttu-id="c0aca-163">Esse comando cria um diretório chamado **mytempdir** na pasta raiz da conta do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c0aca-163">This command creates a directory called **mytempdir** under the root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="c0aca-164">Você deverá ver uma resposta como esta caso a operação seja concluída com êxito:</span><span class="sxs-lookup"><span data-stu-id="c0aca-164">You should see a response like this if the operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="c0aca-165">Listar pastas em uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="c0aca-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="c0aca-166">Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="c0aca-166">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="c0aca-167">Use o comando cURL a seguir.</span><span class="sxs-lookup"><span data-stu-id="c0aca-167">Use the following cURL command.</span></span> <span data-ttu-id="c0aca-168">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c0aca-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="c0aca-169">No comando acima, substitua \<`REDACTED`\> pelo token de autorização recuperado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c0aca-169">In the above command, replace \<`REDACTED`\> with the authorization token you retrieved earlier.</span></span>

<span data-ttu-id="c0aca-170">Você deverá ver uma resposta como esta caso a operação seja concluída com êxito:</span><span class="sxs-lookup"><span data-stu-id="c0aca-170">You should see a response like this if the operation completes successfully:</span></span>

    {
    "FileStatuses": {
        "FileStatus": [{
            "length": 0,
            "pathSuffix": "mytempdir",
            "type": "DIRECTORY",
            "blockSize": 268435456,
            "accessTime": 1458324719512,
            "modificationTime": 1458324719512,
            "replication": 0,
            "permission": "777",
            "owner": "NotSupportYet",
            "group": "NotSupportYet"
        }]
    }
    }

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="c0aca-171">Carregar dados na conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="c0aca-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="c0aca-172">Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="c0aca-172">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="c0aca-173">Use o comando cURL a seguir.</span><span class="sxs-lookup"><span data-stu-id="c0aca-173">Use the following cURL command.</span></span> <span data-ttu-id="c0aca-174">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c0aca-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="c0aca-175">Na sintaxe acima o parâmetro **-T** é o local do arquivo que você está carregando.</span><span class="sxs-lookup"><span data-stu-id="c0aca-175">In the above syntax **-T** parameter is the location of the file you are uploading.</span></span>

<span data-ttu-id="c0aca-176">A saída deverá ser semelhante a esta:</span><span class="sxs-lookup"><span data-stu-id="c0aca-176">The output is similar to the following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="c0aca-177">Ler dados de uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="c0aca-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="c0aca-178">Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="c0aca-178">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="c0aca-179">A leitura de dados de uma conta do Repositório Data Lake é um processo de duas etapas.</span><span class="sxs-lookup"><span data-stu-id="c0aca-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="c0aca-180">Primeiro você envia uma solicitação GET para o ponto de extremidade `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="c0aca-180">You first submit a GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="c0aca-181">Isso retornará um local para o qual será enviada a próxima solicitação GET.</span><span class="sxs-lookup"><span data-stu-id="c0aca-181">This will return a location to submit the next GET request to.</span></span>
* <span data-ttu-id="c0aca-182">Em seguida, você enviará a solicitação GET para o ponto de extremidade `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="c0aca-182">You then submit the GET request against the endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="c0aca-183">Isso exibirá o conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="c0aca-183">This will display the contents of the file.</span></span>

<span data-ttu-id="c0aca-184">No entanto, como não há diferença nos parâmetros de entrada entre a primeira e a segunda etapa, é possível usar o parâmetro `-L` para enviar a primeira solicitação.</span><span class="sxs-lookup"><span data-stu-id="c0aca-184">However, because there is no difference in the input parameters between the first and the second step, you can use the `-L` parameter to submit the first request.</span></span> <span data-ttu-id="c0aca-185">`-L` combina duas solicitações em uma e fará com que a cURL refaça a solicitação no novo local.</span><span class="sxs-lookup"><span data-stu-id="c0aca-185">`-L` option essentially combines two requests into one and will make cURL redo the request on the new location.</span></span> <span data-ttu-id="c0aca-186">Por fim, a saída de todas as chamadas de solicitação é exibida, conforme mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="c0aca-186">Finally, the output from all the request calls is displayed, like shown below.</span></span> <span data-ttu-id="c0aca-187">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c0aca-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="c0aca-188">Você deverá ver um resultado semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="c0aca-188">You should see an output similar to the following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="c0aca-189">Renomear um arquivo em uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="c0aca-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="c0aca-190">Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="c0aca-190">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="c0aca-191">Use o comando cURL a seguir para renomear um arquivo.</span><span class="sxs-lookup"><span data-stu-id="c0aca-191">Use the following cURL command to rename a file.</span></span> <span data-ttu-id="c0aca-192">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c0aca-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="c0aca-193">Você deverá ver um resultado semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="c0aca-193">You should see an output similar to the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="c0aca-194">Excluir um arquivo de uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="c0aca-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="c0aca-195">Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="c0aca-195">This operation is based on the WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="c0aca-196">Use o comando cURL a seguir para excluir um arquivo.</span><span class="sxs-lookup"><span data-stu-id="c0aca-196">Use the following cURL command to delete a file.</span></span> <span data-ttu-id="c0aca-197">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c0aca-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="c0aca-198">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0aca-198">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="c0aca-199">Excluir uma conta do Repositório do Data Lake</span><span class="sxs-lookup"><span data-stu-id="c0aca-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="c0aca-200">Essa operação se baseia na chamada à API REST definida [aqui](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="c0aca-200">This operation is based on the REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="c0aca-201">Use o comando cURL a seguir para excluir uma conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="c0aca-201">Use the following cURL command to delete a Data Lake Store account.</span></span> <span data-ttu-id="c0aca-202">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="c0aca-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="c0aca-203">Você verá algo semelhante ao mostrado a seguir:</span><span class="sxs-lookup"><span data-stu-id="c0aca-203">You should see an output like the following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="c0aca-204">Confira também</span><span class="sxs-lookup"><span data-stu-id="c0aca-204">See also</span></span>
* [<span data-ttu-id="c0aca-205">Aplicativos de Big Data de software livre compatíveis com o Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="c0aca-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

