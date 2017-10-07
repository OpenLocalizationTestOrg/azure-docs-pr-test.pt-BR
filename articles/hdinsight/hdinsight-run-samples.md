---
title: amostras do hello aaaRun Hadoop em HDInsight - Azure | Microsoft Docs
description: "Começar a usar o serviço HDInsight do Azure de saudação com hello exemplos fornecidos. Use os scripts do PowerShell que executam programas MapReduce em clusters de dados."
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: bf76d452-abb4-4210-87bd-a2067778c6ed
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ROBOTS: NOINDEX
ms.openlocfilehash: 544856a2cdfe5154cbd9bf1fb05db081af86cd46
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="run-hadoop-mapreduce-samples-in-windows-based-hdinsight"></a><span data-ttu-id="be447-104">Executar exemplos do MapReduce do Hadoop no HDInsight baseado em Windows</span><span class="sxs-lookup"><span data-stu-id="be447-104">Run Hadoop MapReduce samples in Windows-based HDInsight</span></span>
[!INCLUDE [samples-selector](../../includes/hdinsight-run-samples-selector.md)]

<span data-ttu-id="be447-105">Um conjunto de exemplos são fornecidos toohelp você começar a executar trabalhos de MapReduce em clusters de Hadoop usando o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="be447-105">A set of samples are provided toohelp you get started running MapReduce jobs on Hadoop clusters using Azure HDInsight.</span></span> <span data-ttu-id="be447-106">Esses exemplos são disponibilizados em cada Olá HDInsight clusters gerenciados que você criar.</span><span class="sxs-lookup"><span data-stu-id="be447-106">These samples are made available on each of hello HDInsight managed clusters that you create.</span></span> <span data-ttu-id="be447-107">Executar esses exemplos familiarizá-lo com o uso do Azure PowerShell cmdlets toorun trabalhos em clusters de Hadoop.</span><span class="sxs-lookup"><span data-stu-id="be447-107">Running these samples familiarize you with using Azure PowerShell cmdlets toorun jobs on Hadoop clusters.</span></span>

