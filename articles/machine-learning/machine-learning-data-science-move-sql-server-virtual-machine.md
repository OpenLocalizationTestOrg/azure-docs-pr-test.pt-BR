---
title: "aaaMove dados tooSQL Server em uma máquina virtual do Azure | Microsoft Docs"
description: Move os dados de arquivos simples ou de um tooSQL do SQL Server local Server na VM do Azure.
services: machine-learning
documentationcenter: 
author: bradsev
manager: jhubbard
editor: cgronlun
ms.assetid: 2c9ef1d3-4f5c-4b1f-bf06-223646c8af06
ms.service: machine-learning
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 03/24/2017
ms.author: bradsev
ms.openlocfilehash: 63e02158f9c99f4478c4eb1cde62c877983dcf27
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="move-data-toosql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="2952c-103">Mover dados tooSQL Server em uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="2952c-103">Move data tooSQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="2952c-104">Este tópico descreve as opções de saudação de movimentação de dados de arquivos simples (formatos CSV ou TSV) ou de um tooSQL do SQL Server local Server em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="2952c-104">This topic outlines hello options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server tooSQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="2952c-105">Essas tarefas para mover dados na nuvem toohello fazem parte da saudação processo de ciência de dados de equipe.</span><span class="sxs-lookup"><span data-stu-id="2952c-105">These tasks for moving data toohello cloud are part of hello Team Data Science Process.</span></span>

