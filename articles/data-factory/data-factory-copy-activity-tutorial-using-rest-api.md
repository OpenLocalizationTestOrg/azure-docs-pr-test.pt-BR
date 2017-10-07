---
title: "Tutorial: API de REST de uso toocreate um pipeline da fábrica de dados do Azure | Microsoft Docs"
description: "Neste tutorial, você usar a API REST toocreate um pipeline da fábrica de dados do Azure com um dado de toocopy de atividade de cópia de um armazenamento de BLOBs do Azure, um banco de dados do SQL Azure."
services: data-factory
documentationcenter: 
author: spelluru
manager: jhubbard
editor: monicar
ms.assetid: 1704cdf8-30ad-49bc-a71c-4057e26e7350
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: get-started-article
ms.date: 07/10/2017
ms.author: spelluru
ms.openlocfilehash: aa6c9b035101c4ff9acff90117ca6e3e7067f418
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="tutorial-use-rest-api-toocreate-an-azure-data-factory-pipeline-toocopy-data"></a>Tutorial: API de REST de uso toocreate um Azure Data Factory pipeline toocopy de dados 
> [!div class="op_single_selector"]
> * [Visão geral e pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
> * [Assistente de Cópia](data-factory-copy-data-wizard-tutorial.md)
> * [Portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md)
> * [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md)
> * [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md)
> * [Modelo do Azure Resource Manager](data-factory-copy-activity-tutorial-using-azure-resource-manager-template.md)
> * [API REST](data-factory-copy-activity-tutorial-using-rest-api.md)
> * [API do .NET](data-factory-copy-activity-tutorial-using-dotnet-api.md)
> 
> 

Neste artigo, você aprenderá como toouse REST API toocreate uma fábrica de dados com um pipeline que copia dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure. Se você estiver tooAzure nova fábrica de dados, leia Olá [tooAzure Introdução Data Factory](data-factory-introduction.md) artigo antes de fazer este tutorial.   

Neste tutorial, você criará um pipeline com uma atividade: atividade de cópia. Olá Copiar atividade copia dados de um repositório de dados com suporte de dados repositório tooa coletor com suporte. Para obter uma lista de armazenamentos de dados com suporte como origens e coletores, confira [Armazenamentos de dados com suporte](data-factory-data-movement-activities.md#supported-data-stores-and-formats). atividade de saudação é alimentada por um serviço disponível globalmente que pode copiar dados entre vários repositórios de dados de forma segura, confiável e escalonável. Para obter mais informações sobre hello atividade de cópia, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md).

Um pipeline pode ter mais de uma atividade. E, é possível encadear duas atividades (executadas uma atividade após o outro), definindo Olá o conjunto de dados de saída de uma atividade Olá outra atividade de conjunto de dados de saudação de entrada. Para saber mais, confira [Várias atividades em um pipeline](data-factory-scheduling-and-execution.md#multiple-activities-in-a-pipeline).

> [!NOTE]
> Este artigo não aborda todos Olá API de REST de fábrica de dados. Confira [Referência de API REST do Data Factory](/rest/api/datafactory/) para obter uma documentação abrangente sobre os cmdlets de Data Factory.
>  
> pipeline de dados Olá neste tutorial copia dados de um repositório de dados de destino fonte dados repositório tooa. Para obter um tutorial sobre como tootransform dados usando a fábrica de dados do Azure, consulte [Tutorial: Crie um pipeline de dados tootransform usando o cluster Hadoop](data-factory-build-your-first-pipeline.md).

## <a name="prerequisites"></a>Pré-requisitos
* Passar [visão geral do Tutorial](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) e hello completa **pré-requisito** etapas.
* Instale o [Curl](https://curl.haxx.se/dlwiz/) em seu computador. Use ferramenta de ondulação Olá com REST comandos toocreate uma fábrica de dados. 
* Siga as instruções [deste artigo](../azure-resource-manager/resource-group-create-service-principal-portal.md) para: 
  1. Crie um aplicativo Web chamado **ADFCopyTutorialApp** no Azure Active Directory.
  2. Obtenha a **ID do cliente** e a **chave secreta**. 
  3. Obtenha a **ID do locatário**. 
  4. Atribuir Olá **ADFCopyTutorialApp** aplicativo toohello **colaborador da fábrica de dados** função.  
* Instale o [Azure PowerShell](/powershell/azure/overview).  
* Iniciar **PowerShell** e Olá seguintes etapas. Mantenha o Azure PowerShell aberta até o fim deste tutorial hello. Se você fecha e reabrir o, será necessário comandos de saudação toorun novamente.
  
  1. Execute Olá comando a seguir e insira o nome de usuário de saudação e a senha que você use toosign em toohello portal do Azure:
    
    ```PowerShell 
    Login-AzureRmAccount
    ```   
  2. Execute todas as assinaturas de saudação para esta conta de Olá tooview de comando a seguir:

    ```PowerShell     
    Get-AzureRmSubscription
    ``` 
  3. Execute Olá assinatura de saudação do comando tooselect que você deseja toowork com a seguir. Substituir  **&lt;NameOfAzureSubscription** &gt; com o nome da saudação de sua assinatura do Azure. 
     
    ```PowerShell
    Get-AzureRmSubscription -SubscriptionName <NameOfAzureSubscription> | Set-AzureRmContext
    ```
  4. Criar um grupo de recursos do Azure denominado **ADFTutorialResourceGroup** executando Olá comando de saudação do PowerShell a seguir:  

    ```PowerShell     
      New-AzureRmResourceGroup -Name ADFTutorialResourceGroup  -Location "West US"
    ```
     
      Se o grupo de recursos Olá já existe, especifique se tooupdate-lo (Y) ou mantê-lo como (N). 
     
      Algumas das etapas de saudação neste tutorial presumem que você use o grupo de recursos de saudação chamado ADFTutorialResourceGroup. Se você usar um grupo de recursos diferentes, você precisa toouse nome de saudação do seu grupo de recursos no lugar de ADFTutorialResourceGroup neste tutorial.

## <a name="create-json-definitions"></a>Criar definições JSON
Crie arquivos JSON na pasta Olá onde se encontra curl.exe a seguir. 

### <a name="datafactoryjson"></a>datafactory.json
> [!IMPORTANT]
> Nome deve ser globalmente exclusivo, portanto, talvez você queira tooprefix/sufixo ADFCopyTutorialDF toomake ele um nome exclusivo. 
> 
> 

```JSON
{  
    "name": "ADFCopyTutorialDF",  
    "location": "WestUS"
}  
```

### <a name="azurestoragelinkedservicejson"></a>azurestoragelinkedservice.json
> [!IMPORTANT]
> Substitua **nome da conta** e **chave da conta** pelo nome e pela chave da sua conta de armazenamento do Azure. toolearn como tooget seu armazenamento acessar chave, consulte [exibir, copiar e regenerar as contas de armazenamento de chaves de acesso](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).

```JSON
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
        }
    }
}
```

Para obter detalhes sobre as propriedades JSON, confira [Serviço vinculado do Armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service).

### <a name="azuersqllinkedservicejson"></a>azuersqllinkedservice.json
> [!IMPORTANT]
> Substituir **servername**, **databasename**, **username**, e **senha** com o nome do seu servidor SQL Azure, o nome do banco de dados SQL, usuário conta e senha para conta de saudação.  
> 
>

```JSON
{
    "name": "AzureSqlLinkedService",
    "properties": {
        "type": "AzureSqlDatabase",
        "description": "",
        "typeProperties": {
            "connectionString": "Data Source=tcp:<servername>.database.windows.net,1433;Initial Catalog=<databasename>;User ID=<username>;Password=<password>;Integrated Security=False;Encrypt=True;Connect Timeout=30"
        }
    }
}
```

Para obter detalhes sobre as propriedades JSON, confira [Serviço vinculado do Azure SQL](data-factory-azure-sql-connector.md#linked-service-properties).

### <a name="inputdatasetjson"></a>inputdataset.json

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "AzureStorageLinkedService",
    "typeProperties": {
      "folderPath": "adftutorial/",
      "fileName": "emp.txt",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ","
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:

| Propriedade | Descrição |
|:--- |:--- |
| type | propriedade do tipo Hello está definida muito**AzureBlob** porque os dados residem em um armazenamento de BLOBs do Azure. |
| linkedServiceName | Refere-se toohello **AzureStorageLinkedService** que você criou anteriormente. |
| folderPath | Especifica o blob Olá **contêiner** e hello **pasta** que contém blobs de entrada. Neste tutorial, adftutorial é o contêiner de blob hello e pasta é a pasta raiz de saudação. | 
| fileName | Essa propriedade é opcional. Se você omitir essa propriedade, todos os arquivos de saudação folderPath são escolhidos. Neste tutorial, **emp.txt** é especificado para hello fileName, portanto, somente esse arquivo é escolhida para processamento. |
| formato -> tipo |arquivo de entrada Hello está no formato de texto de saudação, para que possamos usar **TextFormat**. |
| columnDelimiter | saudação de colunas no arquivo de entrada hello é delimitadas por **caractere de vírgula (`,`)**. |
| frequência/intervalo | frequência de saudação está definida muito**hora** e o intervalo é definido muito**1**, que significa que Olá entrada fatias estão disponíveis **por hora**. Em outras palavras, Olá serviço da fábrica de dados procura por dados de entrada a cada hora na pasta raiz de saudação do contêiner de blob (**adftutorial**) especificado. Ele procura os dados de saudação em Olá pipeline início e término vezes, não antes ou depois desses tempos.  |
| externo | Essa propriedade é definida, muito**true** se os dados de saudação não são gerados por este pipeline. dados de entrada Hello neste tutorial estão no arquivo de emp.txt hello, que não é gerado por este pipeline, portanto vamos definir essa propriedade tootrue. |

Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).

### <a name="outputdatasetjson"></a>outputdataset.json

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "structure": [
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "emp"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
Olá, tabela a seguir fornece descrições para propriedades JSON Olá usadas no trecho hello:

| Propriedade | Descrição |
|:--- |:--- |
| type | propriedade do tipo Hello está definida muito**AzureSqlTable** porque os dados são copiados tooa tabela em um banco de dados do SQL Azure. |
| linkedServiceName | Refere-se toohello **AzureSqlLinkedService** que você criou anteriormente. |
| tableName | Olá especificado **tabela** toowhich Olá dados são copiados. | 
| frequência/intervalo | Olá frequência é definida muito**hora** e o intervalo é **1**, o que significa que Olá fatias de saída são produzidas **por hora** entre Olá pipeline início e término vezes, não antes ou Após esses horários.  |

Há três colunas – **ID**, **FirstName**, e **LastName** – na tabela de emp Olá no banco de dados de saudação. ID é uma coluna de identidade, portanto, você precisa apenas toospecify **FirstName** e **LastName** aqui.

Para saber mais sobre essas propriedades JSON, confira o [artigo sobre o conector do SQL](data-factory-azure-sql-connector.md#dataset-properties).

### <a name="pipelinejson"></a>pipeline.json

```JSON
{
  "name": "ADFTutorialPipeline",
  "properties": {
    "description": "Copy data from a blob tooAzure SQL table",
    "activities": [
      {
        "name": "CopyFromBlobToSQL",
        "description": "Push Regional Effectiveness Campaign data tooAzure SQL database",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSqlOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "SqlSink",
            "writeBatchSize": 10000,
            "writeBatchTimeout": "60:00:00"
          }
        },
        "Policy": {
          "concurrency": 1,
          "executionPriorityOrder": "NewestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
    ],
    "start": "2017-05-11T00:00:00Z",
    "end": "2017-05-12T00:00:00Z"
  }
}
```

Observe Olá pontos a seguir:

- Na seção de atividades hello, há apenas uma atividade cuja **tipo** está definido muito**cópia**. Para obter mais informações sobre a atividade de cópia hello, consulte [atividades de movimentação de dados](data-factory-data-movement-activities.md). Nas soluções de Data Factory, você também pode usar [atividades de transformação de dados](data-factory-data-transformation-activities.md).
- Entrada para atividade de saudação é definida muito**AzureBlobInput** e de saída para o conjunto de hello atividade é muito**AzureSqlOutput**. 
- Em Olá **typeProperties** seção, **BlobSource** é especificado como tipo de fonte hello e **SqlSink** é especificado como tipo de coletor de saudação. Para obter uma lista completa de armazenamentos de dados de atividade de cópia hello como origens e coletores com suporte, consulte [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats). toolearn como toouse dados específicos com suporte são armazenados como um fonte/coletor, clique o link de saudação na tabela de saudação.  
 
Substituir valor Olá Olá **iniciar** propriedade com hello dia atual e **final** valor com hello dia seguinte. Você pode especificar apenas parte da data hello e ignore a parte de hora de saudação da saudação data hora. Por exemplo, "2017-02-03", que é o equivalente muito "2017-02-03T00:00:00Z"
 
Ambos os valores de data/hora de início e de término devem estar no [formato ISO](http://en.wikipedia.org/wiki/ISO_8601). Por exemplo: 2016-10-14T16:32:41Z. Olá **final** tempo é opcional, mas usamos neste tutorial. 
 
Se você não especificar o valor para Olá **final** propriedade, ele é calculado como "**início + 48 horas**". pipeline de saudação toorun indefinidamente, especifique **9999-09-09** como valor Olá Olá **final** propriedade.
 
Olá anterior de exemplo, há 24 fatias de dados como cada fatia de dados é produzida por hora.

Para obter descrições das propriedades JSON em uma definição de pipeline, consulte o artigo [Criar pipelines](data-factory-create-pipelines.md). Para obter descrições das propriedades JSON em uma definição de atividade de cópia, consulte [Atividades de movimentação de dados](data-factory-data-movement-activities.md). Para obter descrições das propriedades JSON com suporte pelo BlobSource, consulte o [artigo sobre o conector de blobs do Azure](data-factory-azure-blob-connector.md). Para obter descrições das propriedades JSON com suporte pelo SqlSink, consulte o [artigo sobre o conector do Banco de Dados SQL](data-factory-azure-sql-connector.md).

## <a name="set-global-variables"></a>Definir variáveis globais
No Azure PowerShell, execute Olá comandos a seguir depois de substituir os valores hello com seu próprio:

> [!IMPORTANT]
> Veja a seção [Pré-requisitos](#prerequisites) para obter instruções sobre como obter a ID do cliente, o segredo do cliente, a ID do locatário e ID da assinatura.   
> 
> 

```JSON
$client_id = "<client ID of application in AAD>"
$client_secret = "<client key of application in AAD>"
$tenant = "<Azure tenant ID>";
$subscription_id="<Azure subscription ID>";

$rg = "ADFTutorialResourceGroup"
```

Olá executar comando a seguir depois de atualizar o nome da saudação Olá da fábrica de dados que você está usando: 

```
$adf = "ADFCopyTutorialDF"
```

## <a name="authenticate-with-aad"></a>Autenticar com o AAD
Execute Olá tooauthenticate de comando com o Azure Active Directory (AAD) a seguir: 

```PowerShell
$cmd = { .\curl.exe -X POST https://login.microsoftonline.com/$tenant/oauth2/token  -F grant_type=client_credentials  -F resource=https://management.core.windows.net/ -F client_id=$client_id -F client_secret=$client_secret };
$responseToken = Invoke-Command -scriptblock $cmd;
$accessToken = (ConvertFrom-Json $responseToken).access_token;

(ConvertFrom-Json $responseToken) 
```

## <a name="create-data-factory"></a>Criar um data factory
Nesta etapa, você criará um Azure Data Factory chamado **ADFCopyTutorialDF**. Uma fábrica de dados pode ter um ou mais pipelines. Um pipeline em um data factory pode ter uma ou mais atividades. Por exemplo, armazenar dados de toocopy uma atividade de cópia de uma fonte de dados de destino tooa. Dados de saída de tooproduct de dados de entrada de uma atividade de Hive do HDInsight toorun um tootransform de script do Hive. Execute Olá fábrica de dados de saudação de toocreate comandos a seguir: 

1. Atribuir Olá comando toovariable chamado **cmd**. 
   
    > [!IMPORTANT]
    > Confirmar esse nome Olá Olá da fábrica de dados especificadas aqui (ADFCopyTutorialDF) correspondências Olá nome especificado no hello **datafactory.json**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@datafactory.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/ADFCopyTutorialDF0411?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se a fábrica de dados Olá foi criada com êxito, você vê Olá JSON Olá fábrica de dados em Olá **resultados**; caso contrário, você verá uma mensagem de erro.  
   
    ```
    Write-Host $results
    ```

Observe Olá pontos a seguir:

* nome de saudação do hello Azure Data Factory deve ser globalmente exclusivo. Se você vir o erro Olá nos resultados: **"ADFCopyTutorialDF" nome da fábrica de dados não está disponível**, Olá seguintes etapas:  
  
  1. Alterar nome da saudação (por exemplo, yournameADFCopyTutorialDF) em Olá **datafactory.json** arquivo.
  2. No comando primeiro Olá Olá onde **$cmd** variável é atribuída a um valor, substitua ADFCopyTutorialDF pelo novo nome de saudação e execute o comando de saudação. 
  3. Execute Olá dois comandos tooinvoke Olá API REST toocreate Olá dados fábrica e impressão Olá resultados da operação de saudação. 
     
     Consulte o tópico [Data Factory - regras de nomenclatura](data-factory-naming-rules.md) para ver as regras de nomenclatura para artefatos de Data Factory.
* toocreate instâncias de fábrica de dados, você precisa toobe um colaborador/administrador de saudação assinatura do Azure
* nome Olá Olá da fábrica de dados pode ser registrado como um nome DNS no futuro de saudação e, portanto, se tornar publicamente visível.
* Se você receber o erro Olá: "**esta assinatura não está registrado toouse namespace DataFactory**", execute um dos seguintes hello e tente publicar novamente: 
  
  * No Azure PowerShell, execute Olá provedor do comando tooregister Olá fábrica de dados a seguir: 

    ```PowerShell    
    Register-AzureRmResourceProvider -ProviderNamespace Microsoft.DataFactory
    ```
    Você pode executar Olá tooconfirm de comando a seguir que Olá Data Factory provedor está registrado. 
    
    ```PowerShell
    Get-AzureRmResourceProvider
    ```
  * Usando o logon Olá assinatura do Azure em Olá [portal do Azure](https://portal.azure.com) e navegue tooa folha de fábrica de dados (ou) criar uma fábrica de dados no hello portal do Azure. Esta ação registra automaticamente o provedor de saudação para você.

Antes de criar um pipeline, é necessário toocreate algumas entidades da fábrica de dados pela primeira vez. Você primeiro criar a fonte de toolink serviços vinculados e dados de destino armazena dados tooyour armazenar. Em seguida, defina conjuntos de dados de entrada e saída toorepresent dados em repositórios de dados vinculados. Finalmente, crie o pipeline de saudação com uma atividade que usa esses conjuntos de dados.

## <a name="create-linked-services"></a>Criar serviços vinculados
Você pode criar serviços vinculados em um toolink de fábrica de dados seus dados, armazena e fábrica de dados toohello de serviços de computação. Neste tutorial, você não usa serviços de computação, como o Azure HDInsight ou o Azure Data Lake Analytics. Você usa dois armazenamentos de dados do tipo Armazenamento do Azure (origem) e o banco de dados SQL (destino). Portanto, você pode criar dois serviços vinculados, chamados AzureStorageLinkedService e AzureSqlLinkedService, dos tipos: AzureStorage e AzureSqlDatabase.  

Olá AzureStorageLinkedService vincula sua fábrica de dados de toohello de conta de armazenamento do Azure. Esta conta de armazenamento é hello um no qual você criou um contêiner e carregou dados de saudação como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).   

AzureSqlLinkedService vincula sua fábrica de dados de toohello de banco de dados do SQL Azure. Olá dados são copiados do armazenamento de blob Olá são armazenados neste banco de dados. Você criou tabela emp de saudação neste banco de dados como parte do [pré-requisitos](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).  

### <a name="create-azure-storage-linked-service"></a>Criar o serviço vinculado do armazenamento do Azure
Nesta etapa, você vincular sua fábrica de dados de tooyour de conta de armazenamento do Azure. Especifique o nome hello e a chave da sua conta de armazenamento do Azure nesta seção. Consulte [serviço vinculado do armazenamento do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) para obter detalhes sobre o JSON propriedades usadas toodefine um armazenamento do Azure serviço vinculado.  

1. Atribuir Olá comando toovariable chamado **cmd**. 

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@azurestoragelinkedservice.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureStorageLinkedService?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se Olá vinculado serviço foi criado com êxito, consulte Olá JSON para o serviço de saudação vinculado no hello **resultados**; caso contrário, você verá uma mensagem de erro.

    ```PowerShell   
    Write-Host $results
    ```

### <a name="create-azure-sql-linked-service"></a>Criar serviço vinculado do Azure SQL
Nesta etapa, você vincular sua fábrica de dados de tooyour de banco de dados do SQL Azure. Especifique o nome do servidor SQL Azure Olá, nome do banco de dados, nome de usuário e senha de usuário nesta seção. Consulte [serviço vinculado do SQL Azure](data-factory-azure-sql-connector.md#linked-service-properties) para obter detalhes sobre o JSON propriedades usadas toodefine um SQL Azure serviço vinculado.

1. Atribuir Olá comando toovariable chamado **cmd**. 
   
    ```PowerShell
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data “@azuresqllinkedservice.json” https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/linkedservices/AzureSqlLinkedService?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se Olá vinculado serviço foi criado com êxito, consulte Olá JSON para o serviço de saudação vinculado no hello **resultados**; caso contrário, você verá uma mensagem de erro.
   
    ```PowerShell
    Write-Host $results
    ```

## <a name="create-datasets"></a>Criar conjuntos de dados
Na etapa anterior de saudação, você criou serviços vinculados toolink sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure. Nesta etapa, você definirá dois conjuntos de dados denominados AzureBlobInput AzureSqlOutput que representam a entrada e saída dados e que são armazenados em repositórios de dados Olá referenciados por AzureStorageLinkedService e AzureSqlLinkedService, respectivamente.

serviço de armazenamento do Azure vinculado Olá Especifica a cadeia de conexão de Olá usada pelo serviço de fábrica de dados em tempo de execução tooconnect tooyour conta de armazenamento do Azure. E, Olá o conjunto de dados de blob de entrada (AzureBlobInput) Especifica o contêiner de saudação e a pasta de saudação que contém os dados de entrada hello.  

Da mesma forma, Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução. E, Olá saída SQL o conjunto de dados de tabela (OututDataset) Especifica a tabela de saudação em Olá Olá de toowhich de banco de dados dados saudação do armazenamento de blob são copiados. 

### <a name="create-input-dataset"></a>Criar conjunto de dados de entrada
Nesta etapa, você criar um conjunto de dados chamado AzureBlobInput que aponta o arquivo de blob tooa (emp.txt) na pasta raiz de saudação de um contêiner de blob (adftutorial) no hello representado por Olá AzureStorageLinkedService vinculado de serviço de armazenamento do Azure. Se você não especificar um valor para o nome de arquivo hello (ou ignorá-lo), dados de todos os blobs na pasta de entrada hello são copiados toohello destino. Neste tutorial, você deve especificar um valor para o nome de arquivo hello. 

1. Atribuir Olá comando toovariable chamado **cmd**. 

    ```PowerSHell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@inputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureBlobInput?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.
   
    ```PowerShell
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.
   
    ```PowerShell
    Write-Host $results
    ```

### <a name="create-output-dataset"></a>Criar conjunto de dados de saída
Olá serviço de banco de dados do SQL Azure vinculado Especifica a cadeia de caracteres de conexão de saudação que usa o serviço de fábrica de dados no banco de dados SQL do Azure tooyour de tooconnect de tempo de execução. Olá saída SQL tabela dataset (OututDataset) você criar nessa etapa Especifica a tabela Olá Olá toowhich Olá de banco de dados armazenamento de blob de saudação é copiada.

1. Atribuir Olá comando toovariable chamado **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@outputdataset.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/AzureSqlOutput?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.
    
    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.
   
    ```PowerShell
    Write-Host $results
    ``` 

## <a name="create-pipeline"></a>Criar um pipeline
Nesta etapa, você cria um pipeline com uma **atividade de cópia** que usa **AzureBlobInput** como uma entrada e **AzureSqlOutput** como uma saída.

Atualmente, o conjunto de dados de saída é quais unidades Olá agenda. Neste tutorial, o conjunto de dados de saída é configurado tooproduce uma fatia de uma vez por hora. pipeline de saudação tem uma hora de início e a hora de término que são um dia de distância, que é de 24 horas. Portanto, 24 fatias de conjunto de dados de saída são produzidas pelo pipeline de saudação. 

1. Atribuir Olá comando toovariable chamado **cmd**.

    ```PowerShell   
    $cmd = {.\curl.exe -X PUT -H "Authorization: Bearer $accessToken" -H "Content-Type: application/json" --data "@pipeline.json" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datapipelines/MyFirstPipeline?api-version=2015-10-01};
    ```
2. Execute o comando hello usando **Invoke-Command**.

    ```PowerShell   
    $results = Invoke-Command -scriptblock $cmd;
    ```
3. Exibir resultados de saudação. Se Olá conjunto de dados foi criado com êxito, você verá hello JSON para o conjunto de dados Olá Olá **resultados**; caso contrário, você verá uma mensagem de erro.  

    ```PowerShell   
    Write-Host $results
    ```

**Parabéns!** Você criou com êxito uma fábrica de dados do Azure, com um pipeline que copia dados de banco de dados do SQL Azure Blob Storage tooAzure.

## <a name="monitor-pipeline"></a>Monitorar o pipeline
Nesta etapa, você deve usar fatias de toomonitor de API de REST de fábrica de dados produzidas pelo pipeline de saudação.

```PowerShell
$ds ="AzureSqlOutput"
```

> [!IMPORTANT] 
> Certifique-se de início de saudação e de término horas Olá especificado no seguinte comando correspondência Olá início e término do pipeline de saudação. 

```PowerShell
$cmd = {.\curl.exe -X GET -H "Authorization: Bearer $accessToken" https://management.azure.com/subscriptions/$subscription_id/resourcegroups/$rg/providers/Microsoft.DataFactory/datafactories/$adf/datasets/$ds/slices?start=2017-05-11T00%3a00%3a00.0000000Z"&"end=2017-05-12T00%3a00%3a00.0000000Z"&"api-version=2015-10-01};
```

```PowerShell
$results2 = Invoke-Command -scriptblock $cmd;
```

```PowerShell
IF ((ConvertFrom-Json $results2).value -ne $NULL) {
    ConvertFrom-Json $results2 | Select-Object -Expand value | Format-Table
} else {
        (convertFrom-Json $results2).RemoteException
}
```

Executar Olá Invoke-Command e hello outro até que você veja uma fatia em **pronto** estado ou **falha** estado. Quando a fatia hello está no estado pronto, verificar Olá **emp** tabela no banco de dados SQL do Azure para dados de saída de hello. 

Para cada fatia, duas linhas de dados do arquivo de origem de saudação são copiados toohello tabela de emp no banco de dados do SQL Azure hello. Portanto, você ver 24 novos registros na tabela de emp hello quando todas as fatias de saudação são processadas com êxito (no estado pronto). 

## <a name="summary"></a>Resumo
Neste tutorial, você usou a API REST toocreate um Azure fábrica toocopy dados de um banco de dados do SQL Azure de tooan BLOBs do Azure. Aqui estão as etapas de alto nível Olá executada neste tutorial:  

1. Foi criada uma **data factory**do Azure.
2. Foram criados **serviços vinculados**:
   1. Um armazenamento do Azure vinculada ao serviço toolink sua conta de armazenamento do Azure que contém dados de entrada.     
   2. Um SQL Azure vinculado serviço toolink seu banco de dados SQL do Azure que contém dados de saída de saudação. 
3. Foram criados **conjuntos de dados**que descrevem os dados de entrada e de saída para os pipelines.
4. Foi criado um **pipeline** com uma Atividade de Cópia com BlobSource como origem e SqlSink como coletor. 

## <a name="next-steps"></a>Próximas etapas
Neste tutorial, você usou o armazenamento de blobs do Azure como um armazenamento de dados de origem e um banco de dados SQL do Azure como um armazenamento de dados de destino em uma operação de cópia. Olá tabela a seguir fornece uma lista de repositórios de dados com suporte como origens e destinos de atividade de cópia de saudação: 

[!INCLUDE [data-factory-supported-data-stores](../../includes/data-factory-supported-data-stores.md)]

toolearn sobre como armazenam dados toocopy para/de uma data, clique o link Olá Olá repositório de dados na tabela de saudação.
