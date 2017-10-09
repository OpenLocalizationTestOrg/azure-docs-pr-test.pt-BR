---
title: "exibições de aaaUsing T-SQL no Azure SQL Data Warehouse | Microsoft Docs"
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
ms.openlocfilehash: 3990b133946621691bdfa4b09523d21867470c74
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="views-in-sql-data-warehouse"></a><span data-ttu-id="64910-103">Modos de exibição no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="64910-103">Views in SQL Data Warehouse</span></span>
<span data-ttu-id="64910-104">Os modos de exibição são particularmente úteis no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="64910-104">Views are particularly useful in SQL Data Warehouse.</span></span> <span data-ttu-id="64910-105">Eles podem ser usados em um número de qualidade de saudação tooimprove maneiras diferentes de sua solução.</span><span class="sxs-lookup"><span data-stu-id="64910-105">They can be used in a number of different ways tooimprove hello quality of your solution.</span></span>  <span data-ttu-id="64910-106">Este artigo destaca alguns exemplos de como tooenrich sua solução com modos de exibição, bem como limitações Olá que precisam toobe considerados.</span><span class="sxs-lookup"><span data-stu-id="64910-106">This article highlights a few examples of how tooenrich your solution with views, as well as hello limitations that need toobe considered.</span></span>

> [!NOTE]
> <span data-ttu-id="64910-107">A sintaxe para `CREATE VIEW` não é discutida neste artigo.</span><span class="sxs-lookup"><span data-stu-id="64910-107">Syntax for `CREATE VIEW` is not discussed in this article.</span></span> <span data-ttu-id="64910-108">Consulte toohello [CREATE VIEW] [ CREATE VIEW] artigo no MSDN para obter essas informações de referência.</span><span class="sxs-lookup"><span data-stu-id="64910-108">Please refer toohello [CREATE VIEW][CREATE VIEW] article on MSDN for this reference information.</span></span>
> 
> 

## <a name="architectural-abstraction"></a><span data-ttu-id="64910-109">Abstração de arquitetura</span><span class="sxs-lookup"><span data-stu-id="64910-109">Architectural abstraction</span></span>
<span data-ttu-id="64910-110">Um padrão de aplicativo muito comum é toore-criar tabelas usando criar tabela como selecionar (CTAS) seguido por um objeto de renomeação padrão durante o carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="64910-110">A very common application pattern is toore-create tables using CREATE TABLE AS SELECT (CTAS) followed by an object renaming pattern whilst loading data.</span></span>

<span data-ttu-id="64910-111">exemplo Hello abaixo adiciona uma dimensão de data de tooa data novos registros.</span><span class="sxs-lookup"><span data-stu-id="64910-111">hello example below adds new date records tooa date dimension.</span></span> <span data-ttu-id="64910-112">Observe como uma nova tabble, DimDate_New, é criado pela primeira vez e em seguida renomeou versão original do hello tooreplace da tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="64910-112">Note how a new tabble, DimDate_New, is first created and then renamed tooreplace hello original version of hello table.</span></span>

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

RENAME OBJECT DimDate tooDimDate_Old;
RENAME OBJECT DimDate_New tooDimDate;

