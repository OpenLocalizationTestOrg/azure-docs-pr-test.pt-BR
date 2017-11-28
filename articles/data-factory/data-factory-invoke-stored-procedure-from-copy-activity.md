---
title: "aaaInvoke procedimento armazenado de atividade de cópia de fábrica de dados do Azure | Microsoft Docs"
description: "Saiba como atividade de cópia tooinvoke um procedimento armazenado no banco de dados SQL ou SQL Server a partir de uma fábrica de dados do Azure."
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
ms.openlocfilehash: 986377118afb8c08607c2325fcc3ab00b3de9268
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="invoke-stored-procedure-from-copy-activity-in-azure-data-factory"></a><span data-ttu-id="4fb7b-103">Invocar procedimento armazenado de atividade de cópia no Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="4fb7b-103">Invoke stored procedure from copy activity in Azure Data Factory</span></span>
<span data-ttu-id="4fb7b-104">Ao copiar dados no [do SQL Server](data-factory-sqlserver-connector.md) ou [banco de dados do SQL Azure](data-factory-azure-sql-connector.md), você pode configurar Olá **SqlSink** na atividade de cópia tooinvoke um procedimento armazenado.</span><span class="sxs-lookup"><span data-stu-id="4fb7b-104">When copying data into [SQL Server](data-factory-sqlserver-connector.md) or [Azure SQL Database](data-factory-azure-sql-connector.md), you can configure hello **SqlSink** in copy activity tooinvoke a stored procedure.</span></span> <span data-ttu-id="4fb7b-105">Talvez você queira toouse Olá armazenado procedimento tooperform qualquer processamento adicional (mesclagem de colunas, pesquisar valores de inserção em várias tabelas, etc.) é necessária antes de inserir dados na tabela de destino toohello.</span><span class="sxs-lookup"><span data-stu-id="4fb7b-105">You may want toouse hello stored procedure tooperform any additional processing (merging columns, looking up values, insertion into multiple tables, etc.) is required before inserting data in toohello destination table.</span></span> <span data-ttu-id="4fb7b-106">Esse recurso se beneficia de [parâmetros com valores de tabela](https://msdn.microsoft.com/library/bb675163.aspx).</span><span class="sxs-lookup"><span data-stu-id="4fb7b-106">This feature takes advantage of [Table-Valued Parameters](https://msdn.microsoft.com/library/bb675163.aspx).</span></span> 

<span data-ttu-id="4fb7b-107">saudação de exemplo a seguir mostra como tooinvoke um procedimento armazenado em um SQL Server do banco de dados de um pipeline da fábrica de dados (Copiar atividade):</span><span class="sxs-lookup"><span data-stu-id="4fb7b-107">hello following sample shows how tooinvoke a stored procedure in a SQL Server database from a Data Factory pipeline (copy activity):</span></span>  

## <a name="output-dataset-json"></a><span data-ttu-id="4fb7b-108">JSON do conjunto de dados de saída</span><span class="sxs-lookup"><span data-stu-id="4fb7b-108">Output dataset JSON</span></span>
<span data-ttu-id="4fb7b-109">Olá saída conjunto de dados JSON, defina Olá **tipo** para: **SqlServerTable**.</span><span class="sxs-lookup"><span data-stu-id="4fb7b-109">In hello output dataset JSON, set hello **type** to: **SqlServerTable**.</span></span> <span data-ttu-id="4fb7b-110">Defina-o muito**AzureSqlTable** toouse com um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="4fb7b-110">Set it too**AzureSqlTable** toouse with an Azure SQL database.</span></span> <span data-ttu-id="4fb7b-111">Olá valor **tableName** propriedade deve corresponder saudação do primeiro parâmetro do procedimento armazenado de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fb7b-111">hello value for **tableName** property must match hello name of first parameter of hello stored procedure.</span></span>  

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

## <a name="sqlsink-section-in-copy-activity-json"></a><span data-ttu-id="4fb7b-112">Seção SqlSink na atividade de cópia JSON</span><span class="sxs-lookup"><span data-stu-id="4fb7b-112">SqlSink section in copy activity JSON</span></span>
<span data-ttu-id="4fb7b-113">Definir Olá **SqlSink** seção na atividade de cópia Olá JSON da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="4fb7b-113">Define hello **SqlSink** section in hello copy activity JSON as follows.</span></span> <span data-ttu-id="4fb7b-114">tooinvoke um procedimento armazenado ao inserir dados no banco de dados de destino/coletor hello, especifique valores para os dois **SqlWriterStoredProcedureName** e **SqlWriterTableType** propriedades.</span><span class="sxs-lookup"><span data-stu-id="4fb7b-114">tooinvoke a stored procedure while inserting data into hello sink/destination database, specify values for both **SqlWriterStoredProcedureName** and **SqlWriterTableType** properties.</span></span> <span data-ttu-id="4fb7b-115">Para obter descrições dessas propriedades, consulte [do SqlSink seção no artigo de conector do SQL Server Olá](data-factory-sqlserver-connector.md#sqlsink).</span><span class="sxs-lookup"><span data-stu-id="4fb7b-115">For descriptions of these properties, see [SqlSink section in hello SQL Server connector article](data-factory-sqlserver-connector.md#sqlsink).</span></span>

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

## <a name="stored-procedure-definition"></a><span data-ttu-id="4fb7b-116">Definição do procedimento armazenado</span><span class="sxs-lookup"><span data-stu-id="4fb7b-116">Stored procedure definition</span></span> 
<span data-ttu-id="4fb7b-117">No banco de dados, definir o procedimento de saudação armazenado com hello mesmo nome como **SqlWriterStoredProcedureName**.</span><span class="sxs-lookup"><span data-stu-id="4fb7b-117">In your database, define hello stored procedure with hello same name as **SqlWriterStoredProcedureName**.</span></span> <span data-ttu-id="4fb7b-118">procedimento armazenado de saudação lida com dados de entrada de repositório de dados de origem hello e insere dados em uma tabela no banco de dados de destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="4fb7b-118">hello stored procedure handles input data from hello source data store, and inserts data into a table in hello destination database.</span></span> <span data-ttu-id="4fb7b-119">nome de saudação do primeiro parâmetro hello de procedimento armazenado deve corresponder tableName Olá definido no conjunto de dados Olá JSON (Marketing).</span><span class="sxs-lookup"><span data-stu-id="4fb7b-119">hello name of hello first parameter of stored procedure must match hello tableName defined in hello dataset JSON (Marketing).</span></span>

```sql
CREATE PROCEDURE spOverwriteMarketing @Marketing [dbo].[MarketingType] READONLY, @stringData varchar(256)
AS
BEGIN
    DELETE FROM [dbo].[Marketing] where ProfileID = @stringData
    INSERT [dbo].[Marketing](ProfileID, State)
    SELECT * FROM @Marketing
END
```

## <a name="table-type-definition"></a><span data-ttu-id="4fb7b-120">Definição de tipo de tabela</span><span class="sxs-lookup"><span data-stu-id="4fb7b-120">Table type definition</span></span>
<span data-ttu-id="4fb7b-121">No banco de dados, definir o tipo de tabela de saudação com hello mesmo nome como **SqlWriterTableType**.</span><span class="sxs-lookup"><span data-stu-id="4fb7b-121">In your database, define hello table type with hello same name as **SqlWriterTableType**.</span></span> <span data-ttu-id="4fb7b-122">esquema Olá Olá do tipo de tabela deve corresponder o esquema de saudação do conjunto de dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="4fb7b-122">hello schema of hello table type must match hello schema of hello input dataset.</span></span>

```sql
CREATE TYPE [dbo].[MarketingType] AS TABLE(
    [ProfileID] [varchar](256) NOT NULL,
    [State] [varchar](256) NOT NULL
)
```

## <a name="next-steps"></a><span data-ttu-id="4fb7b-123">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="4fb7b-123">Next steps</span></span>
<span data-ttu-id="4fb7b-124">Examine Olá conector artigos para concluir os exemplos JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="4fb7b-124">Review hello following connector articles that for complete JSON examples:</span></span> 

- [<span data-ttu-id="4fb7b-125">Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="4fb7b-125">Azure SQL Database</span></span>](data-factory-azure-sql-connector.md)
- [<span data-ttu-id="4fb7b-126">SQL Server</span><span class="sxs-lookup"><span data-stu-id="4fb7b-126">SQL Server</span></span>](data-factory-sqlserver-connector.md)
