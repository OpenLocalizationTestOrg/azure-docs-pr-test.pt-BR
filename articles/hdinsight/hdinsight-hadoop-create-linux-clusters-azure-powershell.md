---
title: clusters de Hadoop aaaCreate usando o PowerShell - HDInsight do Azure | Microsoft Docs
description: Saiba como toocreate Hadoop, HBase, tempestade ou Spark clusters no Linux para HDInsight usando o PowerShell do Azure.
services: hdinsight
documentationcenter: 
author: nitinme
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 4208deca-d64a-45e1-8948-2673d5d7678c
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 05/10/2017
ms.author: nitinme
ms.openlocfilehash: 53afe4702f6b61a0720ceda48a4a34d7fa8797d1
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="ceda8-103">Criar clusters baseados em Linux no HDInsight usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="ceda8-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="ceda8-104">PowerShell do Azure é um ambiente de script poderoso que você pode usar toocontrol e automatizar a implantação de saudação e o gerenciamento de suas cargas de trabalho no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="ceda8-104">Azure PowerShell is a powerful scripting environment that you can use toocontrol and automate hello deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="ceda8-105">Este documento fornece informações sobre como toocreate uma HDInsight baseados em Linux de cluster usando o PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceda8-105">This document provides information about how toocreate a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="ceda8-106">Ele também inclui um script de exemplo.</span><span class="sxs-lookup"><span data-stu-id="ceda8-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="ceda8-107">O Azure PowerShell só está disponível em clientes do Windows.</span><span class="sxs-lookup"><span data-stu-id="ceda8-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="ceda8-108">Se você estiver usando um cliente Mac OS X, Unix ou Linux, consulte [criar um cluster HDInsight baseados em Linux usando a CLI do Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) para obter informações sobre como usar o hello CLI do Azure toocreate um cluster.</span><span class="sxs-lookup"><span data-stu-id="ceda8-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using hello Azure CLI toocreate a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="ceda8-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="ceda8-109">Prerequisites</span></span>
<span data-ttu-id="ceda8-110">Você deve ter o seguinte Olá antes de iniciar este procedimento:</span><span class="sxs-lookup"><span data-stu-id="ceda8-110">You must have hello following before starting this procedure:</span></span>

