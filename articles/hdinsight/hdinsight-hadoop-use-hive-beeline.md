---
title: aaaUse Beeline com o Apache Hive - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse Olá Beeline cliente toorun Hive consultas com Hadoop no HDInsight. Beeline é um utilitário para trabalhar com HiveServer2 sobre JDBC."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
keywords: beeline hive, hive beeline
ms.assetid: 3adfb1ba-8924-4a13-98db-10a67ab24fca
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: e788ff39f33d928808cfcb83a92f62ac9ae8ca09
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-hello-beeline-client-with-apache-hive"></a><span data-ttu-id="1de05-105">Usar o cliente de Beeline Olá com o Apache Hive</span><span class="sxs-lookup"><span data-stu-id="1de05-105">Use hello Beeline client with Apache Hive</span></span>

<span data-ttu-id="1de05-106">Saiba como toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) consultas toorun Hive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1de05-106">Learn how toouse [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) toorun Hive queries on HDInsight.</span></span>

<span data-ttu-id="1de05-107">Beeline é um cliente de Hive que está incluído em nós de cabeçalho de saudação do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1de05-107">Beeline is a Hive client that is included on hello head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="1de05-108">Beeline usa JDBC tooconnect tooHiveServer2, um serviço hospedado em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1de05-108">Beeline uses JDBC tooconnect tooHiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="1de05-109">Você também pode usar Beeline tooaccess Hive no HDInsight remotamente em Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="1de05-109">You can also use Beeline tooaccess Hive on HDInsight remotely over hello internet.</span></span> <span data-ttu-id="1de05-110">Olá, a tabela a seguir fornece cadeias de caracteres de conexão para uso com Beeline:</span><span class="sxs-lookup"><span data-stu-id="1de05-110">hello following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="1de05-111">De que local você executa o Beeline</span><span class="sxs-lookup"><span data-stu-id="1de05-111">Where you run Beeline from</span></span> | <span data-ttu-id="1de05-112">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1de05-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="1de05-113">Um nó de um nó principal ou de borda de tooa do conexão SSH</span><span class="sxs-lookup"><span data-stu-id="1de05-113">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="1de05-114">Cluster de saudação externa</span><span class="sxs-lookup"><span data-stu-id="1de05-114">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="1de05-115">Substituir `admin` com a conta de logon de cluster Olá para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="1de05-115">Replace `admin` with hello cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="1de05-116">Substituir `password` com senha Olá Olá cluster conta de logon.</span><span class="sxs-lookup"><span data-stu-id="1de05-116">Replace `password` with hello password for hello cluster login account.</span></span>
>
> <span data-ttu-id="1de05-117">Substituir `clustername` com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1de05-117">Replace `clustername` with hello name of your HDInsight cluster.</span></span>

