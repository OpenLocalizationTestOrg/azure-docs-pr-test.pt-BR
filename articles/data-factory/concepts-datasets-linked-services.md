---
title: "Conjuntos de dados e serviços vinculados no Azure Data Factory | Microsoft Docs"
description: "Saiba mais sobre conjuntos de dados e serviços vinculados no Data Factory. Os serviços vinculados vinculam computação/armazenamentos de dados a um data factory. Os conjuntos de dados representam os dados de entrada/saída."
services: data-factory
documentationcenter: 
author: sharonlo101
manager: jhubbard
editor: spelluru
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: 
ms.date: 01/22/2018
ms.author: shlo
ms.openlocfilehash: bfc95588378466fe1e83bcc4e899eca6b66b358a
ms.sourcegitcommit: 9cc3d9b9c36e4c973dd9c9028361af1ec5d29910
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/23/2018
---
# <a name="datasets-and-linked-services-in-azure-data-factory"></a>Conjuntos de dados e serviços vinculados no Azure Data Factory 
> [!div class="op_single_selector" title1="Select the version of Data Factory service you are using:"]
> * [Versão 1 – já disponível](v1/data-factory-create-datasets.md)
> * [Versão 2 – Versão prévia](concepts-datasets-linked-services.md)

Este artigo descreve o que são conjuntos de dados, como eles são definidos no formato JSON e como são usados em pipelines V2 do Azure Data Factory. 

> [!NOTE]
> Este artigo aplica-se à versão 2 do Data Factory, que está atualmente em versão prévia. Se você estiver usando a versão 1 do serviço Data Factory, que está em GA (disponibilidade geral), consulte [Conjuntos de dados no Data Factory V1](v1/data-factory-create-datasets.md).

Se estiver conhecendo o Azure Data Factory agora, consulte [Introdução ao Azure Data Factory](introduction.md) para obter uma visão geral. 

## <a name="overview"></a>Visão geral
Uma fábrica de dados pode ter um ou mais pipelines. Um **pipeline** é um agrupamento lógico de **atividades** que juntas executam uma tarefa. As atividades em um pipeline definem ações para executar em seus dados. Por exemplo, você poderá usar uma atividade de cópia para copiar os dados de um SQL Server local para um armazenamento de Blobs do Azure. Em seguida, poderá usar uma atividade do Hive que executa um script Hive em um cluster HDInsight do Azure a fim de processar dados do armazenamento de Blobs para gerar dados de saída. Por fim, poderá usar uma segunda atividade de cópia para copiar os dados de saída para o SQL Data Warehouse do Azure, no qual as soluções de relatório de BI (business intelligence) são criadas. Para obter mais informações sobre pipelines e atividades, consulte [Pipelines e atividades](concepts-pipelines-activities.md) no Azure Data Factory.

Por outro lado, um **conjunto de dados** é uma exibição nomeada de dados que simplesmente aponta ou faz referência aos dados que você deseja usar em suas **atividades** como entradas e saídas. Conjuntos de dados identificam dados em armazenamentos de dados diferentes, como tabelas, arquivos, pastas e documentos. Por exemplo, um conjunto de dados de Blob do Azure especifica o contêiner de blobs e a pasta no armazenamento de Blobs dos quais a atividade deve ler os dados.

Antes de criar um conjunto de dados, você deve criar um **serviço vinculado** para vincular seu armazenamento de dados com o data factory. Serviços vinculados são como cadeias de conexão, que definem as informações de conexão necessárias para o Data Factory para se conectar a recursos externos. Pense dessa maneira: o conjunto de dados representa a estrutura dos dados nos armazenamentos de dados vinculados e o serviço vinculado define a conexão à fonte de dados. Por exemplo, um serviço vinculado do Armazenamento do Azure vincula uma conta de armazenamento ao data factory. Um conjunto de dados de Blob do Azure representa o contêiner de blob e a pasta naquela conta de armazenamento do Azure que contém os blobs de entrada a serem processados.

