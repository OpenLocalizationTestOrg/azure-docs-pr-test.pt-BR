---
title: aaaMove dados na tabela do Azure | Microsoft Docs
description: Saiba como toomove dados para/do armazenamento de tabela do Azure usando o Azure Data Factory.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 07b046b1-7884-4e57-a613-337292416319
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/22/2017
ms.author: jingwang
ms.openlocfilehash: 3dc3da6d88854674a9108b600534bc5d07575f15
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-table-using-azure-data-factory"></a>Mover tooand de dados de tabela do Azure usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de/para o armazenamento de tabela do Azure. Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação. 

Você pode copiar dados de qualquer fonte com suporte de dados armazenam tooAzure armazenamento de tabela ou de dados do armazenamento de tabela do Azure tooany suportada coletor armazenam. Para obter uma lista de repositórios de dados com suporte como origens ou Coletores de atividade de cópia hello, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. 

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados bidirecionalmente de um Armazenamento de Tabelas do Azure usando diferentes ferramentas/APIs.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir: 

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. 
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de um armazenamento de tabela do Azure, consulte [exemplos JSON](#json-examples) deste artigo. 

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAzure armazenamento de tabela: 

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Há dois tipos de serviços vinculados, você pode usar toolink uma fábrica de dados do Azure de tooan de armazenamento de BLOBs do Azure. São eles: o serviço vinculado **AzureStorage** e o serviço vinculado **AzureStorageSas**. Olá serviço vinculado do armazenamento do Azure fornece a fábrica de dados Olá com acesso global toohello armazenamento do Azure. Enquanto o hello Azure armazenamento SAS (assinatura de acesso compartilhado) vinculado serviço fornece a fábrica de dados Olá com acesso restrito/tempo-limite toohello armazenamento do Azure. Não há outras diferenças entre esses dois serviços vinculados. Escolha o serviço de saudação vinculado que atenda às suas necessidades. Olá seções a seguir fornecem mais detalhes sobre esses dois serviços vinculados.

[!INCLUDE [data-factory-azure-storage-linked-services](../../includes/data-factory-azure-storage-linked-services.md)]

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação. Olá **typeProperties** seção de conjunto de dados de saudação do tipo **AzureTable** tem Olá propriedades a seguir.

| Propriedade | Descrição | Obrigatório |
| --- | --- | --- |
| tableName |Nome da tabela de saudação na instância de banco de dados de tabela do Azure Olá que serviço vinculado refere-se a. |Sim. Quando um nome de tabela é especificado sem um azureTableSourceQuery, todos os registros da tabela de saudação são copiados toohello destino. Se um azureTableSourceQuery também for especificado, registros da tabela de saudação que atenda a consulta de saudação são copiados toohello destino. |

### <a name="schema-by-data-factory"></a>Esquema do Data Factory
Para repositórios de dados sem esquema como tabelas do Azure, Olá serviço da fábrica de dados infere o esquema Olá em uma saudação maneiras a seguir:

1. Se você especificar a estrutura de saudação de dados usando Olá **estrutura** propriedade na definição de conjunto de dados hello, Olá serviço da fábrica de dados honra essa estrutura como esquema de saudação. Nesse caso, se uma linha não contiver um valor de uma coluna, um valor nulo será fornecido para ele.
2. Se você não especificar a estrutura de saudação de dados usando Olá **estrutura** propriedade na definição de conjunto de dados hello, Data Factory infere o esquema de saudação usando a primeira linha de saudação nos dados de saudação. Nesse caso, se a primeira linha de saudação não contém um esquema completo hello, algumas colunas estão ausentes no resultado de saudação da operação de cópia.

Portanto, para fontes de dados sem esquema prática recomendada Olá é toospecify estrutura de saudação de dados usando Olá **estrutura** propriedade.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte Olá [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, conjuntos de dados de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade.

Propriedades disponíveis na seção de typeProperties Olá de atividade Olá Olá outro lado variam de acordo com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

**AzureTableSource** dá suporte a saudação propriedades typeProperties seção a seguir:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| AzureTableSourceQuery |Use dados de tooread Olá consulta personalizada. |Cadeia de caracteres de consulta de tabela do Azure. Consulte os exemplos na próxima seção, Olá. |Não. Quando um nome de tabela é especificado sem um azureTableSourceQuery, todos os registros da tabela de saudação são copiados toohello destino. Se um azureTableSourceQuery também for especificado, registros da tabela de saudação que atenda a consulta de saudação são copiados toohello destino. |
| azureTableSourceIgnoreTableNotFound |Indique se a exceção de Olá de assimilação da tabela não existe. |TRUE<br/>FALSE |Não |

### <a name="azuretablesourcequery-examples"></a>Exemplos do azureTableSourceQuery
Se a coluna Tabela do Azure é do tipo cadeia de caracteres:

```JSON
azureTableSourceQuery": "$$Text.Format('PartitionKey ge \\'{0:yyyyMMddHH00_0000}\\' and PartitionKey le \\'{0:yyyyMMddHH00_9999}\\'', SliceStart)"
```

Se a coluna Tabela do Azure é do tipo datetime:

```JSON
"azureTableSourceQuery": "$$Text.Format('DeploymentEndTime gt datetime\\'{0:yyyy-MM-ddTHH:mm:ssZ}\\' and DeploymentEndTime le datetime\\'{1:yyyy-MM-ddTHH:mm:ssZ}\\'', SliceStart, SliceEnd)"
```

**AzureTableSink** dá suporte a saudação propriedades typeProperties seção a seguir:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| azureTableDefaultPartitionKeyValue |Partição chave valor padrão que pode ser usado pelo coletor de saudação. |Um valor de cadeia de caracteres. |Não |
| azureTablePartitionKeyName |Especifique o nome da coluna Olá cujos valores são usados como chaves de partição. Se não especificado, AzureTableDefaultPartitionKeyValue será usado como chave de partição hello. |Um nome de coluna. |Não |
| azureTableRowKeyName |Especifique o nome da coluna Olá cujos valores de coluna são usados como chave de linha. Se não especificado, um GUID é usado para cada linha. |Um nome de coluna. |Não |
| azureTableInsertType |dados de tooinsert de modo de saudação na tabela do Azure.<br/><br/>Essa propriedade controla se as linhas existentes na tabela de saída de hello com correspondência de chaves de partição e de linha têm seus valores substituídos ou mesclados. <br/><br/>toolearn sobre como essas configurações (mesclagem e substituir) funcionam, consulte [inserir ou mesclar entidade](https://msdn.microsoft.com/library/azure/hh452241.aspx) e [inserir ou substituir entidade](https://msdn.microsoft.com/library/azure/hh452242.aspx) tópicos. <br/><br> Essa configuração se aplica no nível de linha hello, não os nível de tabela Olá, e nenhuma opção exclui linhas na tabela de saída de saudação que não existem na entrada hello. |mesclar (padrão)<br/>substituir |Não |
| writeBatchSize |Insere dados em Olá tabela do Azure quando Olá writeBatchSize ou writeBatchTimeout é atingido. |Inteiro (número de linhas) |Não (padrão: 10000) |
| writeBatchTimeout |Insere dados na Olá tabela do Azure quando Olá writeBatchSize ou writeBatchTimeout é atingido |timespan<br/><br/>Exemplo: "00:20:00" (20 minutos) |Não (valor de tempo limite padrão de cliente de toostorage padrão 90 segundos) |

### <a name="azuretablepartitionkeyname"></a>azureTablePartitionKeyName
Mapear uma coluna de destino do código-fonte coluna tooa usando a propriedade JSON do tradutor Olá antes que você pode usar a coluna de destino hello como Olá azureTablePartitionKeyName.

Em Olá exemplo a seguir, a coluna de origem DivisionID é mapeada toohello coluna de destino: DivisionID.  

```JSON
"translator": {
    "type": "TabularTranslator",
    "columnMappings": "DivisionID: DivisionID, FirstName: FirstName, LastName: LastName"
}
```
Olá DivisionID é especificado como chave de partição hello.

```JSON
"sink": {
    "type": "AzureTableSink",
    "azureTablePartitionKeyName": "DivisionID",
    "writeBatchSize": 100,
    "writeBatchTimeout": "01:00:00"
}
```
## <a name="json-examples"></a>Exemplos de JSON
Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Eles mostram como toocopy tooand de dados do armazenamento de tabela do Azure e banco de dados de Blob do Azure. No entanto, os dados podem ser copiados **diretamente** de qualquer um dos Olá fontes tooany de Coletores de saudação com suporte. Para obter mais informações, consulte a seção de hello "e formatos de armazenamentos de dados com suporte" em [mover dados usando a atividade de cópia](data-factory-data-movement-activities.md).

## <a name="example-copy-data-from-azure-table-tooazure-blob"></a>Exemplo: Copiar dados de tabela do Azure tooAzure Blob
Olá mostra de exemplo a seguir:

1. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabela e blob).
2. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureTable](#dataset-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [AzureTableSource](#activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia os dados pertencentes a partição padrão de toohello em um blob de tooa de tabela do Azure a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

**Serviço vinculado de armazenamento do Azure:**

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
O Azure Data Factory dá suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**. Para Olá primeiro, você especificar a cadeia de caracteres de conexão de saudação que inclui a chave da conta hello e hello mais recente, você especificar Olá Uri de assinatura de acesso compartilhado (SAS). Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.  

**Conjunto de dados de entrada da Tabela do Azure:**

exemplo Hello pressupõe que você tenha criado uma tabela "MyTable" na tabela do Azure.

Definindo "externo": "verdadeiro" informa serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```JSON
{
  "name": "AzureTableInput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

**Conjunto de dados de saída de Blob do Azure:**

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário da hora de início da saudação.

```JSON
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

**Atividade de cópia em um pipeline com AzureTableSource e BlobSink:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**AzureTableSource** e **coletor** tipo está definido muito**BlobSink**. consulta SQL Olá especificada com **AzureTableSourceQuery** propriedade seleciona dados da saudação da partição padrão de saudação toocopy cada hora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
        "start":"2014-06-01T18:00:00",
        "end":"2014-06-01T19:00:00",
        "description":"pipeline for copy activity",
        "activities":[  
            {
                "name": "AzureTabletoBlob",
                "description": "copy activity",
                "type": "Copy",
                "inputs": [
                      {
                        "name": "AzureTableInput"
                    }
                ],
                "outputs": [
                      {
                            "name": "AzureBlobOutput"
                      }
                ],
                "typeProperties": {
                      "source": {
                        "type": "AzureTableSource",
                        "AzureTableSourceQuery": "PartitionKey eq 'DefaultPartitionKey'"
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

## <a name="example-copy-data-from-azure-blob-tooazure-table"></a>Exemplo: Copiar dados de Blob do Azure tooAzure tabela
Olá mostra de exemplo a seguir:

1. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties) (usado para tabela e blob)
2. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureTable](#dataset-properties).
4. Olá [pipeline](data-factory-create-pipelines.md) com atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [AzureTableSink](#copy-activity-properties).

exemplo Hello copia dados de série de tempo de uma tabela do Azure de tooan de BLOBs do Azure por hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

**Serviço de armazenamento vinculado do Azure (para Tabela e Blob do Azure):**

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

O Azure Data Factory dá suporte a dois tipos de serviços vinculados do Armazenamento do Azure: **AzureStorage** e **AzureStorageSas**. Para Olá primeiro, você especificar a cadeia de caracteres de conexão de saudação que inclui a chave da conta hello e hello mais recente, você especificar Olá Uri de assinatura de acesso compartilhado (SAS). Confira a seção [Serviços vinculados](#linked-service-properties) para obter detalhes.

**Conjunto de dados de entrada de Blob do Azure:**

Os dados são coletados de um novo blob a cada hora (frequência: hora, intervalo: 1). Olá pasta caminho e nome de arquivo para blob Olá são avaliados dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa year, month e parte do dia da hora de início da saudação e nome do arquivo usa a parte de hora Olá Olá da hora de início. "externo": "verdadeira" configuração informa o serviço de fábrica de dados de Olá Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```JSON
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

**Conjunto de dados de saída de Tabela do Azure:**

exemplo Hello copiará a tabela de tooa de dados denominada "MyTable" na tabela do Azure. Criar uma tabela do Azure com hello mesmo número de colunas, conforme o esperado toocontain de arquivo CSV de Blob hello. Novas linhas são adicionadas a tabela de toohello a cada hora.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

**Atividade de cópia em um pipeline com BlobSource e AzureTableSink:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**BlobSource** e **coletor** tipo está definido muito**AzureTableSink**.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline with copy activity",
    "activities":[  
      {
        "name": "AzureBlobtoTable",
        "description": "Copy Activity",
        "type": "Copy",
        "inputs": [
          {
            "name": "AzureBlobInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureTableOutput"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "AzureTableSink",
            "writeBatchSize": 100,
            "writeBatchTimeout": "01:00:00"
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
## <a name="type-mapping-for-azure-table"></a>Mapeamento de tipo de Tabela do Azure
Conforme mencionado em Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, a atividade de cópia executa conversões de tipo automática tipos toosink de tipos de origem com hello abordagem em duas etapas a seguir.

1. Converter nativo tipos too.NET do tipo de origem
2. Converter do tipo de coletor de toonative de tipo .NET

Ao mover dados muito & da tabela do Azure, Olá após [mapeamentos definidos pelo serviço de tabela do Azure](https://msdn.microsoft.com/library/azure/dd179338.aspx) são usados com o tipo de too.NET de tipos do OData de tabela do Azure e vice-versa.

| Tipo de dados OData | Tipo .NET | Detalhes |
| --- | --- | --- |
| Edm.Binary |byte[] |Uma matriz de bytes de too64 KB. |
| Edm.Boolean |bool |Um valor booliano. |
| Edm.DateTime |DateTime |Um valor de 64 bits expressado como Tempo Universal Coordenado (UTC). Olá suporte para DateTime intervalo começa de 12:00 meia-noite de 1º de janeiro de 1601 D.C. (C.E.), UTC. intervalo de saudação termina em 31 de dezembro de 9999. |
| Edm.Double |double |Um valor de ponto flutuante de 64 bits. |
| Edm.Guid |Guid |Um identificador global exclusivo de 128 bits. |
| Edm.Int32 |Int32 |Um inteiro de 32 bits. |
| Edm.Int64 |Int64 |Um inteiro de 64 bits. |
| Edm.String |Cadeia de caracteres |Um valor codificado em UTF-16. Valores de cadeia de caracteres podem ser up too64 KB. |

### <a name="type-conversion-sample"></a>Exemplo de conversão de tipo
saudação de exemplo a seguir é copiar dados de uma tabela de tooAzure de BLOBs do Azure com conversões de tipo.

Suponha que o conjunto de dados de Blob hello está em formato CSV e contém três colunas. Um deles é uma coluna de data e hora com um formato de data e hora personalizado usando nomes abreviados de francês para o dia da semana hello.

Define o conjunto de dados de fonte de Blob de saudação da seguinte maneira juntamente com definições de tipo para colunas de saudação.

```JSON
{
    "name": " AzureBlobInput",
    "properties":
    {
         "structure":
          [
                { "name": "userid", "type": "Int64"},
                { "name": "name", "type": "String"},
                { "name": "lastlogindate", "type": "Datetime", "culture": "fr-fr", "format": "ddd-MM-YYYY"}
          ],
        "type": "AzureBlob",
        "linkedServiceName": "StorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/myfolder",
            "fileName":"myfile.csv",
            "format":
            {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        },
        "external": true,
        "availability":
        {
            "frequency": "Hour",
            "interval": 1,
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
Dado o mapeamento de tipo de saudação de too.NET de tipo de OData de tabela do Azure, você deve definir tabela Olá na tabela do Azure com hello esquema a seguir.

**Esquema da tabela do Azure:**

| Nome da coluna | Tipo |
| --- | --- |
| userid |Edm.Int64 |
| name |Edm.String |
| lastlogindate |Edm.DateTime |

Em seguida, defina o conjunto de dados de tabela do Azure Olá da seguinte maneira. Seção de "structure" toospecify com informações de tipo hello não é necessário porque as informações de tipo de saudação já estão especificadas em Olá subjacente de repositório de dados.

```JSON
{
  "name": "AzureTableOutput",
  "properties": {
    "type": "AzureTable",
    "linkedServiceName": "StorageLinkedService",
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

Nesse caso, a fábrica de dados automaticamente conversões de tipo incluindo o campo de data/hora de saudação com formato de data e hora personalizado hello usando a cultura de hello "fr-fr" quando a movimentação de dados de Blob tooAzure tabela.

> [!NOTE]
> colunas de toomap de toocolumns de conjunto de dados de origem do conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias maneiras, consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md).
