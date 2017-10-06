---
title: aaaMove tooand de dados do SQL Server | Microsoft Docs
description: "Saiba mais sobre como toomove dados do SQL Server/para o banco de dados que é local ou em uma VM do Azure usando o Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 864ece28-93b5-4309-9873-b095bbe6fedd
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jingwang
ms.openlocfilehash: f0cccf56a670e62ec893d75052a81eb26d562050
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-sql-server-on-premises-or-on-iaas-azure-vm-using-azure-data-factory"></a>Mover dados tooand do SQL Server local ou na IaaS (VM do Azure) usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de/para um banco de dados do SQL Server local. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação. 

## <a name="supported-scenarios"></a>Cenários com suporte
Você pode copiar dados **de um banco de dados do SQL Server** toohello repositórios de dados a seguir:

[!INCLUDE [data-factory-supported-sink](../../includes/data-factory-supported-sinks.md)]

Você pode copiar dados de saudação armazenamentos de dados a seguir **banco de dados do SQL Server tooa**:

[!INCLUDE [data-factory-supported-sources](../../includes/data-factory-supported-sources.md)]

## <a name="supported-sql-server-versions"></a>Versões do SQL Server com suporte
Esse suporte de conector do SQL Server copiar dados do / toohello versões de instância hospedada no local ou na IaaS do Azure usando a autenticação do SQL e a autenticação do Windows a seguir: SQL Server 2016, SQL Server 2014, SQL Server 2012, SQL Server 2008 R2, SQL Server 2008, SQL Server 2005

## <a name="enabling-connectivity"></a>Habilitando a conectividade
conceitos de saudação e as etapas necessárias para conectar-se com o SQL Server hospedado no local ou no Azure IaaS VMs (uma infraestrutura como serviço) são Olá mesmo. Em ambos os casos, você precisa toouse Data Management Gateway para conectividade.

Consulte [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) toolearn artigo sobre o Gateway de gerenciamento de dados e instruções passo a passo sobre como configurar o gateway de saudação. Configurar uma instância de gateway é um pré-requisito para a conexão com o SQL Server.

Embora você possa instalar o gateway Olá mesmo no local instância da máquina ou nuvem de VM como Olá do SQL Server para obter melhor desempenho, é recomendável instalá-los em computadores separados. Ter Olá gateway e o SQL Server em máquinas separadas reduz a contenção de recursos.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com atividade de cópia que move dados de/para um banco de dados SQL Server local por meio de ferramentas/APIs diferentes.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir: 

