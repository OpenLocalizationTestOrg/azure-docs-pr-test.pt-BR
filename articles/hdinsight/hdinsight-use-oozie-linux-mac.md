---
title: fluxos de trabalho do aaaUse Oozie Hadoop em HDInsight baseados em Linux | Microsoft Docs
description: Usar o Oozie do Hadoop no HDInsight baseado em Linux. Saiba como toodefine um fluxo de trabalho do Oozie e enviar um trabalho de Oozie.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d7603471-5076-43d1-8b9a-dbc4e366ce5d
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 08/04/2017
ms.author: larryfr
ms.openlocfilehash: cb5682837543312621e3424b7a9341b5d2a00bf8
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="1c177-104">Usar Oozie com toodefine Hadoop e executar um fluxo de trabalho no HDInsight baseados em Linux</span><span class="sxs-lookup"><span data-stu-id="1c177-104">Use Oozie with Hadoop toodefine and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="1c177-105">Saiba como toouse Apache Oozie com Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c177-105">Learn how toouse Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="1c177-106">O Apache Oozie é um sistema de fluxo de trabalho/coordenação que gerencia trabalhos do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="1c177-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="1c177-107">Oozie é integrado com pilha de Hadoop hello e dá suporte a saudação trabalhos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-107">Oozie is integrated with hello Hadoop stack, and it supports hello following jobs:</span></span>

* <span data-ttu-id="1c177-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="1c177-108">Apache MapReduce</span></span>
* <span data-ttu-id="1c177-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="1c177-109">Apache Pig</span></span>
* <span data-ttu-id="1c177-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="1c177-110">Apache Hive</span></span>
* <span data-ttu-id="1c177-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="1c177-111">Apache Sqoop</span></span>

<span data-ttu-id="1c177-112">Oozie também pode ser tooschedule usado trabalhos que são tooa específicas do sistema, como programas de Java ou scripts de shell</span><span class="sxs-lookup"><span data-stu-id="1c177-112">Oozie can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="1c177-113">Outra opção para definir fluxos de trabalho com o HDInsight é uma Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="1c177-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="1c177-114">toolearn mais sobre o Azure Data Factory, consulte [usar o Pig e Hive com a fábrica de dados][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="1c177-114">toolearn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c177-115">O Oozie não está habilitado no HDInsight ingressado no domínio.</span><span class="sxs-lookup"><span data-stu-id="1c177-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="1c177-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="1c177-116">Prerequisites</span></span>

