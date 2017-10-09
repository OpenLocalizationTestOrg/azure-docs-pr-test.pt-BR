---
title: aaaResources para o desenvolvimento de um data warehouse no Azure | Microsoft Docs
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
ms.openlocfilehash: 67e3a6a3e2664919c3445ea5d5eba251054de020
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="design-decisions-and-coding-techniques-for-sql-data-warehouse"></a><span data-ttu-id="04d2f-103">Decisões de design e técnicas de codificação para o SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="04d2f-103">Design decisions and coding techniques for SQL Data Warehouse</span></span>
<span data-ttu-id="04d2f-104">Examine esses artigos de desenvolvimento toobetter entender principais decisões de design, as recomendações e as técnicas de codificação para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="04d2f-104">Take a look through these development articles toobetter understand key design decisions, recommendations and coding techniques for SQL Data Warehouse.</span></span>

## <a name="key-design-decisions"></a><span data-ttu-id="04d2f-105">Principais decisões de design</span><span class="sxs-lookup"><span data-stu-id="04d2f-105">Key design decisions</span></span>
<span data-ttu-id="04d2f-106">Olá artigos a seguir realçam alguns dos principais conceitos de saudação e decisões de design, que você precisará toounderstand para desenvolvimento de saudação do distributed data warehouse usando o SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="04d2f-106">hello following articles highlight some of hello key concepts and design decisions you will need toounderstand for hello development of your distributed data warehouse using SQL Data Warehouse:</span></span>

* <span data-ttu-id="04d2f-107">[conexões][connections]</span><span class="sxs-lookup"><span data-stu-id="04d2f-107">[connections][connections]</span></span>
* <span data-ttu-id="04d2f-108">[simultaneidade][concurrency]</span><span class="sxs-lookup"><span data-stu-id="04d2f-108">[concurrency][concurrency]</span></span>
* <span data-ttu-id="04d2f-109">[transações][transactions]</span><span class="sxs-lookup"><span data-stu-id="04d2f-109">[transactions][transactions]</span></span>
* <span data-ttu-id="04d2f-110">[esquemas definidos pelo usuário][user-defined schemas]</span><span class="sxs-lookup"><span data-stu-id="04d2f-110">[user-defined schemas][user-defined schemas]</span></span>
* <span data-ttu-id="04d2f-111">[distribuição de tabelas][table distribution]</span><span class="sxs-lookup"><span data-stu-id="04d2f-111">[table distribution][table distribution]</span></span>
* <span data-ttu-id="04d2f-112">[índices da tabela][table indexes]</span><span class="sxs-lookup"><span data-stu-id="04d2f-112">[table indexes][table indexes]</span></span>
* <span data-ttu-id="04d2f-113">[partições da tabela][table partitions]</span><span class="sxs-lookup"><span data-stu-id="04d2f-113">[table partitions][table partitions]</span></span>
* <span data-ttu-id="04d2f-114">[CTAS][CTAS]</span><span class="sxs-lookup"><span data-stu-id="04d2f-114">[CTAS][CTAS]</span></span>
* <span data-ttu-id="04d2f-115">[estatísticas][statistics]</span><span class="sxs-lookup"><span data-stu-id="04d2f-115">[statistics][statistics]</span></span>

## <a name="development-recommendations-and-coding-techniques"></a><span data-ttu-id="04d2f-116">Recomendações para o desenvolvimento e técnicas de codificação</span><span class="sxs-lookup"><span data-stu-id="04d2f-116">Development recommendations and coding techniques</span></span>
<span data-ttu-id="04d2f-117">Esses artigos realçam as técnicas de codificação específicas, dicas e recomendações para o desenvolvimento de seu SQL Data Warehouse:</span><span class="sxs-lookup"><span data-stu-id="04d2f-117">These articles highlight specific coding techniques, tips and recommendations for developing your SQL Data Warehouse:</span></span>

* <span data-ttu-id="04d2f-118">[procedimentos armazenados][stored procedures]</span><span class="sxs-lookup"><span data-stu-id="04d2f-118">[stored procedures][stored procedures]</span></span>
* <span data-ttu-id="04d2f-119">[rótulos][labels]</span><span class="sxs-lookup"><span data-stu-id="04d2f-119">[labels][labels]</span></span>
* <span data-ttu-id="04d2f-120">[modos de exibição][views]</span><span class="sxs-lookup"><span data-stu-id="04d2f-120">[views][views]</span></span>
* <span data-ttu-id="04d2f-121">[tabelas temporárias][temporary tables]</span><span class="sxs-lookup"><span data-stu-id="04d2f-121">[temporary tables][temporary tables]</span></span>
* <span data-ttu-id="04d2f-122">[SQL dinâmico][dynamic SQL]</span><span class="sxs-lookup"><span data-stu-id="04d2f-122">[dynamic SQL][dynamic SQL]</span></span>
* <span data-ttu-id="04d2f-123">[looping][looping]</span><span class="sxs-lookup"><span data-stu-id="04d2f-123">[looping][looping]</span></span>
* <span data-ttu-id="04d2f-124">[agrupar por opções][group by options]</span><span class="sxs-lookup"><span data-stu-id="04d2f-124">[group by options][group by options]</span></span>
* <span data-ttu-id="04d2f-125">[atribuição de variável][variable assignment]</span><span class="sxs-lookup"><span data-stu-id="04d2f-125">[variable assignment][variable assignment]</span></span>

## <a name="next-steps"></a><span data-ttu-id="04d2f-126">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="04d2f-126">Next steps</span></span>
<span data-ttu-id="04d2f-127">Depois de você ter sido por meio de artigos de desenvolvimento Olá dê uma olhada Olá [referência Transact-SQL] [ Transact-SQL reference] para obter mais detalhes sobre a sintaxe de saudação com suporte para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="04d2f-127">Once you have been through hello development articles take a look through hello [Transact-SQL reference][Transact-SQL reference] page for more details on hello supported syntax for SQL Data Warehouse.</span></span>

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