Veja abaixo um cenário de exemplo. Para copiar dados do armazenamento de Blobs para um banco de dados SQL, crie dois serviços vinculados: Armazenamento do Azure e Banco de Dados SQL do Azure. Em seguida, crie dois conjuntos de dados: o conjunto de dados de Blob do Azure (que se refere ao serviço vinculado do Armazenamento do Azure) e o conjunto de dados de Tabela do SQL do Azure (que se refere ao serviço vinculado do Banco de Dados SQL do Azure). Os serviços vinculados do Armazenamento do Azure e do Banco de Dados SQL do Azure contêm cadeias de conexão que o Data Factory usa em tempo de execução para se conectar ao Armazenamento do Azure e ao Banco de Dados SQL do Azure, respectivamente. O conjunto de dados de Blob do Azure especifica o contêiner de blobs e a pasta de blobs que contém os blobs de entrada no armazenamento de Blobs. O conjunto de dados de Tabela do SQL do Azure especifica a tabela do SQL no banco de dados SQL para o qual os dados serão copiados.

O seguinte diagrama mostra a relação entre pipeline, atividade, conjunto de dados e serviço vinculado no Data Factory:

![Relação entre pipeline, atividade e conjunto de dados, serviços vinculados](media/concepts-datasets-linked-services/relationship-between-data-factory-entities.png)

## <a name="linked-service-json"></a>JOSN de serviço vinculado
Um serviço vinculado no Data Factory é definido no formato JSON da seguinte maneira:

```json
{
    "name": "<Name of the linked service>",
    "properties": {
        "type": "<Type of the linked service>",
        "typeProperties": {
              "<data store or compute-specific type properties>"
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

A tabela a seguir descreve as propriedades no JSON acima:

Propriedade | DESCRIÇÃO | Obrigatório |
-------- | ----------- | -------- |
Nome | Nome do serviço vinculado. Consulte [Azure Data Factory – Regras de nomenclatura](naming-rules.md). |  sim |
Tipo | Tipo de serviço vinculado. Por exemplo: AzureStorage (armazenamento de dados) ou AzureBatch (computação). Consulte a descrição de typeProperties. | sim |
typeProperties | As propriedades de tipo são diferentes para cada armazenamento de dados ou de computação. <br/><br/> Para os tipos de armazenamento de dados suportados e suas propriedades de tipo, consulte a tabela [tipo de conjunto de dados](#dataset-type) neste artigo. Navegue até o artigo de conector do armazenamento de dados para saber mais sobre as propriedades de tipo específicas para um armazenamento de dados. <br/><br/> Para os tipos de computação suportados e suas propriedades de tipo, consulte [serviços vinculados de computação](compute-linked-services.md). | sim |
connectVia | O [Integration Runtime](concepts-integration-runtime.md) a ser usado para se conectar ao armazenamento de dados. Você pode usar o Integration Runtime do Azure ou o Integration Runtime auto-hospedado (se o armazenamento de dados estiver localizado em uma rede privada). Se não for especificado, ele usa o Integration Runtime padrão do Azure. | Não 

## <a name="linked-service-example"></a>Exemplo de serviço vinculado
O seguinte serviço vinculado é um serviço vinculado de Armazenamento do Azure. Observe que o tipo é definido como AzureStorage. As propriedades de tipo para o serviço vinculado do Armazenamento do Azure incluem uma cadeia de conexão. O serviço de Data Factory usa essa cadeia de conexão para se conectar ao armazenamento de dados em tempo de execução. 

```json
{
    "name": "AzureStorageLinkedService",
    "properties": {
        "type": "AzureStorage",
        "typeProperties": {
            "connectionString": {
                "type": "SecureString",
                "value": "DefaultEndpointsProtocol=https;AccountName=<accountname>;AccountKey=<accountkey>"
            }
        },
        "connectVia": {
            "referenceName": "<name of Integration Runtime>",
            "type": "IntegrationRuntimeReference"
        }
    }
}
```

## <a name="dataset-json"></a>Conjunto de dados do JSON
Um conjunto de dados no Data Factory é definido no formato JSON da seguinte maneira:

```json
{
    "name": "<name of dataset>",
    "properties": {
        "type": "<type of dataset: AzureBlob, AzureSql etc...>",
        "linkedServiceName": {
                "referenceName": "<name of linked service>",
                 "type": "LinkedServiceReference",
        },
        "structure": [
            {
                "name": "<Name of the column>",
                "type": "<Name of the type>"
            }
        ],
        "typeProperties": {
            "<type specific property>": "<value>",
            "<type specific property 2>": "<value 2>",
        }
    }
}

