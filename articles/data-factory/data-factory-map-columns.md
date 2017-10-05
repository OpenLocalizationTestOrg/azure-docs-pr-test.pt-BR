---
title: Mapear colunas de conjunto de dados no Azure Data Factory | Microsoft Docs
description: Saiba como mapear colunas de origem para colunas de destino.
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
ms.openlocfilehash: a50661b377cfbbff3f1f762342cb275d5da82cea
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="map-source-dataset-columns-to-destination-dataset-columns"></a><span data-ttu-id="b5ca0-103">Mapear colunas de conjunto de dados de origem para colunas de conjunto de dados de destino</span><span class="sxs-lookup"><span data-stu-id="b5ca0-103">Map source dataset columns to destination dataset columns</span></span>
<span data-ttu-id="b5ca0-104">O mapeamento de coluna pode ser usado para definir como colunas especificadas na "estrutura" da tabela de origem estão correlacionadas a colunas especificada na "estrutura" da tabela de coletor.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-104">Column mapping can be used to specify how columns specified in the “structure” of source table map to columns specified in the “structure” of sink table.</span></span> <span data-ttu-id="b5ca0-105">A propriedade **columnMapping** está disponível na seção **typeProperties** da atividade Copiar.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-105">The **columnMapping** property is available in the **typeProperties** section of the Copy activity.</span></span>

<span data-ttu-id="b5ca0-106">O mapeamento de coluna oferece suporte para os seguintes cenários:</span><span class="sxs-lookup"><span data-stu-id="b5ca0-106">Column mapping supports the following scenarios:</span></span>

* <span data-ttu-id="b5ca0-107">Todas as colunas na estrutura do conjunto de dados de origem são mapeadas para todas as colunas na estrutura do conjunto de dados do coletor.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-107">All columns in the source dataset structure are mapped to all columns in the sink dataset structure.</span></span>
* <span data-ttu-id="b5ca0-108">Um subconjunto das colunas na estrutura do conjunto de dados de origem é mapeado para todas as colunas na estrutura do conjunto de dados do coletor.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-108">A subset of the columns in the source dataset structure is mapped to all columns in the sink dataset structure.</span></span>

<span data-ttu-id="b5ca0-109">Veja a seguir condições de erro que resultam em uma exceção:</span><span class="sxs-lookup"><span data-stu-id="b5ca0-109">The following are error conditions that result in an exception:</span></span>

* <span data-ttu-id="b5ca0-110">Menos colunas ou mais colunas na "estrutura" da tabela de coletor do que o especificado no mapeamento.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-110">Either fewer columns or more columns in the “structure” of sink table than specified in the mapping.</span></span>
* <span data-ttu-id="b5ca0-111">Mapeamento duplicado.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-111">Duplicate mapping.</span></span>
* <span data-ttu-id="b5ca0-112">O resultado da consulta SQL não tem um nome de coluna especificado no mapeamento.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-112">SQL query result does not have a column name that is specified in the mapping.</span></span>

> [!NOTE]
> <span data-ttu-id="b5ca0-113">Os exemplos a seguir são para o Azure SQL e os Blobs do Azure, mas são aplicáveis a qualquer repositório de dados com suporte a conjuntos de dados retangulares.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-113">The following samples are for Azure SQL and Azure Blob but are applicable to any data store that supports rectangular datasets.</span></span> <span data-ttu-id="b5ca0-114">Ajuste o conjunto de dados e as definições de serviço vinculado nos exemplos para apontar para dados na fonte de dados relevante.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-114">Adjust dataset and linked service definitions in examples to point to data in the relevant data source.</span></span>

## <a name="sample-1--column-mapping-from-azure-sql-to-azure-blob"></a><span data-ttu-id="b5ca0-115">Exemplo 1 - mapeamento de coluna do SQL Azure para blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="b5ca0-115">Sample 1 – column mapping from Azure SQL to Azure blob</span></span>
<span data-ttu-id="b5ca0-116">Neste exemplo, a tabela de entrada tem uma estrutura e ela aponta para uma tabela do SQL em um banco de dados SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-116">In this sample, the input table has a structure and it points to a SQL table in an Azure SQL database.</span></span>

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