1. Criar uma **data factory**. Um data factory pode conter um ou mais pipelines. 
2. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica. Por exemplo, se você estiver copiando dados de um banco de dados de SQL Server tooan armazenamento de BLOBs do Azure, você criar duas toolink de serviços vinculados seu banco de dados do SQL Server e a fábrica de dados de tooyour de conta de armazenamento do Azure. Para propriedades de serviço vinculado que banco de dados de servidor tooSQL específicos, consulte [vinculado propriedades do serviço](#linked-service-properties) seção. 
3. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. No exemplo hello mencionado na última etapa do hello, você pode criar uma tabela do dataset toospecify Olá SQL no banco de dados do SQL Server que contém os dados de entrada hello. E, criar outro contêiner de blob do conjunto de dados toospecify hello e pasta Olá que contém dados saudação copiados da saudação banco de dados do SQL Server. Para propriedades de conjunto de dados que são específicos tooSQL banco de dados do servidor, consulte [propriedades de conjunto de dados](#dataset-properties) seção.
4. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. Exemplo hello mencionado anteriormente, você usar SqlSource como uma origem e BlobSink como um coletor de atividade de cópia de saudação. Da mesma forma, se você está copiando do armazenamento de BLOBs do Azure tooSQL banco de dados do servidor, use BlobSource e SqlSink na atividade de cópia de saudação. Para propriedades de atividade de cópia que específico tooSQL banco de dados do servidor, consulte [copiar as propriedades de atividade](#copy-activity-properties) seção. Para obter detalhes sobre como toouse um repositório de dados como uma origem ou um coletor, clique em Olá link na seção anterior de saudação para seu armazenamento de dados. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um banco de dados do SQL Server local, consulte [exemplos JSON](#json-examples-for-copying-data-from-and-to-sql-server) deste artigo. 

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooSQL Server: 

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Criar um serviço vinculado do tipo **OnPremisesSqlServer** toolink uma fábrica de dados tooa de banco de dados do local do SQL Server. Olá a tabela a seguir fornece uma descrição para o serviço vinculado do SQL Server do JSON elementos tooon local específico.

Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooSQL serviço do servidor vinculado.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **OnPremisesSqlServer**. |Sim |
| connectionString |Especifica informações de connectionString necessárias tooconnect toohello no SQL Server banco de dados local usando a autenticação do Windows ou autenticação do SQL. |Sim |
| gatewayName |Nome do gateway Olá Olá serviço da fábrica de dados deve usar o banco de dados do tooconnect toohello no local do SQL Server. |Sim |
| Nome de Usuário |Especifique o nome de usuário se você estiver usando a Autenticação do Windows. Exemplo: **domainname\\username**. |Não |
| Senha |Especifique a senha da conta de usuário de saudação especificado para nome de usuário de saudação. |Não |

Você pode criptografar credenciais usando Olá **New-AzureRmDataFactoryEncryptValue** cmdlet e usá-los na cadeia de caracteres de conexão hello, conforme mostrado no exemplo a seguir de saudação (**EncryptedCredential** propriedade):  

```JSON
"connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=True;EncryptedCredential=<encrypted credential>",
```

### <a name="samples"></a>Exemplos
**JSON para usar Autenticação SQL**

```json
{
    "name": "MyOnPremisesSQLDB",
    "properties":
    {
        "type": "OnPremisesSqlServer",
        "typeProperties": {
            "connectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=False;User ID=<username>;Password=<password>;",
            "gatewayName": "<gateway name>"
        }
    }
}
```
**JSON para usar Autenticação Windows**

Gateway de gerenciamento de dados representará Olá especificado usuário conta tooconnect toohello no SQL Server banco de dados local. 

```json
{
     "Name": " MyOnPremisesSQLDB",
     "Properties":
     {
         "type": "OnPremisesSqlServer",
         "typeProperties": {
             "ConnectionString": "Data Source=<servername>;Initial Catalog=MarketingCampaigns;Integrated Security=True;",
             "username": "<domain\\username>",
             "password": "<password>",
             "gatewayName": "<gateway name>"
        }
     }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Exemplos de hello, você usou um conjunto de dados do tipo **SqlServerTable** toorepresent uma tabela em um banco de dados do SQL Server.  

Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. Seções como estrutura, disponibilidade e política de um conjunto de dados JSON são semelhantes para todos os tipos de conjunto de dados (SQL Server, blob do Azure, tabela do Azure, etc.).

seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação. Olá **typeProperties** seção de conjunto de dados de saudação do tipo **SqlServerTable** tem Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação ou exibição na instância de banco de dados do SQL Server Olá que serviço vinculado refere-se a. |Sim |

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Se você estiver movendo dados de um banco de dados do SQL Server, você defina o tipo de fonte de saudação na atividade de cópia de saudação muito**SqlSource**. Da mesma forma, se você estiver movendo o banco de dados do SQL Server data tooa, você definir o tipo de coletor Olá na atividade de cópia de saudação muito**SqlSink**. Esta seção fornece uma lista das propriedades com suporte de SqlSource e SqlSink.

Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.

> [!NOTE]
> Hello atividade de cópia usa apenas uma entrada e produz apenas uma saída.

Por outro lado, as propriedades disponíveis na seção typeProperties hello atividade Olá variam com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

### <a name="sqlsource"></a>SqlSource
Quando a fonte em uma atividade de cópia é do tipo **SqlSource**, Olá propriedades a seguir está disponível em **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| SqlReaderQuery |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta SQL. Por exemplo: select * from MyTable. Pode fazer referência a várias tabelas de banco de dados de saudação referenciado pelo conjunto de dados de entrada hello. Se não for especificado, Olá instrução SQL executada: selecione MyTable. |Não |
| sqlReaderStoredProcedureName |Nome da saudação procedimento armazenado que lê dados da tabela de origem hello. |Nome da saudação de procedimento armazenado. Olá a última instrução de SQL deve ser uma instrução SELECT no procedimento armazenado de saudação. |Não |
| storedProcedureParameters |Parâmetros de saudação de procedimento armazenado. |Pares de nome/valor. Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação. |Não |

Se hello **sqlReaderQuery** é especificada para Olá SqlSource, hello atividade de cópia executa esta consulta em relação aos dados de Olá Olá banco de dados do SQL Server fonte tooget.

Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros).

Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de Olá definidas na seção de estrutura hello são usada toobuild toorun uma consulta select contra Olá banco de dados do SQL Server. Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.

> [!NOTE]
> Quando você usa **sqlReaderStoredProcedureName**, você ainda precisa toospecify um valor para Olá **tableName** propriedade no conjunto de dados Olá JSON. Contudo, não há nenhuma validação executada nessa tabela.

### <a name="sqlsink"></a>SqlSink
**SqlSink** dá suporte a saudação propriedades a seguir:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| writeBatchTimeout |Tempo de espera para Olá toocomplete de operação de inserção de lote antes de expirar. |timespan<br/><br/> Exemplo: "00:30:00" (30 minutos). |Não |
| writeBatchSize |Insere dados na tabela do SQL hello quando o tamanho do buffer de saudação atingir writeBatchSize. |Inteiro (número de linhas) |Não (padrão: 10000) |
| sqlWriterCleanupScript |Especifique a consulta para a atividade de cópia tooexecute, de modo que os dados de uma fatia específica é limpa. Para obter mais informações, consulte a seção [Cópia repetida](#repeatable-copy). |Uma instrução de consulta. |Não |
| sliceIdentifierColumnName |Especifique o nome de coluna para a atividade de cópia toofill com identificador de fatia gerado automaticamente, que é usado tooclean os dados de uma fatia específica quando executada novamente. Para obter mais informações, consulte a seção [Cópia repetida](#repeatable-copy). |Nome de uma coluna com tipo de dados de binário (32). |Não |
| sqlWriterStoredProcedureName |Nome do hello procedimento armazenado dados upserts (atualizações/inserções) na tabela de destino de saudação. |Nome da saudação de procedimento armazenado. |Não |
| storedProcedureParameters |Parâmetros de saudação de procedimento armazenado. |Pares de nome/valor. Nomes e o uso de maiusculas e minúsculas dos parâmetros devem corresponder a nomes de saudação e uso de maiusculas e minúsculas dos parâmetros de procedimento armazenado de saudação. |Não |
| sqlWriterTableType |Especifique toobe de nome de tipo de tabela usado no procedimento armazenado de saudação. Atividade de cópia disponibiliza dados Olá movidos em uma tabela temporária com esse tipo de tabela. Código do procedimento armazenado, em seguida, pode mesclar dados de saudação sejam copiados com os dados existentes. |Um nome de tipo de tabela. |Não |


## <a name="json-examples-for-copying-data-from-and-toosql-server"></a>Exemplos JSON para copiar dados do e tooSQL Server
Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Olá seguintes exemplos mostram como toocopy tooand de dados do SQL Server e o armazenamento de BLOBs do Azure. No entanto, os dados podem ser copiados **diretamente** de qualquer uma das fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.     

## <a name="example-copy-data-from-sql-server-tooazure-blob"></a>Exemplo: Copiar dados do SQL Server tooAzure Blob
Olá mostra de exemplo a seguir:

1. Um serviço vinculado do tipo [OnPremisesSqlServer](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [SqlServerTable](#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [SqlSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados de série temporal de um tooan de tabela do SQL Server BLOBs do Azure a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação. Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Serviço vinculado do SQL Server**
```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
**Serviço vinculado do armazenamento de Blob do Azure**

```json
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
**Conjunto de dados de entrada do SQL Server**

exemplo Hello supõe que você criou uma tabela "MyTable" no SQL Server e contém uma coluna chamada "timestampcolumn" para dados de série temporal. Você pode consultar em várias tabelas em Olá mesmo usando um único conjunto de dados, mas uma única tabela de banco de dados deve ser usado para typeProperty de tableName de saudação do dataset.

Definindo "externo": "verdadeiro" informa o serviço de fábrica de dados Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```json
{
  "name": "SqlServerInput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**Conjunto de dados de saída de Blob do Azure**

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```json
{
  "name": "AzureBlobOutput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
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
**Pipeline com Atividade de cópia**

pipeline de saudação contém uma atividade de cópia que esteja configurado toouse esses conjuntos de dados de entrada e saídos e toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlSource** e **coletor** tipo está definido muito**BlobSink**. consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.

```json
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2016-06-01T18:00:00",
    "end":"2016-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoBlob",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
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
Neste exemplo, **sqlReaderQuery** é especificado para Olá SqlSource. Hello atividade de cópia executa esta consulta Olá dados do banco de dados do SQL Server origem tooget hello. Como alternativa, você pode especificar um procedimento armazenado especificando Olá **sqlReaderStoredProcedureName** e **storedProcedureParameters** (se hello procedimento armazenado usa parâmetros). Olá sqlReaderQuery pode fazer referência a várias tabelas no banco de dados de saudação referenciado pelo conjunto de dados de entrada hello. Ele não é limitado tooonly Olá definido como Olá typeProperty de tableName do conjunto de dados.

Se você não especificar sqlReaderQuery ou sqlReaderStoredProcedureName, colunas de Olá definidas na seção de estrutura hello são usada toobuild toorun uma consulta select contra Olá banco de dados do SQL Server. Se definição de conjunto de dados de saudação não tem estrutura Olá, todas as colunas da tabela de hello estão selecionadas.

Consulte Olá [fonte Sql](#sqlsource) seção e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties) para lista de saudação de propriedades com suporte SqlSource e BlobSink.

## <a name="example-copy-data-from-azure-blob-toosql-server"></a>Exemplo: Copiar dados de Blob do Azure tooSQL Server
Olá mostra de exemplo a seguir:

1. Olá vinculado de serviço do tipo [OnPremisesSqlServer](#linked-service-properties).
2. Olá vinculado de serviço do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
5. Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [SqlSink](#sql-server-copy-activity-type-properties).

exemplo Hello copia dados de série de tempo de uma tabela do SQL Server tooa BLOBs do Azure a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

**Serviço vinculado do SQL Server**

```json
{
  "Name": "SqlServerLinkedService",
  "properties": {
    "type": "OnPremisesSqlServer",
    "typeProperties": {
      "connectionString": "Data Source=<servername>;Initial Catalog=<databasename>;Integrated Security=False;User ID=<username>;Password=<password>;",
      "gatewayName": "<gatewayname>"
    }
  }
}
```
**Serviço vinculado do armazenamento de Blob do Azure**

```json
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
**Conjunto de dados de entrada de Blob do Azure**

Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1). Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início. "externo": "verdadeira" configuração informa o serviço de fábrica de dados de Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```json
{
  "name": "AzureBlobInput",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "mycontainer/myfolder/yearno={Year}/monthno={Month}/dayno={Day}",
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
**Conjunto de dados de saída do SQL Server**

exemplo Hello copiará a tabela de tooa de dados denominada "MyTable" no SQL Server. Criar tabela Olá no SQL Server com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello. Novas linhas são adicionadas a tabela de toohello a cada hora.

```json
{
  "name": "SqlServerOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlServerLinkedService",
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
**Pipeline com Atividade de cópia**

pipeline de saudação contém uma atividade de cópia que esteja configurado toouse esses conjuntos de dados de entrada e saídos e toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**SqlSink**.

```json
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
            "name": " SqlServerOutput "
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

## <a name="troubleshooting-connection-issues"></a>Solucionar problemas de conexão
1. Configure as conexões remotas de tooaccept do SQL Server. Inicie o **SQL Server Management Studio**, clique com o botão direito do mouse em **servidor** e clique em **Propriedades**. Selecione **conexões** na lista de saudação e seleção **server do permitir conexões remotas toohello**.

    ![Habilitar conexões remotas](./media/data-factory-sqlserver-connector/AllowRemoteConnections.png)

    Consulte [configurar o acesso remoto de saudação opção de configuração do servidor](https://msdn.microsoft.com/library/ms191464.aspx) para obter etapas detalhadas.
2. Inicie o **SQL Server Configuration Manager**(Gerenciador de Configuração do SQL Server). Expanda **configuração de rede do SQL Server** para Olá instância você deseja e selecione **protocolos para MSSQLSERVER**. Você deve ver os protocolos no painel direito de saudação. Habilite o TCP/IP clicando com o botão direito do mouse em **TCP/IP** e clicando em **Habilitar**.

    ![Habilitar TCP/IP](./media/data-factory-sqlserver-connector/EnableTCPProptocol.png)

    Veja [Habilitar ou Desabilitar um Protocolo de Rede do Servidor](https://msdn.microsoft.com/library/ms191294.aspx) para ver detalhes e formas alternativas de habilitar um protocolo TCP/IP.
3. No hello mesma janela, clique duas vezes em **TCP/IP** toolaunch **propriedades de TCP/IP** janela.
4. Alternar toohello **endereços IP** guia. Role para baixo toosee **IPAll** seção. Anote hello * * porta TCP * * (o padrão é **1433**).
5. Criar um **regra de Firewall do Windows de saudação** no hello máquina tooallow tráfego de entrada por essa porta.  
6. **Verifique se a conexão**: tooconnect toohello SQL Server usando o nome totalmente qualificado, use o SQL Server Management Studio em uma máquina diferente. Por exemplo: “<machine><domain>.corp<company>.com,1433”.

   > [!IMPORTANT]

   > Consulte [mover dados entre fontes locais e na nuvem de saudação com Data Management Gateway](data-factory-move-data-between-onprem-and-cloud.md) para obter informações detalhadas.
   >
   > Consulte [Solucionar problemas de gateway](data-factory-data-management-gateway.md#troubleshooting-gateway-issues) para ver dicas sobre como solucionar os problemas relacionados à conexão/gateway.
   >
   >


## <a name="identity-columns-in-hello-target-database"></a>Colunas de identidade no banco de dados de destino Olá
Esta seção fornece um exemplo que copia dados de uma tabela de origem com nenhuma tabela de destino identidade coluna tooa com uma coluna de identidade.

**Tabela de origem:**

```sql
create table dbo.SourceTbl
(
       name varchar(100),
       age int
)
```
**Tabela de destino:**

```sql
create table dbo.TargetTbl
(
       identifier int identity(1,1),
       name varchar(100),
       age int
)
```

Observe que essa tabela de destino Olá tem uma coluna de identidade.

**Definição de JSON do conjunto de dados de origem**

```json
{
    "name": "SampleSource",
    "properties": {
        "published": false,
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

```json
{
    "name": "SampleTarget",
    "properties": {
        "structure": [
            { "name": "name" },
            { "name": "age" }
        ],
        "published": false,
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

## <a name="type-mapping-for-sql-server"></a>Mapeamento de tipo para o SQL Server
Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, hello atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem 2 etapas a seguir:

1. Converter nativo tipos too.NET do tipo de origem
2. Converter do tipo de coletor de toonative de tipo .NET

Quando a movimentação de dados muito & do SQL server, Olá mapeamentos a seguir são usados do tipo SQL de too.NET e vice-versa.

mapeamento de saudação é igual a saudação mapeamento de tipo de dados do SQL Server do ADO.NET.

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

## <a name="mapping-source-toosink-columns"></a>Mapeamento de colunas da fonte de toosink
colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="repeatable-copy"></a>Cópia repetida
Ao copiar dados tooSQL banco de dados do servidor, atividade de cópia de saudação acrescenta a tabela de dados do coletor toohello por padrão. em vez disso, consulte tooperform um UPSERT [tooSqlSink gravação Repeatable](data-factory-repeatable-copy.md#repeatable-write-to-sqlsink) artigo. 

Ao copiar dados de armazenamentos de dados relacional, manter a capacidade de repetição em mente tooavoid resultados não intencionais. No Azure Data Factory, você pode repetir a execução de uma fatia manualmente. Você também pode configurar a política de repetição para um conjunto de dados de modo que uma fatia seja executada novamente quando ocorrer uma falha. Quando uma fatia é executado novamente em qualquer modo, você precisa toomake-se de que Olá os mesmos dados é lido como não importa quantas vezes uma fatia é executada. Confira [Leitura repetida de fontes relacionais](data-factory-repeatable-copy.md#repeatable-read-from-relational-sources).

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
