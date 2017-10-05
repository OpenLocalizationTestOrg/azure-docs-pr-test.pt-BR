---
title: "Criar clusters Hadoop usando o PowerShell – Azure HDInsight | Microsoft Docs"
description: Saiba como criar clusters Hadoop, HBase, Storm ou Spark no Linux para o HDInsight usando o Azure PowerShell.
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
ms.openlocfilehash: ca75974e6ec4f60739137d4cb5458bbfd735de3e
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-linux-based-clusters-in-hdinsight-using-azure-powershell"></a><span data-ttu-id="560a2-103">Criar clusters baseados em Linux no HDInsight usando o Azure PowerShell</span><span class="sxs-lookup"><span data-stu-id="560a2-103">Create Linux-based clusters in HDInsight using Azure PowerShell</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="560a2-104">O Azure PowerShell é um ambiente de script poderoso que você pode usar para controlar e para automatizar a implantação e o gerenciamento de suas cargas de trabalho no Microsoft Azure.</span><span class="sxs-lookup"><span data-stu-id="560a2-104">Azure PowerShell is a powerful scripting environment that you can use to control and automate the deployment and management of your workloads in Microsoft Azure.</span></span> <span data-ttu-id="560a2-105">Este documento fornece informações sobre como criar um cluster HDInsight baseadas em Linux usando o Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="560a2-105">This document provides information about how to create a Linux-based HDInsight cluster by using Azure PowerShell.</span></span> <span data-ttu-id="560a2-106">Ele também inclui um script de exemplo.</span><span class="sxs-lookup"><span data-stu-id="560a2-106">It also includes an example script.</span></span>

> [!NOTE]
> <span data-ttu-id="560a2-107">O Azure PowerShell só está disponível em clientes do Windows.</span><span class="sxs-lookup"><span data-stu-id="560a2-107">Azure PowerShell is only available on Windows clients.</span></span> <span data-ttu-id="560a2-108">Se você estiver usando um cliente Linux, Unix ou Mac OS X, veja [Criar um cluster HDInsight baseado em Linux usando a CLI Azure](hdinsight-hadoop-create-linux-clusters-azure-cli.md) para obter informações sobre como usar a CLI do Azure para criar um cluster.</span><span class="sxs-lookup"><span data-stu-id="560a2-108">If you are using a Linux, Unix, or Mac OS X client, see [Create a Linux-based HDInsight cluster using Azure CLI](hdinsight-hadoop-create-linux-clusters-azure-cli.md) for information about using the Azure CLI to create a cluster.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="560a2-109">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="560a2-109">Prerequisites</span></span>
<span data-ttu-id="560a2-110">Você deve ter o seguinte antes de iniciar este procedimento:</span><span class="sxs-lookup"><span data-stu-id="560a2-110">You must have the following before starting this procedure:</span></span>

