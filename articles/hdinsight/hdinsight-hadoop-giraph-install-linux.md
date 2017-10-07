---
title: aaaInstall e usar Giraph no HDInsight (Hadoop) - Azure | Microsoft Docs
description: "Saiba como tooinstall Giraph no HDInsight baseados em Linux clusters usando ações de Script. Ações de script permite que você toocustomize Olá cluster durante a criação, alteração de configuração de cluster ou instalando serviços e utilitários."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 9fcac906-8f06-4002-9fe8-473e42f8fd0f
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/31/2017
ms.author: larryfr
ms.openlocfilehash: 0f195b65cebf5e24d1808ef33b95b4d362555521
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-tooprocess-large-scale-graphs"></a><span data-ttu-id="5871f-104">Instalar Giraph em clusters de HDInsight Hadoop e usar gráficos em grande escala do Giraph tooprocess</span><span class="sxs-lookup"><span data-stu-id="5871f-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph tooprocess large-scale graphs</span></span>

<span data-ttu-id="5871f-105">Saiba como tooinstall Giraph Apache em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5871f-105">Learn how tooinstall Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="5871f-106">recurso de ação de script de saudação do HDInsight permite que você toocustomize o cluster executando um script de bash.</span><span class="sxs-lookup"><span data-stu-id="5871f-106">hello script action feature of HDInsight allows you toocustomize your cluster by running a bash script.</span></span> <span data-ttu-id="5871f-107">Scripts podem ser usados toocustomize clusters durante e após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="5871f-107">Scripts can be used toocustomize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5871f-108">etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux.</span><span class="sxs-lookup"><span data-stu-id="5871f-108">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5871f-109">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5871f-109">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5871f-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5871f-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="5871f-111"><a name="whatis"></a>O que é Giraph</span><span class="sxs-lookup"><span data-stu-id="5871f-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="5871f-112">[Apache Giraph](http://giraph.apache.org/) permite gráfico tooperform processamento usando Hadoop e pode ser usado com o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5871f-112">[Apache Giraph](http://giraph.apache.org/) allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="5871f-113">Gráficos moldam as relações entre objetos.</span><span class="sxs-lookup"><span data-stu-id="5871f-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="5871f-114">Por exemplo, conexões de saudação entre roteadores em uma rede grande como Olá Internet ou relações entre as pessoas em redes sociais.</span><span class="sxs-lookup"><span data-stu-id="5871f-114">For example, hello connections between routers on a large network like hello Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="5871f-115">Processamento de gráfico permite que você tooreason sobre relações de saudação entre objetos em um gráfico, como:</span><span class="sxs-lookup"><span data-stu-id="5871f-115">Graph processing allows you tooreason about hello relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="5871f-116">Identificar possíveis amigos com base em suas relações atuais.</span><span class="sxs-lookup"><span data-stu-id="5871f-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="5871f-117">Identificando a rota mais curta Olá entre dois computadores em uma rede.</span><span class="sxs-lookup"><span data-stu-id="5871f-117">Identifying hello shortest route between two computers in a network.</span></span>

* <span data-ttu-id="5871f-118">Calculando a classificação de página Olá das páginas da Web.</span><span class="sxs-lookup"><span data-stu-id="5871f-118">Calculating hello page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="5871f-119">Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados - Microsoft Support ajuda tooisolate e resolver problemas relacionados toothese componentes.</span><span class="sxs-lookup"><span data-stu-id="5871f-119">Components provided with hello HDInsight cluster are fully supported - Microsoft Support helps tooisolate and resolve issues related toothese components.</span></span>
>
> <span data-ttu-id="5871f-120">Componentes personalizados, como Giraph, recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="5871f-120">Custom components, such as Giraph, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="5871f-121">Microsoft Support pode ser capaz de tooresolving problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="5871f-121">Microsoft Support may be able tooresolving hello issue.</span></span> <span data-ttu-id="5871f-122">Caso contrário, você deve consultar comunidades de software livre em que é possível encontrar conhecimento aprofundado sobre essa tecnologia.</span><span class="sxs-lookup"><span data-stu-id="5871f-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="5871f-123">Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="5871f-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-hello-script-does"></a><span data-ttu-id="5871f-124">O script hello faz</span><span class="sxs-lookup"><span data-stu-id="5871f-124">What hello script does</span></span>

<span data-ttu-id="5871f-125">Esse script executa Olá ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="5871f-125">This script performs hello following actions:</span></span>

* <span data-ttu-id="5871f-126">Instala Giraph muito`/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="5871f-126">Installs Giraph too`/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="5871f-127">Olá cópias `giraph-examples.jar` armazenamento de arquivos toodefault (WASB) para o cluster:`/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="5871f-127">Copies hello `giraph-examples.jar` file toodefault storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="5871f-128"><a name="install"></a>Instalar o Giraph usando Ações de Script</span><span class="sxs-lookup"><span data-stu-id="5871f-128"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="5871f-129">Tooinstall um script de exemplo Giraph em um cluster HDInsight está disponível em Olá local a seguir:</span><span class="sxs-lookup"><span data-stu-id="5871f-129">A sample script tooinstall Giraph on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="5871f-130">Esta seção fornece instruções sobre como toouse Olá script de exemplo durante a criação de cluster hello usando Olá portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="5871f-130">This section provides instructions on how toouse hello sample script while creating hello cluster by using hello Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="5871f-131">Uma ação de script pode ser aplicada usando qualquer um dos métodos a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="5871f-131">A script action can be applied using any of hello following methods:</span></span>
> * <span data-ttu-id="5871f-132">Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="5871f-132">Azure PowerShell</span></span>
> * <span data-ttu-id="5871f-133">Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="5871f-133">hello Azure CLI</span></span>
> * <span data-ttu-id="5871f-134">Olá HDInsight .NET SDK</span><span class="sxs-lookup"><span data-stu-id="5871f-134">hello HDInsight .NET SDK</span></span>
> * <span data-ttu-id="5871f-135">Modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="5871f-135">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="5871f-136">Você também pode aplicar o script ações tooalready clusters em execução.</span><span class="sxs-lookup"><span data-stu-id="5871f-136">You can also apply script actions tooalready running clusters.</span></span> <span data-ttu-id="5871f-137">Para saber mais, veja [Personalizar clusters HDInsight com as Ações de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5871f-137">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="5871f-138">Começar a criar um cluster usando as etapas de saudação em [clusters HDInsight baseados em Linux criar](hdinsight-hadoop-create-linux-clusters-portal.md), mas não conclua o processo de criação.</span><span class="sxs-lookup"><span data-stu-id="5871f-138">Start creating a cluster by using hello steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="5871f-139">Em Olá **configuração opcional** folha, selecione **ações de Script**e fornecer Olá informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="5871f-139">On hello **Optional Configuration** blade, select **Script Actions**, and provide hello following information:</span></span>

   * <span data-ttu-id="5871f-140">**NOME**: insira um nome amigável para a ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="5871f-140">**NAME**: Enter a friendly name for hello script action.</span></span>

   * <span data-ttu-id="5871f-141">**URI do SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="5871f-141">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="5871f-142">**CABEÇALHO**: marque esta entrada</span><span class="sxs-lookup"><span data-stu-id="5871f-142">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="5871f-143">**TRABALHO**: deixe esta entrada desmarcada</span><span class="sxs-lookup"><span data-stu-id="5871f-143">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="5871f-144">**ZOOKEEPER**: deixe esta entrada desmarcada</span><span class="sxs-lookup"><span data-stu-id="5871f-144">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="5871f-145">**PARÂMETROS**: deixe este campo em branco</span><span class="sxs-lookup"><span data-stu-id="5871f-145">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="5871f-146">Na parte inferior de saudação do hello **ações de Script**, use Olá **selecione** configuração de saudação do botão toosave.</span><span class="sxs-lookup"><span data-stu-id="5871f-146">At hello bottom of hello **Script Actions**, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="5871f-147">Por fim, use Olá **selecione** botão na parte inferior de saudação do hello **configuração opcional** informações de configuração opcional de saudação de toosave de folha.</span><span class="sxs-lookup"><span data-stu-id="5871f-147">Finally, use hello **Select** button at hello bottom of hello **Optional Configuration** blade toosave hello optional configuration information.</span></span>

4. <span data-ttu-id="5871f-148">Continuar a criar o cluster Olá conforme descrito em [clusters HDInsight baseados em Linux criar](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="5871f-148">Continue creating hello cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="5871f-149"><a name="usegiraph"></a>Como usar o Giraph no HDInsight?</span><span class="sxs-lookup"><span data-stu-id="5871f-149"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="5871f-150">Depois que o cluster Olá tiver sido criado, use Olá etapas toorun Olá SimpleShortestPathsComputation exemplo incluído com Giraph a seguir.</span><span class="sxs-lookup"><span data-stu-id="5871f-150">Once hello cluster has been created, use hello following steps toorun hello SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="5871f-151">Este exemplo usa Olá basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementação para localizar o caminho mais curto de saudação entre objetos em um gráfico.</span><span class="sxs-lookup"><span data-stu-id="5871f-151">This example uses hello basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding hello shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="5871f-152">Conecte o cluster do HDInsight toohello usando SSH:</span><span class="sxs-lookup"><span data-stu-id="5871f-152">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="5871f-153">Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5871f-153">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="5871f-154">Comando de uso a seguir de saudação toocreate um arquivo chamado **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="5871f-154">Use hello following command toocreate a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="5871f-155">Use Olá depois do texto como o conteúdo deste arquivo hello:</span><span class="sxs-lookup"><span data-stu-id="5871f-155">Use hello following text as hello contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="5871f-156">Esses dados descrevem uma relação entre objetos em um gráfico direcionado, usando o formato de saudação `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="5871f-156">This data describes a relationship between objects in a directed graph, by using hello format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="5871f-157">Cada linha representa uma relação entre um objeto `source_id` e um ou mais objetos `dest_id`.</span><span class="sxs-lookup"><span data-stu-id="5871f-157">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="5871f-158">Olá `edge_value` pode ser pensada como intensidade hello ou distância de conexão Olá entre `source_id` e `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="5871f-158">hello `edge_value` can be thought of as hello strength or distance of hello connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="5871f-159">Desenhado, e usando o valor de hello (ou peso) como a distância Olá entre objetos, dados saudação podem parecer com hello diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="5871f-159">Drawn out, and using hello value (or weight) as hello distance between objects, hello data might look like hello following diagram:</span></span>

    ![tiny_graph.txt Desenhado como círculos com linhas de distância variável entre](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="5871f-161">arquivo de saudação toosave, use **Ctrl + X**, em seguida, **Y**e, finalmente, **Enter** nome de arquivo hello tooaccept.</span><span class="sxs-lookup"><span data-stu-id="5871f-161">toosave hello file, use **Ctrl+X**, then **Y**, and finally **Enter** tooaccept hello file name.</span></span>

4. <span data-ttu-id="5871f-162">Use Olá seguintes dados de saudação do toostore no armazenamento primário para seu cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="5871f-162">Use hello following toostore hello data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="5871f-163">Execute o exemplo de SimpleShortestPathsComputation hello usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="5871f-163">Run hello SimpleShortestPathsComputation example using hello following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="5871f-164">parâmetros de saudação usados com este comando são descritos na Olá a tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="5871f-164">hello parameters used with this command are described in hello following table:</span></span>

   | <span data-ttu-id="5871f-165">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="5871f-165">Parameter</span></span> | <span data-ttu-id="5871f-166">O que faz</span><span class="sxs-lookup"><span data-stu-id="5871f-166">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="5871f-167">arquivo jar do Hello que contém exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5871f-167">hello jar file containing hello examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="5871f-168">classe de saudação usada toostart exemplos de saudação.</span><span class="sxs-lookup"><span data-stu-id="5871f-168">hello class used toostart hello examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="5871f-169">exemplo Hello que é usado.</span><span class="sxs-lookup"><span data-stu-id="5871f-169">hello example that is used.</span></span> <span data-ttu-id="5871f-170">Neste exemplo, ele computa o caminho mais curto de saudação entre ID 1 e todos os outros IDs no gráfico de saudação.</span><span class="sxs-lookup"><span data-stu-id="5871f-170">In this example, it computes hello shortest path between ID 1 and all other IDs in hello graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="5871f-171">Olá um nó principal para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="5871f-171">hello headnode for hello cluster.</span></span> |
   | `-vif` |<span data-ttu-id="5871f-172">Olá toouse de formato de entrada para os dados de entrada hello.</span><span class="sxs-lookup"><span data-stu-id="5871f-172">hello input format toouse for hello input data.</span></span> |
   | `-vip` |<span data-ttu-id="5871f-173">arquivo de dados de entrada Hello.</span><span class="sxs-lookup"><span data-stu-id="5871f-173">hello input data file.</span></span> |
   | `-vof` |<span data-ttu-id="5871f-174">saudação de formato de saída.</span><span class="sxs-lookup"><span data-stu-id="5871f-174">hello output format.</span></span> <span data-ttu-id="5871f-175">Nesse exemplo, a ID e o valor como texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="5871f-175">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="5871f-176">saudação de local de saída.</span><span class="sxs-lookup"><span data-stu-id="5871f-176">hello output location.</span></span> |
   | `-w 2` |<span data-ttu-id="5871f-177">número de saudação de trabalhadores toouse.</span><span class="sxs-lookup"><span data-stu-id="5871f-177">hello number of workers toouse.</span></span> <span data-ttu-id="5871f-178">Neste exemplo, 2.</span><span class="sxs-lookup"><span data-stu-id="5871f-178">In this example, 2.</span></span> |

    <span data-ttu-id="5871f-179">Para obter mais informações sobre esses e outros parâmetros usados com Giraph exemplos, consulte Olá [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="5871f-179">For more information on these, and other parameters used with Giraph samples, see hello [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="5871f-180">Quando tiver terminado de trabalho hello, resultados de saudação são armazenados em Olá **/example/out/shotestpaths** directory.</span><span class="sxs-lookup"><span data-stu-id="5871f-180">Once hello job has finished, hello results are stored in hello **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="5871f-181">Olá nomes de arquivo de saída começam com **parte-m -** e terminar com um número indicando Olá primeiro, segundo, arquivo etc.</span><span class="sxs-lookup"><span data-stu-id="5871f-181">hello output file names begin with **part-m-** and end with a number indicating hello first, second, etc. file.</span></span> <span data-ttu-id="5871f-182">Use Olá saída do comando tooview Olá a seguir:</span><span class="sxs-lookup"><span data-stu-id="5871f-182">Use hello following command tooview hello output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="5871f-183">saída de Hello deve aparecer semelhante toohello texto a seguir:</span><span class="sxs-lookup"><span data-stu-id="5871f-183">hello output should appear similar toohello following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="5871f-184">exemplo de SimpleShortestPathComputation Hello é toostart codificado com o objeto ID 1 e localizar Olá shortest path tooother objetos.</span><span class="sxs-lookup"><span data-stu-id="5871f-184">hello SimpleShortestPathComputation example is hard coded toostart with object ID 1 and find hello shortest path tooother objects.</span></span> <span data-ttu-id="5871f-185">saída de Hello está no formato de saudação do `destination_id` e `distance`.</span><span class="sxs-lookup"><span data-stu-id="5871f-185">hello output is in hello format of `destination_id` and `distance`.</span></span> <span data-ttu-id="5871f-186">Olá `distance` é Olá valor (ou peso) das bordas Olá percorridas entre o objeto ID 1 e ID de destino hello.</span><span class="sxs-lookup"><span data-stu-id="5871f-186">hello `distance` is hello value (or weight) of hello edges traveled between object ID 1 and hello target ID.</span></span>

    <span data-ttu-id="5871f-187">Visualizar esses dados, você pode verificar os resultados de saudação percorrerem caminhos mais curto Olá ID 1 e todos os outros objetos.</span><span class="sxs-lookup"><span data-stu-id="5871f-187">Visualizing this data, you can verify hello results by traveling hello shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="5871f-188">caminho mais curto de saudação entre ID 1 e 4 ID é 5.</span><span class="sxs-lookup"><span data-stu-id="5871f-188">hello shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="5871f-189">Esse valor é a distância total Olá entre <span style="color:orange">ID 1 e 3</span>e, em seguida, <span style="color:red">ID 3 e 4</span>.</span><span class="sxs-lookup"><span data-stu-id="5871f-189">This value is hello total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Desenho dos objetos como círculos com os percursos mais curtos entre](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="5871f-191">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5871f-191">Next steps</span></span>

* <span data-ttu-id="5871f-192">[Instalar e usar o Hue em clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5871f-192">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="5871f-193">[Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5871f-193">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
