---
title: "colunas do conjunto de dados aaaMapping na fábrica de dados do Azure | Microsoft Docs"
description: Saiba como o toomap colunas de toodestination de colunas de origem.
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: monicar
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: 8f78d4af675bec0a70e5f6e83ec1ffb511408b5a
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a>Mapeie colunas do conjunto de dados colunas toodestination conjunto de dados da fonte
Mapeamento de coluna pode ser usado toospecify como colunas especificadas na hello "structure" de toocolumns de mapa de tabela de origem especificadas no hello "structure" da tabela de coletor. Olá **columnMapping** propriedade está disponível no hello **typeProperties** seção hello atividade de cópia.

Mapeamento de coluna dá suporte a saudação os seguintes cenários:

* Todas as colunas na estrutura de conjunto de dados de origem de saudação são mapeadas tooall colunas na estrutura de conjunto de dados do coletor de saudação.
* Um subconjunto de colunas de saudação na estrutura de conjunto de dados de origem de saudação é mapeada tooall colunas na estrutura de conjunto de dados do coletor de saudação.

Olá seguem as condições de erro que resultam em uma exceção:

* Menos colunas ou mais colunas na hello "structure" da tabela de coletor que especificado no mapeamento de saudação.
* Mapeamento duplicado.
* Resultado da consulta SQL não tem um nome de coluna especificado no mapeamento de saudação.

> [!NOTE]
> Hello exemplos a seguir são para BLOBs do Azure e SQL Azure, mas são aplicáveis tooany repositório de dados que oferece suporte a conjuntos de dados retangulares. Ajuste o conjunto de dados e as definições de serviço vinculado em exemplos toopoint toodata na fonte de dados relevantes de saudação.

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a>Exemplo 1 – mapeamento de blob do Azure SQL tooAzure de coluna
Neste exemplo, tabela de entrada hello tem uma estrutura e aponta tooa tabela do SQL em um banco de dados do SQL Azure.

```json
{
    "name": "AzureSQLInput",
    "properties": {
        "structure": 
         [
           { "name": "userid"},
           { "name": "name"},
           { "name": "group"}
         ],
        "type": "AzureSqlTable",
        "linkedServiceName": "AzureSqlLinkedService",
        "typeProperties": {
            "tableName": "MyTable"
        },
        "availability": {
            "frequency": "Hour",
            "interval": 1
        },
        "external": true,
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

Neste exemplo, a tabela de saída Olá tem uma estrutura e aponta tooa blob em um armazenamento de BLOBs do Azure.

```json
{
    "name": "AzureBlobOutput",
    "properties":
    {
         "structure": 
          [
                { "name": "myuserid"},
                { "name": "myname" },
                { "name": "mygroup"}
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
        "availability":
        {
            "frequency": "Hour",
            "interval": 1
        }
    }
}
```

Olá JSON a seguir define uma atividade de cópia em um pipeline. colunas de saudação da fonte mapeado toocolumns no coletor (**columnMappings**) usando Olá **conversor** propriedade.

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "Copy",
    "inputs":  [ { "name": "AzureSQLInput"  } ],
    "outputs":  [ { "name": "AzureBlobOutput" } ],
    "typeProperties":    {
        "source":
        {
            "type": "SqlSource"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup, Name: MyName"
        }
    },
   "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
**Fluxo de mapeamento de coluna:**

![Fluxo de mapeamento de coluna](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a>Exemplo 2 – com a consulta SQL de blob do Azure SQL tooAzure de mapeamento de coluna
Neste exemplo, uma consulta SQL é usada tooextract dados do SQL Azure, em vez de simplesmente especificando o nome da tabela hello e nomes de coluna de saudação na seção "estrutura". 

```json
{
    "name": "CopyActivity",
    "description": "description", 
    "type": "CopyActivity",
    "inputs":  [ { "name": " AzureSQLInput"  } ],
    "outputs":  [ { "name": " AzureBlobOutput" } ],
    "typeProperties":
    {
        "source":
        {
            "type": "SqlSource",
            "SqlReaderQuery": "$$Text.Format('SELECT * FROM MyTable WHERE StartDateTime = \\'{0:yyyyMMdd-HH}\\'', WindowStart)"
        },
        "sink":
        {
            "type": "BlobSink"
        },
        "Translator": 
        {
            "type": "TabularTranslator",
            "ColumnMappings": "UserId: MyUserId, Group: MyGroup,Name: MyName"
        }
    },
    "scheduler": {
          "frequency": "Hour",
          "interval": 1
        }
}
```
Nesse caso, os resultados da consulta de saudação são primeiro toocolumns mapeado especificado em "structure" de origem. Em seguida, colunas de saudação da fonte "structure" são mapeadas toocolumns no coletor "structure" com as regras especificadas em columnMappings.  Suponha que a consulta Olá retorna 5 colunas, duas ou mais colunas daquelas especificadas no hello "structure" de origem.

**Fluxo de mapeamento de coluna**

![Fluxo de mapeamento de coluna-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a>Próximas etapas
Consulte o artigo de saudação para obter um tutorial sobre como usar a atividade de cópia: 

- [Copiar dados de armazenamento de Blob tooSQL banco de dados](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
