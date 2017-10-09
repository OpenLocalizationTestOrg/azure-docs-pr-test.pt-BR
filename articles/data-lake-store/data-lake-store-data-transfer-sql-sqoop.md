---
title: "dados de aaaCopy entre repositório Data Lake e banco de dados do SQL Azure usando o Sqoop | Microsoft Docs"
description: "Usar Sqoop toocopy dados entre o banco de dados do SQL Azure e o repositório Data Lake"
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
ms.openlocfilehash: f58483455f0ebe9544673a1d5c5884f2721c800c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="copy-data-between-data-lake-store-and-azure-sql-database-using-sqoop"></a><span data-ttu-id="29db5-103">Copiar dados entre o Repositório Data Lake e o banco de dados SQL do Azure usando o Sqoop</span><span class="sxs-lookup"><span data-stu-id="29db5-103">Copy data between Data Lake Store and Azure SQL database using Sqoop</span></span>
<span data-ttu-id="29db5-104">Saiba como toouse Apache Sqoop tooimport e exportação de dados entre o banco de dados do SQL Azure e o repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="29db5-104">Learn how toouse Apache Sqoop tooimport and export data between Azure SQL Database and Data Lake Store.</span></span>

## <a name="what-is-sqoop"></a><span data-ttu-id="29db5-105">O que é o Sqoop?</span><span class="sxs-lookup"><span data-stu-id="29db5-105">What is Sqoop?</span></span>
<span data-ttu-id="29db5-106">Os aplicativos de big data são uma opção natural para o processamento de dados semi-estruturados e não estruturados, como logs e arquivos.</span><span class="sxs-lookup"><span data-stu-id="29db5-106">Big data applications are a natural choice for processing unstructured and semi-structured data, such as logs and files.</span></span> <span data-ttu-id="29db5-107">No entanto, também pode haver uma necessidade de dados tooprocess estruturados armazenados em bancos de dados relacionais.</span><span class="sxs-lookup"><span data-stu-id="29db5-107">However, there may also be a need tooprocess structured data that is stored in relational databases.</span></span>

<span data-ttu-id="29db5-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) é uma ferramenta desenvolvida tootransfer dados entre bancos de dados relacionais e um repositório de dados grande, como repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="29db5-108">[Apache Sqoop](https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html) is a tool designed tootransfer data between  relational databases and a big data repository, such as Data Lake Store.</span></span> <span data-ttu-id="29db5-109">Você pode usá-lo tooimport dados de um sistema de gerenciamento de banco de dados relacional (RDBMS), como o banco de dados do SQL Azure no repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="29db5-109">You can use it tooimport data from a relational database management system (RDBMS) such as Azure SQL Database into Data Lake Store.</span></span> <span data-ttu-id="29db5-110">Você pode, em seguida, transformar e analisar dados hello usando dados de grandes cargas de trabalho e, em seguida, exportar dados de saudação volta para um RDBMS.</span><span class="sxs-lookup"><span data-stu-id="29db5-110">You can then transform and analyze hello data using big data workloads and then export hello data back into an RDBMS.</span></span> <span data-ttu-id="29db5-111">Neste tutorial, você pode usar um banco de dados do SQL Azure como seu banco de dados relacional tooimport/exportação do.</span><span class="sxs-lookup"><span data-stu-id="29db5-111">In this tutorial, you use an Azure SQL Database as your relational database tooimport/export from.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="29db5-112">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="29db5-112">Prerequisites</span></span>
<span data-ttu-id="29db5-113">Antes de começar este artigo, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="29db5-113">Before you begin this article, you must have hello following:</span></span>

