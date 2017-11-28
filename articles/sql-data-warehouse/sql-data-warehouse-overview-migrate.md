---
title: "Migrar sua solução para o SQL Data Warehouse | Microsoft Docs"
description: "Orientação de migração para levar sua solução até a plataforma SQL Data Warehouse do Azure."
services: sql-data-warehouse
documentationcenter: NA
author: sqlmojo
manager: jhubbard
editor: 
ms.assetid: 198365eb-7451-4222-b99c-d1d9ef687f1b
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: migrate
ms.date: 06/27/2017
ms.author: joeyong;barbkess
ms.openlocfilehash: 771b9456e66b8a1e41f72340b695b19e2adaf793
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="migrate-your-solution-to-azure-sql-data-warehouse"></a><span data-ttu-id="f15e0-103">Migrar sua solução para o SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="f15e0-103">Migrate your solution to Azure SQL Data Warehouse</span></span>
<span data-ttu-id="f15e0-104">Veja o que envolve a migração de uma solução de banco de dados existente para o SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="f15e0-104">See what's involved in migrating an existing database solution to Azure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="f15e0-105">Criar o perfil de sua carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="f15e0-105">Profile your workload</span></span>
<span data-ttu-id="f15e0-106">Antes de migrar, convém verificar se o SQL Data Warehouse é a solução correta para sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="f15e0-106">Before migrating, you want to be certain SQL Data Warehouse is the right solution for your workload.</span></span> <span data-ttu-id="f15e0-107">O SQL Data Warehouse é um sistema distribuído projetado para executar uma análise em dados grandes.</span><span class="sxs-lookup"><span data-stu-id="f15e0-107">SQL Data Warehouse is a distributed system designed to perform analytics on large data.</span></span>  <span data-ttu-id="f15e0-108">A migração para o SQL Data Warehouse exige algumas alterações de design que não são muito difíceis de entender, mas que podem demorar algum tempo para serem implementadas.</span><span class="sxs-lookup"><span data-stu-id="f15e0-108">Migrating to SQL Data Warehouse requires some design changes that are not too hard to understand but might take some time to implement.</span></span> <span data-ttu-id="f15e0-109">Se sua empresa exige um data warehouse corporativo, os benefícios valem a pena.</span><span class="sxs-lookup"><span data-stu-id="f15e0-109">If your business requires an enterprise-class data warehouse, the benefits are worth the effort.</span></span> <span data-ttu-id="f15e0-110">No entanto, se você não precisar da potência do SQL Data Warehouse, é mais barato usar o SQL Server ou o Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f15e0-110">However, if you don't need the power of SQL Data Warehouse, it is more cost-effective to use SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="f15e0-111">Considere o uso do SQL Data Warehouse quando você:</span><span class="sxs-lookup"><span data-stu-id="f15e0-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="f15e0-112">Tiver um ou mais Terabytes de dados</span><span class="sxs-lookup"><span data-stu-id="f15e0-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="f15e0-113">Planejar executar análise em grandes quantidades de dados</span><span class="sxs-lookup"><span data-stu-id="f15e0-113">Plan to run analytics on large amounts of data</span></span>
- <span data-ttu-id="f15e0-114">Precisar da capacidade de dimensionar a computação e o armazenamento</span><span class="sxs-lookup"><span data-stu-id="f15e0-114">Need the ability to scale compute and storage</span></span> 
- <span data-ttu-id="f15e0-115">Quiser economizar nos custos pausando os recursos de computação quando não precisar deles.</span><span class="sxs-lookup"><span data-stu-id="f15e0-115">Want to save costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="f15e0-116">Não use o SQL Data Warehouse para cargas de trabalho operacionais (OLTP) que têm:</span><span class="sxs-lookup"><span data-stu-id="f15e0-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="f15e0-117">Alta frequência de leituras e gravações</span><span class="sxs-lookup"><span data-stu-id="f15e0-117">High frequency reads and writes</span></span>
- <span data-ttu-id="f15e0-118">Grande quantidade de seleções singleton</span><span class="sxs-lookup"><span data-stu-id="f15e0-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="f15e0-119">Muitos volumes de inserções de linha única</span><span class="sxs-lookup"><span data-stu-id="f15e0-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="f15e0-120">Necessidades de processamento linha por linha</span><span class="sxs-lookup"><span data-stu-id="f15e0-120">Row by row processing needs</span></span>
- <span data-ttu-id="f15e0-121">Formatos incompatíveis (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="f15e0-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-the-migration"></a><span data-ttu-id="f15e0-122">Planejar a migração</span><span class="sxs-lookup"><span data-stu-id="f15e0-122">Plan the migration</span></span>

<span data-ttu-id="f15e0-123">Depois que você decidiu migrar uma solução existente para o SQL Data Warehouse, é importante planejar a migração antes de começar.</span><span class="sxs-lookup"><span data-stu-id="f15e0-123">Once you have decided to migrate an existing solution to SQL Data Warehouse, it is important to plan the migration before getting started.</span></span> 

<span data-ttu-id="f15e0-124">Uma meta do planejamento é garantir que seu código, os esquemas de tabela e seus dados sejam compatíveis com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f15e0-124">One goal of planning is to ensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="f15e0-125">Há algumas diferenças de compatibilidade para solucionar entre seu sistema atual e o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="f15e0-125">There are some compatibility differences to work around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="f15e0-126">Além disso, a migração de grandes quantidades de dados para o Azure leva tempo.</span><span class="sxs-lookup"><span data-stu-id="f15e0-126">Plus, migrating large amounts of data to Azure takes time.</span></span> <span data-ttu-id="f15e0-127">Um planejamento cuidadoso acelera a obtenção de seus dados no Azure.</span><span class="sxs-lookup"><span data-stu-id="f15e0-127">Careful planning expedites getting your data to Azure.</span></span> 

<span data-ttu-id="f15e0-128">Outro objetivo do planejamento é fazer ajustes de design para garantir que sua solução aproveite o alto desempenho de consultas que o SQL Data Warehouse foi projetado para fornecer.</span><span class="sxs-lookup"><span data-stu-id="f15e0-128">Another goal of planning is to make design adjustments to ensure your solution takes advantage of the high query performance SQL Data Warehouse is designed to provide.</span></span> <span data-ttu-id="f15e0-129">O design de data warehouses, de acordo com a escala, apresenta padrões de design diferentes. Portanto, as abordagens tradicionais nem sempre são as melhores.</span><span class="sxs-lookup"><span data-stu-id="f15e0-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always the best.</span></span> <span data-ttu-id="f15e0-130">Embora você possa fazer alguns ajustes de design após a migração, fazer alterações logo no início do processo economizará tempo mais tarde.</span><span class="sxs-lookup"><span data-stu-id="f15e0-130">Although you can make some design adjustments after migration, making changes sooner in the process will save time later.</span></span>

<span data-ttu-id="f15e0-131">Para executar uma migração bem-sucedida, você precisa migrar seus dados, seu código e os esquemas de tabela.</span><span class="sxs-lookup"><span data-stu-id="f15e0-131">To perform a successful migration, you need to migrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="f15e0-132">Para obter orientação sobre esses tópicos de migração, consulte:</span><span class="sxs-lookup"><span data-stu-id="f15e0-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="f15e0-133">Migrar seus esquemas</span><span class="sxs-lookup"><span data-stu-id="f15e0-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="f15e0-134">Migrar seu código</span><span class="sxs-lookup"><span data-stu-id="f15e0-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="f15e0-135">[Migrar seus dados](sql-data-warehouse-migrate-data.md).</span><span class="sxs-lookup"><span data-stu-id="f15e0-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform the migration


## Deploy the solution


## Validate the migration

-->

## <a name="next-steps"></a><span data-ttu-id="f15e0-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="f15e0-136">Next steps</span></span>
<span data-ttu-id="f15e0-137">A CAT (Equipe Consultiva para Clientes) também tem algumas diretrizes ótimas do SQL Data Warehouse, que publica por meio de blogs.</span><span class="sxs-lookup"><span data-stu-id="f15e0-137">The CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="f15e0-138">Dê uma olhada no artigo [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] (Migrando dados para o SQL Data Warehouse do Azure na prática) para obter diretrizes adicionais sobre a migração.</span><span class="sxs-lookup"><span data-stu-id="f15e0-138">Take a look at their article, [Migrating data to Azure SQL Data Warehouse in practice][Migrating data to Azure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data to Azure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
