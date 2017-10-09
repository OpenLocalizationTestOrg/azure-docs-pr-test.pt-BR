---
title: "dados de aaaMove do serviço de armazenamento simples Amazon usando a fábrica de dados | Microsoft Docs"
description: "Saiba mais sobre como dados toomove do serviço de armazenamento simples Amazon (S3) por meio do Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.assetid: 636d3179-eba8-4841-bcb4-3563f6822a26
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8a8cd2845fd1de74413bd0372f3aabfb4817549b
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-from-amazon-simple-storage-service-by-using-azure-data-factory"></a>Mover dados do Amazon Simple Storage Service usando o Azure Data Factory
Este artigo explica como toouse hello atividade de cópia de dados do Azure Data Factory toomove do serviço de armazenamento simples Amazon (S3). Ele se baseia no hello [atividades de movimentação de dados](data-factory-data-movement-activities.md) artigo, que apresenta uma visão geral de movimentação de dados com a atividade de cópia de saudação.

Você pode copiar dados de repositório de dados do Amazon S3 tooany suportada coletor. Para obter uma lista de dados de repositórios de suporte como coletores pela atividade de cópia Olá, consulte Olá [suporte para armazenamentos de dados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) tabela. Fábrica de dados atualmente suporta apenas mover os dados do Amazon S3 tooother armazenamentos de dados, mas não movendo os dados de outros dados armazena tooAmazon S3.

## <a name="required-permissions"></a>Permissões necessárias
toocopy dados do Amazon S3, certifique-se de ter recebido Olá as seguintes permissões:

* `s3:GetObject` e `s3:GetObjectVersion` para operações de objeto do Amazon S3
* `s3:ListBucket` para operações de bucket do Amazon S3. Se você estiver usando o Assistente para cópia de fábrica de dados, de saudação `s3:ListAllMyBuckets` também é necessária.

Para obter detalhes sobre a lista completa de saudação do Amazon S3 permissões, consulte [especificando permissões em uma política de](http://docs.aws.amazon.com/AmazonS3/latest/dev/using-with-s3-actions.html).

## <a name="getting-started"></a>Introdução
Você pode criar um pipeline com uma atividade de cópia que mova dados de uma origem do Amazon S3 usando diferentes ferramentas ou APIs.

toocreate de maneira mais fácil de saudação um pipeline é Olá toouse **Assistente para cópia de**. Para obter uma explicação rápida, confira [Tutorial: Create a pipeline using Copy Wizard](data-factory-copy-data-wizard-tutorial.md) (Tutorial: criar um pipeline usando o Assistente de Cópia).

Você também pode usar o hello ferramentas toocreate um pipeline a seguir: **portal do Azure**, **Visual Studio**, **Azure PowerShell**, **modelo do Gerenciador de recursos do Azure** , **API .NET**, e **API REST**. Para obter instruções passo a passo toocreate um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).

Se você usar ferramentas ou APIs, você pode executar Olá etapas toocreate um pipeline que move o armazenamento de dados do coletor tooa do repositório de dados de uma fonte de dados a seguir:

1. Criar **serviços vinculados** toolink dados de entrada e saída repositórios tooyour dados fábrica.
2. Criar **conjuntos de dados** toorepresent de entrada e saída de operação de cópia de dados para hello.
3. Criar um **pipeline** com uma atividade de cópia que usa um conjunto de dados como uma entrada e um conjunto de dados como uma saída.

