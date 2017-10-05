---
title: "Compilar e otimizar tabelas para importação paralela rápida de dados para um SQL Server em uma VM do Azure | Microsoft Docs"
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
ms.openlocfilehash: aae4e4f59e76bf48b00a2ee92aedd7d5643ba91a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a><span data-ttu-id="abbce-103">Importação de Dados em Massa Paralela Usando Tabelas de Partição do SQL</span><span class="sxs-lookup"><span data-stu-id="abbce-103">Parallel Bulk Data Import Using SQL Partition Tables</span></span>
<span data-ttu-id="abbce-104">Este documento descreve como compilar tabelas particionadas para rápida importação de dados em massa paralela para um banco de dados do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="abbce-104">This document describes how to build partitioned tables for fast parallel bulk importing of data to a SQL Server database.</span></span> <span data-ttu-id="abbce-105">Para carregamento/transferência de Big Data para um banco de dados SQL, a importação de dados para o banco de dados SQL e consultas posteriores podem ser melhoradas usando *Exibições e Tabelas Particionadas*.</span><span class="sxs-lookup"><span data-stu-id="abbce-105">For big data loading/transfer to a SQL database, importing data to the SQL DB and subsequent queries can be improved by using *Partitioned Tables and Views*.</span></span> 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a><span data-ttu-id="abbce-106">Criar um novo banco de dados e um conjunto de grupos de arquivos</span><span class="sxs-lookup"><span data-stu-id="abbce-106">Create a new database and a set of filegroups</span></span>
* <span data-ttu-id="abbce-107">[Crie um novo banco de dados](https://technet.microsoft.com/library/ms176061.aspx), se ainda não houver um.</span><span class="sxs-lookup"><span data-stu-id="abbce-107">[Create a new database](https://technet.microsoft.com/library/ms176061.aspx), if it doesn't exist already.</span></span>
* <span data-ttu-id="abbce-108">Adicione grupos de arquivos de banco de dados ao banco de dados que contém os arquivos físicos particionados. Isso poderá ser feito com [CRIAR BANCO DE DADOS](https://technet.microsoft.com/library/ms176061.aspx), se for novo, ou [ALTERAR BANCO DE DADOS](https://msdn.microsoft.com/library/bb522682.aspx), se o banco de dados já existir.</span><span class="sxs-lookup"><span data-stu-id="abbce-108">Add database filegroups to the database which will hold the partitioned physical files.This can be done with [CREATE DATABASE](https://technet.microsoft.com/library/ms176061.aspx) if new or [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) if the database exists already.</span></span>
* <span data-ttu-id="abbce-109">Adicione um ou mais arquivos (conforme necessário) para cada grupo de arquivos de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="abbce-109">Add one or more files (as needed) to each database filegroup.</span></span>
  
  > [!NOTE]
  > <span data-ttu-id="abbce-110">Especifique o grupo de arquivos de destino que contém os dados dessa partição e os nomes dos arquivos de banco de dados físico em que serão armazenados os dados do grupo de arquivos.</span><span class="sxs-lookup"><span data-stu-id="abbce-110">Specify the target filegroup which holds data for this partition and the physical database file name(s) where the filegroup data will be stored.</span></span>
  > 
  > 

<span data-ttu-id="abbce-111">O exemplo a seguir cria um novo banco de dados com três grupos de arquivos que não são os grupos principal e de registro, contendo um arquivo físico cada um.</span><span class="sxs-lookup"><span data-stu-id="abbce-111">The following example creates a new database with three filegroups other than the primary and log groups, containing one physical file in each.</span></span> <span data-ttu-id="abbce-112">Os arquivos de banco de dados são criados na pasta de Dados do SQL Server padrão, conforme configurado na instância do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="abbce-112">The database files are created in the default SQL Server Data folder, as configured in the SQL Server instance.</span></span> <span data-ttu-id="abbce-113">Para obter mais informações sobre os locais de arquivo padrão, consulte [Locais de arquivo para instâncias padrão e nomeadas do SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span><span class="sxs-lookup"><span data-stu-id="abbce-113">For more information about the default file locations, see [File Locations for Default and Named Instances of SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).</span></span>

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

## <a name="create-a-partitioned-table"></a><span data-ttu-id="abbce-114">Criar uma tabela particionada</span><span class="sxs-lookup"><span data-stu-id="abbce-114">Create a partitioned table</span></span>
<span data-ttu-id="abbce-115">Crie tabelas particionadas de acordo com o esquema de dados mapeado para os grupos de arquivos de banco de dados criados na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="abbce-115">Create partitioned table(s) according to the data schema, mapped to the database filegroups created in the previous step.</span></span> <span data-ttu-id="abbce-116">Quando dados são importados em massa para a tabela particionada, os registros serão distribuídos entre os grupos de arquivos de acordo com um esquema de partição, conforme descrito abaixo.</span><span class="sxs-lookup"><span data-stu-id="abbce-116">When data is bulk imported to the partitioned table(s), records will be distributed among the filegroups according to a partition scheme, as described below.</span></span>

<span data-ttu-id="abbce-117">**Para criar uma tabela de partição, você precisa:**</span><span class="sxs-lookup"><span data-stu-id="abbce-117">**To create a partition table, you need to:**</span></span>

* <span data-ttu-id="abbce-118">[Criar uma função de partição](https://msdn.microsoft.com/library/ms187802.aspx), que define o intervalo de valores/limites a serem incluídos em cada tabela de partição individual, por exemplo, para limitar as partições por month(some\_datetime\_field) no ano de 2013:</span><span class="sxs-lookup"><span data-stu-id="abbce-118">[Create a partition function](https://msdn.microsoft.com/library/ms187802.aspx) which defines the range of values/boundaries to be included in each individual partition table, e.g., to limit partitions by month(some\_datetime\_field) in the year 2013:</span></span>
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* <span data-ttu-id="abbce-119">[Criar um esquema de partição](https://msdn.microsoft.com/library/ms179854.aspx) , que mapeia cada intervalo de partição na função de partição para um grupo de arquivos físicos, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="abbce-119">[Create a partition scheme](https://msdn.microsoft.com/library/ms179854.aspx) which maps each partition range in the partition function to a physical filegroup, e.g.:</span></span>
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> TO (
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  <span data-ttu-id="abbce-120">Para verificar se os intervalos em vigor em cada partição de acordo com a função/esquema, execute a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="abbce-120">To verify the ranges in effect in each partition according to the function/scheme, run the following query:</span></span>
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* <span data-ttu-id="abbce-121">[Crie tabelas particionadas](https://msdn.microsoft.com/library/ms174979.aspx)de acordo com seu esquema de dados e especifique o campo de esquema e de restrição usados para particionar a tabela, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="abbce-121">[Create partitioned table](https://msdn.microsoft.com/library/ms174979.aspx)(s) according to your data schema, and specify the partition scheme and constraint field used to partition the table, e.g.:</span></span>
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

<span data-ttu-id="abbce-122">Para obter mais informações, consulte [Criar tabelas e índices particionados](https://msdn.microsoft.com/library/ms188730.aspx).</span><span class="sxs-lookup"><span data-stu-id="abbce-122">For more information, see [Create Partitioned Tables and Indexes](https://msdn.microsoft.com/library/ms188730.aspx).</span></span>

## <a name="bulk-import-the-data-for-each-individual-partition-table"></a><span data-ttu-id="abbce-123">Importe os dados em massa para cada tabela de partição individual</span><span class="sxs-lookup"><span data-stu-id="abbce-123">Bulk import the data for each individual partition table</span></span>
* <span data-ttu-id="abbce-124">Você pode usar o BCP, BULK INSERT ou outros métodos como o [Assistente de Migração do SQL Server](http://sqlazuremw.codeplex.com/).</span><span class="sxs-lookup"><span data-stu-id="abbce-124">You may use BCP, BULK INSERT, or other methods such as [SQL Server Migration Wizard](http://sqlazuremw.codeplex.com/).</span></span> <span data-ttu-id="abbce-125">O exemplo fornecido usa o método BCP.</span><span class="sxs-lookup"><span data-stu-id="abbce-125">The example provided uses the BCP method.</span></span>
* <span data-ttu-id="abbce-126">[Altere o banco de dados](https://msdn.microsoft.com/library/bb522682.aspx) para alterar o esquema de registro em log de transações como BULK_LOGGED para minimizar a sobrecarga de registros, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="abbce-126">[Alter the database](https://msdn.microsoft.com/library/bb522682.aspx) to change transaction logging scheme to BULK_LOGGED to minimize overhead of logging, e.g.:</span></span>
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* <span data-ttu-id="abbce-127">Para acelerar o carregamento de dados, inicie as operações de importação em massa paralela.</span><span class="sxs-lookup"><span data-stu-id="abbce-127">To expedite data loading, launch the bulk import operations in parallel.</span></span> <span data-ttu-id="abbce-128">Para obter dicas sobre como acelerar a importação em massa de big data em bancos de dados do SQL Server, consulte [Carregar 1 TB em menos de 1 hora](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span><span class="sxs-lookup"><span data-stu-id="abbce-128">For tips on expediting bulk importing of big data into SQL Server databases, see [Load 1TB in less than 1 hour](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).</span></span>

<span data-ttu-id="abbce-129">O script do PowerShell a seguir é um exemplo de carregamento de dados paralela que usa o BCP.</span><span class="sxs-lookup"><span data-stu-id="abbce-129">The following PowerShell script is an example of parallel data loading using BCP.</span></span>

    # Set database name, input data directory, and output log directory
    # This example loads comma-separated input data files
    # The example assumes the partitioned data files are named as <base_file_name>_<partition_number>.csv
    # Assumes the input data files include a header line. Loading starts at line number 2.

    $dbname = "<database_name>"
    $indir  = "<path_to_data_files>"
    $logdir = "<path_to_log_directory>"

    # Select authentication mode
    $sqlauth = 0

    # For SQL authentication, set the server and user credentials
    $sqlusr = "<user@server>"
    $server = "<tcp:serverdns>"
    $pass   = "<password>"

    # Set number of partitions per table - Should match the number of input data files per table
    $numofparts = <number_of_partitions>

    # Set table name to be loaded, basename of input data files, input format file, and number of partitions
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


## <a name="create-indexes-to-optimize-joins-and-query-performance"></a><span data-ttu-id="abbce-130">Crie índices para otimizar o desempenho de associações e consultas</span><span class="sxs-lookup"><span data-stu-id="abbce-130">Create indexes to optimize joins and query performance</span></span>
* <span data-ttu-id="abbce-131">Se você pretende extrair dados de modelagem de várias tabelas, crie índices nas chaves de associação para melhorar o desempenho da junção.</span><span class="sxs-lookup"><span data-stu-id="abbce-131">If you will extract data for modeling from multiple tables, create indexes on the join keys to improve the join performance.</span></span>
* <span data-ttu-id="abbce-132">[Crie índices](https://technet.microsoft.com/library/ms188783.aspx) (em cluster ou não clusterizados) direcionando o mesmo grupo de arquivos para cada partição, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="abbce-132">[Create indexes](https://technet.microsoft.com/library/ms188783.aspx) (clustered or non-clustered) targeting the same filegroup for each partition, for e.g.:</span></span>
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  <span data-ttu-id="abbce-133">ou</span><span class="sxs-lookup"><span data-stu-id="abbce-133">or,</span></span>
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > <span data-ttu-id="abbce-134">Você pode optar por criar os índices antes de importar os dados em massa.</span><span class="sxs-lookup"><span data-stu-id="abbce-134">You may choose to create the indexes before bulk importing the data.</span></span> <span data-ttu-id="abbce-135">Criar índices antes da importação em massa retardará o carregamento de dados.</span><span class="sxs-lookup"><span data-stu-id="abbce-135">Index creation before bulk importing will slow down the data loading.</span></span>
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a><span data-ttu-id="abbce-136">Exemplo de Processo e Tecnologia de Análise Avançada em ação</span><span class="sxs-lookup"><span data-stu-id="abbce-136">Advanced Analytics Process and Technology in Action Example</span></span>
<span data-ttu-id="abbce-137">Para obter um exemplo passo a passo completo do Processo de Análise do Cortana com um conjunto de dados público, consulte [Processo de Análise do Cortana em ação: usando o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span><span class="sxs-lookup"><span data-stu-id="abbce-137">For an end-to-end walkthrough example using the Cortana Analytics Process with a public dataset, see [Cortana Analytics Process in Action: using SQL Server](machine-learning-data-science-process-sql-walkthrough.md).</span></span>

