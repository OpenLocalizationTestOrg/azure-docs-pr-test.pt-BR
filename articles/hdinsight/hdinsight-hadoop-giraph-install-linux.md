---
title: "Instalar e usar o Giraph em clusters HDInsight (Hadoop) – Azure | Microsoft Docs"
description: "Saiba como instalar o Giraph em clusters HDInsight baseados em Linux usando as Ações de Script. Ações de script permitem que você personalize o cluster durante a criação, alterando a configuração do cluster ou instalando serviços e utilitários."
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
ms.openlocfilehash: 6e2f6983e00f874420f7f0907dbc68185f0af713
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="install-giraph-on-hdinsight-hadoop-clusters-and-use-giraph-to-process-large-scale-graphs"></a><span data-ttu-id="323d5-104">Instalar o Giraph nos clusters Hadoop do HDInsight e usar o Giraph para processar gráficos em grande escala</span><span class="sxs-lookup"><span data-stu-id="323d5-104">Install Giraph on HDInsight Hadoop clusters, and use Giraph to process large-scale graphs</span></span>

<span data-ttu-id="323d5-105">Saiba como instalar o Apache Giraph em um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="323d5-105">Learn how to install Apache Giraph on an HDInsight cluster.</span></span> <span data-ttu-id="323d5-106">O recurso de ação de script do HDInsight permite que você personalize o cluster executando um script de bash.</span><span class="sxs-lookup"><span data-stu-id="323d5-106">The script action feature of HDInsight allows you to customize your cluster by running a bash script.</span></span> <span data-ttu-id="323d5-107">Scripts podem ser usados para personalizar os clusters durante e após a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="323d5-107">Scripts can be used to customize clusters during and after cluster creation.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="323d5-108">As etapas deste documento exigem um cluster HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="323d5-108">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="323d5-109">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="323d5-109">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="323d5-110">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="323d5-110">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

## <span data-ttu-id="323d5-111"><a name="whatis"></a>O que é Giraph</span><span class="sxs-lookup"><span data-stu-id="323d5-111"><a name="whatis"></a>What is Giraph</span></span>

