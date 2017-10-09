---
title: "tecnologias de banco de dados de SQL na memória aaaAzure | Microsoft Docs"
description: "Tecnologias de banco de dados de SQL na memória do Azure aprimorar o desempenho de saudação do transacional e de cargas de trabalho de análise. Saiba como tootake proveito dessas tecnologias."
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
ms.openlocfilehash: 1bacd7297b2f9b018853088eabf2a2ee66a9cb43
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="optimize-performance-by-using-in-memory-technologies-in-sql-database"></a><span data-ttu-id="dd75d-104">Otimizar o desempenho usando tecnologias In-Memory no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="dd75d-104">Optimize performance by using In-Memory technologies in SQL Database</span></span>

<span data-ttu-id="dd75d-105">Usando tecnologias In-Memory no Banco de Dados SQL do Azure, você pode obter melhorias no desempenho com várias cargas de trabalho: transacional (OLTP [processamento transacional online]), análise (OLAP [processamento analítico online]) e misto (HTAP [processamento híbrido analítico/de transação]).</span><span class="sxs-lookup"><span data-stu-id="dd75d-105">By using In-Memory technologies in Azure SQL Database, you can achieve performance improvements with various workloads: transactional (online transactional processing (OLTP)), analytics (online analytical processing (OLAP)), and mixed (hybrid transaction/analytical processing (HTAP)).</span></span> <span data-ttu-id="dd75d-106">Porque hello mais eficiente de consultas e processamento de transações, tecnologias na memória também ajudarão-lo tooreduce custo.</span><span class="sxs-lookup"><span data-stu-id="dd75d-106">Because of hello more efficient query and transaction processing, In-Memory technologies also help you tooreduce cost.</span></span> <span data-ttu-id="dd75d-107">Normalmente, você não precisa tooupgrade Olá preço de saudação ganhos de desempenho de tooachieve de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="dd75d-107">You typically don't need tooupgrade hello pricing tier of hello database tooachieve performance gains.</span></span> <span data-ttu-id="dd75d-108">Em alguns casos, você mesmo poderá reduzir Olá preço, enquanto continua vendo melhorias de desempenho com tecnologias na memória.</span><span class="sxs-lookup"><span data-stu-id="dd75d-108">In some cases, you might even be able reduce hello pricing tier, while still seeing performance improvements with In-Memory technologies.</span></span>

<span data-ttu-id="dd75d-109">Aqui estão dois exemplos de como o OLTP na memória ajudou toosignificantly melhorar o desempenho:</span><span class="sxs-lookup"><span data-stu-id="dd75d-109">Here are two examples of how In-Memory OLTP helped toosignificantly improve performance:</span></span>

