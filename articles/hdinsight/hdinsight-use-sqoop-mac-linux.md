---
title: aaaApache Sqoop com Hadoop - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse tooimport Sqoop Apache e exportação entre Hadoop no HDInsight e um banco de dados do SQL Azure."
editor: cgronlun
manager: jhubbard
services: hdinsight
documentationcenter: 
author: Blackmist
tags: azure-portal
keywords: hadoop sqoop,sqoop
ms.assetid: 303649a5-4be5-4933-bf1d-4b232083c354
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/19/2017
ms.author: larryfr
ms.openlocfilehash: b256285659bbcf18ff05e220ccdf51c21eb8fbf7
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-sqoop-tooimport-and-export-data-between-hadoop-on-hdinsight-and-sql-database"></a><span data-ttu-id="8b582-104">Use Apache Sqoop tooimport e exportar dados entre o banco de dados SQL e o Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="8b582-104">Use Apache Sqoop tooimport and export data between Hadoop on HDInsight and SQL Database</span></span>

[!INCLUDE [sqoop-selector](../../includes/hdinsight-selector-use-sqoop.md)]

<span data-ttu-id="8b582-105">Saiba como cluster de toouse Apache Sqoop tooimport e exportação entre um Hadoop no HDInsight do Azure e banco de dados do banco de dados SQL ou Microsoft SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8b582-105">Learn how toouse Apache Sqoop tooimport and export between a Hadoop cluster in Azure HDInsight and Azure SQL Database or Microsoft SQL Server database.</span></span> <span data-ttu-id="8b582-106">Olá etapas Olá de usar este documento `sqoop` comando diretamente da saudação um nó principal do cluster de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="8b582-106">hello steps in this document use hello `sqoop` command directly from hello headnode of hello Hadoop cluster.</span></span> <span data-ttu-id="8b582-107">Use o nó principal do SSH tooconnect toohello e executar comandos de saudação neste documento.</span><span class="sxs-lookup"><span data-stu-id="8b582-107">You use SSH tooconnect toohello head node and run hello commands in this document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b582-108">Olá etapas deste documento só funcionam com clusters de HDInsight que usam o Linux.</span><span class="sxs-lookup"><span data-stu-id="8b582-108">hello steps in this document only work with HDInsight clusters that use Linux.</span></span> <span data-ttu-id="8b582-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="8b582-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="8b582-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="8b582-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="install-freetds"></a><span data-ttu-id="8b582-111">Instalar o FreeTDS</span><span class="sxs-lookup"><span data-stu-id="8b582-111">Install FreeTDS</span></span>

