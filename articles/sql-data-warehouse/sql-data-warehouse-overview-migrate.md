---
title: "aaaMigrate tooSQL sua solução do Data Warehouse | Microsoft Docs"
description: "Orientação de migração para colocar sua plataforma de SQL Data Warehouse tooAzure solução."
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
ms.openlocfilehash: 27b51f15247603f054070f360ede7f24541c0288
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="migrate-your-solution-tooazure-sql-data-warehouse"></a><span data-ttu-id="3086b-103">Migrar tooAzure sua solução SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="3086b-103">Migrate your solution tooAzure SQL Data Warehouse</span></span>
<span data-ttu-id="3086b-104">Veja o que está envolvido na migração de uma tooAzure de solução de banco de dados existente do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3086b-104">See what's involved in migrating an existing database solution tooAzure SQL Data Warehouse.</span></span> 

## <a name="profile-your-workload"></a><span data-ttu-id="3086b-105">Criar o perfil de sua carga de trabalho</span><span class="sxs-lookup"><span data-stu-id="3086b-105">Profile your workload</span></span>
<span data-ttu-id="3086b-106">Antes de migrar, você deseja toobe determinado que SQL Data Warehouse é a solução certa Olá para sua carga de trabalho.</span><span class="sxs-lookup"><span data-stu-id="3086b-106">Before migrating, you want toobe certain SQL Data Warehouse is hello right solution for your workload.</span></span> <span data-ttu-id="3086b-107">SQL Data Warehouse é um sistema distribuído projetado tooperform análise dados grandes.</span><span class="sxs-lookup"><span data-stu-id="3086b-107">SQL Data Warehouse is a distributed system designed tooperform analytics on large data.</span></span>  <span data-ttu-id="3086b-108">Migrando tooSQL Data Warehouse exige algumas alterações de design que não são muito difíceis toounderstand, mas podem levar algum tempo tooimplement.</span><span class="sxs-lookup"><span data-stu-id="3086b-108">Migrating tooSQL Data Warehouse requires some design changes that are not too hard toounderstand but might take some time tooimplement.</span></span> <span data-ttu-id="3086b-109">Se sua empresa exige um data warehouse corporativo, benefícios Olá valem esforço hello.</span><span class="sxs-lookup"><span data-stu-id="3086b-109">If your business requires an enterprise-class data warehouse, hello benefits are worth hello effort.</span></span> <span data-ttu-id="3086b-110">No entanto, se não precisar de capacidade de saudação do SQL Data Warehouse, é mais econômico toouse do SQL Server ou banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="3086b-110">However, if you don't need hello power of SQL Data Warehouse, it is more cost-effective toouse SQL Server or Azure SQL Database.</span></span>

<span data-ttu-id="3086b-111">Considere o uso do SQL Data Warehouse quando você:</span><span class="sxs-lookup"><span data-stu-id="3086b-111">Consider using SQL Data Warehouse when you:</span></span>
- <span data-ttu-id="3086b-112">Tiver um ou mais Terabytes de dados</span><span class="sxs-lookup"><span data-stu-id="3086b-112">Have one or more Terabytes of data</span></span>
- <span data-ttu-id="3086b-113">Planejar toorun análise em grandes quantidades de dados</span><span class="sxs-lookup"><span data-stu-id="3086b-113">Plan toorun analytics on large amounts of data</span></span>
- <span data-ttu-id="3086b-114">Necessário Olá capacidade tooscale computação e armazenamento</span><span class="sxs-lookup"><span data-stu-id="3086b-114">Need hello ability tooscale compute and storage</span></span> 
- <span data-ttu-id="3086b-115">Deseja que os custos de toosave pausando recursos de computação quando você não precisa deles.</span><span class="sxs-lookup"><span data-stu-id="3086b-115">Want toosave costs by pausing compute resources when you don't need them.</span></span>

<span data-ttu-id="3086b-116">Não use o SQL Data Warehouse para cargas de trabalho operacionais (OLTP) que têm:</span><span class="sxs-lookup"><span data-stu-id="3086b-116">Don't use SQL Data Warehouse for operational (OLTP) workloads that have:</span></span>
- <span data-ttu-id="3086b-117">Alta frequência de leituras e gravações</span><span class="sxs-lookup"><span data-stu-id="3086b-117">High frequency reads and writes</span></span>
- <span data-ttu-id="3086b-118">Grande quantidade de seleções singleton</span><span class="sxs-lookup"><span data-stu-id="3086b-118">Large numbers of singleton selects</span></span>
- <span data-ttu-id="3086b-119">Muitos volumes de inserções de linha única</span><span class="sxs-lookup"><span data-stu-id="3086b-119">High volumes of single row inserts</span></span>
- <span data-ttu-id="3086b-120">Necessidades de processamento linha por linha</span><span class="sxs-lookup"><span data-stu-id="3086b-120">Row by row processing needs</span></span>
- <span data-ttu-id="3086b-121">Formatos incompatíveis (JSON, XML)</span><span class="sxs-lookup"><span data-stu-id="3086b-121">Incompatible formats (JSON, XML)</span></span>


## <a name="plan-hello-migration"></a><span data-ttu-id="3086b-122">Planejar migração Olá</span><span class="sxs-lookup"><span data-stu-id="3086b-122">Plan hello migration</span></span>

