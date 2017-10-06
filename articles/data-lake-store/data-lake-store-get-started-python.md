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
# <a name="get-started-with-azure-data-lake-store-using-python"></a>Introdução ao Azure Data Lake Store usando o Python

> [!div class="op_single_selector"]
> * [Portal](data-lake-store-get-started-portal.md)
> * [PowerShell](data-lake-store-get-started-powershell.md)
> * [SDK .NET](data-lake-store-get-started-net-sdk.md)
> * [Java SDK](data-lake-store-get-started-java-sdk.md)
> * [API REST](data-lake-store-get-started-rest-api.md)
> * [CLI 2.0 do Azure](data-lake-store-get-started-cli-2.0.md)
> * [Node.js](data-lake-store-manage-use-nodejs.md)
> * [Python](data-lake-store-get-started-python.md)
>
>

Saiba como toouse Olá Python SDK do Azure e operações básicas do repositório Azure Data Lake tooperform como criam pastas, upload e download de arquivos de dados, etc. Para obter mais informações sobre o Data Lake, veja [Azure Data Lake Store](data-lake-store-overview.md).

## <a name="prerequisites"></a>Pré-requisitos

* **Python**. Você pode baixar o Python [aqui](https://www.python.org/downloads/). Este artigo usa o Python versão 3.5.2.

* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).

* **Criar um aplicativo do Azure Active Directory**. Você pode usar Olá AD do Azure tooauthenticate Olá repositório Data Lake aplicativo com o Azure AD. Há diferentes abordagens tooauthenticate com o AD do Azure, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**. Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).

## <a name="install-hello-modules"></a>Instalar módulos Olá

toowork com repositório Data Lake com Python, você precisa tooinstall três módulos.

