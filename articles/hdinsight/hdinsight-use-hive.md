---
title: "aaaWhat é o Apache Hive e HiveQL - HDInsight do Azure | Microsoft Docs"
description: "O Apache Hive é um sistema de data warehouse para Hadoop. Você pode consultar os dados armazenados no Hive usando o HiveQL, quais semelhante tooTransact-SQL. Neste documento, saiba como toouse Hive e HiveQL com HDInsight do Azure."
keywords: "o hiveql, o que é o hive, hiveql hadoop, hive, o que é o hive de saber como toouse hive,"
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 2c10f989-7636-41bf-b7f7-c4b67ec0814f
ms.service: hdinsight
ms.custom: hdinsightactive,hdiseo17may2017
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/03/2017
ms.author: larryfr
ms.openlocfilehash: a2772312263895ff99b499898264c2e6d5e816e9
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="what-is-apache-hive-and-hiveql-on-azure-hdinsight"></a><span data-ttu-id="adffe-106">Saiba mais sobre o Apache Hive e o HiveQL no Azure HDInsight?</span><span class="sxs-lookup"><span data-stu-id="adffe-106">What is Apache Hive and HiveQL on Azure HDInsight?</span></span>

<span data-ttu-id="adffe-107">O [Apache Hive](http://hive.apache.org/) é um sistema de data warehouse para Hadoop.</span><span class="sxs-lookup"><span data-stu-id="adffe-107">[Apache Hive](http://hive.apache.org/) is a data warehouse system for Hadoop.</span></span> <span data-ttu-id="adffe-108">O Hive permite o resumo de dados, consultas e análise de dados.</span><span class="sxs-lookup"><span data-stu-id="adffe-108">Hive enables data summarization, querying, and analysis of data.</span></span> <span data-ttu-id="adffe-109">Consultas de hive são gravadas em HiveQL, que é um tooSQL semelhante de linguagem de consulta.</span><span class="sxs-lookup"><span data-stu-id="adffe-109">Hive queries are written in HiveQL, which is a query language similar tooSQL.</span></span>

<span data-ttu-id="adffe-110">Seção permite que você tooproject estrutura em dados amplamente.</span><span class="sxs-lookup"><span data-stu-id="adffe-110">Hive allows you tooproject structure on largely unstructured data.</span></span> <span data-ttu-id="adffe-111">Depois de definir a estrutura de saudação, você pode usar dados de saudação do HiveQL tooquery sem o conhecimento do Java ou MapReduce.</span><span class="sxs-lookup"><span data-stu-id="adffe-111">After you define hello structure, you can use HiveQL tooquery hello data without knowledge of Java or MapReduce.</span></span>

<span data-ttu-id="adffe-112">O HDInsight fornece vários tipos de cluster, que são ajustados para cargas de trabalho específicas.</span><span class="sxs-lookup"><span data-stu-id="adffe-112">HDInsight provides several cluster types, which are tuned for specific workloads.</span></span> <span data-ttu-id="adffe-113">Olá seguintes tipos de cluster é geralmente usada para consultas de Hive:</span><span class="sxs-lookup"><span data-stu-id="adffe-113">hello following cluster types are most often used for Hive queries:</span></span>

* <span data-ttu-id="adffe-114">__Hive interativo__: Hadoop de um cluster que fornece [baixa latência analíticos processamento (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) tempos de resposta de tooimprove funcionalidade para consultas interativas.</span><span class="sxs-lookup"><span data-stu-id="adffe-114">__Interactive Hive__: A Hadoop cluster that provides [Low Latency Analytical Processing (LLAP)](https://cwiki.apache.org/confluence/display/Hive/LLAP) functionality tooimprove response times for interactive queries.</span></span> <span data-ttu-id="adffe-115">Para obter mais informações, consulte Olá [iniciar com interativo Hive no HDInsight](hdinsight-hadoop-use-interactive-hive.md) documento.</span><span class="sxs-lookup"><span data-stu-id="adffe-115">For more information, see hello [Start with Interactive Hive in HDInsight](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

* <span data-ttu-id="adffe-116">__Hadoop__: um cluster Hadoop que está ajustado para cargas de trabalho de processamento em lotes.</span><span class="sxs-lookup"><span data-stu-id="adffe-116">__Hadoop__: A Hadoop cluster that is tuned for batch processing workloads.</span></span> <span data-ttu-id="adffe-117">Para obter mais informações, consulte Olá [iniciar com Hadoop no HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) documento.</span><span class="sxs-lookup"><span data-stu-id="adffe-117">For more information, see hello [Start with Hadoop in HDInsight](hdinsight-hadoop-linux-tutorial-get-started.md) document.</span></span>

* <span data-ttu-id="adffe-118">__Spark__: o Apache Spark tem funcionalidade interna para trabalhar com o Hive.</span><span class="sxs-lookup"><span data-stu-id="adffe-118">__Spark__: Apache Spark has built-in functionality for working with Hive.</span></span> <span data-ttu-id="adffe-119">Para obter mais informações, consulte Olá [iniciar com Spark no HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) documento.</span><span class="sxs-lookup"><span data-stu-id="adffe-119">For more information, see hello [Start with Spark on HDInsight](hdinsight-apache-spark-jupyter-spark-sql.md) document.</span></span>

* <span data-ttu-id="adffe-120">__HBase__: HiveQL pode ser usado tooquery dados armazenados em HBase.</span><span class="sxs-lookup"><span data-stu-id="adffe-120">__HBase__: HiveQL can be used tooquery data stored in HBase.</span></span> <span data-ttu-id="adffe-121">Para obter mais informações, consulte Olá [iniciar com HBase em HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) documento.</span><span class="sxs-lookup"><span data-stu-id="adffe-121">For more information, see hello [Start with HBase on HDInsight](hdinsight-hbase-tutorial-get-started-linux.md) document.</span></span>

## <a name="how-toouse-hive"></a><span data-ttu-id="adffe-122">Como toouse Hive</span><span class="sxs-lookup"><span data-stu-id="adffe-122">How toouse Hive</span></span>

<span data-ttu-id="adffe-123">Use Olá toodiscover de tabela como toouse Hive com HDInsight a seguir:</span><span class="sxs-lookup"><span data-stu-id="adffe-123">Use hello following table toodiscover how toouse Hive with HDInsight:</span></span>

| <span data-ttu-id="adffe-124">**Use esse método** se você quiser...</span><span class="sxs-lookup"><span data-stu-id="adffe-124">**Use this method** if you want...</span></span> | <span data-ttu-id="adffe-125">...um shell **interativo**</span><span class="sxs-lookup"><span data-stu-id="adffe-125">...an **interactive** shell</span></span> | <span data-ttu-id="adffe-126">...Processamento em**lotes**</span><span class="sxs-lookup"><span data-stu-id="adffe-126">...**batch** processing</span></span> | <span data-ttu-id="adffe-127">... com esse **sistema operacional de cluster**</span><span class="sxs-lookup"><span data-stu-id="adffe-127">...with this **cluster operating system**</span></span> | <span data-ttu-id="adffe-128">... desse **sistema operacional cliente**</span><span class="sxs-lookup"><span data-stu-id="adffe-128">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="adffe-129">Exibição de Hive</span><span class="sxs-lookup"><span data-stu-id="adffe-129">Hive View</span></span>](hdinsight-hadoop-use-hive-ambari-view.md) |<span data-ttu-id="adffe-130">✔</span><span class="sxs-lookup"><span data-stu-id="adffe-130">✔</span></span> |<span data-ttu-id="adffe-131">✔</span><span class="sxs-lookup"><span data-stu-id="adffe-131">✔</span></span> |<span data-ttu-id="adffe-132">Linux</span><span class="sxs-lookup"><span data-stu-id="adffe-132">Linux</span></span> |<span data-ttu-id="adffe-133">Qualquer um (baseado em navegador)</span><span class="sxs-lookup"><span data-stu-id="adffe-133">Any (browser based)</span></span> |
| [<span data-ttu-id="adffe-134">Cliente de Beeline</span><span class="sxs-lookup"><span data-stu-id="adffe-134">Beeline client</span></span>](hdinsight-hadoop-use-hive-beeline.md) |<span data-ttu-id="adffe-135">✔</span><span class="sxs-lookup"><span data-stu-id="adffe-135">✔</span></span> |<span data-ttu-id="adffe-136">✔</span><span class="sxs-lookup"><span data-stu-id="adffe-136">✔</span></span> |<span data-ttu-id="adffe-137">Linux</span><span class="sxs-lookup"><span data-stu-id="adffe-137">Linux</span></span> |<span data-ttu-id="adffe-138">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="adffe-138">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="adffe-139">API REST</span><span class="sxs-lookup"><span data-stu-id="adffe-139">REST API</span></span>](hdinsight-hadoop-use-hive-curl.md) |&nbsp; |<span data-ttu-id="adffe-140">✔</span><span class="sxs-lookup"><span data-stu-id="adffe-140">✔</span></span> |<span data-ttu-id="adffe-141">Linux ou Windows*</span><span class="sxs-lookup"><span data-stu-id="adffe-141">Linux or Windows*</span></span> |<span data-ttu-id="adffe-142">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="adffe-142">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="adffe-143">Ferramentas do HDInsight para Visual Studio</span><span class="sxs-lookup"><span data-stu-id="adffe-143">HDInsight tools for Visual Studio</span></span>](hdinsight-hadoop-use-hive-visual-studio.md) |&nbsp; |<span data-ttu-id="adffe-144">✔</span><span class="sxs-lookup"><span data-stu-id="adffe-144">✔</span></span> |<span data-ttu-id="adffe-145">Linux ou Windows*</span><span class="sxs-lookup"><span data-stu-id="adffe-145">Linux or Windows*</span></span> |<span data-ttu-id="adffe-146">Windows</span><span class="sxs-lookup"><span data-stu-id="adffe-146">Windows</span></span> |
| [<span data-ttu-id="adffe-147">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="adffe-147">Windows PowerShell</span></span>](hdinsight-hadoop-use-hive-powershell.md) |&nbsp; |<span data-ttu-id="adffe-148">✔</span><span class="sxs-lookup"><span data-stu-id="adffe-148">✔</span></span> |<span data-ttu-id="adffe-149">Linux ou Windows*</span><span class="sxs-lookup"><span data-stu-id="adffe-149">Linux or Windows*</span></span> |<span data-ttu-id="adffe-150">Windows</span><span class="sxs-lookup"><span data-stu-id="adffe-150">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="adffe-151">\*Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="adffe-151">\* Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="adffe-152">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="adffe-152">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>
>
> <span data-ttu-id="adffe-153">Se você estiver usando um cluster HDInsight baseados no Windows, você pode usar o hello [console de consulta](hdinsight-hadoop-use-hive-query-console.md) do navegador ou [área de trabalho remota](hdinsight-hadoop-use-hive-remote-desktop.md) toorun consultas de Hive.</span><span class="sxs-lookup"><span data-stu-id="adffe-153">If you are using a Windows-based HDInsight cluster, you can use hello [Query console](hdinsight-hadoop-use-hive-query-console.md) from your browser or [Remote Desktop](hdinsight-hadoop-use-hive-remote-desktop.md) toorun Hive queries.</span></span>

