---
title: aaaTransform dados usando o script U-SQL - Azure | Microsoft Docs
description: "Saiba como o serviço de computação tooprocess ou transformar dados executando os scripts de U-SQL na análise do Azure Data Lake."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: e17c1255-62c2-4e2e-bb60-d25274903e80
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/10/2017
ms.author: spelluru
ms.openlocfilehash: 51fdb40334d0c131720f65c3a96b4c5045a98b24
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="transform-data-by-running-u-sql-scripts-on-azure-data-lake-analytics"></a>Transforme dados executando scripts U-SQL no serviço de computação do Azure Data Lake Analytics 
> [!div class="op_single_selector" title1="Transformation Activities"]
> * [Atividade de Hive](data-factory-hive-activity.md) 
> * [Atividade Pig](data-factory-pig-activity.md)
> * [Atividade MapReduce](data-factory-map-reduce.md)
> * [Atividade de Transmissão do Hadoop](data-factory-hadoop-streaming-activity.md)
> * [Atividade do Spark](data-factory-spark.md)
> * [Atividade de Execução em Lote do Machine Learning](data-factory-azure-ml-batch-execution-activity.md)
> * [Atividade do Recurso de Atualização do Machine Learning](data-factory-azure-ml-update-resource-activity.md)
> * [Atividade de Procedimento Armazenado](data-factory-stored-proc-activity.md)
> * [Atividade do U-SQL do Data Lake Analytics](data-factory-usql-activity.md)
> * [Atividade Personalizada do .NET](data-factory-use-custom-activities.md)

Um pipeline em uma fábrica de dados do Azure processa dados nos serviços de armazenamento vinculados utilizando serviços de computação vinculados. Ela contém uma sequência de atividades em que cada atividade executa uma operação de processamento específica. Este artigo descreve Olá **atividade U-SQL do Data Lake análise** que executa um **U-SQL** script em um **análise Azure Data Lake** serviço vinculado de computação. 

> [!NOTE]
> Crie uma conta do Azure Data Lake Analytics antes de criar um pipeline com uma atividade do U-SQL do Data Lake Analytics. toolearn sobre análise Azure Data Lake, consulte [Introdução à análise Azure Data Lake](../data-lake-analytics/data-lake-analytics-get-started-portal.md).
> 
> Saudação de revisão [criar seu primeiro tutorial pipeline](data-factory-build-your-first-pipeline.md) para obter etapas detalhadas toocreate uma fábrica de dados, vinculada a um pipeline, conjuntos de dados e serviços. Use trechos de código JSON com o Editor de fábrica de dados ou entidades de fábrica de dados toocreate Visual Studio ou o Azure PowerShell.

## <a name="supported-authentication-types"></a>Tipos de autenticação com suporte
A atividade do U-SQL dá suporte aos tipos de autenticação abaixo no Data Lake Analytics:
* Autenticação de entidade de serviço
* Autenticação de credencial do usuário (OAuth) 

