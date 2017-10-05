---
title: "Mover dados para o SQL Server em uma máquina virtual do Azure | Microsoft Docs"
description: Mover dados de arquivos simples ou de um SQL Server local para o SQL Server em uma VM do Azure.
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
ms.openlocfilehash: aa0cbba6bdb4cfdfe6ceee50c94f706aa0974924
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="move-data-to-sql-server-on-an-azure-virtual-machine"></a><span data-ttu-id="08a89-103">Mover dados para o SQL Server em uma máquina virtual do Azure</span><span class="sxs-lookup"><span data-stu-id="08a89-103">Move data to SQL Server on an Azure virtual machine</span></span>
<span data-ttu-id="08a89-104">Este tópico descreve as opções para mover dados de arquivos simples (formatos CSV ou TSV) ou de um SQL Server local para o SQL Server em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="08a89-104">This topic outlines the options for moving data either from flat files (CSV or TSV formats) or from an on-premises SQL Server to SQL Server on an Azure virtual machine.</span></span> <span data-ttu-id="08a89-105">Essas tarefas para movimentar dados para a nuvem fazem parte do Processo de Ciência de Dados de Equipe.</span><span class="sxs-lookup"><span data-stu-id="08a89-105">These tasks for moving data to the cloud are part of the Team Data Science Process.</span></span>

