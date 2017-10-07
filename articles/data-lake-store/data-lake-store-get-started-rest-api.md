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
# <a name="get-started-with-azure-data-lake-store-using-rest-apis"></a>Introdução ao Repositório Azure Data Lake usando APIs REST
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

Neste artigo, você aprenderá como toouse WebHDFS APIs de REST e APIs de REST de repositório Data Lake tooperform conta de gerenciamento, bem como operações de sistema de arquivos no repositório Azure Data Lake. O Repositório Azure Data Lake expõe suas próprias APIs REST para operações de gerenciamento de conta. No entanto, como o Repositório Data Lake é compatível com o ecossistema HDFS e Hadoop, ele oferece suporte usando as APIs REST WebHDFS para operações do sistema de arquivos.

> [!NOTE]
> Para obter informações detalhadas sobre o suporte de API REST de saudação do repositório Data Lake, consulte [referência de API de REST do Azure Data Lake repositório](https://msdn.microsoft.com/library/mt693424.aspx).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Criar um aplicativo do Azure Active Directory**. Você pode usar Olá AD do Azure tooauthenticate Olá repositório Data Lake aplicativo com o Azure AD. Há diferentes abordagens tooauthenticate com o AD do Azure, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**. Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). Este artigo usa ondulação toodemonstrate como toomake API REST chama em uma conta do repositório Data Lake.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Como faço para me autenticar usando o Azure Active Directory?
Você pode usar dois tooauthenticate abordagens usando o Active Directory do Azure.

### <a name="end-user-authentication-interactive"></a>Autenticação do usuário (interativa)
Nesse cenário, aplicativo hello solicita Olá usuário toolog em e todas as operações de saudação são executadas no contexto de saudação do usuário de saudação. Execute Olá seguindo as etapas para a autenticação interativa.

1. Por meio de seu aplicativo, redirecione Olá usuário toohello URL a seguir:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<URI de REDIRECIONAMENTO > precisa toobe codificado para uso em uma URL. Portanto, para https://localhost, use `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    Para finalidade de saudação deste tutorial, você pode substituir os valores de espaço reservado Olá Olá URL acima e cole-o na barra de endereços do navegador. Você será redirecionado tooauthenticate usando o logon do Azure. Depois que você fizer logon, a resposta de saudação é exibida na barra de endereços do navegador hello. resposta de saudação será em Olá formato a seguir:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Capture o código de autorização de saudação da resposta de saudação. Para este tutorial, você pode copiar o código de autorização Olá Olá na barra de endereços do navegador da web de saudação e passá-lo no hello POST solicitação toohello token ponto de extremidade, conforme mostrado abaixo:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > Nesse caso, Olá \<URI de REDIRECIONAMENTO > não precisa ser codificado.
   > 
   > 
3. resposta de saudação é um objeto JSON que contém um token de acesso (por exemplo, `"access_token": "<ACCESS_TOKEN>"`) e um token de atualização (por exemplo, `"refresh_token": "<REFRESH_TOKEN>"`). Seu aplicativo usa o token de acesso Olá ao acessar o repositório Azure Data Lake e tooget de token de atualização de saudação outro token de acesso quando um token de acesso expira.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Quando o token de acesso de saudação expirar, você pode solicitar um novo token de acesso usando o token de atualização hello, conforme mostrado abaixo:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Para obter mais informações sobre a autenticação interativa de usuário, confira [Fluxo de concessão de código de autorização](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Autenticação serviço a serviço (não interativa)
Nesse cenário, o aplicativo de saudação do hello fornece suas próprias credenciais tooperform operações de saudação. Para isso, você deverá emitir uma solicitação POST como Olá mostrada abaixo. 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

saída de Hello desta solicitação incluirá um token de autorização (indicado por `access-token` na saída de hello abaixo) que você passará subsequentemente com suas chamadas de API REST. Salve esse token de autenticação em um arquivo de texto. Você precisará dele posteriormente neste artigo.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

Este artigo usa Olá **não interativo** abordagem. Para obter mais informações sobre não interativo (chamadas de serviços), consulte [tooservice chamadas usando as credenciais do serviço](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-store-account"></a>Criar uma conta do Repositório Data Lake
Esta operação baseia-se a chamada hello API REST definida [aqui](https://msdn.microsoft.com/library/mt694078.aspx).

Use Olá ondulação de comando a seguir. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

Olá acima de comando, substitua \< `REDACTED` \> com token de autorização Olá recuperados anteriormente. carga de solicitação Olá para este comando está contida no hello **input.json** arquivo que é fornecido para Olá `-d` parâmetro acima. conteúdo de saudação do arquivo de input.json Olá semelhante a seguinte hello:

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a>Criar pastas na conta do Repositório Data Lake
Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).

Use Olá ondulação de comando a seguir. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

Olá acima de comando, substitua \< `REDACTED` \> com token de autorização Olá recuperados anteriormente. Este comando cria um diretório chamado **mytempdir** na pasta raiz de saudação da sua conta do repositório Data Lake.

Se a operação de saudação for concluído com êxito, você deve ver uma resposta como este:

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a>Listar pastas em uma conta do Repositório Data Lake
Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).

Use Olá ondulação de comando a seguir. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

Olá acima de comando, substitua \< `REDACTED` \> com token de autorização Olá recuperados anteriormente.

Se a operação de saudação for concluído com êxito, você deve ver uma resposta como este:

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

## <a name="upload-data-into-a-data-lake-store-account"></a>Carregar dados na conta do Repositório Data Lake
Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).

Use Olá ondulação de comando a seguir. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

Em Olá acima sintaxe **-T** parâmetro é o local de saudação do arquivo hello você está carregando.

saída de Hello é a seguir toohello semelhante:
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a>Ler dados de uma conta do Repositório Data Lake
Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).

A leitura de dados de uma conta do Repositório Data Lake é um processo de duas etapas.

* Enviar uma solicitação GET no ponto de extremidade Olá primeiro `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`. Isso retornará uma local toosubmit Olá próxima solicitação GET para.
* Em seguida, enviar solicitação GET hello no ponto de extremidade Olá `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`. Isso exibirá o conteúdo de saudação do arquivo hello.

No entanto, porque não há nenhuma diferença em hello parâmetros de entrada entre hello primeiro e hello segunda etapa, você pode usar o hello `-L` primeira solicitação de parâmetro toosubmit hello. `-L`opção essencialmente combina duas solicitações em um e tornará ondulação Refazer Olá solicitação no novo local de saudação. Por fim, Olá saída de todas as chamadas de solicitação de saudação é exibida, como mostrado abaixo. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

Você verá uma saída semelhante toohello a seguir:

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a>Renomear um arquivo em uma conta do Repositório Data Lake
Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).

A seguir use Olá cURL comando toorename um arquivo. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

Você verá uma saída semelhante toohello a seguir:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a>Excluir um arquivo de uma conta do Repositório Data Lake
Esta operação baseia-se a chamada hello WebHDFS REST API definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).

A seguir use Olá cURL comando toodelete um arquivo. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

Você verá uma saída semelhante Olá seguinte:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a>Excluir uma conta do Repositório do Data Lake
Esta operação baseia-se a chamada hello API REST definida [aqui](https://msdn.microsoft.com/library/mt694075.aspx).

A seguir use Olá cURL comando toodelete uma conta do repositório Data Lake. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

Você verá uma saída semelhante Olá seguinte:

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a>Consulte também
* [Aplicativos de Big Data de software livre compatíveis com o Repositório Azure Data Lake](data-lake-store-compatible-oss-other-applications.md)

