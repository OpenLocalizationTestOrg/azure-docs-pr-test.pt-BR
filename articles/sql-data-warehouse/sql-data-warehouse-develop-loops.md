---
title: Utilizar loops T-SQL no Azure SQL Data Warehouse | Microsoft Docs
description: "Dicas para execução de loops do Transact_SQL e substituição de cursores no SQL Data Warehouse Azure para desenvolver soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: f3384b81-b943-431b-bc73-90e47e4c195f
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 40a872ff310f48bfd543ac184fe7301b85b50258
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="1eb8b-103">Executar loops no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1eb8b-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="1eb8b-104">O SQL Data Warehouse oferece suporte ao loop [WHILE][WHILE] para executar repetidamente blocos de instrução.</span><span class="sxs-lookup"><span data-stu-id="1eb8b-104">SQL Data Warehouse supports the [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="1eb8b-105">Isso continuará enquanto as condições especificadas forem verdadeiras ou até que o código especificamente encerre o loop usando a palavra-chave `BREAK` .</span><span class="sxs-lookup"><span data-stu-id="1eb8b-105">This will continue for as long as the specified conditions are true or until the code specifically terminates the loop using the `BREAK` keyword.</span></span> <span data-ttu-id="1eb8b-106">A execução de loops é particularmente útil para a substituição de cursores definidos no código SQL.</span><span class="sxs-lookup"><span data-stu-id="1eb8b-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="1eb8b-107">Felizmente, quase todos os cursores que são escritos em código SQL são do tipo somente leitura de avanço rápido.</span><span class="sxs-lookup"><span data-stu-id="1eb8b-107">Fortunately, almost all cursors that are written in SQL code are of the fast forward, read only variety.</span></span> <span data-ttu-id="1eb8b-108">Portanto, a execução de loops [WHILE] é uma ótima alternativa se você precisar substituir um.</span><span class="sxs-lookup"><span data-stu-id="1eb8b-108">Therefore [WHILE] loops are a great alternative if you find yourself having to replace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="1eb8b-109">Aproveitando a execução de loops e substituindo cursores no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1eb8b-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="1eb8b-110">No entanto, antes de mergulhar na memória, primeiro você deve fazer a seguinte pergunta: “Esse cursor poderia ser reescrito para usar operações baseadas em conjunto?”.</span><span class="sxs-lookup"><span data-stu-id="1eb8b-110">However, before diving in head first you should ask yourself the following question: "Could this cursor be re-written to use set based operations?".</span></span> <span data-ttu-id="1eb8b-111">Em muitos casos, a resposta será “Sim” e geralmente esta será a melhor abordagem.</span><span class="sxs-lookup"><span data-stu-id="1eb8b-111">In many cases the answer will be yes and is often the best approach.</span></span> <span data-ttu-id="1eb8b-112">Uma operação baseada em conjunto geralmente terá um desempenho consideravelmente mais rápido do que uma abordagem iterativa de linha por linha.</span><span class="sxs-lookup"><span data-stu-id="1eb8b-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="1eb8b-113">Os cursores somente leitura de avanço rápido podem ser facilmente substituídos por um constructo de looping.</span><span class="sxs-lookup"><span data-stu-id="1eb8b-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="1eb8b-114">Veja abaixo um exemplo simples.</span><span class="sxs-lookup"><span data-stu-id="1eb8b-114">Below is a simple example.</span></span> <span data-ttu-id="1eb8b-115">Este exemplo de código atualiza as estatísticas para cada tabela no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1eb8b-115">This code example updates the statistics for every table in the database.</span></span> <span data-ttu-id="1eb8b-116">Iterando sobre as tabelas no loop somos capazes de executar cada comando em sequência.</span><span class="sxs-lookup"><span data-stu-id="1eb8b-116">By iterating over the tables in the loop we are able to execute each command in sequence.</span></span>

<span data-ttu-id="1eb8b-117">Primeiro, crie uma tabela temporária que contém um número de linha exclusivo usado para identificar as instruções individuais:</span><span class="sxs-lookup"><span data-stu-id="1eb8b-117">First, create a temporary table containing a unique row number used to identify the individual statements:</span></span>

```
CREATE TABLE #tbl
WITH
( DISTRIBUTION = ROUND_ROBIN
)
AS
SELECT  ROW_NUMBER() OVER(ORDER BY (SELECT NULL)) AS Sequence
,       [name]
,       'UPDATE STATISTICS '+QUOTENAME([name]) AS sql_code
FROM    sys.tables
;
```

<span data-ttu-id="1eb8b-118">Em segundo lugar, inicialize as variáveis necessárias para executar o loop:</span><span class="sxs-lookup"><span data-stu-id="1eb8b-118">Second, initialize the variables required to perform the loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="1eb8b-119">Agora, execute um loop sobre as instruções para executar uma por vez:</span><span class="sxs-lookup"><span data-stu-id="1eb8b-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="1eb8b-120">Finalmente, descarte a tabela temporária criada na primeira etapa</span><span class="sxs-lookup"><span data-stu-id="1eb8b-120">Finally drop the temporary table created in the first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links to the next logical set of content to keep the customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="1eb8b-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1eb8b-121">Next steps</span></span>
<span data-ttu-id="1eb8b-122">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="1eb8b-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
<span data-ttu-id="1eb8b-123">[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx</span><span class="sxs-lookup"><span data-stu-id="1eb8b-123">[WHILE]: https://msdn.microsoft.com/library/ms178642.aspx</span></span>


<!--Other Web references-->
