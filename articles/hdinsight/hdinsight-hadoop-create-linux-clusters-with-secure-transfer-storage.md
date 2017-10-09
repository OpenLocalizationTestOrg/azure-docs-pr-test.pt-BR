---
title: "aaaCreate Hadoop de cluster com contas de armazenamento seguro de transferência no Azure HDInsight | Microsoft Docs"
description: "Saiba como clusters de HDInsight toocreate com transferência segura habilitado contas de armazenamento do Azure."
keywords: "guia de introdução do hadoop, hadoop linux, início rápido do hadoop, transferência segura, conta de armazenamento do azure"
services: hdinsight
documentationcenter: 
author: mumian
manager: jhubbard
editor: cgronlun
tags: azure-portal
ms.service: hdinsight
ms.custom: hdinsightactive
ms.devlang: na
ms.topic: hero-article
ms.tgt_pltfrm: na
ms.workload: big-data
ms.date: 08/21/2017
ms.author: jgao
ms.openlocfilehash: 0acb8814ad0d5d5b5652d930b2e3da90f9d7978d
ms.sourcegitcommit: 523283cc1b3c37c428e77850964dc1c33742c5f0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/06/2017
---
# <a name="create-hadoop-cluster-with-secure-transfer-storage-accounts-in-azure-hdinsight"></a><span data-ttu-id="9e16f-104">Criar um cluster Hadoop com contas de armazenamento para transferência segura no Azure HDInsight</span><span class="sxs-lookup"><span data-stu-id="9e16f-104">Create Hadoop cluster with secure transfer storage accounts in Azure HDInsight</span></span>

<span data-ttu-id="9e16f-105">Olá [necessária de transferência segura](../storage/common/storage-require-secure-transfer.md) recurso aprimora a segurança de saudação da sua conta de armazenamento do Azure através da aplicação de todas as contas de tooyour solicitações por meio de uma conexão segura.</span><span class="sxs-lookup"><span data-stu-id="9e16f-105">hello [Secure transfer required](../storage/common/storage-require-secure-transfer.md) feature enhances hello security of your Azure Storage account by enforcing all requests tooyour account through a secure connection.</span></span> <span data-ttu-id="9e16f-106">Esse esquema de recurso e hello wasbs só são suportados pela versão de cluster do HDInsight 3.6 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="9e16f-106">This feature and hello wasbs scheme are only supported by HDInsight cluster version 3.6 or newer.</span></span> 

## <a name="prerequisites"></a><span data-ttu-id="9e16f-107">Pré-requisitos</span><span class="sxs-lookup"><span data-stu-id="9e16f-107">Prerequisites</span></span>
<span data-ttu-id="9e16f-108">Antes de começar este tutorial, você deverá ter o seguinte:</span><span class="sxs-lookup"><span data-stu-id="9e16f-108">Before you begin this tutorial, you must have:</span></span>

