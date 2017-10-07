---
title: dados de aaaLoad no Azure SQL Data Warehouse | Microsoft Docs
description: "Saiba mais cenários comuns de saudação para carregamento no SQL Data Warehouse de dados. Essas opções incluem usar PolyBase, armazenamento de blobs do Azure, arquivos simples e envio de disco. Você também pode usar ferramentas de terceiros."
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
ms.openlocfilehash: d1a5063f484e9bd95f854e27a4baed512148aad0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="load-data-into-azure-sql-data-warehouse"></a><span data-ttu-id="00036-105">Carregar dados no SQL Data Warehouse do Azure</span><span class="sxs-lookup"><span data-stu-id="00036-105">Load data into Azure SQL Data Warehouse</span></span>
<span data-ttu-id="00036-106">Um resumo das opções de cenário hello e recomendações para carregar dados no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="00036-106">A summary of hello scenario options and recommendations for loading data into SQL Data Warehouse.</span></span>

<span data-ttu-id="00036-107">Olá mais difícil de carregamento de dados geralmente está preparando dados saudação para carga de saudação.</span><span class="sxs-lookup"><span data-stu-id="00036-107">hello hardest part of loading data is usually preparing hello data for hello load.</span></span> <span data-ttu-id="00036-108">Carregamento simplifica o Azure usando o armazenamento de BLOBs do Azure como um repositório de dados comum para muitos serviços Olá e usando o Azure Data Factory tooorchestrate a movimentação de dados e comunicação entre Olá serviços do Azure.</span><span class="sxs-lookup"><span data-stu-id="00036-108">Azure simplifies loading by using Azure blob storage as a common data store for many of hello services, and using Azure Data Factory tooorchestrate communication and data movement between hello Azure services.</span></span> <span data-ttu-id="00036-109">Esses processos são integrados com a tecnologia PolyBase que usa processamento altamente paralelo dados de tooload (MPP) em paralelo do armazenamento de BLOBs do Azure no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="00036-109">These processes are integrated with PolyBase technology which uses massively parallel processing (MPP) tooload data in parallel from Azure blob storage into SQL Data Warehouse.</span></span> 

<span data-ttu-id="00036-110">Para ver os tutoriais que carregam bancos de dados de exemplo, consulte [Carregar bancos de dados de exemplo][Load sample databases].</span><span class="sxs-lookup"><span data-stu-id="00036-110">For tutorials that load sample databases, see [Load sample databases][Load sample databases].</span></span>

## <a name="load-from-azure-blob-storage"></a><span data-ttu-id="00036-111">Carregar por meio do armazenamento de blobs do Azure</span><span class="sxs-lookup"><span data-stu-id="00036-111">Load from Azure blob storage</span></span>
<span data-ttu-id="00036-112">tooimport dados de maneira mais rápidos de saudação no SQL Data Warehouse são toouse dados tooload do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="00036-112">hello fastest way tooimport data into SQL Data Warehouse is toouse PolyBase tooload data from Azure blob storage.</span></span> <span data-ttu-id="00036-113">PolyBase usa SQL Data Warehouse processamento altamente paralelo dados de tooload de design (MPP) em paralelo do armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="00036-113">PolyBase uses SQL Data Warehouse's massively parallel processing (MPP) design tooload data in parallel from Azure blob storage.</span></span> <span data-ttu-id="00036-114">toouse PolyBase, você pode usar os comandos T-SQL ou um pipeline da fábrica de dados do Azure.</span><span class="sxs-lookup"><span data-stu-id="00036-114">toouse PolyBase, you can use T-SQL commands or an Azure Data Factory pipeline.</span></span>

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="00036-115">1. Usar PolyBase e T-SQL</span><span class="sxs-lookup"><span data-stu-id="00036-115">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="00036-116">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="00036-116">Summary of loading process:</span></span>

1. <span data-ttu-id="00036-117">Mover o armazenamento de blob de tooAzure de dados ou o repositório Azure Data Lake e armazená-lo em arquivos de texto.</span><span class="sxs-lookup"><span data-stu-id="00036-117">Move your data tooAzure blob storage or Azure Data Lake Store and store it in text files.</span></span>
2. <span data-ttu-id="00036-118">Configurar objetos externos no local do SQL Data Warehouse toodefine hello e formato de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="00036-118">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data</span></span>
3. <span data-ttu-id="00036-119">Execute um T-SQL comando tooload Olá de dados em paralelo em uma nova tabela de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="00036-119">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<!-- 5. Schedule and run a loading job. --> 

