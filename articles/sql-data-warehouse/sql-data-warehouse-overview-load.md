---
title: Carregar dados no SQL Data Warehouse do Azure | Microsoft Docs
description: "Aprenda sobre os cenários comuns para carregamento de dados no SQL Data Warehouse. Essas opções incluem usar PolyBase, armazenamento de blobs do Azure, arquivos simples e envio de disco. Você também pode usar ferramentas de terceiros."
services: sql-data-warehouse
documentationcenter: NA
author: ckarst
manager: jhubbard
editor: 
ms.assetid: 2253bf46-cf72-4de7-85ce-f267494d55fa
ms.service: sql-data-warehouse
ms.devlang: NA
ms.topic: article
ms.tgt_pltfrm: NA
ms.workload: data-services
ms.custom: loading
ms.date: 10/31/2016
ms.author: cakarst;barbkess
ms.openlocfilehash: c4199a387f5cdbd477a5e348e48ba8e8b5900075
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="232a6-105">Carregar dados no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="232a6-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="232a6-106">Um resumo das opções de cenário e recomendações para carregar dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="232a6-106">A summary of the scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="232a6-107">A parte mais difícil do carregamento de dados geralmente é preparar os dados para a carga.</span><span class="sxs-lookup"><span data-stu-id="232a6-107">The hardest part of loading data is usually preparing the data for the load.</span></span> <span data-ttu-id="232a6-108">O Azure simplifica o carregamento usando o armazenamento de blobs de Azure como um armazenamento de dados comum para muitos dos serviços, e usando o Azure Data Factory para orquestrar a movimentação de dados e comunicação entre os serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="232a6-108">Azure simplifies loading by using Azure blob storage as a common data store for many of the services, and using Azure Data Factory to orchestrate communication and data movement between the Azure services.</span></span> <span data-ttu-id="232a6-109">Esses processos são integrados com a tecnologia PolyBase que usa MPP (Processamento Paralelo Maciço) para carregar dados em paralelo do armazenamento de blobs do Azure no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="232a6-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) to load data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="232a6-110">Para ver os tutoriais que carregam bancos de dados de exemplo, consulte [Carregar bancos de dados de exemplo][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="232a6-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="232a6-111">Carregar por meio do armazenamento de blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="232a6-111">Load from Azure blob storage</span></span>
<span data-ttu-id="232a6-112">A maneira mais rápida para importar dados para o SQL Data Warehouse é usar o PolyBase para carregar dados do armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="232a6-112">The fastest way to import data into SQL Data Warehouse is to use PolyBase to load data from Azure blob storage.</span></span> <span data-ttu-id="232a6-113">O PolyBase usa o design de MPP (Processamento Paralelo Maciço) do SQL Data Warehouse para carregar dados em paralelo do armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="232a6-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design to load data in parallel from Azure blob storage.</span></span> <span data-ttu-id="232a6-114">Para usar o PolyBase, você pode usar comandos T-SQL ou um pipeline da Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="232a6-114">To use PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="232a6-115">1. Usar PolyBase e T-SQL</span><span class="sxs-lookup"><span data-stu-id="232a6-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="232a6-116">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="232a6-116">Summary of loading process:</span></span>

1. <span data-ttu-id="232a6-117">Mover os dados para o armazenamento de blobs do Azure ou o Azure Data Lake Store e armazene-os em arquivos de texto.</span><span class="sxs-lookup"><span data-stu-id="232a6-117">Move your data to Azure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="232a6-118">Configurar objetos externos no SQL Data Warehouse para definir o local e o formato dos dados</span><span class="sxs-lookup"><span data-stu-id="232a6-118">Configure external objects in SQL Data Warehouse to define the location and format of the data</span></span>
3. <span data-ttu-id="232a6-119">Execute um comando T-SQL para carregar os dados em paralelo em uma nova tabela de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="232a6-119">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="232a6-120">Para obter um tutorial, confira [Carregar os dados do armazenamento de blobs do Azure para o SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="232a6-120">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="232a6-121">2. Usar o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="232a6-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="232a6-122">Para uma forma mais simples de usar o PolyBase, você pode criar um pipeline do Azure Data Factory que usa o PolyBase para carregar dados do armazenamento de blobs do Azure no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="232a6-122">For a simpler way to use PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase to load data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="232a6-123">Ele é rápido de configurar porque você não precisa definir os objetos de T-SQL.</span><span class="sxs-lookup"><span data-stu-id="232a6-123">This is fast to configure since you don't need to define the T-SQL objects.</span></span> <span data-ttu-id="232a6-124">Se você precisar consultar dados externos sem importá-los, use o T-SQL.</span><span class="sxs-lookup"><span data-stu-id="232a6-124">If you need to query the external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="232a6-125">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="232a6-125">Summary of loading process:</span></span>

1. <span data-ttu-id="232a6-126">Mova seus dados do armazenamento de blobs Azure e armazene-os em arquivos de texto.</span><span class="sxs-lookup"><span data-stu-id="232a6-126">Move your data to Azure blob storage and store it in text files.</span></span> <span data-ttu-id="232a6-127">O Azure Data Factory atualmente não dá suporte à conectividade ADLS com PolyBase).</span><span class="sxs-lookup"><span data-stu-id="232a6-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="232a6-128">Crie um pipeline do Azure Data Factory para ingestão dos dados.</span><span class="sxs-lookup"><span data-stu-id="232a6-128">Create an Azure Data Factory pipeline to ingest the data.</span></span> <span data-ttu-id="232a6-129">Use a opção PolyBase.</span><span class="sxs-lookup"><span data-stu-id="232a6-129">Use the PolyBase option.</span></span>
4. <span data-ttu-id="232a6-130">Agende e execute o pipeline.</span><span class="sxs-lookup"><span data-stu-id="232a6-130">Schedule and run the pipeline.</span></span>

<span data-ttu-id="232a6-131">Para ver um tutorial, confira [Carregar dados do armazenamento de blobs do Azure para o SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="232a6-131">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="232a6-132">Carregar do SQL Server</span><span class="sxs-lookup"><span data-stu-id="232a6-132">Load from SQL Server</span></span>
<span data-ttu-id="232a6-133">Para carregar os dados do SQL Server para o SQL Data Warehouse, você pode usar o SSIS (Integration Services), transferir arquivos simples ou enviar discos à Microsoft.</span><span class="sxs-lookup"><span data-stu-id="232a6-133">To load data from SQL Server to SQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks to Microsoft.</span></span> <span data-ttu-id="232a6-134">Continue lendo para obter um resumo dos diferentes processos e links de carregamento a tutoriais.</span><span class="sxs-lookup"><span data-stu-id="232a6-134">Read on to see a summary of the different loading processes and links to tutorials.</span></span>

<span data-ttu-id="232a6-135">Para planejar uma migração de dados completa do SQL Server para o SQL Data Warehouse, confira a [Visão geral da migração][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="232a6-135">To plan a full data migration from SQL Server to SQL Data Warehouse, see the [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="232a6-136">Usar o SSIS (Integration Services)</span><span class="sxs-lookup"><span data-stu-id="232a6-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="232a6-137">Se você já estiver usando pacotes do SSIS (Integration Services) para carregar no SQL Server, você poderá atualizar seus pacotes para usar o SQL Server como a origem e o SQL Data Warehouse como destino.</span><span class="sxs-lookup"><span data-stu-id="232a6-137">If you are already using Integration Services (SSIS) packages to load into SQL Server, you can update your packages to use SQL Server as the source and SQL Data Warehouse as the destination.</span></span> <span data-ttu-id="232a6-138">Isso é rápido e fácil e é uma boa opção se você não está tentando migrar seu processo de carregamento para usar dados já na nuvem.</span><span class="sxs-lookup"><span data-stu-id="232a6-138">This is quick and easy to do, and is a good choice if you are not trying to migrate your loading process to use data already in the cloud.</span></span> <span data-ttu-id="232a6-139">A desvantagem é que a carga será mais lenta do que usar o PolyBase porque esse SSIS não executa a carga em paralelo.</span><span class="sxs-lookup"><span data-stu-id="232a6-139">The tradeoff is the load will be slower than using PolyBase because this SSIS does not perform the load in parallel.</span></span>

<span data-ttu-id="232a6-140">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="232a6-140">Summary of loading process:</span></span>

1. <span data-ttu-id="232a6-141">Revise o pacote do Integration Services para apontar para a instância do SQL Server para a origem e o banco de dados do SQL Data Warehouse para o destino.</span><span class="sxs-lookup"><span data-stu-id="232a6-141">Revise your Integration Services package to point to the SQL Server instance for the source and the SQL Data Warehouse database for the destination.</span></span>
2. <span data-ttu-id="232a6-142">Migre seu esquema para o SQL Data Warehouse, se ainda não estiver no local.</span><span class="sxs-lookup"><span data-stu-id="232a6-142">Migrate your schema to SQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="232a6-143">Altere o mapeamento em seus pacotes para usar apenas os tipos de dados com suporte do SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="232a6-143">Change the mapping in your packages use only the data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="232a6-144">Agende e execute o pacote.</span><span class="sxs-lookup"><span data-stu-id="232a6-144">Schedule and run the package.</span></span>

<span data-ttu-id="232a6-145">Para ver um tutorial, confira [Carregar dados do SQL Server para o Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="232a6-145">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (SSIS)][Load data from SQL Server to Azure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="232a6-146">Usar o AZCopy (recomendado para < 10 TB de dados)</span><span class="sxs-lookup"><span data-stu-id="232a6-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="232a6-147">Se o tamanho dos dados é < 10 TB, você pode exportar os dados do SQL Server para arquivos simples, copiar os arquivos para o armazenamento de blobs do Azure e, em seguida, use o PolyBase para carregar os dados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="232a6-147">If your data size is < 10 TB, you can export the data from SQL Server to flat files, copy the files to Azure blob storage, and then use PolyBase to load the data into SQL Data Warehouse</span></span>

<span data-ttu-id="232a6-148">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="232a6-148">Summary of loading process:</span></span>

1. <span data-ttu-id="232a6-149">Use o utilitário de linha de comando bcp para exportar dados do SQL Server para arquivos simples.</span><span class="sxs-lookup"><span data-stu-id="232a6-149">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="232a6-150">Use o utilitário de linha de comando AZCopy para copiar dados de arquivos simples para o armazenamento de blobs do Azure.</span><span class="sxs-lookup"><span data-stu-id="232a6-150">Use the AZCopy command-line utility to copy data from flat files to Azure blob storage.</span></span>
3. <span data-ttu-id="232a6-151">Usar o PolyBase para carregar SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="232a6-151">Use PolyBase to load into SQL Data Warehouse.</span></span>

<span data-ttu-id="232a6-152">Para obter um tutorial, confira [Carregar os dados do armazenamento de blobs do Azure para o SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="232a6-152">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="232a6-153">Usar o bcp</span><span class="sxs-lookup"><span data-stu-id="232a6-153">Use bcp</span></span>
<span data-ttu-id="232a6-154">Se você tiver uma pequena quantidade de dados, você poderá usar o bcp para carregar diretamente no SQL Data Warehouse do Azure.</span><span class="sxs-lookup"><span data-stu-id="232a6-154">If you have a small amount of data you can use bcp to load directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="232a6-155">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="232a6-155">Summary of loading process:</span></span>

1. <span data-ttu-id="232a6-156">Use o utilitário de linha de comando bcp para exportar dados do SQL Server para arquivos simples.</span><span class="sxs-lookup"><span data-stu-id="232a6-156">Use the bcp command-line utility to export data from SQL Server to flat files.</span></span>
2. <span data-ttu-id="232a6-157">Use o bcp para carregar dados de arquivos simples diretamente para o SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="232a6-157">Use bcp to load data from flat files directly to SQL Data Warehouse.</span></span>

<span data-ttu-id="232a6-158">Para ver um tutorial, confira [Carregar dados do SQL Server para o Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="232a6-158">For a tutorial, see [Load data from SQL Server to Azure SQL Data Warehouse (bcp)][Load data from SQL Server to Azure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="232a6-159">Usar Importar/Exportar (recomendado para > 10 TB de dados)</span><span class="sxs-lookup"><span data-stu-id="232a6-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="232a6-160">Se o tamanho dos dados é > 10 TB e você deseja movê-lo para o Azure, recomendamos que você use o serviço de envio de disco [Importar/Exportar][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="232a6-160">If your data size is > 10 TB and you want to move it to Azure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="232a6-161">Resumo do processo de carregamento</span><span class="sxs-lookup"><span data-stu-id="232a6-161">Summary of loading process</span></span>

1. <span data-ttu-id="232a6-162">Use o utilitário de linha de comando bcp para exportar dados do SQL Server para arquivos simples em discos transferíveis.</span><span class="sxs-lookup"><span data-stu-id="232a6-162">Use the bcp command-line utility to export data from SQL Server to flat files on transferrable disks.</span></span>
2. <span data-ttu-id="232a6-163">Envie os discos para a Microsoft.</span><span class="sxs-lookup"><span data-stu-id="232a6-163">Ship the disks to Microsoft.</span></span>
3. <span data-ttu-id="232a6-164">A Microsoft carrega os dados no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="232a6-164">Microsoft loads the data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="232a6-165">Carregar do HDInsight</span><span class="sxs-lookup"><span data-stu-id="232a6-165">Load from HDInsight</span></span>
<span data-ttu-id="232a6-166">O SQL Data Warehouse dá suporte ao carregamento de dados do HDInsight via PolyBase.</span><span class="sxs-lookup"><span data-stu-id="232a6-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="232a6-167">O processo é igual ao carregamento de dados do Armazenamento de Blobs do Azure, usando o PolyBase para se conectar ao HDInsight para carregar dados.</span><span class="sxs-lookup"><span data-stu-id="232a6-167">The process is the same as loading data from Azure Blob Storage - using PolyBase to connect to HDInsight to load data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="232a6-168">1. Usar PolyBase e T-SQL</span><span class="sxs-lookup"><span data-stu-id="232a6-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="232a6-169">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="232a6-169">Summary of loading process:</span></span>

1. <span data-ttu-id="232a6-170">Transfira seus dados para o HDInsight e armazene-os em arquivos de texto, no formato ORC ou Parquet.</span><span class="sxs-lookup"><span data-stu-id="232a6-170">Move your data to HDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="232a6-171">Configurar objetos externos no SQL Data Warehouse para definir o local e o formato dos dados.</span><span class="sxs-lookup"><span data-stu-id="232a6-171">Configure external objects in SQL Data Warehouse to define the location and format of the data.</span></span>
3. <span data-ttu-id="232a6-172">Execute um comando T-SQL para carregar os dados em paralelo em uma nova tabela de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="232a6-172">Run a T-SQL command to load the data in parallel into a new database table.</span></span>

<span data-ttu-id="232a6-173">Para obter um tutorial, confira [Carregar os dados do armazenamento de blobs do Azure para o SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="232a6-173">For a tutorial, see [Load data from Azure blob storage to SQL Data Warehouse (PolyBase)][Load data from Azure blob storage to SQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="232a6-174">Recomendações</span><span class="sxs-lookup"><span data-stu-id="232a6-174">Recommendations</span></span>
<span data-ttu-id="232a6-175">Muitos de nossos parceiros têm soluções de carregamento.</span><span class="sxs-lookup"><span data-stu-id="232a6-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="232a6-176">Para saber mais, confira uma lista de nossos [parceiros de solução][solution partners].</span><span class="sxs-lookup"><span data-stu-id="232a6-176">To find out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="232a6-177">Se seus dados forem provenientes de uma fonte não relacional e você desejar carregá-los no SQL Data Warehouse, você precisará transformá-los em linhas e colunas antes de carregá-los.</span><span class="sxs-lookup"><span data-stu-id="232a6-177">If your data is coming from a non-relational source and you want to load it into SQL Data Warehouse you will need to transform it into rows and columns before you load it.</span></span> <span data-ttu-id="232a6-178">Os dados transformados não precisam ser armazenado em um banco de dados, eles podem ser armazenados em arquivos de texto.</span><span class="sxs-lookup"><span data-stu-id="232a6-178">The transformed data doesn't need to be stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="232a6-179">Crie estatísticas sobre os dados recém-carregados.</span><span class="sxs-lookup"><span data-stu-id="232a6-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="232a6-180">O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.</span><span class="sxs-lookup"><span data-stu-id="232a6-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="232a6-181">Para obter o melhor desempenho de suas consultas, é importante que as estatísticas sejam criadas em todas as colunas de todas as tabelas após o primeiro carregamento ou após uma alteração significativa nos dados.</span><span class="sxs-lookup"><span data-stu-id="232a6-181">In order to get the best performance from your queries, it's important to create statistics on all columns of all tables after the first load or any substantial changes occur in the data.</span></span>  <span data-ttu-id="232a6-182">Para obter detalhes, confira [Estatísticas][Statistics].</span><span class="sxs-lookup"><span data-stu-id="232a6-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="232a6-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="232a6-183">Next steps</span></span>
<span data-ttu-id="232a6-184">Para obter mais dicas de desenvolvimento, confira a [visão geral sobre desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="232a6-184">For more development tips, see the [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage to SQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage to SQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server to Azure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server to Azure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server to Azure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
