---
title: "Usar C# com MapReduce no Hadoop no HDInsight – Azure | Microsoft Docs"
description: "Saiba como usar C# para criar soluções de MapReduce com Hadoop no Azure HDInsight."
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
ms.openlocfilehash: adb454e56378a800c671614735aec78b6851aeb2
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="use-c-with-mapreduce-streaming-on-hadoop-in-hdinsight"></a><span data-ttu-id="80ee4-103">Use C# com streaming de MapReduce no Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="80ee4-103">Use C# with MapReduce streaming on Hadoop in HDInsight</span></span>

<span data-ttu-id="80ee4-104">Saiba como usar C# para criar uma solução de MapReduce no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80ee4-104">Learn how to use C# to create a MapReduce solution on HDInsight.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="80ee4-105">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="80ee4-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="80ee4-106">Para obter mais informações, consulte [Controle de versão do componente do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="80ee4-106">For more information, see [HDInsight component versioning](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="80ee4-107">Hadoop Streaming é um utilitário que permite que você execute trabalhos MapReduce usando um script ou executável.</span><span class="sxs-lookup"><span data-stu-id="80ee4-107">Hadoop streaming is a utility that allows you to run MapReduce jobs using a script or executable.</span></span> <span data-ttu-id="80ee4-108">Neste exemplo, o .NET é usado para implementar o mapeador e Redutor de uma solução de contagem de palavras.</span><span class="sxs-lookup"><span data-stu-id="80ee4-108">In this example, .NET is used to implement the mapper and reducer for a word count solution.</span></span>

## <a name="net-on-hdinsight"></a><span data-ttu-id="80ee4-109">.NET no HDInsight</span><span class="sxs-lookup"><span data-stu-id="80ee4-109">.NET on HDInsight</span></span>