<span data-ttu-id="08a89-106">Para um tópico que descreve as opções para movimentação de dados para um Banco de Dados SQL do Azure para Machine Learning, consulte [Mover dados para um banco de dados SQL do Azure para o Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span><span class="sxs-lookup"><span data-stu-id="08a89-106">For a topic that outlines the options for moving data to an Azure SQL Database for Machine Learning, see [Move data to an Azure SQL Database for Azure Machine Learning](machine-learning-data-science-move-sql-azure.md).</span></span>

<span data-ttu-id="08a89-107">O **menu** abaixo vincula-se a tópicos que descrevem a inclusão de dados em outros ambientes de destino em que os dados podem ser armazenados e processados durante o TDSP (Processo de Ciência de Dados de Equipe).</span><span class="sxs-lookup"><span data-stu-id="08a89-107">The **menu** below links to topics that describe how to ingest data into other target environments where the data can be stored and processed during the Team Data Science Process (TDSP).</span></span>

[!INCLUDE [cap-ingest-data-selector](../../includes/cap-ingest-data-selector.md)]

<span data-ttu-id="08a89-108">A tabela a seguir resume as opções para mover dados para o SQL Server em uma máquina virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="08a89-108">The following table summarizes the options for moving data to SQL Server on an Azure virtual machine.</span></span>

| <span data-ttu-id="08a89-109"><b>FONTE</b></span><span class="sxs-lookup"><span data-stu-id="08a89-109"><b>SOURCE</b></span></span> | <span data-ttu-id="08a89-110"><b>DESTINO: SQL Server na VM do Azure</b></span><span class="sxs-lookup"><span data-stu-id="08a89-110"><b>DESTINATION: SQL Server on Azure VM</b></span></span> |
| --- | --- |
| <span data-ttu-id="08a89-111"><b>Arquivo simples</b></span><span class="sxs-lookup"><span data-stu-id="08a89-111"><b>Flat File</b></span></span> |<span data-ttu-id="08a89-112">1. <a href="#insert-tables-bcp">Utilitário de BCP (cópia em massa de linha de comando)</a></span><span class="sxs-lookup"><span data-stu-id="08a89-112">1. <a href="#insert-tables-bcp">Command-line bulk copy utility (BCP) </a></span></span><br> <span data-ttu-id="08a89-113">2. <a href="#insert-tables-bulkquery">Consulta SQL de inserção em massa </a></span><span class="sxs-lookup"><span data-stu-id="08a89-113">2. <a href="#insert-tables-bulkquery">Bulk Insert SQL Query </a></span></span><br> <span data-ttu-id="08a89-114">3. <a href="#sql-builtin-utilities">Utilitários gráficos internos no SQL Server</a></span><span class="sxs-lookup"><span data-stu-id="08a89-114">3. <a href="#sql-builtin-utilities">Graphical Built-in Utilities in SQL Server</a></span></span> |
| <span data-ttu-id="08a89-115"><b>SQL Server local</b></span><span class="sxs-lookup"><span data-stu-id="08a89-115"><b>On-Premises SQL Server</b></span></span> |<span data-ttu-id="08a89-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Assistente para implantar um Banco de Dados do SQL Server em uma VM do Microsoft Azure</a></span><span class="sxs-lookup"><span data-stu-id="08a89-116">1. <a href="#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard">Deploy a SQL Server Database to a Microsoft Azure VM wizard</a></span></span><br> <span data-ttu-id="08a89-117">2. <a href="#export-flat-file">Exportar para um arquivo simples </a></span><span class="sxs-lookup"><span data-stu-id="08a89-117">2. <a href="#export-flat-file">Export to a flat File </a></span></span><br> <span data-ttu-id="08a89-118">3. <a href="#sql-migration">Assistente de Migração de Banco de Dados SQL</a></span><span class="sxs-lookup"><span data-stu-id="08a89-118">3. <a href="#sql-migration">SQL Database Migration Wizard </a></span></span> <br> <span data-ttu-id="08a89-119">4. <a href="#sql-backup">Backup e restauração de banco de dados</a></span><span class="sxs-lookup"><span data-stu-id="08a89-119">4. <a href="#sql-backup">Database back up and restore </a></span></span><br> |

<span data-ttu-id="08a89-120">Observe que este documento pressupõe que os comandos SQL sejam executados no SQL Server Management Studio ou no Gerenciador de Banco de Dados do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="08a89-120">Note that this document assumes that SQL commands are executed from SQL Server Management Studio or Visual Studio Database Explorer.</span></span>

> [!TIP]
> <span data-ttu-id="08a89-121">Como alternativa, você pode usar o [Azure  Factory](https://azure.microsoft.com/services/data-factory/) para criar e agendar um pipeline que move dados para uma VM do SQL Server no Azure.</span><span class="sxs-lookup"><span data-stu-id="08a89-121">As an alternative, you can use [Azure Data Factory](https://azure.microsoft.com/services/data-factory/) to create and schedule a pipeline that will move data to a SQL Server VM on Azure.</span></span> <span data-ttu-id="08a89-122">Para obter mais informações, consulte [Copiar dados com o Azure Data Factory (Atividade de Cópia)](../data-factory/data-factory-data-movement-activities.md).</span><span class="sxs-lookup"><span data-stu-id="08a89-122">For more information, see [Copy data with Azure Data Factory (Copy Activity)](../data-factory/data-factory-data-movement-activities.md).</span></span>
>
>

## <span data-ttu-id="08a89-123"><a name="prereqs"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="08a89-123"><a name="prereqs"></a>Prerequisites</span></span>
<span data-ttu-id="08a89-124">Este tutorial presume que você tenha:</span><span class="sxs-lookup"><span data-stu-id="08a89-124">This tutorial assumes you have:</span></span>

* <span data-ttu-id="08a89-125">Uma **assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="08a89-125">An **Azure subscription**.</span></span> <span data-ttu-id="08a89-126">Se você não tiver uma assinatura, você pode se inscrever em uma [avaliação gratuita](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="08a89-126">If you do not have a subscription, you can sign up for a [free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="08a89-127">Uma **conta de armazenamento do Azure**.</span><span class="sxs-lookup"><span data-stu-id="08a89-127">An **Azure storage account**.</span></span> <span data-ttu-id="08a89-128">Você usará uma conta de armazenamento do Azure para armazenar os dados neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="08a89-128">You will use an Azure storage account for storing the data in this tutorial.</span></span> <span data-ttu-id="08a89-129">Se você não tiver uma conta de armazenamento do Azure, consulte o artigo [Criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) .</span><span class="sxs-lookup"><span data-stu-id="08a89-129">If you don't have an Azure storage account, see the [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) article.</span></span> <span data-ttu-id="08a89-130">Depois de criar a conta de armazenamento, você precisará obter a chave de conta usada para acessar o armazenamento.</span><span class="sxs-lookup"><span data-stu-id="08a89-130">After you have created the storage account, you will need to obtain the account key used to access the storage.</span></span> <span data-ttu-id="08a89-131">Confira [Gerenciar as chaves de acesso de armazenamento](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span><span class="sxs-lookup"><span data-stu-id="08a89-131">See [Manage your storage access keys](../storage/common/storage-create-storage-account.md#manage-your-storage-access-keys).</span></span>
* <span data-ttu-id="08a89-132">**SQL Server em uma VM do Azure**provisionado.</span><span class="sxs-lookup"><span data-stu-id="08a89-132">Provisioned **SQL Server on an Azure VM**.</span></span> <span data-ttu-id="08a89-133">Para obter instruções, consulte [Configurar uma máquina virtual do SQL Server do Azure como um servidor do IPython Notebook para análises avançadas](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span><span class="sxs-lookup"><span data-stu-id="08a89-133">For instructions, see [Set up an Azure SQL Server virtual machine as an IPython Notebook server for advanced analytics](machine-learning-data-science-setup-sql-server-virtual-machine.md).</span></span>
* <span data-ttu-id="08a89-134">**Azure PowerShell** instalado e configurado localmente.</span><span class="sxs-lookup"><span data-stu-id="08a89-134">Installed and configured **Azure PowerShell** locally.</span></span> <span data-ttu-id="08a89-135">Para saber mais, confira [Como instalar e configurar o PowerShell do Azure](/powershell/azure/overview).</span><span class="sxs-lookup"><span data-stu-id="08a89-135">For instructions, see [How to install and configure Azure PowerShell](/powershell/azure/overview).</span></span>

## <span data-ttu-id="08a89-136"><a name="filesource_to_sqlonazurevm"></a> Movimentação de dados de uma fonte de arquivo simples para o SQL Server em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="08a89-136"><a name="filesource_to_sqlonazurevm"></a> Moving data from a flat file source to SQL Server on an Azure VM</span></span>
<span data-ttu-id="08a89-137">Se os dados estiverem em um arquivo simples (organizado em um formato de linha/coluna), ele pode ser movido para a VM do SQL Server no Azure pelos métodos a seguir:</span><span class="sxs-lookup"><span data-stu-id="08a89-137">If your data is in a flat file (arranged in a row/column format), it can be moved to SQL Server VM on Azure via the following methods:</span></span>

1. [<span data-ttu-id="08a89-138">Utilitário de BCP (cópia em massa de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="08a89-138">Command-line bulk copy utility (BCP)</span></span>](#insert-tables-bcp)
2. [<span data-ttu-id="08a89-139">Consulta SQL de inserção em massa </span><span class="sxs-lookup"><span data-stu-id="08a89-139">Bulk Insert SQL Query </span></span>](#insert-tables-bulkquery)
3. [<span data-ttu-id="08a89-140">Utilitários gráficos internos no SQL Server (Importar/Exportar, SSIS)</span><span class="sxs-lookup"><span data-stu-id="08a89-140">Graphical Built-in Utilities in SQL Server (Import/Export, SSIS)</span></span>](#sql-builtin-utilities)

### <span data-ttu-id="08a89-141"><a name="insert-tables-bcp"></a>Utilitário de BCP (cópia em massa de linha de comando)</span><span class="sxs-lookup"><span data-stu-id="08a89-141"><a name="insert-tables-bcp"></a>Command-line bulk copy utility (BCP)</span></span>
<span data-ttu-id="08a89-142">O BCP é um utilitário de linha de comando instalado com o SQL Server e é uma das maneiras mais rápidas de mover dados.</span><span class="sxs-lookup"><span data-stu-id="08a89-142">BCP is a command-line utility installed with SQL Server and is one of the quickest ways to move data.</span></span> <span data-ttu-id="08a89-143">Ele funciona em todas as três variantes do SQL Server (SQL Server local, SQL Azure e VM do SQL Server no Azure).</span><span class="sxs-lookup"><span data-stu-id="08a89-143">It works across all three SQL Server variants (On-premises SQL Server, SQL Azure and SQL Server VM on Azure).</span></span>

> [!NOTE]
> <span data-ttu-id="08a89-144">**Onde os dados devem estar para o BCP?**</span><span class="sxs-lookup"><span data-stu-id="08a89-144">**Where should my data be for BCP?**</span></span>  
> <span data-ttu-id="08a89-145">Embora não seja necessário, ter arquivos que contêm dados de origem localizados no mesmo computador que o SQL Server de destino possibilita transferências mais rápidas (velocidade de rede em comparação com velocidade de E/S do disco local).</span><span class="sxs-lookup"><span data-stu-id="08a89-145">While it is not required, having files containing source data located on the same machine as the target SQL Server allows for faster transfers (network speed vs local disk IO speed).</span></span> <span data-ttu-id="08a89-146">Você pode mover os arquivos simples que contêm dados para máquina em que o SQL Server está instalado usando várias ferramentas de cópia de arquivo, como [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) ou copiar/colar do Windows via protocolo RDP.</span><span class="sxs-lookup"><span data-stu-id="08a89-146">You can move the flat files containing data to the machine where SQL Server is installed using various file copying tools such as [AZCopy](../storage/common/storage-use-azcopy.md), [Azure Storage Explorer](http://storageexplorer.com/) or windows copy/paste via Remote Desktop Protocol (RDP).</span></span>
>
>

1. <span data-ttu-id="08a89-147">Certifique-se de que o banco de dados e as tabelas foram criados no banco de dados do SQL Server de destino.</span><span class="sxs-lookup"><span data-stu-id="08a89-147">Ensure that the database and the tables are created on the target SQL Server database.</span></span> <span data-ttu-id="08a89-148">Aqui está um exemplo de como fazer isso usando os comandos `Create Database` e `Create Table`:</span><span class="sxs-lookup"><span data-stu-id="08a89-148">Here is an example of how to do that using the `Create Database` and `Create Table` commands:</span></span>

        CREATE DATABASE <database_name>

        CREATE TABLE <tablename>
        (
            <columnname1> <datatype> <constraint>,
            <columnname2> <datatype> <constraint>,
            <columnname3> <datatype> <constraint>
        )
2. <span data-ttu-id="08a89-149">Gere o arquivo de formato que descreve o esquema da tabela emitindo o comando a seguir na linha de comando do computador em que o BCP está instalado.</span><span class="sxs-lookup"><span data-stu-id="08a89-149">Generate the format file that describes the schema for the table by issuing the following command from the command-line of the machine where bcp is installed.</span></span>

    `bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n`
3. <span data-ttu-id="08a89-150">Insira os dados no banco de dados usando o comando bcp da seguinte maneira.</span><span class="sxs-lookup"><span data-stu-id="08a89-150">Insert the data into the database using the bcp command as follows.</span></span> <span data-ttu-id="08a89-151">Isso deve funcionar na linha de comando, supondo que o SQL Server esteja instalado no mesmo computador:</span><span class="sxs-lookup"><span data-stu-id="08a89-151">This should work from the command-line assuming that the SQL Server is installed on same machine:</span></span>

    `bcp dbname..tablename in datafilename.tsv -f exportformatfilename.xml -S servername\sqlinstancename -U username -P password -b block_size_to_move_in_single_attemp -t \t -r \n`

> <span data-ttu-id="08a89-152">**Otimizando inserções de BCP** Consulte o artigo a seguir, ['Diretrizes para otimizar a importação de massa'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) , para otimizar essas inserções.</span><span class="sxs-lookup"><span data-stu-id="08a89-152">**Optimizing BCP Inserts** Please refer the following article ['Guidelines for Optimizing Bulk Import'](https://technet.microsoft.com/library/ms177445%28v=sql.105%29.aspx) to optimize such inserts.</span></span>
>
>

### <span data-ttu-id="08a89-153"><a name="insert-tables-bulkquery-parallel"></a>Paralelização de inserções para movimentação de dados mais rápida</span><span class="sxs-lookup"><span data-stu-id="08a89-153"><a name="insert-tables-bulkquery-parallel"></a>Parallelizing Inserts for Faster Data Movement</span></span>
<span data-ttu-id="08a89-154">Se os dados que você está movendo forem grandes, você pode acelerar as coisas executando simultaneamente vários comandos BCP em paralelo em um Script do PowerShell.</span><span class="sxs-lookup"><span data-stu-id="08a89-154">If the data you are moving is large, you can speed things up by simultaneously executing multiple BCP commands in parallel in a PowerShell Script.</span></span>

> [!NOTE]
> <span data-ttu-id="08a89-155">**Ingestão de big data** Para otimizar o carregamento de dados para conjuntos de dados grandes e muito grandes, particione suas tabelas de banco de dados lógicas e físicas usando várias tabelas de partição e grupos de arquivos.</span><span class="sxs-lookup"><span data-stu-id="08a89-155">**Big data Ingestion** To optimize data loading for large and very large datasets, partition your logical and physical database tables using multiple filegroups and partition tables.</span></span> <span data-ttu-id="08a89-156">Para obter mais informações sobre como criar e carregar dados em tabelas de partição, consulte [Tabelas de partição do SQL de carga paralela](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span><span class="sxs-lookup"><span data-stu-id="08a89-156">For more information about creating and loading data to partition tables, see [Parallel Load SQL Partition Tables](machine-learning-data-science-parallel-load-sql-partitioned-tables.md).</span></span>
>
>

<span data-ttu-id="08a89-157">O script do PowerShell de exemplo abaixo demonstra inserções paralelas usando BCP:</span><span class="sxs-lookup"><span data-stu-id="08a89-157">The sample PowerShell script below demonstrate parallel inserts using bcp:</span></span>

    $NO_OF_PARALLEL_JOBS=2

     Set-ExecutionPolicy RemoteSigned #set execution policy for the script to execute
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


    # Wait for it all to complete
    While (Get-Job -State "Running")
    {
      Start-Sleep 10
      Get-Job
    }

    # Getting the information back from the jobs
    Get-Job | Receive-Job
    Set-ExecutionPolicy Restricted #reset the execution policy


### <span data-ttu-id="08a89-158"><a name="insert-tables-bulkquery"></a>Consulta SQL de inserção em massa</span><span class="sxs-lookup"><span data-stu-id="08a89-158"><a name="insert-tables-bulkquery"></a>Bulk Insert SQL Query</span></span>
<span data-ttu-id="08a89-159">A [Consulta SQL de inserção em massa](https://msdn.microsoft.com/library/ms188365) pode ser usada para importar dados para o banco de dados de arquivos com base em linha/coluna - os tipos com suporte são abordados no tópico [Preparar dados para exportação ou importação em massa (SQL Server)](https://msdn.microsoft.com/library/ms188609).</span><span class="sxs-lookup"><span data-stu-id="08a89-159">[Bulk Insert SQL Query](https://msdn.microsoft.com/library/ms188365) can be used to import data into the database from row/column based files (the supported types are covered in the[Prepare Data for Bulk Export or Import (SQL Server)](https://msdn.microsoft.com/library/ms188609)) topic.</span></span>

<span data-ttu-id="08a89-160">Aqui estão alguns comandos de exemplo para inserção em massa:</span><span class="sxs-lookup"><span data-stu-id="08a89-160">Here are some sample commands for Bulk Insert are as below:</span></span>  

1. <span data-ttu-id="08a89-161">Analise seus dados e defina as opções personalizadas antes da importação para certificar-se de que o banco de dados do SQL Server entende o mesmo formato para campos especiais, tal como datas.</span><span class="sxs-lookup"><span data-stu-id="08a89-161">Analyze your data and set any custom options before importing to make sure that the SQL Server database assumes the same format for any special fields such as dates.</span></span> <span data-ttu-id="08a89-162">Aqui está um exemplo de como definir o formato de data como ano-mês-dia (se seus dados contiverem a data no formato de ano-mês-dia):</span><span class="sxs-lookup"><span data-stu-id="08a89-162">Here is an example of how to set the date format as year-month-day (if your data contains the date in year-month-day format):</span></span>

        SET DATEFORMAT ymd;    
2. <span data-ttu-id="08a89-163">Importe dados usando as instruções de importação em massa:</span><span class="sxs-lookup"><span data-stu-id="08a89-163">Import data using bulk import statements:</span></span>

        BULK INSERT <tablename>
        FROM    
        '<datafilename>'
        WITH
        (
        FirstRow=2,
        FIELDTERMINATOR =',', --this should be column separator in your data
        ROWTERMINATOR ='\n'   --this should be the row separator in your data
        )

### <span data-ttu-id="08a89-164"><a name="sql-builtin-utilities"></a>Utilitários internos no SQL Server</span><span class="sxs-lookup"><span data-stu-id="08a89-164"><a name="sql-builtin-utilities"></a>Built-in Utilities in SQL Server</span></span>
<span data-ttu-id="08a89-165">Você pode usar o SSIS (Serviços de Integrações do SQL Server) para importar dados para a VM do SQL Server no Azure por meio de um arquivo simples.</span><span class="sxs-lookup"><span data-stu-id="08a89-165">You can use SQL Server Integrations Services (SSIS) to import data into SQL Server VM on Azure from a flat file.</span></span>
<span data-ttu-id="08a89-166">O SSIS está disponível em dois ambientes de estúdio.</span><span class="sxs-lookup"><span data-stu-id="08a89-166">SSIS is available in two studio environments.</span></span> <span data-ttu-id="08a89-167">Para obter detalhes, consulte [Ambientes do Integration Services (SSIS) e Estúdio](https://technet.microsoft.com/library/ms140028.aspx):</span><span class="sxs-lookup"><span data-stu-id="08a89-167">For details, see [Integration Services (SSIS) and Studio Environments](https://technet.microsoft.com/library/ms140028.aspx):</span></span>

* <span data-ttu-id="08a89-168">Para obter detalhes sobre SQL Server Data Tools, consulte [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span><span class="sxs-lookup"><span data-stu-id="08a89-168">For details on SQL Server Data Tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/tools.aspx)</span></span>  
* <span data-ttu-id="08a89-169">Para obter detalhes sobre o Assistente de Importação/Exportação, consulte [Assistente de Importação/Exportação do SQL Server](https://msdn.microsoft.com/library/ms141209.aspx)</span><span class="sxs-lookup"><span data-stu-id="08a89-169">For details on the Import/Export Wizard, see [SQL Server Import and Export Wizard](https://msdn.microsoft.com/library/ms141209.aspx)</span></span>

## <span data-ttu-id="08a89-170"><a name="sqlonprem_to_sqlonazurevm"></a>Movimentação de dados do servidor SQL local para o SQL Server em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="08a89-170"><a name="sqlonprem_to_sqlonazurevm"></a>Moving Data from on-premises SQL Server to SQL Server on an Azure VM</span></span>
<span data-ttu-id="08a89-171">Você também pode usar as seguintes estratégias de migração:</span><span class="sxs-lookup"><span data-stu-id="08a89-171">You can also use the following migration strategies:</span></span>

1. [<span data-ttu-id="08a89-172">Assistente para implantar um Banco de Dados do SQL Server em uma VM do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="08a89-172">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>](#deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard)
2. [<span data-ttu-id="08a89-173">Exportar para arquivo simples</span><span class="sxs-lookup"><span data-stu-id="08a89-173">Export to Flat File</span></span>](#export-flat-file)
3. [<span data-ttu-id="08a89-174">Assistente de Migração de Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="08a89-174">SQL Database Migration Wizard</span></span>](#sql-migration)
4. [<span data-ttu-id="08a89-175">Backup e restauração de banco de dados</span><span class="sxs-lookup"><span data-stu-id="08a89-175">Database back up and restore</span></span>](#sql-backup)

<span data-ttu-id="08a89-176">Descrevemos cada um deles abaixo:</span><span class="sxs-lookup"><span data-stu-id="08a89-176">We describe each of these below:</span></span>

### <a name="deploy-a-sql-server-database-to-a-microsoft-azure-vm-wizard"></a><span data-ttu-id="08a89-177">Assistente para implantar um Banco de Dados do SQL Server em uma VM do Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="08a89-177">Deploy a SQL Server Database to a Microsoft Azure VM wizard</span></span>
<span data-ttu-id="08a89-178">O **Assistente para implantar um banco de dados do SQL Server em uma Máquina Virtual do Microsoft Azure** é uma maneira simples e recomendada de mover dados de uma instância do SQL Server local para o SQL Server em uma Máquina Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="08a89-178">The **Deploy a SQL Server Database to a Microsoft Azure VM wizard** is a simple and recommended way to move data from an on-premises SQL Server instance to SQL Server on an Azure VM.</span></span> <span data-ttu-id="08a89-179">Para obter etapas detalhadas, bem como uma discussão sobre outras alternativas, confira [Migrar um banco de dados para o SQL Server em uma Máquina Virtual do Azure](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span><span class="sxs-lookup"><span data-stu-id="08a89-179">For detailed steps as well as a discussion of other alternatives, see [Migrate a database to SQL Server on an Azure VM](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md).</span></span>

### <span data-ttu-id="08a89-180"><a name="export-flat-file"></a>Exportar para arquivo simples</span><span class="sxs-lookup"><span data-stu-id="08a89-180"><a name="export-flat-file"></a>Export to Flat File</span></span>
<span data-ttu-id="08a89-181">Vários métodos podem ser usados para exportar dados em massa de um SQL Server local, conforme documentado no tópico [Importação e importação de dados em massa (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) .</span><span class="sxs-lookup"><span data-stu-id="08a89-181">Various methods can be used to bulk export data from an On-Premises SQL Server as documented in the [Bulk Import and Export of Data (SQL Server)](https://msdn.microsoft.com/library/ms175937.aspx) topic.</span></span> <span data-ttu-id="08a89-182">Este documento abordará o BCP (Programa de Cópia em Massa) como um exemplo.</span><span class="sxs-lookup"><span data-stu-id="08a89-182">This document will cover the Bulk Copy Program (BCP) as an example.</span></span> <span data-ttu-id="08a89-183">Depois que os dados são exportados para um arquivo simples, ele pode ser importado para outro SQL Server usando a importação em massa.</span><span class="sxs-lookup"><span data-stu-id="08a89-183">Once data is exported into a flat file, it can be imported to another SQL server using bulk import.</span></span>

1. <span data-ttu-id="08a89-184">Exporte os dados do SQL Server local para um arquivo usando o utilitário bcp da seguinte maneira</span><span class="sxs-lookup"><span data-stu-id="08a89-184">Export the data from on-premises SQL Server to a File using the bcp utility as follows</span></span>

    `bcp dbname..tablename out datafile.tsv -S    servername\sqlinstancename -T -t \t -t \n -c`
2. <span data-ttu-id="08a89-185">Crie o banco de dados e a tabela na VM do SQL Server no Azure usando `create database` e `create table` para o esquema de tabela exportado na etapa 1.</span><span class="sxs-lookup"><span data-stu-id="08a89-185">Create the database and the table on SQL Server VM on Azure using the `create database` and `create table` for the table schema exported in step 1.</span></span>
3. <span data-ttu-id="08a89-186">Crie um arquivo de formato para descrever o esquema da tabela de dados que está sendo importado/exportado.</span><span class="sxs-lookup"><span data-stu-id="08a89-186">Create a format file for describing the table schema of the data being exported/imported.</span></span> <span data-ttu-id="08a89-187">Os detalhes do formato de arquivo são descritos em [Criar um arquivo de formato (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span><span class="sxs-lookup"><span data-stu-id="08a89-187">Details of the format file are described in [Create a Format File (SQL Server)](https://msdn.microsoft.com/library/ms191516.aspx).</span></span>

    <span data-ttu-id="08a89-188">Geração de arquivo de formato ao executar o BCP no computador do SQL Server</span><span class="sxs-lookup"><span data-stu-id="08a89-188">Format file generation when running BCP from the SQL Server machine</span></span>

        bcp dbname..tablename format nul -c -x -f exportformatfilename.xml -S servername\sqlinstance -T -t \t -r \n

    <span data-ttu-id="08a89-189">Geração de arquivo de formato ao executar o BCP remotamente em um SQL Server</span><span class="sxs-lookup"><span data-stu-id="08a89-189">Format file generation when running BCP remotely against a SQL Server</span></span>

        bcp dbname..tablename format nul -c -x -f  exportformatfilename.xml  -U username@servername.database.windows.net -S tcp:servername -P password  --t \t -r \n
4. <span data-ttu-id="08a89-190">Use qualquer um dos métodos descritos na seção [Movendo dados da origem do arquivo](#filesource_to_sqlonazurevm) para mover os dados em arquivos simples para o SQL Server.</span><span class="sxs-lookup"><span data-stu-id="08a89-190">Use any of the methods described in section [Moving Data from File Source](#filesource_to_sqlonazurevm) to move the data in flat files to a SQL Server.</span></span>

### <span data-ttu-id="08a89-191"><a name="sql-migration"></a>Assistente de Migração de Banco de Dados SQL</span><span class="sxs-lookup"><span data-stu-id="08a89-191"><a name="sql-migration"></a>SQL Database Migration Wizard</span></span>
<span data-ttu-id="08a89-192">[Assistente de Migração de Banco de Dados do SQL Server](http://sqlazuremw.codeplex.com/) fornece uma maneira amigável de mover dados entre duas instâncias do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="08a89-192">[SQL Server Database Migration Wizard](http://sqlazuremw.codeplex.com/) provides a user-friendly way to move data between two SQL server instances.</span></span> <span data-ttu-id="08a89-193">Ele permite que o usuário mapeie o esquema de dados entre as tabelas de origem e destino, escolha os tipos de coluna e vários outros recursos.</span><span class="sxs-lookup"><span data-stu-id="08a89-193">It allows the user to map the data schema between sources and destination tables, choose column types and various other functionalities.</span></span> <span data-ttu-id="08a89-194">Ele usa BCP (cópia em massa) nos bastidores.</span><span class="sxs-lookup"><span data-stu-id="08a89-194">It uses bulk copy (BCP) under the covers.</span></span> <span data-ttu-id="08a89-195">Abaixo está uma captura de tela da tela de boas-vindas para o Assistente de Migração de Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="08a89-195">A screenshot of the welcome screen for the SQL Database Migration wizard is shown below.</span></span>  

![Assistente de Migração do SQL Server][2]

### <span data-ttu-id="08a89-197"><a name="sql-backup"></a>Backup e restauração de banco de dados</span><span class="sxs-lookup"><span data-stu-id="08a89-197"><a name="sql-backup"></a>Database back up and restore</span></span>
<span data-ttu-id="08a89-198">O SQL Server dá suporte a:</span><span class="sxs-lookup"><span data-stu-id="08a89-198">SQL Server supports:</span></span>

1. <span data-ttu-id="08a89-199">[Funcionalidade de backup e restauração de banco de dados](https://msdn.microsoft.com/library/ms187048.aspx) (para um arquivo local ou exportação de bacpac para blob) e [Aplicativos de Camada de Dados](https://msdn.microsoft.com/library/ee210546.aspx) (usando bacpac).</span><span class="sxs-lookup"><span data-stu-id="08a89-199">[Database back up and restore functionality](https://msdn.microsoft.com/library/ms187048.aspx) (both to a local file or bacpac export to blob) and [Data Tier Applications](https://msdn.microsoft.com/library/ee210546.aspx) (using bacpac).</span></span>
2. <span data-ttu-id="08a89-200">Capacidade de criar VMs do SQL Server diretamente no Azure com um banco de dados copiado ou copiar um banco de dados do SQL do Azure existente.</span><span class="sxs-lookup"><span data-stu-id="08a89-200">Ability to directly create SQL Server VMs on Azure with a copied database or copy to an existing SQL Azure database.</span></span> <span data-ttu-id="08a89-201">Para obter mais detalhes, consulte [Usar o Assistente para Cópia de Banco de Dados](https://msdn.microsoft.com/library/ms188664.aspx).</span><span class="sxs-lookup"><span data-stu-id="08a89-201">For more details, see [Use the Copy Database Wizard](https://msdn.microsoft.com/library/ms188664.aspx).</span></span>

<span data-ttu-id="08a89-202">Abaixo está uma captura de tela das opções de backup/restauração de banco de dados do SQL Server Management Studio.</span><span class="sxs-lookup"><span data-stu-id="08a89-202">A screenshot of the Database back up/restore options from SQL Server Management Studio is shown below.</span></span>

![Ferramenta de Importação do SQL Server][1]

## <a name="resources"></a><span data-ttu-id="08a89-204">Recursos</span><span class="sxs-lookup"><span data-stu-id="08a89-204">Resources</span></span>
[<span data-ttu-id="08a89-205">Migrar um banco de dados para o SQL Server em uma VM do Azure</span><span class="sxs-lookup"><span data-stu-id="08a89-205">Migrate a Database to SQL Server on an Azure VM</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-migrate-sql.md)

[<span data-ttu-id="08a89-206">Visão geral do SQL Server em máquinas virtuais do Azure</span><span class="sxs-lookup"><span data-stu-id="08a89-206">SQL Server on Azure Virtual Machines overview</span></span>](../virtual-machines/windows/sql/virtual-machines-windows-sql-server-iaas-overview.md)

[1]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/sqlserver_builtin_utilities.png
[2]: ./media/machine-learning-data-science-move-sql-server-virtual-machine/database_migration_wizard.png
