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

Neste artigo, você aprenderá a usar as APIs REST WebHDFS e as APIs REST do Repositório Data Lake para executar o gerenciamento de contas e as operações de sistema de arquivos no Repositório Azure Data Lake. O Repositório Azure Data Lake expõe suas próprias APIs REST para operações de gerenciamento de conta. No entanto, como o Repositório Data Lake é compatível com o ecossistema HDFS e Hadoop, ele oferece suporte usando as APIs REST WebHDFS para operações do sistema de arquivos.

> [!NOTE]
> Para obter informações detalhadas sobre o suporte à API REST para o Repositório Data Lake, consulte [Referência da API REST do Repositório Azure Data Lake](https://msdn.microsoft.com/library/mt693424.aspx).
> 
> 

## <a name="prerequisites"></a>Pré-requisitos
* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Criar um aplicativo do Azure Active Directory**. Você pode usar o aplicativo Azure AD para autenticar o aplicativo Data Lake Store com o Azure AD. Há diferentes abordagens para autenticar com o Azure AD, que são a **autenticação de usuário final** ou a **autenticação serviço a serviço**. Para obter instruções e saber mais sobre como se autenticar, veja [Autenticação do usuário final](data-lake-store-end-user-authenticate-using-active-directory.md) ou [Autenticação de serviço a serviço](data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). Este artigo usa cURL para demonstrar como fazer chamadas à API REST em uma conta do Repositório Data Lake.

## <a name="how-do-i-authenticate-using-azure-active-directory"></a>Como faço para me autenticar usando o Azure Active Directory?
Você pode usar duas abordagens para se autenticar usando o Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Autenticação do usuário (interativa)
Nesse cenário, o aplicativo solicita o logon do usuário e todas as operações são executadas no contexto do usuário. Realize as seguintes etapas para a autenticação interativa.

1. Por meio de seu aplicativo, redirecione o usuário para a seguinte URL:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<APPLICATION-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<<REDIRECT-URI> precisa ser codificado para uso em uma URL. Portanto, para https://localhost, use `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    Para os fins deste tutorial, é possível substituir os valores de espaço reservado na URL acima e colá-los na barra de endereços do navegador da Web. Você será redirecionado para autenticar usando seu logon do Azure. Depois de fazer logon com êxito, a resposta será exibida na barra de endereços do navegador. A resposta estará no seguinte formato:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Capture o código de autorização da resposta. Para este tutorial, é possível copiar o código de autorização da barra de endereços do navegador da Web e passá-lo na solicitação POST para o ponto de extremidade do token, conforme mostrado abaixo:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<APPLICATION-ID> \
        -F code=<AUTHORIZATION-CODE>
   
   > [!NOTE]
   > Nesse caso, o \<REDIRECT-URI> não precisa ser codificado.
   > 
   > 
3. A resposta é um objeto JSON que contém um token de acesso (por exemplo, `"access_token": "<ACCESS_TOKEN>"`) e um token de atualização (por exemplo, `"refresh_token": "<REFRESH_TOKEN>"`). Seu aplicativo usa o token de acesso ao acessar o Repositório Azure Data Lake e o token de atualização para obter outro token de acesso quando um token de acesso expira.
   
        {"token_type":"Bearer","scope":"user_impersonation","expires_in":"3599","expires_on":"1461865782","not_before":    "1461861882","resource":"https://management.core.windows.net/","access_token":"<REDACTED>","refresh_token":"<REDACTED>","id_token":"<REDACTED>"}
4. Quando o token de acesso expira, é possível solicitar um novo token de acesso usando o token de atualização, conforme mostrado abaixo:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
             -F grant_type=refresh_token \
             -F resource=https://management.core.windows.net/ \
             -F client_id=<APPLICATION-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Para obter mais informações sobre a autenticação interativa de usuário, confira [Fluxo de concessão de código de autorização](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Autenticação serviço a serviço (não interativa)
Nesse cenário, o aplicativo fornece suas próprias credenciais para executar as operações. Para isso, você deve emitir uma solicitação POST como a mostrada abaixo. 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

A saída dessa solicitação incluirá um token de autorização (indicado por `access-token` na saída abaixo) que você transmitirá posteriormente com as chamadas à API REST. Salve esse token de autenticação em um arquivo de texto. Você precisará dele posteriormente neste artigo.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

Este artigo usa uma abordagem **não interativa** . Para saber mais sobre (chamadas de serviço a serviço) não interativas, confira [Chamadas de serviço a serviço usando credenciais](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-store-account"></a>Criar uma conta do Repositório Data Lake
Essa operação se baseia na chamada à API REST definida [aqui](https://msdn.microsoft.com/library/mt694078.aspx).

Use o comando cURL a seguir. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview -d@"C:\temp\input.json"

No comando acima, substitua \<`REDACTED`\> pelo token de autorização recuperado anteriormente. A carga de solicitação para esse comando está contida no arquivo **input.json** fornecido para o parâmetro `-d` acima. O conteúdo do arquivo input.json lembra o seguinte:

    {
    "location": "eastus2",
    "tags": {
        "department": "finance"
        },
    "properties": {}
    }    

## <a name="create-folders-in-a-data-lake-store-account"></a>Criar pastas na conta do Repositório Data Lake
Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Make_a_Directory).

Use o comando cURL a seguir. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/?op=MKDIRS'

No comando acima, substitua \<`REDACTED`\> pelo token de autorização recuperado anteriormente. Esse comando cria um diretório chamado **mytempdir** na pasta raiz da conta do Data Lake Store.

Você deverá ver uma resposta como esta caso a operação seja concluída com êxito:

    {"boolean":true}

## <a name="list-folders-in-a-data-lake-store-account"></a>Listar pastas em uma conta do Repositório Data Lake
Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#List_a_Directory).

Use o comando cURL a seguir. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/?op=LISTSTATUS'

No comando acima, substitua \<`REDACTED`\> pelo token de autorização recuperado anteriormente.

Você deverá ver uma resposta como esta caso a operação seja concluída com êxito:

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
Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Create_and_Write_to_a_File).

Use o comando cURL a seguir. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X PUT -L -T 'C:\temp\list.txt' -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE'

Na sintaxe acima o parâmetro **-T** é o local do arquivo que você está carregando.

A saída deverá ser semelhante a esta:
   
    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/list.txt?op=CREATE&write=true
    ...
    Content-Length: 0

    HTTP/1.1 100 Continue

    HTTP/1.1 201 Created
    ...

## <a name="read-data-from-a-data-lake-store-account"></a>Ler dados de uma conta do Repositório Data Lake
Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Open_and_Read_a_File).

A leitura de dados de uma conta do Repositório Data Lake é um processo de duas etapas.

* Primeiro você envia uma solicitação GET para o ponto de extremidade `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN`. Isso retornará um local para o qual será enviada a próxima solicitação GET.
* Em seguida, você enviará a solicitação GET para o ponto de extremidade `https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN&read=true`. Isso exibirá o conteúdo do arquivo.

No entanto, como não há diferença nos parâmetros de entrada entre a primeira e a segunda etapa, é possível usar o parâmetro `-L` para enviar a primeira solicitação. `-L` combina duas solicitações em uma e fará com que a cURL refaça a solicitação no novo local. Por fim, a saída de todas as chamadas de solicitação é exibida, conforme mostrado abaixo. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -L GET -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=OPEN'

Você deverá ver um resultado semelhante ao seguinte:

    HTTP/1.1 307 Temporary Redirect
    ...
    Location: https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/somerandomfile.txt?op=OPEN&read=true
    ...

    HTTP/1.1 200 OK
    ...

    Hello, Data Lake Store user!

## <a name="rename-a-file-in-a-data-lake-store-account"></a>Renomear um arquivo em uma conta do Repositório Data Lake
Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Rename_a_FileDirectory).