Recomendamos o uso da autenticação de entidade de serviço, especialmente para uma execução de U-SQL agendada. O comportamento de expiração do token pode ocorrer com autenticação de credenciais do usuário. Para obter detalhes de configuração, consulte Olá [vinculado propriedades do serviço](#azure-data-lake-analytics-linked-service) seção.

## <a name="azure-data-lake-analytics-linked-service"></a>Serviço Vinculado da Análise Azure Data Lake
Você cria um **análise Azure Data Lake** vinculado serviço toolink uma análise do Azure Data Lake computação serviço tooan data factory do Azure. Hello atividade U-SQL do Data Lake análise no pipeline de saudação refere-se serviço toothis vinculado. 

Olá tabela a seguir fornece descrições para Olá genéricas propriedades usadas em Olá definição JSON. Você ainda pode escolher entre a autenticação de credencial do usuário e entidade de serviço.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| **tipo** |propriedade de tipo Hello deve ser definida como: **AzureDataLakeAnalytics**. |Sim |
| **accountName** |Nome da conta da Análise Azure Data Lake. |Sim |
| **dataLakeAnalyticsUri** |URI da Análise Azure Data Lake. |Não |
| **subscriptionId** |Id de assinatura do Azure |Não (se não especificado, a assinatura de saudação fábrica de dados é usada). |
| **resourceGroupName** |Nome do grupo de recursos do Azure |Não (se não especificado, o grupo de recursos de saudação fábrica de dados é usada). |

### <a name="service-principal-authentication-recommended"></a>Autenticação de entidade de serviço (recomendada)
autenticação principal do serviço toouse, registre uma entidade de aplicativo no Azure Active Directory (AD do Azure) e conceda ele Olá acessar tooData Lake repositório. Para encontrar as etapas detalhadas, consulte [Autenticação de serviço a serviço](../data-lake-store/data-lake-store-authenticate-using-active-directory.md). Anote Olá valores, que você usar a seguir toodefine Olá vinculado de serviço:
* ID do aplicativo
* Chave do aplicativo 
* ID do locatário

Use autenticação principal do serviço especificando Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| **servicePrincipalId** | Especifique a ID do cliente. do aplicativo hello | Sim |
| **servicePrincipalKey** | Especifique a chave de aplicativo hello. | Sim |
| **tenant** | Especifique as informações de locatário hello (ID de locatário ou de nome de domínio) em que o aplicativo reside. Você pode recuperá-la por focalização mouse Olá no canto superior direito Olá Olá portal do Azure. | Sim |

**Exemplo: autenticação de entidade de serviço**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

### <a name="user-credential-authentication"></a>Autenticação de credenciais de usuário
Como alternativa, você pode usar a autenticação de credenciais de usuário para análise Data Lake especificando Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| **authorization** | Clique em Olá **autorizar** botão no hello Editor da fábrica de dados e insira suas credenciais que atribui a propriedade toothis de URL de autorização do hello gerado automaticamente. | Sim |
| **sessionId** | ID de sessão do OAuth da sessão de autorização de OAuth hello. Cada ID da sessão é exclusiva e pode ser usada somente uma vez. Essa configuração é gerada automaticamente quando você usa Olá Editor da fábrica de dados. | Sim |

**Exemplo: autenticação de credenciais do usuário**
```json
{
    "name": "AzureDataLakeAnalyticsLinkedService",
    "properties": {
        "type": "AzureDataLakeAnalytics",
        "typeProperties": {
            "accountName": "adftestaccount",
            "dataLakeAnalyticsUri": "azuredatalakeanalytics.net",
            "authorization": "<authcode>",
            "sessionId": "<session ID>", 
            "subscriptionId": "<optional, subscription id of ADLA>",
            "resourceGroupName": "<optional, resource group name of ADLA>"
        }
    }
}
```

#### <a name="token-expiration"></a>Expiração do token
Olá código de autorização gerado usando Olá **autorizar** botão expira após algum tempo. Consulte a tabela a seguir para tempos de expiração de saudação para diferentes tipos de contas de usuário de saudação. Você pode ver Olá a seguinte mensagem de erro hello quando a autenticação **token expira**: erro na operação de credencial: invalid_grant - AADSTS70002: erro ao validar credenciais. AADSTS70008: Olá fornecido a concessão de acesso expirou ou foi revogado. ID do Rastreamento: d18629e8-af88-43c5-88e3-d8419eb1fca1 ID da Correlação: fac30a0c-6be6-4e02-8d69-a776d2ffefd7 Carimbo de data/hora: 2015-12-15 21:09:31Z

| Tipo de usuário | Expira após |
|:--- |:--- |
| Contas de usuário NÃO gerenciadas pelo Azure Active Directory (@hotmail.com, @live.com etc.) |12 horas |
| Contas de usuários gerenciadas pelo AAD (Azure Active Directory) |Execute a 14 dias após a última fatia de saudação. <br/><br/>90 dias, se uma fatia com base em serviços vinculados do OAuth for executada pelo menos uma vez a cada 14 dias. |

tooavoid e resolver esse erro, autorize novamente usando Olá **autorizar** botão quando hello **token expira** e reimplante o serviço vinculado de saudação. Você também pode gerar valores para as propriedades **sessionId** e **authorization** de modo programático usando o código da seguinte maneira:

```csharp
if (linkedService.Properties.TypeProperties is AzureDataLakeStoreLinkedService ||
    linkedService.Properties.TypeProperties is AzureDataLakeAnalyticsLinkedService)
{
    AuthorizationSessionGetResponse authorizationSession = this.Client.OAuth.Get(this.ResourceGroupName, this.DataFactoryName, linkedService.Properties.Type);

    WindowsFormsWebAuthenticationDialog authenticationDialog = new WindowsFormsWebAuthenticationDialog(null);
    string authorization = authenticationDialog.AuthenticateAAD(authorizationSession.AuthorizationSession.Endpoint, new Uri("urn:ietf:wg:oauth:2.0:oob"));

    AzureDataLakeStoreLinkedService azureDataLakeStoreProperties = linkedService.Properties.TypeProperties as AzureDataLakeStoreLinkedService;
    if (azureDataLakeStoreProperties != null)
    {
        azureDataLakeStoreProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeStoreProperties.Authorization = authorization;
    }

    AzureDataLakeAnalyticsLinkedService azureDataLakeAnalyticsProperties = linkedService.Properties.TypeProperties as AzureDataLakeAnalyticsLinkedService;
    if (azureDataLakeAnalyticsProperties != null)
    {
        azureDataLakeAnalyticsProperties.SessionId = authorizationSession.AuthorizationSession.SessionId;
        azureDataLakeAnalyticsProperties.Authorization = authorization;
    }
}
```

Consulte [AzureDataLakeStoreLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakestorelinkedservice.aspx), [AzureDataLakeAnalyticsLinkedService classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.azuredatalakeanalyticslinkedservice.aspx), e [AuthorizationSessionGetResponse classe](https://msdn.microsoft.com/library/microsoft.azure.management.datafactories.models.authorizationsessiongetresponse.aspx) tópicos para obter detalhes sobre classes de fábrica de dados Olá usadas no código de saudação. Adicione uma referência a: Microsoft.IdentityModel.Clients.ActiveDirectory.WindowsForms.dll para Olá WindowsFormsWebAuthenticationDialog classe. 

## <a name="data-lake-analytics-u-sql-activity"></a>Atividade do U-SQL da Análise Data Lake
Olá trecho JSON a seguir define um pipeline com uma atividade de U-SQL análise Data Lake. definição de atividade Olá tem uma referência toohello serviço vinculado de análise do Azure Data Lake criado anteriormente.   

```json
{
    "name": "ComputeEventsByRegionPipeline",
    "properties": {
        "description": "This is a pipeline toocompute events for en-gb locale and date less than 2012/02/19.",
        "activities": 
        [
            {
                "type": "DataLakeAnalyticsU-SQL",
                "typeProperties": {
                    "scriptPath": "scripts\\kona\\SearchLogProcessing.txt",
                    "scriptLinkedService": "StorageLinkedService",
                    "degreeOfParallelism": 3,
                    "priority": 100,
                    "parameters": {
                        "in": "/datalake/input/SearchLog.tsv",
                        "out": "/datalake/output/Result.tsv"
                    }
                },
                "inputs": [
                    {
                        "name": "DataLakeTable"
                    }
                ],
                "outputs": 
                [
                    {
                        "name": "EventsByRegionTable"
                    }
                ],
                "policy": {
                    "timeout": "06:00:00",
                    "concurrency": 1,
                    "executionPriorityOrder": "NewestFirst",
                    "retry": 1
                },
                "scheduler": {
                    "frequency": "Day",
                    "interval": 1
                },
                "name": "EventsByRegion",
                "linkedServiceName": "AzureDataLakeAnalyticsLinkedService"
            }
        ],
        "start": "2015-08-08T00:00:00Z",
        "end": "2015-08-08T01:00:00Z",
        "isPaused": false
    }
}
```

Olá tabela a seguir descreve os nomes e descrições das propriedades de atividade toothis específico. 

| Propriedade | Descrição | Obrigatório |
|:--- |:--- |:--- |
| type |propriedade do tipo Hello deve ser definida muito**DataLakeAnalyticsU SQL**. |Sim |
| scriptPath |Toofolder de caminho que contém o script hello U-SQL. Nome do arquivo hello diferencia maiusculas de minúsculas. |Não (se você usar o script) |
| scriptLinkedService |Serviço vinculado que vincula o armazenamento de saudação que contém a fábrica de dados Olá script toohello |Não (se você usar o script) |
| script |Especificar script embutido em vez de especificar scriptPath e scriptLinkedService. Por exemplo: `"script": "CREATE DATABASE test"`. |Não (se você usar scriptPath e scriptLinkedService) |
| degreeOfParallelism |número máximo de saudação de nós usados simultaneamente toorun trabalho de saudação. |Não |
| prioridade |Determina quais trabalhos entre todos os que estão na fila devem ser selecionada toorun primeiro. Olá Olá número menor, Olá Olá prioridade. |Não |
| parâmetros |Parâmetros de script hello U-SQL |Não |
| runtimeVersion | Versão de tempo de execução do toouse do mecanismo de saudação U-SQL | Não | 
| compilationMode | <p>Modo de compilação do U-SQL. Deve ser um destes valores:</p> <ul><li>**Semantic:** apenas realize verificações de semântica e as verificações de integridade necessárias.</li><li>**Completo:** executar Olá de compilação completo, incluindo verificação de sintaxe, otimização, geração de código, etc.</li><li>**SingleBox:** executar compilação completa hello, com tooSingleBox de configuração de TargetType.</li></ul><p>Se você não especificar um valor para essa propriedade, o servidor de saudação determina o modo de compilação ideal de saudação. </p>| Não | 

Consulte [SearchLogProcessing.txt Script definição](#sample-u-sql-script) para definição de saudação do script. 

## <a name="sample-input-and-output-datasets"></a>Conjuntos de dados de entrada e saída de exemplo
### <a name="input-dataset"></a>Conjunto de dados de entrada
Neste exemplo, os dados de entrada hello residem em um repositório Azure Data Lake (SearchLog.tsv arquivo na pasta de datalake/entrada hello). 

```json
{
    "name": "DataLakeTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/input/",
            "fileName": "SearchLog.tsv",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            }
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}    
```

### <a name="output-dataset"></a>Conjunto de dados de saída
Neste exemplo, os dados de saída de hello produzidos pelo Olá script U-SQL são armazenados em um repositório Azure Data Lake (pasta datalake/saída). 

```json
{
    "name": "EventsByRegionTable",
    "properties": {
        "type": "AzureDataLakeStore",
        "linkedServiceName": "AzureDataLakeStoreLinkedService",
        "typeProperties": {
            "folderPath": "datalake/output/"
        },
        "availability": {
            "frequency": "Day",
            "interval": 1
        }
    }
}
```

### <a name="sample-data-lake-store-linked-service"></a>Exemplo de serviço vinculado do Data Lake Store
Esta é a definição de saudação do exemplo hello que repositório Azure Data Lake vinculado usado por conjuntos de dados de entrada/saída de saudação do serviço. 

```json
{
    "name": "AzureDataLakeStoreLinkedService",
    "properties": {
        "type": "AzureDataLakeStore",
        "typeProperties": {
            "dataLakeUri": "https://<accountname>.azuredatalakestore.net/webhdfs/v1",
            "servicePrincipalId": "<service principal id>",
            "servicePrincipalKey": "<service principal key>",
            "tenant": "<tenant info, e.g. microsoft.onmicrosoft.com>",
        }
    }
}
```

Consulte [mover tooand de dados do repositório Azure Data Lake](data-factory-azure-datalake-connector.md) artigo para obter descrições das propriedades JSON. 

## <a name="sample-u-sql-script"></a>Exemplo de script U-SQL

```
@searchlog =
    EXTRACT UserId          int,
            Start           DateTime,
            Region          string,
            Query           string,
            Duration        int?,
            Urls            string,
            ClickedUrls     string
    FROM @in
    USING Extractors.Tsv(nullEscape:"#NULL#");

@rs1 =
    SELECT Start, Region, Duration
    FROM @searchlog
WHERE Region == "en-gb";

@rs1 =
    SELECT Start, Region, Duration
    FROM @rs1
    WHERE Start <= DateTime.Parse("2012/02/19");

OUTPUT @rs1   
    too@out
      USING Outputters.Tsv(quoting:false, dateTimeFormat:null);
```

Olá valores para  **@in**  e  **@out**  parâmetros no script hello U-SQL são transmitidos dinamicamente por ADF usando Olá 'parameters' seção. Consulte a seção de 'parameters' de saudação na definição do pipeline de saudação.

Você pode especificar outras propriedades, como prioridade e degreeOfParallelism também em sua definição de pipeline para trabalhos de saudação que são executados em Olá serviço de análise do Azure Data Lake.

## <a name="dynamic-parameters"></a>Parâmetros dinâmicos
Na definição de pipeline de exemplo hello, e parâmetros são atribuídos com valores codificados. 

```json
"parameters": {
    "in": "/datalake/input/SearchLog.tsv",
    "out": "/datalake/output/Result.tsv"
}
```

Em vez disso, é parâmetros dinâmicos toouse possíveis. Por exemplo: 

```json
"parameters": {
    "in": "$$Text.Format('/datalake/input/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)",
    "out": "$$Text.Format('/datalake/output/{0:yyyy-MM-dd HH:mm:ss}.tsv', SliceStart)"
}
```

Nesse caso, arquivos de entrada ainda são retirados da pasta de /datalake/input hello e arquivos de saída são gerados na pasta de /datalake/output hello. nomes de arquivo Hello são dinâmicos com base na hora de início de fatia hello.  

