---
title: aaaMove dados para/de banco de dados do Azure Cosmos | Microsoft Docs
description: "Saiba como mover dados de/para a coleção Azure Cosmos DB usando o Azure Data Factory"
services: data-factory, cosmosdb
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: c9297b71-1bb4-4b29-ba3c-4cf1f5575fac
ms.service: multiple
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: bd23ce4e004a972ce6f3e4165cfdea4f0c18fecc
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-tooand-from-azure-cosmos-db-using-azure-data-factory"></a>Mover dados tooand do banco de dados do Cosmos do Azure usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia em dados do Azure Data Factory toomove de banco de dados do Azure Cosmos (API de documentos). Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação. 

Você pode copiar dados de qualquer fonte com suporte de dados armazenam tooAzure Cosmos banco de dados ou de dados do banco de dados do Azure Cosmos tooany suportada coletor armazenam. Para obter uma lista de repositórios de dados com suporte como origens ou Coletores de atividade de cópia hello, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. 

> [!IMPORTANT]
> O conector do Azure Cosmos DB dá suporte apenas à API do DocumentDB.

dados de toocopy como-é de/para arquivos JSON ou outra coleção Cosmos DB, consulte [documentos JSON de importação/exportação](#importexport-json-documents).

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados de/para o Azure Cosmos DB usando diferentes ferramentas/APIs.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir: 

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. 
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter exemplos com definições de JSON para entidades de fábrica de dados que são usados toocopy dados para/de banco de dados do Cosmos, consulte [exemplos JSON](#json-examples) deste artigo. 

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específicas tooCosmos banco de dados: 

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Olá, a tabela a seguir fornece uma descrição para o JSON de elementos específico tooAzure Cosmos DB vinculado de serviço.

| **Propriedade** | **Descrição** | **Obrigatório** |
| --- | --- | --- |
| type |propriedade de tipo Hello deve ser definida como: **DocumentDb** |Sim |
| connectionString |Especifique o banco de dados do banco de dados do Cosmos tooconnect tooAzure as informações necessárias. |Sim |

Exemplo:

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
Para obter uma lista completa das seções e propriedades disponíveis para definir conjuntos de dados, consulte toohello [criando conjuntos de dados](data-factory-create-datasets.md) artigo. Seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados (SQL Azure, Blob do Azure, Tabela do Azure etc.).

seção de typeProperties Olá é diferente para cada tipo de conjunto de dados e fornece informações sobre local de saudação de dados Olá no repositório de dados de saudação. Olá typeProperties seção de conjunto de dados de saudação do tipo **DocumentDbCollection** tem Olá propriedades a seguir.

| **Propriedade** | **Descrição** | **Obrigatório** |
| --- | --- | --- |
| collectionName |Nome da saudação coleção de documentos do banco de dados do Cosmos. |Sim |

Exemplo:

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
### <a name="schema-by-data-factory"></a>Esquema do Data Factory
Para repositórios de dados sem esquema, como o banco de dados do Azure Cosmos, Olá serviço da fábrica de dados infere o esquema Olá em uma saudação maneiras a seguir:  

1. Se você especificar a estrutura de saudação de dados usando Olá **estrutura** propriedade na definição de conjunto de dados hello, Olá serviço da fábrica de dados honra essa estrutura como esquema de saudação. Nesse caso, se uma linha não contiver um valor de uma coluna, um valor nulo será fornecido para ele.
2. Se você não especificar a estrutura Olá dos dados usando Olá **estrutura** propriedade na definição de conjunto de dados hello, Olá serviço da fábrica de dados infere o esquema de saudação usando a primeira linha de saudação nos dados de saudação. Nesse caso, se a primeira linha de saudação não contém um esquema completo hello, algumas colunas serão ausentes no resultado de saudação da operação de cópia.

Portanto, para fontes de dados sem esquema prática recomendada Olá é toospecify estrutura de saudação de dados usando Olá **estrutura** propriedade.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para a definição de atividades, consulte toohello [criar Pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e política, estão disponíveis para todos os tipos de atividades.

> [!NOTE]
> Hello atividade de cópia usa apenas uma entrada e produz apenas uma saída.

Propriedades disponíveis na seção de typeProperties Olá de atividade Olá Olá outro lado variam de acordo com cada tipo de atividade e, em caso de atividade de cópia que variam de acordo com os tipos de saudação de origens e coletores.

No caso de atividade de cópia quando a fonte é do tipo **DocumentDbCollectionSource** Olá propriedades a seguir está disponível em **typeProperties** seção:

| **Propriedade** | **Descrição** | **Valores permitidos** | **Obrigatório** |
| --- | --- | --- | --- |
| query |Especifica Olá consulta tooread dados. |Cadeia de consulta com suporte no Azure Cosmos DB. <br/><br/>Exemplo: `SELECT c.BusinessEntityID, c.PersonType, c.NameStyle, c.Title, c.Name.First AS FirstName, c.Name.Last AS LastName, c.Suffix, c.EmailPromotion FROM c WHERE c.ModifiedDate > \"2009-01-01T00:00:00\"` |Não <br/><br/>Se não for especificado, Olá instrução SQL executada:`select <columns defined in structure> from mycollection` |
| nestingSeparator |Caractere especial tooindicate que Olá documento está aninhado |Qualquer caractere. <br/><br/>O Azure Cosmos DB é um repositório NoSQL para documentos JSON, em que estruturas aninhadas são permitidas. A fábrica de dados do Azure permite que a hierarquia de toodenote de usuário por meio de nestingSeparator, que é "." em hello acima exemplos. Separador hello, atividade de cópia Olá irá gerar objeto de "Nome" hello com elementos de três filhos too"Name.First primeiro, intermediária e último, acordo", "Name.Middle" e ". Sobrenome" hello definição da tabela. |Não |

**DocumentDbCollectionSink** dá suporte a saudação propriedades a seguir:

| **Propriedade** | **Descrição** | **Valores permitidos** | **Obrigatório** |
| --- | --- | --- | --- |
| nestingSeparator |Um caractere especial em Olá fonte coluna Nome tooindicate que aninhada documento é necessário. <br/><br/>Por exemplo acima: `Name.First` na saída de hello tabela produz Olá estrutura JSON no documento de banco de dados do Cosmos Olá a seguir:<br/><br/>"Name": {<br/>    "First": "John"<br/>}, |Caractere usado tooseparate níveis de aninhamento.<br/><br/>O valor padrão é `.` (ponto). |Caractere usado tooseparate níveis de aninhamento. <br/><br/>O valor padrão é `.` (ponto). |
| writeBatchSize |Número de paralelo solicitações tooAzure documentos de toocreate do serviço de banco de dados do Cosmos.<br/><br/>Você pode ajustar o desempenho de saudação ao copiar dados de banco de dados do Cosmos usando essa propriedade. Você pode esperar um desempenho melhor quando você aumenta writeBatchSize porque mais solicitações paralelas tooCosmos banco de dados são enviados. No entanto, você precisará tooavoid limitação que pode gerar a mensagem de saudação do erro: "Solicitação de taxa for grande".<br/><br/>A limitação é decida por uma série de fatores, incluindo o tamanho dos documentos, o número de termos incluídos, a política de indexação da coleção de destino, etc. Para operações de cópia, você pode usar uma saudação de toohave de coleção (por exemplo, S3) melhor taxa de transferência mais disponível (2.500 solicitação unidades/segundo). |Número inteiro |Não (padrão: 5) |
| writeBatchTimeout |Tempo de espera para Olá operação toocomplete antes de expirar. |timespan<br/><br/> Exemplo: "00:30:00" (30 minutos). |Não |

## <a name="importexport-json-documents"></a>Importar/Exportar documentos JSON
Usando esse conector do Cosmos DB, você pode facilmente

* Importar documentos JSON de várias fontes para o Cosmos DB, incluindo Blobs do Azure, Azure Data Lake, Sistema de Arquivos local ou outros repositórios com base em arquivos com suporte pelo Azure Data Factory.
* Exportar documentos JSON da coleção do Cosmos DB para vários repositórios com base em arquivo.
* Migrar dados entre duas coleções do Cosmos DB no estado em que se encontram.

Copiar de tais independentes de esquema tooachieve, 
* Ao usar o Assistente para cópia, marque Olá **"Exportar como-é tooJSON arquivos ou uma coleção de banco de dados do Cosmos"** opção.
* Quando usando a edição de JSON, não especifique seção de "structure" hello no conjunto de dados do banco de dados do Cosmos nem a propriedade "nestingSeparator" no banco de dados do Cosmos fonte/coletor na atividade de cópia. tooimport de / tooJSON arquivos de exportação, no conjunto de dados de repositório de arquivo hello especificar tipo de formato como "JsonFormat", "filePattern" de configuração e ignorar as configurações de formato Olá rest, consulte [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format) seção em detalhes.

## <a name="json-examples"></a>Exemplos de JSON
Olá, exemplos a seguir fornecem as definições de JSON de exemplo que você pode usar toocreate um pipeline usando [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md) ou [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md) ou [Azure PowerShell](data-factory-copy-activity-tutorial-using-powershell.md). Eles mostram como toocopy tooand de dados do banco de dados do Azure Cosmos e armazenamento de BLOBs do Azure. No entanto, os dados podem ser copiados **diretamente** de qualquer um dos Olá fontes tooany de Coletores Olá mencionado [aqui](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando hello atividade de cópia na fábrica de dados do Azure.

## <a name="example-copy-data-from-azure-cosmos-db-tooazure-blob"></a>Exemplo: Dados de cópia do banco de dados do Azure Cosmos tooAzure Blob
exemplo Hello abaixo mostra:

1. Um serviço vinculado do tipo [DocumentDB](#linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [DocumentDbCollection](#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
5. Um [pipeline](data-factory-create-pipelines.md) com Atividade de cópia que usa [DocumentDbCollectionSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados no banco de dados do Azure Cosmos tooAzure Blob. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

**Serviço vinculado do Azure Cosmos DB:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
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
**Conjunto de dados de entrada do Azure DocumentDB:**

exemplo Hello pressupõe que você tenha uma coleção denominada **pessoa** em um banco de dados do banco de dados do Azure Cosmos.

Definindo "externo": "true" e especificando externalData informações da política de saudação do Azure Data Factory do serviço tabela Olá toohello externo fábrica de dados e não são produzidos por uma atividade na fábrica de dados hello.

```JSON
{
  "name": "PersonCosmosDbTable",
  "properties": {
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```

**Conjunto de dados de saída de Blob do Azure:**

Dados são copiado tooa novo blob a cada hora com caminho Olá blob Olá refletindo Olá data e hora específicas com granularidade de hora.

```JSON
{
  "name": "PersonBlobTableOut",
  "properties": {
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
Documento JSON de exemplo no hello coleção pessoa em um banco de dados do banco de dados do Cosmos:

```JSON
{
  "PersonId": 2,
  "Name": {
    "First": "Jane",
    "Middle": "",
    "Last": "Doe"
  }
}
```
O Cosmos DB dá suporte a consultas de documentos usando um SQL como sintaxe nos documentos JSON hierárquicos.

Exemplo: 

```sql
SELECT Person.PersonId, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person
```

a seguir Olá pipeline copia dados da saudação coleta de pessoa Olá tooan de banco de dados do banco de dados do Azure Cosmos BLOBs do Azure. Como parte da saudação de atividade de cópia Olá conjuntos de dados de entrada e saídos foi especificados.  

```JSON
{
  "name": "DocDbToBlobPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "DocumentDbCollectionSource",
            "query": "SELECT Person.Id, Person.Name.First AS FirstName, Person.Name.Middle as MiddleName, Person.Name.Last AS LastName FROM Person",
            "nestingSeparator": "."
          },
          "sink": {
            "type": "BlobSink",
            "blobWriterAddHeader": true,
            "writeBatchSize": 1000,
            "writeBatchTimeout": "00:00:59"
          }
        },
        "inputs": [
          {
            "name": "PersonCosmosDbTable"
          }
        ],
        "outputs": [
          {
            "name": "PersonBlobTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromDocDbToBlob"
      }
    ],
    "start": "2015-04-01T00:00:00Z",
    "end": "2015-04-02T00:00:00Z"
  }
}
```
## <a name="example-copy-data-from-azure-blob-tooazure-cosmos-db"></a>Exemplo: Copiar dados de Blob do Azure tooAzure Cosmos DB 
exemplo Hello abaixo mostra:

1. Um serviço vinculado do tipo [DocumentDB](#azure-documentdb-linked-service-properties).
2. Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
3. Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
4. Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [DocumentDbCollection](#azure-documentdb-dataset-type-properties).
5. O [pipeline](data-factory-create-pipelines.md) com a Atividade de cópia que usa [BlobSource](data-factory-azure-blob-connector.md#copy-activity-properties) e [DocumentDbCollectionSink](#azure-documentdb-copy-activity-type-properties).

exemplo Hello copia dados de blob do Azure tooAzure Cosmos DB. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

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
**Serviço vinculado do Azure Cosmos DB:**

```JSON
{
  "name": "CosmosDbLinkedService",
  "properties": {
    "type": "DocumentDb",
    "typeProperties": {
      "connectionString": "AccountEndpoint=<EndpointUrl>;AccountKey=<AccessKey>;Database=<Database>"
    }
  }
}
```
**Conjunto de dados de entrada de Blob do Azure:**

```JSON
{
  "name": "PersonBlobTableIn",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "FirstName",
        "type": "String"
      },
      {
        "name": "MiddleName",
        "type": "String"
      },
      {
        "name": "LastName",
        "type": "String"
      }
    ],
    "type": "AzureBlob",
    "linkedServiceName": "StorageLinkedService",
    "typeProperties": {
      "fileName": "input.csv",
      "folderPath": "docdb",
      "format": {
        "type": "TextFormat",
        "columnDelimiter": ",",
        "nullValue": "NULL"
      }
    },
    "external": true,
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
**Conjunto de dados de saída do Azure Cosmos DB:**

exemplo Hello copia a coleção de tooa de dados denominada "Pessoa".

```JSON
{
  "name": "PersonCosmosDbTableOut",
  "properties": {
    "structure": [
      {
        "name": "Id",
        "type": "Int"
      },
      {
        "name": "Name.First",
        "type": "String"
      },
      {
        "name": "Name.Middle",
        "type": "String"
      },
      {
        "name": "Name.Last",
        "type": "String"
      }
    ],
    "type": "DocumentDbCollection",
    "linkedServiceName": "CosmosDbLinkedService",
    "typeProperties": {
      "collectionName": "Person"
    },
    "availability": {
      "frequency": "Day",
      "interval": 1
    }
  }
}
```
a seguir Olá pipeline copia dados de Blob do Azure toohello coleta de pessoa Olá Cosmos DB. Como parte da saudação de atividade de cópia Olá conjuntos de dados de entrada e saídos foi especificados.

```JSON
{
  "name": "BlobToDocDbPipeline",
  "properties": {
    "activities": [
      {
        "type": "Copy",
        "typeProperties": {
          "source": {
            "type": "BlobSource"
          },
          "sink": {
            "type": "DocumentDbCollectionSink",
            "nestingSeparator": ".",
            "writeBatchSize": 2,
            "writeBatchTimeout": "00:00:00"
          }
          "translator": {
              "type": "TabularTranslator",
              "ColumnMappings": "FirstName: Name.First, MiddleName: Name.Middle, LastName: Name.Last, BusinessEntityID: BusinessEntityID, PersonType: PersonType, NameStyle: NameStyle, title: aaaTitle, Suffix: Suffix, EmailPromotion: EmailPromotion, rowguid: rowguid, ModifiedDate: ModifiedDate"
          }
        },
        "inputs": [
          {
            "name": "PersonBlobTableIn"
          }
        ],
        "outputs": [
          {
            "name": "PersonCosmosDbTableOut"
          }
        ],
        "policy": {
          "concurrency": 1
        },
        "name": "CopyFromBlobToDocDb"
      }
    ],
    "start": "2015-04-14T00:00:00Z",
    "end": "2015-04-15T00:00:00Z"
  }
}
```
Se a entrada de blob de exemplo hello como

```
1,John,,Doe
```
Olá, em seguida, a saída que será JSON no banco de dados do Cosmos como:

```JSON
{
  "Id": 1,
  "Name": {
    "First": "John",
    "Middle": null,
    "Last": "Doe"
  },
  "id": "a5e8595c-62ec-4554-a118-3940f4ff70b6"
}
```
O Azure Cosmos DB é um repositório NoSQL para documentos JSON, em que estruturas aninhadas são permitidas. A fábrica de dados do Azure permite que a hierarquia de toodenote de usuário por meio de **nestingSeparator**, que é "." neste exemplo. Separador hello, atividade de cópia Olá irá gerar objeto de "Nome" hello com elementos de três filhos too"Name.First primeiro, intermediária e último, acordo", "Name.Middle" e ". Sobrenome" hello definição da tabela.

## <a name="appendix"></a>Apêndice
1. **Pergunta:** Olá a atualização de suporte a atividade de cópia de registros existentes?

    **Resposta:** Não.
2. **Pergunta:** como faz uma nova tentativa de uma cópia tooAzure Cosmos DB para tratar já copiados registros?

    **Resposta:** se registros têm um campo "ID" e a operação de cópia Olá tenta tooinsert um registro com hello mesmo ID de operação de cópia hello gera um erro.  
3. **Pergunta:** o Data Factory dá suporte ao [intervalo ou particionamento de dados com base em hash](../documentdb/documentdb-partition-data.md)?

    **Resposta:** Não.
4. **Pergunta:** posso especificar mais de uma coleção do Azure Cosmos DB para uma tabela?

    **Resposta:** Não. Somente uma coleção pode ser especificada no momento.

## <a name="performance-and-tuning"></a>Desempenho e Ajuste
Consulte [guia de ajuste e desempenho de atividade de cópia](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) no Azure Data Factory e toooptimize de várias formas-lo.