* Olá `azure-mgmt-resource` módulo. Isso inclui módulos do Azure para o Active Directory, etc...
* Olá `azure-mgmt-datalake-store` módulo. Isso inclui operações de gerenciamento de conta de repositório Azure Data Lake hello. Para obter mais informações sobre esse módulo, consulte [Referência do módulo de gerenciamento do Azure Data Lake Store](http://azure-sdk-for-python.readthedocs.io/en/latest/sample_azure-mgmt-datalake-store.html).
* Olá `azure-datalake-store` módulo. Isso inclui operações de sistema de arquivos do repositório Azure Data Lake hello. Para obter mais informações sobre esse módulo, consulte [Referência do módulo de Sistema de Arquivos do Azure Data Lake Store](http://azure-datalake-store.readthedocs.io/en/latest/).

Use Olá módulos de saudação tooinstall comandos a seguir.

```
pip install azure-mgmt-resource
pip install azure-mgmt-datalake-store
pip install azure-datalake-store
```

## <a name="create-a-new-python-application"></a>Criar um novo aplicativo Python

1. No hello IDE de sua escolha, crie um novo aplicativo de Python, por exemplo, **mysample.py**.

2. Adicionar Olá módulos de saudação necessário tooimport linhas a seguir

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

3. Salve alterações toomysample.py.

## <a name="authentication"></a>Autenticação

Nesta seção, falamos sobre tooauthenticate de maneiras diferentes de saudação com o Azure AD. Olá opções disponíveis são:

* Autenticação do usuário final
* Autenticação serviço a serviço
* Autenticação multifator

Você deve usar essas opções de autenticação para ambos os módulos de gerenciamento de contas e de gerenciamento do sistema.

### <a name="end-user-authentication-for-account-management"></a>Autenticação de usuário final para o gerenciamento de conta

Use este tooauthenticate com o AD do Azure para operações de gerenciamento de conta (Criar/excluir conta de repositório Data Lake, etc.). Você deve fornecer o nome de usuário e a senha para um usuário do Azure AD. Observe que o usuário Olá não deve ser configurado para autenticação multifator.

    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    credentials = UserPassCredentials(user, password)

### <a name="end-user-authentication-for-filesystem-operations"></a>Autenticação de usuário final para operações do sistema de arquivos

Use este tooauthenticate com o AD do Azure para operações de sistema de arquivos (criar pasta, arquivo de upload, etc.). Use-o com um aplicativo de **cliente nativo** do Azure AD existente. usuário de saudação do AD do Azure para que é fornecer credenciais não deve ser configurado para autenticação multifator.

    tenant_id = 'FILL-IN-HERE'
    client_id = 'FILL-IN-HERE'
    user = input('Enter hello user tooauthenticate with that has permission toosubscription: ')
    password = getpass.getpass()

    token = lib.auth(tenant_id, user, password, client_id)

### <a name="service-to-service-authentication-with-client-secret-for-account-management"></a>Autenticação de serviço a serviço com o segredo do cliente para gerenciamento de conta

Use este tooauthenticate com o AD do Azure para operações de gerenciamento de conta (Criar/excluir conta de repositório Data Lake, etc.). Olá trecho de código a seguir pode ser usado tooauthenticate seu aplicativo não interativamente, usando o segredo de saudação do cliente para uma entidade de segurança do aplicativo / serviço. Use-o com o aplicativo "Aplicativo Web" Azure AD existente.

    credentials = ServicePrincipalCredentials(client_id = 'FILL-IN-HERE', secret = 'FILL-IN-HERE', tenant = 'FILL-IN-HERE')

### <a name="service-to-service-authentication-with-client-secret-for-filesystem-operations"></a>Autenticação de serviço a serviço com o segredo do cliente para operações do sistema de arquivos

Use este tooauthenticate com o AD do Azure para operações de sistema de arquivos (criar pasta, arquivo de upload, etc.). Olá trecho de código a seguir pode ser usado tooauthenticate seu aplicativo não interativamente, usando o segredo de saudação do cliente para uma entidade de segurança do aplicativo / serviço. Use-o com o aplicativo "Aplicativo Web" Azure AD existente.

    token = lib.auth(tenant_id = 'FILL-IN-HERE', client_secret = 'FILL-IN-HERE', client_id = 'FILL-IN-HERE')

### <a name="multi-factor-authentication-for-account-management"></a>Autenticação multifator para o gerenciamento de contas

Use este tooauthenticate com o AD do Azure para operações de gerenciamento de conta (Criar/excluir conta de repositório Data Lake, etc.). Olá trecho a seguir pode ser usado tooauthenticate seu aplicativo usando a autenticação multifator. Use-o com o aplicativo "Aplicativo Web" Azure AD existente.

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

### <a name="multi-factor-authentication-for-filesystem-management"></a>Autenticação multifator para gerenciamento do sistema de arquivos

Use este tooauthenticate com o AD do Azure para operações de sistema de arquivos (criar pasta, arquivo de upload, etc.). Olá trecho a seguir pode ser usado tooauthenticate seu aplicativo usando a autenticação multifator. Use-o com o aplicativo "Aplicativo Web" Azure AD existente.

    token = lib.auth(tenant_id='FILL-IN-HERE')

## <a name="create-an-azure-resource-group"></a>Criar um grupo de recursos do Azure

Use Olá seguindo o trecho de código toocreate um grupo de recursos do Azure:

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

## <a name="create-clients-and-data-lake-store-account"></a>Crie uma conta do Azure Data Lake Store

Olá trecho de código a seguir primeiro cria um cliente de conta do repositório Data Lake hello. Ele usa Olá cliente objeto toocreate uma conta do repositório Data Lake. Por fim, o trecho de saudação cria um objeto de cliente do sistema de arquivos.

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

## <a name="list-hello-data-lake-store-accounts"></a>Lista de contas do repositório Data Lake Olá

    ## List hello existing Data Lake Store accounts
    result_list_response = adlsAcctClient.account.list()
    result_list = list(result_list_response)
    for items in result_list:
        print(items)

## <a name="create-a-directory"></a>Criar um diretório

    ## Create a directory
    adlsFileSystemClient.mkdir('/mysampledirectory')

## <a name="upload-a-file"></a>Carregar um arquivo


    ## Upload a file
    multithread.ADLUploader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)


## <a name="download-a-file"></a>Baixar um arquivo

    ## Download a file
    multithread.ADLDownloader(adlsFileSystemClient, lpath='C:\\data\\mysamplefile.txt.out', rpath='/mysampledirectory/mysamplefile.txt', nthreads=64, overwrite=True, buffersize=4194304, blocksize=4194304)

## <a name="delete-a-directory"></a>Excluir um diretório

    ## Delete a directory
    adlsFileSystemClient.rm('/mysampledirectory', recursive=True)

## <a name="see-also"></a>Consulte também

- [Proteger dados no Repositório Data Lake](data-lake-store-secure-data.md)
- [Usar a Análise Data Lake do Azure com o Repositório Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
- [Usar o Azure HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md)
- [Referência do SDK do .NET do Azure Data Lake Store](https://msdn.microsoft.com/library/mt581387.aspx)
- [Referência do REST do Azure Data Lake Store](https://msdn.microsoft.com/library/mt693424.aspx)
