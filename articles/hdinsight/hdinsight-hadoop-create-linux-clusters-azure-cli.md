---
title: "clusters de Hadoop aaaCreate usando a linha de comando - Olá HDInsight do Azure | Microsoft Docs"
description: "Saiba como clusters de HDInsight toocreate usando Olá 1.0 de CLI do Azure de plataforma cruzada."
services: hdinsight
documentationcenter: 
author: Blackmist
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.assetid: 50b01483-455c-4d87-b754-2229005a8ab9
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 06/26/2017
ms.author: larryfr
ms.openlocfilehash: 5295b01054b8c23df0e3b75a3e0e8c933ac48b3c
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hdinsight-clusters-using-hello-azure-cli"></a><span data-ttu-id="aab6f-103">Criar clusters HDInsight usando Olá CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="aab6f-103">Create HDInsight clusters using hello Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="aab6f-104">Olá etapas para este passo a passo documento criando um cluster HDInsight 3.5 usando Olá 1.0 da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="aab6f-104">hello steps in this document walk-through creating a HDInsight 3.5 cluster using hello Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="aab6f-105">Linux é Olá sistema operacional somente de usado no HDInsight versão 3.4 ou posterior.</span><span class="sxs-lookup"><span data-stu-id="aab6f-105">Linux is hello only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="aab6f-106">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="aab6f-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="aab6f-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="aab6f-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="aab6f-108">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="aab6f-108">**An Azure subscription**.</span></span> <span data-ttu-id="aab6f-109">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="aab6f-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="aab6f-110">**CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="aab6f-110">**Azure CLI**.</span></span> <span data-ttu-id="aab6f-111">etapas Olá neste documento foram testadas última CLI do Azure versão 0.10.14.</span><span class="sxs-lookup"><span data-stu-id="aab6f-111">hello steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="aab6f-112">Olá etapas neste documento não funcionam com o Azure CLI 2.0.</span><span class="sxs-lookup"><span data-stu-id="aab6f-112">hello steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="aab6f-113">A CLI do Azure 2.0 não dá suporte à criação de um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aab6f-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-tooyour-azure-subscription"></a><span data-ttu-id="aab6f-114">Faça logon no tooyour assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="aab6f-114">Log in tooyour Azure subscription</span></span>