<span data-ttu-id="b5ca0-117">Neste exemplo, a tabela de saída tem uma estrutura e ela aponta para um blob em um armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-117">In this sample, the output table has a structure and it points to a blob in an Azure blob storage.</span></span>

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

<span data-ttu-id="b5ca0-118">O JSON a seguir define uma atividade de cópia em um pipeline.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-118">The following JSON defines a copy activity in a pipeline.</span></span> <span data-ttu-id="b5ca0-119">As colunas da fonte são mapeadas para colunas no coletor (**columnMappings**) utilizando a propriedade **Translator**.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-119">The columns from source mapped to columns in sink (**columnMappings**) by using the **Translator** property.</span></span>

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
<span data-ttu-id="b5ca0-120">**Fluxo de mapeamento de coluna:**</span><span class="sxs-lookup"><span data-stu-id="b5ca0-120">**Column mapping flow:**</span></span>

![Fluxo de mapeamento de coluna](./media/data-factory-map-columns/column-mapping-flow.png)

## <a name="sample-2--column-mapping-with-sql-query-from-azure-sql-to-azure-blob"></a><span data-ttu-id="b5ca0-122">Exemplo 2 - mapeamento de coluna com a consulta SQL do SQL Azure para blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="b5ca0-122">Sample 2 – column mapping with SQL query from Azure SQL to Azure blob</span></span>
<span data-ttu-id="b5ca0-123">Neste exemplo, uma consulta SQL é usada para extrair dados do SQL Azure, em vez de simplesmente especificar o nome da tabela e os nomes das colunas na seção de "estrutura".</span><span class="sxs-lookup"><span data-stu-id="b5ca0-123">In this sample, a SQL query is used to extract data from Azure SQL instead of simply specifying the table name and the column names in “structure” section.</span></span> 

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
<span data-ttu-id="b5ca0-124">Nesse caso, os resultados da consulta primeiro são mapeados para colunas especificadas na "estrutura" da origem.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-124">In this case, the query results are first mapped to columns specified in “structure” of source.</span></span> <span data-ttu-id="b5ca0-125">Em seguida, as colunas da "estrutura" de origem são mapeadas para colunas na "estrutura" do coletor com as regras especificadas em columnMappings.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-125">Next, the columns from source “structure” are mapped to columns in sink “structure” with rules specified in columnMappings.</span></span>  <span data-ttu-id="b5ca0-126">Suponha que a consulta retorne cinco colunas, duas colunas adicionais e as especificadas na "estrutura" de origem.</span><span class="sxs-lookup"><span data-stu-id="b5ca0-126">Suppose the query returns 5 columns, two more columns than those specified in the “structure” of source.</span></span>

<span data-ttu-id="b5ca0-127">**Fluxo de mapeamento de coluna**</span><span class="sxs-lookup"><span data-stu-id="b5ca0-127">**Column mapping flow**</span></span>

![Fluxo de mapeamento de coluna-2](./media/data-factory-map-columns/column-mapping-flow-2.png)

## <a name="next-steps"></a><span data-ttu-id="b5ca0-129">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b5ca0-129">Next steps</span></span>
<span data-ttu-id="b5ca0-130">Veja o artigo para obter um tutorial sobre como usar a Atividade de Cópia:</span><span class="sxs-lookup"><span data-stu-id="b5ca0-130">See the article for a tutorial on using Copy Activity:</span></span> 

- [<span data-ttu-id="b5ca0-131">Copiar dados do Armazenamento de Blobs para o Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="b5ca0-131">Copy data from Blob Storage to SQL Database</span></span>](data-factory-copy-data-from-azure-blob-storage-to-sql-database.md)