Use o comando cURL a seguir para renomear um arquivo. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -d "" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile.txt?op=RENAME&destination=/mytempdir/myinputfile1.txt'

Você deverá ver um resultado semelhante ao seguinte:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-file-from-a-data-lake-store-account"></a>Excluir um arquivo de uma conta do Repositório Data Lake
Essa operação se baseia na chamada à API REST WebHDFS definida [aqui](http://hadoop.apache.org/docs/stable/hadoop-project-dist/hadoop-hdfs/WebHDFS.html#Delete_a_FileDirectory).

Use o comando cURL a seguir para excluir um arquivo. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" 'https://<yourstorename>.azuredatalakestore.net/webhdfs/v1/mytempdir/myinputfile1.txt?op=DELETE'

Você verá algo semelhante ao mostrado a seguir:

    HTTP/1.1 200 OK
    ...

    {"boolean":true}

## <a name="delete-a-data-lake-store-account"></a>Excluir uma conta do Repositório do Data Lake
Essa operação se baseia na chamada à API REST definida [aqui](https://msdn.microsoft.com/library/mt694075.aspx).

Use o comando cURL a seguir para excluir uma conta do Repositório Data Lake. Substitua **\<nomedorepositório** pelo nome do Data Lake Store.

    curl -i -X DELETE -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/{subscription-id}/resourceGroups/{resource-group-name}/providers/Microsoft.DataLakeStore/accounts/<yourstorename>?api-version=2015-10-01-preview

Você verá algo semelhante ao mostrado a seguir:

    HTTP/1.1 200 OK
    ...
    ...

## <a name="see-also"></a>Confira também
* [Aplicativos de Big Data de software livre compatíveis com o Repositório Azure Data Lake](data-lake-store-compatible-oss-other-applications.md)

