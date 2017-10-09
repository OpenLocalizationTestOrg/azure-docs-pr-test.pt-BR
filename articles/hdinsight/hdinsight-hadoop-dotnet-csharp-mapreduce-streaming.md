---
title: aaaUse c# com MapReduce no Hadoop no HDInsight - Azure | Microsoft Docs
description: "Saiba como toouse c# toocreate MapReduce soluções com Hadoop no HDInsight do Azure."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: d83def76-12ad-4538-bb8e-3ba3542b7211
ms.custom: hdinsightactive
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: dotnet
ms.topic: article
ms.date: 07/12/2017
ms.author: larryfr
ms.openlocfilehash: dd8b684e74155bc1a37d4ab8d6f9033276ef5aa3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="b7410-103">Use C# com streaming de MapReduce no Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7410-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="b7410-104">Saiba como toouse c# toocreate uma solução de MapReduce no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b7410-104">Learn how toouse C# toocreate a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="b7410-105">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="b7410-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="b7410-106">Para obter mais informações, consulte [Controle de versão do componente do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b7410-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="b7410-107">Transmissão do Hadoop é um utilitário que permite que os trabalhos de MapReduce toorun usando um script ou executável.</span><span class="sxs-lookup"><span data-stu-id="b7410-107">Hadoop streaming is a utility that allows you toorun MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="b7410-108">Neste exemplo, o .NET é usado tooimplement Olá mapeador e Redutor para uma solução de contagem de palavras.</span><span class="sxs-lookup"><span data-stu-id="b7410-108">In this example, .NET is used tooimplement hello mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="b7410-109">.NET no HDInsight</span><span class="sxs-lookup"><span data-stu-id="b7410-109">.NET on HDInsight</span></span>