```

<span data-ttu-id="64910-113">No entanto, essa abordagem pode resultar em tabelas que aparecem e desaparecem da exibição do usuário, bem como nas mensagens de erro "a tabela não existe".</span><span class="sxs-lookup"><span data-stu-id="64910-113">However, this approach can result in tables appearing and disappearing from a user's view as well as "table does not exist" error messages.</span></span> <span data-ttu-id="64910-114">Modos de exibição podem ser usado tooprovide usuários com uma camada de apresentação consistente enquanto objetos subjacentes Olá são renomeados.</span><span class="sxs-lookup"><span data-stu-id="64910-114">Views can be used tooprovide users with a consistent presentation layer whilst hello underlying objects are renamed.</span></span> <span data-ttu-id="64910-115">Fornecendo aos usuários acesso toohello dados por meio de modos de exibição, significa que os usuários não precisam toohave visibilidade de tabelas subjacentes hello.</span><span class="sxs-lookup"><span data-stu-id="64910-115">By providing users access toohello data through a views, means users don't need toohave visibility of hello underlying tables.</span></span> <span data-ttu-id="64910-116">Isso fornece uma experiência de usuário consistente enquanto garante que os designers do data warehouse Olá podem desenvolver um modelo de dados de saudação e maximizar o desempenho usando CTAS durante o processo de carregamento de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="64910-116">This provides a consistent user experience while ensuring that hello data warehouse designers can evolve hello data model and maximize performance by using CTAS during hello data loading process.</span></span>    

## <a name="performance-optimization"></a><span data-ttu-id="64910-117">Otimização do desempenho</span><span class="sxs-lookup"><span data-stu-id="64910-117">Performance optimization</span></span>
<span data-ttu-id="64910-118">Modos de exibição também podem ser utilizadas tooenforce desempenho otimizado junções entre tabelas.</span><span class="sxs-lookup"><span data-stu-id="64910-118">Views can also be utilized tooenforce performance optimized joins between tables.</span></span> <span data-ttu-id="64910-119">Por exemplo, um modo de exibição pode incorporar uma chave de distribuição redundante como parte da saudação ingressar na movimentação de dados de toominimize critérios.</span><span class="sxs-lookup"><span data-stu-id="64910-119">For example, a view can incorporate a redundant distribution key as part of hello joining criteria toominimize data movement.</span></span>  <span data-ttu-id="64910-120">Outro benefício de um modo de exibição pode ser tooforce uma consulta específica ou dica de junção.</span><span class="sxs-lookup"><span data-stu-id="64910-120">Another benefit of a view could be tooforce a specific query or joining hint.</span></span> <span data-ttu-id="64910-121">Usando modos de exibição desta maneira garante que as junções sempre são executadas de maneira ideal, evitando a necessidade de saudação de construção da saudação correto do tooremember usuários para suas associações.</span><span class="sxs-lookup"><span data-stu-id="64910-121">Using views in this manner guarantees that joins are always performed in an optimal fashion avoiding hello need for users tooremember hello correct construct for their joins.</span></span>

## <a name="limitations"></a><span data-ttu-id="64910-122">Limitações</span><span class="sxs-lookup"><span data-stu-id="64910-122">Limitations</span></span>
<span data-ttu-id="64910-123">Os modos de exibição no SQL Data Warehouse são somente metadados.</span><span class="sxs-lookup"><span data-stu-id="64910-123">Views in SQL Data Warehouse are metadata only.</span></span>  <span data-ttu-id="64910-124">Consequentemente, Olá as opções a seguir não está disponível:</span><span class="sxs-lookup"><span data-stu-id="64910-124">Consequently hello following options are not available:</span></span>

* <span data-ttu-id="64910-125">Não há opção de associação de esquema</span><span class="sxs-lookup"><span data-stu-id="64910-125">There is no schema binding option</span></span>
* <span data-ttu-id="64910-126">Tabelas base não podem ser atualizadas por meio do modo de exibição de saudação</span><span class="sxs-lookup"><span data-stu-id="64910-126">Base tables cannot be updated through hello view</span></span>
* <span data-ttu-id="64910-127">Exibições não podem ser criadas em tabelas temporárias</span><span class="sxs-lookup"><span data-stu-id="64910-127">Views cannot be created over temporary tables</span></span>
* <span data-ttu-id="64910-128">Não há suporte para Olá expandir / dicas NOEXPAND</span><span class="sxs-lookup"><span data-stu-id="64910-128">There is no support for hello EXPAND / NOEXPAND hints</span></span>
* <span data-ttu-id="64910-129">não há exibições indexadas no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="64910-129">There are no indexed views in SQL Data Warehouse</span></span>

## <a name="next-steps"></a><span data-ttu-id="64910-130">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="64910-130">Next steps</span></span>
<span data-ttu-id="64910-131">Para obter mais dicas de desenvolvimento, consulte [Visão geral de desenvolvimento do SQL Data Warehouse][SQL Data Warehouse development overview].</span><span class="sxs-lookup"><span data-stu-id="64910-131">For more development tips, see [SQL Data Warehouse development overview][SQL Data Warehouse development overview].</span></span>
<span data-ttu-id="64910-132">Para `CREATE VIEW` sintaxe, consulte muito[CREATE VIEW][CREATE VIEW].</span><span class="sxs-lookup"><span data-stu-id="64910-132">For `CREATE VIEW` syntax please refer too[CREATE VIEW][CREATE VIEW].</span></span>

<!--Image references-->

<!--Article references-->
[SQL Data Warehouse development overview]: ./sql-data-warehouse-overview-develop.md

<!--MSDN references-->
[CREATE VIEW]: https://msdn.microsoft.com/en-us/library/ms187956.aspx

<!--Other Web references-->
