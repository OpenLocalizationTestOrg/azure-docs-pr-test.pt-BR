---
title: Tecnologias In-Memory do Banco de Dados SQL do Azure | Microsoft Docs
description: "As tecnologias In-Memory do Banco de Dados SQL do Azure melhoram muito o desempenho de cargas de trabalho transacionais e analíticas. Saiba como aproveitar as vantagens dessas tecnologias."
services: sql-database
documentationCenter: 
author: jodebrui
manager: jhubbard
editor: 
ms.assetid: 250ef341-90e5-492f-b075-b4750d237c05
ms.service: sql-database
ms.custom: develop databases
ms.workload: data-management
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/24/2017
ms.author: jodebrui
ms.openlocfilehash: 4cb45551c486263f26947e5684d54b4f2ecc7410
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="0d3bc-104">Otimizar o desempenho usando tecnologias In-Memory no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="0d3bc-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="0d3bc-105">Usando tecnologias In-Memory no Banco de Dados SQL do Azure, você pode obter melhorias no desempenho com várias cargas de trabalho: transacional (OLTP [processamento transacional online]), análise (OLAP [processamento analítico online]) e misto (HTAP [processamento híbrido analítico/de transação]).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="0d3bc-106">Devido ao processamento de transações e consulta mais eficientes, as tecnologias In-Memory também ajudam a reduzir os custos.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-106">Because of the more efficient query and transaction processing, In-Memory technologies also help you to reduce cost.</span></span> <span data-ttu-id="0d3bc-107">Você normalmente não precisa atualizar o tipo de preço do banco de dados para obter ganhos de desempenho.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-107">You typically don't need to upgrade the pricing tier of the database to achieve performance gains.</span></span> <span data-ttu-id="0d3bc-108">Em alguns casos, você mesmo poderá até mesmo reduzir o tipo de preço e ainda continuar a ver melhorias de desempenho com as tecnologias In-Memory.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-108">In some cases, you might even be able reduce the pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="0d3bc-109">Estes são dois exemplos de como o OLTP In-Memory ajudou a melhorar significativamente o desempenho:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-109">Here are two examples of how In-Memory OLTP helped to significantly improve performance:</span></span>

