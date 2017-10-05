---
title: "Usar o Beeline com o Apache Hive – Azure HDInsight | Microsoft Docs"
description: "Aprenda a usar o cliente Beeline para executar consultas Hive com Hadoop no HDInsight. Beeline é um utilitário para trabalhar com HiveServer2 sobre JDBC."
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
ms.openlocfilehash: 153044aafa3a67ee85bb1997beb821777c938563
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-the-beeline-client-with-apache-hive"></a><span data-ttu-id="00bee-105">Usar o cliente Beeline com o Apache Hive</span><span class="sxs-lookup"><span data-stu-id="00bee-105">Use the Beeline client with Apache Hive</span></span>

<span data-ttu-id="00bee-106">Saiba como usar o [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) para executar consultas Hive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00bee-106">Learn how to use [Beeline](https://cwiki.apache.org/confluence/display/Hive/HiveServer2+Clients#HiveServer2Clients-Beeline–NewCommandLineShell) to run Hive queries on HDInsight.</span></span>

<span data-ttu-id="00bee-107">O Beeline é um cliente Hive que está incluído em nós principais do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00bee-107">Beeline is a Hive client that is included on the head nodes of your HDInsight cluster.</span></span> <span data-ttu-id="00bee-108">O Beeline usa o JDBC para se conectar ao HiveServer2, um serviço hospedado em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00bee-108">Beeline uses JDBC to connect to HiveServer2, a service hosted on your HDInsight cluster.</span></span> <span data-ttu-id="00bee-109">Você também pode usar o Beeline para acessar remotamente o Hive no HDInsight pela internet.</span><span class="sxs-lookup"><span data-stu-id="00bee-109">You can also use Beeline to access Hive on HDInsight remotely over the internet.</span></span> <span data-ttu-id="00bee-110">A tabela a seguir fornece as cadeias de caracteres de conexão para uso com o Beeline:</span><span class="sxs-lookup"><span data-stu-id="00bee-110">The following table provides connection strings for use with Beeline:</span></span>

| <span data-ttu-id="00bee-111">De que local você executa o Beeline</span><span class="sxs-lookup"><span data-stu-id="00bee-111">Where you run Beeline from</span></span> | <span data-ttu-id="00bee-112">parâmetros</span><span class="sxs-lookup"><span data-stu-id="00bee-112">Parameters</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00bee-113">Uma conexão SSH para um nó principal ou nó de borda</span><span class="sxs-lookup"><span data-stu-id="00bee-113">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
| <span data-ttu-id="00bee-114">Fora do cluster</span><span class="sxs-lookup"><span data-stu-id="00bee-114">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

> [!NOTE]
> <span data-ttu-id="00bee-115">Substitua `admin` pela conta de logon do cluster de seu cluster.</span><span class="sxs-lookup"><span data-stu-id="00bee-115">Replace `admin` with the cluster login account for your cluster.</span></span>
>
> <span data-ttu-id="00bee-116">Substitua `password` pela senha da conta de logon do cluster.</span><span class="sxs-lookup"><span data-stu-id="00bee-116">Replace `password` with the password for the cluster login account.</span></span>
>
> <span data-ttu-id="00bee-117">Substitua `clustername` pelo nome do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00bee-117">Replace `clustername` with the name of your HDInsight cluster.</span></span>

## <span data-ttu-id="00bee-118"><a id="prereq"></a>Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="00bee-118"><a id="prereq"></a>Prerequisites</span></span>

* <span data-ttu-id="00bee-119">Um cluster do Hadoop no HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="00bee-119">A Linux-based Hadoop on HDInsight cluster.</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="00bee-120">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="00bee-120">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="00bee-121">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="00bee-121">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