<span data-ttu-id="00036-120">Para obter um tutorial, consulte [carregar dados de armazenamento de BLOBs do Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="00036-120">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="2-use-azure-data-factory"></a><span data-ttu-id="00036-121">2. Usar o Azure Data Factory</span><span class="sxs-lookup"><span data-stu-id="00036-121">2. Use Azure Data Factory</span></span>
<span data-ttu-id="00036-122">Para um toouse de maneira mais simples do PolyBase, você pode criar um pipeline da fábrica de dados do Azure que usa dados tooload do armazenamento de BLOBs do Azure no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="00036-122">For a simpler way toouse PolyBase, you can create an Azure Data Factory pipeline that uses PolyBase tooload data from Azure blob storage into SQL Data Warehouse.</span></span> <span data-ttu-id="00036-123">Isso é rápido tooconfigure como objetos de T-SQL Olá toodefine não é necessário.</span><span class="sxs-lookup"><span data-stu-id="00036-123">This is fast tooconfigure since you don't need toodefine hello T-SQL objects.</span></span> <span data-ttu-id="00036-124">Se você precisar de dados externos de saudação tooquery sem importá-lo, use T-SQL.</span><span class="sxs-lookup"><span data-stu-id="00036-124">If you need tooquery hello external data without importing it, use T-SQL.</span></span> 

<span data-ttu-id="00036-125">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="00036-125">Summary of loading process:</span></span>

1. <span data-ttu-id="00036-126">Mover o armazenamento de blob de tooAzure de dados e armazená-lo em arquivos de texto.</span><span class="sxs-lookup"><span data-stu-id="00036-126">Move your data tooAzure blob storage and store it in text files.</span></span> <span data-ttu-id="00036-127">O Azure Data Factory atualmente não dá suporte à conectividade ADLS com PolyBase).</span><span class="sxs-lookup"><span data-stu-id="00036-127">Azure Data Factory does not currently support ADLS connectivity with PolyBase).</span></span>
2. <span data-ttu-id="00036-128">Crie um pipeline do Azure Data Factory tooingest Olá dados.</span><span class="sxs-lookup"><span data-stu-id="00036-128">Create an Azure Data Factory pipeline tooingest hello data.</span></span> <span data-ttu-id="00036-129">Use a opção de PolyBase de saudação.</span><span class="sxs-lookup"><span data-stu-id="00036-129">Use hello PolyBase option.</span></span>
4. <span data-ttu-id="00036-130">Agendar e executar o pipeline de saudação.</span><span class="sxs-lookup"><span data-stu-id="00036-130">Schedule and run hello pipeline.</span></span>

<span data-ttu-id="00036-131">Para obter um tutorial, consulte [carregar dados de armazenamento de BLOBs do Azure tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span><span class="sxs-lookup"><span data-stu-id="00036-131">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)][Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)].</span></span>

## <a name="load-from-sql-server"></a><span data-ttu-id="00036-132">Carregar do SQL Server</span><span class="sxs-lookup"><span data-stu-id="00036-132">Load from SQL Server</span></span>
<span data-ttu-id="00036-133">dados de tooload de tooSQL do SQL Server Data Warehouse, você pode usar o Integration Services (SSIS), transferência de arquivos simples ou enviar tooMicrosoft de discos.</span><span class="sxs-lookup"><span data-stu-id="00036-133">tooload data from SQL Server tooSQL Data Warehouse you can use Integration Services (SSIS), transfer flat files, or ship disks tooMicrosoft.</span></span> <span data-ttu-id="00036-134">Ler em toosee um resumo da saudação diferente carregar tootutorials processos e links.</span><span class="sxs-lookup"><span data-stu-id="00036-134">Read on toosee a summary of hello different loading processes and links tootutorials.</span></span>

<span data-ttu-id="00036-135">tooplan uma migração de dados completo do SQL Server tooSQL Data Warehouse, consulte Olá [visão geral da migração][Migration overview].</span><span class="sxs-lookup"><span data-stu-id="00036-135">tooplan a full data migration from SQL Server tooSQL Data Warehouse, see hello [Migration overview][Migration overview].</span></span> 