## <span data-ttu-id="1de05-118"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1de05-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="1de05-119">Um cluster do Hadoop no HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="1de05-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="1de05-120">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1de05-120">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1de05-121">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1de05-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="1de05-122">Um cliente SSH ou um cliente Beeline local.</span><span class="sxs-lookup"><span data-stu-id="1de05-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="1de05-123">A maioria das etapas neste documento hello presumem que você está usando Beeline de um cluster de toohello sessão SSH.</span><span class="sxs-lookup"><span data-stu-id="1de05-123">Most of hello steps in this document assume that you are using Beeline from an SSH session toohello cluster.</span></span> <span data-ttu-id="1de05-124">Para obter informações sobre a execução Beeline do cluster de saudação externa, consulte Olá [usar Beeline remotamente](#remote) seção.</span><span class="sxs-lookup"><span data-stu-id="1de05-124">For information on running Beeline from outside hello cluster, see hello [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="1de05-125">Para saber mais sobre como usar SSH, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1de05-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="1de05-126"><a id="beeline"></a>Usar o Beeline</span><span class="sxs-lookup"><span data-stu-id="1de05-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="1de05-127">Ao iniciar o Beeline, você deve fornecer uma cadeia de conexão para HiveServer2 em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1de05-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="1de05-128">comando de Olá toorun do cluster fora do hello, você deve fornecer nome de conta de logon de cluster de saudação (padrão `admin`) e a senha.</span><span class="sxs-lookup"><span data-stu-id="1de05-128">toorun hello command from outside hello cluster, you must also provide hello cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="1de05-129">Use Olá tabela toofind Olá conexão cadeia de caracteres formato e os parâmetros toouse a seguir:</span><span class="sxs-lookup"><span data-stu-id="1de05-129">Use hello following table toofind hello connection string format and parameters toouse:</span></span>

    | <span data-ttu-id="1de05-130">De que local você executa o Beeline</span><span class="sxs-lookup"><span data-stu-id="1de05-130">Where you run Beeline from</span></span> | <span data-ttu-id="1de05-131">parâmetros</span><span class="sxs-lookup"><span data-stu-id="1de05-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="1de05-132">Um nó de um nó principal ou de borda de tooa do conexão SSH</span><span class="sxs-lookup"><span data-stu-id="1de05-132">An SSH connection tooa headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="1de05-133">Cluster de saudação externa</span><span class="sxs-lookup"><span data-stu-id="1de05-133">Outside hello cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="1de05-134">Por exemplo, Olá comando a seguir pode ser usado toostart Beeline de um cluster de toohello sessão SSH:</span><span class="sxs-lookup"><span data-stu-id="1de05-134">For example, hello following command can be used toostart Beeline from an SSH session toohello cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="1de05-135">Esse comando inicia o cliente de Beeline hello e conecta tooHiveServer2 no nó principal do cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1de05-135">This command starts hello Beeline client, and connects tooHiveServer2 on hello cluster head node.</span></span> <span data-ttu-id="1de05-136">Após a conclusão do comando hello, você chegar a um `jdbc:hive2://headnodehost:10001/>` prompt.</span><span class="sxs-lookup"><span data-stu-id="1de05-136">Once hello command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="1de05-137">Os comandos Beeline normalmente começam com um caractere `!`, por exemplo, `!help` exibe a ajuda.</span><span class="sxs-lookup"><span data-stu-id="1de05-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="1de05-138">No entanto Olá `!` pode ser omitido para alguns comandos.</span><span class="sxs-lookup"><span data-stu-id="1de05-138">However hello `!` can be omitted for some commands.</span></span> <span data-ttu-id="1de05-139">Por exemplo, `help` também funciona.</span><span class="sxs-lookup"><span data-stu-id="1de05-139">For example, `help` also works.</span></span>

    <span data-ttu-id="1de05-140">Há um `!sql`, que é usado tooexecute HiveQL instruções.</span><span class="sxs-lookup"><span data-stu-id="1de05-140">There is a `!sql`, which is used tooexecute HiveQL statements.</span></span> <span data-ttu-id="1de05-141">No entanto, HiveQL é usado muito comum que você pode omitir Olá anterior `!sql`.</span><span class="sxs-lookup"><span data-stu-id="1de05-141">However, HiveQL is so commonly used that you can omit hello preceding `!sql`.</span></span> <span data-ttu-id="1de05-142">Olá duas instruções a seguir é equivalente:</span><span class="sxs-lookup"><span data-stu-id="1de05-142">hello following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="1de05-143">Em um novo cluster, somente uma tabela é listada: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="1de05-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="1de05-144">Use Olá comando toodisplay Olá esquema Olá hivesampletable a seguir:</span><span class="sxs-lookup"><span data-stu-id="1de05-144">Use hello following command toodisplay hello schema for hello hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="1de05-145">Esse comando retorna Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="1de05-145">This command returns hello following information:</span></span>

        +-----------------------+------------+----------+--+
        |       col_name        | data_type  | comment  |
        +-----------------------+------------+----------+--+
        | clientid              | string     |          |
        | querytime             | string     |          |
        | market                | string     |          |
        | deviceplatform        | string     |          |
        | devicemake            | string     |          |
        | devicemodel           | string     |          |
        | state                 | string     |          |
        | country               | string     |          |
        | querydwelltime        | double     |          |
        | sessionid             | bigint     |          |
        | sessionpagevieworder  | bigint     |          |
        +-----------------------+------------+----------+--+

    <span data-ttu-id="1de05-146">Essas informações descrevem colunas Olá na tabela de saudação.</span><span class="sxs-lookup"><span data-stu-id="1de05-146">This information describes hello columns in hello table.</span></span> <span data-ttu-id="1de05-147">Enquanto estamos pode executar algumas consultas em relação a esses dados, vamos em vez disso, crie um novo toodemonstrate de tabela como dados tooload Hive e aplicar um esquema.</span><span class="sxs-lookup"><span data-stu-id="1de05-147">While we could perform some queries against this data, let's instead create a brand new table toodemonstrate how tooload data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="1de05-148">Digite hello seguindo as instruções toocreate uma tabela chamada **log4jLogs** usando dados de exemplo fornecidos com o cluster do HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="1de05-148">Enter hello following statements toocreate a table named **log4jLogs** by using sample data provided with hello HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="1de05-149">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="1de05-149">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="1de05-150">`DROP TABLE`-Se Olá tabela existir, ele será excluído.</span><span class="sxs-lookup"><span data-stu-id="1de05-150">`DROP TABLE` - If hello table exists, it is deleted.</span></span>

    * <span data-ttu-id="1de05-151">`CREATE EXTERNAL TABLE` – Cria uma tabela **externa** no Hive.</span><span class="sxs-lookup"><span data-stu-id="1de05-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="1de05-152">Tabelas externas apenas armazenam a definição de tabela Olá no Hive.</span><span class="sxs-lookup"><span data-stu-id="1de05-152">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="1de05-153">dados de saudação são deixados no local original hello.</span><span class="sxs-lookup"><span data-stu-id="1de05-153">hello data is left in hello original location.</span></span>

    * <span data-ttu-id="1de05-154">`ROW FORMAT`-Como dados de saudação são formatados.</span><span class="sxs-lookup"><span data-stu-id="1de05-154">`ROW FORMAT` - How hello data is formatted.</span></span> <span data-ttu-id="1de05-155">Nesse caso, os campos de saudação em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="1de05-155">In this case, hello fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="1de05-156">`STORED AS TEXTFILE LOCATION`-Onde Olá dados são armazenados e em qual formato de arquivo.</span><span class="sxs-lookup"><span data-stu-id="1de05-156">`STORED AS TEXTFILE LOCATION` - Where hello data is stored and in what file format.</span></span>

    * <span data-ttu-id="1de05-157">`SELECT`-Seleciona uma contagem de todas as linhas em que coluna **t4** contém valor Olá **[Erro]**.</span><span class="sxs-lookup"><span data-stu-id="1de05-157">`SELECT` - Selects a count of all rows where column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="1de05-158">Essa consulta deve retornar um valor de **3**, já que existem três linhas que contêm esse valor.</span><span class="sxs-lookup"><span data-stu-id="1de05-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="1de05-159">`INPUT__FILE__NAME LIKE '%.log'`-Hive tentativas tooapply Olá esquema tooall arquivos Olá diretório.</span><span class="sxs-lookup"><span data-stu-id="1de05-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="1de05-160">Nesse caso, o diretório de saudação contém arquivos que não correspondem ao esquema de saudação.</span><span class="sxs-lookup"><span data-stu-id="1de05-160">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="1de05-161">dados de lixo tooprevent nos resultados de hello, essa instrução informa Hive que só deve retornar dados de arquivos que terminam em. log.</span><span class="sxs-lookup"><span data-stu-id="1de05-161">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="1de05-162">Tabelas externas devem ser usadas quando você espera Olá toobe de dados subjacentes atualizado por uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="1de05-162">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="1de05-163">Por exemplo, um processo de upload de dados automatizado ou uma operação MapReduce.</span><span class="sxs-lookup"><span data-stu-id="1de05-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="1de05-164">Descartar uma tabela externa **não** excluir dados hello, definição de tabela Olá somente.</span><span class="sxs-lookup"><span data-stu-id="1de05-164">Dropping an external table does **not** delete hello data, only hello table definition.</span></span>

    <span data-ttu-id="1de05-165">saudação de saída desse comando é semelhante toohello seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="1de05-165">hello output of this command is similar toohello following text:</span></span>

        INFO  : Tez session hasn't been created yet. Opening session
        INFO  :

        INFO  : Status: Running (Executing on YARN cluster with App id application_1443698635933_0001)

        INFO  : Map 1: -/-      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0/1      Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 0(+1)/1  Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0/1
        INFO  : Map 1: 1/1      Reducer 2: 0(+1)/1
        INFO  : Map 1: 1/1      Reducer 2: 1/1
        +----------+--------+--+
        |   sev    | count  |
        +----------+--------+--+
        | [ERROR]  | 3      |
        +----------+--------+--+
        1 row selected (47.351 seconds)

