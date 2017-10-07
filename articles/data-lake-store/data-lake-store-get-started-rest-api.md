---
title: "aaaUse Olá API REST tooget Introdução ao repositório Data Lake | Microsoft Docs"
description: "Use APIs de REST WebHDFS tooperform operações no repositório Data Lake"
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
ms.openlocfilehash: 62fce8293dfee730a61f2a3d37fc138ce7c3afdf
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a><span data-ttu-id="45645-103">Introdução ao Repositório Azure Data Lake usando APIs REST</span><span class="sxs-lookup"><span data-stu-id="45645-103">Get started with Azure Data Lake Store using REST APIs</span></span>
> [!div class="op_single_selector"]
> * [<span data-ttu-id="45645-104">Portal</span><span class="sxs-lookup"><span data-stu-id="45645-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="45645-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="45645-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="45645-106">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="45645-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="45645-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="45645-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="45645-108">API REST</span><span class="sxs-lookup"><span data-stu-id="45645-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="45645-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="45645-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="45645-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="45645-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="45645-111">Python</span><span class="sxs-lookup"><span data-stu-id="45645-111">Python</span></span>](data-lake-store-get-started-python.md)
>
> 

<span data-ttu-id="45645-112">Neste artigo, você aprenderá como toouse WebHDFS APIs de REST e APIs de REST de repositório Data Lake tooperform conta de gerenciamento, bem como operações de sistema de arquivos no repositório Azure Data Lake.</span><span class="sxs-lookup"><span data-stu-id="45645-112">In this article, you will learn how toouse WebHDFS REST APIs and Data Lake Store REST APIs tooperform account management as well as filesystem operations on Azure Data Lake Store.</span></span> <span data-ttu-id="45645-113">O Repositório Azure Data Lake expõe suas próprias APIs REST para operações de gerenciamento de conta.</span><span class="sxs-lookup"><span data-stu-id="45645-113">Azure Data Lake Store exposes its own REST APIs for account management operations.</span></span> <span data-ttu-id="45645-114">No entanto, como o Repositório Data Lake é compatível com o ecossistema HDFS e Hadoop, ele oferece suporte usando as APIs REST WebHDFS para operações do sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="45645-114">However, because Data Lake Store is compatible with HDFS and Hadoop ecosystem, it supports using WebHDFS REST APIs for filesystem operations.</span></span>

> [!NOTE]
> <span data-ttu-id="45645-115">Para obter informações detalhadas sobre o suporte de API REST de saudação do repositório Data Lake, consulte [referência de API de REST do Azure Data Lake repositório](https://msdn.microsoft.com/library/mt693424.aspx).</span><span class="sxs-lookup"><span data-stu-id="45645-115">For detailed information on hello REST API support for Data Lake Store, see [Azure Data Lake Store REST API Reference](https://msdn.microsoft.com/library/mt693424.aspx).</span></span>
> 
> 

## <a name="prerequisites"></a><span data-ttu-id="45645-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="45645-116">Prerequisites</span></span>
* <span data-ttu-id="45645-117">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="45645-117">**An Azure subscription**.</span></span> <span data-ttu-id="45645-118">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="45645-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="45645-119">**Criar um aplicativo do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="45645-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="45645-120">Você pode usar Olá AD do Azure tooauthenticate Olá repositório Data Lake aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="45645-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="45645-121">Há diferentes abordagens tooauthenticate com o AD do Azure, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**.</span><span class="sxs-lookup"><span data-stu-id="45645-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="45645-122">Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="45645-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>
* <span data-ttu-id="45645-123">[cURL](http://curl.haxx.se/).</span><span class="sxs-lookup"><span data-stu-id="45645-123">[cURL](http://curl.haxx.se/).</span></span> <span data-ttu-id="45645-124">Este artigo usa ondulação toodemonstrate como toomake API REST chama em uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="45645-124">This article uses cURL toodemonstrate how toomake REST API calls against a Data Lake Store account.</span></span>

## <a name="how-do-i-authenticate-using-azure-active-directory"></a><span data-ttu-id="45645-125">Como faço para me autenticar usando o Azure Active Directory?</span><span class="sxs-lookup"><span data-stu-id="45645-125">How do I authenticate using Azure Active Directory?</span></span>
<span data-ttu-id="45645-126">Você pode usar dois tooauthenticate abordagens usando o Active Directory do Azure.</span><span class="sxs-lookup"><span data-stu-id="45645-126">You can use two approaches tooauthenticate using Azure Active Directory.</span></span>

### <a name="end-user-authentication-interactive"></a><span data-ttu-id="45645-127">Autenticação do usuário (interativa)</span><span class="sxs-lookup"><span data-stu-id="45645-127">End-user authentication (interactive)</span></span>
<span data-ttu-id="45645-128">Nesse cenário, aplicativo hello solicita Olá usuário toolog em e todas as operações de saudação são executadas no contexto de saudação do usuário de saudação.</span><span class="sxs-lookup"><span data-stu-id="45645-128">In this scenario, hello application prompts hello user toolog in and all hello operations are performed in hello context of hello user.</span></span> <span data-ttu-id="45645-129">Execute Olá seguindo as etapas para a autenticação interativa.</span><span class="sxs-lookup"><span data-stu-id="45645-129">Perform hello following steps for interactive authentication.</span></span>

1. <span data-ttu-id="45645-130">Por meio de seu aplicativo, redirecione Olá usuário toohello URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="45645-130">Through your application, redirect hello user toohello following URL:</span></span>
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > <span data-ttu-id="45645-131">\<URI de REDIRECIONAMENTO > precisa toobe codificado para uso em uma URL.</span><span class="sxs-lookup"><span data-stu-id="45645-131">\<REDIRECT-URI> needs toobe encoded for use in a URL.</span></span> <span data-ttu-id="45645-132">Portanto, para https://localhost, use `https%3A%2F%2Flocalhost`)</span><span class="sxs-lookup"><span data-stu-id="45645-132">So, for https://localhost, use `https%3A%2F%2Flocalhost`)</span></span>
   > 
   > 
   
    <span data-ttu-id="45645-133">Para finalidade de saudação deste tutorial, você pode substituir os valores de espaço reservado Olá Olá URL acima e cole-o na barra de endereços do navegador.</span><span class="sxs-lookup"><span data-stu-id="45645-133">For hello purpose of this tutorial, you can replace hello placeholder values in hello URL above and paste it in a web browser's address bar.</span></span> <span data-ttu-id="45645-134">Você será redirecionado tooauthenticate usando o logon do Azure.</span><span class="sxs-lookup"><span data-stu-id="45645-134">You will be redirected tooauthenticate using your Azure login.</span></span> <span data-ttu-id="45645-135">Depois que você fizer logon, a resposta de saudação é exibida na barra de endereços do navegador hello.</span><span class="sxs-lookup"><span data-stu-id="45645-135">Once you successfully log in, hello response is displayed in hello browser's address bar.</span></span> <span data-ttu-id="45645-136">resposta de saudação será em Olá formato a seguir:</span><span class="sxs-lookup"><span data-stu-id="45645-136">hello response will be in hello following format:</span></span>
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. <span data-ttu-id="45645-137">Capture o código de autorização de saudação da resposta de saudação.</span><span class="sxs-lookup"><span data-stu-id="45645-137">Capture hello authorization code from hello response.</span></span> <span data-ttu-id="45645-138">Para este tutorial, você pode copiar o código de autorização Olá Olá na barra de endereços do navegador da web de saudação e passá-lo no hello POST solicitação toohello token ponto de extremidade, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="45645-138">For this tutorial, you can copy hello authorization code from hello address bar of hello web browser and pass it in hello POST request toohello token endpoint, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > <span data-ttu-id="45645-139">Nesse caso, Olá \<URI de REDIRECIONAMENTO > não precisa ser codificado.</span><span class="sxs-lookup"><span data-stu-id="45645-139">In this case, hello \<REDIRECT-URI> need not be encoded.</span></span>
   > 
   > 
3. <span data-ttu-id="45645-140">resposta de saudação é um objeto JSON que contém um token de acesso (por exemplo, `"access_token": "<ACCESS_TOKEN>"`) e um token de atualização (por exemplo, `"refresh_token": "<REFRESH_TOKEN>"`).</span><span class="sxs-lookup"><span data-stu-id="45645-140">hello response is a JSON object that contains an access token (e.g., `"access_token": "<ACCESS_TOKEN>"`) and a refresh token (e.g., `"refresh_token": "<REFRESH_TOKEN>"`).</span></span> <span data-ttu-id="45645-141">Seu aplicativo usa o token de acesso Olá ao acessar o repositório Azure Data Lake e tooget de token de atualização de saudação outro token de acesso quando um token de acesso expira.</span><span class="sxs-lookup"><span data-stu-id="45645-141">Your application uses hello access token when accessing Azure Data Lake Store and hello refresh token tooget another access token when an access token expires.</span></span>
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. <span data-ttu-id="45645-142">Quando o token de acesso de saudação expirar, você pode solicitar um novo token de acesso usando o token de atualização hello, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="45645-142">When hello access token expires, you can request a new access token using hello refresh token, as shown below:</span></span>
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

<span data-ttu-id="45645-143">Para obter mais informações sobre a autenticação interativa de usuário, confira [Fluxo de concessão de código de autorização](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span><span class="sxs-lookup"><span data-stu-id="45645-143">For more information on interactive user authentication, see [Authorization code grant flow](https://msdn.microsoft.com/library/azure/dn645542.aspx).</span></span>

### <a name="service-to-service-authentication-non-interactive"></a><span data-ttu-id="45645-144">Autenticação serviço a serviço (não interativa)</span><span class="sxs-lookup"><span data-stu-id="45645-144">Service-to-service authentication (non-interactive)</span></span>
<span data-ttu-id="45645-145">Nesse cenário, o aplicativo de saudação do hello fornece suas próprias credenciais tooperform operações de saudação.</span><span class="sxs-lookup"><span data-stu-id="45645-145">In this scenario, hello hello application provides its own credentials tooperform hello operations.</span></span> <span data-ttu-id="45645-146">Para isso, você deverá emitir uma solicitação POST como Olá mostrada abaixo.</span><span class="sxs-lookup"><span data-stu-id="45645-146">For this, you must issue a POST request like hello one shown below.</span></span> 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

<span data-ttu-id="45645-147">saída de Hello desta solicitação incluirá um token de autorização (indicado por `access-token` na saída de hello abaixo) que você passará subsequentemente com suas chamadas de API REST.</span><span class="sxs-lookup"><span data-stu-id="45645-147">hello output of this request will include an authorization token (denoted by `access-token` in hello output below) that you will subsequently pass with your REST API calls.</span></span> <span data-ttu-id="45645-148">Salve esse token de autenticação em um arquivo de texto. Você precisará dele posteriormente neste artigo.</span><span class="sxs-lookup"><span data-stu-id="45645-148">Save this authentication token in a text file; you will need this later in this article.</span></span>

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

<span data-ttu-id="45645-149">Este artigo usa Olá **não interativo** abordagem.</span><span class="sxs-lookup"><span data-stu-id="45645-149">This article uses hello **non-interactive** approach.</span></span> <span data-ttu-id="45645-150">Para obter mais informações sobre não interativo (chamadas de serviços), consulte [tooservice chamadas usando as credenciais do serviço](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span><span class="sxs-lookup"><span data-stu-id="45645-150">For more information on non-interactive (service-to-service calls), see [Service tooservice calls using credentials](https://msdn.microsoft.com/library/azure/dn645543.aspx).</span></span>

## <a name="create-a-data-lake-store-account"></a><span data-ttu-id="45645-151">Criar uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="45645-151">Create a Data Lake Store account</span></span>
<span data-ttu-id="45645-152">Esta operação baseia-se a chamada hello API REST definida [aqui](https://msdn.microsoft.com/library/mt694078.aspx).</span><span class="sxs-lookup"><span data-stu-id="45645-152">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694078.aspx).</span></span>

<span data-ttu-id="45645-153">Use Olá ondulação de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="45645-153">Use hello following cURL command.</span></span> <span data-ttu-id="45645-154">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45645-154">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

<span data-ttu-id="45645-155">Olá acima de comando, substitua \< `REDACTED` \> com token de autorização Olá recuperados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="45645-155">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="45645-156">carga de solicitação Olá para este comando está contida no hello **input.json** arquivo que é fornecido para Olá `-d` parâmetro acima.</span><span class="sxs-lookup"><span data-stu-id="45645-156">hello request payload for this command is contained in hello **input.json** file that is provided for hello `-d` parameter above.</span></span> <span data-ttu-id="45645-157">conteúdo de saudação do arquivo de input.json Olá semelhante a seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="45645-157">hello contents of hello input.json file resemble hello following:</span></span>

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a><span data-ttu-id="45645-158">Criar pastas na conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="45645-158">Create folders in a Data Lake Store account</span></span>
<span data-ttu-id="45645-159">Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="45645-159">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).</span></span>

<span data-ttu-id="45645-160">Use Olá ondulação de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="45645-160">Use hello following cURL command.</span></span> <span data-ttu-id="45645-161">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45645-161">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

<span data-ttu-id="45645-162">Olá acima de comando, substitua \< `REDACTED` \> com token de autorização Olá recuperados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="45645-162">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span> <span data-ttu-id="45645-163">Este comando cria um diretório chamado **mytempdir** na pasta raiz de saudação da sua conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="45645-163">This command creates a directory called **mytempdir** under hello root folder of your Data Lake Store account.</span></span>

<span data-ttu-id="45645-164">Se a operação de saudação for concluído com êxito, você deve ver uma resposta como este:</span><span class="sxs-lookup"><span data-stu-id="45645-164">You should see a response like this if hello operation completes successfully:</span></span>

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a><span data-ttu-id="45645-165">Listar pastas em uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="45645-165">List folders in a Data Lake Store account</span></span>
<span data-ttu-id="45645-166">Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span><span class="sxs-lookup"><span data-stu-id="45645-166">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).</span></span>

<span data-ttu-id="45645-167">Use Olá ondulação de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="45645-167">Use hello following cURL command.</span></span> <span data-ttu-id="45645-168">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45645-168">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

<span data-ttu-id="45645-169">Olá acima de comando, substitua \< `REDACTED` \> com token de autorização Olá recuperados anteriormente.</span><span class="sxs-lookup"><span data-stu-id="45645-169">In hello above command, replace \<`REDACTED`\> with hello authorization token you retrieved earlier.</span></span>

<span data-ttu-id="45645-170">Se a operação de saudação for concluído com êxito, você deve ver uma resposta como este:</span><span class="sxs-lookup"><span data-stu-id="45645-170">You should see a response like this if hello operation completes successfully:</span></span>

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

## <a name="upload-data-into-a-data-lake-store-account"></a><span data-ttu-id="45645-171">Carregar dados na conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="45645-171">Upload data into a Data Lake Store account</span></span>
<span data-ttu-id="45645-172">Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span><span class="sxs-lookup"><span data-stu-id="45645-172">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).</span></span>

<span data-ttu-id="45645-173">Use Olá ondulação de comando a seguir.</span><span class="sxs-lookup"><span data-stu-id="45645-173">Use hello following cURL command.</span></span> <span data-ttu-id="45645-174">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45645-174">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

<span data-ttu-id="45645-175">Em Olá acima sintaxe **-T** parâmetro é o local de saudação do arquivo hello você está carregando.</span><span class="sxs-lookup"><span data-stu-id="45645-175">In hello above syntax **-T** parameter is hello location of hello file you are uploading.</span></span>

<span data-ttu-id="45645-176">saída de Hello é a seguir toohello semelhante:</span><span class="sxs-lookup"><span data-stu-id="45645-176">hello output is similar toohello following:</span></span>
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a><span data-ttu-id="45645-177">Ler dados de uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="45645-177">Read data from a Data Lake Store account</span></span>
<span data-ttu-id="45645-178">Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span><span class="sxs-lookup"><span data-stu-id="45645-178">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).</span></span>

<span data-ttu-id="45645-179">A leitura de dados de uma conta do Repositório Data Lake é um processo de duas etapas.</span><span class="sxs-lookup"><span data-stu-id="45645-179">Reading data from a Data Lake Store account is a two-step process.</span></span>

* <span data-ttu-id="45645-180">Enviar uma solicitação GET no ponto de extremidade Olá primeiro `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span><span class="sxs-lookup"><span data-stu-id="45645-180">You first submit a GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`.</span></span> <span data-ttu-id="45645-181">Isso retornará uma local toosubmit Olá próxima solicitação GET para.</span><span class="sxs-lookup"><span data-stu-id="45645-181">This will return a location toosubmit hello next GET request to.</span></span>
* <span data-ttu-id="45645-182">Em seguida, enviar solicitação GET hello no ponto de extremidade Olá `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span><span class="sxs-lookup"><span data-stu-id="45645-182">You then submit hello GET request against hello endpoint `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`.</span></span> <span data-ttu-id="45645-183">Isso exibirá o conteúdo de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="45645-183">This will display hello contents of hello file.</span></span>

<span data-ttu-id="45645-184">No entanto, porque não há nenhuma diferença em hello parâmetros de entrada entre hello primeiro e hello segunda etapa, você pode usar o hello `-L` primeira solicitação de parâmetro toosubmit hello.</span><span class="sxs-lookup"><span data-stu-id="45645-184">However, because there is no difference in hello input parameters between hello first and hello second step, you can use hello `-L` parameter toosubmit hello first request.</span></span> <span data-ttu-id="45645-185">`-L`opção essencialmente combina duas solicitações em um e tornará ondulação Refazer Olá solicitação no novo local de saudação.</span><span class="sxs-lookup"><span data-stu-id="45645-185">`-L` option essentially combines two requests into one and will make cURL redo hello request on hello new location.</span></span> <span data-ttu-id="45645-186">Por fim, Olá saída de todas as chamadas de solicitação de saudação é exibida, como mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="45645-186">Finally, hello output from all hello request calls is displayed, like shown below.</span></span> <span data-ttu-id="45645-187">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45645-187">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

<span data-ttu-id="45645-188">Você verá uma saída semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="45645-188">You should see an output similar toohello following:</span></span>

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a><span data-ttu-id="45645-189">Renomear um arquivo em uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="45645-189">Rename a file in a Data Lake Store account</span></span>
<span data-ttu-id="45645-190">Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="45645-190">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).</span></span>

<span data-ttu-id="45645-191">A seguir use Olá cURL comando toorename um arquivo.</span><span class="sxs-lookup"><span data-stu-id="45645-191">Use hello following cURL command toorename a file.</span></span> <span data-ttu-id="45645-192">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45645-192">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

<span data-ttu-id="45645-193">Você verá uma saída semelhante toohello a seguir:</span><span class="sxs-lookup"><span data-stu-id="45645-193">You should see an output similar toohello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a><span data-ttu-id="45645-194">Excluir um arquivo de uma conta do Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="45645-194">Delete a file from a Data Lake Store account</span></span>
<span data-ttu-id="45645-195">Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span><span class="sxs-lookup"><span data-stu-id="45645-195">This operation is based on hello WebHDFS REST API call defined [here](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).</span></span>

<span data-ttu-id="45645-196">A seguir use Olá cURL comando toodelete um arquivo.</span><span class="sxs-lookup"><span data-stu-id="45645-196">Use hello following cURL command toodelete a file.</span></span> <span data-ttu-id="45645-197">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45645-197">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

<span data-ttu-id="45645-198">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="45645-198">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a><span data-ttu-id="45645-199">Excluir uma conta do Repositório do Data Lake</span><span class="sxs-lookup"><span data-stu-id="45645-199">Delete a Data Lake Store account</span></span>
<span data-ttu-id="45645-200">Esta operação baseia-se a chamada hello API REST definida [aqui](https://msdn.microsoft.com/library/mt694075.aspx).</span><span class="sxs-lookup"><span data-stu-id="45645-200">This operation is based on hello REST API call defined [here](https://msdn.microsoft.com/library/mt694075.aspx).</span></span>

<span data-ttu-id="45645-201">A seguir use Olá cURL comando toodelete uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="45645-201">Use hello following cURL command toodelete a Data Lake Store account.</span></span> <span data-ttu-id="45645-202">Substitua **\<nomedorepositório** pelo nome do Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="45645-202">Replace **\<yourstorename>** with your Data Lake Store name.</span></span>

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

<span data-ttu-id="45645-203">Você verá uma saída semelhante Olá seguinte:</span><span class="sxs-lookup"><span data-stu-id="45645-203">You should see an output like hello following:</span></span>

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a><span data-ttu-id="45645-204">Consulte também</span><span class="sxs-lookup"><span data-stu-id="45645-204">See also</span></span>
* [<span data-ttu-id="45645-205">Aplicativos de Big Data de software livre compatíveis com o Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="45645-205">Open Source Big Data applications compatible with Azure Data Lake Store</span></span>](data-lake-store-compatible-oss-other-applications.md)