1. <span data-ttu-id="8b582-112">Use SSH tooconnect toohello HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="8b582-112">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="8b582-113">Por exemplo, Olá comando a seguir se conecta a nó principal primário toohello de um cluster denominado `mycluster`:</span><span class="sxs-lookup"><span data-stu-id="8b582-113">For example, hello following command connects toohello primary headnode of a cluster named `mycluster`:</span></span>

    ```bash
    ssh CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="8b582-114">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="8b582-114">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="8b582-115">Use Olá comando tooinstall FreeTDS a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b582-115">Use hello following command tooinstall FreeTDS:</span></span>

    ```bash
    sudo apt --assume-yes install freetds-dev freetds-bin
    ```

    <span data-ttu-id="8b582-116">FreeTDS é usado em tooSQL tooconnect de várias etapas banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8b582-116">FreeTDS is used in several steps tooconnect tooSQL Database.</span></span>

## <a name="create-hello-table-in-sql-database"></a><span data-ttu-id="8b582-117">Criar tabela de saudação no banco de dados SQL</span><span class="sxs-lookup"><span data-stu-id="8b582-117">Create hello table in SQL Database</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8b582-118">Se você estiver usando o cluster do HDInsight hello e banco de dados SQL criado no [criar o cluster e o banco de dados SQL](hdinsight-use-sqoop.md), ignore as etapas de saudação nesta seção.</span><span class="sxs-lookup"><span data-stu-id="8b582-118">If you are using hello HDInsight cluster and SQL Database created in [Create cluster and SQL database](hdinsight-use-sqoop.md), skip hello steps in this section.</span></span> <span data-ttu-id="8b582-119">Olá banco de dados e tabela foram criados como parte da saudação etapas nas Olá [criar o cluster e o banco de dados SQL](hdinsight-use-sqoop.md) documento.</span><span class="sxs-lookup"><span data-stu-id="8b582-119">hello database and table were created as part of hello steps in hello [Create cluster and SQL database](hdinsight-use-sqoop.md) document.</span></span>

1. <span data-ttu-id="8b582-120">Da sessão SSH hello, use Olá servidor de banco de dados SQL do comando tooconnect toohello a seguir.</span><span class="sxs-lookup"><span data-stu-id="8b582-120">From hello SSH session, use hello following command tooconnect toohello SQL Database server.</span></span>

        TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D sqooptest

    <span data-ttu-id="8b582-121">Você receberá a saída toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b582-121">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toosqooptest
        1>

2. <span data-ttu-id="8b582-122">Em Olá `1>` prompt, digite Olá consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b582-122">At hello `1>` prompt, enter hello following query:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(clientid)
    GO
    ```

    <span data-ttu-id="8b582-123">Olá quando `GO` instrução for inserida, instruções de saudação anterior são avaliadas.</span><span class="sxs-lookup"><span data-stu-id="8b582-123">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="8b582-124">Primeiro, Olá **mobiledata** tabela é criada e, em seguida, um índice clusterizado é adicionado tooit (exigido pelo banco de dados SQL).</span><span class="sxs-lookup"><span data-stu-id="8b582-124">First, hello **mobiledata** table is created, then a clustered index is added tooit (required by SQL Database.)</span></span>

    <span data-ttu-id="8b582-125">Saudação de uso tooverify de consulta que Olá a tabela a seguir foi criada:</span><span class="sxs-lookup"><span data-stu-id="8b582-125">Use hello following query tooverify that hello table has been created:</span></span>

    ```sql
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="8b582-126">Você verá a saída toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b582-126">You see output similar toohello following text:</span></span>

        TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
        sqooptest       dbo     mobiledata      BASE TABLE

3. <span data-ttu-id="8b582-127">Digite `exit` em Olá `1>` tooexit Olá tsql utilitário do prompt.</span><span class="sxs-lookup"><span data-stu-id="8b582-127">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="sqoop-export"></a><span data-ttu-id="8b582-128">Exportação do Sqoop</span><span class="sxs-lookup"><span data-stu-id="8b582-128">Sqoop export</span></span>

1. <span data-ttu-id="8b582-129">De cluster para toohello de conexão do SSH hello, use Olá tooverify de comando que Sqoop pode ver o banco de dados SQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b582-129">From hello SSH connection toohello cluster, use hello following command tooverify that Sqoop can see your SQL Database:</span></span>

    ```bash
    sqoop list-databases --connect jdbc:sqlserver://<serverName>.database.windows.net:1433 --username <adminLogin> -P
    ```
    <span data-ttu-id="8b582-130">Quando solicitado, insira a senha de saudação para logon de banco de dados SQL hello.</span><span class="sxs-lookup"><span data-stu-id="8b582-130">When prompted, enter hello password for hello SQL Database login.</span></span>

    <span data-ttu-id="8b582-131">Esse comando retorna uma lista de bancos de dados, incluindo Olá **sqooptest** banco de dados que você criou anteriormente.</span><span class="sxs-lookup"><span data-stu-id="8b582-131">This command returns a list of databases, including hello **sqooptest** database that you created earlier.</span></span>

2. <span data-ttu-id="8b582-132">dados de tooexport de **hivesampletable** toohello **mobiledata** de tabela, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b582-132">tooexport data from **hivesampletable** toohello **mobiledata** table, use hello following command:</span></span>

    ```bash
    sqoop export --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> -P --table 'mobiledata' --export-dir 'wasb:///hive/warehouse/hivesampletable' --fields-terminated-by '\t' -m 1
    ```

    <span data-ttu-id="8b582-133">Este comando instrui o Sqoop tooconnect toohello **sqooptest** banco de dados.</span><span class="sxs-lookup"><span data-stu-id="8b582-133">This command instructs Sqoop tooconnect toohello **sqooptest** database.</span></span> <span data-ttu-id="8b582-134">Sqoop, em seguida, exporta dados de **wasb: / / / hive/warehouse/hivesampletable** toohello **mobiledata** tabela.</span><span class="sxs-lookup"><span data-stu-id="8b582-134">Sqoop then exports data from **wasb:///hive/warehouse/hivesampletable** toohello **mobiledata** table.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="8b582-135">Use `wasb:///` se o armazenamento padrão da saudação para seu cluster é uma conta de armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b582-135">Use `wasb:///` if hello default storage for your cluster is an Azure Storage account.</span></span> <span data-ttu-id="8b582-136">Use `adl:///` se for um Azure Data Lake Store.</span><span class="sxs-lookup"><span data-stu-id="8b582-136">Use `adl:///` if it is an Azure Data Lake Store.</span></span>

