---
title: "Usar o Hive Interativo no HDInsight – Azure | Microsoft Docs"
description: Saiba como usar o Hive Interativo (Hive no LLAP) no HDInsight.
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
ms.openlocfilehash: e7874b55fc72f14d8e2c801872359e823cb2ba34
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="use-interactive-hive-in-hdinsight-preview"></a><span data-ttu-id="86513-103">Usar o Hive Interativo no HDInsight (Visualização)</span><span class="sxs-lookup"><span data-stu-id="86513-103">Use Interactive Hive in HDInsight (Preview)</span></span>
<span data-ttu-id="86513-104">O Hive Interativo (também conhecido como</span><span class="sxs-lookup"><span data-stu-id="86513-104">Interactive Hive (A.K.A.</span></span> <span data-ttu-id="86513-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) é um novo [tipo de cluster](hdinsight-hadoop-provision-linux-clusters.md#cluster-types) do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86513-105">[Live Long and Process](https://cwiki.apache.org/confluence/display/Hive/LLAP)) is a new HDInsight [cluster type](hdinsight-hadoop-provision-linux-clusters.md#cluster-types).</span></span>  <span data-ttu-id="86513-106">O Hive Interativo permite o armazenamento em cache na memória, o que torna as consultas do Hive muito mais interativas e rápidas.</span><span class="sxs-lookup"><span data-stu-id="86513-106">Interactive Hive allows in memory caching that makes Hive queries much more interactive and faster.</span></span> <span data-ttu-id="86513-107">Esse novo recurso torna o HDInsight uma das soluções de Big Data de melhor desempenho, flexível e aberta na nuvem com caches na memória (usando Hive e Spark) e análise avançada por meio de integração profunda aos serviços de R.</span><span class="sxs-lookup"><span data-stu-id="86513-107">This new feature makes HDInsight one of the world’s most performant, flexible, and open Big Data solutions on the cloud with in-memory caches (using Hive and Spark) and advanced analytics through deep integration with R Services.</span></span> 

<span data-ttu-id="86513-108">O cluster Hive Interativo é diferente do cluster Hadoop.</span><span class="sxs-lookup"><span data-stu-id="86513-108">The Interactive Hive cluster is different from the Hadoop cluster.</span></span> <span data-ttu-id="86513-109">Ele contém apenas o serviço do Hive.</span><span class="sxs-lookup"><span data-stu-id="86513-109">It only contains the Hive service.</span></span> 

> [!NOTE]
> <span data-ttu-id="86513-110">MapReduce, Pig, Sqoop, Oozie e outros serviços, em breve, serão removidos desse tipo de cluster.</span><span class="sxs-lookup"><span data-stu-id="86513-110">MapReduce, Pig, Sqoop, Oozie, and other services will be removed from this cluster type soon.</span></span>
> <span data-ttu-id="86513-111">O serviço Hive no cluster do Hive Interativo só pode ser acessado por meio da exibição Hive do Ambari, do Beeline e do ODBC do Hive.</span><span class="sxs-lookup"><span data-stu-id="86513-111">The Hive service in the Interactive Hive cluster is only accessible via the Ambari Hive view, Beeline, and Hive ODBC.</span></span> <span data-ttu-id="86513-112">Ele não pode ser acessado por meio do console do Hive, do Templeton, da CLI do Azure e do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="86513-112">It can’t be accessed via Hive console, Templeton, Azure CLI, and Azure PowerShell.</span></span> 
> 
> 

## <a name="create-an-interactive-hive-cluster"></a><span data-ttu-id="86513-113">Criar um cluster do Hive Interativo</span><span class="sxs-lookup"><span data-stu-id="86513-113">Create an Interactive Hive cluster</span></span>
<span data-ttu-id="86513-114">O cluster do Hive Interativo é compatível apenas com clusters baseados em Linux.</span><span class="sxs-lookup"><span data-stu-id="86513-114">Interactive Hive cluster is only supported on Linux-based clusters.</span></span> <span data-ttu-id="86513-115">Para obter informações sobre a criação de clusters HDInsight, confira [Criar clusters Hadoop baseados em Linux em HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="86513-115">For information about creating HDInsight clusters, see [Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

## <a name="execute-hive-from-interactive-hive"></a><span data-ttu-id="86513-116">Executar o Hive do Hive Interativo</span><span class="sxs-lookup"><span data-stu-id="86513-116">Execute Hive from Interactive Hive</span></span>
<span data-ttu-id="86513-117">Há diferentes opções para executar consultas do Hive:</span><span class="sxs-lookup"><span data-stu-id="86513-117">There are different options how you can execute Hive queries:</span></span>

* <span data-ttu-id="86513-118">Executar o Hive usando a exibição Hive do Ambari</span><span class="sxs-lookup"><span data-stu-id="86513-118">Run Hive using the Ambari Hive view</span></span>
  
    <span data-ttu-id="86513-119">Para saber mais sobre como usar a Exibição Hive, confira [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md) (Usar a exibição Hive com o Hadoop no HDInsight).</span><span class="sxs-lookup"><span data-stu-id="86513-119">For the information about using the Hive View, see [Use the Hive View with Hadoop in HDInsight](hdinsight-hadoop-use-hive-ambari-view.md).</span></span>
* <span data-ttu-id="86513-120">Executar o Hive usando o Beeline</span><span class="sxs-lookup"><span data-stu-id="86513-120">Run Hive using Beeline</span></span>
  
    <span data-ttu-id="86513-121">Para obter informações sobre como usar o Beeline no HDInsight, confira [Usar o Hive com o Hadoop no HDInsight com Beeline](hdinsight-hadoop-use-hive-beeline.md).</span><span class="sxs-lookup"><span data-stu-id="86513-121">For the information on using Beeline on HDInsight, see [Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md).</span></span>
  
    <span data-ttu-id="86513-122">Use o Beeline no nó de cabeçalho ou em um nó de borda vazio.</span><span class="sxs-lookup"><span data-stu-id="86513-122">You use Beeline from either the headnode or an empty edge node.</span></span>  <span data-ttu-id="86513-123">É recomendável usar o Beeline em um nó de borda vazio.</span><span class="sxs-lookup"><span data-stu-id="86513-123">Using Beeline from an empty edge node is recommended.</span></span>  <span data-ttu-id="86513-124">Para saber mais sobre como criar um cluster HDInsight com um nó de borda vazio, confira [Usar nós de borda vazios no HDInsight](hdinsight-apps-use-edge-node.md).</span><span class="sxs-lookup"><span data-stu-id="86513-124">For information on creating an HDInsight cluster with an empty edgenode, see [Use empty edge nodes in HDInsight](hdinsight-apps-use-edge-node.md).</span></span>
* <span data-ttu-id="86513-125">Executar o Hive usando o ODBC do Hive</span><span class="sxs-lookup"><span data-stu-id="86513-125">Run Hive using Hive ODBC</span></span>
  
    <span data-ttu-id="86513-126">Para obter informações sobre como usar o ODBC do Hive, confira [Conectar o Excel ao Hadoop com o driver ODBC do Microsoft Hive](hdinsight-connect-excel-hive-odbc-driver.md).</span><span class="sxs-lookup"><span data-stu-id="86513-126">For the information on using Hive ODBC, see [Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md).</span></span>

<span data-ttu-id="86513-127">**Para encontrar a cadeia de conexão JDBC:**</span><span class="sxs-lookup"><span data-stu-id="86513-127">**To find the JDBC connection string:**</span></span>

1. <span data-ttu-id="86513-128">Entre no Ambari usando a seguinte URL: https://<ClusterName>.AzureHDInsight.net.</span><span class="sxs-lookup"><span data-stu-id="86513-128">Sign on to Ambari using the following URL: https://<ClusterName>.AzureHDInsight.net.</span></span>
2. <span data-ttu-id="86513-129">Clique em **Hive** no menu à esquerda.</span><span class="sxs-lookup"><span data-stu-id="86513-129">Click **Hive** from the left menu.</span></span>
3. <span data-ttu-id="86513-130">Clique no ícone realçado para copiar a URL:</span><span class="sxs-lookup"><span data-stu-id="86513-130">Click the highlighted icon to copy the URL:</span></span>
   
   ![JDBC LLAP do Hive Interativo no Hadoop HDInsight](./media/hdinsight-hadoop-use-interactive-hive/hdinsight-hadoop-use-interactive-hive-jdbc.png)

## <a name="see-also"></a><span data-ttu-id="86513-132">Consulte também</span><span class="sxs-lookup"><span data-stu-id="86513-132">See also</span></span>
* <span data-ttu-id="86513-133">[Criar clusters Hadoop baseados em Linux no HDInsight](hdinsight-hadoop-provision-linux-clusters.md): saiba como criar clusters Hive Interativo no HDInsight.</span><span class="sxs-lookup"><span data-stu-id="86513-133">[Create Linux-based Hadoop clusters in HDInsight](hdinsight-hadoop-provision-linux-clusters.md): Learn how to create Interactive Hive clusters in HDInsight.</span></span>
* <span data-ttu-id="86513-134">[Usar o Hive com o Hadoop no HDInsight com Beeline](hdinsight-hadoop-use-hive-beeline.md): saiba como usar o Beeline para enviar consultas do Hive.</span><span class="sxs-lookup"><span data-stu-id="86513-134">[Use Hive with Hadoop in HDInsight with Beeline](hdinsight-hadoop-use-hive-beeline.md): Learn how to use Beeline to submit Hive queries.</span></span>
* <span data-ttu-id="86513-135">[Conectar o Excel ao Hadoop com o driver ODBC do Microsoft Hive](hdinsight-connect-excel-hive-odbc-driver.md): saiba como conectar o Excel ao Hive.</span><span class="sxs-lookup"><span data-stu-id="86513-135">[Connect Excel to Hadoop with the Microsoft Hive ODBC driver](hdinsight-connect-excel-hive-odbc-driver.md): learn how to connect Excel to Hive.</span></span>

