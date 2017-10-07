---
title: "índice de tooSearch aaaPush dados usando a fábrica de dados | Microsoft Docs"
description: "Saiba mais sobre como dados de toopush tooAzure índice de pesquisa usando o Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: f8d46e1e-5c37-4408-80fb-c54be532a4ab
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/04/2017
ms.author: jingwang
ms.openlocfilehash: f2d973d0a2c24d6448e2d59e37e24503aa433018
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="push-data-tooan-azure-search-index-by-using-azure-data-factory"></a>Enviar por push o índice de pesquisa do Azure tooan dados por meio do Azure Data Factory
Este artigo descreve como os dados de toopush do toouse hello atividade de cópia de dados de origem com suporte armazenam tooAzure índice de pesquisa. Armazenamentos de dados de origem com suporte são listados na coluna de origem de saudação do hello [suporte para origens e coletores](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Este artigo aproveita Olá [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia e combinações de repositório de dados com suporte.

## <a name="enabling-connectivity"></a>Habilitando a conectividade
tooallow serviço da fábrica de dados se conectar o repositório de dados do local de tooan, instalar o Gateway de gerenciamento de dados em seu ambiente local. Você pode instalar o gateway em Olá mesma máquina que hospeda os dados de origem Olá armazenar ou em um tooavoid máquina separada competição por recursos com dados saudação repositório.

Gateway de gerenciamento de dados se conecta a serviços de toocloud de fontes de dados no local de forma segura e gerenciada. Consulte o artigo [Mover dados entre local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) para obter detalhes sobre o Gateway de Gerenciamento de Dados.

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que envia dados de um índice de pesquisa do código-fonte dados repositório tooAzure usando APIs/ferramentas diferentes.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Consulte [Tutorial: criar um pipeline usando o Assistente para cópia de](data-factory-copy-data-wizard-tutorial.md) para uma rápida explicação passo a passo sobre como criar um pipeline usando o Assistente para cópia de dados da saudação.

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Consulte [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para instruções passo a passo toocreate um pipeline com uma atividade de cópia. 

Se você usar ferramentas de saudação ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir: 

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello. 
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída. 

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usa ferramentas/APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação.  Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy índice de pesquisa de tooAzure de dados, consulte [exemplo JSON: copiar dados de índice de pesquisa do local do SQL Server tooAzure](#json-example-copy-data-from-on-premises-sql-server-to-azure-search-index) deste artigo. 

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAzure índice de pesquisa:

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado

Olá a tabela a seguir fornece descrições dos elementos JSON de serviço de pesquisa do Azure vinculada toohello específico.

| Propriedade | Descrição | Obrigatório |
| -------- | ----------- | -------- |
| type | propriedade de tipo Hello deve ser definida como: **AzureSearch**. | Sim |
| url | URL de saudação serviço de pesquisa do Azure. | Sim |
| chave | Chave de administração de saudação serviço de pesquisa do Azure. | Sim |

## <a name="dataset-properties"></a>Propriedades do conjunto de dados

Para obter uma lista completa de seções e propriedades que estão disponíveis para definir conjuntos de dados, consulte Olá [criando conjuntos de dados](data-factory-create-datasets.md) artigo. As seções como structure, availability e policy de um conjunto de dados JSON são similares para todos os tipos de conjunto de dados. Olá **typeProperties** seção é diferente para cada tipo de conjunto de dados. Olá typeProperties seção um conjunto de dados do tipo hello **AzureSearchIndex** tem Olá propriedades a seguir:

| Propriedade | Descrição | Obrigatório |
| -------- | ----------- | -------- |
| type | propriedade do tipo Hello deve ser definida muito**AzureSearchIndex**.| Sim |
| indexName | Nome do índice de pesquisa do Azure hello. Fábrica de dados não cria o índice de saudação. Olá índice deve existir na pesquisa do Azure. | Sim |


## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa de seções e propriedades que estão disponíveis para a definição de atividades, consulte Olá [criar pipelines](data-factory-create-pipelines.md) artigo. As propriedades, como nome, descrição, tabelas de entrada e saída, e diversas políticas, estão disponíveis para todos os tipos de atividade. Por outro lado, as propriedades disponíveis na seção de typeProperties Olá variam com cada tipo de atividade. Para a atividade de cópia, eles variam dependendo Olá tipos de fontes e coletores.

Para a atividade de cópia, quando o coletor de saudação é do tipo de saudação **AzureSearchIndexSink**, Olá propriedades a seguir está disponível na seção de typeProperties:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| -------- | ----------- | -------------- | -------- |
| WriteBehavior | Especifica se toomerge ou substituição quando um documento já existe no índice de saudação. Consulte Olá [WriteBehavior propriedade](#writebehavior-property).| Merge (padrão)<br/>Carregar| Não |
| WriteBatchSize | Carrega dados no índice de pesquisa do Azure hello quando o tamanho do buffer de saudação atingir writeBatchSize. Consulte Olá [WriteBatchSize propriedade](#writebatchsize-property) para obter detalhes. | 1 too1, 000. O valor padrão é 1000. | Não |

### <a name="writebehavior-property"></a>Propriedade WriteBehavior
Upsert do AzureSearchSink ao gravar dados. Em outras palavras, ao escrever um documento, se a chave de documento hello já existe no índice de pesquisa do Azure hello, pesquisa do Azure atualiza o documento de saudação existente em vez de gerar uma exceção de conflito.

Olá AzureSearchSink fornece Olá após dois comportamentos upsert (usando AzureSearch SDK):

- **Mesclar**: combinar todas as colunas de saudação em novo documento de saudação com hello existente a um. Para colunas com valor nulo em novo documento de hello, Olá valor Olá existente de um é preservado.
- **Carregar**: substitui o documento novo Olá Olá existente. Para colunas não especificadas no documento novo hello, o valor de saudação é definido toonull se há um valor não nulo no documento existente hello, ou não.

comportamento padrão de saudação é **mesclar**.

### <a name="writebatchsize-property"></a>Propriedade WriteBatchSize
O serviço de Azure Search oferece suporte a escrever documentos como um lote. Um lote pode conter 1 too1, ações, 000. Uma ação lida com uma operação de carregamento/mesclagem documento tooperform hello.

### <a name="data-type-support"></a>Suporte ao tipo de dados
Olá tabela a seguir especifica se um tipo de dados de pesquisa do Azure tem suporte ou não.

| Tipo de dados do Azure Search | Suporte no coletor do Azure Search |
| ---------------------- | ------------------------------ |
| Cadeia de caracteres | S |
| Int32 | S |
| Int64 | S |
| Duplo | S |
| Booliano | S |
| DataTimeOffset | S |
| Matriz de cadeia de caracteres | N |
| GeographyPoint | N |

## <a name="json-example-copy-data-from-on-premises-sql-server-tooazure-search-index"></a>Exemplo JSON: copiar dados de índice de pesquisa de tooAzure do local do SQL Server

Olá mostra de exemplo a seguir:

1.  Um serviço vinculado do tipo [AzureSearch](#linked-service-properties).
2.  Um serviço vinculado do tipo [OnPremisesSqlServer](data-factory-sqlserver-connector.md#linked-service-properties).
3.  Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [SqlServerTable](data-factory-sqlserver-connector.md#dataset-properties).
4.  Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureSearchIndex](#dataset-properties).
4.  Um [pipeline](data-factory-create-pipelines.md) com a atividade de cópia que usa [SqlSource](data-factory-sqlserver-connector.md#copy-activity-properties) e [AzureSearchIndexSink](#copy-activity-properties).

exemplo Hello copia dados de série temporal de um índice de pesquisa do Azure tooan banco de dados do local do SQL Server por hora. propriedades JSON Olá usadas neste exemplo são descritas nas seções a seguir exemplos de saudação.

Como uma primeira etapa, configure o gateway de gerenciamento de dados de saudação em seu computador local. Olá instruções são Olá [mover dados entre locais de local e nuvem](data-factory-move-data-between-onprem-and-cloud.md) artigo.

**Serviço vinculado ao Azure Search:**

```JSON
{
    "name": "AzureSearchLinkedService",
    "properties": {
        "type": "AzureSearch",
        "typeProperties": {
            "url": "https://<service>.search.windows.net",
            "key": "<AdminKey>"
        }
    }
}
```

**Serviço vinculado do SQL Server**

```JSON
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

**Conjunto de dados de entrada do SQL Server**

exemplo Hello supõe que você criou uma tabela "MyTable" no SQL Server e contém uma coluna chamada "timestampcolumn" para dados de série temporal. Você pode consultar em várias tabelas em Olá mesmo usando um único conjunto de dados, mas uma única tabela de banco de dados deve ser usado para typeProperty de tableName de saudação do dataset.

Definindo "externo": "verdadeiro" informa o serviço de fábrica de dados Olá conjunto de dados é externo toohello fábrica de dados e não é produzido por uma atividade na fábrica de dados hello.

```JSON
{
  "name": "SqlServerDataset",
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

**Conjunto de dados de saída do Azure Search:**

Olá exemplo copia dados tooan Azure índice de pesquisa denominada **produtos**. Fábrica de dados não cria o índice de saudação. Olá tootest de exemplo, crie um índice com este nome. Criar o índice de pesquisa do Azure Olá com hello mesmo número de colunas como Olá conjunto de dados de entrada. São adicionadas novas entradas toohello índice de pesquisa do Azure a cada hora.

```JSON
{
    "name": "AzureSearchIndexDataset",
    "properties": {
        "type": "AzureSearchIndex",
        "linkedServiceName": "AzureSearchLinkedService",
        "typeProperties" : {
            "indexName": "products",
        },
        "availability": {
            "frequency": "Minute",
            "interval": 15
        }
   }
}
```

**Atividade de cópia em um pipeline com origem SQL e coletor de Índice do Azure Search:**

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**SqlSource** e **coletor** tipo está definido muito**AzureSearchIndexSink**. consulta SQL Olá especificada para Olá **SqlReaderQuery** propriedade seleciona dados Olá Olá após toocopy de hora.

```JSON
{  
    "name":"SamplePipeline",
    "properties":{  
    "start":"2014-06-01T18:00:00",
    "end":"2014-06-01T19:00:00",
    "description":"pipeline for copy activity",
    "activities":[  
      {
        "name": "SqlServertoAzureSearchIndex",
        "description": "copy activity",
        "type": "Copy",
        "inputs": [
          {
            "name": " SqlServerInput"
          }
        ],
        "outputs": [
          {
            "name": "AzureSearchIndexDataset"
          }
        ],
        "typeProperties": {
          "source": {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('select * from MyTable where timestampcolumn >= \\'{0:yyyy-MM-dd HH:mm}\\' AND timestampcolumn < \\'{1:yyyy-MM-dd HH:mm}\\'', WindowStart, WindowEnd)"
          },
          "sink": {
            "type": "AzureSearchIndexSink"
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

Se você estiver copiando dados de um armazenamento de dados de nuvem para o Azure Search, a propriedade `executionLocation` será necessária. Olá, trecho JSON a seguir mostra alterações Olá necessária na atividade de cópia `typeProperties` como exemplo. Verifique a seção [Copiar dados entre armazenamentos de dados de nuvem](data-factory-data-movement-activities.md#global) para obter mais detalhes e valores com suporte.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```


## <a name="copy-from-a-cloud-source"></a>Copiar de uma origem de nuvem
Se você estiver copiando dados de um armazenamento de dados de nuvem para o Azure Search, a propriedade `executionLocation` será necessária. Olá, trecho JSON a seguir mostra alterações Olá necessária na atividade de cópia `typeProperties` como exemplo. Verifique a seção [Copiar dados entre armazenamentos de dados de nuvem](data-factory-data-movement-activities.md#global) para obter mais detalhes e valores com suporte.

```JSON
"typeProperties": {
  "source": {
    "type": "BlobSource"
  },
  "sink": {
    "type": "AzureSearchIndexSink"
  },
  "executionLocation": "West US"
}
```

Você também pode mapear colunas de origem toocolumns de conjunto de dados do conjunto de coletor de dados na definição de atividade de cópia de saudação. Para obter detalhes, confira [Mapear colunas de conjunto de dados no Azure Data Factory](data-factory-map-columns.md).

## <a name="performance-and-tuning"></a>Desempenho e ajuste  
Consulte Olá [atividade de cópia guia de desempenho e ajuste](data-factory-copy-activity-performance.md) toolearn sobre a chave de fatores que afetam o desempenho de movimento de dados (Copiar atividade) e toooptimize de várias formas-lo.

## <a name="next-steps"></a>Próximas etapas
Consulte Olá artigos a seguir:

* [Tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md) para obter instruções passo a passo para criação de um pipeline com uma Atividade de cópia.