<span data-ttu-id="323d5-112">O [Apache Giraph](http://giraph.apache.org/) permite executar processamento de gráficos usando o Hadoop e pode ser usado com o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="323d5-112">[Apache Giraph](http://giraph.apache.org/) allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span> <span data-ttu-id="323d5-113">Gráficos moldam as relações entre objetos.</span><span class="sxs-lookup"><span data-stu-id="323d5-113">Graphs model relationships between objects.</span></span> <span data-ttu-id="323d5-114">Por exemplo, as conexões entre roteadores em uma rede grande como a Internet ou relações entre pessoas em redes sociais.</span><span class="sxs-lookup"><span data-stu-id="323d5-114">For example, the connections between routers on a large network like the Internet, or relationships between people on social networks.</span></span> <span data-ttu-id="323d5-115">O processamento de tabelas permite que você faça a análise das relações entre objetos em uma tabela, como:</span><span class="sxs-lookup"><span data-stu-id="323d5-115">Graph processing allows you to reason about the relationships between objects in a graph, such as:</span></span>

* <span data-ttu-id="323d5-116">Identificar possíveis amigos com base em suas relações atuais.</span><span class="sxs-lookup"><span data-stu-id="323d5-116">Identifying potential friends based on your current relationships.</span></span>

* <span data-ttu-id="323d5-117">Identificar a menor rota entre dois computadores em uma rede.</span><span class="sxs-lookup"><span data-stu-id="323d5-117">Identifying the shortest route between two computers in a network.</span></span>

* <span data-ttu-id="323d5-118">Calcular a ordem de classificação de página da Web.</span><span class="sxs-lookup"><span data-stu-id="323d5-118">Calculating the page rank of webpages.</span></span>

> [!WARNING]
> <span data-ttu-id="323d5-119">Há suporte total a componentes fornecidos com o cluster do HDInsight – o Suporte da Microsoft ajudará a isolar e resolver problemas relacionados a esses componentes.</span><span class="sxs-lookup"><span data-stu-id="323d5-119">Components provided with the HDInsight cluster are fully supported - Microsoft Support helps to isolate and resolve issues related to these components.</span></span>
>
> <span data-ttu-id="323d5-120">Componentes personalizados, como o Giraph, recebem suporte comercialmente razoável para ajudá-lo a solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="323d5-120">Custom components, such as Giraph, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="323d5-121">O Suporte da Microsoft pode ser capaz de resolver o problema.</span><span class="sxs-lookup"><span data-stu-id="323d5-121">Microsoft Support may be able to resolving the issue.</span></span> <span data-ttu-id="323d5-122">Caso contrário, você deve consultar comunidades de software livre em que é possível encontrar conhecimento aprofundado sobre essa tecnologia.</span><span class="sxs-lookup"><span data-stu-id="323d5-122">If not, you must consult open source communities where deep expertise for that technology is found.</span></span> <span data-ttu-id="323d5-123">Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="323d5-123">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="323d5-124">Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="323d5-124">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>


## <a name="what-the-script-does"></a><span data-ttu-id="323d5-125">O que o script faz</span><span class="sxs-lookup"><span data-stu-id="323d5-125">What the script does</span></span>

<span data-ttu-id="323d5-126">O script executa as ações a seguir:</span><span class="sxs-lookup"><span data-stu-id="323d5-126">This script performs the following actions:</span></span>

* <span data-ttu-id="323d5-127">Instala o Giraph no `/usr/hdp/current/giraph`</span><span class="sxs-lookup"><span data-stu-id="323d5-127">Installs Giraph to `/usr/hdp/current/giraph`</span></span>

* <span data-ttu-id="323d5-128">Copia o arquivo `giraph-examples.jar` para o armazenamento padrão (WASB) para o seu cluster: `/example/jars/giraph-examples.jar`</span><span class="sxs-lookup"><span data-stu-id="323d5-128">Copies the `giraph-examples.jar` file to default storage (WASB) for your cluster: `/example/jars/giraph-examples.jar`</span></span>

## <span data-ttu-id="323d5-129"><a name="install"></a>Instalar o Giraph usando Ações de Script</span><span class="sxs-lookup"><span data-stu-id="323d5-129"><a name="install"></a>Install Giraph using Script Actions</span></span>

<span data-ttu-id="323d5-130">Um script de exemplo para instalar o Giraph em um cluster HDInsight está disponível na seguinte localização:</span><span class="sxs-lookup"><span data-stu-id="323d5-130">A sample script to install Giraph on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh

<span data-ttu-id="323d5-131">Esta seção fornece instruções sobre como usar o exemplo de script durante a criação do cluster usando o Portal do Azure.</span><span class="sxs-lookup"><span data-stu-id="323d5-131">This section provides instructions on how to use the sample script while creating the cluster by using the Azure portal.</span></span>

> [!NOTE]
> <span data-ttu-id="323d5-132">As ações de script podem ser aplicadas por meio dos seguintes métodos:</span><span class="sxs-lookup"><span data-stu-id="323d5-132">A script action can be applied using any of the following methods:</span></span>
> * <span data-ttu-id="323d5-133">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="323d5-133">Azure PowerShell</span></span>
> * <span data-ttu-id="323d5-134">A CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="323d5-134">The Azure CLI</span></span>
> * <span data-ttu-id="323d5-135">O SDK .NET do HDInsight</span><span class="sxs-lookup"><span data-stu-id="323d5-135">The HDInsight .NET SDK</span></span>
> * <span data-ttu-id="323d5-136">Modelos do Gerenciador de Recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="323d5-136">Azure Resource Manager templates</span></span>
> 
> <span data-ttu-id="323d5-137">Também é possível aplicar ações de script a clusters que já estão em execução.</span><span class="sxs-lookup"><span data-stu-id="323d5-137">You can also apply script actions to already running clusters.</span></span> <span data-ttu-id="323d5-138">Para saber mais, veja [Personalizar clusters HDInsight com as Ações de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="323d5-138">For more information, see [Customize HDInsight clusters with Script Actions](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

1. <span data-ttu-id="323d5-139">Inicie a criação de um cluster usando as etapas em [Criar clusters de HDInsight baseados em Linux](hdinsight-hadoop-create-linux-clusters-portal.md), mas não conclua a criação.</span><span class="sxs-lookup"><span data-stu-id="323d5-139">Start creating a cluster by using the steps in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md), but do not complete creation.</span></span>

2. <span data-ttu-id="323d5-140">Na folha **Configuração Opcional**, escolha **Ações de Script** e forneça as seguintes informações:</span><span class="sxs-lookup"><span data-stu-id="323d5-140">On the **Optional Configuration** blade, select **Script Actions**, and provide the following information:</span></span>

   * <span data-ttu-id="323d5-141">**NOME**: insira um nome amigável para a ação de script.</span><span class="sxs-lookup"><span data-stu-id="323d5-141">**NAME**: Enter a friendly name for the script action.</span></span>

   * <span data-ttu-id="323d5-142">**URI do SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="323d5-142">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxgiraphconfigactionv01/giraph-installer-v01.sh</span></span>

   * <span data-ttu-id="323d5-143">**CABEÇALHO**: marque esta entrada</span><span class="sxs-lookup"><span data-stu-id="323d5-143">**HEAD**: Check this entry</span></span>

   * <span data-ttu-id="323d5-144">**TRABALHO**: deixe esta entrada desmarcada</span><span class="sxs-lookup"><span data-stu-id="323d5-144">**WORKER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="323d5-145">**ZOOKEEPER**: deixe esta entrada desmarcada</span><span class="sxs-lookup"><span data-stu-id="323d5-145">**ZOOKEEPER**: Leave this entry unchecked</span></span>

   * <span data-ttu-id="323d5-146">**PARÂMETROS**: deixe este campo em branco</span><span class="sxs-lookup"><span data-stu-id="323d5-146">**PARAMETERS**: Leave this field blank</span></span>

3. <span data-ttu-id="323d5-147">Na parte inferior das **Ações de Script**, use o botão **Selecionar** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="323d5-147">At the bottom of the **Script Actions**, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="323d5-148">Por fim, use o botão **Selecionar** na parte inferior da folha **Configuração opcional** para salvar as informações de configuração opcional.</span><span class="sxs-lookup"><span data-stu-id="323d5-148">Finally, use the **Select** button at the bottom of the **Optional Configuration** blade to save the optional configuration information.</span></span>

4. <span data-ttu-id="323d5-149">Continue a criação do cluster conforme descrito em [Criar clusters HDInsight baseados em Linux](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="323d5-149">Continue creating the cluster as described in [Create Linux-based HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md).</span></span>

## <span data-ttu-id="323d5-150"><a name="usegiraph"></a>Como usar o Giraph no HDInsight?</span><span class="sxs-lookup"><span data-stu-id="323d5-150"><a name="usegiraph"></a>How do I use Giraph in HDInsight?</span></span>

<span data-ttu-id="323d5-151">Quando o cluster tiver sido criado, use as etapas a seguir para executar o exemplo SimpleShortestPathsComputation incluído com o Giraph.</span><span class="sxs-lookup"><span data-stu-id="323d5-151">Once the cluster has been created, use the following steps to run the SimpleShortestPathsComputation example included with Giraph.</span></span> <span data-ttu-id="323d5-152">Este exemplo usa a implementação do [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) básico para encontrar o caminho mais curto entre objetos em um gráfico.</span><span class="sxs-lookup"><span data-stu-id="323d5-152">This example uses the basic [Pregel](http://people.apache.org/~edwardyoon/documents/pregel.pdf) implementation for finding the shortest path between objects in a graph.</span></span>

1. <span data-ttu-id="323d5-153">Conecte-se ao cluster HDInsight usando SSH:</span><span class="sxs-lookup"><span data-stu-id="323d5-153">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="323d5-154">Para obter informações, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="323d5-154">For information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="323d5-155">Use o comando a seguir para criar um novo arquivo chamado **tiny_graph.txt**:</span><span class="sxs-lookup"><span data-stu-id="323d5-155">Use the following command to create a file named **tiny_graph.txt**:</span></span>

    ```bash
    nano tiny_graph.txt
    ```

    <span data-ttu-id="323d5-156">Use o seguinte texto como o conteúdo deste arquivo:</span><span class="sxs-lookup"><span data-stu-id="323d5-156">Use the following text as the contents of this file:</span></span>

    ```text
    [0,0,[[1,1],[3,3]]]
    [1,0,[[0,1],[2,2],[3,1]]]
    [2,0,[[1,2],[4,4]]]
    [3,0,[[0,3],[1,1],[4,4]]]
    [4,0,[[3,4],[2,4]]]
    ```

    <span data-ttu-id="323d5-157">Esses dados descrevem uma relação entre objetos em uma tabela direcionada, usando o formato `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span><span class="sxs-lookup"><span data-stu-id="323d5-157">This data describes a relationship between objects in a directed graph, by using the format `[source_id, source_value,[[dest_id], [edge_value],...]]`.</span></span> <span data-ttu-id="323d5-158">Cada linha representa uma relação entre um objeto `source_id` e um ou mais objetos `dest_id`.</span><span class="sxs-lookup"><span data-stu-id="323d5-158">Each line represents a relationship between a `source_id` object and one or more `dest_id` objects.</span></span> <span data-ttu-id="323d5-159">O `edge_value` pode ser considerado a força ou a distância da conexão entre `source_id` e `dest\_id`.</span><span class="sxs-lookup"><span data-stu-id="323d5-159">The `edge_value` can be thought of as the strength or distance of the connection between `source_id` and `dest\_id`.</span></span>

    <span data-ttu-id="323d5-160">Desenhados e utilizando o valor (ou peso) como distância entre os objetos, os dados acima podem se parecer com o diagrama a seguir:</span><span class="sxs-lookup"><span data-stu-id="323d5-160">Drawn out, and using the value (or weight) as the distance between objects, the data might look like the following diagram:</span></span>

    ![tiny_graph.txt Desenhado como círculos com linhas de distância variável entre](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph.png)

3. <span data-ttu-id="323d5-162">Para salvar o arquivo, use **Ctrl + X**, em seguida, **Y** e, finalmente, **Enter** para aceitar o nome de arquivo.</span><span class="sxs-lookup"><span data-stu-id="323d5-162">To save the file, use **Ctrl+X**, then **Y**, and finally **Enter** to accept the file name.</span></span>

4. <span data-ttu-id="323d5-163">Use o seguinte para armazenar os dados no armazenamento primário para o cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="323d5-163">Use the following to store the data into primary storage for your HDInsight cluster:</span></span>

    ```bash
    hdfs dfs -put tiny_graph.txt /example/data/tiny_graph.txt
    ```

5. <span data-ttu-id="323d5-164">Execute o exemplo SimpleShortestPathsComputation usando o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="323d5-164">Run the SimpleShortestPathsComputation example using the following command:</span></span>

    ```bash
    yarn jar /usr/hdp/current/giraph/giraph-examples.jar org.apache.giraph.GiraphRunner org.apache.giraph.examples.SimpleShortestPathsComputation -ca mapred.job.tracker=headnodehost:9010 -vif org.apache.giraph.io.formats.JsonLongDoubleFloatDoubleVertexInputFormat -vip /example/data/tiny_graph.txt -vof org.apache.giraph.io.formats.IdWithValueTextOutputFormat -op /example/output/shortestpaths -w 2
    ```

    <span data-ttu-id="323d5-165">Os parâmetros usados com este comando são descritos na tabela a seguir:</span><span class="sxs-lookup"><span data-stu-id="323d5-165">The parameters used with this command are described in the following table:</span></span>

   | <span data-ttu-id="323d5-166">Parâmetro</span><span class="sxs-lookup"><span data-stu-id="323d5-166">Parameter</span></span> | <span data-ttu-id="323d5-167">O que faz</span><span class="sxs-lookup"><span data-stu-id="323d5-167">What it does</span></span> |
   | --- | --- |
   | `jar` |<span data-ttu-id="323d5-168">O arquivo jar que contém os exemplos.</span><span class="sxs-lookup"><span data-stu-id="323d5-168">The jar file containing the examples.</span></span> |
   | `org.apache.giraph.GiraphRunner` |<span data-ttu-id="323d5-169">A classe usada para iniciar os exemplos.</span><span class="sxs-lookup"><span data-stu-id="323d5-169">The class used to start the examples.</span></span> |
   | `org.apache.giraph.examples.SimpleShortestPathsCoputation` |<span data-ttu-id="323d5-170">O exemplo usado.</span><span class="sxs-lookup"><span data-stu-id="323d5-170">The example that is used.</span></span> <span data-ttu-id="323d5-171">Nesse exemplo, ele calcula o caminho mais curto entre a ID 1 e todas as outras IDs no gráfico.</span><span class="sxs-lookup"><span data-stu-id="323d5-171">In this example, it computes the shortest path between ID 1 and all other IDs in the graph.</span></span> |
   | `-ca mapred.job.tracker` |<span data-ttu-id="323d5-172">O nó de cabeçalho do cluster.</span><span class="sxs-lookup"><span data-stu-id="323d5-172">The headnode for the cluster.</span></span> |
   | `-vif` |<span data-ttu-id="323d5-173">O formato de entrada a ser usado para os dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="323d5-173">The input format to use for the input data.</span></span> |
   | `-vip` |<span data-ttu-id="323d5-174">O arquivo de dados de entrada.</span><span class="sxs-lookup"><span data-stu-id="323d5-174">The input data file.</span></span> |
   | `-vof` |<span data-ttu-id="323d5-175">O formato de saída.</span><span class="sxs-lookup"><span data-stu-id="323d5-175">The output format.</span></span> <span data-ttu-id="323d5-176">Nesse exemplo, a ID e o valor como texto sem formatação.</span><span class="sxs-lookup"><span data-stu-id="323d5-176">In this example, ID and value as plain text.</span></span> |
   | `-op` |<span data-ttu-id="323d5-177">O local de saída.</span><span class="sxs-lookup"><span data-stu-id="323d5-177">The output location.</span></span> |
   | `-w 2` |<span data-ttu-id="323d5-178">O número de trabalhos a usar.</span><span class="sxs-lookup"><span data-stu-id="323d5-178">The number of workers to use.</span></span> <span data-ttu-id="323d5-179">Neste exemplo, 2.</span><span class="sxs-lookup"><span data-stu-id="323d5-179">In this example, 2.</span></span> |

    <span data-ttu-id="323d5-180">Para obter mais informações sobre esses e outros parâmetros usados com exemplos do Giraph, consulte o [Guia de início rápido do Giraph](http://giraph.apache.org/quick_start.html).</span><span class="sxs-lookup"><span data-stu-id="323d5-180">For more information on these, and other parameters used with Giraph samples, see the [Giraph quickstart](http://giraph.apache.org/quick_start.html).</span></span>

6. <span data-ttu-id="323d5-181">Assim que o trabalho tiver sido concluído, os resultados serão armazenados no diretório **/example/out/shotestpaths**.</span><span class="sxs-lookup"><span data-stu-id="323d5-181">Once the job has finished, the results are stored in the **/example/out/shotestpaths** directory.</span></span> <span data-ttu-id="323d5-182">Os nomes de arquivo saída começam com **part-m-** e terminam com um número indicando o primeiro, segundo etc. arquivo.</span><span class="sxs-lookup"><span data-stu-id="323d5-182">The output file names begin with **part-m-** and end with a number indicating the first, second, etc. file.</span></span> <span data-ttu-id="323d5-183">Use o comando a seguir para exibir a saída:</span><span class="sxs-lookup"><span data-stu-id="323d5-183">Use the following command to view the output:</span></span>

    ```bash
    hdfs dfs -text /example/output/shortestpaths/*
    ```

    <span data-ttu-id="323d5-184">A saída deve ter aparência similar ao seguinte texto:</span><span class="sxs-lookup"><span data-stu-id="323d5-184">The output should appear similar to the following text:</span></span>

        0    1.0
        4    5.0
        2    2.0
        1    0.0
        3    1.0

    <span data-ttu-id="323d5-185">O exemplo SimpleShortestPathComputation está codificado para começar com a ID do objeto 1 e localizar o caminho mais curto para os outros objetos.</span><span class="sxs-lookup"><span data-stu-id="323d5-185">The SimpleShortestPathComputation example is hard coded to start with object ID 1 and find the shortest path to other objects.</span></span> <span data-ttu-id="323d5-186">A saída está no formato de `destination_id` e `distance`.</span><span class="sxs-lookup"><span data-stu-id="323d5-186">The output is in the format of `destination_id` and `distance`.</span></span> <span data-ttu-id="323d5-187">`distance` é o valor (ou peso) das bordas percorridas entre a ID do objeto 1 e a ID de destino.</span><span class="sxs-lookup"><span data-stu-id="323d5-187">The `distance` is the value (or weight) of the edges traveled between object ID 1 and the target ID.</span></span>

    <span data-ttu-id="323d5-188">Visualizando esses dados, você pode verificar os resultados percorrendo os caminhos mais curtos entre a ID 1 e todos os outros objetos.</span><span class="sxs-lookup"><span data-stu-id="323d5-188">Visualizing this data, you can verify the results by traveling the shortest paths between ID 1 and all other objects.</span></span> <span data-ttu-id="323d5-189">Observe que o caminho mais curto entre a ID 1 e a ID 4 é 5.</span><span class="sxs-lookup"><span data-stu-id="323d5-189">The shortest path between ID 1 and ID 4 is 5.</span></span> <span data-ttu-id="323d5-190">Esse valor é a distância total entre <span style="color:orange">ID 1 e 3</span> e, em seguida, entre <span style="color:red">ID 3 e 4</span>.</span><span class="sxs-lookup"><span data-stu-id="323d5-190">This value is the total distance between <span style="color:orange">ID 1 and 3</span>, and then <span style="color:red">ID 3 and 4</span>.</span></span>

    ![Desenho dos objetos como círculos com os percursos mais curtos entre](./media/hdinsight-hadoop-giraph-install-linux/giraph-graph-out.png)

## <a name="next-steps"></a><span data-ttu-id="323d5-192">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="323d5-192">Next steps</span></span>

* <span data-ttu-id="323d5-193">[Instalar e usar o Hue em clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="323d5-193">[Install and use Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span>

* <span data-ttu-id="323d5-194">[Instalar o Solr em clusters HDInsight](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="323d5-194">[Install Solr on HDInsight clusters](hdinsight-hadoop-solr-install-linux.md).</span></span>