* <span data-ttu-id="ceda8-111">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceda8-111">An Azure subscription.</span></span> <span data-ttu-id="ceda8-112">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ceda8-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="ceda8-113">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="ceda8-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="ceda8-114">O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e foi removido em 1º de janeiro de 2017.</span><span class="sxs-lookup"><span data-stu-id="ceda8-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="ceda8-115">Olá etapas para esse documento use Olá novos cmdlets do HDInsight que funcionam com o Gerenciador de recursos do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceda8-115">hello steps in this document use hello new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="ceda8-116">Siga as etapas de saudação em [instalar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall Olá última versão do PowerShell do Azure.</span><span class="sxs-lookup"><span data-stu-id="ceda8-116">Please follow hello steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) tooinstall hello latest version of Azure PowerShell.</span></span> <span data-ttu-id="ceda8-117">Se você tiver scripts que toobe necessidade modificado toouse Olá novos cmdlets que funcionam com o Gerenciador de recursos do Azure, consulte [tooAzure migrando desenvolvimento baseado no Gerenciador de recursos de ferramentas para clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="ceda8-117">If you have scripts that need toobe modified toouse hello new cmdlets that work with Azure Resource Manager, see [Migrating tooAzure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="ceda8-118">Criar cluster</span><span class="sxs-lookup"><span data-stu-id="ceda8-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="ceda8-119">toocreate um cluster HDInsight usando o PowerShell do Azure, você deve concluir Olá procedimentos a seguir:</span><span class="sxs-lookup"><span data-stu-id="ceda8-119">toocreate an HDInsight cluster by using Azure PowerShell, you must complete hello following procedures:</span></span>

* <span data-ttu-id="ceda8-120">Criar um grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="ceda8-120">Create an Azure resource group</span></span>
* <span data-ttu-id="ceda8-121">Criar uma conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="ceda8-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="ceda8-122">Criar um contêiner de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="ceda8-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="ceda8-123">Crie um cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceda8-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="ceda8-124">Olá script a seguir demonstra como toocreate um novo cluster:</span><span class="sxs-lookup"><span data-stu-id="ceda8-124">hello following script demonstrates how toocreate a new cluster:</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]

<span data-ttu-id="ceda8-125">os valores de Olá especificado para o logon de cluster Olá são toocreate usado Olá conta de usuário do Hadoop para cluster hello.</span><span class="sxs-lookup"><span data-stu-id="ceda8-125">hello values you specify for hello cluster login are used toocreate hello Hadoop user account for hello cluster.</span></span> <span data-ttu-id="ceda8-126">Use este tooservices de tooconnect conta hospedadas no cluster hello como web interfaces do usuário ou APIs REST.</span><span class="sxs-lookup"><span data-stu-id="ceda8-126">Use this account tooconnect tooservices hosted on hello cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="ceda8-127">os valores Hello especificado para o usuário SSH Olá são usuário SSH Olá toocreate usado para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="ceda8-127">hello values you specify for hello SSH user are used toocreate hello SSH user for hello cluster.</span></span> <span data-ttu-id="ceda8-128">Use esta conta toostart uma sessão remota do SSH no cluster hello e executar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="ceda8-128">Use this account toostart a remote SSH session on hello cluster and run jobs.</span></span> <span data-ttu-id="ceda8-129">Para obter mais informações, consulte Olá [usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) documento.</span><span class="sxs-lookup"><span data-stu-id="ceda8-129">For more information, see hello [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ceda8-130">Se você planejar toouse mais de 32 nós de trabalho (na criação de cluster ou escala Olá cluster após a criação), você também deve especificar um tamanho de nó principal com pelo menos 8 núcleos e 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="ceda8-130">If you plan toouse more than 32 worker nodes (either at cluster creation or by scaling hello cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="ceda8-131">Para saber mais sobre tamanhos de nós e custos associados, consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="ceda8-131">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="ceda8-132">Pode demorar até too20 minutos toocreate um cluster.</span><span class="sxs-lookup"><span data-stu-id="ceda8-132">It can take up too20 minutes toocreate a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="ceda8-133">Criar cluster: objeto de configuração</span><span class="sxs-lookup"><span data-stu-id="ceda8-133">Create cluster: Configuration object</span></span>

<span data-ttu-id="ceda8-134">Você também pode criar um objeto de configuração de HDInsight usando o cmdlet `New-AzureRmHDInsightClusterConfig`.</span><span class="sxs-lookup"><span data-stu-id="ceda8-134">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="ceda8-135">Você pode modificar essa configuração objeto tooenable outras opções de configuração para o cluster.</span><span class="sxs-lookup"><span data-stu-id="ceda8-135">You can then modify this configuration object tooenable additional configuration options for your cluster.</span></span> <span data-ttu-id="ceda8-136">Por fim, use Olá `-Config` parâmetro hello `New-AzureRmHDInsightCluster` configuração de saudação do cmdlet toouse.</span><span class="sxs-lookup"><span data-stu-id="ceda8-136">Finally, use hello `-Config` parameter of hello `New-AzureRmHDInsightCluster` cmdlet toouse hello configuration.</span></span>

<span data-ttu-id="ceda8-137">Olá script a seguir cria um tooconfigure do objeto de configuração um servidor de R no tipo de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="ceda8-137">hello following script creates a configuration object tooconfigure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="ceda8-138">configuração de saudação permite que um nó de borda, RStudio e uma conta de armazenamento adicionais.</span><span class="sxs-lookup"><span data-stu-id="ceda8-138">hello configuration enables an edge node, RStudio, and an additional storage account.</span></span>

[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]

> [!WARNING]
> <span data-ttu-id="ceda8-139">Não há suporte para usar uma conta de armazenamento no cluster do HDInsight Olá um local diferente.</span><span class="sxs-lookup"><span data-stu-id="ceda8-139">Using a storage account in a different location than hello HDInsight cluster is not supported.</span></span> <span data-ttu-id="ceda8-140">Ao usar este exemplo, criar a conta de armazenamento adicional de saudação em Olá mesmo local como servidor de saudação.</span><span class="sxs-lookup"><span data-stu-id="ceda8-140">When using this example, create hello additional storage account in hello same location as hello server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="ceda8-141">Personalizar clusters</span><span class="sxs-lookup"><span data-stu-id="ceda8-141">Customize clusters</span></span>

* <span data-ttu-id="ceda8-142">Consulte [Personalizar clusters do HDInsight usando a Inicialização](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="ceda8-142">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="ceda8-143">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="ceda8-143">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-hello-cluster"></a><span data-ttu-id="ceda8-144">Excluir o cluster Olá</span><span class="sxs-lookup"><span data-stu-id="ceda8-144">Delete hello cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="ceda8-145">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="ceda8-145">Troubleshoot</span></span>

<span data-ttu-id="ceda8-146">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="ceda8-146">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="ceda8-147">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="ceda8-147">Next steps</span></span>

<span data-ttu-id="ceda8-148">Agora que você criou com êxito um cluster HDInsight, use Olá toolearn recursos a seguir como toowork com o cluster.</span><span class="sxs-lookup"><span data-stu-id="ceda8-148">Now that you have successfully created an HDInsight cluster, use hello following resources toolearn how toowork with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="ceda8-149">Clusters do Hadoop</span><span class="sxs-lookup"><span data-stu-id="ceda8-149">Hadoop clusters</span></span>

* [<span data-ttu-id="ceda8-150">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceda8-150">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="ceda8-151">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceda8-151">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="ceda8-152">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceda8-152">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="ceda8-153">Clusters do HBase</span><span class="sxs-lookup"><span data-stu-id="ceda8-153">HBase clusters</span></span>

* [<span data-ttu-id="ceda8-154">Introdução ao HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceda8-154">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="ceda8-155">Desenvolvimento de aplicativos Java para HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceda8-155">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="ceda8-156">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="ceda8-156">Storm clusters</span></span>

* [<span data-ttu-id="ceda8-157">Desenvolver topologias Java para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceda8-157">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="ceda8-158">Usar componentes de Python no Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceda8-158">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="ceda8-159">Implantar e monitorar topologias com o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="ceda8-159">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="ceda8-160">Clusters do Spark</span><span class="sxs-lookup"><span data-stu-id="ceda8-160">Spark clusters</span></span>

* [<span data-ttu-id="ceda8-161">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="ceda8-161">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="ceda8-162">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="ceda8-162">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="ceda8-163">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="ceda8-163">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* [<span data-ttu-id="ceda8-164">Spark com o aprendizado de máquina: Use Spark nos resultados de inspeção de alimentos HDInsight toopredict</span><span class="sxs-lookup"><span data-stu-id="ceda8-164">Spark with Machine Learning: Use Spark in HDInsight toopredict food inspection results</span></span>](hdinsight-apache-spark-machine-learning-mllib-ipython.md)
* [<span data-ttu-id="ceda8-165">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos de streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="ceda8-165">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