```
A tabela a seguir descreve as propriedades no JSON acima:

Propriedade | DESCRIÇÃO | Obrigatório |
-------- | ----------- | -------- |
Nome | Nome do conjunto de dados. Consulte [Azure Data Factory – Regras de nomenclatura](naming-rules.md). |  sim |
Tipo | Tipo de conjunto de dados. Especifique um dos tipos com suporte no Data Factory (por exemplo: AzureBlob, AzureSqlTable). <br/><br/>Para obter detalhes, consulte [Tipos de conjunto de dados](#dataset-types). | sim |
estrutura | Esquema do conjunto de dados. Para obter detalhes, consulte [Estrutura de conjunto de dados](#dataset-structure). | Não  |
typeProperties | As propriedades de tipo são diferentes para cada tipo (por exemplo: Blob do Azure, tabela do SQL Azure). Para obter detalhes sobre os tipos com suporte e suas propriedades, consulte [Tipo de conjunto de dados](#dataset-type). | sim |

## <a name="dataset-example"></a>Exemplo de conjunto de dados
No exemplo a seguir, o conjunto de dados representa uma tabela chamada MyTable em um banco de dados SQL.

```json
{
    "name": "DatasetSample",
    "properties": {
        "type": "AzureSqlTable",
        "linkedServiceName": {
                "referenceName": "MyAzureSqlLinkedService",
                 "type": "LinkedServiceReference",
        },
        "typeProperties":
        {
            "tableName": "MyTable"
        },
    }
}

