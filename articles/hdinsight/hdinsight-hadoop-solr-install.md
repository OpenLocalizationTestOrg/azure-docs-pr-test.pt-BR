---
title: "Ação de Script de aaaUse tooinstall Solr no cluster de Hadoop - Azure | Microsoft Docs"
description: "Saiba como toocustomize HDInsight cluster com Solr usando a ação de Script."
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: b1e6f338-8ac1-4b38-bbb5-2f7388b9de3b
ms.service: hdinsight
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/05/2016
ms.author: nitinme
ROBOTS: NOINDEX
ms.openlocfilehash: 022ba56b7499390a91bfe869e5069893e56b6503
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="7ef6f-103">Instalar e usar o Solr em clusters HDInsight baseados no Windows</span><span class="sxs-lookup"><span data-stu-id="7ef6f-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="7ef6f-104">Saiba como toocustomize HDInsight baseados em Windows cluster com Solr usando a ação de Script e toouse Solr toosearch dados.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-104">Learn how toocustomize Windows-based HDInsight cluster with Solr using Script Action, and how toouse Solr toosearch data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7ef6f-105">Olá etapas para esse documento só funciona com clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-105">hello steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="7ef6f-106">O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="7ef6f-107">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-107">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="7ef6f-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="7ef6f-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="7ef6f-109">Para obter informações sobre como usar o Solr com um cluster baseado no Linux, consulte [Instalar e usar o Solr em clusters Hadoop do HDinsight (Linux)](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6f-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="7ef6f-110">Você pode instalar o Solr em qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight usando a *Ação de Script*.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="7ef6f-111">Tooinstall um script de exemplo Solr em um cluster HDInsight está disponível de um blob de armazenamento do Azure somente leitura em [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="7ef6f-111">A sample script tooinstall Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="7ef6f-112">script de exemplo Hello funciona apenas com a versão 3.1 do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-112">hello sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="7ef6f-113">Para obter mais informações sobre as versões do cluster HDInsight, consulte [Versões do cluster HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6f-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="7ef6f-114">script de exemplo Hello usado neste tópico cria um cluster de Solr baseados no Windows com uma configuração específica.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-114">hello sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="7ef6f-115">Se desejar que o cluster de Solr tooconfigure Olá com diferentes coleções, fragmentos, esquemas, réplicas, etc., você deve modificar Solr binários e script hello adequadamente.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-115">If you want tooconfigure hello Solr cluster with different collections, shards, schemas, replicas, etc., you must modify hello script and Solr binaries accordingly.</span></span>

<span data-ttu-id="7ef6f-116">**Artigos relacionados**</span><span class="sxs-lookup"><span data-stu-id="7ef6f-116">**Related articles**</span></span>

* [<span data-ttu-id="7ef6f-117">Instalar e usar o Solr em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="7ef6f-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="7ef6f-118">[Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ef6f-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="7ef6f-119">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="7ef6f-120">[Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="7ef6f-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="7ef6f-121">O que é Solr?</span><span class="sxs-lookup"><span data-stu-id="7ef6f-121">What is Solr?</span></span>
<span data-ttu-id="7ef6f-122">O <a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> é uma plataforma de pesquisa empresarial que habilita operações poderosas de pesquisa de texto completo nos dados.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="7ef6f-123">Enquanto o Hadoop permite armazenar e gerenciar grandes quantidades de dados, o Apache Solr fornece recursos de pesquisa de saudação tooquickly recupera dados de saudação.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides hello search capabilities tooquickly retrieve hello data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="7ef6f-124">Instalar o Solr usando o Portal</span><span class="sxs-lookup"><span data-stu-id="7ef6f-124">Install Solr using portal</span></span>
1. <span data-ttu-id="7ef6f-125">Começar a criar um cluster usando Olá **criação personalizada** opção, conforme descrito em [Hadoop criar clusters de HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="7ef6f-125">Start creating a cluster by using hello **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="7ef6f-126">Em Olá **ações de Script** página do Assistente de saudação, clique em **Adicionar ação de script** tooprovide detalhes sobre a ação de script hello, conforme mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="7ef6f-126">On hello **Script Actions** page of hello wizard, click **add script action** tooprovide details about hello script action, as shown below:</span></span>

    <span data-ttu-id="7ef6f-127">![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "toocustomize de ação de Script de Use um cluster")</span><span class="sxs-lookup"><span data-stu-id="7ef6f-127">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action toocustomize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="7ef6f-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="7ef6f-128">Property</span></span></th><th><span data-ttu-id="7ef6f-129">Valor</span><span class="sxs-lookup"><span data-stu-id="7ef6f-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="7ef6f-130">Nome</span><span class="sxs-lookup"><span data-stu-id="7ef6f-130">Name</span></span></td>
            <td><span data-ttu-id="7ef6f-131">Especifique um nome para a ação de script hello.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-131">Specify a name for hello script action.</span></span> <span data-ttu-id="7ef6f-132">Por exemplo, <b>Instalar o Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="7ef6f-133">URI do script</span><span class="sxs-lookup"><span data-stu-id="7ef6f-133">Script URI</span></span></td>
            <td><span data-ttu-id="7ef6f-134">Especifique o script hello de toohello de identificador de recurso uniforme (URI) que é invocado toocustomize Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-134">Specify hello Uniform Resource Identifier (URI) toohello script that is invoked toocustomize hello cluster.</span></span> <span data-ttu-id="7ef6f-135">Por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="7ef6f-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="7ef6f-136">Tipo de nó</span><span class="sxs-lookup"><span data-stu-id="7ef6f-136">Node Type</span></span></td>
            <td><span data-ttu-id="7ef6f-137">Especifica Olá nós em que o script de personalização de saudação é executado.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-137">Specify hello nodes on which hello customization script is run.</span></span> <span data-ttu-id="7ef6f-138">Você pode escolher <b>Todos os nós</b>, <b>Somente nós do cabeçalho</b> ou <b>Somente nós de trabalho</b>.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="7ef6f-139">parâmetros</span><span class="sxs-lookup"><span data-stu-id="7ef6f-139">Parameters</span></span></td>
            <td><span data-ttu-id="7ef6f-140">Especifica parâmetros de hello, se exigido pelo script hello.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-140">Specify hello parameters, if required by hello script.</span></span> <span data-ttu-id="7ef6f-141">Olá script tooinstall Solr não requer nenhum parâmetro, você poderá deixar isso em branco.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-141">hello script tooinstall Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="7ef6f-142">Você pode adicionar mais de um tooinstall de ação de script vários componentes no cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-142">You can add more than one script action tooinstall multiple components on hello cluster.</span></span> <span data-ttu-id="7ef6f-143">Depois de adicionar scripts de saudação, clique em Olá toostart de marca de seleção Criar cluster hello.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-143">After you have added hello scripts, click hello checkmark toostart creating hello cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="7ef6f-144">Usar o Solr</span><span class="sxs-lookup"><span data-stu-id="7ef6f-144">Use Solr</span></span>
<span data-ttu-id="7ef6f-145">Você deve começar com indexação Solr, com alguns arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="7ef6f-146">Você pode usar consultas de pesquisa do Solr toorun nos dados hello indexado.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-146">You can then use Solr toorun search queries on hello indexed data.</span></span> <span data-ttu-id="7ef6f-147">Execute Olá etapas toouse Solr em um cluster do HDInsight a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ef6f-147">Perform hello following steps toouse Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="7ef6f-148">**Usar protocolo de área de trabalho remota (RDP) tooremote em cluster do HDInsight Olá com Solr instalado**.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-148">**Use Remote Desktop Protocol (RDP) tooremote into hello HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="7ef6f-149">De Olá portal do Azure, habilite área de trabalho remota para cluster Olá criado com o cluster de saudação instalado e, em seguida, remoto em Solr.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-149">From hello Azure portal, enable Remote Desktop for hello cluster you created with Solr installed, and then remote into hello cluster.</span></span> <span data-ttu-id="7ef6f-150">Para obter instruções, consulte [conectar tooHDInsight clusters usando o RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="7ef6f-150">For instructions, see [Connect tooHDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="7ef6f-151">**Indexar o Solr carregando arquivos de dados**.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="7ef6f-152">Quando você indexar Solr, você colocar os documentos que talvez seja necessário toosearch em.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-152">When you index Solr, you put documents in it that you may need toosearch on.</span></span> <span data-ttu-id="7ef6f-153">tooindex Solr, use tooremote RDP em cluster Olá, navegue toohello área de trabalho, abra a linha de comando do Hadoop hello e navegar muito**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-153">tooindex Solr, use RDP tooremote into hello cluster, navigate toohello desktop, open hello Hadoop command line, and navigate too**C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="7ef6f-154">Execute Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ef6f-154">Run hello following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="7ef6f-155">Você verá Olá saída a seguir no console de saudação:</span><span class="sxs-lookup"><span data-stu-id="7ef6f-155">You'll see hello following output on hello console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes toohttp://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="7ef6f-156">Utilitário de post.jar Olá índices Solr com dois documentos de exemplo, **solr.xml** e **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-156">hello post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="7ef6f-157">Utilitário de post.jar Hello e documentos de exemplo hello estão disponíveis com a instalação do Solr.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-157">hello post.jar utility and hello sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="7ef6f-158">**Use Olá Solr painel toosearch em hello indexado documentos**.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-158">**Use hello Solr dashboard toosearch within hello indexed documents**.</span></span> <span data-ttu-id="7ef6f-159">Em Olá RDP sessão toohello HDInsight cluster, abra o Internet Explorer e iniciar Olá Solr painel em **solr/http://headnodehost:8983 / #/**.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-159">In hello RDP session toohello HDInsight cluster, open Internet Explorer, and launch hello Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="7ef6f-160">No painel esquerdo hello, de saudação **Core seletor** lista suspensa, selecione **collection1**e dentro dele, clique em **consulta**.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-160">From hello left pane, from hello **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="7ef6f-161">Como um exemplo, tooselect e retornar todos os documentos de saudação em Solr, fornecer Olá valores a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ef6f-161">As an example, tooselect and return all hello docs in Solr, provide hello following values:</span></span>

   * <span data-ttu-id="7ef6f-162">Em Olá **p** texto, digite  **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-162">In hello **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="7ef6f-163">Isso retornará todos os documentos de saudação que são indexados Solr.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-163">This will return all hello documents that are indexed in Solr.</span></span> <span data-ttu-id="7ef6f-164">Se você quiser toosearch para uma cadeia de caracteres específica dentro de documentos hello, você pode inserir essa cadeia de caracteres aqui.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-164">If you want toosearch for a specific string within hello documents, you can enter that string here.</span></span>
   * <span data-ttu-id="7ef6f-165">Em Olá **wt** caixa de texto, selecione Olá formato de saída.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-165">In hello **wt** text box, select hello output format.</span></span> <span data-ttu-id="7ef6f-166">O padrão é **json**.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-166">Default is **json**.</span></span> <span data-ttu-id="7ef6f-167">Clique em **Executar consulta**.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="7ef6f-168">![Use a ação de Script toocustomize um cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "executar uma consulta no painel Solr")</span><span class="sxs-lookup"><span data-stu-id="7ef6f-168">![Use Script Action toocustomize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="7ef6f-169">saída de Hello retorna Olá dois documentos que foram usados para indexação Solr.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-169">hello output returns hello two docs that we used for indexing Solr.</span></span> <span data-ttu-id="7ef6f-170">saída de Hello é semelhante a seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="7ef6f-170">hello output resembles hello following:</span></span>

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
4. <span data-ttu-id="7ef6f-171">**Recomendado: Backup hello indexado dados de Solr tooAzure armazenamento Blob associado do cluster do HDInsight Olá**.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-171">**Recommended: Back up hello indexed data from Solr tooAzure Blob storage associated with hello HDInsight cluster**.</span></span> <span data-ttu-id="7ef6f-172">Como uma prática recomendada, você deve fazer backup de dados indexado de saudação de nós de cluster Solr Olá para o armazenamento de BLOBs do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-172">As a good practice, you should back up hello indexed data from hello Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="7ef6f-173">Execute Olá toodo as etapas a seguir para:</span><span class="sxs-lookup"><span data-stu-id="7ef6f-173">Perform hello following steps toodo so:</span></span>

   1. <span data-ttu-id="7ef6f-174">Da sessão RDP hello, abra o Internet Explorer e toohello de ponto de URL a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ef6f-174">From hello RDP session, open Internet Explorer, and point toohello following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="7ef6f-175">Você verá uma resposta semelhante a essa:</span><span class="sxs-lookup"><span data-stu-id="7ef6f-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="7ef6f-176">Na sessão remota do hello, navegue muito {SOLR_HOME}\{coleção} \data.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-176">In hello remote session, navigate too{SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="7ef6f-177">Para o cluster Olá criado por meio do script de exemplo hello, esta deve ser **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-177">For hello cluster created via hello sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="7ef6f-178">Nesse local, você deve ver uma pasta de instantâneo criada com um nome semelhante muito**instantâneo.* carimbo de hora** *.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-178">At this location, you should see a snapshot folder created with a name similar too**snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="7ef6f-179">Compacte a pasta de instantâneo hello e carregá-lo tooAzure o armazenamento de Blob.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-179">Zip hello snapshot folder and upload it tooAzure Blob storage.</span></span> <span data-ttu-id="7ef6f-180">Na linha de comando do Hadoop hello, navegar toohello local da pasta de instantâneo hello usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="7ef6f-180">From hello Hadoop command line, navigate toohello location of hello snapshot folder by using hello following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="7ef6f-181">Este comando cópias Olá instantâneo muito / / dados de exemplo/no contêiner Olá no padrão de saudação armazenamento conta associada Olá cluster.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-181">This command copies hello snapshot too/example/data/ under hello container within hello default Storage account associated with hello cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="7ef6f-182">Instalar o Solr usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="7ef6f-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="7ef6f-183">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="7ef6f-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="7ef6f-184">exemplo Hello demonstra como tooinstall Spark usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-184">hello sample demonstrates how tooinstall Spark using Azure PowerShell.</span></span> <span data-ttu-id="7ef6f-185">Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="7ef6f-185">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="7ef6f-186">Instalar o Solr usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="7ef6f-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="7ef6f-187">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="7ef6f-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="7ef6f-188">exemplo Hello demonstra como tooinstall Spark usando Olá .NET SDK.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-188">hello sample demonstrates how tooinstall Spark using hello .NET SDK.</span></span> <span data-ttu-id="7ef6f-189">Você precisa toocustomize Olá script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="7ef6f-189">You need toocustomize hello script toouse [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="7ef6f-190">Consulte também</span><span class="sxs-lookup"><span data-stu-id="7ef6f-190">See also</span></span>
* [<span data-ttu-id="7ef6f-191">Instalar e usar o Solr em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="7ef6f-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="7ef6f-192">[Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="7ef6f-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="7ef6f-193">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="7ef6f-194">[Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="7ef6f-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="7ef6f-195">[Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]: exemplo de Ação de Script sobre a instalação do Spark.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="7ef6f-196">[Instalar R em clusters HDInsight][hdinsight-install-r]: exemplo de Ação de Script sobre a instalação do R.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="7ef6f-197">[Instalar Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md): exemplo de Ação de Script sobre a instalação do Giraph.</span><span class="sxs-lookup"><span data-stu-id="7ef6f-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