### <a name="use-integration-services-ssis"></a><span data-ttu-id="00036-136">Usar o SSIS (Integration Services)</span><span class="sxs-lookup"><span data-stu-id="00036-136">Use Integration Services (SSIS)</span></span>
<span data-ttu-id="00036-137">Se você já estiver usando tooload de pacotes do Integration Services (SSIS) no SQL Server, você pode atualizar seu toouse de pacotes do SQL Server como origem hello e SQL Data Warehouse como destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="00036-137">If you are already using Integration Services (SSIS) packages tooload into SQL Server, you can update your packages toouse SQL Server as hello source and SQL Data Warehouse as hello destination.</span></span> <span data-ttu-id="00036-138">Isso é rápido e fácil toodo, e é uma boa opção se estiver tentando toomigrate não o carregamento de dados toouse já na nuvem de saudação do processo.</span><span class="sxs-lookup"><span data-stu-id="00036-138">This is quick and easy toodo, and is a good choice if you are not trying toomigrate your loading process toouse data already in hello cloud.</span></span> <span data-ttu-id="00036-139">compensação de saudação é carga Olá será mais lenta do que o PolyBase porque esse SSIS não executa Olá carga em paralelo.</span><span class="sxs-lookup"><span data-stu-id="00036-139">hello tradeoff is hello load will be slower than using PolyBase because this SSIS does not perform hello load in parallel.</span></span>

<span data-ttu-id="00036-140">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="00036-140">Summary of loading process:</span></span>

1. <span data-ttu-id="00036-141">Revise sua instância de SQL Server Integration Services pacote toopoint toohello para fonte hello e Olá o banco de dados de SQL Data Warehouse para o destino de saudação.</span><span class="sxs-lookup"><span data-stu-id="00036-141">Revise your Integration Services package toopoint toohello SQL Server instance for hello source and hello SQL Data Warehouse database for hello destination.</span></span>
2. <span data-ttu-id="00036-142">Migre seu tooSQL de esquema do Data Warehouse, se ainda não estiver lá.</span><span class="sxs-lookup"><span data-stu-id="00036-142">Migrate your schema tooSQL Data Warehouse, if it is not there already.</span></span>
3. <span data-ttu-id="00036-143">Mapeamento de saudação de alteração em seus pacotes use somente tipos de dados Olá que são suportados pelo SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="00036-143">Change hello mapping in your packages use only hello data types that are supported by SQL Data Warehouse.</span></span>
4. <span data-ttu-id="00036-144">Agendar e executar o pacote de saudação.</span><span class="sxs-lookup"><span data-stu-id="00036-144">Schedule and run hello package.</span></span>

<span data-ttu-id="00036-145">Para obter um tutorial, consulte [carregar dados do SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span><span class="sxs-lookup"><span data-stu-id="00036-145">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)][Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)].</span></span>

### <a name="use-azcopy-recommended-for--10-tb-data"></a><span data-ttu-id="00036-146">Usar o AZCopy (recomendado para < 10 TB de dados)</span><span class="sxs-lookup"><span data-stu-id="00036-146">Use AZCopy (recommended for < 10 TB data)</span></span>
<span data-ttu-id="00036-147">Se o tamanho de dados é < 10 TB, você pode exportar dados de saudação do arquivos de tooflat do SQL Server, copie o armazenamento de blob Olá arquivos tooAzure e, em seguida, usar dados tooload Olá no SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="00036-147">If your data size is < 10 TB, you can export hello data from SQL Server tooflat files, copy hello files tooAzure blob storage, and then use PolyBase tooload hello data into SQL Data Warehouse</span></span>

<span data-ttu-id="00036-148">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="00036-148">Summary of loading process:</span></span>

1. <span data-ttu-id="00036-149">Use dados de tooexport de utilitário de linha de comando do hello bcp de arquivos de tooflat do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="00036-149">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="00036-150">Use Olá AZCopy utilitário de linha de comando toocopy dados do armazenamento de blob de tooAzure de arquivos simples.</span><span class="sxs-lookup"><span data-stu-id="00036-150">Use hello AZCopy command-line utility toocopy data from flat files tooAzure blob storage.</span></span>
3. <span data-ttu-id="00036-151">Use tooload PolyBase no SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="00036-151">Use PolyBase tooload into SQL Data Warehouse.</span></span>