5. <span data-ttu-id="1de05-166">tooexit Beeline, use `!exit`.</span><span class="sxs-lookup"><span data-stu-id="1de05-166">tooexit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="1de05-167"><a id="file"></a>Use Beeline toorun um arquivo de estilo</span><span class="sxs-lookup"><span data-stu-id="1de05-167"><a id="file"></a>Use Beeline toorun a HiveQL file</span></span>

<span data-ttu-id="1de05-168">Use Olá etapas toocreate um arquivo, em seguida, executá-lo usando Beeline a seguir.</span><span class="sxs-lookup"><span data-stu-id="1de05-168">Use hello following steps toocreate a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="1de05-169">Comando de uso a seguir de saudação toocreate um arquivo chamado **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="1de05-169">Use hello following command toocreate a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="1de05-170">Use Olá depois do texto como conteúdo de saudação do arquivo hello.</span><span class="sxs-lookup"><span data-stu-id="1de05-170">Use hello following text as hello contents of hello file.</span></span> <span data-ttu-id="1de05-171">Essa consulta cria uma nova tabela 'interna' chamada **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="1de05-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="1de05-172">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="1de05-172">These statements perform hello following actions:</span></span>

    * <span data-ttu-id="1de05-173">**Criar tabela IF NOT EXISTS** -se a tabela de saudação ainda não existir, ele será criado.</span><span class="sxs-lookup"><span data-stu-id="1de05-173">**CREATE TABLE IF NOT EXISTS** - If hello table does not already exist, it is created.</span></span> <span data-ttu-id="1de05-174">Desde Olá **externo** palavra-chave não for usada, essa instrução cria uma tabela interna.</span><span class="sxs-lookup"><span data-stu-id="1de05-174">Since hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="1de05-175">Tabelas internas são armazenadas no data warehouse do hello Hive e são totalmente gerenciadas pelo Hive.</span><span class="sxs-lookup"><span data-stu-id="1de05-175">Internal tables are stored in hello Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="1de05-176">**ARMAZENADOS como ORC** -armazena dados de saudação em formato de linha de otimização Colunar (ORC).</span><span class="sxs-lookup"><span data-stu-id="1de05-176">**STORED AS ORC** - Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="1de05-177">O formato ORC é altamente otimizado e eficiente para o armazenamento de dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="1de05-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="1de05-178">**INSERT OVERWRITE ... Selecione** -seleciona linhas de saudação **log4jLogs** tabela que contém **[Erro]**, em seguida, insere Olá dados em hello **em decorrência** tabela.</span><span class="sxs-lookup"><span data-stu-id="1de05-178">**INSERT OVERWRITE ... SELECT** - Selects rows from hello **log4jLogs** table that contain **[ERROR]**, then inserts hello data into hello **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="1de05-179">Ao contrário das tabelas externas, descartar uma tabela interna exclui dados subjacentes Olá também.</span><span class="sxs-lookup"><span data-stu-id="1de05-179">Unlike external tables, dropping an internal table deletes hello underlying data as well.</span></span>

