---
title: "Use o Apache Phoenix e o SQuirreL com o HBase – Azure HDInsight | Microsoft Docs"
description: "Saiba como usar o Apache Phoenix no HDInsight e como instalar e configurar o SQuirreL na sua estação de trabalho para se conectar a um cluster HBase no HDInsight."
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: cda0f33b-a2e8-494c-972f-ae0bb482b818
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/26/2017
ms.author: jgao
ms.openlocfilehash: 13d17083bbe26fa9745ce4c5fef9f56859243c2e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="41c61-103">Usar o Apache Phoenix com clusters do HBase baseados em Linux no HDInsight</span><span class="sxs-lookup"><span data-stu-id="41c61-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="41c61-104">Saiba como usar o [Apache Phoenix](http://phoenix.apache.org/) no HDInsight e como usar o SQLLine.</span><span class="sxs-lookup"><span data-stu-id="41c61-104">Learn how to use [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how to use SQLLine.</span></span> <span data-ttu-id="41c61-105">Para obter mais informações sobre o Phoenix, consulte [Phoenix em 15 minutos ou menos](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="41c61-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="41c61-106">Para conhecer a gramática de Phoenix, consulte [Gramática do Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="41c61-106">For the Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="41c61-107">Para obter as informações de versão do Phoenix no HDInsight, consulte [Novidades nas versões de cluster Hadoop fornecidas pelo HDInsight](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="41c61-107">For the Phoenix version information in HDInsight, see [What's new in the Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="41c61-108">Usar o SQLLine</span><span class="sxs-lookup"><span data-stu-id="41c61-108">Use SQLLine</span></span>
<span data-ttu-id="41c61-109">[SQLLine](http://sqlline.sourceforge.net/) é um utilitário de linha de comando para executar o SQL.</span><span class="sxs-lookup"><span data-stu-id="41c61-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility to execute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="41c61-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="41c61-110">Prerequisites</span></span>
<span data-ttu-id="41c61-111">Antes de poder usar o SQLLine, você deve ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="41c61-111">Before you can use SQLLine, you must have the following:</span></span>

* <span data-ttu-id="41c61-112">**Um cluster HBase no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="41c61-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="41c61-113">Para obter informações sobre como provisionar o cluster HBase, consulte [Introdução ao Apache HBase no HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="41c61-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="41c61-114">**Conectar-se ao cluster HBase por meio do protocolo de área de trabalho remoto**.</span><span class="sxs-lookup"><span data-stu-id="41c61-114">**Connect to the HBase cluster via the remote desktop protocol**.</span></span> <span data-ttu-id="41c61-115">Para obter instruções, veja [Gerenciar clusters Hadoop no HDInsight usando o Portal do Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="41c61-115">For instructions, see [Manage Hadoop clusters in HDInsight by using the Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="41c61-116">Ao se conectar a um cluster HBase, você precisa se conectar a um dos Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="41c61-116">When you connect to an HBase cluster, you need to connect to one of the Zookeepers.</span></span> <span data-ttu-id="41c61-117">Cada cluster HDInsight tem três Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="41c61-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="41c61-118">**Para descobrir o nome de host do Zookeeper**</span><span class="sxs-lookup"><span data-stu-id="41c61-118">**To find out the Zookeeper host name**</span></span>

1. <span data-ttu-id="41c61-119">Abra o Ambari navegando até **https://<ClusterName>.azurehdinsight.net**.</span><span class="sxs-lookup"><span data-stu-id="41c61-119">Open Ambari by browsing to **https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="41c61-120">Insira o nome de usuário HTTP (cluster) e a senha para fazer logon.</span><span class="sxs-lookup"><span data-stu-id="41c61-120">Enter the HTTP (cluster) username and password to login.</span></span>
3. <span data-ttu-id="41c61-121">Clique em **ZooKeeper** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="41c61-121">Click **ZooKeeper** from the left menu.</span></span> <span data-ttu-id="41c61-122">Você vê três **Servidores do ZooKeeper** listados.</span><span class="sxs-lookup"><span data-stu-id="41c61-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="41c61-123">Clique em um dos **Servidores do ZooKeeper** listados.</span><span class="sxs-lookup"><span data-stu-id="41c61-123">Click one of the **ZooKeeper Server** listed.</span></span> <span data-ttu-id="41c61-124">No painel Resumo, encontre o **Nome do host**.</span><span class="sxs-lookup"><span data-stu-id="41c61-124">On the Summary pane, find the **Hostname**.</span></span> <span data-ttu-id="41c61-125">Ele é semelhante a *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="41c61-125">It is similar to *zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="41c61-126">**Usar SQLLine**</span><span class="sxs-lookup"><span data-stu-id="41c61-126">**To use SQLLine**</span></span>

1. <span data-ttu-id="41c61-127">Conecte-se ao cluster usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="41c61-127">Connect to the cluster using SSH.</span></span> <span data-ttu-id="41c61-128">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="41c61-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="41c61-129">No SSH, execute os seguintes comandos para executar o SQLLine:</span><span class="sxs-lookup"><span data-stu-id="41c61-129">From SSH, run the following commands to run SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="41c61-130">Execute os seguintes comandos para criar uma tabela do HBase e insira alguns dados:</span><span class="sxs-lookup"><span data-stu-id="41c61-130">Run the following commands to create a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="41c61-131">Para obter mais informações, consulte o [Manual SQLLine](http://sqlline.sourceforge.net/#manual) e [Gramática do Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="41c61-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="41c61-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="41c61-132">Next steps</span></span>
<span data-ttu-id="41c61-133">Neste artigo, você aprendeu a usar o Apache Phoenix no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41c61-133">In this article, you have learned how to use Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="41c61-134">Para obter mais informações, consulte:</span><span class="sxs-lookup"><span data-stu-id="41c61-134">To learn more, see:</span></span>

* <span data-ttu-id="41c61-135">[Visão geral do HBase do HDInsight][hdinsight-hbase-overview]: o HBase é um banco de dados NoSQL de software livre Apache baseado no Hadoop que fornece acesso aleatório e uma sólida consistência para grandes quantidades de dados não estruturados e semiestruturados.</span><span class="sxs-lookup"><span data-stu-id="41c61-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="41c61-136">[Provisionar clusters do HBase na Rede Virtual do Azure][hdinsight-hbase-provision-vnet]: com a integração da rede virtual, os clusters do HBase podem ser implantados na mesma rede virtual que seus aplicativos, de modo que os aplicativos possam se comunicar diretamente com o HBase.</span><span class="sxs-lookup"><span data-stu-id="41c61-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed to the same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="41c61-137">[Configurar replicação HBase no HDInsight](hdinsight-hbase-replication.md): saiba como configurar a replicação do HBase entre dois datacenters do Azure.</span><span class="sxs-lookup"><span data-stu-id="41c61-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how to configure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="41c61-138">[Analisar sentimentos do Twitter com o HBase no HDInsight][hbase-twitter-sentiment]: saiba como fazer a [análise de sentimento](http://en.wikipedia.org/wiki/Sentiment_analysis) em tempo real de Big Data usando o HBase em um cluster do Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="41c61-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how to do real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

[azure-portal]: https://portal.azure.com
[vnet-point-to-site-connectivity]: https://msdn.microsoft.com/library/azure/09926218-92ab-4f43-aa99-83ab4d355555#BKMK_VNETPT

[hdinsight-hbase-get-started]: hdinsight-hbase-tutorial-get-started.md
[hdinsight-manage-portal]: hdinsight-administer-use-management-portal.md#connect-to-clusters-using-rdp
[hdinsight-hbase-provision-vnet]: hdinsight-hbase-provision-vnet.md
[hdinsight-hbase-overview]: hdinsight-hbase-overview.md
[hbase-twitter-sentiment]: hdinsight-hbase-analyze-twitter-sentiment.md

[hdinsight-hbase-phoenix-sqlline]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-phoenix-sqlline.png
[img-certificate]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vpn-certificate.png
[img-vnet-diagram]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-vnet-point-to-site.png
[img-squirrel-driver]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-driver.png
[img-squirrel-alias]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-alias.png
[img-squirrel]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel.png
[img-squirrel-sql]: ./media/hdinsight-hbase-phoenix-squirrel/hdinsight-hbase-squirrel-sql.png
