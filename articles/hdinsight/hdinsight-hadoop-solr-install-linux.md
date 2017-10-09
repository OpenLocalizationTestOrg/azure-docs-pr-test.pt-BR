---
title: "Ação de Script de aaaUse tooinstall Solr no HDInsight baseados em Linux - Azure | Microsoft Docs"
description: "Saiba como tooinstall Solr no Hadoop de HDInsight baseados em Linux clusters usando ações de Script."
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
ms.openlocfilehash: 4c179032b95ae187f1830d8927f8796372fa8ebe
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-hdinsight-hadoop-clusters"></a><span data-ttu-id="5670c-103">Instalar e usar o Solr em clusters HDInsight do Hadoop</span><span class="sxs-lookup"><span data-stu-id="5670c-103">Install and use Solr on HDInsight Hadoop clusters</span></span>

<span data-ttu-id="5670c-104">Saiba como tooinstall Solr no Azure HDInsight usando a ação de Script.</span><span class="sxs-lookup"><span data-stu-id="5670c-104">Learn how tooinstall Solr on Azure HDInsight by using Script Action.</span></span> <span data-ttu-id="5670c-105">O Solr é uma plataforma de pesquisa poderosa e oferece recursos de pesquisa em nível corporativo para os dados gerenciados pelo Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5670c-105">Solr is a powerful search platform and provides enterprise-level search capabilities on data managed by Hadoop.</span></span>

> [!IMPORTANT]
    > <span data-ttu-id="5670c-106">etapas de saudação neste documento exigem um cluster HDInsight que usa o Linux.</span><span class="sxs-lookup"><span data-stu-id="5670c-106">hello steps in this document require an HDInsight cluster that uses Linux.</span></span> <span data-ttu-id="5670c-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="5670c-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="5670c-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="5670c-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5670c-109">script de exemplo Hello usado neste documento instala 4.9 Solr com uma configuração específica.</span><span class="sxs-lookup"><span data-stu-id="5670c-109">hello sample script used in this document installs Solr 4.9 with a specific configuration.</span></span> <span data-ttu-id="5670c-110">Se desejar que o cluster de Solr tooconfigure Olá com diferentes coleções, fragmentos, esquemas, réplicas, etc., você deve modificar o script hello e binários do Solr.</span><span class="sxs-lookup"><span data-stu-id="5670c-110">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries.</span></span>

## <span data-ttu-id="5670c-111"><a name="whatis"></a>O que é Solr</span><span class="sxs-lookup"><span data-stu-id="5670c-111"><a name="whatis"></a>What is Solr</span></span>