3. <span data-ttu-id="1de05-180">arquivo de saudação toosave, use **Ctrl**+**x**, em seguida, digite **Y**e, finalmente, **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1de05-180">toosave hello file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="1de05-181">Olá usar arquivo de saudação toorun usando Beeline a seguir:</span><span class="sxs-lookup"><span data-stu-id="1de05-181">Use hello following toorun hello file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="1de05-182">Olá `-i` parâmetro Beeline é iniciado, executa Olá instruções no arquivo de query.hql hello.</span><span class="sxs-lookup"><span data-stu-id="1de05-182">hello `-i` parameter starts Beeline, runs hello statements in hello query.hql file.</span></span> <span data-ttu-id="1de05-183">Após a conclusão da consulta hello, chegam Olá `jdbc:hive2://headnodehost:10001/>` prompt.</span><span class="sxs-lookup"><span data-stu-id="1de05-183">Once hello query completes, you arrive at hello `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="1de05-184">Você também pode executar um arquivo usando Olá `-f` parâmetro, que será encerrado Beeline após a conclusão da consulta de saudação.</span><span class="sxs-lookup"><span data-stu-id="1de05-184">You can also run a file using hello `-f` parameter, which exits Beeline after hello query completes.</span></span>

5. <span data-ttu-id="1de05-185">tooverify Olá **em decorrência** tabela foi criada, use Olá após a instrução tooreturn todos Olá linhas de **em decorrência**:</span><span class="sxs-lookup"><span data-stu-id="1de05-185">tooverify that hello **errorLogs** table was created, use hello following statement tooreturn all hello rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="1de05-186">Três linhas de dados devem ser devolvidas, todas contendo **[ERROR]** na coluna t4:</span><span class="sxs-lookup"><span data-stu-id="1de05-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="1de05-187"><a id="remote"></a>Usar o Beeline remotamente</span><span class="sxs-lookup"><span data-stu-id="1de05-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="1de05-188">Se você tiver Beeline instalado localmente, ou são usá-lo por meio de uma imagem do Docker como [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), você deve usar o hello parâmetros a seguir:</span><span class="sxs-lookup"><span data-stu-id="1de05-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use hello following parameters:</span></span>