* <span data-ttu-id="be447-108">[**Contagem de palavras**][hdinsight-sample-wordcount]: conta as ocorrências de palavras em um arquivo de texto.</span><span class="sxs-lookup"><span data-stu-id="be447-108">[**Word count**][hdinsight-sample-wordcount]: Counts word occurrences in a text file.</span></span>
* <span data-ttu-id="be447-109">[**Contagem de palavras de streaming em c#**][hdinsight-sample-csharp-streaming]: Olá contagens de ocorrências de palavras em um arquivo de texto usando a interface de transmissão do Hadoop.</span><span class="sxs-lookup"><span data-stu-id="be447-109">[**C# streaming word count**][hdinsight-sample-csharp-streaming]: Counts word occurrences in a text file using hello Hadoop streaming interface.</span></span>
* <span data-ttu-id="be447-110">[**Avaliador de pi**][hdinsight-sample-pi-estimator]: usa uma estatística (quase Monte Carlo) valor de saudação do método tooestimate de pi.</span><span class="sxs-lookup"><span data-stu-id="be447-110">[**Pi estimator**][hdinsight-sample-pi-estimator]: Uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span>
* <span data-ttu-id="be447-111">[**Graysort de 10 GB**][hdinsight-sample-10gb-graysort]: executar um GraySort de finalidade geral em um arquivo de 10 GB usando o HDInsight.</span><span class="sxs-lookup"><span data-stu-id="be447-111">[**10-GB Graysort**][hdinsight-sample-10gb-graysort]: Run a general-purpose GraySort on a 10 GB file by using HDInsight.</span></span> <span data-ttu-id="be447-112">Há três toorun de trabalhos: Teragen toogenerate Olá dados, dados de saudação do Terasort toosort e tooconfirm Teravalidate dados saudação foram classificados corretamente.</span><span class="sxs-lookup"><span data-stu-id="be447-112">There are three jobs toorun: Teragen toogenerate hello data, Terasort toosort hello data, and Teravalidate tooconfirm that hello data has been properly sorted.</span></span>

> [!NOTE]
> <span data-ttu-id="be447-113">código-fonte Olá pode ser encontrado no hello apêndice.</span><span class="sxs-lookup"><span data-stu-id="be447-113">hello source code can be found in hello Appendix.</span></span>

<span data-ttu-id="be447-114">Documentação adicional muito existe no web Olá para tecnologias relacionadas ao Hadoop, como programação baseada em Java MapReduce e streaming e documentação sobre os cmdlets de saudação que são usados no Windows PowerShell scripts.</span><span class="sxs-lookup"><span data-stu-id="be447-114">Much additional documentation exists on hello web for Hadoop-related technologies, such as Java-based MapReduce programming and streaming, and documentation about hello cmdlets that are used in Windows PowerShell scripting.</span></span> <span data-ttu-id="be447-115">Para obter mais informações sobre esses recursos, consulte</span><span class="sxs-lookup"><span data-stu-id="be447-115">For more information about these resources, see:</span></span>

* [<span data-ttu-id="be447-116">Desenvolver programas Java MapReduce para Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="be447-116">Develop Java MapReduce programs for Hadoop in HDInsight</span></span>](hdinsight-develop-deploy-java-mapreduce-linux.md)
* [<span data-ttu-id="be447-117">Enviar trabalhos Hadoop no HDInsight</span><span class="sxs-lookup"><span data-stu-id="be447-117">Submit Hadoop jobs in HDInsight</span></span>](hdinsight-submit-hadoop-jobs-programmatically.md)
* <span data-ttu-id="be447-118">[Introdução tooAzure HDInsight][hdinsight-introduction]</span><span class="sxs-lookup"><span data-stu-id="be447-118">[Introduction tooAzure HDInsight][hdinsight-introduction]</span></span>

<span data-ttu-id="be447-119">Hoje em dia, muitas pessoas escolhem o Hive e o Pig em vez do MapReduce.</span><span class="sxs-lookup"><span data-stu-id="be447-119">Nowadays, many people choose Hive and Pig over MapReduce.</span></span>  <span data-ttu-id="be447-120">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="be447-120">For more information, see:</span></span>

* [<span data-ttu-id="be447-121">Usar o Hive no HDInsight</span><span class="sxs-lookup"><span data-stu-id="be447-121">Use Hive in HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="be447-122">Usar o Pig no HDInsight</span><span class="sxs-lookup"><span data-stu-id="be447-122">Use Pig in HDInsight</span></span>](hdinsight-use-pig.md)

<span data-ttu-id="be447-123">**Pré-requisitos**:</span><span class="sxs-lookup"><span data-stu-id="be447-123">**Prerequisites**:</span></span>

* <span data-ttu-id="be447-124">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="be447-124">**An Azure subscription**.</span></span> <span data-ttu-id="be447-125">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="be447-125">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* <span data-ttu-id="be447-126">**um cluster do HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="be447-126">**an HDInsight cluster**.</span></span> <span data-ttu-id="be447-127">Para obter instruções sobre Olá várias maneiras em que esses clusters podem ser criados, consulte [Hadoop criar clusters de HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="be447-127">For instructions on hello various ways in which such clusters can be created, see [Create Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="be447-128">**Uma estação de trabalho com o PowerShell do Azure**.</span><span class="sxs-lookup"><span data-stu-id="be447-128">**A workstation with Azure PowerShell**.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="be447-129">O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e será removido em 1º de janeiro de 2017.</span><span class="sxs-lookup"><span data-stu-id="be447-129">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and will be removed by January 1, 2017.</span></span> <span data-ttu-id="be447-130">Olá etapas para esse documento use Olá novos cmdlets do HDInsight que funcionam com o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="be447-130">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="be447-131">Siga as etapas de saudação em [instalar e configurar o Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall Olá última versão do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="be447-131">Follow hello steps in [Install and configure Azure PowerShell](/powershell/azureps-cmdlets-docs) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="be447-132">Se você tiver scripts que toobe necessidade modificado toouse Olá novos cmdlets que funcionam com o Gerenciador de recursos do Azure, consulte [tooAzure migrando desenvolvimento baseado no Gerenciador de recursos de ferramentas para clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md).</span><span class="sxs-lookup"><span data-stu-id="be447-132">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md).</span></span>

## <span data-ttu-id="be447-133"><a name="hdinsight-sample-wordcount"></a>Contagem de palavras - Java</span><span class="sxs-lookup"><span data-stu-id="be447-133"><a name="hdinsight-sample-wordcount"></a>Word count - Java</span></span>
<span data-ttu-id="be447-134">toosubmit um projeto de MapReduce, primeiro crie uma definição de trabalho de MapReduce.</span><span class="sxs-lookup"><span data-stu-id="be447-134">toosubmit a MapReduce project, you first create a MapReduce job definition.</span></span> <span data-ttu-id="be447-135">Na definição de trabalho hello, você especificar o arquivo jar do hello MapReduce programa e o local de saudação do arquivo jar hello, o que é **wasb:///example/jars/hadoop-mapreduce-examples.jar**, Olá nome de classe e Olá argumentos.</span><span class="sxs-lookup"><span data-stu-id="be447-135">In hello job definition, you specify hello MapReduce program jar file and hello location of hello jar file, which is **wasb:///example/jars/hadoop-mapreduce-examples.jar**, hello class name, and hello arguments.</span></span>  <span data-ttu-id="be447-136">programa de MapReduce wordcount Olá leva dois argumentos: arquivo de origem Olá palavras usadas toocount e local de saudação para saída.</span><span class="sxs-lookup"><span data-stu-id="be447-136">hello wordcount MapReduce program takes two arguments: hello source file that is used toocount words, and hello location for output.</span></span>

<span data-ttu-id="be447-137">código-fonte Olá pode ser encontrado no hello [Apêndice A](#apendix-a---the-word-count-MapReduce-program-in-java).</span><span class="sxs-lookup"><span data-stu-id="be447-137">hello source code can be found in hello [Appendix A](#apendix-a---the-word-count-MapReduce-program-in-java).</span></span>

<span data-ttu-id="be447-138">Para o procedimento de saudação do desenvolvimento de um MapReduce Java de programa, consulte - [programas de MapReduce desenvolver de Java para Hadoop no HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)</span><span class="sxs-lookup"><span data-stu-id="be447-138">For hello procedure of developing a Java MapReduce program, see - [Develop Java MapReduce programs for Hadoop in HDInsight](hdinsight-develop-deploy-java-mapreduce-linux.md)</span></span>

<span data-ttu-id="be447-139">**toosubmit um trabalho de MapReduce de contagem de palavras**</span><span class="sxs-lookup"><span data-stu-id="be447-139">**toosubmit a word count MapReduce job**</span></span>

1. <span data-ttu-id="be447-140">Abra o **ISE do Windows PowerShell**.</span><span class="sxs-lookup"><span data-stu-id="be447-140">Open **Windows PowerShell ISE**.</span></span> <span data-ttu-id="be447-141">Para obter instruções, consulte [Instalar e configurar o Azure PowerShell][powershell-install-configure].</span><span class="sxs-lookup"><span data-stu-id="be447-141">For instructions, see [Install and configure Azure PowerShell][powershell-install-configure].</span></span>
2. <span data-ttu-id="be447-142">Cole Olá script do PowerShell a seguir:</span><span class="sxs-lookup"><span data-stu-id="be447-142">Paste hello following PowerShell script:</span></span>

    ```powershell
    $subscriptionName = "<Azure Subscription Name>"
    $resourceGroupName = "<Resource Group Name>"
    $clusterName = "<HDInsight cluster name>"             # HDInsight cluster name

    Select-AzureRmSubscription -SubscriptionName $subscriptionName

    # Define hello MapReduce job
    $mrJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "wordcount" `
                                -Arguments "wasb:///example/data/gutenberg/davinci.txt", "wasb:///example/data/WordCountOutput"

    # Submit hello job and wait for job completion
    $cred = Get-Credential -Message "Enter hello HDInsight cluster HTTP user credential:"
    $mrJob = Start-AzureRmHDInsightJob `
                        -ResourceGroupName $resourceGroupName `
                        -ClusterName $clusterName `
                        -HttpCredential $cred `
                        -JobDefinition $mrJobDefinition

    Wait-AzureRmHDInsightJob `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -JobId $mrJob.JobId

    # Get hello job output
    $cluster = Get-AzureRmHDInsightCluster -ResourceGroupName $resourceGroupName -ClusterName $clusterName
    $defaultStorageAccount = $cluster.DefaultStorageAccount -replace '.blob.core.windows.net'
    $defaultStorageAccountKey = (Get-AzureRmStorageAccountKey -ResourceGroupName $resourceGroupName -Name $defaultStorageAccount)[0].Value
    $defaultStorageContainer = $cluster.DefaultStorageContainer

    Get-AzureRmHDInsightJobOutput `
        -ResourceGroupName $resourceGroupName `
        -ClusterName $clusterName `
        -HttpCredential $cred `
        -DefaultStorageAccountName $defaultStorageAccount `
        -DefaultStorageAccountKey $defaultStorageAccountKey `
        -DefaultContainer $defaultStorageContainer  `
        -JobId $mrJob.JobId `
        -DisplayOutputType StandardError

    # Download hello job output toohello workstation
    $storageContext = New-AzureStorageContext -StorageAccountName $defaultStorageAccount -StorageAccountKey $defaultStorageAccountKey
    Get-AzureStorageBlobContent -Container $defaultStorageContainer -Blob example/data/WordCountOutput/part-r-00000 -Context $storageContext -Force

    # Display hello output file
    cat ./example/data/WordCountOutput/part-r-00000 | findstr "there"
    ```

    <span data-ttu-id="be447-143">trabalho de MapReduce Hello produz um arquivo chamado *parte-r-00000*, que contém palavras e contagens de saudação.</span><span class="sxs-lookup"><span data-stu-id="be447-143">hello MapReduce job produces a file named *part-r-00000*, which contains words and hello counts.</span></span> <span data-ttu-id="be447-144">script Hello usa Olá **findstr** comando toolist Olá a todas as palavras que contém *"there"*.</span><span class="sxs-lookup"><span data-stu-id="be447-144">hello script uses hello **findstr** command toolist all hello words that contains *"there"*.</span></span>
3. <span data-ttu-id="be447-145">Defina Olá primeiro três variáveis e execute o script hello.</span><span class="sxs-lookup"><span data-stu-id="be447-145">Set hello first three variables, and run hello script.</span></span>

## <span data-ttu-id="be447-146"><a name="hdinsight-sample-csharp-streaming"></a>Contagem de palavras - Transmissão em C#</span><span class="sxs-lookup"><span data-stu-id="be447-146"><a name="hdinsight-sample-csharp-streaming"></a>Word count - C# streaming</span></span>
<span data-ttu-id="be447-147">Hadoop fornece um fluxo tooMapReduce de API, que permite que você toowrite mapa e diminuir as funções em idiomas diferentes do Java.</span><span class="sxs-lookup"><span data-stu-id="be447-147">Hadoop provides a streaming API tooMapReduce, which enables you toowrite map and reduce functions in languages other than Java.</span></span>

> [!NOTE]
> <span data-ttu-id="be447-148">Olá etapas neste tutorial aplicam-se apenas com base em tooWindows clusters de HDInsight.</span><span class="sxs-lookup"><span data-stu-id="be447-148">hello steps in this tutorial apply only tooWindows-based HDInsight clusters.</span></span> <span data-ttu-id="be447-149">Para obter um exemplo de streaming para clusters do HDInsight baseados em Linux, consulte [Desenvolver programas de streaming em Python para o HDInsight](hdinsight-hadoop-streaming-python.md).</span><span class="sxs-lookup"><span data-stu-id="be447-149">For an example of streaming for Linux-based HDInsight clusters, see [Develop Python streaming programs for HDInsight](hdinsight-hadoop-streaming-python.md).</span></span>

<span data-ttu-id="be447-150">No exemplo hello, mapeador hello e Redutor Olá são executáveis que leia a entrada de saudação do [stdin] [ stdin-stdout-stderr] (linha por linha) e emitir saída Olá muito[stdout] [stdin-stdout-stderr].</span><span class="sxs-lookup"><span data-stu-id="be447-150">In hello example, hello mapper and hello reducer are executables that read hello input from [stdin][stdin-stdout-stderr] (line-by-line) and emit hello output too[stdout][stdin-stdout-stderr].</span></span> <span data-ttu-id="be447-151">programa Hello contagens de todas as palavras Olá no texto de saudação.</span><span class="sxs-lookup"><span data-stu-id="be447-151">hello program counts all hello words in hello text.</span></span>

<span data-ttu-id="be447-152">Quando um arquivo executável é especificado para **mapeadores de**, cada tarefa mapeador inicia Olá executável como um processo separado quando mapeador de saudação é inicializado.</span><span class="sxs-lookup"><span data-stu-id="be447-152">When an executable is specified for **mappers**, each mapper task launches hello executable as a separate process when hello mapper is initialized.</span></span> <span data-ttu-id="be447-153">Olá mapeador tarefa é executada, converte sua entrada em linhas e feeds Olá linhas toohello [stdin] [ stdin-stdout-stderr] do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="be447-153">As hello mapper task runs, it converts its input into lines, and feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="be447-154">Enquanto isso, no hello mapeador Olá coleta saída orientado por linha de saudação de saudação stdout do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="be447-154">In hello meantime, hello mapper collects hello line-oriented output from hello stdout of hello process.</span></span> <span data-ttu-id="be447-155">Converte cada linha em um par chave/valor, que é coletado como saída de saudação do mapeador de saudação.</span><span class="sxs-lookup"><span data-stu-id="be447-155">It converts each line into a key/value pair, which is collected as hello output of hello mapper.</span></span> <span data-ttu-id="be447-156">Por padrão, prefixo de saudação de uma linha para cima toohello primeiro caractere de tabulação é chave hello e restante Olá linha hello (excluindo Olá caractere de tabulação) é o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="be447-156">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span> <span data-ttu-id="be447-157">Se não houver nenhum caractere de tabulação na linha hello, toda a linha é considerada como chave hello e Olá valor é nulo.</span><span class="sxs-lookup"><span data-stu-id="be447-157">If there is no Tab character in hello line, entire line is considered as hello key, and hello value is null.</span></span>

<span data-ttu-id="be447-158">Quando um arquivo executável é especificado para **reducers**, cada tarefa Redutor inicia Olá executável como um processo separado quando Redutor Olá é inicializado.</span><span class="sxs-lookup"><span data-stu-id="be447-158">When an executable is specified for **reducers**, each reducer task launches hello executable as a separate process when hello reducer is initialized.</span></span> <span data-ttu-id="be447-159">Olá Redutor tarefa é executada, converte seus pares de chave/valores de entrada em linhas e feeds de saudação linhas toohello [stdin] [ stdin-stdout-stderr] do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="be447-159">As hello reducer task runs, it converts its input key/values pairs into lines, and it feeds hello lines toohello [stdin][stdin-stdout-stderr] of hello process.</span></span>

<span data-ttu-id="be447-160">Em Olá enquanto isso, Redutor Olá coleta saída orientado por linha de saudação do hello [stdout] [ stdin-stdout-stderr] do processo de saudação.</span><span class="sxs-lookup"><span data-stu-id="be447-160">In hello meantime, hello reducer collects hello line-oriented output from hello [stdout][stdin-stdout-stderr] of hello process.</span></span> <span data-ttu-id="be447-161">Ele converte cada par chave/valor de tooa de linha, que é coletado como saída de saudação do Redutor hello.</span><span class="sxs-lookup"><span data-stu-id="be447-161">It converts each line tooa key/value pair, which is collected as hello output of hello reducer.</span></span> <span data-ttu-id="be447-162">Por padrão, prefixo de saudação de uma linha para cima toohello primeiro caractere de tabulação é chave hello e restante Olá linha hello (excluindo Olá caractere de tabulação) é o valor de saudação.</span><span class="sxs-lookup"><span data-stu-id="be447-162">By default, hello prefix of a line up toohello first Tab character is hello key, and hello remainder of hello line (excluding hello Tab character) is hello value.</span></span>

<span data-ttu-id="be447-163">**trabalho de contagem de palavras de streaming toosubmit c#**</span><span class="sxs-lookup"><span data-stu-id="be447-163">**toosubmit a C# streaming word count job**</span></span>

* <span data-ttu-id="be447-164">Siga o procedimento Olá [palavras contagem - Java](#word-count-java)e substitua a definição de trabalho de saudação com hello seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="be447-164">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobDefinition = New-AzureRmHDInsightStreamingMapReduceJobDefinition `
                            -Files "/example/apps/cat.exe","/example/apps/wc.exe" `
                            -Mapper "cat.exe" `
                            -Reducer "wc.exe" `
                            -InputPath "/example/data/gutenberg/davinci.txt" `
                            -OutputPath "/example/data/StreamingOutput/wc.txt"
    ```

    <span data-ttu-id="be447-165">arquivo de saída de Hello deverá ser:</span><span class="sxs-lookup"><span data-stu-id="be447-165">hello output file shall be:</span></span>

        example/data/StreamingOutput/wc.txt/part-00000

## <span data-ttu-id="be447-166"><a name="hdinsight-sample-pi-estimator"></a>Estimador de PI</span><span class="sxs-lookup"><span data-stu-id="be447-166"><a name="hdinsight-sample-pi-estimator"></a>PI estimator</span></span>
<span data-ttu-id="be447-167">Avaliador de pi Olá usa uma estatística (quase Monte Carlo) valor de saudação do método tooestimate de pi.</span><span class="sxs-lookup"><span data-stu-id="be447-167">hello pi estimator uses a statistical (quasi-Monte Carlo) method tooestimate hello value of pi.</span></span> <span data-ttu-id="be447-168">Pontos colocados aleatório dentro de uma unidade quadrada também se enquadram dentro de um círculo inscritas dentro desse quadrado com uma área de toohello igual probabilidade de círculo hello, pi/4.</span><span class="sxs-lookup"><span data-stu-id="be447-168">Points placed at random inside of a unit square also fall within a circle inscribed within that square with a probability equal toohello area of hello circle, pi/4.</span></span> <span data-ttu-id="be447-169">valor de saudação de pi pode ser estimada do valor de saudação do 4R, onde R é a taxa de saudação do número de saudação de pontos que estão dentro de saudação círculo toohello número total de pontos que estão dentro do quadrado hello.</span><span class="sxs-lookup"><span data-stu-id="be447-169">hello value of pi can be estimated from hello value of 4R, where R is hello ratio of hello number of points that are inside hello circle toohello total number of points that are within hello square.</span></span> <span data-ttu-id="be447-170">Olá exemplo a saudação maior de pontos usados, melhor estimativa de Olá Olá é.</span><span class="sxs-lookup"><span data-stu-id="be447-170">hello larger hello sample of points used, hello better hello estimate is.</span></span>

<span data-ttu-id="be447-171">script Hello fornecido para este exemplo envia um trabalho do Hadoop jar e é configurado toorun com um valor de 16 mapas, cada um dos quais é necessário toocompute 10 milhões pontos de exemplo pelos valores de parâmetro hello.</span><span class="sxs-lookup"><span data-stu-id="be447-171">hello script provided for this sample submits a Hadoop jar job and is set up toorun with a value 16 maps, each of which is required toocompute 10 million sample points by hello parameter values.</span></span> <span data-ttu-id="be447-172">Esses parâmetros, os valores podem ser alterados tooimprove Olá estimado valor de pi.</span><span class="sxs-lookup"><span data-stu-id="be447-172">These parameter values can be changed tooimprove hello estimated value of pi.</span></span> <span data-ttu-id="be447-173">Para referência, hello 10 primeiros casas decimais de pi são 3.1415926535.</span><span class="sxs-lookup"><span data-stu-id="be447-173">For reference, hello first 10 decimal places of pi are 3.1415926535.</span></span>

<span data-ttu-id="be447-174">**toosubmit um trabalho do avaliador de pi**</span><span class="sxs-lookup"><span data-stu-id="be447-174">**toosubmit a pi estimator job**</span></span>

* <span data-ttu-id="be447-175">Siga o procedimento Olá [palavras contagem - Java](#word-count-java)e substitua a definição de trabalho de saudação com hello seguinte linha:</span><span class="sxs-lookup"><span data-stu-id="be447-175">Follow hello procedure in [Word count - Java](#word-count-java), and replace hello job definition with hello following line:</span></span>

    ```powershell
    $mrJobJobDefinition = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "wasb:///example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "pi" `
                                -Arguments "16", "10000000"
    ```

## <span data-ttu-id="be447-176"><a name="hdinsight-sample-10gb-graysort"></a>Graysort de 10 GB</span><span class="sxs-lookup"><span data-stu-id="be447-176"><a name="hdinsight-sample-10gb-graysort"></a>10-GB Graysort</span></span>
<span data-ttu-id="be447-177">Este exemplo usa uma quantidade modesta de 10 GB de dados para que possa ser executado de modo relativamente rápido.</span><span class="sxs-lookup"><span data-stu-id="be447-177">This sample uses a modest 10GB of data so that it can be run relatively quickly.</span></span> <span data-ttu-id="be447-178">Ele usa os aplicativos de MapReduce Olá desenvolvidos por Owen O'Malley e Arun Murthy que venceu o parâmetro de comparação do hello anual para fins gerais ("daytona") terabyte classificação em 2009 com uma taxa de 0.578 TB/min (100 TB em 173 minutos).</span><span class="sxs-lookup"><span data-stu-id="be447-178">It uses hello MapReduce applications developed by Owen O'Malley and Arun Murthy that won hello annual general-purpose ("daytona") terabyte sort benchmark in 2009 with a rate of 0.578TB/min (100TB in 173 minutes).</span></span> <span data-ttu-id="be447-179">Para obter mais informações sobre este e outros parâmetros de comparação de classificação, consulte Olá [Sortbenchmark](http://sortbenchmark.org/) site.</span><span class="sxs-lookup"><span data-stu-id="be447-179">For more information on this and other sorting benchmarks, see hello [Sortbenchmark](http://sortbenchmark.org/) site.</span></span>

<span data-ttu-id="be447-180">Este exemplo usa três conjuntos de programas MapReduce:</span><span class="sxs-lookup"><span data-stu-id="be447-180">This sample uses three sets of MapReduce programs:</span></span>

1. <span data-ttu-id="be447-181">**TeraGen** é um programa MapReduce que você pode usar linhas de saudação do toogenerate de toosort de dados.</span><span class="sxs-lookup"><span data-stu-id="be447-181">**TeraGen** is a MapReduce program that you can use toogenerate hello rows of data toosort.</span></span>
2. <span data-ttu-id="be447-182">**TeraSort** amostras de dados de entrada hello e usa dados de saudação do MapReduce toosort em uma ordem de total.</span><span class="sxs-lookup"><span data-stu-id="be447-182">**TeraSort** samples hello input data and uses MapReduce toosort hello data into a total order.</span></span> <span data-ttu-id="be447-183">TeraSort é uma classificação padrão das funções de MapReduce, exceto um particionador personalizado que usa uma lista classificada de chaves de n-1 de amostra que definem o intervalo de chave Olá para cada reduzir.</span><span class="sxs-lookup"><span data-stu-id="be447-183">TeraSort is a standard sort of MapReduce functions, except for a custom partitioner that uses a sorted list of N-1 sampled keys that define hello key range for each reduce.</span></span> <span data-ttu-id="be447-184">Em particular, todas as chaves de tal que exemplo [i-1] < = chave < exemplo [i] são enviadas tooreduce i.</span><span class="sxs-lookup"><span data-stu-id="be447-184">In particular, all keys such that sample[i-1] <= key < sample[i] are sent tooreduce i.</span></span> <span data-ttu-id="be447-185">Isso garante que as saídas da saudação reduzem i é todos os inferiores a reduzir a saída de saudação do i + 1.</span><span class="sxs-lookup"><span data-stu-id="be447-185">This guarantees that hello outputs of reduce i are all less than hello output of reduce i+1.</span></span>
3. <span data-ttu-id="be447-186">**TeraValidate** é um programa MapReduce que valida essa saída Olá global é classificado.</span><span class="sxs-lookup"><span data-stu-id="be447-186">**TeraValidate** is a MapReduce program that validates that hello output is globally sorted.</span></span> <span data-ttu-id="be447-187">Ele cria um mapa por arquivo no diretório de saída de hello e cada mapa garante que cada chave é menor ou igual a toohello anterior.</span><span class="sxs-lookup"><span data-stu-id="be447-187">It creates one map per file in hello output directory, and each map ensures that each key is less than or equal toohello previous one.</span></span> <span data-ttu-id="be447-188">função de mapa Hello também gera registros de saudação primeiro e último chaves de cada arquivo e Olá reduzem função garante que Olá primeira chave de arquivo i é maior que a chave do último Olá de i-1 de arquivo.</span><span class="sxs-lookup"><span data-stu-id="be447-188">hello map function also generates records of hello first and last keys of each file, and hello reduce function ensures that hello first key of file i is greater than hello last key of file i-1.</span></span> <span data-ttu-id="be447-189">Todos os problemas são relatados como uma saída de hello reduzir com chaves de saudação que estão fora de ordem.</span><span class="sxs-lookup"><span data-stu-id="be447-189">Any problems are reported as an output of hello reduce with hello keys that are out of order.</span></span>

<span data-ttu-id="be447-190">saudação de entrada e o formato de saída, usado por todos os três aplicativos lê e grava arquivos de texto de saudação no formato correto de saudação.</span><span class="sxs-lookup"><span data-stu-id="be447-190">hello input and output format, used by all three applications, reads and writes hello text files in hello right format.</span></span> <span data-ttu-id="be447-191">reduzir a saída Olá Olá replicação definiu too1, em vez de padrão de saudação 3, como o concurso de benchmark Olá não exige que os dados de saída Olá ser replicados em nós toomultiple.</span><span class="sxs-lookup"><span data-stu-id="be447-191">hello output of hello reduce has replication set too1, instead of hello default 3, because hello benchmark contest does not require that hello output data be replicated on toomultiple nodes.</span></span>

<span data-ttu-id="be447-192">Exemplo hello, cada tooone correspondente de programas de MapReduce Olá descrito na introdução Olá necessários três tarefas:</span><span class="sxs-lookup"><span data-stu-id="be447-192">Three tasks are required by hello sample, each corresponding tooone of hello MapReduce programs described in hello introduction:</span></span>

1. <span data-ttu-id="be447-193">Gerar dados Olá para classificação executando Olá **TeraGen** trabalho MapReduce.</span><span class="sxs-lookup"><span data-stu-id="be447-193">Generate hello data for sorting by running hello **TeraGen** MapReduce job.</span></span>
2. <span data-ttu-id="be447-194">Classificar dados saudação executando Olá **TeraSort** trabalho MapReduce.</span><span class="sxs-lookup"><span data-stu-id="be447-194">Sort hello data by running hello **TeraSort** MapReduce job.</span></span>
3. <span data-ttu-id="be447-195">Confirme que os dados de saudação foram classificados corretamente executando Olá **TeraValidate** trabalho MapReduce.</span><span class="sxs-lookup"><span data-stu-id="be447-195">Confirm that hello data has been correctly sorted by running hello **TeraValidate** MapReduce job.</span></span>

<span data-ttu-id="be447-196">**trabalhos de saudação toosubmit**</span><span class="sxs-lookup"><span data-stu-id="be447-196">**toosubmit hello jobs**</span></span>

* <span data-ttu-id="be447-197">Siga o procedimento Olá [palavras contagem - Java](#word-count-java), e use Olá definições de trabalho a seguir:</span><span class="sxs-lookup"><span data-stu-id="be447-197">Follow hello procedure in [Word count - Java](#word-count-java), and use hello following job definitions:</span></span>

    ```powershell
    $teragen = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teragen" `
                                -Arguments "-Dmapred.map.tasks=50", "100000000", "/example/data/10GB-sort-input"

    $terasort = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "terasort" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-input", "/example/data/10GB-sort-output"

    $teravalidate = New-AzureRmHDInsightMapReduceJobDefinition `
                                -JarFile "/example/jars/hadoop-mapreduce-examples.jar" `
                                -ClassName "teravalidate" `
                                -Arguments "-Dmapred.map.tasks=50", "-Dmapred.reduce.tasks=25", "/example/data/10GB-sort-output", "/example/data/10GB-sort-validate"
    ```

## <a name="next-steps"></a><span data-ttu-id="be447-198">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="be447-198">Next steps</span></span>
<span data-ttu-id="be447-199">Desse artigo e artigos de saudação em cada um dos exemplos de saudação, você aprendeu como exemplos de saudação toorun incluídos com hello clusters HDInsight usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="be447-199">From this article and hello articles in each of hello samples, you learned how toorun hello samples included with hello HDInsight clusters by using Azure PowerShell.</span></span> <span data-ttu-id="be447-200">Para tutoriais sobre como usar o Pig, Hive e MapReduce com HDInsight, consulte Olá seguintes tópicos:</span><span class="sxs-lookup"><span data-stu-id="be447-200">For tutorials about using Pig, Hive, and MapReduce with HDInsight, see hello following topics:</span></span>

* <span data-ttu-id="be447-201">[Começar a usar Hadoop com Hive no uso de celular tooanalyze HDInsight][hdinsight-get-started]</span><span class="sxs-lookup"><span data-stu-id="be447-201">[Get started using Hadoop with Hive in HDInsight tooanalyze mobile handset use][hdinsight-get-started]</span></span>
* <span data-ttu-id="be447-202">[Usar o Pig com Hadoop no HDInsight][hdinsight-use-pig]</span><span class="sxs-lookup"><span data-stu-id="be447-202">[Use Pig with Hadoop on HDInsight][hdinsight-use-pig]</span></span>
* <span data-ttu-id="be447-203">[Usar o Hive com Hadoop no HDInsight][hdinsight-use-hive]</span><span class="sxs-lookup"><span data-stu-id="be447-203">[Use Hive with Hadoop on HDInsight][hdinsight-use-hive]</span></span>
* <span data-ttu-id="be447-204">[Enviar trabalhos Hadoop no HDInsight][hdinsight-submit-jobs]</span><span class="sxs-lookup"><span data-stu-id="be447-204">[Submit Hadoop Jobs in HDInsight][hdinsight-submit-jobs]</span></span>
* <span data-ttu-id="be447-205">[Documentação do SDK do Azure HDInsight][hdinsight-sdk-documentation]</span><span class="sxs-lookup"><span data-stu-id="be447-205">[Azure HDInsight SDK documentation][hdinsight-sdk-documentation]</span></span>

## <a name="appendix-a---hello-word-count-source-code"></a><span data-ttu-id="be447-206">Apêndice A - Olá código-fonte contagem palavra</span><span class="sxs-lookup"><span data-stu-id="be447-206">Appendix A - hello Word count source code</span></span>

```java
package org.apache.hadoop.examples;
import java.io.IOException;
import java.util.StringTokenizer;
import org.apache.hadoop.conf.Configuration;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.IntWritable;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapreduce.Job;
import org.apache.hadoop.mapreduce.Mapper;
import org.apache.hadoop.mapreduce.Reducer;
import org.apache.hadoop.mapreduce.lib.input.FileInputFormat;
import org.apache.hadoop.mapreduce.lib.output.FileOutputFormat;
import org.apache.hadoop.util.GenericOptionsParser;

public class WordCount {

    public static class TokenizerMapper
    extends Mapper<Object, Text, Text, IntWritable>{

private final static IntWritable one = new IntWritable(1);
private Text word = new Text();

public void map(Object key, Text value, Context context
                ) throws IOException, InterruptedException {
    StringTokenizer itr = new StringTokenizer(value.toString());
    while (itr.hasMoreTokens()) {
    word.set(itr.nextToken());
    context.write(word, one);
        }
    }
    }

    public static class IntSumReducer
    extends Reducer<Text,IntWritable,Text,IntWritable> {
private IntWritable result = new IntWritable();

public void reduce(Text key, Iterable<IntWritable> values,
                    Context context
                    ) throws IOException, InterruptedException {
    int sum = 0;
    for (IntWritable val : values) {
    sum += val.get();
    }
    result.set(sum);
    context.write(key, result);
    }
    }

    public static void main(String[] args) throws Exception {
Configuration conf = new Configuration();
String[] otherArgs = new GenericOptionsParser(conf, args).getRemainingArgs();
if (otherArgs.length != 2) {
    System.err.println("Usage: wordcount <in> <out>");
    System.exit(2);
    }
Job job = new Job(conf, "word count");
job.setJarByClass(WordCount.class);
job.setMapperClass(TokenizerMapper.class);
job.setCombinerClass(IntSumReducer.class);
job.setReducerClass(IntSumReducer.class);
job.setOutputKeyClass(Text.class);
job.setOutputValueClass(IntWritable.class);
FileInputFormat.addInputPath(job, new Path(otherArgs[0]));
FileOutputFormat.setOutputPath(job, new Path(otherArgs[1]));
System.exit(job.waitForCompletion(true) ? 0 : 1);
    }
    }
```

## <a name="appendix-b---hello-word-count-streaming-source-code"></a><span data-ttu-id="be447-207">Apêndice B - contagem de palavras Olá streaming código-fonte</span><span class="sxs-lookup"><span data-stu-id="be447-207">Appendix B - hello word count streaming source code</span></span>
<span data-ttu-id="be447-208">programa de MapReduce Olá usa aplicativo de cat.exe hello como um texto de saudação do mapeamento interface toostream no console de saudação e aplicativo de wc.exe hello Olá reduzir o número de saudação toocount interface de palavras que são transmitidas de um documento.</span><span class="sxs-lookup"><span data-stu-id="be447-208">hello MapReduce program uses hello cat.exe application as a mapping interface toostream hello text into hello console and hello wc.exe application as hello reduce interface toocount hello number of words that are streamed from a document.</span></span> <span data-ttu-id="be447-209">Mapeador de saudação e Redutor leem caracteres, linha por linha, Olá padrão do fluxo de entrada (stdin) e escrever toohello fluxo de saída padrão (stdout).</span><span class="sxs-lookup"><span data-stu-id="be447-209">Both hello mapper and reducer read characters, line-by-line, from hello standard input stream (stdin) and write toohello standard output stream (stdout).</span></span>

```csharp
// hello source code for hello cat.exe (Mapper).

using System;
using System.IO;

namespace cat
{
    class cat
    {
        static void Main(string[] args)
        {
            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            string line;
            char[] separators = { ' ', '\n'};
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split(separators);
                foreach (var word in words)
                {
                    Console.WriteLine("{0}\t1", word);
                }
            }
        }
    }
}
```

<span data-ttu-id="be447-210">Olá código mapeador Olá cat.cs arquivo usa uma [StreamReader] [ streamreader] tooread caracteres de Olá Olá entrada fluxo toohello do console do, que, em seguida, grava Olá fluxo de saída padrão de toohello de fluxo do objeto com hello estático [console. WriteLine] [ console-writeline] método.</span><span class="sxs-lookup"><span data-stu-id="be447-210">hello mapper code in hello cat.cs file uses a [StreamReader][streamreader] object tooread hello characters of hello incoming stream toohello console, which then writes hello stream toohello standard output stream with hello static [Console.Writeline][console-writeline] method.</span></span>

```csharp
// hello source code for wc.exe (Reducer) is:

using System;
using System.IO;
using System.Linq;
using System.Collections;

namespace wc
{
    class wc
    {
        static void Main(string[] args)
        {
            string line;

            if (args.Length > 0)
            {
                Console.SetIn(new StreamReader(args[0]));
            }

            Hashtable wordCount = new Hashtable();
            while ((line = Console.ReadLine()) != null)
            {
                string[] words = line.Split('\t');

                string key = words[0];

                if (wordCount.ContainsKey(key) == true)
                {
                    int n = Convert.ToInt32(wordCount[key]);
                    wordCount[key] = Convert.ToString(n + 1);
                }
                else
                {
                    wordCount[key] = words[1];
                }
            }
            foreach (var key in wordCount.Keys)
            {
                Console.WriteLine("{0} {1}", key, wordCount[key]);
            }
        }
    }
}
```

<span data-ttu-id="be447-211">Olá código Redutor Olá wc.cs arquivo usa uma [StreamReader] [ streamreader] tooread caracteres saudação padrão do fluxo de entrada que foram saída pelo mapeador de cat.exe de saudação do objeto.</span><span class="sxs-lookup"><span data-stu-id="be447-211">hello reducer code in hello wc.cs file uses a [StreamReader][streamreader]   object tooread characters from hello standard input stream that have been output by hello cat.exe mapper.</span></span> <span data-ttu-id="be447-212">Medida que lê caracteres de saudação com hello [console. WriteLine] [ console-writeline] método, ele conta palavras Olá contando espaços e caracteres de final de linha no final de saudação de cada palavra.</span><span class="sxs-lookup"><span data-stu-id="be447-212">As it reads hello characters with hello [Console.Writeline][console-writeline] method, it counts hello words by counting spaces and end-of-line characters at hello end of each word.</span></span> <span data-ttu-id="be447-213">Ele grava Olá total toohello fluxo de saída padrão com hello [console. WriteLine] [ console-writeline] método.</span><span class="sxs-lookup"><span data-stu-id="be447-213">It then writes hello total toohello standard output stream with hello [Console.Writeline][console-writeline] method.</span></span>

## <a name="appendix-c---hello-pi-estimator-source-code"></a><span data-ttu-id="be447-214">Apêndice C - Olá código-fonte avaliador Pi</span><span class="sxs-lookup"><span data-stu-id="be447-214">Appendix C - hello Pi estimator source code</span></span>
<span data-ttu-id="be447-215">Avaliador de pi Olá código Java que contém funções de mapeador e Redutor hello está disponível para inspeção abaixo.</span><span class="sxs-lookup"><span data-stu-id="be447-215">hello pi estimator Java code that contains hello mapper and reducer functions is available for inspection below.</span></span> <span data-ttu-id="be447-216">programa de mapeador de Hello gera um número especificado de pontos colocado aleatório dentro de um quadrado da unidade de e, em seguida, calcula o número de saudação desses pontos que estão dentro de círculo de saudação.</span><span class="sxs-lookup"><span data-stu-id="be447-216">hello mapper program generates a specified number of points placed at random inside of a unit square and then counts hello number of those points that are inside hello circle.</span></span> <span data-ttu-id="be447-217">programa do Redutor Olá acumula pontos contados por mapeadores de saudação e, em seguida, calcula o valor Olá de pi do 4R de fórmula hello, onde R é a taxa de saudação do número de saudação de pontos contados dentro Olá círculo toohello número total de pontos que estão dentro do quadrado hello.</span><span class="sxs-lookup"><span data-stu-id="be447-217">hello reducer program accumulates points counted by hello mappers and then estimates hello value of pi from hello formula 4R, where R is hello ratio of hello number of points counted inside hello circle toohello total number of points that are within hello square.</span></span>

```java
/**
* Licensed toohello Apache Software Foundation (ASF) under one
* or more contributor license agreements. See hello NOTICE file
* distributed with this work for additional information
* regarding copyright ownership. hello ASF licenses this file
* tooyou under hello Apache License, Version 2.0 (the
* "License"); you may not use this file except in compliance
* with hello License. You may obtain a copy of hello License at
*
* http://www.apache.org/licenses/LICENSE-2.0
*
* Unless required by applicable law or agreed tooin writing, software
* distributed under hello License is distributed on an "AS IS" BASIS,
* WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or     implied.
* See hello License for hello specific language governing permissions and
* limitations under hello License.
*/

package org.apache.hadoop.examples;

import java.io.IOException;
import java.math.BigDecimal;
import java.util.Iterator;

import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.BooleanWritable;
import org.apache.hadoop.io.LongWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Writable;
import org.apache.hadoop.io.WritableComparable;
import org.apache.hadoop.io.SequenceFile.CompressionType;
import org.apache.hadoop.mapred.FileInputFormat;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.MapReduceBase;
import org.apache.hadoop.mapred.Mapper;
import org.apache.hadoop.mapred.OutputCollector;
import org.apache.hadoop.mapred.Reducer;
import org.apache.hadoop.mapred.Reporter;
import org.apache.hadoop.mapred.SequenceFileInputFormat;
import org.apache.hadoop.mapred.SequenceFileOutputFormat;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

//A Map-reduce program tooestimate hello value of Pi
//using quasi-Monte Carlo method.
//
//Mapper:
//Generate points in a unit square
//and then count points inside/outside of hello inscribed circle of hello square.
//
//Reducer:
//Accumulate points inside/outside results from hello mappers.
//Let numTotal = numInside + numOutside.
//hello fraction numInside/numTotal is a rational approximation of
//hello value (Area of hello circle)/(Area of hello square),
//where hello area of hello inscribed circle is Pi/4
//and hello area of unit square is 1.
//Then, Pi is estimated value toobe 4(numInside/numTotal).
//

public class PiEstimator extends Configured implements Tool {
//tmp directory for input/output
static private final Path TMP_DIR = new Path(
PiEstimator.class.getSimpleName() + "_TMP_3_141592654");

//2-dimensional Halton sequence {H(i)},
//where H(i) is a 2-dimensional point and i >= 1 is hello index.
//Halton sequence is used toogenerate sample points for Pi estimation.
private static class HaltonSequence {
// Bases
static final int[] P = {2, 3};
//Maximum number of digits allowed
static final int[] K = {63, 40};

private long index;
private double[] x;
private double[][] q;
private int[][] d;

//Initialize tooH(startindex),
//so hello sequence begins with H(startindex+1).
HaltonSequence(long startindex) {
index = startindex;
x = new double[K.length];
q = new double[K.length][];
d = new int[K.length][];
for(int i = 0; i < K.length; i++) {
q[i] = new double[K[i]];
d[i] = new int[K[i]];
}

for(int i = 0; i < K.length; i++) {
long k = index;
x[i] = 0;

for(int j = 0; j < K[i]; j++) {
q[i][j] = (j == 0? 1.0: q[i][j-1])/P[i];
d[i][j] = (int)(k % P[i]);
k = (k - d[i][j])/P[i];
x[i] += d[i][j] * q[i][j];
}
}
}

//Compute next point.
//Assume hello current point is H(index).
//Compute H(index+1).
//@return a 2-dimensional point with coordinates in [0,1)^2
double[] nextPoint() {
index++;
for(int i = 0; i < K.length; i++) {
for(int j = 0; j < K[i]; j++) {
d[i][j]++;
x[i] += q[i][j];
if (d[i][j] < P[i]) {
break;
}
d[i][j] = 0;
x[i] -= (j == 0? 1.0: q[i][j-1]);
}
}
return x;
}
}

//Mapper class for Pi estimation.
//Generate points in a unit square and then
//count points inside/outside of hello inscribed circle of hello square.
public static class PiMapper extends MapReduceBase
implements Mapper<LongWritable, LongWritable, BooleanWritable, LongWritable> {

//Map method.
//@param offset samples starting from hello (offset+1)th sample.
//@param size hello number of samples for this map
//@param out output {ture->numInside, false->numOutside}
//@param reporter
public void map(LongWritable offset,
LongWritable size,
OutputCollector<BooleanWritable, LongWritable> out,
Reporter reporter) throws IOException {

final HaltonSequence haltonsequence = new HaltonSequence(offset.get());
long numInside = 0L;
long numOutside = 0L;

for(long i = 0; i < size.get(); ) {
//generate points in a unit square
final double[] point = haltonsequence.nextPoint();

//count points inside/outside of hello inscribed circle of hello square
final double x = point[0] - 0.5;
final double y = point[1] - 0.5;
if (x*x + y*y > 0.25) {
numOutside++;
} else {
numInside++;
}

//report status
i++;
if (i % 1000 == 0) {
reporter.setStatus("Generated " + i + " samples.");
}
}

//output map results
out.collect(new BooleanWritable(true), new LongWritable(numInside));
out.collect(new BooleanWritable(false), new LongWritable(numOutside));
}
}

//Reducer class for Pi estimation.
//Accumulate points inside/outside results from hello mappers.
public static class PiReducer extends MapReduceBase
implements Reducer<BooleanWritable, LongWritable, WritableComparable<?>, Writable> {

private long numInside = 0;
private long numOutside = 0;
private JobConf conf; //configuration for accessing hello file system

//Store job configuration.
@Override
public void configure(JobConf job) {
conf = job;
}

// Accumulate number of points inside/outside results from hello mappers.
// @param isInside Is hello points inside?
// @param values An iterator tooa list of point counts
// @param output dummy, not used here.
// @param reporter

public void reduce(BooleanWritable isInside,
Iterator<LongWritable> values,
OutputCollector<WritableComparable<?>, Writable> output,
Reporter reporter) throws IOException {
if (isInside.get()) {
for(; values.hasNext(); numInside += values.next().get());
} else {
for(; values.hasNext(); numOutside += values.next().get());
}
}

//Reduce task done, write output tooa file.
@Override
public void close() throws IOException {
//write output tooa file
Path outDir = new Path(TMP_DIR, "out");
Path outFile = new Path(outDir, "reduce-out");
FileSystem fileSys = FileSystem.get(conf);
SequenceFile.Writer writer = SequenceFile.createWriter(fileSys, conf,
outFile, LongWritable.class, LongWritable.class,
CompressionType.NONE);
writer.append(new LongWritable(numInside), new LongWritable(numOutside));
writer.close();
}
}

//Run a map/reduce job for estimating Pi.
//@return hello estimated value of Pi.
public static BigDecimal estimate(int numMaps, long numPoints, JobConf jobConf
)
throws IOException {
//setup job conf
jobConf.setJobName(PiEstimator.class.getSimpleName());

jobConf.setInputFormat(SequenceFileInputFormat.class);

jobConf.setOutputKeyClass(BooleanWritable.class);
jobConf.setOutputValueClass(LongWritable.class);
jobConf.setOutputFormat(SequenceFileOutputFormat.class);

jobConf.setMapperClass(PiMapper.class);
jobConf.setNumMapTasks(numMaps);

jobConf.setReducerClass(PiReducer.class);
jobConf.setNumReduceTasks(1);

// turn off speculative execution, because DFS doesn't handle
// multiple writers toohello same file.
jobConf.setSpeculativeExecution(false);

//setup input/output directories
final Path inDir = new Path(TMP_DIR, "in");
final Path outDir = new Path(TMP_DIR, "out");
FileInputFormat.setInputPaths(jobConf, inDir);
FileOutputFormat.setOutputPath(jobConf, outDir);

final FileSystem fs = FileSystem.get(jobConf);
if (fs.exists(TMP_DIR)) {
throw new IOException("Tmp directory " + fs.makeQualified(TMP_DIR)
+ " already exists. Remove it first.");
}
if (!fs.mkdirs(inDir)) {
throw new IOException("Cannot create input directory " + inDir);
}

//generate an input file for each map task
try {
for(int i=0; i < numMaps; ++i) {
final Path file = new Path(inDir, "part"+i);
final LongWritable offset = new LongWritable(i * numPoints);
final LongWritable size = new LongWritable(numPoints);
final SequenceFile.Writer writer = SequenceFile.createWriter(
fs, jobConf, file,
LongWritable.class, LongWritable.class, CompressionType.NONE);
try {
writer.append(offset, size);
} finally {
writer.close();
}
System.out.println("Wrote input for Map #"+i);
}

//start a map/reduce job
System.out.println("Starting Job");
final long startTime = System.currentTimeMillis();
JobClient.runJob(jobConf);
final double duration = (System.currentTimeMillis() - startTime)/1000.0;
System.out.println("Job Finished in " + duration + " seconds");

//read outputs
Path inFile = new Path(outDir, "reduce-out");
LongWritable numInside = new LongWritable();
LongWritable numOutside = new LongWritable();
SequenceFile.Reader reader = new SequenceFile.Reader(fs, inFile, jobConf);
try {
reader.next(numInside, numOutside);
} finally {
reader.close();
}

//compute estimated value
return BigDecimal.valueOf(4).setScale(20)
.multiply(BigDecimal.valueOf(numInside.get()))
.divide(BigDecimal.valueOf(numMaps))
.divide(BigDecimal.valueOf(numPoints));
} finally {
fs.delete(TMP_DIR, true);
}
}

//Parse arguments and then runs a map/reduce job.
//Print output in standard out.
//@return a non-zero if there is an error. Otherwise, return 0.
public int run(String[] args) throws Exception {
if (args.length != 2) {
System.err.println("Usage: "+getClass().getName()+" <nMaps> <nSamples>");
ToolRunner.printGenericCommandUsage(System.err);
return -1;
}

final int nMaps = Integer.parseInt(args[0]);
final long nSamples = Long.parseLong(args[1]);

System.out.println("Number of Maps = " + nMaps);
System.out.println("Samples per Map = " + nSamples);

final JobConf jobConf = new JobConf(getConf(), getClass());
System.out.println("Estimated value of Pi is "
+ estimate(nMaps, nSamples, jobConf));
return 0;
}

//main method for running it as a stand alone command.
public static void main(String[] argv) throws Exception {
System.exit(ToolRunner.run(null, new PiEstimator(), argv));
}
}
```

## <a name="appendix-d---hello-10gb-graysort-source-code"></a><span data-ttu-id="be447-218">Apêndice D - código-fonte graysort Olá 10gb</span><span class="sxs-lookup"><span data-stu-id="be447-218">Appendix D - hello 10gb graysort source code</span></span>
<span data-ttu-id="be447-219">código Olá Olá programa TeraSort MapReduce é apresentado para inspeção nesta seção.</span><span class="sxs-lookup"><span data-stu-id="be447-219">hello code for hello TeraSort MapReduce program is presented for inspection in this section.</span></span>

```java
/**
    * Licensed toohello Apache Software Foundation (ASF) under one
    * or more contributor license agreements.  See hello NOTICE file
    * distributed with this work for additional information
    * regarding copyright ownership.  hello ASF licenses this file
    * tooyou under hello Apache License, Version 2.0 (the
    * "License"); you may not use this file except in compliance
    * with hello License.  You may obtain a copy of hello License at
    *
    *     http://www.apache.org/licenses/LICENSE-2.0
    *
    * Unless required by applicable law or agreed tooin writing, software
    * distributed under hello License is distributed on an "AS IS" BASIS,
    * WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
    * See hello License for hello specific language governing permissions and
    * limitations under hello License.
    */

package org.apache.hadoop.examples.terasort;

import java.io.IOException;
import java.io.PrintStream;
import java.net.URI;
import java.util.ArrayList;
import java.util.List;

import org.apache.commons.logging.Log;
import org.apache.commons.logging.LogFactory;
import org.apache.hadoop.conf.Configured;
import org.apache.hadoop.filecache.DistributedCache;
import org.apache.hadoop.fs.FileSystem;
import org.apache.hadoop.fs.Path;
import org.apache.hadoop.io.NullWritable;
import org.apache.hadoop.io.SequenceFile;
import org.apache.hadoop.io.Text;
import org.apache.hadoop.mapred.FileOutputFormat;
import org.apache.hadoop.mapred.JobClient;
import org.apache.hadoop.mapred.JobConf;
import org.apache.hadoop.mapred.Partitioner;
import org.apache.hadoop.util.Tool;
import org.apache.hadoop.util.ToolRunner;

/**
    * Generates hello sampled split points, launches hello job,
    * and waits for it toofinish.
    * <p>
    * toorun hello program:
    * <b>bin/hadoop jar hadoop-examples-*.jar terasort in-dir out-dir</b>
    */

public class TeraSort extends Configured implements Tool {
    private static final Log LOG = LogFactory.getLog(TeraSort.class);

    /**
    * A partitioner that splits text keys into roughly equal
    * partitions in a global sorted order.
    */

    static class TotalOrderPartitioner implements Partitioner<Text,Text>{
    private TrieNode trie;
    private Text[] splitPoints;

    /**
        * A generic trie node
        */
    static abstract class TrieNode {
        private int level;
        TrieNode(int level) {
        this.level = level;
        }
        abstract int findPartition(Text key);
        abstract void print(PrintStream strm) throws IOException;
        int getLevel() {
        return level;
        }
    }

    /**
        * An inner trie node that contains 256 children based on hello next
        * character.
        */
    static class InnerTrieNode extends TrieNode {
        private TrieNode[] child = new TrieNode[256];

        InnerTrieNode(int level) {
        super(level);
        }
        int findPartition(Text key) {
        int level = getLevel();
        if (key.getLength() <= level) {
            return child[0].findPartition(key);
        }
        return child[key.getBytes()[level]].findPartition(key);
        }
        void setChild(int idx, TrieNode child) {
        this.child[idx] = child;
        }
        void print(PrintStream strm) throws IOException {
        for(int ch=0; ch < 255; ++ch) {
            for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
            }
            strm.print(ch);
            strm.println(" ->");
            if (child[ch] != null) {
            child[ch].print(strm);
            }
        }
        }
    }

    /**
        * A leaf trie node that does string compares toofigure out where hello given
        * key belongs between lower..upper.
        */
    static class LeafTrieNode extends TrieNode {
        int lower;
        int upper;
        Text[] splitPoints;
        LeafTrieNode(int level, Text[] splitPoints, int lower, int upper) {
        super(level);
        this.splitPoints = splitPoints;
        this.lower = lower;
        this.upper = upper;
        }
        int findPartition(Text key) {
        for(int i=lower; i<upper; ++i) {
            if (splitPoints[i].compareTo(key) >= 0) {
            return i;
            }
        }
        return upper;
        }
        void print(PrintStream strm) throws IOException {
        for(int i = 0; i < 2*getLevel(); ++i) {
            strm.print(' ');
        }
        strm.print(lower);
        strm.print(", ");
        strm.println(upper);
        }
    }

    /**
        * Read hello cut points from hello given sequence file.
        * @param fs hello file system
        * @param p hello path tooread
        * @param job hello job config
        * @return hello strings toosplit hello partitions on
        * @throws IOException
        */
    private static Text[] readPartitions(FileSystem fs, Path p,
                                            JobConf job) throws IOException {
        SequenceFile.Reader reader = new SequenceFile.Reader(fs, p, job);
        List<Text> parts = new ArrayList<Text>();
        Text key = new Text();
        NullWritable value = NullWritable.get();
        while (reader.next(key, value)) {
        parts.add(key);
        key = new Text();
        }
        reader.close();
        return parts.toArray(new Text[parts.size()]);
    }

    /**
        * Given a sorted set of cut points, build a trie that will find hello correct
        * partition quickly.
        * @param splits hello list of cut points
        * @param lower hello lower bound of partitions 0..numPartitions-1
        * @param upper hello upper bound of partitions 0..numPartitions-1
        * @param prefix hello prefix that we have already checked against
        * @param maxDepth hello maximum depth we will build a trie for
        * @return hello trie node that will divide hello splits correctly
        */
    private static TrieNode buildTrie(Text[] splits, int lower, int upper,
                                        Text prefix, int maxDepth) {
        int depth = prefix.getLength();
        if (depth >= maxDepth || lower == upper) {
        return new LeafTrieNode(depth, splits, lower, upper);
        }
        InnerTrieNode result = new InnerTrieNode(depth);
        Text trial = new Text(prefix);
        // append an extra byte on toohello prefix
        trial.append(new byte[1], 0, 1);
        int currentBound = lower;
        for(int ch = 0; ch < 255; ++ch) {
        trial.getBytes()[depth] = (byte) (ch + 1);
        lower = currentBound;
        while (currentBound < upper) {
            if (splits[currentBound].compareTo(trial) >= 0) {
            break;
            }
            currentBound += 1;
        }
        trial.getBytes()[depth] = (byte) ch;
        result.child[ch] = buildTrie(splits, lower, currentBound, trial,
                                        maxDepth);
        }
        // pick up hello rest
        trial.getBytes()[depth] = 127;
        result.child[255] = buildTrie(splits, currentBound, upper, trial,
                                    maxDepth);
        return result;
    }

    public void configure(JobConf job) {
        try {
        FileSystem fs = FileSystem.getLocal(job);
        Path partFile = new Path(TeraInputFormat.PARTITION_FILENAME);
        splitPoints = readPartitions(fs, partFile, job);
        trie = buildTrie(splitPoints, 0, splitPoints.length, new Text(), 2);
        } catch (IOException ie) {
        throw new IllegalArgumentException("can't read paritions file", ie);
        }
    }

    public TotalOrderPartitioner() {
    }

    public int getPartition(Text key, Text value, int numPartitions) {
        return trie.findPartition(key);
    }

    }

    public int run(String[] args) throws Exception {
    LOG.info("starting");
    JobConf job = (JobConf) getConf();
    Path inputDir = new Path(args[0]);
    inputDir = inputDir.makeQualified(inputDir.getFileSystem(job));
    Path partitionFile = new Path(inputDir, TeraInputFormat.PARTITION_FILENAME);
    URI partitionUri = new URI(partitionFile.toString() +
                                "#" + TeraInputFormat.PARTITION_FILENAME);
    TeraInputFormat.setInputPaths(job, new Path(args[0]));
    FileOutputFormat.setOutputPath(job, new Path(args[1]));
    job.setJobName("TeraSort");
    job.setJarByClass(TeraSort.class);
    job.setOutputKeyClass(Text.class);
    job.setOutputValueClass(Text.class);
    job.setInputFormat(TeraInputFormat.class);
    job.setOutputFormat(TeraOutputFormat.class);
    job.setPartitionerClass(TotalOrderPartitioner.class);
    TeraInputFormat.writePartitionFile(job, partitionFile);
    DistributedCache.addCacheFile(partitionUri, job);
    DistributedCache.createSymlink(job);
    job.setInt("dfs.replication", 1);
    TeraOutputFormat.setFinalSync(job, true);
    JobClient.runJob(job);
    LOG.info("done");
    return 0;
    }

    /**
    * @param args
    */

    public static void main(String[] args) throws Exception {
    int res = ToolRunner.run(new JobConf(), new TeraSort(), args);
    System.exit(res);
    }
}
```

[hdinsight-sdk-documentation]: https://msdn.microsoft.com/library/azure/dn479185.aspx

[hdinsight-submit-jobs]: hdinsight-submit-hadoop-jobs-programmatically.md
[hdinsight-introduction]: hdinsight-hadoop-introduction.md

[powershell-install-configure]: /powershell/azureps-cmdlets-docs

[hdinsight-get-started]: hdinsight-hadoop-linux-tutorial-get-started.md

[hdinsight-samples]: hdinsight-run-samples.md
[hdinsight-sample-10gb-graysort]: #hdinsight-sample-10gb-graysort
[hdinsight-sample-csharp-streaming]: #hdinsight-sample-csharp-streaming
[hdinsight-sample-pi-estimator]: #hdinsight-sample-pi-estimator
[hdinsight-sample-wordcount]: #hdinsight-sample-wordcount

[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md

[streamreader]: http://msdn.microsoft.com/library/system.io.streamreader.aspx
[console-writeline]: http://msdn.microsoft.com/library/system.console.writeline
[stdin-stdout-stderr]: https://msdn.microsoft.com/library/3x292kth.aspx
