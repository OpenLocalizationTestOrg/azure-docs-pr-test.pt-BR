---
title: aaaUse Hadoop Oozie em HDInsight | Microsoft Docs
description: "Usar o Oozie do Hadoop no HDInsight, uma solução de big data. Saiba como toodefine um fluxo de trabalho do Oozie e enviar um trabalho de Oozie."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 870098f0-f416-4491-9719-78994bf4a369
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 12d0cf1a01838ab0f4e699c384ce2fb18f85cbad
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-oozie-with-hadoop-toodefine-and-run-a-workflow-in-hdinsight"></a><span data-ttu-id="159d4-104">Usar Oozie com toodefine Hadoop e executar um fluxo de trabalho no HDInsight</span><span class="sxs-lookup"><span data-stu-id="159d4-104">Use Oozie with Hadoop toodefine and run a workflow in HDInsight</span></span>
[!INCLUDE [oozie-selector](../../includes/hdinsight-oozie-selector.md)]

<span data-ttu-id="159d4-105">Saiba como toouse Apache Oozie toodefine um fluxo de trabalho e execute Olá fluxo de trabalho no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="159d4-105">Learn how toouse Apache Oozie toodefine a workflow and run hello workflow on HDInsight.</span></span> <span data-ttu-id="159d4-106">toolearn sobre coordenador do Oozie hello, consulte [usar o coordenador de Oozie Hadoop baseada em tempo com HDInsight][hdinsight-oozie-coordinator-time].</span><span class="sxs-lookup"><span data-stu-id="159d4-106">toolearn about hello Oozie coordinator, see [Use time-based Hadoop Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time].</span></span> <span data-ttu-id="159d4-107">toolearn do Azure Data Factory, consulte [usar o Pig e Hive com a fábrica de dados][azure-data-factory-pig-hive].</span><span class="sxs-lookup"><span data-stu-id="159d4-107">toolearn Azure Data Factory, see [Use Pig and Hive with Data Factory][azure-data-factory-pig-hive].</span></span>

<span data-ttu-id="159d4-108">O Apache Oozie é um sistema de fluxo de trabalho/coordenação que gerencia trabalhos do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="159d4-108">Apache Oozie is a workflow/coordination system that manages Hadoop jobs.</span></span> <span data-ttu-id="159d4-109">Ele é integrado com pilha de Hadoop hello e dá suporte à trabalhos de Hadoop MapReduce Apache, Pig do Apache, Apache Hive e Apache Sqoop.</span><span class="sxs-lookup"><span data-stu-id="159d4-109">It is integrated with hello Hadoop stack, and it supports Hadoop jobs for Apache MapReduce, Apache Pig, Apache Hive, and Apache Sqoop.</span></span> <span data-ttu-id="159d4-110">Ele também pode ser tooschedule usado trabalhos que são tooa específicas do sistema, como programas de Java ou scripts de shell.</span><span class="sxs-lookup"><span data-stu-id="159d4-110">It can also be used tooschedule jobs that are specific tooa system, like Java programs or shell scripts.</span></span>

<span data-ttu-id="159d4-111">fluxo de trabalho de saudação que implementar seguindo as instruções de saudação este tutorial contém duas ações:</span><span class="sxs-lookup"><span data-stu-id="159d4-111">hello workflow you implement by following hello instructions in this tutorial contains two actions:</span></span>

![Diagrama de fluxo de trabalho][img-workflow-diagram]

