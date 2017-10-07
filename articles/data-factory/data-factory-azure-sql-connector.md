---
title: aaaCopy dados para/de banco de dados do SQL Azure | Microsoft Docs
description: Saiba como toocopy dados para/de banco de dados do SQL Azure usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 484f735b-8464-40ba-a9fc-820e6553159e
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: d2ff16191afb028da75699c5e4d0bb310538db0f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-tooand-from-azure-sql-database-using-azure-data-factory"></a>Copiar dados tooand do banco de dados do SQL Azure usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia no Azure Data Factory toomove dados tooand do banco de dados do SQL Azure. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.  

## <a name="supported-scenarios"></a>Cenários com suporte
Você pode copiar dados **do banco de dados do SQL Azure** toohello repositórios de dados a seguir:

[!INCLUDE [data-factory-supported-sinks](../../includes/data-factory-supported-sinks.md)]

Você pode copiar dados de saudação armazenamentos de dados a seguir **tooAzure banco de dados SQL**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-authentication-type"></a>Tipos de autenticação com suporte
O conector do Banco de Dados SQL do Azure dá suporte à autenticação básica.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente de um Banco de Dados SQL do Azure usando diferentes ferramentas/APIs.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir: 

1. Criar uma **data factory**. Um data factory pode conter um ou mais pipelines. 
2. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica. Por exemplo, se você estiver copiando dados de um banco de dados de SQL do Azure de tooan do armazenamento de BLOBs do Azure, você criar duas toolink de serviços vinculados sua conta de armazenamento do Azure e a fábrica de dados de tooyour de banco de dados do SQL Azure. Para propriedades de serviço vinculado que específico tooAzure banco de dados SQL, consulte [vinculado propriedades do serviço](#linked-service-properties) seção. 
3. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. O exemplo hello mencionado na última etapa do hello, você criará um contêiner de blob do conjunto de dados toospecify hello e a pasta que contém os dados de entrada hello. E, você cria outra tabela do conjunto de dados toospecify Olá SQL no banco de dados de SQL do Azure de saudação que contém dados Olá copiados saudação do armazenamento de blob. Para propriedades de conjunto de dados que são específico tooAzure repositório Data Lake, consulte [propriedades de conjunto de dados](#dataset-properties) seção.
4. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. Exemplo hello mencionado anteriormente, você usar BlobSource como uma origem e do SqlSink como um coletor de atividade de cópia de saudação. Da mesma forma, se você estiver copiando de banco de dados do Azure SQL tooAzure armazenamento de Blob, use SqlSource e BlobSink na atividade de cópia de saudação. Para propriedades de atividade de cópia que específico tooAzure banco de dados SQL, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção. Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados.

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um banco de dados do SQL Azure, consulte [exemplos JSON](#json-examples-for-copying-data-to-and-from-sql-database) deste artigo. 

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAzure banco de dados SQL: 

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Um SQL Azure vinculado links serviço uma fábrica de dados de tooyour de banco de dados do SQL Azure. Olá, a tabela a seguir fornece o serviço vinculado de descrição de JSON de elementos específico tooAzure SQL.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **AzureSqlDatabase** |Sim |
| connectionString |Especifique informações necessárias a instância de banco de dados do Azure SQL toohello tooconnect para a propriedade connectionString de saudação. Há suporte somente para autenticação básica. |Sim |

> [!IMPORTANT]
> Configurar [Firewall de banco de dados do SQL Azure](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure) Olá o servidor de banco de dados muito[permitir que serviços do Azure tooaccess Olá servidor](https://msdn.microsoft.com/library/azure/ee621782.aspx#ConnectingFromAzure). Além disso, se você estiver copiando dados tooAzure banco de dados SQL, incluindo Azure fora de fontes de dados local com o gateway da fábrica de dados, configure o intervalo de endereços IP apropriado para a máquina de saudação que está enviando dados tooAzure banco de dados SQL.

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
toospecify toorepresent um conjunto de dados dados de entrada ou saídos em um banco de dados do SQL Azure, defina propriedade de tipo de saudação do conjunto de dados Olá para: **AzureSqlTable**. Saudação de conjunto **linkedServiceName** serviço vinculado de propriedade de nome de toohello Olá dataset de saudação SQL Azure.  

Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação. Olá **typeProperties** seção de conjunto de dados de saudação do tipo **AzureSqlTable** tem Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação ou exibição na instância de banco de dados do Azure SQL Olá que serviço vinculado refere-se a. |Sim |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.

> [!NOTE]
> Hello atividade de cópia usa apenas uma entrada e produz apenas uma saída.

Por outro lado, as propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Se você estiver movendo dados de um banco de dados do SQL Azure, você defina o tipo de fonte de saudação na atividade de cópia de saudação muito**SqlSource**. Da mesma forma, se você estiver movendo o banco de dados do SQL Azure data tooan, você definir o tipo de coletor Olá na atividade de cópia de saudação muito**SqlSink**. Esta seção fornece uma lista das propriedades com suporte de SqlSource e SqlSink.

### <a name="sqlsource"></a>SqlSource
Atividade de cópia, quando a fonte de saudação é do tipo **SqlSource**, Olá propriedades a seguir está disponível em **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| SqlReaderQuery |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Exemplo: `select * from MyTable`. |Não |
| sqlReaderStoredProcedureName |Nome da saudação procedimento armazenado que lê dados da tabela de origem hello. |Nome da saudação de procedimento armazenado. Olá a última instrução de SQL deve ser uma instrução SELECT no procedimento armazenado de saudação. |Não |
| storedProcedureParameters |Parâmetros de saudação de procedimento armazenado. |Pares de nome/valor. Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação. |Não |

Se hello **sqlReaderQuery** é especificada para Olá SqlSource, hello atividade de cópia executa esta consulta em relação aos dados de saudação do hello Azure SQL Database fonte tooget. Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).

Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de saudação definidas na seção de estrutura de saudação do conjunto de dados Olá JSON são usado toobuild uma consulta (`select column1, column2 from mytable`) toorun contra hello Azure SQL Database. Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.

> [!NOTE]
> Quando você usa **sqlReaderStoredProcedureName**, você ainda precisa toospecify um valor para Olá **tableName** propriedade no conjunto de dados Olá JSON. Contudo, não há nenhuma validação executada nessa tabela.
>
>

### <a name="sqlsource-example"></a>Exemplo de SqlSource

```JSON
"source": {
    "type": "SqlSource",
    "sqlReaderStoredProcedureName": "CopyTestSrcStoredProcedureWithParameters",
    "storedProcedureParameters": {
        "stringData": { "value": "str3" },
        "identifier": { "value": "$$Text.Format('{0:yyyy}', SliceStart)", "type": "Int"}
    }
}
```

**definição do procedimento armazenada de saudação:**

```SQL
CREATE PROCEDURE CopyTestSrcStoredProcedureWithParameters
(
    @stringData varchar(20),
    @identifier int
)
AS
SET NOCOUNT ON;
BEGIN
     select *
     from dbo.UnitTestSrcTable
     where dbo.UnitTestSrcTable.stringData != stringData
    and dbo.UnitTestSrcTable.identifier != identifier
END
GO
```

### <a name="sqlsink"></a>SqlSink
**SqlSink** dá suporte a saudação propriedades a seguir:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar. |timespan<br/><br/> Exemplo: "00:30:00" (30 minutos). |Não |
| writeBatchSize |Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize. |Inteiro (número de linhas) |Não (padrão: 10000) |
| sqlWriterCleanupScript |Especifique uma consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa. Para saber mais, consulte [cópia repetida](#repeatable-copy). |Uma instrução de consulta. |Não |
| sliceIdentifierColumnName |Especifique um nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente. Para saber mais, consulte [cópia repetida](#repeatable-copy). |Nome de uma coluna com tipo de dados de binário (32). |Não |
| sqlWriterStoredProcedureName |Nome do hello procedimento armazenado dados upserts (atualizações/inserções) na tabela de destino de saudação. |Nome da saudação de procedimento armazenado. |Não |
| storedProcedureParameters |Parâmetros de saudação de procedimento armazenado. |Pares de nome/valor. Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação. |Não |
| sqlWriterTableType |Especifique um toobe de nome de tipo de tabela usado no procedimento armazenado de saudação. Atividade de cópia disponibiliza dados Olá movidos em uma tabela temporária com esse tipo de tabela. Código do procedimento armazenado, em seguida, pode mesclar dados de saudação sejam copiados com os dados existentes. |Um nome de tipo de tabela. |Não |

#### <a name="sqlsink-example"></a>Exemplo de SqlSink

```JSON
"sink": {
    "type": "SqlSink",
    "writeBatchSize": 1000000,
    "writeBatchTimeout": "00:05:00",
    "sqlWriterStoredProcedureName": "CopyTestStoredProcedureWithParameters",
    "sqlWriterTableType": "CopyTestTableType",
    "storedProcedureParameters": {
        "identifier": { "value": "1", "type": "Int" },
        "stringData": { "value": "str1" },
        "decimalData": { "value": "1", "type": "Decimal" }
    }
}
```

## <a name="json-examples-for-copying-data-tooand-from-sql-database"></a>Exemplos JSON para copiar dados tooand do banco de dados SQL
Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Eles mostram como toocopy tooand de dados do banco de dados do SQL Azure e armazenamento de BLOBs do Azure. No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.

### <a name="example-copy-data-from-azure-sql-database-tooazure-blob"></a>Exemplo: Copiar dados de banco de dados do Azure SQL tooAzure Blob
Olá mesmo define Olá entidades da fábrica de dados a seguir:

1. Um serviço vinculado do tipo [AzureSqlDatabase](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureSqlTable](#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com uma Atividade de Cópia que usa [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de série temporal (por hora, diariamente, etc) de uma tabela no blob de tooa de banco de dados do SQL Azure a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.  

**Serviço vinculado para o Banco de Dados SQL do Azure:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Consulte Olá [serviço vinculado do SQL Azure](#linked-service) seção para obter lista de saudação de propriedades com suporte por esse serviço vinculado.

**Serviço vinculado do armazenamento de Blob do Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Consulte Olá [BLOBs do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) artigo de lista de saudação de propriedades com suporte por esse serviço vinculado.


**Conjunto de dados de entrada do SQL Azure:**

exemplo Hello supõe que você criou uma tabela "MyTable" no SQL Azure e contém uma coluna chamada "timestampcolumn" para dados de série temporal.

Definindo "externo": "verdadeiro" informa serviço do Azure Data Factory Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```JSON
{
  "name": "AzureSqlInput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyTable"
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```

Consulte Olá [propriedades de tipo de conjunto de dados do SQL Azure](#dataset) seção para obter lista de saudação de propriedades com suporte por este tipo de conjunto de dados.  

**Conjunto de dados de saída de Blob do Azure:**

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```JSON
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}/",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": "\t",
        "rowDelimiter": "\n"
      }
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
Consulte Olá [propriedades de tipo de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) seção para obter lista de saudação de propriedades com suporte por este tipo de conjunto de dados.  

**Uma atividade de cópia em um pipeline com origem SQL e coletor de Blob:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlSource** e **coletor** tipo está definido muito**BlobSink**. consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "AzureSQLtoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureSQLInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureBlobOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "BlobSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
     ]
   }
}
```
No exemplo hello, **sqlReaderQuery** é especificado para Olá SqlSource. Hello atividade de cópia executa esta consulta Olá dados do banco de dados do Azure SQL origem tooget hello. Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).

Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de saudação definidas na seção de estrutura de saudação do conjunto de dados Olá JSON são usado toobuild toorun uma consulta em relação a saudação banco de dados do SQL Azure. Por exemplo: `select column1, column2 from mytable`. Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.

Consulte Olá [fonte Sql](#sqlsource) seção e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de saudação de propriedades com suporte SqlSource e BlobSink.

### <a name="example-copy-data-from-azure-blob-tooazure-sql-database"></a>Exemplo: Copiar dados de Blob do Azure tooAzure banco de dados SQL
exemplo Hello define Olá entidades da fábrica de dados a seguir:  

1. Um serviço vinculado do tipo [AzureSqlDatabase](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSqlTable](#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com a atividade de Cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#copy-activity-properties).

exemplo Hello copia dados de série temporal (por hora, diariamente, etc) da tabela de tooa de BLOBs do Azure no banco de dados do SQL Azure a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

**Serviço vinculado do SQL Azure:**

```JSON
{
  "name": "AzureSqlLinkedService",
  "properties": {
    "type": "AzureSqlDatabase",
    "typeProperties": {
      "connectionString": "Server=tcp:<servername>.database.windows.net,1433;Database=<databasename>;User ID=<username>@<servername>;Password=<password>;Trusted_Connection=False;Encrypt=True;Connection Timeout=30"
    }
  }
}
```
Consulte Olá [serviço vinculado do SQL Azure](#linked-service) seção para obter lista de saudação de propriedades com suporte por esse serviço vinculado.

**Serviço vinculado do armazenamento de Blob do Azure:**

```JSON
{
  "name": "StorageLinkedService",
  "properties": {
    "type": "AzureStorage",
    "typeProperties": {
      "connectionString": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
    }
  }
}
```
Consulte Olá [BLOBs do Azure](data-factory-azure-blob-connector.md#azure-storage-linked-service) artigo de lista de saudação de propriedades com suporte por esse serviço vinculado.


**Conjunto de dados de entrada de Blob do Azure:**

Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1). Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início. "externo": "verdadeira" configuração informa o serviço de fábrica de dados de saudação que essa tabela é toohello externo fábrica de dados e não é produzida por uma atividade na fábrica de dados hello.

```JSON
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/",
      "fileName": "{Hour}.csv",
      "partitionedBy": [
        {
          "name": "Year",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "yyyy"
          }
        },
        {
          "name": "Month",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "MM"
          }
        },
        {
          "name": "Day",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "dd"
          }
        },
        {
          "name": "Hour",
          "value": {
            "type": "DateTime",
            "date": "SliceStart",
            "format": "HH"
          }
        }
      ],
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "rowDelimiter": "\n"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Hour",
      "interval": 1
    },
    "policy": {
      "externalData": {
        "retryInterval": "00:01:00",
        "retryTimeout": "00:10:00",
        "maximumRetry": 3
      }
    }
  }
}
```
Consulte Olá [propriedades de tipo de conjunto de dados de Blob do Azure](data-factory-azure-blob-connector.md#dataset-properties) seção para obter lista de saudação de propriedades com suporte por este tipo de conjunto de dados.

**Conjunto de dados de saída do Banco de Dados SQL do Azure:**

exemplo Hello copiará a tabela de tooa de dados denominada "MyTable" no SQL Azure. Criar tabela de saudação no SQL Azure com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello. Novas linhas são adicionadas a tabela de toohello a cada hora.

```JSON
{
  "name": "AzureSqlOutput",
  "properties": {
    "type": "AzureSqlTable",
    "linkedServiceName": "AzureSqlLinkedService",
    "typeProperties": {
      "tableName": "MyOutputTable"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```
Consulte Olá [propriedades de tipo de conjunto de dados do SQL Azure](#dataset) seção para obter lista de saudação de propriedades com suporte por este tipo de conjunto de dados.

**Uma atividade de cópia em um pipeline com origem de Blob e coletor SQL:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**SqlSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoSQL",
        "description": "Copy Activity",
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
            "type": "BlobSource",
            "blobColumnSeparators": ","
          },
          "sink": {
            "type": "SqlSink"
          }
        },
       "scheduler": {
          "frequency": "Hour",
          "interval": 1
        },
        "policy": {
          "concurrency": 1,
          "executionPriorityOrder": "OldestFirst",
          "retry": 0,
          "timeout": "01:00:00"
        }
      }
      ]
   }
}
```
Consulte Olá [coletor Sql](#sqlsink) seção e [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de saudação de propriedades com suporte do SqlSink e BlobSource.

## <a name="identity-columns-in-hello-target-database"></a>Colunas de identidade no banco de dados de destino Olá
Esta seção fornece um exemplo para copiar dados de uma tabela de origem sem uma tabela de destino identidade coluna tooa com uma coluna de identidade.

**Tabela de origem:**

```SQL
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Tabela de destino:**

```SQL
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```
Observe que essa tabela de destino Olá tem uma coluna de identidade.

**Definição de JSON do conjunto de dados de origem**

```JSON
{
    "name": "SampleSource",
    "properties": {
        "type": " SqlServerTable",
        "linkedServiceName": "TestIdentitySQL",
        "typeProperties": {
            "tableName": "SourceTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
        "policy": {}
    }
}
```
**Definição de JSON do conjunto de dados de destino**

```JSON
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "type": "AzureSqlTable",
        "linkedServiceName": "TestIdentitySQLSource",
        "typeProperties": {
            "tableName": "TargetTbl"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": false,
        "policy": {}
    }    
}
```

Observe que sua tabela de origem e de destino têm um esquema diferente (a de destino tem uma coluna adicional com identidade). Nesse cenário, você precisa toospecify **estrutura** propriedade na definição de conjunto de dados de destino hello, que não inclui a coluna de identidade de saudação.

## <a name="invoke-stored-procedure-from-sql-sink"></a>Invocar o procedimento armazenado do coletor SQL
Para obter um exemplo de como invocar um procedimento armazenado do coletor SQL em uma atividade de cópia de um pipeline, confira o artigo [Invoke stored procedure for SQL sink in copy activity](data-factory-invoke-stored-procedure-from-copy-activity.md) (Invocar procedimento armazenado para coletor SQL na atividade de cópia). 

## <a name="type-mapping-for-azure-sql-database"></a>Mapeamento de tipo do Banco de Dados SQL do Azure
Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:

1. Converter nativo tipos too.NET do tipo de origem
2. Converter do tipo de coletor de toonative de tipo .NET

Ao mover dados tooand do banco de dados do SQL Azure, hello mapeamentos a seguir são usados do tipo SQL de too.NET e vice-versa. mapeamento de saudação é igual a saudação mapeamento de tipo de dados do SQL Server do ADO.NET.

| Tipo de mecanismo do Banco de Dados do SQL Server | Tipo .NET Framework |
| --- | --- |
| bigint |Int64 |
| binário |Byte[] |
| bit |Booliano |
| char |String, Char[] |
| data |DateTime |
| DateTime |DateTime |
| datetime2 |DateTime |
| Datetimeoffset |Datetimeoffset |
| Decimal |Decimal |
| Atributo FILESTREAM (varbinary(max)) |Byte[] |
| Float |Duplo |
| imagem |Byte[] |
| int |Int32 |
| money |Decimal |
| nchar |String, Char[] |
| ntext |String, Char[] |
| numérico |Decimal |
| nvarchar |String, Char[] |
| real |Single |
| rowversion |Byte[] |
| smalldatetime |DateTime |
| smallint |Int16 |
| smallmoney |Decimal |
| sql_variant |Objeto * |
| texto |String, Char[] |
| tempo real |timespan |
| timestamp |Byte[] |
| tinyint |Byte |
| uniqueidentifier |Guid |
| varbinary |Byte[] |
| varchar |String, Char[] |
| xml |xml |

## <a name="map-source-toosink-columns"></a>Mapear colunas de toosink de origem
toolearn sobre mapeamento de colunas em toocolumns de conjunto de dados de origem no conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Cópia repetida
Ao copiar dados tooSQL banco de dados do servidor, atividade de cópia de saudação acrescenta a tabela de dados do coletor toohello por padrão. em vez disso, consulte tooperform um UPSERT [tooSqlSink gravação Repeatable](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artigo. 

Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais. No Azure Data Factory, você pode repetir a execução de uma fatia manualmente. Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha. Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada. Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
