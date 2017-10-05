---
title: Recursos para o desenvolvimento de um data warehouse no Azure | Microsoft Docs
description: "Conceitos de desenvolvimento, decisões de design, recomendações e técnicas de codificação para o SQL Data Warehouse."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: barbkess
editor: 
ms.assetid: 996e3afc-c21c-4e21-b9df-997f953f6dfd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: develop
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: b85a4f09e561e429aa5bf46ec680014487fb40c7
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="ae266-103">Decisões de design e técnicas de codificação para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="ae266-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="ae266-104">Dê uma olhada nesses artigos sobre desenvolvimento para entender melhor as principais decisões de design, recomendações e técnicas de codificação para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ae266-104">Take a look through these development articles to better understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="ae266-105">Principais decisões de design</span><span class="sxs-lookup"><span data-stu-id="ae266-105">Key design decisions</span></span>
<span data-ttu-id="ae266-106">Os artigos a seguir destacam alguns dos principais conceitos e as decisões de design que você precisará entender para desenvolver seu data warehouse distribuído usando o SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="ae266-106">The following articles highlight some of the key concepts and design decisions you will need to understand for the development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="ae266-107">[conexões][connections]</span><span class="sxs-lookup"><span data-stu-id="ae266-107">[connections][connections]</span></span>
* <span data-ttu-id="ae266-108">[simultaneidade][concurrency]</span><span class="sxs-lookup"><span data-stu-id="ae266-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="ae266-109">[transações][transactions]</span><span class="sxs-lookup"><span data-stu-id="ae266-109">[transactions][transactions]</span></span>
* <span data-ttu-id="ae266-110">[esquemas definidos pelo usuário][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="ae266-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="ae266-111">[distribuição de tabelas][table distribution]</span><span class="sxs-lookup"><span data-stu-id="ae266-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="ae266-112">[índices da tabela][table indexes]</span><span class="sxs-lookup"><span data-stu-id="ae266-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="ae266-113">[partições da tabela][table partitions]</span><span class="sxs-lookup"><span data-stu-id="ae266-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="ae266-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="ae266-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="ae266-115">[estatísticas][statistics]</span><span class="sxs-lookup"><span data-stu-id="ae266-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="ae266-116">Recomendações para o desenvolvimento e técnicas de codificação</span><span class="sxs-lookup"><span data-stu-id="ae266-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="ae266-117">Esses artigos realçam as técnicas de codificação específicas, dicas e recomendações para o desenvolvimento de seu SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="ae266-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="ae266-118">[procedimentos armazenados][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="ae266-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="ae266-119">[rótulos][labels]</span><span class="sxs-lookup"><span data-stu-id="ae266-119">[labels][labels]</span></span>
* <span data-ttu-id="ae266-120">[modos de exibição][views]</span><span class="sxs-lookup"><span data-stu-id="ae266-120">[views][views]</span></span>
* <span data-ttu-id="ae266-121">[tabelas temporárias][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="ae266-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="ae266-122">[SQL dinâmico][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="ae266-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="ae266-123">[looping][looping]</span><span class="sxs-lookup"><span data-stu-id="ae266-123">[looping][looping]</span></span>
* <span data-ttu-id="ae266-124">[agrupar por opções][group by options]</span><span class="sxs-lookup"><span data-stu-id="ae266-124">[group by options][group by options]</span></span>
* <span data-ttu-id="ae266-125">[atribuição de variável][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="ae266-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="ae266-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ae266-126">Next steps</span></span>
<span data-ttu-id="ae266-127">Após a leitura dos artigos de desenvolvimento, confira a página [Referência a Transact-SQL][Transact-SQL reference] para obter mais detalhes sobre a sintaxe com suporte para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="ae266-127">Once you have been through the development articles take a look through the [Transact-SQL reference][Transact-SQL reference] page for more details on the supported syntax for SQL Data Warehouse.</span></span>

<!--Image references-->

<!--Article references-->
[concurrency]: ./sql-data-warehouse-develop-concurrency.md
[connections]: ./sql-data-warehouse-connect-overview.md
[CTAS]: ./sql-data-warehouse-develop-ctas.md
[dynamic SQL]: ./sql-data-warehouse-develop-dynamic-sql.md
[group by options]: ./sql-data-warehouse-develop-group-by-options.md
[labels]: ./sql-data-warehouse-develop-label.md
[looping]: ./sql-data-warehouse-develop-loops.md
[statistics]: ./sql-data-warehouse-tables-statistics.md
[stored procedures]: ./sql-data-warehouse-develop-stored-procedures.md
[table distribution]: ./sql-data-warehouse-tables-distribute.md
[table indexes]: ./sql-data-warehouse-tables-index.md
[table partitions]: ./sql-data-warehouse-tables-partition.md
[temporary tables]: ./sql-data-warehouse-tables-temporary.md
[transactions]: ./sql-data-warehouse-develop-transactions.md
[user-defined schemas]: ./sql-data-warehouse-develop-user-defined-schemas.md
[variable assignment]: ./sql-data-warehouse-develop-variable-assignment.md
[views]: ./sql-data-warehouse-develop-views.md
[Transact-SQL reference]: ./sql-data-warehouse-overview-reference.md

<!--MSDN references-->
[renaming objects]: https://msdn.microsoft.com/library/mt631611.aspx

<!--Other Web references-->