1. <span data-ttu-id="159d4-113">Uma ação de Hive executa uma saudação de toocount script HiveQL ocorrências de cada tipo de nível de log em um arquivo log4j.</span><span class="sxs-lookup"><span data-stu-id="159d4-113">A Hive action runs a HiveQL script toocount hello occurrences of each log-level type in a log4j file.</span></span> <span data-ttu-id="159d4-114">Cada arquivo log4j consiste em uma linha de campos que contém um campo [nível de LOG] mostra o tipo de saudação e severidade hello, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="159d4-114">Each log4j file consists of a line of fields that contains a [LOG LEVEL] field that shows hello type and hello severity, for example:</span></span>
   
        2012-02-03 18:35:34 SampleClass6 [INFO] everything normal for id 577725851
        2012-02-03 18:35:34 SampleClass4 [FATAL] system problem at id 1991281254
        2012-02-03 18:35:34 SampleClass3 [DEBUG] detail for id 1304807656
        ...
   
    <span data-ttu-id="159d4-115">saudação de saída do script de Hive é semelhante a:</span><span class="sxs-lookup"><span data-stu-id="159d4-115">hello Hive script output is similar to:</span></span>
   
        [DEBUG] 434
        [ERROR] 3
        [FATAL] 1
        [INFO]  96
        [TRACE] 816
        [WARN]  4
   
    <span data-ttu-id="159d4-116">Para obter mais informações sobre o Hive, consulte [Usar o Hive com o HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="159d4-116">For more information about Hive, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
2. <span data-ttu-id="159d4-117">Uma ação de Sqoop exporta a tabela de tooa de saída Olá HiveQL em um banco de dados do SQL Azure.</span><span class="sxs-lookup"><span data-stu-id="159d4-117">A Sqoop action exports hello HiveQL output tooa table in an Azure SQL database.</span></span> <span data-ttu-id="159d4-118">Para saber mais sobre o Sqoop, confira [Usar o Hadoop Sqoop com o HDInsight][hdinsight-use-sqoop].</span><span class="sxs-lookup"><span data-stu-id="159d4-118">For more information about Sqoop, see [Use Hadoop Sqoop with HDInsight][hdinsight-use-sqoop].</span></span>

> [!NOTE]
> <span data-ttu-id="159d4-119">Para versões com suporte do Oozie em clusters de HDInsight, consulte [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight?] [hdinsight-versions].</span><span class="sxs-lookup"><span data-stu-id="159d4-119">For supported Oozie versions on HDInsight clusters, see [What's new in hello Hadoop cluster versions provided by HDInsight?][hdinsight-versions].</span></span>
> 
> 

### <a name="prerequisites"></a><span data-ttu-id="159d4-120">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="159d4-120">Prerequisites</span></span>
<span data-ttu-id="159d4-121">Antes de começar este tutorial, você deve ter Olá item a seguir:</span><span class="sxs-lookup"><span data-stu-id="159d4-121">Before you begin this tutorial, you must have hello following item:</span></span>

* <span data-ttu-id="159d4-122">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="159d4-122">**A workstation with Azure PowerShell**.</span></span> 
  

[!INCLUDE [upgrade-powershell](../../includes/hdinsight-use-latest-powershell.md)]
  

## <a name="define-oozie-workflow-and-hello-related-hiveql-script"></a><span data-ttu-id="159d4-123">Definir o fluxo de trabalho do Oozie e Olá script HiveQL relacionados</span><span class="sxs-lookup"><span data-stu-id="159d4-123">Define Oozie workflow and hello related HiveQL script</span></span>
<span data-ttu-id="159d4-124">As definições de fluxos de trabalho do Oozie são escritas em hPDL (uma Linguagem de Definição de Processo XML).</span><span class="sxs-lookup"><span data-stu-id="159d4-124">Oozie workflows definitions are written in hPDL (a XML Process Definition Language).</span></span> <span data-ttu-id="159d4-125">nome de arquivo de fluxo de trabalho saudação padrão *. XML*.</span><span class="sxs-lookup"><span data-stu-id="159d4-125">hello default workflow file name is *workflow.xml*.</span></span> <span data-ttu-id="159d4-126">a seguir Olá é o arquivo de fluxo de trabalho de Olá que usar neste tutorial.</span><span class="sxs-lookup"><span data-stu-id="159d4-126">hello following is hello workflow file you use in this tutorial.</span></span>

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
                <param>hiveOutputFolder=${hiveOutputFolder}</param>
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
            <arg>${hiveOutputFolder}</arg>
            <arg>-m</arg>
            <arg>1</arg>
            <arg>--input-fields-terminated-by</arg>
            <arg>"\001"</arg>
            </sqoop>
            <ok to="end"/>
            <error to="fail"/>
        </action>

        <kill name="fail">
            <message>Job failed, error message[${wf:errorMessage(wf:lastErrorNode())}] </message>
        </kill>

        <end name="end"/>
    </workflow-app>

<span data-ttu-id="159d4-127">Há duas ações definidas no fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="159d4-127">There are two actions defined in hello workflow.</span></span> <span data-ttu-id="159d4-128">Olá start-tooaction é *RunHiveScript*.</span><span class="sxs-lookup"><span data-stu-id="159d4-128">hello start-tooaction is *RunHiveScript*.</span></span> <span data-ttu-id="159d4-129">Se a ação de saudação é executada com êxito, próxima ação de saudação é *RunSqoopExport*.</span><span class="sxs-lookup"><span data-stu-id="159d4-129">If hello action runs successfully, hello next action is *RunSqoopExport*.</span></span>

<span data-ttu-id="159d4-130">Olá RunHiveScript tem diversas variáveis.</span><span class="sxs-lookup"><span data-stu-id="159d4-130">hello RunHiveScript has several variables.</span></span> <span data-ttu-id="159d4-131">Você passar valores hello quando você enviar o trabalho de Oozie de saudação de sua estação de trabalho usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="159d4-131">You pass hello values when you submit hello Oozie job from your workstation by using Azure PowerShell.</span></span>

<table border = "1">
<tr><th><span data-ttu-id="159d4-132">Variáveis de fluxo de trabalho</span><span class="sxs-lookup"><span data-stu-id="159d4-132">Workflow variables</span></span></th><th><span data-ttu-id="159d4-133">Descrição</span><span class="sxs-lookup"><span data-stu-id="159d4-133">Description</span></span></th></tr>
<tr><td><span data-ttu-id="159d4-134">${jobTracker}</span><span class="sxs-lookup"><span data-stu-id="159d4-134">${jobTracker}</span></span></td><td><span data-ttu-id="159d4-135">Especifica a URL de saudação do rastreador de trabalho do Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="159d4-135">Specifies hello URL of hello Hadoop job tracker.</span></span> <span data-ttu-id="159d4-136">Use <strong>jobtrackerhost: 9010</strong> nas versões 3.0 e 2.1 do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="159d4-136">Use <strong>jobtrackerhost:9010</strong> in HDInsight version 3.0 and 2.1.</span></span></td></tr>
<tr><td><span data-ttu-id="159d4-137">${nameNode}</span><span class="sxs-lookup"><span data-stu-id="159d4-137">${nameNode}</span></span></td><td><span data-ttu-id="159d4-138">Especifica a URL de saudação do nó do nome de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="159d4-138">Specifies hello URL of hello Hadoop name node.</span></span> <span data-ttu-id="159d4-139">Use o endereço do sistema de arquivos de padrão de hello, por exemplo, <i>wasb: / /&lt;containerName&gt;@&lt;storageAccountName&gt;. >.blob.Core.Windows.NET</i>.</span><span class="sxs-lookup"><span data-stu-id="159d4-139">Use hello default file system address, for example, <i>wasb://&lt;containerName&gt;@&lt;storageAccountName&gt;.blob.core.windows.net</i>.</span></span></td></tr>
<tr><td><span data-ttu-id="159d4-140">${queueName}</span><span class="sxs-lookup"><span data-stu-id="159d4-140">${queueName}</span></span></td><td><span data-ttu-id="159d4-141">Especifica o nome de fila Olá Olá trabalho é enviado para o.</span><span class="sxs-lookup"><span data-stu-id="159d4-141">Specifies hello queue name that hello job is submitted to.</span></span> <span data-ttu-id="159d4-142">Saudação de uso <strong>padrão</strong>.</span><span class="sxs-lookup"><span data-stu-id="159d4-142">Use hello <strong>default</strong>.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="159d4-143">Variável de ação do Hive</span><span class="sxs-lookup"><span data-stu-id="159d4-143">Hive action variable</span></span></th><th><span data-ttu-id="159d4-144">Descrição</span><span class="sxs-lookup"><span data-stu-id="159d4-144">Description</span></span></th></tr>
<tr><td><span data-ttu-id="159d4-145">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="159d4-145">${hiveDataFolder}</span></span></td><td><span data-ttu-id="159d4-146">Especifica o diretório de origem de saudação de saudação comando Hive Create Table.</span><span class="sxs-lookup"><span data-stu-id="159d4-146">Specifies hello source directory for hello Hive Create Table command.</span></span></td></tr>
<tr><td><span data-ttu-id="159d4-147">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="159d4-147">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="159d4-148">Especifica a pasta de saída de saudação para Olá instrução inserir substituir.</span><span class="sxs-lookup"><span data-stu-id="159d4-148">Specifies hello output folder for hello INSERT OVERWRITE statement.</span></span></td></tr>
<tr><td><span data-ttu-id="159d4-149">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="159d4-149">${hiveTableName}</span></span></td><td><span data-ttu-id="159d4-150">Especifica o nome de saudação da tabela de Hive Olá que faz referência a arquivos de dados de log4j hello.</span><span class="sxs-lookup"><span data-stu-id="159d4-150">Specifies hello name of hello Hive table that references hello log4j data files.</span></span></td></tr>
</table>

<table border = "1">
<tr><th><span data-ttu-id="159d4-151">Variável de ação do Sqoop</span><span class="sxs-lookup"><span data-stu-id="159d4-151">Sqoop action variable</span></span></th><th><span data-ttu-id="159d4-152">Descrição</span><span class="sxs-lookup"><span data-stu-id="159d4-152">Description</span></span></th></tr>
<tr><td><span data-ttu-id="159d4-153">${sqlDatabaseConnectionString}</span><span class="sxs-lookup"><span data-stu-id="159d4-153">${sqlDatabaseConnectionString}</span></span></td><td><span data-ttu-id="159d4-154">Especifica a cadeia de conexão de banco de dados de SQL do Azure hello.</span><span class="sxs-lookup"><span data-stu-id="159d4-154">Specifies hello Azure SQL database connection string.</span></span></td></tr>
<tr><td><span data-ttu-id="159d4-155">${sqlDatabaseTableName}</span><span class="sxs-lookup"><span data-stu-id="159d4-155">${sqlDatabaseTableName}</span></span></td><td><span data-ttu-id="159d4-156">Especifica a tabela de banco de dados do SQL Azure Olá onde os dados de saudação são exportados para.</span><span class="sxs-lookup"><span data-stu-id="159d4-156">Specifies hello Azure SQL database table where hello data is exported to.</span></span></td></tr>
<tr><td><span data-ttu-id="159d4-157">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="159d4-157">${hiveOutputFolder}</span></span></td><td><span data-ttu-id="159d4-158">Especifica a pasta de saída de saudação para Olá instrução Hive inserir substituir.</span><span class="sxs-lookup"><span data-stu-id="159d4-158">Specifies hello output folder for hello Hive INSERT OVERWRITE statement.</span></span> <span data-ttu-id="159d4-159">Isso é hello mesma pasta para exportação de Sqoop hello (export-dir).</span><span class="sxs-lookup"><span data-stu-id="159d4-159">This is hello same folder for hello Sqoop export (export-dir).</span></span></td></tr>
</table>

<span data-ttu-id="159d4-160">Para saber mais sobre o fluxo de trabalho do Oozie e sobre como usar ações de fluxo de trabalho, confira a [Documentação do Apache Oozie 4.0][apache-oozie-400] (para o HDInsight versão 3.0) ou a [Documentação do Oozie Apache 3.3.2][apache-oozie-332] (para o HDInsight versão 2.1).</span><span class="sxs-lookup"><span data-stu-id="159d4-160">For more information about Oozie workflow and using workflow actions, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="159d4-161">Olá ação de Hive no fluxo de trabalho Olá chama um arquivo de script HiveQL.</span><span class="sxs-lookup"><span data-stu-id="159d4-161">hello Hive action in hello workflow calls a HiveQL script file.</span></span> <span data-ttu-id="159d4-162">Esse arquivo de script contém três instruções HiveQL:</span><span class="sxs-lookup"><span data-stu-id="159d4-162">This script file contains three HiveQL statements:</span></span>

    DROP TABLE ${hiveTableName};
    CREATE EXTERNAL TABLE ${hiveTableName}(t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string) ROW FORMAT DELIMITED FIELDS TERMINATED BY ' ' STORED AS TEXTFILE LOCATION '${hiveDataFolder}';
    INSERT OVERWRITE DIRECTORY '${hiveOutputFolder}' SELECT t4 AS sev, COUNT(*) AS cnt FROM ${hiveTableName} WHERE t4 LIKE '[%' GROUP BY t4;

1. <span data-ttu-id="159d4-163">**Olá instrução DROP TABLE** exclusões Olá log4j Hive tabela se ela existir.</span><span class="sxs-lookup"><span data-stu-id="159d4-163">**hello DROP TABLE statement** deletes hello log4j Hive table if it exists.</span></span>
2. <span data-ttu-id="159d4-164">**Olá instrução CREATE TABLE** cria uma tabela de Hive externa de log4j que aponta toohello local do arquivo de log log4j hello.</span><span class="sxs-lookup"><span data-stu-id="159d4-164">**hello CREATE TABLE statement** creates a log4j Hive external table that points toohello location of hello log4j log file.</span></span> <span data-ttu-id="159d4-165">é o delimitador de campo Hello ",".</span><span class="sxs-lookup"><span data-stu-id="159d4-165">hello field delimiter is ",".</span></span> <span data-ttu-id="159d4-166">delimitador de linha Hello padrão é "\n".</span><span class="sxs-lookup"><span data-stu-id="159d4-166">hello default line delimiter is "\n".</span></span> <span data-ttu-id="159d4-167">Uma tabela externa Hive é o arquivo de dados de saudação de tooavoid usado que está sendo removido do local original Olá se você quiser que o fluxo de trabalho do toorun Olá Oozie várias vezes.</span><span class="sxs-lookup"><span data-stu-id="159d4-167">A Hive external table is used tooavoid hello data file being removed from hello original location if you want toorun hello Oozie workflow multiple times.</span></span>
3. <span data-ttu-id="159d4-168">**Olá instrução inserir substituir** contagens de ocorrências de saudação de cada tipo de nível de log da tabela de Hive log4j hello e salva o blob de tooa Olá saída no armazenamento do Azure.</span><span class="sxs-lookup"><span data-stu-id="159d4-168">**hello INSERT OVERWRITE statement** counts hello occurrences of each log-level type from hello log4j Hive table, and saves hello output tooa blob in Azure Storage.</span></span>

<span data-ttu-id="159d4-169">Há três variáveis usadas em script hello:</span><span class="sxs-lookup"><span data-stu-id="159d4-169">There are three variables used in hello script:</span></span>

* <span data-ttu-id="159d4-170">${hiveTableName}</span><span class="sxs-lookup"><span data-stu-id="159d4-170">${hiveTableName}</span></span>
* <span data-ttu-id="159d4-171">${hiveDataFolder}</span><span class="sxs-lookup"><span data-stu-id="159d4-171">${hiveDataFolder}</span></span>
* <span data-ttu-id="159d4-172">${hiveOutputFolder}</span><span class="sxs-lookup"><span data-stu-id="159d4-172">${hiveOutputFolder}</span></span>

<span data-ttu-id="159d4-173">arquivo de definição de fluxo de trabalho (. XML neste tutorial) Olá passa esses valores toothis script HiveQL em tempo de execução.</span><span class="sxs-lookup"><span data-stu-id="159d4-173">hello workflow definition file (workflow.xml in this tutorial) passes these values toothis HiveQL script at run time.</span></span>

<span data-ttu-id="159d4-174">Arquivo de fluxo de trabalho hello e o arquivo de estilo de saudação são armazenados em um contêiner de blob.</span><span class="sxs-lookup"><span data-stu-id="159d4-174">Both hello workflow file and hello HiveQL file are stored in a blob container.</span></span>  <span data-ttu-id="159d4-175">Olá script do PowerShell que você usará posteriormente neste tutorial copia a conta de armazenamento ambos os arquivos toohello padrão.</span><span class="sxs-lookup"><span data-stu-id="159d4-175">hello PowerShell script you use later in this tutorial copies both files toohello default Storage account.</span></span> 

## <a name="submit-oozie-jobs-using-powershell"></a><span data-ttu-id="159d4-176">Enviar trabalhos do Oozie usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="159d4-176">Submit Oozie jobs using PowerShell</span></span>
<span data-ttu-id="159d4-177">Atualmente, o PowerShell do Azure não fornece nenhum cmdlet para definir trabalhos do Oozie.</span><span class="sxs-lookup"><span data-stu-id="159d4-177">Azure PowerShell currently doesn't provide any cmdlets for defining Oozie jobs.</span></span> <span data-ttu-id="159d4-178">Você pode usar o hello **Invoke-RestMethod** tooinvoke cmdlet Oozie os serviços da web.</span><span class="sxs-lookup"><span data-stu-id="159d4-178">You can use hello **Invoke-RestMethod** cmdlet tooinvoke Oozie web services.</span></span> <span data-ttu-id="159d4-179">API de serviços web de Oozie Olá é uma API de JSON de REST de HTTP.</span><span class="sxs-lookup"><span data-stu-id="159d4-179">hello Oozie web services API is a HTTP REST JSON API.</span></span> <span data-ttu-id="159d4-180">Para obter mais informações sobre a API de serviços web de Oozie hello, consulte [documentação do Apache Oozie 4.0] [ apache-oozie-400] (para HDInsight versão 3.0) ou [documentação do Apache Oozie 3.3.2] [ apache-oozie-332] (para HDInsight versão 2.1).</span><span class="sxs-lookup"><span data-stu-id="159d4-180">For more information about hello Oozie web services API, see [Apache Oozie 4.0 documentation][apache-oozie-400] (for HDInsight version 3.0) or [Apache Oozie 3.3.2 documentation][apache-oozie-332] (for HDInsight version 2.1).</span></span>

<span data-ttu-id="159d4-181">Olá script do PowerShell nesta seção executa Olá etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="159d4-181">hello PowerShell script in this section performs hello following steps:</span></span>

1. <span data-ttu-id="159d4-182">Conecte-se tooAzure.</span><span class="sxs-lookup"><span data-stu-id="159d4-182">Connect tooAzure.</span></span>
2. <span data-ttu-id="159d4-183">Crie um grupo de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="159d4-183">Create an Azure resource group.</span></span> <span data-ttu-id="159d4-184">Para obter mais informações, veja [Usando o Azure PowerShell com o Gerenciador de Recursos do Azure](../powershell-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="159d4-184">For more information, see [Use Azure PowerShell with Azure Resource Manager](../powershell-azure-resource-manager.md).</span></span>
3. <span data-ttu-id="159d4-185">Crie um servidor de Banco de Dados SQL do Azure, um banco de dados SQL do Azure e duas tabelas.</span><span class="sxs-lookup"><span data-stu-id="159d4-185">Create an Azure SQL Database server, an Azure SQL database, and two tables.</span></span> <span data-ttu-id="159d4-186">Eles são usados pelo Olá Sqoop ação no fluxo de trabalho de saudação.</span><span class="sxs-lookup"><span data-stu-id="159d4-186">These are used by hello Sqoop action in hello workflow.</span></span>
   
    <span data-ttu-id="159d4-187">nome da tabela Olá é *log4jLogCount*.</span><span class="sxs-lookup"><span data-stu-id="159d4-187">hello table name is *log4jLogCount*.</span></span>
4. <span data-ttu-id="159d4-188">Crie um toorun de cluster usado HDInsight Oozie trabalhos.</span><span class="sxs-lookup"><span data-stu-id="159d4-188">Create an HDInsight cluster used toorun Oozie jobs.</span></span>
   
    <span data-ttu-id="159d4-189">cluster de saudação tooexamine, você pode usar o hello portal do Azure ou o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="159d4-189">tooexamine hello cluster, you can use hello Azure portal or Azure PowerShell.</span></span>
5. <span data-ttu-id="159d4-190">Copie o arquivo de fluxo de trabalho do oozie hello e sistema de arquivos padrão de toohello arquivos de script HiveQL de saudação.</span><span class="sxs-lookup"><span data-stu-id="159d4-190">Copy hello oozie workflow file and hello HiveQL script file toohello default file system.</span></span>
   
    <span data-ttu-id="159d4-191">Os dois arquivos são armazenados em um contêiner de Blob público.</span><span class="sxs-lookup"><span data-stu-id="159d4-191">Both files are stored in a public Blob container.</span></span>
   
   * <span data-ttu-id="159d4-192">Copie Olá HiveQL script (useoozie.hql) tooAzure (wasb:///tutorials/useoozie/useoozie.hql) de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="159d4-192">Copy hello HiveQL script (useoozie.hql) tooAzure Storage (wasb:///tutorials/useoozie/useoozie.hql).</span></span>
   * <span data-ttu-id="159d4-193">Copie toowasb:///tutorials/useoozie/workflow.xml. XML.</span><span class="sxs-lookup"><span data-stu-id="159d4-193">Copy workflow.xml toowasb:///tutorials/useoozie/workflow.xml.</span></span>
   * <span data-ttu-id="159d4-194">Copiar arquivo de dados de saudação (/ example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span><span class="sxs-lookup"><span data-stu-id="159d4-194">Copy hello data file (/example/data/sample.log) toowasb:///tutorials/useoozie/data/sample.log.</span></span>
6. <span data-ttu-id="159d4-195">Enviar um trabalho do Oozie.</span><span class="sxs-lookup"><span data-stu-id="159d4-195">Submit an Oozie job.</span></span>
   
    <span data-ttu-id="159d4-196">resultados do trabalho do tooexamine Olá OOzie, use o Visual Studio ou outra toohello tooconnect de ferramentas do Azure SQL Database.</span><span class="sxs-lookup"><span data-stu-id="159d4-196">tooexamine hello OOzie job results, use Visual Studio or other tools tooconnect toohello Azure SQL Database.</span></span>

<span data-ttu-id="159d4-197">Aqui está o script hello.</span><span class="sxs-lookup"><span data-stu-id="159d4-197">Here is hello script.</span></span>  <span data-ttu-id="159d4-198">Você pode executar o script de saudação do Windows PowerShell ISE.</span><span class="sxs-lookup"><span data-stu-id="159d4-198">You can run hello script from Windows PowerShell ISE.</span></span> <span data-ttu-id="159d4-199">Você só precisa tooconfigure Olá 7 primeiros variáveis.</span><span class="sxs-lookup"><span data-stu-id="159d4-199">You only need tooconfigure hello first 7 variables.</span></span>

    #region - provide hello following values

    $subscriptionID = "<Enter your Azure subscription ID>"

    # SQL Database server login credentials used for creating and connecting
    $sqlDatabaseLogin = "<Enter SQL Database Login Name>"
    $sqlDatabasePassword = "<Enter SQL Database Login Password>"

    # HDInsight cluster HTTP user credential used for creating and connectin
    $httpUserName = "admin"  # hello default name is "admin"
    $httpPassword = "<Enter HDInsight Cluster HTTP User Password>"

    # Used for creating Azure service names
    $nameToken = "<Enter an Alias>"
    $namePrefix = $nameToken.ToLower() + (Get-Date -Format "MMdd")
    #endregion

    #region - variables

    # Resource group variables
    $resourceGroupName = $namePrefix + "rg"
    $location = "East US 2" # used by all Azure services defined in this tutorial

    # SQL database varialbes
    $sqlDatabaseServerName = $namePrefix + "sqldbserver"
    $sqlDatabaseName = $namePrefix + "sqldb"
    $sqlDatabaseConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $sqlDatabaseMaxSizeGB = 10

    # Used for retrieving external IP address and creating firewall rules
    $ipAddressRestService = "http://bot.whatismyipaddress.com"
    $fireWallRuleName = "UseSqoop"

    # HDInsight variables
    $hdinsightClusterName = $namePrefix + "hdi"
    $defaultStorageAccountName = $namePrefix + "store"
    $defaultBlobContainerName = $hdinsightClusterName
    #endregion

    # Treat all errors as terminating
    $ErrorActionPreference = "Stop"

    #region - Connect tooAzure subscription
    Write-Host "`nConnecting tooyour Azure subscription ..." -ForegroundColor Green
    try{Get-AzureRmContext}
    catch{
        Login-AzureRmAccount
        Select-AzureRmSubscription -SubscriptionId $subscriptionID
    }
    #endregion

    #region - Create Azure resouce group
    Write-Host "`nCreating an Azure resource group ..." -ForegroundColor Green
    try{
        Get-AzureRmResourceGroup -Name $resourceGroupName
    }
    catch{
        New-AzureRmResourceGroup -Name $resourceGroupName -Location $location
    }
    #endregion

    #region - Create Azure SQL database server
    Write-Host "`nCreating an Azure SQL Database server ..." -ForegroundColor Green
    try{
        Get-AzureRmSqlServer -ServerName $sqlDatabaseServerName -ResourceGroupName $resourceGroupName}
    catch{
        Write-Host "`nCreating SQL Database server ..."  -ForegroundColor Green

        $sqlDatabasePW = ConvertTo-SecureString -String $sqlDatabasePassword -AsPlainText -Force
        $sqlLoginCredentials = New-Object System.Management.Automation.PSCredential($sqlDatabaseLogin,$sqlDatabasePW)

        $sqlDatabaseServerName = (New-AzureRmSqlServer `
                                    -ResourceGroupName $resourceGroupName `
                                    -ServerName $sqlDatabaseServerName `
                                    -SqlAdministratorCredentials $sqlLoginCredentials `
                                    -Location $location).ServerName
        Write-Host "`tThe new SQL database server name is $sqlDatabaseServerName." -ForegroundColor Cyan

        Write-Host "`nCreating firewall rule, $fireWallRuleName ..." -ForegroundColor Green
        $workstationIPAddress = Invoke-RestMethod $ipAddressRestService
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-workstation" `
            -StartIpAddress $workstationIPAddress `
            -EndIpAddress $workstationIPAddress

        #tooallow other Azure services tooaccess hello server add a firewall rule and set both hello StartIpAddress and EndIpAddress too0.0.0.0. 
        #Note that this allows Azure traffic from any Azure subscription tooaccess hello server.
        New-AzureRmSqlServerFirewallRule `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -FirewallRuleName "$fireWallRuleName-Azureservices" `
            -StartIpAddress "0.0.0.0" `
            -EndIpAddress "0.0.0.0"
    }
    #endregion

    #region - Create and validate Azure SQL database
    Write-Host "`nCreating SQL Database, $sqlDatabaseName ..."  -ForegroundColor Green

    try {
        Get-AzureRmSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName
    }
    catch {
        New-AzureRMSqlDatabase `
            -ResourceGroupName $resourceGroupName `
            -ServerName $sqlDatabaseServerName `
            -DatabaseName $sqlDatabaseName `
            -Edition "Standard" `
            -RequestedServiceObjectiveName "S1"
    }
    #endregion

    #region - Create SQL database tables
    Write-Host "Creating hello log4jlogs table  ..." -ForegroundColor Green

    $sqlDatabaseTableName = "log4jLogsCount"
    $cmdCreateLog4jCountTable = " CREATE TABLE [dbo].[$sqlDatabaseTableName](
            [Level] [nvarchar](10) NOT NULL,
            [Total] float,
        CONSTRAINT [PK_$sqlDatabaseTableName] PRIMARY KEY CLUSTERED
        (
        [Level] ASC
        )
        )"

    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = $sqlDatabaseConnectionString
    $conn.Open()

    # Create hello log4jlogs table and index
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.Connection = $conn
    $cmd.CommandText = $cmdCreateLog4jCountTable
    $cmd.ExecuteNonQuery()

    $conn.close()
    #endregion

    #region - Create HDInsight cluster

    Write-Host "Creating hello HDInsight cluster and hello dependent services ..." -ForegroundColor Green

    # Create hello default storage account
    New-AzureRmStorageAccount `
        -ResourceGroupName $resourceGroupName `
        -Name $defaultStorageAccountName `
        -Location $location `
        -Type Standard_LRS

    # Create hello default Blob container
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                    -ResourceGroupName $resourceGroupName `
                                    -Name $defaultStorageAccountName)[0].Value
    $defaultStorageAccountContext = New-AzureStorageContext `
                                        -StorageAccountName $defaultStorageAccountName `
                                        -StorageAccountKey $defaultStorageAccountKey 
    New-AzureStorageContainer `
        -Name $defaultBlobContainerName `
        -Context $defaultStorageAccountContext 

    # Create hello HDInsight cluster
    $pw = ConvertTo-SecureString -String $httpPassword -AsPlainText -Force
    $httpCredential = New-Object System.Management.Automation.PSCredential($httpUserName,$pw)

    New-AzureRmHDInsightCluster `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $HDInsightClusterName `
        -Location $location `
        -ClusterType Hadoop `
        -OSType Windows `
        -ClusterSizeInNodes 2 `
        -HttpCredential $httpCredential `
        -DefaultStorageAccountName "$defaultStorageAccountName.blob.core.windows.net" `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultStorageContainer $defaultBlobContainerName 

    # Validate hello cluster
    Get-AzureRmHDInsightCluster -ClusterName $hdinsightClusterName
    #endregion

    #region - copy Oozie workflow and HiveQL files

    Write-Host "Copy workflow definition and HiveQL script file ..." -ForegroundColor Green

    # Both files are stored in a public Blob
    $publicBlobContext = New-AzureStorageContext -StorageAccountName "hditutorialdata" -Anonymous

    # WASB folder for storing hello Oozie tutorial files.
    $destFolder = "tutorials/useoozie"  # Do NOT use hello long path here

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "useooziewf.hql"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/useooziewf.hql" `
        -Force

    Start-CopyAzureStorageBlob `
        -Context $publicBlobContext `
        -SrcContainer "useoozie" `
        -SrcBlob "workflow.xml"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -DestBlob "$destFolder/workflow.xml" `
        -Force

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/workflow.xml

    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/useooziewf.hql

    #endregion

    #region - copy hello sample.log file

    Write-Host "Make a copy of hello sample.log file ... " -ForegroundColor Green

    Start-CopyAzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -SrcContainer $defaultBlobContainerName `
        -SrcBlob "example/data/sample.log"  `
        -DestContext $defaultStorageAccountContext `
        -DestContainer $defaultBlobContainerName `
        -destBlob "$destFolder/data/sample.log" 

    #validate hello copy
    Get-AzureStorageBlob `
        -Context $defaultStorageAccountContext `
        -Container $defaultBlobContainerName `
        -Blob $destFolder/data/sample.log

    #endregion

    #region - submit Oozie job

    $storageUri="wasb://$defaultBlobContainerName@$defaultStorageAccountName.blob.core.windows.net"

    $oozieJobName = $namePrefix + "OozieJob"

    #Oozie WF variables
    $oozieWFPath="$storageUri/tutorials/useoozie"  # hello default name is workflow.xml. And you don't need toospecify hello file name.
    $waitTimeBetweenOozieJobStatusCheck=10

    #Hive action variables
    $hiveScript = "$storageUri/tutorials/useoozie/useooziewf.hql"
    $hiveTableName = "log4jlogs"
    $hiveDataFolder = "$storageUri/tutorials/useoozie/data"
    $hiveOutputFolder = "$storageUri/tutorials/useoozie/output"

    #Sqoop action variables
    $sqlDatabaseConnectionString = "jdbc:sqlserver://$sqlDatabaseServerName.database.windows.net;user=$sqlDatabaseLogin@$sqlDatabaseServerName;password=$sqlDatabasePassword;database=$sqlDatabaseName"

    $OoziePayload =  @"
    <?xml version="1.0" encoding="UTF-8"?>
    <configuration>

    <property>
        <name>nameNode</name>
        <value>$storageUrI</value>
    </property>

    <property>
        <name>jobTracker</name>
        <value>jobtrackerhost:9010</value>
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
        <value>$hiveScript</value>
    </property>

    <property>
        <name>hiveTableName</name>
        <value>$hiveTableName</value>
    </property>

    <property>
        <name>hiveDataFolder</name>
        <value>$hiveDataFolder</value>
    </property>

    <property>
        <name>hiveOutputFolder</name>
        <value>$hiveOutputFolder</value>
    </property>

    <property>
        <name>sqlDatabaseConnectionString</name>
        <value>&quot;$sqlDatabaseConnectionString&quot;</value>
    </property>

    <property>
        <name>sqlDatabaseTableName</name>
        <value>$SQLDatabaseTableName</value>
    </property>

    <property>
        <name>user.name</name>
        <value>$httpUserName</value>
    </property>

    <property>
        <name>oozie.wf.application.path</name>
        <value>$oozieWFPath</value>
    </property>

    </configuration>
    "@

    Write-Host "Checking Oozie server status..." -ForegroundColor Green
    $clusterUriStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/admin/status"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriStatus -Credential $httpCredential -OutVariable $OozieServerStatus

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieServerSatus = $jsonResponse[0].("systemMode")
    Write-Host "Oozie server status is $oozieServerSatus."

    # create Oozie job
    Write-Host "Sending hello following Payload toohello cluster:" -ForegroundColor Green
    Write-Host "`n--------`n$OoziePayload`n--------"
    $clusterUriCreateJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/jobs"
    $response = Invoke-RestMethod -Method Post -Uri $clusterUriCreateJob -Credential $httpCredential -Body $OoziePayload -ContentType "application/xml" -OutVariable $OozieJobName #-debug

    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $oozieJobId = $jsonResponse[0].("id")
    Write-Host "Oozie job id is $oozieJobId..."

    # start Oozie job
    Write-Host "Starting hello Oozie job $oozieJobId..." -ForegroundColor Green
    $clusterUriStartJob = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?action=start"
    $response = Invoke-RestMethod -Method Put -Uri $clusterUriStartJob -Credential $httpCredential | Format-Table -HideTableHeaders #-debug

    # get job status
    Write-Host "Sleeping for $waitTimeBetweenOozieJobStatusCheck seconds until hello job metadata is populated in hello Oozie metastore..." -ForegroundColor Green
    Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck

    Write-Host "Getting job status and waiting for hello job toocomplete..." -ForegroundColor Green
    $clusterUriGetJobStatus = "https://$hdinsightClusterName.azurehdinsight.net:443/oozie/v2/job/" + $oozieJobId + "?show=info"
    $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
    $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
    $JobStatus = $jsonResponse[0].("status")

    while($JobStatus -notmatch "SUCCEEDED|KILLED")
    {
        Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state...waiting $waitTimeBetweenOozieJobStatusCheck seconds for hello job toocomplete..."
        Start-Sleep -Seconds $waitTimeBetweenOozieJobStatusCheck
        $response = Invoke-RestMethod -Method Get -Uri $clusterUriGetJobStatus -Credential $httpCredential
        $jsonResponse = ConvertFrom-Json (ConvertTo-Json -InputObject $response)
        $JobStatus = $jsonResponse[0].("status")
        $jobStatus
    }

    Write-Host "$(Get-Date -format 'G'): $oozieJobId is in $JobStatus state!" -ForegroundColor Green

    #endregion


<span data-ttu-id="159d4-200">**tutorial de execução toore Olá**</span><span class="sxs-lookup"><span data-stu-id="159d4-200">**toore-run hello tutorial**</span></span>

<span data-ttu-id="159d4-201">fluxo de trabalho de execução toore hello, você deve excluir Olá itens a seguir:</span><span class="sxs-lookup"><span data-stu-id="159d4-201">toore-run hello workflow, you must delete hello following items:</span></span>

* <span data-ttu-id="159d4-202">saudação de arquivo de saída do script de Hive</span><span class="sxs-lookup"><span data-stu-id="159d4-202">hello Hive script output file</span></span>
* <span data-ttu-id="159d4-203">dados de saudação na tabela de log4jLogsCount Olá</span><span class="sxs-lookup"><span data-stu-id="159d4-203">hello data in hello log4jLogsCount table</span></span>

<span data-ttu-id="159d4-204">Este é um exemplo de script do PowerShell que você pode usar:</span><span class="sxs-lookup"><span data-stu-id="159d4-204">Here is a sample PowerShell script that you can use:</span></span>

    $resourceGroupName = "<AzureResourceGroupName>"

    $defaultStorageAccountName = "<AzureStorageAccountName>"
    $defaultBlobContainerName = "<ContainerName>"

    #SQL database variables
    $sqlDatabaseServerName = "<SQLDatabaseServerName>"
    $sqlDatabaseLogin = "<SQLDatabaseLoginName>"
    $sqlDatabasePassword = "<SQLDatabaseLoginPassword>"
    $sqlDatabaseName = "<SQLDatabaseName>"
    $sqlDatabaseTableName = "log4jLogsCount"

    Write-host "Delete hello Hive script output file ..." -ForegroundColor Green
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey `
                                -ResourceGroupName $resourceGroupName `
                                -Name $defaultStorageAccountName)[0].Value
    $destContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccountName -StorageAccountKey $defaultStorageAccountKey
    Remove-AzureStorageBlob -Context $destContext -Blob "tutorials/useoozie/output/000000_0" -Container $defaultBlobContainerName

    Write-host "Delete all hello records from hello log4jLogsCount table ..." -ForegroundColor Green
    $conn = New-Object System.Data.SqlClient.SqlConnection
    $conn.ConnectionString = "Data Source=$sqlDatabaseServerName.database.windows.net;Initial Catalog=$sqlDatabaseName;User ID=$sqlDatabaseLogin;Password=$sqlDatabasePassword;Encrypt=true;Trusted_Connection=false;"
    $conn.open()
    $cmd = New-Object System.Data.SqlClient.SqlCommand
    $cmd.connection = $conn
    $cmd.commandtext = "delete from $sqlDatabaseTableName"
    $cmd.executenonquery()

    $conn.close()

## <a name="next-steps"></a><span data-ttu-id="159d4-205">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="159d4-205">Next steps</span></span>
<span data-ttu-id="159d4-206">Neste tutorial, você aprendeu como toodefine uma Oozie como toorun uma Oozie de trabalho usando o PowerShell e o fluxo de trabalho.</span><span class="sxs-lookup"><span data-stu-id="159d4-206">In this tutorial, you learned how toodefine an Oozie workflow and how toorun an Oozie job by using PowerShell.</span></span> <span data-ttu-id="159d4-207">toolearn mais, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="159d4-207">toolearn more, see hello following articles:</span></span>

* <span data-ttu-id="159d4-208">[Usar o Coordenador do Oozie baseado em tempo com o HDInsight][hdinsight-oozie-coordinator-time]</span><span class="sxs-lookup"><span data-stu-id="159d4-208">[Use time-based Oozie Coordinator with HDInsight][hdinsight-oozie-coordinator-time]</span></span>
* <span data-ttu-id="159d4-209">[Começar a usar Hadoop com Hive no uso de celular tooanalyze HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="159d4-209">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="159d4-210">[Usar o armazenamento de Blobs do Azure com o HDInsight][hdinsight-storage]</span><span class="sxs-lookup"><span data-stu-id="159d4-210">[Use Azure Blob storage with HDInsight][hdinsight-storage]</span></span>
* <span data-ttu-id="159d4-211">[Administrar o HDInsight usando o PowerShell][hdinsight-admin-powershell]</span><span class="sxs-lookup"><span data-stu-id="159d4-211">[Administer HDInsight using PowerShell][hdinsight-admin-powershell]</span></span>
* <span data-ttu-id="159d4-212">[Carregar dados para trabalhos do Hadoop no HDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="159d4-212">[Upload data for Hadoop jobs in HDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="159d4-213">[Usar Sqoop com o Hadoop no HDInsight][hdinsight-use-sqoop]</span><span class="sxs-lookup"><span data-stu-id="159d4-213">[Use Sqoop with Hadoop in HDInsight][hdinsight-use-sqoop]</span></span>
* <span data-ttu-id="159d4-214">[Usar o Hive com Hadoop no HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="159d4-214">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="159d4-215">[Usar o Pig com Hadoop no HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="159d4-215">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="159d4-216">[Desenvolver programas Java MapReduce para HDInsight][hdinsight-develop-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="159d4-216">[Develop Java MapReduce programs for HDInsight][hdinsight-develop-mapreduce]</span></span>

[hdinsight-cmdlets-download]: http://go.microsoft.com/fwlink/?LinkID=325563



[azure-data-factory-pig-hive]: ../data-factory/data-factory-data-transformation-activities.md
[hdinsight-oozie-coordinator-time]: hdinsight-use-oozie-coordinator-time.md
[hdinsight-versions]:  hdinsight-component-versioning.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md
[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md
[hdinsight-admin-portal]: hdinsight-administer-use-management-portal.md


[hdinsight-use-sqoop]: hdinsight-use-sqoop.md
[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-develop-mapreduce]: hdinsight-develop-deploy-java-mapreduce-linux.md

[sqldatabase-create-configue]: ../sql-database-create-configure.md
[sqldatabase-get-started]: ../sql-database-get-started.md

[azure-management-portal]: https://portal.azure.com/
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
