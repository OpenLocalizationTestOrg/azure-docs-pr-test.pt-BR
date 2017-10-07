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
# <a name="parallel-bulk-data-import-using-sql-partition-tables"></a>Importação de Dados em Massa Paralela Usando Tabelas de Partição do SQL
Este documento descreve como toobuild particionada tabelas para a importação em massa paralela rápido do banco de dados do SQL Server data tooa. Para grandes dados carregamento/transferência tooa banco de dados SQL, o importar dados toohello banco de dados SQL e as consultas subsequentes pode ser melhorado usando *tabelas particionadas e exibições*. 

## <a name="create-a-new-database-and-a-set-of-filegroups"></a>Criar um novo banco de dados e um conjunto de grupos de arquivos
* [Crie um novo banco de dados](https://technet.microsoft.com/library/ms176061.aspx), se ainda não houver um.
* Adicione grupos de arquivos toohello banco de dados que armazenará arquivos físicos Olá particionado. Isso pode ser feito com [criar banco de dados](https://technet.microsoft.com/library/ms176061.aspx) se novo ou [ALTER DATABASE](https://msdn.microsoft.com/library/bb522682.aspx) se o banco de dados de saudação já existe.
* Adicione um ou mais arquivos de banco de dados tooeach de arquivos (conforme necessário).
  
  > [!NOTE]
  > Especifique o grupo de arquivos de destino de saudação que mantém os dados para esta partição e hello nomes do arquivo de banco de dados físico onde os dados do grupo de arquivos de saudação serão armazenados.
  > 
  > 

Olá exemplo a seguir cria um novo banco de dados com três grupos de arquivos diferentes Olá primário e grupos de log, que contém um arquivo físico em cada um. arquivos de banco de dados de saudação são criados na pasta de dados do SQL Server padrão hello, conforme configurado na instância do SQL Server hello. Para obter mais informações sobre os locais de arquivo padrão hello, consulte [locais de arquivo padrão e nomeadas instâncias do SQL Server](https://msdn.microsoft.com/library/ms143547.aspx).

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

## <a name="create-a-partitioned-table"></a>Criar uma tabela particionada
Crie tabelas particionadas de acordo com o esquema de dados toohello, grupos de arquivos do banco de dados mapeado toohello criados na etapa anterior hello. Quando os dados são importados em massa toohello particionada tabelas, registros serão distribuídos entre grupos de arquivos de saudação de acordo com o esquema de partição tooa, conforme descrito abaixo.

**toocreate uma tabela de partição, você precisa:**

* [Criar uma função de partição](https://msdn.microsoft.com/library/ms187802.aspx) que define o intervalo de saudação de valores/limites toobe incluídos em cada tabela de partição individual, por exemplo, as partições de toolimit por mês (alguns\_datetime\_campo) no ano Olá 2013:
  
        CREATE PARTITION FUNCTION <DatetimeFieldPFN>(<datetime_field>)  
        AS RANGE RIGHT FOR VALUES (
            '20130201', '20130301', '20130401',
            '20130501', '20130601', '20130701', '20130801',
            '20130901', '20131001', '20131101', '20131201' )
* [Criar um esquema de partição](https://msdn.microsoft.com/library/ms179854.aspx) que mapeia cada intervalo de partição no hello partição função tooa grupo de arquivos físico, por exemplo:
  
        CREATE PARTITION SCHEME <DatetimeFieldPScheme> AS  
        PARTITION <DatetimeFieldPFN> too(
        <filegroup_1>, <filegroup_2>, <filegroup_3>, <filegroup_4>,
        <filegroup_5>, <filegroup_6>, <filegroup_7>, <filegroup_8>,
        <filegroup_9>, <filegroup_10>, <filegroup_11>, <filegroup_12> )
  
  intervalos de saudação tooverify em vigor em cada função toohello de acordo/esquema de partição, execute Olá consulta a seguir:
  
        SELECT psch.name as PartitionScheme,
            prng.value AS ParitionValue,
            prng.boundary_id AS BoundaryID
        FROM sys.partition_functions AS pfun
        INNER JOIN sys.partition_schemes psch ON pfun.function_id = psch.function_id
        INNER JOIN sys.partition_range_values prng ON prng.function_id=pfun.function_id
        WHERE pfun.name = <DatetimeFieldPFN>
* [Criar tabela particionada](https://msdn.microsoft.com/library/ms174979.aspx)(s) de acordo com o esquema de dados tooyour e especifique o campo de esquema e a restrição de partição Olá usado toopartition tabela de hello, por exemplo:
  
        CREATE TABLE <table_name> ( [include schema definition here] )
        ON <TablePScheme>(<partition_field>)

Para obter mais informações, consulte [Criar tabelas e índices particionados](https://msdn.microsoft.com/library/ms188730.aspx).

## <a name="bulk-import-hello-data-for-each-individual-partition-table"></a>Saudação de importar em massa dados para cada tabela de partição individual
* Você pode usar o BCP, BULK INSERT ou outros métodos como o [Assistente de Migração do SQL Server](http://sqlazuremw.codeplex.com/). exemplo Hello fornecido usa o método BCP de saudação.
* [Alterar banco de dados de saudação](https://msdn.microsoft.com/library/bb522682.aspx) sobrecarga de toominimize tooBULK_LOGGED esquema de log, por exemplo, de log de transações de toochange:
  
        ALTER DATABASE <database_name> SET RECOVERY BULK_LOGGED
* dados tooexpedite carregar, inicie operações de importação em massa Olá em paralelo. Para obter dicas sobre como acelerar a importação em massa de big data em bancos de dados do SQL Server, consulte [Carregar 1 TB em menos de 1 hora](http://blogs.msdn.com/b/sqlcat/archive/2006/05/19/602142.aspx).

Olá seguinte script do PowerShell é um exemplo de carregamento usando o BCP de dados paralelos.

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


## <a name="create-indexes-toooptimize-joins-and-query-performance"></a>Criar índices toooptimize junções e o desempenho da consulta
* Se você extrairá dados para modelagem de várias tabelas, crie índices em chaves de junção Olá tooimprove Olá junção desempenho.
* [Criar índices](https://technet.microsoft.com/library/ms188783.aspx) (clusterizado ou não clusterizado) direcionamento hello mesmo grupo de arquivos para cada partição, para ex.:
  
        CREATE CLUSTERED INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  ou
  
        CREATE INDEX <table_idx> ON <table_name>( [include index columns here] )
        ON <TablePScheme>(<partition)field>)
  
  > [!NOTE]
  > Você pode escolher toocreate índices Olá antes de importar dados de saudação em massa. Carregamento de dados Olá reduzem a criação de índice antes da importação em massa.
  > 
  > 

## <a name="advanced-analytics-process-and-technology-in-action-example"></a>Exemplo de Processo e Tecnologia de Análise Avançada em ação
Para obter um exemplo passo a passo de ponta a ponta usando Olá o processo de análise do Cortana com um conjunto de dados público, consulte [Cortana análise de processo em ação: usando o SQL Server](machine-learning-data-science-process-sql-walkthrough.md).