3. <span data-ttu-id="8b582-137">Após a conclusão do comando hello, use Olá comando tooconnect toohello banco de dados usando TSQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b582-137">After hello command completes, use hello following command tooconnect toohello database using TSQL:</span></span>

    ```bash
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P -p 1433 -D sqooptest
    ```

    <span data-ttu-id="8b582-138">Uma vez conectado, use Olá tooverify instruções que Olá dados a seguir foi exportado toohello **mobiledata** tabela:</span><span class="sxs-lookup"><span data-stu-id="8b582-138">Once connected, use hello following statements tooverify that hello data was exported toohello **mobiledata** table:</span></span>

    ```sql
    SET ROWCOUNT 50;
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="8b582-139">Você deve ver uma lista dos dados na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="8b582-139">You should see a listing of data in hello table.</span></span> <span data-ttu-id="8b582-140">Tipo `exit` utilitário do tooexit Olá tsql.</span><span class="sxs-lookup"><span data-stu-id="8b582-140">Type `exit` tooexit hello tsql utility.</span></span>

## <a name="sqoop-import"></a><span data-ttu-id="8b582-141">Importação do Sqoop</span><span class="sxs-lookup"><span data-stu-id="8b582-141">Sqoop import</span></span>

1. <span data-ttu-id="8b582-142">Dados tooimport de saudação do comando de uso a seguir de saudação **mobiledata** tabela no banco de dados SQL, toohello **wasb: / / / tutoriais/usesqoop/importeddata** do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="8b582-142">Use hello following command tooimport data from hello **mobiledata** table in SQL Database, toohello **wasb:///tutorials/usesqoop/importeddata** directory on HDInsight:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://<serverName>.database.windows.net:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

    <span data-ttu-id="8b582-143">campos de saudação nos dados de saudação são separados por um caractere de tabulação e linhas de saudação são terminadas por um caractere de nova linha.</span><span class="sxs-lookup"><span data-stu-id="8b582-143">hello fields in hello data are separated by a tab character, and hello lines are terminated by a new-line character.</span></span>

2. <span data-ttu-id="8b582-144">Depois de saudação importação for concluída, use Olá toolist comando dados Olá no novo diretório de saudação a seguir:</span><span class="sxs-lookup"><span data-stu-id="8b582-144">Once hello import has completed, use hello following command toolist out hello data in hello new directory:</span></span>

    ```bash
    hdfs dfs -text /tutorials/usesqoop/importeddata/part-m-00000
    ```

## <a name="using-sql-server"></a><span data-ttu-id="8b582-145">Usar o SQL Server</span><span class="sxs-lookup"><span data-stu-id="8b582-145">Using SQL Server</span></span>

<span data-ttu-id="8b582-146">Você também pode usar o Sqoop tooimport e exportar dados do SQL Server, no seu data center ou em uma máquina Virtual hospedada no Azure.</span><span class="sxs-lookup"><span data-stu-id="8b582-146">You can also use Sqoop tooimport and export data from SQL Server, either in your data center or on a Virtual Machine hosted in Azure.</span></span> <span data-ttu-id="8b582-147">Olá diferenças entre usar o banco de dados SQL e SQL Server são:</span><span class="sxs-lookup"><span data-stu-id="8b582-147">hello differences between using SQL Database and SQL Server are:</span></span>

* <span data-ttu-id="8b582-148">HDInsight e o SQL Server deve ser em Olá mesma rede Virtual do Azure.</span><span class="sxs-lookup"><span data-stu-id="8b582-148">Both HDInsight and SQL Server must be on hello same Azure Virtual Network.</span></span>

    <span data-ttu-id="8b582-149">Para obter um exemplo, consulte Olá [HDInsight conectar rede de local de tooyour](./connect-on-premises-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="8b582-149">For an example, see hello [Connect HDInsight tooyour on-premises network](./connect-on-premises-network.md) document.</span></span>

    <span data-ttu-id="8b582-150">Para obter mais informações sobre como usar o HDInsight com uma rede Virtual do Azure, consulte Olá [estender HDInsight com a rede Virtual do Azure](hdinsight-extend-hadoop-virtual-network.md) documento.</span><span class="sxs-lookup"><span data-stu-id="8b582-150">For more information on using HDInsight with an Azure Virtual Network, see hello [Extend HDInsight with Azure Virtual Network](hdinsight-extend-hadoop-virtual-network.md) document.</span></span> <span data-ttu-id="8b582-151">Para obter mais informações sobre a rede Virtual do Azure, consulte Olá [visão geral da rede Virtual](../virtual-network/virtual-networks-overview.md) documento.</span><span class="sxs-lookup"><span data-stu-id="8b582-151">For more information on Azure Virtual Network, see hello [Virtual Network Overview](../virtual-network/virtual-networks-overview.md) document.</span></span>

* <span data-ttu-id="8b582-152">SQL Server deve ser configurado tooallow a autenticação do SQL.</span><span class="sxs-lookup"><span data-stu-id="8b582-152">SQL Server must be configured tooallow SQL authentication.</span></span> <span data-ttu-id="8b582-153">Para obter mais informações, consulte Olá [escolher um modo de autenticação](https://msdn.microsoft.com/ms144284.aspx) documento.</span><span class="sxs-lookup"><span data-stu-id="8b582-153">For more information, see hello [Choose an Authentication Mode](https://msdn.microsoft.com/ms144284.aspx) document.</span></span>

* <span data-ttu-id="8b582-154">Você pode ter conexões remotas do tooaccept tooconfigure do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8b582-154">You may have tooconfigure SQL Server tooaccept remote connections.</span></span> <span data-ttu-id="8b582-155">Para obter mais informações, consulte Olá [como tootroubleshoot conexão toohello do SQL Server do banco de dados mecanismo](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) documento.</span><span class="sxs-lookup"><span data-stu-id="8b582-155">For more information, see hello [How tootroubleshoot connecting toohello SQL Server database engine](http://social.technet.microsoft.com/wiki/contents/articles/2102.how-to-troubleshoot-connecting-to-the-sql-server-database-engine.aspx) document.</span></span>

* <span data-ttu-id="8b582-156">Criar hello **sqooptest** banco de dados no SQL Server usando um utilitário como **SQL Server Management Studio** ou **tsql**.</span><span class="sxs-lookup"><span data-stu-id="8b582-156">Create hello **sqooptest** database in SQL Server using a utility such as **SQL Server Management Studio** or **tsql**.</span></span> <span data-ttu-id="8b582-157">etapas de saudação para usar o hello CLI do Azure só funcionam para o banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8b582-157">hello steps for using hello Azure CLI only work for Azure SQL Database.</span></span>

    <span data-ttu-id="8b582-158">Olá Use Olá de toocreate de instruções Transact-SQL a seguir **mobiledata** tabela:</span><span class="sxs-lookup"><span data-stu-id="8b582-158">Use hello following Transact-SQL statements toocreate hello **mobiledata** table:</span></span>

    ```sql
    CREATE TABLE [dbo].[mobiledata](
    [clientid] [nvarchar](50),
    [querytime] [nvarchar](50),
    [market] [nvarchar](50),
    [deviceplatform] [nvarchar](50),
    [devicemake] [nvarchar](50),
    [devicemodel] [nvarchar](50),
    [state] [nvarchar](50),
    [country] [nvarchar](50),
    [querydwelltime] [float],
    [sessionid] [bigint],
    [sessionpagevieworder] [bigint])
    ```

* <span data-ttu-id="8b582-159">Ao se conectar toohello do SQL Server de HDInsight, você pode ter toouse endereço IP de saudação de saudação do SQL Server.</span><span class="sxs-lookup"><span data-stu-id="8b582-159">When connecting toohello SQL Server from HDInsight, you may have toouse hello IP address of hello SQL Server.</span></span> <span data-ttu-id="8b582-160">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="8b582-160">For example:</span></span>

    ```bash
    sqoop import --connect 'jdbc:sqlserver://10.0.1.1:1433;database=sqooptest' --username <adminLogin> --password <adminPassword> --table 'mobiledata' --target-dir 'wasb:///tutorials/usesqoop/importeddata' --fields-terminated-by '\t' --lines-terminated-by '\n' -m 1
    ```

## <a name="limitations"></a><span data-ttu-id="8b582-161">Limitações</span><span class="sxs-lookup"><span data-stu-id="8b582-161">Limitations</span></span>

* <span data-ttu-id="8b582-162">A exportação em massa - HDInsight baseados em Linux com, Olá Sqoop conector usado tooexport dados tooMicrosoft do SQL Server ou banco de dados do SQL Azure atualmente não dá suporte para inserções em massa.</span><span class="sxs-lookup"><span data-stu-id="8b582-162">Bulk export - With Linux-based HDInsight, hello Sqoop connector used tooexport data tooMicrosoft SQL Server or Azure SQL Database does not currently support bulk inserts.</span></span>

* <span data-ttu-id="8b582-163">Envio em lote - com HDInsight baseados em Linux, ao usar o hello `-batch` opção ao executar inserções, Sqoop faz várias inserções em vez de envio em lote as operações de inserção hello.</span><span class="sxs-lookup"><span data-stu-id="8b582-163">Batching - With Linux-based HDInsight, When using hello `-batch` switch when performing inserts, Sqoop makes multiple inserts instead of batching hello insert operations.</span></span>

## <a name="next-steps"></a><span data-ttu-id="8b582-164">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="8b582-164">Next steps</span></span>

<span data-ttu-id="8b582-165">Agora que você aprendeu como toouse Sqoop.</span><span class="sxs-lookup"><span data-stu-id="8b582-165">Now you have learned how toouse Sqoop.</span></span> <span data-ttu-id="8b582-166">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="8b582-166">toolearn more, see:</span></span>

* <span data-ttu-id="8b582-167">[Usar o Oozie com o HDInsight][hdinsight-use-oozie]: use a ação do Sqoop no fluxo de trabalho do Oozie.</span><span class="sxs-lookup"><span data-stu-id="8b582-167">[Use Oozie with HDInsight][hdinsight-use-oozie]: Use Sqoop action in an Oozie workflow.</span></span>
* <span data-ttu-id="8b582-168">[Analisar dados de atraso de voo usando HDInsight][hdinsight-analyze-flight-data]: usar Hive tooanalyze voo atrasar dados e, em seguida, usar o banco de dados do Sqoop tooexport dados tooan SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="8b582-168">[Analyze flight delay data using HDInsight][hdinsight-analyze-flight-data]: Use Hive tooanalyze flight delay data, and then use Sqoop tooexport data tooan Azure SQL database.</span></span>
* <span data-ttu-id="8b582-169">[Carregar dados tooHDInsight][hdinsight-upload-data]: encontrar outros métodos para carregar o armazenamento de BLOBs do Azure/tooHDInsight de dados.</span><span class="sxs-lookup"><span data-stu-id="8b582-169">[Upload data tooHDInsight][hdinsight-upload-data]: Find other methods for uploading data tooHDInsight/Azure Blob storage.</span></span>

[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-storage]: ../hdinsight-hadoop-use-blob-storage.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md

[sqldatabase-get-started]: ../sql-database-get-started.md
[sqldatabase-create-configue]: ../sql-database-create-configure.md

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-install]: /powershell/azureps-cmdlets-docs
[powershell-script]: http://technet.microsoft.com/library/ee176949.aspx

[sqoop-user-guide-1.4.4]: https://sqoop.apache.org/docs/1.4.4/SqoopUserGuide.html
