---
title: "aaaUse Olá SDK de Python tooget Introdução ao repositório Azure Data Lake | Microsoft Docs"
description: "Saiba como o sistema de arquivos toouse toowork de SDK de Python com contas do repositório Data Lake e hello."
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 75f6de6f-6fd8-48f4-8707-cb27d22d27a6
ms.service: data-lake-store
ms.devlang: na
ms.topic: get-started-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 7061fdf25ef607608bab618a20ddd3d6fc7af01d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-store-using-python"></a><span data-ttu-id="bc1fb-103">Introdução ao Azure Data Lake Store usando o Python</span><span class="sxs-lookup"><span data-stu-id="bc1fb-103">Get started with Azure Data Lake Store using Python</span></span>

> [!div class="op_single_selector"]
> * [<span data-ttu-id="bc1fb-104">Portal</span><span class="sxs-lookup"><span data-stu-id="bc1fb-104">Portal</span></span>](data-lake-store-get-started-portal.md)
> * [<span data-ttu-id="bc1fb-105">PowerShell</span><span class="sxs-lookup"><span data-stu-id="bc1fb-105">PowerShell</span></span>](data-lake-store-get-started-powershell.md)
> * [<span data-ttu-id="bc1fb-106">SDK .NET</span><span class="sxs-lookup"><span data-stu-id="bc1fb-106">.NET SDK</span></span>](data-lake-store-get-started-net-sdk.md)
> * [<span data-ttu-id="bc1fb-107">Java SDK</span><span class="sxs-lookup"><span data-stu-id="bc1fb-107">Java SDK</span></span>](data-lake-store-get-started-java-sdk.md)
> * [<span data-ttu-id="bc1fb-108">API REST</span><span class="sxs-lookup"><span data-stu-id="bc1fb-108">REST API</span></span>](data-lake-store-get-started-rest-api.md)
> * [<span data-ttu-id="bc1fb-109">CLI 2.0 do Azure</span><span class="sxs-lookup"><span data-stu-id="bc1fb-109">Azure CLI 2.0</span></span>](data-lake-store-get-started-cli-2.0.md)
> * [<span data-ttu-id="bc1fb-110">Node.js</span><span class="sxs-lookup"><span data-stu-id="bc1fb-110">Node.js</span></span>](data-lake-store-manage-use-nodejs.md)
> * [<span data-ttu-id="bc1fb-111">Python</span><span class="sxs-lookup"><span data-stu-id="bc1fb-111">Python</span></span>](data-lake-store-get-started-python.md)
>
>

<span data-ttu-id="bc1fb-112">Saiba como toouse Olá Python SDK do Azure e operações básicas do repositório Azure Data Lake tooperform como criam pastas, upload e download de arquivos de dados, etc. Para obter mais informações sobre o Data Lake, veja [Azure Data Lake Store](data-lake-store-overview.md).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-112">Learn how toouse hello Python SDK for Azure and Azure Data Lake Store tooperform basic operations such as create folders, upload and download data files, etc. For more information about Data Lake, see [Azure Data Lake Store](data-lake-store-overview.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bc1fb-113">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="bc1fb-113">Prerequisites</span></span>

