---
title: Copiar dados entre o Data Lake Store e o banco de dados SQL do Azure usando o Sqoop | Microsoft Docs
description: "Usar o Sqoop para copiar dados entre o Banco de Dados SQL do Azure e o Repositório Data Lake"
services: data-lake-store
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
ms.assetid: 3f914b2a-83cc-4950-b3f7-69c921851683
ms.service: data-lake-store
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/29/2017
ms.author: nitinme
ms.openlocfilehash: 53bf33f6027f1f365bd92251490d5c851fb83f8b
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="f7da3-103">Copiar dados entre o Repositório Data Lake e o banco de dados SQL do Azure usando o Sqoop</span><span class="sxs-lookup"><span data-stu-id="f7da3-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="f7da3-104">Saiba como usar o Apache Sqoop para importar e exportar dados entre o Banco de Dados SQL do Azure e o Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f7da3-104">Learn how to use Apache Sqoop to import and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="f7da3-105">O que é o Sqoop?</span><span class="sxs-lookup"><span data-stu-id="f7da3-105">What is Sqoop?</span></span>
<span data-ttu-id="f7da3-106">Os aplicativos de big data são uma opção natural para o processamento de dados semi-estruturados e não estruturados, como logs e arquivos.</span><span class="sxs-lookup"><span data-stu-id="f7da3-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="f7da3-107">No entanto, também pode ser necessário processar dados estruturados armazenados em bancos de dados relacionais.</span><span class="sxs-lookup"><span data-stu-id="f7da3-107">However, there may also be a need to process structured data that is stored in relational databases.</span></span>

<span data-ttu-id="f7da3-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) é uma ferramenta desenvolvida para transferir dados entre bancos de dados relacionais e um repositório de Big Data, como o Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="f7da3-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed to transfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="f7da3-109">Você pode usá-lo para importar dados de um RDBMS (sistema de gerenciamento de banco de dados relacionais), como o Banco de Dados SQL do Azure no Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f7da3-109">You can use it to import data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="f7da3-110">E, em seguida, transformar e analisar os dados usando cargas de trabalho de big data e exportar os dados de volta para um RDBMS.</span><span class="sxs-lookup"><span data-stu-id="f7da3-110">You can then transform and analyze the data using big data workloads and then export the data back into an RDBMS.</span></span> <span data-ttu-id="f7da3-111">Neste tutorial, você usa um Banco de Dados SQL do Azure como seu banco de dados relacional para importação/exportação.</span><span class="sxs-lookup"><span data-stu-id="f7da3-111">In this tutorial, you use an Azure SQL Database as your relational database to import/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f7da3-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="f7da3-112">Prerequisites</span></span>
<span data-ttu-id="f7da3-113">Antes de começar este artigo, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="f7da3-113">Before you begin this article, you must have the following:</span></span>