<span data-ttu-id="80ee4-110">Clusters do __HDInsight baseado em Linux__ usam [Mono (https://mono-project.com)](https://mono-project.com) para executar aplicativos .NET.</span><span class="sxs-lookup"><span data-stu-id="80ee4-110">__Linux-based HDInsight__ clusters use [Mono (https://mono-project.com)](https://mono-project.com) to run .NET applications.</span></span> <span data-ttu-id="80ee4-111">O Mono versão 4.2.1 está incluído no HDInsight versão 3.5.</span><span class="sxs-lookup"><span data-stu-id="80ee4-111">Mono version 4.2.1 is included with HDInsight version 3.5.</span></span> <span data-ttu-id="80ee4-112">Para obter mais informações sobre a versão de Mono incluída com o HDInsight, consulte [Versão de componente do HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="80ee4-112">For more information on the version of Mono included with HDInsight, see [HDInsight component versions](hdinsight-component-versioning.md).</span></span> <span data-ttu-id="80ee4-113">Para usar uma versão específica do Mono, consulte o documento [Instalar ou atualizar](hdinsight-hadoop-install-mono.md).</span><span class="sxs-lookup"><span data-stu-id="80ee4-113">To use a specific version of Mono, see the [Install or update Mono](hdinsight-hadoop-install-mono.md) document.</span></span>

<span data-ttu-id="80ee4-114">Para obter mais informações sobre compatibilidade de Mono com versões do .NET Framework, consulte [Compatibilidade de Mono](http://www.mono-project.com/docs/about-mono/compatibility/).</span><span class="sxs-lookup"><span data-stu-id="80ee4-114">For more information on Mono compatibility with .NET Framework versions, see [Mono compatibility](http://www.mono-project.com/docs/about-mono/compatibility/).</span></span>

## <a name="how-hadoop-streaming-works"></a><span data-ttu-id="80ee4-115">Como funciona o Hadoop Streaming</span><span class="sxs-lookup"><span data-stu-id="80ee4-115">How Hadoop streaming works</span></span>

<span data-ttu-id="80ee4-116">O processo básico usado para streaming neste documento é o seguinte:</span><span class="sxs-lookup"><span data-stu-id="80ee4-116">The basic process used for streaming in this document is as follows:</span></span>

1. <span data-ttu-id="80ee4-117">O Hadoop passa dados para o mapeador (mapper.exe neste exemplo) no STDIN.</span><span class="sxs-lookup"><span data-stu-id="80ee4-117">Hadoop passes data to the mapper (mapper.exe in this example) on STDIN.</span></span>
2. <span data-ttu-id="80ee4-118">O mapeador processa os dados e emite pares de chave/valor delimitados por tabulação para STDOUT.</span><span class="sxs-lookup"><span data-stu-id="80ee4-118">The mapper processes the data, and emits tab-delimited key/value pairs to STDOUT.</span></span>
3. <span data-ttu-id="80ee4-119">A saída é lida pelo Hadoop e, em seguida, passada para o redutor (reducer.exe neste exemplo) no STDIN.</span><span class="sxs-lookup"><span data-stu-id="80ee4-119">The output is read by Hadoop, and then passed to the reducer (reducer.exe in this example) on STDIN.</span></span>
4. <span data-ttu-id="80ee4-120">O redutor lê os pares de chave/valor delimitados por tabulação, processa os dados e, em seguida, emite o resultado como pares de chave/valor delimitados por tabulação no STDOUT.</span><span class="sxs-lookup"><span data-stu-id="80ee4-120">The reducer reads the tab-delimited key/value pairs, processes the data, and then emits the result as tab-delimited key/value pairs on STDOUT.</span></span>
5. <span data-ttu-id="80ee4-121">A saída é lido pelo Hadoop e gravada no diretório de saída.</span><span class="sxs-lookup"><span data-stu-id="80ee4-121">The output is read by Hadoop and written to the output directory.</span></span>

<span data-ttu-id="80ee4-122">Para obter mais informações sobre streaming, consulte [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span><span class="sxs-lookup"><span data-stu-id="80ee4-122">For more information on streaming, see [Hadoop Streaming (https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html)](https://hadoop.apache.org/docs/r2.7.1/hadoop-streaming/HadoopStreaming.html).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="80ee4-123">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="80ee4-123">Prerequisites</span></span>

* <span data-ttu-id="80ee4-124">Familiaridade com gravação e compilação de código em C# que se destina ao .NET Framework 4.5.</span><span class="sxs-lookup"><span data-stu-id="80ee4-124">A familiarity with writing and building C# code that targets .NET Framework 4.5.</span></span> <span data-ttu-id="80ee4-125">As etapas neste tutorial usam o Visual Studio 2017.</span><span class="sxs-lookup"><span data-stu-id="80ee4-125">The steps in this document use Visual Studio 2017.</span></span>

* <span data-ttu-id="80ee4-126">Uma forma de carregar arquivos .exe no cluster.</span><span class="sxs-lookup"><span data-stu-id="80ee4-126">A way to upload .exe files to the cluster.</span></span> <span data-ttu-id="80ee4-127">As etapas neste documento usam o Data Lake Tools para Visual Studio para carregar os arquivos no armazenamento primário do cluster.</span><span class="sxs-lookup"><span data-stu-id="80ee4-127">The steps in this document use the Data Lake Tools for Visual Studio to upload the files to primary storage for the cluster.</span></span>

* <span data-ttu-id="80ee4-128">Azure PowerShell ou um cliente SSH.</span><span class="sxs-lookup"><span data-stu-id="80ee4-128">Azure PowerShell or a SSH client.</span></span>

* <span data-ttu-id="80ee4-129">Um Hadoop no cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80ee4-129">A Hadoop on HDInsight cluster.</span></span> <span data-ttu-id="80ee4-130">Para obter mais informações sobre como criar um cluster, consulte [Criar um cluster do HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="80ee4-130">For more information on creating a cluster, see [Create an HDInsight cluster](hdinsight-provision-clusters.md).</span></span>

## <a name="create-the-mapper"></a><span data-ttu-id="80ee4-131">Criar o mapeador</span><span class="sxs-lookup"><span data-stu-id="80ee4-131">Create the mapper</span></span>

<span data-ttu-id="80ee4-132">No Visual Studio, crie um novo __aplicativo de console__ chamado __mapeador__.</span><span class="sxs-lookup"><span data-stu-id="80ee4-132">In Visual Studio, create a new __Console application__ named __mapper__.</span></span> <span data-ttu-id="80ee4-133">Use o seguinte código para o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="80ee4-133">Use the following code for the application:</span></span>

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
            //Hadoop passes data to the mapper on STDIN
            while((line = Console.ReadLine()) != null)
            {
                // We only want words, so strip out punctuation, numbers, etc.
                var onlyText = Regex.Replace(line, @"\.|;|:|,|[0-9]|'", "");
                // Split at whitespace.
                var words = Regex.Matches(onlyText, @"[\w]+");
                // Loop over the words
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

<span data-ttu-id="80ee4-134">Depois de criar o aplicativo, compile-o para produzir o arquivo `/bin/Debug/mapper.exe` no diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="80ee4-134">After creating the application, build it to produce the `/bin/Debug/mapper.exe` file in the project directory.</span></span>

## <a name="create-the-reducer"></a><span data-ttu-id="80ee4-135">Criar o redutor</span><span class="sxs-lookup"><span data-stu-id="80ee4-135">Create the reducer</span></span>

<span data-ttu-id="80ee4-136">No Visual Studio, crie um novo __Aplicativo de console__ chamado __redutor__.</span><span class="sxs-lookup"><span data-stu-id="80ee4-136">In Visual Studio, create a new __Console application__ named __reducer__.</span></span> <span data-ttu-id="80ee4-137">Use o seguinte código para o aplicativo:</span><span class="sxs-lookup"><span data-stu-id="80ee4-137">Use the following code for the application:</span></span>

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
                // Get the word
                string word = sArr[0];
                // Get the count
                int count = Convert.ToInt32(sArr[1]);

                //Do we already have a count for the word?
                if(words.ContainsKey(word))
                {
                    //If so, increment the count
                    words[word] += count;
                } else
                {
                    //Add the key to the collection
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

<span data-ttu-id="80ee4-138">Depois de criar o aplicativo, compile-o para produzir o arquivo `/bin/Debug/reducer.exe` no diretório do projeto.</span><span class="sxs-lookup"><span data-stu-id="80ee4-138">After creating the application, build it to produce the `/bin/Debug/reducer.exe` file in the project directory.</span></span>

## <a name="upload-to-storage"></a><span data-ttu-id="80ee4-139">Carregar para o armazenamento</span><span class="sxs-lookup"><span data-stu-id="80ee4-139">Upload to storage</span></span>

1. <span data-ttu-id="80ee4-140">No Visual Studio, abra **Gerenciador de Servidores**.</span><span class="sxs-lookup"><span data-stu-id="80ee4-140">In Visual Studio, open **Server Explorer**.</span></span>

2. <span data-ttu-id="80ee4-141">Expanda **Azure** e expanda **HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="80ee4-141">Expand **Azure**, and then expand **HDInsight**.</span></span>

3. <span data-ttu-id="80ee4-142">Se solicitado, insira suas credenciais de assinatura do Azure e, em seguida, clique em **Entrar**.</span><span class="sxs-lookup"><span data-stu-id="80ee4-142">If prompted, enter your Azure subscription credentials, and then click **Sign In**.</span></span>

4. <span data-ttu-id="80ee4-143">Expanda o cluster HDInsight no qual você deseja implantar esse aplicativo.</span><span class="sxs-lookup"><span data-stu-id="80ee4-143">Expand the HDInsight cluster that you wish to deploy this application to.</span></span> <span data-ttu-id="80ee4-144">Uma entrada com o texto __(Conta de armazenamento padrão)__ é listada.</span><span class="sxs-lookup"><span data-stu-id="80ee4-144">An entry with the text __(Default Storage Account)__ is listed.</span></span>

    ![Gerenciador de Servidores mostrando a conta de armazenamento para o cluster](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/storage.png)

    * <span data-ttu-id="80ee4-146">Se essa entrada puder ser expandida, você estará usando uma __Conta de Armazenamento do Azure__ como armazenamento padrão do cluster.</span><span class="sxs-lookup"><span data-stu-id="80ee4-146">If this entry can be expanded, you are using an __Azure Storage Account__ as default storage for the cluster.</span></span> <span data-ttu-id="80ee4-147">Para exibir os arquivos no armazenamento padrão para o cluster, expanda a entrada e clique duas vezes no __(Contêiner Padrão)__.</span><span class="sxs-lookup"><span data-stu-id="80ee4-147">To view the files on the default storage for the cluster, expand the entry and then double-click the __(Default Container)__.</span></span>

    * <span data-ttu-id="80ee4-148">Se essa entrada não puder ser expandida, você estará usando __Azure Data Lake Store__ como o armazenamento padrão do cluster.</span><span class="sxs-lookup"><span data-stu-id="80ee4-148">If this entry cannot be expanded, you are using __Azure Data Lake Store__ as the default storage for the cluster.</span></span> <span data-ttu-id="80ee4-149">Para exibir os arquivos no armazenamento padrão do cluster, clique duas vezes na entrada __(Conta de Armazenamento Padrão)__.</span><span class="sxs-lookup"><span data-stu-id="80ee4-149">To view the files on the default storage for the cluster, double-click the __(Default Storage Account)__ entry.</span></span>

5. <span data-ttu-id="80ee4-150">Para carregar os arquivos .exe, use um dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="80ee4-150">To upload the .exe files, use one of the following methods:</span></span>

    * <span data-ttu-id="80ee4-151">Se estiver usando uma __Conta de Armazenamento do Azure__, clique no ícone de upload e, em seguida, navegue até a pasta **bin\debug** do projeto **mapeador**.</span><span class="sxs-lookup"><span data-stu-id="80ee4-151">If using an __Azure Storage Account__, click the upload icon, and then browse to the **bin\debug** folder for the **mapper** project.</span></span> <span data-ttu-id="80ee4-152">Por fim, selecione o arquivo **mapper.exe** e clique em **Ok**.</span><span class="sxs-lookup"><span data-stu-id="80ee4-152">Finally, select the **mapper.exe** file and click **Ok**.</span></span>

        ![ícone de carregamento](./media/hdinsight-hadoop-hive-pig-udf-dotnet-csharp/upload.png)
    
    * <span data-ttu-id="80ee4-154">Se estiver usando o __Azure Data Lake Store__, clique com o botão direito do mouse em uma área vazia na listagem de arquivos e, em seguida, selecione __Carregar__.</span><span class="sxs-lookup"><span data-stu-id="80ee4-154">If using __Azure Data Lake Store__, right-click an empty area in the file listing, and then select __Upload__.</span></span> <span data-ttu-id="80ee4-155">Por fim, selecione o arquivo **mapper.exe** e clique em **Abrir**.</span><span class="sxs-lookup"><span data-stu-id="80ee4-155">Finally, select the **mapper.exe** file and click **Open**.</span></span>

    <span data-ttu-id="80ee4-156">Após o __mapper.exe__ cser carregado, repita o processo de upload para o arquivo __reducer.exe__.</span><span class="sxs-lookup"><span data-stu-id="80ee4-156">Once the __mapper.exe__ upload has finished, repeat the upload process for the __reducer.exe__ file.</span></span>

## <a name="run-a-job-using-an-ssh-session"></a><span data-ttu-id="80ee4-157">Executar um trabalho: usando uma sessão SSH</span><span class="sxs-lookup"><span data-stu-id="80ee4-157">Run a job: Using an SSH session</span></span>

1. <span data-ttu-id="80ee4-158">Use o SSH para conectar ao cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80ee4-158">Use SSH to connect to the HDInsight cluster.</span></span> <span data-ttu-id="80ee4-159">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="80ee4-159">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="80ee4-160">Use um dos seguintes comandos para iniciar o trabalho MapReduce:</span><span class="sxs-lookup"><span data-stu-id="80ee4-160">Use one of the following command to start the MapReduce job:</span></span>

    * <span data-ttu-id="80ee4-161">Se estiver usando o __Data Lake Store__ como armazenamento padrão:</span><span class="sxs-lookup"><span data-stu-id="80ee4-161">If using __Data Lake Store__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files adl:///mapper.exe,adl:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```
    
    * <span data-ttu-id="80ee4-162">Se estiver usando o __Armazenamento do Azure__ como armazenamento padrão:</span><span class="sxs-lookup"><span data-stu-id="80ee4-162">If using __Azure Storage__ as default storage:</span></span>

        ```bash
        yarn jar /usr/hdp/current/hadoop-mapreduce-client/hadoop-streaming.jar -files wasb:///mapper.exe,wasb:///reducer.exe -mapper mapper.exe -reducer reducer.exe -input /example/data/gutenberg/davinci.txt -output /example/wordcountout
        ```

    <span data-ttu-id="80ee4-163">A lista a seguir descreve o que cada parâmetro faz:</span><span class="sxs-lookup"><span data-stu-id="80ee4-163">The following list describes what each parameter does:</span></span>

    * <span data-ttu-id="80ee4-164">`hadoop-streaming.jar`: o arquivo jar que contém a funcionalidade MapReduce de streaming.</span><span class="sxs-lookup"><span data-stu-id="80ee4-164">`hadoop-streaming.jar`: The jar file that contains the streaming MapReduce functionality.</span></span>
    * <span data-ttu-id="80ee4-165">`-files`: adiciona os arquivos `mapper.exe` e `reducer.exe` a esse trabalho.</span><span class="sxs-lookup"><span data-stu-id="80ee4-165">`-files`: Adds the `mapper.exe` and `reducer.exe` files to this job.</span></span> <span data-ttu-id="80ee4-166">O `adl:///` ou `wasb:///` antes de cada arquivo é o caminho para a raiz do armazenamento padrão do cluster.</span><span class="sxs-lookup"><span data-stu-id="80ee4-166">The `adl:///` or `wasb:///` before each file is the path to the root of default storage for the cluster.</span></span>
    * <span data-ttu-id="80ee4-167">`-mapper`: especifica qual arquivo implementa o mapeador.</span><span class="sxs-lookup"><span data-stu-id="80ee4-167">`-mapper`: Specifies which file implements the mapper.</span></span>
    * <span data-ttu-id="80ee4-168">`-reducer`: especifica qual arquivo implementa o redutor.</span><span class="sxs-lookup"><span data-stu-id="80ee4-168">`-reducer`: Specifies which file implements the reducer.</span></span>
    * <span data-ttu-id="80ee4-169">`-input`: os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="80ee4-169">`-input`: The input data.</span></span>
    * <span data-ttu-id="80ee4-170">`-output`: o diretório de saída.</span><span class="sxs-lookup"><span data-stu-id="80ee4-170">`-output`: The output directory.</span></span>

3. <span data-ttu-id="80ee4-171">Após a conclusão do trabalho MapReduce, use o seguinte para exibir os resultados:</span><span class="sxs-lookup"><span data-stu-id="80ee4-171">Once the MapReduce job completes, use the following to view the results:</span></span>

    ```bash
    hdfs dfs -text /example/wordcountout/part-00000
    ```

    <span data-ttu-id="80ee4-172">A seguinte lista é um exemplo dos dados retornados pelos comandos anteriores:</span><span class="sxs-lookup"><span data-stu-id="80ee4-172">The following text is an example of the data returned by this command:</span></span>

        you     1128
        young   38
        younger 1
        youngest        1
        your    338
        yours   4
        yourself        34
        yourselves      3
        youth   17

## <a name="run-a-job-using-powershell"></a><span data-ttu-id="80ee4-173">Executar um trabalho: usando o PowerShell</span><span class="sxs-lookup"><span data-stu-id="80ee4-173">Run a job: Using PowerShell</span></span>

<span data-ttu-id="80ee4-174">Use o seguinte script de PowerShell para executar um trabalho MapReduce e baixar os resultados.</span><span class="sxs-lookup"><span data-stu-id="80ee4-174">Use the following PowerShell script to run a MapReduce job and download the results.</span></span>

<span data-ttu-id="80ee4-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span><span class="sxs-lookup"><span data-stu-id="80ee4-175">[!code-powershell[main](../../powershell_scripts/hdinsight/use-csharp-mapreduce/use-csharp-mapreduce.ps1?range=5-87)]</span></span>

<span data-ttu-id="80ee4-176">Esse script solicita nome e senha da conta de logon do cluster, juntamente com o nome do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="80ee4-176">This script prompts you for the cluster login account name and password, along with the HDInsight cluster name.</span></span> <span data-ttu-id="80ee4-177">Após a conclusão do trabalho, o resultado será baixado no arquivo `output.txt` no diretório em que o script foi executado.</span><span class="sxs-lookup"><span data-stu-id="80ee4-177">Once the job completes, the output is downloaded to the `output.txt` file in the directory the script is ran from.</span></span> <span data-ttu-id="80ee4-178">O seguinte texto é um exemplo dos dados no arquivo `output.txt`:</span><span class="sxs-lookup"><span data-stu-id="80ee4-178">The following text is an example of the data in the `output.txt` file:</span></span>

    you     1128
    young   38
    younger 1
    youngest        1
    your    338
    yours   4
    yourself        34
    yourselves      3
    youth   17

## <a name="next-steps"></a><span data-ttu-id="80ee4-179">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="80ee4-179">Next steps</span></span>

<span data-ttu-id="80ee4-180">Para obter mais informações sobre como usar o MapReduce com HDInsight, veja [Usar MapReduce com HDInsight](hdinsight-use-mapreduce.md).</span><span class="sxs-lookup"><span data-stu-id="80ee4-180">For more information on using MapReduce with HDInsight, see [Use MapReduce with HDInsight](hdinsight-use-mapreduce.md).</span></span>

<span data-ttu-id="80ee4-181">Para obter informações sobre como usar C# com Hive e Pig, consulte [Usar uma função C# definida pelo usuário com Hive e Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span><span class="sxs-lookup"><span data-stu-id="80ee4-181">For information on using C# with Hive and Pig, see [Use a C# user defined function with Hive and Pig](hdinsight-hadoop-hive-pig-udf-dotnet-csharp.md).</span></span>

<span data-ttu-id="80ee4-182">Para obter informações sobre como usar C# com Storm no HDInsight, consulte [Desenvolver topologias C# para Storm no HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span><span class="sxs-lookup"><span data-stu-id="80ee4-182">For information on using C# with Storm on HDInsight, see [Develop C# topologies for Storm on HDInsight](hdinsight-storm-develop-csharp-visual-studio-topology.md).</span></span>