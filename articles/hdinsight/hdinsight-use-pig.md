---
title: aaaUse Pig do Hadoop no HDInsight | Microsoft Docs
description: Saiba como toouse Pig com Hadoop no HDInsight.
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: acfeb52b-4b81-4a7d-af77-3e9908407404
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/15/2017
ms.author: larryfr
ms.openlocfilehash: 90850f2c742b8954c66ce277127e01b14fc3906f
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-pig-with-hadoop-on-hdinsight"></a><span data-ttu-id="73dfd-103">Usar o Pig com Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="73dfd-103">Use Pig with Hadoop on HDInsight</span></span>

<span data-ttu-id="73dfd-104">Saiba como toouse [Pig Apache](http://pig.apache.org/) com HDInsight...</span><span class="sxs-lookup"><span data-stu-id="73dfd-104">Learn how toouse [Apache Pig](http://pig.apache.org/) with HDInsight...</span></span>

<span data-ttu-id="73dfd-105">O Pig é uma plataforma para criar programas para o Hadoop usando uma linguagem de procedimento conhecida como *Pig Latin*.</span><span class="sxs-lookup"><span data-stu-id="73dfd-105">Pig is a platform for creating programs for Hadoop by using a procedural language known as *Pig Latin*.</span></span> <span data-ttu-id="73dfd-106">Pig é uma alternativa tooJava para a criação de *MapReduce* soluções e ele está incluído no Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="73dfd-106">Pig is an alternative tooJava for creating *MapReduce* solutions, and it is included with Azure HDInsight.</span></span> <span data-ttu-id="73dfd-107">Use Olá Olá toodiscover de tabela que Pig pode ser usado com HDInsight de várias maneiras a seguir:</span><span class="sxs-lookup"><span data-stu-id="73dfd-107">Use hello following table toodiscover hello various ways that Pig can be used with HDInsight:</span></span>

| <span data-ttu-id="73dfd-108">**Use** se quiser...</span><span class="sxs-lookup"><span data-stu-id="73dfd-108">**Use this** if you want...</span></span> | <span data-ttu-id="73dfd-109">...um shell **interativo**</span><span class="sxs-lookup"><span data-stu-id="73dfd-109">...an **interactive** shell</span></span> | <span data-ttu-id="73dfd-110">...Processamento em**lotes**</span><span class="sxs-lookup"><span data-stu-id="73dfd-110">...**batch** processing</span></span> | <span data-ttu-id="73dfd-111">... com esse **sistema operacional de cluster**</span><span class="sxs-lookup"><span data-stu-id="73dfd-111">...with this **cluster operating system**</span></span> | <span data-ttu-id="73dfd-112">... desse **sistema operacional cliente**</span><span class="sxs-lookup"><span data-stu-id="73dfd-112">...from this **client operating system**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="73dfd-113">SSH</span><span class="sxs-lookup"><span data-stu-id="73dfd-113">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="73dfd-114">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-114">✔</span></span> |<span data-ttu-id="73dfd-115">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-115">✔</span></span> |<span data-ttu-id="73dfd-116">Linux</span><span class="sxs-lookup"><span data-stu-id="73dfd-116">Linux</span></span> |<span data-ttu-id="73dfd-117">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-117">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="73dfd-118">API REST</span><span class="sxs-lookup"><span data-stu-id="73dfd-118">REST API</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="73dfd-119">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-119">✔</span></span> |<span data-ttu-id="73dfd-120">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-120">Linux or Windows</span></span> |<span data-ttu-id="73dfd-121">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-121">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="73dfd-122">SDK .NET para Hadoop</span><span class="sxs-lookup"><span data-stu-id="73dfd-122">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="73dfd-123">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-123">✔</span></span> |<span data-ttu-id="73dfd-124">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-124">Linux or Windows</span></span> |<span data-ttu-id="73dfd-125">Windows (por enquanto)</span><span class="sxs-lookup"><span data-stu-id="73dfd-125">Windows (for now)</span></span> |
| [<span data-ttu-id="73dfd-126">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="73dfd-126">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="73dfd-127">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-127">✔</span></span> |<span data-ttu-id="73dfd-128">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-128">Linux or Windows</span></span> |<span data-ttu-id="73dfd-129">Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-129">Windows</span></span> |
| <span data-ttu-id="73dfd-130">[Área de Trabalho Remota](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="73dfd-130">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="73dfd-131">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-131">✔</span></span> |<span data-ttu-id="73dfd-132">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-132">✔</span></span> |<span data-ttu-id="73dfd-133">Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-133">Windows</span></span> |<span data-ttu-id="73dfd-134">Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-134">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="73dfd-135">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="73dfd-135">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="73dfd-136">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="73dfd-136">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="73dfd-137"><a id="why"></a>Por que usar o Pig</span><span class="sxs-lookup"><span data-stu-id="73dfd-137"><a id="why"></a>Why use Pig</span></span>

<span data-ttu-id="73dfd-138">Um dos desafios de saudação do processamento de dados usando MapReduce no Hadoop implementa a lógica de processamento usando somente um mapa e uma função de redução.</span><span class="sxs-lookup"><span data-stu-id="73dfd-138">One of hello challenges of processing data by using MapReduce in Hadoop is implementing your processing logic by using only a map and a reduce function.</span></span> <span data-ttu-id="73dfd-139">Processamento complexo, você geralmente tem toobreak processamento em várias operações de MapReduce que são encadeados juntos tooachieve resultados de saudação desejado.</span><span class="sxs-lookup"><span data-stu-id="73dfd-139">For complex processing, you often have toobreak processing into multiple MapReduce operations that are chained together tooachieve hello desired result.</span></span>

<span data-ttu-id="73dfd-140">Pig permite que você toodefine processamento como uma série de transformações que Olá fluxos de dados por meio da saída do tooproduce Olá desejado.</span><span class="sxs-lookup"><span data-stu-id="73dfd-140">Pig allows you toodefine processing as a series of transformations that hello data flows through tooproduce hello desired output.</span></span>

<span data-ttu-id="73dfd-141">linguagem de Pig latino Olá permite que você toodescribe Olá fluxo de dados de entrada não processada, por meio de um ou mais transformações, saída de saudação desejada tooproduce.</span><span class="sxs-lookup"><span data-stu-id="73dfd-141">hello Pig Latin language allows you toodescribe hello data flow from raw input, through one or more transformations, tooproduce hello desired output.</span></span> <span data-ttu-id="73dfd-142">Os programas em Pig Latin seguem este padrão geral:</span><span class="sxs-lookup"><span data-stu-id="73dfd-142">Pig Latin programs follow this general pattern:</span></span>

* <span data-ttu-id="73dfd-143">**Carga**: ler dados toobe manipulado saudação do sistema de arquivos</span><span class="sxs-lookup"><span data-stu-id="73dfd-143">**Load**: Read data toobe manipulated from hello file system</span></span>

* <span data-ttu-id="73dfd-144">**Transformar**: manipular dados Olá</span><span class="sxs-lookup"><span data-stu-id="73dfd-144">**Transform**: Manipulate hello data</span></span>

* <span data-ttu-id="73dfd-145">**Despejar ou armazenar**: tela de toohello de dados de saída ou armazená-lo para processamento</span><span class="sxs-lookup"><span data-stu-id="73dfd-145">**Dump or store**: Output data toohello screen or store it for processing</span></span>

### <a name="user-defined-functions"></a><span data-ttu-id="73dfd-146">Funções definidas pelo usuário</span><span class="sxs-lookup"><span data-stu-id="73dfd-146">User-defined functions</span></span>

<span data-ttu-id="73dfd-147">Latino pig também oferece suporte a funções definidas pelo usuário (UDF), que permite que você tooinvoke componentes externos que implementam a lógica que é difícil toomodel em latim Pig.</span><span class="sxs-lookup"><span data-stu-id="73dfd-147">Pig Latin also supports user-defined functions (UDF), which allows you tooinvoke external components that implement logic that is difficult toomodel in Pig Latin.</span></span>

<span data-ttu-id="73dfd-148">Para saber mais sobre o Pig Latin, confira o [Manual de referência do Pig Latin 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) e o [Manual de referência do Pig Latin 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span><span class="sxs-lookup"><span data-stu-id="73dfd-148">For more information about Pig Latin, see [Pig Latin Reference Manual 1](http://pig.apache.org/docs/r0.7.0/piglatin_ref1.html) and [Pig Latin Reference Manual 2](http://pig.apache.org/docs/r0.7.0/piglatin_ref2.html).</span></span>

<span data-ttu-id="73dfd-149">Para obter um exemplo do uso de UDFs com Pig, consulte Olá documentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="73dfd-149">For an example of using UDFs with Pig, see hello following documents:</span></span>

* <span data-ttu-id="73dfd-150">[DataFu de uso com Pig no HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) -DataFu é uma coleção de útil UDFs mantida pela Apache</span><span class="sxs-lookup"><span data-stu-id="73dfd-150">[Use DataFu with Pig in HDInsight](hdinsight-hadoop-use-pig-datafu-udf.md) - DataFu is a collection of useful UDFs maintained by Apache</span></span>
* [<span data-ttu-id="73dfd-151">Use o Python com o Pig e o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="73dfd-151">Use Python with Pig and Hive in HDInsight</span></span>](hdinsight-python.md)
* [<span data-ttu-id="73dfd-152">Use o C# com o Hive e com o Pig no HDInsight</span><span class="sxs-lookup"><span data-stu-id="73dfd-152">Use C# with Hive and Pig in HDInsight</span></span>](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md)

## <span data-ttu-id="73dfd-153"><a id="data"></a>Dados de exemplo</span><span class="sxs-lookup"><span data-stu-id="73dfd-153"><a id="data"></a>Example data</span></span>

<span data-ttu-id="73dfd-154">HDInsight fornece vários conjuntos de dados de exemplo, que são armazenados em Olá `/example/data` e `/HdiSamples` diretórios.</span><span class="sxs-lookup"><span data-stu-id="73dfd-154">HDInsight provides various example data sets, which are stored in hello `/example/data` and `/HdiSamples` directories.</span></span> <span data-ttu-id="73dfd-155">São esses diretórios no armazenamento padrão da saudação para seu cluster.</span><span class="sxs-lookup"><span data-stu-id="73dfd-155">These directories are in hello default storage for your cluster.</span></span> <span data-ttu-id="73dfd-156">exemplo de Pig Hello neste documento usa Olá *log4j* arquivo `/example/data/sample.log`.</span><span class="sxs-lookup"><span data-stu-id="73dfd-156">hello Pig example in this document uses hello *log4j* file from `/example/data/sample.log`.</span></span>

<span data-ttu-id="73dfd-157">Cada log no arquivo hello consiste em uma linha de campos que contém um `[LOG LEVEL]` campo tooshow Olá tipo e hello gravidade, por exemplo:</span><span class="sxs-lookup"><span data-stu-id="73dfd-157">Each log inside hello file consists of a line of fields that contains a `[LOG LEVEL]` field tooshow hello type and hello severity, for example:</span></span>

    2012-02-03 20:26:41 SampleClass3 [ERROR] verbose detail for id 1527353937

<span data-ttu-id="73dfd-158">No exemplo anterior de saudação, o nível de log de saudação é erro.</span><span class="sxs-lookup"><span data-stu-id="73dfd-158">In hello previous example, hello log level is ERROR.</span></span>

> [!NOTE]
> <span data-ttu-id="73dfd-159">Você também pode gerar um arquivo log4j usando Olá [Log4j Apache](http://en.wikipedia.org/wiki/Log4j) ferramenta de registro em log e, em seguida, carregar blob tooyour arquivo.</span><span class="sxs-lookup"><span data-stu-id="73dfd-159">You can also generate a log4j file by using hello [Apache Log4j](http://en.wikipedia.org/wiki/Log4j) logging tool and then upload that file tooyour blob.</span></span> <span data-ttu-id="73dfd-160">Consulte [tooHDInsight carregar dados](hdinsight-upload-data.md) para obter instruções.</span><span class="sxs-lookup"><span data-stu-id="73dfd-160">See [Upload Data tooHDInsight](hdinsight-upload-data.md) for instructions.</span></span> <span data-ttu-id="73dfd-161">Para saber mais sobre como o armazenamento de blob do Azure é usado com o HDInsight, confira [Usar armazenamento de blob do Azure com o HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="73dfd-161">For more information about how blobs in Azure storage are used with HDInsight, see [Use Azure Blob Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>

## <span data-ttu-id="73dfd-162"><a id="job"></a>Exemplo de trabalho</span><span class="sxs-lookup"><span data-stu-id="73dfd-162"><a id="job"></a>Example job</span></span>

<span data-ttu-id="73dfd-163">próximo trabalho de Pig latino Hello carrega Olá `sample.log` arquivo de armazenamento padrão da saudação para seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="73dfd-163">hello following Pig Latin job loads hello `sample.log` file from hello default storage for your HDInsight cluster.</span></span> <span data-ttu-id="73dfd-164">Em seguida, ele executa uma série de transformações que resultam em uma contagem de como quantas vezes cada dados de entrada de saudação ocorreu no nível de log.</span><span class="sxs-lookup"><span data-stu-id="73dfd-164">Then it performs a series of transformations that result in a count of how many times each log level occurred in hello input data.</span></span> <span data-ttu-id="73dfd-165">resultados de saudação são gravados tooSTDOUT.</span><span class="sxs-lookup"><span data-stu-id="73dfd-165">hello results are written tooSTDOUT.</span></span>

    LOGS = LOAD 'wasb:///example/data/sample.log';
    LEVELS = foreach LOGS generate REGEX_EXTRACT($0, '(TRACE|DEBUG|INFO|WARN|ERROR|FATAL)', 1)  as LOGLEVEL;
    FILTEREDLEVELS = FILTER LEVELS by LOGLEVEL is not null;
    GROUPEDLEVELS = GROUP FILTEREDLEVELS by LOGLEVEL;
    FREQUENCIES = foreach GROUPEDLEVELS generate group as LOGLEVEL, COUNT(FILTEREDLEVELS.LOGLEVEL) as COUNT;
    RESULT = order FREQUENCIES by COUNT desc;
    DUMP RESULT;

<span data-ttu-id="73dfd-166">Olá imagem a seguir mostra um resumo do que cada transformação faz toohello dados.</span><span class="sxs-lookup"><span data-stu-id="73dfd-166">hello following image shows a summary of what each transformation does toohello data.</span></span>

![Representação gráfica de transformações Olá][image-hdi-pig-data-transformation]

## <span data-ttu-id="73dfd-168"><a id="run"></a>Executar trabalho de Pig latino Olá</span><span class="sxs-lookup"><span data-stu-id="73dfd-168"><a id="run"></a>Run hello Pig Latin job</span></span>

<span data-ttu-id="73dfd-169">O HDInsight pode executar trabalhos de Pig Latin usando vários métodos.</span><span class="sxs-lookup"><span data-stu-id="73dfd-169">HDInsight can run Pig Latin jobs by using a variety of methods.</span></span> <span data-ttu-id="73dfd-170">Usar o hello toodecide tabela qual método é ideal para você a seguir, siga o link Olá para obter uma explicação.</span><span class="sxs-lookup"><span data-stu-id="73dfd-170">Use hello following table toodecide which method is right for you, then follow hello link for a walkthrough.</span></span>

| <span data-ttu-id="73dfd-171">**Use** se quiser...</span><span class="sxs-lookup"><span data-stu-id="73dfd-171">**Use this** if you want...</span></span> | <span data-ttu-id="73dfd-172">...um shell **interativo**</span><span class="sxs-lookup"><span data-stu-id="73dfd-172">...an **interactive** shell</span></span> | <span data-ttu-id="73dfd-173">...Processamento em**lotes**</span><span class="sxs-lookup"><span data-stu-id="73dfd-173">...**batch** processing</span></span> | <span data-ttu-id="73dfd-174">... com esse **sistema operacional de cluster**</span><span class="sxs-lookup"><span data-stu-id="73dfd-174">...with this **cluster operating system**</span></span> | <span data-ttu-id="73dfd-175">... deste **cliente**</span><span class="sxs-lookup"><span data-stu-id="73dfd-175">...from this **client**</span></span> |
|:--- |:---:|:---:|:--- |:--- |
| [<span data-ttu-id="73dfd-176">SSH</span><span class="sxs-lookup"><span data-stu-id="73dfd-176">SSH</span></span>](hdinsight-hadoop-use-pig-ssh.md) |<span data-ttu-id="73dfd-177">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-177">✔</span></span> |<span data-ttu-id="73dfd-178">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-178">✔</span></span> |<span data-ttu-id="73dfd-179">Linux</span><span class="sxs-lookup"><span data-stu-id="73dfd-179">Linux</span></span> |<span data-ttu-id="73dfd-180">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-180">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="73dfd-181">Curl</span><span class="sxs-lookup"><span data-stu-id="73dfd-181">Curl</span></span>](hdinsight-hadoop-use-pig-curl.md) |&nbsp; |<span data-ttu-id="73dfd-182">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-182">✔</span></span> |<span data-ttu-id="73dfd-183">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-183">Linux or Windows</span></span> |<span data-ttu-id="73dfd-184">Linux, Unix, Mac OS X ou Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-184">Linux, Unix, Mac OS X, or Windows</span></span> |
| [<span data-ttu-id="73dfd-185">SDK .NET para Hadoop</span><span class="sxs-lookup"><span data-stu-id="73dfd-185">.NET SDK for Hadoop</span></span>](hdinsight-hadoop-use-pig-dotnet-sdk.md) |&nbsp; |<span data-ttu-id="73dfd-186">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-186">✔</span></span> |<span data-ttu-id="73dfd-187">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-187">Linux or Windows</span></span> |<span data-ttu-id="73dfd-188">Windows (por enquanto)</span><span class="sxs-lookup"><span data-stu-id="73dfd-188">Windows (for now)</span></span> |
| [<span data-ttu-id="73dfd-189">Windows PowerShell</span><span class="sxs-lookup"><span data-stu-id="73dfd-189">Windows PowerShell</span></span>](hdinsight-hadoop-use-pig-powershell.md) |&nbsp; |<span data-ttu-id="73dfd-190">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-190">✔</span></span> |<span data-ttu-id="73dfd-191">Linux ou Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-191">Linux or Windows</span></span> |<span data-ttu-id="73dfd-192">Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-192">Windows</span></span> |
| <span data-ttu-id="73dfd-193">[Área de Trabalho Remota](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 e 3.3)</span><span class="sxs-lookup"><span data-stu-id="73dfd-193">[Remote Desktop](hdinsight-hadoop-use-pig-remote-desktop.md) (HDInsight 3.2 and 3.3)</span></span> |<span data-ttu-id="73dfd-194">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-194">✔</span></span> |<span data-ttu-id="73dfd-195">✔</span><span class="sxs-lookup"><span data-stu-id="73dfd-195">✔</span></span> |<span data-ttu-id="73dfd-196">Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-196">Windows</span></span> |<span data-ttu-id="73dfd-197">Windows</span><span class="sxs-lookup"><span data-stu-id="73dfd-197">Windows</span></span> |

> [!IMPORTANT]
> <span data-ttu-id="73dfd-198">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="73dfd-198">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="73dfd-199">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="73dfd-199">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <a name="pig-and-sql-server-integration-services"></a><span data-ttu-id="73dfd-200">Pig e SQL Server Integration Services</span><span class="sxs-lookup"><span data-stu-id="73dfd-200">Pig and SQL Server Integration Services</span></span>

<span data-ttu-id="73dfd-201">Você pode usar o SQL Server Integration Services (SSIS) toorun um trabalho de Pig.</span><span class="sxs-lookup"><span data-stu-id="73dfd-201">You can use SQL Server Integration Services (SSIS) toorun a Pig job.</span></span> <span data-ttu-id="73dfd-202">Hello Azure Feature Pack para SSIS fornece Olá componentes que funcionam com os trabalhos de Pig no HDInsight a seguir.</span><span class="sxs-lookup"><span data-stu-id="73dfd-202">hello Azure Feature Pack for SSIS provides hello following components that work with Pig jobs on HDInsight.</span></span>

* <span data-ttu-id="73dfd-203">[Tarefa do Pig do Azure HDInsight][pigtask]</span><span class="sxs-lookup"><span data-stu-id="73dfd-203">[Azure HDInsight Pig Task][pigtask]</span></span>

* <span data-ttu-id="73dfd-204">[Gerenciador de Conexões de Assinatura do Azure][connectionmanager]</span><span class="sxs-lookup"><span data-stu-id="73dfd-204">[Azure Subscription Connection Manager][connectionmanager]</span></span>

<span data-ttu-id="73dfd-205">Saiba mais sobre hello Azure Feature Pack para SSIS [aqui][ssispack].</span><span class="sxs-lookup"><span data-stu-id="73dfd-205">Learn more about hello Azure Feature Pack for SSIS [here][ssispack].</span></span>

## <span data-ttu-id="73dfd-206"><a id="nextsteps"></a>Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="73dfd-206"><a id="nextsteps"></a>Next steps</span></span>
<span data-ttu-id="73dfd-207">Agora que você aprendeu como toouse Pig com HDInsight, Olá uso a seguir vincula tooexplore toowork outras formas ao HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="73dfd-207">Now that you have learned how toouse Pig with HDInsight, use hello following links tooexplore other ways toowork with Azure HDInsight.</span></span>

* <span data-ttu-id="73dfd-208">[Carregar dados tooHDInsight][hdinsight-upload-data]</span><span class="sxs-lookup"><span data-stu-id="73dfd-208">[Upload data tooHDInsight][hdinsight-upload-data]</span></span>
* <span data-ttu-id="73dfd-209">[Usar o Hive com o HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="73dfd-209">[Use Hive with HDInsight][hdinsight-use-hive]</span></span>
* [<span data-ttu-id="73dfd-210">Use o Sqoop com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="73dfd-210">Use Sqoop with HDInsight</span></span>](hdinsight-use-sqoop.md)
* [<span data-ttu-id="73dfd-211">Usar o Oozie com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="73dfd-211">Use Oozie with HDInsight</span></span>](hdinsight-use-oozie.md)
* <span data-ttu-id="73dfd-212">[Usar trabalhos do MapReduce com o HDInsight][hdinsight-use-mapreduce]</span><span class="sxs-lookup"><span data-stu-id="73dfd-212">[Use MapReduce jobs with HDInsight][hdinsight-use-mapreduce]</span></span>

[apachepig-home]: http://pig.apache.org/
[putty]: http://www.chiark.greenend.org.uk/~sgtatham/putty/download.html
[curl]: http://curl.haxx.se/
[pigtask]: http://msdn.microsoft.com/library/mt146781(v=sql.120).aspx
[connectionmanager]: http://msdn.microsoft.com/library/mt146773(v=sql.120).aspx
[ssispack]: http://msdn.microsoft.com/library/mt146770(v=sql.120).aspx


[hdinsight-upload-data]: hdinsight-upload-data.md

[hdinsight-admin-powershell]: hdinsight-administer-use-powershell.md

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md

[hdinsight-provision]: hdinsight-hadoop-provision-linux-clusters.md
[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md#mapreduce-sdk

[Powershell-install-configure]: /powershell/azureps-cmdlets-docs

[powershell-start]: http://technet.microsoft.com/library/hh847889.aspx


[image-hdi-pig-data-transformation]: ./media/hdinsight-use-pig/HDI.DataTransformation.gif