## <a name="hiveql-language-reference"></a><span data-ttu-id="adffe-154">Referência da linguagem HiveQL</span><span class="sxs-lookup"><span data-stu-id="adffe-154">HiveQL language reference</span></span>

<span data-ttu-id="adffe-155">Referência de linguagem HiveQL está disponível no hello [manual do idioma (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span><span class="sxs-lookup"><span data-stu-id="adffe-155">HiveQL language reference is available in hello [language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual).</span></span>

## <a name="hive-and-data-structure"></a><span data-ttu-id="adffe-156">Hive e estrutura de dados</span><span class="sxs-lookup"><span data-stu-id="adffe-156">Hive and data structure</span></span>

<span data-ttu-id="adffe-157">Hive entende como toowork com estruturado e dados estruturados.</span><span class="sxs-lookup"><span data-stu-id="adffe-157">Hive understands how toowork with structured and semi-structured data.</span></span> <span data-ttu-id="adffe-158">Por exemplo, arquivos de texto onde os campos de saudação são delimitados por caracteres específicos.</span><span class="sxs-lookup"><span data-stu-id="adffe-158">For example, text files where hello fields are delimited by specific characters.</span></span> <span data-ttu-id="adffe-159">Olá HiveQL instrução a seguir cria uma tabela de dados delimitados por espaço:</span><span class="sxs-lookup"><span data-stu-id="adffe-159">hello following HiveQL statement creates a table over space-delimited data:</span></span>

```hiveql
CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
STORED AS TEXTFILE LOCATION '/example/data/';
```

<span data-ttu-id="adffe-160">O Hive também dá suporte a **serializador/desserializadores (SerDe)** personalizados para dados complexos ou com estrutura irregular.</span><span class="sxs-lookup"><span data-stu-id="adffe-160">Hive also supports custom **serializer/deserializers (SerDe)** for complex or irregularly structured data.</span></span> <span data-ttu-id="adffe-161">Para obter mais informações, consulte Olá [como toouse uma SerDe JSON personalizado com HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) documento.</span><span class="sxs-lookup"><span data-stu-id="adffe-161">For more information, see hello [How toouse a custom JSON SerDe with HDInsight](http://blogs.msdn.com/b/bigdatasupport/archive/2014/06/18/how-to-use-a-custom-json-serde-with-microsoft-azure-hdinsight.aspx) document.</span></span>

<span data-ttu-id="adffe-162">Para obter mais informações sobre formatos de arquivo suportados pelo Hive, consulte Olá [manual do idioma (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span><span class="sxs-lookup"><span data-stu-id="adffe-162">For more information on file formats supported by Hive, see hello [Language manual (https://cwiki.apache.org/confluence/display/Hive/LanguageManual)](https://cwiki.apache.org/confluence/display/Hive/LanguageManual)</span></span>

## <a name="hive-internal-tables-vs-external-tables"></a><span data-ttu-id="adffe-163">Tabelas internas Hive vs. tabelas externas</span><span class="sxs-lookup"><span data-stu-id="adffe-163">Hive internal tables vs external tables</span></span>

<span data-ttu-id="adffe-164">Há dois tipos de tabelas que você pode criar com o Hive:</span><span class="sxs-lookup"><span data-stu-id="adffe-164">There are two types of tables that you can create with Hive:</span></span>

* <span data-ttu-id="adffe-165">__Interno__: dados são armazenados no data warehouse do hello Hive.</span><span class="sxs-lookup"><span data-stu-id="adffe-165">__Internal__: Data is stored in hello Hive data warehouse.</span></span> <span data-ttu-id="adffe-166">Olá do data warehouse está localizado em `/hive/warehouse/` no armazenamento de padrão de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="adffe-166">hello data warehouse is located at `/hive/warehouse/` on hello default storage for hello cluster.</span></span>

    <span data-ttu-id="adffe-167">Use tabelas internas quando:</span><span class="sxs-lookup"><span data-stu-id="adffe-167">Use internal tables when:</span></span>

    * <span data-ttu-id="adffe-168">Os dados são temporários.</span><span class="sxs-lookup"><span data-stu-id="adffe-168">Data is temporary.</span></span>
    * <span data-ttu-id="adffe-169">Você deseja Hive toomanage saudação do ciclo de vida de saudação e os dados.</span><span class="sxs-lookup"><span data-stu-id="adffe-169">You want Hive toomanage hello lifecycle of hello table and data.</span></span>

* <span data-ttu-id="adffe-170">__Externa__: os dados são armazenados fora do hello data warehouse.</span><span class="sxs-lookup"><span data-stu-id="adffe-170">__External__: Data is stored outside hello data warehouse.</span></span> <span data-ttu-id="adffe-171">dados de saudação podem ser armazenados em qualquer armazenamento acessível pelo cluster hello.</span><span class="sxs-lookup"><span data-stu-id="adffe-171">hello data can be stored on any storage accessible by hello cluster.</span></span>

    <span data-ttu-id="adffe-172">Use tabelas externas quando:</span><span class="sxs-lookup"><span data-stu-id="adffe-172">Use external tables when:</span></span>

    * <span data-ttu-id="adffe-173">dados de saudação também são usados fora do Hive.</span><span class="sxs-lookup"><span data-stu-id="adffe-173">hello data is also used outside of Hive.</span></span> <span data-ttu-id="adffe-174">Por exemplo, arquivos de dados de saudação são atualizados por outro processo (que não bloqueia arquivos hello.)</span><span class="sxs-lookup"><span data-stu-id="adffe-174">For example, hello data files are updated by another process (that does not lock hello files.)</span></span>
    * <span data-ttu-id="adffe-175">Dados precisam tooremain em Olá subjacente local, mesmo depois de descartar a tabela hello.</span><span class="sxs-lookup"><span data-stu-id="adffe-175">Data needs tooremain in hello underlying location, even after dropping hello table.</span></span>
    * <span data-ttu-id="adffe-176">Você precisa de um local personalizado, como uma conta de armazenamento não padrão.</span><span class="sxs-lookup"><span data-stu-id="adffe-176">You need a custom location, such as a non-default storage account.</span></span>
    * <span data-ttu-id="adffe-177">Um programa diferente do hive gerencia o formato de dados hello, local, etc.</span><span class="sxs-lookup"><span data-stu-id="adffe-177">A program other than hive manages hello data format, location, etc.</span></span>

<span data-ttu-id="adffe-178">Para obter mais informações, consulte Olá [Hive internos e externos introdução de tabelas] [ cindygross-hive-tables] postagem de blog.</span><span class="sxs-lookup"><span data-stu-id="adffe-178">For more information, see hello [Hive Internal and External Tables Intro][cindygross-hive-tables] blog post.</span></span>

## <a name="user-defined-functions-udf"></a><span data-ttu-id="adffe-179">UDF (Funções definidas pelo usuário)</span><span class="sxs-lookup"><span data-stu-id="adffe-179">User-defined functions (UDF)</span></span>

<span data-ttu-id="adffe-180">O Hive também pode ser estendido por meio de **UDF (funções definidas pelo usuário)**.</span><span class="sxs-lookup"><span data-stu-id="adffe-180">Hive can also be extended through **user-defined functions (UDF)**.</span></span> <span data-ttu-id="adffe-181">Um UDF permite funcionalidade tooimplement ou lógica que não é modelada facilmente no estilo.</span><span class="sxs-lookup"><span data-stu-id="adffe-181">A UDF allows you tooimplement functionality or logic that isn't easily modeled in HiveQL.</span></span> <span data-ttu-id="adffe-182">Para obter um exemplo do uso de UDFs com Hive, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="adffe-182">For an example of using UDFs with Hive, see hello following documents:</span></span>

* [<span data-ttu-id="adffe-183">Como usar uma função definida pelo usuário do Java com o Hive</span><span class="sxs-lookup"><span data-stu-id="adffe-183">Use a Java user-defined function with Hive</span></span>](hdinsight-hadoop-hive-java-udf.md)

* [<span data-ttu-id="adffe-184">Como usar uma função definida pelo usuário do Python com Hive e Pig</span><span class="sxs-lookup"><span data-stu-id="adffe-184">Use a Python user-defined function with Hive and Pig</span></span>](hdinsight-python.md)

* [<span data-ttu-id="adffe-185">Como usar uma função definidas pelo usuário do C# com Hive e Pig</span><span class="sxs-lookup"><span data-stu-id="adffe-185">Use a C# user-defined function with Hive and Pig</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

* [<span data-ttu-id="adffe-186">Como tooadd um Hive personalizado definido pelo usuário função tooHDInsight</span><span class="sxs-lookup"><span data-stu-id="adffe-186">How tooadd a custom Hive user-defined function tooHDInsight</span></span>](http://blogs.msdn.com/b/bigdatasupport/archive/2014/01/14/how-to-add-custom-hive-udfs-to-hdinsight.aspx)

* [<span data-ttu-id="adffe-187">Uma exemplo Hive função definida pelo usuário tooconvert data/hora formatos tooHive timestamp</span><span class="sxs-lookup"><span data-stu-id="adffe-187">An example Hive user-defined function tooconvert date/time formats tooHive timestamp</span></span>](https://github.com/Azure-Samples/hdinsight-java-hive-udf)

## <span data-ttu-id="adffe-188"><a id="data"></a>Dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="adffe-188"><a id="data"></a>Example data</span></span>

<span data-ttu-id="adffe-189">O Hive no HDInsight vem pré-carregado com uma tabela interna chamada `hivesampletable`.</span><span class="sxs-lookup"><span data-stu-id="adffe-189">Hive on HDInsight comes pre-loaded with an internal table named `hivesampletable`.</span></span> <span data-ttu-id="adffe-190">O HDInsight também fornece conjuntos de dados de exemplo que podem ser usados com o Hive.</span><span class="sxs-lookup"><span data-stu-id="adffe-190">HDInsight also provides example data sets that can be used with Hive.</span></span> <span data-ttu-id="adffe-191">Esses conjuntos de dados são armazenados em Olá `/example/data` e `/HdiSamples` diretórios.</span><span class="sxs-lookup"><span data-stu-id="adffe-191">These data sets are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="adffe-192">Esses diretórios existem no armazenamento padrão da saudação para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="adffe-192">These directories exist in hello default storage for your cluster.</span></span>

## <span data-ttu-id="adffe-193"><a id="job"></a>Exemplo de consulta do Hive</span><span class="sxs-lookup"><span data-stu-id="adffe-193"><a id="job"></a>Example Hive query</span></span>

<span data-ttu-id="adffe-194">Olá após HiveQL instruções projeto colunas Olá `/example/data/sample.log` arquivo:</span><span class="sxs-lookup"><span data-stu-id="adffe-194">hello following HiveQL statements project columns onto hello `/example/data/sample.log` file:</span></span>

    set hive.execution.engine=tez;
    DROP TABLE log4jLogs;
    CREATE EXTERNAL TABLE log4jLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    ROW FORMAT DELIMITED FIELDS TERMINATED BY ' '
    STORED AS TEXTFILE LOCATION '/example/data/';
    SELECT t4 AS sev, COUNT(*) AS count FROM log4jLogs WHERE t4 = '[ERROR]' AND INPUT__FILE__NAME LIKE '%.log' GROUP BY t4;

<span data-ttu-id="adffe-195">No exemplo anterior de saudação, instruções de HiveQL Olá executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="adffe-195">In hello previous example, hello HiveQL statements perform hello following actions:</span></span>

* <span data-ttu-id="adffe-196">`set hive.execution.engine=tez;`: Define Olá toouse do mecanismo de execução Tez.</span><span class="sxs-lookup"><span data-stu-id="adffe-196">`set hive.execution.engine=tez;`: Sets hello execution engine toouse Tez.</span></span> <span data-ttu-id="adffe-197">Usar o Tez no lugar do MapReduce pode fornecer um aumento no desempenho da consulta.</span><span class="sxs-lookup"><span data-stu-id="adffe-197">Using Tez instead of MapReduce can provide an increase in query performance.</span></span> <span data-ttu-id="adffe-198">Para obter mais informações sobre Tez, consulte Olá [Tez do Apache de uso para melhorar o desempenho](#usetez) seção.</span><span class="sxs-lookup"><span data-stu-id="adffe-198">For more information on Tez, see hello [Use Apache Tez for improved performance](#usetez) section.</span></span>

    > [!NOTE]
    > <span data-ttu-id="adffe-199">Essa instrução só é necessária ao usar um cluster HDInsight baseado em Windows.</span><span class="sxs-lookup"><span data-stu-id="adffe-199">This statement is only required when using a Windows-based HDInsight cluster.</span></span> <span data-ttu-id="adffe-200">Tez é o mecanismo de execução padrão Olá para HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="adffe-200">Tez is hello default execution engine for Linux-based HDInsight.</span></span>

* <span data-ttu-id="adffe-201">`DROP TABLE`: Se Olá tabela já existir, exclua-o.</span><span class="sxs-lookup"><span data-stu-id="adffe-201">`DROP TABLE`: If hello table already exists, delete it.</span></span>

* <span data-ttu-id="adffe-202">`CREATE EXTERNAL TABLE`: cria uma nova tabela **externa** no Hive.</span><span class="sxs-lookup"><span data-stu-id="adffe-202">`CREATE EXTERNAL TABLE`: Creates a new **external** table in Hive.</span></span> <span data-ttu-id="adffe-203">Tabelas externas apenas armazenam a definição de tabela Olá no Hive.</span><span class="sxs-lookup"><span data-stu-id="adffe-203">External tables only store hello table definition in Hive.</span></span> <span data-ttu-id="adffe-204">dados de saudação são deixados no local original hello e no formato original hello.</span><span class="sxs-lookup"><span data-stu-id="adffe-204">hello data is left in hello original location and in hello original format.</span></span>

* <span data-ttu-id="adffe-205">`ROW FORMAT`: Informa ao Hive como Olá dados são formatados.</span><span class="sxs-lookup"><span data-stu-id="adffe-205">`ROW FORMAT`: Tells Hive how hello data is formatted.</span></span> <span data-ttu-id="adffe-206">Nesse caso, os campos de saudação em cada log são separados por um espaço.</span><span class="sxs-lookup"><span data-stu-id="adffe-206">In this case, hello fields in each log are separated by a space.</span></span>

* <span data-ttu-id="adffe-207">`STORED AS TEXTFILE LOCATION`: Informa ao Hive onde hello os dados são armazenados (Olá `example/data` directory) e que ela é armazenada como texto.</span><span class="sxs-lookup"><span data-stu-id="adffe-207">`STORED AS TEXTFILE LOCATION`: Tells Hive where hello data is stored (hello `example/data` directory) and that it is stored as text.</span></span> <span data-ttu-id="adffe-208">dados saudação podem estar em um arquivo ou distribuídos em vários arquivos no diretório de saudação.</span><span class="sxs-lookup"><span data-stu-id="adffe-208">hello data can be in one file or spread across multiple files within hello directory.</span></span>

* <span data-ttu-id="adffe-209">`SELECT`: Seleciona uma contagem de todas as linhas onde hello coluna **t4** contém valor Olá **[Erro]**.</span><span class="sxs-lookup"><span data-stu-id="adffe-209">`SELECT`: Selects a count of all rows where hello column **t4** contains hello value **[ERROR]**.</span></span> <span data-ttu-id="adffe-210">Essa instrução retorna um valor de **3**, já que há três linhas que contêm esse valor.</span><span class="sxs-lookup"><span data-stu-id="adffe-210">This statement returns a value of **3** because there are three rows that contain this value.</span></span>

* <span data-ttu-id="adffe-211">`INPUT__FILE__NAME LIKE '%.log'`-Hive tentativas tooapply Olá esquema tooall arquivos Olá diretório.</span><span class="sxs-lookup"><span data-stu-id="adffe-211">`INPUT__FILE__NAME LIKE '%.log'` - Hive attempts tooapply hello schema tooall files in hello directory.</span></span> <span data-ttu-id="adffe-212">Nesse caso, o diretório de saudação contém arquivos que não correspondem ao esquema de saudação.</span><span class="sxs-lookup"><span data-stu-id="adffe-212">In this case, hello directory contains files that do not match hello schema.</span></span> <span data-ttu-id="adffe-213">dados de lixo tooprevent nos resultados de hello, essa instrução informa Hive que só deve retornar dados de arquivos que terminam em. log.</span><span class="sxs-lookup"><span data-stu-id="adffe-213">tooprevent garbage data in hello results, this statement tells Hive that we should only return data from files ending in .log.</span></span>

> [!NOTE]
> <span data-ttu-id="adffe-214">Tabelas externas devem ser usadas quando você espera Olá toobe de dados subjacentes atualizado por uma fonte externa.</span><span class="sxs-lookup"><span data-stu-id="adffe-214">External tables should be used when you expect hello underlying data toobe updated by an external source.</span></span> <span data-ttu-id="adffe-215">Por exemplo, um processo de upload de dados automatizado ou uma operação MapReduce.</span><span class="sxs-lookup"><span data-stu-id="adffe-215">For example, an automated data upload process, or MapReduce operation.</span></span>
>
> <span data-ttu-id="adffe-216">Descartar uma tabela externa **não** excluir dados hello, exclui somente a definição de tabela hello.</span><span class="sxs-lookup"><span data-stu-id="adffe-216">Dropping an external table does **not** delete hello data, it only deletes hello table definition.</span></span>

<span data-ttu-id="adffe-217">toocreate um **interno** tabela em vez de externo, use Olá HiveQL a seguir:</span><span class="sxs-lookup"><span data-stu-id="adffe-217">toocreate an **internal** table instead of external, use hello following HiveQL:</span></span>

    set hive.execution.engine=tez;
    CREATE TABLE IF NOT EXISTS errorLogs (t1 string, t2 string, t3 string, t4 string, t5 string, t6 string, t7 string)
    STORED AS ORC;
    INSERT OVERWRITE TABLE errorLogs
    SELECT t1, t2, t3, t4, t5, t6, t7 FROM log4jLogs WHERE t4 = '[ERROR]';

<span data-ttu-id="adffe-218">Essas instruções executam Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="adffe-218">These statements perform hello following actions:</span></span>

* <span data-ttu-id="adffe-219">`CREATE TABLE IF NOT EXISTS`: Se a tabela de saudação não existe, criá-lo.</span><span class="sxs-lookup"><span data-stu-id="adffe-219">`CREATE TABLE IF NOT EXISTS`: If hello table does not exist, create it.</span></span> <span data-ttu-id="adffe-220">Porque Olá **externo** palavra-chave não for usada, essa instrução cria uma tabela interna.</span><span class="sxs-lookup"><span data-stu-id="adffe-220">Because hello **EXTERNAL** keyword is not used, this statement creates an internal table.</span></span> <span data-ttu-id="adffe-221">tabela de saudação é armazenada no data warehouse do hello Hive e é totalmente gerenciada pelo Hive.</span><span class="sxs-lookup"><span data-stu-id="adffe-221">hello table is stored in hello Hive data warehouse and is managed completely by Hive.</span></span>

* <span data-ttu-id="adffe-222">`STORED AS ORC`: Armazena dados saudação no formato de linha de otimização Colunar (ORC).</span><span class="sxs-lookup"><span data-stu-id="adffe-222">`STORED AS ORC`: Stores hello data in Optimized Row Columnar (ORC) format.</span></span> <span data-ttu-id="adffe-223">Esse é um formato altamente otimizado e eficiente para o armazenamento de dados do Hive.</span><span class="sxs-lookup"><span data-stu-id="adffe-223">ORC is a highly optimized and efficient format for storing Hive data.</span></span>

* <span data-ttu-id="adffe-224">`INSERT OVERWRITE ... SELECT`: Seleciona linhas Olá **log4jLogs** tabela que contém **[Erro]**, e, em seguida, insere Olá dados em Olá **em decorrência** tabela.</span><span class="sxs-lookup"><span data-stu-id="adffe-224">`INSERT OVERWRITE ... SELECT`: Selects rows from hello **log4jLogs** table that contains **[ERROR]**, and then inserts hello data into hello **errorLogs** table.</span></span>

> [!NOTE]
> <span data-ttu-id="adffe-225">Ao contrário das tabelas externas, descartar uma tabela interna também exclui dados subjacentes hello.</span><span class="sxs-lookup"><span data-stu-id="adffe-225">Unlike external tables, dropping an internal table also deletes hello underlying data.</span></span>

## <a name="improve-hive-query-performance"></a><span data-ttu-id="adffe-226">Como melhorar o desempenho de consulta de Hive</span><span class="sxs-lookup"><span data-stu-id="adffe-226">Improve Hive query performance</span></span>

### <span data-ttu-id="adffe-227"><a id="usetez"></a>Apache Tez</span><span class="sxs-lookup"><span data-stu-id="adffe-227"><a id="usetez"></a>Apache Tez</span></span>

<span data-ttu-id="adffe-228">[Apache Tez](http://tez.apache.org) é uma estrutura que permite que aplicativos intensivos de dados, como o Hive, toorun muito mais eficiência em escala.</span><span class="sxs-lookup"><span data-stu-id="adffe-228">[Apache Tez](http://tez.apache.org) is a framework that allows data intensive applications, such as Hive, toorun much more efficiently at scale.</span></span> <span data-ttu-id="adffe-229">O Tez está habilitado por padrão para clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="adffe-229">Tez is enabled by default for Linux-based HDInsight clusters.</span></span>

> [!NOTE]
> <span data-ttu-id="adffe-230">Atualmente o Tez está desativado por padrão para clusters baseados no Windows HDInsight e deve ser habilitado.</span><span class="sxs-lookup"><span data-stu-id="adffe-230">Tez is currently off by default for Windows-based HDInsight clusters and it must be enabled.</span></span> <span data-ttu-id="adffe-231">tootake aproveitar Tez, Olá seguinte valor deve ser definida para uma consulta de Hive:</span><span class="sxs-lookup"><span data-stu-id="adffe-231">tootake advantage of Tez, hello following value must be set for a Hive query:</span></span>
>
> `set hive.execution.engine=tez;`
>
> <span data-ttu-id="adffe-232">Tez é o mecanismo padrão de saudação para clusters HDInsight baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="adffe-232">Tez is hello default engine for Linux-based HDInsight clusters.</span></span>

<span data-ttu-id="adffe-233">Olá [Hive em documentos de design Tez](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contém detalhes sobre as opções de implementação de saudação e configurações de ajustes.</span><span class="sxs-lookup"><span data-stu-id="adffe-233">hello [Hive on Tez design documents](https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez) contains details about hello implementation choices and tuning configurations.</span></span>

<span data-ttu-id="adffe-234">tooaid na depuração de trabalhos foi executada usando Tez, HDInsight fornece Olá interfaces do usuário da web que permitem que você tooview detalhes dos trabalhos Tez a seguir:</span><span class="sxs-lookup"><span data-stu-id="adffe-234">tooaid in debugging jobs ran using Tez, HDInsight provides hello following web UIs that allow you tooview details of Tez jobs:</span></span>

* [<span data-ttu-id="adffe-235">Use Olá exibição Ambari Tez no HDInsight baseados em Linux</span><span class="sxs-lookup"><span data-stu-id="adffe-235">Use hello Ambari Tez view on Linux-based HDInsight</span></span>](hdinsight-debug-ambari-tez-view.md)

* [<span data-ttu-id="adffe-236">Use Olá Tez UI no HDInsight baseados no Windows</span><span class="sxs-lookup"><span data-stu-id="adffe-236">Use hello Tez UI on Windows-based HDInsight</span></span>](hdinsight-debug-tez-ui.md)

### <a name="low-latency-analytical-processing-llap"></a><span data-ttu-id="adffe-237">Processamento analítico de baixa latência (LLAP)</span><span class="sxs-lookup"><span data-stu-id="adffe-237">Low Latency Analytical Processing (LLAP)</span></span>

<span data-ttu-id="adffe-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (também conhecido como vida longa e processo) é um novo recurso no Hive 2.0 que permite armazenar as consultas em cache na memória.</span><span class="sxs-lookup"><span data-stu-id="adffe-238">[LLAP](https://cwiki.apache.org/confluence/display/Hive/LLAP) (sometimes known as Live Long and Process) is a new feature in Hive 2.0 that allows in-memory caching of queries.</span></span> <span data-ttu-id="adffe-239">LLAP torna muito mais rápido, backup de consultas de Hive muito[26 x mais rápido do que 1. x em alguns casos de Hive](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span><span class="sxs-lookup"><span data-stu-id="adffe-239">LLAP makes Hive queries much faster, up too[26x faster than Hive 1.x in some cases](https://hortonworks.com/blog/announcing-apache-hive-2-1-25x-faster-queries-much/).</span></span>

<span data-ttu-id="adffe-240">HDInsight fornece LLAP no hello Hive interativo tipo de cluster.</span><span class="sxs-lookup"><span data-stu-id="adffe-240">HDInsight provides LLAP in hello Interactive Hive cluster type.</span></span> <span data-ttu-id="adffe-241">Para obter mais informações, consulte Olá [iniciar com Hive interativo](hdinsight-hadoop-use-interactive-hive.md) documento.</span><span class="sxs-lookup"><span data-stu-id="adffe-241">For more information, see hello [Start with Interactive Hive](hdinsight-hadoop-use-interactive-hive.md) document.</span></span>

## <a name="hive-jobs-and-sql-server-integration-services"></a><span data-ttu-id="adffe-242">Trabalhos do Hive e SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="adffe-242">Hive jobs and SQL Server Integration Services</span></span>

<span data-ttu-id="adffe-243">Você pode usar o SQL Server Integration Services (SSIS) toorun um trabalho de Hive.</span><span class="sxs-lookup"><span data-stu-id="adffe-243">You can use SQL Server Integration Services (SSIS) toorun a Hive job.</span></span> <span data-ttu-id="adffe-244">Hello Azure Feature Pack para SSIS fornece Olá componentes que funcionam com os trabalhos de Hive no HDInsight a seguir.</span><span class="sxs-lookup"><span data-stu-id="adffe-244">hello Azure Feature Pack for SSIS provides hello following components that work with Hive jobs on HDInsight.</span></span>

* <span data-ttu-id="adffe-245">[Tarefa do Hive do Azure HDInsight][hivetask]</span><span class="sxs-lookup"><span data-stu-id="adffe-245">[Azure HDInsight Hive Task][hivetask]</span></span>

* <span data-ttu-id="adffe-246">[Gerenciador de Conexões de Assinatura do Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="adffe-246">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="adffe-247">Saiba mais sobre hello Azure Feature Pack para SSIS [aqui][ssispack].</span><span class="sxs-lookup"><span data-stu-id="adffe-247">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="adffe-248"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="adffe-248"><a id="nextsteps"></a>Next steps</span></span>

<span data-ttu-id="adffe-249">Agora que você aprendeu Hive e como toouse com Hadoop no HDInsight, Olá uso a seguir vincula tooexplore toowork outras formas ao HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="adffe-249">Now that you've learned what Hive is and how toouse it with Hadoop in HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="adffe-250">[Carregar dados tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="adffe-250">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="adffe-251">[Usar o Pig com o HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="adffe-251">[Use Pig with HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="adffe-252">[Usar trabalhos do MapReduce com o HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="adffe-252">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[hdinsight-sdk-documentation]: http://msdnstage.redmond.corp.microsoft.com/library/dn479185.aspx

[azure-purchase-options]: http://azure.microsoft.com/pricing/purchase-options/
[azure-member-offers]: http://azure.microsoft.com/pricing/member-offers/
[azure-free-trial]: http://azure.microsoft.com/pricing/free-trial/

[apache-tez]: http://tez.apache.org
[apache-hive]: http://hive.apache.org/
[apache-log4j]: http://en.wikipedia.org/wiki/Log4j
[hive-on-tez-wiki]: https://cwiki.apache.org/confluence/display/Hive/Hive+on+Tez
[import-to-excel]: http://azure.microsoft.com/documentation/articles/hdinsight-connect-excel-power-query/
[hivetask]: http://msdn.microsoft.com/library/mt146771(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx

[hdinsight-use-pig]: hdinsight-use-pig.md
[hdinsight-use-oozie]: hdinsight-use-oozie.md
[hdinsight-analyze-flight-data]: hdinsight-analyze-flight-delay-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md


[hdinsight-storage]: hdinsight-hadoop-use-blob-storage.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-upload-data]: hdinsight-upload-data.md

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs
[powershell-here-strings]: http://technet.microsoft.com/library/ee692792.aspx


[cindygross-hive-tables]: http://blogs.msdn.com/b/cindygross/archive/2013/02/06/hdinsight-hive-internal-and-external-tables-intro.aspx