<span data-ttu-id="aab6f-115">Execute as etapas de saudação documentadas em [conectar tooan assinatura do Azure do hello Azure Interface de linha de comando (CLI do Azure)](../xplat-cli-connect.md) e conecte-se a assinatura de tooyour usando Olá **login** método.</span><span class="sxs-lookup"><span data-stu-id="aab6f-115">Follow hello steps documented in [Connect tooan Azure subscription from hello Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect tooyour subscription using hello **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="aab6f-116">Criar um cluster</span><span class="sxs-lookup"><span data-stu-id="aab6f-116">Create a cluster</span></span>

<span data-ttu-id="aab6f-117">Olá, as etapas a seguir deve ser executada em uma linha de comando, como o PowerShell ou Bash.</span><span class="sxs-lookup"><span data-stu-id="aab6f-117">hello following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="aab6f-118">Use Olá comando tooauthenticate tooyour assinatura do Azure a seguir:</span><span class="sxs-lookup"><span data-stu-id="aab6f-118">Use hello following command tooauthenticate tooyour Azure subscription:</span></span>

        azure login

    <span data-ttu-id="aab6f-119">Você está tooprovide solicitado seu nome e senha.</span><span class="sxs-lookup"><span data-stu-id="aab6f-119">You are prompted tooprovide your name and password.</span></span> <span data-ttu-id="aab6f-120">Se você tiver várias assinaturas do Azure, use `azure account set <subscriptionname>` uso de comandos de assinatura Olá tooset Olá CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="aab6f-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` tooset hello subscription that hello Azure CLI commands use.</span></span>

2. <span data-ttu-id="aab6f-121">Alternar o modo de Gerenciador de recursos de tooAzure usando Olá comando a seguir:</span><span class="sxs-lookup"><span data-stu-id="aab6f-121">Switch tooAzure Resource Manager mode using hello following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="aab6f-122">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="aab6f-122">Create a resource group.</span></span> <span data-ttu-id="aab6f-123">Este grupo de recursos contém o cluster do HDInsight hello e conta de armazenamento associada.</span><span class="sxs-lookup"><span data-stu-id="aab6f-123">This resource group contains hello HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="aab6f-124">Substituir `groupname` com um nome exclusivo para o grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab6f-124">Replace `groupname` with a unique name for hello group.</span></span>

    * <span data-ttu-id="aab6f-125">Substituir `location` com região Olá que deseja toocreate grupo de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab6f-125">Replace `location` with hello geographic region that you want toocreate hello group in.</span></span>

       <span data-ttu-id="aab6f-126">Para obter uma lista de locais válidos, use Olá `azure location list` de comando e, em seguida, use um dos locais de saudação do hello `Name` coluna.</span><span class="sxs-lookup"><span data-stu-id="aab6f-126">For a list of valid locations, use hello `azure location list` command, and then use one of hello locations from hello `Name` column.</span></span>

4. <span data-ttu-id="aab6f-127">Criar uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="aab6f-127">Create a storage account.</span></span> <span data-ttu-id="aab6f-128">Esta conta de armazenamento é usada como o armazenamento padrão da saudação para cluster de HDInsight hello.</span><span class="sxs-lookup"><span data-stu-id="aab6f-128">This storage account is used as hello default storage for hello HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="aab6f-129">Substituir `groupname` com nome Olá Olá grupo criado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="aab6f-129">Replace `groupname` with hello name of hello group created in hello previous step.</span></span>

    * <span data-ttu-id="aab6f-130">Substituir `location` com hello mesmo local usado na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="aab6f-130">Replace `location` with hello same location used in hello previous step.</span></span>

    * <span data-ttu-id="aab6f-131">Substituir `storagename` com um nome exclusivo para a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="aab6f-131">Replace `storagename` with a unique name for hello storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="aab6f-132">Para obter mais informações sobre parâmetros de saudação usado neste comando, use `azure storage account create -h` tooview ajuda para este comando.</span><span class="sxs-lookup"><span data-stu-id="aab6f-132">For more information on hello parameters used in this command, use `azure storage account create -h` tooview help for this command.</span></span>

5. <span data-ttu-id="aab6f-133">Recupere a conta de armazenamento de Olá Olá chave tooaccess usado.</span><span class="sxs-lookup"><span data-stu-id="aab6f-133">Retrieve hello key used tooaccess hello storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="aab6f-134">Substituir `groupname` com o nome do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab6f-134">Replace `groupname` with hello resource group name.</span></span>
    * <span data-ttu-id="aab6f-135">Substituir `storagename` com nome Olá Olá da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="aab6f-135">Replace `storagename` with hello name of hello storage account.</span></span>

     <span data-ttu-id="aab6f-136">Em dados de saudação que são retornados, salvar Olá `key` valor para `key1`.</span><span class="sxs-lookup"><span data-stu-id="aab6f-136">In hello data that is returned, save hello `key` value for `key1`.</span></span>

6. <span data-ttu-id="aab6f-137">Crie um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="aab6f-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="aab6f-138">Substituir `groupname` com o nome do grupo de recursos de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab6f-138">Replace `groupname` with hello resource group name.</span></span>

    * <span data-ttu-id="aab6f-139">Substituir `Hadoop` com o tipo de cluster Olá que você deseja toocreate.</span><span class="sxs-lookup"><span data-stu-id="aab6f-139">Replace `Hadoop` with hello cluster type that you wish toocreate.</span></span> <span data-ttu-id="aab6f-140">Por exemplo, `Hadoop`, `HBase`, `Kafka`, `Spark` ou `Storm`.</span><span class="sxs-lookup"><span data-stu-id="aab6f-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="aab6f-141">HDInsight clusters são fornecidos em vários tipos, que correspondem a carga de trabalho toohello ou tecnologia que Olá cluster é ajustada para.</span><span class="sxs-lookup"><span data-stu-id="aab6f-141">HDInsight clusters come in various types, which correspond toohello workload or technology that hello cluster is tuned for.</span></span> <span data-ttu-id="aab6f-142">Não há nenhum método com suporte toocreate um cluster que combina vários tipos, como Storm e HBase em um cluster.</span><span class="sxs-lookup"><span data-stu-id="aab6f-142">There is no supported method toocreate a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="aab6f-143">Substituir `location` com hello mesmo local usado nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="aab6f-143">Replace `location` with hello same location used in previous steps.</span></span>

    * <span data-ttu-id="aab6f-144">Substituir `storagename` com o nome de conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="aab6f-144">Replace `storagename` with hello storage account name.</span></span>

    * <span data-ttu-id="aab6f-145">Substituir `storagekey` com chave Olá obtido na etapa anterior hello.</span><span class="sxs-lookup"><span data-stu-id="aab6f-145">Replace `storagekey` with hello key obtained in hello previous step.</span></span>

    * <span data-ttu-id="aab6f-146">Para Olá `--defaultStorageContainer` parâmetro, use Olá mesmo nome que você está usando para o cluster de saudação.</span><span class="sxs-lookup"><span data-stu-id="aab6f-146">For hello `--defaultStorageContainer` parameter, use hello same name as you are using for hello cluster.</span></span>

    * <span data-ttu-id="aab6f-147">Substituir `admin` e `httppassword` com hello nome e senha você deseja toouse ao acessar o cluster Olá através de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="aab6f-147">Replace `admin` and `httppassword` with hello name and password you wish toouse when accessing hello cluster through HTTPS.</span></span>

    * <span data-ttu-id="aab6f-148">Substituir `sshuser` e `sshuserpassword` com hello nome de usuário e senha você deseja toouse ao acessar o cluster hello usando SSH</span><span class="sxs-lookup"><span data-stu-id="aab6f-148">Replace `sshuser` and `sshuserpassword` with hello username and password you wish toouse when accessing hello cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="aab6f-149">Este exemplo cria um cluster com duas anotações de trabalho.</span><span class="sxs-lookup"><span data-stu-id="aab6f-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="aab6f-150">Você também pode alterar o número de saudação de nós de trabalho após a criação do cluster realizando operações de dimensionamento.</span><span class="sxs-lookup"><span data-stu-id="aab6f-150">You can also change hello number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="aab6f-151">Se você planeja usar mais de 32 nós de trabalho, será necessário selecionar um tamanho de nó de cabeçalho com pelo menos oito núcleos e 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="aab6f-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="aab6f-152">Você pode definir o tamanho de nó principal do hello usando Olá `--headNodeSize` parâmetro durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="aab6f-152">You can set hello head node size by using hello `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="aab6f-153">Para saber mais sobre tamanhos de nós e custos associados, consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="aab6f-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="aab6f-154">Ele pode levar vários minutos para Olá toofinish de processo de criação de cluster.</span><span class="sxs-lookup"><span data-stu-id="aab6f-154">It may take several minutes for hello cluster creation process toofinish.</span></span> <span data-ttu-id="aab6f-155">Geralmente, cerca de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="aab6f-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="aab6f-156">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="aab6f-156">Troubleshoot</span></span>

<span data-ttu-id="aab6f-157">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="aab6f-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="aab6f-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="aab6f-158">Next steps</span></span>

<span data-ttu-id="aab6f-159">Agora que você criou com êxito um cluster HDInsight usando Olá CLI do Azure, use Olá toolearn a seguir como toowork com o cluster:</span><span class="sxs-lookup"><span data-stu-id="aab6f-159">Now that you have successfully created an HDInsight cluster using hello Azure CLI, use hello following toolearn how toowork with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="aab6f-160">Clusters do Hadoop</span><span class="sxs-lookup"><span data-stu-id="aab6f-160">Hadoop clusters</span></span>

* [<span data-ttu-id="aab6f-161">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="aab6f-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="aab6f-162">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="aab6f-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="aab6f-163">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="aab6f-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="aab6f-164">Clusters do HBase</span><span class="sxs-lookup"><span data-stu-id="aab6f-164">HBase clusters</span></span>

* [<span data-ttu-id="aab6f-165">Introdução ao HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="aab6f-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="aab6f-166">Desenvolvimento de aplicativos Java para HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="aab6f-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="aab6f-167">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="aab6f-167">Storm clusters</span></span>

* [<span data-ttu-id="aab6f-168">Desenvolver topologias Java para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="aab6f-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="aab6f-169">Usar componentes de Python no Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="aab6f-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="aab6f-170">Implantar e monitorar topologias com o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="aab6f-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