* <span data-ttu-id="00bee-122">Um cliente SSH ou um cliente Beeline local.</span><span class="sxs-lookup"><span data-stu-id="00bee-122">An SSH client or a local Beeline client.</span></span> <span data-ttu-id="00bee-123">A maioria das etapas neste documento pressupõe que você está usando o Beeline em uma sessão SSH para o cluster.</span><span class="sxs-lookup"><span data-stu-id="00bee-123">Most of the steps in this document assume that you are using Beeline from an SSH session to the cluster.</span></span> <span data-ttu-id="00bee-124">Para saber mais sobre como executar o Beeline fora do cluster, veja a seção [Usar o Beeline remotamente](#remote).</span><span class="sxs-lookup"><span data-stu-id="00bee-124">For information on running Beeline from outside the cluster, see the [use Beeline remotely](#remote) section.</span></span>

    <span data-ttu-id="00bee-125">Para saber mais sobre como usar SSH, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="00bee-125">For more information on using SSH, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

## <span data-ttu-id="00bee-126"><a id="beeline"></a>Usar o Beeline</span><span class="sxs-lookup"><span data-stu-id="00bee-126"><a id="beeline"></a>Use Beeline</span></span>

1. <span data-ttu-id="00bee-127">Ao iniciar o Beeline, você deve fornecer uma cadeia de conexão para HiveServer2 em seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00bee-127">When starting Beeline, you must provide a connection string for HiveServer2 on your HDInsight cluster.</span></span> <span data-ttu-id="00bee-128">Para executar o comando de fora do cluster, você também deverá fornecer o nome de conta de logon do cluster (padrão `admin`) e a senha.</span><span class="sxs-lookup"><span data-stu-id="00bee-128">To run the command from outside the cluster, you must also provide the cluster login account name (default `admin`) and password.</span></span> <span data-ttu-id="00bee-129">Use a tabela a seguir para localizar o formato da cadeia de conexão e os parâmetros a serem usados:</span><span class="sxs-lookup"><span data-stu-id="00bee-129">Use the following table to find the connection string format and parameters to use:</span></span>

    | <span data-ttu-id="00bee-130">De que local você executa o Beeline</span><span class="sxs-lookup"><span data-stu-id="00bee-130">Where you run Beeline from</span></span> | <span data-ttu-id="00bee-131">parâmetros</span><span class="sxs-lookup"><span data-stu-id="00bee-131">Parameters</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="00bee-132">Uma conexão SSH para um nó principal ou nó de borda</span><span class="sxs-lookup"><span data-stu-id="00bee-132">An SSH connection to a headnode or edge node</span></span> | `-u 'jdbc:hive2://headnodehost:10001/;transportMode=http'` |
    | <span data-ttu-id="00bee-133">Fora do cluster</span><span class="sxs-lookup"><span data-stu-id="00bee-133">Outside the cluster</span></span> | `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2' -n admin -p password` |

    <span data-ttu-id="00bee-134">Por exemplo, o comando a seguir pode ser usado para iniciar o Beeline em uma sessão SSH para o cluster:</span><span class="sxs-lookup"><span data-stu-id="00bee-134">For example, the following command can be used to start Beeline from an SSH session to the cluster:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http'
    ```

    <span data-ttu-id="00bee-135">Esse comando inicia o cliente Beeline e conecta-se ao HiveServer2 no nó de cabeçalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="00bee-135">This command starts the Beeline client, and connects to HiveServer2 on the cluster head node.</span></span> <span data-ttu-id="00bee-136">Quando o comando for concluído, você chegará a um prompt `jdbc:hive2://headnodehost:10001/>`.</span><span class="sxs-lookup"><span data-stu-id="00bee-136">Once the command completes, you arrive at a `jdbc:hive2://headnodehost:10001/>` prompt.</span></span>

2. <span data-ttu-id="00bee-137">Os comandos Beeline normalmente começam com um caractere `!`, por exemplo, `!help` exibe a ajuda.</span><span class="sxs-lookup"><span data-stu-id="00bee-137">Beeline commands begin with a `!` character, for example `!help` displays help.</span></span> <span data-ttu-id="00bee-138">No entanto, o `!` pode ser omitido para alguns comandos.</span><span class="sxs-lookup"><span data-stu-id="00bee-138">However the `!` can be omitted for some commands.</span></span> <span data-ttu-id="00bee-139">Por exemplo, `help` também funciona.</span><span class="sxs-lookup"><span data-stu-id="00bee-139">For example, `help` also works.</span></span>

    <span data-ttu-id="00bee-140">Há um `!sql`, que é usado para executar instruções HiveQL.</span><span class="sxs-lookup"><span data-stu-id="00bee-140">There is a `!sql`, which is used to execute HiveQL statements.</span></span> <span data-ttu-id="00bee-141">No entanto, o HiveQL é tão usado que é possível omitir o `!sql`anterior.</span><span class="sxs-lookup"><span data-stu-id="00bee-141">However, HiveQL is so commonly used that you can omit the preceding `!sql`.</span></span> <span data-ttu-id="00bee-142">As duas instruções a seguir são equivalentes:</span><span class="sxs-lookup"><span data-stu-id="00bee-142">The following two statements are equivalent:</span></span>

    ```hiveql
    !sql show tables;
    show tables;
    ```

    <span data-ttu-id="00bee-143">Em um novo cluster, somente uma tabela é listada: **hivesampletable**.</span><span class="sxs-lookup"><span data-stu-id="00bee-143">On a new cluster, only one table is listed: **hivesampletable**.</span></span>

3. <span data-ttu-id="00bee-144">Use o comando a seguir para exibir o esquema para a hivesampletable:</span><span class="sxs-lookup"><span data-stu-id="00bee-144">Use the following command to display the schema for the hivesampletable:</span></span>

    ```hiveql
    describe hivesampletable;
    ```

    <span data-ttu-id="00bee-145">Esse comando retorna as informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="00bee-145">This command returns the following information:</span></span>

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

    <span data-ttu-id="00bee-146">Essas informações descrevem as colunas na tabela.</span><span class="sxs-lookup"><span data-stu-id="00bee-146">This information describes the columns in the table.</span></span> <span data-ttu-id="00bee-147">Embora possamos executar algumas consultas nestes dados, vamos criar uma nova tabela para demonstrarmos como carregar os dados no Hive e como aplicar um esquema.</span><span class="sxs-lookup"><span data-stu-id="00bee-147">While we could perform some queries against this data, let's instead create a brand new table to demonstrate how to load data into Hive and apply a schema.</span></span>

4. <span data-ttu-id="00bee-148">Insira as instruções a seguir para criar uma tabela chamada **log4jLogs** usando os dados de exemplo fornecidos com o cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="00bee-148">Enter the following statements to create a table named **log4jLogs** by using sample data provided with the HDInsight cluster:</span></span>

    ```hiveql
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION 'wasb:///example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;
    ```

    <span data-ttu-id="00bee-149">As instruções executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="00bee-149">These statements perform the following actions:</span></span>

    * <span data-ttu-id="00bee-150">`DROP TABLE` – Se a tabela existir, ela será excluída.</span><span class="sxs-lookup"><span data-stu-id="00bee-150">`DROP TABLE` - If the table exists, it is deleted.</span></span>

    * <span data-ttu-id="00bee-151">`CREATE EXTERNAL TABLE` – Cria uma tabela **externa** no Hive.</span><span class="sxs-lookup"><span data-stu-id="00bee-151">`CREATE EXTERNAL TABLE` - Creates an **external** table in Hive.</span></span> <span data-ttu-id="00bee-152">Tabelas externas só armazenam a definição da tabela no Hive.</span><span class="sxs-lookup"><span data-stu-id="00bee-152">External tables only store the table definition in Hive.</span></span> <span data-ttu-id="00bee-153">Os dados são mantidos no local original.</span><span class="sxs-lookup"><span data-stu-id="00bee-153">The data is left in the original location.</span></span>

    * <span data-ttu-id="00bee-154">`ROW FORMAT` – o modo como os dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="00bee-154">`ROW FORMAT` - How the data is formatted.</span></span> <span data-ttu-id="00bee-155">Nesse caso, os campos em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="00bee-155">In this case, the fields in each log are separated by a space.</span></span>

    * <span data-ttu-id="00bee-156">`STORED AS TEXTFILE LOCATION` – O local em que os dados são armazenados e em qual formato de arquivo.</span><span class="sxs-lookup"><span data-stu-id="00bee-156">`STORED AS TEXTFILE LOCATION` - Where the data is stored and in what file format.</span></span>

    * <span data-ttu-id="00bee-157">`SELECT` – Seleciona uma contagem de todas as linhas em que a coluna **t4** contém o valor **[ERROR]**.</span><span class="sxs-lookup"><span data-stu-id="00bee-157">`SELECT` - Selects a count of all rows where column **t4** contains the value **[ERROR]**.</span></span> <span data-ttu-id="00bee-158">Essa consulta deve retornar um valor de **3**, já que existem três linhas que contêm esse valor.</span><span class="sxs-lookup"><span data-stu-id="00bee-158">This query returns a value of **3** as there are three rows that contain this value.</span></span>

    * <span data-ttu-id="00bee-159">`INPUT__FILE__NAME LIKE '%.log'` – O Hive tenta aplicar o esquema a todos os arquivos no diretório.</span><span class="sxs-lookup"><span data-stu-id="00bee-159">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts to apply the schema to all files in the directory.</span></span> <span data-ttu-id="00bee-160">Nesse caso, o diretório contém arquivos que não correspondem ao esquema.</span><span class="sxs-lookup"><span data-stu-id="00bee-160">In this case, the directory contains files that do not match the schema.</span></span> <span data-ttu-id="00bee-161">Para evitar dados incorretos nos resultados, essa instrução informa ao Hive que devemos retornar apenas dados de arquivos que terminam em .log.</span><span class="sxs-lookup"><span data-stu-id="00bee-161">To prevent garbage data in the results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

  > [!NOTE]
  > <span data-ttu-id="00bee-162">As tabelas externas devem ser usadas quando você espera que os dados subjacentes sejam atualizados por uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="00bee-162">External tables should be used when you expect the underlying data to be updated by an external source.</span></span> <span data-ttu-id="00bee-163">Por exemplo, um processo de upload de dados automatizado ou uma operação MapReduce.</span><span class="sxs-lookup"><span data-stu-id="00bee-163">For example, an automated data upload process or a MapReduce operation.</span></span>
  >
  > <span data-ttu-id="00bee-164">Remover uma tabela externa **não** exclui os dados, somente a definição de tabela.</span><span class="sxs-lookup"><span data-stu-id="00bee-164">Dropping an external table does **not** delete the data, only the table definition.</span></span>

    <span data-ttu-id="00bee-165">A saída desse comando é semelhante ao texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="00bee-165">The output of this command is similar to the following text:</span></span>

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

5. <span data-ttu-id="00bee-166">Para sair do Beeline, use `!exit`.</span><span class="sxs-lookup"><span data-stu-id="00bee-166">To exit Beeline, use `!exit`.</span></span>

## <span data-ttu-id="00bee-167"><a id="file"></a>Usar o Beeline para executar um arquivo HiveQL</span><span class="sxs-lookup"><span data-stu-id="00bee-167"><a id="file"></a>Use Beeline to run a HiveQL file</span></span>

<span data-ttu-id="00bee-168">Use as etapas a seguir para criar um arquivo e  executá-lo usando o Beeline.</span><span class="sxs-lookup"><span data-stu-id="00bee-168">Use the following steps to create a file, then run it using Beeline.</span></span>

1. <span data-ttu-id="00bee-169">Use o comando a seguir para criar um novo arquivo chamado **query.hql**:</span><span class="sxs-lookup"><span data-stu-id="00bee-169">Use the following command to create a file named **query.hql**:</span></span>

    ```bash
    nano query.hql
    ```

2. <span data-ttu-id="00bee-170">Use o texto a seguir como conteúdo do arquivo.</span><span class="sxs-lookup"><span data-stu-id="00bee-170">Use the following text as the contents of the file.</span></span> <span data-ttu-id="00bee-171">Essa consulta cria uma nova tabela 'interna' chamada **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="00bee-171">This query creates a new 'internal' table named **errorLogs**:</span></span>

    ```hiveql
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log';
    ```

    <span data-ttu-id="00bee-172">As instruções executam as seguintes ações:</span><span class="sxs-lookup"><span data-stu-id="00bee-172">These statements perform the following actions:</span></span>

    * <span data-ttu-id="00bee-173">**CREATE TABLE IF NOT EXISTS** – criará uma tabela, se ela ainda não existir.</span><span class="sxs-lookup"><span data-stu-id="00bee-173">**CREATE TABLE IF NOT EXISTS** - If the table does not already exist, it is created.</span></span> <span data-ttu-id="00bee-174">Uma vez que a palavra-chave **EXTERNAL** não é usada, essa instrução cria uma tabela interna.</span><span class="sxs-lookup"><span data-stu-id="00bee-174">Since the **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="00bee-175">As tabelas internas são armazenadas no data warehouse do Hive e totalmente gerenciadas por ele.</span><span class="sxs-lookup"><span data-stu-id="00bee-175">Internal tables are stored in the Hive data warehouse and are managed completely by Hive.</span></span>
    * <span data-ttu-id="00bee-176">**STORES AS ORC** : armazena os dados no formato ORC (Optimized Row Columnar).</span><span class="sxs-lookup"><span data-stu-id="00bee-176">**STORED AS ORC** - Stores the data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="00bee-177">O formato ORC é altamente otimizado e eficiente para o armazenamento de dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="00bee-177">ORC format is a highly optimized and efficient format for storing Hive data.</span></span>
    * <span data-ttu-id="00bee-178">**INSERT OVERWRITE ... SELECT** - seleciona linhas da tabela **log4jLogs** que contêm **[ERROR]** e insere os dados na tabela **errorLogs**.</span><span class="sxs-lookup"><span data-stu-id="00bee-178">**INSERT OVERWRITE ... SELECT** - Selects rows from the **log4jLogs** table that contain **[ERROR]**, then inserts the data into the **errorLogs** table.</span></span>

    > [!NOTE]
    > <span data-ttu-id="00bee-179">Diferentemente de tabelas externas, o descarte de uma tabela interna excluirá também os dados subjacentes.</span><span class="sxs-lookup"><span data-stu-id="00bee-179">Unlike external tables, dropping an internal table deletes the underlying data as well.</span></span>

3. <span data-ttu-id="00bee-180">Para salvar o arquivo, use **Ctrl**+**_X**, insira **Y** e, por fim, **Enter**.</span><span class="sxs-lookup"><span data-stu-id="00bee-180">To save the file, use **Ctrl**+**_X**, then enter **Y**, and finally **Enter**.</span></span>

4. <span data-ttu-id="00bee-181">Use o seguinte para executar o arquivo usando Beeline:</span><span class="sxs-lookup"><span data-stu-id="00bee-181">Use the following to run the file using Beeline:</span></span>

    ```bash
    beeline -u 'jdbc:hive2://headnodehost:10001/;transportMode=http' -i query.hql
    ```

    > [!NOTE]
    > <span data-ttu-id="00bee-182">O parâmetro `-i` inicia o Beeline e executa as instruções no arquivo query.hql.</span><span class="sxs-lookup"><span data-stu-id="00bee-182">The `-i` parameter starts Beeline, runs the statements in the query.hql file.</span></span> <span data-ttu-id="00bee-183">Quando a consulta for concluída, você verá um prompt `jdbc:hive2://headnodehost:10001/>`.</span><span class="sxs-lookup"><span data-stu-id="00bee-183">Once the query completes, you arrive at the `jdbc:hive2://headnodehost:10001/>` prompt.</span></span> <span data-ttu-id="00bee-184">Você também pode executar um arquivo usando o parâmetro `-f`, que fechará o Beeline após a conclusão da consulta.</span><span class="sxs-lookup"><span data-stu-id="00bee-184">You can also run a file using the `-f` parameter, which exits Beeline after the query completes.</span></span>

5. <span data-ttu-id="00bee-185">Para verificar se a tabela **errorLogs** foi criada, use a seguinte instrução para retornar todas as linhas de **errorLogs**:</span><span class="sxs-lookup"><span data-stu-id="00bee-185">To verify that the **errorLogs** table was created, use the following statement to return all the rows from **errorLogs**:</span></span>

    ```hiveql
    SELECT * from errorLogs;
    ```

    <span data-ttu-id="00bee-186">Três linhas de dados devem ser devolvidas, todas contendo **[ERROR]** na coluna t4:</span><span class="sxs-lookup"><span data-stu-id="00bee-186">Three rows of data should be returned, all containing **[ERROR]** in column t4:</span></span>

        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | errorlogs.t1  | errorlogs.t2  | errorlogs.t3  | errorlogs.t4  | errorlogs.t5  | errorlogs.t6  | errorlogs.t7  |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        | 2012-02-03    | 18:35:34      | SampleClass0  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 18:55:54      | SampleClass1  | [ERROR]       | incorrect     | id            |               |
        | 2012-02-03    | 19:25:27      | SampleClass4  | [ERROR]       | incorrect     | id            |               |
        +---------------+---------------+---------------+---------------+---------------+---------------+---------------+--+
        3 rows selected (1.538 seconds)

## <span data-ttu-id="00bee-187"><a id="remote"></a>Usar o Beeline remotamente</span><span class="sxs-lookup"><span data-stu-id="00bee-187"><a id="remote"></a>Use Beeline remotely</span></span>

<span data-ttu-id="00bee-188">Se você tiver Beeline instalado localmente ou são usá-lo por meio de uma imagem de Docker como [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), você deverá usar os seguintes parâmetros:</span><span class="sxs-lookup"><span data-stu-id="00bee-188">If you have Beeline installed locally, or are using it through a Docker image such as [sutoiku/beeline](https://hub.docker.com/r/sutoiku/beeline/), you must use the following parameters:</span></span>

* <span data-ttu-id="00bee-189">__Cadeia de conexão__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span><span class="sxs-lookup"><span data-stu-id="00bee-189">__Connection string__: `-u 'jdbc:hive2://clustername.azurehdinsight.net:443/;ssl=true;transportMode=http;httpPath=/hive2'`</span></span>

* <span data-ttu-id="00bee-190">__Nome de logon do cluster__: `-n admin`</span><span class="sxs-lookup"><span data-stu-id="00bee-190">__Cluster login name__: `-n admin`</span></span>

* <span data-ttu-id="00bee-191">__Senha de logon do cluster__ `-p 'password'`</span><span class="sxs-lookup"><span data-stu-id="00bee-191">__Cluster login password__ `-p 'password'`</span></span>

<span data-ttu-id="00bee-192">Substitua o `clustername` na cadeia de conexão pelo nome do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00bee-192">Replace the `clustername` in the connection string with the name of your HDInsight cluster.</span></span>

<span data-ttu-id="00bee-193">Substitua `admin` pelo nome de logon do cluster e substitua `password` pela senha para o logon do cluster.</span><span class="sxs-lookup"><span data-stu-id="00bee-193">Replace `admin` with the name of your cluster login, and replace `password` with the password for your cluster login.</span></span>

## <span data-ttu-id="00bee-194"><a id="sparksql"></a>Usar Beeline com Spark</span><span class="sxs-lookup"><span data-stu-id="00bee-194"><a id="sparksql"></a>Use Beeline with Spark</span></span>

<span data-ttu-id="00bee-195">O Spark fornece sua própria implementação de HiveServer2, que geralmente é referenciado como o servidor Spark Thrift.</span><span class="sxs-lookup"><span data-stu-id="00bee-195">Spark provides its own implementation of HiveServer2, which is often refered to as the Spark Thrift server.</span></span> <span data-ttu-id="00bee-196">Esse serviço usa Spark SQL para resolver consultas em vez de Hive e pode fornecer um desempenho melhor, dependendo da consulta.</span><span class="sxs-lookup"><span data-stu-id="00bee-196">This service uses Spark SQL to resolve queries instead of Hive, and may provide better performance depending on your query.</span></span>

<span data-ttu-id="00bee-197">Para se conectar ao servidor Spark Thrift de um Spark no cluster HDInsight, use a porta `10002` em vez de `10001`.</span><span class="sxs-lookup"><span data-stu-id="00bee-197">To connect to the Spark Thrift server of a Spark on HDInsight cluster, use port `10002` instead of `10001`.</span></span> <span data-ttu-id="00bee-198">Por exemplo: `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span><span class="sxs-lookup"><span data-stu-id="00bee-198">For example, `beeline -u 'jdbc:hive2://headnodehost:10002/;transportMode=http'`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="00bee-199">O servidor Spark Thrift não pode ser acessado diretamente pela internet.</span><span class="sxs-lookup"><span data-stu-id="00bee-199">The Spark Thrift server is not directly accessible over the internet.</span></span> <span data-ttu-id="00bee-200">Você pode conectar-se a ele somente partir de uma sessão SSH ou dentro da mesma Rede Virtual do Azure que o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="00bee-200">You can only connect to it from an SSH session or inside the same Azure Virtual Network as the HDInsight cluster.</span></span>

## <span data-ttu-id="00bee-201"><a id="summary"></a><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="00bee-201"><a id="summary"></a><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="00bee-202">Para obter mais informações gerais sobre como usar o Hive no HDInsight, veja o seguinte documento:</span><span class="sxs-lookup"><span data-stu-id="00bee-202">For more general information on Hive in HDInsight, see the following document:</span></span>

* [<span data-ttu-id="00bee-203">Usar o Hive com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="00bee-203">Use Hive with Hadoop on HDInsight</span></span>](hdinsight-use-hive.md)

<span data-ttu-id="00bee-204">Para saber mais sobre outras maneiras pelas quais você pode trabalhar com o Hadoop no HDInsight, veja os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="00bee-204">For more information on other ways you can work with Hadoop on HDInsight, see the following documents:</span></span>

* [<span data-ttu-id="00bee-205">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="00bee-205">Use Pig with Hadoop on HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="00bee-206">Usar o MapReduce com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="00bee-206">Use MapReduce with Hadoop on HDInsight</span></span>](hdinsight-use-mapreduce.md)

<span data-ttu-id="00bee-207">Se você estiver usando o Tez com o Hive, consulte os seguintes documentos:</span><span class="sxs-lookup"><span data-stu-id="00bee-207">If you are using Tez with Hive, see the following documents:</span></span>

* [<span data-ttu-id="00bee-208">Usar a interface de usuário do Tez no HDInsight baseado em Windows</span><span class="sxs-lookup"><span data-stu-id="00bee-208">Use the Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)
* [<span data-ttu-id="00bee-209">Usar a exibição de Ambari Tez no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="00bee-209">Use the Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

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