* <span data-ttu-id="560a2-111">Uma assinatura do Azure.</span><span class="sxs-lookup"><span data-stu-id="560a2-111">An Azure subscription.</span></span> <span data-ttu-id="560a2-112">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="560a2-112">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>
* [<span data-ttu-id="560a2-113">PowerShell do Azure</span><span class="sxs-lookup"><span data-stu-id="560a2-113">Azure PowerShell</span></span>](/powershell/azure/install-azurerm-ps)

    > [!IMPORTANT]
    > <span data-ttu-id="560a2-114">O suporte do Azure PowerShell para gerenciar os recursos do HDInsight usando o Gerenciador de Serviços do Azure está **preterido** e foi removido em 1º de janeiro de 2017.</span><span class="sxs-lookup"><span data-stu-id="560a2-114">Azure PowerShell support for managing HDInsight resources using Azure Service Manager is **deprecated**, and was removed on January 1, 2017.</span></span> <span data-ttu-id="560a2-115">As etapas neste documento usam os novos cmdlets do HDInsight que funcionam com o Azure Resource Manager.</span><span class="sxs-lookup"><span data-stu-id="560a2-115">The steps in this document use the new HDInsight cmdlets that work with Azure Resource Manager.</span></span>
    >
    > <span data-ttu-id="560a2-116">Siga as etapas em [Instalar o Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) para instalar a versão mais recente do Azure PowerShell.</span><span class="sxs-lookup"><span data-stu-id="560a2-116">Please follow the steps in [Install Azure PowerShell](https://docs.microsoft.com/powershell/azure/install-azurerm-ps) to install the latest version of Azure PowerShell.</span></span> <span data-ttu-id="560a2-117">Se você tiver scripts que precisam ser modificados para usar os novos cmdlets que funcionam com o Azure Resource Manager, confira [Migrando para as ferramentas de desenvolvimento baseadas no Azure Resource Manager dos clusters de HDInsight](hdinsight-hadoop-development-using-azure-resource-manager.md) para obter mais informações.</span><span class="sxs-lookup"><span data-stu-id="560a2-117">If you have scripts that need to be modified to use the new cmdlets that work with Azure Resource Manager, see [Migrating to Azure Resource Manager-based development tools for HDInsight clusters](hdinsight-hadoop-development-using-azure-resource-manager.md) for more information.</span></span>

## <a name="create-cluster"></a><span data-ttu-id="560a2-118">Criar cluster</span><span class="sxs-lookup"><span data-stu-id="560a2-118">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

<span data-ttu-id="560a2-119">Para criar um cluster HDInsight usando o Azure PowerShell, siga estes procedimentos:</span><span class="sxs-lookup"><span data-stu-id="560a2-119">To create an HDInsight cluster by using Azure PowerShell, you must complete the following procedures:</span></span>

* <span data-ttu-id="560a2-120">Criar um grupo de recursos do Azure</span><span class="sxs-lookup"><span data-stu-id="560a2-120">Create an Azure resource group</span></span>
* <span data-ttu-id="560a2-121">Criar uma conta de Armazenamento do Azure</span><span class="sxs-lookup"><span data-stu-id="560a2-121">Create an Azure Storage account</span></span>
* <span data-ttu-id="560a2-122">Criar um contêiner de Blob do Azure</span><span class="sxs-lookup"><span data-stu-id="560a2-122">Create an Azure Blob container</span></span>
* <span data-ttu-id="560a2-123">Crie um cluster HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a2-123">Create an HDInsight cluster</span></span>

<span data-ttu-id="560a2-124">O script a seguir demonstra como criar um novo cluster:</span><span class="sxs-lookup"><span data-stu-id="560a2-124">The following script demonstrates how to create a new cluster:</span></span>

<span data-ttu-id="560a2-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span><span class="sxs-lookup"><span data-stu-id="560a2-125">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster.ps1?range=5-71)]</span></span>

<span data-ttu-id="560a2-126">Os valores especificados para o logon de cluster são usados para criar a conta de usuário do Hadoop para o cluster.</span><span class="sxs-lookup"><span data-stu-id="560a2-126">The values you specify for the cluster login are used to create the Hadoop user account for the cluster.</span></span> <span data-ttu-id="560a2-127">Use essa conta para se conectar a serviços hospedados no cluster, como interfaces do usuário da Web ou APIs REST.</span><span class="sxs-lookup"><span data-stu-id="560a2-127">Use this account to connect to services hosted on the cluster such as web UIs or REST APIs.</span></span>

<span data-ttu-id="560a2-128">Os valores especificados para o usuário SSH são usados para criar o usuário SSH para o cluster.</span><span class="sxs-lookup"><span data-stu-id="560a2-128">The values you specify for the SSH user are used to create the SSH user for the cluster.</span></span> <span data-ttu-id="560a2-129">Use essa conta para iniciar uma sessão SSH remota no cluster e executar trabalhos.</span><span class="sxs-lookup"><span data-stu-id="560a2-129">Use this account to start a remote SSH session on the cluster and run jobs.</span></span> <span data-ttu-id="560a2-130">Para saber mais, consulte o documento [Usar SSH com HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md).</span><span class="sxs-lookup"><span data-stu-id="560a2-130">For more information, see the [Use SSH with HDInsight](hdinsight-hadoop-linux-use-ssh-unix.md) document.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="560a2-131">Se você planeja ter mais de 32 nós de trabalho (seja na criação do cluster ou em seu dimensionamento após a criação), deverá também especificar um tamanho de nó de cabeçalho com pelo menos oito núcleos e 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="560a2-131">If you plan to use more than 32 worker nodes (either at cluster creation or by scaling the cluster after creation), you must also specify a head node size with at least 8 cores and 14 GB of RAM.</span></span>
>
> <span data-ttu-id="560a2-132">Para saber mais sobre tamanhos de nós e custos associados, consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="560a2-132">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

<span data-ttu-id="560a2-133">Pode levar até 20 minutos para criar um cluster.</span><span class="sxs-lookup"><span data-stu-id="560a2-133">It can take up to 20 minutes to create a cluster.</span></span>

## <a name="create-cluster-configuration-object"></a><span data-ttu-id="560a2-134">Criar cluster: objeto de configuração</span><span class="sxs-lookup"><span data-stu-id="560a2-134">Create cluster: Configuration object</span></span>

<span data-ttu-id="560a2-135">Você também pode criar um objeto de configuração de HDInsight usando o cmdlet `New-AzureRmHDInsightClusterConfig`.</span><span class="sxs-lookup"><span data-stu-id="560a2-135">You can also create an HDInsight configuration object using `New-AzureRmHDInsightClusterConfig` cmdlet.</span></span> <span data-ttu-id="560a2-136">Será possível, então, modificar esse objeto de configuração para habilitar as opções de configuração adicionais para o cluster.</span><span class="sxs-lookup"><span data-stu-id="560a2-136">You can then modify this configuration object to enable additional configuration options for your cluster.</span></span> <span data-ttu-id="560a2-137">Por fim, use o parâmetro `-Config` do cmdlet `New-AzureRmHDInsightCluster` para usar a configuração.</span><span class="sxs-lookup"><span data-stu-id="560a2-137">Finally, use the `-Config` parameter of the `New-AzureRmHDInsightCluster` cmdlet to use the configuration.</span></span>

<span data-ttu-id="560a2-138">O script a seguir cria um objeto de configuração para configurar um R Server no tipo de cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="560a2-138">The following script creates a configuration object to configure an R Server on HDInsight cluster type.</span></span> <span data-ttu-id="560a2-139">A configuração habilita um nó de borda, RStudio e uma conta de armazenamento adicionais.</span><span class="sxs-lookup"><span data-stu-id="560a2-139">The configuration enables an edge node, RStudio, and an additional storage account.</span></span>

<span data-ttu-id="560a2-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span><span class="sxs-lookup"><span data-stu-id="560a2-140">[!code-powershell[main](../../powershell_scripts/hdinsight/create-cluster/create-cluster-with-config.ps1?range=59-98)]</span></span>

> [!WARNING]
> <span data-ttu-id="560a2-141">Não há suporte para o uso de uma conta de armazenamento em um local diferente do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="560a2-141">Using a storage account in a different location than the HDInsight cluster is not supported.</span></span> <span data-ttu-id="560a2-142">Ao usar este exemplo, crie a conta de armazenamento adicional no mesmo local do servidor.</span><span class="sxs-lookup"><span data-stu-id="560a2-142">When using this example, create the additional storage account in the same location as the server.</span></span>

## <a name="customize-clusters"></a><span data-ttu-id="560a2-143">Personalizar clusters</span><span class="sxs-lookup"><span data-stu-id="560a2-143">Customize clusters</span></span>

* <span data-ttu-id="560a2-144">Consulte [Personalizar clusters do HDInsight usando a Inicialização](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span><span class="sxs-lookup"><span data-stu-id="560a2-144">See [Customize HDInsight clusters using Bootstrap](hdinsight-hadoop-customize-cluster-bootstrap.md#use-azure-powershell).</span></span>
* <span data-ttu-id="560a2-145">Consulte [Personalizar os clusters HDInsight usando a Ação de Script](hdinsight-hadoop-customize-cluster-linux.md).</span><span class="sxs-lookup"><span data-stu-id="560a2-145">See [Customize HDInsight clusters using Script Action](hdinsight-hadoop-customize-cluster-linux.md).</span></span>

## <a name="delete-the-cluster"></a><span data-ttu-id="560a2-146">Excluir o cluster</span><span class="sxs-lookup"><span data-stu-id="560a2-146">Delete the cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

## <a name="troubleshoot"></a><span data-ttu-id="560a2-147">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="560a2-147">Troubleshoot</span></span>

<span data-ttu-id="560a2-148">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="560a2-148">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="560a2-149">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="560a2-149">Next steps</span></span>

<span data-ttu-id="560a2-150">Agora que você criou com êxito um cluster HDInsight, use os seguintes recursos para aprender a trabalhar com o seu cluster.</span><span class="sxs-lookup"><span data-stu-id="560a2-150">Now that you have successfully created an HDInsight cluster, use the following resources to learn how to work with your cluster.</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="560a2-151">Clusters do Hadoop</span><span class="sxs-lookup"><span data-stu-id="560a2-151">Hadoop clusters</span></span>

* [<span data-ttu-id="560a2-152">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a2-152">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="560a2-153">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a2-153">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="560a2-154">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a2-154">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="560a2-155">Clusters do HBase</span><span class="sxs-lookup"><span data-stu-id="560a2-155">HBase clusters</span></span>

* [<span data-ttu-id="560a2-156">Introdução ao HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a2-156">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="560a2-157">Desenvolvimento de aplicativos Java para HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a2-157">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="560a2-158">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="560a2-158">Storm clusters</span></span>

* [<span data-ttu-id="560a2-159">Desenvolver topologias Java para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a2-159">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="560a2-160">Usar componentes de Python no Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a2-160">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="560a2-161">Implantar e monitorar topologias com o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="560a2-161">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)

### <a name="spark-clusters"></a><span data-ttu-id="560a2-162">Clusters do Spark</span><span class="sxs-lookup"><span data-stu-id="560a2-162">Spark clusters</span></span>

* [<span data-ttu-id="560a2-163">Criar um aplicativo autônomo usando Scala</span><span class="sxs-lookup"><span data-stu-id="560a2-163">Create a standalone application using Scala</span></span>](hdinsight-apache-spark-create-standalone-application.md)
* [<span data-ttu-id="560a2-164">Executar trabalhos remotamente em um cluster do Spark usando Livy</span><span class="sxs-lookup"><span data-stu-id="560a2-164">Run jobs remotely on a Spark cluster using Livy</span></span>](hdinsight-apache-spark-livy-rest-interface.md)
* [<span data-ttu-id="560a2-165">Spark com BI: executar análise de dados interativa usando o Spark no HDInsight com ferramentas de BI</span><span class="sxs-lookup"><span data-stu-id="560a2-165">Spark with BI: Perform interactive data analysis using Spark in HDInsight with BI tools</span></span>](hdinsight-apache-spark-use-bi-tools.md)
* <span data-ttu-id="560a2-166">
            [Spark com Machine Learning: usar o Spark no HDInsight para prever resultados da inspeção de alimentos](hdinsight-apache-spark-machine-learning-mllib-ipython.md)</span><span class="sxs-lookup"><span data-stu-id="560a2-166">[Spark with Machine Learning: Use Spark in HDInsight to predict food inspection results](hdinsight-apache-spark-machine-learning-mllib-ipython.md)</span></span>
* [<span data-ttu-id="560a2-167">Streaming Spark: usar o Spark no HDInsight para a criação de aplicativos streaming em tempo real</span><span class="sxs-lookup"><span data-stu-id="560a2-167">Spark Streaming: Use Spark in HDInsight for building real-time streaming applications</span></span>](hdinsight-apache-spark-eventhub-streaming.md)