<span data-ttu-id="5670c-112">O [Apache Solr](http://lucene.apache.org/solr/features.html) é uma plataforma de pesquisa empresarial que habilita operações poderosas de pesquisa de texto completo nos dados.</span><span class="sxs-lookup"><span data-stu-id="5670c-112">[Apache Solr](http://lucene.apache.org/solr/features.html) is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="5670c-113">Enquanto o Hadoop permite armazenar e gerenciar grandes quantidades de dados, o Apache Solr fornece recursos de pesquisa de saudação tooquickly recupera dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="5670c-113">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

> [!WARNING]
> <span data-ttu-id="5670c-114">Componentes fornecidos com o cluster do HDInsight Olá são totalmente suportados pela Microsoft.</span><span class="sxs-lookup"><span data-stu-id="5670c-114">Components provided with hello HDInsight cluster are fully supported by Microsoft.</span></span>
>
> <span data-ttu-id="5670c-115">Componentes personalizados, como Solr, recebem suporte comercialmente razoável toohelp toofurther você solucionar o problema de saudação.</span><span class="sxs-lookup"><span data-stu-id="5670c-115">Custom components, such as Solr, receive commercially reasonable support toohelp you toofurther troubleshoot hello issue.</span></span> <span data-ttu-id="5670c-116">O suporte da Microsoft pode não ser capaz de tooresolve problemas com componentes personalizados.</span><span class="sxs-lookup"><span data-stu-id="5670c-116">Microsoft support may not be able tooresolve problems with custom components.</span></span> <span data-ttu-id="5670c-117">Talvez seja necessário comunidades de código-fonte aberto Olá tooengage para obter assistência.</span><span class="sxs-lookup"><span data-stu-id="5670c-117">You may need tooengage hello open source communities for assistance.</span></span> <span data-ttu-id="5670c-118">Por exemplo, há muitos sites de comunidades que podem ser usados, como o [Fórum do MSDN para o HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Além disso, os projetos do Apache têm sites do projeto em [http://apache.org](http://apache.org), por exemplo: [Hadoop](http://hadoop.apache.org/).</span><span class="sxs-lookup"><span data-stu-id="5670c-118">For example, there are many community sites that can be used, like: [MSDN forum for HDInsight](https://social.msdn.microsoft.com/Forums/azure/en-US/home?forum=hdinsight), [http://stackoverflow.com](http://stackoverflow.com). Also Apache projects have project sites on [http://apache.org](http://apache.org), for example: [Hadoop](http://hadoop.apache.org/).</span></span>

## <a name="what-hello-script-does"></a><span data-ttu-id="5670c-119">O script hello faz</span><span class="sxs-lookup"><span data-stu-id="5670c-119">What hello script does</span></span>

<span data-ttu-id="5670c-120">Esse script faz Olá cluster do HDInsight toohello alterações a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-120">This script makes hello following changes toohello HDInsight cluster:</span></span>

* <span data-ttu-id="5670c-121">Instala o Solr 4.9 em `/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="5670c-121">Installs Solr 4.9 into `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="5670c-122">Cria um usuário, **solrusr**, que é usado toorun Olá Solr serviço</span><span class="sxs-lookup"><span data-stu-id="5670c-122">Creates a user, **solrusr**, which is used toorun hello Solr service</span></span>
* <span data-ttu-id="5670c-123">Conjuntos de **solruser** como proprietário de saudação do`/usr/hdp/current/solr`</span><span class="sxs-lookup"><span data-stu-id="5670c-123">Sets **solruser** as hello owner of `/usr/hdp/current/solr`</span></span>
* <span data-ttu-id="5670c-124">Adiciona uma configuração [Upstart](http://upstart.ubuntu.com/) que inicia automaticamente o Solr.</span><span class="sxs-lookup"><span data-stu-id="5670c-124">Adds an [Upstart](http://upstart.ubuntu.com/) configuration that starts Solr automatically.</span></span>

## <span data-ttu-id="5670c-125"><a name="install"></a>Instalar o Solr usando ações de script</span><span class="sxs-lookup"><span data-stu-id="5670c-125"><a name="install"></a>Install Solr using Script Actions</span></span>

<span data-ttu-id="5670c-126">Tooinstall um script de exemplo Solr em um cluster HDInsight está disponível em Olá local a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-126">A sample script tooinstall Solr on an HDInsight cluster is available at hello following location:</span></span>

    https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh

<span data-ttu-id="5670c-127">toocreate um cluster que tem Solr instalado, use Olá etapas Olá [HDInsight criar clusters](hdinsight-hadoop-create-linux-clusters-portal.md) documento.</span><span class="sxs-lookup"><span data-stu-id="5670c-127">toocreate a cluster that has Solr installed, use hello steps in hello [Create HDInsight clusters](hdinsight-hadoop-create-linux-clusters-portal.md) document.</span></span> <span data-ttu-id="5670c-128">Durante o processo de criação de hello, use Olá etapas tooinstall Solr a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-128">During hello creation process, use hello following steps tooinstall Solr:</span></span>

1. <span data-ttu-id="5670c-129">De saudação __resumo do Cluster__ folha, select__Advanced settings__, em seguida, __ações de Script__.</span><span class="sxs-lookup"><span data-stu-id="5670c-129">From hello __Cluster summary__ blade, select__Advanced settings__, then __Script actions__.</span></span> <span data-ttu-id="5670c-130">Use Olá formulário de saudação toopopulate informações a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-130">Use hello following information toopopulate hello form:</span></span>

   * <span data-ttu-id="5670c-131">**NOME**: insira um nome amigável para a ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="5670c-131">**NAME**: Enter a friendly name for hello script action.</span></span>
   * <span data-ttu-id="5670c-132">**URI do SCRIPT**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span><span class="sxs-lookup"><span data-stu-id="5670c-132">**SCRIPT URI**: https://hdiconfigactions.blob.core.windows.net/linuxsolrconfigactionv01/solr-installer-v01.sh</span></span>
   * <span data-ttu-id="5670c-133">**CABEÇALHO**: marque esta opção</span><span class="sxs-lookup"><span data-stu-id="5670c-133">**HEAD**: Check this option</span></span>
   * <span data-ttu-id="5670c-134">**TRABALHO**: marque esta opção</span><span class="sxs-lookup"><span data-stu-id="5670c-134">**WORKER**: Check this option</span></span>
   * <span data-ttu-id="5670c-135">**ZOOKEEPER**: verificar tooinstall essa opção no nó de Zookeeper Olá</span><span class="sxs-lookup"><span data-stu-id="5670c-135">**ZOOKEEPER**: Check this option tooinstall on hello Zookeeper node</span></span>
   * <span data-ttu-id="5670c-136">**PARÂMETROS**: deixe este campo em branco</span><span class="sxs-lookup"><span data-stu-id="5670c-136">**PARAMETERS**: Leave this field blank</span></span>

2. <span data-ttu-id="5670c-137">Na parte inferior de saudação do hello **ações de Script** folha, use Olá **selecione** configuração de saudação do botão toosave.</span><span class="sxs-lookup"><span data-stu-id="5670c-137">At hello bottom of hello **Script actions** blade, use hello **Select** button toosave hello configuration.</span></span> <span data-ttu-id="5670c-138">Por fim, use Olá **próximo** botão tooreturn toohello __resumo do Cluster__</span><span class="sxs-lookup"><span data-stu-id="5670c-138">Finally, use hello **Next** button tooreturn toohello __Cluster summary__</span></span>

3. <span data-ttu-id="5670c-139">De saudação __resumo do Cluster__ página, selecione __criar__ toocreate cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="5670c-139">From hello __Cluster summary__ page, select __Create__ toocreate hello cluster.</span></span>

## <span data-ttu-id="5670c-140"><a name="usesolr"></a>Como usar o Solr no HDInsight</span><span class="sxs-lookup"><span data-stu-id="5670c-140"><a name="usesolr"></a>How do I use Solr in HDInsight</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5670c-141">etapas de Olá nesta seção demonstram a funcionalidade básica do Solr.</span><span class="sxs-lookup"><span data-stu-id="5670c-141">hello steps in this section demonstrate basic Solr functionality.</span></span> <span data-ttu-id="5670c-142">Para obter mais informações sobre como usar Solr, consulte Olá [Solr Apache site](http://lucene.apache.org/solr/).</span><span class="sxs-lookup"><span data-stu-id="5670c-142">For more information on using Solr, see hello [Apache Solr site](http://lucene.apache.org/solr/).</span></span>

### <a name="index-data"></a><span data-ttu-id="5670c-143">Dados de índice</span><span class="sxs-lookup"><span data-stu-id="5670c-143">Index data</span></span>

<span data-ttu-id="5670c-144">Use Olá tooSolr de dados de exemplo de tooadd as etapas a seguir e, em seguida, consultá-los:</span><span class="sxs-lookup"><span data-stu-id="5670c-144">Use hello following steps tooadd example data tooSolr, and then query it:</span></span>

1. <span data-ttu-id="5670c-145">Conecte o cluster do HDInsight toohello usando SSH:</span><span class="sxs-lookup"><span data-stu-id="5670c-145">Connect toohello HDInsight cluster using SSH:</span></span>

    ```bash
    ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net
    ```

    <span data-ttu-id="5670c-146">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5670c-146">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="5670c-147">As etapas neste documento usam SSL túnel tooconnect toohello Solr da web da interface do usuário.</span><span class="sxs-lookup"><span data-stu-id="5670c-147">Steps later in this document use an SSL tunnel tooconnect toohello Solr web UI.</span></span> <span data-ttu-id="5670c-148">toouse essas etapas, você deve estabelecer um SSL de túnel e, em seguida, configure seu navegador toouse-lo.</span><span class="sxs-lookup"><span data-stu-id="5670c-148">toouse these steps, you must establish an SSL tunnel and then configure your browser toouse it.</span></span>
     >
     > <span data-ttu-id="5670c-149">Para obter mais informações, consulte Olá [usar SSH de encapsulamento HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="5670c-149">For more information, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

2. <span data-ttu-id="5670c-150">Use Olá dados de exemplo do comandos toohave Solr índice a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-150">Use hello following commands toohave Solr index sample data:</span></span>

    ```bash
    cd /usr/hdp/current/solr/example/exampledocs
    java -jar post.jar solr.xml monitor.xml
    ```

    <span data-ttu-id="5670c-151">Olá saída a seguir será retornada toohello console:</span><span class="sxs-lookup"><span data-stu-id="5670c-151">hello following output is returned toohello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="5670c-152">Olá `post.jar` utilitário adiciona Olá **solr.xml** e **monitor.xml** índice de toohello de documentos.</span><span class="sxs-lookup"><span data-stu-id="5670c-152">hello `post.jar` utility adds hello **solr.xml** and **monitor.xml** documents toohello index.</span></span>
  
3. <span data-ttu-id="5670c-153">Use Olá Olá do comando tooquery Solr API de REST a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-153">Use hello following command tooquery hello Solr REST API:</span></span>

    ```bash
    curl "http://localhost:8983/solr/collection1/select?q=*%3A*&wt=json&indent=true"
    ```

    <span data-ttu-id="5670c-154">Este comando localiza **collection1** para documentos que correspondam a  **\*:\***  (codificado como \*% 3A\* na cadeia de caracteres de consulta de saudação).</span><span class="sxs-lookup"><span data-stu-id="5670c-154">This command searches **collection1** for any documents matching **\*:\*** (encoded as \*%3A\* in hello query string).</span></span> <span data-ttu-id="5670c-155">Olá documento JSON a seguir está um exemplo de resposta de saudação:</span><span class="sxs-lookup"><span data-stu-id="5670c-155">hello following JSON document is an example of hello response:</span></span>

            "response": {
                "numFound": 2,
                "start": 0,
                "maxScore": 1,
                "docs": [
                  {
                    "id": "SOLR1000",
                    "name": "Solr, hello Enterprise Search Server",
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
                      "Scalability - Efficient Replication tooother Solr Search Servers",
                      "Flexible and Adaptable with XML configuration and Schema",
                      "Good unicode support: héllo (hello with an accent over hello e)"
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

### <a name="using-hello-solr-dashboard"></a><span data-ttu-id="5670c-156">Usando o painel de Solr Olá</span><span class="sxs-lookup"><span data-stu-id="5670c-156">Using hello Solr dashboard</span></span>

<span data-ttu-id="5670c-157">Painel de Solr Olá é uma interface que permite que você toowork com Solr através do seu navegador da web.</span><span class="sxs-lookup"><span data-stu-id="5670c-157">hello Solr dashboard is a web UI that allows you toowork with Solr through your web browser.</span></span> <span data-ttu-id="5670c-158">Painel de Solr Olá não seja exposto diretamente no Olá da Internet do seu cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5670c-158">hello Solr dashboard is not exposed directly on hello Internet from your HDInsight cluster.</span></span> <span data-ttu-id="5670c-159">Você pode usar um tooaccess de túnel SSH-lo.</span><span class="sxs-lookup"><span data-stu-id="5670c-159">You can use an SSH tunnel tooaccess it.</span></span> <span data-ttu-id="5670c-160">Para obter mais informações sobre o uso de um túnel SSH, consulte Olá [usar SSH de encapsulamento HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) documento.</span><span class="sxs-lookup"><span data-stu-id="5670c-160">For more information on using an SSH tunnel, see hello [Use SSH Tunneling with HDInsight](hdinsight-linux-ambari-ssh-tunnel.md) document.</span></span>

<span data-ttu-id="5670c-161">Depois de estabelecer um túnel SSH, use Olá painel de Solr de saudação de toouse etapas a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-161">Once you have established an SSH tunnel, use hello following steps toouse hello Solr dashboard:</span></span>

1. <span data-ttu-id="5670c-162">Determine o nome do host de saudação para um nó principal do hello primário:</span><span class="sxs-lookup"><span data-stu-id="5670c-162">Determine hello host name for hello primary headnode:</span></span>

   1. <span data-ttu-id="5670c-163">Use o nó principal do cluster SSH tooconnect toohello.</span><span class="sxs-lookup"><span data-stu-id="5670c-163">Use SSH tooconnect toohello cluster head node.</span></span> <span data-ttu-id="5670c-164">Por exemplo: `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span><span class="sxs-lookup"><span data-stu-id="5670c-164">For example, `ssh USERNAME@CLUSTERNAME-ssh.azurehdinsight.net`.</span></span>

       <span data-ttu-id="5670c-165">Para obter mais informações sobre como usar SSH, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="5670c-165">For more information on using SSH, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

   2. <span data-ttu-id="5670c-166">Use Olá tooget Olá nome de host totalmente qualificado do comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-166">Use hello following command tooget hello fully qualified hostname:</span></span>

        ```bash
        hostname -f
        ```

        <span data-ttu-id="5670c-167">Este comando retorna um toohello semelhante valor após o nome do host:</span><span class="sxs-lookup"><span data-stu-id="5670c-167">This command returns a value similar toohello following host name:</span></span>

            hn0-myhdi-nfebtpfdv1nubcidphpap2eq2b.ex.internal.cloudapp.net

        <span data-ttu-id="5670c-168">Salve o valor de saudação retornado, pois ele é usado mais tarde.</span><span class="sxs-lookup"><span data-stu-id="5670c-168">Save hello value returned, as it is used later.</span></span>

2. <span data-ttu-id="5670c-169">No seu navegador, conecte-se muito**solr/http://HOSTNAME:8983 / #/**, onde **HOSTNAME** é Olá nome determinado nas etapas anteriores hello.</span><span class="sxs-lookup"><span data-stu-id="5670c-169">In your browser, connect too**http://HOSTNAME:8983/solr/#/**, where **HOSTNAME** is hello name you determined in hello previous steps.</span></span>

    <span data-ttu-id="5670c-170">Olá solicitação é encaminhada por meio de saudação SSH túnel toohello Solr interface da web em seu cluster.</span><span class="sxs-lookup"><span data-stu-id="5670c-170">hello request is routed through hello SSH tunnel toohello Solr web UI on your cluster.</span></span> <span data-ttu-id="5670c-171">Olá aparecerá semelhante toohello imagem a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-171">hello page appears similar toohello following image:</span></span>

    ![Imagem do painel do Solr](./media/hdinsight-hadoop-solr-install-linux/solrdashboard.png)

3. <span data-ttu-id="5670c-173">No painel esquerdo do hello, use Olá **Core seletor** suspensa tooselect **collection1**.</span><span class="sxs-lookup"><span data-stu-id="5670c-173">From hello left pane, use hello **Core Selector** drop-down tooselect **collection1**.</span></span> <span data-ttu-id="5670c-174">Várias entradas deverão aparecer abaixo de **collection1**.</span><span class="sxs-lookup"><span data-stu-id="5670c-174">Several entries should them appear below **collection1**.</span></span>

4. <span data-ttu-id="5670c-175">Entradas de saudação abaixo **collection1**, selecione **consulta**.</span><span class="sxs-lookup"><span data-stu-id="5670c-175">From hello entries below **collection1**, select **Query**.</span></span> <span data-ttu-id="5670c-176">Use Olá página de pesquisa de saudação de toopopulate valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-176">Use hello following values toopopulate hello search page:</span></span>

   * <span data-ttu-id="5670c-177">Em Olá **p** texto, digite  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="5670c-177">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="5670c-178">Essa consulta retorna todos os documentos de saudação que são indexados em Solr.</span><span class="sxs-lookup"><span data-stu-id="5670c-178">This query returns all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="5670c-179">Se você quiser toosearch para uma cadeia de caracteres específica dentro de documentos hello, você pode inserir essa cadeia de caracteres aqui.</span><span class="sxs-lookup"><span data-stu-id="5670c-179">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="5670c-180">Em Olá **wt** caixa de texto, selecione Olá formato de saída.</span><span class="sxs-lookup"><span data-stu-id="5670c-180">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="5670c-181">O padrão é **json**.</span><span class="sxs-lookup"><span data-stu-id="5670c-181">Default is **json**.</span></span>

     <span data-ttu-id="5670c-182">Por fim, selecione Olá **executar consulta** botão na parte inferior de saudação do e de pesquisa de saudação.</span><span class="sxs-lookup"><span data-stu-id="5670c-182">Finally, select hello **Execute Query** button at hello bottom of hello search pate.</span></span>

     ![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-solr-install-linux/hdi-solr-dashboard-query.png)

     <span data-ttu-id="5670c-184">saída de Hello retorna Olá dois documentos que você adicionou toohello índice anteriormente.</span><span class="sxs-lookup"><span data-stu-id="5670c-184">hello output returns hello two documents that you added toohello index earlier.</span></span> <span data-ttu-id="5670c-185">saudação de saída é similar toohello documento JSON a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-185">hello output is similar toohello following JSON document:</span></span>

           "response": {
               "numFound": 2,
               "start": 0,
               "maxScore": 1,
               "docs": [
                 {
                   "id": "SOLR1000",
                   "name": "Solr, hello Enterprise Search Server",
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
                     "Scalability - Efficient Replication tooother Solr Search Servers",
                     "Flexible and Adaptable with XML configuration and Schema",
                     "Good unicode support: héllo (hello with an accent over hello e)"
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

### <a name="starting-and-stopping-solr"></a><span data-ttu-id="5670c-186">Iniciando e parando o Solr</span><span class="sxs-lookup"><span data-stu-id="5670c-186">Starting and stopping Solr</span></span>

<span data-ttu-id="5670c-187">Use Olá toomanually parar e iniciar Solr de comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-187">Use hello following commands toomanually stop and start Solr:</span></span>

```bash
sudo stop solr
sudo start solr
```

## <a name="backup-indexed-data"></a><span data-ttu-id="5670c-188">Backup de dados indexados</span><span class="sxs-lookup"><span data-stu-id="5670c-188">Backup indexed data</span></span>

<span data-ttu-id="5670c-189">Use Olá etapas tooback o armazenamento do Solr dados toohello padrão para o cluster a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-189">Use hello following steps tooback up Solr data toohello default storage for your cluster:</span></span>

1. <span data-ttu-id="5670c-190">Conectar-se o cluster toohello usando SSH, use Olá após o nome de host do comando tooget Olá para o nó principal hello:</span><span class="sxs-lookup"><span data-stu-id="5670c-190">Connect toohello cluster using SSH, then use hello following command tooget hello host name for hello head node:</span></span>

    ```bash
    hostname -f
    ```

2. <span data-ttu-id="5670c-191">Use Olá comando toocreate um instantâneo dos dados indexado de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="5670c-191">Use hello following command toocreate a snapshot of hello indexed data.</span></span> <span data-ttu-id="5670c-192">Substituir **HOSTNAME** com nome hello retornado pelo comando anterior hello:</span><span class="sxs-lookup"><span data-stu-id="5670c-192">Replace **HOSTNAME** with hello name returned from hello previous command:</span></span>

    ```bash
    curl http://HOSTNAME:8983/solr/replication?command=backup
    ```

    <span data-ttu-id="5670c-193">resposta de saudação é semelhante toohello XML a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-193">hello response is similar toohello following XML:</span></span>

        <?xml version="1.0" encoding="UTF-8"?>
        <response>
          <lst name="responseHeader">
            <int name="status">0</int>
            <int name="QTime">9</int>
          </lst>
          <str name="status">OK</str>
        </response>

3. <span data-ttu-id="5670c-194">Altere os diretórios muito`/usr/hdp/current/solr/example/solr`.</span><span class="sxs-lookup"><span data-stu-id="5670c-194">Change directories too`/usr/hdp/current/solr/example/solr`.</span></span> <span data-ttu-id="5670c-195">Há um subdiretório aqui para cada coleção.</span><span class="sxs-lookup"><span data-stu-id="5670c-195">There is a subdirectory here for each collection.</span></span> <span data-ttu-id="5670c-196">O diretório de cada coleção contém um `data` diretório que contém o instantâneo Olá para coleção hello.</span><span class="sxs-lookup"><span data-stu-id="5670c-196">Each collection directory contains a `data` directory that contains hello snapshot for hello collection.</span></span>

4. <span data-ttu-id="5670c-197">toocreate um arquivo compactado de pasta de instantâneo de Olá Olá use comandos a seguir:</span><span class="sxs-lookup"><span data-stu-id="5670c-197">toocreate a compressed archive of hello snapshot folder, use hello following command:</span></span>

    ```bash
    tar -zcf snapshot.20150806185338855.tgz snapshot.20150806185338855
    ```

    <span data-ttu-id="5670c-198">Substituir saudação `snapshot.20150806185338855` valores com o nome de saudação do instantâneo Olá para sua coleção.</span><span class="sxs-lookup"><span data-stu-id="5670c-198">Replace hello `snapshot.20150806185338855` values with hello name of hello snapshot for your collection.</span></span>

    <span data-ttu-id="5670c-199">Este comando cria um arquivo chamado **snapshot.20150806185338855.tgz**, que contém o conteúdo de saudação do hello **snapshot.20150806185338855** directory.</span><span class="sxs-lookup"><span data-stu-id="5670c-199">This command creates an archive named **snapshot.20150806185338855.tgz**, which contains hello contents of hello **snapshot.20150806185338855** directory.</span></span>

5. <span data-ttu-id="5670c-200">Em seguida, você pode armazenar o armazenamento primário do cluster de toohello arquivo hello, usando o comando a seguir de saudação:</span><span class="sxs-lookup"><span data-stu-id="5670c-200">You can then store hello archive toohello cluster's primary storage using hello following command:</span></span>

    ```bash
    hdfs dfs -put snapshot.20150806185338855.tgz /example/data
    ```

<span data-ttu-id="5670c-201">Para obter mais informações sobre como trabalhar com backups e restaurações do Solr, consulte [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span><span class="sxs-lookup"><span data-stu-id="5670c-201">For more information on working with Solr backup and restores, see [https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups](https://cwiki.apache.org/confluence/display/solr/Making+and+Restoring+Backups).</span></span>

## <a name="next-steps"></a><span data-ttu-id="5670c-202">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="5670c-202">Next steps</span></span>

* <span data-ttu-id="5670c-203">[Instalar o Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5670c-203">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install-linux.md).</span></span> <span data-ttu-id="5670c-204">Use cluster personalização tooinstall que giraph no Hadoop de HDInsight clusters.</span><span class="sxs-lookup"><span data-stu-id="5670c-204">Use cluster customization tooinstall Giraph on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="5670c-205">Giraph permite gráfico tooperform processamento usando Hadoop e pode ser usado com o Azure HDInsight.</span><span class="sxs-lookup"><span data-stu-id="5670c-205">Giraph allows you tooperform graph processing by using Hadoop, and can be used with Azure HDInsight.</span></span>

* <span data-ttu-id="5670c-206">[Instalar matiz em clusters HDInsight](hdinsight-hadoop-hue-linux.md).</span><span class="sxs-lookup"><span data-stu-id="5670c-206">[Install Hue on HDInsight clusters](hdinsight-hadoop-hue-linux.md).</span></span> <span data-ttu-id="5670c-207">Use o matiz de tooinstall de personalização de cluster em clusters de HDInsight Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5670c-207">Use cluster customization tooinstall Hue on HDInsight Hadoop clusters.</span></span> <span data-ttu-id="5670c-208">O matiz é que um conjunto de aplicativos da Web usado toointeract com um cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="5670c-208">Hue is a set of Web applications used toointeract with a Hadoop cluster.</span></span>

[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster-linux.md
