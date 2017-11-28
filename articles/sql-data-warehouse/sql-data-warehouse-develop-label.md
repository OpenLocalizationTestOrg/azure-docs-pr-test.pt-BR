---
title: "Usar rótulos para consultas de instrumento no SQL Data Warehouse | Microsoft Docs"
description: "Dicas para usar rótulos para consultas de instrumento no SQL Data Warehouse do Azure para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: 44988de8-04c1-4fed-92be-e1935661a4e8
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: queries
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: 9e75bbe528a427724a623305fbd45e2277e9d0af
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-labels-to-instrument-queries-in-sql-data-warehouse"></a><span data-ttu-id="8fad8-103">Usar rótulos para consultas de instrumento no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="8fad8-103">Use labels to instrument queries in SQL Data Warehouse</span></span>
<span data-ttu-id="8fad8-104">O SQL Data Warehouse oferece suporte a um conceito chamado rótulos de consulta.</span><span class="sxs-lookup"><span data-stu-id="8fad8-104">SQL Data Warehouse supports a concept called query labels.</span></span> <span data-ttu-id="8fad8-105">Antes de entrar em qualquer profundidade, vamos examinar um exemplo:</span><span class="sxs-lookup"><span data-stu-id="8fad8-105">Before going into any depth let's look at an example of one:</span></span>

```sql
SELECT *
FROM sys.tables
OPTION (LABEL = 'My Query Label')
;
```

<span data-ttu-id="8fad8-106">Essa última linha marca a cadeia de caracteres ‘Meu Rótulo de Consulta’ à consulta.</span><span class="sxs-lookup"><span data-stu-id="8fad8-106">This last line tags the string 'My Query Label' to the query.</span></span> <span data-ttu-id="8fad8-107">Isso é particularmente útil, pois o rótulo é capaz de executar consultas por meio de DMVs.</span><span class="sxs-lookup"><span data-stu-id="8fad8-107">This is particularly helpful as the label is query-able through the DMVs.</span></span> <span data-ttu-id="8fad8-108">Isso fornece um mecanismo para rastrear consultas de problemas e também para ajudar a identificar o andamento por meio de uma execução ETL.</span><span class="sxs-lookup"><span data-stu-id="8fad8-108">This provides us with a mechanism to track down problem queries and also to help identify progress through an ETL run.</span></span>

<span data-ttu-id="8fad8-109">Uma boa convenção de nomenclatura ajuda muito aqui.</span><span class="sxs-lookup"><span data-stu-id="8fad8-109">A good naming convention really helps here.</span></span> <span data-ttu-id="8fad8-110">Por exemplo, algo como ‘ PROJECT : PROCEDURE : STATEMENT : COMMENT’ ajudaria para identificar exclusivamente a consulta entre todos os códigos no controle de origem.</span><span class="sxs-lookup"><span data-stu-id="8fad8-110">For example something like ' PROJECT : PROCEDURE : STATEMENT : COMMENT' would help to uniquely identify the query in amongst all the code in source control.</span></span>

<span data-ttu-id="8fad8-111">Para pesquisar por rótulo, você pode usar a consulta a seguir que usa os modos de exibição de gerenciamento dinâmico:</span><span class="sxs-lookup"><span data-stu-id="8fad8-111">To search by label you can use the following query that uses the dynamic management views:</span></span>

```sql
SELECT  *
FROM    sys.dm_pdw_exec_requests r
WHERE   r.[label] = 'My Query Label'
;
```

> [!NOTE]
> <span data-ttu-id="8fad8-112">É essencial encapsular colchetes ou aspas duplas em torno da palavra do rótulo ao consultar.</span><span class="sxs-lookup"><span data-stu-id="8fad8-112">It is essential that you wrap square brackets or double quotes around the word label when querying.</span></span> <span data-ttu-id="8fad8-113">Rótulo é uma palavra reservada e causará um erro se não for delimitada.</span><span class="sxs-lookup"><span data-stu-id="8fad8-113">Label is a reserved word and will caused an error if it has not been delimited.</span></span>
> 
> 

## <a name="next-steps"></a><span data-ttu-id="8fad8-114">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8fad8-114">Next steps</span></span>
<span data-ttu-id="8fad8-115">Para obter mais dicas de desenvolvimento, confira [visão geral de desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="8fad8-115">For more development tips, see [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[development overview]: sql-data-warehouse-overview-develop.md

<!--MSDN references-->

<!--Other Web references-->