<span data-ttu-id="b7410-110">__HDInsight baseados em Linux__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun aplicativos de .NET.</span><span class="sxs-lookup"><span data-stu-id="b7410-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) toorun .NET applications.</span></span> <span data-ttu-id="b7410-111">O Mono versão 4.2.1 está incluído no HDInsight versão 3.5.</span><span class="sxs-lookup"><span data-stu-id="b7410-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="b7410-112">Para obter mais informações sobre a versão de saudação do Mono incluído no HDInsight, consulte [versões de componente do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="b7410-112">For more information on hello version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="b7410-113">toouse uma versão específica do Mono, consulte Olá [instalação ou atualização Mono](hdinsight-hadoop-install-mono.md) documento.</span><span class="sxs-lookup"><span data-stu-id="b7410-113">toouse a specific version of Mono, see hello [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="b7410-114">Para obter mais informações sobre compatibilidade de Mono com versões do .NET Framework, consulte [Compatibilidade de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="b7410-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="b7410-115">Como funciona o Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="b7410-115">How Hadoop streaming works</span></span>

<span data-ttu-id="b7410-116">Olá basic processo usado para streaming neste documento é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="b7410-116">hello basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="b7410-117">Hadoop passa STDIN mapeador de dados de toohello (mapper.exe neste exemplo).</span><span class="sxs-lookup"><span data-stu-id="b7410-117">Hadoop passes data toohello mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="b7410-118">Mapeador de saudação processa dados hello e emite tooSTDOUT de pares chave/valor delimitado por tabulação.</span><span class="sxs-lookup"><span data-stu-id="b7410-118">hello mapper processes hello data, and emits tab-delimited key/value pairs tooSTDOUT.</span></span>
3. <span data-ttu-id="b7410-119">saída de Hello é lido pelo Hadoop e encaminhada toohello Redutor (reducer.exe neste exemplo) STDIN.</span><span class="sxs-lookup"><span data-stu-id="b7410-119">hello output is read by Hadoop, and then passed toohello reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="b7410-120">Redutor Olá lê pares de chave/valor Olá delimitado por tabulação, processa dados hello e, em seguida, emite resultados hello como pares de chave/valor delimitado por tabulação em STDOUT.</span><span class="sxs-lookup"><span data-stu-id="b7410-120">hello reducer reads hello tab-delimited key/value pairs, processes hello data, and then emits hello result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="b7410-121">saída de Hello lidos por Hadoop e gravada toohello diretório de saída.</span><span class="sxs-lookup"><span data-stu-id="b7410-121">hello output is read by Hadoop and written toohello output directory.</span></span>

<span data-ttu-id="b7410-122">Para obter mais informações sobre streaming, consulte [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="b7410-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b7410-123">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="b7410-123">Prerequisites</span></span>

* <span data-ttu-id="b7410-124">Familiaridade com gravação e compilação de código em C# que se destina ao .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="b7410-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="b7410-125">Olá as etapas neste documento utilizarem 2017 do Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b7410-125">hello steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="b7410-126">Uma maneira tooupload .exe arquivos toohello cluster.</span><span class="sxs-lookup"><span data-stu-id="b7410-126">A way tooupload .exe files toohello cluster.</span></span> <span data-ttu-id="b7410-127">Olá etapas deste documento usam Olá Data Lake Tools para Visual Studio tooupload Olá arquivos tooprimary armazenamento Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="b7410-127">hello steps in this document use hello Data Lake Tools for Visual Studio tooupload hello files tooprimary storage for hello cluster.</span></span>

* <span data-ttu-id="b7410-128">Azure PowerShell ou um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="b7410-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="b7410-129">Um Hadoop no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="b7410-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="b7410-130">Para obter mais informações sobre como criar um cluster, consulte [Criar um cluster do HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="b7410-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-hello-mapper"></a><span data-ttu-id="b7410-131">Criar mapeador Olá</span><span class="sxs-lookup"><span data-stu-id="b7410-131">Create hello mapper</span></span>

<span data-ttu-id="b7410-132">No Visual Studio, crie um novo __aplicativo de console__ chamado __mapeador__.</span><span class="sxs-lookup"><span data-stu-id="b7410-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="b7410-133">Use Olá código para o aplicativo hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7410-133">Use hello following code for hello application:</span></span>

```csharp
using System;
using System.Text.RegularExpressions;

namespace mapper
{
    class Program
    {
        static void Main(string[] args)
        {
            string line;
            //Hadoop passes data toohello mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over hello words
                foreach(var word in words)
                {
                    //Emit tab-delimited key/value pairs.
                    //In this case, a word and a count of 1.
                    Console.WriteLine("{0}\t1",word);
                }
            }
        }
    }
}
```

<span data-ttu-id="b7410-134">Depois de criar o aplicativo hello, compile-Olá tooproduce `/bin/Debug/mapper.exe` arquivo no diretório de projeto hello.</span><span class="sxs-lookup"><span data-stu-id="b7410-134">After creating hello application, build it tooproduce hello `/bin/Debug/mapper.exe` file in hello project directory.</span></span>

## <a name="create-hello-reducer"></a><span data-ttu-id="b7410-135">Criar Redutor Olá</span><span class="sxs-lookup"><span data-stu-id="b7410-135">Create hello reducer</span></span>

<span data-ttu-id="b7410-136">No Visual Studio, crie um novo __Aplicativo de console__ chamado __redutor__.</span><span class="sxs-lookup"><span data-stu-id="b7410-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="b7410-137">Use Olá código para o aplicativo hello a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7410-137">Use hello following code for hello application:</span></span>

```csharp
using System;
using System.Collections.Generic;

namespace reducer
{
    class Program
    {
        static void Main(string[] args)
        {
            //Dictionary for holding a count of words
            Dictionary<string, int> words = new Dictionary<string, int>();

            string line;
            //Read from STDIN
            while ((line = Console.ReadLine()) != null)
            {
                // Data from Hadoop is tab-delimited key/value pairs
                var sArr = line.Split('\t');
                // Get hello word
                string word = sArr[0];
                // Get hello count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for hello word?
                if(words.ContainsKey(word))
                {
                    //If so, increment hello count
                    words[word] += count;
                } else
                {
                    //Add hello key toohello collection
                    words.Add(word, count);
                }
            }
            //Finally, emit each word and count
            foreach (var word in words)
            {
                //Emit tab-delimited key/value pairs.
                //In this case, a word and a count of 1.
                Console.WriteLine("{0}\t{1}", word.Key, word.Value);
            }
        }
    }
}
```

<span data-ttu-id="b7410-138">Depois de criar o aplicativo hello, compile-Olá tooproduce `/bin/Debug/reducer.exe` arquivo no diretório de projeto hello.</span><span class="sxs-lookup"><span data-stu-id="b7410-138">After creating hello application, build it tooproduce hello `/bin/Debug/reducer.exe` file in hello project directory.</span></span>

## <a name="upload-toostorage"></a><span data-ttu-id="b7410-139">Carregar toostorage</span><span class="sxs-lookup"><span data-stu-id="b7410-139">Upload toostorage</span></span>

1. <span data-ttu-id="b7410-140">No Visual Studio, abra **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="b7410-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="b7410-141">Expanda **Azure** e expanda **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="b7410-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="b7410-142">Se solicitado, insira suas credenciais de assinatura do Azure e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="b7410-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="b7410-143">Expanda o cluster de HDInsight de saudação que você deseja toodeploy este aplicativo.</span><span class="sxs-lookup"><span data-stu-id="b7410-143">Expand hello HDInsight cluster that you wish toodeploy this application to.</span></span> <span data-ttu-id="b7410-144">Uma entrada com o texto de saudação __(conta de armazenamento padrão)__ está listado.</span><span class="sxs-lookup"><span data-stu-id="b7410-144">An entry with hello text __(Default Storage Account)__ is listed.</span></span>

    ![Mostrando conta de armazenamento Olá para cluster de saudação do Gerenciador de servidores](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="b7410-146">Se essa entrada pode ser expandida, você está usando um __conta de armazenamento do Azure__ como armazenamento padrão para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7410-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for hello cluster.</span></span> <span data-ttu-id="b7410-147">arquivos de saudação tooview no armazenamento padrão da saudação para cluster hello, expanda a entrada hello e clique duas vezes Olá __(contêiner padrão)__.</span><span class="sxs-lookup"><span data-stu-id="b7410-147">tooview hello files on hello default storage for hello cluster, expand hello entry and then double-click hello __(Default Container)__.</span></span>

    * <span data-ttu-id="b7410-148">Se essa entrada não pode ser expandida, você está usando __repositório Azure Data Lake__ como armazenamento de padrão de saudação para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="b7410-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as hello default storage for hello cluster.</span></span> <span data-ttu-id="b7410-149">arquivos de saudação tooview no armazenamento padrão da saudação para cluster hello, clique duas vezes em Olá __(conta de armazenamento padrão)__ entrada.</span><span class="sxs-lookup"><span data-stu-id="b7410-149">tooview hello files on hello default storage for hello cluster, double-click hello __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="b7410-150">arquivos de .exe do tooupload Olá, use um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="b7410-150">tooupload hello .exe files, use one of hello following methods:</span></span>

    * <span data-ttu-id="b7410-151">Se usar um __conta de armazenamento do Azure__, clique ícone de carregamento Olá e, em seguida, procure toohello **bin\debug** pasta Olá **mapeador** projeto.</span><span class="sxs-lookup"><span data-stu-id="b7410-151">If using an __Azure Storage Account__, click hello upload icon, and then browse toohello **bin\debug** folder for hello **mapper** project.</span></span> <span data-ttu-id="b7410-152">Por fim, selecione Olá **mapper.exe** de arquivo e clique em **Okey**.</span><span class="sxs-lookup"><span data-stu-id="b7410-152">Finally, select hello **mapper.exe** file and click **Ok**.</span></span>

        ![ícone de carregamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="b7410-154">Se usar __repositório Azure Data Lake__, uma área vazia na listagem de arquivo hello e, em seguida, selecione __carregar__.</span><span class="sxs-lookup"><span data-stu-id="b7410-154">If using __Azure Data Lake Store__, right-click an empty area in hello file listing, and then select __Upload__.</span></span> <span data-ttu-id="b7410-155">Por fim, selecione Olá **mapper.exe** de arquivo e clique em **abrir**.</span><span class="sxs-lookup"><span data-stu-id="b7410-155">Finally, select hello **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="b7410-156">Uma vez Olá __mapper.exe__ carregamento for concluída, o processo de carregamento de repetição Olá para Olá __reducer.exe__ arquivo.</span><span class="sxs-lookup"><span data-stu-id="b7410-156">Once hello __mapper.exe__ upload has finished, repeat hello upload process for hello __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="b7410-157">Executar um trabalho: usando uma sessão SSH</span><span class="sxs-lookup"><span data-stu-id="b7410-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="b7410-158">Use SSH tooconnect toohello HDInsight cluster.</span><span class="sxs-lookup"><span data-stu-id="b7410-158">Use SSH tooconnect toohello HDInsight cluster.</span></span> <span data-ttu-id="b7410-159">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="b7410-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="b7410-160">Use uma saudação trabalho MapReduce do comando toostart Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7410-160">Use one of hello following command toostart hello MapReduce job:</span></span>

    * <span data-ttu-id="b7410-161">Se estiver usando o __Data Lake Store__ como armazenamento padrão:</span><span class="sxs-lookup"><span data-stu-id="b7410-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="b7410-162">Se estiver usando o __Armazenamento do Azure__ como armazenamento padrão:</span><span class="sxs-lookup"><span data-stu-id="b7410-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="b7410-163">Olá lista a seguir descreve o que faz cada parâmetro:</span><span class="sxs-lookup"><span data-stu-id="b7410-163">hello following list describes what each parameter does:</span></span>

    * <span data-ttu-id="b7410-164">`hadoop-streaming.jar`: arquivo jar Olá que contém Olá MapReduce funcionalidade de streaming.</span><span class="sxs-lookup"><span data-stu-id="b7410-164">`hadoop-streaming.jar`: hello jar file that contains hello streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="b7410-165">`-files`: Adiciona Olá `mapper.exe` e `reducer.exe` trabalho toothis de arquivos.</span><span class="sxs-lookup"><span data-stu-id="b7410-165">`-files`: Adds hello `mapper.exe` and `reducer.exe` files toothis job.</span></span> <span data-ttu-id="b7410-166">Olá `adl:///` ou `wasb:///` antes de cada arquivo é toohello raiz do caminho do hello de armazenamento padrão para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7410-166">hello `adl:///` or `wasb:///` before each file is hello path toohello root of default storage for hello cluster.</span></span>
    * <span data-ttu-id="b7410-167">`-mapper`: Especifica qual arquivo implementa mapeador de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7410-167">`-mapper`: Specifies which file implements hello mapper.</span></span>
    * <span data-ttu-id="b7410-168">`-reducer`: Especifica qual arquivo implementa Redutor hello.</span><span class="sxs-lookup"><span data-stu-id="b7410-168">`-reducer`: Specifies which file implements hello reducer.</span></span>
    * <span data-ttu-id="b7410-169">`-input`: dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="b7410-169">`-input`: hello input data.</span></span>
    * <span data-ttu-id="b7410-170">`-output`: diretório de saída de hello.</span><span class="sxs-lookup"><span data-stu-id="b7410-170">`-output`: hello output directory.</span></span>

3. <span data-ttu-id="b7410-171">Após a conclusão do trabalho de MapReduce hello, use Olá resultados de saudação tooview a seguir:</span><span class="sxs-lookup"><span data-stu-id="b7410-171">Once hello MapReduce job completes, use hello following tooview hello results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="b7410-172">Olá, texto a seguir é um exemplo de dados de saudação retornados por este comando:</span><span class="sxs-lookup"><span data-stu-id="b7410-172">hello following text is an example of hello data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="b7410-173">Executar um trabalho: usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="b7410-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="b7410-174">Usar Olá toorun de script do PowerShell um trabalho MapReduce a seguir e baixar os resultados de saudação.</span><span class="sxs-lookup"><span data-stu-id="b7410-174">Use hello following PowerShell script toorun a MapReduce job and download hello results.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]

<span data-ttu-id="b7410-175">Esse script solicita nome de conta de logon de cluster hello e a senha, juntamente com o nome do cluster HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="b7410-175">This script prompts you for hello cluster login account name and password, along with hello HDInsight cluster name.</span></span> <span data-ttu-id="b7410-176">Após a conclusão do trabalho hello, saída de hello é baixado toohello `output.txt` arquivo no script de saudação do diretório Olá é executado de.</span><span class="sxs-lookup"><span data-stu-id="b7410-176">Once hello job completes, hello output is downloaded toohello `output.txt` file in hello directory hello script is ran from.</span></span> <span data-ttu-id="b7410-177">Olá, texto a seguir é um exemplo de dados Olá Olá `output.txt` arquivo:</span><span class="sxs-lookup"><span data-stu-id="b7410-177">hello following text is an example of hello data in hello `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="b7410-178">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="b7410-178">Next steps</span></span>

<span data-ttu-id="b7410-179">Para obter mais informações sobre como usar o MapReduce com HDInsight, veja [Usar MapReduce com HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="b7410-179">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="b7410-180">Para obter informações sobre como usar C# com Hive e Pig, consulte [Usar uma função C# definida pelo usuário com Hive e Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="b7410-180">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="b7410-181">Para obter informações sobre como usar C# com Storm no HDInsight, consulte [Desenvolver topologias C# para Storm no HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="b7410-181">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>