- <span data-ttu-id="dd75d-110">Usando OLTP na memória, [soluções de negócios de Quorum foi capaz de toodouble sua carga de trabalho melhorando DTUs em 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span><span class="sxs-lookup"><span data-stu-id="dd75d-110">By using In-Memory OLTP, [Quorum Business Solutions was able toodouble their workload while improving DTUs by 70%](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database).</span></span>
    - <span data-ttu-id="dd75d-111">DTU significa *unidade de taxa de transferência de banco de dados* e inclui uma medição de consumo de recursos.</span><span class="sxs-lookup"><span data-stu-id="dd75d-111">DTU means *database throughput unit*, and it includes a mesurement of resource consumption.</span></span>
- <span data-ttu-id="dd75d-112">Olá, vídeo a seguir demonstra uma melhoria significativa no consumo de recursos com uma carga de trabalho de exemplo: [OLTP na memória de vídeo de banco de dados do SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span><span class="sxs-lookup"><span data-stu-id="dd75d-112">hello following video demonstrates significant improvement in resource consumption with a sample workload: [In-Memory OLTP in Azure SQL Database Video](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB).</span></span>
    - <span data-ttu-id="dd75d-113">Para obter mais detalhes, consulte Olá postagem de blog: [OLTP na memória na postagem do Blog de banco de dados do Azure SQL](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span><span class="sxs-lookup"><span data-stu-id="dd75d-113">For more details, see hello blog post: [In-Memory OLTP in Azure SQL Database Blog Post](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)</span></span>

<span data-ttu-id="dd75d-114">Tecnologias na memória estão disponíveis em todos os bancos de dados da camada Premium Olá, incluindo bancos de dados em pools Elásticos Premium.</span><span class="sxs-lookup"><span data-stu-id="dd75d-114">In-Memory technologies are available in all databases in hello Premium tier, including databases in Premium elastic pools.</span></span>

<span data-ttu-id="dd75d-115">Hello vídeo a seguir explica os ganhos potenciais de desempenho com tecnologias na memória no banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="dd75d-115">hello following video explains potential performance gains with In-Memory technologies in Azure SQL Database.</span></span> <span data-ttu-id="dd75d-116">Lembre-se que o ganho de desempenho Olá que você sempre vê depende de muitos fatores, incluindo a natureza de saudação de carga de trabalho de saudação e dados, o padrão de acesso de banco de dados Olá e assim por diante.</span><span class="sxs-lookup"><span data-stu-id="dd75d-116">Remember that hello performance gain that you see always depends on many factors, including hello nature of hello workload and data, access pattern of hello database, and so on.</span></span>

> [!VIDEO https://channel9.msdn.com/Blogs/Azure/Azure-SQL-Database-In-Memory-Technologies/player]
>
>

<span data-ttu-id="dd75d-117">Banco de dados SQL do Azure tem Olá tecnologias na memória a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd75d-117">Azure SQL Database has hello following In-Memory technologies:</span></span>

- <span data-ttu-id="dd75d-118">O *OLTP in-memory* aumenta a taxa de transferência e reduz a latência do processamento de transações.</span><span class="sxs-lookup"><span data-stu-id="dd75d-118">*In-Memory OLTP* increases throughput and reduces latency for transaction processing.</span></span> <span data-ttu-id="dd75d-119">Os cenários que se beneficiam do OLTP In-Memory são: processamento de transações de alta taxa de transferência, como comércio e jogos, ingestão de dados de eventos ou dispositivos IoT, cache, carregamento de dados e cenários de variáveis de tabela e tabelas temporárias.</span><span class="sxs-lookup"><span data-stu-id="dd75d-119">Scenarios that benefit from In-Memory OLTP are: high-throughput transaction processing such as trading and gaming, data ingestion from events or IoT devices, caching, data load, and temporary table and table variable scenarios.</span></span>
- <span data-ttu-id="dd75d-120">*Índices columnstore clusterizados* reduzir o volume de armazenamento (os tempos de too10) e melhorar o desempenho de consultas de relatórios e análises.</span><span class="sxs-lookup"><span data-stu-id="dd75d-120">*Clustered columnstore indexes* reduce your storage footprint (up too10 times) and improve performance for reporting and analytics queries.</span></span> <span data-ttu-id="dd75d-121">Você pode usá-lo com as tabelas de fatos em seu toofit armazéns de dados mais dados no banco de dados e melhorar o desempenho.</span><span class="sxs-lookup"><span data-stu-id="dd75d-121">You can use it with fact tables in your data marts toofit more data in your database and improve performance.</span></span> <span data-ttu-id="dd75d-122">Além disso, você pode usá-lo com os dados históricos em tooarchive seu banco de dados operacional e ser capaz de tooquery too10 horas mais dados.</span><span class="sxs-lookup"><span data-stu-id="dd75d-122">Also, you can use it with historical data in your operational database tooarchive and be able tooquery up too10 times more data.</span></span>
- <span data-ttu-id="dd75d-123">*Índices columnstore não clusterizados* para obter ajuda HTAP você toogain de informações em tempo real em seus negócios por meio de consulta Olá operacional do banco de dados diretamente, sem Olá necessidade toorun um cara extração, transformação e processo de carregamento (ETL) e aguarde para toobe de depósito de dados Olá preenchido.</span><span class="sxs-lookup"><span data-stu-id="dd75d-123">*Nonclustered columnstore indexes* for HTAP help you toogain real-time insights into your business through querying hello operational database directly, without hello need toorun an expensive extract, transform, and load (ETL) process and wait for hello data warehouse toobe populated.</span></span> <span data-ttu-id="dd75d-124">Índices columnstore não clusterizados permitem a execução muito rápida de consultas de análise no banco de dados OLTP hello, reduzindo o impacto de Olá na carga de trabalho operacional hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-124">Nonclustered columnstore indexes allow very fast execution of analytics queries on hello OLTP database, while reducing hello impact on hello operational workload.</span></span>
- <span data-ttu-id="dd75d-125">Você também pode ter a combinação de saudação de uma tabela com otimização de memória com um índice columnstore.</span><span class="sxs-lookup"><span data-stu-id="dd75d-125">You can also have hello combination of a memory-optimized table with a columnstore index.</span></span> <span data-ttu-id="dd75d-126">Essa combinação permite que você tooperform transação muito rápido processamento e muito*simultaneamente* executar análise de consultas muito rapidamente em Olá mesmo dados.</span><span class="sxs-lookup"><span data-stu-id="dd75d-126">This combination enables you tooperform very fast transaction processing, and too*concurrently* run analytics queries very quickly on hello same data.</span></span>

<span data-ttu-id="dd75d-127">Índices columnstore e OLTP na memória tem sido parte do produto do SQL Server Olá desde 2012 e 2014, respectivamente.</span><span class="sxs-lookup"><span data-stu-id="dd75d-127">Both columnstore indexes and In-Memory OLTP have been part of hello SQL Server product since 2012 and 2014, respectively.</span></span> <span data-ttu-id="dd75d-128">SQL Server e banco de dados SQL do Azure compartilham Olá mesma implementação das tecnologias na memória.</span><span class="sxs-lookup"><span data-stu-id="dd75d-128">Azure SQL Database and SQL Server share hello same implementation of In-Memory technologies.</span></span> <span data-ttu-id="dd75d-129">Daqui em diante, os novos recursos para essas tecnologias serão lançados primeiro no Banco de Dados SQL do Azure, antes de serem lançados no SQL Server.</span><span class="sxs-lookup"><span data-stu-id="dd75d-129">Going forward, new capabilities for these technologies are released in Azure SQL Database first, before they are released in SQL Server.</span></span>

<span data-ttu-id="dd75d-130">Este tópico descreve os aspectos de índices columnstore e OLTP na memória que são específico tooAzure banco de dados SQL e também inclui exemplos:</span><span class="sxs-lookup"><span data-stu-id="dd75d-130">This topic describes aspects of In-Memory OLTP and columnstore indexes that are specific tooAzure SQL Database and also includes samples:</span></span>
- <span data-ttu-id="dd75d-131">Você verá o impacto de saudação dessas tecnologias em limites de tamanho de armazenamento e os dados.</span><span class="sxs-lookup"><span data-stu-id="dd75d-131">You'll see hello impact of these technologies on storage and data size limits.</span></span>
- <span data-ttu-id="dd75d-132">Você verá como toomanage Olá movimentação de bancos de dados usar essas tecnologias entre hello diferente camadas de preços.</span><span class="sxs-lookup"><span data-stu-id="dd75d-132">You'll see how toomanage hello movement of databases that use these technologies between hello different pricing tiers.</span></span>
- <span data-ttu-id="dd75d-133">Você verá dois exemplos que ilustram o uso de saudação do OLTP na memória, bem como índices columnstore no banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="dd75d-133">You'll see two samples that illustrate hello use of In-Memory OLTP, as well as columnstore indexes in Azure SQL Database.</span></span>

<span data-ttu-id="dd75d-134">Consulte Olá recursos para obter mais informações a seguir.</span><span class="sxs-lookup"><span data-stu-id="dd75d-134">See hello following resources for more information.</span></span>

<span data-ttu-id="dd75d-135">Informações detalhadas sobre as tecnologias de saudação:</span><span class="sxs-lookup"><span data-stu-id="dd75d-135">In-depth information about hello technologies:</span></span>

- <span data-ttu-id="dd75d-136">[Visão geral de OLTP na memória e cenários de uso](https://msdn.microsoft.com/library/mt774593.aspx) (inclui referências estudos de caso de toocustomer e informações tooget iniciado)</span><span class="sxs-lookup"><span data-stu-id="dd75d-136">[In-Memory OLTP Overview and Usage Scenarios](https://msdn.microsoft.com/library/mt774593.aspx) (includes references toocustomer case studies and information tooget started)</span></span>
- [<span data-ttu-id="dd75d-137">Documentação para OLTP in-memory</span><span class="sxs-lookup"><span data-stu-id="dd75d-137">Documentation for In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)
- [<span data-ttu-id="dd75d-138">Guia de índices ColumnStore</span><span class="sxs-lookup"><span data-stu-id="dd75d-138">Columnstore Indexes Guide</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)
- <span data-ttu-id="dd75d-139">HTAP (Processamento Transacional e Analítico Híbrido), também conhecido como [análise operacional em tempo real](https://msdn.microsoft.com/library/dn817827.aspx)</span><span class="sxs-lookup"><span data-stu-id="dd75d-139">Hybrid transactional/analytical processing (HTAP), also known as [real-time operational analytics](https://msdn.microsoft.com/library/dn817827.aspx)</span></span>

<span data-ttu-id="dd75d-140">Uma rápida introdução em OLTP na memória: [início rápido 1: tecnologias do OLTP na memória para um desempenho mais rápido do T-SQL](http://msdn.microsoft.com/library/mt694156.aspx) (outro artigo toohelp começar)</span><span class="sxs-lookup"><span data-stu-id="dd75d-140">A quick primer on In-Memory OLTP: [Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance](http://msdn.microsoft.com/library/mt694156.aspx) (another article toohelp you get started)</span></span>

<span data-ttu-id="dd75d-141">Vídeos detalhados sobre as tecnologias de saudação:</span><span class="sxs-lookup"><span data-stu-id="dd75d-141">In-depth videos about hello technologies:</span></span>

- <span data-ttu-id="dd75d-142">[O OLTP na memória no banco de dados do SQL Azure](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (que contém uma demonstração de desempenho de benefícios e as etapas tooreproduce esses resultados por conta própria)</span><span class="sxs-lookup"><span data-stu-id="dd75d-142">[In-Memory OLTP in Azure SQL Database](https://channel9.msdn.com/Shows/Data-Exposed/In-Memory-OTLP-in-Azure-SQL-DB) (which contains a demo of performance benefits and steps tooreproduce these results yourself)</span></span>
- [<span data-ttu-id="dd75d-143">Vídeos OLTP na memória: O que é e quando/como toouse-lo</span><span class="sxs-lookup"><span data-stu-id="dd75d-143">In-Memory OLTP Videos: What it is and When/How toouse it</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/03/in-memory-oltp-video-what-it-is-and-whenhow-to-use-it/)
- [<span data-ttu-id="dd75d-144">Índice Columnstore: vídeos sobre a análise em memória do Ignite 2016</span><span class="sxs-lookup"><span data-stu-id="dd75d-144">Columnstore Index: In-Memory Analytics Videos from Ignite 2016</span></span>](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/10/04/columnstore-index-in-memory-analytics-i-e-columnstore-index-videos-from-ignite-2016/)

## <a name="storage-and-data-size"></a><span data-ttu-id="dd75d-145">Armazenamento e tamanho dos dados</span><span class="sxs-lookup"><span data-stu-id="dd75d-145">Storage and data size</span></span>

### <a name="data-size-and-storage-cap-for-in-memory-oltp"></a><span data-ttu-id="dd75d-146">Tamanho dos dados e limite de armazenamento do OLTP in-memory</span><span class="sxs-lookup"><span data-stu-id="dd75d-146">Data size and storage cap for In-Memory OLTP</span></span>

<span data-ttu-id="dd75d-147">O OLTP in-memory inclui tabelas com otimização de memória, que são usadas para armazenar dados do usuário.</span><span class="sxs-lookup"><span data-stu-id="dd75d-147">In-Memory OLTP includes memory-optimized tables, which are used for storing user data.</span></span> <span data-ttu-id="dd75d-148">Essas tabelas são necessária toofit na memória.</span><span class="sxs-lookup"><span data-stu-id="dd75d-148">These tables are required toofit in memory.</span></span> <span data-ttu-id="dd75d-149">Porque você gerencia memória diretamente em Olá serviço de banco de dados SQL, temos o conceito de saudação de uma cota para dados de usuário.</span><span class="sxs-lookup"><span data-stu-id="dd75d-149">Because you manage memory directly in hello SQL Database service, we have hello  concept of a quota for user data.</span></span> <span data-ttu-id="dd75d-150">Essa ideia é chamado tooas *armazenamento OLTP na memória*.</span><span class="sxs-lookup"><span data-stu-id="dd75d-150">This idea is referred tooas *In-Memory OLTP storage*.</span></span>

<span data-ttu-id="dd75d-151">Cada tipo de preço de banco de dados independente e cada tipo de preço de pool elástico com suporte incluem determinada quantidade de Armazenamento do OLTP in-memory.</span><span class="sxs-lookup"><span data-stu-id="dd75d-151">Each supported standalone database pricing tier and each elastic pool pricing tier includes a certain amount of In-Memory OLTP storage.</span></span> <span data-ttu-id="dd75d-152">No momento da saudação de gravação, você obterá um gigabyte de armazenamento para cada 125 unidades de transação do banco de dados (DTUs) ou o banco de dados Elástico unidades de transação (eDTUs).</span><span class="sxs-lookup"><span data-stu-id="dd75d-152">At hello time of writing, you get a gigabyte of storage for every 125 database transaction units (DTUs) or elastic database transaction units (eDTUs).</span></span>

<span data-ttu-id="dd75d-153">Olá [camadas de serviço do banco de dados SQL](sql-database-service-tiers.md) artigo possui a lista oficial Olá Olá OLTP na memória de armazenamento do que está disponível para cada banco de dados autônomo e camada de preços de pool Elástico.</span><span class="sxs-lookup"><span data-stu-id="dd75d-153">hello [SQL Database service tiers](sql-database-service-tiers.md) article has hello official list of hello In-Memory OLTP storage that is available for each supported standalone database and elastic pool pricing tier.</span></span>

<span data-ttu-id="dd75d-154">saudação de contagem de itens para o limite de armazenamento do OLTP na memória a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd75d-154">hello following items count toward your In-Memory OLTP storage cap:</span></span>

- <span data-ttu-id="dd75d-155">Linhas de dados de usuário ativo em tabelas com otimização de memória e variáveis de tabela.</span><span class="sxs-lookup"><span data-stu-id="dd75d-155">Active user data rows in memory-optimized tables and table variables.</span></span> <span data-ttu-id="dd75d-156">Observe que as versões antigas de linha não são contadas cap hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-156">Note that old row versions don't count toward hello cap.</span></span>
- <span data-ttu-id="dd75d-157">Índices em tabelas com otimização de memória.</span><span class="sxs-lookup"><span data-stu-id="dd75d-157">Indexes on memory-optimized tables.</span></span>
- <span data-ttu-id="dd75d-158">Custo operacional das operações ALTER TABLE.</span><span class="sxs-lookup"><span data-stu-id="dd75d-158">Operational overhead of ALTER TABLE operations.</span></span>

<span data-ttu-id="dd75d-159">Se você atingir o limite Olá, você receberá um erro de limite de cota, e você não é mais capaz de dados tooinsert ou atualização.</span><span class="sxs-lookup"><span data-stu-id="dd75d-159">If you hit hello cap, you receive an out-of-quota error, and you are no longer able tooinsert or update data.</span></span> <span data-ttu-id="dd75d-160">toomitigate esse erro, exclua dados ou aumente Olá preço do banco de dados de saudação ou pool.</span><span class="sxs-lookup"><span data-stu-id="dd75d-160">toomitigate this error, delete data or increase hello pricing tier of hello database or pool.</span></span>

<span data-ttu-id="dd75d-161">Para obter detalhes sobre como monitorar a utilização de armazenamento do OLTP na memória e como configurar alertas quando é atingido o limite de saudação quase, consulte [armazenamento na memória do Monitor](sql-database-in-memory-oltp-monitoring.md).</span><span class="sxs-lookup"><span data-stu-id="dd75d-161">For details about monitoring In-Memory OLTP storage utilization and configuring alerts when you almost hit hello cap, see [Monitor In-Memory storage](sql-database-in-memory-oltp-monitoring.md).</span></span>

#### <a name="about-elastic-pools"></a><span data-ttu-id="dd75d-162">Sobre pools elásticos</span><span class="sxs-lookup"><span data-stu-id="dd75d-162">About elastic pools</span></span>

<span data-ttu-id="dd75d-163">Com pools Elásticos, Olá armazenamento OLTP na memória é compartilhada entre todos os bancos de dados no pool de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd75d-163">With elastic pools, hello In-Memory OLTP storage is shared across all databases in hello pool.</span></span> <span data-ttu-id="dd75d-164">Portanto, o uso de saudação em um banco de dados pode afetar potencialmente outros bancos de dados.</span><span class="sxs-lookup"><span data-stu-id="dd75d-164">Therefore, hello usage in one database can potentially affect other databases.</span></span> <span data-ttu-id="dd75d-165">As duas mitigações para esse problema são:</span><span class="sxs-lookup"><span data-stu-id="dd75d-165">Two mitigations for this are:</span></span>

- <span data-ttu-id="dd75d-166">Configure um Max-eDTU para bancos de dados que é menor do que a contagem de eDTU Olá para pool hello como um todo.</span><span class="sxs-lookup"><span data-stu-id="dd75d-166">Configure a Max-eDTU for databases that is lower than hello eDTU count for hello pool as a whole.</span></span> <span data-ttu-id="dd75d-167">Esse máximo Arredonda a utilização do armazenamento Olá OLTP na memória, em qualquer banco de dados no pool de hello, tamanho toohello que corresponde a contagem de eDTU toohello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-167">This maximum caps hello In-Memory OLTP storage utilization, in any database in hello pool, toohello size that corresponds toohello eDTU count.</span></span>
- <span data-ttu-id="dd75d-168">Defina um Min-eDTU maior que 0.</span><span class="sxs-lookup"><span data-stu-id="dd75d-168">Configure a Min-eDTU that is greater than 0.</span></span> <span data-ttu-id="dd75d-169">Este mínimo garante que cada banco de dados no pool de saudação tenha a quantidade de saudação do armazenamento de OLTP na memória disponível que corresponde a toohello configurado eDTU mínimo.</span><span class="sxs-lookup"><span data-stu-id="dd75d-169">This minimum guarantees that each database in hello pool has hello amount of available In-Memory OLTP storage that corresponds toohello configured Min-eDTU.</span></span>

### <a name="data-size-and-storage-for-columnstore-indexes"></a><span data-ttu-id="dd75d-170">Tamanho dos dados e armazenamento para índices columnstore</span><span class="sxs-lookup"><span data-stu-id="dd75d-170">Data size and storage for columnstore indexes</span></span>

<span data-ttu-id="dd75d-171">Índices ColumnStore não são necessária toofit na memória.</span><span class="sxs-lookup"><span data-stu-id="dd75d-171">Columnstore indexes aren't required toofit in memory.</span></span> <span data-ttu-id="dd75d-172">Portanto, Olá apenas limite no tamanho de saudação de índices Olá Olá geral o tamanho máximo, que está documentado na Olá [camadas de serviço do banco de dados SQL](sql-database-service-tiers.md) artigo.</span><span class="sxs-lookup"><span data-stu-id="dd75d-172">Therefore, hello only cap on hello size of hello indexes is hello maximum overall database size, which is documented in hello [SQL Database service tiers](sql-database-service-tiers.md) article.</span></span>

<span data-ttu-id="dd75d-173">Quando você usa os índices columnstore clusterizados, compactação Colunar é usada para o armazenamento de tabela base hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-173">When you use clustered columnstore indexes, columnar compression is used for hello base table storage.</span></span> <span data-ttu-id="dd75d-174">Essa compactação pode reduzir significativamente o volume de armazenamento de saudação de seus dados de usuário, o que significa que você pode colocar mais dados no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd75d-174">This compression can significantly reduce hello storage footprint of your user data, which means that you can fit more data in hello database.</span></span> <span data-ttu-id="dd75d-175">E compactação Olá pode ser aumentada com [compactação de arquivamento Colunar](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span><span class="sxs-lookup"><span data-stu-id="dd75d-175">And hello compression can be further increased with [columnar archival compression](https://msdn.microsoft.com/library/cc280449.aspx#Using Columnstore and Columnstore Archive Compression).</span></span> <span data-ttu-id="dd75d-176">Olá compactação que você pode obter depende da natureza de saudação do dados saudação, mas a compactação de saudação 10 vezes não é incomum.</span><span class="sxs-lookup"><span data-stu-id="dd75d-176">hello amount of compression that you can achieve depends on hello nature of hello data, but 10 times hello compression is not uncommon.</span></span>

<span data-ttu-id="dd75d-177">Por exemplo, se você tiver um banco de dados com um tamanho máximo de 1 TB (terabyte) e obter a compactação Olá 10 vezes usando índices columnstore, você pode ajustar um total de 10 TB de dados de usuário no banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd75d-177">For example, if you have a database with a maximum size of 1 terabyte (TB) and you achieve 10 times hello compression by using columnstore indexes, you can fit a total of 10 TB of user data in hello database.</span></span>

<span data-ttu-id="dd75d-178">Quando você usar índices columnstore não clusterizado, tabela base Olá ainda é armazenada em formato de rowstore tradicionais de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd75d-178">When you use nonclustered columnstore indexes, hello base table is still stored in hello traditional rowstore format.</span></span> <span data-ttu-id="dd75d-179">Portanto, Olá economia de armazenamento não é tão grande como com índices columnstore clusterizados.</span><span class="sxs-lookup"><span data-stu-id="dd75d-179">Therefore, hello storage savings aren't as big as with clustered columnstore indexes.</span></span> <span data-ttu-id="dd75d-180">No entanto, se você estiver substituindo um número de índices não clusterizados tradicionais com um único índice columnstore, você ainda pode ver uma economia geral no espaço de armazenamento Olá para a tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd75d-180">However, if you're replacing a number of traditional nonclustered indexes with a single columnstore index, you can still see an overall savings in hello storage footprint for hello table.</span></span>

## <a name="moving-databases-that-use-in-memory-technologies-between-pricing-tiers"></a><span data-ttu-id="dd75d-181">Movendo bancos de dados que usam tecnologias In-Memory entre tipos de preço</span><span class="sxs-lookup"><span data-stu-id="dd75d-181">Moving databases that use In-Memory technologies between pricing tiers</span></span>

<span data-ttu-id="dd75d-182">Há nunca quaisquer incompatibilidades ou outros problemas ao atualizar tooa maior preço, como de tooPremium padrão.</span><span class="sxs-lookup"><span data-stu-id="dd75d-182">There are never any incompatibilities or other problems when you upgrade tooa higher pricing tier, such as from Standard tooPremium.</span></span> <span data-ttu-id="dd75d-183">recursos e funcionalidades disponíveis Olá apenas aumentam.</span><span class="sxs-lookup"><span data-stu-id="dd75d-183">hello available functionality and resources only increase.</span></span>

<span data-ttu-id="dd75d-184">Mas Olá downgrade preço pode afetar negativamente o seu banco de dados.</span><span class="sxs-lookup"><span data-stu-id="dd75d-184">But downgrading hello pricing tier can negatively impact your database.</span></span> <span data-ttu-id="dd75d-185">impacto de saudação é especialmente aparente quando você fazer o downgrade de tooStandard Premium ou Basic ao seu banco de dados contém objetos OLTP na memória.</span><span class="sxs-lookup"><span data-stu-id="dd75d-185">hello impact is especially apparent when you downgrade from Premium tooStandard or Basic when your database contains In-Memory OLTP objects.</span></span> <span data-ttu-id="dd75d-186">Tabelas com otimização de memória e índices columnstore, não estão disponíveis após o downgrade da saudação (mesmo se elas permanecem visíveis).</span><span class="sxs-lookup"><span data-stu-id="dd75d-186">Memory-optimized tables, and columnstore indexes, are unavailable after hello downgrade (even if they remain visible).</span></span> <span data-ttu-id="dd75d-187">Olá mesmas considerações se aplicam quando você está diminuindo Olá preço de um pool Elástico ou mover um banco de dados com tecnologias na memória, em um padrão ou básico pool Elástico.</span><span class="sxs-lookup"><span data-stu-id="dd75d-187">hello same considerations apply when you're lowering hello pricing tier of an elastic pool, or moving a database with In-Memory technologies, into a Standard or Basic elastic pool.</span></span>

### <a name="in-memory-oltp"></a><span data-ttu-id="dd75d-188">OLTP Na Memória</span><span class="sxs-lookup"><span data-stu-id="dd75d-188">In-Memory OLTP</span></span>

<span data-ttu-id="dd75d-189">*Fazendo downgrade tooBasic/Standard*: OLTP na memória não tem suporte em bancos de dados Olá camada Standard ou Basic.</span><span class="sxs-lookup"><span data-stu-id="dd75d-189">*Downgrading tooBasic/Standard*: In-Memory OLTP isn't supported in databases in hello Standard or Basic tier.</span></span> <span data-ttu-id="dd75d-190">Além disso, não é possível toomove um banco de dados que tenha qualquer toohello de objetos OLTP na memória camada Standard ou Basic.</span><span class="sxs-lookup"><span data-stu-id="dd75d-190">In addition, it isn't possible toomove a database that has any In-Memory OLTP objects toohello Standard or Basic tier.</span></span>

<span data-ttu-id="dd75d-191">Antes de fazer o downgrade do banco de dados de saudação tooStandard/Basic, remova todas as tabelas com otimização de memória e os tipos de tabela, bem como todos os módulos do T-SQL compilados nativamente.</span><span class="sxs-lookup"><span data-stu-id="dd75d-191">Before you downgrade hello database tooStandard/Basic, remove all memory-optimized tables and table types, as well as all natively compiled T-SQL modules.</span></span>

<span data-ttu-id="dd75d-192">Não há um modo programático toounderstand se um determinado banco de dados oferece suporte a OLTP na memória.</span><span class="sxs-lookup"><span data-stu-id="dd75d-192">There is a programmatic way toounderstand whether a given database supports In-Memory OLTP.</span></span> <span data-ttu-id="dd75d-193">Você pode executar Olá consulta Transact-SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd75d-193">You can execute hello following Transact-SQL query:</span></span>

```
SELECT DatabasePropertyEx(DB_NAME(), 'IsXTPSupported');
```

<span data-ttu-id="dd75d-194">Se a consulta Olá retorna **1**, há suporte para o OLTP na memória no banco de dados.</span><span class="sxs-lookup"><span data-stu-id="dd75d-194">If hello query returns **1**, In-Memory OLTP is supported in this database.</span></span>


<span data-ttu-id="dd75d-195">*Fazendo downgrade de nível mais baixo de Premium tooa*: dados em tabelas com otimização de memória devem se ajustar no armazenamento do OLTP na memória Olá que está associado a saudação de preço do banco de dados de saudação ou está disponível no pool Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-195">*Downgrading tooa lower Premium tier*: Data in memory-optimized tables must fit within hello In-Memory OLTP storage that is associated with hello pricing tier of hello database or is available in hello elastic pool.</span></span> <span data-ttu-id="dd75d-196">Se você tentar Olá toolower preço ou move o banco de dados de saudação em um pool que não tem o armazenamento de OLTP na memória suficiente disponível, Olá operação falhará.</span><span class="sxs-lookup"><span data-stu-id="dd75d-196">If you try toolower hello pricing tier or move hello database into a pool that doesn't have enough available In-Memory OLTP storage, hello operation fails.</span></span>

### <a name="columnstore-indexes"></a><span data-ttu-id="dd75d-197">Índices ColumnStore</span><span class="sxs-lookup"><span data-stu-id="dd75d-197">Columnstore indexes</span></span>

<span data-ttu-id="dd75d-198">*Fazendo downgrade tooBasic ou padrão*: Columnstore índices têm suporte apenas de preço Premium Olá e não no hello camadas Standard ou Basic.</span><span class="sxs-lookup"><span data-stu-id="dd75d-198">*Downgrading tooBasic or Standard*: Columnstore indexes are supported only on hello Premium pricing tier, and not on hello Standard or Basic tiers.</span></span> <span data-ttu-id="dd75d-199">Quando você fazer downgrade do seu banco de dados tooStandard ou Basic, o índice columnstore ficará indisponível.</span><span class="sxs-lookup"><span data-stu-id="dd75d-199">When you downgrade your database tooStandard or Basic, your columnstore index becomes unavailable.</span></span> <span data-ttu-id="dd75d-200">sistema de saudação mantém o índice columnstore, mas ele nunca utiliza um índice de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd75d-200">hello system maintains your columnstore index, but it never leverages hello index.</span></span> <span data-ttu-id="dd75d-201">Se você atualizar o tooPremium voltar mais tarde, o índice columnstore é imediatamente pronto toobe utilizada novamente.</span><span class="sxs-lookup"><span data-stu-id="dd75d-201">If you later upgrade back tooPremium, your columnstore index is immediately ready toobe leveraged again.</span></span>

<span data-ttu-id="dd75d-202">Se você tiver um **clusterizado** índice columnstore, toda a tabela Olá fica indisponível após o downgrade da camada.</span><span class="sxs-lookup"><span data-stu-id="dd75d-202">If you have a **clustered** columnstore index, hello whole table becomes unavailable after tier downgrade.</span></span> <span data-ttu-id="dd75d-203">Portanto, recomendamos que você remova todos os *clusterizado* antes de fazer o downgrade do seu banco de dados abaixo da camada de Premium Olá dos índices columnstore.</span><span class="sxs-lookup"><span data-stu-id="dd75d-203">Therefore we recommend that you drop all *clustered* columnstore indexes before you downgrade your database below hello Premium tier.</span></span>

<span data-ttu-id="dd75d-204">*Fazendo downgrade de nível mais baixo de Premium tooa*: este downgrade terá êxito se o banco de dados inteiro Olá adequada Olá o tamanho máximo para o destino de saudação preço, ou em armazenamento de saudação disponível no pool Elástico hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-204">*Downgrading tooa lower Premium tier*: This downgrade succeeds if hello whole database fits within hello maximum database size for hello target pricing tier, or within hello available storage in hello elastic pool.</span></span> <span data-ttu-id="dd75d-205">Não há nenhum impacto específico de índices de columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-205">There is no specific impact from hello columnstore indexes.</span></span>


<a id="install_oltp_manuallink" name="install_oltp_manuallink"></a>

&nbsp;

## <a name="1-install-hello-in-memory-oltp-sample"></a><span data-ttu-id="dd75d-206">1. Instalar o exemplo de OLTP na memória hello</span><span class="sxs-lookup"><span data-stu-id="dd75d-206">1. Install hello In-Memory OLTP sample</span></span>

<span data-ttu-id="dd75d-207">Você pode criar o banco de dados do exemplo hello AdventureWorksLT com alguns cliques no hello [portal do Azure](https://portal.azure.com/).</span><span class="sxs-lookup"><span data-stu-id="dd75d-207">You can create hello AdventureWorksLT sample database with a few clicks in hello [Azure portal](https://portal.azure.com/).</span></span> <span data-ttu-id="dd75d-208">Em seguida, hello etapas nesta seção explicam como você pode aprimorar seu banco de dados AdventureWorksLT com objetos OLTP na memória e demonstrar os benefícios de desempenho.</span><span class="sxs-lookup"><span data-stu-id="dd75d-208">Then, hello steps in this section explain how you can enrich your AdventureWorksLT database with In-Memory OLTP objects and demonstrate performance benefits.</span></span>

<span data-ttu-id="dd75d-209">Para ver uma demonstração de desempenho mais simples, porém, mais visualmente interessante do OLTP in-memory, veja:</span><span class="sxs-lookup"><span data-stu-id="dd75d-209">For a more simplistic, but more visually appealing performance demo for In-Memory OLTP, see:</span></span>

- <span data-ttu-id="dd75d-210">Versão: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span><span class="sxs-lookup"><span data-stu-id="dd75d-210">Release: [in-memory-oltp-demo-v1.0](https://github.com/Microsoft/sql-server-samples/releases/tag/in-memory-oltp-demo-v1.0)</span></span>
- <span data-ttu-id="dd75d-211">Código-fonte: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span><span class="sxs-lookup"><span data-stu-id="dd75d-211">Source code: [in-memory-oltp-demo-source-code](https://github.com/Microsoft/sql-server-samples/tree/master/samples/features/in-memory/ticket-reservations)</span></span>

#### <a name="installation-steps"></a><span data-ttu-id="dd75d-212">Etapas de instalação</span><span class="sxs-lookup"><span data-stu-id="dd75d-212">Installation steps</span></span>

1. <span data-ttu-id="dd75d-213">Em Olá [portal do Azure](https://portal.azure.com/), criar um banco de dados Premium em um servidor.</span><span class="sxs-lookup"><span data-stu-id="dd75d-213">In hello [Azure portal](https://portal.azure.com/), create a Premium database on a server.</span></span> <span data-ttu-id="dd75d-214">Saudação de conjunto **fonte** toohello AdventureWorksLT de dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="dd75d-214">Set hello **Source** toohello AdventureWorksLT sample database.</span></span> <span data-ttu-id="dd75d-215">Para obter instruções detalhadas, consulte [Criar seu primeiro Banco de Dados SQL do Azure](sql-database-get-started-portal.md).</span><span class="sxs-lookup"><span data-stu-id="dd75d-215">For detailed instructions, see [Create your first Azure SQL database](sql-database-get-started-portal.md).</span></span>

2. <span data-ttu-id="dd75d-216">Conecte-se o banco de dados toohello com o SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd75d-216">Connect toohello database with SQL Server Management Studio [(SSMS.exe)](http://msdn.microsoft.com/library/mt238290.aspx).</span></span>

3. <span data-ttu-id="dd75d-217">Saudação de cópia [script In-Memory OLTP Transact-SQL](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour área de transferência.</span><span class="sxs-lookup"><span data-stu-id="dd75d-217">Copy hello [In-Memory OLTP Transact-SQL script](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_oltp_sample.sql) tooyour clipboard.</span></span> <span data-ttu-id="dd75d-218">Olá script T-SQL cria Olá objetos na memória necessária no banco de dados do hello AdventureWorksLT exemplo que você criou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="dd75d-218">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>

4. <span data-ttu-id="dd75d-219">Cole o script T-SQL de saudação no SSMS e, em seguida, execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-219">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="dd75d-220">Olá `MEMORY_OPTIMIZED = ON` instruções CREATE TABLE de cláusula são cruciais.</span><span class="sxs-lookup"><span data-stu-id="dd75d-220">hello `MEMORY_OPTIMIZED = ON` clause CREATE TABLE statements are crucial.</span></span> <span data-ttu-id="dd75d-221">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="dd75d-221">For example:</span></span>


```
CREATE TABLE [SalesLT].[SalesOrderHeader_inmem](
    [SalesOrderID] int IDENTITY NOT NULL PRIMARY KEY NONCLUSTERED ...,
    ...
) WITH (MEMORY_OPTIMIZED = ON);
```


#### <a name="error-40536"></a><span data-ttu-id="dd75d-222">Erro 40536</span><span class="sxs-lookup"><span data-stu-id="dd75d-222">Error 40536</span></span>


<span data-ttu-id="dd75d-223">Se você receber o erro 40536 quando você executar o script hello T-SQL, execute Olá tooverify de script T-SQL a seguir se na memória oferece suporte a banco de dados de saudação:</span><span class="sxs-lookup"><span data-stu-id="dd75d-223">If you get error 40536 when you run hello T-SQL script, run hello following T-SQL script tooverify whether hello database supports In-Memory:</span></span>


```
SELECT DatabasePropertyEx(DB_Name(), 'IsXTPSupported');
```


<span data-ttu-id="dd75d-224">Um resultado **0** significa que não há suporte para In-Memory e **1** significa que há suporte.</span><span class="sxs-lookup"><span data-stu-id="dd75d-224">A result of **0** means that In-Memory isn't supported, and **1** means that it is supported.</span></span> <span data-ttu-id="dd75d-225">problema de saudação toodiagnose, certifique-se de que esse banco de dados de saudação é a camada de serviço Premium Olá.</span><span class="sxs-lookup"><span data-stu-id="dd75d-225">toodiagnose hello problem, ensure that hello database is at hello Premium service tier.</span></span>


#### <a name="about-hello-created-memory-optimized-items"></a><span data-ttu-id="dd75d-226">Sobre Olá criado itens com otimização de memória</span><span class="sxs-lookup"><span data-stu-id="dd75d-226">About hello created memory-optimized items</span></span>

<span data-ttu-id="dd75d-227">**Tabelas**: exemplo hello contém Olá tabelas com otimização de memória a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd75d-227">**Tables**: hello sample contains hello following memory-optimized tables:</span></span>

- <span data-ttu-id="dd75d-228">SalesLT.Product_inmem</span><span class="sxs-lookup"><span data-stu-id="dd75d-228">SalesLT.Product_inmem</span></span>
- <span data-ttu-id="dd75d-229">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="dd75d-229">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="dd75d-230">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="dd75d-230">SalesLT.SalesOrderDetail_inmem</span></span>
- <span data-ttu-id="dd75d-231">Demo.DemoSalesOrderHeaderSeed</span><span class="sxs-lookup"><span data-stu-id="dd75d-231">Demo.DemoSalesOrderHeaderSeed</span></span>
- <span data-ttu-id="dd75d-232">Demo.DemoSalesOrderDetailSeed</span><span class="sxs-lookup"><span data-stu-id="dd75d-232">Demo.DemoSalesOrderDetailSeed</span></span>


<span data-ttu-id="dd75d-233">Você pode inspecionar as tabelas com otimização de memória por meio de saudação **Pesquisador de objetos** no SSMS.</span><span class="sxs-lookup"><span data-stu-id="dd75d-233">You can inspect memory-optimized tables through hello **Object Explorer** in SSMS.</span></span> <span data-ttu-id="dd75d-234">Clique com o botão direito do mouse em **Tabelas** > **Filtro** > **Configurações do Filtro** > **Com otimização de memória**.</span><span class="sxs-lookup"><span data-stu-id="dd75d-234">Right-click **Tables** > **Filter** > **Filter Settings** > **Is Memory Optimized**.</span></span> <span data-ttu-id="dd75d-235">valor de saudação é igual a 1.</span><span class="sxs-lookup"><span data-stu-id="dd75d-235">hello value equals 1.</span></span>


<span data-ttu-id="dd75d-236">Ou você pode consultar as exibições do catálogo hello, como:</span><span class="sxs-lookup"><span data-stu-id="dd75d-236">Or you can query hello catalog views, such as:</span></span>


```
SELECT is_memory_optimized, name, type_desc, durability_desc
    FROM sys.tables
    WHERE is_memory_optimized = 1;
```


<span data-ttu-id="dd75d-237">**Procedimento armazenado compilado nativamente**: você pode inspecionar SalesLT.usp_InsertSalesOrder_inmem por meio de uma consulta de exibição de catálogo:</span><span class="sxs-lookup"><span data-stu-id="dd75d-237">**Natively compiled stored procedure**: You can inspect SalesLT.usp_InsertSalesOrder_inmem through a catalog view query:</span></span>


```
SELECT uses_native_compilation, OBJECT_NAME(object_id), definition
    FROM sys.sql_modules
    WHERE uses_native_compilation = 1;
```


&nbsp;

### <a name="run-hello-sample-oltp-workload"></a><span data-ttu-id="dd75d-238">Executar a carga de trabalho OLTP de exemplo hello</span><span class="sxs-lookup"><span data-stu-id="dd75d-238">Run hello sample OLTP workload</span></span>

<span data-ttu-id="dd75d-239">Olá a única diferença entre Olá após dois *procedimentos armazenados* é que o primeiro procedimento de saudação usa versões com otimização de memória das tabelas de saudação, durante a saudação segundo procedimento usa tabelas em disco regulares de saudação:</span><span class="sxs-lookup"><span data-stu-id="dd75d-239">hello only difference between hello following two *stored procedures* is that hello first procedure uses memory-optimized versions of hello tables, while hello second procedure uses hello regular on-disk tables:</span></span>

- <span data-ttu-id="dd75d-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span><span class="sxs-lookup"><span data-stu-id="dd75d-240">SalesLT**.**usp_InsertSalesOrder**_inmem**</span></span>
- <span data-ttu-id="dd75d-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span><span class="sxs-lookup"><span data-stu-id="dd75d-241">SalesLT**.**usp_InsertSalesOrder**_ondisk**</span></span>


<span data-ttu-id="dd75d-242">Nesta seção, consulte como toouse Olá útil **ostress.exe** tooexecute utilitário Olá dois procedimentos armazenados nos níveis estressantes.</span><span class="sxs-lookup"><span data-stu-id="dd75d-242">In this section, you see how toouse hello handy **ostress.exe** utility tooexecute hello two stored procedures at stressful levels.</span></span> <span data-ttu-id="dd75d-243">Você pode comparar quanto tempo demora para Olá dois estresse executa toofinish.</span><span class="sxs-lookup"><span data-stu-id="dd75d-243">You can compare how long it takes for hello two stress runs toofinish.</span></span>


<span data-ttu-id="dd75d-244">Ao executar ostress.exe, recomendamos que você passa valores de parâmetro projetados para os seguintes hello:</span><span class="sxs-lookup"><span data-stu-id="dd75d-244">When you run ostress.exe, we recommend that you pass parameter values designed for both of hello following:</span></span>

- <span data-ttu-id="dd75d-245">Execute um grande número de conexões simultâneas usando -n100.</span><span class="sxs-lookup"><span data-stu-id="dd75d-245">Run a large number of concurrent connections, by using -n100.</span></span>
- <span data-ttu-id="dd75d-246">Faça com que cada conexão entre em loop centenas de vezes usando -r500.</span><span class="sxs-lookup"><span data-stu-id="dd75d-246">Have each connection loop hundreds of times, by using -r500.</span></span>


<span data-ttu-id="dd75d-247">No entanto, você talvez queira toostart com valores muito menores como - n10 e - r50 tooensure que tudo está funcionando.</span><span class="sxs-lookup"><span data-stu-id="dd75d-247">However, you might want toostart with much smaller values like -n10 and -r50 tooensure that everything is working.</span></span>


### <a name="script-for-ostressexe"></a><span data-ttu-id="dd75d-248">Script para ostress.exe</span><span class="sxs-lookup"><span data-stu-id="dd75d-248">Script for ostress.exe</span></span>


<span data-ttu-id="dd75d-249">Esta seção exibe o script T-SQL Olá incorporado em nossa linha de comando ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="dd75d-249">This section displays hello T-SQL script that is embedded in our ostress.exe command line.</span></span> <span data-ttu-id="dd75d-250">script Hello usa itens que foram criados pelo Olá script T-SQL que você instalou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="dd75d-250">hello script uses items that were created by hello T-SQL script that you installed earlier.</span></span>


<span data-ttu-id="dd75d-251">Olá script a seguir insere um pedido de vendas de exemplo com cinco itens de linha com otimização de memória a seguir Olá *tabelas*:</span><span class="sxs-lookup"><span data-stu-id="dd75d-251">hello following script inserts a sample sales order with five line items into hello following memory-optimized *tables*:</span></span>

- <span data-ttu-id="dd75d-252">SalesLT.SalesOrderHeader_inmem</span><span class="sxs-lookup"><span data-stu-id="dd75d-252">SalesLT.SalesOrderHeader_inmem</span></span>
- <span data-ttu-id="dd75d-253">SalesLT.SalesOrderDetail_inmem</span><span class="sxs-lookup"><span data-stu-id="dd75d-253">SalesLT.SalesOrderDetail_inmem</span></span>


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


<span data-ttu-id="dd75d-254">Olá toomake *ondisk* Olá a versão do script T-SQL anterior para ostress.exe, você substituiria as duas ocorrências de saudação *inmem* subcadeia de caracteres com *ondisk*.</span><span class="sxs-lookup"><span data-stu-id="dd75d-254">toomake hello *_ondisk* version of hello preceding T-SQL script for ostress.exe, you would replace both occurrences of hello *_inmem* substring with *_ondisk*.</span></span> <span data-ttu-id="dd75d-255">Essas substituições afetam os nomes de saudação de tabelas e procedimentos armazenados.</span><span class="sxs-lookup"><span data-stu-id="dd75d-255">These replacements affect hello names of tables and stored procedures.</span></span>


### <a name="install-rml-utilities-and-ostress"></a><span data-ttu-id="dd75d-256">Instalar utilitários RML e o ostress</span><span class="sxs-lookup"><span data-stu-id="dd75d-256">Install RML utilities and ostress</span></span>


<span data-ttu-id="dd75d-257">Idealmente, você deve planejar toorun ostress.exe em uma máquina virtual do Azure (VM).</span><span class="sxs-lookup"><span data-stu-id="dd75d-257">Ideally, you would plan toorun ostress.exe on an Azure virtual machine (VM).</span></span> <span data-ttu-id="dd75d-258">Você deve criar um [VM do Azure](https://azure.microsoft.com/documentation/services/virtual-machines/) em Olá mesma região geográfica do Azure onde seu banco de dados AdventureWorksLT reside.</span><span class="sxs-lookup"><span data-stu-id="dd75d-258">You would create an [Azure VM](https://azure.microsoft.com/documentation/services/virtual-machines/) in hello same Azure geographic region where your AdventureWorksLT database resides.</span></span> <span data-ttu-id="dd75d-259">Mas você pode executar o ostress.exe em seu laptop.</span><span class="sxs-lookup"><span data-stu-id="dd75d-259">But you can run ostress.exe on your laptop instead.</span></span>


<span data-ttu-id="dd75d-260">Olá VM, ou em qualquer host que você escolher, instalar utilitários de linguagem de marcação de reprodução (RML) hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-260">On hello VM, or on whatever host you choose, install hello Replay Markup Language (RML) utilities.</span></span> <span data-ttu-id="dd75d-261">utilitários de saudação incluem ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="dd75d-261">hello utilities include ostress.exe.</span></span>

<span data-ttu-id="dd75d-262">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="dd75d-262">For more information, see:</span></span>
- <span data-ttu-id="dd75d-263">Olá discussão ostress.exe [banco de dados de exemplo para OLTP na memória](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd75d-263">hello ostress.exe discussion in [Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="dd75d-264">[Banco de dados de exemplo para OLTP In-Memory](http://msdn.microsoft.com/library/mt465764.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd75d-264">[Sample Database for In-Memory OLTP](http://msdn.microsoft.com/library/mt465764.aspx).</span></span>
- <span data-ttu-id="dd75d-265">Olá [blog para a instalação ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd75d-265">hello [blog for installing ostress.exe](http://blogs.msdn.com/b/psssql/archive/2013/10/29/cumulative-update-2-to-the-rml-utilities-for-microsoft-sql-server-released.aspx).</span></span>



<!--
dn511655.aspx is for SQL 2014,
[Extensions tooAdventureWorks tooDemonstrate In-Memory OLTP]
(http://msdn.microsoft.com/library/dn511655&#x28;v=sql.120&#x29;.aspx)

whereas for SQL 2016+
[Sample Database for In-Memory OLTP]
(http://msdn.microsoft.com/library/mt465764.aspx)
-->



### <a name="run-hello-inmem-stress-workload-first"></a><span data-ttu-id="dd75d-266">Executar Olá *inmem* enfatizar a carga de trabalho pela primeira vez</span><span class="sxs-lookup"><span data-stu-id="dd75d-266">Run hello *_inmem* stress workload first</span></span>


<span data-ttu-id="dd75d-267">Você pode usar um *Cmd Prompt RML* janela toorun nossa linha de comando ostress.exe.</span><span class="sxs-lookup"><span data-stu-id="dd75d-267">You can use an *RML Cmd Prompt* window toorun our ostress.exe command line.</span></span> <span data-ttu-id="dd75d-268">parâmetros de linha de comando Olá direcionam ostress para:</span><span class="sxs-lookup"><span data-stu-id="dd75d-268">hello command-line parameters direct ostress to:</span></span>

- <span data-ttu-id="dd75d-269">Execute 100 conexões simultaneamente (-n100).</span><span class="sxs-lookup"><span data-stu-id="dd75d-269">Run 100 connections concurrently (-n100).</span></span>
- <span data-ttu-id="dd75d-270">Ter cada conexão que executar o script T-SQL de saudação 50 vezes (-r50).</span><span class="sxs-lookup"><span data-stu-id="dd75d-270">Have each connection run hello T-SQL script 50 times (-r50).</span></span>


```
ostress.exe -n100 -r50 -S<servername>.database.windows.net -U<login> -P<password> -d<database> -q -Q"DECLARE @i int = 0, @od SalesLT.SalesOrderDetailType_inmem, @SalesOrderID int, @DueDate datetime2 = sysdatetime(), @CustomerID int = rand() * 8000, @BillToAddressID int = rand() * 10000, @ShipToAddressID int = rand()* 10000; INSERT INTO @od SELECT OrderQty, ProductID FROM Demo.DemoSalesOrderDetailSeed WHERE OrderID= cast((rand()*60) as int); WHILE (@i < 20) begin; EXECUTE SalesLT.usp_InsertSalesOrder_inmem @SalesOrderID OUTPUT, @DueDate, @CustomerID, @BillToAddressID, @ShipToAddressID, @od; set @i += 1; end"
```


<span data-ttu-id="dd75d-271">Olá toorun anterior ostress.exe linha de comando:</span><span class="sxs-lookup"><span data-stu-id="dd75d-271">toorun hello preceding ostress.exe command line:</span></span>


1. <span data-ttu-id="dd75d-272">Redefina conteúdo de dados do banco de dados de saudação executando todos os dados de saudação que foi inseridos por todas as execuções anteriores Olá comando no SSMS, toodelete a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd75d-272">Reset hello database data content by running hello following command in SSMS, toodelete all hello data that was inserted by any previous runs:</span></span>

    ``` tsql
    EXECUTE Demo.usp_DemoReset;
    ```

2. <span data-ttu-id="dd75d-273">Copie o texto de saudação de saudação anterior ostress.exe linha de comando tooyour área de transferência.</span><span class="sxs-lookup"><span data-stu-id="dd75d-273">Copy hello text of hello preceding ostress.exe command line tooyour clipboard.</span></span>

3. <span data-ttu-id="dd75d-274">Substituir saudação `<placeholders>` para Olá parâmetros -S - U -P -d com hello corrigir os valores reais.</span><span class="sxs-lookup"><span data-stu-id="dd75d-274">Replace hello `<placeholders>` for hello parameters -S -U -P -d with hello correct real values.</span></span>

4. <span data-ttu-id="dd75d-275">Execute a linha de comando editada em uma janela Cmd RML.</span><span class="sxs-lookup"><span data-stu-id="dd75d-275">Run your edited command line in an RML Cmd window.</span></span>


#### <a name="result-is-a-duration"></a><span data-ttu-id="dd75d-276">O resultado é uma duração</span><span class="sxs-lookup"><span data-stu-id="dd75d-276">Result is a duration</span></span>


<span data-ttu-id="dd75d-277">Quando ostress.exe é concluído, ele grava Olá duração da execução como a linha final de saída na janela de Cmd RML hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-277">When ostress.exe finishes, it writes hello run duration as its final line of output in hello RML Cmd window.</span></span> <span data-ttu-id="dd75d-278">Por exemplo, uma execução de teste mais curta dura aproximadamente 1,5 minuto:</span><span class="sxs-lookup"><span data-stu-id="dd75d-278">For example, a shorter test run lasted about 1.5 minutes:</span></span>

`11/12/15 00:35:00.873 [0x000030A8] OSTRESS exiting normally, elapsed time: 00:01:31.867`


#### <a name="reset-edit-for-ondisk-then-rerun"></a><span data-ttu-id="dd75d-279">Redefinir, editar *_ondisk* e executar novamente</span><span class="sxs-lookup"><span data-stu-id="dd75d-279">Reset, edit for *_ondisk*, then rerun</span></span>


<span data-ttu-id="dd75d-280">Depois de ter resultado de saudação do hello *inmem* executar, execute Olá seguindo as etapas para Olá *ondisk* executar:</span><span class="sxs-lookup"><span data-stu-id="dd75d-280">After you have hello result from hello *_inmem* run, perform hello following steps for hello *_ondisk* run:</span></span>


1. <span data-ttu-id="dd75d-281">Redefina o banco de dados de Olá executando todos os dados de saudação que foi inseridos por Olá anterior executar Olá comando no SSMS toodelete a seguir:</span><span class="sxs-lookup"><span data-stu-id="dd75d-281">Reset hello database by running hello following command in SSMS toodelete all hello data that was inserted by hello previous run:</span></span>
```
EXECUTE Demo.usp_DemoReset;
```

2. <span data-ttu-id="dd75d-282">Editar saudação ostress.exe linha de comando tooreplace todos os *inmem* com *ondisk*.</span><span class="sxs-lookup"><span data-stu-id="dd75d-282">Edit hello ostress.exe command line tooreplace all *_inmem* with *_ondisk*.</span></span>

3. <span data-ttu-id="dd75d-283">Execute novamente o ostress.exe para Olá pela segunda vez e capturar resultados de duração de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd75d-283">Rerun ostress.exe for hello second time, and capture hello duration result.</span></span>

4. <span data-ttu-id="dd75d-284">Novamente, redefina Olá banco de dados (com responsabilidade excluindo o que pode ser uma grande quantidade de dados de teste).</span><span class="sxs-lookup"><span data-stu-id="dd75d-284">Again, reset hello database (for responsibly deleting what can be a large amount of test data).</span></span>


#### <a name="expected-comparison-results"></a><span data-ttu-id="dd75d-285">Resultados esperados para a comparação</span><span class="sxs-lookup"><span data-stu-id="dd75d-285">Expected comparison results</span></span>

<span data-ttu-id="dd75d-286">Nossos testes na memória mostraram que o desempenho aprimorado por **nove vezes** para essa carga de trabalho simples, com ostress em execução em uma VM do Azure no hello mesma região do Azure como banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="dd75d-286">Our In-Memory tests have shown that performance improved by **nine times** for this simplistic workload, with ostress running on an Azure VM in hello same Azure region as hello database.</span></span>

<a id="install_analytics_manuallink" name="install_analytics_manuallink"></a>

&nbsp;

## <a name="2-install-hello-in-memory-analytics-sample"></a><span data-ttu-id="dd75d-287">2. Instalar o exemplo de análise in-memory hello</span><span class="sxs-lookup"><span data-stu-id="dd75d-287">2. Install hello In-Memory Analytics sample</span></span>


<span data-ttu-id="dd75d-288">Nesta seção, você comparar hello e/s e resultados de estatísticas quando você estiver usando um índice columnstore em vez de um índice de árvore b tradicional.</span><span class="sxs-lookup"><span data-stu-id="dd75d-288">In this section, you compare hello IO and statistics results when you're using a columnstore index versus a traditional b-tree index.</span></span>


<span data-ttu-id="dd75d-289">Para análise em tempo real em uma carga de trabalho OLTP, geralmente é melhor toouse um índice columnstore não clusterizado.</span><span class="sxs-lookup"><span data-stu-id="dd75d-289">For real-time analytics on an OLTP workload, it's often best toouse a nonclustered columnstore index.</span></span> <span data-ttu-id="dd75d-290">Para ver mais detalhes, confira [Índices Columnstore Descritos](http://msdn.microsoft.com/library/gg492088.aspx).</span><span class="sxs-lookup"><span data-stu-id="dd75d-290">For details, see [Columnstore Indexes Described](http://msdn.microsoft.com/library/gg492088.aspx).</span></span>



### <a name="prepare-hello-columnstore-analytics-test"></a><span data-ttu-id="dd75d-291">Preparar o teste de análise de columnstore Olá</span><span class="sxs-lookup"><span data-stu-id="dd75d-291">Prepare hello columnstore analytics test</span></span>


1. <span data-ttu-id="dd75d-292">Use Olá toocreate portal do Azure um banco de dados novo AdventureWorksLT do exemplo hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-292">Use hello Azure portal toocreate a fresh AdventureWorksLT database from hello sample.</span></span>
 - <span data-ttu-id="dd75d-293">Use esse nome exato.</span><span class="sxs-lookup"><span data-stu-id="dd75d-293">Use that exact name.</span></span>
 - <span data-ttu-id="dd75d-294">Escolha qualquer camada de serviço Premium.</span><span class="sxs-lookup"><span data-stu-id="dd75d-294">Choose any Premium service tier.</span></span>

2. <span data-ttu-id="dd75d-295">Saudação de cópia [sql_in memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour área de transferência.</span><span class="sxs-lookup"><span data-stu-id="dd75d-295">Copy hello [sql_in-memory_analytics_sample](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/sql_in-memory_analytics_sample.sql) tooyour clipboard.</span></span>
 - <span data-ttu-id="dd75d-296">Olá script T-SQL cria Olá objetos na memória necessária no banco de dados do hello AdventureWorksLT exemplo que você criou na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="dd75d-296">hello T-SQL script creates hello necessary In-Memory objects in hello AdventureWorksLT sample database that you created in step 1.</span></span>
 - <span data-ttu-id="dd75d-297">script Hello cria a tabela de dimensões hello e duas tabelas de fatos.</span><span class="sxs-lookup"><span data-stu-id="dd75d-297">hello script creates hello Dimension table and two fact tables.</span></span> <span data-ttu-id="dd75d-298">tabelas de fatos Olá são preenchidas com 3.5 milhões de linhas cada.</span><span class="sxs-lookup"><span data-stu-id="dd75d-298">hello fact tables are populated with 3.5 million rows each.</span></span>
 - <span data-ttu-id="dd75d-299">script Hello pode levar 15 minutos toocomplete.</span><span class="sxs-lookup"><span data-stu-id="dd75d-299">hello script might take 15 minutes toocomplete.</span></span>

3. <span data-ttu-id="dd75d-300">Cole o script T-SQL de saudação no SSMS e, em seguida, execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-300">Paste hello T-SQL script into SSMS, and then execute hello script.</span></span> <span data-ttu-id="dd75d-301">Olá **COLUMNSTORE** palavra-chave em Olá **CREATE INDEX** instrução é fundamental, como:</span><span class="sxs-lookup"><span data-stu-id="dd75d-301">hello **COLUMNSTORE** keyword in hello **CREATE INDEX** statement is crucial, as in:</span></span><br/>`CREATE NONCLUSTERED COLUMNSTORE INDEX ...;`

4. <span data-ttu-id="dd75d-302">Defina nível de toocompatibility AdventureWorksLT 130:</span><span class="sxs-lookup"><span data-stu-id="dd75d-302">Set AdventureWorksLT toocompatibility level 130:</span></span><br/>`ALTER DATABASE AdventureworksLT SET compatibility_level = 130;`

    <span data-ttu-id="dd75d-303">Nível 130 não é recursos de memória de tooIn diretamente relacionados.</span><span class="sxs-lookup"><span data-stu-id="dd75d-303">Level 130 is not directly related tooIn-Memory features.</span></span> <span data-ttu-id="dd75d-304">Mas o nível 130 geralmente oferece desempenho de consulta mais rápido que o 120.</span><span class="sxs-lookup"><span data-stu-id="dd75d-304">But level 130 generally provides faster query performance than 120.</span></span>


#### <a name="key-tables-and-columnstore-indexes"></a><span data-ttu-id="dd75d-305">Tabelas chave e índices de columnstore</span><span class="sxs-lookup"><span data-stu-id="dd75d-305">Key tables and columnstore indexes</span></span>


- <span data-ttu-id="dd75d-306">dbo. FactResellerSalesXL_CCI é uma tabela que tem um índice columnstore clusterizado, avançou compactação no hello *dados* nível.</span><span class="sxs-lookup"><span data-stu-id="dd75d-306">dbo.FactResellerSalesXL_CCI is a table that has a clustered columnstore index, which has advanced compression at hello *data* level.</span></span>

- <span data-ttu-id="dd75d-307">dbo. FactResellerSalesXL_PageCompressed é uma tabela que tem um equivalente regular índice clusterizado, é compactado apenas no hello *página* nível.</span><span class="sxs-lookup"><span data-stu-id="dd75d-307">dbo.FactResellerSalesXL_PageCompressed is a table that has an equivalent regular clustered index, which is compressed only at hello *page* level.</span></span>


#### <a name="key-queries-toocompare-hello-columnstore-index"></a><span data-ttu-id="dd75d-308">Índice de columnstore consultas chave toocompare Olá</span><span class="sxs-lookup"><span data-stu-id="dd75d-308">Key queries toocompare hello columnstore index</span></span>


<span data-ttu-id="dd75d-309">Há [vários tipos de consultas T-SQL que você pode executar](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee melhorias de desempenho.</span><span class="sxs-lookup"><span data-stu-id="dd75d-309">There are [several T-SQL query types that you can run](https://raw.githubusercontent.com/Microsoft/sql-server-samples/master/samples/features/in-memory/t-sql-scripts/clustered_columnstore_sample_queries.sql) toosee performance improvements.</span></span> <span data-ttu-id="dd75d-310">Na etapa 2 Olá script T-SQL, paga par de toothis atenção de consultas.</span><span class="sxs-lookup"><span data-stu-id="dd75d-310">In step 2 in hello T-SQL script, pay attention toothis pair of queries.</span></span> <span data-ttu-id="dd75d-311">Elas diferem apenas em uma linha:</span><span class="sxs-lookup"><span data-stu-id="dd75d-311">They differ only on one line:</span></span>


- `FROM FactResellerSalesXL_PageCompressed a`
- `FROM FactResellerSalesXL_CCI a`


<span data-ttu-id="dd75d-312">Um índice columnstore clusterizado está em Olá FactResellerSalesXL\_tabela CCI.</span><span class="sxs-lookup"><span data-stu-id="dd75d-312">A clustered columnstore index is in hello FactResellerSalesXL\_CCI table.</span></span>

<span data-ttu-id="dd75d-313">Olá trecho de script T-SQL a seguir imprime estatísticas de e/s e o tempo de consulta de saudação de cada tabela.</span><span class="sxs-lookup"><span data-stu-id="dd75d-313">hello following T-SQL script excerpt prints statistics for IO and TIME for hello query of each table.</span></span>


```
/*********************************************************************
Step 2 -- Overview
-- Page Compressed BTree table v/s Columnstore table performance differences
-- Enable actual Query Plan in order toosee Plan differences when Executing
*/
-- Ensure Database is in 130 compatibility mode
ALTER DATABASE AdventureworksLT SET compatibility_level = 130
GO

-- Execute a typical query that joins hello Fact Table with dimension tables
-- Note this query will run on hello Page Compressed table, Note down hello time
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


-- This is hello same Prior query on a table with a clustered columnstore index CCI
-- hello comparison numbers are even more dramatic hello larger hello table is (this is an 11 million row table only)
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

<span data-ttu-id="dd75d-314">Em um banco de dados de preço P2 hello, você pode esperar aproximadamente nove vezes Olá ganho de desempenho para essa consulta usando um índice columnstore clusterizado Olá em comparação com um índice tradicional hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-314">In a database with hello P2 pricing tier, you can expect about nine times hello performance gain for this query by using hello clustered columnstore index compared with hello traditional index.</span></span> <span data-ttu-id="dd75d-315">Com P15, você pode esperar aproximadamente 57 vezes ganho de desempenho de saudação usando o índice de columnstore hello.</span><span class="sxs-lookup"><span data-stu-id="dd75d-315">With P15, you can expect about 57 times hello performance gain by using hello columnstore index.</span></span>



## <a name="next-steps"></a><span data-ttu-id="dd75d-316">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="dd75d-316">Next steps</span></span>

- [<span data-ttu-id="dd75d-317">Início Rápido 1: Tecnologias OLTP in-memory para um desempenho mais rápido do T-SQL</span><span class="sxs-lookup"><span data-stu-id="dd75d-317">Quick Start 1: In-Memory OLTP Technologies for Faster T-SQL Performance</span></span>](http://msdn.microsoft.com/library/mt694156.aspx)

- [<span data-ttu-id="dd75d-318">Usar o OLTP In-Memory em um aplicativo existente do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="dd75d-318">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

- <span data-ttu-id="dd75d-319">[Monitorar o armazenamento do OLTP In-Memory](sql-database-in-memory-oltp-monitoring.md) para o OLTP In-Memory</span><span class="sxs-lookup"><span data-stu-id="dd75d-319">[Monitor In-Memory OLTP storage](sql-database-in-memory-oltp-monitoring.md) for In-Memory OLTP</span></span>


## <a name="additional-resources"></a><span data-ttu-id="dd75d-320">Recursos adicionais</span><span class="sxs-lookup"><span data-stu-id="dd75d-320">Additional resources</span></span>

#### <a name="deeper-information"></a><span data-ttu-id="dd75d-321">Informações mais detalhadas</span><span class="sxs-lookup"><span data-stu-id="dd75d-321">Deeper information</span></span>

- [<span data-ttu-id="dd75d-322">Saiba como o Quorum dobra a principal carga de trabalho do banco de dados, enquanto reduz a DTU em 70% com o OLTP in-memory no Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="dd75d-322">Learn how Quorum doubles key database’s workload while lowering DTU by 70% with In-Memory OLTP in SQL Database</span></span>](https://customers.microsoft.com/story/quorum-doubles-key-databases-workload-while-lowering-dtu-with-sql-database)

- [<span data-ttu-id="dd75d-323">Postagem de Blog de OLTP na memória do Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="dd75d-323">In-Memory OLTP in Azure SQL Database Blog Post</span></span>](https://azure.microsoft.com/blog/in-memory-oltp-in-azure-sql-database/)

- [<span data-ttu-id="dd75d-324">Saiba mais sobre o OLTP in-memory</span><span class="sxs-lookup"><span data-stu-id="dd75d-324">Learn about In-Memory OLTP</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="dd75d-325">Saiba mais sobre os índices columnstore</span><span class="sxs-lookup"><span data-stu-id="dd75d-325">Learn about columnstore indexes</span></span>](https://msdn.microsoft.com/library/gg492088.aspx)

- [<span data-ttu-id="dd75d-326">Saiba mais sobre a análise operacional em tempo real</span><span class="sxs-lookup"><span data-stu-id="dd75d-326">Learn about real-time operational analytics</span></span>](http://msdn.microsoft.com/library/dn817827.aspx)

- <span data-ttu-id="dd75d-327">Veja [Padrões comuns de carga de trabalho e considerações sobre migração](http://msdn.microsoft.com/library/dn673538.aspx) (que descreve os padrões de carga de trabalho para os quais o OLTP In-Memory geralmente fornece ganhos significativos de desempenho)</span><span class="sxs-lookup"><span data-stu-id="dd75d-327">See [Common Workload Patterns and Migration Considerations](http://msdn.microsoft.com/library/dn673538.aspx) (which describes workload patterns where In-Memory OLTP commonly provides significant performance gains)</span></span>

#### <a name="application-design"></a><span data-ttu-id="dd75d-328">Design do aplicativo</span><span class="sxs-lookup"><span data-stu-id="dd75d-328">Application design</span></span>

- [<span data-ttu-id="dd75d-329">OLTP Na Memória (Otimização Na Memória)</span><span class="sxs-lookup"><span data-stu-id="dd75d-329">In-Memory OLTP (In-Memory Optimization)</span></span>](http://msdn.microsoft.com/library/dn133186.aspx)

- [<span data-ttu-id="dd75d-330">Usar o OLTP In-Memory em um aplicativo existente do SQL Azure</span><span class="sxs-lookup"><span data-stu-id="dd75d-330">Use In-Memory OLTP in an existing Azure SQL application</span></span>](sql-database-in-memory-oltp-migration.md)

#### <a name="tools"></a><span data-ttu-id="dd75d-331">Ferramentas</span><span class="sxs-lookup"><span data-stu-id="dd75d-331">Tools</span></span>

- [<span data-ttu-id="dd75d-332">Portal do Azure</span><span class="sxs-lookup"><span data-stu-id="dd75d-332">Azure portal</span></span>](https://portal.azure.com/)

- [<span data-ttu-id="dd75d-333">SQL Server Management Studio (SSMS)</span><span class="sxs-lookup"><span data-stu-id="dd75d-333">SQL Server Management Studio (SSMS)</span></span>](https://msdn.microsoft.com/library/mt238290.aspx)

- [<span data-ttu-id="dd75d-334">SSDT (Ferramentas de Dados do SQL Server)</span><span class="sxs-lookup"><span data-stu-id="dd75d-334">SQL Server Data Tools (SSDT)</span></span>](http://msdn.microsoft.com/library/mt204009.aspx)
