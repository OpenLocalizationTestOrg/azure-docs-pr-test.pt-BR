---
title: Usar os fluxos de trabalho de Sqoop do Hadoop no HDInsight baseado em Linux | Microsoft Docs
description: Usar o Oozie do Hadoop no HDInsight baseado em Linux. Saiba como definir um fluxo de trabalho do Oozie e enviar um trabalho do Oozie.
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
ms.openlocfilehash: e3206078e451aefe02689bfb61ce22a20dd0fa70
ms.sourcegitcommit: 18ad9bc049589c8e44ed277f8f43dcaa483f3339
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/29/2017
---
# <a name="use-oozie-with-hadoop-to-define-and-run-a-workflow-on-linux-based-hdinsight"></a><span data-ttu-id="c865b-104">Usar o Oozie com Hadoop para definir e executar um fluxo de trabalho no HDInsight baseado em Linux</span><span class="sxs-lookup"><span data-stu-id="c865b-104">Use Oozie with Hadoop to define and run a workflow on Linux-based HDInsight</span></span>

[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="c865b-105">Saiba como usar o Apache Oozie com o Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c865b-105">Learn how to use Apache Oozie with Hadoop on HDInsight.</span></span> <span data-ttu-id="c865b-106">O Apache Oozie é um sistema de fluxo de trabalho/coordenação que gerencia trabalhos do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="c865b-106">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="c865b-107">O Oozie é integrado à pilha do Hadoop e dá suporte aos seguintes trabalhos:</span><span class="sxs-lookup"><span data-stu-id="c865b-107">Oozie is integrated with the Hadoop stack, and it supports the following jobs:</span></span>

* <span data-ttu-id="c865b-108">Apache MapReduce</span><span class="sxs-lookup"><span data-stu-id="c865b-108">Apache MapReduce</span></span>
* <span data-ttu-id="c865b-109">Apache Pig</span><span class="sxs-lookup"><span data-stu-id="c865b-109">Apache Pig</span></span>
* <span data-ttu-id="c865b-110">Apache Hive</span><span class="sxs-lookup"><span data-stu-id="c865b-110">Apache Hive</span></span>
* <span data-ttu-id="c865b-111">Apache Sqoop</span><span class="sxs-lookup"><span data-stu-id="c865b-111">Apache Sqoop</span></span>

<span data-ttu-id="c865b-112">O Oozie também pode ser usado para agendar trabalhos específicos para um sistema, como programas Java ou scripts de shell</span><span class="sxs-lookup"><span data-stu-id="c865b-112">Oozie can also be used to schedule jobs that are specific to a system, like Java programs or shell scripts</span></span>

> [!NOTE]
> <span data-ttu-id="c865b-113">Outra opção para definir fluxos de trabalho com o HDInsight é uma Azure Data Factory.</span><span class="sxs-lookup"><span data-stu-id="c865b-113">Another option for defining workflows with HDInsight is Azure Data Factory.</span></span> <span data-ttu-id="c865b-114">Para conhecer mais o Azure Data Factory, confira [Usar o Pig e o Hive com o Data Factory][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="c865b-114">To learn more about Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c865b-115">O Oozie não está habilitado no HDInsight ingressado no domínio.</span><span class="sxs-lookup"><span data-stu-id="c865b-115">Oozie is not enabled on domain-joined HDInsight.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c865b-116">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="c865b-116">Prerequisites</span></span>

* <span data-ttu-id="c865b-117">**Um cluster hdinsight**: consulte [Introdução ao HDInsight no Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span><span class="sxs-lookup"><span data-stu-id="c865b-117">**An HDInsight cluster**: See [Get Started with HDInsight on Linux](hdinsight-hadoop-linux-tutorial-get-started.md)</span></span>

  > [!IMPORTANT]
  > <span data-ttu-id="c865b-118">As etapas deste documento exigem um cluster HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="c865b-118">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="c865b-119">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="c865b-119">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="c865b-120">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="c865b-120">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="example-workflow"></a><span data-ttu-id="c865b-121">Fluxo de trabalho de exemplo</span><span class="sxs-lookup"><span data-stu-id="c865b-121">Example workflow</span></span>

<span data-ttu-id="c865b-122">O fluxo de trabalho usado neste documento contém duas ações.</span><span class="sxs-lookup"><span data-stu-id="c865b-122">The workflow used in this document contains two actions.</span></span> <span data-ttu-id="c865b-123">Ações são definições de tarefas, como Sqoop, Hive, MapReduce ou outro processo de execução:</span><span class="sxs-lookup"><span data-stu-id="c865b-123">Actions are definitions for tasks, such as running Hive, Sqoop, MapReduce, or other process:</span></span>

![Diagrama de fluxo de trabalho][img-workflow-diagram]

1. <span data-ttu-id="c865b-125">Uma ação do Hive executa um script HiveQL para extrair os registros de **hivesampletable** incluídos com o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c865b-125">A Hive action runs a HiveQL script to extract records from the **hivesampletable** included with HDInsight.</span></span> <span data-ttu-id="c865b-126">Cada linha de dados descreve uma visita de um dispositivo móvel específico.</span><span class="sxs-lookup"><span data-stu-id="c865b-126">Each row of data describes a visit from a specific mobile device.</span></span> <span data-ttu-id="c865b-127">O formato de registro aparece semelhante ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="c865b-127">The record format appears similar to the following text:</span></span>

        8       18:54:20        en-US   Android Samsung SCH-i500        California     United States    13.9204007      0       0
        23      19:19:44        en-US   Android HTC     Incredible      Pennsylvania   United States    NULL    0       0
        23      19:19:46        en-US   Android HTC     Incredible      Pennsylvania   United States    1.4757422       0       1

    <span data-ttu-id="c865b-128">O script do Hive usado neste documento conta o total de visitas de cada plataforma (como Android ou iPhone) e armazena as contagens em uma nova tabela do Hive.</span><span class="sxs-lookup"><span data-stu-id="c865b-128">The Hive script used in this document counts the total visits for each platform (such as Android or iPhone) and stores the counts to a new Hive table.</span></span>

    <span data-ttu-id="c865b-129">Para obter mais informações sobre o Hive, consulte [Usar o Hive com o HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="c865b-129">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>

2. <span data-ttu-id="c865b-130">Uma ação do Sqoop exporta o conteúdo da nova tabela Hive para uma tabela em um Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="c865b-130">A Sqoop action exports the contents of the new Hive table to a table in an Azure SQL database.</span></span> <span data-ttu-id="c865b-131">Para saber mais sobre o Sqoop, confira [Usar o Hadoop Sqoop com o HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="c865b-131">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="c865b-132">Para obter as versões do Oozie com suporte em clusters HDInsight, confira [Novidades nas versões de clusters Hadoop fornecidas pelo HDInsight][hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="c865b-132">For supported Oozie versions on HDInsight clusters, see [What's new in the Hadoop cluster versions provided by HDInsight][hdinsight-versions].</span></span>

## <a name="create-the-working-directory"></a><span data-ttu-id="c865b-133">Criar o diretório de trabalho</span><span class="sxs-lookup"><span data-stu-id="c865b-133">Create the working directory</span></span>

<span data-ttu-id="c865b-134">O Oozie espera que os recursos necessários para um trabalho sejam armazenados no mesmo diretório.</span><span class="sxs-lookup"><span data-stu-id="c865b-134">Oozie expects resources required for a job to be stored in the same directory.</span></span> <span data-ttu-id="c865b-135">Este exemplo usa **wasb:///tutorials/useoozie**.</span><span class="sxs-lookup"><span data-stu-id="c865b-135">This example uses **wasb:///tutorials/useoozie**.</span></span> <span data-ttu-id="c865b-136">Use o comando a seguir para criar esse diretório e o diretório de dados que armazenará a nova tabela do Hive criada por este fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="c865b-136">Use the following command to create this directory, and the data directory that holds the new Hive table created by this workflow:</span></span>

```
hdfs dfs -mkdir -p /tutorials/useoozie/data
```

> [!NOTE]
> <span data-ttu-id="c865b-137">O parâmetro `-p` faz com que todos os diretórios no caminho sejam criados.</span><span class="sxs-lookup"><span data-stu-id="c865b-137">The `-p` parameter causes all directories in the path to be created.</span></span> <span data-ttu-id="c865b-138">O diretório de **dados** é usado para armazenar dados usados pelo script **useooziewf.hql**.</span><span class="sxs-lookup"><span data-stu-id="c865b-138">The **data** directory is used to hold data used by the **useooziewf.hql** script.</span></span>

<span data-ttu-id="c865b-139">Além disso, execute o seguinte comando, que garante que o Oozie possa representar a conta de usuário durante a execução de trabalhos de Hive e Sqoop.</span><span class="sxs-lookup"><span data-stu-id="c865b-139">Also run the following command, which ensures that Oozie can impersonate your user account when running Hive and Sqoop jobs.</span></span> <span data-ttu-id="c865b-140">Substitua **NOME DE USUÁRIO** pelo seu nome de logon:</span><span class="sxs-lookup"><span data-stu-id="c865b-140">Replace **USERNAME** with your login name:</span></span>

```
sudo adduser USERNAME users
```

> [!NOTE]
> <span data-ttu-id="c865b-141">Você pode ignorar os erros que indicam o usuário como já sendo membro do grupo `users`.</span><span class="sxs-lookup"><span data-stu-id="c865b-141">You can ignore errors that the user is already a member of the `users` group.</span></span>

## <a name="add-a-database-driver"></a><span data-ttu-id="c865b-142">Adicionar um driver de banco de dados</span><span class="sxs-lookup"><span data-stu-id="c865b-142">Add a database driver</span></span>

<span data-ttu-id="c865b-143">Como esse fluxo de trabalho usa Sqoop para exportar dados para o banco de dados SQL, você deve fornecer uma cópia do driver JDBC usado para se comunicar com o Banco de Dados SQL.</span><span class="sxs-lookup"><span data-stu-id="c865b-143">Since this workflow uses Sqoop to export data to SQL Database, you must provide a copy of the JDBC driver used to talk to SQL Database.</span></span> <span data-ttu-id="c865b-144">Use o seguinte comando para copiá-lo para o diretório de trabalho:</span><span class="sxs-lookup"><span data-stu-id="c865b-144">Use the following command to copy it to the working directory:</span></span>

```
hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc*.jar /tutorials/useoozie/
```

<span data-ttu-id="c865b-145">Caso o fluxo de trabalho tenha usado outros recursos, como um jar que contém um aplicativo MapReduce, você precisará adicionar esses recursos também.</span><span class="sxs-lookup"><span data-stu-id="c865b-145">If your workflow used other resources, such as a jar containing a MapReduce application, you would need to add these resources as well.</span></span>

## <a name="define-the-hive-query"></a><span data-ttu-id="c865b-146">Definir a consulta de Hive</span><span class="sxs-lookup"><span data-stu-id="c865b-146">Define the Hive query</span></span>

<span data-ttu-id="c865b-147">Use as seguintes etapas para criar um script HiveQL que define uma consulta, que será usada em um fluxo de trabalho Oozie mais adiante neste documento.</span><span class="sxs-lookup"><span data-stu-id="c865b-147">Use the following steps to create a HiveQL script that defines a query, which is used in an Oozie workflow later in this document.</span></span>

1. <span data-ttu-id="c865b-148">Conecte-se ao cluster usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="c865b-148">Connect to the cluster using SSH.</span></span> <span data-ttu-id="c865b-149">O comando a seguir é um exemplo de como usar o comando `ssh`.</span><span class="sxs-lookup"><span data-stu-id="c865b-149">The following command is an example of using the `ssh` command.</span></span> <span data-ttu-id="c865b-150">Substitua __NOMEDOUSUÁRIO__ pelo nome de usuário SSH do cluster.</span><span class="sxs-lookup"><span data-stu-id="c865b-150">Replace __USERNAME__ with the SSH user for the cluster.</span></span> <span data-ttu-id="c865b-151">Substitua __NOMEDOCLUSTER__ pelo nome do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c865b-151">Replace __CLUSTERNAME__ with the name of the HDInsight cluster.</span></span>

    ```
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="c865b-152">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="c865b-152">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="c865b-153">Na conexão SSH, use o seguinte comando para criar um arquivo:</span><span class="sxs-lookup"><span data-stu-id="c865b-153">From the SSH connection, use the following command to create a file:</span></span>

    ```
    nano useooziewf.hql
    ```

3. <span data-ttu-id="c865b-154">Quando o editor nano for aberto, use a seguinte consulta como o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="c865b-154">Once the nano editor opens, use the following query as the contents of the file:</span></span>

    ```hiveql
    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(deviceplatform string, count string) ROW FORMAT DELIMITED
    FIELDS TERMINATED BY '\t' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE TABLE ${hiveTableName} SELECT deviceplatform, COUNT(*) as count FROM hivesampletable GROUP BY deviceplatform;
    ```

    <span data-ttu-id="c865b-155">Duas variáveis são usadas no script:</span><span class="sxs-lookup"><span data-stu-id="c865b-155">There are two variables used in the script:</span></span>

    * <span data-ttu-id="c865b-156">**${hiveTableName}**: contém o nome da tabela a ser criada</span><span class="sxs-lookup"><span data-stu-id="c865b-156">**${hiveTableName}**: contains the name of the table to be created</span></span>

    * <span data-ttu-id="c865b-157">**${hiveDataFolder}**: contém o local para armazenar os arquivos de dados para a tabela</span><span class="sxs-lookup"><span data-stu-id="c865b-157">**${hiveDataFolder}**: contains the location to store the data files for the table</span></span>

    <span data-ttu-id="c865b-158">O arquivo de definição do fluxo de trabalho (workflow.xml neste tutorial) passa esses valores para o script HiveQL no tempo de execução</span><span class="sxs-lookup"><span data-stu-id="c865b-158">The workflow definition file (workflow.xml in this tutorial) passes these values to this HiveQL script at run time</span></span>

4. <span data-ttu-id="c865b-159">Para sair do editor, pressione Ctrl-X.</span><span class="sxs-lookup"><span data-stu-id="c865b-159">To exit the editor, press Ctrl-X.</span></span> <span data-ttu-id="c865b-160">Quando solicitado, selecione **Y** para salvar o arquivo e, em seguida, use **Enter** para usar o nome de arquivo **useooziewf.hql**.</span><span class="sxs-lookup"><span data-stu-id="c865b-160">When prompted, select **Y** to save the file, then use **Enter** to use the **useooziewf.hql** file name.</span></span>

5. <span data-ttu-id="c865b-161">Use os seguintes comandos para copiar **useooziewf.hql** para **wasb:///tutorials/useoozie/useooziewf.hql**:</span><span class="sxs-lookup"><span data-stu-id="c865b-161">Use the following commands to copy **useooziewf.hql** to **wasb:///tutorials/useoozie/useooziewf.hql**:</span></span>

    ```
    hdfs dfs -put useooziewf.hql /tutorials/useoozie/useooziewf.hql
    ```

    <span data-ttu-id="c865b-162">Esses comandos armazenam o arquivo **useooziewf.hql** no armazenamento compatível com o HDFS para o cluster.</span><span class="sxs-lookup"><span data-stu-id="c865b-162">These commands store the **useooziewf.hql** file on the HDFS-compatible storage for the cluster.</span></span>

## <a name="define-the-workflow"></a><span data-ttu-id="c865b-163">Definir o fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="c865b-163">Define the workflow</span></span>

<span data-ttu-id="c865b-164">As definições de fluxos de trabalho do Oozie são escritas em hPDL (uma Linguagem de Definição de Processo XML).</span><span class="sxs-lookup"><span data-stu-id="c865b-164">Oozie workflows definitions are written in hPDL (an XML Process Definition Language).</span></span> <span data-ttu-id="c865b-165">Use as etapas a seguir para definir o fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="c865b-165">Use the following steps to define the workflow:</span></span>

1. <span data-ttu-id="c865b-166">Use a instrução a seguir para criar e editar um novo arquivo:</span><span class="sxs-lookup"><span data-stu-id="c865b-166">Use the following statement to create and edit a new file:</span></span>

    ```
    nano workflow.xml
    ```

2. <span data-ttu-id="c865b-167">Quando o editor nano for aberto, insira o seguinte XML como o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="c865b-167">Once the nano editor opens, enter the following XML as the file contents:</span></span>

    ```xml
    <workflow-app name="useooziewf" xmlns="uri:oozie:workflow:0.2">
        <start to = "RunHiveScript"/>
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

    <span data-ttu-id="c865b-168">Existem duas ações definidas no fluxo de trabalho:</span><span class="sxs-lookup"><span data-stu-id="c865b-168">There are two actions defined in the workflow:</span></span>

   * <span data-ttu-id="c865b-169">**RunHiveScript**: essa ação é a ação inicial e executa o script do Hive **useooziewf.hql**</span><span class="sxs-lookup"><span data-stu-id="c865b-169">**RunHiveScript**: This action is the start action, and runs the **useooziewf.hql** Hive script</span></span>

   * <span data-ttu-id="c865b-170">**RunSqoopExport**: essa ação exporta os dados criados por meio do script do Hive para o Banco de Dados SQL usando o Sqoop.</span><span class="sxs-lookup"><span data-stu-id="c865b-170">**RunSqoopExport**: This action exports the data created from the Hive script to SQL Database using Sqoop.</span></span> <span data-ttu-id="c865b-171">Essa ação será executada apenas se a ação **RunHiveScript** for bem-sucedida.</span><span class="sxs-lookup"><span data-stu-id="c865b-171">This action only runs if the **RunHiveScript** action is successful.</span></span>

     <span data-ttu-id="c865b-172">O fluxo de trabalho tem várias entradas, como `${jobTracker}`.</span><span class="sxs-lookup"><span data-stu-id="c865b-172">The workflow has several entries, such as `${jobTracker}`.</span></span> <span data-ttu-id="c865b-173">Essas entradas são substituídas por valores usados na definição de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-173">These entries are replaced by values you use in the job definition.</span></span> <span data-ttu-id="c865b-174">A definição de trabalho é criada mais tarde neste documento.</span><span class="sxs-lookup"><span data-stu-id="c865b-174">The job definition is created later in this document.</span></span>

     <span data-ttu-id="c865b-175">Observe também a entrada `<archive>sqljdbc4.jar</arcive>` na seção Sqoop.</span><span class="sxs-lookup"><span data-stu-id="c865b-175">Also note the `<archive>sqljdbc4.jar</arcive>` entry in the Sqoop section.</span></span> <span data-ttu-id="c865b-176">Essa entrada instrui o Oozie a disponibilizar esse arquivo morto ao Sqoop quando essa ação é executada.</span><span class="sxs-lookup"><span data-stu-id="c865b-176">This entry instructs Oozie to make this archive available for Sqoop when this action runs.</span></span>

3. <span data-ttu-id="c865b-177">Use Ctrl-X e, em seguida, **Y** e **Enter** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="c865b-177">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

4. <span data-ttu-id="c865b-178">Use o comando a seguir para copiar o arquivo **workflow.xml** para **/tutorials/useoozie/workflow.xml**:</span><span class="sxs-lookup"><span data-stu-id="c865b-178">Use the following command to copy the **workflow.xml** file to **/tutorials/useoozie/workflow.xml**:</span></span>

    ```
    hdfs dfs -put workflow.xml /tutorials/useoozie/workflow.xml
    ```

## <a name="create-the-database"></a><span data-ttu-id="c865b-179">Criar o banco de dados</span><span class="sxs-lookup"><span data-stu-id="c865b-179">Create the database</span></span>

<span data-ttu-id="c865b-180">Para criar um Banco de Dados SQL do Azure, siga as etapas do documento [Criar um Banco de Dados SQL](../sql-database/sql-database-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="c865b-180">To create an Azure SQL Database, follow the steps in the [Create a SQL Database](../sql-database/sql-database-get-started.md) document.</span></span> <span data-ttu-id="c865b-181">Ao criar o banco de dados, use `oozietest` como o nome do banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c865b-181">When creating the database, use `oozietest` as the database name.</span></span> <span data-ttu-id="c865b-182">Além disso, anote o nome do servidor de banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c865b-182">Also make a note of the name of the database server.</span></span>

### <a name="create-the-table"></a><span data-ttu-id="c865b-183">Criar a tabela.</span><span class="sxs-lookup"><span data-stu-id="c865b-183">Create the table</span></span>

> [!NOTE]
> <span data-ttu-id="c865b-184">Há várias maneiras para se conectar ao Banco de Dados SQL para criar uma tabela.</span><span class="sxs-lookup"><span data-stu-id="c865b-184">There are many ways to connect to SQL Database to create a table.</span></span> <span data-ttu-id="c865b-185">As seguintes etapas usam [FreeTDS](http://www.freetds.org/) do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c865b-185">The following steps use [FreeTDS](http://www.freetds.org/) from the HDInsight cluster.</span></span>


1. <span data-ttu-id="c865b-186">Use o seguinte comando para instalar o FreeTDS no cluster do HDInsight:</span><span class="sxs-lookup"><span data-stu-id="c865b-186">Use the following command to install FreeTDS on the HDInsight cluster:</span></span>

    ```
    sudo apt-get --assume-yes install freetds-dev freetds-bin
    ```

2. <span data-ttu-id="c865b-187">Uma vez que o FreeTDS tiver sido instalado, use o seguinte comando para conectar-se ao Banco de Dados SQL Server criado anteriormente:</span><span class="sxs-lookup"><span data-stu-id="c865b-187">Once FreeTDS has been installed, use the following command to connect to the SQL Database server you created previously:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <sqlLogin> -P <sqlPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="c865b-188">Você receberá saídas semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="c865b-188">You receive output similar to the following text:</span></span>

        locale is "en_US.UTF-8"
        locale charset is "UTF-8"
        using default charset "UTF-8"
        Default database being set to oozietest
        1>

3. <span data-ttu-id="c865b-189">Ao prompt `1>` , insira o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c865b-189">At the `1>` prompt, enter the following lines:</span></span>

    ```
    CREATE TABLE [dbo].[mobiledata](
    [deviceplatform] [nvarchar](50),
    [count] [bigint])
    GO
    CREATE CLUSTERED INDEX mobiledata_clustered_index on mobiledata(deviceplatform)
    GO
    ```

    <span data-ttu-id="c865b-190">Quando a instrução `GO` for inserida, as instruções anteriores serão avaliadas.</span><span class="sxs-lookup"><span data-stu-id="c865b-190">When the `GO` statement is entered, the previous statements are evaluated.</span></span> <span data-ttu-id="c865b-191">Essas instruções criam uma tabela chamada **mobiledata** que é usada pelo fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-191">These statements create a table named **mobiledata** that is used by the workflow.</span></span>

    <span data-ttu-id="c865b-192">Use o seguinte para verificar se a tabela foi criada:</span><span class="sxs-lookup"><span data-stu-id="c865b-192">Use the following to verify that the table has been created:</span></span>

    ```
    SELECT * FROM information_schema.tables
    GO
    ```

    <span data-ttu-id="c865b-193">Você verá uma saída semelhante ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="c865b-193">You see output similar to the following text:</span></span>

    ```
    TABLE_CATALOG   TABLE_SCHEMA    TABLE_NAME      TABLE_TYPE
    oozietest       dbo     mobiledata      BASE TABLE
    ```

4. <span data-ttu-id="c865b-194">Para sair do utilitário tsql, insira `exit` at the `1>` .</span><span class="sxs-lookup"><span data-stu-id="c865b-194">Enter `exit` at the `1>` prompt to exit the tsql utility.</span></span>

## <a name="create-the-job-definition"></a><span data-ttu-id="c865b-195">Criar a definição de trabalho</span><span class="sxs-lookup"><span data-stu-id="c865b-195">Create the job definition</span></span>

<span data-ttu-id="c865b-196">A definição de trabalho descreve o local em que o workflow.xml se encontra.</span><span class="sxs-lookup"><span data-stu-id="c865b-196">The job definition describes where to find the workflow.xml.</span></span> <span data-ttu-id="c865b-197">Ela também descreve o local em que você pode encontrar outros arquivos usados pelo fluxo de trabalho (como useooziewf.hql). Isso também define os valores para as propriedades usadas no fluxo de trabalho e arquivos associados.</span><span class="sxs-lookup"><span data-stu-id="c865b-197">It also describes where to find other files used by the workflow (such as useooziewf.hql.) It also defines the values for properties used within the workflow and associated files.</span></span>

1. <span data-ttu-id="c865b-198">Use o comando a seguir para obter o endereço completo do armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="c865b-198">Use the following command to get the full address of the default storage.</span></span> <span data-ttu-id="c865b-199">Este endereço será usado no arquivo de configuração em breve:</span><span class="sxs-lookup"><span data-stu-id="c865b-199">This address is used in the configuration file in a moment:</span></span>

    ```
    sed -n '/<name>fs.default/,/<\/value>/p' /etc/hadoop/conf/core-site.xml
    ```

    <span data-ttu-id="c865b-200">Este comando retorna informações semelhantes ao seguinte XML:</span><span class="sxs-lookup"><span data-stu-id="c865b-200">This command returns information similar to the following XML:</span></span>

    ```xml
    <name>fs.defaultFS</name>
    <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net</value>
    ```

    > [!NOTE]
    > <span data-ttu-id="c865b-201">Se o cluster HDInsight usa o armazenamento do Azure como o armazenamento padrão, o conteúdo de elemento `<value>` começa com `wasb://`.</span><span class="sxs-lookup"><span data-stu-id="c865b-201">If the HDInsight cluster uses Azure Storage as the default storage, the `<value>` element contents begin with `wasb://`.</span></span> <span data-ttu-id="c865b-202">Se o Azure Data Lake Store é usado, ele começa com `adl://`.</span><span class="sxs-lookup"><span data-stu-id="c865b-202">If Azure Data Lake Store is used instead, it begins with `adl://`.</span></span>

    <span data-ttu-id="c865b-203">Salve o conteúdo do elemento `<value>`, pois ele será usado nas próximas etapas.</span><span class="sxs-lookup"><span data-stu-id="c865b-203">Save the contents of the `<value>` element, as it is used in the next steps.</span></span>

2. <span data-ttu-id="c865b-204">Use o seguinte comando para obter o FQDN do headnode do cluster.</span><span class="sxs-lookup"><span data-stu-id="c865b-204">Use the following command to get FQDN of the cluster headnode.</span></span> <span data-ttu-id="c865b-205">Estas informações são usadas para o endereço do JobTracker no cluster:</span><span class="sxs-lookup"><span data-stu-id="c865b-205">This information is used for the JobTracker address for the cluster:</span></span>

    ```
    hostname -f
    ```

    <span data-ttu-id="c865b-206">Isso retorna informações semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="c865b-206">This returns information similar to the following text:</span></span>

    ```hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net```

    <span data-ttu-id="c865b-207">A porta usada para o JobTracker é a 8050, portanto, o endereço completo a ser usado para o JobTracker é `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span><span class="sxs-lookup"><span data-stu-id="c865b-207">The port used for the JobTracker is 8050, so the full address to use for the JobTracker is `hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:8050`.</span></span>

3. <span data-ttu-id="c865b-208">Use o seguinte para criar a configuração de definição de trabalho do Oozie:</span><span class="sxs-lookup"><span data-stu-id="c865b-208">Use the following to create the Oozie job definition configuration:</span></span>

    ```
    nano job.xml
    ```

4. <span data-ttu-id="c865b-209">Quando o editor nano for aberto, use o seguinte XML como o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="c865b-209">Once the nano editor opens, use the following XML as the contents of the file:</span></span>

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

   * <span data-ttu-id="c865b-210">Substitua todas as instâncias de **wasb://mycontainer@mystorageaccount.blob.core.windows.net** pelo valor que você recebeu anteriormente para armazenamento padrão.</span><span class="sxs-lookup"><span data-stu-id="c865b-210">Replace all instances of **wasb://mycontainer@mystorageaccount.blob.core.windows.net** with the value you received earlier for default storage.</span></span>

     > [!WARNING]
     > <span data-ttu-id="c865b-211">Se o caminho for um caminho `wasb`, use o caminho completo.</span><span class="sxs-lookup"><span data-stu-id="c865b-211">If the path is a `wasb` path, you must use the full path.</span></span> <span data-ttu-id="c865b-212">Não o reduza para apenas `wasb:///`.</span><span class="sxs-lookup"><span data-stu-id="c865b-212">Do not shorten it to just `wasb:///`.</span></span>

   * <span data-ttu-id="c865b-213">Substitua **JOBTRACKERADDRESS** pelo endereço de JobTracker/ResourceManager recebido anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c865b-213">Replace **JOBTRACKERADDRESS** with the JobTracker/ResourceManager address you received earlier.</span></span>
   * <span data-ttu-id="c865b-214">Substitua **YourName** pelo seu nome de logon para o cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c865b-214">Replace **YourName** with your login name for the HDInsight cluster.</span></span>
   * <span data-ttu-id="c865b-215">Substitua **serverName**, **adminLogin** e **adminPassword** pelas informações de seu Banco de Dados SQL do Azure.</span><span class="sxs-lookup"><span data-stu-id="c865b-215">Replace **serverName**, **adminLogin**, and **adminPassword** with the information for your Azure SQL Database.</span></span>

     <span data-ttu-id="c865b-216">A maioria das informações contidas nesse arquivo é usada para preencher os valores usados nos arquivos workflow.xml ou ooziewf.hql (por exemplo, ${nameNode}.)</span><span class="sxs-lookup"><span data-stu-id="c865b-216">Most of the information in this file is used to populate the values used in the workflow.xml or ooziewf.hql files (such as ${nameNode}.)</span></span>

     > [!NOTE]
     > <span data-ttu-id="c865b-217">A entrada **oozie.wf.application.path** define onde encontrar o arquivo workflow.xml, que contém o fluxo de trabalho executado por esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-217">The **oozie.wf.application.path** entry defines where to find the workflow.xml file, which contains the workflow ran by this job.</span></span>

5. <span data-ttu-id="c865b-218">Use Ctrl-X e, em seguida, **Y** e **Enter** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="c865b-218">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

## <a name="submit-and-manage-the-job"></a><span data-ttu-id="c865b-219">Enviar e gerenciar o trabalho</span><span class="sxs-lookup"><span data-stu-id="c865b-219">Submit and manage the job</span></span>

<span data-ttu-id="c865b-220">As etapas a seguir usam o comando Oozie para enviar e gerenciar fluxos de trabalho do Oozie no cluster.</span><span class="sxs-lookup"><span data-stu-id="c865b-220">The following steps use the Oozie command to submit and manage Oozie workflows on the cluster.</span></span> <span data-ttu-id="c865b-221">O comando do Oozie é uma interface amigável sobre a [API REST do Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="c865b-221">The Oozie command is a friendly interface over the [Oozie REST API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c865b-222">Ao usar o comando Oozie, você deve usar o FQDN para headnode do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c865b-222">When using the Oozie command, you must use the FQDN for the HDInsight headnode.</span></span> <span data-ttu-id="c865b-223">Esse FQDN só está acessível no cluster ou, se o cluster estiver em uma Rede Virtual do Azure, de outros computadores na mesma rede.</span><span class="sxs-lookup"><span data-stu-id="c865b-223">This FQDN is only accessible from the cluster, or if the cluster is on an Azure Virtual Network, from other machines on the same network.</span></span>


1. <span data-ttu-id="c865b-224">Use o seguinte para obter a URL para o serviço do Oozie:</span><span class="sxs-lookup"><span data-stu-id="c865b-224">Use the following to obtain the URL to the Oozie service:</span></span>

    ```
    sed -n '/<name>oozie.base.url/,/<\/value>/p' /etc/oozie/conf/oozie-site.xml
    ```

    <span data-ttu-id="c865b-225">Isso retorna informações semelhantes ao seguinte XML:</span><span class="sxs-lookup"><span data-stu-id="c865b-225">This returns information similar to the following XML:</span></span>

    ```xml
    <name>oozie.base.url</name>
    <value>http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie</value>
    ```

    <span data-ttu-id="c865b-226">A parte `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` é a URL a ser usada com o comando do Oozie.</span><span class="sxs-lookup"><span data-stu-id="c865b-226">The `http://hn0-CLUSTERNAME.randomcharacters.cx.internal.cloudapp.net:11000/oozie` portion is the URL to use with the Oozie command.</span></span>

2. <span data-ttu-id="c865b-227">Use o seguinte para criar uma variável de ambiente para a URL para que você não precise digitá-la para cada comando:</span><span class="sxs-lookup"><span data-stu-id="c865b-227">Use the following to create an environment variable for the URL, so you don't have to type it for every command:</span></span>

    ```
    export OOZIE_URL=http://HOSTNAMEt:11000/oozie
    ```

    <span data-ttu-id="c865b-228">Substitua a URL pela recebida anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c865b-228">Replace the URL with the one you received earlier.</span></span>
3. <span data-ttu-id="c865b-229">Use o seguinte para enviar o trabalho:</span><span class="sxs-lookup"><span data-stu-id="c865b-229">Use the following to submit the job:</span></span>

    ```
    oozie job -config job.xml -submit
    ```

    <span data-ttu-id="c865b-230">Esse comando carrega as informações do trabalho de **job.xml** e as envia para o Oozie, mas não o executa.</span><span class="sxs-lookup"><span data-stu-id="c865b-230">This command loads the job information from **job.xml** and submits it to Oozie, but does not run it.</span></span>

    <span data-ttu-id="c865b-231">Quando o comando for concluído, ele deverá retornar a ID do trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-231">Once the command completes, it should return the ID of the job.</span></span> <span data-ttu-id="c865b-232">Por exemplo: `0000005-150622124850154-oozie-oozi-W`.</span><span class="sxs-lookup"><span data-stu-id="c865b-232">For example, `0000005-150622124850154-oozie-oozi-W`.</span></span> <span data-ttu-id="c865b-233">Essa ID será usada para gerenciar o trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-233">This ID is used to manage the job.</span></span>

4. <span data-ttu-id="c865b-234">Exiba o status do trabalho usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c865b-234">View the status of the job using the following command:</span></span>

    ```
    oozie job -info <JOBID>
    ```

    > [!NOTE]
    > <span data-ttu-id="c865b-235">Substitua `<JOBID>` pela ID retornada na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="c865b-235">Replace `<JOBID>` with the ID returned in the previous step.</span></span>

    <span data-ttu-id="c865b-236">Isso retorna informações semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="c865b-236">This returns information similar to the following text:</span></span>

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

    <span data-ttu-id="c865b-237">Este trabalho tem o status `PREP`.</span><span class="sxs-lookup"><span data-stu-id="c865b-237">This job has a status of `PREP`.</span></span> <span data-ttu-id="c865b-238">Este status indica que o trabalho foi criado, mas não foi iniciado.</span><span class="sxs-lookup"><span data-stu-id="c865b-238">This status indicates that the job was created, but not started.</span></span>

5. <span data-ttu-id="c865b-239">Use o seguinte comando para iniciar o trabalho:</span><span class="sxs-lookup"><span data-stu-id="c865b-239">Use the following command to start the job:</span></span>

    ```
    oozie job -start JOBID
    ```

    > [!NOTE]
    > <span data-ttu-id="c865b-240">Substitua `<JOBID>` pela ID retornada anteriormente.</span><span class="sxs-lookup"><span data-stu-id="c865b-240">Replace `<JOBID>` with the ID returned previously.</span></span>

    <span data-ttu-id="c865b-241">Se você verificar o status após este comando, ele estará em um estado de execução e as informações serão retornadas para as ações dentro do trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-241">If you check the status after this command, it is in a running state, and information is returned for the actions within the job.</span></span>

6. <span data-ttu-id="c865b-242">Depois que a tarefa for concluída com sucesso, você poderá verificar se os dados foram gerados e exportados para a tabela do Banco de Dados SQL usando os seguintes comandos:</span><span class="sxs-lookup"><span data-stu-id="c865b-242">Once the task completes successfully, you can verify that the data was generated and exported to the SQL Database table by using the following commands:</span></span>

    ```
    TDSVER=8.0 tsql -H <serverName>.database.windows.net -U <adminLogin> -P <adminPassword> -p 1433 -D oozietest
    ```

    <span data-ttu-id="c865b-243">No prompt `1>`, insira a seguinte consulta:</span><span class="sxs-lookup"><span data-stu-id="c865b-243">At the `1>` prompt, enter the following query:</span></span>

    ```
    SELECT * FROM mobiledata
    GO
    ```

    <span data-ttu-id="c865b-244">As informações retornadas são semelhantes ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="c865b-244">The information returned is similar to the following text:</span></span>

        deviceplatform  count
        Android 31591
        iPhone OS       22731
        proprietary development 3
        RIM OS  3464
        Unknown 213
        Windows Phone   1791
        (6 rows affected)

<span data-ttu-id="c865b-245">Para obter mais informações sobre o comando do Oozie, consulte [Ferramenta de linha de comando do Oozie](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span><span class="sxs-lookup"><span data-stu-id="c865b-245">For more information on the Oozie command, see [Oozie command-line tool](https://oozie.apache.org/docs/4.1.0/DG_CommandLineTool.html).</span></span>

## <a name="oozie-rest-api"></a><span data-ttu-id="c865b-246">API REST do Oozie</span><span class="sxs-lookup"><span data-stu-id="c865b-246">Oozie REST API</span></span>

<span data-ttu-id="c865b-247">A API REST do Oozie permite que você crie suas próprias ferramentas que funcionam com o Oozie.</span><span class="sxs-lookup"><span data-stu-id="c865b-247">The Oozie REST API allows you to build your own tools that work with Oozie.</span></span> <span data-ttu-id="c865b-248">A seguir estão informações específicas do HDInsight sobre como usar a API REST do Oozie:</span><span class="sxs-lookup"><span data-stu-id="c865b-248">The following are HDInsight specific information about using the Oozie REST API:</span></span>

* <span data-ttu-id="c865b-249">**URI**: a API REST pode ser acessada de fora do cluster em `https://CLUSTERNAME.azurehdinsight.net/oozie`</span><span class="sxs-lookup"><span data-stu-id="c865b-249">**URI**: The REST API can be accessed from outside the cluster at `https://CLUSTERNAME.azurehdinsight.net/oozie`</span></span>

* <span data-ttu-id="c865b-250">**Autenticação**: faça a autenticação na API usando a conta HTTP do cluster (admin) e a senha.</span><span class="sxs-lookup"><span data-stu-id="c865b-250">**Authentication**: Authenticate to the API using the cluster HTTP account (admin) and password.</span></span> <span data-ttu-id="c865b-251">Por exemplo:</span><span class="sxs-lookup"><span data-stu-id="c865b-251">For example:</span></span>

    ```
    curl -u admin:PASSWORD https://CLUSTERNAME.azurehdinsight.net/oozie/versions
    ```

<span data-ttu-id="c865b-252">Para obter mais informações sobre como usar a API REST do Oozie, consulte [API de serviços Web do Oozie](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span><span class="sxs-lookup"><span data-stu-id="c865b-252">For more information on using the Oozie REST API, see [Oozie Web Services API](https://oozie.apache.org/docs/4.1.0/WebServicesAPI.html).</span></span>

## <a name="oozie-web-ui"></a><span data-ttu-id="c865b-253">Interface da Web do Oozie</span><span class="sxs-lookup"><span data-stu-id="c865b-253">Oozie Web UI</span></span>

<span data-ttu-id="c865b-254">A IU da Web do Oozie fornece um modo de exibição baseado na web sobre o status dos trabalhos do Oozie no cluster.</span><span class="sxs-lookup"><span data-stu-id="c865b-254">The Oozie Web UI provides a web-based view into the status of Oozie jobs on the cluster.</span></span> <span data-ttu-id="c865b-255">A interface do usuário da Web permite exibir as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="c865b-255">The web UI allows you to view the following information:</span></span>

* <span data-ttu-id="c865b-256">Status do trabalho</span><span class="sxs-lookup"><span data-stu-id="c865b-256">Job status</span></span>
* <span data-ttu-id="c865b-257">Definição de trabalho</span><span class="sxs-lookup"><span data-stu-id="c865b-257">Job definition</span></span>
* <span data-ttu-id="c865b-258">Configuração</span><span class="sxs-lookup"><span data-stu-id="c865b-258">Configuration</span></span>
* <span data-ttu-id="c865b-259">Um gráfico das ações no trabalho</span><span class="sxs-lookup"><span data-stu-id="c865b-259">A graph of the actions in the job</span></span>
* <span data-ttu-id="c865b-260">Logs do trabalho</span><span class="sxs-lookup"><span data-stu-id="c865b-260">Logs for the job</span></span>

<span data-ttu-id="c865b-261">Você também pode exibir detalhes de ações dentro de um trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-261">You can also view details for actions within a job.</span></span>

<span data-ttu-id="c865b-262">Para acessar a interface do usuário do Oozie da Web, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c865b-262">To access the Oozie Web UI, use the following steps:</span></span>

1. <span data-ttu-id="c865b-263">Crie um túnel SSH para o cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="c865b-263">Create an SSH tunnel to the HDInsight cluster.</span></span> <span data-ttu-id="c865b-264">Para obter informações, consulte o documento [Usar o túnel SSH com o HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="c865b-264">For information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="c865b-265">Quando um túnel tiver sido criado, abra a interface do usuário da Web do Ambari no navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="c865b-265">Once a tunnel has been created, open the Ambari web UI in your web browser.</span></span> <span data-ttu-id="c865b-266">O URI para o site Ambari é **https://CLUSTERNAME.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="c865b-266">The URI for the Ambari site is **https://CLUSTERNAME.azurehdinsight.net**.</span></span> <span data-ttu-id="c865b-267">Substitua **CLUSTERNAME** pelo nome do seu cluster do HDInsight baseado em Linux.</span><span class="sxs-lookup"><span data-stu-id="c865b-267">Replace **CLUSTERNAME** with the name of your Linux-based HDInsight cluster.</span></span>

3. <span data-ttu-id="c865b-268">No lado esquerdo da página, selecione **Oozie** e, em seguida, **Links rápidos** e, finalmente, **Interface do usuário da Web do Oozie**.</span><span class="sxs-lookup"><span data-stu-id="c865b-268">From the left side of the page, select **Oozie**, then **Quick Links**, and finally **Oozie Web UI**.</span></span>

    ![imagem dos menus](./media/hdinsight-use-oozie-linux-mac/ooziewebuisteps.png)

4. <span data-ttu-id="c865b-270">A interface do usuário da Web do Oozie assume como padrão a exibição de Trabalhos do fluxo de trabalho em execução.</span><span class="sxs-lookup"><span data-stu-id="c865b-270">The Oozie Web UI defaults to displaying running Workflow Jobs.</span></span> <span data-ttu-id="c865b-271">Para ver todos os trabalhos de fluxo de trabalho, selecione **Todos os trabalhos**.</span><span class="sxs-lookup"><span data-stu-id="c865b-271">To see all workflow jobs, select **All Jobs**.</span></span>

    ![Todos os trabalhos exibidos](./media/hdinsight-use-oozie-linux-mac/ooziejobs.png)

5. <span data-ttu-id="c865b-273">Selecione um trabalho para exibir mais informações sobre ele.</span><span class="sxs-lookup"><span data-stu-id="c865b-273">Select a job to view more information about the job.</span></span>

    ![Informações do Trabalho](./media/hdinsight-use-oozie-linux-mac/jobinfo.png)

6. <span data-ttu-id="c865b-275">Na guia Informações do Trabalho, veja informações básicas sobre o trabalho, bem como as ações individuais dentro do trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-275">From the Job Info tab, you can see basic job information and the individual actions within the job.</span></span> <span data-ttu-id="c865b-276">Usando as guias na parte superior, você pode ver a Definição de trabalho, a Configuração de trabalho, acessar o Log de trabalho ou ver um gráfico acíclico dirigido (DAG) do trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-276">Using the tabs at the top you can view the Job Definition, Job Configuration, access the Job Log or view a Directed Acyclic Graph (DAG) of the job.</span></span>

   * <span data-ttu-id="c865b-277">**Log de trabalho**: selecione o botão **GetLogs** para obter todos os logs do trabalho, ou use o campo **Inserir filtro de pesquisa** para filtrar os logs</span><span class="sxs-lookup"><span data-stu-id="c865b-277">**Job Log**: Select the **GetLogs** button to get all logs for the job, or use the **Enter Search Filter** field to filter logs</span></span>

       ![Log de trabalhos](./media/hdinsight-use-oozie-linux-mac/joblog.png)

   * <span data-ttu-id="c865b-279">**JobDAG**: o DAG é uma visão geral gráfica dos caminhos de dados percorridos pelo fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="c865b-279">**JobDAG**: The DAG is a graphical overview of the data paths taken through the workflow</span></span>

       ![DAG de trabalho](./media/hdinsight-use-oozie-linux-mac/jobdag.png)

7. <span data-ttu-id="c865b-281">Selecionar uma das ações na guia **Informações do Trabalho** exibe informações para a ação.</span><span class="sxs-lookup"><span data-stu-id="c865b-281">Selecting one of the actions from the **Job Info** tab brings up information for the action.</span></span> <span data-ttu-id="c865b-282">Por exemplo, selecione a ação **RunHiveScript** .</span><span class="sxs-lookup"><span data-stu-id="c865b-282">For example, select the **RunHiveScript** action.</span></span>

    ![Informações da ação](./media/hdinsight-use-oozie-linux-mac/action.png)

8. <span data-ttu-id="c865b-284">Você pode ver detalhes da ação, como um link para a **URL do Console**.</span><span class="sxs-lookup"><span data-stu-id="c865b-284">You can see details for the action, such as a link to the **Console URL**.</span></span> <span data-ttu-id="c865b-285">Esse link pode ser usado para exibir informações do JobTracker para o trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-285">This link can be used to view JobTracker information for the job.</span></span>

## <a name="scheduling-jobs"></a><span data-ttu-id="c865b-286">Agendamento de trabalhos</span><span class="sxs-lookup"><span data-stu-id="c865b-286">Scheduling jobs</span></span>

<span data-ttu-id="c865b-287">O coordenador permite que você especifique um início, um fim e a frequência de ocorrência para trabalhos.</span><span class="sxs-lookup"><span data-stu-id="c865b-287">The coordinator allows you to specify a start, end, and occurrence frequency for jobs.</span></span> <span data-ttu-id="c865b-288">Para definir uma agenda para o fluxo de trabalho, use as seguintes etapas:</span><span class="sxs-lookup"><span data-stu-id="c865b-288">To define a schedule for the workflow, use the following steps:</span></span>

1. <span data-ttu-id="c865b-289">Use o seguinte para criar um arquivo chamado **coordinator.xml**:</span><span class="sxs-lookup"><span data-stu-id="c865b-289">Use the following to create a file named **coordinator.xml**:</span></span>

    ```
    nano coordinator.xml
    ```

    <span data-ttu-id="c865b-290">Use o seguinte XML como o conteúdo do arquivo:</span><span class="sxs-lookup"><span data-stu-id="c865b-290">Use the following XML as the contents of the file:</span></span>

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
    > <span data-ttu-id="c865b-291">As variáveis `${...}` são substituídas pelos valores na definição de trabalho em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="c865b-291">The `${...}` variables are replaced by values in the job definition at run-time.</span></span> <span data-ttu-id="c865b-292">As variáveis são:</span><span class="sxs-lookup"><span data-stu-id="c865b-292">The variables are:</span></span>
    >
    > * <span data-ttu-id="c865b-293">`${coordFrequency}`: tempo entre as instâncias em execução do trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-293">`${coordFrequency}`: Time between running instances of the job.</span></span>
    > <span data-ttu-id="c865b-294">** `${coordStart}`: a hora de início do trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-294">** `${coordStart}`: The job start time.</span></span>
    > * <span data-ttu-id="c865b-295">`${coordEnd}`: a hora de término do trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-295">`${coordEnd}`: The job end time.</span></span>
    > * <span data-ttu-id="c865b-296">`${coordTimezone}`: os trabalhos do coordenador estão em um fuso horário fixo sem horário de verão (geralmente representado com o uso do UTC).</span><span class="sxs-lookup"><span data-stu-id="c865b-296">`${coordTimezone}`: Coordinator jobs are in a fixed time zone with no daylight savings time (typically represented by using UTC).</span></span> <span data-ttu-id="c865b-297">Esse fuso horário é chamado de "fuso horário de processamento do Oozie".</span><span class="sxs-lookup"><span data-stu-id="c865b-297">This time zone is referred as the "Oozie processing timezone."</span></span>
    > * <span data-ttu-id="c865b-298">`${wfPath}`: o caminho para workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="c865b-298">`${wfPath}`: The path to the workflow.xml.</span></span>

2. <span data-ttu-id="c865b-299">Para salvar o arquivo, use Ctrl-X, **Y** e **Enter**.</span><span class="sxs-lookup"><span data-stu-id="c865b-299">To save the file, use Ctrl-X, **Y**, and **Enter**.</span></span>

3. <span data-ttu-id="c865b-300">Para copiar o arquivo para o diretório de trabalho para este trabalho, use o seguinte:</span><span class="sxs-lookup"><span data-stu-id="c865b-300">Use the following command to copy the file to the working directory for this job:</span></span>

    ```
    hadoop fs -put coordinator.xml /tutorials/useoozie/coordinator.xml
    ```

4. <span data-ttu-id="c865b-301">Use o seguinte para modificar o arquivo **job.xml** :</span><span class="sxs-lookup"><span data-stu-id="c865b-301">Use the following to modify the **job.xml** file:</span></span>

    ```
    nano job.xml
    ```

    <span data-ttu-id="c865b-302">Faça as seguintes alterações:</span><span class="sxs-lookup"><span data-stu-id="c865b-302">Make the following changes:</span></span>

   * <span data-ttu-id="c865b-303">Para instruir o Oozie a executar o arquivo coordenador em vez do de fluxo de trabalho, altere `<name>oozie.wf.application.path</name>` para `<name>oozie.coord.application.path</name>`.</span><span class="sxs-lookup"><span data-stu-id="c865b-303">To instruct oozie to run the coordinator file instead of the workflow, change `<name>oozie.wf.application.path</name>` to `<name>oozie.coord.application.path</name>`.</span></span>

   * <span data-ttu-id="c865b-304">Para definir o `workflowPath` variável usada pelo coordenador, adicione o XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="c865b-304">To set the `workflowPath` variable used by the coordinator, add the following XML:</span></span>

        ```xml
        <property>
            <name>workflowPath</name>
            <value>wasb://mycontainer@mystorageaccount.blob.core.windows.net/tutorials/useoozie</value>
        </property>
        ```

       <span data-ttu-id="c865b-305">Substitua o texto `wasb://mycontainer@mystorageaccount.blob.core.windows` pelo valor usado em outras entradas no arquivo job.xml.</span><span class="sxs-lookup"><span data-stu-id="c865b-305">Replace the `wasb://mycontainer@mystorageaccount.blob.core.windows` text with the value used in other entries in the job.xml file.</span></span>

   * <span data-ttu-id="c865b-306">Para definir o início, o fim e a frequência a usar para o coordenador, adicione o XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="c865b-306">To define the start, end, and frequency for the coordinator, add the following XML:</span></span>

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

       <span data-ttu-id="c865b-307">Esses valores definem a hora de início como 12h00 em 10 de maio de 10, 2017 e a hora de término como 12 de maio de 12, 2017.</span><span class="sxs-lookup"><span data-stu-id="c865b-307">These values set the start time to 12:00PM on May 10, 2017, the end time to May 12, 2017.</span></span> <span data-ttu-id="c865b-308">O intervalo para execução desse trabalho é diário.</span><span class="sxs-lookup"><span data-stu-id="c865b-308">The interval for running this job daily.</span></span> <span data-ttu-id="c865b-309">A frequência está em minutos, então 24 horas x 60 minutos = 1440 minutos.</span><span class="sxs-lookup"><span data-stu-id="c865b-309">The frequency is in minutes, so 24 hours x 60 minutes = 1440 minutes.</span></span> <span data-ttu-id="c865b-310">Por fim, o fuso horário é definido como UTC.</span><span class="sxs-lookup"><span data-stu-id="c865b-310">Finally, the timezone is set to UTC.</span></span>

5. <span data-ttu-id="c865b-311">Use Ctrl-X e, em seguida, **Y** e **Enter** para salvar o arquivo.</span><span class="sxs-lookup"><span data-stu-id="c865b-311">Use Ctrl-X, then **Y** and **Enter** to save the file.</span></span>

6. <span data-ttu-id="c865b-312">Para executar o trabalho, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="c865b-312">To run the job, use the following command:</span></span>

    ```
    oozie job -config job.xml -run
    ```

    <span data-ttu-id="c865b-313">Esse comando envia e inicia o trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-313">This command submits and starts the job.</span></span>

7. <span data-ttu-id="c865b-314">Se você visitar a interface do usuário da Web do Oozie e selecionar a guia **Trabalhos do Coordenador**, verá informações semelhantes à seguinte imagem:</span><span class="sxs-lookup"><span data-stu-id="c865b-314">If you visit the Oozie Web UI and select the **Coordinator Jobs** tab, you see information similar to the following image:</span></span>

    ![guia de trabalhos do coordenador](./media/hdinsight-use-oozie-linux-mac/coordinatorjob.png)

    <span data-ttu-id="c865b-316">A entrada **Próxima Materialização** contém a próxima hora em que o trabalho é executado.</span><span class="sxs-lookup"><span data-stu-id="c865b-316">The **Next Materialization** entry contains the next time that the job runs.</span></span>

8. <span data-ttu-id="c865b-317">De forma semelhante ao fluxo de trabalho anterior, selecionar a entrada de trabalho na interface do usuário da Web exibirá informações sobre o trabalho:</span><span class="sxs-lookup"><span data-stu-id="c865b-317">Similar to the earlier workflow job, selecting the job entry in the web UI displays information on the job:</span></span>

    ![Informações de trabalho do coordenador](./media/hdinsight-use-oozie-linux-mac/coordinatorjobinfo.png)

    > [!NOTE]
    > <span data-ttu-id="c865b-319">Essa imagem mostra apenas as execuções bem-sucedidas do trabalho, não as ações individuais do fluxo de trabalho agendado.</span><span class="sxs-lookup"><span data-stu-id="c865b-319">This image only shows successful runs of the job, not individual actions within the scheduled workflow.</span></span> <span data-ttu-id="c865b-320">Para ver isso, selecione uma das entradas de **Ação** .</span><span class="sxs-lookup"><span data-stu-id="c865b-320">To see that, select one of the **Action** entries.</span></span>

    ![Informações da ação](./media/hdinsight-use-oozie-linux-mac/coordinatoractionjob.png)

## <a name="troubleshooting"></a><span data-ttu-id="c865b-322">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="c865b-322">Troubleshooting</span></span>

<span data-ttu-id="c865b-323">A interface do usuário do Oozie permite exibir os logs do Oozie.</span><span class="sxs-lookup"><span data-stu-id="c865b-323">The Oozie UI allows you to view Oozie logs.</span></span> <span data-ttu-id="c865b-324">Ela também contém links para logs do JobTracker de tarefas do MapReduce iniciadas pelo fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-324">It also contains links to JobTracker logs for MapReduce tasks started by the workflow.</span></span> <span data-ttu-id="c865b-325">O padrão para solução de problemas deve ser:</span><span class="sxs-lookup"><span data-stu-id="c865b-325">The pattern for troubleshooting should be:</span></span>

1. <span data-ttu-id="c865b-326">Exiba o trabalho na interface do usuário da Web do Oozie.</span><span class="sxs-lookup"><span data-stu-id="c865b-326">View the job in Oozie Web UI.</span></span>

2. <span data-ttu-id="c865b-327">Se houver um erro ou falha de uma ação específica, selecione a ação para ver se o campo **Mensagem de Erro** fornece mais informações sobre a falha.</span><span class="sxs-lookup"><span data-stu-id="c865b-327">If there is an error or failure for a specific action, select the action to see if the **Error Message** field provides more information on the failure.</span></span>

3. <span data-ttu-id="c865b-328">Se estiver disponível, use a URL da ação para exibir mais detalhes (como logs do JobTracker) para a ação.</span><span class="sxs-lookup"><span data-stu-id="c865b-328">If available, use the URL from the action to view more details (such as JobTracker logs) for the action.</span></span>

<span data-ttu-id="c865b-329">A seguir estão os erros específicos que podem ser encontrados e como resolvê-los.</span><span class="sxs-lookup"><span data-stu-id="c865b-329">The following are specific errors you may encounter, and how to resolve them.</span></span>

### <a name="ja009-cannot-initialize-cluster"></a><span data-ttu-id="c865b-330">JA009: não é possível inicializar o cluster</span><span class="sxs-lookup"><span data-stu-id="c865b-330">JA009: Cannot initialize cluster</span></span>

<span data-ttu-id="c865b-331">**Sintomas**: o status do trabalho é alterado para **SUSPENSO**.</span><span class="sxs-lookup"><span data-stu-id="c865b-331">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="c865b-332">Os detalhes do trabalho mostram o status de RunHiveScript como **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="c865b-332">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="c865b-333">Selecionar a ação exibirá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="c865b-333">Selecting the action displays the following error message:</span></span>

    JA009: Cannot initialize Cluster. Please check your configuration for map

<span data-ttu-id="c865b-334">**Causa**: os endereços de WASB usados no arquivo **job.xml** não contêm o contêiner de armazenamento ou o nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="c865b-334">**Cause**: The WASB addresses used in the **job.xml** file do not contain the storage container or storage account name.</span></span> <span data-ttu-id="c865b-335">O formato do endereço WASB deve ser `wasb://containername@storageaccountname.blob.core.windows.net`.</span><span class="sxs-lookup"><span data-stu-id="c865b-335">The WASB address format must be `wasb://containername@storageaccountname.blob.core.windows.net`.</span></span>

<span data-ttu-id="c865b-336">**Resolução**: alterar os endereços WASB usados pelo trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-336">**Resolution**: Change the WASB addresses used by the job.</span></span>

### <a name="ja002-oozie-is-not-allowed-to-impersonate-ltuser"></a><span data-ttu-id="c865b-337">JA002: o Oozie não tem permissão para representar o &lt;USER></span><span class="sxs-lookup"><span data-stu-id="c865b-337">JA002: Oozie is not allowed to impersonate &lt;USER></span></span>

<span data-ttu-id="c865b-338">**Sintomas**: o status do trabalho é alterado para **SUSPENSO**.</span><span class="sxs-lookup"><span data-stu-id="c865b-338">**Symptoms**: The job status changes to **SUSPENDED**.</span></span> <span data-ttu-id="c865b-339">Os detalhes do trabalho mostram o status de RunHiveScript como **START_MANUAL**.</span><span class="sxs-lookup"><span data-stu-id="c865b-339">Details for the job show the RunHiveScript status as **START_MANUAL**.</span></span> <span data-ttu-id="c865b-340">Selecionar a ação exibirá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="c865b-340">Selecting the action shows the following error message:</span></span>

    JA002: User: oozie is not allowed to impersonate <USER>

<span data-ttu-id="c865b-341">**Causa**: as configurações de permissão atuais não permitem ao Oozie representar a conta de usuário especificada.</span><span class="sxs-lookup"><span data-stu-id="c865b-341">**Cause**: Current permission settings do not allow Oozie to impersonate the specified user account.</span></span>

<span data-ttu-id="c865b-342">**Resolução**: o Oozie tem permissão para representar os usuários no grupo **usuários**.</span><span class="sxs-lookup"><span data-stu-id="c865b-342">**Resolution**: Oozie is allowed to impersonate users in the **users** group.</span></span> <span data-ttu-id="c865b-343">Use o `groups USERNAME` para ver os grupos do qual a conta de usuário é membro.</span><span class="sxs-lookup"><span data-stu-id="c865b-343">Use the `groups USERNAME` to see the groups that the user account is a member of.</span></span> <span data-ttu-id="c865b-344">Se o usuário não for membro do grupo **usuários** , use o seguinte comando para adicionar o usuário ao grupo:</span><span class="sxs-lookup"><span data-stu-id="c865b-344">If the user is not a member of the **users** group, use the following command to add the user to the group:</span></span>

    sudo adduser USERNAME users

> [!NOTE]
> <span data-ttu-id="c865b-345">Pode levar vários minutos antes de o HDInsight reconhecer que o usuário foi adicionado ao grupo.</span><span class="sxs-lookup"><span data-stu-id="c865b-345">It may take several minutes before HDInsight recognizes that the user has been added to the group.</span></span>

### <a name="launcher-error-sqoop"></a><span data-ttu-id="c865b-346">ERRO do Iniciador (Sqoop)</span><span class="sxs-lookup"><span data-stu-id="c865b-346">Launcher ERROR (Sqoop)</span></span>

<span data-ttu-id="c865b-347">**Sintomas**: o status do trabalho é alterado para **ENCERRADO**.</span><span class="sxs-lookup"><span data-stu-id="c865b-347">**Symptoms**: The job status changes to **KILLED**.</span></span> <span data-ttu-id="c865b-348">Os detalhes do trabalho mostram o status de RunSqoopExport como **ERRO**.</span><span class="sxs-lookup"><span data-stu-id="c865b-348">Details for the job show the RunSqoopExport status as **ERROR**.</span></span> <span data-ttu-id="c865b-349">Selecionar a ação exibirá a seguinte mensagem de erro:</span><span class="sxs-lookup"><span data-stu-id="c865b-349">Selecting the action shows the following error message:</span></span>

    Launcher ERROR, reason: Main class [org.apache.oozie.action.hadoop.SqoopMain], exit code [1]

<span data-ttu-id="c865b-350">**Causa**: o Sqoop não conseguiu carregar o driver do banco de dados necessário para acessar o banco de dados.</span><span class="sxs-lookup"><span data-stu-id="c865b-350">**Cause**: Sqoop is unable to load the database driver required to access the database.</span></span>

<span data-ttu-id="c865b-351">**Resolução**: ao usar o Sqoop em um trabalho do Oozie, você deve incluir o driver de banco de dados com os outros recursos (como o workflow.xml) usados pelo trabalho.</span><span class="sxs-lookup"><span data-stu-id="c865b-351">**Resolution**: When using Sqoop from an Oozie job, you must include the database driver with the other resources (such as the workflow.xml) used by the job.</span></span> <span data-ttu-id="c865b-352">Também referencie o arquivo morto que contém o driver de banco de dados na seção `<sqoop>...</sqoop>` do workflow.xml.</span><span class="sxs-lookup"><span data-stu-id="c865b-352">Also Reference the archive containing the database driver from the `<sqoop>...</sqoop>` section of the workflow.xml.</span></span>

<span data-ttu-id="c865b-353">Por exemplo, para o trabalho neste documento, você usaria o seguinte procedimento:</span><span class="sxs-lookup"><span data-stu-id="c865b-353">For example, for the job in this document, you would use the following steps:</span></span>

1. <span data-ttu-id="c865b-354">Copie o arquivo sqljdbc4.1.jar para o diretório /tutorials/useoozie:</span><span class="sxs-lookup"><span data-stu-id="c865b-354">Copy the sqljdbc4.1.jar file to the /tutorials/useoozie directory:</span></span>

    ```
    hdfs dfs -put /usr/share/java/sqljdbc_4.1/enu/sqljdbc41.jar /tutorials/useoozie/sqljdbc41.jar
    ```

2. <span data-ttu-id="c865b-355">Modifique o workflow.xml para adicionar o seguinte XML a uma nova linha acima `</sqoop>`:</span><span class="sxs-lookup"><span data-stu-id="c865b-355">Modify the workflow.xml to add the following XML on a new line above `</sqoop>`:</span></span>

    ```xml
    <archive>sqljdbc41.jar</archive>
    ```

## <a name="next-steps"></a><span data-ttu-id="c865b-356">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="c865b-356">Next steps</span></span>

<span data-ttu-id="c865b-357">Neste tutorial, você aprendeu a definir um fluxo de trabalho do Oozie e a executar um trabalho do Oozie.</span><span class="sxs-lookup"><span data-stu-id="c865b-357">In this tutorial, you learned how to define an Oozie workflow and how to run an Oozie job.</span></span> <span data-ttu-id="c865b-358">Para saber mais sobre como trabalhar com o HDInsight, consulte os seguintes artigos:</span><span class="sxs-lookup"><span data-stu-id="c865b-358">To learn more about working with HDInsight, see the following articles:</span></span>

* <span data-ttu-id="c865b-359">[Usar o Coordenador do Oozie baseado em tempo com o HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="c865b-359">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="c865b-360">[Carregar dados para trabalhos do Hadoop no HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="c865b-360">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="c865b-361">[Usar Sqoop com o Hadoop no HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="c865b-361">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="c865b-362">[Usar o Hive com Hadoop no HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="c865b-362">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="c865b-363">[Usar o Pig com Hadoop no HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="c865b-363">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="c865b-364">[Desenvolver programas Java MapReduce para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="c865b-364">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

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
