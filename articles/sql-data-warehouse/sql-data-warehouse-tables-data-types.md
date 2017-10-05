---
title: "Orientação sobre tipos de dados - SQL Data Warehouse do Azure | Microsoft Docs"
description: "Recomendações para definir os tipos de dados que são compatíveis com o SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: shivaniguptamsft
manager: barbkess
editor: 
ms.assetid: d4a1f0a3-ba9f-44b9-95f6-16a4f30746d6
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: tables
ms.date: 06/02/2017
ms.author: shigu;barbkess
ms.openlocfilehash: 5c24c71af16bd9851d9caf15fecfa4bb76f5f77e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="guidance-for-defining-data-types-for-tables-in-sql-data-warehouse"></a><span data-ttu-id="7d3a8-103">Orientação para definição de tipos de dados para as tabelas no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="7d3a8-103">Guidance for defining data types for tables in SQL Data Warehouse</span></span>
<span data-ttu-id="7d3a8-104">Use estas recomendações para definir os tipos de dados de tabela que são compatíveis com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-104">Use these recommendations to define table data types that are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="7d3a8-105">Além da compatibilidade, minimizar o tamanho dos tipos de dados melhora o desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-105">In addition to compatibility, minimizing the size of data types improves query performance.</span></span>

<span data-ttu-id="7d3a8-106">O SQL Data Warehouse oferece suporte aos tipos comuns de dados usados.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-106">SQL Data Warehouse supports the most commonly used data types.</span></span> <span data-ttu-id="7d3a8-107">Para obter uma lista dos tipos de dados com suporte, consulte [tipos de dados](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) na instrução CREATE TABLE.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-107">For a list of the supported data types, see [data types](/sql/docs/t-sql/statements/create-table-azure-sql-data-warehouse.md#datatypes) in the CREATE TABLE statement.</span></span> 


## <a name="minimize-row-length"></a><span data-ttu-id="7d3a8-108">Minimizar o tamanho da linha</span><span class="sxs-lookup"><span data-stu-id="7d3a8-108">Minimize row length</span></span>
<span data-ttu-id="7d3a8-109">Minimizar o tamanho dos tipos de dados reduz o tamanho da linha, o que leva a um desempenho de consulta melhor.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-109">Minimizing the size of data types shortens the row length, which leads to better query performance.</span></span> <span data-ttu-id="7d3a8-110">Use o menor tipo de dados que funcione para seus dados.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-110">Use the smallest data type that works for your data.</span></span> 

- <span data-ttu-id="7d3a8-111">Evite definir as colunas de caractere como um tamanho padrão grande.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-111">Avoid defining character columns with a large default length.</span></span> <span data-ttu-id="7d3a8-112">Por exemplo, se o maior valor for 25 caracteres, defina a coluna como VARCHAR(25).</span><span class="sxs-lookup"><span data-stu-id="7d3a8-112">For example, if the longest value is 25 characters, then define your column as VARCHAR(25).</span></span> 
- <span data-ttu-id="7d3a8-113">Evite usar [NVARCHAR][NVARCHAR] quando precisar somente de VARCHAR.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-113">Avoid using [NVARCHAR][NVARCHAR] when you only need VARCHAR.</span></span>
- <span data-ttu-id="7d3a8-114">Quando possível, use NVARCHAR(4000) ou VARCHAR(8000) em vez de NVARCHAR(MAX) ou VARCHAR(MAX).</span><span class="sxs-lookup"><span data-stu-id="7d3a8-114">When possible, use NVARCHAR(4000) or VARCHAR(8000) instead of NVARCHAR(MAX) or VARCHAR(MAX).</span></span>

<span data-ttu-id="7d3a8-115">Se estiver usando o Polybase para carregar as tabelas, o tamanho definido da linha da tabela não pode exceder 1 MB.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-115">If you are using Polybase to load your tables, the defined length of the table row cannot exceed 1 MB.</span></span> <span data-ttu-id="7d3a8-116">Quando uma linha com dados de tamanho variável exceder 1 MB, você poderá carregar a linha com BCP, mas não com PolyBase.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-116">When a row with variable-length data exceeds 1 MB, you can load the row with BCP, but not with PolyBase.</span></span>

## <a name="identify-unsupported-data-types"></a><span data-ttu-id="7d3a8-117">Identificar tipos de dados sem suporte</span><span class="sxs-lookup"><span data-stu-id="7d3a8-117">Identify unsupported data types</span></span>
<span data-ttu-id="7d3a8-118">Se você estiver migrando o banco de dados de outro banco de dados SQL, poderá encontrar alguns tipos de dados que não têm suporte no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-118">If you are migrating your database from another SQL database, you might encounter data types that are not supported in SQL Data Warehouse.</span></span> <span data-ttu-id="7d3a8-119">Use esta consulta para descobrir os tipos de dados sem suporte em seu esquema SQL existente.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-119">Use this query to discover unsupported data types in your existing SQL schema.</span></span>

```sql
SELECT  t.[name], c.[name], c.[system_type_id], c.[user_type_id], y.[is_user_defined], y.[name]
FROM sys.tables  t
JOIN sys.columns c on t.[object_id]    = c.[object_id]
JOIN sys.types   y on c.[user_type_id] = y.[user_type_id]
WHERE y.[name] IN ('geography','geometry','hierarchyid','image','text','ntext','sql_variant','timestamp','xml')
 AND  y.[is_user_defined] = 1;
```


## <span data-ttu-id="7d3a8-120"><a name="unsupported-data-types"></a>Usar soluções alternativas para os tipos de dados sem suporte</span><span class="sxs-lookup"><span data-stu-id="7d3a8-120"><a name="unsupported-data-types"></a>Use workarounds for unsupported data types</span></span>

<span data-ttu-id="7d3a8-121">A lista a seguir mostra os tipos de dados para os quais o SQL Data Warehouse não dá suporte e fornece alternativas que você pode usar no lugar dos tipos de dados sem suporte.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-121">The following list shows the data types that SQL Data Warehouse does not support and gives alternatives that you can use instead of the unsupported data types.</span></span>

| <span data-ttu-id="7d3a8-122">Tipos de dados sem suporte</span><span class="sxs-lookup"><span data-stu-id="7d3a8-122">Unsupported data type</span></span> | <span data-ttu-id="7d3a8-123">Solução alternativa</span><span class="sxs-lookup"><span data-stu-id="7d3a8-123">Workaround</span></span> |
| --- | --- |
| <span data-ttu-id="7d3a8-124">[geometry][geometry]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-124">[geometry][geometry]</span></span> |<span data-ttu-id="7d3a8-125">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-125">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="7d3a8-126">[geography][geography]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-126">[geography][geography]</span></span> |<span data-ttu-id="7d3a8-127">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-127">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="7d3a8-128">[hierarchyid][hierarchyid]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-128">[hierarchyid][hierarchyid]</span></span> |<span data-ttu-id="7d3a8-129">[nvarchar][nvarchar](4000)</span><span class="sxs-lookup"><span data-stu-id="7d3a8-129">[nvarchar][nvarchar](4000)</span></span> |
| <span data-ttu-id="7d3a8-130">[image][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-130">[image][ntext,text,image]</span></span> |<span data-ttu-id="7d3a8-131">[varbinary][varbinary]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-131">[varbinary][varbinary]</span></span> |
| <span data-ttu-id="7d3a8-132">[text][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-132">[text][ntext,text,image]</span></span> |<span data-ttu-id="7d3a8-133">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-133">[varchar][varchar]</span></span> |
| <span data-ttu-id="7d3a8-134">[ntext][ntext,text,image]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-134">[ntext][ntext,text,image]</span></span> |<span data-ttu-id="7d3a8-135">[nvarchar][nvarchar]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-135">[nvarchar][nvarchar]</span></span> |
| <span data-ttu-id="7d3a8-136">[sql_variant][sql_variant]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-136">[sql_variant][sql_variant]</span></span> |<span data-ttu-id="7d3a8-137">Divida a coluna em várias colunas fortemente tipadas.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-137">Split column into several strongly typed columns.</span></span> |
| <span data-ttu-id="7d3a8-138">[table][table]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-138">[table][table]</span></span> |<span data-ttu-id="7d3a8-139">Converta em tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-139">Convert to temporary tables.</span></span> |
| <span data-ttu-id="7d3a8-140">[timestamp][timestamp]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-140">[timestamp][timestamp]</span></span> |<span data-ttu-id="7d3a8-141">Retrabalhe o código para usar [datetime2][datetime2] e a função `CURRENT_TIMESTAMP`.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-141">Rework code to use [datetime2][datetime2] and `CURRENT_TIMESTAMP` function.</span></span>  <span data-ttu-id="7d3a8-142">Somente as constantes são suportados como padrões, portanto, current_timestamp não pode ser definida como uma restrição padrão.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-142">Only constants are supported as defaults, therefore current_timestamp cannot be defined as a default constraint.</span></span> <span data-ttu-id="7d3a8-143">Se precisar migrar os valores de versão de linha de uma coluna tipada com o carimbo de data/hora, use [BINARY][BINARY](8) ou [VARBINARY][BINARY](8) para os valores de versão de linha NOT NULL ou NULL.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-143">If you need to migrate row version values from a timestamp typed column, then use [BINARY][BINARY](8) or [VARBINARY][BINARY](8) for NOT NULL or NULL row version values.</span></span> |
| <span data-ttu-id="7d3a8-144">[xml][xml]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-144">[xml][xml]</span></span> |<span data-ttu-id="7d3a8-145">[varchar][varchar]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-145">[varchar][varchar]</span></span> |
| <span data-ttu-id="7d3a8-146">[Tipos definidos pelo usuário][user defined types]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-146">[user-defined type][user defined types]</span></span> |<span data-ttu-id="7d3a8-147">Converta para o tipo de dados nativo quando possível.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-147">Convert back to the native data type when possible.</span></span> |
| <span data-ttu-id="7d3a8-148">valores padrão</span><span class="sxs-lookup"><span data-stu-id="7d3a8-148">default values</span></span> | <span data-ttu-id="7d3a8-149">Os valores padrão dão suporte somente a literais e constantes.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-149">Default values support literals and constants only.</span></span>  <span data-ttu-id="7d3a8-150">Não há suporte para expressões ou funções não determinísticas como `GETDATE()` ou `CURRENT_TIMESTAMP`.</span><span class="sxs-lookup"><span data-stu-id="7d3a8-150">Non-deterministic expressions or functions, such as `GETDATE()` or `CURRENT_TIMESTAMP`, are not supported.</span></span> |


## <a name="next-steps"></a><span data-ttu-id="7d3a8-151">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="7d3a8-151">Next steps</span></span>
<span data-ttu-id="7d3a8-152">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="7d3a8-152">To learn more, see:</span></span>

- <span data-ttu-id="7d3a8-153">[Práticas recomendadas do SQL Data Warehouse][SQL Data Warehouse Best Practices]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-153">[SQL Data Warehouse Best Practices][SQL Data Warehouse Best Practices]</span></span>
- <span data-ttu-id="7d3a8-154">[Visão geral da tabela][Overview]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-154">[Table Overview][Overview]</span></span>
- <span data-ttu-id="7d3a8-155">[Distribuição de uma tabela][Distribute]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-155">[Distributing a Table][Distribute]</span></span>
- <span data-ttu-id="7d3a8-156">[Indexação de uma tabela][Index]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-156">[Indexing a Table][Index]</span></span>
- <span data-ttu-id="7d3a8-157">[Particionamento de uma tabela][Partition]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-157">[Partitioning a Table][Partition]</span></span>
- <span data-ttu-id="7d3a8-158">[Manter estatísticas de tabela][Statistics]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-158">[Maintaining Table Statistics][Statistics]</span></span>
- <span data-ttu-id="7d3a8-159">[Tabelas temporárias][Temporary]</span><span class="sxs-lookup"><span data-stu-id="7d3a8-159">[Temporary Tables][Temporary]</span></span>

<!--Image references-->

<!--Article references-->
[Overview]: ./sql-data-warehouse-tables-overview.md
[Data Types]: ./sql-data-warehouse-tables-data-types.md
[Distribute]: ./sql-data-warehouse-tables-distribute.md
[Index]: ./sql-data-warehouse-tables-index.md
[Partition]: ./sql-data-warehouse-tables-partition.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md
[Temporary]: ./sql-data-warehouse-tables-temporary.md
[SQL Data Warehouse Best Practices]: ./sql-data-warehouse-best-practices.md

<!--MSDN references-->

<!--Other Web references-->
[create table]: https://msdn.microsoft.com/library/mt203953.aspx
[bigint]: https://msdn.microsoft.com/library/ms187745.aspx
[binary]: https://msdn.microsoft.com/library/ms188362.aspx
[bit]: https://msdn.microsoft.com/library/ms177603.aspx
[char]: https://msdn.microsoft.com/library/ms176089.aspx
[date]: https://msdn.microsoft.com/library/bb630352.aspx
[datetime]: https://msdn.microsoft.com/library/ms187819.aspx
[datetime2]: https://msdn.microsoft.com/library/bb677335.aspx
[datetimeoffset]: https://msdn.microsoft.com/library/bb630289.aspx
[decimal]: https://msdn.microsoft.com/library/ms187746.aspx
[float]: https://msdn.microsoft.com/library/ms173773.aspx
[geometry]: https://msdn.microsoft.com/library/cc280487.aspx
[geography]: https://msdn.microsoft.com/library/cc280766.aspx
[hierarchyid]: https://msdn.microsoft.com/library/bb677290.aspx
[int]: https://msdn.microsoft.com/library/ms187745.aspx
[money]: https://msdn.microsoft.com/library/ms179882.aspx
[nchar]: https://msdn.microsoft.com/library/ms186939.aspx
[nvarchar]: https://msdn.microsoft.com/library/ms186939.aspx
[ntext,text,image]: https://msdn.microsoft.com/library/ms187993.aspx
[real]: https://msdn.microsoft.com/library/ms173773.aspx
[smalldatetime]: https://msdn.microsoft.com/library/ms182418.aspx
[smallint]: https://msdn.microsoft.com/library/ms187745.aspx
[smallmoney]: https://msdn.microsoft.com/library/ms179882.aspx
[sql_variant]: https://msdn.microsoft.com/library/ms173829.aspx
[sysname]: https://msdn.microsoft.com/library/ms186939.aspx
[table]: https://msdn.microsoft.com/library/ms175010.aspx
[time]: https://msdn.microsoft.com/library/bb677243.aspx
[timestamp]: https://msdn.microsoft.com/library/ms182776.aspx
[tinyint]: https://msdn.microsoft.com/library/ms187745.aspx
[uniqueidentifier]: https://msdn.microsoft.com/library/ms187942.aspx
[varbinary]: https://msdn.microsoft.com/library/ms188362.aspx
[varchar]: https://msdn.microsoft.com/library/ms186939.aspx
[xml]: https://msdn.microsoft.com/library/ms187339.aspx
[user defined types]: https://msdn.microsoft.com/library/ms131694.aspx