- <span data-ttu-id="0d3bc-110">Usando o OLTP In-Memory, a [Quorum Business Solutions foi capaz de duplicar a carga de trabalho, melhorando as DTUs em 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-110">By using In-Memory OLTP, [Quorum Business Solutions was able to double their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="0d3bc-111">DTU significa *unidade de taxa de transferência de banco de dados* e inclui uma medição de consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="0d3bc-112">O vídeo a seguir demonstra uma melhoria significativa no consumo de recursos com uma carga de trabalho de exemplo: [OLTP In-Memory no Vídeo do Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-112">The following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="0d3bc-113">Para obter mais detalhes, confira a postagem no blog: [Postagem de Blog de OLTP na memória do Banco de Dados SQL do Azure](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="0d3bc-113">For more details, see the blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="0d3bc-114">As tecnologias In-Memory estão disponíveis em todos os bancos de dados da camada Premium, incluindo bancos de dados em pools elásticos Premium.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-114">In-Memory technologies are available in all databases in the Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="0d3bc-115">O vídeo a seguir explica os possíveis ganhos de desempenho com as tecnologias em memória no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-115">The following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="0d3bc-116">Lembre-se de que o ganho de desempenho que você verá sempre dependerá de diversos fatores, incluindo a natureza da carga de trabalho e dos dados, o padrão de acesso do banco de dados e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-116">Remember that the performance gain that you see always depends on many factors, including the nature of the workload and data, access pattern of the database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="0d3bc-117">O Banco de Dados SQL do Azure conta com as seguintes tecnologias em memória:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-117">Azure SQL Database has the following In-Memory technologies:</span></span>

- <span data-ttu-id="0d3bc-118">O *OLTP in-memory* aumenta a taxa de transferência e reduz a latência do processamento de transações.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="0d3bc-119">Os cenários que se beneficiam do OLTP In-Memory são: processamento de transações de alta taxa de transferência, como comércio e jogos, ingestão de dados de eventos ou dispositivos IoT, cache, carregamento de dados e cenários de variáveis de tabela e tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="0d3bc-120">Os *índices columnstore clusterizados* reduzem seu volume de armazenamento (em até 10 vezes) e melhoram o desempenho de relatórios e consultas de análise.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-120">*Clustered columnstore indexes* reduce your storage footprint (up to 10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="0d3bc-121">Você pode usá-lo com tabelas de fatos em data marts para colocar mais dados no banco de dados e melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-121">You can use it with fact tables in your data marts to fit more data in your database and improve performance.</span></span> <span data-ttu-id="0d3bc-122">Além disso, também é possível usá-lo com os dados históricos no banco de dados operacional para arquivar e conseguir consultar até 10 vezes mais dados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-122">Also, you can use it with historical data in your operational database to archive and be able to query up to 10 times more data.</span></span>
- <span data-ttu-id="0d3bc-123">*Índices columnstore não clusterizados* para HTAP ajudam a obter análises em tempo real sobre seus negócios consultando o banco de dados operacional diretamente, sem a necessidade de executar um processo ETL (extração, transformação e carregamento) caro e aguardar o data warehouse ser populado.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-123">*Nonclustered columnstore indexes* for HTAP help you to gain real-time insights into your business through querying the operational database directly, without the need to run an expensive extract, transform, and load (ETL) process and wait for the data warehouse to be populated.</span></span> <span data-ttu-id="0d3bc-124">Os índices columnstore não clusterizados permitem uma execução muito rápida das consultas de análise no banco de dados OLTP, enquanto reduzem o impacto sobre a carga de trabalho operacional.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on the OLTP database, while reducing the impact on the operational workload.</span></span>
- <span data-ttu-id="0d3bc-125">Você também pode ter a combinação de tabela com otimização de memória com um índice columnstore.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-125">You can also have the combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="0d3bc-126">Essa combinação permite que você execute o processamento de transações com muita rapidez e execute *simultaneamente* consultas de análise rapidamente nos mesmos dados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-126">This combination enables you to perform very fast transaction processing, and to *concurrently* run analytics queries very quickly on the same data.</span></span>

<span data-ttu-id="0d3bc-127">Tanto os índices columnstore quanto o OLTP In-Memory integram o produto SQL Server desde 2012 e 2014, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-127">Both columnstore indexes and In-Memory OLTP have been part of the SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="0d3bc-128">O Banco de Dados SQL do Azure e o SQL Server compartilham a mesma implementação de tecnologias In-Memory.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-128">Azure SQL Database and SQL Server share the same implementation of In-Memory technologies.</span></span> <span data-ttu-id="0d3bc-129">Daqui em diante, os novos recursos para essas tecnologias serão lançados primeiro no Banco de Dados SQL do Azure, antes de serem lançados no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="0d3bc-130">Este tópico descreve aspectos do OLTP In-Memory e dos índices Columnstore específicos ao Banco de Dados SQL do Azure, além de também incluir exemplos:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific to Azure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="0d3bc-131">Você verá o impacto dessas tecnologias no armazenamento e dos limites de tamanho dos dados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-131">You'll see the impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="0d3bc-132">Você verá como gerenciar a movimentação dos bancos de dados que utilizam essas tecnologias entre os diferentes tipos de preço.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-132">You'll see how to manage the movement of databases that use these technologies between the different pricing tiers.</span></span>
- <span data-ttu-id="0d3bc-133">Você verá dois exemplos que ilustram o uso do OLTP In-Memory, bem como dos índices columnstore, no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-133">You'll see two samples that illustrate the use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="0d3bc-134">Consulte os seguintes recursos para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-134">See the following resources for more information.</span></span>

<span data-ttu-id="0d3bc-135">Informações detalhadas sobre as tecnologias:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-135">In-depth information about the technologies:</span></span>

- <span data-ttu-id="0d3bc-136">[Visão geral e cenários de uso do OLTP In-Memory](https://msdn.microsoft.com/library/mt774593.aspx) (incluindo referências a estudos de caso de cliente e informações para começar)</span><span class="sxs-lookup"><span data-stu-id="0d3bc-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references to customer case studies and information to get started)</span></span>
- [<span data-ttu-id="0d3bc-137">Documentação para OLTP in-memory</span><span class="sxs-lookup"><span data-stu-id="0d3bc-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="0d3bc-138">Guia de índices ColumnStore</span><span class="sxs-lookup"><span data-stu-id="0d3bc-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="0d3bc-139">HTAP (Processamento Transacional e Analítico Híbrido), também conhecido como [análise operacional em tempo real](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="0d3bc-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="0d3bc-140">Uma prévia rápida no OLTP In-Memory: [Início Rápido 1: tecnologias OLTP In-Memory para um desempenho mais rápido do T-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (outro artigo para ajudar você a se familiarizar)</span><span class="sxs-lookup"><span data-stu-id="0d3bc-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article to help you get started)</span></span>

<span data-ttu-id="0d3bc-141">Vídeos detalhados sobre as tecnologias:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-141">In-depth videos about the technologies:</span></span>

- <span data-ttu-id="0d3bc-142">[OLTP In-Memory no Banco de Dados SQL do Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (que contém uma demonstração dos benefícios de desempenho e as etapas para você mesmo reproduzir esses resultados)</span><span class="sxs-lookup"><span data-stu-id="0d3bc-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps to reproduce these results yourself)</span></span>
- [<span data-ttu-id="0d3bc-143">Vídeos sobre o OLTP in-memory: O que é e quando e como usá-lo</span><span class="sxs-lookup"><span data-stu-id="0d3bc-143">In-Memory OLTP Videos: What it is and When/How to use it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="0d3bc-144">Índice Columnstore: vídeos sobre a análise em memória do Ignite 2016</span><span class="sxs-lookup"><span data-stu-id="0d3bc-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="0d3bc-145">Armazenamento e tamanho dos dados</span><span class="sxs-lookup"><span data-stu-id="0d3bc-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="0d3bc-146">Tamanho dos dados e limite de armazenamento do OLTP in-memory</span><span class="sxs-lookup"><span data-stu-id="0d3bc-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="0d3bc-147">O OLTP in-memory inclui tabelas com otimização de memória, que são usadas para armazenar dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="0d3bc-148">Essas tabelas precisam caber na memória.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-148">These tables are required to fit in memory.</span></span> <span data-ttu-id="0d3bc-149">Como você gerencia a memória diretamente no serviço do Banco de Dados SQL, temos o conceito de uma cota para dados de usuário.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-149">Because you manage memory directly in the SQL Database service, we have the  concept of a quota for user data.</span></span> <span data-ttu-id="0d3bc-150">Esse conceito é conhecido como *Armazenamento de OLTP In-Memory*.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-150">This idea is referred to as *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="0d3bc-151">Cada tipo de preço de banco de dados independente e cada tipo de preço de pool elástico com suporte incluem determinada quantidade de Armazenamento do OLTP in-memory.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="0d3bc-152">Até o momento em que esse documento foi redigido, você recebe um gigabyte de armazenamento para cada 125 DTUs (unidades de transação do banco de dados) ou eDTUs (unidades de transação do banco de dados elástico).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-152">At the time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="0d3bc-153">Os artigo [Tipos de preço do Banco de Dados SQL](sql-database-service-tiers.md) contém a lista oficial de armazenamento do OLTP in-memory disponível para cada tipo de preço de banco de dados independente e pool elástico com suporte.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-153">The [SQL Database service tiers](sql-database-service-tiers.md) article has the official list of the In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="0d3bc-154">Os itens a seguir contam para seu limite de armazenamento do OLTP in-memory:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-154">The following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="0d3bc-155">Linhas de dados de usuário ativo em tabelas com otimização de memória e variáveis de tabela.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="0d3bc-156">Observe que as versões de linha antigas não entram na contagem do limite.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-156">Note that old row versions don't count toward the cap.</span></span>
- <span data-ttu-id="0d3bc-157">Índices em tabelas com otimização de memória.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="0d3bc-158">Custo operacional das operações ALTER TABLE.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="0d3bc-159">Se atingir o limite, você receberá um erro de limite de cota atingido e não conseguirá inserir ou atualizar os dados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-159">If you hit the cap, you receive an out-of-quota error, and you are no longer able to insert or update data.</span></span> <span data-ttu-id="0d3bc-160">Para atenuar esse erro, exclua dados ou aumente o tipo de preço do banco de dados ou do pool.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-160">To mitigate this error, delete data or increase the pricing tier of the database or pool.</span></span>

<span data-ttu-id="0d3bc-161">Para obter detalhes sobre como monitorar a utilização do armazenamento do OLTP in-memory e configurar alertas quando estiver perto de atingir o limite, consulte [Monitorar o armazenamento in-memory](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit the cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="0d3bc-162">Sobre pools elásticos</span><span class="sxs-lookup"><span data-stu-id="0d3bc-162">About elastic pools</span></span>

<span data-ttu-id="0d3bc-163">Com os pools elásticos, o armazenamento do OLTP in-memory é compartilhado entre todos os bancos de dados no pool.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-163">With elastic pools, the In-Memory OLTP storage is shared across all databases in the pool.</span></span> <span data-ttu-id="0d3bc-164">Portanto, o uso de um banco de dados pode afetar outros bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-164">Therefore, the usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="0d3bc-165">As duas mitigações para esse problema são:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="0d3bc-166">Configure um Max-eDTU para bancos de dados que seja menor que a contagem de eDTUs do pool como um todo.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-166">Configure a Max-eDTU for databases that is lower than the eDTU count for the pool as a whole.</span></span> <span data-ttu-id="0d3bc-167">Isso proporciona um limite máximo à utilização no armazenamento do OLTP in-memory em qualquer banco de dados no pool ao tamanho que corresponde à contagem de eDTUs.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-167">This maximum caps the In-Memory OLTP storage utilization, in any database in the pool, to the size that corresponds to the eDTU count.</span></span>
- <span data-ttu-id="0d3bc-168">Defina um Min-eDTU maior que 0.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="0d3bc-169">Isso garante o mínimo que cada banco de dados no pool tem a quantidade de armazenamento do OLTP in-memory disponível correspondente ao Min-eDTU configurado.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-169">This minimum guarantees that each database in the pool has the amount of available In-Memory OLTP storage that corresponds to the configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="0d3bc-170">Tamanho dos dados e armazenamento para índices columnstore</span><span class="sxs-lookup"><span data-stu-id="0d3bc-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="0d3bc-171">Os índices columnstore não precisam caber na memória.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-171">Columnstore indexes aren't required to fit in memory.</span></span> <span data-ttu-id="0d3bc-172">Portanto, o único limite para o tamanho dos índices é o tamanho máximo do banco de dados geral, que está documentado no artigo [Camadas de serviço do Banco de Dados SQL](sql-database-service-tiers.md).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-172">Therefore, the only cap on the size of the indexes is the maximum overall database size, which is documented in the [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="0d3bc-173">Ao usar os índices columnstore clusterizados, a compactação vertical é usada para o armazenamento de tabelas base.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-173">When you use clustered columnstore indexes, columnar compression is used for the base table storage.</span></span> <span data-ttu-id="0d3bc-174">Essa compactação pode reduzir consideravelmente o volume de armazenamento dos dados do usuário, o que significa que você pode colocar mais dados no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-174">This compression can significantly reduce the storage footprint of your user data, which means that you can fit more data in the database.</span></span> <span data-ttu-id="0d3bc-175">E a compactação pode ser ainda maior com a [compactação de arquivamento vertical](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-175">And the compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="0d3bc-176">A quantidade de compactação que pode ser obtida depende da natureza dos dados, mas uma compactação de 10 vezes não é incomum.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-176">The amount of compression that you can achieve depends on the nature of the data, but 10 times the compression is not uncommon.</span></span>

<span data-ttu-id="0d3bc-177">Por exemplo, se você tiver um banco de dados com tamanho máximo de 1 TB (terabyte) e obter uma compactação de 10 vezes usando índices columnstore, você poderá colocar um total de 10 TB de dados de usuário no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times the compression by using columnstore indexes, you can fit a total of 10 TB of user data in the database.</span></span>

<span data-ttu-id="0d3bc-178">Quando você usa os índices columnstore não clusterizado, a tabela base ainda é armazenada no formato rowstore tradicional.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-178">When you use nonclustered columnstore indexes, the base table is still stored in the traditional rowstore format.</span></span> <span data-ttu-id="0d3bc-179">Portanto, a economia de armazenamento não é tão grande quanto com os índices columnstore clusterizados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-179">Therefore, the storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="0d3bc-180">No entanto, se você estiver substituindo vários índices não clusterizados tradicionais por um único índice columnstore, você ainda poderá observar uma economia geral no espaço de armazenamento da tabela.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in the storage footprint for the table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="0d3bc-181">Movendo bancos de dados que usam tecnologias In-Memory entre tipos de preço</span><span class="sxs-lookup"><span data-stu-id="0d3bc-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="0d3bc-182">Nunca há incompatibilidades ou outros problemas quando você atualiza para um preço mais alto, por exemplo, do Standard para Premium.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-182">There are never any incompatibilities or other problems when you upgrade to a higher pricing tier, such as from Standard to Premium.</span></span> <span data-ttu-id="0d3bc-183">Os recursos e funcionalidades disponíveis só aumentam.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-183">The available functionality and resources only increase.</span></span>

<span data-ttu-id="0d3bc-184">Mas o downgrade do tipo de preço pode afetar negativamente seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-184">But downgrading the pricing tier can negatively impact your database.</span></span> <span data-ttu-id="0d3bc-185">O impacto é especialmente aparente quando você faz o downgrade de Premium para Básico ou Standard quando o banco de dados contém objetos OLTP in-memory.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-185">The impact is especially apparent when you downgrade from Premium to Standard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="0d3bc-186">As tabelas otimizadas para memória e índices columnstore não ficam disponíveis após o downgrade (mesmo se permanecerem visíveis).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-186">Memory-optimized tables, and columnstore indexes, are unavailable after the downgrade (even if they remain visible).</span></span> <span data-ttu-id="0d3bc-187">As mesmas considerações se aplicam ao reduzir o tipo de preço de um pool elástico ou ao mover um banco de dados com tecnologias In-Memory para um pool elástico Standard ou Básico.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-187">The same considerations apply when you're lowering the pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="0d3bc-188">OLTP Na Memória</span><span class="sxs-lookup"><span data-stu-id="0d3bc-188">In-Memory OLTP</span></span>

<span data-ttu-id="0d3bc-189">*Fazer downgrade para Básico/Standard*: não há suporte para o OLTP in-memory em bancos de dados na camada Standard ou Básico.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-189">*Downgrading to Basic/Standard*: In-Memory OLTP isn't supported in databases in the Standard or Basic tier.</span></span> <span data-ttu-id="0d3bc-190">Além disso, não é possível mover um banco de dados que tem objetos OLTP in-memory para a camada Standard ou Básico.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-190">In addition, it isn't possible to move a database that has any In-Memory OLTP objects to the Standard or Basic tier.</span></span>

<span data-ttu-id="0d3bc-191">Antes de fazer o downgrade do banco de dados para Standard/Básico, remova todas as tabelas com otimização de memória e os tipos de tabela, bem como todos os módulos do T-SQL compilados nativamente.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-191">Before you downgrade the database to Standard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="0d3bc-192">Há uma maneira programática de entender se determinado banco de dados dá suporte ao OLTP in-memory.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-192">There is a programmatic way to understand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="0d3bc-193">Execute a seguinte consulta Transact-SQL:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-193">You can execute the following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="0d3bc-194">Se a consulta retorna **1**, há suporte para o OLTP in-memory neste banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-194">If the query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="0d3bc-195">*Fazer downgrade para uma camada Premium mais baixa*: os dados em tabelas com otimização de memória devem caber no armazenamento OLTP in-memory associado ao tipo de preço do banco de dados ou disponível no pool elástico.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-195">*Downgrading to a lower Premium tier*: Data in memory-optimized tables must fit within the In-Memory OLTP storage that is associated with the pricing tier of the database or is available in the elastic pool.</span></span> <span data-ttu-id="0d3bc-196">Se você tentar reduzir o tipo de preço ou mover o banco de dados para um pool que não tem armazenamento do OLTP in-memory suficiente disponível, a operação falhará.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-196">If you try to lower the pricing tier or move the database into a pool that doesn't have enough available In-Memory OLTP storage, the operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="0d3bc-197">Índices ColumnStore</span><span class="sxs-lookup"><span data-stu-id="0d3bc-197">Columnstore indexes</span></span>

<span data-ttu-id="0d3bc-198">*Downgrade para Básico ou Standard*: os índices columnstore só têm suporte no tipo de preço Premium, e não nos tipos Standard ou Básico.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-198">*Downgrading to Basic or Standard*: Columnstore indexes are supported only on the Premium pricing tier, and not on the Standard or Basic tiers.</span></span> <span data-ttu-id="0d3bc-199">Ao fazer o downgrade de seu banco de dados para Básico ou Standard, seu índice columnstore fica indisponível.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-199">When you downgrade your database to Standard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="0d3bc-200">O sistema mantém seu índice columnstore, mas nunca utiliza o índice.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-200">The system maintains your columnstore index, but it never leverages the index.</span></span> <span data-ttu-id="0d3bc-201">Se, mais tarde, você atualizar para Premium, o índice columnstore será imediatamente disponibilizado para uso novamente.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-201">If you later upgrade back to Premium, your columnstore index is immediately ready to be leveraged again.</span></span>

<span data-ttu-id="0d3bc-202">Se você tiver um índice columnstore **clusterizado**, a tabela inteira ficará indisponível após o downgrade do tipo.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-202">If you have a **clustered** columnstore index, the whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="0d3bc-203">Portanto, recomendamos que você remova todos os índices columnstore *clusterizado* antes de fazer o downgrade de seu banco de dados abaixo do tipo Premium.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below the Premium tier.</span></span>

<span data-ttu-id="0d3bc-204">*Fazer downgrade para um tipo Premium mais baixo*: esse downgrade terá êxito se todo o banco de dados couber dentro do tamanho máximo de banco de dados para o tipo de preço de destino, ou dentro do armazenamento disponível no pool elástico.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-204">*Downgrading to a lower Premium tier*: This downgrade succeeds if the whole database fits within the maximum database size for the target pricing tier, or within the available storage in the elastic pool.</span></span> <span data-ttu-id="0d3bc-205">Não há nenhum impacto específico nos índices columnstore.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-205">There is no specific impact from the columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-the-in-memory-oltp-sample"></a><span data-ttu-id="0d3bc-206">1. Instalar o exemplo de OLTP Na Memória.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-206">1. Install the In-Memory OLTP sample</span></span>

<span data-ttu-id="0d3bc-207">Você pode criar o banco de dados de exemplo AdventureWorksLT com alguns cliques no [Portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-207">You can create the AdventureWorksLT sample database with a few clicks in the [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="0d3bc-208">Em seguida, as etapas desta seção explicam como você pode aprimorar seu banco de dados AdventureWorksLT com objetos OLTP in-memory e demonstram os benefícios de desempenho.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-208">Then, the steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="0d3bc-209">Para ver uma demonstração de desempenho mais simples, porém, mais visualmente interessante do OLTP in-memory, veja:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="0d3bc-210">Versão: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="0d3bc-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="0d3bc-211">Código-fonte: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="0d3bc-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="0d3bc-212">Etapas de instalação</span><span class="sxs-lookup"><span data-stu-id="0d3bc-212">Installation steps</span></span>

1. <span data-ttu-id="0d3bc-213">No [Portal do Azure](https://portal.azure.com/), crie um banco de dados Premium em um servidor.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-213">In the [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="0d3bc-214">Defina a **Origem** como o banco de dados de exemplo AdventureWorksLT.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-214">Set the **Source** to the AdventureWorksLT sample database.</span></span> <span data-ttu-id="0d3bc-215">Para obter instruções detalhadas, consulte [Criar seu primeiro Banco de Dados SQL do Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="0d3bc-216">Conecte-se ao banco de dados com o SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-216">Connect to the database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="0d3bc-217">Copie o [script Transact-SQL do OLTP Na Memória](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-217">Copy the [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) to your clipboard.</span></span> <span data-ttu-id="0d3bc-218">O script T-SQL cria os objetos necessários In-Memory no banco de dados de exemplo AdventureWorksLT criado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-218">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="0d3bc-219">Cole o script T-SQL no SSMS e execute o script.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-219">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="0d3bc-220">As instruções CREATE TABLE da cláusula `MEMORY_OPTIMIZED = ON` são cruciais.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-220">The `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="0d3bc-221">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="0d3bc-222">Erro 40536</span><span class="sxs-lookup"><span data-stu-id="0d3bc-222">Error 40536</span></span>


<span data-ttu-id="0d3bc-223">Se você receber o erro 40536 quando executar o script T-SQL, execute o seguinte script T-SQL para verificar se o banco de dados oferece suporte a Na Memória:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-223">If you get error 40536 when you run the T-SQL script, run the following T-SQL script to verify whether the database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="0d3bc-224">Um resultado **0** significa que não há suporte para In-Memory e **1** significa que há suporte.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="0d3bc-225">Para diagnosticar o problema, verifique se o banco de dados está na camada de serviço Premium.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-225">To diagnose the problem, ensure that the database is at the Premium service tier.</span></span>


#### <a name="about-the-created-memory-optimized-items"></a><span data-ttu-id="0d3bc-226">Sobre os itens criados com otimização de memória</span><span class="sxs-lookup"><span data-stu-id="0d3bc-226">About the created memory-optimized items</span></span>

<span data-ttu-id="0d3bc-227">**Tabelas**: o exemplo contém as seguintes tabelas com otimização de memória:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-227">**Tables**: The sample contains the following memory-optimized tables:</span></span>

- <span data-ttu-id="0d3bc-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="0d3bc-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="0d3bc-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="0d3bc-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="0d3bc-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="0d3bc-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="0d3bc-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="0d3bc-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="0d3bc-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="0d3bc-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="0d3bc-233">Você pode inspecionar as tabelas com otimização de memória por meio do **Pesquisador de Objetos** no SSMS.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-233">You can inspect memory-optimized tables through the **Object Explorer** in SSMS.</span></span> <span data-ttu-id="0d3bc-234">Clique com o botão direito do mouse em **Tabelas** > **Filtro** > **Configurações do Filtro** > **Com otimização de memória**.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="0d3bc-235">O valor é igual a 1.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-235">The value equals 1.</span></span>


<span data-ttu-id="0d3bc-236">Ou então, você pode consultar as exibições do catálogo, tal como:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-236">Or you can query the catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="0d3bc-237">**Procedimento armazenado compilado nativamente**: você pode inspecionar SalesLT.usp_InsertSalesOrder_inmem por meio de uma consulta de exibição de catálogo:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-the-sample-oltp-workload"></a><span data-ttu-id="0d3bc-238">Executar a carga de trabalho OLTP</span><span class="sxs-lookup"><span data-stu-id="0d3bc-238">Run the sample OLTP workload</span></span>

<span data-ttu-id="0d3bc-239">A única diferença entre os dois *procedimentos armazenados* a seguir é que o primeiro procedimento usa versões com otimização de memória das tabelas, enquanto o segundo procedimento usa as tabelas em disco regulares:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-239">The only difference between the following two *stored procedures* is that the first procedure uses memory-optimized versions of the tables, while the second procedure uses the regular on-disk tables:</span></span>

- <span data-ttu-id="0d3bc-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="0d3bc-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="0d3bc-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="0d3bc-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="0d3bc-242">Nesta seção, você verá como usar o utilitário **ostress.exe** para executar os dois procedimentos armazenados em níveis estressantes.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-242">In this section, you see how to use the handy **ostress.exe** utility to execute the two stored procedures at stressful levels.</span></span> <span data-ttu-id="0d3bc-243">Você pode comparar quanto tempo as duas execuções demoram para serem concluídas.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-243">You can compare how long it takes for the two stress runs to finish.</span></span>


<span data-ttu-id="0d3bc-244">Quando executar ostress.exe, recomendamos será passar valores de parâmetro projetados para ambos os seguintes:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of the following:</span></span>

- <span data-ttu-id="0d3bc-245">Execute um grande número de conexões simultâneas usando -n100.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="0d3bc-246">Faça com que cada conexão entre em loop centenas de vezes usando -r500.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="0d3bc-247">No entanto, talvez você queira começar com valores muito menores, como -n10 e -r50 para garantir que tudo esteja funcionando.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-247">However, you might want to start with much smaller values like -n10 and -r50 to ensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="0d3bc-248">Script para ostress.exe</span><span class="sxs-lookup"><span data-stu-id="0d3bc-248">Script for ostress.exe</span></span>


<span data-ttu-id="0d3bc-249">Esta seção exibe o script T-SQL, que está inserido em nossa linha de comando do ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-249">This section displays the T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="0d3bc-250">O script usa itens que foram criados pelo script T-SQL instalado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-250">The script uses items that were created by the T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="0d3bc-251">O script a seguir insere um pedido de vendas de exemplo com cinco itens de linha nas seguintes *tabelas*com otimização de memória:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-251">The following script inserts a sample sales order with five line items into the following memory-optimized *tables*:</span></span>

- <span data-ttu-id="0d3bc-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="0d3bc-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="0d3bc-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="0d3bc-253">SalesLT.SalesOrderDetail_inmem</span></span>


```
DECLARE
    @i int = 0,
    @od SalesLT.SalesOrderDetailType_inmem,
    @SalesOrderID int,
    @DueDate datetime2 = sysdatetime(),
    @CustomerID int = rand() * 8000,
    @BillToAddressID int = rand() * 10000,
    @ShipToAddressID int = rand() * 10000;

INSERT INTO @od
    SELECT OrderQty, ProductID
    FROM Demo.DemoSalesOrderDetailSeed
    WHERE OrderID= cast((rand()*60) as int);

WHILE (@i < 20)
begin;
    EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT,
        @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od;
    SET @i = @i + 1;
end
```


<span data-ttu-id="0d3bc-254">Para criar a versão *_ondisk* do script T-SQL anterior para ostress.exe, substitua as duas ocorrências da subcadeia de caracteres *_inmem* por *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-254">To make the *_ondisk* version of the preceding T-SQL script for ostress.exe, you would replace both occurrences of the *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="0d3bc-255">Essas substituições afetam os nomes de tabelas e os procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-255">These replacements affect the names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="0d3bc-256">Instalar utilitários RML e o ostress</span><span class="sxs-lookup"><span data-stu-id="0d3bc-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="0d3bc-257">O ideal é você planejar executar o ostress.exe em uma VM (máquina virtual) do Azure.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-257">Ideally, you would plan to run ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="0d3bc-258">Você criaria uma [VM do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) na mesma região geográfica do Azure em que seu banco de dados AdventureWorksLT reside.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in the same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="0d3bc-259">Mas você pode executar o ostress.exe em seu laptop.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="0d3bc-260">Na VM ou em qualquer host que você escolher, instale os utilitários RML (Replay Markup Language).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-260">On the VM, or on whatever host you choose, install the Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="0d3bc-261">Os utilitários incluem ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-261">The utilities include ostress.exe.</span></span>

<span data-ttu-id="0d3bc-262">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-262">For more information, see:</span></span>
- <span data-ttu-id="0d3bc-263">A discussão sobre ostress.exe no [Banco de dados de exemplo para OLTP In-Memory](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-263">The ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="0d3bc-264">[Banco de dados de exemplo para OLTP In-Memory](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="0d3bc-265">O [blog para instalar o ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-265">The [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions to AdventureWorks to Demonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-the-inmem-stress-workload-first"></a><span data-ttu-id="0d3bc-266">Executar a carga de trabalho de estresse do *_inmem* primeiro</span><span class="sxs-lookup"><span data-stu-id="0d3bc-266">Run the *_inmem* stress workload first</span></span>


<span data-ttu-id="0d3bc-267">Você pode usar uma janela *Prompt Cmd RML* para executar nossa linha de comando do ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-267">You can use an *RML Cmd Prompt* window to run our ostress.exe command line.</span></span> <span data-ttu-id="0d3bc-268">Os parâmetros de linha de comando direcionam o ostress para:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-268">The command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="0d3bc-269">Execute 100 conexões simultaneamente (-n100).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="0d3bc-270">Faça cada conexão executar o script T-SQL 50 vezes (-r50).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-270">Have each connection run the T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="0d3bc-271">Para executar a linha de comando do ostress.exe anterior:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-271">To run the preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="0d3bc-272">Redefina o conteúdo de dados do banco de dados executando o seguinte comando no SSMS para excluir todos os dados inseridos por todas as execuções anteriores:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-272">Reset the database data content by running the following command in SSMS, to delete all the data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="0d3bc-273">Copie o texto da linha de comando anterior do ostress.exe para a área de transferência.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-273">Copy the text of the preceding ostress.exe command line to your clipboard.</span></span>

3. <span data-ttu-id="0d3bc-274">Substitua o `<placeholders>` para os parâmetros -S -U -P -d pelos valores reais corretos.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-274">Replace the `<placeholders>` for the parameters -S -U -P -d with the correct real values.</span></span>

4. <span data-ttu-id="0d3bc-275">Execute a linha de comando editada em uma janela Cmd RML.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="0d3bc-276">O resultado é uma duração</span><span class="sxs-lookup"><span data-stu-id="0d3bc-276">Result is a duration</span></span>


<span data-ttu-id="0d3bc-277">Quando o ostress.exe é concluído, ele grava a duração da execução como sua linha final de saída na janela Cmd RML.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-277">When ostress.exe finishes, it writes the run duration as its final line of output in the RML Cmd window.</span></span> <span data-ttu-id="0d3bc-278">Por exemplo, uma execução de teste mais curta dura aproximadamente 1,5 minuto:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="0d3bc-279">Redefinir, editar *_ondisk* e executar novamente</span><span class="sxs-lookup"><span data-stu-id="0d3bc-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="0d3bc-280">Depois de obter o resultado da execução do *_inmem*, realize as seguintes etapas para a execução de *_ondisk*:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-280">After you have the result from the *_inmem* run, perform the following steps for the *_ondisk* run:</span></span>


1. <span data-ttu-id="0d3bc-281">Redefina o banco de dados executando o seguinte comando no SSMS para excluir todos os dados inseridos pela execução anterior:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-281">Reset the database by running the following command in SSMS to delete all the data that was inserted by the previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="0d3bc-282">Edite a linha de comando do ostress.exe para substituir todos os *_inmem* por *_ondisk*.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-282">Edit the ostress.exe command line to replace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="0d3bc-283">Execute novamente o ostress.exe pela segunda vez e capture o resultado da duração.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-283">Rerun ostress.exe for the second time, and capture the duration result.</span></span>

4. <span data-ttu-id="0d3bc-284">Redefina novamente o banco de dados (para exclusão responsável do que pode ser uma grande quantidade de dados de teste).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-284">Again, reset the database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="0d3bc-285">Resultados esperados para a comparação</span><span class="sxs-lookup"><span data-stu-id="0d3bc-285">Expected comparison results</span></span>

<span data-ttu-id="0d3bc-286">Os testes In-Memory mostraram uma melhoria de desempenho de **nove vezes** para essa carga de trabalho simplista, com o ostress sendo executado em uma VM do Azure na mesma região do Azure que o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in the same Azure region as the database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-the-in-memory-analytics-sample"></a><span data-ttu-id="0d3bc-287">2. Instalar o exemplo de Análise Na Memória</span><span class="sxs-lookup"><span data-stu-id="0d3bc-287">2. Install the In-Memory Analytics sample</span></span>


<span data-ttu-id="0d3bc-288">Nesta seção, você vai comparar os resultados de E/S e de estatísticas ao usar um índice columnstore versus um índice b-tree tradicional.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-288">In this section, you compare the IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="0d3bc-289">Para fazer uma análise em tempo real em uma carga de trabalho OLTP, quase sempre será melhor usar um índice columnstore não clusterizado.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-289">For real-time analytics on an OLTP workload, it's often best to use a nonclustered columnstore index.</span></span> <span data-ttu-id="0d3bc-290">Para ver mais detalhes, confira [Índices Columnstore Descritos](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="0d3bc-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-the-columnstore-analytics-test"></a><span data-ttu-id="0d3bc-291">Preparar o teste de análise de columnstore</span><span class="sxs-lookup"><span data-stu-id="0d3bc-291">Prepare the columnstore analytics test</span></span>


1. <span data-ttu-id="0d3bc-292">Use o portal do Azure para criar um novo banco de dados AdventureWorksLT desde o exemplo.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-292">Use the Azure portal to create a fresh AdventureWorksLT database from the sample.</span></span>
 - <span data-ttu-id="0d3bc-293">Use esse nome exato.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-293">Use that exact name.</span></span>
 - <span data-ttu-id="0d3bc-294">Escolha qualquer camada de serviço Premium.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="0d3bc-295">Copie o [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) para sua área de transferência.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-295">Copy the [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) to your clipboard.</span></span>
 - <span data-ttu-id="0d3bc-296">O script T-SQL cria os objetos necessários In-Memory no banco de dados de exemplo AdventureWorksLT criado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-296">The T-SQL script creates the necessary In-Memory objects in the AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="0d3bc-297">O script cria a tabela Dimension e duas tabelas de fatos.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-297">The script creates the Dimension table and two fact tables.</span></span> <span data-ttu-id="0d3bc-298">As tabelas de fatos são preenchidas com 3,5 milhões de linhas cada.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-298">The fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="0d3bc-299">O script pode levar 15 minutos para ser concluído.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-299">The script might take 15 minutes to complete.</span></span>

3. <span data-ttu-id="0d3bc-300">Cole o script T-SQL no SSMS e execute o script.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-300">Paste the T-SQL script into SSMS, and then execute the script.</span></span> <span data-ttu-id="0d3bc-301">A palavra-chave **COLUMNSTORE** na instrução **CREATE INDEX** é crucial, como em:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-301">The **COLUMNSTORE** keyword in the **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="0d3bc-302">Defina o AdventureWorksLT com um nível de compatibilidade 130:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-302">Set AdventureWorksLT to compatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="0d3bc-303">O nível 130 não está diretamente relacionado aos recursos Na Memória.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-303">Level 130 is not directly related to In-Memory features.</span></span> <span data-ttu-id="0d3bc-304">Mas o nível 130 geralmente oferece desempenho de consulta mais rápido que o 120.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="0d3bc-305">Tabelas chave e índices de columnstore</span><span class="sxs-lookup"><span data-stu-id="0d3bc-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="0d3bc-306">dbo.FactResellerSalesXL_CCI é uma tabela com um índice columnstore clusterizado, que tem compactação avançada no nível de *dados*.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at the *data* level.</span></span>

- <span data-ttu-id="0d3bc-307">dbo.FactResellerSalesXL_PageCompressed é uma tabela com um índice clusterizado regular equivalente, compactado somente no nível de *página*.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at the *page* level.</span></span>


#### <a name="key-queries-to-compare-the-columnstore-index"></a><span data-ttu-id="0d3bc-308">Consultas chave para comparar o índice columnstore</span><span class="sxs-lookup"><span data-stu-id="0d3bc-308">Key queries to compare the columnstore index</span></span>


<span data-ttu-id="0d3bc-309">Há [diversos tipos de consulta T-SQL que podem ser executados](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) para ver as melhorias de desempenho.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) to see performance improvements.</span></span> <span data-ttu-id="0d3bc-310">Na etapa 2 no script T-SQL, preste atenção neste par de consultas.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-310">In step 2 in the T-SQL script, pay attention to this pair of queries.</span></span> <span data-ttu-id="0d3bc-311">Elas diferem apenas em uma linha:</span><span class="sxs-lookup"><span data-stu-id="0d3bc-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="0d3bc-312">Um índice columnstore clusterizado está na tabela FactResellerSalesXL\_CCI.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-312">A clustered columnstore index is in the FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="0d3bc-313">O seguinte trecho de script T-SQL imprime estatísticas de E/S e de TIME para a consulta de cada tabela.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-313">The following T-SQL script excerpt prints statistics for IO and TIME for the query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order to see Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins the Fact Table with dimension tables
-- Note this query will run on the Page Compressed table, Note down the time
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO

SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_PageCompressed a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO
SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO


-- This is the same Prior query on a table with a clustered columnstore index CCI
-- The comparison numbers are even more dramatic the larger the table is (this is an 11 million row table only)
SET STATISTICS IO ON
SET STATISTICS TIME ON
GO
SELECT c.Year
    ,e.ProductCategoryKey
    ,FirstName + ' ' + LastName AS FullName
    ,count(SalesOrderNumber) AS NumSales
    ,sum(SalesAmount) AS TotalSalesAmt
    ,Avg(SalesAmount) AS AvgSalesAmt
    ,count(DISTINCT SalesOrderNumber) AS NumOrders
    ,count(DISTINCT a.CustomerKey) AS CountCustomers
FROM FactResellerSalesXL_CCI a
INNER JOIN DimProduct b ON b.ProductKey = a.ProductKey
INNER JOIN DimCustomer d ON d.CustomerKey = a.CustomerKey
Inner JOIN DimProductSubCategory e on e.ProductSubcategoryKey = b.ProductSubcategoryKey
INNER JOIN DimDate c ON c.DateKey = a.OrderDateKey
GROUP BY e.ProductCategoryKey,c.Year,d.CustomerKey,d.FirstName,d.LastName
GO

SET STATISTICS IO OFF
SET STATISTICS TIME OFF
GO
```

<span data-ttu-id="0d3bc-314">Em um banco de dados com o tipo de preço P2, você pode esperar um ganho de desempenho de cerca de nove vezes para essa consulta usando o índice columnstore clusterizado em comparação com o índice tradicional.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-314">In a database with the P2 pricing tier, you can expect about nine times the performance gain for this query by using the clustered columnstore index compared with the traditional index.</span></span> <span data-ttu-id="0d3bc-315">Com P15, você pode esperar cerca de 57 vezes o ganho de desempenho ao usar o índice columnstore.</span><span class="sxs-lookup"><span data-stu-id="0d3bc-315">With P15, you can expect about 57 times the performance gain by using the columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="0d3bc-316">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="0d3bc-316">Next steps</span></span>

- [<span data-ttu-id="0d3bc-317">Início Rápido 1: Tecnologias OLTP in-memory para um desempenho mais rápido do T-SQL</span><span class="sxs-lookup"><span data-stu-id="0d3bc-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="0d3bc-318">Usar o OLTP In-Memory em um aplicativo existente do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0d3bc-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="0d3bc-319">[Monitorar o armazenamento do OLTP In-Memory](sql-database-in-memory-oltp-monitoring.md) para o OLTP In-Memory</span><span class="sxs-lookup"><span data-stu-id="0d3bc-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="0d3bc-320">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="0d3bc-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="0d3bc-321">Informações mais detalhadas</span><span class="sxs-lookup"><span data-stu-id="0d3bc-321">Deeper information</span></span>

- [<span data-ttu-id="0d3bc-322">Saiba como o Quorum dobra a principal carga de trabalho do banco de dados, enquanto reduz a DTU em 70% com o OLTP in-memory no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="0d3bc-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="0d3bc-323">Postagem de Blog de OLTP na memória do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="0d3bc-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="0d3bc-324">Saiba mais sobre o OLTP in-memory</span><span class="sxs-lookup"><span data-stu-id="0d3bc-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="0d3bc-325">Saiba mais sobre os índices columnstore</span><span class="sxs-lookup"><span data-stu-id="0d3bc-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="0d3bc-326">Saiba mais sobre a análise operacional em tempo real</span><span class="sxs-lookup"><span data-stu-id="0d3bc-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="0d3bc-327">Veja [Padrões comuns de carga de trabalho e considerações sobre migração](http://msdn.microsoft.com/library/dn673538.aspx) (que descreve os padrões de carga de trabalho para os quais o OLTP In-Memory geralmente fornece ganhos significativos de desempenho)</span><span class="sxs-lookup"><span data-stu-id="0d3bc-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="0d3bc-328">Design do aplicativo</span><span class="sxs-lookup"><span data-stu-id="0d3bc-328">Application design</span></span>

- [<span data-ttu-id="0d3bc-329">OLTP Na Memória (Otimização Na Memória)</span><span class="sxs-lookup"><span data-stu-id="0d3bc-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="0d3bc-330">Usar o OLTP In-Memory em um aplicativo existente do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="0d3bc-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="0d3bc-331">Ferramentas</span><span class="sxs-lookup"><span data-stu-id="0d3bc-331">Tools</span></span>

- [<span data-ttu-id="0d3bc-332">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="0d3bc-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="0d3bc-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="0d3bc-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="0d3bc-334">SSDT (Ferramentas de Dados do SQL Server)</span><span class="sxs-lookup"><span data-stu-id="0d3bc-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