```
Observe os seguintes pontos:

- O tipo foi definido como AzureSqlTable.
- A propriedade de tipo tableName (específica do tipo AzureSqlTable) foi definida como MyTable.
- linkedServiceName se refere a um serviço vinculado do tipo AzureSqlDatabase, que é definido no seguinte trecho de JSON.

## <a name="dataset-type"></a>Tipo de conjunto de dados
Há muitos tipos diferentes de conjuntos de dados, dependendo do armazenamento de dados que você usa. Consulte a tabela a seguir para obter uma lista de armazenamentos de dados com suporte pelo Data Factory. Clique em um armazenamento de dados para saber como criar um serviço vinculado e um conjunto de dados para esse armazenamento de dados.

[!INCLUDE [data-factory-v2-supported-data-stores](../../includes/data-factory-v2-supported-data-stores.md)]

No exemplo na seção anterior, o tipo do conjunto de dados é definido como **AzureSqlTable**. Da mesma forma, para um conjunto de dados de Blob do Azure, o tipo do conjunto de dados é definido como **AzureBlob**, conforme mostrado no seguinte JSON:

```json
{
    "name": "AzureBlobInput",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": {
                "referenceName": "MyAzureStorageLinkedService",
                 "type": "LinkedServiceReference",
        }, 
 
        "typeProperties": {
            "fileName": "input.log",
            "folderPath": "adfgetstarted/inputdata",
            "format": {
                "type": "TextFormat",
                "columnDelimiter": ","
            }
        }
    }
}
```
## <a name="dataset-structure"></a>Estrutura do conjunto de dados
A seção **estrutura** é opcional. Ela define o esquema do conjunto de dados contendo uma coleção de nomes e tipos de dados de colunas. Use a seção de estrutura para fornecer informações de tipo que são usadas para converter tipos e mapear colunas da origem para o destino. No seguinte exemplo, o conjunto de dados tem três colunas: timestamp, projectname e pageviews. Elas são do tipo String, String e Decimal, respectivamente.

```json
[
    { "name": "timestamp", "type": "String"},
    { "name": "projectname", "type": "String"},
    { "name": "pageviews", "type": "Decimal"}
]
```

Cada coluna da seção Estrutura contém as seguintes propriedades:

Propriedade | DESCRIÇÃO | Obrigatório
-------- | ----------- | --------
Nome | Nome da coluna. | sim
Tipo | Tipo de dados da coluna. | Não 
culture | Cultura baseada em .NET a ser usada quando o tipo é um tipo .NET `Datetime` ou `Datetimeoffset`. O padrão é `en-us`. | Não 
formato | O formato de cadeia de caracteres a ser usado quando o tipo é um tipo .NET `Datetime` ou `Datetimeoffset`. | Não 

As diretrizes a seguir ajudam você a determinar quando incluir informações de estrutura e o que incluir na seção **estrutura**.

- **Para fontes de dados estruturadas**, especifique a seção de estrutura somente se desejar mapear colunas de origem para colunas do coletor; além disso, seus nomes não são os mesmos. Esse tipo de fonte de dados estruturada armazena informações de esquema de dados e de tipo juntamente com os próprios dados. Exemplos de fontes de dados estruturadas incluem SQL Server, Oracle e Banco de Dados SQL do Azure.<br/><br/>Como as informações de tipo já estão disponíveis para fontes de dados estruturadas, não inclua informações de tipo quando incluir a seção de estrutura.
- **Para o esquema em fontes de dados de leitura (especificamente o armazenamento de Blobs)**, você pode optar por armazenar os dados sem armazenar nenhuma informação de tipo ou de esquema juntamente com os dados. Para esses tipos de fontes de dados, inclua a estrutura quando desejar mapear as colunas de origem para as colunas do coletor. Também inclua a estrutura quando o conjunto de dados for uma entrada para uma atividade de cópia e os tipos de dados do conjunto de dados de origem precisarem ser convertidos em tipos nativos para o coletor.<br/><br/> O Data Factory dá suporte aos seguintes valores para fornecer informações de tipo na estrutura: `Int16, Int32, Int64, Single, Double, Decimal, Byte[], Boolean, String, Guid, Datetime, Datetimeoffset, and Timespan`. 

Saiba mais sobre como o data factory mapeia dados de origem até o coletor e quando especificar informações de estrutura em [Esquema e mapeamento de tipo]( copy-activity-schema-and-type-mapping.md).

## <a name="create-datasets"></a>Criar conjuntos de dados
Você pode criar conjuntos de dados usando uma dessas ferramentas ou SDKs: [API do .NET](quickstart-create-data-factory-dot-net.md), [PowerShell](quickstart-create-data-factory-powershell.md), [API REST](quickstart-create-data-factory-rest-api.md), modelo do Azure Resource Manager e Portal do Azure

## <a name="v1-vs-v2-datasets"></a>Conjuntos de dados V1 versus V2

Aqui estão algumas diferenças entre conjuntos de dados v1 e v2 do Data Factory: 

- Não há suporte para a propriedade externa no v2. Ela é substituída por um [gatilho](concepts-pipeline-execution-triggers.md).
- Não há suporte para as propriedades de disponibilidade e política no V2. A hora de início de um pipeline depende de [gatilhos](concepts-pipeline-execution-triggers.md).
- Não há suporte para conjuntos de dados com escopo (conjuntos de dados definidos em um pipeline) no V2. 

## <a name="next-steps"></a>Próximas etapas
Consulte os seguintes tutoriais para obter instruções passo a passo para criar pipelines e conjuntos de dados usando uma destas ferramentas ou SDKs. 

- [Início rápido: criar um data factory usando o .NET](quickstart-create-data-factory-dot-net.md)
- [Início rápido: criar um data factory usando o PowerShell](quickstart-create-data-factory-powershell.md)
- [Início rápido: criar um data factory usando a API REST](quickstart-create-data-factory-rest-api.md)
- Início rápido: criar um data factory usando o Portal do Azure
