---
title: "Use a ação de Script para instalar o Solr em cluster Hadoop – Azure | Microsoft Docs"
description: "Saiba como personalizar o cluster HDInsight com o Solr usando a Ação de Script."
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
ms.openlocfilehash: 6efb7ea26c3cdf7748fff4b02b5810c85cc41e1a
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="install-and-use-solr-on-windows-based-hdinsight-clusters"></a><span data-ttu-id="84cc1-103">Instalar e usar o Solr em clusters HDInsight baseados no Windows</span><span class="sxs-lookup"><span data-stu-id="84cc1-103">Install and use Solr on Windows-based HDInsight clusters</span></span>

<span data-ttu-id="84cc1-104">Saiba como personalizar o cluster HDInsight baseado em Windows com Solr usando a Ação de Script, e como usar o Solr para pesquisar dados.</span><span class="sxs-lookup"><span data-stu-id="84cc1-104">Learn how to customize Windows-based HDInsight cluster with Solr using Script Action, and how to use Solr to search data.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="84cc1-105">As etapas neste documento só funcionam com clusters HDInsight baseados no Windows.</span><span class="sxs-lookup"><span data-stu-id="84cc1-105">The steps in this document only work with Windows-based HDInsight clusters.</span></span> <span data-ttu-id="84cc1-106">O HDInsight está disponível somente no Windows para versões inferiores ao HDInsight 3.4.</span><span class="sxs-lookup"><span data-stu-id="84cc1-106">HDInsight is only available on Windows for versions lower than HDInsight 3.4.</span></span> <span data-ttu-id="84cc1-107">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="84cc1-107">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="84cc1-108">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="84cc1-108">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span> <span data-ttu-id="84cc1-109">Para obter informações sobre como usar o Solr com um cluster baseado no Linux, consulte [Instalar e usar o Solr em clusters Hadoop do HDinsight (Linux)](hdinsight-hadoop-solr-install-linux.md).</span><span class="sxs-lookup"><span data-stu-id="84cc1-109">For information on using Solr with a Linux-based cluster, see [Install and use Solr on HDinsight Hadoop clusters (Linux)](hdinsight-hadoop-solr-install-linux.md).</span></span>