* <span data-ttu-id="f7da3-114">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f7da3-114">**An Azure subscription**.</span></span> <span data-ttu-id="f7da3-115">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="f7da3-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="f7da3-116">**Uma conta do repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="f7da3-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="f7da3-117">Para obter instruções sobre como criar uma, consulte [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="f7da3-117">For instructions on how to create one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="f7da3-118">**Cluster HDInsight do Azure** com acesso a uma conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f7da3-118">**Azure HDInsight cluster** with access to a Data Lake Store account.</span></span> <span data-ttu-id="f7da3-119">Confira [Criar um cluster HDInsight com o Repositório Data Lake](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="f7da3-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="f7da3-120">Este artigo pressupõe que você tenha um cluster HDInsight Linux com acesso ao Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f7da3-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="f7da3-121">**Banco de dados SQL do Azure**.</span><span class="sxs-lookup"><span data-stu-id="f7da3-121">**Azure SQL Database**.</span></span> <span data-ttu-id="f7da3-122">Para saber mais sobre como criar um, confira [Criar um banco de dados SQL do Azure](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="f7da3-122">For instructions on how to create one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="f7da3-123">Você aprende rapidamente com vídeos?</span><span class="sxs-lookup"><span data-stu-id="f7da3-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="f7da3-124">[Assista a este vídeo](https://mix.office.com/watch/1butcdjxmu114) sobre como copiar dados entre o Repositório do Data Lake e os Blobs de Armazenamento do Azure usando o DistCp.</span><span class="sxs-lookup"><span data-stu-id="f7da3-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how to copy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-the-azure-sql-database"></a><span data-ttu-id="f7da3-125">Criar tabelas de exemplo no Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="f7da3-125">Create sample tables in the Azure SQL Database</span></span>
1. <span data-ttu-id="f7da3-126">Para começar, crie duas tabelas de exemplo no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7da3-126">To start with, create two sample tables in the Azure SQL Database.</span></span> <span data-ttu-id="f7da3-127">Use o [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou o Visual Studio para se conectar ao Banco de Dados SQL do Azure e então execute as consultas a seguir.</span><span class="sxs-lookup"><span data-stu-id="f7da3-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following queries.</span></span>

    <span data-ttu-id="f7da3-128">**Criar Tabela1**</span><span class="sxs-lookup"><span data-stu-id="f7da3-128">**Create Table1**</span></span>

        CREATE TABLE [dbo].[Table1](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO

    <span data-ttu-id="f7da3-129">**Criar Tabela2**</span><span class="sxs-lookup"><span data-stu-id="f7da3-129">**Create Table2**</span></span>

        CREATE TABLE [dbo].[Table2](
        [ID] [int] NOT NULL,
        [FName] [nvarchar](50) NOT NULL,
        [LName] [nvarchar](50) NOT NULL,
         CONSTRAINT [PK_Table_4] PRIMARY KEY CLUSTERED
            (
                   [ID] ASC
            )
        ) ON [PRIMARY]
        GO
2. <span data-ttu-id="f7da3-130">Na **Tabela1**, adicione alguns dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="f7da3-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="f7da3-131">Deixe a **Tabela2** vazia.</span><span class="sxs-lookup"><span data-stu-id="f7da3-131">Leave **Table2** empty.</span></span> <span data-ttu-id="f7da3-132">Importaremos dados da **Tabela1** para o Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f7da3-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="f7da3-133">Em seguida, exportaremos dados do Repositório Data Lake Store para a **Tabela2**.</span><span class="sxs-lookup"><span data-stu-id="f7da3-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="f7da3-134">Execute o trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="f7da3-134">Run the following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-to-data-lake-store"></a><span data-ttu-id="f7da3-135">Usar o Sqoop de um cluster HDInsight com acesso ao Repositório Azure Data Lake</span><span class="sxs-lookup"><span data-stu-id="f7da3-135">Use Sqoop from an HDInsight cluster with access to Data Lake Store</span></span>
<span data-ttu-id="f7da3-136">Um cluster HDInsight já tem os pacotes Sqoop disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f7da3-136">An HDInsight cluster already has the Sqoop packages available.</span></span> <span data-ttu-id="f7da3-137">Se você tiver configurado o cluster HDInsight para usar o Repositório Data Lake como armazenamento adicional, poderá usar o Sqoop (sem alterações de configuração) para importar/exportar dados entre um banco de dados relacional (neste exemplo, o Banco de Dados SQL do Azure) e uma conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f7da3-137">If you have configured the HDInsight cluster to use Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) to import/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="f7da3-138">Para este tutorial, vamos supor que você tenha criado um cluster Linux para poder usar o SSH para se conectar ao cluster.</span><span class="sxs-lookup"><span data-stu-id="f7da3-138">For this tutorial, we assume you created a Linux cluster so you should use SSH to connect to the cluster.</span></span> <span data-ttu-id="f7da3-139">Confira [Conectar-se a um cluster HDInsight baseado em Linux](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="f7da3-139">See [Connect to a Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="f7da3-140">Verifique se você pode acessar a conta do Repositório Data Lake do cluster.</span><span class="sxs-lookup"><span data-stu-id="f7da3-140">Verify whether you can access the Data Lake Store account from the cluster.</span></span> <span data-ttu-id="f7da3-141">Execute o comando a seguir do prompt do SSH:</span><span class="sxs-lookup"><span data-stu-id="f7da3-141">Run the following command from the SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="f7da3-142">Isso deve fornecer uma lista de arquivos/pastas na conta de Repositório do Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f7da3-142">This should provide a list of files/folders in the Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="f7da3-143">Importar dados do Banco de Dados SQL do Azure para o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="f7da3-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="f7da3-144">Navegue até o diretório onde os pacotes do Sqoop estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="f7da3-144">Navigate to the directory where Sqoop packages are available.</span></span> <span data-ttu-id="f7da3-145">Normalmente, será `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="f7da3-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="f7da3-146">Importe os dados da **Tabela1** para a conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f7da3-146">Import the data from **Table1** into the Data Lake Store account.</span></span> <span data-ttu-id="f7da3-147">Use a seguinte sintaxe:</span><span class="sxs-lookup"><span data-stu-id="f7da3-147">Use the following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="f7da3-148">Observe que o espaço reservado **sql-database-server-name** representa o nome do servidor onde o banco de dados SQL do Azure está em execução.</span><span class="sxs-lookup"><span data-stu-id="f7da3-148">Note that **sql-database-server-name** placeholder represents the name of the server where the Azure SQL database is running.</span></span> <span data-ttu-id="f7da3-149">**sql-database-name** representa o nome do banco de dados real.</span><span class="sxs-lookup"><span data-stu-id="f7da3-149">**sql-database-name** placeholder represents the actual database name.</span></span>

    <span data-ttu-id="f7da3-150">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f7da3-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="f7da3-151">Verifique se os dados foram transferidos para a conta do Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="f7da3-151">Verify that the data has been transferred to the Data Lake Store account.</span></span> <span data-ttu-id="f7da3-152">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="f7da3-152">Run the following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="f7da3-153">Você deve ver a saída a seguir.</span><span class="sxs-lookup"><span data-stu-id="f7da3-153">You should see the following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="f7da3-154">Cada arquivo **part-m-** corresponde a uma linha na tabela de origem, **Table1**.</span><span class="sxs-lookup"><span data-stu-id="f7da3-154">Each **part-m-*** file corresponds to a row in the source table, **Table1**.</span></span> <span data-ttu-id="f7da3-155">Você pode exibir o conteúdo dos arquivos part-m-* para verificação.</span><span class="sxs-lookup"><span data-stu-id="f7da3-155">You can view the contents of the part-m-* files to verify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="f7da3-156">Exportar dados do Repositório Data Lake para o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="f7da3-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="f7da3-157">Exporte os dados da conta do Data Lake Store para a tabela vazia, a **Tabela2**, no Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="f7da3-157">Export the data from Data Lake Store account to the empty table, **Table2**, in the Azure SQL Database.</span></span> <span data-ttu-id="f7da3-158">Use a sintaxe a seguir.</span><span class="sxs-lookup"><span data-stu-id="f7da3-158">Use the following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="f7da3-159">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="f7da3-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="f7da3-160">Verifique se os dados foram carregados na tabela do Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="f7da3-160">Verify that the data was uploaded to the SQL Database table.</span></span> <span data-ttu-id="f7da3-161">Use o [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou o Visual Studio para se conectar ao Banco de Dados SQL Azure e então execute a consulta a seguir.</span><span class="sxs-lookup"><span data-stu-id="f7da3-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio to connect to the Azure SQL Database and then run the following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="f7da3-162">Isso deverá ter a saída a seguir.</span><span class="sxs-lookup"><span data-stu-id="f7da3-162">This should have the following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="f7da3-163">Considerações de desempenho ao usar o Sqoop</span><span class="sxs-lookup"><span data-stu-id="f7da3-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="f7da3-164">Para ajustar o desempenho do seu trabalho do Sqoop para copiar dados para o Data Lake Store, consulte [Documento de desempenho do Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="f7da3-164">For performance tuning your Sqoop job to copy data to Data Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="f7da3-165">Consulte também</span><span class="sxs-lookup"><span data-stu-id="f7da3-165">See also</span></span>
* [<span data-ttu-id="f7da3-166">Copiar dados de Blobs do Armazenamento do Azure para o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="f7da3-166">Copy data from Azure Storage Blobs to Data Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="f7da3-167">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="f7da3-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="f7da3-168">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="f7da3-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="f7da3-169">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="f7da3-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
