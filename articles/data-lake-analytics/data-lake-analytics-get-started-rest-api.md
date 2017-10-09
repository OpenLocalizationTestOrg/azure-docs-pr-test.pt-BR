---
title: "aaaGet iniciado com análise Data Lake usando a API REST | Microsoft Docs"
description: "Use APIs de REST WebHDFS tooperform operações em análise Data Lake"
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
ms.openlocfilehash: a0b13d521821fd2d74716cc52485585feb7c51b2
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="get-started-with-azure-data-lake-analytics-using-rest-apis"></a>Introdução ao Azure Data Lake Analytics usando APIs REST
[!INCLUDE [get-started-selector](../../includes/data-lake-analytics-selector-get-started.md)]

Saiba como toouse WebHDFS APIs de REST e APIs de REST de análise Data Lake toomanage análise Data Lake contas, trabalhos e catálogo. 

## <a name="prerequisites"></a>Pré-requisitos
* **Uma assinatura do Azure**. Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).
* **Criar um aplicativo do Azure Active Directory**. Você pode usar Olá AD do Azure tooauthenticate Olá análise Data Lake aplicativo com o Azure AD. Há diferentes abordagens tooauthenticate com o AD do Azure, que são **autenticação do usuário final** ou **autenticação de serviço a serviço**. Para obter instruções e mais informações sobre como tooauthenticate, consulte [autenticar com análise Data Lake usando o Azure Active Directory](../data-lake-store/data-lake-store-authenticate-using-active-directory.md).
* [cURL](http://curl.haxx.se/). Este artigo usa ondulação toodemonstrate como toomake API REST chama em relação a uma conta da análise Data Lake.

## <a name="authenticate-with-azure-active-directory"></a>Autenticar com o Azure Active Directory
Há dois métodos para autenticar com o Azure Active Directory.

### <a name="end-user-authentication-interactive"></a>Autenticação do usuário (interativa)
Usando esse método, aplicativo solicita Olá usuário toolog em e todas as operações de saudação são executadas no contexto de saudação do usuário de saudação. 

Siga estas etapas para a autenticação interativa:

1. Por meio de seu aplicativo, redirecione Olá usuário toohello URL a seguir:
   
        https://login.microsoftonline.com/<TENANT-ID>/oauth2/authorize?client_id=<CLIENT-ID>&response_type=code&redirect_uri=<REDIRECT-URI>
   
   > [!NOTE]
   > \<URI de REDIRECIONAMENTO > precisa toobe codificado para uso em uma URL. Portanto, para https://localhost, use `https%3A%2F%2Flocalhost`)
   > 
   > 
   
    Para finalidade de saudação deste tutorial, você pode substituir os valores de espaço reservado Olá Olá URL acima e cole-o na barra de endereços do navegador. Você será redirecionado tooauthenticate usando o logon do Azure. Depois que você com êxito login, resposta Olá é exibida na barra de endereços do navegador hello. resposta de saudação será em Olá formato a seguir:
   
        http://localhost/?code=<AUTHORIZATION-CODE>&session_state=<GUID>
2. Capture o código de autorização de saudação da resposta de saudação. Para este tutorial, você pode copiar o código de autorização Olá Olá na barra de endereços do navegador da web de saudação e passá-lo no hello POST solicitação toohello token ponto de extremidade, conforme mostrado abaixo:
   
        curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token \
        -F redirect_uri=<REDIRECT-URI> \
        -F grant_type=authorization_code \
        -F resource=https://management.core.windows.net/ \
        -F client_id=<CLIENT-ID> \
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
             -F client_id=<CLIENT-ID> \
             -F refresh_token=<REFRESH-TOKEN>

Para obter mais informações sobre a autenticação interativa de usuário, confira [Fluxo de concessão de código de autorização](https://msdn.microsoft.com/library/azure/dn645542.aspx).

### <a name="service-to-service-authentication-non-interactive"></a>Autenticação serviço a serviço (não interativa)
Usando esse método, aplicativo fornece suas próprias credenciais tooperform Olá operações. Para isso, você deverá emitir uma solicitação POST como Olá mostrado abaixo: 

    curl -X POST https://login.microsoftonline.com/<TENANT-ID>/oauth2/token  \
      -F grant_type=client_credentials \
      -F resource=https://management.core.windows.net/ \
      -F client_id=<CLIENT-ID> \
      -F client_secret=<AUTH-KEY>

saída de Hello desta solicitação incluirá um token de autorização (indicado por `access-token` na saída de hello abaixo) que você passará subsequentemente com suas chamadas de API REST. Salve esse token de autenticação em um arquivo de texto. Você precisará dele posteriormente neste artigo.

    {"token_type":"Bearer","expires_in":"3599","expires_on":"1458245447","not_before":"1458241547","resource":"https://management.core.windows.net/","access_token":"<REDACTED>"}

Este artigo usa Olá **não interativo** abordagem. Para obter mais informações sobre não interativo (chamadas de serviços), consulte [tooservice chamadas usando as credenciais do serviço](https://msdn.microsoft.com/library/azure/dn645543.aspx).

## <a name="create-a-data-lake-analytics-account"></a>Criar uma conta da Análise Data Lake
Você deve criar um grupo de Recursos do Azure e uma conta do Data Lake Store para poder criar uma conta do Data Lake Analytics.  Veja [Criar uma conta do Data Lake Store](../data-lake-store/data-lake-store-get-started-rest-api.md#create-a-data-lake-store-account).

Olá após a rotação de comando mostra como toocreate uma conta:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" -H "Content-Type: application/json" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<NewAzureDataLakeAnalyticsAccountName>?api-version=2016-11-01 -d@"C:\tutorials\adla\CreateDataLakeAnalyticsAccountRequest.json"

Substituir \< `REDACTED` \> com token de autorização Olá \< `AzureSubscriptionID` \> com sua ID de assinatura \< `AzureResourceGroupName` \> com um recurso existente do Azure Nome do grupo, e \< `NewAzureDataLakeAnalyticsAccountName` \> com um novo nome de conta de análise Data Lake. carga de solicitação Olá para este comando está contida no hello **CreateDatalakeAnalyticsAccountRequest.json** arquivo que é fornecido para Olá `-d` parâmetro acima. conteúdo de saudação do arquivo de input.json Olá semelhante a seguinte hello:

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


## <a name="list-data-lake-analytics-accounts-in-a-subscription"></a>Listar contas do Data Lake Analytics em uma assinatura
Olá ondulação de comando a seguir mostra como toolist contas em uma assinatura:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/providers/Microsoft.DataLakeAnalytics/Accounts?api-version=2016-11-01

Substituir \< `REDACTED` \> com token de autorização Olá \< `AzureSubscriptionID` \> com sua ID de assinatura. saída de Hello é semelhante a:

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

## <a name="get-information-about-a-data-lake-analytics-account"></a>Obter informações sobre uma conta do Data Lake Analytics
Olá após a rotação de comando mostra como tooget um informações da conta:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>?api-version=2015-11-01

Substituir \< `REDACTED` \> com token de autorização Olá \< `AzureSubscriptionID` \> com sua ID de assinatura \< `AzureResourceGroupName` \> com um recurso existente do Azure Nome do grupo, e \< `DataLakeAnalyticsAccountName` \> com o nome de saudação de uma conta existente do Data Lake análise. saída de Hello é semelhante a:

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

## <a name="list-data-lake-stores-of-a-data-lake-analytics-account"></a>Listar Data Lake Stores de uma conta do Data Lake Analytics
Olá ondulação de comando a seguir mostra como toolist Data Lake armazena de uma conta:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://management.azure.com/subscriptions/<AzureSubscriptionID>/resourceGroups/<AzureResourceGroupName>/providers/Microsoft.DataLakeAnalytics/accounts/<DataLakeAnalyticsAccountName>/DataLakeStoreAccounts/?api-version=2016-11-01

Substituir \< `REDACTED` \> com token de autorização Olá \< `AzureSubscriptionID` \> com sua ID de assinatura \< `AzureResourceGroupName` \> com um recurso existente do Azure Nome do grupo, e \< `DataLakeAnalyticsAccountName` \> com o nome de saudação de uma conta existente do Data Lake análise. saída de Hello é semelhante a:

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

## <a name="submit-u-sql-jobs"></a>Enviar trabalhos de U-SQL
Olá após a rotação de comando mostra como trabalho toosubmit um U-SQL:

    curl -i -X PUT -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs/<NewGUID>?api-version=2016-03-20-preview -d@"C:\tutorials\adla\SubmitADLAJob.json"

Substituir \< `REDACTED` \> com token de autorização Olá \< `DataLakeAnalyticsAccountName` \> com o nome de saudação de uma conta existente do Data Lake análise. carga de solicitação Olá para este comando está contida no hello **SubmitADLAJob.json** arquivo que é fornecido para Olá `-d` parâmetro acima. conteúdo de saudação do arquivo de input.json Olá semelhante a seguinte hello:

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
        ING Extractors.Tsv();\n\nOUTPUT @searchlog   \n    too\"/Output/SearchLog-from-Data-Lake.csv\"\nUSING Outputters.Csv();"
        }
    }

saída de Hello é semelhante a:

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


## <a name="list-u-sql-jobs"></a>Listar trabalhos de U-SQL
Olá após a rotação de comando mostra como trabalhos toolist U-SQL:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/Jobs?api-version=2016-11-01 

Substituir \< `REDACTED` \> com token de autorização hello e \< `DataLakeAnalyticsAccountName` \> com o nome de saudação de uma conta existente do Data Lake análise. 

saída de Hello é semelhante a:

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


## <a name="get-catalog-items"></a>Obter itens do catálogo
Olá ondulação de comando a seguir mostra como tooget bancos de dados de saudação do hello catálogo:

    curl -i -X GET -H "Authorization: Bearer <REDACTED>" https://<DataLakeAnalyticsAccountName>.azuredatalakeanalytics.net/catalog/usql/databases?api-version=2016-11-01

saída de Hello é semelhante a:

    {
    "@odata.context":"https://myadla0831.azuredatalakeanalytics.net/sqlip/$metadata#databases","value":[
        {
        "computeAccountName":"myadla0831","databaseName":"mytest","version":"f6956327-90b8-4648-ad8b-de3ff09274ea"
        },{
        "computeAccountName":"myadla0831","databaseName":"master","version":"e8bca908-cc73-41a3-9564-e9bcfaa21f4e"
        }
    ]
    }

## <a name="see-also"></a>Consulte também
* toosee uma consulta mais complexa, consulte [site analisar logs usando a análise do Azure Data Lake](data-lake-analytics-analyze-weblogs.md).
* tooget iniciar o desenvolvimento de aplicativos de U-SQL, consulte [scripts de desenvolver U-SQL usando o Data Lake Tools para Visual Studio](data-lake-analytics-data-lake-tools-get-started.md).
* toolearn U-SQL, consulte [começar com a linguagem da análise Azure Data Lake U-SQL](data-lake-analytics-u-sql-get-started.md).
* Para obter as tarefas de gerenciamento, confira [Gerenciar o Azure Data Lake Analytics usando o portal do Azure](data-lake-analytics-manage-use-portal.md).
* tooget uma visão geral da análise Data Lake, consulte [visão geral da análise Azure Data Lake](data-lake-analytics-overview.md).
* toosee Olá mesmo tutorial usando outras ferramentas, clique em seletores de guia Olá na parte superior de saudação da página de saudação.

