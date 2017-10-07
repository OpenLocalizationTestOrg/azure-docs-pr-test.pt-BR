---
title: aaaLeverage loops de T-SQL no SQL Data Warehouse do Azure | Microsoft Docs
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
ms.openlocfilehash: c7e8f71b910d00d0dfc30f6e5eba190fd05014b3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="loops-in-sql-data-warehouse"></a><span data-ttu-id="1f8e1-103">Executar loops no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1f8e1-103">Loops in SQL Data Warehouse</span></span>
<span data-ttu-id="1f8e1-104">SQL Data Warehouse dá suporte a saudação [ENQUANTO][ENQUANTO] loop para repetidamente executar blocos de instrução.</span><span class="sxs-lookup"><span data-stu-id="1f8e1-104">SQL Data Warehouse supports hello [WHILE][WHILE] loop for repeatedly executing statement blocks.</span></span> <span data-ttu-id="1f8e1-105">Isso continuará para como Olá especificado condições forem verdadeiras, ou até que o código Olá finaliza especificamente loop de hello usando Olá `BREAK` palavra-chave.</span><span class="sxs-lookup"><span data-stu-id="1f8e1-105">This will continue for as long as hello specified conditions are true or until hello code specifically terminates hello loop using hello `BREAK` keyword.</span></span> <span data-ttu-id="1f8e1-106">A execução de loops é particularmente útil para a substituição de cursores definidos no código SQL.</span><span class="sxs-lookup"><span data-stu-id="1f8e1-106">Loops are particularly useful for replacing cursors defined in SQL code.</span></span> <span data-ttu-id="1f8e1-107">Felizmente, quase todos os cursores que são escritos em código SQL são de saudação rápida, leitura apenas variedade.</span><span class="sxs-lookup"><span data-stu-id="1f8e1-107">Fortunately, almost all cursors that are written in SQL code are of hello fast forward, read only variety.</span></span> <span data-ttu-id="1f8e1-108">Portanto, [ENQUANTO] loops são uma excelente alternativa, se você estiver tendo tooreplace um.</span><span class="sxs-lookup"><span data-stu-id="1f8e1-108">Therefore [WHILE] loops are a great alternative if you find yourself having tooreplace one.</span></span>

## <a name="leveraging-loops-and-replacing-cursors-in-sql-data-warehouse"></a><span data-ttu-id="1f8e1-109">Aproveitando a execução de loops e substituindo cursores no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="1f8e1-109">Leveraging loops and replacing cursors in SQL Data Warehouse</span></span>
<span data-ttu-id="1f8e1-110">No entanto, antes de se aprofundar no cabeçalho primeiro você deve estar se perguntando Olá seguinte pergunta: "foi gravado nesse cursor toouse operações baseadas em conjunto?".</span><span class="sxs-lookup"><span data-stu-id="1f8e1-110">However, before diving in head first you should ask yourself hello following question: "Could this cursor be re-written toouse set based operations?".</span></span> <span data-ttu-id="1f8e1-111">Em muitos casos resposta Olá será Sim e é geralmente a melhor abordagem de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f8e1-111">In many cases hello answer will be yes and is often hello best approach.</span></span> <span data-ttu-id="1f8e1-112">Uma operação baseada em conjunto geralmente terá um desempenho consideravelmente mais rápido do que uma abordagem iterativa de linha por linha.</span><span class="sxs-lookup"><span data-stu-id="1f8e1-112">A set based operation often performs significantly faster than an iterative, row by row approach.</span></span>

<span data-ttu-id="1f8e1-113">Os cursores somente leitura de avanço rápido podem ser facilmente substituídos por um constructo de looping.</span><span class="sxs-lookup"><span data-stu-id="1f8e1-113">Fast forward read-only cursors can be easily replaced with a looping construct.</span></span> <span data-ttu-id="1f8e1-114">Veja abaixo um exemplo simples.</span><span class="sxs-lookup"><span data-stu-id="1f8e1-114">Below is a simple example.</span></span> <span data-ttu-id="1f8e1-115">Este exemplo de código atualiza estatísticas de saudação para cada tabela no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1f8e1-115">This code example updates hello statistics for every table in hello database.</span></span> <span data-ttu-id="1f8e1-116">Pela iteração em tabelas de saudação em loop Olá nós é tooexecute capaz de cada comando em sequência.</span><span class="sxs-lookup"><span data-stu-id="1f8e1-116">By iterating over hello tables in hello loop we are able tooexecute each command in sequence.</span></span>

<span data-ttu-id="1f8e1-117">Primeiro, crie uma tabela temporária que contém uma linha exclusiva usada tooidentify Olá individuais instruções de número:</span><span class="sxs-lookup"><span data-stu-id="1f8e1-117">First, create a temporary table containing a unique row number used tooidentify hello individual statements:</span></span>

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

<span data-ttu-id="1f8e1-118">Em segundo lugar, inicialize o loop de Olá Olá variáveis tooperform necessária:</span><span class="sxs-lookup"><span data-stu-id="1f8e1-118">Second, initialize hello variables required tooperform hello loop:</span></span>

```
DECLARE @nbr_statements INT = (SELECT COUNT(*) FROM #tbl)
,       @i INT = 1
;
```

<span data-ttu-id="1f8e1-119">Agora, execute um loop sobre as instruções para executar uma por vez:</span><span class="sxs-lookup"><span data-stu-id="1f8e1-119">Now loop over statements executing them one at a time:</span></span>

```
WHILE   @i <= @nbr_statements
BEGIN
    DECLARE @sql_code NVARCHAR(4000) = (SELECT sql_code FROM #tbl WHERE Sequence = @i);
    EXEC    sp_executesql @sql_code;
    SET     @i +=1;
END
```

<span data-ttu-id="1f8e1-120">Por fim Descartar tabela temporária de saudação criada na primeira etapa de saudação</span><span class="sxs-lookup"><span data-stu-id="1f8e1-120">Finally drop hello temporary table created in hello first step</span></span>

```
DROP TABLE #tbl;
```


<!--Every topic should have next steps and links toohello next logical set of content tookeep hello customer engaged-->

## <a name="next-steps"></a><span data-ttu-id="1f8e1-121">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1f8e1-121">Next steps</span></span>
<span data-ttu-id="1f8e1-122">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="1f8e1-122">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[ENQUANTO]: https://msdn.microsoft.com/library/ms178642.aspx


<!--Other Web references-->