* <span data-ttu-id="9e16f-109">**Assinatura do Azure**: toocreate uma conta de avaliação de um mês livre, procurar muito[azure.microsoft.com/free](https://azure.microsoft.com/free).</span><span class="sxs-lookup"><span data-stu-id="9e16f-109">**Azure subscription**: toocreate a free one-month trial account, browse too[azure.microsoft.com/free](https://azure.microsoft.com/free).</span></span>
* <span data-ttu-id="9e16f-110">**Uma conta de Armazenamento do Azure com transferência segura habilitada**.</span><span class="sxs-lookup"><span data-stu-id="9e16f-110">**An Azure Storage account with secure transfer enabled**.</span></span> <span data-ttu-id="9e16f-111">Para obter instruções hello, consulte [criar uma conta de armazenamento](../storage/common/storage-create-storage-account.md#create-a-storage-account) e [requerem a transferência segura](../storage/common/storage-require-secure-transfer.md).</span><span class="sxs-lookup"><span data-stu-id="9e16f-111">For hello instructions, see [Create a storage account](../storage/common/storage-create-storage-account.md#create-a-storage-account) and [Require secure transfer](../storage/common/storage-require-secure-transfer.md).</span></span>
* <span data-ttu-id="9e16f-112">**Um contêiner de Blob na conta de armazenamento Olá**.</span><span class="sxs-lookup"><span data-stu-id="9e16f-112">**A Blob container on hello storage account**.</span></span> 
## <a name="create-cluster"></a><span data-ttu-id="9e16f-113">Criar cluster</span><span class="sxs-lookup"><span data-stu-id="9e16f-113">Create cluster</span></span>

[!INCLUDE [delete-cluster-warning](../../includes/hdinsight-delete-cluster-warning.md)]


<span data-ttu-id="9e16f-114">Nesta seção, você criará um cluster Hadoop no HDInsight usando um [modelo do Azure Resource Manager](../azure-resource-manager/resource-group-template-deploy.md).</span><span class="sxs-lookup"><span data-stu-id="9e16f-114">In this section, you create a Hadoop cluster in HDInsight using an [Azure Resource Manager template](../azure-resource-manager/resource-group-template-deploy.md).</span></span> <span data-ttu-id="9e16f-115">Olá modelo está localizado em [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span><span class="sxs-lookup"><span data-stu-id="9e16f-115">hello template is located in [Gibhub](https://azure.microsoft.com/resources/templates/101-hdinsight-linux-with-existing-default-storage-account/).</span></span> <span data-ttu-id="9e16f-116">Não é necessário ter experiência com o modelo do Resource Manager para seguir este tutorial.</span><span class="sxs-lookup"><span data-stu-id="9e16f-116">Resource Manager template experience is not required for following this tutorial.</span></span> <span data-ttu-id="9e16f-117">Para outros métodos de criação de cluster e Noções básicas sobre propriedades de saudação usadas neste tutorial, consulte [HDInsight criar clusters](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9e16f-117">For other cluster creation methods and understanding hello properties used in this tutorial, see [Create HDInsight clusters](hdinsight-hadoop-provision-linux-clusters.md).</span></span>

1. <span data-ttu-id="9e16f-118">Clique em Olá toosign de imagem no tooAzure e modelo do Gerenciador de recursos de saudação abrir no portal do Azure de saudação a seguir.</span><span class="sxs-lookup"><span data-stu-id="9e16f-118">Click hello following image toosign in tooAzure and open hello Resource Manager template in hello Azure portal.</span></span> 
   
    <a href="https://portal.azure.com/#create/Microsoft.Template/uri/https%3A%2F%2Fraw.githubusercontent.com%2FAzure%2Fazure-quickstart-templates%2Fmaster%2F101-hdinsight-linux-with-existing-default-storage-account%2Fazuredeploy.json" target="_blank"><img src="./media/hdinsight-hadoop-linux-tutorial-get-started/deploy-to-azure.png" alt="Deploy tooAzure"></a>

2. <span data-ttu-id="9e16f-119">Execute o cluster de Olá Olá instruções toocreate com hello especificações a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e16f-119">Follow hello instructions toocreate hello cluster with hello following specifications:</span></span> 

    - <span data-ttu-id="9e16f-120">Especifique o HDInsight versão 3.6.</span><span class="sxs-lookup"><span data-stu-id="9e16f-120">Specify HDInsight version 3.6.</span></span>  <span data-ttu-id="9e16f-121">versão do padrão de saudação é 3.5.</span><span class="sxs-lookup"><span data-stu-id="9e16f-121">hello default version is 3.5.</span></span> <span data-ttu-id="9e16f-122">É necessário ter a versão 3.6 ou mais recente.</span><span class="sxs-lookup"><span data-stu-id="9e16f-122">Version 3.6 or newer is required.</span></span>
    - <span data-ttu-id="9e16f-123">Especifique uma conta de armazenamento com transferência segura habilitada.</span><span class="sxs-lookup"><span data-stu-id="9e16f-123">Specify a secure transfer enabled storage account.</span></span>
    - <span data-ttu-id="9e16f-124">Use o nome curto para a conta de armazenamento hello.</span><span class="sxs-lookup"><span data-stu-id="9e16f-124">Use short name for hello storage account.</span></span>
    - <span data-ttu-id="9e16f-125">Conta de armazenamento hello e o contêiner de blob Olá devem ser criados com antecedência.</span><span class="sxs-lookup"><span data-stu-id="9e16f-125">Both hello storage account and hello blob container must be created beforehand.</span></span> 

    <span data-ttu-id="9e16f-126">Para obter instruções hello, consulte [criar cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span><span class="sxs-lookup"><span data-stu-id="9e16f-126">For hello instructions, see [Create cluster](./hdinsight-hadoop-linux-tutorial-get-started.md#create-cluster).</span></span> 

<span data-ttu-id="9e16f-127">Se você usar o script ação tooprovide seus próprios arquivos de configuração, você deve usar wasbs no hello configurações a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e16f-127">If you use script action tooprovide your own configuration files, you must use wasbs in hello following settings:</span></span>

- <span data-ttu-id="9e16f-128">fs.defaultFS (site principal)</span><span class="sxs-lookup"><span data-stu-id="9e16f-128">fs.defaultFS (core-site)</span></span>
- <span data-ttu-id="9e16f-129">spark.eventLog.dir</span><span class="sxs-lookup"><span data-stu-id="9e16f-129">spark.eventLog.dir</span></span> 
- <span data-ttu-id="9e16f-130">spark.history.fs.logDirectory</span><span class="sxs-lookup"><span data-stu-id="9e16f-130">spark.history.fs.logDirectory</span></span>

## <a name="add-additional-storage-accounts"></a><span data-ttu-id="9e16f-131">Adicionar outras contas de armazenamento</span><span class="sxs-lookup"><span data-stu-id="9e16f-131">Add additional storage accounts</span></span>

<span data-ttu-id="9e16f-132">Há várias contas de armazenamento opções tooadd adicionais transferência segura habilitada:</span><span class="sxs-lookup"><span data-stu-id="9e16f-132">There are several options tooadd additional secure transfer enabled storage accounts:</span></span>

- <span data-ttu-id="9e16f-133">Modifica modelo de Gerenciador de recursos do Azure Olá na última seção do hello.</span><span class="sxs-lookup"><span data-stu-id="9e16f-133">Modify hello Azure Resource Manager template in hello last section.</span></span>
- <span data-ttu-id="9e16f-134">Criar um cluster usando Olá [portal do Azure](https://portal.azure.com) e especifique a conta de armazenamento vinculada.</span><span class="sxs-lookup"><span data-stu-id="9e16f-134">Create a cluster using hello [Azure portal](https://portal.azure.com) and specify linked storage account.</span></span>
- <span data-ttu-id="9e16f-135">Use script ação tooadd adicional transferência segura habilitada armazenamento contas tooan existente cluster do HDInsight.</span><span class="sxs-lookup"><span data-stu-id="9e16f-135">Use script action tooadd additional secure transfer enabled storage accounts tooan existing HDInsight cluster.</span></span>  <span data-ttu-id="9e16f-136">Para obter mais informações, consulte [adicionar tooHDInsight de contas de armazenamento adicional](hdinsight-hadoop-add-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9e16f-136">For more information, see [Add additional storage accounts tooHDInsight](hdinsight-hadoop-add-storage.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="9e16f-137">Próximas etapas</span><span class="sxs-lookup"><span data-stu-id="9e16f-137">Next steps</span></span>
<span data-ttu-id="9e16f-138">Neste tutorial, você aprendeu como toocreate um cluster HDInsight e habilitar seguro transferir toohello contas de armazenamento.</span><span class="sxs-lookup"><span data-stu-id="9e16f-138">In this tutorial, you have learned how toocreate an HDInsight cluster, and enable secure transfer toohello storage accounts.</span></span>

<span data-ttu-id="9e16f-139">toolearn mais sobre a análise de dados com o HDInsight, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e16f-139">toolearn more about analyzing data with HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="9e16f-140">toolearn mais sobre como usar o Hive com HDInsight, incluindo como tooperform Hive as consultas do Visual Studio, consulte [uso de Hive do HDInsight][hdinsight-use-hive].</span><span class="sxs-lookup"><span data-stu-id="9e16f-140">toolearn more about using Hive with HDInsight, including how tooperform Hive queries from Visual Studio, see [Use Hive with HDInsight][hdinsight-use-hive].</span></span>
* <span data-ttu-id="9e16f-141">toolearn sobre Pig, uma linguagem usada tootransform dados, consulte [usar o Pig com HDInsight][hdinsight-use-pig].</span><span class="sxs-lookup"><span data-stu-id="9e16f-141">toolearn about Pig, a language used tootransform data, see [Use Pig with HDInsight][hdinsight-use-pig].</span></span>
* <span data-ttu-id="9e16f-142">toolearn sobre MapReduce, programas de toowrite uma maneira que processam dados no Hadoop, consulte [Use MapReduce com HDInsight][hdinsight-use-mapreduce].</span><span class="sxs-lookup"><span data-stu-id="9e16f-142">toolearn about MapReduce, a way toowrite programs that process data on Hadoop, see [Use MapReduce with HDInsight][hdinsight-use-mapreduce].</span></span>
* <span data-ttu-id="9e16f-143">toolearn sobre como usar ferramentas do HDInsight Olá para dados do Visual Studio tooanalyze no HDInsight, consulte [começar a usar ferramentas Hadoop do Visual Studio para HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span><span class="sxs-lookup"><span data-stu-id="9e16f-143">toolearn about using hello HDInsight Tools for Visual Studio tooanalyze data on HDInsight, see [Get started using Visual Studio Hadoop tools for HDInsight](hdinsight-hadoop-visual-studio-tools-get-started.md).</span></span>

<span data-ttu-id="9e16f-144">mais informações sobre como HDInsight armazena dados de toolearn ou como dados tooget em HDInsight, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e16f-144">toolearn more about how HDInsight stores data or how tooget data into HDInsight, see hello following articles:</span></span>

* <span data-ttu-id="9e16f-145">Para saber mais sobre como o HDInsight usa o Armazenamento do Azure, veja [Usar Armazenamento do Azure com o HDInsight](hdinsight-hadoop-use-blob-storage.md).</span><span class="sxs-lookup"><span data-stu-id="9e16f-145">For information on how HDInsight uses Azure Storage, see [Use Azure Storage with HDInsight](hdinsight-hadoop-use-blob-storage.md).</span></span>
* <span data-ttu-id="9e16f-146">Para obter informações sobre como tooupload tooHDInsight de dados, consulte [carregar dados tooHDInsight][hdinsight-upload-data].</span><span class="sxs-lookup"><span data-stu-id="9e16f-146">For information on how tooupload data tooHDInsight, see [Upload data tooHDInsight][hdinsight-upload-data].</span></span>

<span data-ttu-id="9e16f-147">toolearn mais sobre como criar ou gerenciar um cluster HDInsight, consulte Olá artigos a seguir:</span><span class="sxs-lookup"><span data-stu-id="9e16f-147">toolearn more about creating or managing an HDInsight cluster, see hello following articles:</span></span>

* <span data-ttu-id="9e16f-148">toolearn sobre como gerenciar seu cluster HDInsight baseados em Linux, consulte [HDInsight gerenciar clusters usando o Ambari](hdinsight-hadoop-manage-ambari.md).</span><span class="sxs-lookup"><span data-stu-id="9e16f-148">toolearn about managing your Linux-based HDInsight cluster, see [Manage HDInsight clusters using Ambari](hdinsight-hadoop-manage-ambari.md).</span></span>
* <span data-ttu-id="9e16f-149">toolearn mais sobre opções de saudação, você pode selecionar ao criar um cluster HDInsight, consulte [criando HDInsight no Linux usando opções personalizadas](hdinsight-hadoop-provision-linux-clusters.md).</span><span class="sxs-lookup"><span data-stu-id="9e16f-149">toolearn more about hello options you can select when creating an HDInsight cluster, see [Creating HDInsight on Linux using custom options](hdinsight-hadoop-provision-linux-clusters.md).</span></span>
* <span data-ttu-id="9e16f-150">Se você estiver familiarizado com Linux e Hadoop, mas desejar tooknow obter as informações específicas sobre o Hadoop Olá HDInsight, consulte [trabalhando com HDInsight no Linux](hdinsight-hadoop-linux-information.md).</span><span class="sxs-lookup"><span data-stu-id="9e16f-150">If you are familiar with Linux, and Hadoop, but want tooknow specifics about Hadoop on hello HDInsight, see [Working with HDInsight on Linux](hdinsight-hadoop-linux-information.md).</span></span> <span data-ttu-id="9e16f-151">Este artigo oferece informações como:</span><span class="sxs-lookup"><span data-stu-id="9e16f-151">This article provides information such as:</span></span>
  
  * <span data-ttu-id="9e16f-152">URLs para serviços hospedados no cluster hello, como Ambari e WebHCat</span><span class="sxs-lookup"><span data-stu-id="9e16f-152">URLs for services hosted on hello cluster, such as Ambari and WebHCat</span></span>
  * <span data-ttu-id="9e16f-153">local de saudação de arquivos Hadoop e exemplos no sistema de arquivos local Olá</span><span class="sxs-lookup"><span data-stu-id="9e16f-153">hello location of Hadoop files and examples on hello local file system</span></span>
  * <span data-ttu-id="9e16f-154">uso de saudação do Azure Storage (WASB) em vez de HDFS como armazenamento de dados padrão de saudação</span><span class="sxs-lookup"><span data-stu-id="9e16f-154">hello use of Azure Storage (WASB) instead of HDFS as hello default data store</span></span>

[1]: ../HDInsight/hdinsight-hadoop-visual-studio-tools-get-started.md

[hdinsight-provision]: hdinsight-provision-linux-clusters.md
[hdinsight-upload-data]: hdinsight-upload-data.md
[hdinsight-use-mapreduce]: hdinsight-use-mapreduce.md
[hdinsight-use-hive]: hdinsight-use-hive.md
[hdinsight-use-pig]: hdinsight-use-pig.md