<span data-ttu-id="2952c-106">Para um tópico que descreve as opções de saudação para mover dados tooan banco de dados do SQL Azure para o aprendizado de máquina, consulte [mover dados tooan banco de dados do SQL Azure para o aprendizado de máquina do Azure](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="2952c-106">For a topic that outlines hello options for moving data tooan Azure SQL Database for Machine Learning, see [Move data tooan Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="2952c-107">Olá **menu** abaixo tootopics links que descrevem como dados tooingest em outros ambientes de destino onde os dados saudação podem ser armazenados e processados durante Olá processo de ciência de dados da equipe (TDSP).</span><span class="sxs-lookup"><span data-stu-id="2952c-107">hello **menu** below links tootopics that describe how tooingest data into other target environments where hello data can be stored and processed during hello Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="2952c-108">Olá tabela a seguir resume as opções de saudação para mover dados tooSQL Server em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="2952c-108">hello following table summarizes hello options for moving data tooSQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="2952c-109"><b>FONTE</b></span><span class="sxs-lookup"><span data-stu-id="2952c-109"><b>SOURCE</b></span></span> | <span data-ttu-id="2952c-110"><b>DESTINO: SQL Server na VM do Azure</b></span><span class="sxs-lookup"><span data-stu-id="2952c-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="2952c-111"><b>Arquivo simples</b></span><span class="sxs-lookup"><span data-stu-id="2952c-111"><b>Flat File</b></span></span> |<span data-ttu-id="2952c-112">1. <a href="#insert-tables-bcp">Utilitário de BCP (cópia em massa de linha de comando)</a></span><span class="sxs-lookup"><span data-stu-id="2952c-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="2952c-113">2. <a href="#insert-tables-bulkquery">Consulta SQL de inserção em massa </a></span><span class="sxs-lookup"><span data-stu-id="2952c-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="2952c-114">3. <a href="#sql-builtin-utilities">Utilitários gráficos internos no SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="2952c-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="2952c-115"><b>SQL Server local</b></span><span class="sxs-lookup"><span data-stu-id="2952c-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="2952c-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Implantar um Assistente de VM do Microsoft Azure tooa banco de dados do SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="2952c-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="2952c-117">2. <a href="#export-flat-file">Exportar tooa simples de arquivo</a></span><span class="sxs-lookup"><span data-stu-id="2952c-117">2. <a href="#export-flat-file">Export tooa flat File </a></span></span><br> <span data-ttu-id="2952c-118">3. <a href="#sql-migration">Assistente de Migração de Banco de Dados SQL</a></span><span class="sxs-lookup"><span data-stu-id="2952c-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="2952c-119">4. <a href="#sql-backup">Backup e restauração de banco de dados</a></span><span class="sxs-lookup"><span data-stu-id="2952c-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="2952c-120">Observe que este documento pressupõe que os comandos SQL sejam executados no SQL Server Management Studio ou no Gerenciador de Banco de Dados do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="2952c-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="2952c-121">Como alternativa, você pode usar [do Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate e agendar um pipeline que irá mover dados tooa VM do SQL Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="2952c-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) toocreate and schedule a pipeline that will move data tooa SQL Server VM on Azure.</span></span> <span data-ttu-id="2952c-122">Para obter mais informações, consulte [Copiar dados com o Azure Data Factory (Atividade de Cópia)](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="2952c-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="2952c-123"><a name="prereqs"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="2952c-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="2952c-124">Este tutorial presume que você tenha:</span><span class="sxs-lookup"><span data-stu-id="2952c-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="2952c-125">Uma **assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="2952c-125">An **Azure subscription**.</span></span> <span data-ttu-id="2952c-126">Se você não tiver uma assinatura, você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="2952c-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="2952c-127">Uma **conta de armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="2952c-127">An **Azure storage account**.</span></span> <span data-ttu-id="2952c-128">Você usará uma conta de armazenamento do Azure para armazenar dados de saudação neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="2952c-128">You will use an Azure storage account for storing hello data in this tutorial.</span></span> <span data-ttu-id="2952c-129">Se você não tiver uma conta de armazenamento do Azure, consulte Olá [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) artigo.</span><span class="sxs-lookup"><span data-stu-id="2952c-129">If you don't have an Azure storage account, see hello [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="2952c-130">Depois que você criou a conta de armazenamento hello, você precisará conta de saudação tooobtain chave usada tooaccess armazenamento de saudação.</span><span class="sxs-lookup"><span data-stu-id="2952c-130">After you have created hello storage account, you will need tooobtain hello account key used tooaccess hello storage.</span></span> <span data-ttu-id="2952c-131">Confira [Gerenciar as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="2952c-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="2952c-132">**SQL Server em uma VM do Azure**provisionado.</span><span class="sxs-lookup"><span data-stu-id="2952c-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="2952c-133">Para obter instruções, consulte [Configurar uma máquina virtual do SQL Server do Azure como um servidor do IPython Notebook para análises avançadas](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="2952c-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="2952c-134">**Azure PowerShell** instalado e configurado localmente.</span><span class="sxs-lookup"><span data-stu-id="2952c-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="2952c-135">Para obter instruções, consulte [como tooinstall e configurar o Azure PowerShell](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="2952c-135">For instructions, see [How tooinstall and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="2952c-136"><a name="filesource_to_sqlonazurevm"></a>Movimentação de dados de uma fonte de arquivo simples tooSQL Server em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="2952c-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="2952c-137">Se os dados estiverem em um arquivo simples (organizado em um formato de linha ou coluna), ele pode ser movido tooSQL Server VM no Azure por meio de saudação métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="2952c-137">If your data is in a flat file (arranged in a row/column format), it can be moved tooSQL Server VM on Azure via hello following methods:</span></span>

1. [<span data-ttu-id="2952c-138">Utilitário de BCP (cópia em massa de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="2952c-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="2952c-139">Consulta SQL de inserção em massa </span><span class="sxs-lookup"><span data-stu-id="2952c-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="2952c-140">Utilitários gráficos internos no SQL Server (Importar/Exportar, SSIS)</span><span class="sxs-lookup"><span data-stu-id="2952c-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="2952c-141"><a name="insert-tables-bcp"></a>Utilitário de BCP (cópia em massa de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="2952c-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="2952c-142">BCP é um utilitário de linha de comando instalado com o SQL Server e é um dos dados de toomove maneiras mais rápidos de saudação.</span><span class="sxs-lookup"><span data-stu-id="2952c-142">BCP is a command-line utility installed with SQL Server and is one of hello quickest ways toomove data.</span></span> <span data-ttu-id="2952c-143">Ele funciona em todas as três variantes do SQL Server (SQL Server local, SQL Azure e VM do SQL Server no Azure).</span><span class="sxs-lookup"><span data-stu-id="2952c-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="2952c-144">**Onde os dados devem estar para o BCP?**</span><span class="sxs-lookup"><span data-stu-id="2952c-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="2952c-145">Embora não seja necessário, com arquivos que contêm dados de origem localizados no mesmo computador que o SQL Server de destino Olá permite transferências mais rápidas (velocidade vs local disco rede velocidade de e/s) de saudação.</span><span class="sxs-lookup"><span data-stu-id="2952c-145">While it is not required, having files containing source data located on hello same machine as hello target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="2952c-146">Você pode mover Olá simples arquivos contendo máquina toohello de dados onde o SQL Server está instalado usando cópia de arquivo de várias ferramentas, como [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) ou copie/cole do windows via remoto Protocolo de área de trabalho (RDP).</span><span class="sxs-lookup"><span data-stu-id="2952c-146">You can move hello flat files containing data toohello machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="2952c-147">Certifique-se de que banco de dados de saudação e tabelas de saudação são criadas no banco de dados do SQL Server Olá destino.</span><span class="sxs-lookup"><span data-stu-id="2952c-147">Ensure that hello database and hello tables are created on hello target SQL Server database.</span></span> <span data-ttu-id="2952c-148">Aqui está um exemplo de como toodo que usar Olá `Create Database` e `Create Table` comandos:</span><span class="sxs-lookup"><span data-stu-id="2952c-148">Here is an example of how toodo that using hello `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="2952c-149">Gere Olá arquivo de formato que descreve o esquema Olá Olá da tabela emitindo Olá comando a seguir de saudação de linha de comando da máquina Olá onde bcp está instalado.</span><span class="sxs-lookup"><span data-stu-id="2952c-149">Generate hello format file that describes hello schema for hello table by issuing hello following command from hello command-line of hello machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="2952c-150">Inserir dados de saudação no banco de dados de saudação usando o comando bcp de saudação da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="2952c-150">Insert hello data into hello database using hello bcp command as follows.</span></span> <span data-ttu-id="2952c-151">Supondo que hello do SQL Server está instalado no mesmo computador, isso deve funcionar de saudação de linha de comando:</span><span class="sxs-lookup"><span data-stu-id="2952c-151">This should work from hello command-line assuming that hello SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="2952c-152">**Otimizando BCP insere** consulte Olá artigo a seguir ['Diretrizes para otimizar importação'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize tal insere.</span><span class="sxs-lookup"><span data-stu-id="2952c-152">**Optimizing BCP Inserts** Please refer hello following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) toooptimize such inserts.</span></span>
>
>

### <span data-ttu-id="2952c-153"><a name="insert-tables-bulkquery-parallel"></a>Paralelização de inserções para movimentação de dados mais rápida</span><span class="sxs-lookup"><span data-stu-id="2952c-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="2952c-154">Se dados Olá que você está movendo forem grandes, você pode acelerar as coisas executando vários comandos BCP ao mesmo tempo em paralelo em um Script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="2952c-154">If hello data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="2952c-155">**Ingestão de grandes dados** toooptimize dados carregando para conjuntos de dados grandes e muito grande, partição suas tabelas de banco de dados lógico e físico usando várias tabelas de grupos de arquivos e de partição.</span><span class="sxs-lookup"><span data-stu-id="2952c-155">**Big data Ingestion** toooptimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="2952c-156">Para obter mais informações sobre como criar e carregar dados toopartition tabelas, consulte [tabelas de partição do SQL carga paralela](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="2952c-156">For more information about creating and loading data toopartition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="2952c-157">Olá abaixo de script do PowerShell de exemplo demonstram paralelas inserções usando bcp:</span><span class="sxs-lookup"><span data-stu-id="2952c-157">hello sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for hello script tooexecute
     # Define what each job does
       $ScriptBlock = {
           param($partitionnumber)

           #Explictly using SQL username password
           bcp database..tablename in datafile_path.csv -F 2 -f format_file_path.xml -U username@servername -S tcp:servername -P password -b block_size_to_move_in_single_attempt -t "," -r \n -o path_to_outputfile.$partitionnumber.txt

            #Trusted connection w.o username password (if you are using windows auth and are signed in with that credentials)
            #bcp database..tablename in datafile_path.csv -o path_to_outputfile.$partitionnumber.txt -h "TABLOCK" -F 2 -f format_file_path.xml  -T -b block_size_to_move_in_single_attempt -t "," -r \n
      }


    # Background processing of all partitions
    for ($i=1; $i -le $NO_OF_PARALLEL_JOBS; $i++)
    {
      Write-Debug "Submit loading partition # $i"
      Start-Job $ScriptBlock -Arg $i      
    }


    # Wait for it all toocomplete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting hello information back from hello jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset hello execution policy


### <span data-ttu-id="2952c-158"><a name="insert-tables-bulkquery"></a>Consulta SQL de inserção em massa</span><span class="sxs-lookup"><span data-stu-id="2952c-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="2952c-159">[Em massa inserir consulta do SQL](https://msdn.microsoft.com/library/ms188365) podem ser usados tooimport dados no banco de dados de saudação de arquivos com base em linha ou coluna (Olá suporte para tipos são abordados a[preparar dados para exportação em massa ou importar (SQL Server)](https://msdn.microsoft.com/library/ms188609)) tópico.</span><span class="sxs-lookup"><span data-stu-id="2952c-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used tooimport data into hello database from row/column based files (hello supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="2952c-160">Aqui estão alguns comandos de exemplo para inserção em massa:</span><span class="sxs-lookup"><span data-stu-id="2952c-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="2952c-161">Analisar os dados e definir opções personalizadas antes de importar toomake se que supõe que esse banco de dados do SQL Server Olá Olá mesmo formato para os campos especiais, como datas.</span><span class="sxs-lookup"><span data-stu-id="2952c-161">Analyze your data and set any custom options before importing toomake sure that hello SQL Server database assumes hello same format for any special fields such as dates.</span></span> <span data-ttu-id="2952c-162">Aqui está um exemplo de como data de saudação tooset Formatar como ano-mês-dia (se seus dados contiverem date de hello no formato ano-mês-dia):</span><span class="sxs-lookup"><span data-stu-id="2952c-162">Here is an example of how tooset hello date format as year-month-day (if your data contains hello date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="2952c-163">Importe dados usando as instruções de importação em massa:</span><span class="sxs-lookup"><span data-stu-id="2952c-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be hello row separator in your data
        )

### <span data-ttu-id="2952c-164"><a name="sql-builtin-utilities"></a>Utilitários internos no SQL Server</span><span class="sxs-lookup"><span data-stu-id="2952c-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="2952c-165">Você pode usar dados do SQL Server integrações Services (SSIS) tooimport em VM do SQL Server no Azure de um arquivo simples.</span><span class="sxs-lookup"><span data-stu-id="2952c-165">You can use SQL Server Integrations Services (SSIS) tooimport data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="2952c-166">O SSIS está disponível em dois ambientes de estúdio.</span><span class="sxs-lookup"><span data-stu-id="2952c-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="2952c-167">Para obter detalhes, consulte [Ambientes do Integration Services (SSIS) e Estúdio](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="2952c-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="2952c-168">Para obter detalhes sobre SQL Server Data Tools, consulte [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="2952c-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="2952c-169">Para obter detalhes sobre o Assistente de importação/exportação de saudação, consulte [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="2952c-169">For details on hello Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="2952c-170"><a name="sqlonprem_to_sqlonazurevm"></a>Movimentação de dados de local do SQL Server tooSQL Server em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="2952c-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server tooSQL Server on an Azure VM</span></span>
<span data-ttu-id="2952c-171">Você também pode usar o hello estratégias de migração a seguir:</span><span class="sxs-lookup"><span data-stu-id="2952c-171">You can also use hello following migration strategies:</span></span>

1. [<span data-ttu-id="2952c-172">Implantar um Assistente de VM do Microsoft Azure tooa banco de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="2952c-172">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="2952c-173">Exportar arquivo de tooFlat</span><span class="sxs-lookup"><span data-stu-id="2952c-173">Export tooFlat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="2952c-174">Assistente de Migração de Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="2952c-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="2952c-175">Backup e restauração de banco de dados</span><span class="sxs-lookup"><span data-stu-id="2952c-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="2952c-176">Descrevemos cada um deles abaixo:</span><span class="sxs-lookup"><span data-stu-id="2952c-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-tooa-microsoft-azure-vm-wizard"></a><span data-ttu-id="2952c-177">Implantar um Assistente de VM do Microsoft Azure tooa banco de dados do SQL Server</span><span class="sxs-lookup"><span data-stu-id="2952c-177">Deploy a SQL Server Database tooa Microsoft Azure VM wizard</span></span>
<span data-ttu-id="2952c-178">Olá **implantar um Assistente de VM do Microsoft Azure do banco de dados do SQL Server tooa** é um modo simples e recomendada toomove os dados de um tooSQL de instância do SQL Server local Server em uma VM do Azure.</span><span class="sxs-lookup"><span data-stu-id="2952c-178">hello **Deploy a SQL Server Database tooa Microsoft Azure VM wizard** is a simple and recommended way toomove data from an on-premises SQL Server instance tooSQL Server on an Azure VM.</span></span> <span data-ttu-id="2952c-179">Para obter etapas detalhadas, bem como uma discussão sobre outras alternativas, consulte [migrar um banco de dados tooSQL Server em uma VM do Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="2952c-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database tooSQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="2952c-180"><a name="export-flat-file"></a>Exportar arquivo de tooFlat</span><span class="sxs-lookup"><span data-stu-id="2952c-180"><a name="export-flat-file"></a>Export tooFlat File</span></span>
<span data-ttu-id="2952c-181">Vários métodos podem ser usado toobulk exportar dados do servidor SQL local conforme documentado no hello [importação e exportação de dados (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) tópico.</span><span class="sxs-lookup"><span data-stu-id="2952c-181">Various methods can be used toobulk export data from an On-Premises SQL Server as documented in hello [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="2952c-182">Este documento aborda Olá programa de cópia em massa (BCP) como um exemplo.</span><span class="sxs-lookup"><span data-stu-id="2952c-182">This document will cover hello Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="2952c-183">Quando dados são exportados em um arquivo simples, ele poderá ser importado tooanother SQL server usando a importação em massa.</span><span class="sxs-lookup"><span data-stu-id="2952c-183">Once data is exported into a flat file, it can be imported tooanother SQL server using bulk import.</span></span>

1. <span data-ttu-id="2952c-184">Exportar dados de saudação do local do SQL Server tooa arquivo usando o utilitário bcp de saudação da seguinte maneira</span><span class="sxs-lookup"><span data-stu-id="2952c-184">Export hello data from on-premises SQL Server tooa File using hello bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="2952c-185">Criar banco de dados de saudação e a tabela de saudação na VM do SQL Server no Azure usando Olá `create database` e `create table` para o esquema da tabela Olá exportada na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="2952c-185">Create hello database and hello table on SQL Server VM on Azure using hello `create database` and `create table` for hello table schema exported in step 1.</span></span>
3. <span data-ttu-id="2952c-186">Crie um arquivo de formato para descrever o esquema de tabela de saudação de dados hello está sendo exportado/importado.</span><span class="sxs-lookup"><span data-stu-id="2952c-186">Create a format file for describing hello table schema of hello data being exported/imported.</span></span> <span data-ttu-id="2952c-187">Detalhes do arquivo de formato de saudação são descritos em [criar um arquivo de formato (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="2952c-187">Details of hello format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="2952c-188">Geração de arquivo de formato quando executar o BCP do hello máquina do SQL Server</span><span class="sxs-lookup"><span data-stu-id="2952c-188">Format file generation when running BCP from hello SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="2952c-189">Geração de arquivo de formato ao executar o BCP remotamente em um SQL Server</span><span class="sxs-lookup"><span data-stu-id="2952c-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="2952c-190">Use qualquer um dos métodos de saudação descritos na seção [movendo dados de origem de arquivo](#filesource_to_sqlonazurevm) toomove dados de saudação em arquivos simples tooa do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="2952c-190">Use any of hello methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) toomove hello data in flat files tooa SQL Server.</span></span>

### <span data-ttu-id="2952c-191"><a name="sql-migration"></a>Assistente de Migração de Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="2952c-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="2952c-192">[Assistente de migração de banco de dados do SQL Server](http://sqlazuremw.codeplex.com/) fornece uma maneira fácil de usar toomove dados entre duas instâncias do SQL server.</span><span class="sxs-lookup"><span data-stu-id="2952c-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way toomove data between two SQL server instances.</span></span> <span data-ttu-id="2952c-193">Ele permite que o esquema de dados de Olá Olá usuário toomap entre as origens e tabelas de destino, escolha tipos de coluna e várias outras funcionalidades.</span><span class="sxs-lookup"><span data-stu-id="2952c-193">It allows hello user toomap hello data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="2952c-194">Ele usa a cópia em massa (BCP) sob as coberturas de saudação.</span><span class="sxs-lookup"><span data-stu-id="2952c-194">It uses bulk copy (BCP) under hello covers.</span></span> <span data-ttu-id="2952c-195">Uma captura de tela de saudação bem-vindo à tela hello migração de banco de dados SQL assistente é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2952c-195">A screenshot of hello welcome screen for hello SQL Database Migration wizard is shown below.</span></span>  

![Assistente de Migração do SQL Server][2]

### <span data-ttu-id="2952c-197"><a name="sql-backup"></a>Backup e restauração de banco de dados</span><span class="sxs-lookup"><span data-stu-id="2952c-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="2952c-198">O SQL Server dá suporte a:</span><span class="sxs-lookup"><span data-stu-id="2952c-198">SQL Server supports:</span></span>

1. <span data-ttu-id="2952c-199">[O banco de dados fazer backup e restaurar a funcionalidade](https://msdn.microsoft.com/library/ms187048.aspx) (ambos os tooa local bacpac ou arquivo de exportação tooblob) e [aplicativos da camada de dados](https://msdn.microsoft.com/library/ee210546.aspx) (usando bacpac).</span><span class="sxs-lookup"><span data-stu-id="2952c-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both tooa local file or bacpac export tooblob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="2952c-200">Capacidade toodirectly criar VMs do SQL Server no Azure com um banco de dados copiado ou cópia tooan SQL Azure banco de dados existente.</span><span class="sxs-lookup"><span data-stu-id="2952c-200">Ability toodirectly create SQL Server VMs on Azure with a copied database or copy tooan existing SQL Azure database.</span></span> <span data-ttu-id="2952c-201">Para obter mais detalhes, consulte [Olá Use o Assistente para cópia de banco de dados](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="2952c-201">For more details, see [Use hello Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="2952c-202">Backup/restauração de uma captura de tela de volta do banco de dados de saudação opções do SQL Server Management Studio é mostrado abaixo.</span><span class="sxs-lookup"><span data-stu-id="2952c-202">A screenshot of hello Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Ferramenta de Importação do SQL Server][1]

## <a name="resources"></a><span data-ttu-id="2952c-204">Recursos</span><span class="sxs-lookup"><span data-stu-id="2952c-204">Resources</span></span>
[<span data-ttu-id="2952c-205">Migrar um banco de dados tooSQL Server em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="2952c-205">Migrate a Database tooSQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="2952c-206">Visão geral do SQL Server em máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="2952c-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