* <span data-ttu-id="bc1fb-114">**Python**.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-114">**Python**.</span></span> <span data-ttu-id="bc1fb-115">Você pode baixar o Python [aqui](https://www.python.org/downloads/).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-115">You can download Python from [here](https://www.python.org/downloads/).</span></span> <span data-ttu-id="bc1fb-116">Este artigo usa o Python versão 3.5.2.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-116">This article uses Python 3.5.2.</span></span>

* <span data-ttu-id="bc1fb-117">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-117">**An Azure subscription**.</span></span> <span data-ttu-id="bc1fb-118">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-118">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>

* <span data-ttu-id="bc1fb-119">**Criar um aplicativo do Azure Active Directory**.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-119">**Create an Azure Active Directory Application**.</span></span> <span data-ttu-id="bc1fb-120">Você pode usar Olá AD do Azure tooauthenticate Olá repositório Data Lake aplicativo com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-120">You use hello Azure AD application tooauthenticate hello Data Lake Store application with Azure AD.</span></span> <span data-ttu-id="bc1fb-121">Há diferentes abordagens tooauthenticate com o AD do Azure, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-121">There are different approaches tooauthenticate with Azure AD, which are **end-user authentication** or **service-to-service authentication**.</span></span> <span data-ttu-id="bc1fb-122">Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-122">For instructions and more information on how tooauthenticate, see [End-user authentication](data-lake-store-end-user-authenticate-using-active-directory.md) or [Service-to-service authentication](data-lake-store-authenticate-using-active-directory.md).</span></span>

## <a name="install-hello-modules"></a><span data-ttu-id="bc1fb-123">Instalar módulos Olá</span><span class="sxs-lookup"><span data-stu-id="bc1fb-123">Install hello modules</span></span>

<span data-ttu-id="bc1fb-124">toowork com repositório Data Lake com Python, você precisa tooinstall três módulos.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-124">toowork with Data Lake Store using Python, you need tooinstall three modules.</span></span>

* <span data-ttu-id="bc1fb-125">Olá `azure-mgmt-resource` módulo.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-125">hello `azure-mgmt-resource` module.</span></span> <span data-ttu-id="bc1fb-126">Isso inclui módulos do Azure para o Active Directory, etc...</span><span class="sxs-lookup"><span data-stu-id="bc1fb-126">This includes Azure modules for Active Directory, etc..</span></span>
* <span data-ttu-id="bc1fb-127">Olá `azure-mgmt-datalake-store` módulo.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-127">hello `azure-mgmt-datalake-store` module.</span></span> <span data-ttu-id="bc1fb-128">Isso inclui operações de gerenciamento de conta de repositório Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-128">This includes hello Azure Data Lake Store account management operations.</span></span> <span data-ttu-id="bc1fb-129">Para obter mais informações sobre esse módulo, consulte [Referência do módulo de gerenciamento do Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-129">For more information on this module, see [Azure Data Lake Store Management module reference](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).</span></span>
* <span data-ttu-id="bc1fb-130">Olá `azure-datalake-store` módulo.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-130">hello `azure-datalake-store` module.</span></span> <span data-ttu-id="bc1fb-131">Isso inclui operações de sistema de arquivos do repositório Azure Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-131">This includes hello Azure Data Lake Store filesystem operations.</span></span> <span data-ttu-id="bc1fb-132">Para obter mais informações sobre esse módulo, consulte [Referência do módulo de Sistema de Arquivos do Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-132">For more information on this module, see [Azure Data Lake Store Filesystem module reference](http://azure-datalake-store.readthedocs.io/en/latest/).</span></span>

<span data-ttu-id="bc1fb-133">Use Olá módulos de saudação tooinstall comandos a seguir.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-133">Use hello following commands tooinstall hello modules.</span></span>

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a><span data-ttu-id="bc1fb-134">Criar um novo aplicativo Python</span><span class="sxs-lookup"><span data-stu-id="bc1fb-134">Create a new Python application</span></span>

1. <span data-ttu-id="bc1fb-135">No hello IDE de sua escolha, crie um novo aplicativo de Python, por exemplo, **mysample.py**.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-135">In hello IDE of your choice create a new Python application, for example, **mysample.py**.</span></span>

2. <span data-ttu-id="bc1fb-136">Adicionar Olá módulos de saudação necessário tooimport linhas a seguir</span><span class="sxs-lookup"><span data-stu-id="bc1fb-136">Add hello following lines tooimport hello required modules</span></span>

    ```
    ## Use this only for Azure AD service-to-service authentication
    from azure.common.credentials import ServicePrincipalCredentials

    ## Use this only for Azure AD end-user authentication
    from azure.common.credentials import UserPassCredentials

    ## Use this only for Azure AD multi-factor authentication
    from msrestazure.azure_active_directory import AADTokenCredentials

    ## Required for Azure Data Lake Store account management
    from azure.mgmt.datalake.store import DataLakeStoreAccountManagementClient
    from azure.mgmt.datalake.store.models import DataLakeStoreAccount

    ## Required for Azure Data Lake Store filesystem management
    from azure.datalake.store import core, lib, multithread

    # Common Azure imports
    from azure.mgmt.resource.resources import ResourceManagementClient
    from azure.mgmt.resource.resources.models import ResourceGroup

    ## Use these as needed for your application
    import logging, getpass, pprint, uuid, time
    ```

3. <span data-ttu-id="bc1fb-137">Salve alterações toomysample.py.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-137">Save changes toomysample.py.</span></span>

## <a name="authentication"></a><span data-ttu-id="bc1fb-138">Autenticação</span><span class="sxs-lookup"><span data-stu-id="bc1fb-138">Authentication</span></span>

<span data-ttu-id="bc1fb-139">Nesta seção, falamos sobre tooauthenticate de maneiras diferentes de saudação com o Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-139">In this section, we talk about hello different ways tooauthenticate with Azure AD.</span></span> <span data-ttu-id="bc1fb-140">Olá opções disponíveis são:</span><span class="sxs-lookup"><span data-stu-id="bc1fb-140">hello options available are:</span></span>

* <span data-ttu-id="bc1fb-141">Autenticação do usuário final</span><span class="sxs-lookup"><span data-stu-id="bc1fb-141">End-user authentication</span></span>
* <span data-ttu-id="bc1fb-142">Autenticação serviço a serviço</span><span class="sxs-lookup"><span data-stu-id="bc1fb-142">Service-to-service authentication</span></span>
* <span data-ttu-id="bc1fb-143">Autenticação multifator</span><span class="sxs-lookup"><span data-stu-id="bc1fb-143">Multi-factor authentication</span></span>

<span data-ttu-id="bc1fb-144">Você deve usar essas opções de autenticação para ambos os módulos de gerenciamento de contas e de gerenciamento do sistema.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-144">You must use these authentication options for both account management and filesystem management modules.</span></span>

### <a name="end-user-authentication-for-account-management"></a><span data-ttu-id="bc1fb-145">Autenticação de usuário final para o gerenciamento de conta</span><span class="sxs-lookup"><span data-stu-id="bc1fb-145">End-user authentication for account management</span></span>

<span data-ttu-id="bc1fb-146">Use este tooauthenticate com o AD do Azure para operações de gerenciamento de conta (Criar/excluir conta de repositório Data Lake, etc.).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-146">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="bc1fb-147">Você deve fornecer o nome de usuário e a senha para um usuário do Azure AD.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-147">You must provide username and password for an Azure AD user.</span></span> <span data-ttu-id="bc1fb-148">Observe que o usuário Olá não deve ser configurado para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-148">Note that hello user should not be configured for multi-factor authentication.</span></span>

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a><span data-ttu-id="bc1fb-149">Autenticação de usuário final para operações do sistema de arquivos</span><span class="sxs-lookup"><span data-stu-id="bc1fb-149">End-user authentication for filesystem operations</span></span>

<span data-ttu-id="bc1fb-150">Use este tooauthenticate com o AD do Azure para operações de sistema de arquivos (criar pasta, arquivo de upload, etc.).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-150">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="bc1fb-151">Use-o com um aplicativo de **cliente nativo** do Azure AD existente.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-151">Use this with an existing Azure AD **native client** application.</span></span> <span data-ttu-id="bc1fb-152">usuário de saudação do AD do Azure para que é fornecer credenciais não deve ser configurado para autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-152">hello Azure AD user you provide credentials for should not be configured for multi-factor authentication.</span></span>

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a><span data-ttu-id="bc1fb-153">Autenticação de serviço a serviço com o segredo do cliente para gerenciamento de conta</span><span class="sxs-lookup"><span data-stu-id="bc1fb-153">Service-to-service authentication with client secret for account management</span></span>

<span data-ttu-id="bc1fb-154">Use este tooauthenticate com o AD do Azure para operações de gerenciamento de conta (Criar/excluir conta de repositório Data Lake, etc.).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-154">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="bc1fb-155">Olá trecho de código a seguir pode ser usado tooauthenticate seu aplicativo não interativamente, usando o segredo de saudação do cliente para uma entidade de segurança do aplicativo / serviço.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-155">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="bc1fb-156">Use-o com o aplicativo "Aplicativo Web" Azure AD existente.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-156">Use this with an existing Azure AD "Web App" application.</span></span>

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a><span data-ttu-id="bc1fb-157">Autenticação de serviço a serviço com o segredo do cliente para operações do sistema de arquivos</span><span class="sxs-lookup"><span data-stu-id="bc1fb-157">Service-to-service authentication with client secret for filesystem operations</span></span>

<span data-ttu-id="bc1fb-158">Use este tooauthenticate com o AD do Azure para operações de sistema de arquivos (criar pasta, arquivo de upload, etc.).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-158">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="bc1fb-159">Olá trecho de código a seguir pode ser usado tooauthenticate seu aplicativo não interativamente, usando o segredo de saudação do cliente para uma entidade de segurança do aplicativo / serviço.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-159">hello following snippet can be used tooauthenticate your application non-interactively, using hello client secret for an application / service principal.</span></span> <span data-ttu-id="bc1fb-160">Use-o com o aplicativo "Aplicativo Web" Azure AD existente.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-160">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a><span data-ttu-id="bc1fb-161">Autenticação multifator para o gerenciamento de contas</span><span class="sxs-lookup"><span data-stu-id="bc1fb-161">Multi-factor authentication for account management</span></span>

<span data-ttu-id="bc1fb-162">Use este tooauthenticate com o AD do Azure para operações de gerenciamento de conta (Criar/excluir conta de repositório Data Lake, etc.).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-162">Use this tooauthenticate with Azure AD for account management operations (create/delete Data Lake Store account, etc.).</span></span> <span data-ttu-id="bc1fb-163">Olá trecho a seguir pode ser usado tooauthenticate seu aplicativo usando a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-163">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="bc1fb-164">Use-o com o aplicativo "Aplicativo Web" Azure AD existente.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-164">Use this with an existing Azure AD "Web App" application.</span></span>

    authority_host_url = "https://login.microsoftonline.com"
    tenant = "FILL-IN-HERE"
    authority_url = authority_host_url + '/' + tenant
    client_id = 'FILL-IN-HERE'
    redirect = 'urn:ietf:wg:oauth:2.0:oob'
    RESOURCE = 'https://management.core.windows.net/'
    
    context = adal.AuthenticationContext(authority_url)
    code = context.acquire_user_code(RESOURCE, client_id)
    print(code['message'])
    mgmt_token = context.acquire_token_with_device_code(RESOURCE, code, client_id)
    credentials = AADTokenCredentials(mgmt_token, client_id)

### <a name="multi-factor-authentication-for-filesystem-management"></a><span data-ttu-id="bc1fb-165">Autenticação multifator para gerenciamento do sistema de arquivos</span><span class="sxs-lookup"><span data-stu-id="bc1fb-165">Multi-factor authentication for filesystem management</span></span>

<span data-ttu-id="bc1fb-166">Use este tooauthenticate com o AD do Azure para operações de sistema de arquivos (criar pasta, arquivo de upload, etc.).</span><span class="sxs-lookup"><span data-stu-id="bc1fb-166">Use this tooauthenticate with Azure AD for filesystem operations (create folder, upload file, etc.).</span></span> <span data-ttu-id="bc1fb-167">Olá trecho a seguir pode ser usado tooauthenticate seu aplicativo usando a autenticação multifator.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-167">hello following snippet can be used tooauthenticate your application using multi-factor authentication.</span></span> <span data-ttu-id="bc1fb-168">Use-o com o aplicativo "Aplicativo Web" Azure AD existente.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-168">Use this with an existing Azure AD "Web App" application.</span></span>

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a><span data-ttu-id="bc1fb-169">Criar um grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="bc1fb-169">Create an Azure Resource Group</span></span>

<span data-ttu-id="bc1fb-170">Use Olá seguindo o trecho de código toocreate um grupo de recursos do Azure:</span><span class="sxs-lookup"><span data-stu-id="bc1fb-170">Use hello following code snippet toocreate an Azure Resource Group:</span></span>

    ## Declare variables
    subscriptionId= 'FILL-IN-HERE'
    resourceGroup = 'FILL-IN-HERE'
    location = 'eastus2'
    
    ## Create management client object
    resourceClient = ResourceManagementClient(
        credentials,
        subscriptionId
    )
    
    ## Create an Azure Resource Group
    resourceClient.resource_groups.create_or_update(
        resourceGroup,
        ResourceGroup(
            location=location
        )
    )

## <a name="create-clients-and-data-lake-store-account"></a><span data-ttu-id="bc1fb-171">Crie uma conta do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bc1fb-171">Create clients and Data Lake Store account</span></span>

<span data-ttu-id="bc1fb-172">Olá trecho de código a seguir primeiro cria um cliente de conta do repositório Data Lake hello.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-172">hello following snippet first creates hello Data Lake Store account client.</span></span> <span data-ttu-id="bc1fb-173">Ele usa Olá cliente objeto toocreate uma conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-173">It uses hello client object toocreate a Data Lake Store account.</span></span> <span data-ttu-id="bc1fb-174">Por fim, o trecho de saudação cria um objeto de cliente do sistema de arquivos.</span><span class="sxs-lookup"><span data-stu-id="bc1fb-174">Finally, hello snippet creates a filesystem client object.</span></span>

    ## Declare variables
    subscriptionId = 'FILL-IN-HERE'
    adlsAccountName = 'FILL-IN-HERE'

    ## Create management client object
    adlsAcctClient = DataLakeStoreAccountManagementClient(credentials, subscriptionId)

    ## Create a Data Lake Store account
    adlsAcctResult = adlsAcctClient.account.create(
        resourceGroup,
        adlsAccountName,
        DataLakeStoreAccount(
            location=location
        )
    ).wait()

    ## Create a filesystem client object
    adlsFileSystemClient = core.AzureDLFileSystem(token, store_name=adlsAccountName)

## <a name="list-hello-data-lake-store-accounts"></a><span data-ttu-id="bc1fb-175">Lista de contas do repositório Data Lake Olá</span><span class="sxs-lookup"><span data-stu-id="bc1fb-175">List hello Data Lake Store accounts</span></span>

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a><span data-ttu-id="bc1fb-176">Criar um diretório</span><span class="sxs-lookup"><span data-stu-id="bc1fb-176">Create a directory</span></span>

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a><span data-ttu-id="bc1fb-177">Carregar um arquivo</span><span class="sxs-lookup"><span data-stu-id="bc1fb-177">Upload a file</span></span>


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a><span data-ttu-id="bc1fb-178">Baixar um arquivo</span><span class="sxs-lookup"><span data-stu-id="bc1fb-178">Download a file</span></span>

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a><span data-ttu-id="bc1fb-179">Excluir um diretório</span><span class="sxs-lookup"><span data-stu-id="bc1fb-179">Delete a directory</span></span>

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a><span data-ttu-id="bc1fb-180">Consulte também</span><span class="sxs-lookup"><span data-stu-id="bc1fb-180">See also</span></span>

- [<span data-ttu-id="bc1fb-181">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="bc1fb-181">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
- [<span data-ttu-id="bc1fb-182">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="bc1fb-182">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [<span data-ttu-id="bc1fb-183">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="bc1fb-183">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
- [<span data-ttu-id="bc1fb-184">Referência do SDK do .NET do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bc1fb-184">Data Lake Store .NET SDK Reference</span></span>](https://msdn.microsoft.com/library/mt581387.aspx)
- [<span data-ttu-id="bc1fb-185">Referência do REST do Azure Data Lake Store</span><span class="sxs-lookup"><span data-stu-id="bc1fb-185">Data Lake Store REST Reference</span></span>](https://msdn.microsoft.com/library/mt693424.aspx)
