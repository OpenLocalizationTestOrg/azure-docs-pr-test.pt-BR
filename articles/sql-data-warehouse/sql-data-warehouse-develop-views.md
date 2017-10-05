---
title: "Usando exibições do T-SQL no Azure SQL Data Warehouse | Microsoft Docs"
description: "Dicas para usar exibições Transact-SQL no Azure SQL Data Warehouse para desenvolvimento de soluções."
services: sql-data-warehouse
documentationcenter: NA
author: jrowlandjones
manager: jhubbard
editor: 
ms.assetid: b5208f32-8f4a-4056-8788-2adbb253d9fd
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: t-sql
ms.date: 10/31/2016
ms.author: jrj;barbkess
ms.openlocfilehash: d2a03be810bd7f792876607ec735eb578b65a3b5
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="426a4-103">Modos de exibição no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="426a4-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="426a4-104">Os modos de exibição são particularmente úteis no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="426a4-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="426a4-105">Eles podem ser usados em diversas maneiras diferentes de melhorar a qualidade de sua solução.</span><span class="sxs-lookup"><span data-stu-id="426a4-105">They can be used in a number of different ways to improve the quality of your solution.</span></span>  <span data-ttu-id="426a4-106">Este artigo destaca alguns exemplos de como aprimorar sua solução com exibições, bem como as limitações que precisam ser consideradas.</span><span class="sxs-lookup"><span data-stu-id="426a4-106">This article highlights a few examples of how to enrich your solution with views, as well as the limitations that need to be considered.</span></span>

> [!NOTE]
> <span data-ttu-id="426a4-107">A sintaxe para `CREATE VIEW` não é discutida neste artigo.</span><span class="sxs-lookup"><span data-stu-id="426a4-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="426a4-108">Consulte o artigo [CREATE VIEW][CREATE VIEW] no MSDN para obter essas informações de referência.</span><span class="sxs-lookup"><span data-stu-id="426a4-108">Please refer to the [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="426a4-109">Abstração de arquitetura</span><span class="sxs-lookup"><span data-stu-id="426a4-109">Architectural abstraction</span></span>
<span data-ttu-id="426a4-110">Um padrão de aplicativo muito comum é recriar tabelas usando CREATE TABLE AS SELECT (CTAS) seguido por um objeto de renomeação do padrão durante o carregamento dos dados.</span><span class="sxs-lookup"><span data-stu-id="426a4-110">A very common application pattern is to re-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="426a4-111">O exemplo a seguir adiciona novos registros de data para uma dimensão de data.</span><span class="sxs-lookup"><span data-stu-id="426a4-111">The example below adds new date records to a date dimension.</span></span> <span data-ttu-id="426a4-112">Observe como uma nova tabela, DimDate_New, é criada pela primeira vez e renomeada para substituir a versão original da tabela.</span><span class="sxs-lookup"><span data-stu-id="426a4-112">Note how a new tabble, DimDate_New, is first created and then renamed to replace the original version of the table.</span></span>

```sql
CREATE TABLE dbo.DimDate_New
WITH (DISTRIBUTION = ROUND_ROBIN
, CLUSTERED INDEX (DateKey ASC)
)
AS
SELECT *
FROM   dbo.DimDate  AS prod
UNION ALL
SELECT *
FROM   dbo.DimDate_stg AS stg
;

RENAME OBJECT DimDate TO DimDate_Old;
RENAME OBJECT DimDate_New TO DimDate;

```

<span data-ttu-id="426a4-113">No entanto, essa abordagem pode resultar em tabelas que aparecem e desaparecem da exibição do usuário, bem como nas mensagens de erro "a tabela não existe".</span><span class="sxs-lookup"><span data-stu-id="426a4-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="426a4-114">As exibições podem ser usadas para fornecer aos usuários uma camada de apresentação consistente enquanto os objetos subjacentes são renomeados.</span><span class="sxs-lookup"><span data-stu-id="426a4-114">Views can be used to provide users with a consistent presentation layer whilst the underlying objects are renamed.</span></span> <span data-ttu-id="426a4-115">Fornecer aos usuários o acesso aos dados através de uma exibição significa que os usuários não precisam ter visibilidade das tabelas subjacentes.</span><span class="sxs-lookup"><span data-stu-id="426a4-115">By providing users access to the data through a views, means users don't need to have visibility of the underlying tables.</span></span> <span data-ttu-id="426a4-116">Isso fornece uma experiência de usuário consistente enquanto garante que os designers do data warehouse podem aprimorar o modelo de dados e maximizar o desempenho usando o CTAS durante o processo de carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="426a4-116">This provides a consistent user experience while ensuring that the data warehouse designers can evolve the data model and maximize performance by using CTAS during the data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="426a4-117">Otimização do desempenho</span><span class="sxs-lookup"><span data-stu-id="426a4-117">Performance optimization</span></span>
<span data-ttu-id="426a4-118">As exibições também podem ser utilizadas para impor junções de desempenho otimizadas entre as tabelas.</span><span class="sxs-lookup"><span data-stu-id="426a4-118">Views can also be utilized to enforce performance optimized joins between tables.</span></span> <span data-ttu-id="426a4-119">Por exemplo, uma exibição pode incorporar uma chave de distribuição redundante como parte dos critérios de junção para minimizar a movimentação dos dados.</span><span class="sxs-lookup"><span data-stu-id="426a4-119">For example, a view can incorporate a redundant distribution key as part of the joining criteria to minimize data movement.</span></span>  <span data-ttu-id="426a4-120">Outro benefício de uma exibição pode ser forçar uma dica de consulta ou junção específica.</span><span class="sxs-lookup"><span data-stu-id="426a4-120">Another benefit of a view could be to force a specific query or joining hint.</span></span> <span data-ttu-id="426a4-121">Usar exibições dessa maneira garante que as junções sempre sejam executadas de forma ideal, evitando a necessidade dos usuários lembrarem a construção correta de suas junções.</span><span class="sxs-lookup"><span data-stu-id="426a4-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding the need for users to remember the correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="426a4-122">Limitações</span><span class="sxs-lookup"><span data-stu-id="426a4-122">Limitations</span></span>
<span data-ttu-id="426a4-123">Os modos de exibição no SQL Data Warehouse são somente metadados.</span><span class="sxs-lookup"><span data-stu-id="426a4-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="426a4-124">Consequentemente, as opções a seguir não estão disponíveis:</span><span class="sxs-lookup"><span data-stu-id="426a4-124">Consequently the following options are not available:</span></span>

* <span data-ttu-id="426a4-125">Não há opção de associação de esquema</span><span class="sxs-lookup"><span data-stu-id="426a4-125">There is no schema binding option</span></span>
* <span data-ttu-id="426a4-126">Tabelas base não podem ser atualizadas por meio da exibição</span><span class="sxs-lookup"><span data-stu-id="426a4-126">Base tables cannot be updated through the view</span></span>
* <span data-ttu-id="426a4-127">Exibições não podem ser criadas em tabelas temporárias</span><span class="sxs-lookup"><span data-stu-id="426a4-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="426a4-128">Não há suporte para as dicas EXPAND / NOEXPAND</span><span class="sxs-lookup"><span data-stu-id="426a4-128">There is no support for the EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="426a4-129">não há exibições indexadas no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="426a4-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="426a4-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="426a4-130">Next steps</span></span>
<span data-ttu-id="426a4-131">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="426a4-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="426a4-132">Para ver a sintaxe `CREATE VIEW` , consulte [CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="426a4-132">For `CREATE VIEW` syntax please refer to [CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