* <span data-ttu-id="1de05-189">__Cadeia de conexão__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="1de05-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="1de05-190">__Nome de logon do cluster__: `-n admin`</span><span class="sxs-lookup"><span data-stu-id="1de05-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="1de05-191">__Senha de logon do cluster__ `-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="1de05-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="1de05-192">Substituir saudação `clustername` na cadeia de caracteres de conexão de saudação com nome de saudação do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1de05-192">Replace hello `clustername` in hello connection string with hello name of your HDInsight cluster.</span></span>

<span data-ttu-id="1de05-193">Substituir `admin` com o nome de saudação do logon de cluster e substituir `password` com senha Olá para o seu logon de cluster.</span><span class="sxs-lookup"><span data-stu-id="1de05-193">Replace `admin` with hello name of your cluster login, and replace `password` with hello password for your cluster login.</span></span>

## <span data-ttu-id="1de05-194"><a id="sparksql"></a>Usar Beeline com Spark</span><span class="sxs-lookup"><span data-stu-id="1de05-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="1de05-195">Spark fornece sua própria implementação de HiveServer2, que frequentemente mencionado como tooas Olá Spark Thrift servidor.</span><span class="sxs-lookup"><span data-stu-id="1de05-195">Spark provides its own implementation of HiveServer2, which is often refered tooas hello Spark Thrift server.</span></span> <span data-ttu-id="1de05-196">Esse serviço usa consultas de tooresolve Spark SQL em vez de Hive e pode fornecer melhor desempenho, dependendo da consulta.</span><span class="sxs-lookup"><span data-stu-id="1de05-196">This service uses Spark SQL tooresolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="1de05-197">servidor de Spark Thrift toohello tooconnect de um Spark no HDInsight cluster, use porta `10002` em vez de `10001`.</span><span class="sxs-lookup"><span data-stu-id="1de05-197">tooconnect toohello Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="1de05-198">Por exemplo: `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="1de05-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1de05-199">servidor do Spark Thrift Olá é não diretamente acessível via Olá da internet.</span><span class="sxs-lookup"><span data-stu-id="1de05-199">hello Spark Thrift server is not directly accessible over hello internet.</span></span> <span data-ttu-id="1de05-200">Somente pode se conectar a tooit de uma sessão SSH ou dentro Olá mesma rede Virtual do Azure como Olá cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1de05-200">You can only connect tooit from an SSH session or inside hello same Azure Virtual Network as hello HDInsight cluster.</span></span>

## <span data-ttu-id="1de05-201"><a id="summary"></a><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1de05-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="1de05-202">Para obter mais informações sobre o Hive no HDInsight, consulte Olá documento a seguir:</span><span class="sxs-lookup"><span data-stu-id="1de05-202">For more general information on Hive in HDInsight, see hello following document:</span></span>

* [<span data-ttu-id="1de05-203">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="1de05-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="1de05-204">Para obter mais informações sobre outras maneiras que você pode trabalhar com Hadoop no HDInsight, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1de05-204">For more information on other ways you can work with Hadoop on HDInsight, see hello following documents:</span></span>

* [<span data-ttu-id="1de05-205">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="1de05-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="1de05-206">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="1de05-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="1de05-207">Se você estiver usando Tez com Hive, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1de05-207">If you are using Tez with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="1de05-208">Use Olá Tez UI no HDInsight baseados no Windows</span><span class="sxs-lookup"><span data-stu-id="1de05-208">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="1de05-209">Use Olá exibição Ambari Tez no HDInsight baseados em Linux</span><span class="sxs-lookup"><span data-stu-id="1de05-209">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/


[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md

[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html


[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md


[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx
