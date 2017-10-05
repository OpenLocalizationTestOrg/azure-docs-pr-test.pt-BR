---
title: "Usar a Ação de Script para instalar o Solr no HDInsight baseado em Linux – Azure | Microsoft Docs"
description: "Saiba como instalar o Solr em clusters baseados Hadoop HDInsight baseados em Linux usando as ações de script."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: cc93ed5c-a358-456a-91a4-f179185c0e98
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 07/07/2017
ms.author: larryfr
ms.openlocfilehash: ad930ca023a36fa5874483873c82fdba11d117c7
ms.sourcegitcommit: 02e69c4a9d17645633357fe3d46677c2ff22c85a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/03/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="a867a-103">Instalar e usar o Solr em clusters HDInsight do Hadoop</span><span class="sxs-lookup"><span data-stu-id="a867a-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="a867a-104">Saiba como instalar o Solr no Azure HDInsight usando a Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="a867a-104">Learn how to install Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="a867a-105">O Solr é uma plataforma de pesquisa poderosa e oferece recursos de pesquisa em nível corporativo para os dados gerenciados pelo Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a867a-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="a867a-106">As etapas deste documento exigem um cluster HDInsight que usa Linux.</span><span class="sxs-lookup"><span data-stu-id="a867a-106">The steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="a867a-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="a867a-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="a867a-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="a867a-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a867a-109">O script de exemplo usado neste documento instala o Solr 4.9 com uma configuração específica.</span><span class="sxs-lookup"><span data-stu-id="a867a-109">The sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="a867a-110">Se você quiser configurar o cluster Solr com diferentes coleções, fragmentos, esquemas, réplicas, etc., modifique o script e os binários do Sol.</span><span class="sxs-lookup"><span data-stu-id="a867a-110">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries.</span></span>

## <span data-ttu-id="a867a-111"><a name="whatis"></a>O que é Solr</span><span class="sxs-lookup"><span data-stu-id="a867a-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="a867a-112">[Apache Solr](http://lucene.apache.org/solr/features.html) é uma plataforma de pesquisa empresarial que habilita operações poderosas de pesquisa de texto completo nos dados.</span><span class="sxs-lookup"><span data-stu-id="a867a-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="a867a-113">Enquanto o Hadoop permite armazenar e gerenciar grandes quantidades de dados, o Apache Solr oferece os recursos de pesquisa para recuperar rapidamente os dados.</span><span class="sxs-lookup"><span data-stu-id="a867a-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

> [!WARNING]
> <span data-ttu-id="a867a-114">Componentes fornecidos com o cluster HDInsight contam com suporte total da Microsoft.</span><span class="sxs-lookup"><span data-stu-id="a867a-114">Components provided with the HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="a867a-115">Componentes personalizados, como o Solr, recebem suporte comercialmente razoável para ajudá-lo a solucionar o problema.</span><span class="sxs-lookup"><span data-stu-id="a867a-115">Custom components, such as Solr, receive commercially reasonable support to help you to further troubleshoot the issue.</span></span> <span data-ttu-id="a867a-116">O suporte da Microsoft pode não ser capaz de resolver problemas com componentes personalizados.</span><span class="sxs-lookup"><span data-stu-id="a867a-116">Microsoft support may not be able to resolve problems with custom components.</span></span> <span data-ttu-id="a867a-117">Pode ser necessário envolver as comunidades de software livre para obter assistência.</span><span class="sxs-lookup"><span data-stu-id="a867a-117">You may need to engage the open source communities for assistance.</span></span> <span data-ttu-id="a867a-118">Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span><span class="sxs-lookup"><span data-stu-id="a867a-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com).</span></span> <span data-ttu-id="a867a-119">Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="a867a-119">Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-the-script-does"></a><span data-ttu-id="a867a-120">O que o script faz</span><span class="sxs-lookup"><span data-stu-id="a867a-120">What the script does</span></span>

<span data-ttu-id="a867a-121">Esse script faz as seguintes alterações ao cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="a867a-121">This script makes the following changes to the HDInsight cluster:</span></span>

* <span data-ttu-id="a867a-122">Instala o Solr 4.9 em `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="a867a-122">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="a867a-123">Cria um usuário, **solrusr**, que é usado para executar o serviço do Solr</span><span class="sxs-lookup"><span data-stu-id="a867a-123">Creates a user, **solrusr**, which is used to run the Solr service</span></span>
* <span data-ttu-id="a867a-124">Define **solruser** como o proprietário de `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="a867a-124">Sets **solruser** as the owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="a867a-125">Adiciona uma configuração [Upstart](http://upstart.ubuntu.com/) que inicia automaticamente o Solr.</span><span class="sxs-lookup"><span data-stu-id="a867a-125">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="a867a-126"><a name="install"></a>Instalar o Solr usando ações de script</span><span class="sxs-lookup"><span data-stu-id="a867a-126"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="a867a-127">Um script de exemplo para instalar o Solr em um cluster HDInsight está disponível no seguinte local:</span><span class="sxs-lookup"><span data-stu-id="a867a-127">A sample script to install Solr on an HDInsight cluster is available at the following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="a867a-128">Para criar um cluster com Solr instalado, use as etapas no documento [Criar clusters do HDInsight](hdinsight-hadoop-create-linux-clusters-portal.md).</span><span class="sxs-lookup"><span data-stu-id="a867a-128">To create a cluster that has Solr installed, use the steps in the [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="a867a-129">Durante o processo de criação, use as seguintes etapas para instalar o Solr:</span><span class="sxs-lookup"><span data-stu-id="a867a-129">During the creation process, use the following steps to install Solr:</span></span>

1. <span data-ttu-id="a867a-130">Na folha __Resumo do cluster__, selecione__Configurações avançadas__ e __Ações de script__.</span><span class="sxs-lookup"><span data-stu-id="a867a-130">From the __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="a867a-131">Use as informações a seguir para popular o formulário:</span><span class="sxs-lookup"><span data-stu-id="a867a-131">Use the following information to populate the form:</span></span>

   * <span data-ttu-id="a867a-132">**NOME**: insira um nome amigável para a ação de script.</span><span class="sxs-lookup"><span data-stu-id="a867a-132">**NAME**: Enter a friendly name for the script action.</span></span>
   * <span data-ttu-id="a867a-133">**URI do SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="a867a-133">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="a867a-134">**CABEÇALHO**: marque esta opção</span><span class="sxs-lookup"><span data-stu-id="a867a-134">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="a867a-135">**TRABALHO**: marque esta opção</span><span class="sxs-lookup"><span data-stu-id="a867a-135">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="a867a-136">**ZOOKEEPER**: marque esta opção para instalar no nó Zookeeper</span><span class="sxs-lookup"><span data-stu-id="a867a-136">**ZOOKEEPER**: Check this option to install on the Zookeeper node</span></span>
   * <span data-ttu-id="a867a-137">**PARÂMETROS**: deixe este campo em branco</span><span class="sxs-lookup"><span data-stu-id="a867a-137">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="a867a-138">Na parte inferior da folha **Ações de script**, use o botão **Selecionar** para salvar a configuração.</span><span class="sxs-lookup"><span data-stu-id="a867a-138">At the bottom of the **Script actions** blade, use the **Select** button to save the configuration.</span></span> <span data-ttu-id="a867a-139">Por fim, use o botão **Próximo** para retornar ao __Resumo do cluster__</span><span class="sxs-lookup"><span data-stu-id="a867a-139">Finally, use the **Next** button to return to the __Cluster summary__</span></span>

3. <span data-ttu-id="a867a-140">Na página __Resumo do cluster__, selecione __Criar__ para criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="a867a-140">From the __Cluster summary__ page, select __Create__ to create the cluster.</span></span>

## <span data-ttu-id="a867a-141"><a name="usesolr"></a>Como usar o Solr no HDInsight</span><span class="sxs-lookup"><span data-stu-id="a867a-141"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a867a-142">As etapas nesta seção demonstram a funcionalidade básica do Solr.</span><span class="sxs-lookup"><span data-stu-id="a867a-142">The steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="a867a-143">Para obter mais informações sobre como usar o Solr, consulte o [site Apache Solr](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="a867a-143">For more information on using Solr, see the [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="a867a-144">Dados de índice</span><span class="sxs-lookup"><span data-stu-id="a867a-144">Index data</span></span>

<span data-ttu-id="a867a-145">Use as etapas a seguir para adicionar dados de exemplo para Solr e, em seguida, consultá-los:</span><span class="sxs-lookup"><span data-stu-id="a867a-145">Use the following steps to add example data to Solr, and then query it:</span></span>

1. <span data-ttu-id="a867a-146">Conecte-se ao cluster HDInsight usando SSH:</span><span class="sxs-lookup"><span data-stu-id="a867a-146">Connect to the HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="a867a-147">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a867a-147">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="a867a-148">Etapas posteriormente nesse documento usam um túnel SSL para conectar-se à interface do usuário da Web do Solr.</span><span class="sxs-lookup"><span data-stu-id="a867a-148">Steps later in this document use an SSL tunnel to connect to the Solr web UI.</span></span> <span data-ttu-id="a867a-149">Para usar essas etapas, você deve estabelecer um túnel SSL e configurar seu navegador para usá-lo.</span><span class="sxs-lookup"><span data-stu-id="a867a-149">To use these steps, you must establish an SSL tunnel and then configure your browser to use it.</span></span>
     >
     > <span data-ttu-id="a867a-150">Para obter mais informações, consulte o documento [Usar túnel SSH com HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="a867a-150">For more information, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="a867a-151">Use os comandos a seguir para ter dados de exemplo do índice Solr:</span><span class="sxs-lookup"><span data-stu-id="a867a-151">Use the following commands to have Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="a867a-152">A seguinte saída será retornada para o console:</span><span class="sxs-lookup"><span data-stu-id="a867a-152">The following output is returned to the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="a867a-153">O utilitário `post.jar` adiciona os documentos **solr.xml** e **monitor.xml** ao índice.</span><span class="sxs-lookup"><span data-stu-id="a867a-153">The `post.jar` utility adds the **solr.xml** and **monitor.xml** documents to the index.</span></span>
  
3. <span data-ttu-id="a867a-154">Use o comando a seguir para consultar a API REST do Solr:</span><span class="sxs-lookup"><span data-stu-id="a867a-154">Use the following command to query the Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="a867a-155">Este comando busca **collection1** nos documentos que correspondem a **\*:\*** (codificado como \*%3A\* na cadeia de caracteres de consulta).</span><span class="sxs-lookup"><span data-stu-id="a867a-155">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in the query string).</span></span> <span data-ttu-id="a867a-156">No documento JSON a seguir há um exemplo de resposta:</span><span class="sxs-lookup"><span data-stu-id="a867a-156">The following JSON document is an example of the response:</span></span>

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, the Enterprise Search Server",
                    "manu": "Apache Software Foundation",
                    "cat": [
                      "software",
                      "search"
                    ],
                    "features": [
                      "Advanced Full-Text Search Capabilities using Lucene",
                      "Optimized for High Volume Web Traffic",
                      "Standards Based Open Interfaces - XML and HTTP",
                      "Comprehensive HTML Administration Interfaces",
                      "Scalability - Efficient Replication to other Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over the e)"
                    ],
                    "price": 0,
                    "price_c": "0,USD",
                    "popularity": 10,
                    "inStock": true,
                    "incubationdate_dt": "2006-01-17T00:00:00Z",
                    "_version_": 1486960636996878300
                  },
                  {
                    "id": "3007WFP",
                    "name": "Dell Widescreen UltraSharp 3007WFP",
                    "manu": "Dell, Inc.",
                    "manu_id_s": "dell",
                    "cat": [
                      "electronics and computer1"
                    ],
                    "features": [
                      "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                    ],
                    "includes": "USB cable",
                    "weight": 401.6,
                    "price": 2199,
                    "price_c": "2199,USD",
                    "popularity": 6,
                    "inStock": true,
                    "store": "43.17614,-90.57341",
                    "_version_": 1486960637584081000
                  }
                ]
              }

### <a name="using-the-solr-dashboard"></a><span data-ttu-id="a867a-157">Usando o painel do Solr</span><span class="sxs-lookup"><span data-stu-id="a867a-157">Using the Solr dashboard</span></span>

<span data-ttu-id="a867a-158">O painel do Solr é uma IU Web que permite que você trabalhe com o Solr através do seu navegador da Web.</span><span class="sxs-lookup"><span data-stu-id="a867a-158">The Solr dashboard is a web UI that allows you to work with Solr through your web browser.</span></span> <span data-ttu-id="a867a-159">O painel do Solr não é exposto diretamente à Internet no seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a867a-159">The Solr dashboard is not exposed directly on the Internet from your HDInsight cluster.</span></span> <span data-ttu-id="a867a-160">É possível usar um túnel SSH para acessá-lo.</span><span class="sxs-lookup"><span data-stu-id="a867a-160">You can use an SSH tunnel to access it.</span></span> <span data-ttu-id="a867a-161">Para obter mais informações sobre como usar um túnel SSH, consulte o documento [Usar túnel SSH com HDInsight](hdinsight-linux-ambari-ssh-tunnel.md).</span><span class="sxs-lookup"><span data-stu-id="a867a-161">For more information on using an SSH tunnel, see the [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="a867a-162">Depois de estabelecer um túnel SSH, use as seguintes etapas para usar o painel do Solr:</span><span class="sxs-lookup"><span data-stu-id="a867a-162">Once you have established an SSH tunnel, use the following steps to use the Solr dashboard:</span></span>

1. <span data-ttu-id="a867a-163">Determine o nome de host para o nó de cabeçalho primário:</span><span class="sxs-lookup"><span data-stu-id="a867a-163">Determine the host name for the primary headnode:</span></span>

   1. <span data-ttu-id="a867a-164">Use SSH para conectar-se ao nó principal do cluster.</span><span class="sxs-lookup"><span data-stu-id="a867a-164">Use SSH to connect to the cluster head node.</span></span> <span data-ttu-id="a867a-165">Por exemplo: `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="a867a-165">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="a867a-166">Para saber mais sobre como usar SSH, consulte [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a867a-166">For more information on using SSH, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="a867a-167">Use o seguinte comando para obter o nome de host totalmente qualificado:</span><span class="sxs-lookup"><span data-stu-id="a867a-167">Use the following command to get the fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="a867a-168">Esse comando retorna um valor semelhante ao nome de host a seguir:</span><span class="sxs-lookup"><span data-stu-id="a867a-168">This command returns a value similar to the following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="a867a-169">Salve o valor retornado, pois ele será usado posteriormente.</span><span class="sxs-lookup"><span data-stu-id="a867a-169">Save the value returned, as it is used later.</span></span>

2. <span data-ttu-id="a867a-170">Em seu navegador, conecte **http://HOSTNAME:8983/solr/#/**, onde **HOSTNAME** é o nome determinado nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="a867a-170">In your browser, connect to **http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is the name you determined in the previous steps.</span></span>

    <span data-ttu-id="a867a-171">A solicitação é roteada através do túnel SSH para a interface do usuário da Web do Solr no cluster.</span><span class="sxs-lookup"><span data-stu-id="a867a-171">The request is routed through the SSH tunnel to the Solr web UI on your cluster.</span></span> <span data-ttu-id="a867a-172">A página exibida é semelhante à imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="a867a-172">The page appears similar to the following image:</span></span>

    ![Imagem do painel do Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="a867a-174">No painel à esquerda, use a lista suspensa **Seletor de Núcleo** para selecionar **collection1**.</span><span class="sxs-lookup"><span data-stu-id="a867a-174">From the left pane, use the **Core Selector** drop-down to select **collection1**.</span></span> <span data-ttu-id="a867a-175">Várias entradas deverão aparecer abaixo de **collection1**.</span><span class="sxs-lookup"><span data-stu-id="a867a-175">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="a867a-176">Nas entradas abaixo de **collection1**, selecione **Consultar**.</span><span class="sxs-lookup"><span data-stu-id="a867a-176">From the entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="a867a-177">Use os valores a seguir para preencher a página de pesquisa:</span><span class="sxs-lookup"><span data-stu-id="a867a-177">Use the following values to populate the search page:</span></span>

   * <span data-ttu-id="a867a-178">Na caixa de texto **q**, digite **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="a867a-178">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="a867a-179">Essa consulta retorna todos os documentos que são indexados em Solr.</span><span class="sxs-lookup"><span data-stu-id="a867a-179">This query returns all the documents that are indexed in Solr.</span></span> <span data-ttu-id="a867a-180">Se você quiser procurar uma cadeia de caracteres específica dentro dos documentos, você pode inserir essa cadeia de caracteres aqui.</span><span class="sxs-lookup"><span data-stu-id="a867a-180">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="a867a-181">Na caixa de texto **wt** , selecione o formato de saída.</span><span class="sxs-lookup"><span data-stu-id="a867a-181">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="a867a-182">O padrão é **json**.</span><span class="sxs-lookup"><span data-stu-id="a867a-182">Default is **json**.</span></span>

     <span data-ttu-id="a867a-183">Por fim, selecione o botão **Executar Consulta** na parte inferior da página de pesquisa.</span><span class="sxs-lookup"><span data-stu-id="a867a-183">Finally, select the **Execute Query** button at the bottom of the search pate.</span></span>

     ![Usar Ação de Script para personalizar um cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="a867a-185">A saída retorna os dois documentos que você adicionou anteriormente ao índice.</span><span class="sxs-lookup"><span data-stu-id="a867a-185">The output returns the two documents that you added to the index earlier.</span></span> <span data-ttu-id="a867a-186">A saída é semelhante ao documento JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="a867a-186">The output is similar to the following JSON document:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, the Enterprise Search Server",
                   "manu": "Apache Software Foundation",
                   "cat": [
                     "software",
                     "search"
                   ],
                   "features": [
                     "Advanced Full-Text Search Capabilities using Lucene",
                     "Optimized for High Volume Web Traffic",
                     "Standards Based Open Interfaces - XML and HTTP",
                     "Comprehensive HTML Administration Interfaces",
                     "Scalability - Efficient Replication to other Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over the e)"
                   ],
                   "price": 0,
                   "price_c": "0,USD",
                   "popularity": 10,
                   "inStock": true,
                   "incubationdate_dt": "2006-01-17T00:00:00Z",
                   "_version_": 1486960636996878300
                 },
                 {
                   "id": "3007WFP",
                   "name": "Dell Widescreen UltraSharp 3007WFP",
                   "manu": "Dell, Inc.",
                   "manu_id_s": "dell",
                   "cat": [
                     "electronics and computer1"
                   ],
                   "features": [
                     "30\" TFT active matrix LCD, 2560 x 1600, .25mm dot pitch, 700:1 contrast"
                   ],
                   "includes": "USB cable",
                   "weight": 401.6,
                   "price": 2199,
                   "price_c": "2199,USD",
                   "popularity": 6,
                   "inStock": true,
                   "store": "43.17614,-90.57341",
                   "_version_": 1486960637584081000
                 }
               ]
             }

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="a867a-187">Iniciando e parando o Solr</span><span class="sxs-lookup"><span data-stu-id="a867a-187">Starting and stopping Solr</span></span>

<span data-ttu-id="a867a-188">Use o seguintes comandos para interromper ou iniciar o Solr manualmente:</span><span class="sxs-lookup"><span data-stu-id="a867a-188">Use the following commands to manually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="a867a-189">Backup de dados indexados</span><span class="sxs-lookup"><span data-stu-id="a867a-189">Backup indexed data</span></span>

<span data-ttu-id="a867a-190">Use as etapas a seguir para fazer backup de dados do Solr no armazenamento padrão do cluster:</span><span class="sxs-lookup"><span data-stu-id="a867a-190">Use the following steps to back up Solr data to the default storage for your cluster:</span></span>

1. <span data-ttu-id="a867a-191">Conecte-se ao cluster usando o SSH, depois use o comando a seguir para obter o nome de host do nó de cabeçalho:</span><span class="sxs-lookup"><span data-stu-id="a867a-191">Connect to the cluster using SSH, then use the following command to get the host name for the head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="a867a-192">Use o comando a seguir para criar um instantâneo dos dados indexados.</span><span class="sxs-lookup"><span data-stu-id="a867a-192">Use the following command to create a snapshot of the indexed data.</span></span> <span data-ttu-id="a867a-193">Substitua **HOSTNAME** pelo nome retornado do comando anterior:</span><span class="sxs-lookup"><span data-stu-id="a867a-193">Replace **HOSTNAME** with the name returned from the previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="a867a-194">A resposta é semelhante ao XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="a867a-194">The response is similar to the following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="a867a-195">Altere os diretórios para `/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="a867a-195">Change directories to `/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="a867a-196">Há um subdiretório aqui para cada coleção.</span><span class="sxs-lookup"><span data-stu-id="a867a-196">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="a867a-197">Cada diretório da coleção contém um diretório `data`, que contém o instantâneo dessa coleção.</span><span class="sxs-lookup"><span data-stu-id="a867a-197">Each collection directory contains a `data` directory that contains the snapshot for the collection.</span></span>

4. <span data-ttu-id="a867a-198">Para criar um arquivo morto compactado da pasta de instantâneos, use o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a867a-198">To create a compressed archive of the snapshot folder, use the following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="a867a-199">Substitua os valores `snapshot.20150806185338855` pelo nome do instantâneo da coleção.</span><span class="sxs-lookup"><span data-stu-id="a867a-199">Replace the `snapshot.20150806185338855` values with the name of the snapshot for your collection.</span></span>

    <span data-ttu-id="a867a-200">Esse comando cria um arquivo morto denominado **snapshot.20150806185338855.tgz**, que tem o conteúdo do diretório **snapshot.20150806185338855**.</span><span class="sxs-lookup"><span data-stu-id="a867a-200">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains the contents of the **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="a867a-201">Em seguida, você pode armazenar o arquivo para armazenamento primário do cluster usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="a867a-201">You can then store the archive to the cluster's primary storage using the following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="a867a-202">Para obter mais informações sobre como trabalhar com backups e restaurações do Solr, consulte [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="a867a-202">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a867a-203">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a867a-203">Next steps</span></span>

* <span data-ttu-id="a867a-204">[Instalar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a867a-204">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="a867a-205">Use a personalização do cluster para instalar o Giraph em clusters de Hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a867a-205">Use cluster customization to install Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="a867a-206">O Giraph permite que você realize processamento de tabelas usando o Hadoop, além de poder ser usado com o HDInsight do Azure.</span><span class="sxs-lookup"><span data-stu-id="a867a-206">Giraph allows you to perform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="a867a-207">[Instalar matiz em clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="a867a-207">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="a867a-208">Use a personalização do cluster para instalar o Hue em clusters de Hadoop do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a867a-208">Use cluster customization to install Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="a867a-209">A Matiz é um conjunto de aplicativos da Web usado para interagir com um cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="a867a-209">Hue is a set of Web applications used to interact with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
