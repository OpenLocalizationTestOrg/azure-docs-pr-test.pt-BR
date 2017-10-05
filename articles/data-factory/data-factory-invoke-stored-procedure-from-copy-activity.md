---
title: "Invocar o procedimento armazenado de atividade de cópia do Azure Data Factory | Microsoft Docs"
description: "Saiba como invocar um procedimento armazenado no Banco de Dados SQL do Azure ou SQL Server de uma atividade de cópia do Azure Data Factory."
services: data-factory
documentationcenter: 
author: linda33wj
manager: jhubbard
editor: 
ms.service: data-factory
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/20/2017
ms.author: jingwang
ms.openlocfilehash: af6e4a57e726598c266ee766656aa2cc22e374e3
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="1d7c4-103">Invocar procedimento armazenado de atividade de cópia no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="1d7c4-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="1d7c4-104">Ao copiar dados no [SQL Server](data-factory-sqlserver-connector.md) ou [Banco de Dados SQL do Azure](data-factory-azure-sql-connector.md), você pode configurar o **SqlSink** na atividade de cópia para invocar um procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="1d7c4-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure the **SqlSink** in copy activity to invoke a stored procedure.</span></span> <span data-ttu-id="1d7c4-105">Talvez você queira usar o procedimento armazenado para executar algum processamento adicional (mesclar colunas, pesquisar valores, inserção em várias tabelas, etc.) necessário antes de inserir dados na tabela de destino.</span><span class="sxs-lookup"><span data-stu-id="1d7c4-105">You may want to use the stored procedure to perform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in to the destination table.</span></span> <span data-ttu-id="1d7c4-106">Esse recurso se beneficia de [parâmetros com valores de tabela](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="1d7c4-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="1d7c4-107">A amostra a seguir mostra como invocar um procedimento armazenado em um banco de dados do SQL Server de um pipeline de Data Factory (atividade de cópia):</span><span class="sxs-lookup"><span data-stu-id="1d7c4-107">The following sample shows how to invoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="1d7c4-108">JSON do conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="1d7c4-108">Output dataset JSON</span></span>
<span data-ttu-id="1d7c4-109">No JSON do conjunto de dados de saída, defina **tipo** para: **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="1d7c4-109">In the output dataset JSON, set the **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="1d7c4-110">Defina-o como **AzureSqlTable** para usá-lo com um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="1d7c4-110">Set it to **AzureSqlTable** to use with an Azure SQL database.</span></span> <span data-ttu-id="1d7c4-111">O valor da propriedade **tableName** deve corresponder ao nome do primeiro parâmetro do procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="1d7c4-111">The value for **tableName** property must match the name of first parameter of the stored procedure.</span></span>  

```json
{
  "name": "SqlOutput",
  "properties": {
    "type": "SqlServerTable",
    "linkedServiceName": "SqlLinkedService",
    "typeProperties": {
      "tableName": "Marketing"
    },
    "availability": {
      "frequency": "Hour",
      "interval": 1
    }
  }
}
```

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="1d7c4-112">Seção SqlSink na atividade de cópia JSON</span><span class="sxs-lookup"><span data-stu-id="1d7c4-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="1d7c4-113">Defina a seção **SqlSink** na atividade de cópia JSON conforme demonstrado a seguir.</span><span class="sxs-lookup"><span data-stu-id="1d7c4-113">Define the **SqlSink** section in the copy activity JSON as follows.</span></span> <span data-ttu-id="1d7c4-114">Para invocar um procedimento armazenado ao inserir dados no banco de dados do coletor/destino, especifique valores para ambas as propriedades **SqlWriterStoredProcedureName** e **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="1d7c4-114">To invoke a stored procedure while inserting data into the sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="1d7c4-115">Para obter descrições dessas propriedades, consulte a [seção SqlSink no artigo de conector do SQL Server](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="1d7c4-115">For descriptions of these properties, see [SqlSink section in the SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

```json
"sink":
{
    "type": "SqlSink",
    "SqlWriterTableType": "MarketingType",
    "SqlWriterStoredProcedureName": "spOverwriteMarketing", 
    "storedProcedureParameters":
            {
                "stringData": 
                {
                    "value": "str1"     
                }
            }
}
```

## <a name="stored-procedure-definition"></a><span data-ttu-id="1d7c4-116">Definição do procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="1d7c4-116">Stored procedure definition</span></span> 
<span data-ttu-id="1d7c4-117">No banco de dados, defina o procedimento armazenado com o mesmo nome que **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="1d7c4-117">In your database, define the stored procedure with the same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="1d7c4-118">O procedimento armazenado manipula dados de entrada do armazenamento de dados de origem e insere dados em uma tabela no banco de dados de destino.</span><span class="sxs-lookup"><span data-stu-id="1d7c4-118">The stored procedure handles input data from the source data store, and inserts data into a table in the destination database.</span></span> <span data-ttu-id="1d7c4-119">O nome do primeiro parâmetro do procedimento armazenado deve corresponder ao tableName definido no JSON do conjunto de dados (Marketing).</span><span class="sxs-lookup"><span data-stu-id="1d7c4-119">The name of the first parameter of stored procedure must match the tableName defined in the dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="1d7c4-120">Definição de tipo de tabela</span><span class="sxs-lookup"><span data-stu-id="1d7c4-120">Table type definition</span></span>
<span data-ttu-id="1d7c4-121">No banco de dados, defina o tipo de tabela com o mesmo nome que **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="1d7c4-121">In your database, define the table type with the same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="1d7c4-122">O esquema do tipo de tabela deve corresponder ao esquema de conjunto de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="1d7c4-122">The schema of the table type must match the schema of the input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="1d7c4-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1d7c4-123">Next steps</span></span>
<span data-ttu-id="1d7c4-124">Examine os artigos sobre conector a seguir para obter exemplos de JSON completos:</span><span class="sxs-lookup"><span data-stu-id="1d7c4-124">Review the following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="1d7c4-125">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="1d7c4-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="1d7c4-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="1d7c4-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
