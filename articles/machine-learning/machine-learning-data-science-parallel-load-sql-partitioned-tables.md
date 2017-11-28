---
title: "aaaBuild e otimizar tabelas para importação paralela rápida de dados em um SQL Server em uma VM do Azure | Microsoft Docs"
description: "Importação de Dados em Massa Paralela Usando Tabelas de Partição do SQL"
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: ff90fdb0-5bc7-49e8-aee7-678b54f901c8
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/29/2017
ms.author: bradsev
ms.openlocfilehash: ab748c47348ec6ca3b98ba39e27181bba5d36fc0
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="011db-103">Importação de Dados em Massa Paralela Usando Tabelas de Partição do SQL</span><span class="sxs-lookup"><span data-stu-id="011db-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="011db-104">Este documento descreve como toobuild particionada tabelas para a importação em massa paralela rápido do banco de dados do SQL Server data tooa.</span><span class="sxs-lookup"><span data-stu-id="011db-104">This document describes how toobuild partitioned tables for fast parallel bulk importing of data tooa SQL Server database.</span></span> <span data-ttu-id="011db-105">Para grandes dados carregamento/transferência tooa banco de dados SQL, o importar dados toohello banco de dados SQL e as consultas subsequentes pode ser melhorado usando *tabelas particionadas e exibições*.</span><span class="sxs-lookup"><span data-stu-id="011db-105">For big data loading/transfer tooa SQL database, importing data toohello SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="011db-106">Criar um novo banco de dados e um conjunto de grupos de arquivos</span><span class="sxs-lookup"><span data-stu-id="011db-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="011db-107">[Crie um novo banco de dados](https://technet.microsoft.com/library/ms176061.aspx), se ainda não houver um.</span><span class="sxs-lookup"><span data-stu-id="011db-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="011db-108">Adicione grupos de arquivos toohello banco de dados que armazenará arquivos físicos Olá particionado. Isso pode ser feito com [criar banco de dados](https://technet.microsoft.com/library/ms176061.aspx) se novo ou [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) se o banco de dados de saudação já existe.</span><span class="sxs-lookup"><span data-stu-id="011db-108">Add database filegroups toohello database which will hold hello partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if hello database exists already.</span></span>
* <span data-ttu-id="011db-109">Adicione um ou mais arquivos de banco de dados tooeach de arquivos (conforme necessário).</span><span class="sxs-lookup"><span data-stu-id="011db-109">Add one or more files (as needed) tooeach database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="011db-110">Especifique o grupo de arquivos de destino de saudação que mantém os dados para esta partição e hello nomes do arquivo de banco de dados físico onde os dados do grupo de arquivos de saudação serão armazenados.</span><span class="sxs-lookup"><span data-stu-id="011db-110">Specify hello target filegroup which holds data for this partition and hello physical database file name(s) where hello filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="011db-111">Olá exemplo a seguir cria um novo banco de dados com três grupos de arquivos diferentes Olá primário e grupos de log, que contém um arquivo físico em cada um.</span><span class="sxs-lookup"><span data-stu-id="011db-111">hello following example creates a new database with three filegroups other than hello primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="011db-112">arquivos de banco de dados de saudação são criados na pasta de dados do SQL Server padrão hello, conforme configurado na instância do SQL Server hello.</span><span class="sxs-lookup"><span data-stu-id="011db-112">hello database files are created in hello default SQL Server Data folder, as configured in hello SQL Server instance.</span></span> <span data-ttu-id="011db-113">Para obter mais informações sobre os locais de arquivo padrão hello, consulte [locais de arquivo padrão e nomeadas instâncias do SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span><span class="sxs-lookup"><span data-stu-id="011db-113">For more information about hello default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

    DECLARE @data_path nvarchar(256);
    SET @data_path = (SELECT SUBSTRING(physical_name, 1, CHARINDEX(N'master.mdf', LOWER(physical_name)) - 1)
      FROM master.sys.master_files
      WHERE database_id = 1 AND file_id = 1);

    EXECUTE ('
        CREATE DATABASE <database_name>
         ON  PRIMARY 
        ( NAME = ''Primary'', FILENAME = ''' + @data_path + '<primary_file_name>.mdf'', SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_1] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_1>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_2] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name_2>.ndf'' , SIZE = 4096KB , FILEGROWTH = 1024KB ), 
         FILEGROUP [filegroup_3] 
        ( NAME = ''FileGroup1'', FILENAME = ''' + @data_path + '<file_name>.ndf'' , SIZE = 102400KB , FILEGROWTH = 10240KB ), 
         LOG ON 
        ( NAME = ''LogFileGroup'', FILENAME = ''' + @data_path + '<log_file_name>.ldf'' , SIZE = 1024KB , FILEGROWTH = 10%)
    ')

## <a name="create-a-partitioned-table"></a><span data-ttu-id="011db-114">Criar uma tabela particionada</span><span class="sxs-lookup"><span data-stu-id="011db-114">Create a partitioned table</span></span>
<span data-ttu-id="011db-115">Crie tabelas particionadas de acordo com o esquema de dados toohello, grupos de arquivos do banco de dados mapeado toohello criados na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="011db-115">Create partitioned table(s) according toohello data schema, mapped toohello database filegroups created in hello previous step.</span></span> <span data-ttu-id="011db-116">Quando os dados são importados em massa toohello particionada tabelas, registros serão distribuídos entre grupos de arquivos de saudação de acordo com o esquema de partição tooa, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="011db-116">When data is bulk imported toohello partitioned table(s), records will be distributed among hello filegroups according tooa partition scheme, as described below.</span></span>

<span data-ttu-id="011db-117">**toocreate uma tabela de partição, você precisa:**</span><span class="sxs-lookup"><span data-stu-id="011db-117">**toocreate a partition table, you need to:**</span></span>

* <span data-ttu-id="011db-118">[Criar uma função de partição](https://msdn.microsoft.com/library/ms187802.aspx) que define o intervalo de saudação de valores/limites toobe incluídos em cada tabela de partição individual, por exemplo, as partições de toolimit por mês (alguns\_datetime\_campo) no ano Olá 2013:</span><span class="sxs-lookup"><span data-stu-id="011db-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines hello range of values/boundaries toobe included in each individual partition table, e.g., toolimit partitions by month(some\_datetime\_field) in hello year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="011db-119">[Criar um esquema de partição](https://msdn.microsoft.com/library/ms179854.aspx) que mapeia cada intervalo de partição no hello partição função tooa grupo de arquivos físico, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="011db-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in hello partition function tooa physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="011db-120">intervalos de saudação tooverify em vigor em cada função toohello de acordo/esquema de partição, execute Olá consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="011db-120">tooverify hello ranges in effect in each partition according toohello function/scheme, run hello following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="011db-121">[Criar tabela particionada](https://msdn.microsoft.com/library/ms174979.aspx)(s) de acordo com o esquema de dados tooyour e especifique o campo de esquema e a restrição de partição Olá usado toopartition tabela de hello, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="011db-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according tooyour data schema, and specify hello partition scheme and constraint field used toopartition hello table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="011db-122">Para obter mais informações, consulte [Criar tabelas e índices particionados](https://msdn.microsoft.com/library/ms188730.aspx).</span><span class="sxs-lookup"><span data-stu-id="011db-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a><span data-ttu-id="011db-123">Saudação de importar em massa dados para cada tabela de partição individual</span><span class="sxs-lookup"><span data-stu-id="011db-123">Bulk import hello data for each individual partition table</span></span>
* <span data-ttu-id="011db-124">Você pode usar o BCP, BULK INSERT ou outros métodos como o [Assistente de Migração do SQL Server](http://sqlazuremw.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="011db-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="011db-125">exemplo Hello fornecido usa o método BCP de saudação.</span><span class="sxs-lookup"><span data-stu-id="011db-125">hello example provided uses hello BCP method.</span></span>
* <span data-ttu-id="011db-126">[Alterar banco de dados de saudação](https://msdn.microsoft.com/library/bb522682.aspx) sobrecarga de toominimize tooBULK_LOGGED esquema de log, por exemplo, de log de transações de toochange:</span><span class="sxs-lookup"><span data-stu-id="011db-126">[Alter hello database](https://msdn.microsoft.com/library/bb522682.aspx) toochange transaction logging scheme tooBULK_LOGGED toominimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="011db-127">dados tooexpedite carregar, inicie operações de importação em massa Olá em paralelo.</span><span class="sxs-lookup"><span data-stu-id="011db-127">tooexpedite data loading, launch hello bulk import operations in parallel.</span></span> <span data-ttu-id="011db-128">Para obter dicas sobre como acelerar a importação em massa de big data em bancos de dados do SQL Server, consulte [Carregar 1 TB em menos de 1 hora](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span><span class="sxs-lookup"><span data-stu-id="011db-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="011db-129">Olá seguinte script do PowerShell é um exemplo de carregamento usando o BCP de dados paralelos.</span><span class="sxs-lookup"><span data-stu-id="011db-129">hello following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # hello example assumes hello partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes hello input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set hello server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match hello number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name toobe loaded, basename of input data files, input format file, and number of partitions
    $tbname = "<table_name>"
    $basename = "<base_input_data_filename_no_extension>"
    $fmtfile = "<full_path_to_format_file>"

    # Create log directory if it does not exist
    New-Item -ErrorAction Ignore -ItemType directory -Path $logdir

    # BCP example using Windows authentication
    $ScriptBlock1 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -T -b 2500 -t "," -r \n
    }

    # BCP example using SQL authentication
    $ScriptBlock2 = {
       param($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $num, $sqlusr, $server, $pass)
       bcp ($dbname + ".." + $tbname) in ($indir + "\" + $basename + "_" + $num + ".csv") -o ($logdir + "\" + $tbname + "_" + $num + ".txt") -h "TABLOCK" -F 2 -C "RAW" -f ($fmtfile) -U $sqlusr -S $server -P $pass -b 2500 -t "," -r \n
    }

    # Background processing of all partitions
    for ($i=1; $i -le $numofparts; $i++)
    {
       Write-Output "Submit loading trip and fare partitions # $i"
       if ($sqlauth -eq 0) {
          # Use Windows authentication
          Start-Job -ScriptBlock $ScriptBlock1 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i)
       } 
       else {
          # Use SQL authentication
          Start-Job -ScriptBlock $ScriptBlock2 -Arg ($dbname, $tbname, $basename, $fmtfile, $indir, $logdir, $i, $sqlusr, $server, $pass)
       }
    }

    Get-Job

    # Optional - Wait till all jobs complete and report date and time
    date
    While (Get-Job -State "Running") { Start-Sleep 10 }
    date


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a><span data-ttu-id="011db-130">Criar índices toooptimize junções e o desempenho da consulta</span><span class="sxs-lookup"><span data-stu-id="011db-130">Create indexes toooptimize joins and query performance</span></span>
* <span data-ttu-id="011db-131">Se você extrairá dados para modelagem de várias tabelas, crie índices em chaves de junção Olá tooimprove Olá junção desempenho.</span><span class="sxs-lookup"><span data-stu-id="011db-131">If you will extract data for modeling from multiple tables, create indexes on hello join keys tooimprove hello join performance.</span></span>
* <span data-ttu-id="011db-132">[Criar índices](https://technet.microsoft.com/library/ms188783.aspx) (clusterizado ou não clusterizado) direcionamento hello mesmo grupo de arquivos para cada partição, para ex.:</span><span class="sxs-lookup"><span data-stu-id="011db-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting hello same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="011db-133">ou</span><span class="sxs-lookup"><span data-stu-id="011db-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="011db-134">Você pode escolher toocreate índices Olá antes de importar dados de saudação em massa.</span><span class="sxs-lookup"><span data-stu-id="011db-134">You may choose toocreate hello indexes before bulk importing hello data.</span></span> <span data-ttu-id="011db-135">Carregamento de dados Olá reduzem a criação de índice antes da importação em massa.</span><span class="sxs-lookup"><span data-stu-id="011db-135">Index creation before bulk importing will slow down hello data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="011db-136">Exemplo de Processo e Tecnologia de Análise Avançada em ação</span><span class="sxs-lookup"><span data-stu-id="011db-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="011db-137">Para obter um exemplo passo a passo de ponta a ponta usando Olá o processo de análise do Cortana com um conjunto de dados público, consulte [Cortana análise de processo em ação: usando o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="011db-137">For an end-to-end walkthrough example using hello Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