* <span data-ttu-id="29db5-114">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="29db5-114">**An Azure subscription**.</span></span> <span data-ttu-id="29db5-115">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/pricing/free-trial/).</span><span class="sxs-lookup"><span data-stu-id="29db5-115">See [Get Azure free trial](https://azure.microsoft.com/pricing/free-trial/).</span></span>
* <span data-ttu-id="29db5-116">**Uma conta do repositório Azure Data Lake**.</span><span class="sxs-lookup"><span data-stu-id="29db5-116">**An Azure Data Lake Store account**.</span></span> <span data-ttu-id="29db5-117">Para obter instruções sobre como um, ver toocreate [Introdução ao repositório Azure Data Lake](data-lake-store-get-started-portal.md)</span><span class="sxs-lookup"><span data-stu-id="29db5-117">For instructions on how toocreate one, see [Get started with Azure Data Lake Store](data-lake-store-get-started-portal.md)</span></span>
* <span data-ttu-id="29db5-118">**Cluster de HDInsight do Azure** com acesso tooa conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="29db5-118">**Azure HDInsight cluster** with access tooa Data Lake Store account.</span></span> <span data-ttu-id="29db5-119">Confira [Criar um cluster HDInsight com o Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span><span class="sxs-lookup"><span data-stu-id="29db5-119">See [Create an HDInsight cluster with Data Lake Store](data-lake-store-hdinsight-hadoop-use-portal.md).</span></span> <span data-ttu-id="29db5-120">Este artigo pressupõe que você tenha um cluster HDInsight Linux com acesso ao Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="29db5-120">This article assumes you have an HDInsight Linux cluster with Data Lake Store access.</span></span>
* <span data-ttu-id="29db5-121">**Banco de dados SQL do Azure**.</span><span class="sxs-lookup"><span data-stu-id="29db5-121">**Azure SQL Database**.</span></span> <span data-ttu-id="29db5-122">Para obter instruções sobre como um, ver toocreate [criar um banco de dados do SQL Azure](../sql-database/sql-database-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="29db5-122">For instructions on how toocreate one, see [Create an Azure SQL database](../sql-database/sql-database-get-started.md)</span></span>

## <a name="do-you-learn-fast-with-videos"></a><span data-ttu-id="29db5-123">Você aprende rapidamente com vídeos?</span><span class="sxs-lookup"><span data-stu-id="29db5-123">Do you learn fast with videos?</span></span>
<span data-ttu-id="29db5-124">[Assista a este vídeo](https://mix.office.com/watch/1butcdjxmu114) sobre como os dados de toocopy entre Blobs de armazenamento do Azure e o repositório Data Lake usando DistCp.</span><span class="sxs-lookup"><span data-stu-id="29db5-124">[Watch this video](https://mix.office.com/watch/1butcdjxmu114) on how toocopy data between Azure Storage Blobs and Data Lake Store using DistCp.</span></span>

## <a name="create-sample-tables-in-hello-azure-sql-database"></a><span data-ttu-id="29db5-125">Criar tabelas de exemplo no hello Azure SQL Database</span><span class="sxs-lookup"><span data-stu-id="29db5-125">Create sample tables in hello Azure SQL Database</span></span>
1. <span data-ttu-id="29db5-126">toostart, crie duas tabelas de exemplo no hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="29db5-126">toostart with, create two sample tables in hello Azure SQL Database.</span></span> <span data-ttu-id="29db5-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio tooconnect toohello banco de dados do SQL Azure e, em seguida, execute Olá seguindo consultas.</span><span class="sxs-lookup"><span data-stu-id="29db5-127">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following queries.</span></span>

    <span data-ttu-id="29db5-128">**Criar Tabela1**</span><span class="sxs-lookup"><span data-stu-id="29db5-128">**Create Table1**</span></span>

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

    <span data-ttu-id="29db5-129">**Criar Tabela2**</span><span class="sxs-lookup"><span data-stu-id="29db5-129">**Create Table2**</span></span>

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
2. <span data-ttu-id="29db5-130">Na **Tabela1**, adicione alguns dados de exemplo.</span><span class="sxs-lookup"><span data-stu-id="29db5-130">In **Table1**, add some sample data.</span></span> <span data-ttu-id="29db5-131">Deixe a **Tabela2** vazia.</span><span class="sxs-lookup"><span data-stu-id="29db5-131">Leave **Table2** empty.</span></span> <span data-ttu-id="29db5-132">Importaremos dados da **Tabela1** para o Repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="29db5-132">We will import data from **Table1** into Data Lake Store.</span></span> <span data-ttu-id="29db5-133">Em seguida, exportaremos dados do Repositório Data Lake Store para a **Tabela2**.</span><span class="sxs-lookup"><span data-stu-id="29db5-133">Then, we will export data from Data Lake Store into **Table2**.</span></span> <span data-ttu-id="29db5-134">Execute Olá trecho de código a seguir.</span><span class="sxs-lookup"><span data-stu-id="29db5-134">Run hello following snippet.</span></span>

        INSERT INTO [dbo].[Table1] VALUES (1,'Neal','Kell'), (2,'Lila','Fulton'), (3, 'Erna','Myers'), (4,'Annette','Simpson');


## <a name="use-sqoop-from-an-hdinsight-cluster-with-access-toodata-lake-store"></a><span data-ttu-id="29db5-135">Sqoop de uso de um cluster de HDInsight com acesso tooData Lake repositório</span><span class="sxs-lookup"><span data-stu-id="29db5-135">Use Sqoop from an HDInsight cluster with access tooData Lake Store</span></span>
<span data-ttu-id="29db5-136">Um cluster HDInsight já tem pacotes de Sqoop Olá disponíveis.</span><span class="sxs-lookup"><span data-stu-id="29db5-136">An HDInsight cluster already has hello Sqoop packages available.</span></span> <span data-ttu-id="29db5-137">Se você tiver configurado o repositório Data Lake do toouse de cluster de HDInsight hello como um armazenamento adicional, você pode usar o Sqoop (sem alterações de configuração) tooimport/exportar dados entre um banco de dados relacional (por exemplo, banco de dados do SQL Azure) e um repositório Data Lake conta.</span><span class="sxs-lookup"><span data-stu-id="29db5-137">If you have configured hello HDInsight cluster toouse Data Lake Store as an additional storage, you can use Sqoop (without any configuration changes) tooimport/export data between a relational database (in this example, Azure SQL Database) and a Data Lake Store account.</span></span>

1. <span data-ttu-id="29db5-138">Para este tutorial, vamos supor que você criou um cluster do Linux, então você deve usar SSH tooconnect toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="29db5-138">For this tutorial, we assume you created a Linux cluster so you should use SSH tooconnect toohello cluster.</span></span> <span data-ttu-id="29db5-139">Consulte [conectar tooa HDInsight baseados em Linux cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="29db5-139">See [Connect tooa Linux-based HDInsight cluster](../hdinsight/hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>
2. <span data-ttu-id="29db5-140">Verifique se você pode acessar Olá conta do repositório Data Lake do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="29db5-140">Verify whether you can access hello Data Lake Store account from hello cluster.</span></span> <span data-ttu-id="29db5-141">Execute Olá comando a seguir no prompt SSH hello:</span><span class="sxs-lookup"><span data-stu-id="29db5-141">Run hello following command from hello SSH prompt:</span></span>

        hdfs dfs -ls adl://<data_lake_store_account>.azuredatalakestore.net/

    <span data-ttu-id="29db5-142">Isso deve fornecer uma lista de arquivos/pastas Olá conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="29db5-142">This should provide a list of files/folders in hello Data Lake Store account.</span></span>

### <a name="import-data-from-azure-sql-database-into-data-lake-store"></a><span data-ttu-id="29db5-143">Importar dados do Banco de Dados SQL do Azure para o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="29db5-143">Import data from Azure SQL Database into Data Lake Store</span></span>
1. <span data-ttu-id="29db5-144">Navegue toohello diretório onde os pacotes de Sqoop estão disponíveis.</span><span class="sxs-lookup"><span data-stu-id="29db5-144">Navigate toohello directory where Sqoop packages are available.</span></span> <span data-ttu-id="29db5-145">Normalmente, será `/usr/hdp/<version>/sqoop/bin`.</span><span class="sxs-lookup"><span data-stu-id="29db5-145">Typically, this will be at `/usr/hdp/<version>/sqoop/bin`.</span></span>
2. <span data-ttu-id="29db5-146">Importar dados de saudação do **Table1** em Olá conta do repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="29db5-146">Import hello data from **Table1** into hello Data Lake Store account.</span></span> <span data-ttu-id="29db5-147">Use Olá sintaxe a seguir:</span><span class="sxs-lookup"><span data-stu-id="29db5-147">Use hello following syntax:</span></span>

        sqoop-import --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table1 --target-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1

    <span data-ttu-id="29db5-148">Observe que **-banco de dados--nome do sql server** espaço reservado representa o nome de saudação do servidor de saudação onde o banco de dados do SQL Azure hello está sendo executado.</span><span class="sxs-lookup"><span data-stu-id="29db5-148">Note that **sql-database-server-name** placeholder represents hello name of hello server where hello Azure SQL database is running.</span></span> <span data-ttu-id="29db5-149">**nome de banco de dados SQL** espaço reservado representa o nome do banco de dados real hello.</span><span class="sxs-lookup"><span data-stu-id="29db5-149">**sql-database-name** placeholder represents hello actual database name.</span></span>

    <span data-ttu-id="29db5-150">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="29db5-150">For example,</span></span>


        sqoop-import --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table1 --target-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1

1. <span data-ttu-id="29db5-151">Verifique se esse Olá dados foram transferidos toohello conta de repositório Data Lake.</span><span class="sxs-lookup"><span data-stu-id="29db5-151">Verify that hello data has been transferred toohello Data Lake Store account.</span></span> <span data-ttu-id="29db5-152">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="29db5-152">Run hello following command:</span></span>

        hdfs dfs -ls adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/

    <span data-ttu-id="29db5-153">Você deve ver Olá saída a seguir.</span><span class="sxs-lookup"><span data-stu-id="29db5-153">You should see hello following output.</span></span>


        -rwxrwxrwx   0 sshuser hdfs          0 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/_SUCCESS
        -rwxrwxrwx   0 sshuser hdfs         12 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00000
        -rwxrwxrwx   0 sshuser hdfs         14 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00001
        -rwxrwxrwx   0 sshuser hdfs         13 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00002
        -rwxrwxrwx   0 sshuser hdfs         18 2016-02-26 21:09 adl://hdiadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1/part-m-00003

    <span data-ttu-id="29db5-154">Cada **parte-m -*** arquivo corresponde tooa linha na tabela de origem hello, **Table1**.</span><span class="sxs-lookup"><span data-stu-id="29db5-154">Each **part-m-*** file corresponds tooa row in hello source table, **Table1**.</span></span> <span data-ttu-id="29db5-155">Você pode exibir o conteúdo de saudação da parte Olá - m-* arquivos tooverify.</span><span class="sxs-lookup"><span data-stu-id="29db5-155">You can view hello contents of hello part-m-* files tooverify.</span></span>


### <a name="export-data-from-data-lake-store-into-azure-sql-database"></a><span data-ttu-id="29db5-156">Exportar dados do Repositório Data Lake para o Banco de Dados SQL do Azure</span><span class="sxs-lookup"><span data-stu-id="29db5-156">Export data from Data Lake Store into Azure SQL Database</span></span>
1. <span data-ttu-id="29db5-157">Exportar dados de saudação do repositório Data Lake conta toohello tabela vazia **Table2**, em hello Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="29db5-157">Export hello data from Data Lake Store account toohello empty table, **Table2**, in hello Azure SQL Database.</span></span> <span data-ttu-id="29db5-158">Use Olá sintaxe a seguir.</span><span class="sxs-lookup"><span data-stu-id="29db5-158">Use hello following syntax.</span></span>

        sqoop-export --connect "jdbc:sqlserver://<sql-database-server-name>.database.windows.net:1433;username=<username>@<sql-database-server-name>;password=<password>;database=<sql-database-name>" --table Table2 --export-dir adl://<data-lake-store-name>.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

    <span data-ttu-id="29db5-159">Por exemplo,</span><span class="sxs-lookup"><span data-stu-id="29db5-159">For example,</span></span>


        sqoop-export --connect "jdbc:sqlserver://mysqoopserver.database.windows.net:1433;username=nitinme@mysqoopserver;password=<password>;database=mysqoopdatabase" --table Table2 --export-dir adl://myadlstore.azuredatalakestore.net/Sqoop/SqoopImportTable1 --input-fields-terminated-by ","

1. <span data-ttu-id="29db5-160">Verifique se esse Olá dados foram carregada toohello tabela de banco de dados SQL.</span><span class="sxs-lookup"><span data-stu-id="29db5-160">Verify that hello data was uploaded toohello SQL Database table.</span></span> <span data-ttu-id="29db5-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) ou Visual Studio tooconnect toohello banco de dados do SQL Azure e, em seguida, execute Olá seguindo a consulta.</span><span class="sxs-lookup"><span data-stu-id="29db5-161">Use [SQL Server Management Studio](../sql-database/sql-database-connect-query-ssms.md) or Visual Studio tooconnect toohello Azure SQL Database and then run hello following query.</span></span>

        SELECT * FROM TABLE2

    <span data-ttu-id="29db5-162">Isso deve ter Olá saída a seguir.</span><span class="sxs-lookup"><span data-stu-id="29db5-162">This should have hello following output.</span></span>

         ID  FName   LName
        ------------------
        1    Neal    Kell
        2    Lila    Fulton
        3    Erna    Myers
        4    Annette    Simpson

## <a name="performance-considerations-while-using-sqoop"></a><span data-ttu-id="29db5-163">Considerações de desempenho ao usar o Sqoop</span><span class="sxs-lookup"><span data-stu-id="29db5-163">Performance considerations while using Sqoop</span></span>

<span data-ttu-id="29db5-164">Para o Sqoop de ajuste de desempenho de trabalho repositório toocopy data tooData Lake, consulte [documento de desempenho de Sqoop](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span><span class="sxs-lookup"><span data-stu-id="29db5-164">For performance tuning your Sqoop job toocopy data tooData Lake Store, see [Sqoop performance document](https://blogs.msdn.microsoft.com/bigdatasupport/2015/02/17/sqoop-job-performance-tuning-in-hdinsight-hadoop/).</span></span>

## <a name="see-also"></a><span data-ttu-id="29db5-165">Consulte também</span><span class="sxs-lookup"><span data-stu-id="29db5-165">See also</span></span>
* [<span data-ttu-id="29db5-166">Copiar dados do repositório Azure armazenamento de Blobs tooData Lake</span><span class="sxs-lookup"><span data-stu-id="29db5-166">Copy data from Azure Storage Blobs tooData Lake Store</span></span>](data-lake-store-copy-data-azure-storage-blob.md)
* [<span data-ttu-id="29db5-167">Proteger dados no Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="29db5-167">Secure data in Data Lake Store</span></span>](data-lake-store-secure-data.md)
* [<span data-ttu-id="29db5-168">Usar a Análise Data Lake do Azure com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="29db5-168">Use Azure Data Lake Analytics with Data Lake Store</span></span>](../data-lake-analytics/data-lake-analytics-get-started-portal.md)
* [<span data-ttu-id="29db5-169">Usar o Azure HDInsight com o Repositório Data Lake</span><span class="sxs-lookup"><span data-stu-id="29db5-169">Use Azure HDInsight with Data Lake Store</span></span>](data-lake-store-hdinsight-hadoop-use-portal.md)