Quando você usa o Assistente de saudação, definições de JSON para essas entidades da fábrica de dados (serviços vinculados, conjuntos de dados e pipeline de saudação) são criadas automaticamente para você. Quando você usar ferramentas ou APIs (exceto API .NET), você define essas entidades da fábrica de dados usando o formato JSON de saudação. Para obter um exemplo com definições de JSON para entidades de fábrica de dados que são usados toocopy dados de um repositório de dados do Amazon S3, consulte Olá [exemplo JSON: copiar dados do Amazon S3 tooAzure Blob](#json-example-copy-data-from-amazon-s3-to-azure-blob) deste artigo.

> [!NOTE]
> Para obter detalhes sobre os formatos de arquivo e de compactação com suporte para uma atividade de cópia, consulte [Formatos de arquivo e de compactação no Azure Data Factory](data-factory-supported-file-and-compression-formats.md).

Olá seções a seguir fornece detalhes sobre as propriedades JSON que são usadas toodefine Data Factory entidades específica tooAmazon S3.

## <a name="linked-service-properties"></a>Propriedades do serviço vinculado
Um serviço vinculado vincula uma fábrica de dados de tooa de repositório de dados. Criar um serviço vinculado do tipo **AwsAccessKey** toolink tooyour fábrica de dados do repositório de seus dados do Amazon S3. Olá, a tabela a seguir fornece o serviço de descrição de JSON de elementos específico tooAmazon S3 (AwsAccessKey) vinculado.

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| accessKeyID |ID da chave de acesso ao segredo hello. |string |Sim |
| secretAccessKey |chave de acesso ao segredo Olá em si. |Cadeia de caracteres secreta criptografada |Sim |

Aqui está um exemplo:

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

## <a name="dataset-properties"></a>Propriedades do conjunto de dados
toospecify toorepresent um conjunto de dados de entrada dados no armazenamento de BLOBs do Azure, defina a propriedade tipo saudação do conjunto de dados de saudação muito**AmazonS3**. Saudação de conjunto **linkedServiceName** serviço vinculado de propriedade de nome de toohello Olá dataset de saudação Amazon S3. Para obter uma lista completa das seções e propriedades disponíveis para definir os conjuntos de dados, confira [Criando conjuntos de dados](data-factory-create-datasets.md). 

As seções como structure, availability e policy são similares para todos os tipos de conjunto de dados (como banco de dados SQL Azure, Blob do Azure, Tabela do Azure etc.). Olá **typeProperties** seção é diferente para cada tipo de conjunto de dados e fornece informações sobre o local de saudação de dados Olá no repositório de dados de saudação. Olá **typeProperties** seção um conjunto de dados do tipo **AmazonS3** (que inclui o conjunto de dados Olá Amazon S3) tem Olá propriedades a seguir:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| bucketName |nome de bucket Olá S3. |Cadeia de caracteres |Sim |
| chave |chave do objeto Olá S3. |Cadeia de caracteres |Não |
| prefixo |Prefixo da chave do objeto Olá S3. Objetos cujas chaves começam com esse prefixo serão selecionados. Aplica-se apenas quando a chave está vazia. |string |Não |
| version |versão de saudação do objeto de Olá S3, se o controle de versão S3 estiver habilitado. |Cadeia de caracteres |Não |
| formato | Olá, tipos de formato a seguir têm suporte: **TextFormat**, **JsonFormat**, **AvroFormat**, **OrcFormat**,  **ParquetFormat**. Saudação de conjunto **tipo** propriedade em formato tooone desses valores. Para obter mais informações, consulte Olá [formato de texto](data-factory-supported-file-and-compression-formats.md#text-format), [formato JSON](data-factory-supported-file-and-compression-formats.md#json-format), [formato Avro](data-factory-supported-file-and-compression-formats.md#avro-format), [formato Orc](data-factory-supported-file-and-compression-formats.md#orc-format), e [formato Parquet ](data-factory-supported-file-and-compression-formats.md#parquet-format) seções. <br><br> Se você deseja que os arquivos de toocopy como-entre repositórios baseada em arquivo (cópia binário), skip Olá formato seção em ambas as definições de conjunto de dados de entrada e saída. |Não | |
| compactação | Especifica tipo de saudação e nível de compactação de dados de saudação. tipos de saudação com suporte são: **GZip**, **Deflate**, **BZip2**, e **ZipDeflate**. níveis de saudação com suporte são: **ideal** e **mais rápido**. Para saber mais, confira [File and compression formats in Azure Data Factory](data-factory-supported-file-and-compression-formats.md#compression-support) (Formatos de arquivo e de compactação no Azure Data Factory). |Não | |


> [!NOTE]
> **bucketName + tecla** Especifica o local de saudação do objeto Olá S3, onde bucket é recipiente raiz Olá S3 objetos e a chave é Olá caminho completo toohello S3 objeto.

### <a name="sample-dataset-with-prefix"></a>Conjunto de dados de exemplo com o prefixo

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "prefix": "testFolder/test",
            "bucketName": "testbucket",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```
### <a name="sample-dataset-with-version"></a>Conjunto de dados de exemplo (com a versão)

```json
{
    "name": "dataset-s3",
    "properties": {
        "type": "AmazonS3",
        "linkedServiceName": "link- testS3",
        "typeProperties": {
            "key": "testFolder/test.orc",
            "bucketName": "testbucket",
            "version": "XXXXXXXXXczm0CJajYkHf0_k6LhBmkcL",
            "format": {
                "type": "OrcFormat"
            }
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true
    }
}
```

### <a name="dynamic-paths-for-s3"></a>Caminhos dinâmicos para S3
Olá exemplo anterior usa valores fixos para Olá **chave** e **bucketName** propriedades no conjunto de dados Olá Amazon S3.

```json
"key": "testFolder/test.orc",
"bucketName": "testbucket",
```

Você pode fazer com que o Data Factory calcule essas propriedades dinamicamente em tempo de execução usando variáveis de sistema como SliceStart.

```json
"key": "$$Text.Format('{0:MM}/{0:dd}/test.orc', SliceStart)"
"bucketName": "$$Text.Format('{0:yyyy}', SliceStart)"
```

Você pode fazer hello mesmo para Olá **prefixo** propriedade de um conjunto de dados do Amazon S3. Veja [Funções e variáveis do sistema do Data Factory](data-factory-functions-variables.md) para obter uma lista das funções e variáveis com suporte.

## <a name="copy-activity-properties"></a>Propriedades da atividade de cópia
Para obter uma lista completa das seções e propriedades disponíveis para definir as atividades, consulte [Criando pipelines](data-factory-create-pipelines.md). As propriedades, como nome, descrição, tabelas de entrada e saída, e políticas, estão disponíveis para todos os tipos de atividade. As propriedades disponíveis no hello **typeProperties** seção de atividade Olá variam de acordo com cada tipo de atividade. Para a atividade de cópia hello, propriedades variam dependendo Olá tipos de fontes e coletores. Quando uma fonte na atividade de cópia de saudação é do tipo **FileSystemSource** (que inclui Amazon S3), Olá propriedade a seguir está disponível em **typeProperties** seção:

| Propriedade | Descrição | Valores permitidos | Obrigatório |
| --- | --- | --- | --- |
| recursiva |Especifica se a lista de toorecursively S3 objetos no diretório de saudação. |true/false |Não |

## <a name="json-example-copy-data-from-amazon-s3-tooazure-blob-storage"></a>Exemplo JSON: copiar dados do Amazon S3 tooAzure armazenamento de Blob
Este exemplo mostra como toocopy dados do Amazon S3 tooan armazenamento de BLOBs do Azure. No entanto, dados podem ser copiados diretamente muito[qualquer um dos coletores Olá suportados](data-factory-data-movement-activities.md#supported-data-stores-and-formats) usando a atividade de cópia de saudação na fábrica de dados.

exemplo Hello fornece definições de JSON para Olá entidades da fábrica de dados a seguir. Você pode usar essas definições toocreate um pipeline toocopy os dados de armazenamento de tooBlob Amazon S3, usando Olá [portal do Azure](data-factory-copy-activity-tutorial-using-azure-portal.md), [Visual Studio](data-factory-copy-activity-tutorial-using-visual-studio.md), ou [PowerShell](data-factory-copy-activity-tutorial-using-powershell.md).   

* Um serviço vinculado do tipo [AwsAccessKey](#linked-service-properties).
* Um serviço vinculado do tipo [AzureStorage](data-factory-azure-blob-connector.md#linked-service-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de entrada do tipo [AmazonS3](#dataset-properties).
* Um [conjunto de dados](data-factory-create-datasets.md) de saída do tipo [AzureBlob](data-factory-azure-blob-connector.md#dataset-properties).
* Um [pipeline](data-factory-create-pipelines.md) com a Atividade de Cópia que usa [FileSystemSource](#copy-activity-properties) e [BlobSink](data-factory-azure-blob-connector.md#copy-activity-properties).

exemplo Hello copia dados do Amazon S3 tooan BLOBs do Azure a cada hora. propriedades JSON Olá usadas nesses exemplos são descritas nas seções a seguir exemplos de saudação.

### <a name="amazon-s3-linked-service"></a>Serviço vinculado do Amazon S3

```json
{
    "name": "AmazonS3LinkedService",
    "properties": {
        "type": "AwsAccessKey",
        "typeProperties": {
            "accessKeyId": "<access key id>",
            "secretAccessKey": "<secret access key>"
        }
    }
}
```

### <a name="azure-storage-linked-service"></a>Serviço vinculado de armazenamento do Azure

```json
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

### <a name="amazon-s3-input-dataset"></a>Conjunto de dados de entrada do Amazon S3

Configuração **"externo": true** informa que o serviço da fábrica de dados Olá Olá conjunto de dados é externo toohello fábrica de dados. Defina essa propriedade tootrue em um conjunto de dados de entrada não é produzido por uma atividade no pipeline de saudação.

```json
    {
        "name": "AmazonS3InputDataset",
        "properties": {
            "type": "AmazonS3",
            "linkedServiceName": "AmazonS3LinkedService",
            "typeProperties": {
                "key": "testFolder/test.orc",
                "bucketName": "testbucket",
                "format": {
                    "type": "OrcFormat"
                }
            },
            "availability": {
                "frequency": "Hour",
                "interval": 1
            },
            "external": true
        }
    }
```


### <a name="azure-blob-output-dataset"></a>Conjunto de dados de saída de Blob do Azure

Os dados são gravados tooa novo blob a cada hora (frequência: hora, intervalo: 1). caminho da pasta Olá blob Olá é avaliado dinamicamente com base na hora de início de saudação da fatia Olá que está sendo processada. caminho da pasta Olá usa partes de ano, mês, dia e horário Olá Olá da hora de início.

```json
{
    "name": "AzureBlobOutputDataSet",
    "properties": {
        "type": "AzureBlob",
        "linkedServiceName": "AzureStorageLinkedService",
        "typeProperties": {
            "folderPath": "mycontainer/fromamazons3/yearno={Year}/monthno={Month}/dayno={Day}/hourno={Hour}",
            "format": {
                "type": "TextFormat",
                "rowDelimiter": "\n",
                "columnDelimiter": "\t"
            },
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
            ]
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```


### <a name="copy-activity-in-a-pipeline-with-an-amazon-s3-source-and-a-blob-sink"></a>Atividade de cópia em um pipeline com a origem do Amazon S3 e o coletor de blob

Olá, pipeline contém uma atividade de cópia que está configurado toouse Olá conjuntos de dados de entrada e saídos e é toorun agendado a cada hora. Na definição JSON de pipeline hello, Olá **fonte** tipo está definido muito**FileSystemSource**, e **coletor** tipo está definido muito**BlobSink**.

```json
{
    "name": "CopyAmazonS3ToBlob",
    "properties": {
        "description": "pipeline for copy activity",
        "activities": [
            {
                "type": "Copy",
                "typeProperties": {
                    "source": {
                        "type": "FileSystemSource",
                        "recursive": true
                    },
                    "sink": {
                        "type": "BlobSink",
                        "writeBatchSize": 0,
                        "writeBatchTimeout": "00:00:00"
                    }
                },
                "inputs": [
                    {
                        "name": "AmazonS3InputDataset"
                    }
                ],
                "outputs": [
                    {
                        "name": "AzureBlobOutputDataSet"
                    }
                ],
                "policy": {
                    "timeout": "01:00:00",
                    "concurrency": 1
                },
                "scheduler": {
                    "frequency": "Hour",
                    "interval": 1
                },
                "name": "AmazonS3ToBlob"
            }
        ],
        "start": "2014-08-08T18:00:00Z",
        "end": "2014-08-08T19:00:00Z"
    }
}
```
> [!NOTE]
> colunas de toomap de um toocolumns de conjunto de dados de origem de um conjunto de dados do coletor, consulte [mapeando colunas do conjunto de dados no Azure Data Factory](data-factory-map-columns.md).


## <a name="next-steps"></a>Próximas etapas
Consulte Olá artigos a seguir:

* toolearn sobre a chave de fatores que afetam o desempenho de movimentação de dados (Copiar atividade) na fábrica de dados e toooptimize de várias maneiras, consulte Olá [Copiar atividade guia de desempenho e ajuste](data-factory-copy-activity-performance.md).

* Para obter instruções passo a passo para criar um pipeline com uma atividade de cópia, consulte Olá [tutorial de atividade de cópia](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md).