<span data-ttu-id="84cc1-110">Você pode instalar o Solr em qualquer tipo de cluster (Hadoop, Storm, HBase, Spark) no Azure HDInsight usando a *Ação de Script*.</span><span class="sxs-lookup"><span data-stu-id="84cc1-110">You can install Solr on any type of cluster (Hadoop, Storm, HBase, Spark) on Azure HDInsight by using *Script Action*.</span></span> <span data-ttu-id="84cc1-111">Um exemplo de script para instalar o R em um cluster HDInsight está disponível em um blob de armazenamento do Azure somente leitura em [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="84cc1-111">A sample script to install Solr on an HDInsight cluster is available from a read-only Azure storage blob at [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

<span data-ttu-id="84cc1-112">O script de exemplo funciona apenas com o cluster HDInsight versão 3.1.</span><span class="sxs-lookup"><span data-stu-id="84cc1-112">The sample script works only with HDInsight cluster version 3.1.</span></span> <span data-ttu-id="84cc1-113">Para obter mais informações sobre as versões do cluster HDInsight, consulte [Versões do cluster HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="84cc1-113">For more information on HDInsight cluster versions, see [HDInsight cluster versions](hdinsight-component-versioning.md).</span></span>

<span data-ttu-id="84cc1-114">O script de exemplo usado neste tópico cria um cluster do Solr baseado no Windows com uma configuração específica.</span><span class="sxs-lookup"><span data-stu-id="84cc1-114">The sample script used in this topic creates a Windows-based Solr cluster with a specific configuration.</span></span> <span data-ttu-id="84cc1-115">Se você quiser configurar o cluster Solr com diferentes coleções, fragmentos, esquemas, réplicas, etc., você deve modificar o script e os binários do Solr adequadamente.</span><span class="sxs-lookup"><span data-stu-id="84cc1-115">If you want to configure the Solr cluster with different collections, shards, schemas, replicas, etc., you must modify the script and Solr binaries accordingly.</span></span>

<span data-ttu-id="84cc1-116">**Artigos relacionados**</span><span class="sxs-lookup"><span data-stu-id="84cc1-116">**Related articles**</span></span>

* [<span data-ttu-id="84cc1-117">Instalar e usar o Solr em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="84cc1-117">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="84cc1-118">[Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="84cc1-118">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="84cc1-119">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="84cc1-119">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="84cc1-120">[Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="84cc1-120">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>

## <a name="what-is-solr"></a><span data-ttu-id="84cc1-121">O que é Solr?</span><span class="sxs-lookup"><span data-stu-id="84cc1-121">What is Solr?</span></span>
<span data-ttu-id="84cc1-122">O <a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> é uma plataforma de pesquisa empresarial que habilita operações poderosas de pesquisa de texto completo nos dados.</span><span class="sxs-lookup"><span data-stu-id="84cc1-122"><a href="http://lucene.apache.org/solr/features.html" target="_blank">Apache Solr</a> is an enterprise search platform that enables powerful full-text search on data.</span></span> <span data-ttu-id="84cc1-123">Enquanto o Hadoop permite armazenar e gerenciar grandes quantidades de dados, o Apache Solr oferece os recursos de pesquisa para recuperar rapidamente os dados.</span><span class="sxs-lookup"><span data-stu-id="84cc1-123">While Hadoop enables storing and managing vast amounts of data, Apache Solr provides the search capabilities to quickly retrieve the data.</span></span>

## <a name="install-solr-using-portal"></a><span data-ttu-id="84cc1-124">Instalar o Solr usando o Portal</span><span class="sxs-lookup"><span data-stu-id="84cc1-124">Install Solr using portal</span></span>
1. <span data-ttu-id="84cc1-125">Comece a criar um cluster usando a opção **CUSTOM CREATE**, como descrito em [Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="84cc1-125">Start creating a cluster by using the **CUSTOM CREATE** option, as described at [Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md).</span></span>
2. <span data-ttu-id="84cc1-126">Na página **Ações de Script** do assistente, clique em **adicionar ação de script** para fornecer detalhes sobre a ação de script, como mostrado abaixo:</span><span class="sxs-lookup"><span data-stu-id="84cc1-126">On the **Script Actions** page of the wizard, click **add script action** to provide details about the script action, as shown below:</span></span>

    <span data-ttu-id="84cc1-127">![Usar Ação de Script para personalizar um cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Usar Ação de Script para personalizar um cluster")</span><span class="sxs-lookup"><span data-stu-id="84cc1-127">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-script-action-solr.png "Use Script Action to customize a cluster")</span></span>

    <table border='1'>
        <tr><th><span data-ttu-id="84cc1-128">Propriedade</span><span class="sxs-lookup"><span data-stu-id="84cc1-128">Property</span></span></th><th><span data-ttu-id="84cc1-129">Valor</span><span class="sxs-lookup"><span data-stu-id="84cc1-129">Value</span></span></th></tr>
        <tr><td><span data-ttu-id="84cc1-130">Nome</span><span class="sxs-lookup"><span data-stu-id="84cc1-130">Name</span></span></td>
            <td><span data-ttu-id="84cc1-131">Especifique um nome para a ação de script.</span><span class="sxs-lookup"><span data-stu-id="84cc1-131">Specify a name for the script action.</span></span> <span data-ttu-id="84cc1-132">Por exemplo, <b>Instalar o Solr</b>.</span><span class="sxs-lookup"><span data-stu-id="84cc1-132">For example, <b>Install Solr</b>.</span></span></td></tr>
        <tr><td><span data-ttu-id="84cc1-133">URI do script</span><span class="sxs-lookup"><span data-stu-id="84cc1-133">Script URI</span></span></td>
            <td><span data-ttu-id="84cc1-134">Especifique o URI (Uniform Resource Identifier) do script invocado para personalizar o cluster.</span><span class="sxs-lookup"><span data-stu-id="84cc1-134">Specify the Uniform Resource Identifier (URI) to the script that is invoked to customize the cluster.</span></span> <span data-ttu-id="84cc1-135">Por exemplo, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span><span class="sxs-lookup"><span data-stu-id="84cc1-135">For example, <i>https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1</i></span></span></td></tr>
        <tr><td><span data-ttu-id="84cc1-136">Tipo de nó</span><span class="sxs-lookup"><span data-stu-id="84cc1-136">Node Type</span></span></td>
            <td><span data-ttu-id="84cc1-137">Especifique os nós em que o script de personalização deve ser executado.</span><span class="sxs-lookup"><span data-stu-id="84cc1-137">Specify the nodes on which the customization script is run.</span></span> <span data-ttu-id="84cc1-138">Você pode escolher <b>Todos os nós</b>, <b>Somente nós do cabeçalho</b> ou <b>Somente nós de trabalho</b>.</span><span class="sxs-lookup"><span data-stu-id="84cc1-138">You can choose <b>All nodes</b>, <b>Head nodes only</b>, or <b>Worker nodes only</b>.</span></span>
        <tr><td><span data-ttu-id="84cc1-139">parâmetros</span><span class="sxs-lookup"><span data-stu-id="84cc1-139">Parameters</span></span></td>
            <td><span data-ttu-id="84cc1-140">Especifique os parâmetros, se exigido pelo script.</span><span class="sxs-lookup"><span data-stu-id="84cc1-140">Specify the parameters, if required by the script.</span></span> <span data-ttu-id="84cc1-141">O script para instalar o Solr não requer nenhum parâmetro, portanto você pode deixá-los em branco.</span><span class="sxs-lookup"><span data-stu-id="84cc1-141">The script to install Solr does not require any parameters, so you can leave this blank.</span></span></td></tr>
    </table>

    <span data-ttu-id="84cc1-142">Você pode adicionar mais de uma ação de script para instalar vários componentes no cluster.</span><span class="sxs-lookup"><span data-stu-id="84cc1-142">You can add more than one script action to install multiple components on the cluster.</span></span> <span data-ttu-id="84cc1-143">Depois de adicionar os scripts, clique na marca de seleção para começar a criar o cluster.</span><span class="sxs-lookup"><span data-stu-id="84cc1-143">After you have added the scripts, click the checkmark to start creating the cluster.</span></span>

## <a name="use-solr"></a><span data-ttu-id="84cc1-144">Usar o Solr</span><span class="sxs-lookup"><span data-stu-id="84cc1-144">Use Solr</span></span>
<span data-ttu-id="84cc1-145">Você deve começar com indexação Solr, com alguns arquivos de dados.</span><span class="sxs-lookup"><span data-stu-id="84cc1-145">You must start with indexing Solr with some data files.</span></span> <span data-ttu-id="84cc1-146">Em seguida, você pode usar o Solr para executar consultas de pesquisa em dados indexados.</span><span class="sxs-lookup"><span data-stu-id="84cc1-146">You can then use Solr to run search queries on the indexed data.</span></span> <span data-ttu-id="84cc1-147">Execute as seguintes etapas para usar o Solr em um cluster HDInsight:</span><span class="sxs-lookup"><span data-stu-id="84cc1-147">Perform the following steps to use Solr in an HDInsight cluster:</span></span>

1. <span data-ttu-id="84cc1-148">**Usar protocolo RDP (desktop remoto) para remoto para o cluster HDInsight com o Solr instalado**.</span><span class="sxs-lookup"><span data-stu-id="84cc1-148">**Use Remote Desktop Protocol (RDP) to remote into the HDInsight cluster with Solr installed**.</span></span> <span data-ttu-id="84cc1-149">No Portal do Azure, habilite a Área de Trabalho Remota para o cluster criado com Solr instalado e, em seguida, acesse remotamente o cluster.</span><span class="sxs-lookup"><span data-stu-id="84cc1-149">From the Azure portal, enable Remote Desktop for the cluster you created with Solr installed, and then remote into the cluster.</span></span> <span data-ttu-id="84cc1-150">Para instruções, consulte [Conectar-se a clusters HDInsight usando RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span><span class="sxs-lookup"><span data-stu-id="84cc1-150">For instructions, see [Connect to HDInsight clusters using RDP](hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp).</span></span>
2. <span data-ttu-id="84cc1-151">**Indexar o Solr carregando arquivos de dados**.</span><span class="sxs-lookup"><span data-stu-id="84cc1-151">**Index Solr by uploading data files**.</span></span> <span data-ttu-id="84cc1-152">Quando você indexa o Solr, coloque os documentos que você pode precisar pesquisar.</span><span class="sxs-lookup"><span data-stu-id="84cc1-152">When you index Solr, you put documents in it that you may need to search on.</span></span> <span data-ttu-id="84cc1-153">Para indexar o Solr, acesso o cluster remotamente via RDP, navegue até a área de trabalho, abra a linha de comando do Hadoop e navegue até **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span><span class="sxs-lookup"><span data-stu-id="84cc1-153">To index Solr, use RDP to remote into the cluster, navigate to the desktop, open the Hadoop command line, and navigate to **C:\apps\dist\solr-4.7.2\example\exampledocs**.</span></span> <span data-ttu-id="84cc1-154">Execute o comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="84cc1-154">Run the following command:</span></span>

        java -jar post.jar solr.xml monitor.xml

    <span data-ttu-id="84cc1-155">Você verá a saída a seguir no console:</span><span class="sxs-lookup"><span data-stu-id="84cc1-155">You'll see the following output on the console:</span></span>

        POSTing file solr.xml
        POSTing file monitor.xml
        2 files indexed.
        COMMITting Solr index changes to http://localhost:8983/solr/update..
        Time spent: 0:00:01.624

    <span data-ttu-id="84cc1-156">O utilitário post.jar indexa o Solr com dois documentos de amostra, **solr.xml** e **monitor.xml**.</span><span class="sxs-lookup"><span data-stu-id="84cc1-156">The post.jar utility indexes Solr with two sample documents, **solr.xml** and **monitor.xml**.</span></span> <span data-ttu-id="84cc1-157">O utilitário post.jar e os documentos de exemplo estão disponíveis com a instalação do Solr.</span><span class="sxs-lookup"><span data-stu-id="84cc1-157">The post.jar utility and the sample documents are available with Solr installation.</span></span>
3. <span data-ttu-id="84cc1-158">**Use o painel do Solr para pesquisar nos documentos indexados**.</span><span class="sxs-lookup"><span data-stu-id="84cc1-158">**Use the Solr dashboard to search within the indexed documents**.</span></span> <span data-ttu-id="84cc1-159">Na sessão de acesso por RDP ao cluster HDInsight, abra o Internet Explorer e inicie o painel do Solr em **http://headnodehost:8983/solr/#/**.</span><span class="sxs-lookup"><span data-stu-id="84cc1-159">In the RDP session to the HDInsight cluster, open Internet Explorer, and launch the Solr dashboard at **http://headnodehost:8983/solr/#/**.</span></span> <span data-ttu-id="84cc1-160">No painel esquerdo, na lista suspensa **Seletor de Núcleo**, selecione **collection1** e, dentro dessa opção, clique em **Consulta**.</span><span class="sxs-lookup"><span data-stu-id="84cc1-160">From the left pane, from the **Core Selector** drop-down, select **collection1**, and within that, click **Query**.</span></span> <span data-ttu-id="84cc1-161">Por exemplo, para selecionar e retornar todos os documentos em Solr, forneça os seguintes valores:</span><span class="sxs-lookup"><span data-stu-id="84cc1-161">As an example, to select and return all the docs in Solr, provide the following values:</span></span>

   * <span data-ttu-id="84cc1-162">Na caixa de texto **q**, digite **\*:**\*.</span><span class="sxs-lookup"><span data-stu-id="84cc1-162">In the **q** text box, enter **\*:**\*.</span></span> <span data-ttu-id="84cc1-163">Isso retornará como resultado todos os documentos que são indexados em Solr.</span><span class="sxs-lookup"><span data-stu-id="84cc1-163">This will return all the documents that are indexed in Solr.</span></span> <span data-ttu-id="84cc1-164">Se você quiser procurar uma cadeia de caracteres específica dentro dos documentos, você pode inserir essa cadeia de caracteres aqui.</span><span class="sxs-lookup"><span data-stu-id="84cc1-164">If you want to search for a specific string within the documents, you can enter that string here.</span></span>
   * <span data-ttu-id="84cc1-165">Na caixa de texto **wt** , selecione o formato de saída.</span><span class="sxs-lookup"><span data-stu-id="84cc1-165">In the **wt** text box, select the output format.</span></span> <span data-ttu-id="84cc1-166">O padrão é **json**.</span><span class="sxs-lookup"><span data-stu-id="84cc1-166">Default is **json**.</span></span> <span data-ttu-id="84cc1-167">Clique em **Executar consulta**.</span><span class="sxs-lookup"><span data-stu-id="84cc1-167">Click **Execute Query**.</span></span>

     <span data-ttu-id="84cc1-168">![Usar Ação de Script para personalizar um cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Executar uma consulta no painel do Solr")</span><span class="sxs-lookup"><span data-stu-id="84cc1-168">![Use Script Action to customize a cluster](./media/hdinsight-hadoop-solr-install/hdi-solr-dashboard-query.png "Run a query on Solr dashboard")</span></span>

     <span data-ttu-id="84cc1-169">A saída retorna os dois documentos que foram usados para indexação do Solr.</span><span class="sxs-lookup"><span data-stu-id="84cc1-169">The output returns the two docs that we used for indexing Solr.</span></span> <span data-ttu-id="84cc1-170">A saída é semelhante ao seguinte:</span><span class="sxs-lookup"><span data-stu-id="84cc1-170">The output resembles the following:</span></span>

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
4. <span data-ttu-id="84cc1-171">**Recomendado: fazer backup dos dados indexados do Solr para o Blob de Armazenamento do Azure (WASB) associado ao cluster HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="84cc1-171">**Recommended: Back up the indexed data from Solr to Azure Blob storage associated with the HDInsight cluster**.</span></span> <span data-ttu-id="84cc1-172">Como uma prática recomendada, você deve fazer backup dos dados indexados de nós do cluster Solr no armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="84cc1-172">As a good practice, you should back up the indexed data from the Solr cluster nodes onto Azure Blob storage.</span></span> <span data-ttu-id="84cc1-173">Execute as seguintes etapas para fazê-lo:</span><span class="sxs-lookup"><span data-stu-id="84cc1-173">Perform the following steps to do so:</span></span>

   1. <span data-ttu-id="84cc1-174">Na sessão RDP, abra o Internet Explorer e insira a seguinte URL:</span><span class="sxs-lookup"><span data-stu-id="84cc1-174">From the RDP session, open Internet Explorer, and point to the following URL:</span></span>

           http://localhost:8983/solr/replication?command=backup

       <span data-ttu-id="84cc1-175">Você verá uma resposta semelhante a essa:</span><span class="sxs-lookup"><span data-stu-id="84cc1-175">You should see a response like this:</span></span>

           <?xml version="1.0" encoding="UTF-8"?>
           <response>
             <lst name="responseHeader">
               <int name="status">0</int>
               <int name="QTime">9</int>
             </lst>
             <str name="status">OK</str>
           </response>
   2. <span data-ttu-id="84cc1-176">Na sessão remota, navegue até {HOME_DO_SOLR}\{\{Coleção}\data.</span><span class="sxs-lookup"><span data-stu-id="84cc1-176">In the remote session, navigate to {SOLR_HOME}\{Collection}\data.</span></span> <span data-ttu-id="84cc1-177">Para o cluster criado usando o script de exemplo, esse caminho deve ser **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span><span class="sxs-lookup"><span data-stu-id="84cc1-177">For the cluster created via the sample script, this should be **C:\apps\dist\solr-4.7.2\example\solr\collection1\data**.</span></span> <span data-ttu-id="84cc1-178">Nesse local, você deve ver uma pasta de capturas de tela criada com um nome semelhante a **snapshot.*timestamp***.</span><span class="sxs-lookup"><span data-stu-id="84cc1-178">At this location, you should see a snapshot folder created with a name similar to **snapshot.*timestamp***.</span></span>
   3. <span data-ttu-id="84cc1-179">Compacte a pasta de capturas de tela e carregue-la no armazenamento de Blob do Azure.</span><span class="sxs-lookup"><span data-stu-id="84cc1-179">Zip the snapshot folder and upload it to Azure Blob storage.</span></span> <span data-ttu-id="84cc1-180">Na linha de comando do Hadoop, navegue até o local da pasta de capturas de tela usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="84cc1-180">From the Hadoop command line, navigate to the location of the snapshot folder by using the following command:</span></span>

             hadoop fs -CopyFromLocal snapshot._timestamp_.zip /example/data

       <span data-ttu-id="84cc1-181">Este comando copia a capturas de tela para /example/data/ sob o contêiner na conta de armazenamento padrão associada ao cluster.</span><span class="sxs-lookup"><span data-stu-id="84cc1-181">This command copies the snapshot to /example/data/ under the container within the default Storage account associated with the cluster.</span></span>

## <a name="install-solr-using-aure-powershell"></a><span data-ttu-id="84cc1-182">Instalar o Solr usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="84cc1-182">Install Solr using Aure PowerShell</span></span>
<span data-ttu-id="84cc1-183">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="84cc1-183">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span>  <span data-ttu-id="84cc1-184">O exemplo demonstra como instalar o Spark usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="84cc1-184">The sample demonstrates how to install Spark using Azure PowerShell.</span></span> <span data-ttu-id="84cc1-185">Você precisa personalizar o script para usar [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="84cc1-185">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="install-solr-using-net-sdk"></a><span data-ttu-id="84cc1-186">Instalar o Solr usando o SDK do .NET</span><span class="sxs-lookup"><span data-stu-id="84cc1-186">Install Solr using .NET SDK</span></span>
<span data-ttu-id="84cc1-187">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="84cc1-187">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster.md#call-scripts-using-azure-powershell).</span></span> <span data-ttu-id="84cc1-188">O exemplo demonstra como instalar o Spark usando o SDK do .NET.</span><span class="sxs-lookup"><span data-stu-id="84cc1-188">The sample demonstrates how to install Spark using the .NET SDK.</span></span> <span data-ttu-id="84cc1-189">Você precisa personalizar o script para usar [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span><span class="sxs-lookup"><span data-stu-id="84cc1-189">You need to customize the script to use [https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1](https://hdiconfigactions.blob.core.windows.net/solrconfigactionv01/solr-installer-v01.ps1).</span></span>

## <a name="see-also"></a><span data-ttu-id="84cc1-190">Confira também</span><span class="sxs-lookup"><span data-stu-id="84cc1-190">See also</span></span>
* [<span data-ttu-id="84cc1-191">Instalar e usar o Solr em clusters Hadoop do HDInsight (Linux)</span><span class="sxs-lookup"><span data-stu-id="84cc1-191">Install and use Solr on HDinsight Hadoop clusters (Linux)</span></span>](hdinsight-hadoop-solr-install-linux.md)
* <span data-ttu-id="84cc1-192">[Criar clusters Hadoop no HDInsight](hdinsight-provision-clusters.md): informações gerais sobre como criar clusters HDInsight</span><span class="sxs-lookup"><span data-stu-id="84cc1-192">[Create Hadoop clusters in HDInsight](hdinsight-provision-clusters.md): general information on creating HDInsight clusters.</span></span>
* <span data-ttu-id="84cc1-193">[Personalizar clusters HDInsight usando a Ação de Script][hdinsight-cluster-customize]: informações gerais sobre como personalizar os clusters HDInsight usando a Ação de Script.</span><span class="sxs-lookup"><span data-stu-id="84cc1-193">[Customize HDInsight cluster using Script Action][hdinsight-cluster-customize]: general information on customizing HDInsight clusters using Script Action.</span></span>
* <span data-ttu-id="84cc1-194">[Desenvolver scripts de Ação de Script para o HDInsight](hdinsight-hadoop-script-actions.md)</span><span class="sxs-lookup"><span data-stu-id="84cc1-194">[Develop Script Action scripts for HDInsight](hdinsight-hadoop-script-actions.md).</span></span>
* <span data-ttu-id="84cc1-195">[Instalar e usar o Spark em clusters HDInsight][hdinsight-install-spark]: exemplo de Ação de Script sobre a instalação do Spark.</span><span class="sxs-lookup"><span data-stu-id="84cc1-195">[Install and use Spark on HDInsight clusters][hdinsight-install-spark]: Script Action sample about installing Spark.</span></span>
* <span data-ttu-id="84cc1-196">[Instalar R em clusters HDInsight][hdinsight-install-r]: exemplo de Ação de Script sobre a instalação do R.</span><span class="sxs-lookup"><span data-stu-id="84cc1-196">[Install R on HDInsight clusters][hdinsight-install-r]: Script Action sample about installing R.</span></span>
* <span data-ttu-id="84cc1-197">[Instalar Giraph em clusters HDInsight](hdinsight-hadoop-giraph-install.md): exemplo de Ação de Script sobre a instalação do Giraph.</span><span class="sxs-lookup"><span data-stu-id="84cc1-197">[Install Giraph on HDInsight clusters](hdinsight-hadoop-giraph-install.md): Script Action sample about installing Giraph.</span></span>

[powershell-install-configure]: /powershell/azureps-cmdlets-docs
[hdinsight-provision]: hdinsight-provision-clusters.md
[hdinsight-install-r]: hdinsight-hadoop-r-scripts.md
[hdinsight-install-spark]: hdinsight-hadoop-spark-install.md
[hdinsight-cluster-customize]: hdinsight-hadoop-customize-cluster.md
