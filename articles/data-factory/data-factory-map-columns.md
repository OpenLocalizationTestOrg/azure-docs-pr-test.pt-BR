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
# <a name="map-source-dataset-columns-toodestination-dataset-columns"></a><span data-ttu-id="a4343-103">Mapeie colunas do conjunto de dados colunas toodestination conjunto de dados da fonte</span><span class="sxs-lookup"><span data-stu-id="a4343-103">Map source dataset columns toodestination dataset columns</span></span>
<span data-ttu-id="a4343-104">Mapeamento de coluna pode ser usado toospecify como colunas especificadas na hello "structure" de toocolumns de mapa de tabela de origem especificadas no hello "structure" da tabela de coletor.</span><span class="sxs-lookup"><span data-stu-id="a4343-104">Column mapping can be used toospecify how columns specified in hello “structure” of source table map toocolumns specified in hello “structure” of sink table.</span></span> <span data-ttu-id="a4343-105">Olá **columnMapping** propriedade está disponível no hello **typeProperties** seção hello atividade de cópia.</span><span class="sxs-lookup"><span data-stu-id="a4343-105">hello **columnMapping** property is available in hello **typeProperties** section of hello Copy activity.</span></span>

<span data-ttu-id="a4343-106">Mapeamento de coluna dá suporte a saudação os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="a4343-106">Column mapping supports hello following scenarios:</span></span>

* <span data-ttu-id="a4343-107">Todas as colunas na estrutura de conjunto de dados de origem de saudação são mapeadas tooall colunas na estrutura de conjunto de dados do coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4343-107">All columns in hello source dataset structure are mapped tooall columns in hello sink dataset structure.</span></span>
* <span data-ttu-id="a4343-108">Um subconjunto de colunas de saudação na estrutura de conjunto de dados de origem de saudação é mapeada tooall colunas na estrutura de conjunto de dados do coletor de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4343-108">A subset of hello columns in hello source dataset structure is mapped tooall columns in hello sink dataset structure.</span></span>

<span data-ttu-id="a4343-109">Olá seguem as condições de erro que resultam em uma exceção:</span><span class="sxs-lookup"><span data-stu-id="a4343-109">hello following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="a4343-110">Menos colunas ou mais colunas na hello "structure" da tabela de coletor que especificado no mapeamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4343-110">Either fewer columns or more columns in hello “structure” of sink table than specified in hello mapping.</span></span>
* <span data-ttu-id="a4343-111">Mapeamento duplicado.</span><span class="sxs-lookup"><span data-stu-id="a4343-111">Duplicate mapping.</span></span>
* <span data-ttu-id="a4343-112">Resultado da consulta SQL não tem um nome de coluna especificado no mapeamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4343-112">SQL query result does not have a column name that is specified in hello mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="a4343-113">Hello exemplos a seguir são para BLOBs do Azure e SQL Azure, mas são aplicáveis tooany repositório de dados que oferece suporte a conjuntos de dados retangulares.</span><span class="sxs-lookup"><span data-stu-id="a4343-113">hello following samples are for Azure SQL and Azure Blob but are applicable tooany data store that supports rectangular datasets.</span></span> <span data-ttu-id="a4343-114">Ajuste o conjunto de dados e as definições de serviço vinculado em exemplos toopoint toodata na fonte de dados relevantes de saudação.</span><span class="sxs-lookup"><span data-stu-id="a4343-114">Adjust dataset and linked service definitions in examples toopoint toodata in hello relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-tooazure-blob"></a><span data-ttu-id="a4343-115">Exemplo 1 – mapeamento de blob do Azure SQL tooAzure de coluna</span><span class="sxs-lookup"><span data-stu-id="a4343-115">Sample 1 – column mapping from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="a4343-116">Neste exemplo, tabela de entrada hello tem uma estrutura e aponta tooa tabela do SQL em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="a4343-116">In this sample, hello input table has a structure and it points tooa SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="a4343-117">Neste exemplo, a tabela de saída Olá tem uma estrutura e aponta tooa blob em um armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="a4343-117">In this sample, hello output table has a structure and it points tooa blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="a4343-118">Olá JSON a seguir define uma atividade de cópia em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="a4343-118">hello following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="a4343-119">colunas de saudação da fonte mapeado toocolumns no coletor (**columnMappings**) usando Olá **conversor** propriedade.</span><span class="sxs-lookup"><span data-stu-id="a4343-119">hello columns from source mapped toocolumns in sink (**columnMappings**) by using hello **Translator** property.</span></span>

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
<span data-ttu-id="a4343-120">**Fluxo de mapeamento de coluna:**</span><span class="sxs-lookup"><span data-stu-id="a4343-120">**Column mapping flow:**</span></span>

![Fluxo de mapeamento de coluna](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-tooazure-blob"></a><span data-ttu-id="a4343-122">Exemplo 2 – com a consulta SQL de blob do Azure SQL tooAzure de mapeamento de coluna</span><span class="sxs-lookup"><span data-stu-id="a4343-122">Sample 2 – column mapping with SQL query from Azure SQL tooAzure blob</span></span>
<span data-ttu-id="a4343-123">Neste exemplo, uma consulta SQL é usada tooextract dados do SQL Azure, em vez de simplesmente especificando o nome da tabela hello e nomes de coluna de saudação na seção "estrutura".</span><span class="sxs-lookup"><span data-stu-id="a4343-123">In this sample, a SQL query is used tooextract data from Azure SQL instead of simply specifying hello table name and hello column names in “structure” section.</span></span> 

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
<span data-ttu-id="a4343-124">Nesse caso, os resultados da consulta de saudação são primeiro toocolumns mapeado especificado em "structure" de origem.</span><span class="sxs-lookup"><span data-stu-id="a4343-124">In this case, hello query results are first mapped toocolumns specified in “structure” of source.</span></span> <span data-ttu-id="a4343-125">Em seguida, colunas de saudação da fonte "structure" são mapeadas toocolumns no coletor "structure" com as regras especificadas em columnMappings.</span><span class="sxs-lookup"><span data-stu-id="a4343-125">Next, hello columns from source “structure” are mapped toocolumns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="a4343-126">Suponha que a consulta Olá retorna 5 colunas, duas ou mais colunas daquelas especificadas no hello "structure" de origem.</span><span class="sxs-lookup"><span data-stu-id="a4343-126">Suppose hello query returns 5 columns, two more columns than those specified in hello “structure” of source.</span></span>

<span data-ttu-id="a4343-127">**Fluxo de mapeamento de coluna**</span><span class="sxs-lookup"><span data-stu-id="a4343-127">**Column mapping flow**</span></span>

![Fluxo de mapeamento de coluna-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="a4343-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a4343-129">Next steps</span></span>
<span data-ttu-id="a4343-130">Consulte o artigo de saudação para obter um tutorial sobre como usar a atividade de cópia:</span><span class="sxs-lookup"><span data-stu-id="a4343-130">See hello article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="a4343-131">Copiar dados de armazenamento de Blob tooSQL banco de dados</span><span class="sxs-lookup"><span data-stu-id="a4343-131">Copy data from Blob Storage tooSQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
