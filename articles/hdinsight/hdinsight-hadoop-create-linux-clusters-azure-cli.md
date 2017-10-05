---
title: "Criar clusters Hadoop usando a linha de comando – Azure HDInsight | Microsoft Docs"
description: Saiba como criar clusters do HDInsight usando a CLI do Azure 1.0 de plataforma cruzada.
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
ms.openlocfilehash: 8f2fcb46789d000cd66164508f1159338dcae5f9
ms.sourcegitcommit: f537befafb079256fba0529ee554c034d73f36b0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/11/2017
---
# <a name="create-hdinsight-clusters-using-the-azure-cli"></a><span data-ttu-id="504ff-103">Criar os clusters do HDInsight usando a CLI do Azure</span><span class="sxs-lookup"><span data-stu-id="504ff-103">Create HDInsight clusters using the Azure CLI</span></span>

[!INCLUDE [selector](../../includes/hdinsight-create-linux-cluster-selector.md)]

<span data-ttu-id="504ff-104">As etapas deste documento são um passo a passo para a criação de um cluster HDInsight 3.5 usando a CLI do Azure 1.0.</span><span class="sxs-lookup"><span data-stu-id="504ff-104">The steps in this document walk-through creating a HDInsight 3.5 cluster using the Azure CLI 1.0.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="504ff-105">O Linux é o único sistema operacional usado no HDInsight versão 3.4 ou superior.</span><span class="sxs-lookup"><span data-stu-id="504ff-105">Linux is the only operating system used on HDInsight version 3.4 or greater.</span></span> <span data-ttu-id="504ff-106">Para obter mais informações, confira [baixa do HDInsight no Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span><span class="sxs-lookup"><span data-stu-id="504ff-106">For more information, see [HDInsight retirement on Windows](hdinsight-component-versioning.md#hdinsight-windows-retirement).</span></span>


## <a name="prerequisites"></a><span data-ttu-id="504ff-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="504ff-107">Prerequisites</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]

* <span data-ttu-id="504ff-108">**Uma assinatura do Azure**.</span><span class="sxs-lookup"><span data-stu-id="504ff-108">**An Azure subscription**.</span></span> <span data-ttu-id="504ff-109">Consulte [Obter avaliação gratuita do Azure](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="504ff-109">See [Get Azure free trial](https://azure.microsoft.com/documentation/videos/get-azure-free-trial-for-testing-hadoop-in-hdinsight/).</span></span>

* <span data-ttu-id="504ff-110">**CLI do Azure**.</span><span class="sxs-lookup"><span data-stu-id="504ff-110">**Azure CLI**.</span></span> <span data-ttu-id="504ff-111">As etapas neste documento foram testadas pela última vez com a versão 0.10.14 da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="504ff-111">The steps in this document were last tested with Azure CLI version 0.10.14.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="504ff-112">As etapas neste documento não funcionam com a CLI do Azure 2.0.</span><span class="sxs-lookup"><span data-stu-id="504ff-112">The steps in this document do not work with Azure CLI 2.0.</span></span> <span data-ttu-id="504ff-113">A CLI do Azure 2.0 não dá suporte à criação de um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="504ff-113">Azure CLI 2.0 does not support creating an HDInsight cluster.</span></span>

## <a name="log-in-to-your-azure-subscription"></a><span data-ttu-id="504ff-114">Entre na sua assinatura do Azure</span><span class="sxs-lookup"><span data-stu-id="504ff-114">Log in to your Azure subscription</span></span>

<span data-ttu-id="504ff-115">Siga as etapas documentadas em [Conectar a uma assinatura do Azure por meio da CLI do Azure (Interface de Linha de Comando do Azure)](../xplat-cli-connect.md) e conecte à sua assinatura usando o método de **logon** .</span><span class="sxs-lookup"><span data-stu-id="504ff-115">Follow the steps documented in [Connect to an Azure subscription from the Azure Command-Line Interface (Azure CLI)](../xplat-cli-connect.md) and connect to your subscription using the **login** method.</span></span>

## <a name="create-a-cluster"></a><span data-ttu-id="504ff-116">Criar um cluster</span><span class="sxs-lookup"><span data-stu-id="504ff-116">Create a cluster</span></span>

<span data-ttu-id="504ff-117">As etapas a seguir devem ser executadas de uma linha de comando, como o PowerShell ou o Bash.</span><span class="sxs-lookup"><span data-stu-id="504ff-117">The following steps should be performed from a command line, such as PowerShell or Bash.</span></span>

1. <span data-ttu-id="504ff-118">Use o seguinte comando para fazer logon em sua assinatura do Azure:</span><span class="sxs-lookup"><span data-stu-id="504ff-118">Use the following command to authenticate to your Azure subscription:</span></span>

        azure login

    <span data-ttu-id="504ff-119">Você receberá uma solicitação para fornecer seu nome e senha.</span><span class="sxs-lookup"><span data-stu-id="504ff-119">You are prompted to provide your name and password.</span></span> <span data-ttu-id="504ff-120">Se você tiver várias assinaturas do Azure, use `azure account set <subscriptionname>` para definir a assinatura que será usada pelos comandos da CLI do Azure.</span><span class="sxs-lookup"><span data-stu-id="504ff-120">If you have multiple Azure subscriptions, use `azure account set <subscriptionname>` to set the subscription that the Azure CLI commands use.</span></span>

2. <span data-ttu-id="504ff-121">Alterne para modo Gerenciador de Recursos do Azure usando o seguinte comando:</span><span class="sxs-lookup"><span data-stu-id="504ff-121">Switch to Azure Resource Manager mode using the following command:</span></span>

        azure config mode arm

3. <span data-ttu-id="504ff-122">Crie um grupos de recursos.</span><span class="sxs-lookup"><span data-stu-id="504ff-122">Create a resource group.</span></span> <span data-ttu-id="504ff-123">Esse grupo de recursos contém o cluster HDInsight e a conta de armazenamento associada.</span><span class="sxs-lookup"><span data-stu-id="504ff-123">This resource group contains the HDInsight cluster and associated storage account.</span></span>

        azure group create groupname location

    * <span data-ttu-id="504ff-124">Substitua `groupname` por um nome exclusivo para o grupo.</span><span class="sxs-lookup"><span data-stu-id="504ff-124">Replace `groupname` with a unique name for the group.</span></span>

    * <span data-ttu-id="504ff-125">Substitua `location` pela região geográfica na qual você deseja criar um grupo.</span><span class="sxs-lookup"><span data-stu-id="504ff-125">Replace `location` with the geographic region that you want to create the group in.</span></span>

       <span data-ttu-id="504ff-126">Para obter uma lista de locais válidos, use o comando `azure location list` e, então, utilize um dos locais da coluna `Name`.</span><span class="sxs-lookup"><span data-stu-id="504ff-126">For a list of valid locations, use the `azure location list` command, and then use one of the locations from the `Name` column.</span></span>

4. <span data-ttu-id="504ff-127">Criar uma conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="504ff-127">Create a storage account.</span></span> <span data-ttu-id="504ff-128">Essa conta de armazenamento é usada como o armazenamento padrão do cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="504ff-128">This storage account is used as the default storage for the HDInsight cluster.</span></span>

        azure storage account create -g groupname --sku-name RAGRS -l location --kind Storage storagename

    * <span data-ttu-id="504ff-129">Substitua `groupname` pelo nome do grupo criado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="504ff-129">Replace `groupname` with the name of the group created in the previous step.</span></span>

    * <span data-ttu-id="504ff-130">Substitua `location` pelo mesmo local usado na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="504ff-130">Replace `location` with the same location used in the previous step.</span></span>

    * <span data-ttu-id="504ff-131">Substitua `storagename` por um nome exclusivo para a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="504ff-131">Replace `storagename` with a unique name for the storage account.</span></span>

        > [!NOTE]
        > <span data-ttu-id="504ff-132">Para saber mais sobre os parâmetros usados nesse comando, use `azure storage account create -h` para exibir a ajuda deste comando.</span><span class="sxs-lookup"><span data-stu-id="504ff-132">For more information on the parameters used in this command, use `azure storage account create -h` to view help for this command.</span></span>

5. <span data-ttu-id="504ff-133">Recupere a chave usada para acessar a conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="504ff-133">Retrieve the key used to access the storage account.</span></span>

        azure storage account keys list -g groupname storagename

    * <span data-ttu-id="504ff-134">Substitua `groupname` pelo nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="504ff-134">Replace `groupname` with the resource group name.</span></span>
    * <span data-ttu-id="504ff-135">Substitua `storagename` pelo nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="504ff-135">Replace `storagename` with the name of the storage account.</span></span>

     <span data-ttu-id="504ff-136">Nos dados retornados, salve o valor `key` para `key1`.</span><span class="sxs-lookup"><span data-stu-id="504ff-136">In the data that is returned, save the `key` value for `key1`.</span></span>

6. <span data-ttu-id="504ff-137">Crie um cluster HDInsight.</span><span class="sxs-lookup"><span data-stu-id="504ff-137">Create an HDInsight cluster.</span></span>

        azure hdinsight cluster create -g groupname -l location -y Linux --clusterType Hadoop --defaultStorageAccountName storagename.blob.core.windows.net --defaultStorageAccountKey storagekey --defaultStorageContainer clustername --workerNodeCount 3 --userName admin --password httppassword --sshUserName sshuser --sshPassword sshuserpassword clustername

    * <span data-ttu-id="504ff-138">Substitua `groupname` pelo nome do grupo de recursos.</span><span class="sxs-lookup"><span data-stu-id="504ff-138">Replace `groupname` with the resource group name.</span></span>

    * <span data-ttu-id="504ff-139">Substitua `Hadoop` pelo tipo de cluster que você deseja criar.</span><span class="sxs-lookup"><span data-stu-id="504ff-139">Replace `Hadoop` with the cluster type that you wish to create.</span></span> <span data-ttu-id="504ff-140">Por exemplo, `Hadoop`, `HBase`, `Kafka`, `Spark` ou `Storm`.</span><span class="sxs-lookup"><span data-stu-id="504ff-140">For example, `Hadoop`, `HBase`, `Kafka`, `Spark`, or `Storm`.</span></span>

     > [!IMPORTANT]
     > <span data-ttu-id="504ff-141">Clusters HDInsight são fornecidos em uma variedade de tipos que correspondem à carga de trabalho ou à tecnologia para a qual o cluster está ajustado.</span><span class="sxs-lookup"><span data-stu-id="504ff-141">HDInsight clusters come in various types, which correspond to the workload or technology that the cluster is tuned for.</span></span> <span data-ttu-id="504ff-142">Não há nenhum método com suporte para criar um cluster que combina vários tipos, como o Storm e HBase em um cluster.</span><span class="sxs-lookup"><span data-stu-id="504ff-142">There is no supported method to create a cluster that combines multiple types, such as Storm and HBase on one cluster.</span></span>

    * <span data-ttu-id="504ff-143">Substitua `location` pelo mesmo local usado nas etapas anteriores.</span><span class="sxs-lookup"><span data-stu-id="504ff-143">Replace `location` with the same location used in previous steps.</span></span>

    * <span data-ttu-id="504ff-144">Substitua `storagename` pelo nome da conta de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="504ff-144">Replace `storagename` with the storage account name.</span></span>

    * <span data-ttu-id="504ff-145">Substitua `storagekey` pela chave obtida na etapa anterior.</span><span class="sxs-lookup"><span data-stu-id="504ff-145">Replace `storagekey` with the key obtained in the previous step.</span></span>

    * <span data-ttu-id="504ff-146">Como parâmetro `--defaultStorageContainer` , use o mesmo nome que você está usando para o cluster.</span><span class="sxs-lookup"><span data-stu-id="504ff-146">For the `--defaultStorageContainer` parameter, use the same name as you are using for the cluster.</span></span>

    * <span data-ttu-id="504ff-147">Substitua `admin` e `httppassword` pelo nome e pela senha que você deseja usar quando acessar o cluster por meio de HTTPS.</span><span class="sxs-lookup"><span data-stu-id="504ff-147">Replace `admin` and `httppassword` with the name and password you wish to use when accessing the cluster through HTTPS.</span></span>

    * <span data-ttu-id="504ff-148">Substitua `sshuser` e `sshuserpassword` pelo nome de usuário e senha que você deseja usar quando acessar o cluster usando SSH</span><span class="sxs-lookup"><span data-stu-id="504ff-148">Replace `sshuser` and `sshuserpassword` with the username and password you wish to use when accessing the cluster using SSH</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="504ff-149">Este exemplo cria um cluster com duas anotações de trabalho.</span><span class="sxs-lookup"><span data-stu-id="504ff-149">This example creates a cluster with two worker notes.</span></span> <span data-ttu-id="504ff-150">Você também pode alterar o número de nós de trabalho após a criação do cluster realizando operações de colocação em escala.</span><span class="sxs-lookup"><span data-stu-id="504ff-150">You can also change the number of worker nodes after cluster creation by performing scaling operations.</span></span> <span data-ttu-id="504ff-151">Se você planeja usar mais de 32 nós de trabalho, será necessário selecionar um tamanho de nó de cabeçalho com pelo menos oito núcleos e 14 GB de RAM.</span><span class="sxs-lookup"><span data-stu-id="504ff-151">If you plan on using more than 32 worker nodes, then you must select a head node size with at least 8 cores and 14-GB RAM.</span></span> <span data-ttu-id="504ff-152">Você pode definir o tamanho do nó principal usando o parâmetro `--headNodeSize` durante a criação do cluster.</span><span class="sxs-lookup"><span data-stu-id="504ff-152">You can set the head node size by using the `--headNodeSize` parameter during cluster creation.</span></span>
    >
    > <span data-ttu-id="504ff-153">Para saber mais sobre tamanhos de nós e custos associados, consulte [Preços do HDInsight](https://azure.microsoft.com/pricing/details/hdinsight/).</span><span class="sxs-lookup"><span data-stu-id="504ff-153">For more information on node sizes and associated costs, see [HDInsight pricing](https://azure.microsoft.com/pricing/details/hdinsight/).</span></span>

    <span data-ttu-id="504ff-154">Pode levar vários minutos para que o processo de criação de cluster seja concluído.</span><span class="sxs-lookup"><span data-stu-id="504ff-154">It may take several minutes for the cluster creation process to finish.</span></span> <span data-ttu-id="504ff-155">Geralmente, cerca de 15 minutos.</span><span class="sxs-lookup"><span data-stu-id="504ff-155">Usually around 15.</span></span>

## <a name="troubleshoot"></a><span data-ttu-id="504ff-156">Solucionar problemas</span><span class="sxs-lookup"><span data-stu-id="504ff-156">Troubleshoot</span></span>

<span data-ttu-id="504ff-157">Se você tiver problemas com a criação de clusters HDInsight, confira os [requisitos de controle de acesso](hdinsight-administer-use-portal-linux.md#create-clusters).</span><span class="sxs-lookup"><span data-stu-id="504ff-157">If you run into issues with creating HDInsight clusters, see [access control requirements](hdinsight-administer-use-portal-linux.md#create-clusters).</span></span>

## <a name="next-steps"></a><span data-ttu-id="504ff-158">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="504ff-158">Next steps</span></span>

<span data-ttu-id="504ff-159">Agora que você criou com êxito um cluster HDInsight usando a CLI do Azure, use o seguinte para aprender a trabalhar com o seu cluster:</span><span class="sxs-lookup"><span data-stu-id="504ff-159">Now that you have successfully created an HDInsight cluster using the Azure CLI, use the following to learn how to work with your cluster:</span></span>

### <a name="hadoop-clusters"></a><span data-ttu-id="504ff-160">Clusters do Hadoop</span><span class="sxs-lookup"><span data-stu-id="504ff-160">Hadoop clusters</span></span>

* [<span data-ttu-id="504ff-161">Usar o Hive com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="504ff-161">Use Hive with HDInsight</span></span>](hdinsight-use-hive.md)
* [<span data-ttu-id="504ff-162">Usar o Pig com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="504ff-162">Use Pig with HDInsight</span></span>](hdinsight-use-pig.md)
* [<span data-ttu-id="504ff-163">Usar o MapReduce com o HDInsight</span><span class="sxs-lookup"><span data-stu-id="504ff-163">Use MapReduce with HDInsight</span></span>](hdinsight-use-mapreduce.md)

### <a name="hbase-clusters"></a><span data-ttu-id="504ff-164">Clusters do HBase</span><span class="sxs-lookup"><span data-stu-id="504ff-164">HBase clusters</span></span>

* [<span data-ttu-id="504ff-165">Introdução ao HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="504ff-165">Get started with HBase on HDInsight</span></span>](hdinsight-hbase-tutorial-get-started-linux.md)
* [<span data-ttu-id="504ff-166">Desenvolvimento de aplicativos Java para HBase no HDInsight</span><span class="sxs-lookup"><span data-stu-id="504ff-166">Develop Java applications for HBase on HDInsight</span></span>](hdinsight-hbase-build-java-maven-linux.md)

### <a name="storm-clusters"></a><span data-ttu-id="504ff-167">Clusters Storm</span><span class="sxs-lookup"><span data-stu-id="504ff-167">Storm clusters</span></span>

* [<span data-ttu-id="504ff-168">Desenvolver topologias Java para Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="504ff-168">Develop Java topologies for Storm on HDInsight</span></span>](hdinsight-storm-develop-java-topology.md)
* [<span data-ttu-id="504ff-169">Usar componentes de Python no Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="504ff-169">Use Python components in Storm on HDInsight</span></span>](hdinsight-storm-develop-python-topology.md)
* [<span data-ttu-id="504ff-170">Implantar e monitorar topologias com o Storm no HDInsight</span><span class="sxs-lookup"><span data-stu-id="504ff-170">Deploy and monitor topologies with Storm on HDInsight</span></span>](hdinsight-storm-deploy-monitor-topology-linux.md)
