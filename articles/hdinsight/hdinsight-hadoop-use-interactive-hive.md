---
title: aaaUse interativo Hive no HDInsight - Azure | Microsoft Docs
description: Saiba como toouse interativo (Hive no LLAP) de Hive no HDInsight.
keywords: 
services: hdinsight
documentationcenter: 
tags: azure-portal
author: mumian
manager: jhubbard
editor: cgronlun
ms.assetid: 0957643c-4936-48a3-84a3-5dc83db4ab1a
ms.service: hdinsight
ms.custom: hdinsightactive
ms.workload: big-data
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/25/2017
ms.author: jgao
ms.openlocfilehash: 9e751a08091d18bc1b3d070468feef87f6828c61
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="11004-103">Usar o Hive Interativo no HDInsight (Visualização)</span><span class="sxs-lookup"><span data-stu-id="11004-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="11004-104">O Hive Interativo (também conhecido como</span><span class="sxs-lookup"><span data-stu-id="11004-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="11004-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) é um novo [tipo de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11004-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="11004-106">O Hive Interativo permite o armazenamento em cache na memória, o que torna as consultas do Hive muito mais interativas e rápidas.</span><span class="sxs-lookup"><span data-stu-id="11004-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="11004-107">Este novo recurso torna HDInsight uma saudação mais funcionais, flexíveis e abrir soluções de Big Data do mundo na nuvem Olá com caches de memória (usando Hive e Spark) e advanced analytics por meio da profunda integração com serviços de R.</span><span class="sxs-lookup"><span data-stu-id="11004-107">This new feature makes HDInsight one of hello world’s most performant, flexible, and open Big Data solutions on hello cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="11004-108">cluster de Hive interativo Olá é diferente do cluster de Hadoop hello.</span><span class="sxs-lookup"><span data-stu-id="11004-108">hello Interactive Hive cluster is different from hello Hadoop cluster.</span></span> <span data-ttu-id="11004-109">Ele contém apenas serviço de Hive hello.</span><span class="sxs-lookup"><span data-stu-id="11004-109">It only contains hello Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="11004-110">MapReduce, Pig, Sqoop, Oozie e outros serviços, em breve, serão removidos desse tipo de cluster.</span><span class="sxs-lookup"><span data-stu-id="11004-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="11004-111">Olá serviço Hive no cluster de Hive interativo Olá só está acessível por meio de Olá exibição Ambari Hive, Beeline e Hive ODBC.</span><span class="sxs-lookup"><span data-stu-id="11004-111">hello Hive service in hello Interactive Hive cluster is only accessible via hello Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="11004-112">Ele não pode ser acessado por meio do console do Hive, do Templeton, da CLI do Azure e do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="11004-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="11004-113">Criar um cluster do Hive Interativo</span><span class="sxs-lookup"><span data-stu-id="11004-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="11004-114">O cluster do Hive Interativo é compatível apenas com clusters baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="11004-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="11004-115">Para obter informações sobre a criação de clusters HDInsight, confira [Criar clusters Hadoop baseados em Linux em HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="11004-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="11004-116">Executar o Hive do Hive Interativo</span><span class="sxs-lookup"><span data-stu-id="11004-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="11004-117">Há diferentes opções para executar consultas do Hive:</span><span class="sxs-lookup"><span data-stu-id="11004-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="11004-118">Execute o Hive usando Olá Ambari Hive exibição</span><span class="sxs-lookup"><span data-stu-id="11004-118">Run Hive using hello Ambari Hive view</span></span>
  
    <span data-ttu-id="11004-119">Para obter informações de Olá sobre como usar o hello exibição Hive, consulte [Olá Use exibição de Hive com Hadoop no HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span><span class="sxs-lookup"><span data-stu-id="11004-119">For hello information about using hello Hive View, see [Use hello Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="11004-120">Executar o Hive usando o Beeline</span><span class="sxs-lookup"><span data-stu-id="11004-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="11004-121">Para obter informações de saudação usando Beeline no HDInsight, consulte [uso de Hive do Hadoop no HDInsight com Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="11004-121">For hello information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="11004-122">Você pode usar Beeline de saudação um nó principal ou um nó de borda vazia.</span><span class="sxs-lookup"><span data-stu-id="11004-122">You use Beeline from either hello headnode or an empty edge node.</span></span>  <span data-ttu-id="11004-123">É recomendável usar o Beeline em um nó de borda vazio.</span><span class="sxs-lookup"><span data-stu-id="11004-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="11004-124">Para saber mais sobre como criar um cluster HDInsight com um nó de borda vazio, confira [Usar nós de borda vazios no HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="11004-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="11004-125">Executar o Hive usando o ODBC do Hive</span><span class="sxs-lookup"><span data-stu-id="11004-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="11004-126">Para obter informações de hello usando ODBC Hive, consulte [tooHadoop Excel conectar-se com hello Hive do Microsoft ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="11004-126">For hello information on using Hive ODBC, see [Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="11004-127">**Olá toofind cadeia de caracteres de conexão JDBC:**</span><span class="sxs-lookup"><span data-stu-id="11004-127">**toofind hello JDBC connection string:**</span></span>

1. <span data-ttu-id="11004-128">Logon tooAmbari usando Olá URL a seguir: https://<ClusterName>. N e t.</span><span class="sxs-lookup"><span data-stu-id="11004-128">Sign on tooAmbari using hello following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="11004-129">Clique em **Hive** no menu esquerdo hello.</span><span class="sxs-lookup"><span data-stu-id="11004-129">Click **Hive** from hello left menu.</span></span>
3. <span data-ttu-id="11004-130">Clique em Olá realçado ícone toocopy Olá URL:</span><span class="sxs-lookup"><span data-stu-id="11004-130">Click hello highlighted icon toocopy hello URL:</span></span>
   
   ![JDBC LLAP do Hive Interativo no Hadoop HDInsight](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="11004-132">Consulte também</span><span class="sxs-lookup"><span data-stu-id="11004-132">See also</span></span>
* <span data-ttu-id="11004-133">[Criar clusters baseados em Linux Hadoop no HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Saiba como clusters de toocreate interativo Hive no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="11004-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how toocreate Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="11004-134">[Use o Hive com Hadoop no HDInsight com Beeline](hdinsight-hadoop-use-hive-beeline.md): Saiba como consultas de Hive toouse Beeline toosubmit.</span><span class="sxs-lookup"><span data-stu-id="11004-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how toouse Beeline toosubmit Hive queries.</span></span>
* <span data-ttu-id="11004-135">[Conectar Excel tooHadoop com hello Hive do Microsoft ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): Saiba como tooconnect Excel tooHive.</span><span class="sxs-lookup"><span data-stu-id="11004-135">[Connect Excel tooHadoop with hello Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how tooconnect Excel tooHive.</span></span>