<span data-ttu-id="3086b-123">Depois de ter decidido toomigrate um tooSQL de solução do Data Warehouse existente, é importante tooplan migração de saudação antes de começar.</span><span class="sxs-lookup"><span data-stu-id="3086b-123">Once you have decided toomigrate an existing solution tooSQL Data Warehouse, it is important tooplan hello migration before getting started.</span></span> 

<span data-ttu-id="3086b-124">Uma meta de planejamento é tooensure seus dados, os esquemas de tabela, e seu código são compatíveis com o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3086b-124">One goal of planning is tooensure your data, your table schemas, and your code are compatible with SQL Data Warehouse.</span></span> <span data-ttu-id="3086b-125">Há algumas diferenças de compatibilidade toowork em torno entre seu sistema atual e o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="3086b-125">There are some compatibility differences toowork around between your current system and SQL Data Warehouse.</span></span> <span data-ttu-id="3086b-126">Além disso, migrando grandes quantidades de dados tooAzure leva tempo.</span><span class="sxs-lookup"><span data-stu-id="3086b-126">Plus, migrating large amounts of data tooAzure takes time.</span></span> <span data-ttu-id="3086b-127">Um planejamento cuidadoso acelera obtendo tooAzure seus dados.</span><span class="sxs-lookup"><span data-stu-id="3086b-127">Careful planning expedites getting your data tooAzure.</span></span> 

<span data-ttu-id="3086b-128">Outro objetivo de planejamento é design toomake tooensure ajustes que sua solução aproveita Olá alto desempenho de consultas que SQL Data Warehouse é projetada tooprovide.</span><span class="sxs-lookup"><span data-stu-id="3086b-128">Another goal of planning is toomake design adjustments tooensure your solution takes advantage of hello high query performance SQL Data Warehouse is designed tooprovide.</span></span> <span data-ttu-id="3086b-129">Criação de data warehouses para escala apresenta padrões de design diferentes e abordagens tradicionais nem sempre são Olá melhor.</span><span class="sxs-lookup"><span data-stu-id="3086b-129">Designing data warehouses for scale introduces different design patterns and so traditional approaches aren't always hello best.</span></span> <span data-ttu-id="3086b-130">Embora você possa fazer alguns ajustes de design após a migração, a fazer alterações mais cedo no processo de saudação economizará tempo mais tarde.</span><span class="sxs-lookup"><span data-stu-id="3086b-130">Although you can make some design adjustments after migration, making changes sooner in hello process will save time later.</span></span>

<span data-ttu-id="3086b-131">tooperform uma migração bem-sucedida, você precisa toomigrate os esquemas de tabela, seu código e seus dados.</span><span class="sxs-lookup"><span data-stu-id="3086b-131">tooperform a successful migration, you need toomigrate your table schemas, your code, and your data.</span></span> <span data-ttu-id="3086b-132">Para obter orientação sobre esses tópicos de migração, consulte:</span><span class="sxs-lookup"><span data-stu-id="3086b-132">For guidance on these migration topics, see:</span></span>

-  [<span data-ttu-id="3086b-133">Migrar seus esquemas</span><span class="sxs-lookup"><span data-stu-id="3086b-133">Migrate your schemas</span></span>](sql-data-warehouse-migrate-schema.md)
-  [<span data-ttu-id="3086b-134">Migrar seu código</span><span class="sxs-lookup"><span data-stu-id="3086b-134">Migrate your code</span></span>](sql-data-warehouse-migrate-code.md)
-  <span data-ttu-id="3086b-135">[Migrar seus dados](sql-data-warehouse-migrate-data.md).</span><span class="sxs-lookup"><span data-stu-id="3086b-135">[Migrate your data](sql-data-warehouse-migrate-data.md).</span></span> 

<!--
## Perform hello migration


## Deploy hello solution


## Validate hello migration

-->

## <a name="next-steps"></a><span data-ttu-id="3086b-136">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="3086b-136">Next steps</span></span>
<span data-ttu-id="3086b-137">Olá CAT (equipe de consultoria do cliente) também tem alguns excelente orientação de SQL Data Warehouse, que eles publicarem por meio de blogs.</span><span class="sxs-lookup"><span data-stu-id="3086b-137">hello CAT (Customer Advisory Team) also has some great SQL Data Warehouse guidance, which they publish through blogs.</span></span>  <span data-ttu-id="3086b-138">Dê uma olhada em seu artigo, [migrando dados tooAzure SQL Data Warehouse na prática] [ Migrating data tooAzure SQL Data Warehouse in practice] para obter orientação adicional sobre a migração.</span><span class="sxs-lookup"><span data-stu-id="3086b-138">Take a look at their article, [Migrating data tooAzure SQL Data Warehouse in practice][Migrating data tooAzure SQL Data Warehouse in practice] for additional guidance on migration.</span></span>

<!--Image references-->

<!--Article references-->

<!--MSDN references-->

<!--Other Web references-->
[Migrating data tooAzure SQL Data Warehouse in practice]: https://blogs.msdn.microsoft.com/sqlcat/2016/08/18/migrating-data-to-azure-sql-data-warehouse-in-practice/