* <span data-ttu-id="1c177-117">**Um cluster hdinsight**: consulte [Introdução ao HDInsight no Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="1c177-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="1c177-118">etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux.</span><span class="sxs-lookup"><span data-stu-id="1c177-118">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="1c177-119">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="1c177-119">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="1c177-120">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="1c177-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="1c177-121">Fluxo de trabalho de exemplo</span><span class="sxs-lookup"><span data-stu-id="1c177-121">Example workflow</span></span>

<span data-ttu-id="1c177-122">fluxo de trabalho de saudação usado neste documento contém duas ações.</span><span class="sxs-lookup"><span data-stu-id="1c177-122">hello workflow used in this document contains two actions.</span></span> <span data-ttu-id="1c177-123">Ações são definições de tarefas, como Sqoop, Hive, MapReduce ou outro processo de execução:</span><span class="sxs-lookup"><span data-stu-id="1c177-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Diagrama de fluxo de trabalho][img-workflow-diagram]

1. <span data-ttu-id="1c177-125">Uma ação de Hive executa um script HiveQL tooextract registros de saudação **hivesampletable** incluído no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c177-125">A Hive action runs a HiveQL script tooextract records from hello **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="1c177-126">Cada linha de dados descreve uma visita de um dispositivo móvel específico.</span><span class="sxs-lookup"><span data-stu-id="1c177-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="1c177-127">formato de registro de saudação aparece semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-127">hello record format appears similar toohello following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="1c177-128">Olá usado neste documento de script do Hive contagens de visitas a saudação total para cada plataforma (como Android ou iPhone) e armazena Olá contagens tooa nova seção tabela.</span><span class="sxs-lookup"><span data-stu-id="1c177-128">hello Hive script used in this document counts hello total visits for each platform (such as Android or iPhone) and stores hello counts tooa new Hive table.</span></span>

    <span data-ttu-id="1c177-129">Para obter mais informações sobre o Hive, consulte [Usar o Hive com o HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="1c177-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="1c177-130">Uma ação de Sqoop exporta conteúdo Olá Olá nova tabela tooa tabela Hive em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1c177-130">A Sqoop action exports hello contents of hello new Hive table tooa table in an Azure SQL database.</span></span> <span data-ttu-id="1c177-131">Para saber mais sobre o Sqoop, confira [Usar o Hadoop Sqoop com o HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="1c177-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="1c177-132">Para versões com suporte do Oozie em clusters de HDInsight, consulte [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="1c177-132">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-hello-working-directory"></a><span data-ttu-id="1c177-133">Criar o diretório de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="1c177-133">Create hello working directory</span></span>

<span data-ttu-id="1c177-134">Oozie espera os recursos necessários para um trabalho toobe armazenada no hello mesmo diretório.</span><span class="sxs-lookup"><span data-stu-id="1c177-134">Oozie expects resources required for a job toobe stored in hello same directory.</span></span> <span data-ttu-id="1c177-135">Este exemplo usa **wasb:///tutorials/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="1c177-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="1c177-136">Nesse diretório e o diretório de dados de saudação que mantém Olá Hive tabela criada por este fluxo de trabalho, use Olá toocreate de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-136">Use hello following command toocreate this directory, and hello data directory that holds hello new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="1c177-137">Olá `-p` parâmetro faz com que todos os diretórios no hello caminho toobe criado.</span><span class="sxs-lookup"><span data-stu-id="1c177-137">hello `-p` parameter causes all directories in hello path toobe created.</span></span> <span data-ttu-id="1c177-138">Olá **dados** diretório é toohold usado dados usados por Olá **useooziewf.hql** script.</span><span class="sxs-lookup"><span data-stu-id="1c177-138">hello **data** directory is used toohold data used by hello **useooziewf.hql** script.</span></span>

<span data-ttu-id="1c177-139">Também execute Olá comando, o que garante que Oozie pode representar a conta de usuário ao executar trabalhos de Hive e Sqoop a seguir.</span><span class="sxs-lookup"><span data-stu-id="1c177-139">Also run hello following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="1c177-140">Substitua **NOME DE USUÁRIO** pelo seu nome de logon:</span><span class="sxs-lookup"><span data-stu-id="1c177-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="1c177-141">Você pode ignorar erros que o usuário Olá já é um membro de saudação `users` grupo.</span><span class="sxs-lookup"><span data-stu-id="1c177-141">You can ignore errors that hello user is already a member of hello `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="1c177-142">Adicionar um driver de banco de dados</span><span class="sxs-lookup"><span data-stu-id="1c177-142">Add a database driver</span></span>

<span data-ttu-id="1c177-143">Como esse fluxo de trabalho usa Sqoop tooexport dados tooSQL banco de dados, você deve fornecer que uma cópia do driver JDBC Olá usado tootalk tooSQL banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1c177-143">Since this workflow uses Sqoop tooexport data tooSQL Database, you must provide a copy of hello JDBC driver used tootalk tooSQL Database.</span></span> <span data-ttu-id="1c177-144">Use Olá após o comando toocopy-toohello diretório de trabalho:</span><span class="sxs-lookup"><span data-stu-id="1c177-144">Use hello following command toocopy it toohello working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="1c177-145">Se o fluxo de trabalho usados outros recursos, como um jar que contém um aplicativo de MapReduce, você precisaria tooadd esses recursos também.</span><span class="sxs-lookup"><span data-stu-id="1c177-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need tooadd these resources as well.</span></span>

## <a name="define-hello-hive-query"></a><span data-ttu-id="1c177-146">Definir a consulta de Hive Olá</span><span class="sxs-lookup"><span data-stu-id="1c177-146">Define hello Hive query</span></span>

<span data-ttu-id="1c177-147">Use Olá seguindo as etapas toocreate um script de estilo que define uma consulta, que é usada em um fluxo de trabalho do Oozie neste documento.</span><span class="sxs-lookup"><span data-stu-id="1c177-147">Use hello following steps toocreate a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="1c177-148">Conecte-se toohello cluster usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="1c177-148">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="1c177-149">Olá, comando a seguir é um exemplo de como usar o hello `ssh` comando.</span><span class="sxs-lookup"><span data-stu-id="1c177-149">hello following command is an example of using hello `ssh` command.</span></span> <span data-ttu-id="1c177-150">Substituir __nome de usuário__ com usuário SSH Olá cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-150">Replace __USERNAME__ with hello SSH user for hello cluster.</span></span> <span data-ttu-id="1c177-151">Substituir __CLUSTERNAME__ com o nome de saudação do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-151">Replace __CLUSTERNAME__ with hello name of hello HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="1c177-152">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="1c177-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="1c177-153">De Olá conexão SSH, use Olá comando toocreate um arquivo a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-153">From hello SSH connection, use hello following command toocreate a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="1c177-154">Depois de saudação nano editor é aberto, use Olá consulta a seguir como conteúdo de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="1c177-154">Once hello nano editor opens, use hello following query as hello contents of hello file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="1c177-155">Há duas variáveis usadas em script hello:</span><span class="sxs-lookup"><span data-stu-id="1c177-155">There are two variables used in hello script:</span></span>

    * <span data-ttu-id="1c177-156">**${hiveTableName}**: contém nome de saudação do hello tabela toobe criado</span><span class="sxs-lookup"><span data-stu-id="1c177-156">**${hiveTableName}**: contains hello name of hello table toobe created</span></span>

    * <span data-ttu-id="1c177-157">**${hiveDataFolder}**: contém arquivos de dados de Olá Olá local toostore para tabela Olá</span><span class="sxs-lookup"><span data-stu-id="1c177-157">**${hiveDataFolder}**: contains hello location toostore hello data files for hello table</span></span>

    <span data-ttu-id="1c177-158">arquivo de definição de fluxo de trabalho (. XML neste tutorial) Olá passa esses valores toothis script HiveQL em tempo de execução</span><span class="sxs-lookup"><span data-stu-id="1c177-158">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time</span></span>

4. <span data-ttu-id="1c177-159">editor de saudação tooexit, pressione Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="1c177-159">tooexit hello editor, press Ctrl-X.</span></span> <span data-ttu-id="1c177-160">Quando solicitado, selecione **Y** toosave Olá arquivo, em seguida, usar **Enter** toouse Olá **useooziewf.hql** nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="1c177-160">When prompted, select **Y** toosave hello file, then use **Enter** toouse hello **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="1c177-161">A seguir Olá use comandos toocopy **useooziewf.hql** muito**wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="1c177-161">Use hello following commands toocopy **useooziewf.hql** too**wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="1c177-162">Esses comandos armazenam Olá **useooziewf.hql** no arquivo em armazenamento Olá HDFS compatível com cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-162">These commands store hello **useooziewf.hql** file on hello HDFS-compatible storage for hello cluster.</span></span>

## <a name="define-hello-workflow"></a><span data-ttu-id="1c177-163">Definir o fluxo de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="1c177-163">Define hello workflow</span></span>

<span data-ttu-id="1c177-164">As definições de fluxos de trabalho do Oozie são escritas em hPDL (uma Linguagem de Definição de Processo XML).</span><span class="sxs-lookup"><span data-stu-id="1c177-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="1c177-165">Use Olá fluxo de trabalho de saudação de toodefine as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-165">Use hello following steps toodefine hello workflow:</span></span>

1. <span data-ttu-id="1c177-166">Use Olá toocreate instrução a seguir e editar um arquivo novo:</span><span class="sxs-lookup"><span data-stu-id="1c177-166">Use hello following statement toocreate and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="1c177-167">Uma vez Olá nano editor é aberta, digite Olá XML a seguir como o conteúdo do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="1c177-167">Once hello nano editor opens, enter hello following XML as hello file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start too= "RunHiveScript"/>
        <action name="RunHiveScript">
        <hive xmlns="uri:oozie:hive-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.job.queue.name</name>
                <value>${queueName}</value>
            </property>
            </configuration>
            <script>${hiveScript}</script>
            <param>hiveTableName=${hiveTableName}</param>
            <param>hiveDataFolder=${hiveDataFolder}</param>
        </hive>
        <ok to="RunSqoopExport"/>
        <error to="fail"/>
        </action>
        <action name="RunSqoopExport">
        <sqoop xmlns="uri:oozie:sqoop-action:0.2">
            <job-tracker>${jobTracker}</job-tracker>
            <name-node>${nameNode}</name-node>
            <configuration>
            <property>
                <name>mapred.compress.map.output</name>
                <value>true</value>
            </property>
            </configuration>
            <arg>export</arg>
            <arg>--connect</arg>
            <arg>${sqlDatabaseConnectionString}</arg>
            <arg>--table</arg>
            <arg>${sqlDatabaseTableName}</arg>
            <arg>--export-dir</arg>
            <arg>${hiveDataFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\t"</arg>
            <archive>sqljdbc41.jar</archive>
            </sqoop>
        <ok to="end"/>
        <error to="fail"/>
        </action>
        <kill name="fail">
        <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>
        <end name="end"/>
    </workflow-app>
    ```

    <span data-ttu-id="1c177-168">Há duas ações definidas no fluxo de trabalho hello:</span><span class="sxs-lookup"><span data-stu-id="1c177-168">There are two actions defined in hello workflow:</span></span>

   * <span data-ttu-id="1c177-169">**RunHiveScript**: essa ação é Olá iniciar ação e executa Olá **useooziewf.hql** script de Hive</span><span class="sxs-lookup"><span data-stu-id="1c177-169">**RunHiveScript**: This action is hello start action, and runs hello **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="1c177-170">**RunSqoopExport**: essa ação exporta dados de saudação criados a partir de tooSQL de script de Hive hello usando Sqoop de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1c177-170">**RunSqoopExport**: This action exports hello data created from hello Hive script tooSQL Database using Sqoop.</span></span> <span data-ttu-id="1c177-171">Esta ação é executada somente se hello **RunHiveScript** ação foi bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="1c177-171">This action only runs if hello **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="1c177-172">fluxo de trabalho Olá tem várias entradas, como `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="1c177-172">hello workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="1c177-173">Essas entradas são substituídas por valores usados na definição de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-173">These entries are replaced by values you use in hello job definition.</span></span> <span data-ttu-id="1c177-174">definição de trabalho Olá é criada neste documento.</span><span class="sxs-lookup"><span data-stu-id="1c177-174">hello job definition is created later in this document.</span></span>

     <span data-ttu-id="1c177-175">Saudação de Observação também `<archive>sqljdbc4.jar</arcive>` entrada hello Sqoop seção.</span><span class="sxs-lookup"><span data-stu-id="1c177-175">Also note hello `<archive>sqljdbc4.jar</arcive>` entry in hello Sqoop section.</span></span> <span data-ttu-id="1c177-176">Essa entrada instrui Oozie toomake neste arquivo disponível para Sqoop quando esta ação é executada.</span><span class="sxs-lookup"><span data-stu-id="1c177-176">This entry instructs Oozie toomake this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="1c177-177">Use Ctrl-X, em seguida, **Y** e **Enter** toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-177">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

4. <span data-ttu-id="1c177-178">Olá toocopy do comando de uso a seguir de saudação **. XML** arquivo muito**/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="1c177-178">Use hello following command toocopy hello **workflow.xml** file too**/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-hello-database"></a><span data-ttu-id="1c177-179">Criar banco de dados de saudação</span><span class="sxs-lookup"><span data-stu-id="1c177-179">Create hello database</span></span>

<span data-ttu-id="1c177-180">toocreate um banco de dados SQL do Azure, siga as etapas de Olá Olá [criar um banco de dados SQL](../sql-database/sql-database-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="1c177-180">toocreate an Azure SQL Database, follow hello steps in hello [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="1c177-181">Ao criar o banco de dados hello, use `oozietest` como nome do banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-181">When creating hello database, use `oozietest` as hello database name.</span></span> <span data-ttu-id="1c177-182">Também faça uma anotação de nome de saudação do servidor de banco de dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-182">Also make a note of hello name of hello database server.</span></span>

### <a name="create-hello-table"></a><span data-ttu-id="1c177-183">Criar tabela Olá</span><span class="sxs-lookup"><span data-stu-id="1c177-183">Create hello table</span></span>

> [!NOTE]
> <span data-ttu-id="1c177-184">Há muitas maneiras tooconnect tooSQL banco de dados toocreate uma tabela.</span><span class="sxs-lookup"><span data-stu-id="1c177-184">There are many ways tooconnect tooSQL Database toocreate a table.</span></span> <span data-ttu-id="1c177-185">Olá use as etapas a seguir [FreeTDS](http://www.freetds.org/) do cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-185">hello following steps use [FreeTDS](http://www.freetds.org/) from hello HDInsight cluster.</span></span>


1. <span data-ttu-id="1c177-186">Use Olá após o comando tooinstall FreeTDS no cluster do HDInsight hello:</span><span class="sxs-lookup"><span data-stu-id="1c177-186">Use hello following command tooinstall FreeTDS on hello HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="1c177-187">Depois de FreeTDS tiver sido instalado, use Olá após o servidor de banco de dados SQL do comando tooconnect toohello criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="1c177-187">Once FreeTDS has been installed, use hello following command tooconnect toohello SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="1c177-188">Você receberá a saída toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-188">You receive output similar toohello following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set toooozietest
        1>

3. <span data-ttu-id="1c177-189">Em Olá `1>` prompt, digite Olá linhas seguintes:</span><span class="sxs-lookup"><span data-stu-id="1c177-189">At hello `1>` prompt, enter hello following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="1c177-190">Olá quando `GO` instrução for inserida, instruções de saudação anterior são avaliadas.</span><span class="sxs-lookup"><span data-stu-id="1c177-190">When hello `GO` statement is entered, hello previous statements are evaluated.</span></span> <span data-ttu-id="1c177-191">Essas instruções criam uma tabela chamada **mobiledata** que é usada pelo fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-191">These statements create a table named **mobiledata** that is used by hello workflow.</span></span>

    <span data-ttu-id="1c177-192">Saudação de uso tooverify que Olá a tabela a seguir foi criada:</span><span class="sxs-lookup"><span data-stu-id="1c177-192">Use hello following tooverify that hello table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="1c177-193">Você verá a saída toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-193">You see output similar toohello following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="1c177-194">Digite `exit` em Olá `1>` tooexit Olá tsql utilitário do prompt.</span><span class="sxs-lookup"><span data-stu-id="1c177-194">Enter `exit` at hello `1>` prompt tooexit hello tsql utility.</span></span>

## <a name="create-hello-job-definition"></a><span data-ttu-id="1c177-195">Criar definição de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="1c177-195">Create hello job definition</span></span>

<span data-ttu-id="1c177-196">definição de trabalho Olá descreve onde toofind hello. XML.</span><span class="sxs-lookup"><span data-stu-id="1c177-196">hello job definition describes where toofind hello workflow.xml.</span></span> <span data-ttu-id="1c177-197">Ele também descreve onde toofind outros arquivos usados pelo fluxo de trabalho de saudação (como useooziewf.hql). Ele também define os valores de saudação para as propriedades usadas em fluxo de trabalho hello e os arquivos associados.</span><span class="sxs-lookup"><span data-stu-id="1c177-197">It also describes where toofind other files used by hello workflow (such as useooziewf.hql.) It also defines hello values for properties used within hello workflow and associated files.</span></span>

1. <span data-ttu-id="1c177-198">Use Olá endereço completo do comando tooget Olá de armazenamento padrão da saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="1c177-198">Use hello following command tooget hello full address of hello default storage.</span></span> <span data-ttu-id="1c177-199">Este endereço é usado no arquivo de configuração de saudação em breve:</span><span class="sxs-lookup"><span data-stu-id="1c177-199">This address is used in hello configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="1c177-200">Esse comando retorna informações toohello semelhante XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-200">This command returns information similar toohello following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="1c177-201">Se o cluster do HDInsight Olá usa o armazenamento do Azure como armazenamento padrão da saudação, Olá `<value>` conteúdo de elemento começa com `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="1c177-201">If hello HDInsight cluster uses Azure Storage as hello default storage, hello `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="1c177-202">Se o Azure Data Lake Store é usado, ele começa com `adl://`.</span><span class="sxs-lookup"><span data-stu-id="1c177-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="1c177-203">Salvar o conteúdo de saudação do hello `<value>` elemento, como ele é usado em providências hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-203">Save hello contents of hello `<value>` element, as it is used in hello next steps.</span></span>

2. <span data-ttu-id="1c177-204">Use Olá comando tooget FQDN do nó principal do cluster Olá a seguir.</span><span class="sxs-lookup"><span data-stu-id="1c177-204">Use hello following command tooget FQDN of hello cluster headnode.</span></span> <span data-ttu-id="1c177-205">Essas informações são usadas para Olá endereço JobTracker para cluster hello:</span><span class="sxs-lookup"><span data-stu-id="1c177-205">This information is used for hello JobTracker address for hello cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="1c177-206">Isso retorna informações toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-206">This returns information similar toohello following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="1c177-207">Olá porta usada para Olá JobTracker está 8050, Olá endereço completo toouse para Olá JobTracker `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="1c177-207">hello port used for hello JobTracker is 8050, so hello full address toouse for hello JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="1c177-208">Use Olá configuração de definição de trabalho toocreate Olá Oozie a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-208">Use hello following toocreate hello Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="1c177-209">Depois de saudação nano editor é aberto, use Olá XML a seguir como conteúdo de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="1c177-209">Once hello nano editor opens, use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

        <property>
        <name>nameNode</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
        </property>

        <property>
        <name>jobTracker</name>
        <value>JOBTRACKERADDRESS</value>
        </property>

        <property>
        <name>queueName</name>
        <value>default</value>
        </property>

        <property>
        <name>oozie.use.system.libpath</name>
        <value>true</value>
        </property>

        <property>
        <name>hiveScript</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/useooziewf.hql</value>
        </property>

        <property>
        <name>hiveTableName</name>
        <value>mobilecount</value>
        </property>

        <property>
        <name>hiveDataFolder</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie/data</value>
        </property>

        <property>
        <name>sqlDatabaseConnectionString</name>
        <value>"jdbc:sqlserver://serverName.database.windows.net;user=adminLogin;password=adminPassword;database=oozietest"</value>
        </property>

        <property>
        <name>sqlDatabaseTableName</name>
        <value>mobiledata</value>
        </property>

        <property>
        <name>user.name</name>
        <value>YourName</value>
        </property>

        <property>
        <name>oozie.wf.application.path</name>
        <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
    </configuration>
    ```

   * <span data-ttu-id="1c177-210">Substitua todas as instâncias de  **wasb://mycontainer@mystorageaccount.blob.core.windows.net**  com valor de saudação recebidas anteriormente para armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="1c177-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with hello value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="1c177-211">Se o caminho de saudação é um `wasb` caminho, você deve usar o caminho completo da saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-211">If hello path is a `wasb` path, you must use hello full path.</span></span> <span data-ttu-id="1c177-212">Não reduzi-lo toojust `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="1c177-212">Do not shorten it toojust `wasb:///`.</span></span>

   * <span data-ttu-id="1c177-213">Substituir **JOBTRACKERADDRESS** com hello endereço JobTracker/ResourceManager recebidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1c177-213">Replace **JOBTRACKERADDRESS** with hello JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="1c177-214">Substituir **YourName** com seu nome de logon para o cluster do HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-214">Replace **YourName** with your login name for hello HDInsight cluster.</span></span>
   * <span data-ttu-id="1c177-215">Substituir **serverName**, **adminLogin**, e **adminPassword** com informações de saudação para seu banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="1c177-215">Replace **serverName**, **adminLogin**, and **adminPassword** with hello information for your Azure SQL Database.</span></span>

     <span data-ttu-id="1c177-216">A maioria das informações neste arquivo hello é toopopulate usados valores de saudação usados nos arquivos. XML ou ooziewf.hql de saudação (por exemplo, ${nameNode}.)</span><span class="sxs-lookup"><span data-stu-id="1c177-216">Most of hello information in this file is used toopopulate hello values used in hello workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="1c177-217">Olá **oozie.wf.application.path** entrada define onde toofind hello. XML arquivo que contém o fluxo de trabalho Olá foi executado por esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="1c177-217">hello **oozie.wf.application.path** entry defines where toofind hello workflow.xml file, which contains hello workflow ran by this job.</span></span>

5. <span data-ttu-id="1c177-218">Use Ctrl-X, em seguida, **Y** e **Enter** toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-218">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

## <a name="submit-and-manage-hello-job"></a><span data-ttu-id="1c177-219">Enviar e gerenciar o trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="1c177-219">Submit and manage hello job</span></span>

<span data-ttu-id="1c177-220">Hello etapas a seguir usam Olá Oozie comando toosubmit e gerenciar fluxos de trabalho do Oozie no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-220">hello following steps use hello Oozie command toosubmit and manage Oozie workflows on hello cluster.</span></span> <span data-ttu-id="1c177-221">Olá Oozie comando é uma interface amigável sobre Olá [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="1c177-221">hello Oozie command is a friendly interface over hello [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c177-222">Ao usar o comando do hello Oozie, você deve usar Olá FQDN para um nó principal do hello HDInsight.</span><span class="sxs-lookup"><span data-stu-id="1c177-222">When using hello Oozie command, you must use hello FQDN for hello HDInsight headnode.</span></span> <span data-ttu-id="1c177-223">Esse FQDN só está acessível no cluster hello ou se hello cluster estiver em uma rede Virtual do Azure, de outras máquinas Olá mesma rede.</span><span class="sxs-lookup"><span data-stu-id="1c177-223">This FQDN is only accessible from hello cluster, or if hello cluster is on an Azure Virtual Network, from other machines on hello same network.</span></span>


1. <span data-ttu-id="1c177-224">Use Olá após tooobtain Olá URL toohello Oozie serviço:</span><span class="sxs-lookup"><span data-stu-id="1c177-224">Use hello following tooobtain hello URL toohello Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="1c177-225">Isso retorna informações toohello semelhante XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-225">This returns information similar toohello following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="1c177-226">Olá `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` parte é Olá URL toouse com hello Oozie comando.</span><span class="sxs-lookup"><span data-stu-id="1c177-226">hello `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is hello URL toouse with hello Oozie command.</span></span>

2. <span data-ttu-id="1c177-227">Olá Use toocreate uma variável de ambiente a seguir para URL hello, para que você não tenha tootype para cada comando:</span><span class="sxs-lookup"><span data-stu-id="1c177-227">Use hello following toocreate an environment variable for hello URL, so you don't have tootype it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="1c177-228">Substitua URL Olá Olá um recebidas anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1c177-228">Replace hello URL with hello one you received earlier.</span></span>
3. <span data-ttu-id="1c177-229">Use Olá trabalho de saudação toosubmit a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-229">Use hello following toosubmit hello job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="1c177-230">Esse comando carrega informações de trabalho de saudação do **job.xml** e envia tooOozie, mas não não executá-lo.</span><span class="sxs-lookup"><span data-stu-id="1c177-230">This command loads hello job information from **job.xml** and submits it tooOozie, but does not run it.</span></span>

    <span data-ttu-id="1c177-231">Após a conclusão do comando hello, ele deverá retornar Olá ID do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-231">Once hello command completes, it should return hello ID of hello job.</span></span> <span data-ttu-id="1c177-232">Por exemplo: `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="1c177-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="1c177-233">Essa ID é um trabalho de saudação toomanage usado.</span><span class="sxs-lookup"><span data-stu-id="1c177-233">This ID is used toomanage hello job.</span></span>

4. <span data-ttu-id="1c177-234">Exibir o status de saudação do trabalho hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-234">View hello status of hello job using hello following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="1c177-235">Substituir `<JOBID>` com hello ID retornado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-235">Replace `<JOBID>` with hello ID returned in hello previous step.</span></span>

    <span data-ttu-id="1c177-236">Isso retorna informações toohello semelhante texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-236">This returns information similar toohello following text:</span></span>

    ```
    Job ID : 0000005-150622124850154-oozie-oozi-W
    ------------------------------------------------------------------------------------------------------------------------------------
    Workflow Name : useooziewf
    App Path      : wasb:///tutorials/useoozie
    Status        : PREP
    Run           : 0
    User          : USERNAME
    Group         : -
    Created       : 2015-06-22 15:06 GMT
    Started       : -
    Last Modified : 2015-06-22 15:06 GMT
    Ended         : -
    CoordAction ID: -
    ------------------------------------------------------------------------------------------------------------------------------------
    ```

    <span data-ttu-id="1c177-237">Este trabalho tem o status `PREP`.</span><span class="sxs-lookup"><span data-stu-id="1c177-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="1c177-238">Este status indica que esse trabalho Olá foi criado, mas não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="1c177-238">This status indicates that hello job was created, but not started.</span></span>

5. <span data-ttu-id="1c177-239">Use Olá trabalho de saudação do toostart de comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-239">Use hello following command toostart hello job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="1c177-240">Substituir `<JOBID>` com hello ID retornado anteriormente.</span><span class="sxs-lookup"><span data-stu-id="1c177-240">Replace `<JOBID>` with hello ID returned previously.</span></span>

    <span data-ttu-id="1c177-241">Se você verificar o status de saudação após esse comando, ele está em um estado de execução e informações serão retornadas para ações de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-241">If you check hello status after this command, it is in a running state, and information is returned for hello actions within hello job.</span></span>

6. <span data-ttu-id="1c177-242">Depois de concluir a tarefa de saudação com êxito, você pode verificar se os dados saudação foi gerados e exportado toohello tabela de banco de dados SQL usando Olá comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-242">Once hello task completes successfully, you can verify that hello data was generated and exported toohello SQL Database table by using hello following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="1c177-243">Em Olá `1>` prompt, digite Olá consulta a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-243">At hello `1>` prompt, enter hello following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="1c177-244">informações de Hello retornadas são semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-244">hello information returned is similar toohello following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="1c177-245">Para obter mais informações sobre Olá comando Oozie, consulte [ferramenta de linha de comando do Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="1c177-245">For more information on hello Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="1c177-246">API REST do Oozie</span><span class="sxs-lookup"><span data-stu-id="1c177-246">Oozie REST API</span></span>

<span data-ttu-id="1c177-247">Olá Oozie REST API permite que você toobuild suas próprias ferramentas que funcionam com Oozie.</span><span class="sxs-lookup"><span data-stu-id="1c177-247">hello Oozie REST API allows you toobuild your own tools that work with Oozie.</span></span> <span data-ttu-id="1c177-248">Olá seguem HDInsight de informações específicas sobre como usar o hello Oozie REST API:</span><span class="sxs-lookup"><span data-stu-id="1c177-248">hello following are HDInsight specific information about using hello Oozie REST API:</span></span>

* <span data-ttu-id="1c177-249">**URI**: Olá API REST podem ser acessada de fora cluster Olá em`https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="1c177-249">**URI**: hello REST API can be accessed from outside hello cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="1c177-250">**Autenticação**: autenticar toohello API usando a conta de cluster HTTP hello (administrador) e a senha.</span><span class="sxs-lookup"><span data-stu-id="1c177-250">**Authentication**: Authenticate toohello API using hello cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="1c177-251">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="1c177-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="1c177-252">Para obter mais informações sobre como usar o hello Oozie REST API, consulte [API de serviços Web Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="1c177-252">For more information on using hello Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="1c177-253">Interface da Web do Oozie</span><span class="sxs-lookup"><span data-stu-id="1c177-253">Oozie Web UI</span></span>

<span data-ttu-id="1c177-254">Saudação da interface do usuário do Oozie Web fornece uma visão baseado na web status de saudação do Oozie trabalhos no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-254">hello Oozie Web UI provides a web-based view into hello status of Oozie jobs on hello cluster.</span></span> <span data-ttu-id="1c177-255">Interface da web Hello permite Olá tooview informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-255">hello web UI allows you tooview hello following information:</span></span>

* <span data-ttu-id="1c177-256">Status do trabalho</span><span class="sxs-lookup"><span data-stu-id="1c177-256">Job status</span></span>
* <span data-ttu-id="1c177-257">Definição de trabalho</span><span class="sxs-lookup"><span data-stu-id="1c177-257">Job definition</span></span>
* <span data-ttu-id="1c177-258">Configuração</span><span class="sxs-lookup"><span data-stu-id="1c177-258">Configuration</span></span>
* <span data-ttu-id="1c177-259">Um gráfico de ações de saudação em trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="1c177-259">A graph of hello actions in hello job</span></span>
* <span data-ttu-id="1c177-260">Logs para o trabalho de saudação</span><span class="sxs-lookup"><span data-stu-id="1c177-260">Logs for hello job</span></span>

<span data-ttu-id="1c177-261">Você também pode exibir detalhes de ações dentro de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="1c177-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="1c177-262">tooaccess Olá a interface do usuário da Web do Oozie, use Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-262">tooaccess hello Oozie Web UI, use hello following steps:</span></span>

1. <span data-ttu-id="1c177-263">Crie um cluster de HDInsight de toohello de túnel SSH.</span><span class="sxs-lookup"><span data-stu-id="1c177-263">Create an SSH tunnel toohello HDInsight cluster.</span></span> <span data-ttu-id="1c177-264">Para obter informações, consulte Olá [usar SSH de encapsulamento HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="1c177-264">For information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="1c177-265">Quando tiver sido criado um túnel, abra Olá Ambari web da interface do usuário no seu navegador da web.</span><span class="sxs-lookup"><span data-stu-id="1c177-265">Once a tunnel has been created, open hello Ambari web UI in your web browser.</span></span> <span data-ttu-id="1c177-266">Olá URI para o site do Ambari Olá é **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="1c177-266">hello URI for hello Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="1c177-267">Substituir **CLUSTERNAME** com nome de saudação do cluster HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="1c177-267">Replace **CLUSTERNAME** with hello name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="1c177-268">Olá lado esquerdo da página hello, selecione **Oozie**, em seguida, **Links rápidos**e, finalmente, **Oozie Web UI**.</span><span class="sxs-lookup"><span data-stu-id="1c177-268">From hello left side of hello page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![imagem de menus Olá](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="1c177-270">Olá padrões de interface do usuário da Web do Oozie toodisplaying trabalhos de fluxo de trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="1c177-270">hello Oozie Web UI defaults toodisplaying running Workflow Jobs.</span></span> <span data-ttu-id="1c177-271">toosee todos os trabalhos de fluxo de trabalho, selecione **todos os trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="1c177-271">toosee all workflow jobs, select **All Jobs**.</span></span>

    ![Todos os trabalhos exibidos](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="1c177-273">Selecione um trabalho tooview obter mais informações sobre o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-273">Select a job tooview more information about hello job.</span></span>

    ![Informações do Trabalho](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="1c177-275">Na guia de informações sobre o trabalho Olá, você pode ver informações de trabalho básico e ações individuais de saudação do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-275">From hello Job Info tab, you can see basic job information and hello individual actions within hello job.</span></span> <span data-ttu-id="1c177-276">Usando guias de saudação na parte superior de saudação que você pode exibir Olá definição de trabalho, configuração de trabalho, Olá acesso Log do trabalho ou exibir um direcionado acíclico Graph (DAG) do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-276">Using hello tabs at hello top you can view hello Job Definition, Job Configuration, access hello Job Log or view a Directed Acyclic Graph (DAG) of hello job.</span></span>

   * <span data-ttu-id="1c177-277">**Trabalho de Log**: selecione Olá **GetLogs** botão tooget todos os logs de trabalho hello, ou use Olá **inserir o filtro de pesquisa** campo toofilter logs</span><span class="sxs-lookup"><span data-stu-id="1c177-277">**Job Log**: Select hello **GetLogs** button tooget all logs for hello job, or use hello **Enter Search Filter** field toofilter logs</span></span>

       ![Log de trabalhos](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="1c177-279">**JobDAG**: Olá DAG é uma representação gráfica dos caminhos de dados Olá feito por meio do fluxo de trabalho Olá</span><span class="sxs-lookup"><span data-stu-id="1c177-279">**JobDAG**: hello DAG is a graphical overview of hello data paths taken through hello workflow</span></span>

       ![DAG de trabalho](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="1c177-281">Selecionando uma das ações de saudação do hello **informações sobre o trabalho** guia exibe informações de ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-281">Selecting one of hello actions from hello **Job Info** tab brings up information for hello action.</span></span> <span data-ttu-id="1c177-282">Por exemplo, selecione Olá **RunHiveScript** ação.</span><span class="sxs-lookup"><span data-stu-id="1c177-282">For example, select hello **RunHiveScript** action.</span></span>

    ![Informações da ação](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="1c177-284">Você pode ver detalhes de ação de saudação, como um link toohello **URL do Console**.</span><span class="sxs-lookup"><span data-stu-id="1c177-284">You can see details for hello action, such as a link toohello **Console URL**.</span></span> <span data-ttu-id="1c177-285">Esse link pode ser usado tooview JobTracker informações para o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-285">This link can be used tooview JobTracker information for hello job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="1c177-286">Agendamento de trabalhos</span><span class="sxs-lookup"><span data-stu-id="1c177-286">Scheduling jobs</span></span>

<span data-ttu-id="1c177-287">coordenador de saudação permite que você toospecify uma frequência de início, fim e ocorrência para trabalhos.</span><span class="sxs-lookup"><span data-stu-id="1c177-287">hello coordinator allows you toospecify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="1c177-288">toodefine uma agenda para o fluxo de trabalho hello, Olá use as etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-288">toodefine a schedule for hello workflow, use hello following steps:</span></span>

1. <span data-ttu-id="1c177-289">Saudação de uso a seguir toocreate um arquivo chamado **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="1c177-289">Use hello following toocreate a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="1c177-290">Use Olá XML a seguir como conteúdo de saudação do arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="1c177-290">Use hello following XML as hello contents of hello file:</span></span>

    ```xml
    <coordinator-app name="my_coord_app" frequency="${coordFrequency}" start="${coordStart}" end="${coordEnd}" timezone="${coordTimezone}" xmlns="uri:oozie:coordinator:0.4">
        <action>
        <workflow>
            <app-path>${workflowPath}</app-path>
        </workflow>
        </action>
    </coordinator-app>
    ```

    > [!NOTE]
    > <span data-ttu-id="1c177-291">Olá `${...}` variáveis são substituídas pelos valores na definição do trabalho de saudação em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="1c177-291">hello `${...}` variables are replaced by values in hello job definition at run-time.</span></span> <span data-ttu-id="1c177-292">Olá variáveis são:</span><span class="sxs-lookup"><span data-stu-id="1c177-292">hello variables are:</span></span>
    >
    > * <span data-ttu-id="1c177-293">`${coordFrequency}`: Hora entre instâncias do trabalho de saudação de execução.</span><span class="sxs-lookup"><span data-stu-id="1c177-293">`${coordFrequency}`: Time between running instances of hello job.</span></span>
    > <span data-ttu-id="1c177-294">** `${coordStart}`: hora de início do trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-294">** `${coordStart}`: hello job start time.</span></span>
    > * <span data-ttu-id="1c177-295">`${coordEnd}`: hora de término de trabalho hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-295">`${coordEnd}`: hello job end time.</span></span>
    > * <span data-ttu-id="1c177-296">`${coordTimezone}`: os trabalhos do coordenador estão em um fuso horário fixo sem horário de verão (geralmente representado com o uso do UTC).</span><span class="sxs-lookup"><span data-stu-id="1c177-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="1c177-297">Este fuso horário é conhecido como hello "Oozie processamento de fuso horário."</span><span class="sxs-lookup"><span data-stu-id="1c177-297">This time zone is referred as hello "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="1c177-298">`${wfPath}`: Olá. XML toohello de caminho.</span><span class="sxs-lookup"><span data-stu-id="1c177-298">`${wfPath}`: hello path toohello workflow.xml.</span></span>

2. <span data-ttu-id="1c177-299">Olá toosave de arquivo, use Ctrl-X, **Y**, e **Enter**.</span><span class="sxs-lookup"><span data-stu-id="1c177-299">toosave hello file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="1c177-300">Use Olá comando toocopy Olá arquivo toohello diretório de trabalho para esse trabalho a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-300">Use hello following command toocopy hello file toohello working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="1c177-301">Olá Use toomodify Olá a seguir **job.xml** arquivo:</span><span class="sxs-lookup"><span data-stu-id="1c177-301">Use hello following toomodify hello **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="1c177-302">Verifique Olá as seguintes alterações:</span><span class="sxs-lookup"><span data-stu-id="1c177-302">Make hello following changes:</span></span>

   * <span data-ttu-id="1c177-303">arquivo de coordenador de saudação tooinstruct oozie toorun em vez de fluxo de trabalho hello, alteração `<name>oozie.wf.application.path</name>` muito`<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="1c177-303">tooinstruct oozie toorun hello coordinator file instead of hello workflow, change `<name>oozie.wf.application.path</name>` too`<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="1c177-304">Olá tooset `workflowPath` variável usada pelo coordenador hello, adicionar Olá XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-304">tooset hello `workflowPath` variable used by hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="1c177-305">Substituir saudação `wasb://mycontainer@mystorageaccount.blob.core.windows` texto com valor de saudação usado em outras entradas no arquivo de job.xml hello.</span><span class="sxs-lookup"><span data-stu-id="1c177-305">Replace hello `wasb://mycontainer@mystorageaccount.blob.core.windows` text with hello value used in other entries in hello job.xml file.</span></span>

   * <span data-ttu-id="1c177-306">início de saudação toodefine, fim e frequência de coordenador hello, adicionam Olá XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-306">toodefine hello start, end, and frequency for hello coordinator, add hello following XML:</span></span>

        ```xml
        <property>
            <name>coordStart</name>
            <value>2017-05-10T12:00Z</value>
        </property>

        <property>
            <name>coordEnd</name>
            <value>2017-05-12T12:00Z</value>
        </property>

        <property>
            <name>coordFrequency</name>
            <value>1440</value>
        </property>

        <property>
            <name>coordTimezone</name>
            <value>UTC</value>
        </property>
        ```

       <span data-ttu-id="1c177-307">Os valores definidos Olá too12 de hora de início: 00 PM em 10 de maio de 2017, Olá tooMay de hora de término 12, 2017.</span><span class="sxs-lookup"><span data-stu-id="1c177-307">These values set hello start time too12:00PM on May 10, 2017, hello end time tooMay 12, 2017.</span></span> <span data-ttu-id="1c177-308">intervalo de saudação para executar este trabalho diariamente.</span><span class="sxs-lookup"><span data-stu-id="1c177-308">hello interval for running this job daily.</span></span> <span data-ttu-id="1c177-309">frequência de saudação é em minutos, até 24 horas x 60 minutos = 1440 minutos.</span><span class="sxs-lookup"><span data-stu-id="1c177-309">hello frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="1c177-310">Por fim, o fuso horário de saudação é definido tooUTC.</span><span class="sxs-lookup"><span data-stu-id="1c177-310">Finally, hello timezone is set tooUTC.</span></span>

5. <span data-ttu-id="1c177-311">Use Ctrl-X, em seguida, **Y** e **Enter** toosave arquivo de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-311">Use Ctrl-X, then **Y** and **Enter** toosave hello file.</span></span>

6. <span data-ttu-id="1c177-312">trabalho de saudação toorun, use Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-312">toorun hello job, use hello following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="1c177-313">Esse comando envia e inicia o trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-313">This command submits and starts hello job.</span></span>

7. <span data-ttu-id="1c177-314">Se você visitar Olá Oozie Web UI e selecionar Olá **trabalhos do coordenador** guia, você verá informações toohello semelhante imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-314">If you visit hello Oozie Web UI and select hello **Coordinator Jobs** tab, you see information similar toohello following image:</span></span>

    ![guia de trabalhos do coordenador](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="1c177-316">Olá **materialização próxima** entrada contém Olá próxima vez que Olá execuções de trabalho.</span><span class="sxs-lookup"><span data-stu-id="1c177-316">hello **Next Materialization** entry contains hello next time that hello job runs.</span></span>

8. <span data-ttu-id="1c177-317">Toohello semelhante anterior fluxo de trabalho, selecionando a entrada de trabalho Olá na interface da web hello exibe informações sobre o trabalho de saudação:</span><span class="sxs-lookup"><span data-stu-id="1c177-317">Similar toohello earlier workflow job, selecting hello job entry in hello web UI displays information on hello job:</span></span>

    ![Informações de trabalho do coordenador](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="1c177-319">Esta imagem mostra apenas bem-sucedida execuções do trabalho hello, ações não individuais de fluxo de trabalho Olá agendado.</span><span class="sxs-lookup"><span data-stu-id="1c177-319">This image only shows successful runs of hello job, not individual actions within hello scheduled workflow.</span></span> <span data-ttu-id="1c177-320">toosee que, selecione uma saudação **ação** entradas.</span><span class="sxs-lookup"><span data-stu-id="1c177-320">toosee that, select one of hello **Action** entries.</span></span>

    ![Informações da ação](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="1c177-322">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="1c177-322">Troubleshooting</span></span>

<span data-ttu-id="1c177-323">Olá Oozie UI permite tooview Oozie logs.</span><span class="sxs-lookup"><span data-stu-id="1c177-323">hello Oozie UI allows you tooview Oozie logs.</span></span> <span data-ttu-id="1c177-324">Ele também contém logs de tooJobTracker links para tarefas de MapReduce iniciadas pelo fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-324">It also contains links tooJobTracker logs for MapReduce tasks started by hello workflow.</span></span> <span data-ttu-id="1c177-325">saudação padrão para solução de problemas deve ser:</span><span class="sxs-lookup"><span data-stu-id="1c177-325">hello pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="1c177-326">Exibir o trabalho de saudação na interface do usuário da Web do Oozie.</span><span class="sxs-lookup"><span data-stu-id="1c177-326">View hello job in Oozie Web UI.</span></span>

2. <span data-ttu-id="1c177-327">Se houver um erro ou falha de uma ação específica, selecione Olá toosee ação se hello **mensagem de erro** campo fornece mais informações sobre a falha de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-327">If there is an error or failure for a specific action, select hello action toosee if hello **Error Message** field provides more information on hello failure.</span></span>

3. <span data-ttu-id="1c177-328">Se estiver disponível, use a URL de saudação da saudação ação tooview mais detalhes (como logs de JobTracker) para a ação de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-328">If available, use hello URL from hello action tooview more details (such as JobTracker logs) for hello action.</span></span>

<span data-ttu-id="1c177-329">Olá, estes são erros específicos que você pode encontrar, e como tooresolve-los.</span><span class="sxs-lookup"><span data-stu-id="1c177-329">hello following are specific errors you may encounter, and how tooresolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="1c177-330">JA009: não é possível inicializar o cluster</span><span class="sxs-lookup"><span data-stu-id="1c177-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="1c177-331">**Sintomas**: Olá alterações de status de trabalho muito**suspenso**.</span><span class="sxs-lookup"><span data-stu-id="1c177-331">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="1c177-332">Detalhes do trabalho Olá mostram o status de RunHiveScript hello como **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="1c177-332">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="1c177-333">Selecionando a ação de saudação exibe Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="1c177-333">Selecting hello action displays hello following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="1c177-334">**Causa**: Olá endereços WASB usados em Olá **job.xml** arquivo não contém o contêiner de armazenamento hello ou nome de conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="1c177-334">**Cause**: hello WASB addresses used in hello **job.xml** file do not contain hello storage container or storage account name.</span></span> <span data-ttu-id="1c177-335">formato de endereço Olá WASB deve ser `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="1c177-335">hello WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="1c177-336">**Resolução**: alterar Olá WASB endereços usados pelo trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-336">**Resolution**: Change hello WASB addresses used by hello job.</span></span>

### <a name="ja002-oozie-is-not-allowed-tooimpersonate-ltuser"></a><span data-ttu-id="1c177-337">JA002: Oozie não é permitido tooimpersonate &lt;usuário ></span><span class="sxs-lookup"><span data-stu-id="1c177-337">JA002: Oozie is not allowed tooimpersonate &lt;USER></span></span>

<span data-ttu-id="1c177-338">**Sintomas**: Olá alterações de status de trabalho muito**suspenso**.</span><span class="sxs-lookup"><span data-stu-id="1c177-338">**Symptoms**: hello job status changes too**SUSPENDED**.</span></span> <span data-ttu-id="1c177-339">Detalhes do trabalho Olá mostram o status de RunHiveScript hello como **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="1c177-339">Details for hello job show hello RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="1c177-340">Selecionando a ação de saudação mostra Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="1c177-340">Selecting hello action shows hello following error message:</span></span>

    JA002: User: oozie is not allowed tooimpersonate <USER>

<span data-ttu-id="1c177-341">**Causa**: configurações de permissão atuais não permitem Oozie tooimpersonate Olá especificar conta de usuário.</span><span class="sxs-lookup"><span data-stu-id="1c177-341">**Cause**: Current permission settings do not allow Oozie tooimpersonate hello specified user account.</span></span>

<span data-ttu-id="1c177-342">**Resolução**: Oozie é permitido tooimpersonate usuários Olá **usuários** grupo.</span><span class="sxs-lookup"><span data-stu-id="1c177-342">**Resolution**: Oozie is allowed tooimpersonate users in hello **users** group.</span></span> <span data-ttu-id="1c177-343">Saudação de uso `groups USERNAME` toosee grupos de Olá Olá a conta de usuário é membro.</span><span class="sxs-lookup"><span data-stu-id="1c177-343">Use hello `groups USERNAME` toosee hello groups that hello user account is a member of.</span></span> <span data-ttu-id="1c177-344">Se o usuário Olá não é um membro da saudação **usuários** de grupo, use Olá grupo toohello do comando tooadd Olá usuário a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-344">If hello user is not a member of hello **users** group, use hello following command tooadd hello user toohello group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="1c177-345">Pode levar vários minutos antes de HDInsight reconhece que o usuário Olá foi adicionado toohello grupo.</span><span class="sxs-lookup"><span data-stu-id="1c177-345">It may take several minutes before HDInsight recognizes that hello user has been added toohello group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="1c177-346">ERRO do Iniciador (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="1c177-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="1c177-347">**Sintomas**: Olá alterações de status de trabalho muito**KILLED**.</span><span class="sxs-lookup"><span data-stu-id="1c177-347">**Symptoms**: hello job status changes too**KILLED**.</span></span> <span data-ttu-id="1c177-348">Detalhes do trabalho Olá mostram o status de RunSqoopExport hello como **erro**.</span><span class="sxs-lookup"><span data-stu-id="1c177-348">Details for hello job show hello RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="1c177-349">Selecionando a ação de saudação mostra Olá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="1c177-349">Selecting hello action shows hello following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="1c177-350">**Causa**: Sqoop é tooload não é possível Olá banco de dados driver necessário tooaccess Olá banco de dados.</span><span class="sxs-lookup"><span data-stu-id="1c177-350">**Cause**: Sqoop is unable tooload hello database driver required tooaccess hello database.</span></span>

<span data-ttu-id="1c177-351">**Resolução**: ao usar o Sqoop de um trabalho de Oozie, você deve incluir driver do banco de dados de saudação com hello outros recursos (como. XML Olá) usados pelo trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="1c177-351">**Resolution**: When using Sqoop from an Oozie job, you must include hello database driver with hello other resources (such as hello workflow.xml) used by hello job.</span></span> <span data-ttu-id="1c177-352">Também fazer referência a arquivo hello que contém o driver de banco de dados de saudação do hello `<sqoop>...</sqoop>` seção. Olá XML.</span><span class="sxs-lookup"><span data-stu-id="1c177-352">Also Reference hello archive containing hello database driver from hello `<sqoop>...</sqoop>` section of hello workflow.xml.</span></span>

<span data-ttu-id="1c177-353">Por exemplo, para o trabalho de saudação neste documento, você usaria Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-353">For example, for hello job in this document, you would use hello following steps:</span></span>

1. <span data-ttu-id="1c177-354">Copie o diretório do hello sqljdbc4.1.jar arquivo toohello /tutorials/useoozie:</span><span class="sxs-lookup"><span data-stu-id="1c177-354">Copy hello sqljdbc4.1.jar file toohello /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="1c177-355">Modificar Olá. XML tooadd Olá XML a seguir em uma nova linha acima `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="1c177-355">Modify hello workflow.xml tooadd hello following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="1c177-356">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="1c177-356">Next steps</span></span>

<span data-ttu-id="1c177-357">Neste tutorial, você aprendeu como toodefine um fluxo de trabalho do Oozie e como toorun um trabalho Oozie.</span><span class="sxs-lookup"><span data-stu-id="1c177-357">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job.</span></span> <span data-ttu-id="1c177-358">toolearn mais sobre como trabalhar com HDInsight, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="1c177-358">toolearn more about working with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="1c177-359">[Usar o Coordenador do Oozie baseado em tempo com o HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="1c177-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="1c177-360">[Carregar dados para trabalhos do Hadoop no HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="1c177-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="1c177-361">[Usar Sqoop com o Hadoop no HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="1c177-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="1c177-362">[Usar o Hive com Hadoop no HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="1c177-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="1c177-363">[Usar o Pig com Hadoop no HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="1c177-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="1c177-364">[Desenvolver programas Java MapReduce para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="1c177-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563
[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started]: hdinsight-get-started.md
[hdinsight-use-sqoop]: hdinsight-use-sqoop-mac-linux.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-use-blob-storage.md
[hdinsight-get-started-emulator]: hdinsight-get-started-emulator.md
[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: sql-database-create-configure.md
[sqldatabase-get-started]: sql-database-get-started.md

[azure-create-storageaccount]:../storage/common/storage-create-storage-account.md

[apache-hadoop]: http://hadoop.apache.org/
[apache-oozie-400]: http://oozie.apache.org/docs/4.0.0/
[apache-oozie-332]: http://oozie.apache.org/docs/3.3.2/

[powershell-download]: http://azure.microsoft.com/downloads/
[powershell-about-profiles]: http://go.microsoft.com/fwlink/?LinkID=113729
[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx
[powershell-script]: https://technet.microsoft.com/en-us/library/ee176961.aspx

[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx

[img-workflow-diagram]: ./media/hdinsight-use-oozie/HDI.UseOozie.Workflow.Diagram.png
[img-preparation-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.Preparation.Output1.png
[img-runworkflow-output]: ./media/hdinsight-use-oozie/HDI.UseOozie.RunWF.Output.png

[technetwiki-hive-error]: http://social.technet.microsoft.com/wiki/contents/articles/23047.hdinsight-hive-error-unable-to-rename.aspx
