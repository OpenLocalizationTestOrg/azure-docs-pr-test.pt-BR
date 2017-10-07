---
title: aaaUse Apache Phoenix & esquilo com HBase - HDInsight do Azure | Microsoft Docs
description: "Saiba como toouse Phoenix Apache no HDInsight e como tooinstall e configurar esquilo no cluster de estação de trabalho tooconnect tooan HBase em HDInsight."
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
ms.openlocfilehash: a63e8c8212b7a992453ec94fa638ec3863a0ede3
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-apache-phoenix-with-linux-based-hbase-clusters-in-hdinsight"></a><span data-ttu-id="a1e58-103">Usar o Apache Phoenix com clusters do HBase baseados em Linux no HDInsight</span><span class="sxs-lookup"><span data-stu-id="a1e58-103">Use Apache Phoenix with Linux-based HBase clusters in HDInsight</span></span>
<span data-ttu-id="a1e58-104">Saiba como toouse [Apache Phoenix](http://phoenix.apache.org/) no HDInsight e como toouse SQLLine.</span><span class="sxs-lookup"><span data-stu-id="a1e58-104">Learn how toouse [Apache Phoenix](http://phoenix.apache.org/) in HDInsight, and how toouse SQLLine.</span></span> <span data-ttu-id="a1e58-105">Para obter mais informações sobre o Phoenix, consulte [Phoenix em 15 minutos ou menos](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span><span class="sxs-lookup"><span data-stu-id="a1e58-105">For more information about Phoenix, see [Phoenix in 15 minutes or less](http://phoenix.apache.org/Phoenix-in-15-minutes-or-less.html).</span></span> <span data-ttu-id="a1e58-106">Para Olá gramática Phoenix, consulte [Phoenix gramática](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="a1e58-106">For hello Phoenix grammar, see [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

> [!NOTE]
> <span data-ttu-id="a1e58-107">Para Olá informações de versão de Phoenix no HDInsight, consulte [Novidades nas versões de cluster de Hadoop Olá fornecidas pelo HDInsight?](hdinsight-component-versioning.md).</span><span class="sxs-lookup"><span data-stu-id="a1e58-107">For hello Phoenix version information in HDInsight, see [What's new in hello Hadoop cluster versions provided by HDInsight?](hdinsight-component-versioning.md).</span></span>
>
>

## <a name="use-sqlline"></a><span data-ttu-id="a1e58-108">Usar o SQLLine</span><span class="sxs-lookup"><span data-stu-id="a1e58-108">Use SQLLine</span></span>
<span data-ttu-id="a1e58-109">[SQLLine](http://sqlline.sourceforge.net/) é tooexecute um utilitário de linha de comando SQL.</span><span class="sxs-lookup"><span data-stu-id="a1e58-109">[SQLLine](http://sqlline.sourceforge.net/) is a command-line utility tooexecute SQL.</span></span>

### <a name="prerequisites"></a><span data-ttu-id="a1e58-110">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="a1e58-110">Prerequisites</span></span>
<span data-ttu-id="a1e58-111">Antes de usar SQLLine, você deve ter o seguinte hello:</span><span class="sxs-lookup"><span data-stu-id="a1e58-111">Before you can use SQLLine, you must have hello following:</span></span>

* <span data-ttu-id="a1e58-112">**Um cluster HBase no HDInsight**.</span><span class="sxs-lookup"><span data-stu-id="a1e58-112">**An HBase cluster in HDInsight**.</span></span> <span data-ttu-id="a1e58-113">Para obter informações sobre como provisionar o cluster HBase, consulte [Introdução ao Apache HBase no HDInsight][hdinsight-hbase-get-started].</span><span class="sxs-lookup"><span data-stu-id="a1e58-113">For information on provision HBase cluster, see [Get started with Apache HBase in HDInsight][hdinsight-hbase-get-started].</span></span>
* <span data-ttu-id="a1e58-114">**Conecte toohello HBase cluster por meio do protocolo de área de trabalho remota Olá**.</span><span class="sxs-lookup"><span data-stu-id="a1e58-114">**Connect toohello HBase cluster via hello remote desktop protocol**.</span></span> <span data-ttu-id="a1e58-115">Para obter instruções, consulte [clusters gerenciar Hadoop em HDInsight usando Olá portal do Azure][hdinsight-manage-portal].</span><span class="sxs-lookup"><span data-stu-id="a1e58-115">For instructions, see [Manage Hadoop clusters in HDInsight by using hello Azure portal][hdinsight-manage-portal].</span></span>

<span data-ttu-id="a1e58-116">Quando você conectar tooan HBase cluster, é necessário tooone tooconnect de saudação Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="a1e58-116">When you connect tooan HBase cluster, you need tooconnect tooone of hello Zookeepers.</span></span> <span data-ttu-id="a1e58-117">Cada cluster HDInsight tem três Zookeepers.</span><span class="sxs-lookup"><span data-stu-id="a1e58-117">Each HDInsight cluster has three Zookeepers.</span></span>

<span data-ttu-id="a1e58-118">**toofind nome de host Zookeeper Olá**</span><span class="sxs-lookup"><span data-stu-id="a1e58-118">**toofind out hello Zookeeper host name**</span></span>

1. <span data-ttu-id="a1e58-119">Abra o Ambari navegando muito**https://<ClusterName>. cluster>.azurehdinsight.NET**.</span><span class="sxs-lookup"><span data-stu-id="a1e58-119">Open Ambari by browsing too**https://<ClusterName>.azurehdinsight.net**.</span></span>
2. <span data-ttu-id="a1e58-120">Digite hello toologin de nome de usuário e senha do HTTP (cluster).</span><span class="sxs-lookup"><span data-stu-id="a1e58-120">Enter hello HTTP (cluster) username and password toologin.</span></span>
3. <span data-ttu-id="a1e58-121">Clique em **ZooKeeper** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="a1e58-121">Click **ZooKeeper** from hello left menu.</span></span> <span data-ttu-id="a1e58-122">Você vê três **Servidores do ZooKeeper** listados.</span><span class="sxs-lookup"><span data-stu-id="a1e58-122">You see three **ZooKeeper Server** listed.</span></span>
4. <span data-ttu-id="a1e58-123">Clique em uma saudação **ZooKeeper Server** listados.</span><span class="sxs-lookup"><span data-stu-id="a1e58-123">Click one of hello **ZooKeeper Server** listed.</span></span> <span data-ttu-id="a1e58-124">No painel de resumo hello, localize Olá **Hostname**.</span><span class="sxs-lookup"><span data-stu-id="a1e58-124">On hello Summary pane, find hello **Hostname**.</span></span> <span data-ttu-id="a1e58-125">Ele é muito semelhante*zk1 jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span><span class="sxs-lookup"><span data-stu-id="a1e58-125">It is similar too*zk1-jdolehb.3lnng4rcvp5uzokyktxs4a5dhd.bx.internal.cloudapp.net*.</span></span>

<span data-ttu-id="a1e58-126">**toouse SQLLine**</span><span class="sxs-lookup"><span data-stu-id="a1e58-126">**toouse SQLLine**</span></span>

1. <span data-ttu-id="a1e58-127">Conecte-se toohello cluster usando o SSH.</span><span class="sxs-lookup"><span data-stu-id="a1e58-127">Connect toohello cluster using SSH.</span></span> <span data-ttu-id="a1e58-128">Para obter mais informações, confira [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="a1e58-128">For more information, see [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span></span>

2. <span data-ttu-id="a1e58-129">SSH, execute Olá comandos toorun SQLLine a seguir:</span><span class="sxs-lookup"><span data-stu-id="a1e58-129">From SSH, run hello following commands toorun SQLLine:</span></span>

        cd /usr/hdp/2.2.9.1-7/phoenix/bin
        ./sqlline.py <ClusterName>:2181:/hbase-unsecure
3. <span data-ttu-id="a1e58-130">Execute Olá toocreate comandos a seguir uma tabela do HBase e insira alguns dados:</span><span class="sxs-lookup"><span data-stu-id="a1e58-130">Run hello following commands toocreate a HBase table, and insert some data:</span></span>

        CREATE TABLE Company (COMPANY_ID INTEGER PRIMARY KEY, NAME VARCHAR(225));

        !tables

        UPSERT INTO Company VALUES(1, 'Microsoft');

        SELECT * FROM Company;

        !quit

<span data-ttu-id="a1e58-131">Para obter mais informações, consulte o [Manual SQLLine](http://sqlline.sourceforge.net/#manual) e [Gramática do Phoenix](http://phoenix.apache.org/language/index.html).</span><span class="sxs-lookup"><span data-stu-id="a1e58-131">For more information, see [SQLLine manual](http://sqlline.sourceforge.net/#manual) and [Phoenix Grammar](http://phoenix.apache.org/language/index.html).</span></span>

## <a name="next-steps"></a><span data-ttu-id="a1e58-132">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="a1e58-132">Next steps</span></span>
<span data-ttu-id="a1e58-133">Neste artigo, você aprendeu como toouse Phoenix Apache no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a1e58-133">In this article, you have learned how toouse Apache Phoenix in HDInsight.</span></span>  <span data-ttu-id="a1e58-134">toolearn mais, consulte:</span><span class="sxs-lookup"><span data-stu-id="a1e58-134">toolearn more, see:</span></span>

* <span data-ttu-id="a1e58-135">[Visão geral do HBase do HDInsight][hdinsight-hbase-overview]: o HBase é um banco de dados NoSQL de software livre Apache baseado no Hadoop que fornece acesso aleatório e uma sólida consistência para grandes quantidades de dados não estruturados e semiestruturados.</span><span class="sxs-lookup"><span data-stu-id="a1e58-135">[HDInsight HBase overview][hdinsight-hbase-overview]: HBase is an Apache, open-source, NoSQL database built on Hadoop that provides random access and strong consistency for large amounts of unstructured and semistructured data.</span></span>
* <span data-ttu-id="a1e58-136">[Provisionar clusters HBase na rede Virtual do Azure][hdinsight-hbase-provision-vnet]: com a integração de rede virtual, clusters HBase podem ser implantado toohello mesmo virtual de rede como seus aplicativos para que os aplicativos podem se comunicar com o HBase diretamente.</span><span class="sxs-lookup"><span data-stu-id="a1e58-136">[Provision HBase clusters on Azure Virtual Network][hdinsight-hbase-provision-vnet]: With virtual network integration, HBase clusters can be deployed toohello same virtual network as your applications so that applications can communicate with HBase directly.</span></span>
* <span data-ttu-id="a1e58-137">[Configurar a replicação do HBase em HDInsight](hdinsight-hbase-replication.md): Saiba como tooconfigure HBase replicação entre dois datacenters do Azure.</span><span class="sxs-lookup"><span data-stu-id="a1e58-137">[Configure HBase replication in HDInsight](hdinsight-hbase-replication.md): Learn how tooconfigure HBase replication across two Azure datacenters.</span></span>
* <span data-ttu-id="a1e58-138">[Analisar o sentimento do Twitter com HBase em HDInsight][hbase-twitter-sentiment]: Saiba como toodo em tempo real [análise de sentimento](http://en.wikipedia.org/wiki/Sentiment_analysis) de big data usando HBase em um cluster Hadoop no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="a1e58-138">[Analyze Twitter sentiment with HBase in HDInsight][hbase-twitter-sentiment]: Learn how toodo real-time [sentiment analysis](http://en.wikipedia.org/wiki/Sentiment_analysis) of big data by using HBase in a Hadoop cluster in HDInsight.</span></span>

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