<span data-ttu-id="00036-152">Para obter um tutorial, consulte [carregar dados de armazenamento de BLOBs do Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="00036-152">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

### <a name="use-bcp"></a><span data-ttu-id="00036-153">Usar o bcp</span><span class="sxs-lookup"><span data-stu-id="00036-153">Use bcp</span></span>
<span data-ttu-id="00036-154">Se você tiver uma pequena quantidade de dados, você pode usar bcp tooload diretamente no Azure SQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="00036-154">If you have a small amount of data you can use bcp tooload directly into Azure SQL Data Warehouse.</span></span>

<span data-ttu-id="00036-155">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="00036-155">Summary of loading process:</span></span>

1. <span data-ttu-id="00036-156">Use dados de tooexport de utilitário de linha de comando do hello bcp de arquivos de tooflat do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="00036-156">Use hello bcp command-line utility tooexport data from SQL Server tooflat files.</span></span>
2. <span data-ttu-id="00036-157">Usar bcp tooload dados de simples diretamente arquivos tooSQL Data Warehouse.</span><span class="sxs-lookup"><span data-stu-id="00036-157">Use bcp tooload data from flat files directly tooSQL Data Warehouse.</span></span>

<span data-ttu-id="00036-158">Para obter um tutorial, consulte [carregar dados do SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span><span class="sxs-lookup"><span data-stu-id="00036-158">For a tutorial, see [Load data from SQL Server tooAzure SQL Data Warehouse (bcp)][Load data from SQL Server tooAzure SQL Data Warehouse (bcp)].</span></span>

### <a name="use-importexport-recommended-for--10-tb-data"></a><span data-ttu-id="00036-159">Usar Importar/Exportar (recomendado para > 10 TB de dados)</span><span class="sxs-lookup"><span data-stu-id="00036-159">Use Import/Export (recommended for > 10 TB data)</span></span>
<span data-ttu-id="00036-160">Se o tamanho dos dados é > 10 TB e você desejar toomove-tooAzure, recomendamos que você use nosso serviço de envio de disco [importação/exportação][Import/Export].</span><span class="sxs-lookup"><span data-stu-id="00036-160">If your data size is > 10 TB and you want toomove it tooAzure, we recommend that you use our disk shipping service [Import/Export][Import/Export].</span></span> 

<span data-ttu-id="00036-161">Resumo do processo de carregamento</span><span class="sxs-lookup"><span data-stu-id="00036-161">Summary of loading process</span></span>

1. <span data-ttu-id="00036-162">Use dados de tooexport de utilitário de linha de comando do hello bcp de arquivos do SQL Server tooflat em discos transferível.</span><span class="sxs-lookup"><span data-stu-id="00036-162">Use hello bcp command-line utility tooexport data from SQL Server tooflat files on transferrable disks.</span></span>
2. <span data-ttu-id="00036-163">Remeter saudação discos tooMicrosoft.</span><span class="sxs-lookup"><span data-stu-id="00036-163">Ship hello disks tooMicrosoft.</span></span>
3. <span data-ttu-id="00036-164">Microsoft carrega dados saudação em SQL Data Warehouse</span><span class="sxs-lookup"><span data-stu-id="00036-164">Microsoft loads hello data into SQL Data Warehouse</span></span>

## <a name="load-from-hdinsight"></a><span data-ttu-id="00036-165">Carregar do HDInsight</span><span class="sxs-lookup"><span data-stu-id="00036-165">Load from HDInsight</span></span>
<span data-ttu-id="00036-166">O SQL Data Warehouse dá suporte ao carregamento de dados do HDInsight via PolyBase.</span><span class="sxs-lookup"><span data-stu-id="00036-166">SQL Data Warehouse supports loading data from HDInsight via PolyBase.</span></span> <span data-ttu-id="00036-167">processo de saudação é Olá mesmo que o carregamento de dados de armazenamento de BLOBs do Azure - usando PolyBase tooconnect tooHDInsight tooload dados.</span><span class="sxs-lookup"><span data-stu-id="00036-167">hello process is hello same as loading data from Azure Blob Storage - using PolyBase tooconnect tooHDInsight tooload data.</span></span> 

### <a name="1-use-polybase-and-t-sql"></a><span data-ttu-id="00036-168">1. Usar PolyBase e T-SQL</span><span class="sxs-lookup"><span data-stu-id="00036-168">1. Use PolyBase and T-SQL</span></span>
<span data-ttu-id="00036-169">Resumo do processo de carregamento:</span><span class="sxs-lookup"><span data-stu-id="00036-169">Summary of loading process:</span></span>

1. <span data-ttu-id="00036-170">Mover tooHDInsight seus dados e armazená-lo em arquivos de texto, formato ORC ou Parquet.</span><span class="sxs-lookup"><span data-stu-id="00036-170">Move your data tooHDInsight and store it in text files, ORC or Parquet format.</span></span>
2. <span data-ttu-id="00036-171">Configure objetos externos no local do SQL Data Warehouse toodefine hello e formato de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="00036-171">Configure external objects in SQL Data Warehouse toodefine hello location and format of hello data.</span></span>
3. <span data-ttu-id="00036-172">Execute um T-SQL comando tooload Olá de dados em paralelo em uma nova tabela de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="00036-172">Run a T-SQL command tooload hello data in parallel into a new database table.</span></span>

<span data-ttu-id="00036-173">Para obter um tutorial, consulte [carregar dados de armazenamento de BLOBs do Azure tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span><span class="sxs-lookup"><span data-stu-id="00036-173">For a tutorial, see [Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)][Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)].</span></span>

## <a name="recommendations"></a><span data-ttu-id="00036-174">Recomendações</span><span class="sxs-lookup"><span data-stu-id="00036-174">Recommendations</span></span>
<span data-ttu-id="00036-175">Muitos de nossos parceiros têm soluções de carregamento.</span><span class="sxs-lookup"><span data-stu-id="00036-175">Many of our partners have loading solutions.</span></span> <span data-ttu-id="00036-176">toofind mais informações, consulte uma lista de nosso [parceiros de soluções][solution partners].</span><span class="sxs-lookup"><span data-stu-id="00036-176">toofind out more, see a list of our [solution partners][solution partners].</span></span> 

<span data-ttu-id="00036-177">Se seus dados é proveniente de uma fonte não relacionais e você desejar tooload no SQL Data Warehouse você precisará tootransform-lo em linhas e colunas antes de carregá-lo.</span><span class="sxs-lookup"><span data-stu-id="00036-177">If your data is coming from a non-relational source and you want tooload it into SQL Data Warehouse you will need tootransform it into rows and columns before you load it.</span></span> <span data-ttu-id="00036-178">dados transformado de saudação não precisam toobe armazenado em um banco de dados, ele pode ser armazenado em arquivos de texto.</span><span class="sxs-lookup"><span data-stu-id="00036-178">hello transformed data doesn't need toobe stored in a database, it can be stored in text files.</span></span>

<span data-ttu-id="00036-179">Crie estatísticas sobre os dados recém-carregados.</span><span class="sxs-lookup"><span data-stu-id="00036-179">Create statistics on newly loaded data.</span></span> <span data-ttu-id="00036-180">O SQL Data Warehouse do Azure ainda não dá suporte a estatísticas de criação ou atualização automática.</span><span class="sxs-lookup"><span data-stu-id="00036-180">Azure SQL Data Warehouse does not yet support auto create or auto update statistics.</span></span>  <span data-ttu-id="00036-181">Em ordem tooget Olá melhor desempenho de suas consultas, é importante primeiro carregar toocreate estatísticas em todas as colunas de todas as tabelas após hello ou alterações substanciais ocorrerem nos dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="00036-181">In order tooget hello best performance from your queries, it's important toocreate statistics on all columns of all tables after hello first load or any substantial changes occur in hello data.</span></span>  <span data-ttu-id="00036-182">Para obter detalhes, confira [Estatísticas][Statistics].</span><span class="sxs-lookup"><span data-stu-id="00036-182">For details, see [Statistics][Statistics].</span></span>

## <a name="next-steps"></a><span data-ttu-id="00036-183">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00036-183">Next steps</span></span>
<span data-ttu-id="00036-184">Para obter mais dicas de desenvolvimento, consulte Olá [visão geral do desenvolvimento][development overview].</span><span class="sxs-lookup"><span data-stu-id="00036-184">For more development tips, see hello [development overview][development overview].</span></span>

<!--Image references-->

<!--Article references-->
[Load data from Azure blob storage tooSQL Data Warehouse (PolyBase)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-polybase.md
[Load data from Azure blob storage tooSQL Data Warehouse (Azure Data Factory)]: ./sql-data-warehouse-load-from-azure-blob-storage-with-data-factory.md
[Load data from SQL Server tooAzure SQL Data Warehouse (SSIS)]: ./sql-data-warehouse-load-from-sql-server-with-integration-services.md
[Load data from SQL Server tooAzure SQL Data Warehouse (bcp)]: ./sql-data-warehouse-load-from-sql-server-with-bcp.md
[Load data from SQL Server tooAzure SQL Data Warehouse (AZCopy)]: ./sql-data-warehouse-load-from-sql-server-with-azcopy.md

[Load sample databases]: ./sql-data-warehouse-load-sample-databases.md
[Migration overview]: ./sql-data-warehouse-overview-migrate.md
[solution partners]: ./sql-data-warehouse-partner-business-intelligence.md
[development overview]: ./sql-data-warehouse-overview-develop.md
[Statistics]: ./sql-data-warehouse-tables-statistics.md

<!--MSDN references-->

<!--Other Web references-->
[Import/Export]: https://azure.microsoft.com/documentation/articles/storage-import-export-service/
