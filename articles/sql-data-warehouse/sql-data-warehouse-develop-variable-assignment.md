---
title: "variáveis de aaaAssign no SQL Data Warehouse | Microsoft Docs"
description: "Dicas para atribuir variáveis de Transact-SQL no Azure SQL Data Warehouse para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 81ddc7cf-a6ba-4585-91a3-b6ea50f49227
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9de48739bb0af80ff2a117704b31512c680f78d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="assign-variables-in-sql-data-warehouse"></a><span data-ttu-id="090f8-103">Atribuir variáveis no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="090f8-103">Assign variables in SQL Data Warehouse</span></span>
<span data-ttu-id="090f8-104">Variáveis no SQL Data Warehouse são definidas usando Olá `DECLARE` instrução ou hello `SET` instrução.</span><span class="sxs-lookup"><span data-stu-id="090f8-104">Variables in SQL Data Warehouse are set using hello `DECLARE` statement or hello `SET` statement.</span></span>

<span data-ttu-id="090f8-105">Olá seguinte são maneiras válidas perfeitamente tooset um valor de variável:</span><span class="sxs-lookup"><span data-stu-id="090f8-105">All of hello following are perfectly valid ways tooset a variable value:</span></span>

## <a name="setting-variables-with-declare"></a><span data-ttu-id="090f8-106">Definição de variáveis com DECLARE</span><span class="sxs-lookup"><span data-stu-id="090f8-106">Setting variables with DECLARE</span></span>
<span data-ttu-id="090f8-107">Inicializando variáveis com DECLARE é um dos tooset de maneiras mais flexível Olá um valor da variável no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="090f8-107">Initializing variables with DECLARE is one of hello most flexible ways tooset a variable value in SQL Data Warehouse.</span></span>

```sql
DECLARE @v  int = 0
;
```

<span data-ttu-id="090f8-108">Você também pode usar DECLARE tooset mais de uma variável de cada vez.</span><span class="sxs-lookup"><span data-stu-id="090f8-108">You can also use DECLARE tooset more than one variable at a time.</span></span> <span data-ttu-id="090f8-109">Não é possível usar `SELECT` ou `UPDATE` toodo isso:</span><span class="sxs-lookup"><span data-stu-id="090f8-109">You cannot use `SELECT` or `UPDATE` toodo this:</span></span>

```sql
DECLARE @v  INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Smith')
,       @v1 INT = (SELECT TOP 1 c_customer_sk FROM Customer where c_last_name = 'Jones')
;
```

<span data-ttu-id="090f8-110">Você não pode inicializar e usar uma variável em Olá mesma instrução DECLARE.</span><span class="sxs-lookup"><span data-stu-id="090f8-110">You cannot initialise and use a variable in hello same DECLARE statement.</span></span> <span data-ttu-id="090f8-111">tooillustrate Olá ponto Olá exemplo a seguir é **não** permitido como @p1 é inicializado e usado em Olá mesma instrução DECLARE.</span><span class="sxs-lookup"><span data-stu-id="090f8-111">tooillustrate hello point hello example below is **not** allowed as @p1 is both initialized and used in hello same DECLARE statement.</span></span> <span data-ttu-id="090f8-112">Isso resultará em um erro.</span><span class="sxs-lookup"><span data-stu-id="090f8-112">This will result in an error.</span></span>

```sql
DECLARE @p1 int = 0
,       @p2 int = (SELECT COUNT (*) FROM sys.types where is_user_defined = @p1 )
;
```

## <a name="setting-values-with-set"></a><span data-ttu-id="090f8-113">Definição de valores com SET</span><span class="sxs-lookup"><span data-stu-id="090f8-113">Setting values with SET</span></span>
<span data-ttu-id="090f8-114">O SET é um método muito comum para definir uma variável.</span><span class="sxs-lookup"><span data-stu-id="090f8-114">Set is a very common method for setting a single variable.</span></span>

<span data-ttu-id="090f8-115">Todos os exemplos de saudação abaixo são maneiras válidas de configuração de uma variável com o conjunto:</span><span class="sxs-lookup"><span data-stu-id="090f8-115">All of hello examples below are valid ways of setting a variable with SET:</span></span>

```sql
SET     @v = (Select max(database_id) from sys.databases);
SET     @v = 1;
SET     @v = @v+1;
SET     @v +=1;
```

<span data-ttu-id="090f8-116">Você só pode definir uma variável por vez com SET.</span><span class="sxs-lookup"><span data-stu-id="090f8-116">You can only set one variable at a time with SET.</span></span> <span data-ttu-id="090f8-117">No entanto, como pode ser visto acima, são permitidos operadores compostos.</span><span class="sxs-lookup"><span data-stu-id="090f8-117">However, as can be seen above compound operators are permissable.</span></span>

## <a name="limitations"></a><span data-ttu-id="090f8-118">Limitações</span><span class="sxs-lookup"><span data-stu-id="090f8-118">Limitations</span></span>
<span data-ttu-id="090f8-119">Você não pode usar SELECT ou UPDATE para atribuição de variáveis.</span><span class="sxs-lookup"><span data-stu-id="090f8-119">You cannot use SELECT or UPDATE for variable assignment.</span></span>

## <a name="next-steps"></a><span data-ttu-id="090f8-120">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="090f8-120">Next steps</span></span>
<span data-ttu-id="090f8-121">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="090f8-121">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
